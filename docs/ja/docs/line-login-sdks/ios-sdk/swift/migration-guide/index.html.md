# SDKをアップグレードする

## 最新のSDKにアップグレードする 

LINE SDK for iOS Swiftの最初のバージョンは5.0.0です。このバージョンは[以前のObjective-Cで書かれたSDK](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/deprecated/objective-c-v41/overview/)とは互換性がありません。LINE SDK for iOS Swiftにアップグレードする場合は、コードの一部を変更する必要があります。

<!-- note start -->

**注意**

新しいLINE SDK for iOS Swiftは、Swiftのプロジェクトで使用する前提で設計されています。ただし、新しいSDKはObjective-Cのコードと共に使用できます。SDKをObjective-Cのコードと共に使用する方法については、「[Objective-CのコードでSDKを使用する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/using-objc/)」を参照してください。

<!-- note end -->

SDKをアップグレードするには、プロジェクトの言語を問わず以前のSDKに関連するすべてのコードを削除し、「[プロジェクトを設定する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/setting-up-project/)」の手順に従ってクリーンインストールを実行することをお勧めします。 ただし、現在の実装に基づいて変更する場合の一般的な手順は以下のとおりです。

1. コードベースから以前の`LineSDK.framework`ファイルを削除する。
    - CocoaPodsやCarthageなどのパッケージマネージャーを使用した場合は、パッケージ定義ファイル（PodfileやCartfile）から「LineSDK」のエントリを削除します。それからクリーンインストールを実行して、`LineSDK.framework`ファイルへの参照をプロジェクトから削除します。
    - バイナリファイルをダウンロードして使った場合は、プロジェクトからそのファイルを削除します。

1. `Info.plist`ファイルをクリーンアップする。`LineSDKConfig`エントリは使用されないため、安全に削除できます。

1. LINE SDK for iOS Swiftをインストールする。詳しい手順については、「[プロジェクトを設定する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/setting-up-project/)」を参照してください。

1. チャネルIDとコールバックの制御処理を`AppDelegate`ファイルに設定する。

    アプリの起動直後に、以下のように`LoginManager.setup`メソッドを呼び出します。

    ```swift
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        // Add this to your "didFinishLaunching" delegate method.
        LoginManager.shared.setup(channelID: "YOUR_CHANNEL_ID", universalLinkURL: nil)

        return true
    }
    ```

    URLを開く制御を、以下のように更新します。

    ```swift
    func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {
        return LoginManager.shared.application(app, open: url, options: options)
    }
    ```

## コードを更新して最新のSDKを使用する 

上のセクションまでの作業が終わっていれば、コードの他の部分を更新して最新のSDKを使用する準備ができています。以下のセクションでは、一般的な例についていくつか説明します。

ここでは、SDKのすべての機能は説明しません。ただし、LINE SDKの対応するタイプは、同様の規則に従っているため簡単に見つけられるはずです。コードを更新し、最新のLINE SDKを使ってプロジェクトをコンパイルしてください。

最新のLINE SDK for iOS Swiftに対応するサンプルアプリを提供しています。SDKの[オープンソースリポジトリ](https://github.com/line/line-sdk-ios-swift)にアクセスして、基本的な組み込み方法と使い方を確認してください。

<!-- note start -->

**LINEを介してユーザーをアプリにログインさせる**

**LINE SDK 4.xで発行されるアクセストークンは、バージョン5以降ではサポートされません**。 LINE SDKをアップグレードする場合は、ユーザーが再ログインするまで、アプリからLINEプラットフォームにアクセスできません。

<!-- note end -->

#### 以前 

```swift
// First set the delegate to the current object
LineSDKLogin.sharedInstance().delegate = self
LineSDKLogin.sharedInstance().start()

// MARK: LineSDKLoginDelegate

func didLogin(_ login: LineSDKLogin, credential: LineSDKCredential?, profile: LineSDKProfile?, error: Error?) {

    if let error = error {
        print("LINE Login Failed with Error: \(error.localizedDescription) ")
        return
    }

    print("LINE Login Succeeded")
}
```

#### 現在 

```swift
LoginManager.shared.login(permissions: [.profile]) {
    result in
    switch result {
    case .success(let loginResult):
        print("User name: \(loginResult.userProfile?.displayName ?? "nil")")
    case .failure(let error):
        print("Error: \(error)")
    }
}
```

### ユーザープロフィールを取得する 

#### 以前 

```swift
var apiClient: LineSDKAPI
apiClient = LineSDKAPI(configuration: LineSDKConfiguration.defaultConfig())

apiClient.getProfile(queue: .main) {
    (profile, error) in

    if let error = error {
        print("Error getting profile \(error.localizedDescription)")
    }

    print(profile?.displayName ?? "none")
    print(profile?.pictureURL ?? "none")
    print(profile?.statusMessage ?? "none")
    print(profile?.userID ?? "none")
}
```

#### 現在 

```swift
API.getProfile { result in
    switch result {
    case .success(let profile):
        print("User name: \(profile.displayName)")
    case .failure(let error):
        print("Error: \(error)")
    }
}
```

### ユーザーをログアウトする 

#### 以前 

```swift
var apiClient: LineSDKAPI
apiClient = LineSDKAPI(configuration: LineSDKConfiguration.defaultConfig())

apiClient.logout(queue: .main) {
    (success, error) in

    if success {
        print("Logout Succeeded")
    }
    else {
        print("Logout Failed \(error?.localizedDescription as String?)")
    }
}
```

#### 現在 

```swift
LoginManager.shared.logout { result in
    switch result {
    case .success:            print("Logout Succeeded")
    case .failure(let error): print("Logout Failed: \(error)")
    }
}
```

### 現在のアクセストークンを取得する 

#### 以前 

```swift
var apiClient: LineSDKAPI
apiClient = LineSDKAPI(configuration: LineSDKConfiguration.defaultConfig())

let myToken = apiClient.currentAccessToken()
```

#### 現在 

```swift
let token = AccessTokenStore.shared.current?.value
```

### アクセストークンを検証する 

#### 以前 

```swift
var apiClient: LineSDKAPI
apiClient = LineSDKAPI(configuration: LineSDKConfiguration.defaultConfig())

apiClient.verifyToken(queue: .main) {
    (result, error) in

    if let error = error {
        print("Token is Invalid: \(error.localizedDescription)")
        return
    }

    guard let result = result, let permissions = result.permissions else {
        print("Response result is null")
        return
    }
    print("Token is Valid")
}
```

#### 現在 

```swift
API.Auth.verifyAccessToken { result in
    switch result {
    case .success: print("Token is valid.")
    case .failure(let error): print("Error: \(error)")
    }
}
```
