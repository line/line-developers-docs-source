# ウェブアプリにLINEログインを組み込む（LINEログイン v2.0）

<!-- warning start -->

**LINEログイン v2.0は非推奨です**

このページは旧バージョンのLINEログイン v2.0に関するドキュメントです。LINEログイン v2.0は[非推奨](https://developers.line.biz/ja/glossary/#deprecated)であり、時期は未定ですが[廃止](https://developers.line.biz/ja/glossary/#end-of-life)を予定しているため、現行バージョン（LINEログイン v2.1）の利用を推奨します。なお廃止時期の告知から、実際の廃止までは一定の猶予期間を置く予定です。詳しくは、「[LINEログインのバージョンについて](https://developers.line.biz/ja/docs/line-login/overview/#versions)」を参照してください。

<!-- warning end -->

このページでは、ウェブアプリにLINEログインを組み込む方法について説明します。LINEログインを組み込めるアプリがない場合は、サンプルアプリを利用できます。「[LINEログインを利用するには](https://developers.line.biz/ja/docs/line-login/getting-started/)」を参照してください。

## ログインのフロー 

ウェブアプリ向けのLINEログインの処理（ウェブログイン）は、[OAuth 2.0の認可コード付与のフロー](https://datatracker.ietf.org/doc/html/rfc6749)に基づいています。

ウェブログインのフローの概要は以下のとおりです。フロー図で「Web app」が関係しているフローは、ウェブアプリで実装が必要です。

![Web login flow](https://developers.line.biz/media/line-login/web-login-flow.svg)

## チャネルを作成する 

[「LINEログインチャネル」を作成](https://developers.line.biz/ja/docs/line-login/getting-started/#step-1-create-channel)し、ウェブアプリ用に設定します。

- [コールバックURLを設定する](https://developers.line.biz/ja/docs/line-login/integrate-line-login-v2/#setting-callback-url)

### コールバックURLを設定する 

コールバックURLは、ユーザーが認証と認可の操作を行ったあとで、ウェブアプリが認可コードと`state`を受け取るために使用されます。

[LINE Developersコンソール](https://developers.line.biz/console/)のチャネル設定の［**LINEログイン設定**］タブで、コールバックURLを設定してください。1つのチャネルに、複数のコールバックURLを指定できます。

![リダイレクト設定](https://developers.line.biz/media/line-login/integrate-login-web/redirect-settings.png)

<!-- note start -->

**メールアドレスの取得権限について**

LINEログイン v2.0を使用する場合は、LINEログインを使ってログインしたユーザーのメールアドレスを取得できません。

<!-- note end -->

## ユーザーに認証と認可を要求する 

LINEプラットフォームとユーザーの間で、認証と認可のプロセスを開始させます。ユーザーがLINEログインボタンをクリックしたときに、認可URLにユーザーをリダイレクトしてください。

<!-- tip start -->

**ヒント**

- ウェブアプリにLINEログインボタンを追加する際は、「[LINEログインボタン デザインガイドライン](https://developers.line.biz/ja/docs/line-login/login-button/)」に従ってください。
- LINEログインボタンを表示せず、認可URLに直接リンクすることもできます。
- ユーザーの認証情報は、ウェブアプリには通知されません。

<!-- tip end -->

認可URLの例：

```
https://access.line.me/dialog/oauth/weblogin?response_type=code&client_id=1234567890&redirect_uri=https%3A%2F%2Fexample.com%2Fauth&state=123abc
```

認可URLに付与できるクエリパラメータは、以下のとおりです。

| パラメータ | タイプ | 必須  | 説明 |
| --- | --- | --- | --- |
| `response_type` | String | 必須  | `code` |
| `client_id` | String | 必須  | LINEログインチャネルのチャネルID。[LINE Developersコンソール](https://developers.line.biz/console/)で確認できます。 |
| `redirect_uri` | String | 必須  | [LINE Developersコンソール](https://developers.line.biz/console/)に登録したコールバックURL |
| `state` | String | 必須  | [クロスサイトリクエストフォージェリ](https://wikipedia.org/wiki/Cross-site_request_forgery)防止用の固有な英数字の文字列。 **ログインセッションごとにウェブアプリでランダムに生成してください。** なお、URLエンコードされた文字列は使用できません。 |

### ユーザーがユーザー認証と認可を行う 

<!-- tip start -->

**ユーザー認証と認可はユーザーとLINEプラットフォームの間で直接行われます**

LINEログインを組み込むウェブアプリ側で、認可の機能を実装する必要はありません。

<!-- tip end -->

認可URLにリダイレクトされたユーザーは、自分のLINE認証情報を使ってログインし、ウェブアプリが要求するアクセス権を認可します。

同意画面の例：

![同意画面](https://developers.line.biz/media/line-login/integrate-login-web/consent-screen.png)

## ウェブアプリで認可コードまたはエラーレスポンスを受け取る 

ユーザーによる認証と認可のプロセスが終了すると、ユーザーはコールバックURLにリダイレクトされます。

ユーザーがアプリにアクセス権を付与したときは、認可コードが渡されます。また、アクセス権の付与を拒否したときは、エラーレスポンスが渡されます。

### 認可コードを受け取る 

ユーザーの認証と認可が完了すると、以下のクエリパラメータを含むコールバックURLにリダイレクトされます。

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `code` | String | アクセストークンの取得に使用される認可コード。有効期間は10分です。また、認可コードは1回のみ利用可能です。 |
| `state` | String | [クロスサイトリクエストフォージェリ](https://wikipedia.org/wiki/Cross-site_request_forgery)防止用の固有な英数字の文字列。この値が認可URLに付与した`state`パラメータの値と一致することを検証してください。 |

リダイレクト先URLの例：

```
https://example.com/callback?code=b5fd32eacc791df&state=123abc
```

### エラーレスポンスを受け取る 

アプリの要求する権限の付与をユーザーが拒否した場合、以下のクエリパラメータを含むコールバックURLにリダイレクトされます。

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `error_description` | String | `The+user+has+denied+the+approval`<br>注意：このパラメータは、iOSアプリとAndroidアプリのアプリ内ブラウザでは表示されません。この問題については、現在対応中です。 |
| `errorMessage` | String | `DISALLOWED` |
| `errorCode` | Number | `417` |
| `state` | String | 認可URLに含めた`state`パラメータ。この値で、どのプロセスが拒否されたか特定できます。 |
| `error` | String | `access_denied` |

リダイレクト先URLの例：

```
https://example.com/callback?error_description=The+user+has+denied+the+approval&errorMessage=DISALLOWED&errorCode=417&state=123abc&error=access_denied
```

## ウェブアプリでアクセストークンを取得する 

LINEプラットフォームから認可コードを受け取った際、同時に受け取った`state`パラメータと、[認証と認可を要求した](https://developers.line.biz/ja/docs/line-login/integrate-line-login-v2/#making-an-authorization-request)ときに指定した`state`パラメータが一致すれば、アクセストークンを取得できます。

リクエストの例：

```sh
curl -v -X POST https://api.line.me/v2/oauth/accessToken \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=authorization_code' \
-d 'code=b5fd32eacc791df' \
-d 'redirect_uri=https%3A%2F%2Fexample.com%2Fauth' \
-d 'client_id=12345' \
-d 'client_secret=d6524edacc8742aeedf98f'
```

レスポンスの例：

```json
{
  "access_token": "bNl4YEFPI/hjFWhTqexp4MuEw5YPs7qhr6dJDXKwNPuLka...",
  "expires_in": 2591977,
  "refresh_token": "8iFFRdyxNVNLWYeteMMJ",
  "scope": "P",
  "token_type": "Bearer"
}
```

詳しくは、『LINEログイン v2.0 APIリファレンス』の「[アクセストークンを発行する](https://developers.line.biz/ja/reference/line-login-v2/#issue-access-token)」を参照してください。

## 次のステップ 

取得したアクセストークンを使って、以下の操作を行えます。

- [アクセストークンを管理する（LINEログイン v2.0）](https://developers.line.biz/ja/docs/line-login/managing-access-tokens-v2/)
- [ユーザーを管理する（LINEログイン v2.0）](https://developers.line.biz/ja/docs/line-login/managing-users-v2/)
