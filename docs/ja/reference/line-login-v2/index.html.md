# LINEログイン v2.0 APIリファレンス

<!-- warning start -->

**LINEログイン v2.0は非推奨です**

このページは旧バージョンのLINEログイン v2.0のAPIリファレンスです。LINEログイン v2.0は[非推奨](https://developers.line.biz/ja/glossary/#deprecated)であり、時期は未定ですが[廃止](https://developers.line.biz/ja/glossary/#end-of-life)を予定しているため、現行バージョン（LINEログイン v2.1）の利用を推奨します。なお廃止時期の告知から、実際の廃止までは一定の猶予期間を置く予定です。LINEログイン v2.1のAPIリファレンスは、「[LINEログイン v2.1 APIリファレンス](https://developers.line.biz/ja/reference/line-login/)」を参照してください。

<!-- warning end -->

## 共通仕様

### レート制限 

LINEログインのAPIに対して短時間に大量のリクエストを送信し、LINEプラットフォームの動作に影響を与えると判断された場合、一時的にリクエストを制限することがあります。負荷テストを含め、いかなる目的でも大量のリクエストを送信しないでください。

<!-- tip start -->

**レート制限のしきい値について**

LINEログインのAPIにおけるレート制限のしきい値は開示していません。

<!-- tip end -->

### ステータスコード 

APIコールの後で、以下のHTTPステータスコードが返されます。ステータスコードの説明は、特に断りがない限り、[HTTP status code specification](https://datatracker.ietf.org/doc/html/rfc7231#section-6)に準拠しています。

ステータスコード | 説明
---- | ----
200 OK | リクエストが成功しました。
400 Bad Request | リクエストに問題があります。リクエストパラメータとJSONの形式を確認してください。
401 Unauthorized | Authorizationヘッダーを正しく送信していることを確認してください。
403 Forbidden | APIを使用する権限がありません。ご契約中のプランやアカウントに付与されている権限を確認してください。
413 Payload Too Large | リクエストのサイズが上限の2MBを超えています。リクエストのサイズを2MB以下にしてリクエストしなおしてください。
429 Too Many Requests | 大量のリクエストで[レート制限](https://developers.line.biz/ja/reference/line-login-v2/#rate-limits)を超過したため、一時的にリクエストを制限しています。
500 Internal Server Error | APIサーバーの一時的なエラーです。

## OAuth

### アクセストークンを発行する 

アクセストークンを発行します。

LINEログインAPIで管理するアクセストークンは、LINEプラットフォームに保存されているユーザー情報（例：ユーザーID、表示名、プロフィール画像、およびステータスメッセージ）を利用することを、アプリが許可されていることを示します。

レスポンスに含まれるアクセストークンとリフレッシュトークンは、LINEログインAPIを呼び出す際に必要です。

<!-- note start -->

**注意**

ここでは、LINEログイン v2.0のエンドポイントについて解説します。v2.1については、v2.1の「[アクセストークンを発行する](https://developers.line.biz/ja/reference/line-login/#issue-access-token)」を参照してください。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/oauth/accessToken \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=authorization_code' \
-d 'code=b5fd32eacc791df' \
-d 'redirect_uri=https%3A%2F%2Fexample.com%2Fauth' \
-d 'client_id=12345' \
-d 'client_secret=d6524edacc8742aeedf98f'
```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://api.line.me/v2/oauth/accessToken`

#### リクエストヘッダー 

<!-- parameter start (props: required) -->
Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->
grant_type
String

`authorization_code`

<!-- parameter end -->
<!-- parameter start (props: required) -->
code
String

LINEプラットフォームから受け取った[認可コード](https://developers.line.biz/ja/docs/line-login/integrate-line-login-v2/#receiving-the-authorization-code)

<!-- parameter end -->
<!-- parameter start (props: required) -->
redirect_uri
String

コールバックURL

<!-- parameter end -->
<!-- parameter start (props: required) -->
client_id
String

チャネルID。[LINE Developersコンソール](https://developers.line.biz/console/)で確認できます。

<!-- parameter end -->
<!-- parameter start (props: required) -->
client_secret
String

チャネルシークレット。[LINE Developersコンソール](https://developers.line.biz/console/)で確認できます。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->
access_token
String

アクセストークン。有効期間は30日です。

<!-- parameter end -->
<!-- parameter start -->
expires_in
Number

アクセストークンの有効期限が切れるまでの秒数

<!-- parameter end -->
<!-- parameter start -->
refresh_token
String

新しいアクセストークンを取得するためのトークン（リフレッシュトークン）。アクセストークンの有効期限が切れてから最長10日間有効です。

詳しくは、「[アクセストークンを更新する](https://developers.line.biz/ja/reference/line-login-v2/#refresh-access-token)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->
scope
String

アクセストークンに付与されている権限

- `P`：ユーザーのプロフィール情報にアクセスできます。

<!-- parameter end -->
<!-- parameter start -->
token_type
String

`Bearer`

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
    "access_token": "bNl4YEFPI/hjFWhTqexp4MuEw5YPs7qhr6dJDXKwNPuLka...",
    "expires_in": 2591977,
    "refresh_token": "8iFFRdyxNVNLWYeteMMJ",
    "scope": "P",
    "token_type": "Bearer"
}
```

<!-- tab end -->

### アクセストークンの有効性を検証する 

アクセストークンの有効性を検証します。

アクセストークンを利用して、安全にユーザー登録およびログインを処理する方法については、『LINEログインドキュメント』の「[アクセストークンを検証する](https://developers.line.biz/ja/docs/line-login/managing-access-tokens-v2/#verify-access-token)」を参照してください。

<!-- note start -->

**注意**

ここでは、LINEログイン v2.0のエンドポイントについて解説します。v2.1については、v2.1の「[アクセストークンの有効性を検証する](https://developers.line.biz/ja/reference/line-login/#verify-access-token)」を参照してください。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/oauth/verify \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'access_token=bNl4YEFPI/hjFWhTqexp4MuEw5YPs7qhr6dJDXKwNPuLka...'
```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://api.line.me/v2/oauth/verify`

#### リクエストヘッダー 

<!-- parameter start (props: required) -->
Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start -->
access_token
String

アクセストークン

<!-- parameter end -->

#### レスポンス 

アクセストークンが有効である場合は、HTTPステータスコード `200 OK` と、以下の情報を含むJSONオブジェクトが返されます。

<!-- parameter start -->
scope
String

アクセストークンに付与されている権限

- `P`：ユーザーのプロフィール情報にアクセスできます。

<!-- parameter end -->
<!-- parameter start -->
client_id
String

アクセストークンが発行されたチャネルID

<!-- parameter end -->
<!-- parameter start -->
expires_in
Number

アクセストークンの有効期限が切れるまでの秒数

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
   "scope":"P",
   "client_id":"1350031035",
   "expires_in":2591965
}
```

<!-- tab end -->

#### エラーレスポンス 

アクセストークンの有効期限が切れている場合は、HTTPステータスコード `400 Bad Request` と、JSONオブジェクトが返されます。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
{
    "error": "invalid_request",
    "error_description": "access_token invalid"
}
```

<!-- tab end -->

### アクセストークンを更新する 

リフレッシュトークンを使って新しいアクセストークンを取得できます。
ユーザーの認証が終わったときに、アクセストークンと共にリフレッシュトークンが返されます。

<!-- note start -->

**注意**

- ここでは、LINEログイン v2.0のエンドポイントについて解説します。v2.1については、v2.1の「[アクセストークンを更新する](https://developers.line.biz/ja/reference/line-login/#refresh-access-token)」を参照してください。
- Messaging APIで使用されるチャネルアクセストークンの更新には使用できません。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/oauth/accessToken \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=refresh_token' \
--data-urlencode 'client_id={channel ID}' \
--data-urlencode 'client_secret={channel secret}' \
--data-urlencode 'refresh_token={refresh token}'
```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://api.line.me/v2/oauth/accessToken`

#### リクエストヘッダー 

<!-- parameter start (props: required) -->
Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start -->
grant_type
String

`refresh_token`

<!-- parameter end -->
<!-- parameter start -->
refresh_token
String

再発行するアクセストークンに対応するリフレッシュトークン。アクセストークンの有効期限が切れてから最長10日間有効です。リフレッシュトークンの有効期限が切れた場合は、ユーザーに再度ログインを要求して新しいアクセストークンを生成する必要があります。

<!-- parameter end -->
<!-- parameter start -->
client_id
String

チャネルID。[LINE Developersコンソール](https://developers.line.biz/console/)で確認できます。

<!-- parameter end -->
<!-- parameter start -->
client_secret
String

チャネルシークレット。[LINE Developersコンソール](https://developers.line.biz/console/)で確認できます。

<!-- parameter end -->

#### レスポンス 

アクセストークンの更新が成功すると、新しいアクセストークンとリフレッシュトークンが返されます。

<!-- parameter start -->
token_type
String

`Bearer`

<!-- parameter end -->
<!-- parameter start -->
scope
String

アクセストークンに付与されている権限

- `P`：ユーザーのプロフィール情報にアクセスできます。

<!-- parameter end -->
<!-- parameter start -->
access_token
String

アクセストークン

<!-- parameter end -->
<!-- parameter start -->
expires_in
Number

アクセストークンの有効期限が切れるまでの秒数

<!-- parameter end -->
<!-- parameter start -->
refresh_token
String

新しいアクセストークンを取得するためのトークン（リフレッシュトークン）。アクセストークンの有効期限が切れてから最長10日間有効です。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
   "token_type":"Bearer",
   "scope":"P",
   "access_token":"bNl4YEFPI/hjFWhTqexp4MuEw...",
   "expires_in":2591977,
   "refresh_token":"8iFFRdyxNVNLWYeteMMJ"
}
```

<!-- tab end -->

#### エラーレスポンス 

リフレッシュトークンの有効期限が切れている場合は、HTTPステータスコード `400 Bad Request` と、JSONオブジェクトが返されます。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
{
    "error": "invalid_grant",
    "error_description": "invalid refresh_token"
}
```

<!-- tab end -->

### アクセストークンを取り消す 

ユーザーのアクセストークンを無効にします。

<!-- note start -->

**注意**

- ここでは、LINEログイン v2.0のエンドポイントについて解説します。v2.1については、v2.1の「[アクセストークンを取り消す](https://developers.line.biz/ja/reference/line-login/#revoke-access-token)」を参照してください。
- Messaging APIで使用されるチャネルアクセストークンの無効化には使用できません。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/oauth/revoke \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'refresh_token={refresh token}'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/v2/oauth/revoke`

#### Request headers 

<!-- parameter start (props: required) -->
Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### Request body 

Request body は form-urlencoded フォーマットになります。

<!-- parameter start -->
refresh_token
String

無効化するアクセストークンのリフレッシュトークン

<!-- parameter end -->

#### Response 

ステータスコード`200`と空のレスポンスボディを返します。

## プロフィール

### ユーザープロフィールを取得する 

ユーザーのユーザーID、表示名、プロフィール画像、およびステータスメッセージを取得します。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/profile \
-H 'Authorization: Bearer {access token}'
```

<!-- tab end -->

#### HTTPリクエスト 

`GET https://api.line.me/v2/profile`

#### リクエストヘッダー 

<!-- parameter start (props: required) -->
Authorization

Bearer `{access token}`

<!-- parameter end -->

#### レスポンス 

<!-- parameter start -->
userId
String

ユーザーID

<!-- parameter end -->
<!-- parameter start -->
displayName
String

ユーザーの表示名

<!-- parameter end -->
<!-- parameter start -->
pictureUrl
String

プロフィール画像のURL。スキームはhttpsです。ユーザーがプロフィール画像を設定していない場合はレスポンスに含まれません。

プロフィール画像のサムネイル：

プロフィール画像のURLに、以下のサフィックスを付加すると、プロフィール画像のサムネイルを取得できます。

サフィックス | サムネイルサイズ
-------- | ------
`/large` | 200 x 200
`/small` | 51 x 51

例：`https://profile.line-scdn.net/abcdefghijklmn/large`

<!-- parameter end -->
<!-- parameter start -->
statusMessage
String

ユーザーのステータスメッセージ。ユーザーがステータスメッセージを設定していない場合はレスポンスに含まれません。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "userId":"U4af4980629...",
  "displayName":"Brown",
  "pictureUrl":"https://profile.line-scdn.net/abcdefghijklmn",
  "statusMessage":"Hello, LINE!"
}
```

<!-- tab end -->
