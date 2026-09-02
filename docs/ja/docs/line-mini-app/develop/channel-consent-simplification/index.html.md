# LINEミニアプリの認可フロー

LIFFアプリがユーザーの情報を取得したり、ユーザーにメッセージを送信したりするには、ユーザーがLIFFアプリに初めてアクセスする際に、「チャネル同意画面」において、対応する権限に同意する必要があります。

LINEミニアプリでは、「チャネル同意の簡略化」機能を有効にすると、ユーザーがより簡単にLINEミニアプリにアクセスできるようになります。

このページでは「チャネル同意の簡略化」機能と、それに基づく認可フローについて説明します。

<!-- table of contents -->

## 「チャネル同意の簡略化」機能とは 

「チャネル同意の簡略化」機能とは、ユーザーがLINEミニアプリに初めてアクセスする際に必要となる、権限への同意を簡略化する仕組みです。

「チャネル同意の簡略化」機能を有効にすると、ユーザーがLINEミニアプリに初めてアクセスする際に、「チャネル同意画面」をスキップし、すぐにLINEミニアプリの利用を開始できるようになります。ユーザー体験向上のため、「チャネル同意の簡略化」機能を有効にすることを推奨します。

「チャネル同意の簡略化」機能の対象となる権限は、[ユーザーID](https://developers.line.biz/ja/glossary/#user-id)の取得（`openid`スコープ）のみです。ユーザーのプロフィール情報の取得やメッセージ送信に必要な権限（[`profile`スコープや`chat_message.write`スコープ](https://developers.line.biz/ja/docs/liff/registering-liff-apps/#registering-liff-app)など）は対象に含まれません。これらの追加の権限については、各LINEミニアプリ内で必要となったタイミングで「アクセス許可要求画面」が表示されます。詳しくは、「[「アクセス許可要求画面」で`openid`スコープ以外の権限を要求する](https://developers.line.biz/ja/docs/line-mini-app/develop/channel-consent-simplification/#request-permissions-other-than-openid)」を参照してください。

なお、日本の新規LINEミニアプリチャネルでは「チャネル同意の簡略化」機能が常に有効になります。詳しくは、[2026年1月8日のニュース](https://developers.line.biz/ja/news/2026/01/08/channel-consent-simplification/)を参照してください。

<!-- note start -->

**LINEミニアプリの設計によっては正しく動作しなくなる可能性があります**

LIFF SDKで取得した[アクセストークン](https://developers.line.biz/ja/glossary/#access-token)や[IDトークン](https://developers.line.biz/ja/glossary/#id-token)を使って、[LINEログインAPI](https://developers.line.biz/ja/reference/line-login/)を実行する設計の場合、「チャネル同意の簡略化」機能によって、LINEミニアプリが期待どおりに動作しない可能性があります。

たとえば、[IDトークンを検証する](https://developers.line.biz/ja/reference/line-login/#verify-id-token)エンドポイントを実行し、取得したユーザーの[プロフィール情報](https://developers.line.biz/ja/glossary/#profile-information)をLINEミニアプリのサービスアカウントの作成に利用する設計の場合、「チャネル同意の簡略化」機能によって、ユーザーのプロフィール情報（`profile`スコープ）の取得権限への同意がスキップされるため、IDトークンのペイロードにユーザーのプロフィール情報が含まれません。その結果、ユーザーのプロフィール情報をサービスアカウントの作成に利用できなくなります。

この問題を回避するには、アクセストークンやIDトークンを取得する前に、[`liff.permission.query()`](https://developers.line.biz/ja/reference/liff/#permission-query)メソッドと[`liff.permission.requestAll()`](https://developers.line.biz/ja/reference/liff/#permission-request-all)メソッドを使って「アクセス許可要求画面」を表示し、ユーザーに必要な権限を要求してください。詳しくは、「[「アクセス許可要求画面」で`openid`スコープ以外の権限を要求する](https://developers.line.biz/ja/docs/line-mini-app/develop/channel-consent-simplification/#request-permissions-other-than-openid)」を参照してください。

<!-- note end -->

### 「チャネル同意の簡略化」機能の設定方法 

「チャネル同意の簡略化」機能は次の条件をすべて満たす場合のみ設定できます。

- LINEミニアプリチャネルの［**サービスを提供する地域**］が「日本」である。
- LINEミニアプリチャネルのステータスが「審査前」である。

2026年1月8日より前に作成されたLINEミニアプリチャネルの場合、「チャネル同意の簡略化」機能を有効化するには、[LINE Developersコンソール](https://developers.line.biz/console/)のLINEミニアプリチャネルで、［**ウェブアプリ設定**］タブの「チャネル同意の簡略化」セクションのトグルをオン（右）にします。

![](https://developers.line.biz/media/line-mini-app/simplification-feature-setup-ja.png)

なお、「チャネル同意の簡略化」機能はユーザーID（`openid`スコープ）の取得権限への同意を簡略化するため、有効化すると「Scope」セクションの`openid`も自動的に有効になります。

![](https://developers.line.biz/media/line-mini-app/simplification-scope-ja.png)

2026年1月8日以降に作成されたLINEミニアプリチャネルの場合、「チャネル同意の簡略化」機能が常に有効になります。LINE Developersコンソール上の設定は不要です。

### 「チャネル同意の簡略化」機能の動作条件 

「チャネル同意の簡略化」機能が動作するには、次の条件をすべて満たす必要があります。

- LINEミニアプリが認証済ミニアプリである（※）。
- LINEミニアプリのLIFF SDKのバージョンがv2.13.x以降である。
- LINEミニアプリが[LIFF間遷移](https://developers.line.biz/ja/docs/liff/opening-liff-app/#move-liff-to-liff)で開かれていない。

※ 未認証ミニアプリでは、開発用と審査用のLINEミニアプリでのみ動作します。

## 「チャネル同意の簡略化」機能が有効なLINEミニアプリでの認可フロー 

「チャネル同意の簡略化」機能が有効なLINEミニアプリでは、ユーザーID（`openid`スコープ）の取得権限が付与された状態でLINEミニアプリが開かれます。

`openid`スコープ以外の権限が必要な場合は、「[「アクセス許可要求画面」で`openid`スコープ以外の権限を要求する](https://developers.line.biz/ja/docs/line-mini-app/develop/channel-consent-simplification/#request-permissions-other-than-openid)」を参照してください。

![](https://developers.line.biz/media/line-mini-app/channel-consent-simplification/authorization-flow-enabled-ja.webp)

### 「アクセス許可要求画面」で`openid`スコープ以外の権限を要求する 

[`liff.getProfile()`](https://developers.line.biz/ja/reference/liff/#get-profile)メソッドや[`liff.sendMessages()`](https://developers.line.biz/ja/reference/liff/#send-messages)メソッドなど、`openid`スコープ以外の権限を必要とするメソッドを実行すると、「アクセス許可要求画面」が表示されます。「アクセス許可要求画面」では、LINEミニアプリが要求する追加の権限を表示し、権限を許可するかどうかをユーザーに確認します。

![](https://developers.line.biz/media/line-mini-app/line-mini-app-playground-verification-screen-ja.png)

`openid`スコープ以外の権限を必要とするメソッドは次のとおりです。

| スコープ | メソッド |
| --- | --- |
| `email` | <ul><li>[`liff.getIDToken()`](https://developers.line.biz/ja/reference/liff/#get-id-token)</li><li>[`liff.getDecodedIDToken()`](https://developers.line.biz/ja/reference/liff/#get-decoded-id-token)</li></ul> |
| `profile` | <ul><li>[`liff.getProfile()`](https://developers.line.biz/ja/reference/liff/#get-profile)</li><li>[`liff.getFriendship()`](https://developers.line.biz/ja/reference/liff/#get-friendship)</li></ul> |
| `chat_message.write` | <ul><li>[`liff.sendMessages()`](https://developers.line.biz/ja/reference/liff/#send-messages)</li></ul> |

なお、[`liff.permission.query()`](https://developers.line.biz/ja/reference/liff/#permission-query)メソッドと[`liff.permission.requestAll()`](https://developers.line.biz/ja/reference/liff/#permission-request-all)メソッドを使うと、任意のタイミングで「アクセス許可要求画面」を表示できます。

```javascript
liff.permission.query("profile").then((permissionStatus) => {
  if (permissionStatus.state === "prompt") {
    liff.permission.requestAll();
  }
});
```

詳しくは、『LIFF APIリファレンス』の「[`liff.permission.query()`](https://developers.line.biz/ja/reference/liff/#permission-query)」と「[`liff.permission.requestAll()`](https://developers.line.biz/ja/reference/liff/#permission-request-all)」を参照してください。

<!-- tip start -->

**「アクセス許可要求画面」が表示されるタイミング**

「アクセス許可要求画面」は、LINEミニアプリを開いたタイミングではなく、`openid`スコープ以外の権限（[`profile`スコープや`chat_message.write`スコープ](https://developers.line.biz/ja/docs/liff/registering-liff-apps/#registering-liff-app)など）を必要とするタイミングで初めて表示されます。

そのため、LINEミニアプリ起動直後に、[`liff.getProfile()`](https://developers.line.biz/ja/reference/liff/#get-profile)メソッドなど`openid`スコープ以外の権限を必要とするリクエストを実行する設計にしている場合は、LINEミニアプリにアクセスしたユーザーからは、アプリ起動時に「チャネル同意画面」がスキップされずに表示されたように見えてしまいます。`openid`スコープ以外の権限を必要とするリクエストは、可能な限り必要となるタイミングで初めて実行するように実装することをお勧めします。

<!-- tip end -->

### 「チャネル同意の簡略化」機能と友だち追加オプションを併用する際の注意点 

LINEミニアプリでは、[友だち追加オプション](https://developers.line.biz/ja/docs/line-mini-app/service/add-friend-option/)を使って、アクセス許可要求画面、もしくはチャネル同意画面からLINE公式アカウントの友だち追加への誘導ができます。

![](https://developers.line.biz/media/line-mini-app/channel-consent-simplification/add-friend-option-verification-screen-ja.png) ![](https://developers.line.biz/media/line-mini-app/channel-consent-simplification/add-friend-option-channel-consent-screen-ja.png)

しかし、LINEミニアプリチャネルの［**ウェブアプリ設定**］タブの「Scope」セクションで`openid`のみを指定している場合、「チャネル同意の簡略化」機能が有効になると、「アクセス許可要求画面」および「チャネル同意画面」が表示されなくなります。このため、友だち追加オプションによる友だち追加を誘導できなくなります。

「チャネル同意の簡略化」機能と友だち追加オプションを併用する際は、LINEミニアプリチャネルの［**ウェブアプリ設定**］タブの「Scope」セクションで`openid`以外のスコープも指定した上で、アクセス許可要求画面を表示することを推奨します。詳しくは、「[「アクセス許可要求画面」で`openid`スコープ以外の権限を要求する](https://developers.line.biz/ja/docs/line-mini-app/develop/channel-consent-simplification/#request-permissions-other-than-openid)」を参照してください。

また、[`liff.requestFriendship()`](https://developers.line.biz/ja/reference/liff/#request-friendship)メソッドを用いて、任意のタイミングでLINE公式アカウントの友だち追加、またはブロック解除を促すサブウィンドウを表示することも可能です。

## 「チャネル同意の簡略化」が無効なLINEミニアプリでの認可フロー 

ユーザーが「チャネル同意の簡略化」が無効なLINEミニアプリに初めてアクセスすると、「チャネル同意画面」が表示されます。「チャネル同意画面」では、LINEミニアプリが要求する権限の一覧を表示し、権限を許可するかどうかをユーザーに確認します。

［**許可する**］をタップすると、そのLINEミニアプリを利用できるようになります。

![](https://developers.line.biz/media/line-mini-app/channel-consent-simplification/line-mini-app-playground-channel-consent-screen-ja.png)
