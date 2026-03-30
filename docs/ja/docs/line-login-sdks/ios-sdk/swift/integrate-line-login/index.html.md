# iOSアプリにLINEログインを組み込む

[SDKをインストール](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/setting-up-project/)してプロジェクトを設定したら、LINEログインを使ったユーザーエクスペリエンスの向上に取りかかることができます。

## LineSDKフレームワークとチャネルIDを設定する 

ログインアクションで生成される結果を処理するため、LINE SDK for iOS Swiftを`AppDelegate.swift`ファイルに設定します。

### 1. LineSDKフレームワークをインポートする 

`AppDelegate.swift`ファイルの冒頭で、`LineSDK`フレームワークを以下のようにインポートします。

```swift
// AppDelegate.swift
import LineSDK
```

アプリ内の他のファイルでSDKを使用する場合は、各ファイルに`LineSDK`フレームワークをインポートしてください。

### 2. `LoginManager.setup`メソッドを呼び出す 

アプリの起動直後に、以下のように`LoginManager.setup`メソッドを呼び出します。

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    // Add this to your "didFinishLaunching" delegate method.
    LoginManager.shared.setup(channelID: "YOUR_CHANNEL_ID", universalLinkURL: nil)

    return true
}
```

<!-- note start -->

**注意**

LINE SDK for iOS Swiftの他のプロパティにアクセスしたり、他のメソッドを呼び出したりする**前に**、`setup`メソッドを呼び出してください。

<!-- note end -->

#### ユニバーサルリンクを使用する 

LINE Developersコンソールでユニバーサルリンクを設定した場合は、`universalLinkURL`パラメータを指定して`setup`メソッドを呼び出します。LINEによりユニバーサルリンクを使ってアプリが起動されるため、ログイン処理のセキュリティが高まります。

ユニバーサルリンクを使ったログイン処理の制御について詳しくは、「[ユニバーサルリンクを利用する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/universal-links-support/)」を参照してください。

### 3. アプリの起動を制御する 

LINEプラットフォームから返されたログイン結果を制御するには、取得したURLを`LoginManager`の`application(_:open:options:)`メソッドに渡します。プロジェクトがマルチウィンドウ（[iOS13で導入された機能](https://developer.apple.com/documentation/uikit/scenes)）をサポートするかどうかで、アプリデリゲートクラスまたはシーンデリゲートクラスを変更する必要があります。

#### アプリデリゲートを変更する 

iOS 12以前では、`UIApplicationDelegate`オブジェクトを呼び出して、URLを開きます。したがって、アプリデリゲートクラスの`application(_:open:options:)`デリゲートメソッドに、次の行を追加します。

```swift
// AppDelegate.swift
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {
    return LoginManager.shared.application(app, open: url)
}
```

#### シーンデリゲートを変更する 

iOS 13以降では、`UISceneDelegate`オブジェクトを呼び出して、URLを開きます。

Xcode 11以降でプロジェクトを作成した場合は、デフォルトでは、プロジェクトには`SceneDelegate.swift`ファイルが含まれ、`Info.plist`ファイルには`UIApplicationSceneManifest`エントリーが含まれます。

プロジェクトがマルチウィンドウをサポートする場合は、使用するシーンデリゲートクラスに、次の行を追加します。

```swift
// SceneDelegate.swift
func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
    _ = LoginManager.shared.application(.shared, open: URLContexts.first?.url)
}
```

<!-- note start -->

**注意**

プロジェクトがマルチウィンドウをサポートしていない場合は、`UIApplicationDelegate`オブジェクトを呼び出して、URLを開きます。アプリデリゲートクラスを変更してください。

<!-- note end -->

## ログイン処理を実行する 

ユーザーがiOSアプリにログインできるようにするために、LINEロゴがついたログインボタンを作成できます。ユーザーはこのボタンを使ってログインできます。

ログインを実行するには2つの方法があります。

- [LINE SDKに組み込まれているログインボタンを使う](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/integrate-line-login/#use-button)
- [独自のコードを使う](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/integrate-line-login/#use-code)

### LINE SDKに組み込まれているログインボタンを使う 

LINE SDK for iOS Swiftには定義済みのログインボタンが備わっています。SDKに含まれる`LoginButton`クラスは`UIButton`クラスのサブクラスで、「[LINEログインボタン デザインガイドライン](https://developers.line.biz/ja/docs/line-login/login-button/)」で推奨されるスタイルに準拠しています。ユーザーが簡単にアプリにログインできるように、以下の手順に従って、アプリのユーザーインターフェイスにログインボタンを追加できます。

```swift
// In your view controller
override func viewDidLoad() {
    super.viewDidLoad()

    // Create Login Button.
    let loginButton = LoginButton()
    loginButton.delegate = self

    // Configuration for permissions and presenting.
    loginButton.permissions = [.profile]
    loginButton.presentingViewController = self

    // Add button to view and layout it.
    view.addSubview(loginButton)
    loginButton.translatesAutoresizingMaskIntoConstraints = false
    loginButton.centerXAnchor.constraint(equalTo: view.centerXAnchor).isActive = true
    loginButton.centerYAnchor.constraint(equalTo: view.centerYAnchor).isActive = true
}
```

ユーザーがログインボタンをタップすると、適切なログインフローで認証されます。ユーザーがデバイスにLINEをインストール済みの場合、LINEからアプリにユーザーのLINE認証情報が渡されます。ユーザーはこの認証情報を使って認証を受けます。そうでない場合、ブラウザでLINEログイン画面が開きます。ユーザーは、この画面にLINE認証情報を入力します。

ログイン状態を受信するには、`LoginButtonDelegate`プロトコルの関連するデリゲートメソッドを以下のように実装します。

```swift
extension LoginViewController: LoginButtonDelegate {
    func loginButton(_ button: LoginButton, didSucceedLogin loginResult: LoginResult) {
        hideIndicator()
        print("Login Succeeded.")
    }

    func loginButton(_ button: LoginButton, didFailLogin error: LineSDKError) {
        hideIndicator()
        print("Error: \(error)")
    }

    func loginButtonDidStartLogin(_ button: LoginButton) {
        showIndicator()
        print("Login Started.")
    }
}
```

ログイン処理が完了すると、デリゲートメソッドのいずれかがログイン結果と共に呼び出されます。

### 独自のコードを使う 

デフォルトのログインボタンを使う代わりに、コードを使ってユーザーインターフェイスとログインプロセスをカスタマイズすることもできます。

ログイン処理を実行するには、適切なパラメータを指定して`LoginManager.login`メソッドを呼び出します。通常、ログイン処理はビューコントローラーで以下のように実行します。

```swift
// LoginViewController.swift

import LineSDK

class LoginViewController: UIViewController {
    override func viewDidLoad() {
        //...
    }

    func login() {
        LoginManager.shared.login(permissions: [.profile], in: self) {
            result in
            switch result {
            case .success(let loginResult):
                print(loginResult.accessToken.value)
                // Do other things you need with the login result
            case .failure(let error):
                print(error)
            }
        }
    }
}
```

ユーザーがログイン処理を完了すると、完了ハンドラーが`result`引数と共に呼び出されます。ログイン結果にスイッチして、ログインの詳細にアクセスします。

ログインに成功すると、共通のログイン情報を含む`LoginResult`オブジェクトがLINEプラットフォームから返されます。`LoginManager.shared.isAuthorized`メソッドを使ってログイン状態にアクセスします。

ログイン処理中にエラーが発生した場合は、`.failure`の`result`引数と、関連付けられた`LineSDKError`列挙型メンバーがLINE SDKから返されます。SDKからエラーの詳細を取得して適切に制御する方法については、「[エラーを制御する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/error-handling/)」を参照してください。

ログインインターフェイスの設計については、「[LINEログインボタン デザインガイドライン](https://developers.line.biz/ja/docs/line-login/login-button/)」を参照してください。このページからは、LINEログインボタンの画像もダウンロードできます。

## ログイン結果を処理する 

### アクセストークンの権限 

`LoginManager.login`メソッドを呼び出すとき、ユーザーからアプリに付与させたい任意の権限を指定できますが、対応する権限がチャネルに設定されていない可能性があります。その場合は、認可リクエストに指定した権限と、`LoginResult`オブジェクトの`permissions`プロパティの値が異なります。

アクセストークンに関連づけられた付与済みの権限を確認するには、`permissions`プロパティを取得します。たとえば、アクセストークンに`.profile`権限が含まれるかどうかは、以下のコードを使って確認します。

```swift
case .success(let loginResult):
    let profileEnabled = loginResult.permissions.contains(.profile)
```

適切な権限がない場合、APIコールは失敗します。詳しくは、「[エラーを制御する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/error-handling/)」を参照してください。

### ユーザープロフィール 

認可リクエストにプロフィール取得権限を指定した場合、ログイン結果には`UserProfile`オブジェクトが含まれます。以下のようにユーザープロフィール情報にアクセスすれば、独自のユーザーシステムを構築できます。

```swift
LoginManager.shared.login(permissions: [.profile], in: self) {
    result in
    switch result {
    case .success(let loginResult):
        if let profile = loginResult.userProfile {
            print("User ID: \(profile.userID)")
            print("User Display Name: \(profile.displayName)")
            print("User Icon: \(String(describing: profile.pictureURL))")
        }
    case .failure(let error):
        print(error)
    }
}
```

ユーザーIDは各プロバイダーに対してのみ一意です。1人のLINEユーザーは、プロバイダーごとに異なるユーザーIDを持ちます。ユーザーIDでは、異なるプロバイダーを横断してユーザーを識別できません。

### ユーザー情報をバックエンドサーバーで利用する 

<!-- warning start -->

**ユーザーのなりすまし**

バックエンドサーバーでは、`UserProfile`オブジェクトから取得できるユーザーIDなどの情報は、**利用しないでください**。悪意のあるクライアントは、任意のユーザーになりすますために、任意のユーザーIDや不正な情報をバックエンドサーバーに送信できます。

ユーザーIDなどの情報を送信する代わりにアクセストークンを送信し、バックエンドサーバーではアクセストークンからユーザーIDなどの情報を取得します。

<!-- warning end -->

通常、バックエンドサーバーでユーザーを識別するために、ユーザーIDや表示名のような、ユーザーのLINEアカウントに登録されている情報を使用します。そのような情報をアプリからバックエンドサーバーに送信する際は、情報を平文で送信するのではなく、アプリで取得したアクセストークンを送信してください。信頼できる情報を安全に送受信するために、アクセストークンを利用してください。バックエンドサーバーでアクセストークンの正当性を検証したり、ユーザー情報をLINEプラットフォームのサーバーから取得したりできます。

アクセストークンは、`LoginResult`オブジェクトから取得できます。以下のコードは、アクセストークンを取得する方法を示しています。

```swift
LoginManager.shared.login(permissions: [.profile], in: self) {
    result in
    switch result {
    case .success(let loginResult):
        let token = loginResult.accessToken.value
        // Send `token` to your server.
    case .failure(let error):
        print(error)
```

バックエンドサーバーで利用するAPIについては、以下を参照してください。

- [アクセストークンの有効性を検証する](https://developers.line.biz/ja/reference/line-login/#verify-access-token)
- [ユーザープロフィールを取得する](https://developers.line.biz/ja/reference/line-login/#get-user-profile)
