# LINE通知メッセージAPIリファレンス

<!-- note start -->

**オプション機能を利用するには手続きが必要です**

本ドキュメントに記載の機能は、所定の申請等を行った法人ユーザーのみがご利用いただけます。自社のLINE公式アカウントでご利用になりたいお客様は、担当営業までご連絡いただくか、[弊社パートナー](https://www.lycbiz.com/jp/partner/sales/)にお問い合わせください。

<!-- note end -->

<!-- table of contents -->

## 共通仕様 

### ステータスコード 

『Messaging APIリファレンス』の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」を参照してください。

### レスポンスヘッダー 

LINE通知メッセージAPIのレスポンスには、以下のHTTPヘッダーが含まれます。

| レスポンスヘッダー | 説明                                               |
| ------------------ | -------------------------------------------------- |
| x-line-request-id  | リクエストID。各リクエストごとに発行されるIDです。 |

## LINE通知メッセージ（テンプレート） 

- [LINE通知メッセージ（テンプレート）を送る](https://developers.line.biz/ja/reference/line-notification-messages/#send-line-notification-message-template)
- [送信済みのLINE通知メッセージ（テンプレート）の数を取得する](https://developers.line.biz/ja/reference/line-notification-messages/#get-number-of-sent-line-notification-messages-template)

### LINE通知メッセージ（テンプレート）を送る 

ユーザーの電話番号を指定してLINE通知メッセージ（テンプレート）を送るAPIです。

詳しくは、『LINE通知メッセージドキュメント』の「[LINE通知メッセージ（テンプレート）](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/template/)」を参照してください。

<!-- warning start -->

**リクエスト元IPアドレスの制限はしないでください**

LINE通知メッセージを送る場合、Messaging APIチャネルの［**セキュリティ設定**］タブで、LINEプラットフォームのAPIを呼び出せるサーバーのIPアドレスを登録しないでください。リクエスト元のIPアドレスを制限した状態でLINE通知メッセージを送ると、送信に失敗することがあります。

リクエスト元のIPアドレスを制限しているか確認する方法については、『Messaging APIドキュメント』の「[長期のチャネルアクセストークン利用時にAPIの呼び出し元を制限する（任意）](https://developers.line.biz/ja/docs/messaging-api/building-bot/#configure-security-settings)」を参照してください。

<!-- warning end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/message/pnp/templated/push \
-H 'Authorization: Bearer {channel_access_token}' \
-H 'Content-Type:application/json' \
-H 'X-Line-Delivery-Tag:15034552939884E28681A7D668CEA94C147C716C0EC9DFE8B80B44EF3B57F6BD0602366BC3menu01' \
-d '{
    "to": "c9fb9ae95bff879cbcdfc9edf6716640bc40841f3b7352140daa1431af4c319e",
    "templateKey": "shipment_completed_ja",
    "body": {
        "emphasizedItem": {
            "itemKey": "date_002_ja",
            "content": "2024年8月10日(土)"
        },
        "items": [
            {
                "itemKey": "time_range_001_ja",
                "content": "午前中"
            },
            {
                "itemKey": "number_001_ja",
                "content": "1234567"
            },
            {
                "itemKey": "price_001_ja",
                "content": "12,000円"
            },
            {
                "itemKey": "name_010_ja",
                "content": "スープセット（冷凍）"
            }
        ],
        "buttons": [
            {
                "buttonKey": "check_delivery_status_ja",
                "url": "https://example.com/CheckDeliveryStatus/"
            },
            {
                "buttonKey": "contact_ja",
                "url": "https://example.com/ContactUs/"
            }
        ]
    }
}'
```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://api.line.me/v2/bot/message/pnp/templated/push`

#### レート制限 

2,000リクエスト/秒

#### リクエストヘッダー 

<!-- note start -->

**サポートしていない機能**

LINE通知メッセージAPIでは、[リトライキー](https://developers.line.biz/ja/reference/messaging-api/#retry-api-request)（`X-Line-Retry-Key`）を使ったAPIリクエストの再試行はできません。

<!-- note end -->

<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

X-Line-Delivery-Tag

Webhookを介して、[配信完了イベント](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#receive-delivery-event)の`delivery.data`プロパティで返される文字列。詳しくは、「[メッセージの送信通知を受信する](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#receive-delivery-event)」を参照してください。\
最小文字数：16\
最大文字数：100

<!-- parameter end -->

_X-Line-Delivery-Tagの例_

<!-- tab start `shell` -->

```sh
15034552939884E28681A7D668CEA94C147C716C0EC9DFE8B80B44EF3B57F6BD0602366BC3menu01
```

<!-- tab end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

to

String

メッセージの送信先。[E.164](https://developers.line.biz/ja/glossary/#e164)形式に正規化し[SHA256でハッシュ化した電話番号](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#phone-number-hashed)を指定してください。

メッセージの送信条件について詳しくは、「[LINE通知メッセージが送信される条件](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#conditions-for-sending-line-notification-messages)」を参照してください。

<!-- note start -->

**注意**

- [グループトークと複数人トーク](https://developers.line.biz/ja/docs/messaging-api/group-chats/#group-chat-types)は送信対象として指定できません。
- 複数の電話番号を送信対象として指定することはできません。

<!-- note end -->

<!-- parameter end -->
<!-- parameter start (props: required) -->

templateKey

String

使用するテンプレートの`Key`を指定します。

使用できる`Key`は、「[テンプレート](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/template/#templates)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

body

Object

送信するテンプレートのボディオブジェクト。3つのオブジェクトでメッセージに含める内容を指定します。1つのメッセージ内で、同じアイテムを重複して指定することはできません。

- `emphasizedItem`：強調したい[アイテム](https://developers.line.biz/ja/reference/line-notification-messages/#send-line-notification-message-template-items)
- `items`：[アイテム](https://developers.line.biz/ja/reference/line-notification-messages/#send-line-notification-message-template-items)の配列
- `buttons`：[ボタン](https://developers.line.biz/ja/reference/line-notification-messages/#send-line-notification-message-template-buttons)の配列

<!-- parameter end -->
<!-- parameter start (props: optional) -->

body.emphasizedItem

Object

メッセージで強調する[アイテム](https://developers.line.biz/ja/reference/line-notification-messages/#send-line-notification-message-template-items)を指定します。\
最大オブジェクト数：1

<!-- parameter end -->
<!-- parameter start (props: optional) -->

body.items

Array of objects

メッセージに含める[アイテム](https://developers.line.biz/ja/reference/line-notification-messages/#send-line-notification-message-template-items)の配列を指定します。\
最小オブジェクト数：0\
最大オブジェクト数：15

<!-- parameter end -->
<!-- parameter start (props: optional) -->

body.buttons

Array of objects

メッセージに含める[ボタン](https://developers.line.biz/ja/reference/line-notification-messages/#send-line-notification-message-template-buttons)の配列を指定します。\
最小オブジェクト数：0\
最大オブジェクト数：2

<!-- parameter end -->

##### アイテム 

<!-- parameter start (props: required) -->

itemKey

String

使用するアイテムの`Key`を指定します。

使用できる`Key`は、「[アイテム](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/template/#items)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

content

String

アイテムの値として表示する文字列を指定します。\
最大文字数：`body.emphasizedItem`の場合は15、`body.items`の場合は300

<!-- parameter end -->

_アイテムの例_

<!-- tab start `json` -->

```json
{
  "itemKey": "time_range_001_ja",
  "content": "午前中"
}
```

<!-- tab end -->

##### ボタン 

<!-- parameter start (props: required) -->

buttonKey

String

使用するボタンの`Key`を指定します。

使用できる`Key`は、「[ボタン](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/template/#buttons)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

url

String

ボタンを押すと遷移するURLを指定します。\
最大文字数：1000

<!-- parameter end -->

_ボタンの例_

<!-- tab start `json` -->

```json
{
  "buttonKey": "contact_ja",
  "url": "https://example.com/ContactUs/"
}
```

<!-- tab end -->

#### レスポンス 

ステータスコード`202`と空のJSONオブジェクトを返します。

_レスポンスの例_

<!-- tab start `json` -->

```json
{}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>メッセージの送信先が無効です。</li><li>無効なメッセージオブジェクトが指定されています。</li><li>このLINE公式アカウントでは指定したテンプレートは使用できません。</li></ul> |
| `403` | このエンドポイントを使う権限がありません。 |
| `422` | LINE通知メッセージ（テンプレート）の送信に失敗しました。以下のような理由が考えられます。<ul><li>メッセージ送信対象に指定した電話番号に紐づくLINEユーザーが存在しません。</li><li>メッセージ送信対象に指定した電話番号は、LINE通知メッセージのサービス対象国で発行されたものではありません。詳しくは、「[LINE通知メッセージが送信される条件](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#conditions-for-sending-line-notification-messages)」を参照してください。</li><li>メッセージ送信対象に指定した電話番号に紐づくLINEユーザーが[LINE通知メッセージの受信を拒否](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#how-to-consent-for-line-notification-messages)しています。</li><li>メッセージ送信対象に指定した電話番号に紐づくLINEユーザーは、[LINEのプライバシーポリシー（2022年3月改定）](https://guide.line.me/privacy-policy_update/2022/0001/?lang=ja-jp)に同意していません。</li></ul> |

詳しくは、『Messaging APIリファレンス』の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 存在しない、または使用する権限がないテンプレートを指定した場合（400 Bad Request）
{
  "message": "Invalid templateKey: reserve_004",
  "details": [
    {
      "message": "The specified template doesn't exist, or you don't have the permission",
      "property": "templateKey"
    }
  ]
}

// 存在しないアイテムを指定した場合（400 Bad Request）
{
  "message": "The request body has 1 invalid key(s).",
  "details": [
    {
      "message": "The specified item key does not exist: datetime_000",
      "property": "body.items[0].itemKey"
    }
  ]
}

// 同じアイテムを重複して指定した場合（400 Bad Request）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Duplicate itemKey in items or between emphasizedItem and items are not allowed: date_002_ja",
      "property": "body.emphasizedItem.itemKey"
    }
  ]
}

// メッセージの送信先が無効な場合（400 Bad Request）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "The value must be a valid SHA-256 digest.",
      "property": "to"
    }
  ]
}

// LINE通知メッセージ（テンプレート）を送信する権限がない場合（403 Forbidden）
{
  "message": "Access to this API is not available for your account"
}

// LINE通知メッセージの送信に失敗した場合（422 Unprocessable Entity）
{
  "message": "Failed to send messages"
}
```

<!-- tab end -->

### 送信済みのLINE通知メッセージ（テンプレート）の数を取得する 

「[LINE通知メッセージ（テンプレート）を送る](https://developers.line.biz/ja/reference/line-notification-messages/#send-line-notification-message-template)」エンドポイントを使って送信された、LINE通知メッセージ（テンプレート）の数を取得します。

詳しくは、『LINE通知メッセージドキュメント』の「[送信済みLINE通知メッセージの数を取得する](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#get-number-of-sent-line-notification-messages)」を参照してください。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET 'https://api.line.me/v2/bot/message/delivery/pnp/templated?date=20240916' \
-H 'Authorization: Bearer {channel_access_token}'
```

<!-- tab end -->

#### HTTPリクエスト 

`GET https://api.line.me/v2/bot/message/delivery/pnp/templated`

#### レート制限 

2,000リクエスト/秒

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: required) -->

date

メッセージが送信された日付

- フォーマット：`yyyyMMdd`（例：`20240916`）
- タイムゾーン：UTC+9

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

status

String

集計処理の状態。以下のいずれかの値です。

- `ready`：メッセージ数を取得できます。
- `unready`：`date`に指定した日付のメッセージ数の集計がまだ完了していません。しばらくしてからリクエストを再実行してください。通常、集計処理は翌日中に完了します。
- `out_of_service`：`date`に指定した日付が、集計システムの稼働開始日（2018年3月31日）より前です。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

success

Number

`date`に指定した日付に、LINE通知メッセージAPIを使って送信されたメッセージの数。`status`の値が`ready`の場合にのみ、レスポンスに含まれます。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "status": "ready",
  "success": 3
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>無効な日付が指定されています。</li><li>日付が指定されていません。</li></ul> |

詳しくは、『Messaging APIリファレンス』の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効な日付を指定した場合（400 Bad Request）
{
  "message": "The value for the 'date' parameter is invalid"
}
```

<!-- tab end -->

## LINE通知メッセージ（フレキシブル） 

- [LINE通知メッセージ（フレキシブル）を送る](https://developers.line.biz/ja/reference/line-notification-messages/#send-line-notification-message-flexible)
- [送信済みのLINE通知メッセージ（フレキシブル）の数を取得する](https://developers.line.biz/ja/reference/line-notification-messages/#get-number-of-sent-line-notification-messages-flexible)

### LINE通知メッセージ（フレキシブル）を送る 

ユーザーの電話番号を指定してLINE通知メッセージ（フレキシブル）を送るAPIです。

<!-- tip start -->

**従来の「LINE通知メッセージ」は、名称が「LINE通知メッセージ（フレキシブル）」に変更されました**

LINE通知メッセージに、用意されたテンプレートやアイテムを組み合わせて簡単にメッセージを作成できる「[LINE通知メッセージ（テンプレート）](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/template/)」が新たに加わりました。

これに伴い、UX審査を要する従来の「LINE通知メッセージ」は、名称が「LINE通知メッセージ（フレキシブル）」に変更されました。

詳しくは、2025年6月2日の『法人ユーザー向けお知らせ』、「[LINE通知メッセージ（テンプレート）の提供を開始しました](https://developers.line.biz/ja/docs/partner-docs/notice/#partner-news-20250602)」を参照してください。

<!-- tip end -->

<!-- warning start -->

**リクエスト元IPアドレスの制限はしないでください**

LINE通知メッセージを送る場合、Messaging APIチャネルの［**セキュリティ設定**］タブで、LINEプラットフォームのAPIを呼び出せるサーバーのIPアドレスを登録しないでください。リクエスト元のIPアドレスを制限した状態でLINE通知メッセージを送ると、送信に失敗することがあります。

リクエスト元のIPアドレスを制限しているか確認する方法については、『Messaging APIドキュメント』の「[長期のチャネルアクセストークン利用時にAPIの呼び出し元を制限する（任意）](https://developers.line.biz/ja/docs/messaging-api/building-bot/#configure-security-settings)」を参照してください。

<!-- warning end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/bot/pnp/push \
-H 'Authorization: Bearer {channel_access_token}' \
-H 'Content-Type:application/json' \
-d '{
    "to": "{hashed_phone_number}",
    "messages":[
        {
            "type":"text",
            "text":"Hello, world1"
        },
        {
            "type":"text",
            "text":"Hello, world2"
        }
    ]
}'

#リクエストの例(X-Line-Delivery-Tagあり)
curl -v -X POST https://api.line.me/bot/pnp/push \
-H 'Authorization: Bearer {channel_access_token}' \
-H 'Content-Type:application/json' \
-H 'X-Line-Delivery-Tag:{delivery_tag}' \
-d '{
    "to": "{hashed_phone_number}",
    "messages":[
        {
            "type":"text",
            "text":"Hello, world1"
        },
        {
            "type":"text",
            "text":"Hello, world2"
        }
    ]
}'
```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://api.line.me/bot/pnp/push`

#### レート制限 

2,000リクエスト/秒

#### リクエストヘッダー 

<!-- note start -->

**サポートしていない機能**

LINE通知メッセージAPIでは、[リトライキー](https://developers.line.biz/ja/reference/messaging-api/#retry-api-request)（`X-Line-Retry-Key`）を使ったAPIリクエストの再試行はできません。

<!-- note end -->

<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

X-Line-Delivery-Tag

Webhookを介して、[配信完了イベント](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#receive-delivery-event)の`delivery.data`プロパティで返される文字列。詳しくは、「[メッセージの送信通知を受信する](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#receive-delivery-event)」を参照してください。\
最小文字数：16\
最大文字数：100

<!-- parameter end -->

_X-Line-Delivery-Tagの例_

<!-- tab start `shell` -->

```sh
15034552939884E28681A7D668CEA94C147C716C0EC9DFE8B80B44EF3B57F6BD0602366BC3menu01
```

<!-- tab end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

to

String

メッセージの送信先。[E.164](https://developers.line.biz/ja/glossary/#e164)形式に正規化し[SHA256でハッシュ化した電話番号](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#phone-number-hashed)を指定してください。

メッセージの送信条件について詳しくは、「[LINE通知メッセージが送信される条件](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#conditions-for-sending-line-notification-messages)」を参照してください。

<!-- note start -->

**注意**

- [グループトークと複数人トーク](https://developers.line.biz/ja/docs/messaging-api/group-chats/#group-chat-types)は送信対象として指定できません。
- 複数の電話番号を送信対象として指定することはできません。

<!-- note end -->

<!-- parameter end -->

<!-- parameter start (props: required) -->

messages

[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の配列

送信するメッセージ。最大件数：5

詳しくは、「[LINE通知メッセージAPIで送信可能なメッセージタイプ](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#message-types-that-can-be-sent)」を参照してください。

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

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>メッセージの送信先が無効です。</li><li>無効なメッセージオブジェクトが指定されています。</li></ul> |
| `422` | LINE通知メッセージの送信に失敗しました。以下のような理由が考えられます。<ul><li>メッセージ送信対象に指定した電話番号に紐づくLINEユーザーが存在しません。</li><li>メッセージ送信対象に指定した電話番号は、LINE通知メッセージのサービス対象国で発行されたものではありません。詳しくは、「[LINE通知メッセージが送信される条件](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#conditions-for-sending-line-notification-messages)」を参照してください。</li><li>メッセージ送信対象に指定した電話番号に紐づくLINEユーザーが[LINE通知メッセージの受信を拒否](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#how-to-consent-for-line-notification-messages)しています。</li><li>メッセージ送信対象に指定した電話番号に紐づくLINEユーザーは、[LINEのプライバシーポリシー（2022年3月改定）](https://guide.line.me/privacy-policy_update/2022/0001/?lang=ja-jp)に同意していません。</li></ul> |

詳しくは、『Messaging APIリファレンス』の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// メッセージの送信先が無効な場合（400 Bad Request）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "The value must be a valid SHA-256 digest.",
      "property": "to"
    }
  ]
}

// LINE通知メッセージの送信に失敗した場合（422 Unprocessable Entity）
{
  "message": "Failed to send messages"
}
```

<!-- tab end -->

### 送信済みのLINE通知メッセージ（フレキシブル）の数を取得する 

「[LINE通知メッセージ（フレキシブル）を送る](https://developers.line.biz/ja/reference/line-notification-messages/#send-line-notification-message-flexible)」エンドポイントを使って送信された、LINE通知メッセージ（フレキシブル）の数を取得します。

詳しくは、『LINE通知メッセージドキュメント』の「[送信済みLINE通知メッセージの数を取得する](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#get-number-of-sent-line-notification-messages)」を参照してください。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET 'https://api.line.me/v2/bot/message/delivery/pnp?date=20211231' \
-H 'Authorization: Bearer {channel_access_token}'
```

<!-- tab end -->

#### HTTPリクエスト 

`GET https://api.line.me/v2/bot/message/delivery/pnp`

#### レート制限 

2,000リクエスト/秒

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: required) -->

date

メッセージが送信された日付

- フォーマット：`yyyyMMdd`（例：`20211231`）
- タイムゾーン：UTC+9

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

status

String

集計処理の状態。以下のいずれかの値です。

- `ready`：メッセージ数を取得できます。
- `unready`：`date`に指定した日付のメッセージ数の集計がまだ完了していません。しばらくしてからリクエストを再実行してください。通常、集計処理は翌日中に完了します。
- `out_of_service`：`date`に指定した日付が、集計システムの稼働開始日（2018年3月31日）より前です。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

success

Number

`date`に指定した日付に、LINE通知メッセージAPIを使って送信されたメッセージの数。`status`の値が`ready`の場合にのみ、レスポンスに含まれます。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "status": "ready",
  "success": 3
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>無効な日付が指定されています。</li><li>日付が指定されていません。</li></ul> |

詳しくは、『Messaging APIリファレンス』の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効な日付を指定した場合（400 Bad Request）
{
  "message": "The value for the 'date' parameter is invalid"
}
```

<!-- tab end -->
