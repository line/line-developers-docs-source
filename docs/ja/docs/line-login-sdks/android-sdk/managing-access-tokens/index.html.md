# アクセストークンを管理する

このトピックでは、以下のアクセストークン管理タスクの実行方法について説明します。

- [アクセストークンを更新する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/managing-access-tokens/#refresh-token)
- [現在のアクセストークンを取得する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/managing-access-tokens/#get-current-token)
- [アクセストークンを検証する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/managing-access-tokens/#verify-access-token)

<!-- tip start -->

**安全にログインを処理する**

安全にユーザー登録およびログインを処理する方法については、「[アプリとサーバーの間で安全なログインプロセスを構築する](https://developers.line.biz/ja/docs/line-login/secure-login-process/)」を参照してください。

<!-- tip end -->

## アクセストークンを更新する 

認可が成功したあと、ユーザーの有効なアクセストークンがLINE SDKによって保存されます。このアクセストークンを使って、APIリクエストが実行されます。アクセストークンの有効期間は以下のようにして取得できます。

```java
LineAccessToken accessToken = lineApiClient.getCurrentAccessToken().getResponseData();
Log.i(TAG, accessToken.getExpiresInMillis());
```

`LineApiClient`インターフェイスを介してAPIリクエストが実行されるとき、有効期限が切れたアクセストークンは自動的に更新されます。ただし、アクセストークンが失効してから長期間が経過していると、更新操作は失敗します。その場合はエラーが発生し、ユーザーを再ログインさせる必要があります。

開発者自身がアクセストークンを更新することは**推奨されません**。LINE SDKによるアクセストークンの自動管理に任せるほうが、将来のアップグレードを考えるとより簡単で安全な方法です。ただし、以下のようにしてアクセストークンを手動で更新できます。

```java
LineAccessToken newAccessToken = lineApiClient.refreshAccessToken().getResponseData();
```

## 現在のアクセストークンを取得する 

クライアントサーバーアプリケーションでは、アプリとサーバーの間でユーザー情報を送受信する際に、アクセストークンを使用してください。アプリで取得したアクセストークンをサーバーに送信すると、サーバーでLINEログインAPIを呼び出すことができます。LINEログインAPIについて詳しくは、『[LINEログイン v2.1 APIリファレンス](https://developers.line.biz/ja/reference/line-login/)』を参照してください。

アプリでLINE SDKが保存しているアクセストークンを取得するには、以下のように`getCurrentAccessToken()`メソッドを呼び出します。

```java
String accessToken = lineApiClient.getCurrentAccessToken().getResponseData().getTokenString();
```

<!-- note start -->

**注意**

サーバーにアクセストークンを送信するときは、トークンを暗号化し、暗号化したデータをSSLで送信することをお勧めします。サーバーで受信したアクセストークンと、LINEログインの呼び出しに使用するアクセストークンが一致すること、さらにLINEログインの呼び出しに使用するチャネルIDが自分のチャネルのIDと一致することも、検証する必要があります。

<!-- note end -->

## アクセストークンを検証する 

LINE SDKが保存しているアクセストークンの有効性をアプリで検証するには、`verifyToken()`メソッドを呼び出します。結果が含まれる`LineApiResponse`オブジェクトが返されます。次に`isSuccess()`メソッドを呼び出して、トークンの有効性を確認できます。

`isSuccess()`メソッドから`true`が返される場合は、トークンは有効です。そうでない場合は、アクセストークンが無効または期限切れであるか、何らかの理由でLINE SDK内でLINEログインAPIの呼び出しに失敗しています。

`isSuccess()`メソッドから`false`が返される場合は、`LineApiResponse.getErrorData()`メソッドを使用して`verifyToken()`メソッドが失敗した原因を確認できます。なお、この場合は、`getResponseData()`メソッドから`null`が返されます。

```java
LineApiResponse verifyResponse = lineApiClient.verifyToken();

if (verifyResponse.isSuccess()) {

    Log.i(TAG, "getResponseData: " + verifyResponse.getResponseData().toString());
    Log.i(TAG, "getResponseCode: " + verifyResponse.getResponseCode().toString());

    return true;
} else {

    Log.i(TAG, "getResponseCode: " + verifyResponse.getResponseCode());
    Log.i(TAG, "getErrorData: " + verifyResponse.getErrorData());

    return false;

}
```

アクセストークンに関連付けられているスコープのリストを取得するには、`LineApiResponse.getResponseData().getScopes()`メソッドを呼び出します。以下の例では、トーストでアクセストークンのスコープのリストを表示する方法を示しています。

```java
protected void onPostExecute(LineApiResponse response){
    if (response.isSuccess()){
        LineCredential lineCredential = response.getResponseData();
        List<Scope> scopes = lineCredential.getScopes();
        String scopesString = Scope.join(scopes);
        Toast.makeText(getApplicationContext(), scopesString, Toast.LENGTH_SHORT).show();
    }
}
```
