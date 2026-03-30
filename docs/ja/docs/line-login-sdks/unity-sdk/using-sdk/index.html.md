# 他のAPIの利用と実行結果の処理にLINE SDKを使用する

## 実行結果の処理が必要なLINE APIの呼び出し 

失敗する可能性があるすべてのLINE SDK for UnityによるAPI呼び出しでは、コールバックで`Result`オブジェクトが返されます。resultの値を確認すると、成功した場合と失敗した場合の両方を、うまく処理できます。

```csharp
LineSDK.Instance.Login(scopes, result => {
    result.Match(
        value => {
            Debug.Log("Login OK");
        },
        error => {
            Debug.Log("Login failed, error code: " + error.Code);
        }
    );
});
```

`error`節では、すべての`Error`オブジェクトにエラーコード`Code`が含まれます。エラーコードはプラットフォームごとに異なります。詳細については、以下のページを参照してください。

- [LINE SDK for iOS Swift > エラーを制御する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/error-handling/)
- [LINE SDK for Android > エラーを制御する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/handling-errors/)
- [SwiftのエラーAPIリファレンスと定義（英語）](https://developers.line.biz/en/reference/ios-sdk-swift/Enums/LineSDKError.html)
- [AndroidのエラーAPIリファレンスと定義（英語）](https://developers.line.biz/en/reference/android-sdk/reference/com/linecorp/linesdk/LineApiResponseCode.html)

## ユーザープロフィールを取得する 

`profile`スコープを指定してログインリクエストを送信すると、ユーザーのLINEプロフィールを取得できます。ユーザープロフィールには、ユーザーID、表示名、プロフィールメディア（画像または動画）、およびステータスメッセージが含まれます。

`LineAPI.GetProfile`メソッドを以下のように呼び出します。

```csharp
LineAPI.GetProfile(result => {
    result.Match(
        value => {
            Debug.Log("User ID: " + value.UserId);
            Debug.Log("User Display Name: " + value.DisplayName);
            Debug.Log("User Status Message: " + value.StatusMessage);
            Debug.Log("User Icon: " + value.PictureUrl);
        },
        error => {
            Debug.Log(error.Message);
        }
    );
});
```

### ユーザーをログアウトさせる 

アプリからユーザーをログアウトさせることができます。より良いユーザーエクスペリエンスを提供するために、ユーザーがアプリからログアウトする操作を用意することをお勧めします。

`Logout`メソッドを呼び出して、アクセストークンを無効化し、ユーザーをアプリからログアウトさせます。ログアウトした後に再度ログインするには、ユーザーは再度ログインプロセスを行う必要があります。

```csharp
LineSDK.Instance.Logout(result => {
    result.Match(
        _ => { /* User logout done. Update UI. */ },
        error => {
            Debug.Log(error.Message);
        }
    );
});
```

### アクセストークンを取得する 

アクセストークンを使うと、サーバーからLINEログインAPIを呼び出すことができます。詳しくは、『[LINEログイン v2.1 APIリファレンス](https://developers.line.biz/ja/reference/line-login/)』を参照してください。

現在のアクセストークンを取得するには、`LineSDK`インスタンスの`CurrentAccessToken`プロパティを以下のように取得します。

```csharp
var currentToken = LineSDK.Instance.CurrentAccessToken;
if (currentToken != null) {
    Debug.Log("Current token value: " + currentToken.Value);
}
```

<!-- note start -->

**注意**

サーバーにアクセストークンを送信するときは、アクセストークンを暗号化し、暗号化したデータをSSLで送信することをお勧めします。サーバーで受信したアクセストークンと、LINEログインAPIの呼び出しに使用するアクセストークンが一致すること、さらにLINEログインAPIの呼び出しに使用するチャネルIDが自分のチャネルのIDと一致することも、検証する必要があります。

<!-- note end -->

### アクセストークンを検証し、更新する 

`CurrentAccessToken`では、null以外の値が返される場合でも、アクセストークンが有効であることは保証されません。アクセストークンの有効期限がすでに切れていたり、取り消されていたりする可能性があります。`LineAPI.VerifyToken`を使用して、現在のアクセストークンがまだ有効であるかどうかを確認してください。

```csharp
LineAPI.VerifyAccessToken(result => {
    result.Match(
        value => {
            Debug.Log("Channel Id bound to the token: " + value.ChannelId);
        },
        error => {
            Debug.Log("The token verifying failed: " + error.Message);
        }
    );
});
```

`LineAPI`を介してAPIリクエストが実行されるとき、有効期限が切れたアクセストークンは自動的に更新されます。ただし、アクセストークンが失効してから長期間が経過していると、更新操作は失敗します。その場合はエラーが発生し、ユーザーを再ログインさせる必要があります。

開発者自身がアクセストークンを更新することは推奨されません。LINE SDKによるアクセストークンの自動管理に任せるほうが簡単かつ安全です。ただし、以下のようにしてアクセストークンを手動で更新できます。

```csharp
LineAPI.RefreshAccessToken(result => {
    result.Match(
        token => {
            Debug.Log("Token refreshed. New token: " + token.Value);
        },
        error => {
            Debug.Log("Something wrong when refreshing token: " + error.Message);
        }
    );
});
```
