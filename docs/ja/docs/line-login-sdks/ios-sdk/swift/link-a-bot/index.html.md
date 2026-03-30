# SDKで友だち追加オプションを利用する

ユーザーがアプリにログインするときに、LINE公式アカウントを友だち追加するオプションを表示するように設定できます。これを、**友だち追加オプション**と呼びます。友だち追加するLINE公式アカウントは、開発者が指定できます。

設定を始める前に、『LINEログインドキュメント』の「[LINEログインしたときにLINE公式アカウントを友だち追加する（友だち追加オプション）](https://developers.line.biz/ja/docs/line-login/link-a-bot/)」を参照して友だち追加オプションを理解する必要があります。特に、以下の事項を確認してください。

- LINE DevelopersコンソールでLINE公式アカウントをチャネルにリンクする方法
- LINEプラットフォームに送信するボットプロンプトパラメータとその動作
- LINEプラットフォームから返される友だち関係フラグとその意味

ここでは、友だち追加オプションに関係する以下の機能を、LINE SDKで有効にする方法について説明します。

- [ボットプロンプトパラメータをログインリクエストに設定する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/link-a-bot/#bot_prompt)
- [ユーザーとLINE公式アカウントの間の友だち関係を確認する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/link-a-bot/#get_friendship)

## ボットプロンプトパラメータをログインリクエストに設定する 

以下のサンプルコードは、ログインリクエストにボットプロンプトパラメータとして`.botPromptNormal`または`.botPromptAggressive`を設定する方法を示します。

```swift
// Includes an option to add a LINE Official Account as a friend in the consent screen.
var parameters = LoginManager.Parameters()
parameters.botPromptStyle = .normal
LoginManager.shared.login(permissions: [.profile], parameters: parameters) {
    // ...
}

// Opens a new screen to add the LINE Official Account as a friend after the user agrees to the permissions in the consent screen.
parameters.botPromptStyle = .aggressive
LoginManager.shared.login(permissions: [.profile], parameters: parameters) {
    // ...
}
```

パラメータ値について詳しくは、『LINE SDK for iOS Swiftリファレンス（英語）』の「[LoginManager.Parameters](https://developers.line.biz/en/reference/ios-sdk-swift/Classes/LoginManager/Parameters.html)」と「[LoginManager.BotPrompt](https://developers.line.biz/en/reference/ios-sdk-swift/Classes/LoginManager/BotPrompt.html)」を参照してください。

## ユーザーとLINE公式アカウントの間の友だち関係を確認する 

ユーザーとLINE公式アカウントの間の友だち関係は、以下の方法で確認できます。

- [ログインレスポンスの`friendshipStatusChanged`プロパティを確認する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/link-a-bot/#use-friendship_status_changed)：この方法では、ログイン中に友だち関係が変化したかどうかを確認します。
- [LINEログインAPIを使って友だち関係を取得する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/link-a-bot/#use-line-login-api)：この方法では、ユーザーとLINE公式アカウントの間の友だち関係を取得します。

### ログインレスポンスの`friendshipStatusChanged`プロパティを確認する 

ログインに成功すると、`LoginResult`オブジェクトの`friendshipStatusChanged`プロパティには友だち関係が変化したかどうかを示すブール値が含まれます。

友だち関係フラグを取得するには、以下の条件を満たす必要があります。

- ログインリクエストにボットプロンプトオプションを指定する。
- LINE公式アカウントを友だち追加するオプションを伴う同意画面がユーザーに表示される。

以下のサンプルコードは、`friendshipStatusChanged`プロパティを取得する方法を示しています。

```swift
var parameters = LoginManager.Parameters()
parameters.botPromptStyle = .normal
LoginManager.shared.login(permissions: [.profile], parameters: parameters) {
    result in
    switch result {
    case .success(let value):
        print(value.friendshipStatusChanged)
    case .failure(let error):
        print(error)
    }
}
```

`friendshipStatusChanged`プロパティについて詳しくは、『LINE SDK for iOS Swiftリファレンス（英語）』の「[friendshipStatusChanged](https://developers.line.biz/en/reference/ios-sdk-swift/Structs/LoginResult.html#/s:7LineSDK11LoginResultV23friendshipStatusChangedSbSgvp)」を参照してください。

### LINEログインAPIを使って友だち関係を取得する 

ユーザーがアプリにログインしてアクセストークンが返された後で、`getBotFriendshipStatus`メソッドを呼び出します。

```swift
API.getBotFriendshipStatus { result in
    switch result {
    case .success(let value): print(value.friendFlag)
    case .failure(let error): print(error)
    }
}
```

戻り値について詳しくは、『LINE SDK for iOS Swiftリファレンス（英語）』の「[getBotFriendshipStatus](https://developers.line.biz/en/reference/ios-sdk-swift/Enums/API.html#/s:7LineSDK3APIO22getBotFriendshipStatus13callbackQueue17completionHandleryAA08CallbackI0O_ys6ResultOyAA03GetefG7RequestV8ResponseVAA0A8SDKErrorOGctFZ)」を参照してください。
