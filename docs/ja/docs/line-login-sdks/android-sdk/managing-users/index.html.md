# ユーザーを管理する

このトピックでは、以下のユーザー管理タスクの実行方法について説明します。

- [ユーザープロフィールを取得する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/managing-users/#get-profile)
- [IDトークンを使ってユーザーを識別する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/managing-users/#get-id-token)
- [ユーザーをログアウトする](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/managing-users/#logout)

<!-- tip start -->

**安全にログインを処理する**

安全にユーザー登録およびログインを処理する方法については、「[アプリとサーバーの間で安全なログインプロセスを構築する](https://developers.line.biz/ja/docs/line-login/secure-login-process/)」を参照してください。

<!-- tip end -->

## ユーザープロフィールを取得する 

`Scope.PROFILE`スコープを指定してログインリクエストを送信すると、ユーザーのLINEプロフィールを取得できます。ユーザープロフィールには、ユーザーID、表示名、プロフィールメディア（画像または動画）、およびステータスメッセージが含まれます。

`LineApiClient.getProfile()`メソッドを以下のように呼び出します。

```java
LineProfile profile = lineApiClient.getProfile().getResponseData()
Log.i(TAG, profile.getDisplayName());
Log.i(TAG, profile.getUserId());
Log.i(TAG, profile.getStatusMessage());
Log.i(TAG, profile.getPictureUrl().toString());
```

`getDisplayName()`<wbr>メソッド、<wbr>`getPictureURL()`メソッド、および`getStatusMessage()`メソッドでは、ログイン時の値が取得されますが、ユーザーはLINEに設定したこれらの値をいつでも変更できます。ユーザーを識別するには、`getUserId()`メソッドを使用します。このメソッドでは、変更できないユーザーIDが返されます。

ユーザープロフィールの画像サイズは、URLにサフィックスを付加することによって変更できます。

画像サイズ | サフィックス
-|-
200 x 200 | /large
51 x 51 | /small

## IDトークンを使ってユーザーを識別する 

[OpenID Connect](https://openid.net/developers/how-connect-works/) 1.0仕様は、OAuth 2.0プロトコル上に付与されるアイデンティティレイヤーです。OpenID Connectを使えば、LINEプラットフォームと安全に情報を交換できます。現在は、OpenID Connect仕様に準拠するIDトークンを発行する方式で、LINEプラットフォームからユーザープロフィールとメールアドレスを取得できます。

### メールアドレス取得権限を申請する 

LINEログインを使ってログインするユーザーに、メールアドレスを取得する権限をアプリに付与するよう要求できます。これを行うには、[LINE Developersコンソール](https://developers.line.biz/console/)で権限を申請します。詳しくは、『LINEログインドキュメント』の「[メールアドレス取得権限を申請する](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#applying-for-email-permission)」を参照してください。

### OpenIDとメールアドレスのスコープを指定したログイン 

メールアドレス取得権限を付加したチャネルでは、以下のように、`Scope.OPENID_CONNECT`スコープと`Scope.OC_EMAIL`スコープを指定してユーザーにログインさせ、IDトークンからユーザーのメールアドレスを取得できます。

```java
import java.util.Arrays;

private static final int REQUEST_CODE = 1;

LineAuthenticationParams params = new LineAuthenticationParams.Builder()
                                    .scopes(Arrays.asList(Scope.OPENID_CONNECT, Scope.OC_EMAIL))
                                    .build();

Intent loginIntent = LineLoginApi.getLoginIntent(
                        view.getContext(),
                        Constants.CHANNEL_ID,
                        params);

startActivityForResult(loginIntent, REQUEST_CODE);
```

IDトークンは署名付きの[JSONウェブトークン](https://datatracker.ietf.org/doc/html/rfc7519)です。不正なデータを防ぐため、LINE SDKによってIDトークンの署名と有効期間が検証されます。検証が成功すると、以下のように`onActivityResult()`コールバックで`LineIdToken`インスタンスを取得できます。

```java
public void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (requestCode != REQUEST_CODE) {
        Log.e("ERROR", "Unsupported Request");
        return;
    }

    LineLoginResult result = LineLoginApi.getLoginResultFromIntent(data);

    switch (result.getResponseCode()) {
        case SUCCESS:
            // Login successful
            LineIdToken lineIdToken = result.getLineIdToken();
            Log.v("INFO", lineIdToken.getEmail());
    ...
    }
}
```

### IDトークンをバックエンドサーバーで利用する 

<!-- warning start -->

**ユーザーのなりすまし**

アプリからバックエンドサーバーに送信されたユーザーIDなどの情報を、信用しないでください。悪意のあるクライアントは、任意のユーザーになりすますために、任意のユーザーIDや不正な情報をバックエンドサーバーに送信できます。

ユーザーIDなどの情報を送信する代わりに、生のIDトークンを送信してください。LINEプラットフォームが提供するAPIでIDトークンを検証すると、バックエンドサーバーでユーザーIDなどの情報を取得できます。

<!-- warning end -->

#### 生のIDトークンを送信する 

`Scope.OPENID_CONNECT`スコープを指定してLINEログインする場合は、`nonce`パラメータに任意の値を指定できます：

```java
private static final int REQUEST_CODE = 1;
...
LineAuthenticationParams params = new LineAuthenticationParams.Builder()
                                  ...
                                  .nonce("<a randomly-generated string>")
                                  .build();

Intent loginIntent = LineLoginApi.getLoginIntent(
                        view.getContext(),
                        Constants.CHANNEL_ID,
                        params);

startActivityForResult(loginIntent, REQUEST_CODE);
```

`nonce`を省略した場合は、LINE SDKによって自動的に値が指定されますが、ランダムに生成した`nonce`を`nonce`パラメータに指定することをお勧めします。ここで指定した`nonce`は、LINEログインAPIを使用して[IDトークンを検証する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/managing-users/#verify-id-token-on-server)ときに使用します。`nonce`を利用してIDトークンを検証することは、[リプレイアタック](https://en.wikipedia.org/wiki/Replay_attack)の防止に役に立ちます。

`Scope.OPENID_CONNECT`スコープを指定したLINEログインに成功すると、以下のコードで、IDトークンの元になった生のIDトークンを取得できます：

```java
public void onActivityResult(int requestCode, int resultCode, Intent data) {
    ...
    LineLoginResult result = LineLoginApi.getLoginResultFromIntent(data);

    switch (result.getResponseCode()) {
        case SUCCESS:
            // Login successful
            LineIdToken lineIdToken = result.getLineIdToken();
            String idTokenStr = lineIdToken.getRawString();
            if (idTokenStr != null) {
                // Send `idTokenStr` to your server.
            } else {
                // Something went wrong. You should fail the login.
            }
    ...
}
```

[IDトークンを検証する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/managing-users/#verify-id-token-on-server)ために、このコードで取得した`idTokenStr`をバックエンドサーバーに送信してください。

#### バックエンドサーバーでIDトークンを検証する 

バックエンドサーバーで生のIDトークンを受信したら、受信したIDトークンと対応する`nonce`を、LINEプラットフォームが提供するIDトークン検証用のエンドポイントに送信して検証してください。IDトークンが有効な場合は、IDトークンクレームを含むJSON形式のオブジェクトが返されます。

バックエンドサーバーで利用するAPIについては、以下を参照してください。

- [IDトークンを検証する](https://developers.line.biz/ja/reference/line-login/#verify-id-token)（LINEログイン v2.1 APIリファレンス）

### ユーザーデータを慎重に扱う 

ユーザーの機密情報をプレーンテキストでアプリやサーバーに保存したり、セキュリティで保護されていないHTTP通信で転送したりしないでください。アクセストークン、ユーザーID、ユーザー名など、IDトークンに含まれるデータは機密情報に該当します。LINE SDKではユーザーのアクセストークンが保存されます。必要に応じて、認可後に以下のコードでアクセストークンを取得できます。

```java
LineAccessToken accessToken = lineApiClient.getCurrentAccessToken().getResponseData();
```

IDトークンはログイン時にのみ発行されます。IDトークンを更新するには、ユーザーに再ログインさせる必要があります。ただし、ログインリクエストに`Scope.PROFILE`スコープを指定する場合は、`LineApiClient.getProfile()`メソッドを呼び出してユーザーのプロフィール情報を取得できます。

## ユーザーをログアウトする 

アプリからユーザーをログアウトさせることができます。より良いユーザー体験のために、ユーザーがアプリからログアウトする手段を提供することをお勧めします。

アクセストークンを無効化してユーザーをアプリからログアウトするには、`logout()`メソッドを呼び出します。アクセストークンを無効にすると、ユーザーはアプリからログアウトされます。ログアウトした後に再度ログインするには、ユーザーは再度ログインプロセスを行う必要があります。

```java
lineApiClient.logout();
```
