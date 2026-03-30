# ユニバーサルリンクを利用する

Appleの[ユニバーサルリンク](https://developer.apple.com/library/archive/documentation/General/Conceptual/AppSearch/UniversalLinks.html)機能を使ってアプリのセキュリティを高めることができます。ユニバーサルリンクを設定すると、LINEにより、まずユニバーサルリンクを使ってアプリの起動が試行されます。ユニバーサルリンクが無効な場合は、iOSバンドルIDに基づいたURLがフォールバックとして使用されます（詳しくは、「[アプリをチャネルにリンクする](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/setting-up-project/#linking-app-to-channel)」を参照してください）。

<!-- note start -->

**ユニバーサルリンク機能の有効化を推奨します**

ユニバーサルリンク機能の有効化は必須ではありませんが、アプリケーションの安全性を高めるため使用することを推奨します。

<!-- note end -->

ユーザーにユニバーサルリンクを使ってアプリを起動させるには、以下の手順に従います。

1. [アプリとサーバーを関連づける。](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/universal-links-support/#ul-s1)
1. [LINE Developersコンソールでユニバーサルリンクを設定する。](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/universal-links-support/#ul-s2)
1. [ユニバーサルリンクを指定して`LoginManager.setup`メソッドを呼び出す。](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/universal-links-support/#ul-s3)
1. [ユニバーサルリンクでアプリが起動した後でログイン結果を制御する。](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/universal-links-support/#ul-s4)

## 1. アプリとサーバーを関連づける 

この手順については、Appleの「[Allowing Apps and Websites to Link to Your Content](https://developer.apple.com/documentation/xcode/allowing-apps-and-websites-to-link-to-your-content)」を参照してください。

以下の作業を完了します。

- アプリで制御するURLのJSONデータを含む`apple-app-site-association`ファイルを作成して、HTTPSサーバーに配置する。
- Associated Domainsのエンタイトルメントをアプリに追加する。

このセクションは、LINEの認可レスポンスを制御するためのユニバーサルリンクが`https://yourdomain.com/line-auth/`であることを前提とします。

`apple-app-site-association`ファイルの`paths`フィールドに`/line-auth/*`を含めます。有効な`apple-app-site-association`ファイルは以下のようになります。

```json
{
    "applinks": {
        "apps": [],
        "details": [
            {
                "appID": "YOUR_TEAM_ID.com.yourcompany.yourapp",
                "paths": [ "/line-auth/*" ]
            }
        ]
    }
}
```

ユニバーサルリンクは実際のiOSデバイスでのみテストできることに注意してください。アプリのIDとプロファイルを正しく設定する必要があります。ユニバーサルリンクが動作しない場合は、Appleの「[Troubleshooting Universal Links](https://developer.apple.com/library/archive/qa/qa1916/_index.html)」を参照してください。次の手順に進む前に、ユニバーサルリンクが動作することを確認してください。

## 2. LINE Developersコンソールでユニバーサルリンクを設定する 

手順については、「[アプリをチャネルにリンクする](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/setting-up-project/#linking-app-to-channel)」を参照してください。この例では、`https://yourdomain.com/line-auth/`に設定します。

## 3. ユニバーサルリンクを指定して`LoginManager.setup`メソッドを呼び出す 

`LoginManager.setup`メソッドを呼び出すときに、ユニバーサルリンクをLINE SDK for iOS Swiftに渡します。これにより、ユニバーサルリンクの不正使用を防ぐため、リンクがLINE Developersコンソールとアプリの両方で正しく設定されていることがLINEログインによって検証されます。以下の例では、ユニバーサルリンクは`https://yourdomain.com/line-auth/`です。

```swift
let link = URL(string: "https://yourdomain.com/line-auth/")
LoginManager.shared.setup(channelID: "YOUR_CHANNEL_ID", universalLinkURL: link)
```

`LoginManager.setup`メソッドについて詳しくは、「[iOSアプリにLINEログインを組み込む](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/integrate-line-login/)」を参照してください。

## 4. ユニバーサルリンクでアプリが起動した後でログイン結果を制御する 

LINEプラットフォームから返されたログイン結果を制御するには、取得したURLを`LoginManager`の`application(_:open:options:)`メソッドに渡します。プロジェクトがマルチウィンドウ（[iOS13で導入された機能](https://developer.apple.com/documentation/uikit/scenes)）をサポートするかどうかで、アプリデリゲートクラスまたはシーンデリゲートクラスを変更する必要があります。

### アプリデリゲートを変更する 

iOS 12以前では、`UIApplicationDelegate`オブジェクトを呼び出して、URLを開きます。したがって、アプリデリゲートクラスに`application(_:continue:restorationHandler:)`デリゲートメソッドが存在していれば、以下の行を追加します。デリゲートメソッドが存在しない場合は、以下のとおりにデリゲートメソッドを作成してください。

```swift
func application(
    _ app: UIApplication,
    continue userActivity: NSUserActivity,
    restorationHandler: @escaping ([UIUserActivityRestoring]?) -> Void) -> Bool
{
    if LoginManager.shared.application(app, open: userActivity.webpageURL) {
        return true
    }
    // Your other code to handle universal links and/or user activities.
}
```

### シーンデリゲートを変更する 

iOS 13以降では、`UISceneDelegate`オブジェクトを呼び出して、URLを開きます。

Xcode 11以降でプロジェクトを作成した場合は、デフォルトでは、プロジェクトには`SceneDelegate.swift`ファイルが含まれ、`Info.plist`ファイルには`UIApplicationSceneManifest`エントリーが含まれます。

アプリがマルチウィンドウをサポートする場合は、使用するシーンデリゲートクラスに、次の行を追加します。

```swift
// SceneDelegate.swift
func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
    _ = LoginManager.shared.application(.shared, open: URLContexts.first?.url)
}
```

<!-- note start -->

**注意**

ただし、アプリがマルチウィンドウをサポートしていない場合は、`UIApplicationDelegate`オブジェクトを呼び出して、URLを開きます。アプリデリゲートクラスを変更してください。

<!-- note end -->

これで、ユニバーサルリンクを使ってLINEからアプリを起動し、アプリでログイン結果を制御できるようになりました。
