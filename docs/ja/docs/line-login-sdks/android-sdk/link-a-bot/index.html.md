# SDKで友だち追加オプションを利用する

ユーザーがアプリにログインするときに、LINE公式アカウントを友だち追加するオプションを表示するように設定できます。これを、**友だち追加オプション**と呼びます。友だち追加するLINE公式アカウントは、開発者が指定できます。

設定を始める前に、『LINEログインドキュメント』の「[LINEログインしたときにLINE公式アカウントを友だち追加する（友だち追加オプション）](https://developers.line.biz/ja/docs/line-login/link-a-bot/)」を参照して友だち追加オプションを理解する必要があります。特に、以下の事項を確認してください。

- LINE DevelopersコンソールでLINE公式アカウントをチャネルにリンクする方法
- LINEプラットフォームに送信するボットプロンプトパラメータとその動作
- LINEプラットフォームから返される友だち関係フラグとその意味

ここでは、友だち追加オプションに関係する以下の機能を、LINE SDKで有効にする方法について説明します。

- [ボットプロンプトパラメータをログインリクエストに設定する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/link-a-bot/#bot_prompt)
- [ユーザーとLINE公式アカウントの間の友だち関係を確認する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/link-a-bot/#get_friendship)

## ボットプロンプトパラメータをログインリクエストに設定する 

以下のサンプルコードは、`LoginButton`ウィジェットを使用する場合に`botPrompt`パラメータを設定する方法を示しています。

```java
...
LoginButton loginButton = rootView.findViewById(R.id.line_login_btn);

loginButton.setAuthenticationParams(new LineAuthenticationParams.Builder()
        .scopes(Arrays.asList(Scope.PROFILE))
        .botPrompt(BotPrompt.normal) // configure it here
        .build()
);
...
```

以下のサンプルコードは、`LoginApi.getLoginIntent()`メソッドを使用する場合に`botPrompt`パラメータを設定する方法を示しています。

```java
Intent loginIntent = LineLoginApi.getLoginIntent(
    view.getContext(),
    Constants.CHANNEL_ID,
    new LineAuthenticationParams.Builder()
            .scopes(Arrays.asList(Scope.PROFILE))
            .botPrompt(BotPrompt.normal) // configure it here
            .build());

startActivityForResult(loginIntent, REQUEST_CODE);
```

パラメータ値について詳しくは、『LINE SDK for Androidリファレンス（英語）』の「[LineAuthenticationParams.BotPrompt](https://developers.line.biz/en/reference/android-sdk/reference/com/linecorp/linesdk/auth/LineAuthenticationParams.BotPrompt.html)」を参照してください。

## ユーザーとLINE公式アカウントの間の友だち関係を確認する 

ユーザーとLINE公式アカウントの間の友だち関係は、以下の方法で確認できます。

- [ログインレスポンスの`LineLoginResult`オブジェクトを確認する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/link-a-bot/#use-friendship_status_changed)：この方法では、ログイン中に友だち関係が変化したかどうかを確認します。
- [LINEログインAPIを使って友だち関係を取得する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/link-a-bot/#use-line-login-api)：この方法では、ユーザーとLINE公式アカウントの間の友だち関係を取得します。

### ログインレスポンスの`LineLoginResult`オブジェクトを確認する 

ログインに成功すると、`LineLoginResult`オブジェクトには友だち関係が変化したかどうかを示すブール値が含まれます。この値は`getFriendshipStatusChanged()`メソッドで取得できます。

友だち関係フラグを取得するには、以下の条件を満たす必要があります。

- ログインリクエストの`LineAuthenticationParams`オブジェクトに`botPrompt`パラメータを指定する。
- LINE公式アカウントを友だち追加するオプションを伴う同意画面がユーザーに表示される。

以下のサンプルコードは、`LineLoginResult`オブジェクトから友だち関係を取得する方法を示しています。

```java
public void onActivityResult(int requestCode, int resultCode, Intent data) {
    ...

    LineLoginResult result = LineLoginApi.getLoginResultFromIntent(data);

    boolean friendshipStatusChanged = result.getFriendshipStatusChanged();

    ...
}
```

戻り値について詳しくは、『LINE SDK for Androidリファレンス（英語）』の「[getFriendshipStatusChanged()](https://developers.line.biz/en/reference/android-sdk/reference/com/linecorp/linesdk/auth/LineLoginResult.html#getFriendshipStatusChanged())」を参照してください。

### LINEログインAPIを使って友だち関係を取得する 

ユーザーがアプリにログインしてアクセストークンが返された後で、`LineApiClient.getFriendshipStatus()`メソッドを呼び出します。

```
boolean isFriendToTheBot = lineApiClient.getFriendshipStatus();
```

戻り値について詳しくは、『LINE SDK for Androidリファレンス（英語）』の「[getFriendshipStatus()](https://developers.line.biz/en/reference/android-sdk/reference/com/linecorp/linesdk/api/LineApiClient.html#getFriendshipStatus())」を参照してください。
