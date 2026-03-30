# 法人ユーザー向けオプションAPIリファレンス

<!-- note start -->

**オプション機能を利用するには手続きが必要です**

本ドキュメントに記載の機能は、所定の申請等を行った法人ユーザーのみがご利用いただけます。自社のLINE公式アカウントでご利用になりたいお客様は、担当営業までご連絡いただくか、[弊社パートナー](https://www.lycbiz.com/jp/partner/sales/)にお問い合わせください。

<!-- note end -->

<!-- table of contents -->

## 共通仕様 

### ステータスコード 

『Messaging APIリファレンス』の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」を参照してください。

### レスポンスヘッダー 

法人ユーザー向けオプションAPIのレスポンスには、以下のHTTPヘッダーが含まれます。

| レスポンスヘッダー | 説明                                               |
| ------------------ | -------------------------------------------------- |
| x-line-request-id  | リクエストID。各リクエストごとに発行されるIDです。 |

## ミッションスタンプAPI 

ミッションスタンプは、ミッションの達成を条件としてユーザーに提供するスタンプです。スタンプをインセンティブに、ユーザーに「ID情報の連携」や「会員登録」、「アンケート回答」などを促すことができます。

### ユーザーにミッションスタンプを提供する 

ミッションを達成したユーザーに、ミッションスタンプのダウンロード権限を付与します。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -X POST https://api.line.me/shop/v3/mission \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {channel access token}" \
-d '{
    "to": "U4af4980629...",
    "productType": "STICKER",
    "productId": "0000",
    "sendPresentMessage": false
}'
```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://api.line.me/shop/v3/mission`

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

to

String

ダウンロード権限を付与するユーザーのユーザーID

<!-- parameter end -->
<!-- parameter start (props: required) -->

productType

String

`STICKER`

<!-- parameter end -->
<!-- parameter start (props: required) -->

productId

String

スタンプセットのパッケージID

<!-- parameter end -->
<!-- parameter start (props: required) -->

sendPresentMessage

Boolean

`false`

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と空のレスポンスボディを返します。

#### エラーレスポンス 

エラー発生時は、エラーに応じたHTTPステータスコードと、以下のJSONデータを含むレスポンスボディが返されます。

<!-- parameter start -->

message

String

エラー情報を含むメッセージ。詳しくは、以下の「[エラーメッセージ](https://developers.line.biz/ja/reference/partner-docs/#send-mission-stickers-v3-error-messages)」を参照してください。

<!-- parameter end -->

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なユーザーIDを指定した場合（400 Bad Request）
{
  "message": "invalid request"
}
```

<!-- tab end -->

##### エラーメッセージ 

主なエラーのHTTPステータスコードと、JSONデータの`message`プロパティに含まれるエラーメッセージは以下のとおりです。

| コード | メッセージ | 説明 |
| --- | --- | --- |
| `400` | invalid request | `to`に指定した送信先のユーザーIDが無効です。 |
| `400` | illegal argument | `productId`に指定したスタンプセットがミッションスタンプとして設定されていません。 |
| `400` | not in sales period | `productId`に指定したスタンプセットが有効期間外です。 |
| `400` | sticker set not available for channel | チャネルに`productId`で指定したスタンプセットを利用するための権限がありません。 |
| `400` | not available | 次のいずれかの理由により`to`に指定したユーザーにはミッションスタンプを付与できません。<ul><li>`to`に指定した送信先のユーザーの国または地域では、`productId`に指定したスタンプセットが利用できません。</li><li>`to`に指定した送信先のユーザーが利用している端末は、`productId`に指定したスタンプセットに対応していません。</li><li>`to`に指定した送信先のユーザーが利用しているLINEアプリのバージョンは、`productId`に指定したスタンプセットに対応していません。</li></ul> |
| `403` | not allowed to use the API | チャネルに、ミッションスタンプAPIの利用権限が付与されていません。 |
| `404` | not found | `productId`に指定したスタンプセットが存在しません。 |
| `500` | internal error | 内部サーバーのエラーです。しばらく待ってからリクエストを再試行してください。 |
| `502` | upstream error | 内部ネットワークのエラーです。しばらく待ってからリクエストを再試行してください。 |

## 既読API（旧） 

### ユーザーからのメッセージに既読を付ける 

特定のユーザーから送信されたすべてのメッセージに「既読」を表示できます。

<!-- tip start -->

**既読をつける新しいエンドポイントを使用してください**

既読API（旧）は引き続き使用できますが、ユーザーからのメッセージに既読をつける処理をこれから実装する場合は、Messaging APIの「[メッセージに既読をつける](https://developers.line.biz/ja/reference/messaging-api/#mark-as-read)」エンドポイントを使用してください。「メッセージに既読をつける」エンドポイントは申請なしに使用でき、またチャット機能との併用も可能です。

<!-- tip end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/message/markAsRead \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {channel_access_token}' \
-d '{
    "chat": {
        "userId": "Uxxxxxxxxxxxxxxxxxx"
    }
}'
```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://api.line.me/v2/bot/message/markAsRead`

#### レート制限 

2,000リクエスト/秒

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

chat.userId

String

対象のユーザーID。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と空のJSONオブジェクトを返します。

_レスポンスの例_

<!-- tab start `json` -->

```json
{}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明                                 |
| ------ | ------------------------------------ |
| `400`  | 無効なユーザーIDが指定されています。 |

詳しくは、『Messaging APIリファレンス』の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なユーザーIDを指定した場合（400 Bad Request）
{
  "message": "The property, 'chat.chatId', in the request body is invalid (line: -, column: -)"
}
```

<!-- tab end -->

## モジュール 

### モジュールチャネルの提供者の操作で連携（アタッチ）する 

モジュールチャネルをLINE公式アカウントにアタッチします。アタッチするためには、LINE公式アカウントの管理者に認可を要求し、認可コードを取得する必要があります。モジュールの認可フローについて詳しくは、『モジュールドキュメント』の「[モジュールチャネルを連携（アタッチ）する](https://developers.line.biz/ja/docs/partner-docs/module-technical-attach-channel/)」を参照してください。

このAPIを利用する際には、`Authorization`ヘッダーもしくはリクエストボディのどちらかを使って、モジュールチャネルのチャネルIDとチャネルシークレットを指定する必要があります。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://manager.line.biz/module/auth/v1/token \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=authorization_code' \
-d 'code=1234567890abcde' \
--data-urlencode 'redirect_uri=https://example.com/auth?key=value' \
-d 'code_verifier=ayjtZgTunh96nHCvgLEiXzqVQOOC0SwMRs39bh1l5dx' \
-d 'client_id=1234567890' \
-d 'client_secret=1234567890abcdefghij1234567890ab' \
-d 'region=JP' \
-d 'basic_search_id=@linedevelopers' \
-d 'scope=message%3Asend%20message%3Areceive' \
-d 'brand_type=premium'
```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://manager.line.biz/module/auth/v1/token`

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

`application/x-www-form-urlencoded`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

Authorization

`Basic {base64({Channel ID}:{Channel Secret})}`

`{base64({Channel ID}:{Channel Secret})}`には、「モジュールチャネルのチャネルID」と「モジュールチャネルのチャネルシークレット」を`:`で連結し、Base64でエンコードした文字列を指定してください。モジュールチャネルのチャネルIDとチャネルシークレットは、[LINE Developersコンソール](https://developers.line.biz/console/)で確認できます。

リクエストボディ内で`client_id`および`client_secret`を指定する代わりに、このヘッダを使ってモジュールチャネルのチャネルIDとチャネルシークレットを指定できます。

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

LINEプラットフォームから渡された[認可コード](https://developers.line.biz/ja/docs/partner-docs/module-technical-attach-channel/#receive-authorization-code)を指定します。

<!-- parameter end -->
<!-- parameter start (props: required) -->

redirect_uri

String

[認証と認可のためのURL](https://developers.line.biz/ja/docs/partner-docs/module-technical-attach-channel/#request-auth-from-line-oa-admin-query-parameters)で指定した`redirect_uri`を指定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

code_verifier

String

認可コード横取り攻撃への対策としてOAuth 2.0の拡張仕様で定義されるPKCE（Proof Key for Code Exchange）を利用した場合に指定します。

[RFC 7636](https://datatracker.ietf.org/doc/html/rfc7636)に準拠しています。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

client_id

String

`Authorization`ヘッダーを使用する代わりに、このパラメータを使ってモジュールチャネルのチャネルIDを指定できます。 モジュールチャネルのチャネルIDは、[LINE Developersコンソール](https://developers.line.biz/console/)で確認できます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

client_secret

String

`Authorization`ヘッダーを使用する代わりに、このパラメータを使ってモジュールチャネルのチャネルシークレットを指定できます。モジュールチャネルのチャネルシークレットは、[LINE Developersコンソール](https://developers.line.biz/console/)で確認できます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

region

String

[認証と認可のためのURL](https://developers.line.biz/ja/docs/partner-docs/module-technical-attach-channel/#request-auth-from-line-oa-admin-query-parameters)で`region`に値を指定した場合、同じ値を指定してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

basic_search_id

String

認証と認可のためのURLで`basic_search_id`に値を指定した場合、同じ値を指定してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

scope

String

認証と認可のためのURLで`scope`に値を指定した場合、同じ値を指定してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

brand_type

String

認証と認可のためのURLで`brand_type`に値を指定した場合、同じ値を指定してください。

<!-- parameter end -->

#### レスポンス 

成功時は、ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

bot_id

String

LINE公式アカウントのボットのユーザーID。

ボットのユーザーIDは、[Messaging API](https://developers.line.biz/ja/reference/messaging-api/)や[Acquire Control API](https://developers.line.biz/ja/reference/partner-docs/#acquire-control-api)を呼び出す際に利用します。

<!-- note start -->

**注意**

ボットのユーザーIDは、[LINE Developersコンソール](https://developers.line.biz/console/)で、Messaging APIチャネルの［**チャネル基本設定**］タブに表示される［**あなたのユーザーID**］ではありません。

<!-- note end -->

<!-- parameter end -->
<!-- parameter start -->

scope

String

LINE公式アカウントの管理者によって許可された権限（スコープ）。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "bot_id": "U45c5c51f0050ef0f0ee7261d57fd3c56",
  "scopes": [
    "message:send",
    "message:receive"
  ]
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードを返します。

- `400 Bad Request`
- `403 Forbidden`

### モジュールチャネルの管理者の操作でモジュールチャネルを連携解除（デタッチ）する 

LINE公式アカウントからモジュールチャネルをデタッチします。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/channel/detach \
-H 'Content-Type:application/json' \
-H 'Authorization: Bearer {channel access token}' \
-d '{"botId":"U45c5c51f0050ef0f0ee7261d57fd3c56"}'
```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://api.line.me/v2/bot/channel/detach`

#### レート制限 

2,000リクエスト/秒

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

`application/json`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

`Bearer {channel access token}`

`{channel access token}`には、モジュールチャネルのチャネルアクセストークンを指定してください。

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

botId

String

モジュールチャネルにアタッチされたLINE公式アカウントのボットのユーザーID。

ボットのユーザーIDは、「[モジュールチャネルの提供者の操作で連携（アタッチ）する](https://developers.line.biz/ja/reference/partner-docs/#link-attach-by-operation-module-channel-provider)」のレスポンスや[Attachedイベント](https://developers.line.biz/ja/reference/partner-docs/#attached-event)で取得できます。

<!-- parameter end -->

#### レスポンス 

成功時は、ステータスコード`200`を返します。

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | モジュールチャネルを連携解除（デタッチ）できませんでした。次のような理由が考えられます。<ul><li>無効なボットのユーザーIDが指定されている。</li><li>存在しないボットが指定されている。</li><li>モジュールチャネルが連携（アタッチ）されていない。</li><li>モジュールチャネルではないチャネルのチャネルアクセストークンが指定されている。</li></ul> |

詳しくは、『Messaging APIリファレンス』の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なボットのユーザーIDを指定した場合（400 Bad Request）
{
  "message": "user/group/room Id is not available."
}

// モジュールチャネルが連携（アタッチ）されていない場合（400 Bad Request）
{
  "message": "Specified channel is not detachable"
}
```

<!-- tab end -->

### Acquire Control API 

Standby Channelが主導権（Chat Control）を取得する場合は、Acquire Control APIを呼び出します。

それまでActive Channelだったチャネルは、自動的にStandby Channelに切り替わります。

<!-- warning start -->

**警告**

現在提供しているモジュールの仕組みにおいては、本APIを呼び出す必要はありません。そのため本APIの実装は任意となります。

本APIは現状、想定外の問題等によりチャットの主導権が切り替わった際にのみ利用します。

<!-- warning end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/chat/{chatId}/control/acquire \
-H 'Content-Type:application/json' \
-H 'Authorization: Bearer {channel access token}' \
-H 'ボットのユーザーIDを指定するヘッダー:xxxxxx' \
-d '{"expired":true,"ttl":3600}'
```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://api.line.me/v2/bot/chat/{chatId}/control/acquire`

#### レート制限 

2,000リクエスト/秒

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

`application/json`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

`Bearer {channel access token}`

`{channel access token}`には、モジュールチャネルのチャネルアクセストークンを指定してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

ボットのユーザーIDを指定するヘッダー

モジュールチャネルにアタッチされたLINE公式アカウントのボットのユーザーID。

ボットのユーザーIDは、「[モジュールチャネルの提供者の操作で連携（アタッチ）する](https://developers.line.biz/ja/reference/partner-docs/#link-attach-by-operation-module-channel-provider)」のレスポンスや[Attachedイベント](https://developers.line.biz/ja/reference/partner-docs/#attached-event)で取得できます。

<!-- note start -->

**ヘッダーの詳細については参画される際に別途提供いたします**

本ヘッダーの名前（パラメーター名）は、実際に[LINEマーケットプレイス](https://line-marketplace.com/jp/inquiry)に参画するお客様に限定して公開しています。

<!-- note end -->

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

chatId

`userId`、`roomId`、または`groupId`

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: optional) -->

expired

Boolean

- `True`：制限時間（ttl）を経過すると、主導権（Chat Control）がPrimary Channelに戻ります。（デフォルト）
- `False`：制限時間がなく、主導権（Chat Control）は時間経過では変わりません。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

ttl

Number

主導権（Chat Control）がPrimary Channelに戻るまでの時間（モジュールチャネルがActive Channelでいられる時間）。秒で指定します。最大値は1年間（3600 \* 24 \* 365）。デフォルト値は`3600`（1時間）です。

※`expired`の値が`false`の場合は、無視されます。

<!-- parameter end -->

#### レスポンス 

成功時は、ステータスコード`200`を返します。

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | `chatId`パラメータに、不正なIDが指定されています。 |
| `404` | 主導権（Chat Control）を取得できませんでした。次のような理由が考えられます。<ul><li>モジュールと連携しているLINE公式アカウントを友だち追加していないユーザーが指定されている。</li><li>モジュールと連携しているLINE公式アカウントが参加していないグループが指定されている。</li><li>モジュールと連携しているLINE公式アカウントが参加していない複数人トークが指定されている。</li></ul> |
| `423` | 別のチャネルが、一定期間内（数秒程度）に主導権（Chat Control）を取得していた場合。 |

詳しくは、『Messaging APIリファレンス』の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// chatIdパラメータに不正なIDを指定した場合（400 Bad Request）
{
  "message": "The value for the 'chatId' parameter is invalid"
}
```

<!-- tab end -->

### Release Control API 

Active Channelが持っている主導権（Chat Control）を、Primary Channelに返却する場合は、Release Control APIを呼び出します。

<!-- warning start -->

**警告**

現在提供しているモジュールの仕組みにおいては、本APIを呼び出す必要はありません。そのため本APIの実装は任意となります。

本APIは現状、想定外の問題等によりチャットの主導権が切り替わった際にのみ利用します。

<!-- warning end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/chat/{chatId}/control/release \
-H 'Content-Type:application/json' \
-H 'Authorization: Bearer {channel access token}' \
-H 'ボットのユーザーIDを指定するヘッダー:xxxxxx'
```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://api.line.me/v2/bot/chat/{chatId}/control/release`

#### レート制限 

2,000リクエスト/秒

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

`application/json`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

`Bearer {channel access token}`

`{channel access token}`には、モジュールチャネルのチャネルアクセストークンを指定してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

ボットのユーザーIDを指定するヘッダー

モジュールチャネルにアタッチされたLINE公式アカウントのボットのユーザーID。

ボットのユーザーIDは、「[モジュールチャネルの提供者の操作で連携（アタッチ）する](https://developers.line.biz/ja/reference/partner-docs/#link-attach-by-operation-module-channel-provider)」のレスポンスや[Attachedイベント](https://developers.line.biz/ja/reference/partner-docs/#attached-event)で取得できます。

<!-- note start -->

**ヘッダーの詳細については参画される際に別途提供いたします**

本ヘッダーの名前（パラメーター名）は、実際に[LINEマーケットプレイス](https://line-marketplace.com/jp/inquiry)に参画するお客様に限定して公開しています。

<!-- note end -->

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

chatId

`userId`、`roomId`、または`groupId`

<!-- parameter end -->

#### レスポンス 

成功時は、ステータスコード`200`を返します。

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明                                               |
| ------ | -------------------------------------------------- |
| `400`  | `chatId`パラメータに、不正なIDが指定されています。 |

詳しくは、『Messaging APIリファレンス』の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// chatIdパラメータに不正なIDを指定した場合（400 Bad Request）
{
  "message": "The value for the 'chatId' parameter is invalid"
}
```

<!-- tab end -->

### モジュールチャネル専用のWebhookイベントオブジェクト 

#### Attachedイベント 

モジュールチャネルが、LINE公式アカウントにアタッチされたことを示すイベントです。モジュールチャネルのWebhook URLサーバーに送信されます。

<!-- parameter start -->

timestampなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

ただし、`mode`は`active`固定です。

<!-- parameter end -->
<!-- parameter start -->

type

String

`module`

<!-- parameter end -->
<!-- parameter start -->

module.type

String

`attached`

<!-- parameter end -->
<!-- parameter start -->

module.botId

String

アタッチされたLINE公式アカウントのボットのユーザーID

<!-- parameter end -->
<!-- parameter start -->

module.scopes

Array of strings

LINE公式アカウントの管理者によって許可されたスコープを示す文字列の配列です。

<!-- parameter end -->

_Attachedイベントの例_

<!-- tab start `json` -->

```sh
{
  "destination": "U53387d54817...",
  "events": [
    {
      "type": "module",
      "module": {
        "type": "attached",
        "botId": "U53387d54817...",
        "scopes": [
          "message:send",
          "message:receive"
        ]
      },
      "webhookEventId": "01G3GCEEXNWREGSSFVTPYH8465",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1653038594997,
      "mode": "active"
    }
  ]
}
```

<!-- tab end -->

#### Detachedイベント 

モジュールチャネルが、LINE公式アカウントからデタッチされたことを示すイベントです。モジュールチャネルのWebhook URLサーバーに送信されます。

<!-- note start -->

**LINE公式アカウントを削除する操作をしたときにはDetachされません**

LINE Official Account ManagerでLINE公式アカウントを削除する操作をしたときは、モジュールチャネルはデタッチされません。

削除する操作をしてから3か月が経過し、LINE公式アカウントの分析データを含むすべての情報が完全に削除されると、自動的にデタッチされます。

<!-- note end -->

<!-- parameter start -->

timestampなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

ただし、`mode`は`active`固定です。

<!-- parameter end -->
<!-- parameter start -->

type

String

`module`

<!-- parameter end -->
<!-- parameter start -->

module.type

String

`detached`

<!-- parameter end -->
<!-- parameter start -->

module.botId

String

連携解除されたLINE公式アカウントのボットのユーザーID

<!-- parameter end -->
<!-- parameter start -->

module.reason

String

連携解除された理由

`bot_deleted`：LINE公式アカウントの分析データを含むすべての情報が完全に削除されました。

<!-- parameter end -->

_Detachedイベントの例_

<!-- tab start `json` -->

```sh
{
  "destination": "U5fac33f633e72c192759f09afc41fa28",
  "events": [
    {
      "type": "module",
      "module": {
        "type": "detached",
        "botId": "U5fac33f633e72c192759f09afc41fa28"
      },
      "webhookEventId": "01G4CPSV08QGNT1DWFC4DSWDNP",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1653988977672,
      "mode": "active"
    }
  ]
}
```

<!-- tab end -->

#### Activatedイベント 

Acquire Control APIを呼び出して、モジュールチャネルがActive Channelに切り替わったことを示すイベントです。モジュールチャネルのWebhook URLサーバーに送信されます。

<!-- note start -->

**注意**

Acquire Control APIで指定した有効期間が過ぎて、主導権（Chat Control）が切り替わった場合は、Activatedイベントは送信されません。

<!-- note end -->

<!-- parameter start -->

timestamp、sourceなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

ただし、`mode`は`active`固定です。

<!-- parameter end -->
<!-- parameter start -->

type

String

`activated`

<!-- parameter end -->
<!-- parameter start -->

chatControl.expireAt

Number

“active”が維持される期限。

<!-- parameter end -->

_Activatedイベントの例_

<!-- tab start `json` -->

```sh
  {
  "destination": "U5fac33f633e72c192759f09afc41fa28",
  "events": [
    {
      "type": "activated",
      "chatControl": {
        "expireAt": 1653994422933
      },
      "webhookEventId": "01G4CRJ54J7TT4WN190KKHBXXT",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1653990823058,
      "source": {
        "type": "user",
        "userId": "LUb577ef3cbe..."
      },
      "mode": "active"
    }
  ]
}
```

<!-- tab end -->

#### Deactivatedイベント 

Acquire Control APIまたはRelease Control APIを呼び出して、モジュールチャネルがStandby Channelに切り替わったことを示すイベントです。モジュールチャネルのWebhook URLサーバーに送信されます。

<!-- note start -->

**注意**

Acquire Control APIで指定した有効期間が過ぎて、主導権（Chat Control）が切り替わった場合は、Deactivatedイベントは送信されません。

<!-- note end -->

<!-- parameter start -->

timestamp、sourceなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

ただし、`mode`は`active`固定です。

<!-- parameter end -->
<!-- parameter start -->

type

String

`deactivated`

<!-- parameter end -->

_Deactivatedイベントの例_

<!-- tab start `json` -->

```sh
{
  "destination": "U5fac33f633e72c192759f09afc41fa28",
  "events": [
    {
      "type": "deactivated",
      "webhookEventId": "01G4CRJ51100K1D1791KC9J4G4",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1653990822945,
      "source": {
        "type": "user",
        "userId": "LUb577ef3cbe..."
      },
      "mode": "active"
    }
  ]
}
```

<!-- tab end -->

#### botSuspendイベント 

LINE公式アカウントが一時停止状態（Suspend）になったことを示すイベントです。モジュールチャネルのWebhook URLサーバーに送信されます。

このイベントを受信したときは、以下のような処理を行うことを推奨します。

- モジュールチャネルの管理画面に「LINE公式アカウントが利用できない状態になっているため、この管理画面は利用できません」といったメッセージを表示し、管理画面の利用を停止する。
- いったん一時停止状態になっても、一時停止状態から復帰する可能性（botResumeイベントを受信する可能性）があります。すべての情報を保持しておくことを推奨します。

<!-- note start -->

**注意**

Primary ChannelにはbotSuspendイベントは送信されません。

botSuspendイベントを受信したあとでDetachedイベントを受信した場合は、LINE公式アカウントがモジュールチャネルの利用を停止し、契約を解除したことを示します。

<!-- note end -->

<!-- parameter start -->

timestampなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

ただし、`mode`は`active`固定です。

<!-- parameter end -->
<!-- parameter start -->

type

String

`botSuspended`

<!-- parameter end -->

_botSuspendイベントの例_

<!-- tab start `json` -->

```sh
{
  "destination": "U53387d548170020e6cedef5f41d1e01d",
  "events": [
    {
      "type": "botSuspended",
      "webhookEventId": "01G4CRJ54J7TT4WN190KKHBXXT",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1616390574119,
      "mode": "active"
    }
  ]
}
```

<!-- tab end -->

#### botResumedイベント 

LINE公式アカウントが一時停止状態から復帰したことを示すイベントです。モジュールチャネルのWebhook URLサーバーに送信されます。

このイベントを受信したときは、モジュールチャネルの管理画面で「LINE公式アカウントが利用できない状態になっているため、この管理画面は利用できません」といったメッセージを非表示にし、管理画面の利用を再開することを推奨します。

<!-- note start -->

**注意**

Primary ChannelにはbotResumedイベントは送信されません。

<!-- note end -->

<!-- parameter start -->

timestampなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

ただし、`mode`は`active`固定です。

<!-- parameter end -->
<!-- parameter start -->

type

String

`botResumed`

<!-- parameter end -->

_botResumedイベントの例_

<!-- tab start `json` -->

```sh
{
  "destination": "U5fac33f633e72c192759f09afc41fa28",
  "events": [
    {
      "type": "botResumed",
      "webhookEventId": "01G4CS8T91R1V1JCE0G43DQND8",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1653991565601,
      "mode": "active"
    }
  ]
}
```

<!-- tab end -->

### モジュールをアタッチしたボットのリストを取得する 

モジュールチャネルをアタッチした、複数のLINE公式アカウントのボットの基本情報をリストで取得します。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET "https://api.line.me/v2/bot/list?limit={limit}&start={continuationToken}" \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### HTTPリクエスト 

`GET https://api.line.me/v2/bot/list?limit={limit}&start={continuationToken}`

#### レート制限 

2,000リクエスト/秒

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

`Bearer {channel access token}`

`{channel access token}`には、モジュールチャネルのチャネルアクセストークンを指定してください。

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: optional) -->

limit

基本情報を取得するボットの最大個数を指定します。デフォルト値は`100`です。\
最大値：`100`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

start

継続トークンの値。レスポンスで返されるJSONオブジェクトの`next`プロパティに含まれます。1回のリクエストでボットの基本情報をすべて取得できない場合は、このパラメータを指定して残りの配列を取得します。

<!-- parameter end -->

#### レスポンス 

成功時は、ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

bots

Array

ボットの基本情報を表すBot list Item objectの配列。

<!-- parameter end -->
<!-- parameter start -->

bots\[].userId

String

ボットのユーザーID

<!-- parameter end -->
<!-- parameter start -->

bots\[].basicId

String

ボットのベーシックID

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

bots\[].premiumId

String

ボットの[プレミアムID](https://developers.line.biz/ja/glossary/#premium-id)。プレミアムIDが未設定の場合、この値は含まれません。

<!-- parameter end -->
<!-- parameter start -->

bots\[].displayName

String

ボットの表示名

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

bots\[].pictureUrl

String

プロフィール画像のURL。「https://」から始まる画像URLです。ボットにプロフィール画像を設定していない場合は、レスポンスに含まれません。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

next

String

継続トークン。ボットの基本情報の、次の配列を取得するために使用します。このプロパティは、取得しきれなかったボットの基本情報が存在する場合にのみ返されます。

継続トークンの有効期間は24時間（86,400秒間）です。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "bots": [
    {
      "userId": "Uf2dd6e8b081d2ff9c05c98a8a8b269c9",
      "basicId": "@628...",
      "displayName": "Test01",
      "pictureUrl": "https://profile.line-scdn.net/0hyxytJNAlJldEDQzlatVZAHhIKDoz..."
    },
    {
      "userId": "Ua831d37bfe8232808202b85127663f70",
      "basicId": "@076lu...",
      "displayName": "Test02",
      "pictureUrl": "https://profile.line-scdn.net/0hohnizdyzMEdTECbnVo9PEG9VPiok..."
    },
    {
      "userId": "Ub77ea431fba86f7c159a0c0f5be43d9f",
      "basicId": "@290n...",
      "displayName": "Test03"
    },
    {
      "userId": "Ub8ec80a14e879e9c6833fb4cee0e632b",
      "basicId": "@793j...",
      "displayName": "Test04"
    }
  ]
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明                                   |
| ------ | -------------------------------------- |
| `400`  | 無効な継続トークンが指定されています。 |

詳しくは、『Messaging APIリファレンス』の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 有効期限切れなどの無効な継続トークンを指定した場合（400 Bad Request）
{
  "message": "Invalid start param"
}
```

<!-- tab end -->
