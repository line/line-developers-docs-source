# LINEログイン v2.1 APIリファレンス

## 共通仕様 

### レート制限 

LINEログインのAPIに対して短時間に大量のリクエストを送信し、LINEプラットフォームの動作に影響を与えると判断された場合、一時的にリクエストを制限することがあります。負荷テストを含め、いかなる目的でも大量のリクエストを送信しないでください。

<!-- tip start -->

**レート制限のしきい値について**

LINEログインのAPIにおけるレート制限のしきい値は開示していません。

<!-- tip end -->

### ステータスコード 

APIコールの後で、以下のHTTPステータスコードが返されます。ステータスコードの説明は、特に断りがない限り、[HTTP status code specification](https://datatracker.ietf.org/doc/html/rfc7231#section-6)に準拠しています。

| ステータスコード | 説明 |
| --- | --- |
| 200 OK | リクエストが成功しました。 |
| 400 Bad Request | リクエストに問題があります。リクエストパラメータとJSONの形式を確認してください。 |
| 401 Unauthorized | Authorizationヘッダーを正しく送信していることを確認してください。 |
| 403 Forbidden | APIを使用する権限がありません。ご契約中のプランやアカウントに付与されている権限を確認してください。 |
| 413 Payload Too Large | リクエストのサイズが上限の2MBを超えています。リクエストのサイズを2MB以下にしてリクエストしなおしてください。 |
| 429 Too Many Requests | 大量のリクエストで[レート制限](https://developers.line.biz/ja/reference/line-login/#rate-limits)を超過したため、一時的にリクエストを制限しています。 |
| 500 Internal Server Error | APIサーバーの一時的なエラーです。 |

### レスポンスヘッダー 

LINEログインAPIのレスポンスには、以下のHTTPヘッダーが含まれます。

| レスポンスヘッダー | 説明 |
| --- | --- |
| x-line-request-id | リクエストID。各リクエストごとに発行されるIDです。 |

## OAuth 

### アクセストークンを発行する 

Endpoint: `POST` `https://api.line.me/oauth2/v2.1/token`

アクセストークンを発行します。

LINEログインAPIで管理するアクセストークンは、LINEプラットフォームに保存されているユーザー情報（例：ユーザーID、表示名、プロフィール画像、およびステータスメッセージ）を利用することを、アプリが許可されていることを示します。

レスポンスに含まれるアクセストークンとリフレッシュトークンは、LINEログインAPIを呼び出す際に必要です。

<!-- note start -->

**注意**

- ここでは、LINEログイン v2.1のエンドポイントについて解説します。v2.0については、v2.0の「[アクセストークンを発行する](https://developers.line.biz/ja/reference/line-login-v2/#issue-access-token)」を参照してください。
- LINEログイン機能に追加または変更があったときに、レスポンスやIDトークンのJSONオブジェクトの構造が変更される場合があります。この変更には、プロパティの追加、順序の変更、データの要素間の空白や改行の有無、データ長の変化が含まれます。将来、従来と異なる構造のペイロードを受信しても不具合が発生しないように、サーバーを実装してください。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/oauth2/v2.1/token \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=authorization_code' \
-d 'code=1234567890abcde' \
--data-urlencode 'redirect_uri=https://example.com/auth?key=value' \
-d 'client_id=1234567890' \
-d 'client_secret=1234567890abcdefghij1234567890ab' \
-d 'code_verifier=wJKN8qz5t8SSI9lMFhBB6qwNkQBkuPZoCxzRhwLRUo1'
```

<!-- tab end -->

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

LINEプラットフォームから受け取った[認可コード](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#receiving-the-authorization-code)

<!-- parameter end -->
<!-- parameter start (props: required) -->

redirect_uri

String

[認可リクエスト](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#making-an-authorization-request)時に指定した`redirect_uri`と同じ値

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
<!-- parameter start (props: optional) -->

code_verifier

String

半角英数字および記号からなる43〜128文字のランダムな文字列（例：`wJKN8qz5t8SSI9lMFhBB6qwNkQBkuPZoCxzRhwLRUo1`）。<br>LINEログインがPKCEを実装している場合、本パラメータを加えることで、LINEプラットフォーム側で`code_verifier`の有効性を検証したうえでアクセストークンを返却します。<br>PKCEの実装方法について詳しくは、『LINEログインドキュメント』の「[LINEログインにPKCEを実装する](https://developers.line.biz/ja/docs/line-login/integrate-pkce/#how-to-integrate-pkce)」を参照してください。

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

id_token

String

ユーザー情報を含む[JSONウェブトークン（JWT）](https://datatracker.ietf.org/doc/html/rfc7519)。このプロパティは、スコープに`openid`を指定した場合にのみ返されます。IDトークンについて詳しくは、「[IDトークンからプロフィール情報を取得する](https://developers.line.biz/ja/docs/line-login/verify-id-token/)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

refresh_token

String

新しいアクセストークンを取得するためのトークン（リフレッシュトークン）。アクセストークンが発行されてから90日間有効です。

詳しくは、「[アクセストークンを更新する](https://developers.line.biz/ja/reference/line-login/#refresh-access-token)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

scope

String

アクセストークンに付与されている権限。スコープについて詳しくは、「[スコープ](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#scopes)」を参照してください。

注意：`email`スコープは権限が付与されていても`scope`プロパティの値としては返されません。

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
  "access_token": "bNl4YEFPI/hjFWhTqexp4MuEw5YPs...",
  "expires_in": 2592000,
  "id_token": "eyJhbGciOiJIUzI1NiJ9...",
  "refresh_token": "Aa1FdeggRhTnPNNpxr8p",
  "scope": "profile",
  "token_type": "Bearer"
}
```

<!-- tab end -->

### アクセストークンの有効性を検証する 

アクセストークンの有効性を検証します。

アクセストークンを利用して、安全にユーザー登録およびログインを処理する方法については、『LINEログインドキュメント』の「[アプリとサーバーの間で安全なログインプロセスを構築する](https://developers.line.biz/ja/docs/line-login/secure-login-process/)」を参照してください。

<!-- note start -->

**注意**

ここでは、LINEログイン v2.1のエンドポイントについて解説します。v2.0については、v2.0の「[アクセストークンの有効性を検証する](https://developers.line.biz/ja/reference/line-login-v2/#verify-access-token)」を参照してください。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET \
'https://api.line.me/oauth2/v2.1/verify?access_token=eyJhbGciOiJIUzI1NiJ9.UnQ_o-GP0VtnwDjbK0C8E_NvK...'
```

<!-- tab end -->

#### HTTPリクエスト 

`GET https://api.line.me/oauth2/v2.1/verify`

#### クエリパラメータ 

<!-- parameter start (props: required) -->

access_token

アクセストークン

<!-- parameter end -->

#### レスポンス 

アクセストークンが有効である場合は、HTTPステータスコード `200 OK` と、以下の情報を含むJSONオブジェクトが返されます。

<!-- parameter start -->

scope

String

アクセストークンに付与されている権限。スコープについて詳しくは、「[スコープ](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#scopes)」を参照してください。

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
  "scope": "profile",
  "client_id": "1440057261",
  "expires_in": 2591659
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
  "error_description": "access token expired"
}
```

<!-- tab end -->

### アクセストークンを更新する 

リフレッシュトークンを使って新しいアクセストークンを取得できます。

ユーザーの認証が終わったときに、アクセストークンと共にリフレッシュトークンが返されます。

<!-- note start -->

**注意**

- ここでは、LINEログイン v2.1のエンドポイントについて解説します。v2.0については、v2.0の「[アクセストークンを更新する](https://developers.line.biz/ja/reference/line-login-v2/#refresh-access-token)」を参照してください。
- Messaging APIで使用されるチャネルアクセストークンの更新には使用できません。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/oauth2/v2.1/token \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=refresh_token&refresh_token={your_refresh_token}&client_id={your_channel_id}&client_secret={your_channel_secret}'
```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://api.line.me/oauth2/v2.1/token`

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

grant_type

String

`refresh_token`

<!-- parameter end -->
<!-- parameter start (props: required) -->

refresh_token

String

再発行するアクセストークンに対応するリフレッシュトークン。アクセストークンが発行されてから最長90日間有効です。リフレッシュトークンの有効期限が切れた場合は、ユーザーに再度ログインを要求して新しいアクセストークンを生成する必要があります。

<!-- parameter end -->
<!-- parameter start (props: required) -->

client_id

String

チャネルID。[LINE Developersコンソール](https://developers.line.biz/console/)で確認できます。

<!-- parameter end -->
<!-- parameter start (props: annotation="説明を参照") -->

client_secret

String

チャネルシークレット。[LINE Developersコンソール](https://developers.line.biz/console/)で確認できます。

- アプリタイプが［**ウェブアプリ**］のみのチャネルでは必須です。
- アプリタイプが［**ネイティブアプリ**］かつ［**ウェブアプリ**］のチャネルでは無視されます。
- アプリタイプが［**ネイティブアプリ**］のみのチャネルでは無視されます。

<!-- parameter end -->

#### レスポンス 

アクセストークンの更新が成功すると、新しいアクセストークンとリフレッシュトークンが返されます。

<!-- parameter start -->

access_token

String

アクセストークン。有効期間は30日です。

<!-- parameter end -->
<!-- parameter start -->

token_type

String

`Bearer`

<!-- parameter end -->
<!-- parameter start -->

refresh_token

String

リクエスト時に`refresh_token`プロパティで指定したリフレッシュトークン。新しいアクセストークンを取得しても、リフレッシュトークンの有効期間は延長されません。

<!-- parameter end -->
<!-- parameter start -->

expires_in

Number

アクセストークンの有効期間。APIが呼び出された時点から期限切れまでの残り秒数で表されます。

<!-- parameter end -->
<!-- parameter start -->

scope

String

アクセストークンに付与されている権限。スコープについて詳しくは、「[スコープ](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#scopes)」を参照してください。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "token_type": "Bearer",
  "scope": "profile",
  "access_token": "bNl4YEFPI/hjFWhTqexp4MuEw...",
  "expires_in": 2591977,
  "refresh_token": "8iFFRdyxNVNLWYeteMMJ"
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
  "error_description": "invalid refresh token"
}
```

<!-- tab end -->

### アクセストークンを取り消す 

ユーザーのアクセストークンを無効にします。

<!-- note start -->

**注意**

- ここでは、LINEログイン v2.1のエンドポイントについて解説します。v2.0については、v2.0の「[アクセストークンを取り消す](https://developers.line.biz/ja/reference/line-login-v2/#revoke-access-token)」を参照してください。
- Messaging APIで使用されるチャネルアクセストークンの無効化には使用できません。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/oauth2/v2.1/revoke \
-H "Content-Type: application/x-www-form-urlencoded" \
-d "client_id={channel id}&client_secret={channel secret}&access_token={access token}"
```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://api.line.me/oauth2/v2.1/revoke`

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

access_token

String

アクセストークン

<!-- parameter end -->
<!-- parameter start (props: required) -->

client_id

String

チャネルID。[LINE Developersコンソール](https://developers.line.biz/console/)で確認できます。

<!-- parameter end -->
<!-- parameter start (props: annotation="説明を参照") -->

client_secret

String

チャネルシークレット。[LINE Developersコンソール](https://developers.line.biz/console/)で確認できます。

- アプリタイプが［**ウェブアプリ**］のみのチャネルでは必須です。
- アプリタイプが［**ネイティブアプリ**］かつ［**ウェブアプリ**］のチャネルでは無視されます。
- アプリタイプが［**ネイティブアプリ**］のみのチャネルでは無視されます。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と空のレスポンスボディを返します。

### 連動アプリに認可した権限を取り消す 

ユーザーが連動アプリに対して認可した権限を、ユーザーの代わりに取り消します。詳しくは、[LINEログイン開発ガイドライン](https://developers.line.biz/ja/docs/line-login/development-guidelines/)の必須事項である「[ユーザー退会時の連動アプリに対する権限取消](https://developers.line.biz/ja/docs/line-login/development-guidelines/#deauthorize)」を参照してください。

なお、LIFFアプリやLINEミニアプリもこのエンドポイントで権限を取り消すことができます。

連動アプリに対して認可した権限をユーザー自身が取り消す方法については、『LINEログインドキュメント』の「[ユーザーによる連動アプリの管理について](https://developers.line.biz/ja/docs/line-login/managing-authorized-apps/)」を参照してください。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/user/v1/deauthorize \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d '{
    "userAccessToken": "{user access token}"
}'
```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://api.line.me/user/v1/deauthorize`

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

利用できるチャネルアクセストークンの種類は、以下のとおりです。

- [任意の有効期間を指定できるチャネルアクセストークン（チャネルアクセストークンv2.1）](https://developers.line.biz/ja/docs/basics/channel-access-token/#user-specified-expiration)
- [ステートレスチャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/#stateless-channel-access-token)

チャネルアクセストークンの発行方法について詳しくは、『LINEプラットフォームの基礎知識』の「[チャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/)」を参照してください。

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

userAccessToken

String

対象ユーザーのアクセストークン

<!-- parameter end -->

#### レスポンス 

ステータスコード`204`と空のレスポンスボディを返します。

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | 対象ユーザーのアクセストークンが無効です。次のような理由が考えられます。<ul><li>ユーザーがアプリに対する権限を既に取り消している。</li><li>ユーザーに代わって、既にAPIでアプリに対する権限を取り消している。</li></ul> |

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 対象ユーザーのアクセストークンが無効な場合（400 Bad Request）
{
  "message": "invalid token"
}
```

<!-- tab end -->

### IDトークンを検証する 

IDトークンは、ユーザー情報を含むJSONウェブトークン（JWT）です。受信した[IDトークン](https://developers.line.biz/ja/docs/line-login/verify-id-token/#id-tokens)は、なりすましを狙った攻撃者が発行している可能性があります。受信したIDトークンが正規のものであることを確認し、ユーザーのプロフィール情報とメールアドレスを取得します。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST 'https://api.line.me/oauth2/v2.1/verify' \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'id_token=eyJraWQiOiIxNmUwNGQ0ZTU2NzgzYTc5MmRjYjQ2ODRkOD...' \
--data-urlencode 'client_id=1234567890'
```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://api.line.me/oauth2/v2.1/verify`

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

id_token

String

IDトークン

<!-- parameter end -->
<!-- parameter start (props: required) -->

client_id

String

期待されるチャネルID。LINEプラットフォームが発行した、チャネル固有の識別子。[LINE Developersコンソール](https://developers.line.biz/console/)で確認できます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

nonce

String

期待されるnonceの値。認可リクエストに指定したnonceの値を指定します。認可リクエストでnonceの値を指定しなかった場合は省略します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

user_id

String

期待されるユーザーID。ユーザーIDを取得する方法は、「[ユーザープロフィールを取得する](https://developers.line.biz/ja/reference/line-login/#get-user-profile)」を参照してください。

<!-- parameter end -->

#### レスポンス 

IDトークンの検証に成功した場合は、IDトークンのペイロード部分が返されます。

<!-- parameter start -->

iss

String

IDトークンの生成URL

<!-- parameter end -->
<!-- parameter start -->

sub

String

IDトークンの対象ユーザーID

<!-- parameter end -->
<!-- parameter start -->

aud

String

チャネルID

<!-- parameter end -->
<!-- parameter start -->

exp

Number

IDトークンの有効期限。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

iat

Number

IDトークンの生成時間。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

auth_time

Number

ユーザー認証時間。UNIX時間（秒）で返されます。認可リクエストにmax_ageの値を指定しなかった場合は含まれません。

<!-- parameter end -->
<!-- parameter start -->

nonce

String

認可URLに指定したnonceの値。認可リクエストにnonceの値を指定しなかった場合は含まれません。

<!-- parameter end -->
<!-- parameter start -->

amr

Array of strings

ユーザーが使用した認証方法のリスト。特定の条件下ではペイロードに含まれません。

以下のいずれかの値が含まれます。

- `pwd`：メールアドレスとパスワードによるログイン
- `lineautologin`：LINEによる自動ログイン（LINE SDKを使用した場合も含む）
- `lineqr`：QRコードによるログイン
- `linesso`：シングルサインオンによるログイン
- `mfa`：2要素認証によるログイン

<!-- parameter end -->
<!-- parameter start -->

name

String

ユーザーの表示名。認可リクエストに`profile`スコープを指定しなかった場合は含まれません。

<!-- parameter end -->
<!-- parameter start -->

picture

String

ユーザープロフィールの画像URL。認可リクエストに`profile`スコープを指定しなかった場合は含まれません。

<!-- parameter end -->
<!-- parameter start -->

email

String

ユーザーのメールアドレス。認可リクエストに`email`スコープを指定しなかった場合は含まれません。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "iss": "https://access.line.me",
  "sub": "U1234567890abcdef1234567890abcdef",
  "aud": "1234567890",
  "exp": 1504169092,
  "iat": 1504263657,
  "nonce": "0987654asdf",
  "amr": ["pwd"],
  "name": "Taro Line",
  "picture": "https://sample_line.me/aBcdefg123456",
  "email": "taro.line@example.com"
}
```

<!-- tab end -->

#### エラーレスポンス 

IDトークンの検証に失敗した場合は、JSONオブジェクトが返されます。

| error_description | 説明 |
| --- | --- |
| Invalid IdToken. | IDトークンの形式が正しくないか、署名が無効です。 |
| Invalid IdToken Issuer. | IDトークンが "https://access.line.me" 以外のサイトで生成されました。 |
| IdToken expired. | IDトークンの有効期限が切れました。 |
| Invalid IdToken Audience. | IDトークンのAudienceが、リクエストで指定したclient_idと異なります。 |
| Invalid IdToken Nonce. | IDトークンのNonceが、リクエストで指定したnonceと異なります。 |
| Invalid IdToken Subject Identifier. | IDトークンのSubjectIdentifierは、リクエストで指定したuser_idと異なります。 |

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
{
  "error": "invalid_request",
  "error_description": "Invalid IdToken."
}
```

<!-- tab end -->

### ユーザー情報を取得する 

ユーザーのユーザーID、表示名、プロフィール画像を取得します。「[ユーザープロフィールを取得する](https://developers.line.biz/ja/reference/line-login/#get-user-profile)」エンドポイントとは、アクセストークンに必要なスコープが異なります。

なお取得できる情報はメインプロフィールのみです。ユーザーの[サブプロフィール](https://developers.line.biz/ja/glossary/#subprofile)は取得できません。

<!-- note start -->

**注意**

`openid`のスコープを持つアクセストークンが必要です。詳しくは、『LINEログインドキュメント』の「[ユーザーに認証と認可を要求する](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#making-an-authorization-request)」と「[スコープ](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#scopes)」を参照してください。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/oauth2/v2.1/userinfo \
-H 'Authorization: Bearer {access token}'
```

<!-- tab end -->

#### HTTPリクエスト 

`GET https://api.line.me/oauth2/v2.1/userinfo`

`POST https://api.line.me/oauth2/v2.1/userinfo`

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{access token}`

<!-- parameter end -->

#### レスポンス 

<!-- parameter start -->

sub

String

ユーザーID

<!-- parameter end -->
<!-- parameter start -->

name

String

ユーザーの表示名。認可リクエストに`profile`スコープを指定しなかった場合は含まれません。

<!-- parameter end -->
<!-- parameter start -->

picture

String

ユーザープロフィールの画像URL。認可リクエストに`profile`スコープを指定しなかった場合は含まれません。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "sub": "U1234567890abcdef1234567890abcdef",
  "name": "Taro Line",
  "picture": "https://profile.line-scdn.net/0h8pWWElvzZ19qLk3ywQYYCFZraTIdAGEXEhx9ak56MDxDHiUIVEEsPBspMG1EGSEPAk4uP01t0m5G"
}
```

<!-- tab end -->

## プロフィール 

### ユーザープロフィールを取得する 

ユーザーのユーザーID、表示名、プロフィール画像、およびステータスメッセージを取得します。「[ユーザー情報を取得する](https://developers.line.biz/ja/reference/line-login/#userinfo)」エンドポイントとは、アクセストークンに必要なスコープが異なります。

なお取得できる情報はメインプロフィールのみです。ユーザーの[サブプロフィール](https://developers.line.biz/ja/glossary/#subprofile)は取得できません。

<!-- note start -->

**注意**

`profile`のスコープを持つアクセストークンが必要です。詳しくは、『LINEログインドキュメント』の「[ユーザーに認証と認可を要求する](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#making-an-authorization-request)」と「[スコープ](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#scopes)」を参照してください。

<!-- note end -->

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

| サフィックス | サムネイルサイズ |
| ------------ | ---------------- |
| `/large`     | 200 x 200        |
| `/small`     | 51 x 51          |

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
  "userId": "U4af4980629...",
  "displayName": "Brown",
  "pictureUrl": "https://profile.line-scdn.net/abcdefghijklmn",
  "statusMessage": "Hello, LINE!"
}
```

<!-- tab end -->

## 友だち関係 

### LINE公式アカウントとの友だち関係を取得する 

LINEログインのチャネルにリンクされているLINE公式アカウントと、ユーザーの友だち関係を取得します。

友だち追加オプションの使用方法について詳しくは、『LINEログインドキュメント』の「[LINEログインしたときにLINE公式アカウントを友だち追加する（友だち追加オプション）](https://developers.line.biz/ja/docs/line-login/link-a-bot/)」を参照してください。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/friendship/v1/status \
-H 'Authorization: Bearer {access token}'
```

<!-- tab end -->

#### HTTPリクエスト 

`GET https://api.line.me/friendship/v1/status`

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{access token}`

<!-- parameter end -->

<!-- note start -->

**注意**

`profile`のスコープを持つアクセストークンが必要です。詳しくは、『LINEログインドキュメント』の「[ユーザーに認証と認可を要求する](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#making-an-authorization-request)」と「[スコープ](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#scopes)」を参照してください。

<!-- note end -->

#### レスポンス 

<!-- parameter start -->

friendFlag

Boolean

- `true`：ユーザーがLINE公式アカウントを友だち追加済みで、ブロックしていない。
- `false`：それ以外の場合。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "friendFlag": true
}
```

<!-- tab end -->
