# Messaging APIリファレンス

## 共通仕様 

Messaging APIにおけるエンドポイントのドメイン名、リクエストが成功・失敗した際のレスポンス、レート制限などの共通仕様です。

- [ドメイン名](https://developers.line.biz/ja/reference/messaging-api/#domain-name)
- [レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)
- [ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)
- [レスポンスヘッダー](https://developers.line.biz/ja/reference/messaging-api/#response-headers)
- [エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)
- [その他の共通仕様](https://developers.line.biz/ja/reference/messaging-api/#other-common-specifications)

### ドメイン名 

Messaging APIでは、エンドポイントによってドメイン名が異なります。利用時は注意してください。

| ドメイン名 | エンドポイント |
| --- | --- |
| `api-data.line.me`  | <ul><li>[コンテンツを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-content)</li><li>[ユーザーIDアップロード用のオーディエンスを作成する（ファイル指定）](https://developers.line.biz/ja/reference/messaging-api/#create-upload-audience-group-by-file)</li><li>[ユーザーIDアップロード用のオーディエンスにユーザーIDまたはIFAを追加する（ファイル指定）](https://developers.line.biz/ja/reference/messaging-api/#update-upload-audience-group-by-file)</li><li>[リッチメニューの画像をアップロードする](https://developers.line.biz/ja/reference/messaging-api/#upload-rich-menu-image)</li><li>[リッチメニューの画像をダウンロードする](https://developers.line.biz/ja/reference/messaging-api/#download-rich-menu-image)</li></ul> |
| `api.line.me` | 上記以外のエンドポイント |

### レート制限 

Messaging APIでは、チャネル単位かつAPI機能（エンドポイント）ごとに以下のレート制限が適用されます。レート制限が適用される範囲について詳しくは、「[レート制限の範囲](https://developers.line.biz/ja/reference/messaging-api/#rate-limits-scope)」を参照してください。

<!-- note start -->

**レート制限を超えてリクエストを送信しないでください**

レート制限を超えて送信を行った場合、`429 Too Many Requests`が返却され、エラーとなります。Messaging APIを使ったLINEボットを開発する際は、レート制限を含め、[Messaging API開発ガイドライン](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/)に従ってください。

<!-- note end -->

| エンドポイント | レート制限 |
| --- | --- |
| <ul><li>[ナローキャストメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message)</li><li>[ブロードキャストメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-broadcast-message)</li><li>[メッセージの送信数を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-number-of-delivery-messages)</li><li>[友だち数を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-number-of-followers)</li><li>[友だちの属性情報に基づく統計情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-demographic)</li><li>[ユーザーの操作に基づく統計情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-message-event)</li><li>[ユニットごとの統計情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-statistics-per-unit)</li><li>[Webhookエンドポイントを検証する](https://developers.line.biz/ja/reference/messaging-api/#test-webhook-endpoint)</li></ul> | 60リクエスト/時 |
| <ul><li>[ユーザーIDアップロード用のオーディエンスを作成する（JSON指定）](https://developers.line.biz/ja/reference/messaging-api/#create-upload-audience-group)</li><li>[ユーザーIDアップロード用のオーディエンスを作成する（ファイル指定）](https://developers.line.biz/ja/reference/messaging-api/#create-upload-audience-group-by-file)</li><li>[ユーザーIDアップロード用のオーディエンスにユーザーIDまたはIFAを追加する（JSON指定）](https://developers.line.biz/ja/reference/messaging-api/#update-upload-audience-group)</li><li>[ユーザーIDアップロード用のオーディエンスにユーザーIDまたはIFAを追加する（ファイル指定）](https://developers.line.biz/ja/reference/messaging-api/#update-upload-audience-group-by-file)</li><li>[メッセージクリックオーディエンスを作成する](https://developers.line.biz/ja/reference/messaging-api/#create-click-audience-group)</li><li>[メッセージインプレッションオーディエンスを作成する](https://developers.line.biz/ja/reference/messaging-api/#create-imp-audience-group)</li><li>[オーディエンスの名前を更新する](https://developers.line.biz/ja/reference/messaging-api/#set-description-audience-group)</li><li>[オーディエンスを削除する](https://developers.line.biz/ja/reference/messaging-api/#delete-audience-group)</li><li>[オーディエンスの情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-audience-group)</li><li>[複数のオーディエンスの情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-audience-groups)</li><li>[ビジネスマネージャーで共有されたオーディエンスの情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-shared-audience)</li><li>[ビジネスマネージャーで共有されたオーディエンスのリストを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-shared-audience-list)</li></ul> | 60リクエスト/分 |
| <ul><li>[WebhookエンドポイントのURLを設定する](https://developers.line.biz/ja/reference/messaging-api/#set-webhook-endpoint-url)</li><li>[Webhookエンドポイントの情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-webhook-endpoint-information)</li></ul> | 1,000リクエスト/分 |
| <ul><li>[リッチメニューを作成する](https://developers.line.biz/ja/reference/messaging-api/#create-rich-menu)</li><li>[リッチメニューを削除する](https://developers.line.biz/ja/reference/messaging-api/#delete-rich-menu)</li><li>[リッチメニューエイリアスを削除する](https://developers.line.biz/ja/reference/messaging-api/#delete-rich-menu-alias)</li><li>[リッチメニューの一括操作の進行状況を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-batch-control-rich-menus-progress-status)</li></ul> | 100リクエスト/時 ※ |
| <ul><li>[リンク済みのリッチメニューを一括で置き換え・解除する](https://developers.line.biz/ja/reference/messaging-api/#batch-control-rich-menus-of-users)</li></ul> | 3リクエスト/時 |
| <ul><li>[マルチキャストメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-multicast-message)</li><li>[ユーザーのメンバーシップ加入状況を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-a-users-membership-subscription-status)</li><li>[提供中のメンバーシッププランを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-membership-plans)</li><li>[クーポンを作成する](https://developers.line.biz/ja/reference/messaging-api/#create-coupon)</li><li>[クーポンを終了する](https://developers.line.biz/ja/reference/messaging-api/#discontinue-coupon)</li><li>[クーポンの一覧を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-coupons-list)</li><li>[クーポンの詳細を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-coupon)</li></ul> | 200リクエスト/秒 |
| <ul><li>[ローディングのアニメーションを表示する](https://developers.line.biz/ja/reference/messaging-api/#display-a-loading-indicator)</li></ul> | 100リクエスト/秒 |
| <ul><li>[短期のチャネルアクセストークンを発行する](https://developers.line.biz/ja/reference/messaging-api/#issue-shortlived-channel-access-token)</li></ul> | 370リクエスト/秒 |
| 上記以外のエンドポイント | 2,000リクエスト/秒 |

※ [LINE Official Account Manager](https://developers.line.biz/ja/glossary/#line-oa-manager)を使ってリッチメニューを作成・削除する場合は制限の対象外です。

#### レート制限の範囲 

Messaging APIでは、レート制限をチャネル単位かつAPI機能（エンドポイント）ごとに適用します。レート制限の範囲について、以下の点に注意してください。

- エンドポイントのURLが同じであっても、HTTPメソッドが異なれば別のエンドポイントとみなします。
- レート制限は、URL中のパラメータの内容や、リクエストボディの内容を区別せずに適用されます。
- レート制限は、エンドポイントの呼び出し元のIPアドレスの違いを区別せずに適用されます。
- 同じLINE公式アカウントに対するエンドポイントの呼び出しであっても、チャネルが異なる場合はチャネルごとに独立してレート制限が適用されます。

#### 同時処理数の制限 

ユーザーIDアップロード用のオーディエンス作成およびオーディエンスへのユーザーID追加のエンドポイントでは、オーディエンスID（`audienceGroupId`）単位での同時処理数の制限があります。

下記のエンドポイントで同時に処理されているリクエストの合計が、同時処理数としてカウントされます。

| エンドポイント | 同時処理数の上限 |
| --- | --- |
| <ul><li>[ユーザーIDアップロード用のオーディエンスを作成する（JSON指定）](https://developers.line.biz/ja/reference/messaging-api/#create-upload-audience-group)</li><li>[ユーザーIDアップロード用のオーディエンスを作成する（ファイル指定）](https://developers.line.biz/ja/reference/messaging-api/#create-upload-audience-group-by-file)</li><li>[ユーザーIDアップロード用のオーディエンスにユーザーIDまたはIFAを追加する（JSON指定）](https://developers.line.biz/ja/reference/messaging-api/#update-upload-audience-group)</li><li>[ユーザーIDアップロード用のオーディエンスにユーザーIDまたはIFAを追加する（ファイル指定）](https://developers.line.biz/ja/reference/messaging-api/#update-upload-audience-group-by-file)</li></ul> | 10 |

同時処理数の上限を超えるリクエストに対しては、[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)`429 Too Many Requests`のエラーが返ります。エラーを受け取った場合は、しばらく時間をおいてから再度リクエストをしてください。

処理中のリクエストの数は、以下のエンドポイントのレスポンスに含まれる`jobs`プロパティで確認できます。ジョブのステータス（`jobs[].jobStatus`プロパティ）が待機中（`QUEUED`）、もしくは実行中（`WORKING`）の場合に、同時処理数として計上されます。

- [オーディエンスの情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-audience-group)

### ステータスコード 

APIコールの後で、以下のHTTPステータスコードが返されます。ステータスコードの説明は、特に断りがない限り、[HTTP status code specification](https://datatracker.ietf.org/doc/html/rfc7231#section-6)に準拠しています。

| ステータスコード | 説明 |
| --- | --- |
| 200 OK | リクエストが成功しました。 |
| 400 Bad Request | リクエストに問題があります。 |
| 401 Unauthorized | 有効なチャネルアクセストークンが指定されていません。 |
| 403 Forbidden | リソースにアクセスする権限がありません。ご契約中のプランやアカウントに付与されている権限を確認してください。 |
| 404 Not Found | プロフィール情報を取得できませんでした。次のような理由が考えられます。<ul><li>対象のユーザーIDが存在していない。</li><li>ユーザーがプロフィール情報の取得に同意していない。</li><li>ユーザーが対象のLINE公式アカウントを友だち追加していない。</li><li>ユーザーが対象のLINE公式アカウントを友だち追加した後にブロックした。</li></ul>詳しくは、『Messaging APIドキュメント』の「[ユーザーのプロフィール情報取得の同意](https://developers.line.biz/ja/docs/messaging-api/user-consent/)」を参照してください。 |
| 409 Conflict | 同じリトライキーを持つAPIリクエストがすでに受理されています。詳しくは、「[失敗したAPIリクエストを再試行する](https://developers.line.biz/ja/docs/messaging-api/retrying-api-request/)」を参照してください。 |
| 410 Gone | 利用できなくなったリソースにアクセスしています。 |
| 413 Payload Too Large | リクエストのサイズが上限の2MBを超えています。リクエストのサイズを2MB以下にしてリクエストしなおしてください。 |
| 415 Unsupported Media Type | アップロードしようとしたファイルのメディア形式はサポートされていません。 |
| 429 Too Many Requests | <ul><li>APIコールの[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)を超過しました。</li><li>[同時処理数の制限](https://developers.line.biz/ja/reference/messaging-api/#limit-on-the-number-of-concurrent-operations)を超過しました。</li><li>無料メッセージ通数を超過しました。</li><li>追加メッセージ数の上限目安を超過しました。</li></ul><p>無料メッセージ通数や、追加メッセージ数の上限目安について詳しくは、『Messaging APIドキュメント』の「[Messaging APIの料金](https://developers.line.biz/ja/docs/messaging-api/pricing/)」を参照してください。</p><p>当月に配信できるメッセージ数がまだ残っていても、`You have reached your monthly limit.`が返される場合があります。詳しくは、FAQの「[当月に配信できるメッセージ数はまだ残っているのに、メッセージ送信時に429 Too Many Requests（You have reached your monthly limit.）が返されるのはなぜですか？](https://developers.line.biz/ja/faq/#why-do-i-get-429-error-during-message-delivery)」を参照してください。</p> |
| 500 Internal Server Error | 内部サーバーのエラーです。 |

### レスポンスヘッダー 

Messaging APIのレスポンスには以下のHTTPヘッダーが含まれます。

| レスポンスヘッダー | 説明 |
| --- | --- |
| X-Line-Request-Id | リクエストID。各リクエストごとに発行されるIDです。 |
| X-Line-Accepted-Request-Id 含まれないことがあります | 同じリトライキーを使ってすでにリクエストが受理されている場合、そのリクエストの`x-line-request-id`を示します。詳しくは、「[APIリクエストを再試行する](https://developers.line.biz/ja/reference/messaging-api/#retry-api-request)」を参照してください。 |

### エラーレスポンス 

エラー発生時は、以下のJSONデータを含むレスポンスボディが返されます。

<!-- parameter start -->

message

String

エラー情報を含むメッセージ。詳しくは、「[エラーメッセージ](https://developers.line.biz/ja/reference/messaging-api/#error-messages)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

details

Array

エラー詳細の配列。配列が空の場合は、レスポンスに含まれません。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

details\[].message

String

エラーの詳細。特定の状況ではレスポンスに含まれません。

「オーディエンス管理」のエンドポイントに関するエラーの詳細については、「[オーディエンス管理に関するエラーの詳細](https://developers.line.biz/ja/reference/messaging-api/#manage-audience-error)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

details\[].property

String

エラーの発生箇所。リクエストのJSONのフィールド名やクエリパラメータ名が返ります。特定の状況ではレスポンスに含まれません。

<!-- parameter end -->

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
{
  "message": "The request body has 2 error(s)",
  "details": [
    {
      "message": "May not be empty",
      "property": "messages[0].text"
    },
    {
      "message": "Must be one of the following values: [text, image, video, audio, location, sticker, template, imagemap]",
      "property": "messages[1].type"
    }
  ]
}
```

<!-- tab end -->

#### エラーメッセージ 

エラーのJSONレスポンスの`message`プロパティに含まれる、主なエラーメッセージは以下のとおりです。

| メッセージ | 説明 |
| --- | --- |
| The request body has X error(s) | リクエストボディのJSONデータにエラーがありました。Xの部分にエラーの数が表示されます。詳細は`details[].message`プロパティと`details[].property`プロパティに含まれます。 |
| Invalid reply token | [応答メッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)際に`replyToken`で指定した応答トークンが無効です。次のような理由が考えられます。<ul><li>有効期限が切れた応答トークンを使って応答メッセージを送った。</li><li>使用済みの応答トークンを使って応答メッセージを送った。</li></ul> |
| The property, XXX, in the request body is invalid (line: XXX, column: XXX) | リクエストボディに無効なプロパティが指定されていました。XXXの部分に具体的な行と列が表示されます。 |
| The request body could not be parsed as JSON (line: XXX, column: XXX) | リクエストボディのJSONデータを解析できませんでした。XXXの部分に具体的な行と列が表示されます。 |
| The content type, XXX, is not supported | APIでサポートされていないコンテンツタイプがリクエストされました。 |
| Authentication failed due to the following reason: XXX | APIが呼び出されたときに認証に失敗しました。XXXの部分に理由が表示されます。 |
| Access to this API is not available for your account | 実行権限がないAPIを呼び出しました。 |
| Failed to send messages | メッセージの送信に失敗しました。指定したユーザーIDが存在しない場合などにこのエラーが発生します。 |
| You have reached your monthly limit. | <ul><li>無料メッセージ通数を超過しました。</li><li>追加メッセージ数の上限目安を超過しました。</li></ul><p>無料メッセージ通数や、追加メッセージ数の上限目安について詳しくは、『Messaging APIドキュメント』の「[Messaging APIの料金](https://developers.line.biz/ja/docs/messaging-api/pricing/)」を参照してください。</p><p>当月に配信できるメッセージ数がまだ残っていても、`You have reached your monthly limit.`が返される場合があります。詳しくは、FAQの「[当月に配信できるメッセージ数はまだ残っているのに、メッセージ送信時に429 Too Many Requests（You have reached your monthly limit.）が返されるのはなぜですか？](https://developers.line.biz/ja/faq/#why-do-i-get-429-error-during-message-delivery)」を参照してください。</p> |
| The API rate limit has been exceeded. Try again later. | APIコールの[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)を超過しました。 |
| Not found | プロフィール情報を取得できませんでした。次のような理由が考えられます。<ul><li>対象のユーザーIDが存在していない</li><li>ユーザーがプロフィール情報の取得に同意していない</li><li>ユーザーが対象のLINE公式アカウントを友だち追加していない</li><li>ユーザーが対象のLINE公式アカウントを友だち追加した後にブロックした</li></ul>詳しくは、『Messaging APIドキュメント』の「[ユーザーのプロフィール情報取得の同意](https://developers.line.biz/ja/docs/messaging-api/user-consent/)」を参照してください。 |

### その他の共通仕様 

#### リクエストボディのプロパティに指定するURLのエンコードについて 

プロパティにURLを指定する場合は、ドメイン名、パス、クエリパラメータ、フラグメントはUTF-8を用いて[パーセントエンコード](https://ja.wikipedia.org/wiki/%E3%83%91%E3%83%BC%E3%82%BB%E3%83%B3%E3%83%88%E3%82%A8%E3%83%B3%E3%82%B3%E3%83%BC%E3%83%87%E3%82%A3%E3%83%B3%E3%82%B0)してください。

たとえば、以下の構成要素を持つURIを指定する場合は、 `https://example.com/path?q=%E3%81%8A%E3%81%AF%E3%82%88%E3%81%86#%E3%81%93%E3%82%93%E3%81%AB%E3%81%A1%E3%81%AF`とします。

| スキーム | ドメイン名  | パス  | クエリパラメータ | フラグメント |
| -------- | ----------- | ----- | ---------------- | ------------ |
| https    | example.com | /path | q=おはよう       | こんにちは   |

## Webhook 

友だち追加やユーザーからのメッセージ送信のようなイベントが発生すると、LINEプラットフォームからWebhook URL（ボットサーバー）にHTTPS POSTリクエストが送信されます。

Webhook URLはチャネルごとに[LINE Developersコンソール](https://developers.line.biz/console/)で設定します。

<!-- tip start -->

**イベント処理を非同期化することを推奨します**

HTTP POSTリクエストの処理が後続のイベントの処理に遅延を与えないよう、イベント処理を非同期化することを推奨します。

<!-- tip end -->

<!-- note start -->

**LINEプラットフォームのIPアドレスは開示していません**

Webhookリクエスト送信元のLINEプラットフォームのIPアドレスは開示していません。セキュリティの担保はIPアドレスによるアクセス制御ではなく、[署名の検証](https://developers.line.biz/ja/reference/messaging-api/#signature-validation)で実施してください。

<!-- note end -->

### リクエストヘッダー 

<!-- parameter start -->

x-line-signature

[署名の検証](https://developers.line.biz/ja/reference/messaging-api/#signature-validation)に使う署名

<!-- parameter end -->

<!-- note start -->

**リクエストヘッダーのフィールド名は大文字小文字を区別せずに扱ってください**

[リクエストヘッダー](https://developers.line.biz/ja/reference/messaging-api/#request-headers)のフィールド名は、大文字・小文字の表記が予告なく変更される可能性があります。Webhookを受け取るボットサーバー側では、ヘッダーフィールド名の大文字小文字を区別せずに扱ってください。\*1

|                          | 変更前             | 変更後             |
| ------------------------ | ------------------ | ------------------ |
| ヘッダーフィールド名の例 | `X-Line-Signature` | `x-line-signature` |

\*1 [https://datatracker.ietf.org/doc/html/rfc7230#section-3.2](https://datatracker.ietf.org/doc/html/rfc7230#section-3.2)

<!-- note end -->

### リクエストボディ 

リクエストボディは、Webhookイベントを受信すべきボットのユーザーIDと[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の配列を含むJSONオブジェクトです。

<!-- parameter start -->

destination

String

Webhookイベントを受信すべきボットのユーザーID。ユーザーIDの値は、`U[0-9a-f]{32}`の正規表現にマッチする文字列です。

<!-- parameter end -->
<!-- parameter start -->

events

Array

[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の配列。LINEプラットフォームからの疎通確認のために、Webhookイベントオブジェクトを含まない空配列が送信される場合があります。

<!-- parameter end -->

### レスポンス 

LINEプラットフォームから送信されるHTTP POSTリクエストをボットサーバーで受信したときは、ステータスコード`200`を返してください。

<!-- note start -->

**注意**

- LINEプラットフォームから送信されるHTTP POSTリクエストの受信に失敗した場合でも、このリクエストを再度受け取ることができます。詳しくは、「[受け取りに失敗したWebhookを再送する](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#webhook-redelivery)」を参照してください。
- LINEプラットフォームから疎通確認のために、Webhookイベントが含まれないHTTP POSTリクエストが送信されることがあります。この場合も、ステータスコード`200`を返してください。

  Webhookイベントが含まれないHTTP POSTリクエストの例：

  ```json
  {
    "destination": "xxxxxxxxxx",
    "events": []
  }
  ```

<!-- note end -->

### 署名を検証する 

ボットサーバーにWebhookのリクエストが届いたら、[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)を処理する前に、リクエストヘッダーに含まれる署名を検証してください。署名の検証は、開発者のボットサーバーに届いたリクエストが「LINEプラットフォームから送信されたWebhookか」および「通信経路で改ざんされていないか」などを確認するための重要な手順です。

詳しくは、『Messaging APIドキュメント』の「[Webhookの署名を検証する](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-signature/)」を参照してください。

_署名検証の例_

<!-- tab start `java` -->

```java
String channelSecret = '...'; // Channel secret string
String httpRequestBody = '...'; // Request body string
SecretKeySpec key = new SecretKeySpec(channelSecret.getBytes(), "HmacSHA256");
Mac mac = Mac.getInstance("HmacSHA256");
mac.init(key);
byte[] source = httpRequestBody.getBytes("UTF-8");
String signature = Base64.encodeBase64String(mac.doFinal(source));
// Compare x-line-signature request header string and the signature
```

<!-- tab end -->
<!-- tab start `ruby` -->

```ruby
CHANNEL_SECRET = '...' # Channel secret string
http_request_body = request.raw_post # Request body string
hash = OpenSSL::HMAC::digest(OpenSSL::Digest::SHA256.new, CHANNEL_SECRET, http_request_body)
signature = Base64.strict_encode64(hash)
# Compare x-line-signature request header string and the signature
```

<!-- tab end -->
<!-- tab start `go` -->

```go
defer req.Body.Close()
body, err := ioutil.ReadAll(req.Body)
if err != nil {
  // ...
}
decoded, err := base64.StdEncoding.DecodeString(req.Header.Get("x-line-signature"))
if err != nil {
  // ...
}
hash := hmac.New(sha256.New, []byte("<channel secret>"))
hash.Write(body)
// Compare decoded signature and `hash.Sum(nil)` by using `hmac.Equal`
```

<!-- tab end -->
<!-- tab start `php` -->

```php
$channelSecret = '...'; // Channel secret string
$httpRequestBody = '...'; // Request body string
$hash = hash_hmac('sha256', $httpRequestBody, $channelSecret, true);
$signature = base64_encode($hash);
// Compare x-line-signature request header string and the signature
```

<!-- tab end -->
<!-- tab start `perl` -->

```perl
use Digest::SHA 'hmac_sha256';
use MIME::Base64 'encode_base64';

my $channel_secret= '...'; # Channel secret string
my $http_body = '...'; # Request body string
my $signature = encode_base64(hmac_sha256($http_body, $channel_secret));
# Compare x-line-signature request header string and the signature
```

<!-- tab end -->
<!-- tab start `python` -->

```python
import base64
import hashlib
import hmac

channel_secret = '...' # Channel secret string
body = '...' # Request body string
hash = hmac.new(channel_secret.encode('utf-8'),
    body.encode('utf-8'), hashlib.sha256).digest()
signature = base64.b64encode(hash)
# Compare x-line-signature request header and the signature
```

<!-- tab end -->
<!-- tab start `nodejs` -->

```javascript
const crypto = require("crypto");

const channelSecret = "..."; // Channel secret string
const body = "..."; // Request body string
const signature = crypto
  .createHmac("SHA256", channelSecret)
  .update(body)
  .digest("base64");
// Compare x-line-signature request header and the signature
```

<!-- tab end -->

## Webhookイベントオブジェクト 

LINEプラットフォームで生成されるイベントを含むJSONオブジェクトです。

これらのイベントオブジェクトのプロパティは、値が存在しない場合があります。値が存在しないプロパティは、生成されるイベントオブジェクトに含まれません。

<!-- tip start -->

**1つのWebhookに複数のWebhookイベントオブジェクトが含まれる場合があります**

LINEプラットフォームから送信されるWebhookには、複数のWebhookイベントオブジェクトが含まれる場合があります。また1つのWebhookにつき一人のユーザーとは限らず、Aさんからの[メッセージイベント](https://developers.line.biz/ja/reference/messaging-api/#message-event)と、Bさんからの[フォローイベント](https://developers.line.biz/ja/reference/messaging-api/#follow-event)が同じWebhookに入ることもあります。

複数のWebhookイベントオブジェクトを含むWebhookを受信した場合も、ボットサーバーは適切な処理を行えるようにしてください。詳しくは、Webhookの[リクエストボディ](https://developers.line.biz/ja/reference/messaging-api/#request-body)を参照してください。

<!-- tip end -->

_Webhookイベントオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "type": "message",
      "message": {
        "type": "text",
        "id": "14353798921116",
        "text": "Hello, world"
      },
      "timestamp": 1625665242211,
      "source": {
        "type": "user",
        "userId": "U80696558e1aa831..."
      },
      "replyToken": "757913772c4646b784d4b7ce46d12671",
      "mode": "active",
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      }
    },
    {
      "type": "follow",
      "timestamp": 1625665242214,
      "source": {
        "type": "user",
        "userId": "Ufc729a925b3abef..."
      },
      "replyToken": "bb173f4d9cf64aed9d408ab4e36339ad",
      "mode": "active",
      "webhookEventId": "01FZ74ASS536FW97EX38NKCZQK",
      "deliveryContext": {
        "isRedelivery": false
      }
    },
    {
      "type": "unfollow",
      "timestamp": 1625665242215,
      "source": {
        "type": "user",
        "userId": "Ubbd4f124aee5113..."
      },
      "mode": "active",
      "webhookEventId": "01FZ74B5Y0F4TNKA5SCAVKPEDM",
      "deliveryContext": {
        "isRedelivery": false
      }
    }
  ]
}
```

<!-- tab end -->

### 共通プロパティ 

以下のプロパティはWebhookイベントオブジェクトの共通プロパティです。

<!-- parameter start -->

type

String

イベントのタイプを表す識別子

<!-- parameter end -->
<!-- parameter start -->

mode

String

チャネルの状態。

- `active`：チャネルがアクティブです。このWebhookイベントを受信したボットサーバーから、応答メッセージやプッシュメッセージなどを送信できます。
- `standby`：チャネルが待機状態です。チャネルの状態が`standby`のときは、Webhookに[応答メッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)ための応答トークンは含まれません。チャネルの状態が`standby`になるタイミングについて詳しくは、『モジュールドキュメント』の「[Webhookイベントの受信](https://developers.line.biz/ja/docs/partner-docs/module/#bot-module-channel-receive-webhook)」を参照してください。

<!-- note start -->

**チャネルの状態がstandbyのときは、メッセージの送信を控えてください**

チャネルの状態が`standby`のときは、受信したWebhookイベントに対して[モジュール](https://developers.line.biz/ja/docs/partner-docs/module/)がメッセージなどで応答している可能性があります。ユーザーとモジュールがやりとりをしている最中に、ボットからもメッセージが送信されるとユーザーの混乱を招きます。そのため、`mode`プロパティが`standby`のWebhookイベントを受信したボットサーバーはメッセージの送信を控えてください。

<!-- note end -->

<!-- parameter end -->
<!-- parameter start -->

timestamp

Number

イベントの発生時刻。UNIX時間（ミリ秒）で返されます。再送されたWebhookの場合でも、再送された時刻ではなく、イベントの発生時刻を表します。

<!-- note start -->

**Webhookの再送が有効な場合はtimestampを確認してください**

[Webhookの再送](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#webhook-redelivery)が有効である場合、Webhookイベントの発生順序と、ボットサーバーに到達する順序が大きく崩れる可能性があります。これが問題になる場合は、`timestamp`を確認することによって、前後関係を確認してください。

<!-- note end -->

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

source

Object

イベントの送信元情報を含む[ユーザー](https://developers.line.biz/ja/reference/messaging-api/#source-user)、[グループトーク](https://developers.line.biz/ja/reference/messaging-api/#source-group)、または[複数人トーク](https://developers.line.biz/ja/reference/messaging-api/#source-room)オブジェクト。

このプロパティは、アカウントの連携に失敗した場合、[アカウント連携イベント](https://developers.line.biz/ja/reference/messaging-api/#account-link-event)には含まれません。

<!-- parameter end -->
<!-- parameter start -->

webhookEventId

String

WebhookイベントID。Webhookイベントを一意に識別するためのID。ULID形式の文字列になります。

<!-- parameter end -->
<!-- parameter start -->

deliveryContext.isRedelivery

Boolean

Webhookイベントが再送されたものかどうか。詳しくは、「[再送されるWebhook](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#redelivered-webhooks)」を参照してください。

- `true`：再送されたWebhookイベントです。
- `false`：初めて送られたWebhookイベントです。

<!-- parameter end -->

#### 送信元ユーザー 

<!-- parameter start -->

type

String

`user`

<!-- parameter end -->
<!-- parameter start -->

userId

String

送信元ユーザーのID

<!-- parameter end -->

_送信元ユーザーの例_

<!-- tab start `json` -->

```json
  "source": {
    "type": "user",
    "userId": "U4af4980629..."
  }
```

<!-- tab end -->

#### 送信元グループトーク 

<!-- parameter start -->

type

String

`group`

<!-- parameter end -->
<!-- parameter start -->

groupId

String

送信元グループトークのグループID

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

userId

String

送信元ユーザーのID。[メッセージイベント](https://developers.line.biz/ja/reference/messaging-api/#message-event)にのみ含まれます。iOS版LINEまたはAndroid版LINEを使用しているユーザーのみ`userId`に含まれます。詳しくは、「[ユーザーのプロフィール情報取得の同意](https://developers.line.biz/ja/docs/messaging-api/user-consent/)」を参照してください。

<!-- parameter end -->

_送信元グループトークの例_

<!-- tab start `json` -->

```json
  "source": {
    "type": "group",
    "groupId": "Ca56f94637c...",
    "userId": "U4af4980629..."
  }
```

<!-- tab end -->

#### 送信元複数人トーク 

<!-- parameter start -->

type

String

`room`

<!-- parameter end -->
<!-- parameter start -->

roomId

String

送信元複数人トークのトークルームID

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

userId

String

送信元ユーザーのID。[メッセージイベント](https://developers.line.biz/ja/reference/messaging-api/#message-event)にのみ含まれます。iOS版LINEまたはAndroid版LINEを使用しているユーザーのみ`userId`に含まれます。詳しくは、「[ユーザーのプロフィール情報取得の同意](https://developers.line.biz/ja/docs/messaging-api/user-consent/)」を参照してください。

<!-- parameter end -->

_送信元複数人トークの例_

<!-- tab start `json` -->

```json
  "source": {
    "type": "room",
    "roomId": "Ra8dbf4673c...",
    "userId": "U4af4980629..."
  }
```

<!-- tab end -->

### メッセージイベント 

ユーザーから送信されたメッセージを含むWebhookイベントオブジェクトです。メッセージのタイプに対応するメッセージオブジェクトが、`message`プロパティに含まれます。メッセージイベントには応答できます。

<!-- parameter start -->

timestamp、sourceなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

type

String

`message`

<!-- parameter end -->
<!-- parameter start -->

replyToken

String

このイベントに対して[応答メッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)際に使用する応答トークン

<!-- parameter end -->
<!-- parameter start -->

message

Object

メッセージの内容を含むオブジェクト。メッセージには以下のタイプがあります。

- [テキスト](https://developers.line.biz/ja/reference/messaging-api/#wh-text)
- [画像](https://developers.line.biz/ja/reference/messaging-api/#wh-image)
- [動画](https://developers.line.biz/ja/reference/messaging-api/#wh-video)
- [音声](https://developers.line.biz/ja/reference/messaging-api/#wh-audio)
- [ファイル](https://developers.line.biz/ja/reference/messaging-api/#wh-file)
- [位置情報](https://developers.line.biz/ja/reference/messaging-api/#wh-location)
- [スタンプ](https://developers.line.biz/ja/reference/messaging-api/#wh-sticker)

<!-- parameter end -->

#### テキスト 

送信元から送られたテキストを含むメッセージオブジェクトです。

<!-- parameter start -->

id

String

メッセージID

<!-- parameter end -->
<!-- parameter start -->

type

String

`text`

<!-- parameter end -->
<!-- parameter start -->

quoteToken

String

メッセージの引用トークン。詳しくは、『Messaging APIドキュメント』の「[引用トークンを取得する](https://developers.line.biz/ja/docs/messaging-api/get-quote-tokens/)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

markAsReadToken

String

既読トークン。このトークンを使用することで、メッセージに既読をつけることができます。有効期限はありません。詳しくは、『Messaging APIドキュメント』の「[メッセージに既読をつける](https://developers.line.biz/ja/docs/messaging-api/mark-as-read/)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

text

String

メッセージのテキスト

- エンドユーザーがLINE絵文字を送信した場合は、`(hello)`や`(love)`のように、LINE絵文字が文字列で含まれます。LINE絵文字の詳細は、`emojis`プロパティで確認できます。
- エンドユーザーがメンションした場合は、`@example`のように、送信相手のLINEアカウントの表示名が文字列で含まれます。メンションの詳細は、`mention`プロパティで確認できます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

emojis

Array

1個以上のLINE絵文字オブジェクトの配列。`text`プロパティにLINE絵文字が含まれる場合のみ、メッセージイベントに含まれます。

<!-- note start -->

**送信されたLINE絵文字がemojisプロパティに含まれないことがあります**

- Android版LINEから送信されたデフォルトのLINE絵文字は、含まれません。
- Unicodeで定義された絵文字や古いバージョンのLINE絵文字は、含まれないことがあります。

<!-- note end -->

<!-- parameter end -->
<!-- parameter start -->

emojis\[].index

Number

テキストの先頭を`0`とした、`text`プロパティ内の絵文字の開始位置。

<!-- parameter end -->
<!-- parameter start -->

emojis\[].length

Number

LINE絵文字の文字列の長さ。LINE絵文字`(hello)`であれば、`7`が長さになります。

<!-- parameter end -->
<!-- parameter start -->

emojis\[].productId

String

LINE絵文字の集合を示すプロダクトID。プロダクトIDの例として、「[LINE絵文字](https://developers.line.biz/ja/docs/messaging-api/emoji-list/)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

emojis\[].emojiId

String

プロダクトID内のLINE絵文字のID。LINE絵文字のIDの例として、「[LINE絵文字](https://developers.line.biz/ja/docs/messaging-api/emoji-list/)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

mention

Object

メンションの情報を含むオブジェクト。`text`プロパティにメンションが含まれる場合のみ、メッセージイベントに含まれます。

<!-- parameter end -->
<!-- parameter start -->

mention.mentionees[]

Array of objects

1個以上のメンションオブジェクトの配列。

最大メンション数：20

<!-- parameter end -->
<!-- parameter start -->

mention.mentionees[].index

Number

テキストの先頭を`0`とした、`text`プロパティ内のメンションの開始位置。

<!-- parameter end -->
<!-- parameter start -->

mention.mentionees[].length

Number

メンションの長さ。`@example`であれば、`8`が長さになります。

<!-- parameter end -->
<!-- parameter start -->

mention.mentionees[].type

String

メンションの対象。

- `user`：ユーザーまたはボット
- `all`：グループ全体

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

mention.mentionees[].userId

String

メンションされたユーザーまたはボットのユーザーID。`mention.mentionees[].type`が`user`の場合にのみ含まれます。メンションされたのがユーザーの場合は、LINE公式アカウントがプロフィール情報を取得することに、[ユーザーが同意](https://developers.line.biz/ja/docs/messaging-api/user-consent/)しているときにのみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

mention.mentionees[].isSelf

Boolean

Webhookイベントを受信したボット（`destination`）に対するメンションかどうか。`mention.mentionees[].type`プロパティの値が`user`のときのみ含まれます。

- `true`：Webhookイベントを受信したボットに対するメンションである。
- `false`：他のユーザーに対するメンションである。

詳しくは、『Messaging APIドキュメント』の「[ボットへのメンションを含むメッセージが送信されたときのWebhook](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#webhook-message-with-mention-to-bot)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

quotedMessageId

String

引用されたメッセージのメッセージID。過去のメッセージを引用している場合にのみ含まれます。

<!-- parameter end -->

_テキストメッセージの例_

<!-- tab start `json` -->

```json
// グループトークでユーザーからメンションと絵文字を含むテキストメッセージが送られた場合
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "replyToken": "nHuyWiB7yP5Zw52FIkcQobQuGDXCTA",
      "type": "message",
      "mode": "active",
      "timestamp": 1462629479859,
      "source": {
        "type": "group",
        "groupId": "Ca56f94637c...",
        "userId": "U4af4980629..."
      },
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      },
      "message": {
        "id": "444573844083572737",
        "type": "text",
        "quoteToken": "q3Plxr4AgKd...",
        "markAsReadToken": "30yhdy232...",
        "text": "@All @example Good Morning!! (love)",
        "emojis": [
          {
            "index": 29,
            "length": 6,
            "productId": "5ac1bfd5040ab15980c9b435",
            "emojiId": "001"
          }
        ],
        "mention": {
          "mentionees": [
            {
              "index": 0,
              "length": 4,
              "type": "all"
            },
            {
              "index": 5,
              "length": 8,
              "userId": "U49585cd0d5...",
              "type": "user",
              "isSelf": false
            }
          ]
        }
      }
    }
  ]
}
```

<!-- tab end -->

#### 画像 

送信元から送られた画像を含むメッセージオブジェクトです。

<!-- parameter start -->

id

String

メッセージID

<!-- parameter end -->
<!-- parameter start -->

type

String

`image`

<!-- parameter end -->
<!-- parameter start -->

quoteToken

String

メッセージの引用トークン。詳しくは、『Messaging APIドキュメント』の「[引用トークンを取得する](https://developers.line.biz/ja/docs/messaging-api/get-quote-tokens/)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

markAsReadToken

String

既読トークン。このトークンを使用することで、メッセージに既読をつけることができます。有効期限はありません。詳しくは、『Messaging APIドキュメント』の「[メッセージに既読をつける](https://developers.line.biz/ja/docs/messaging-api/mark-as-read/)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

contentProvider.type

String

画像ファイルの提供元。

- `line`：LINEユーザーが画像ファイルを送信しました。画像ファイルのバイナリデータは、メッセージIDを指定して[コンテンツを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-content)エンドポイントを使用することで取得できます。
- `external`：画像ファイルのURLは`contentProvider.originalContentUrl`プロパティに含まれます。なお、画像ファイルの提供元が`external`の場合、画像ファイルのバイナリデータは[コンテンツを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-content)エンドポイントで取得できません。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

contentProvider.originalContentUrl

String

画像ファイルのURL。`contentProvider.type`が`external`の場合にのみ含まれます。画像ファイルが置かれているサーバーは、LINEヤフー株式会社が提供しているものではありません。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

contentProvider.previewImageUrl

String

プレビュー画像のURL。`contentProvider.type`が`external`の場合にのみ含まれます。プレビュー画像が置かれているサーバーは、LINEヤフー株式会社が提供しているものではありません。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

imageSet.id

String

画像セットID。複数の画像を同時に送信した場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

imageSet.index

Number

同時に送信した画像セットの中で、何番目の画像かを示す`1`から始まるインデックス。複数の画像を同時に送信した場合のみ含まれます。ただし送信元がAndroid版LINE 11.15以前の場合は含まれません。

<!-- tip start -->

**Webhookが届く順序は不定です**

ユーザーが複数の画像を同時に送信すると、LINEプラットフォームからボットサーバーにWebhookイベントが複数送られてきます。このときWebhookの順序は不定ですので、`imageSet.index`の値の順序で届くとは限りません。

<!-- tip end -->

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

imageSet.total

Number

同時に送信した画像の総数。同時に2つの画像を送信した場合は`2`です。複数の画像を同時に送信した場合のみ含まれます。ただし送信元がAndroid版LINE 11.15以前の場合は含まれません。

<!-- parameter end -->

_画像メッセージの例_

<!-- tab start `json` -->

```json
// 2つの画像を同時に送った場合（1番目の画像）
{
    "destination": "xxxxxxxxxx",
    "events": [
        {
            "type": "message",
            "message": {
                "type": "image",
                "id": "354718705033693859",
                "quoteToken": "q3Plxr4AgKd...",
                "markAsReadToken": "30yhdy232...",
                "contentProvider": {
                    "type": "line"
                },
                "imageSet": {
                    "id": "E005D41A7288F41B65593ED38FF6E9834B046AB36A37921A56BC236F13A91855",
                    "index": 1,
                    "total": 2
                }
            },
            "timestamp": 1627356924513,
            "source": {
                "type": "user",
                "userId": "U4af4980629..."
            },
            "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
            "deliveryContext": {
                "isRedelivery": false
            },
            "replyToken": "7840b71058e24a5d91f9b5726c7512c9",
            "mode": "active"
        }
    ]
}

// 2つの画像を同時に送った場合（2番目の画像）
{
    "destination": "xxxxxxxxxx",
    "events": [
        {
            "type": "message",
            "message": {
                "type": "image",
                "id": "354718705033693861",
                "quoteToken": "yHAz4Ua2wx7...",
                "markAsReadToken": "30yhdy232...",
                "contentProvider": {
                    "type": "line"
                },
                "imageSet": {
                    "id": "E005D41A7288F41B65593ED38FF6E9834B046AB36A37921A56BC236F13A91855",
                    "index": 2,
                    "total": 2
                }
            },
            "timestamp": 1627356924722,
            "source": {
                "type": "user",
                "userId": "U4af4980629..."
            },
            "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
            "deliveryContext": {
                "isRedelivery": false
            },
            "replyToken": "fbf94e269485410da6b7e3a5e33283e8",
            "mode": "active"
        }
    ]
}
```

<!-- tab end -->

#### 動画 

送信元から送られた動画を含むメッセージオブジェクトです。トーク画面に表示されている画像はプレビュー画像で、画像をタップすると動画が表示されます。

<!-- parameter start -->

id

String

メッセージID

<!-- parameter end -->
<!-- parameter start -->

type

String

`video`

<!-- parameter end -->
<!-- parameter start -->

quoteToken

String

メッセージの引用トークン。詳しくは、『Messaging APIドキュメント』の「[引用トークンを取得する](https://developers.line.biz/ja/docs/messaging-api/get-quote-tokens/)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

markAsReadToken

String

既読トークン。このトークンを使用することで、メッセージに既読をつけることができます。有効期限はありません。詳しくは、『Messaging APIドキュメント』の「[メッセージに既読をつける](https://developers.line.biz/ja/docs/messaging-api/mark-as-read/)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

duration

Number

動画ファイルの長さ（ミリ秒）

<!-- parameter end -->
<!-- parameter start -->

contentProvider.type

String

動画ファイルの提供元。

- `line`：LINEユーザーが動画ファイルを送信しました。動画ファイルのバイナリデータは、メッセージIDを指定して[コンテンツを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-content)エンドポイントを使用することで取得できます。
- `external`：動画ファイルのURLは`contentProvider.originalContentUrl`プロパティに含まれます。なお、動画ファイルの提供元が`external`の場合、動画ファイルのバイナリデータは[コンテンツを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-content)エンドポイントで取得できません。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

contentProvider.originalContentUrl

String

動画ファイルのURL。`contentProvider.type`が`external`の場合にのみ含まれます。動画ファイルが置かれているサーバーは、LINEヤフー株式会社が提供しているものではありません。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

contentProvider.previewImageUrl

String

プレビュー画像のURL。`contentProvider.type`が`external`の場合にのみ含まれます。プレビュー画像が置かれているサーバーは、LINEヤフー株式会社が提供しているものではありません。

<!-- parameter end -->

_動画メッセージの例_

<!-- tab start `json` -->

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "replyToken": "nHuyWiB7yP5Zw52FIkcQobQuGDXCTA",
      "type": "message",
      "mode": "active",
      "timestamp": 1462629479859,
      "source": {
        "type": "user",
        "userId": "U4af4980629..."
      },
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      },
      "message": {
        "id": "325708",
        "type": "video",
        "quoteToken": "q3Plxr4AgKd...",
        "markAsReadToken": "30yhdy232...",
        "duration": 60000,
        "contentProvider": {
          "type": "external",
          "originalContentUrl": "https://example.com/original.mp4",
          "previewImageUrl": "https://example.com/preview.jpg"
        }
      }
    }
  ]
}
```

<!-- tab end -->

#### 音声 

送信元から送られた音声を含むメッセージオブジェクトです。

<!-- parameter start -->

id

String

メッセージID

<!-- parameter end -->
<!-- parameter start -->

type

String

`audio`

<!-- parameter end -->
<!-- parameter start -->

markAsReadToken

String

既読トークン。このトークンを使用することで、メッセージに既読をつけることができます。有効期限はありません。詳しくは、『Messaging APIドキュメント』の「[メッセージに既読をつける](https://developers.line.biz/ja/docs/messaging-api/mark-as-read/)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

duration

Number

音声ファイルの長さ（ミリ秒）

<!-- parameter end -->
<!-- parameter start -->

contentProvider.type

String

音声ファイルの提供元

- `line`：LINEユーザーが音声ファイルを送信しました。音声ファイルのバイナリデータは、メッセージIDを指定して[コンテンツを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-content)エンドポイントを使用することで取得できます。
- `external`：音声ファイルのURLは`contentProvider.originalContentUrl`プロパティに含まれます。なお、音声ファイルの提供元が`external`の場合、音声ファイルのバイナリデータは[コンテンツを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-content)エンドポイントで取得できません。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

contentProvider.originalContentUrl

String

音声ファイルのURL。`contentProvider.type`が`external`の場合にのみ含まれます。音声ファイルが置かれているサーバーは、LINEヤフー株式会社が提供しているものではありません。

<!-- parameter end -->

_音声メッセージの例_

<!-- tab start `json` -->

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "replyToken": "nHuyWiB7yP5Zw52FIkcQobQuGDXCTA",
      "type": "message",
      "mode": "active",
      "timestamp": 1462629479859,
      "source": {
        "type": "user",
        "userId": "U4af4980629..."
      },
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      },
      "message": {
        "id": "325708",
        "type": "audio",
        "markAsReadToken": "30yhdy232...",
        "duration": 60000,
        "contentProvider": {
          "type": "line"
        }
      }
    }
  ]
}
```

<!-- tab end -->

#### ファイル 

送信元から送られたファイルを含むメッセージオブジェクトです。ファイルのバイナリデータは、メッセージIDを指定してAPIを呼び出すことで取得できます。詳しくは、「[コンテンツを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-content)」を参照してください。

<!-- parameter start -->

id

String

メッセージID

<!-- parameter end -->
<!-- parameter start -->

type

String

`file`

<!-- parameter end -->
<!-- parameter start -->

markAsReadToken

String

既読トークン。このトークンを使用することで、メッセージに既読をつけることができます。有効期限はありません。詳しくは、『Messaging APIドキュメント』の「[メッセージに既読をつける](https://developers.line.biz/ja/docs/messaging-api/mark-as-read/)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

fileName

String

ファイル名

<!-- parameter end -->
<!-- parameter start -->

fileSize

Number

ファイルサイズ（バイト）

<!-- parameter end -->

_ファイルメッセージの例_

<!-- tab start `json` -->

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "replyToken": "nHuyWiB7yP5Zw52FIkcQobQuGDXCTA",
      "type": "message",
      "mode": "active",
      "timestamp": 1462629479859,
      "source": {
        "type": "user",
        "userId": "U4af4980629..."
      },
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      },
      "message": {
        "id": "325708",
        "type": "file",
        "markAsReadToken": "30yhdy232...",
        "fileName": "file.txt",
        "fileSize": 2138
      }
    }
  ]
}
```

<!-- tab end -->

#### 位置情報 

送信元から送られた位置情報データを含むメッセージオブジェクトです。

<!-- parameter start -->

id

String

メッセージID

<!-- parameter end -->
<!-- parameter start -->

type

String

`location`

<!-- parameter end -->
<!-- parameter start -->

markAsReadToken

String

既読トークン。このトークンを使用することで、メッセージに既読をつけることができます。有効期限はありません。詳しくは、『Messaging APIドキュメント』の「[メッセージに既読をつける](https://developers.line.biz/ja/docs/messaging-api/mark-as-read/)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

title

String

タイトル

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

address

String

住所

<!-- parameter end -->
<!-- parameter start -->

latitude

Decimal

緯度

<!-- parameter end -->
<!-- parameter start -->

longitude

Decimal

経度

<!-- parameter end -->

_位置情報メッセージの例_

<!-- tab start `json` -->

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "replyToken": "nHuyWiB7yP5Zw52FIkcQobQuGDXCTA",
      "type": "message",
      "mode": "active",
      "timestamp": 1462629479859,
      "source": {
        "type": "user",
        "userId": "U4af4980629..."
      },
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      },
      "message": {
        "id": "325708",
        "type": "location",
        "markAsReadToken": "30yhdy232...",
        "title": "my location",
        "address": "日本、〒102-8282 東京都千代田区紀尾井町1番3号",
        "latitude": 35.67966,
        "longitude": 139.73669
      }
    }
  ]
}
```

<!-- tab end -->

#### スタンプ 

送信元から送られたスタンプデータを含むメッセージオブジェクトです。LINEの基本的なスタンプとスタンプIDについては、[スタンプ](https://developers.line.biz/ja/docs/messaging-api/sticker-list/)を参照してください。

<!-- tip start -->

**スタンプ画像は取得できません**

ユーザーが送信したスタンプのパッケージIDやスタンプIDなどはWebhookで取得できますが、スタンプ画像そのものを取得することはできません。

<!-- tip end -->

<!-- tip start -->

**スタンプアレンジ機能には対応していません**

Messaging APIは、現時点ではスタンプアレンジ機能に対応していないため、どんなスタンプを組み合わせたかという情報は取得できません。ユーザーがスタンプアレンジ機能を用いてスタンプメッセージを送った場合、Webhookでは一律で以下のスタンプ情報が届きます。

- パッケージID：`30563`
- スタンプID：`651698630`
- スタンプのリソースタイプ：`STATIC`

<!-- tip end -->

<!-- parameter start -->

id

String

メッセージID

<!-- parameter end -->
<!-- parameter start -->

type

String

`sticker`

<!-- parameter end -->
<!-- parameter start -->

quoteToken

String

メッセージの引用トークン。詳しくは、『Messaging APIドキュメント』の「[引用トークンを取得する](https://developers.line.biz/ja/docs/messaging-api/get-quote-tokens/)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

markAsReadToken

String

既読トークン。このトークンを使用することで、メッセージに既読をつけることができます。有効期限はありません。詳しくは、『Messaging APIドキュメント』の「[メッセージに既読をつける](https://developers.line.biz/ja/docs/messaging-api/mark-as-read/)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

packageId

String

パッケージID

<!-- parameter end -->
<!-- parameter start -->

stickerId

String

スタンプID

<!-- parameter end -->
<!-- parameter start -->

stickerResourceType

String

スタンプのリソースタイプ。以下のいずれかの値です。

- `STATIC`：静止画スタンプ
- `ANIMATION`：アニメーションスタンプ
- `SOUND`：サウンドスタンプ
- `ANIMATION_SOUND`：アニメーション＋サウンドスタンプ
- `POPUP`：ポップアップスタンプまたはエフェクトスタンプ
- `POPUP_SOUND`：ポップアップ＋サウンドスタンプまたはエフェクト＋サウンドスタンプ
- `CUSTOM`：カスタムスタンプ。ユーザーが入力した任意のテキストは取得できません。
- `MESSAGE`：メッセージスタンプ
- `NAME_TEXT`：カスタムスタンプ（廃止）
- `PER_STICKER_TEXT`：メッセージスタンプ（廃止）

<!-- note start -->

**stickerResourceTypeについて**

今後、新しいリソースタイプが予告なく追加される可能性があります。将来、従来と異なるリソースタイプを受信しても不具合が発生しないように、サーバーを実装してください。

<!-- note end -->

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

keywords

Array of strings

スタンプを表すキーワード。最大15個の文字列が含まれる配列です。16個以上のキーワードを持つスタンプの場合は、その中からランダムに15個のキーワードを返します。そのため同じスタンプでも、異なるキーワードが返ることがあります。

<!-- note start -->

**keywordsについて**

`keywords`プロパティは、現在試験的に提供しています。そのため、今後予告なく仕様が変更されたり、提供を終了する可能性があります。

<!-- note end -->

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

text

String

ユーザーが入力した任意のテキスト。このプロパティは、メッセージスタンプの場合のみ含まれます。\
最大文字数：100

<!-- tip start -->

**カスタムスタンプの場合はテキストは取得できません**

カスタムスタンプの場合は、ユーザーが入力した任意のテキストは取得できません。

<!-- tip end -->

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

quotedMessageId

String

引用されたメッセージのメッセージID。過去のメッセージを引用している場合にのみ含まれます。

<!-- parameter end -->

_スタンプメッセージの例_

<!-- tab start `json` -->

```json
// アニメーションスタンプの例
{
    "destination": "xxxxxxxxxx",
    "events": [
        {
            "replyToken": "nHuyWiB7yP5Zw52FIkcQobQuGDXCTA",
            "type": "message",
            "mode": "active",
            "timestamp": 1462629479859,
            "source": {
                "type": "user",
                "userId": "U4af4980629..."
            },
            "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
            "deliveryContext": {
                "isRedelivery": false
            },
            "message": {
                "type": "sticker",
                "id": "1501597916",
                "quoteToken": "q3Plxr4AgKd...",
                "markAsReadToken": "30yhdy232...",
                "stickerId": "52002738",
                "packageId": "11537",
                "stickerResourceType": "ANIMATION",
                "keywords": [
                    "cony",
                    "sally",
                    "Staring",
                    "hi",
                    "whatsup",
                    "line",
                    "howdy",
                    "HEY",
                    "Peeking",
                    "wave",
                    "peek",
                    "Hello",
                    "yo",
                    "greetings"
                ]
            }
        }
    ]
}

// メッセージスタンプの例
{
    "destination": "xxxxxxxxxx",
    "events": [
        {
            "type": "message",
            "message": {
                "type": "sticker",
                "id": "123456789012345678",
                "quoteToken": "q3Plxr4AgKd...",
                "markAsReadToken": "30yhdy232...",
                "stickerId": "738839",
                "packageId": "12287",
                "stickerResourceType": "MESSAGE",
                "keywords": [
                    "Anticipation",
                    "Sparkle",
                    "Straight face",
                    "Staring",
                    "Thinking"
                ],
                "text": "今週末\n一緒に\n遊ぼうよ！"
            },
            "timestamp": 1635756190879,
            "source": {
                "type": "group",
                "groupId": "C99ae82bcd...",
                "userId": "Ub82c8fd9b..."
            },
            "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
            "deliveryContext": {
                "isRedelivery": false
            },
            "replyToken": "ce8c57ec18374a4b94f40abab97145f8",
            "mode": "active"
        }
    ]
}
```

<!-- tab end -->

### 送信取消イベント 

ユーザーがメッセージの送信を取り消したことを示すイベントです。

ユーザーがメッセージの送信を取り消すと、ボットサーバーに送信取消イベントが届きます。送信取消イベントを受け取った場合、サービス提供者はユーザーがメッセージの送信を取り消した意図を尊重し、以降は対象のメッセージを見たり利用したりできないよう、最大限の配慮を持って対象のメッセージを適切に扱うことを推奨します。詳しくは、『Messaging APIドキュメント』の「[送信取消イベント受信時の処理](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#webhook-unsend-message)」を参照してください。

<!-- parameter start -->

timestamp、sourceなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

type

String

`unsend`

<!-- parameter end -->
<!-- parameter start -->

unsend.messageId

String

送信を取り消したメッセージのID

<!-- parameter end -->

_送信取消イベントの例_

<!-- tab start `json` -->

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "type": "unsend",
      "mode": "active",
      "timestamp": 1462629479859,
      "source": {
        "type": "group",
        "groupId": "Ca56f94637c...",
        "userId": "U4af4980629..."
      },
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      },
      "unsend": {
        "messageId": "325708"
      }
    }
  ]
}
```

<!-- tab end -->

### フォローイベント 

LINE公式アカウントが友だち追加またはブロック解除されたことを示すイベントです。フォローイベントには応答できます。

<!-- parameter start -->

timestamp、sourceなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

type

String

`follow`

<!-- parameter end -->
<!-- parameter start -->

replyToken

String

このイベントに対して[応答メッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)際に使用する応答トークン

<!-- parameter end -->
<!-- parameter start -->

follow.isUnblocked

Boolean

- `true`：ユーザーがLINE公式アカウントをブロック解除しました。
- `false`：ユーザーがLINE公式アカウントを友だち追加しました。

<!-- note start -->

**follow.isUnblockedの正確性について**

`follow.isUnblocked`プロパティは、「友だち追加」および「ブロック解除」の完全な正確性を保証するものではありません。

<!-- note end -->

<!-- parameter end -->

_フォローイベントの例_

<!-- tab start `json` -->

```json
// LINE公式アカウントを友だち追加した場合
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "replyToken": "85cbe770fa8b4f45bbe077b1d4be4a36",
      "type": "follow",
      "mode": "active",
      "timestamp": 1705891467176,
      "source": {
        "type": "user",
        "userId": "U3d3edab4f36c6292e6d8a8131f141b8b"
      },
      "webhookEventId": "01HMQGW40RZJPJM3RAJP7BHC2Q",
      "deliveryContext": {
        "isRedelivery": false
      },
      "follow": {
        "isUnblocked": false
      }
    }
  ]
}

// LINE公式アカウントをブロック解除した場合
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "replyToken": "nHuyWiB7yP5Zw52FIkcQobQuGDXCTA",
      "type": "follow",
      "mode": "active",
      "timestamp": 1462629479859,
      "source": {
        "type": "user",
        "userId": "U4af4980629..."
      },
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      },
      "follow": {
        "isUnblocked": true
      }
    }
  ]
}
```

<!-- tab end -->

### フォロー解除イベント 

LINE公式アカウントがブロックされたことを示すイベントです。

<!-- parameter start -->

timestamp、sourceなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

type

String

`unfollow`

<!-- parameter end -->

_フォロー解除イベントの例_

<!-- tab start `json` -->

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "type": "unfollow",
      "mode": "active",
      "timestamp": 1462629479859,
      "source": {
        "type": "user",
        "userId": "U4af4980629..."
      },
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      }
    }
  ]
}
```

<!-- tab end -->

### 参加イベント 

LINE公式アカウントが[グループトーク](https://developers.line.biz/ja/docs/messaging-api/group-chats/#group)や[複数人トーク](https://developers.line.biz/ja/docs/messaging-api/group-chats/#room)に参加したことを示すイベントです。参加イベントには応答できます。

参加イベントが送信されるタイミングはグループトークと複数人トークで異なります。

- グループトークの場合：ユーザーがLINE公式アカウントを招待したときに送信されます。
- 複数人トークの場合：LINE公式アカウントが複数人トークに追加された後で、最初に何らかのイベントが発生したときに送信されます。たとえば、ユーザーがメッセージを送ったり、ユーザーが複数人トークに追加されたりしたときです。

<!-- parameter start -->

timestamp、sourceなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

type

String

`join`

<!-- parameter end -->
<!-- parameter start -->

replyToken

String

このイベントに対して[応答メッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)際に使用する応答トークン

<!-- parameter end -->

_参加イベントの例_

<!-- tab start `json` -->

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "replyToken": "nHuyWiB7yP5Zw52FIkcQobQuGDXCTA",
      "type": "join",
      "mode": "active",
      "timestamp": 1462629479859,
      "source": {
        "type": "group",
        "groupId": "C4af4980629..."
      },
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      }
    }
  ]
}
```

<!-- tab end -->

### 退出イベント 

ユーザーが[グループトーク](https://developers.line.biz/ja/docs/messaging-api/group-chats/#group)からLINE公式アカウントを削除したか、LINE公式アカウントが[グループトーク](https://developers.line.biz/ja/docs/messaging-api/group-chats/#group)または[複数人トーク](https://developers.line.biz/ja/docs/messaging-api/group-chats/#room)から退出したことを示すイベントです。

<!-- parameter start -->

timestamp、sourceなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

type

String

`leave`

<!-- parameter end -->

_退出イベントの例_

<!-- tab start `json` -->

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "type": "leave",
      "mode": "active",
      "timestamp": 1462629479859,
      "source": {
        "type": "group",
        "groupId": "C4af4980629..."
      },
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      }
    }
  ]
}
```

<!-- tab end -->

### メンバー参加イベント 

LINE公式アカウントがメンバーになっている[グループトーク](https://developers.line.biz/ja/docs/messaging-api/group-chats/#group)または[複数人トーク](https://developers.line.biz/ja/docs/messaging-api/group-chats/#room)にユーザーが参加したことを示すイベントです。

<!-- parameter start -->

timestamp、sourceなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

type

String

`memberJoined`

<!-- parameter end -->
<!-- parameter start -->

joined.members

Array

参加したユーザー。[送信元ユーザー](https://developers.line.biz/ja/reference/messaging-api/#source-user)オブジェクトの配列です。

<!-- parameter end -->
<!-- parameter start -->

replyToken

String

このイベントに対して[応答メッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)際に使用する応答トークン

<!-- parameter end -->

_メンバー参加イベントの例_

<!-- tab start `json` -->

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "replyToken": "0f3779fba3b349968c5d07db31eabf65",
      "type": "memberJoined",
      "mode": "active",
      "timestamp": 1462629479859,
      "source": {
        "type": "group",
        "groupId": "C4af4980629..."
      },
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      },
      "joined": {
        "members": [
          {
            "type": "user",
            "userId": "U4af4980629..."
          },
          {
            "type": "user",
            "userId": "U91eeaf62d9..."
          }
        ]
      }
    }
  ]
}
```

<!-- tab end -->

### メンバー退出イベント 

LINE公式アカウントがメンバーになっている[グループトーク](https://developers.line.biz/ja/docs/messaging-api/group-chats/#group)または[複数人トーク](https://developers.line.biz/ja/docs/messaging-api/group-chats/#room)からユーザーが退出したことを示すイベントです。

<!-- parameter start -->

timestamp、sourceなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

type

String

`memberLeft`

<!-- parameter end -->
<!-- parameter start -->

left.members

Array

退出したユーザー。[送信元ユーザー](https://developers.line.biz/ja/reference/messaging-api/#source-user)オブジェクトの配列です。

<!-- parameter end -->

_メンバー退出イベントの例_

<!-- tab start `json` -->

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "type": "memberLeft",
      "mode": "active",
      "timestamp": 1462629479960,
      "source": {
        "type": "group",
        "groupId": "C4af4980629..."
      },
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      },
      "left": {
        "members": [
          {
            "type": "user",
            "userId": "U4af4980629..."
          },
          {
            "type": "user",
            "userId": "U91eeaf62d9..."
          }
        ]
      }
    }
  ]
}
```

<!-- tab end -->

### ポストバックイベント 

ユーザーが、[ポストバックアクション](https://developers.line.biz/ja/reference/messaging-api/#postback-action)を実行したことを示すイベントオブジェクトです。ポストバックイベントには応答できます。

<!-- parameter start -->

timestamp、sourceなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

type

String

`postback`

<!-- parameter end -->
<!-- parameter start -->

replyToken

String

このイベントに対して[応答メッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)際に使用する応答トークン

<!-- parameter end -->
<!-- parameter start -->

postback.data

String

ポストバックデータ

<!-- parameter end -->
<!-- parameter start -->

[postback.params](https://developers.line.biz/ja/reference/messaging-api/#postback-params-object)

Object

以下のいずれかのJSONオブジェクト

- [日時選択アクションの`postback.params`オブジェクト](https://developers.line.biz/ja/reference/messaging-api/#postback-params-object)。
  - [日時選択アクション](https://developers.line.biz/ja/reference/messaging-api/#datetime-picker-action)を介してユーザーが選択した日時を含むJSONオブジェクト。
  - [日時選択アクション](https://developers.line.biz/ja/reference/messaging-api/#datetime-picker-action)によるポストバックアクションの場合にのみ返されます。
- [リッチメニュー切替アクションの`postback.params`オブジェクト](https://developers.line.biz/ja/reference/messaging-api/#postback-params-object-for-richmenu-switch-action)。
  - [リッチメニュー切替アクション](https://developers.line.biz/ja/reference/messaging-api/#richmenu-switch-action)を介してユーザーが選択したリッチメニューエイリアスIDを含むJSONオブジェクト。
  - [リッチメニュー切替アクション](https://developers.line.biz/ja/reference/messaging-api/#richmenu-switch-action)によるポストバックアクションの場合にのみ返されます。

<!-- parameter end -->

_ポストバックイベントの例_

<!-- tab start `json` -->

```json
// 日時選択アクションのポストバックイベントの場合
{
    "destination": "xxxxxxxxxx",
    "events": [
        {
            "replyToken": "b60d432864f44d079f6d8efe86cf404b",
            "type": "postback",
            "mode": "active",
            "source": {
                "userId": "U91eeaf62d...",
                "type": "user"
            },
            "timestamp": 1513669370317,
            "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
            "deliveryContext": {
                "isRedelivery": false
            },
            "postback": {
                "data": "storeId=12345",
                "params": {
                    "datetime": "2017-12-25T01:00"
                }
            }
        }
    ]
}

// リッチメニュー切替アクションのポストバックイベントの場合
{
    "destination": "xxxxxxxxxx",
    "events": [
        {
            "replyToken": "b60d432864f44d079f6d8efe86cf404b",
            "type": "postback",
            "mode": "active",
            "source": {
                "userId": "U91eeaf62d...",
                "type": "user"
            },
            "timestamp": 1619754620404,
            "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
            "deliveryContext": {
                "isRedelivery": false
            },
            "postback": {
                "data": "richmenu-changed-to-b",
                "params": {
                    "newRichMenuAliasId": "richmenu-alias-b",
                    "status": "SUCCESS"
                }
            }
        }
    ]
}
```

<!-- tab end -->

#### 日時選択アクションの`postback.params`オブジェクト 

[日時選択アクション](https://developers.line.biz/ja/reference/messaging-api/#datetime-picker-action)を介してユーザーが選択した日時を含むオブジェクトです。`full-date`、`time-hour`、および`time-minute`の形式は、[RFC3339プロトコル](https://www.ietf.org/rfc/rfc3339.txt)で定義されています。

| プロパティ | 形式 | 説明 |
| --- | --- | --- |
| date | full-date | ユーザーが選択した日付。`date`モードの場合にのみ含まれます。 |
| time | time-hour ":" time-minute | ユーザーが選択した時刻。`time`モードの場合にのみ含まれます。 |
| datetime | full-date "T" time-hour ":" time-minute | ユーザーが選択した日付と時刻。`datetime`モードの場合にのみ含まれます。 |

_日時選択アクションのpostback.paramsオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "datetime": "2017-12-25T01:00"
}
```

<!-- tab end -->

#### リッチメニュー切替アクションの`postback.params`オブジェクト 

[リッチメニュー切替アクション](https://developers.line.biz/ja/reference/messaging-api/#richmenu-switch-action)を介してユーザーが選択したリッチメニューエイリアスIDを含むオブジェクトです。

| プロパティ | 形式 | 説明 |
| --- | --- | --- |
| newRichMenuAliasId 含まれないことがあります | String | 切替先のリッチメニューエイリアスID。リッチメニューの切替に失敗した場合は含まれません。 |
| status | String | `SUCCESS`：リッチメニューが正常に変更されました。<br/>`RICHMENU_ALIAS_ID_NOTFOUND`：指定されたリッチメニューエイリアスIDが見つかりませんでした。<br/>`RICHMENU_NOTFOUND`：指定されたリッチメニューエイリアスIDに紐づくリッチメニューIDが見つかりませんでした。<br/>`FAILED`：リッチメニューの切替に失敗しました。 |

_リッチメニュー切替アクションのpostback.paramsオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "newRichMenuAliasId": "richmenu-alias-b",
  "status": "SUCCESS"
}
```

<!-- tab end -->

### 動画視聴完了イベント 

LINE公式アカウントから送信された`trackingId`が指定された動画の視聴を、ユーザーが少なくとも一回最後まで視聴したことを示すイベントです。

<!-- note start -->

**動画の視聴回数について**

動画視聴完了イベントは、ユーザーの動画視聴回数を示すものではありません。

トークルーム上で複数回動画を視聴しても、重複してイベントが発生することはありません。ただし、一度トークルームを閉じた後で再度開き動画を視聴すると、再びイベントが発生する場合があります。

<!-- note end -->

<!-- note start -->

**イメージマップメッセージおよびFlex Messageの動画は動画視聴完了イベントの対象外です**

[イメージマップメッセージ](https://developers.line.biz/ja/reference/messaging-api/#imagemap-message)および[Flex Message](https://developers.line.biz/ja/reference/messaging-api/#flex-message)の動画に`trackingId`を指定することはできません。

<!-- note end -->

<!-- parameter start -->

timestamp、sourceなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

type

String

`videoPlayComplete`

<!-- parameter end -->
<!-- parameter start -->

replyToken

String

このイベントに対して[応答メッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)際に使用する応答トークン

<!-- parameter end -->
<!-- parameter start -->

videoPlayComplete.trackingId

String

動画を識別するためのID。[動画メッセージ](https://developers.line.biz/ja/reference/messaging-api/#video-message)に付与した`trackingId`と同じ値を返します。

<!-- parameter end -->

_動画視聴完了イベントの例_

<!-- tab start `json` -->

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "replyToken": "nHuyWiB7yP5Zw52FIkcQobQuGDXCTA",
      "type": "videoPlayComplete",
      "mode": "active",
      "timestamp": 1462629479859,
      "source": {
        "type": "user",
        "userId": "U4af4980629..."
      },
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      },
      "videoPlayComplete": {
        "trackingId": "track-id"
      }
    }
  ]
}
```

<!-- tab end -->

### ビーコンイベント 

[ビーコン](https://developers.line.biz/ja/docs/messaging-api/using-beacons/)の電波の受信圏にユーザーが入ったことを示すイベントオブジェクトです。ビーコンイベントには応答できます。

<!-- parameter start -->

timestamp、sourceなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

type

String

`beacon`

<!-- parameter end -->
<!-- parameter start -->

replyToken

String

このイベントに対して[応答メッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)際に使用する応答トークン

<!-- parameter end -->
<!-- parameter start -->

beacon.hwid

String

検出されたビーコンのハードウェアID

<!-- parameter end -->
<!-- parameter start -->

beacon.type

String

ビーコンイベントのタイプ。「[ビーコンイベントのタイプ](https://developers.line.biz/ja/reference/messaging-api/#beacon-event-types)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

beacon.dm

String

検出されたビーコンのデバイスメッセージ。このメッセージは、ボットサーバーへの通知を目的としてビーコンにより生成されるデータです。Device messageプロパティをサポートするデバイスからのWebhookイベントにのみ含まれます。\
詳しくは、[LINE Simple Beaconの仕様](https://github.com/line/line-simple-beacon/blob/master/README.ja.md#line-simple-beacon-frame)を参照してください。

<!-- parameter end -->

_ビーコンイベントの例_

<!-- tab start `json` -->

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "replyToken": "nHuyWiB7yP5Zw52FIkcQobQuGDXCTA",
      "type": "beacon",
      "mode": "active",
      "timestamp": 1462629479859,
      "source": {
        "type": "user",
        "userId": "U4af4980629..."
      },
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      },
      "beacon": {
        "hwid": "d41d8cd98f",
        "type": "enter"
      }
    }
  ]
}
```

<!-- tab end -->

#### ビーコンイベントのタイプ 

| beacon.type | 説明 |
| --- | --- |
| `enter` | ユーザーがビーコンの電波の受信圏に入りました。 |
| `banner` | ユーザーが[ビーコンバナー](https://developers.line.biz/ja/docs/messaging-api/using-beacons/#beacon-banner)をタップしました。 |
| `stay` | ユーザーがビーコンの電波の受信圏に滞在しています。<br />このイベントは、最短10秒間隔で繰り返し送信されます。 |

<!-- note start -->

**日本では利用受付は停止しています**

2021年1月現在、日本では`banner`および`stay`イベントの新規利用受付は停止していますが、それ以外の地域では継続しています。

<!-- note end -->

### アカウント連携イベント 

ユーザーがLINEアカウントとプロバイダーが提供するサービスのアカウントを連携したことを示すイベントオブジェクトです。アカウント連携イベントには応答できます。

連携トークンの期限が切れている、または使用済みの場合は、Webhookイベント自体が送信されず、ユーザーにエラーが表示されます。

<!-- parameter start -->

timestamp、sourceなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

アカウントの連携に失敗した場合、`source`プロパティはアカウント連携イベントに含まれません。

<!-- parameter end -->
<!-- parameter start -->

type

String

`accountLink`

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

replyToken

String

このイベントに対して[応答メッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)際に使用する応答トークン。アカウントの連携に失敗した場合、このプロパティは含まれません。

<!-- parameter end -->
<!-- parameter start -->

link.result

String

アカウントの連携が成功したかどうかを示す値。以下のどちらかになります。

- `ok`：アカウントの連携が成功したことを示します。
- `failed`：ユーザーのすり替えなどが原因で、アカウントの連携が失敗したことを示します。

<!-- parameter end -->
<!-- parameter start -->

link.nonce

String

ユーザーIDの検証時に指定したnonce（number used once）。詳しくは、『Messaging APIドキュメント』の「[nonceを生成してユーザーをLINEプラットフォームにリダイレクトする](https://developers.line.biz/ja/docs/messaging-api/linking-accounts/#step-four-verifying-user-id)」を参照してください。

<!-- parameter end -->

_アカウント連携イベントの例_

<!-- tab start `json` -->

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "replyToken": "b60d432864f44d079f6d8efe86cf404b",
      "type": "accountLink",
      "mode": "active",
      "source": {
        "userId": "U91eeaf62d...",
        "type": "user"
      },
      "timestamp": 1513669370317,
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      },
      "link": {
        "result": "ok",
        "nonce": "xxxxxxxxxxxxxxx"
      }
    }
  ]
}
```

<!-- tab end -->

### メンバーシップイベント 

ユーザーがLINE公式アカウントのメンバーシップに加入や継続課金、またはメンバーシップを退会したことを示すイベントです。

LINE公式アカウントがメンバーシップで複数のプランを提供している場合において、あるプランに加入中のユーザーが当月中に別のプランに変更したときは、退会と加入に関するWebhookイベントが送信されます。なお、ユーザーがプロフィール情報の取得に同意していない場合は、Webhookイベントは送信されません。詳しくは、『Messaging APIドキュメント』の「[ユーザーのプロフィール情報取得の同意](https://developers.line.biz/ja/docs/messaging-api/user-consent/)」を参照してください。

<!-- parameter start -->

timestamp、sourceなど

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

type

String

`membership`

<!-- parameter end -->
<!-- parameter start -->

replyToken

String

このイベントに対して[応答メッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)際に使用する応答トークン

<!-- parameter end -->
<!-- parameter start -->

membership.type

String

メンバーシップイベントのタイプ。以下のいずれかの値です。

- `joined`：ユーザーがメンバーシップに加入した。
- `left`：ユーザーがメンバーシップを退会した。
- `renewed`：ユーザーがメンバーシップに継続課金した。

<!-- parameter end -->
<!-- parameter start -->

membership.membershipId

Number

ユーザーが加入、退会または継続課金したメンバーシップのID

<!-- parameter end -->

_メンバーシップイベントの例_

<!-- tab start `json` -->

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "type": "membership",
      "source": {
        "type": "user",
        "userId": "U4af4980629..."
      },
      "replyToken": "nHuyWiB7yP5Zw52FIkcQobQuGDXCTA",
      "membership": {
        "type": "joined",
        "membershipId": 3189
      },
      "timestamp": 1462629479859,
      "mode": "active",
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      }
    }
  ]
}
```

<!-- tab end -->

## Webhook設定 

チャネルのWebhookエンドポイントを設定、検証、取得します。

### WebhookエンドポイントのURLを設定する 

Endpoint: `PUT` `https://api.line.me/v2/bot/channel/webhook/endpoint`

WebhookエンドポイントのURLを設定します。キャッシュデータの影響により、URLの更新に1分ほどかかる場合があります。

<!-- note start -->

**Webhook URLの検証ルール**

以下のWebhook URLの検証ルールをすべて満たしていることを確認してください。

- 有効なHTTPS URLである。
- URLの長さが500文字以内である。

<!-- note end -->

_リクエスト例_

<!-- tab start `shell` -->

```sh
curl -X PUT \
-H 'Authorization: Bearer {CHANNEL_ACCESS_TOKEN}' \
-H 'Content-Type:application/json' \
-d '{"endpoint":"https://example.com/hoge"}' \
https://api.line.me/v2/bot/channel/webhook/endpoint
```

<!-- tab end -->

#### レート制限 

1,000リクエスト/分

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

`application/json`

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

endpoint

String

有効なWebhook URL

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と空のJSONオブジェクトを返します。

_レスポンス例_

<!-- tab start `json` -->

```json
{}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | 無効なWebhook URLが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なWebhook URLが指定された場合（400 Bad Request）
{
  "message": "Invalid webhook endpoint URL"
}
```

<!-- tab end -->

### Webhookエンドポイントの情報を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/channel/webhook/endpoint`

Webhookエンドポイントの情報を取得します。

_リクエスト例_

<!-- tab start `shell` -->

```sh
curl -X GET \
-H 'Authorization: Bearer {CHANNEL_ACCESS_TOKEN}' \
-H 'Content-Type:application/json' \
https://api.line.me/v2/bot/channel/webhook/endpoint
```

<!-- tab end -->

#### レート制限 

1,000リクエスト/分

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

`application/json`

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

endpoint

String

Webhook URL

<!-- parameter end -->
<!-- parameter start -->

active

Boolean

Webhookの利用ステータス。有効の場合のみ、LINEプラットフォームからWebhook URLにWebhookイベントを送信します。

- `true`：Webhookの利用が有効です。
- `false`：Webhookの利用が無効です。

<!-- parameter end -->

_レスポンス例_

<!-- tab start `json` -->

```json
// Webhook URLが設定されていて、Webhookの利用が有効になっている場合
{
  "endpoint": "https://example.com/test",
  "active": true
}

// Webhook URLが設定されていて、Webhookの利用が無効になっている場合
{
  "endpoint": "https://example.com/test",
  "active": false
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `404` | チャネルにWebhook URLが設定されていません。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// Webhook URLが設定されていない場合（404 Not Found）
{
  "message": "Webhook endpoint not found"
}
```

<!-- tab end -->

### Webhookエンドポイントを検証する 

Endpoint: `POST` `https://api.line.me/v2/bot/channel/webhook/test`

設定したWebhookエンドポイントがWebhookの検証イベントを受信できるかを確認します。

<!-- note start -->

**Webhook URLの検証ルール**

以下のWebhook URLの検証ルールをすべて満たしていることを確認してください。

- 有効なHTTPS URLである。
- URLの長さが500文字以内である。

<!-- note end -->

_リクエスト例_

<!-- tab start `shell` -->

```sh
# URLを指定して検証したい場合
curl -X POST \
-H 'Authorization: Bearer {CHANNEL_ACCESS_TOKEN}' \
-H 'Content-Type:application/json' \
-d '{"endpoint":"https://example.com/webhook"}' \
https://api.line.me/v2/bot/channel/webhook/test

# LINE Developersコンソールの「Webhook URL」で設定したURLを検証したい場合
curl -X POST \
-H 'Authorization: Bearer {CHANNEL_ACCESS_TOKEN}' \
-H 'Content-Type:application/json' \
-d '{}' \
https://api.line.me/v2/bot/channel/webhook/test
```

<!-- tab end -->

#### レート制限 

60リクエスト/時

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

`application/json`

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: optional) -->

endpoint

String

検証したいWebhook URL

<!-- note start -->

**endpointパラメータ有無による動作の違い**

このエンドポイントは、**Request body**に`endpoint`パラメータが含まれるかどうかで動作が変わります。

**endpointパラメータがある場合**

`endpoint`パラメータに指定したエンドポイントURLが有効か検証し、有効であれば指定されたエンドポイントURLにWebhook検証イベントを送信します。

**endpointパラメータがない場合**

チャネルに設定されているWebhookエンドポイントに、Webhook検証イベントを送信します。チャネルにWebhookエンドポイントが設定されていない場合は `404`が返ります。

<!-- note end -->

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`とおよび以下の情報を含むJSONオブジェクトを返す。

<!-- note start -->

**疎通確認のリクエストにはステータスコード200を返してください**

- 疎通確認の際は、LINEプラットフォームからWebhook URL（ボットサーバー）へ、Webhookイベントが含まれないHTTP POSTリクエストが送信されます。ステータスコード`200`を返すようにボットサーバーを設計してください。

  Webhookイベントが含まれないHTTP POSTリクエストの例：

  ```json
  {
    "destination": "xxxxxxxxxx",
    "events": []
  }
  ```

<!-- note end -->

<!-- parameter start -->

success

Boolean

LINEプラットフォームからWebhook URLへの疎通結果

- `true`：成功
- `false`：失敗

`false`の場合は、『Messaging APIドキュメント』の「[エラーが発生した原因を確認する](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#check-error-reason)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

timestamp

String

「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

statusCode

Number

HTTPステータスコード。Webhookのレスポンスを受信しなかった場合、ステータスコードは0か負の数になります。

<!-- parameter end -->
<!-- parameter start -->

reason

String

レスポンスの原因を表します。詳細は下表を参照してください。

<!-- parameter end -->
<!-- parameter start -->

detail

String

レスポンスの詳細を表します。詳細は下表を参照してください。

<!-- parameter end -->

| `reason`（原因） | `detail`（詳細） | 内容 |
| --- | --- | --- |
| OK | HTTPステータスコード（例：`200`） | Webhookの送信に成功しました。 |
| [COULD_NOT_CONNECT](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#reason-could-not-connect) | 接続失敗 | Webhookエンドポイントに接続できませんでした。詳しくは、『Messaging APIドキュメント』の「[原因が「could_not_connect」の場合](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#reason-could-not-connect)」を参照してください。 |
| [REQUEST_TIMEOUT](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#reason-request-timeout) | Request timeout | リクエストがタイムアウトしました。詳しくは、『Messaging APIドキュメント』の「[原因が「request_timeout」の場合](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#reason-request-timeout)」を参照してください。 |
| [ERROR_STATUS_CODE](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#reason-status-code) | HTTPステータスコード（例：`400`） | エラーレスポンスのステータスコードが返ります。詳しくは、『Messaging APIドキュメント』の「[原因が「error_status_code」の場合](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#reason-status-code)」を参照してください。 |
| [UNCLASSIFIED](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#reason-unclassified) | N/A | 不明なエラーです。詳しくは、『Messaging APIドキュメント』の「[原因が「unclassified」の場合](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#reason-unclassified)」を参照してください。 |

_レスポンスの例（Webhookの送信に成功した場合）_

<!-- tab start `json` -->

```json
{
  "success": true,
  "timestamp": "2020-09-30T05:38:20.031Z",
  "statusCode": 200,
  "reason": "OK",
  "detail": "200"
}
```

<!-- tab end -->

_レスポンスの例（ボットサーバーのSSL/TLS設定が原因でWebhook URLへの疎通に失敗した場合）_

<!-- tab start `json` -->

```json
{
  "success": false,
  "timestamp": "2023-07-07T04:29:51.043124Z",
  "statusCode": 0,
  "reason": "COULD_NOT_CONNECT",
  "detail": "TLS handshake failure: https://example.com/webhook"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明                                        |
| ------ | ------------------------------------------- |
| `400`  | 無効なWebhook URLが指定されています。       |
| `404`  | チャネルにWebhook URLが設定されていません。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// Webhook URLで指定したドメイン名が名前解決できなかった場合（400 Bad Request）
{
  "message": "Invalid webhook endpoint URL"
}

// Webhook URLが設定されていない場合（404 Not Found）
{
  "message": "Webhook endpoint not found"
}
```

<!-- tab end -->

## コンテンツ取得 

ユーザーがLINE公式アカウントに対して送信したコンテンツを、[Webhook](https://developers.line.biz/ja/reference/messaging-api/#webhooks)で受信したメッセージIDを使うことで取得できます。

### コンテンツを取得する 

Endpoint: `GET` `https://api-data.line.me/v2/bot/message/{messageId}/content`

<!-- note start -->

**他のエンドポイントとドメイン名が異なります**

このエンドポイントは、Messaging APIにおけるLINEプラットフォームへの大容量データ送受信用のドメイン名（`api-data.line.me`）です。他のエンドポイントのドメイン名（`api.line.me`）とは異なるため、利用時は注意してください。

<!-- note end -->

Webhookで受信したメッセージIDを使って、ユーザーが送信した[画像](https://developers.line.biz/ja/reference/messaging-api/#wh-image)、[動画](https://developers.line.biz/ja/reference/messaging-api/#wh-video)、[音声](https://developers.line.biz/ja/reference/messaging-api/#wh-audio)、および[ファイル](https://developers.line.biz/ja/reference/messaging-api/#wh-file)を取得するエンドポイントです。

このエンドポイントは、[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`contentProvider.type`プロパティが`line`の場合にのみ利用できます。

ユーザーからデータサイズが大きい動画または音声が送られた場合に、コンテンツのバイナリデータを取得できるようになるまで時間がかかるときがあります。バイナリデータの準備中にコンテンツを取得しようとすると、ステータスコード`202`が返されバイナリデータは取得できません。バイナリデータが取得できるかどうかは、[動画または音声の取得準備の状況を確認する](https://developers.line.biz/ja/reference/messaging-api/#verify-video-or-audio-preparation-status)エンドポイントで確認できます。

なお、ユーザーが送信したコンテンツは、縮小などの変換が内部的に行われる場合があります。

<!-- note start -->

**テキストはAPIでは取得できません**

ユーザーが送信したテキストは、Webhookの[テキスト](https://developers.line.biz/ja/reference/messaging-api/#wh-text)メッセージオブジェクトで受信できます。Webhookを受信した後で、あらためてテキストを取得するためのAPIはありません。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api-data.line.me/v2/bot/message/{messageId}/content \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

messageId

メッセージID

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`とコンテンツのバイナリデータを返します。バイナリデータのファイル形式は、レスポンスの[`Content-Type`](https://developer.mozilla.org/ja/docs/Web/HTTP/Reference/Headers/Content-Type)ヘッダーで示されます。

メッセージが送信されてから一定期間後に、コンテンツは自動的に削除されます。コンテンツの保存期間は保証されません。

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

- `404 Not Found`
- `410 Gone`

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 存在しないメッセージIDを指定した場合（404 Not Found）
{
  "message": "not found"
}

// ユーザーがメッセージの送信を取り消した場合（410 Gone）
{
  "message": "The content is gone"
}
```

<!-- tab end -->

### 動画または音声の取得準備の状況を確認する 

Endpoint: `GET` `https://api-data.line.me/v2/bot/message/{messageId}/content/transcoding`

<!-- note start -->

**他のエンドポイントとドメイン名が異なります**

このエンドポイントは、Messaging APIにおけるLINEプラットフォームへの大容量データ送受信用のドメイン名（`api-data.line.me`）です。他のエンドポイントのドメイン名（`api.line.me`）とは異なるため、利用時は注意してください。

<!-- note end -->

Webhookで受信したメッセージIDを使って、ユーザーが送信した[動画](https://developers.line.biz/ja/reference/messaging-api/#wh-video)、[音声](https://developers.line.biz/ja/reference/messaging-api/#wh-audio)の取得準備の状況を取得するエンドポイントです。

このエンドポイントは、[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`contentProvider.type`プロパティが`line`の場合にのみ利用できます。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api-data.line.me/v2/bot/message/{messageId}/content/transcoding \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

messageId

[動画](https://developers.line.biz/ja/reference/messaging-api/#wh-video)または[音声](https://developers.line.biz/ja/reference/messaging-api/#wh-audio)のメッセージID

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

status

String

取得準備の状況。以下のいずれかの値です。

- `processing`：コンテンツの取得準備中です。
- `succeeded`：コンテンツを取得する準備が完了しました。ユーザーが送信した[コンテンツを取得](https://developers.line.biz/ja/reference/messaging-api/#get-content)できます。
- `failed`：コンテンツの取得準備に失敗しました。

<!-- parameter end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

- `400 Bad Request`
- `404 Not Found`
- `410 Gone`

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 動画、音声以外のメッセージIDを指定した場合（400 Bad Request）
{
  "message": "Transcoding status doesn't support this type of content"
}

// 存在しないメッセージIDを指定した場合（404 Not Found）
{
  "message": "not found"
}

// ユーザーがメッセージの送信を取り消した場合（410 Gone）
{
  "message": "The content is gone"
}
```

<!-- tab end -->

### 画像または動画のプレビュー画像を取得する 

Endpoint: `GET` `https://api-data.line.me/v2/bot/message/{messageId}/content/preview`

<!-- note start -->

**他のエンドポイントとドメイン名が異なります**

このエンドポイントは、Messaging APIにおけるLINEプラットフォームへの大容量データ送受信用のドメイン名（`api-data.line.me`）です。他のエンドポイントのドメイン名（`api.line.me`）とは異なるため、利用時は注意してください。

<!-- note end -->

Webhookで受信したメッセージIDを使って、ユーザーが送信した[画像](https://developers.line.biz/ja/reference/messaging-api/#wh-image)、[動画](https://developers.line.biz/ja/reference/messaging-api/#wh-video)のプレビュー画像を取得するエンドポイントです。プレビュー画像は、実際のコンテンツよりも軽量なデータサイズに変換した画像データです。

このエンドポイントは、[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`contentProvider.type`プロパティが`line`の場合にのみ利用できます。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api-data.line.me/v2/bot/message/{messageId}/content/preview \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

messageId

[画像](https://developers.line.biz/ja/reference/messaging-api/#wh-image)または[動画](https://developers.line.biz/ja/reference/messaging-api/#wh-video)のメッセージID

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`とプレビュー画像のバイナリデータを返します。

メッセージが送信されてから一定期間後に、プレビュー画像は自動的に削除されます。プレビュー画像の保存期間は保証されません。

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

- `400 Bad Request`
- `404 Not Found`
- `410 Gone`

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 画像、動画以外のメッセージIDを指定した場合（400 Bad Request）
{
  "message": "The content can not be previewed"
}

// 存在しないメッセージIDを指定した場合（404 Not Found）
{
  "message": "not found"
}

// ユーザーがメッセージの送信を取り消した場合（410 Gone）
{
  "message": "The content is gone"
}
```

<!-- tab end -->

## チャネルアクセストークン 

アプリからMessaging APIを呼び出す際に必要となるチャネルアクセストークンを発行、取得、取り消しします。詳しくは、『LINEプラットフォームの基礎知識』の「[チャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/)」を参照してください。

### チャネルアクセストークンv2.1を発行する 

Endpoint: `POST` `https://api.line.me/oauth2/v2.1/token`

任意の有効期間を指定できるチャネルアクセストークンを発行します。このメソッドでは、認証にJWTアサーションを使用できます。

チャネルアクセストークンv2.1は、チャネルごとに30件まで発行できます。上限に達した場合は、追加発行のリクエストは拒否されます。なお、有効期限が切れたチャネルアクセストークンは、発行数としてカウントされません。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/oauth2/v2.1/token \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_assertion_type=urn:ietf:params:oauth:client-assertion-type:jwt-bearer' \
--data-urlencode 'client_assertion={JWT}'
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

`client_credentials`

<!-- parameter end -->
<!-- parameter start (props: required) -->

client_assertion_type

String

`urn:ietf:params:oauth:client-assertion-type:jwt-bearer`をURLエンコードした値

<!-- parameter end -->
<!-- parameter start (props: required) -->

client_assertion

String

JSON Web Tokenアサーションを指定します。JWTアサーションは、クライアント側で生成した上で、アサーション署名キーの秘密鍵で署名する必要があります。

JWTアサーションは、生成されてから30分以内に失効するように設定する必要があります。JWTアサーションの生成について詳しくは、「[JWTを生成する](https://developers.line.biz/ja/docs/messaging-api/generate-json-web-token/#generate-jwt)」を参照してください。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

access_token

String

チャネルアクセストークン

<!-- parameter end -->
<!-- parameter start -->

expires_in

Number

チャネルアクセストークンが発行されてから有効期限が切れるまでの秒数

<!-- parameter end -->
<!-- parameter start -->

token_type

String

`Bearer`

<!-- parameter end -->
<!-- parameter start -->

key_id

String

チャネルアクセストークンを識別するための一意のキーID

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "access_token": "eyJhbGciOiJIUz.....",
  "token_type": "Bearer",
  "expires_in": 2592000,
  "key_id": "sDTOzw5wIfxxxxPEzcmeQA"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>JWTアサーションの検証に失敗した。</li><li>JWTアサーションの有効期限が切れている。</li><li>チャネルアクセストークンを発行できる上限に達している。</li></ul> |
| `404` | JWTアサーションと紐づく署名キーがチャネルに登録されていません。 |

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// チャネルアクセストークンを発行できる上限に達している場合（400 Bad Request）
{
  "message": "The maximum number of access tokens has already been issued"
}

// JWTアサーションの検証に失敗した場合（400 Bad Request）
{
  "error": "invalid_client",
  "error_description": "iss and clientId of key do not match"
}

// JWTアサーションと紐づく署名キーがチャネルに登録されていない場合（404 Not Found）
{
  "message": "Cannot find channel key that satisfies the conditions"
}
```

<!-- tab end -->

### チャネルアクセストークンv2.1の有効性を検証する 

Endpoint: `GET` `https://api.line.me/oauth2/v2.1/verify`

[任意の有効期間を指定できるチャネルアクセストークン（チャネルアクセストークンv2.1）](https://developers.line.biz/ja/docs/basics/channel-access-token/#user-specified-expiration)の有効性を検証できます。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/oauth2/v2.1/verify \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'access_token=eyJhbGciOiJIUzI1NiJ9.UnQ_o-GP0VtnwDjbK0C8E_NvK...' \
-G
```

<!-- tab end -->

#### クエリパラメータ 

<!-- parameter start (props: required) -->

access_token

任意の有効期間を指定できるチャネルアクセストークン（チャネルアクセストークンv2.1）。

<!-- parameter end -->

#### レスポンス 

チャネルアクセストークンが有効な場合は、ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

client_id

String

チャネルアクセストークンが発行されたチャネルID。

<!-- parameter end -->
<!-- parameter start -->

expires_in

Number

チャネルアクセストークンの有効期限が切れるまでの秒数。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

scope

String

チャネルアクセストークンに付与されている権限。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "client_id": "1573163733",
  "expires_in": 2591659,
  "scope": "profile chat_message.write"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>無効なフォーマットのチャネルアクセストークンが指定されている。</li><li>チャネルアクセストークンの有効期限が切れている。</li><li>存在しないチャネルアクセストークンが指定されている。</li></ul> |

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// チャネルアクセストークンの有効期限が切れていた場合（400 Bad Request）
{
    "error": "invalid_request",
    "error_description": "The access token expired"
}

// 無効なフォーマットのチャネルアクセストークンが指定された場合（400 Bad Request）
{
    "error": "invalid_request",
    "error_description": "The access token not JWS"
}
```

<!-- tab end -->

### すべての有効なチャネルアクセストークンv2.1のキーIDを取得する 

Endpoint: `GET` `https://api.line.me/oauth2/v2.1/tokens/kid`

すべての有効なチャネルアクセストークンのキーIDを取得します。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -X GET https://api.line.me/oauth2/v2.1/tokens/kid \
--data-urlencode 'client_assertion_type=urn:ietf:params:oauth:client-assertion-type:jwt-bearer' \
--data-urlencode 'client_assertion={JWT}' \
-G
```

<!-- tab end -->

#### クエリパラメータ 

<!-- parameter start (props: required) -->

client_assertion_type

String

`urn:ietf:params:oauth:client-assertion-type:jwt-bearer`をURLエンコードした値

<!-- parameter end -->
<!-- parameter start (props: required) -->

client_assertion

String

クライアントが作成し、秘密鍵で署名する必要がある[JSON Web Token (JWT)](https://datatracker.ietf.org/doc/html/rfc7519)です。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

kids

Array of strings

チャネルアクセストークンのキーIDの配列

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "kids": [
    "U_gdnFYKTWRxxxxDVZexGg",
    "sDTOzw5wIfWxxxxzcmeQA",
    "73hDyp3PxGfxxxxD6U5qYA",
    "FHGanaP79smDxxxxyPrVw",
    "CguB-0kxxxxdSM3A5Q_UtQ",
    "G82YP96jhHwyKSxxxx7IFA"
  ]
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>JWTアサーションの検証に失敗した。</li><li>JWTアサーションの有効期限が切れている。</li></ul> |
| `404` | JWTアサーションと紐づく署名キーがチャネルに登録されていません。 |

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// JWTアサーションの有効期限が切れている場合（400 Bad Request）
{
  "error": "invalid_client",
  "error_description": "Invalid exp"
}

// JWTアサーションと紐づく署名キーがチャネルに登録されていない場合（404 Not Found）
{
  "message": "Cannot find channel key that satisfies the conditions"
}
```

<!-- tab end -->

### チャネルアクセストークンv2.1を取り消す 

Endpoint: `POST` `https://api.line.me/oauth2/v2.1/revoke`

チャネルアクセストークンv2.1を取り消します。

以下のような場合に、チャネルアクセストークンを取り消します。

- チャネルアクセストークンを再発行することで古いチャネルアクセストークンが不要になったとき
- チャネルアクセストークンの漏洩が疑われたとき

なお、すでに有効期限が切れているチャネルアクセストークンを取り消す必要はありません。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -X POST https://api.line.me/oauth2/v2.1/revoke \
--data-urlencode 'client_id={channel ID}' \
--data-urlencode 'client_secret={channel secret}' \
--data-urlencode 'access_token={access token}'
```

<!-- tab end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

client_id

String

チャネルID

<!-- parameter end -->
<!-- parameter start (props: required) -->

client_secret

String

チャネルシークレット

<!-- parameter end -->
<!-- parameter start (props: required) -->

access_token

String

チャネルアクセストークン

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と空のレスポンスボディを返します。

<!-- note start -->

**注意**

無効なチャネルアクセストークンを指定した場合も、エラーレスポンスは発生しません。

<!-- note end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>無効なフォーマットのチャネルアクセストークンが指定されている。</li><li>存在しないチャネルアクセストークンが指定されている。</li><li>不正なチャネルアクセストークンが指定されている。</li></ul> |

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なフォーマットのチャネルアクセストークンが指定された場合（400 Bad Request）
{
  "error": "invalid_request",
  "error_description": "The access token not JWS"
}

// 不正なチャネルアクセストークンが指定された場合（400 Bad Request）
{
  "error": "invalid_request",
  "error_description": "The access token malformed"
}
```

<!-- tab end -->

### ステートレスチャネルアクセストークンを発行する 

Endpoint: `POST` `https://api.line.me/oauth2/v3/token`

15分間だけ有効なチャネルアクセストークンを発行します。発行できる数に制限はありません。ステートレスチャネルアクセストークンを発行すると、取り消すことはできません。

_チャネルIDとチャネルシークレットから発行するリクエストの例_

<code-tabs class="mb-8">

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/oauth2/v3/token \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id={channel ID}' \
--data-urlencode 'client_secret={channel secret}'
```

<!-- tab end -->

_JWTアサーションから発行するリクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/oauth2/v3/token \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_assertion_type=urn:ietf:params:oauth:client-assertion-type:jwt-bearer' \
--data-urlencode 'client_assertion={JWTアサーション}'
```

<!-- tab end -->

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### リクエストボディ 

ステートレスチャネルアクセストークンを発行する方法には、次の2つがあります。どちらの方法で発行しても、レスポンスボディの形式は同じになります。

- [チャネルIDとチャネルシークレットから発行する](https://developers.line.biz/ja/reference/messaging-api/#issue-stateless-channel-access-token-request-body-channel-id)
- [JWTアサーションから発行する](https://developers.line.biz/ja/reference/messaging-api/#issue-stateless-channel-access-token-request-body-jwt)

##### チャネルIDとチャネルシークレットから発行する 

<!-- parameter start (props: required) -->

grant_type

String

`client_credentials`

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

##### JWTアサーションから発行する 

<!-- parameter start (props: required) -->

grant_type

String

`client_credentials`

<!-- parameter end -->
<!-- parameter start (props: required) -->

client_assertion_type

String

`urn:ietf:params:oauth:client-assertion-type:jwt-bearer`をURLエンコードした値

<!-- parameter end -->
<!-- parameter start (props: required) -->

client_assertion

String

JSON Web Tokenアサーションを指定します。JWTアサーションは、クライアント側で生成した上で、アサーション署名キーの秘密鍵で署名する必要があります。

JWTアサーションは、生成されてから30分以内に失効するように設定する必要があります。JWTアサーションの生成について詳しくは、「[JWTを生成する](https://developers.line.biz/ja/docs/messaging-api/generate-json-web-token/#generate-jwt)」を参照してください。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と、以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

token_type

String

`Bearer`

<!-- parameter end -->
<!-- parameter start -->

access_token

String

チャネルアクセストークン

<!-- parameter end -->
<!-- parameter start -->

expires_in

Number

チャネルアクセストークンが発行されてから有効期限が切れるまでの秒数

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "token_type": "Bearer",
  "access_token": "ey....",
  "expires_in": 900
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>無効なチャネルIDが指定されている。</li><li>無効なチャネルシークレットが指定されている。</li><li>JWTアサーションの検証に失敗した。</li><li>JWTアサーションの有効期限が切れている。</li></ul> |
| `404` | JWTアサーションと紐づく署名キーがチャネルに登録されていません。 |

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なチャネルシークレットを指定した場合（400 Bad Request）
{
  "error": "invalid_request",
  "error_description": "Invalid 'client_credentials'."
}

// JWTアサーションと紐づく署名キーがチャネルに登録されていない場合（404 Not Found）
{
  "message": "Cannot find channel key that satisfies the conditions"
}
```

<!-- tab end -->

### 短期のチャネルアクセストークンを発行する 

Endpoint: `POST` `https://api.line.me/v2/oauth/accessToken`

30日間有効な短期のチャネルアクセストークンを発行します。

短期のチャネルアクセストークンは、チャネルごとに30件まで発行できます。上限を超過した場合は、最も古いチャネルアクセストークンが取り消されます。なお、有効期限が切れたチャネルアクセストークンは、発行数としてカウントされません。

<!-- tip start -->

**ヒント**

- Messaging APIのチャネルの場合は、長期のチャネルアクセストークンや任意の有効期間を指定できるチャネルアクセストークンv2.1、ステートレスチャネルアクセストークンを発行できます。詳しくは、『LINEプラットフォームの基礎知識』の「[チャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/)」を参照してください。
- LINEログインのチャネルのチャネルアクセストークンも、このAPIで発行できます。LINEログインのチャネルのチャネルアクセストークンは、[LIFFのサーバーAPI](https://developers.line.biz/ja/reference/liff-server/)で利用します。

<!-- tip end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/oauth/accessToken \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id={channel ID}' \
--data-urlencode 'client_secret={channel secret}'
```

<!-- tab end -->

#### レート制限 

370リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

grant_type

String

`client_credentials`

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

HTTPステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

access_token

String

短期のチャネルアクセストークン。有効期間は30日です。

<!-- note start -->

**注意**

チャネルアクセストークンは更新できません。

<!-- note end -->

<!-- parameter end -->
<!-- parameter start -->

expires_in

Number

チャネルアクセストークンが発行されてから有効期限が切れるまでの秒数

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
  "access_token": "W1TeHCgfH2Liwa.....",
  "expires_in": 2592000,
  "token_type": "Bearer"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>無効なチャネルIDが指定されている。</li><li>無効なチャネルシークレットが指定されている。</li><li>リクエストパラメータが誤ったフォーマットで指定されている。</li></ul> |
| `429` | [レート制限](https://developers.line.biz/ja/reference/messaging-api/#issue-channel-access-token-rate-limit)を超過しました。 |

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なチャネルIDを指定した場合（400 Bad Request）
{
  "error": "invalid_client",
  "error_description": "invalid client_id"
}

// 無効なチャネルシークレットを指定した場合（400 Bad Request）
{
  "error": "invalid_client",
  "error_description": "invalid client_secret"
}
```

<!-- tab end -->

### 短期または長期のチャネルアクセストークンの有効性を検証する 

Endpoint: `POST` `https://api.line.me/v2/oauth/verify`

[短期のチャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/#short-lived-channel-access-token)または[長期のチャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/#long-lived-channel-access-token)の有効性を検証できます。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/oauth/verify \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'access_token=bNl4YEFPI/hjFWhTqexp4MuEw5YPs7qhr6dJDXKwNPuLka...'
```

<!-- tab end -->

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

access_token

String

短期または長期のチャネルアクセストークン。

<!-- parameter end -->

#### レスポンス 

チャネルアクセストークンが有効な場合は、ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

client_id

String

チャネルアクセストークンが発行されたチャネルID。

<!-- parameter end -->
<!-- parameter start -->

expires_in

Number

チャネルアクセストークンの有効期限が切れるまでの秒数。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

scope

String

チャネルアクセストークンに付与されている権限。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "client_id": "1350031035",
  "expires_in": 3138007490,
  "scope": "P CM"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>無効なチャネルアクセストークンが指定されている。</li><li>無効なフォーマットのチャネルアクセストークンが指定されている。</li><li>チャネルアクセストークンの有効期限が切れている。</li></ul> |

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なチャネルアクセストークンを指定した場合（400 Bad Request）
{
    "error": "invalid_request",
    "error_description": "access_token invalid"
}

// 無効なフォーマットのチャネルアクセストークンを指定した場合（400 Bad Request）
{
    "error": "invalid_request",
    "error_description": "access_token in invalid format"
}
```

<!-- tab end -->

### 短期または長期のチャネルアクセストークンを取り消す 

Endpoint: `POST` `https://api.line.me/v2/oauth/revoke`

短期または長期のチャネルアクセストークンを取り消すAPIです。

以下のような場合に、チャネルアクセストークンを取り消します。

- チャネルアクセストークンを再発行することで古いチャネルアクセストークンが不要になったとき
- チャネルアクセストークンの漏洩が疑われたとき

なお、すでに有効期限が切れているチャネルアクセストークンを取り消す必要はありません。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/oauth/revoke \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode 'access_token={channel access token}'
```

<!-- tab end -->

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

access_token

String

チャネルアクセストークン

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と空のレスポンスボディを返します。無効なチャネルアクセストークンを指定した場合はエラーが返りません。

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明                                                             |
| ------ | ---------------------------------------------------------------- |
| `400`  | 無効なフォーマットのチャネルアクセストークンが指定されています。 |

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なフォーマットのチャネルアクセストークンを指定した場合（400 Bad Request）
{
  "error": "invalid_request"
}
```

<!-- tab end -->

## メッセージ 

メッセージを送ったり、送信済みメッセージについての情報を取得したりできます。

### 応答メッセージを送る 

Endpoint: `POST` `https://api.line.me/v2/bot/message/reply`

ユーザー、グループトーク、または複数人トークからのイベントに対して、応答メッセージを送信するAPIです。応答メッセージを送るには、Webhookイベントオブジェクトに含まれる応答トークンが必要です。

イベントが発生すると、[Webhook](https://developers.line.biz/ja/reference/messaging-api/#webhooks)により通知されます。応答できるイベントの場合は、応答トークンが発行されます。

<!-- tip start -->

**応答メッセージの準備中にローディングのアニメーションを表示できます**

LINE公式アカウントがユーザーからのメッセージを受信したあと、メッセージの準備や予約の処理などで返答に少し時間がかかることがあります。そのような場合に、ユーザーにそのまま待機しておいて欲しいことをローディングのアニメーションで視覚的に伝えることができます。詳しくは、『Messaging APIドキュメント』の「[ローディングのアニメーションを表示する](https://developers.line.biz/ja/docs/messaging-api/use-loading-indicator/)」を参照してください。

<!-- tip end -->

#### 応答トークン 

応答トークンを使用する際は、以下の点を確認してください。

- 応答トークンは一度のみ使用できます。
- 応答トークンは、Webhookを受信してから1分以内に使用する必要があります。1分を超える場合の使用については、動作は保証されません。
- 再送されたWebhookに含まれる応答トークンも、再送されたWebhookを受信してから1分以内であれば使用できます。ただし、以下の場合は応答トークンを使用できません。
  - 元のWebhookに含まれる応答トークンをすでに使用している場合。
  - イベントの発生から20分が経過している場合。

<!-- note start -->

**応答トークンは可能な限り早く使用してください**

応答トークンの時間制限は、予告なく変更される可能性があります。また、ネットワークの遅延などにより、実際に使用できる期間は変動します。

このため、時間制限に依存した実装をしないようにしてください。また、応答トークンは可能な限り早く使用してください。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/message/reply \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {channel access token}' \
-d '{
    "replyToken":"nHuyWiB7yP5Zw52FIkcQobQuGDXCTA",
    "messages":[
        {
            "type":"text",
            "text":"Hello, user"
        },
        {
            "type":"text",
            "text":"May I help you?"
        }
    ]
}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

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

replyToken

String

Webhookで受信する応答トークン

<!-- parameter end -->
<!-- parameter start (props: required) -->

messages

[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の配列

送信するメッセージ\
最大件数：5

[応答メッセージのメッセージオブジェクトを検証する](https://developers.line.biz/ja/reference/messaging-api/#validate-message-objects-of-reply-message)エンドポイントを使用すると、メッセージオブジェクトが有効かを検証できます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

notificationDisabled

Boolean

- `true`：メッセージ送信時に、ユーザーに通知されない。
- `false`：メッセージ送信時に、ユーザーに通知される。ただし、LINEで通知をオフにしている場合は通知されません。

デフォルト値は`false`です。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

sentMessages

Array

送信したメッセージの配列。<br />最大件数：5

<!-- parameter end -->
<!-- parameter start -->

sentMessages.id

Number

送信したメッセージのID。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

sentMessages.quoteToken

String

メッセージの引用トークン。引用対象として指定可能なメッセージオブジェクトを送信した場合のみ、レスポンスに含まれます。詳しくは、『Messaging APIドキュメント』の「[引用トークンを取得する](https://developers.line.biz/ja/docs/messaging-api/get-quote-tokens/)」を参照してください。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "sentMessages": [
    {
      "id": "461230966842064897",
      "quoteToken": "IStG5h1Tz7b..."
    }
  ]
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | メッセージを送信できませんでした。次のような理由が考えられます。<ul><li>無効な応答トークンが指定されている。</li><li>無効なメッセージオブジェクトが指定されている。</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

エラーが返された場合、メッセージは送信されません。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 有効期限切れ、使用済みなどの無効な応答トークンを指定した場合（400 Bad Request）
{
  "message": "Invalid reply token"
}
```

<!-- tab end -->

### プッシュメッセージを送る 

Endpoint: `POST` `https://api.line.me/v2/bot/message/push`

ユーザー、グループトーク、または複数人トークに、任意のタイミングでメッセージを送信するAPIです。

#### プッシュメッセージを送信できる条件 

プッシュメッセージは、以下のいずれかの条件に当てはまる場合に送信できます。

- LINE公式アカウントを友だち追加しているユーザー
- LINE公式アカウントが参加しているグループトーク、または複数人トーク
- 1対1のトークで、7日以内にLINE公式アカウントへメッセージを送ったユーザー（※）

なお、以下のユーザーに対してプッシュメッセージの送信処理を行った場合、ステータスコード`200`が返されますが、実際にはユーザーに送信されません。

- LINEアカウントを削除したユーザー
- プッシュメッセージを送信したLINE公式アカウントをブロックしているユーザー
- プッシュメッセージを送信したLINE公式アカウントを友だち追加していないユーザー（※）

※ユーザーは、友だち追加していないLINE公式アカウントに対しても、メッセージを送ることができます。LINE公式アカウントは、友だちでないユーザーから1対1のトークでメッセージを受け取った場合、メッセージを受け取ってから7日以内であれば、そのユーザーに対してメッセージを送信できます。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/message/push \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {channel access token}' \
-H 'X-Line-Retry-Key: {UUID}' \
-d '{
    "to": "U4af4980629...",
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

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

X-Line-Retry-Key

リトライキー。任意の方法で生成した16進表記のUUID（例：123e4567-e89b-12d3-a456-426614174000）を指定します。リトライキーはLINEから提供されません。開発者自身が一意のリトライキーを生成する必要があります。詳しくは、『Messaging APIドキュメント』の「[失敗したAPIリクエストを再試行する](https://developers.line.biz/ja/docs/messaging-api/retrying-api-request/)」を参照してください。

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

to

String

送信先のID。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#common-properties)で返される、`userId`、`groupId`、または`roomId`の値を使用します。

<!-- parameter end -->
<!-- parameter start (props: required) -->

messages

[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の配列

送信するメッセージ\
最大件数：5

[プッシュメッセージのメッセージオブジェクトを検証する](https://developers.line.biz/ja/reference/messaging-api/#validate-message-objects-of-push-message)エンドポイントを使用すると、メッセージオブジェクトが有効かを検証できます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

notificationDisabled

Boolean

- `true`：メッセージ送信時に、ユーザーに通知されない。
- `false`：メッセージ送信時に、ユーザーに通知される。ただし、LINEで通知をオフにしている場合は通知されません。

デフォルト値は`false`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

customAggregationUnits

Array of strings

任意の集計単位のユニット名。大文字と小文字は区別されます。たとえば`promotion_a`と`promotion_A`は別のユニットとして扱われます。\
最大ユニット数：1\
最大文字数：30\
使用可能文字種：半角英数字（`a`〜`z`、`A`～`Z`、`0`～`9`）、アンダースコア（`_`）

ユニット名の付与について詳しくは、『Messaging APIドキュメント』の「[ユニット名を付与する](https://developers.line.biz/ja/docs/messaging-api/unit-based-statistics-aggregation/#assign-names-to-units-when-sending-messages)」を参照してください。

<!-- note start -->

**ユニット名が付与されないことがあります**

ユニット名は、当月中（その月の1日～末日）に最大で1,000種類まで付与できます。1,001種類目以降のユニット名を付与してメッセージを送ろうとした場合、メッセージは送信されますがユニット名はメッセージに付与されません。

ユニット名の種類が多い場合は、以下のいずれかの方法でユニット名が付与できる、あるいは付与できたことを確認してください。

- 当月のユニット名がまだ1,000種類に達していないことを、メッセージの送信前に「[当月中に付与したユニット名の種類数を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-the-number-of-unit-name-types-assigned-during-this-month)」エンドポイントで確認する
- メッセージの送信後に「[当月中に付与したユニット名のリストを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-a-list-of-unit-names-assigned-during-this-month)」エンドポイントで、付与したユニット名が存在することを確認する

<!-- note end -->

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

sentMessages

Array

送信したメッセージの配列。<br />最大件数：5

<!-- parameter end -->
<!-- parameter start -->

sentMessages.id

Number

送信したメッセージのID。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

sentMessages.quoteToken

String

メッセージの引用トークン。引用対象として指定可能なメッセージオブジェクトを送信した場合のみ、レスポンスに含まれます。詳しくは、『Messaging APIドキュメント』の「[引用トークンを取得する](https://developers.line.biz/ja/docs/messaging-api/get-quote-tokens/)」を参照してください。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "sentMessages": [
    {
      "id": "461230966842064897",
      "quoteToken": "IStG5h1Tz7b..."
    }
  ]
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | メッセージを送信できませんでした。次のような理由が考えられます。<ul><li>他のプロバイダー配下のチャネルで取得したユーザーIDなど、チャネルに存在しないユーザーのIDが指定されている。</li><li>存在しないグループやLINE公式アカウントが参加していないグループが指定されている。</li><li>存在しない複数人トークやLINE公式アカウントが参加していない複数人トークが指定されている。</li><li>無効なメッセージオブジェクトが指定されている。</li></ul> |
| `409` | 同じリトライキーを含むリクエストがすでに受理されています。詳しくは、「APIリクエストを再試行する」の「[すでにリクエストが受理されていた場合のレスポンス](https://developers.line.biz/ja/reference/messaging-api/#retry-api-request-response)」を参照してください。 |
| `429` | リクエスト数が上限を超過しました。次のような理由が考えられます。<ul><li>このエンドポイントの[レート制限](https://developers.line.biz/ja/reference/messaging-api/#send-push-message-rate-limit)を超過した。</li><li>同一のユーザーに大量のメッセージを送信した。</li><li>[当月に送信できるメッセージ数の上限目安](https://developers.line.biz/ja/reference/messaging-api/#get-quota)を超過した。</li></ul>メッセージ数の上限目安について詳しくは、『Messaging APIドキュメント』の「[Messaging APIの料金](https://developers.line.biz/ja/docs/messaging-api/pricing/)」を参照してください。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

エラーが返された場合、メッセージは送信されません。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// メッセージの送信に失敗した場合（400 Bad Request）
{
  "message": "Failed to send messages"
}
```

<!-- tab end -->

### マルチキャストメッセージを送る 

Endpoint: `POST` `https://api.line.me/v2/bot/message/multicast`

複数のユーザーに対して同じメッセージを効率よく送信するAPIです。グループトークおよび複数人トークにメッセージを送ることはできません。

なお、1人のユーザーに対してもマルチキャストメッセージでメッセージを送信できますが、送信対象が1人の場合には[プッシュメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-push-message)の利用を推奨します。プッシュメッセージは、低遅延用途でのメッセージの送信に適しています。

#### マルチキャストメッセージを送信できる条件 

マルチキャストメッセージは、LINE公式アカウントを友だち追加しているユーザーに対して送信できます。

なお、以下のユーザーに対してマルチキャストメッセージの送信処理を行った場合、ステータスコード`200`が返されますが、実際にはユーザーに送信されません。

- LINEアカウントを削除したユーザー
- マルチキャストメッセージを送信したLINE公式アカウントをブロックしているユーザー
- マルチキャストメッセージを送信したLINE公式アカウントを友だち追加していないユーザー
- 他のプロバイダー配下のチャネルで取得したユーザーIDなど、チャネルにユーザーIDが存在しないユーザー

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/message/multicast \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {channel access token}' \
-H 'X-Line-Retry-Key: {UUID}' \
-d '{
    "to": ["U4af4980629...","U0c229f96c4..."],
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

#### レート制限 

200リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

X-Line-Retry-Key

リトライキー。任意の方法で生成した16進表記のUUID（例：123e4567-e89b-12d3-a456-426614174000）を指定します。リトライキーはLINEから提供されません。開発者自身が一意のリトライキーを生成する必要があります。詳しくは、『Messaging APIドキュメント』の「[失敗したAPIリクエストを再試行する](https://developers.line.biz/ja/docs/messaging-api/retrying-api-request/)」を参照してください。

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

to

Array of strings

ユーザーIDの配列。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#common-properties)で返される`userId`の値を使用します。LINEに表示されるLINE IDは使用しないでください。\
最大ユーザーID数：500

<!-- parameter end -->
<!-- parameter start (props: required) -->

messages

[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の配列

送信するメッセージ\
最大件数：5

[マルチキャストメッセージのメッセージオブジェクトを検証する](https://developers.line.biz/ja/reference/messaging-api/#validate-message-objects-of-multicast-message)エンドポイントを使用すると、メッセージオブジェクトが有効かを検証できます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

notificationDisabled

Boolean

- `true`：メッセージ送信時に、ユーザーに通知されない。
- `false`：メッセージ送信時に、ユーザーに通知される。ただし、LINEで通知をオフにしている場合は通知されません。

デフォルト値は`false`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

customAggregationUnits

Array of strings

任意の集計単位のユニット名。大文字と小文字は区別されます。たとえば`promotion_a`と`promotion_A`は別のユニットとして扱われます。\
最大ユニット数：1\
最大文字数：30\
使用可能文字種：半角英数字（`a`〜`z`、`A`～`Z`、`0`～`9`）、アンダースコア（`_`）

ユニット名の付与について詳しくは、『Messaging APIドキュメント』の「[ユニット名を付与する](https://developers.line.biz/ja/docs/messaging-api/unit-based-statistics-aggregation/#assign-names-to-units-when-sending-messages)」を参照してください。

<!-- note start -->

**ユニット名が付与されないことがあります**

ユニット名は、当月中（その月の1日～末日）に最大で1,000種類まで付与できます。1,001種類目以降のユニット名を付与してメッセージを送ろうとした場合、メッセージは送信されますがユニット名はメッセージに付与されません。

ユニット名の種類が多い場合は、以下のいずれかの方法でユニット名が付与できる、あるいは付与できたことを確認してください。

- 当月のユニット名がまだ1,000種類に達していないことを、メッセージの送信前に「[当月中に付与したユニット名の種類数を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-the-number-of-unit-name-types-assigned-during-this-month)」エンドポイントで確認する
- メッセージの送信後に「[当月中に付与したユニット名のリストを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-a-list-of-unit-names-assigned-during-this-month)」エンドポイントで、付与したユニット名が存在することを確認する

<!-- note end -->

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
| `400` | メッセージを送信できませんでした。次のような理由が考えられます。<ul><li>他のプロバイダー配下のチャネルで取得したユーザーIDなど、チャネルに存在しないユーザーのIDが指定されている。</li><li>グループIDなど、ユーザーIDではないIDが指定されている。</li><li>無効なメッセージオブジェクトが指定されている。</li></ul> |
| `409` | 同じリトライキーを含むリクエストがすでに受理されています。詳しくは、「APIリクエストを再試行する」の「[すでにリクエストが受理されていた場合のレスポンス](https://developers.line.biz/ja/reference/messaging-api/#retry-api-request-response)」を参照してください。 |
| `429` | リクエスト数が上限を超過しました。次のような理由が考えられます。<ul><li>このエンドポイントの[レート制限](https://developers.line.biz/ja/reference/messaging-api/#send-multicast-rate-limit)を超過した。</li><li>[当月に送信できるメッセージ数の上限目安](https://developers.line.biz/ja/reference/messaging-api/#get-quota)を超過した。</li></ul>メッセージ数の上限目安について詳しくは、『Messaging APIドキュメント』の「[Messaging APIの料金](https://developers.line.biz/ja/docs/messaging-api/pricing/)」を参照してください。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

エラーが返された場合、どのユーザーに対してもメッセージは送信されません。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// リクエストに無効なパラメータが含まれていた場合（400 Bad Request）
{
  "message": "The property, to[1], in the request body is invalid (line: -, column: -)"
}
```

<!-- tab end -->

### ナローキャストメッセージを送る 

Endpoint: `POST` `https://api.line.me/v2/bot/message/narrowcast`

複数のユーザーに、任意のタイミングでメッセージを送信します。送信対象は、属性情報（性別や年齢、OSの種類、地域など）やリターゲティング（オーディエンス）を利用して指定できます。グループトークまたは複数人トークにメッセージを送ることはできません。

ナローキャストメッセージは、LINEプラットフォームがリクエストを受信した後にバックグラウンドで非同期に送信されます。そのため、ナローキャストメッセージを送信するリクエストが成功していたとしても、送信開始後に失敗している可能性があります。メッセージの送信が成功したかどうかは、[ナローキャストメッセージの進行状況を取得](https://developers.line.biz/ja/reference/messaging-api/#get-narrowcast-progress-status)することで確認できます。

<!-- note start -->

**タイの20歳未満のユーザーへのナローキャストメッセージの送信について**

送信対象を特定の条件で絞り込む場合に、タイの20歳未満のユーザーは、メッセージの送信対象から除外されます。

<!-- note end -->

#### ナローキャストメッセージを送信できる条件 

ナローキャストメッセージは、LINE公式アカウントを友だち追加しているユーザーに対して送信できます。

なお、以下のユーザーを送信対象に含めた場合、ステータスコード`202`が返されますが、送信対象からは除外されます。

- LINEアカウントを削除したユーザー
- LINE公式アカウントをブロックしているユーザー
- LINE公式アカウントを友だち追加していないユーザー
- 他のプロバイダー配下のチャネルで取得したユーザーIDなど、チャネルにユーザーIDが存在しないユーザー

#### 属性情報やオーディエンスを利用したメッセージ送信の制限事項 

属性情報やオーディエンスを利用した場合、メッセージの送信条件に応じて、ユーザーのプライバシーを保護するための制限が適用されることがあります。制限に該当した場合、リクエスト送信時もしくはメッセージの送信開始時にエラーになります。

- 送信条件に属性情報を指定するには、LINE公式アカウントの[ターゲットリーチ](https://developers.line.biz/ja/glossary/#target-reach)が100人以上である必要があります。ターゲットリーチが100人未満の場合はステータスコード`403`が返されます。
- 送信条件に属性情報またはオーディエンス（※）を指定した場合、最終的な送信対象が50人以上である必要があります。最終的な送信対象が50人未満の場合にもステータスコード`202`が返されますが、メッセージの送信開始時にエラーとなります。
- 送信条件に1件以上のオーディエンスを指定した場合、各オーディエンス（※）の送信対象がそれぞれ50人以上である必要があります。送信対象が50人未満のオーディエンスが含まれていた場合にもステータスコード`202`が返されますが、メッセージの送信開始時にエラーとなります。

※以下のオーディエンスには、送信対象の人数に関する制限はありません。ただし、他のLINE公式アカウントの下で作成されたオーディエンスについては、以下のオーディエンスであっても制限が適用されます。

- LINE Official Account ManagerやMessaging APIから、ユーザーIDアップロードにより作成されたオーディエンス
- チャットタグオーディエンス

#### 当月に配信できるメッセージの残数に関する注意事項 

LINE Official Account ManagerおよびMessaging APIでは、メッセージの送信開始から、実際に送信される件数が確定するまでの間、当月に配信できるメッセージの残数に対して送信予定のメッセージ数が予約された状態になります。メッセージの送信開始時点で送信予定のメッセージ数が予約ができない場合は、メッセージの送信に失敗します。

ナローキャストメッセージの場合、実際の送信対象となるユーザー数に関わらず、LINE公式アカウントのターゲットリーチ分の予約が必要となります。そのため、ナローキャストメッセージの送信時には、以下の点に注意してください。

- 当月に配信できるメッセージの残数が、LINE公式アカウントのターゲットリーチに満たない場合、ナローキャストメッセージの送信開始時にエラーとなります。
- 実際の送信対象となるユーザー数が十分に少ないにも関わらず、当月分のメッセージの残数が一時的に枯渇することがあります。この場合、ナローキャストメッセージの配信中に別のメッセージを送信すると、`429 Too Many Requests`およびエラーメッセージ`You have reached your monthly limit.`が返され、メッセージの送信に失敗します。

これらはナローキャストメッセージの送信時に、メッセージの送信数を制限することによって回避できる場合があります。詳しくは、[リクエストボディ](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-request-body)の[リミットオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-limit)を参照してください。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/message/narrowcast \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-H 'X-Line-Retry-Key: {UUID}' \
-d '{
    "messages": [
        {
            "type": "text",
            "text": "test message"
        }
    ],
    "recipient": {
        "type": "operator",
        "and": [
            {
                "type": "audience",
                "audienceGroupId": 5614991017776
            },
            {
                "type": "operator",
                "not": {
                    "type": "audience",
                    "audienceGroupId": 4389303728991
                }
            }
        ]
    },
    "filter": {
        "demographic": {
            "type": "operator",
            "or": [
                {
                    "type": "operator",
                    "and": [
                        {
                            "type": "gender",
                            "oneOf": [
                                "male",
                                "female"
                            ]
                        },
                        {
                            "type": "age",
                            "gte": "age_20",
                            "lt": "age_25"
                        },
                        {
                            "type": "appType",
                            "oneOf": [
                                "android",
                                "ios"
                            ]
                        },
                        {
                            "type": "area",
                            "oneOf": [
                                "jp_23",
                                "jp_05"
                            ]
                        },
                        {
                            "type": "subscriptionPeriod",
                            "gte": "day_7",
                            "lt": "day_30"
                        }
                    ]
                },
                {
                    "type": "operator",
                    "and": [
                        {
                            "type": "age",
                            "gte": "age_35",
                            "lt": "age_40"
                        },
                        {
                            "type": "operator",
                            "not": {
                                "type": "gender",
                                "oneOf": [
                                    "male"
                                ]
                            }
                        }
                    ]
                }
            ]
        }
    },
    "limit": {
        "max": 100,
        "upToRemainingQuota": true
    }
}'
```

<!-- tab end -->

#### レート制限 

60リクエスト/時

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

`application/json`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

X-Line-Retry-Key

リトライキー。任意の方法で生成した16進表記のUUID（例：123e4567-e89b-12d3-a456-426614174000）を指定します。リトライキーはLINEから提供されません。開発者自身が一意のリトライキーを生成する必要があります。詳しくは、『Messaging APIドキュメント』の「[失敗したAPIリクエストを再試行する](https://developers.line.biz/ja/docs/messaging-api/retrying-api-request/)」を参照してください。

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

messages

[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の配列

送信するメッセージ\
最大件数：5

[ナローキャストメッセージのメッセージオブジェクトを検証する](https://developers.line.biz/ja/reference/messaging-api/#validate-message-objects-of-narrowcast-message)エンドポイントを使用すると、メッセージオブジェクトが有効かを検証できます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

recipient

Object

[レシピエントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#narrowcast-recipient)。オーディエンスや、過去に配信したナローキャストメッセージのリクエストIDを合計10件まで使用して、送信対象を指定します。指定できる演算子オブジェクトの数に上限はありません。\
省略すると、LINE公式アカウントを友だち追加したすべてのユーザーが送信対象になります。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

filter.demographic

Object

[デモグラフィックフィルターオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#narrowcast-demographic-filter)。友だちの属性情報を使用して、送信対象をフィルタリングできます。\
省略すると、属性が「不明」になっているユーザーを含めた全員に配信されます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

limit

Object

[リミットオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-limit)。ナローキャストメッセージの最大送信数を制限する場合に設定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

notificationDisabled

Boolean

- `true`：メッセージ送信時に、ユーザーに通知されない。
- `false`：メッセージ送信時に、ユーザーに通知される。ただし、LINEで通知をオフにしている場合は通知されません。

デフォルト値は`false`です。

<!-- parameter end -->

##### レシピエントオブジェクト 

レシピエントオブジェクトは、オーディエンスオブジェクトまたは再配信オブジェクトを表すオブジェクトです。演算子オブジェクトを利用すると、条件を組み合わせて送信対象を指定できます。1回のリクエストごとに、オーディエンスオブジェクトと再配信オブジェクトを合計10件まで指定できます。演算子オブジェクトの数に上限はありません。

###### オーディエンスオブジェクト 

<!-- parameter start (props: required) -->

type

String

`audience`

<!-- parameter end -->
<!-- parameter start (props: required) -->

audienceGroupId

Number

オーディエンスID。オーディエンスを作成するには、「[オーディエンス管理](https://developers.line.biz/ja/reference/messaging-api/#manage-audience-group)」のAPIを使用します。

<!-- parameter end -->

###### 再配信オブジェクト 

<!-- parameter start (props: required) -->

type

String

`redelivery`

<!-- parameter end -->
<!-- parameter start (props: required) -->

requestId

String

過去に配信したナローキャストメッセージのリクエストID。リクエストIDは、Messaging APIのリクエストごとに発行されるIDです。[レスポンスヘッダー](https://developers.line.biz/ja/reference/messaging-api/#response-headers)に含まれます。

<!-- parameter end -->

<!-- note start -->

**指定できるリクエストIDにはいくつかの条件があります**

以下の条件をすべて満たすリクエストIDを、`requestId`プロパティで指定してください。条件を満たしていないリクエストIDが指定された場合はステータスコード`400`が返されます。

- ナローキャストメッセージの配信によって発行されたリクエストIDであること
- 「[ナローキャストメッセージの進行状況を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-narrowcast-progress-status-response)」エンドポイントで取得する`acceptedTime`プロパティの値（タイムスタンプ）から14日間（336時間）未満の配信であること
- 送信処理が完了していること（「[ナローキャストメッセージの進行状況を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-narrowcast-progress-status-response)」で、レスポンスの`phase`プロパティの値が`succeeded`であること）

<!-- note end -->

###### 演算子オブジェクト 

積集合（AND）、和集合（OR）、差集合（NOT）を使用して、複数のレシピエントオブジェクトから、新たなレシピエントオブジェクトを作成できます。

<!-- parameter start (props: required) -->

type

String

`operator`

<!-- parameter end -->
<!-- parameter start (props: annotation="※") -->

and

レシピエントオブジェクトの配列

配列で指定したレシピエントオブジェクトの積集合（AND）を、新たなレシピエントオブジェクトとします。

![Audience 1 and Audience 2](https://developers.line.biz/media/messaging-api/narrowcast-message/operator_object_for_reference_and.png)

<!-- parameter end -->
<!-- parameter start (props: annotation="※") -->

or

レシピエントオブジェクトの配列

配列で指定したレシピエントオブジェクトの和集合（OR）を、新たなレシピエントオブジェクトとします。

![Audience 1 or Audience 2](https://developers.line.biz/media/messaging-api/narrowcast-message/operator_object_for_reference_or.png)

<!-- parameter end -->
<!-- parameter start (props: annotation="※") -->

not

レシピエントオブジェクト

指定したレシピエントオブジェクトを配信対象外にした、新たなレシピエントオブジェクトとします。

![not Audience 2](https://developers.line.biz/media/messaging-api/narrowcast-message/operator_object_for_reference_not.png)

<!-- parameter end -->

※`and`プロパティ、`or`プロパティ、`not`プロパティのいずれか1つだけ、必ず指定してください。また、空配列は指定できません。

_レシピエントオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "type": "operator",
  "and": [
    {
      "type": "audience",
      "audienceGroupId": 5614991017776
    },
    {
      "type": "operator",
      "not": {
        "type": "redelivery",
        "requestId": "5b59509c-c57b-11e9-aa8c-2a2ae2dbcce4"
      }
    }
  ]
}
```

<!-- tab end -->

##### デモグラフィックフィルターオブジェクト 

デモグラフィックフィルターオブジェクトは、送信対象をフィルタリングする条件（性別、年齢、OSの種類、地域、友だち期間）を表すオブジェクトです。演算子オブジェクトを利用すると、条件を組み合わせて送信対象をフィルタリングできます。

<!-- note start -->

**属性情報の利用について**

- 属性情報は約3日前（前後する可能性があります）の属性情報を元に絞り込みます。
- 属性を指定しない場合は、属性が「不明」になっているユーザーを含めた全員に配信されます。
- 属性情報を利用するには、100人以上の[ターゲットリーチ](https://developers.line.biz/ja/glossary/#target-reach)が必要です。
  - ターゲットリーチが100人未満の場合はステータスコード`403`が返されます。

<!-- note end -->

###### 性別 

<!-- parameter start (props: required) -->

type

String

`gender`

<!-- parameter end -->
<!-- parameter start (props: required) -->

oneOf

Array of strings

指定した性別を送信対象とします。以下のいずれかの値を指定します。

- `male`
- `female`

<!-- parameter end -->

###### 年齢 

年齢の範囲を指定してフィルタリングします。

<!-- parameter start (props: required) -->

type

String

`age`

<!-- parameter end -->
<!-- parameter start (props: annotation="※") -->

gte

String

指定した年齢以上を送信対象とします。

以下のいずれかの値を指定します。ただし、`lt`プロパティで指定した値より小さい値を指定してください。

- `age_15`
- `age_20`
- `age_25`
- `age_30`
- `age_35`
- `age_40`
- `age_45`
- `age_50`
- `age_55`
- `age_60`
- `age_65`
- `age_70`

<!-- parameter end -->
<!-- parameter start (props: annotation="※") -->

lt

String

指定した年齢未満を送信対象とします。

以下のいずれかの値を指定します。ただし、`gte`プロパティで指定した値より大きい値を指定してください。

- `age_15`
- `age_20`
- `age_25`
- `age_30`
- `age_35`
- `age_40`
- `age_45`
- `age_50`
- `age_55`
- `age_60`
- `age_65`
- `age_70`

<!-- parameter end -->

※`gte`プロパティまたは`lt`プロパティの両方またはいずれか一方を、必ず指定してください。

###### OSの種類 

<!-- parameter start (props: required) -->

type

String

`appType`

<!-- parameter end -->
<!-- parameter start (props: required) -->

oneOf

Array of strings

指定したOSを送信対象とします。以下のいずれかの値を指定します。

- `ios`
- `android`

<!-- parameter end -->

###### 地域 

<!-- parameter start (props: required) -->

type

String

`area`

<!-- parameter end -->
<!-- parameter start (props: required) -->

oneOf

Array of strings

指定した地域を送信対象とします。以下のいずれかの値を指定します。\
**日本 // JP (country code=392)**

- `jp_01`：北海道 // Hokkaido
- `jp_02`：青森県 // Aomori
- `jp_03`：岩手県 // Iwate
- `jp_04`：宮城県 // Miyagi
- `jp_05`：秋田県 // Akita
- `jp_06`：山形県 // Yamagata
- `jp_07`：福島県 // Fukushima
- `jp_08`：茨城県 // Ibaraki
- `jp_09`：栃木県 // Tochigi
- `jp_10`：群馬県 // Gunma
- `jp_11`：埼玉県 // Saitama
- `jp_12`：千葉県 // Chiba
- `jp_13`：東京都 // Tokyo
- `jp_14`：神奈川県 // Kanagawa
- `jp_15`：新潟県 // Niigata
- `jp_16`：富山県 // Toyama
- `jp_17`：石川県 // Ishikawa
- `jp_18`：福井県 // Fukui
- `jp_19`：山梨県 // Yamanashi
- `jp_20`：長野県 // Nagano
- `jp_21`：岐阜県 // Gifu
- `jp_22`：静岡県 // Shizuoka
- `jp_23`：愛知県 // Aichi
- `jp_24`：三重県 // Mie
- `jp_25`：滋賀県 // Shiga
- `jp_26`：京都府 // Kyoto
- `jp_27`：大阪府 // Osaka
- `jp_28`：兵庫県 // Hyougo
- `jp_29`：奈良県 // Nara
- `jp_30`：和歌山県 // Wakayama
- `jp_31`：鳥取県 // Tottori
- `jp_32`：島根県 // Shimane
- `jp_33`：岡山県 // Okayama
- `jp_34`：広島県 // Hiroshima
- `jp_35`：山口県 // Yamaguchi
- `jp_36`：徳島県 // Tokushima
- `jp_37`：香川県 // Kagawa
- `jp_38`：愛媛県 // Ehime
- `jp_39`：高知県 // Kouchi
- `jp_40`：福岡県 // Fukuoka
- `jp_41`：佐賀県 // Saga
- `jp_42`：長崎県 // Nagasaki
- `jp_43`：熊本県 // Kumamoto
- `jp_44`：大分県 // Oita
- `jp_45`：宮崎県 // Miyazaki
- `jp_46`：鹿児島県 // Kagoshima
- `jp_47`：沖縄県 // Okinawa

**台湾 // TW (country code=158)**

- `tw_01`：台北市 // Taipei City
- `tw_02`：新北市 // New Taipei City
- `tw_03`：桃園市 // Taoyuan City
- `tw_04`：台中市 // Taichung City
- `tw_05`：台南市 // Tainan City
- `tw_06`：高雄市 // Kaohsiung City
- `tw_07`：基隆市 // Keelung City
- `tw_08`：新竹市 // Hsinchu City
- `tw_09`：嘉義市 // Chiayi City
- `tw_10`：新竹県 // Hsinchu County
- `tw_11`：苗栗県 // Miaoli County
- `tw_12`：彰化県 // Changhua County
- `tw_13`：南投県 // Nantou County
- `tw_14`：雲林県 // Yunlin County
- `tw_15`：嘉義県 // Chiayi County
- `tw_16`：屏東県 // Pingtung County
- `tw_17`：宜蘭県 // Yilan County
- `tw_18`：花蓮県 // Hualien County
- `tw_19`：台東県 // Taitung County
- `tw_20`：澎湖県 // Penghu County
- `tw_21`：金門県 // Kinmen County
- `tw_22`：連江県 // Lienchiang County

**タイ // TH (country code=764)**

- `th_01`：バンコク // Bangkok
- `th_02`：パタヤ // Pattaya
- `th_03`：北部 // Northern
- `th_04`：中央部 // Central
- `th_05`：南部 // Southern
- `th_06`：東部 // Eastern
- `th_07`：東北部 // NorthEastern
- `th_08`：西部 // Western

<!-- parameter end -->

###### 友だち期間 

友だち期間の範囲を指定してフィルタリングします。

<!-- parameter start (props: required) -->

type

String

`subscriptionPeriod`

<!-- parameter end -->
<!-- parameter start (props: annotation="※") -->

gte

String

指定した日数以上を送信対象とします。\
以下のいずれかの値を指定します。ただし、`lt`プロパティで指定した値より小さい値を指定してください。

- `day_7`
- `day_30`
- `day_90`
- `day_180`
- `day_365`

<!-- parameter end -->
<!-- parameter start (props: annotation="※") -->

lt

String

指定した日数未満を送信対象とします。\
以下のいずれかの値を指定します。ただし、`gte`プロパティで指定した値より大きい値を指定してください。

- `day_7`
- `day_30`
- `day_90`
- `day_180`
- `day_365`

<!-- parameter end -->

※`gte`プロパティまたは`lt`プロパティの両方またはいずれか一方を、必ず指定してください。

###### 演算子オブジェクト 

積集合（AND）、和集合（OR）、差集合（NOT）を使用して、複数のデモグラフィックフィルターオブジェクトから、新たなデモグラフィックフィルターオブジェクトを作成できます。1回のリクエストごとに、デモグラフィックフィルターオブジェクトは、合計10件まで指定できます。

<!-- parameter start (props: required) -->

type

String

`operator`

<!-- parameter end -->
<!-- parameter start (props: annotation="※") -->

and

デモグラフィックフィルターオブジェクトの配列

配列で指定したデモグラフィックフィルターオブジェクトの積集合（AND）を、新たなデモグラフィックフィルターオブジェクトとします。

<!-- parameter end -->
<!-- parameter start (props: annotation="※") -->

or

デモグラフィックフィルターオブジェクトの配列

配列で指定したデモグラフィックフィルターオブジェクトの和集合（OR）を、新たなデモグラフィックフィルターオブジェクトとします。

<!-- parameter end -->
<!-- parameter start (props: annotation="※") -->

not

デモグラフィックフィルターオブジェクト

指定したデモグラフィックフィルターオブジェクトを配信対象外にした、新たなデモグラフィックフィルターオブジェクトとします。

<!-- parameter end -->

※`and`プロパティ、`or`プロパティ、`not`プロパティのいずれか1つだけ、必ず指定してください。また、空配列は指定できません。

_性別を使用してフィルタリングするデモグラフィックフィルターオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "type": "gender",
  "oneOf": ["male", "female"]
}
```

<!-- tab end -->

##### リミットオブジェクト 

リミットオブジェクトは、ナローキャストメッセージの最大送信数を制限する場合に設定します。

各プロパティの設定による最大送信数の制御について詳しくは、『Messaging APIドキュメント』の「[リミットオブジェクトによる最大送信数の制御](https://developers.line.biz/ja/docs/messaging-api/sending-messages/#maximum-send-numbers-control)」を参照してください。

<!-- parameter start (props: optional) -->

max

Number

ナローキャストメッセージの最大送信数。このナローキャストメッセージによる送信数を制限する場合に指定します。なお送信対象は、無作為に抽出されます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

upToRemainingQuota

Boolean

`true`を指定すると、配信可能な上限数の範囲内でメッセージを送信します。デフォルト値は`false`です。なお送信対象は、無作為に抽出されます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

forbidPartialDelivery

Boolean

送信対象の一部にのみメッセージが配信されることを防ぐためのオプションです。`upToRemainingQuota`プロパティに`true`を指定し、`forbidPartialDelivery`プロパティにも`true`を指定すると、送信対象の人数がメッセージの最大送信数を超えていた場合、メッセージの配信を行いません。

メッセージの配信が中止されたかどうかは、[ナローキャストメッセージの進行状況を取得](https://developers.line.biz/ja/reference/messaging-api/#get-narrowcast-progress-status)することで確認できます。配信が中止された場合、進行状況を取得した際のレスポンスで`phase`プロパティが`failed`となり、`errorCode`プロパティで`5`が返されます。

`forbidPartialDelivery`プロパティは`upToRemainingQuota`プロパティが`true`の場合にのみ、指定できます。

<!-- parameter end -->

_リミットオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "max": 100,
  "upToRemainingQuota": true,
  "forbidPartialDelivery": true
}
```

<!-- tab end -->

`max`プロパティおよび`upToRemainingQuota`プロパティの設定値と、メッセージの予約数および最大送信数の関係は以下のとおりです。

| `max`プロパティ | `upToRemainingQuota`プロパティ | 予約数および最大送信数 |
| --- | --- | --- |
| 未指定 | false | ターゲットリーチの数 |
| 任意の数値 | false | ターゲットリーチの数と、`max`プロパティのうちの最小値 |
| 未指定 | true | ターゲットリーチの数と、当月分の上限目安のうちの最小値 |
| 任意の数値 | true | ターゲットリーチの数、当月分の上限目安、`max`プロパティのうちの最小値 |

#### レスポンス 

HTTPステータスコード`202`と空のJSONオブジェクトを返します。

ナローキャストメッセージの送信は非同期に行われます。ナローキャストメッセージの送信状況を確認する方法について詳しくは、「[ナローキャストメッセージの進行状況を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-narrowcast-progress-status)」を参照してください。

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | メッセージを送信できませんでした。次のような理由が考えられます。<ul><li>[再配信オブジェクト](https://developers.line.biz/ja/reference/messaging-api/#narrowcast-recipient-redelivery-object)に無効なリクエストIDが指定されている。</li><li>ステータスが`READY`以外など、無効なオーディエンスが指定されている。</li><li>無効なメッセージオブジェクトが指定されている。</li><li>無効な組み合わせのリクエストパラメータが指定されている。</li></ul> |
| `403` | 送信対象が不足しています。詳しくは、「[属性情報やオーディエンスを利用したメッセージ送信の制限事項](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message-restrictions)」を参照してください。 |
| `409` | 同じリトライキーを含むリクエストがすでに受理されています。詳しくは、「APIリクエストを再試行する」の「[すでにリクエストが受理されていた場合のレスポンス](https://developers.line.biz/ja/reference/messaging-api/#retry-api-request-response)」を参照してください。 |
| `429` | リクエスト数が上限を超過しました。次のような理由が考えられます。<ul><li>このエンドポイントの[レート制限](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-rate-limit)を超過した。</li><li>[当月に送信できるメッセージ数の上限目安](https://developers.line.biz/ja/reference/messaging-api/#get-quota)を超過した。</li></ul>メッセージ数の上限目安について詳しくは、『Messaging APIドキュメント』の「[Messaging APIの料金](https://developers.line.biz/ja/docs/messaging-api/pricing/)」を参照してください。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

エラーが返された場合、どのユーザーに対してもメッセージは送信されません。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なオーディエンスIDを指定した場合（400 Bad Request）
{
    "message": "Invalid audience group id: {audience ID}"
}

// 再配信オブジェクトに無効なリクエストIDを指定した場合（400 Bad Request）
{
    "message": "Invalid request id: {request ID}"
}

// limit.upToRemainingQuotaにtrueを設定せずにlimit.forbidPartialDeliveryにtrueを指定した場合（400 Bad Request）
{
    "message": "The option forbidPartialDelivery must be used with upToRemainingQuota."
}

// 十分な友だち数がない場合（403 Forbidden）
{
    "message": "Your account does not have enough friends"
}
```

<!-- tab end -->

### ナローキャストメッセージの進行状況を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/message/progress/narrowcast`

ナローキャストメッセージの進行状況を取得します。

<!-- note start -->

**送信対象が一定数よりも少ない場合は送信できません**

送信対象のユーザーの属性を推測できないようにするために、送信対象が一定数よりも少ない場合はナローキャストメッセージを送信できません。詳しくは、「[属性情報やオーディエンスを利用したメッセージ送信の制限事項](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message-restrictions)」を参照してください。

<!-- note end -->

<!-- note start -->

**進行状況を取得できる期間**

`acceptedTime`プロパティの値（タイムスタンプ）から14日（336時間）以上経過すると、進行状況は取得できません。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET 'https://api.line.me/v2/bot/message/progress/narrowcast?requestId={request_id}' \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: required) -->

requestId

ナローキャストメッセージのリクエストID。リクエストIDは、Messaging APIのリクエストごとに発行されるIDです。[レスポンスヘッダー](https://developers.line.biz/ja/reference/messaging-api/#response-headers)に含まれます。

<!-- parameter end -->

#### レスポンス 

HTTPステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

phase

String

進行状況。以下のいずれかの値です。

- `waiting`：送信準備ができていません。フィルタリングなどを行っています。
- `sending`：送信中です。
- `succeeded`：送信処理が完了しました。これは、ユーザーがメッセージを正常に受信したことを示していません。
- `failed`：送信が失敗しました。`failedDescription`プロパティで失敗した理由を確認できます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

successCount

Number

メッセージの受信に成功したユーザー数（※）

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

failureCount

Number

メッセージの受信に失敗したユーザー数（※）。\
`phase`が`succeeded`の場合でも、`failureCount`が0でない限りは、ナローキャストメッセージを受信できていないユーザーがいます。たとえば、ナローキャストメッセージを送信中に、ユーザーがLINE公式アカウントをブロックした場合は`failureCount`に加算されます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

targetCount

Number

メッセージが配信される予定のユーザー数（※）

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

failedDescription

String

送信が失敗した理由。`phase`プロパティが`failed`の場合にのみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

errorCode

Number

エラーの概要。`phase`プロパティが`failed`の場合にのみ含まれます。\
以下のいずれかの値が返されます。

- `1`：内部エラーが発生しました。
- `2`：送信対象が少なすぎたためエラーになりました。
- `3`：すでに受理されたリクエストを再試行したため、競合エラーが発生しました。
- `4`：送信対象が50人未満のオーディエンスが、送信条件に含まれています。
- `5`：送信対象の一部のみにメッセージが配信されることを防ぐために、メッセージの配信を中止しました。このエラーは、[`limit.forbidPartialDelivery`](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-limit)に`true`を指定してメッセージを送信し、送信対象の人数がメッセージの最大送信数を超えていた場合に発生します。

<!-- parameter end -->
<!-- parameter start -->

acceptedTime

String

ナローキャストメッセージ送信のリクエストを受け付けた時間をミリ秒で表します。

- フォーマット：[ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)（例：`2020-12-03T10:15:30.121Z`）
- タイムゾーン：UTC

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

completedTime

String

ナローキャストメッセージの送信を完了した時間をミリ秒で表します。`phase`プロパティが`succeeded`または`failed`の場合にのみ返されます。

- フォーマット：[ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)（例：`2020-12-03T10:15:30.121Z`）
- タイムゾーン：UTC

<!-- parameter end -->

※`phase`プロパティが`waiting`の場合は取得できません。

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | 無効なリクエストIDが指定されています。 |
| `404` | 進行状況が取得できませんでした。次のような理由が考えられます。<ul><li>進行状況を取得できる期間を超えている。</li><li>ナローキャストメッセージ以外のリクエストIDを指定した。</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 進行状況を取得できなかった場合（404 Not Found）
{
  "message": "Not found"
}
```

<!-- tab end -->

### ブロードキャストメッセージを送る 

Endpoint: `POST` `https://api.line.me/v2/bot/message/broadcast`

LINE公式アカウントと友だちになっているすべてのユーザーに、任意のタイミングでメッセージを送信します。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/message/broadcast \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {channel access token}' \
-H 'X-Line-Retry-Key: {UUID}' \
-d '{
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

#### レート制限 

60リクエスト/時

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

X-Line-Retry-Key

リトライキー。任意の方法で生成した16進表記のUUID（例：123e4567-e89b-12d3-a456-426614174000）を指定します。リトライキーはLINEから提供されません。開発者自身が一意のリトライキーを生成する必要があります。詳しくは、『Messaging APIドキュメント』の「[失敗したAPIリクエストを再試行する](https://developers.line.biz/ja/docs/messaging-api/retrying-api-request/)」を参照してください。

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

messages

[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の配列

送信するメッセージ\
最大件数：5

[ブロードキャストメッセージのメッセージオブジェクトを検証する](https://developers.line.biz/ja/reference/messaging-api/#validate-message-objects-of-broadcast-message)エンドポイントを使用すると、メッセージオブジェクトが有効かを検証できます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

notificationDisabled

Boolean

- `true`：メッセージ送信時に、ユーザーに通知されない。
- `false`：メッセージ送信時に、ユーザーに通知される。ただし、LINEで通知をオフにしている場合は通知されません。

デフォルト値は`false`です。

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
| `400` | 無効なメッセージオブジェクトが指定されています。 |
| `409` | 同じリトライキーを含むリクエストがすでに受理されています。詳しくは、「APIリクエストを再試行する」の「[すでにリクエストが受理されていた場合のレスポンス](https://developers.line.biz/ja/reference/messaging-api/#retry-api-request-response)」を参照してください。 |
| `429` | リクエスト数が上限を超過しました。次のような理由が考えられます。<ul><li>このエンドポイントの[レート制限](https://developers.line.biz/ja/reference/messaging-api/#send-broadcast-rate-limit)を超過した。</li><li>[当月に送信できるメッセージ数の上限目安](https://developers.line.biz/ja/reference/messaging-api/#get-quota)を超過した。</li></ul>メッセージ数の上限目安について詳しくは、『Messaging APIドキュメント』の「[Messaging APIの料金](https://developers.line.biz/ja/docs/messaging-api/pricing/)」を参照してください。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

エラーが返された場合、メッセージは送信されません。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// リクエストに無効なパラメータが含まれていた場合（400 Bad Request）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "May not be empty",
      "property": "messages[0].type"
    }
  ]
}
```

<!-- tab end -->

### メッセージに既読をつける 

Endpoint: `POST` `https://api.line.me/v2/bot/chat/markAsRead`

指定したメッセージと、それ以前に送られたすべてのメッセージに既読をつけます。詳しくは、『Messaging APIドキュメント』の「[メッセージに既読をつける](https://developers.line.biz/ja/docs/messaging-api/mark-as-read/)」を参照してください。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/chat/markAsRead \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {channel access token}' \
-d '{
  "markAsReadToken": "{mark as read token}"
}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

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

markAsReadToken

String

既読トークン。Webhookの[メッセージイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-event)の`markAsReadToken`プロパティに含まれます。

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

| コード | 説明                                   |
| ------ | -------------------------------------- |
| `400`  | 無効な既読トークンが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効な既読トークンを指定した場合（400 Bad Request）
{
  "message": "Invalid markAsReadToken. Tokens must be used by the bot that received them via Webhook."
}
```

<!-- tab end -->

### ローディングのアニメーションを表示する 

Endpoint: `POST` `https://api.line.me/v2/bot/chat/loading/start`

ユーザーとLINE公式アカウントの1対1のトークにおいて、ローディングのアニメーションを表示します。

ローディングのアニメーションは指定した秒数（5秒〜60秒）が経過するか、表示中にLINE公式アカウントからメッセージが届くと自動的に消えます。

ローディングのアニメーションは、ユーザーが対象のLINE公式アカウントとのトーク画面を表示しているときのみ表示されます。ユーザーがトーク画面を表示していないときに、ローディングのアニメーションを表示するリクエストを行っても、通知は行われません。また、その後にユーザーがトーク画面を開いてもアニメーションは表示されません。

ローディングのアニメーションが表示されている間に再び表示のリクエストを行うと、アニメーションはそのまま表示され続け、表示が消えるまでの時間は2回目のリクエストで指定した秒数に上書きされます。

ローディングのアニメーションが表示されるLINEのバージョンは以下のとおりです。

- iOS版またはAndroid版のLINE：13.16.0以降

詳しくは、『Messaging APIドキュメント』の「[ローディングのアニメーションを表示する](https://developers.line.biz/ja/docs/messaging-api/use-loading-indicator/)」を参照してください。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/chat/loading/start \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {channel access token}' \
-d '{
    "chatId": "U4af4980629...",
    "loadingSeconds": 5
}'
```

<!-- tab end -->

#### レート制限 

100リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

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

chatId

String

ローディングのアニメーションを表示する対象ユーザーのユーザーID。

ユーザーIDの取得方法については、『Messaging APIドキュメント』の「[ユーザーIDを取得する](https://developers.line.biz/ja/docs/messaging-api/getting-user-ids/)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

loadingSeconds

Number

ローディングのアニメーションを表示する秒数。`5`、`10`、`15`、`20`、`25`、`30`、`35`、`40`、`45`、`50`、`55`、`60`のいずれかの値を指定できます。

デフォルト値は`20`です。

<!-- parameter end -->

#### レスポンス 

ステータスコード`202`と空のJSONオブジェクトを返します。

なお、以下のユーザーを表示先に指定してリクエストを行った場合、ステータスコード`202`が返りますが、実際にはローディングのアニメーションは表示されません。

- LINE公式アカウントとのトーク画面を開いていないユーザー
- LINE公式アカウントを友だち追加していないユーザー
- LINE公式アカウントをブロックしているユーザー
- LINEアカウントを削除したユーザー

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
| `400` | ローディングのアニメーションを表示できませんでした。次のような理由が考えられます。<ul><li>無効な秒数が指定されています。</li><li>無効なユーザーIDが指定されています。</li><li>グループトークまたは複数人トークが指定されています。</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

エラーが返された場合、ローディングのアニメーションは表示されません。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効な秒数を指定した場合（400 Bad Request）
{
  "message": "The request body has 2 error(s)",
  "details": [
    {
      "message": "Must be between 5 and 60",
      "property": "loadingSeconds"
    },
    {
      "message": "must be a multiple of five",
      "property": "loadingSeconds"
    }
  ]
}

// 表示先にグループトークや複数人トークを指定した場合（400 Bad Request）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Only user id is acceptable, please confirm if there are any group/room ids or illegal ids.",
      "property": "chatId"
    }
  ]
}
```

<!-- tab end -->

### 当月に送信できるメッセージ数の上限目安を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/message/quota`

当月に送信できるメッセージ数の上限目安を取得します。無料メッセージ数と追加メッセージ数を合わせた値が返されます。

このエンドポイントで取得できるメッセージ数には、LINE Official Account Managerから送信するメッセージの数も含まれます。

追加メッセージの上限は、LINE Official Account Managerで設定します。設定方法について詳しくは、『LINEヤフー for Business』の「[利用と請求（プラン変更やお支払い関連の管理）](https://www.lycbiz.com/jp/manual/OfficialAccountManager/account-settings_plan/?list=7171)」を参照してください。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/message/quota \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

type

String

上限目安が設定されているかどうかを示す値。以下のどちらかになります。

- `none`：上限目安が未設定であることを示します。
- `limited`：上限目安が設定されていることを示します。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

value

Number

当月に送信できるメッセージ数の上限目安。`type`プロパティが`limited`の場合にのみ返されます。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "type": "limited",
  "value": 1000
}
```

<!-- tab end -->

#### エラーレスポンス 

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

### 当月のメッセージ利用状況を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/message/quota/consumption`

当月に送信されたメッセージの数を取得します。

この操作により取得されるメッセージ数には、LINE Official Account Managerから送信するメッセージの数も含まれます。

この操作により取得されるメッセージ数は概算です。正確なメッセージ送信数を取得するには、LINE Official Account Managerを使用するか、送信済みのメッセージ数を取得するAPI操作を実行してください。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/message/quota/consumption \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

totalUsage

Number

当月に送信されたメッセージの数

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "totalUsage": 500
}
```

<!-- tab end -->

#### エラーレスポンス 

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

### 送信済みの応答メッセージの数を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/message/delivery/reply`

[`/bot/message/reply`](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)エンドポイントを使って送信されたメッセージの数を取得します。

この操作により取得されるメッセージ数に、LINE Official Account Managerから送信されたメッセージの数は含まれません。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET "https://api.line.me/v2/bot/message/delivery/reply?date={yyyyMMdd}" \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: required) -->

date

メッセージが送信された日付

- フォーマット：`yyyyMMdd`（例：`20191231`）
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

`date`に指定した日付に、Messaging APIを使って送信されたメッセージの数。`status`の値が`ready`の場合にのみ、レスポンスに含まれます。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "status": "ready",
  "success": 10000
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | 無効なフォーマットの日付が指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なフォーマットの日付を指定した場合（400 Bad Request）
{
  "message": "The value for the 'date' parameter is invalid"
}
```

<!-- tab end -->

### 送信済みのプッシュメッセージの数を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/message/delivery/push`

[`/bot/message/push`](https://developers.line.biz/ja/reference/messaging-api/#send-push-message)エンドポイントを使って送信されたメッセージの数を取得します。

この操作により取得されるメッセージ数に、LINE Official Account Managerから送信されたメッセージの数は含まれません。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET "https://api.line.me/v2/bot/message/delivery/push?date={yyyyMMdd}" \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: required) -->

date

メッセージが送信された日付

- フォーマット：`yyyyMMdd`（例：`20191231`）
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

`date`に指定した日付に、Messaging APIを使って送信されたメッセージの数。`status`の値が`ready`の場合にのみ、レスポンスに含まれます。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "status": "ready",
  "success": 10000
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | 無効なフォーマットの日付が指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なフォーマットの日付を指定した場合（400 Bad Request）
{
  "message": "The value for the 'date' parameter is invalid"
}
```

<!-- tab end -->

### 送信済みのマルチキャストメッセージの数を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/message/delivery/multicast`

[`/bot/message/multicast`](https://developers.line.biz/ja/reference/messaging-api/#send-multicast-message)エンドポイントを使って送信されたメッセージの数を取得します。

この操作により取得されるメッセージ数に、LINE Official Account Managerから送信されたメッセージの数は含まれません。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET "https://api.line.me/v2/bot/message/delivery/multicast?date={yyyyMMdd}" \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: required) -->

date

メッセージが送信された日付

- フォーマット：`yyyyMMdd`（例：`20191231`）
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

`date`に指定した日付に、Messaging APIを使って送信されたメッセージの数。`status`の値が`ready`の場合にのみ、レスポンスに含まれます。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "status": "ready",
  "success": 10000
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | 無効なフォーマットの日付が指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なフォーマットの日付を指定した場合（400 Bad Request）
{
  "message": "The value for the 'date' parameter is invalid"
}
```

<!-- tab end -->

### 送信済みのブロードキャストメッセージの数を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/message/delivery/broadcast`

[`/bot/message/broadcast`](https://developers.line.biz/ja/reference/messaging-api/#send-broadcast-message)エンドポイントを使って送信されたメッセージの数を取得します。

この操作により取得されるメッセージ数に、LINE Official Account Managerから送信されたメッセージの数は含まれません。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET "https://api.line.me/v2/bot/message/delivery/broadcast?date={yyyyMMdd}" \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: required) -->

date

メッセージが送信された日付

- フォーマット：`yyyyMMdd`（例：`20191231`）
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

`date`に指定した日付に、Messaging APIを使って送信されたメッセージの数。`status`の値が`ready`の場合にのみ、レスポンスに含まれます。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "status": "ready",
  "success": 10000
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | 無効なフォーマットの日付が指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なフォーマットの日付を指定した場合（400 Bad Request）
{
  "message": "The value for the 'date' parameter is invalid"
}
```

<!-- tab end -->

### 応答メッセージのメッセージオブジェクトを検証する 

Endpoint: `POST` `https://api.line.me/v2/bot/message/validate/reply`

[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の配列が、[応答メッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)エンドポイントの[リクエストボディ](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message-request-body)の`messages`プロパティの値として有効かを検証します。`messages`プロパティ以外のプロパティの値が有効かは検証しません。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/message/validate/reply \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d \
'{
  "messages": [
    {
      "type": "text",
      "text": "Hello, world"
    }
  ]
}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

messages

Array of objects

検証したい[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の配列

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

| コード | 説明                                             |
| ------ | ------------------------------------------------ |
| `400`  | 無効なメッセージオブジェクトが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例（メッセージオブジェクトを最大件数より多く指定した場合）_

<!-- tab start `json` -->

```json
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Size must be between 1 and 5",
      "property": "messages"
    }
  ]
}
```

<!-- tab end -->

_エラーレスポンスの例（テキストメッセージの文字数を最大文字数より多く指定した場合）_

<!-- tab start `json` -->

```json
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Length must be between 0 and 5000",
      "property": "messages[0].text"
    }
  ]
}
```

<!-- tab end -->

### プッシュメッセージのメッセージオブジェクトを検証する 

Endpoint: `POST` `https://api.line.me/v2/bot/message/validate/push`

[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の配列が、[プッシュメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-push-message)エンドポイントの[リクエストボディ](https://developers.line.biz/ja/reference/messaging-api/#send-push-message-request-body)の`messages`プロパティの値として有効かを検証します。`messages`プロパティ以外のプロパティの値が有効かは検証しません。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/message/validate/push \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d \
'{
  "messages": [
    {
      "type": "text",
      "text": "Hello, world"
    }
  ]
}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

messages

Array of objects

検証したい[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の配列

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

| コード | 説明                                             |
| ------ | ------------------------------------------------ |
| `400`  | 無効なメッセージオブジェクトが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例（メッセージオブジェクトを最大件数より多く指定した場合）_

<!-- tab start `json` -->

```json
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Size must be between 1 and 5",
      "property": "messages"
    }
  ]
}
```

<!-- tab end -->

_エラーレスポンスの例（テキストメッセージの文字数を最大文字数より多く指定した場合）_

<!-- tab start `json` -->

```json
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Length must be between 0 and 5000",
      "property": "messages[0].text"
    }
  ]
}
```

<!-- tab end -->

### マルチキャストメッセージのメッセージオブジェクトを検証する 

Endpoint: `POST` `https://api.line.me/v2/bot/message/validate/multicast`

[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の配列が、[マルチキャストメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-multicast-message)エンドポイントの[リクエストボディ](https://developers.line.biz/ja/reference/messaging-api/#send-multicast-request-body)の`messages`プロパティの値として有効かを検証します。`messages`プロパティ以外のプロパティの値が有効かは検証しません。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/message/validate/multicast \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d \
'{
  "messages": [
    {
      "type": "text",
      "text": "Hello, world"
    }
  ]
}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

messages

Array of objects

検証したい[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の配列

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

| コード | 説明                                             |
| ------ | ------------------------------------------------ |
| `400`  | 無効なメッセージオブジェクトが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例（メッセージオブジェクトを最大件数より多く指定した場合）_

<!-- tab start `json` -->

```json
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Size must be between 1 and 5",
      "property": "messages"
    }
  ]
}
```

<!-- tab end -->

_エラーレスポンスの例（テキストメッセージの文字数を最大文字数より多く指定した場合）_

<!-- tab start `json` -->

```json
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Length must be between 0 and 5000",
      "property": "messages[0].text"
    }
  ]
}
```

<!-- tab end -->

### ナローキャストメッセージのメッセージオブジェクトを検証する 

Endpoint: `POST` `https://api.line.me/v2/bot/message/validate/narrowcast`

[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の配列が、[ナローキャストメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message)エンドポイントの[リクエストボディ](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-request-body)の`messages`プロパティの値として有効かを検証します。`messages`プロパティ以外のプロパティの値が有効かは検証しません。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/message/validate/narrowcast \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d \
'{
  "messages": [
    {
      "type": "text",
      "text": "Hello, world"
    }
  ]
}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

messages

Array of objects

検証したい[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の配列

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

| コード | 説明                                             |
| ------ | ------------------------------------------------ |
| `400`  | 無効なメッセージオブジェクトが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例（メッセージオブジェクトを最大件数より多く指定した場合）_

<!-- tab start `json` -->

```json
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Size must be between 1 and 5",
      "property": "messages"
    }
  ]
}
```

<!-- tab end -->

_エラーレスポンスの例（テキストメッセージの文字数を最大文字数より多く指定した場合）_

<!-- tab start `json` -->

```json
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Length must be between 0 and 5000",
      "property": "messages[0].text"
    }
  ]
}
```

<!-- tab end -->

### ブロードキャストメッセージのメッセージオブジェクトを検証する 

Endpoint: `POST` `https://api.line.me/v2/bot/message/validate/broadcast`

[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の配列が、[ブロードキャストメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-broadcast-message)エンドポイントの[リクエストボディ](https://developers.line.biz/ja/reference/messaging-api/#send-broadcast-request-body)の`messages`プロパティの値として有効かを検証します。`messages`プロパティ以外のプロパティの値が有効かは検証しません。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/message/validate/broadcast \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d \
'{
  "messages": [
    {
      "type": "text",
      "text": "Hello, world"
    }
  ]
}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

messages

Array of objects

検証したい[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の配列

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

| コード | 説明                                             |
| ------ | ------------------------------------------------ |
| `400`  | 無効なメッセージオブジェクトが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例（メッセージオブジェクトを最大件数より多く指定した場合）_

<!-- tab start `json` -->

```json
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Size must be between 1 and 5",
      "property": "messages"
    }
  ]
}
```

<!-- tab end -->

_エラーレスポンスの例（テキストメッセージの文字数を最大文字数より多く指定した場合）_

<!-- tab start `json` -->

```json
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Length must be between 0 and 5000",
      "property": "messages[0].text"
    }
  ]
}
```

<!-- tab end -->

### APIリクエストを再試行する 

プッシュメッセージ、マルチキャストメッセージ、ナローキャストメッセージ、ブロードキャストメッセージに、リトライキー（`X-Line-Retry-Key`）をHTTPヘッダーに含めることで、同じAPIリクエストを重複して処理しないように再試行できます。

LINEプラットフォーム側のリトライキーの管理期間は24時間です。同じリトライキーを24時間を超えて使用すると、新しいAPIリクエストとして扱われます。

APIリクエストの再試行について詳しくは、『Messaging APIドキュメント』の「[失敗したAPIリクエストを再試行する](https://developers.line.biz/ja/docs/messaging-api/retrying-api-request/)」を参照してください。

<!-- note start -->

**同じリトライキーを24時間を超えて使用しないでください**

同じリトライキーを24時間を超えて使用すると、同じリトライキーを含むAPIリクエストがすでに成功していても、新しいAPIリクエストとして成功します。その結果、重複したメッセージが送信されてしまいます。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/message/push \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {CHANNEL_ACCESS_TOKEN}' \
-H 'X-Line-Retry-Key: {UUID}' \
-d '{
    "messages": [
        {
            "type": "text",
            "text": "Hello, user"
        }
    ]
}'
```

<!-- tab end -->

#### リクエストヘッダー 

<!-- parameter start (props: annotation="任意※") -->

X-Line-Retry-Key

任意の方法で生成した16進表記のUUID（例：123e4567-e89b-12d3-a456-426614174000）

<!-- parameter end -->

※ APIリクエストを再試行する場合は必須です。

#### すでにリクエストが受理されていた場合のレスポンス 

同じリトライキーを含むリクエストがすでに受理されていた場合は、ステータスコード`409`と、すでに受理されたリクエストのリクエストIDを示す`x-line-accepted-request-id`ヘッダー、および以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

message

String

すでにリクエストが受理されていることを知らせるメッセージ

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

sentMessages

Array

送信したメッセージの配列。プッシュメッセージを送信した場合のみ、レスポンスに含まれます。<br />最大件数：5

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

sentMessages.id

Number

送信したメッセージのID。プッシュメッセージを送信した場合のみ、レスポンスに含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

sentMessages.quoteToken

String

メッセージの引用トークン。プッシュメッセージで、引用対象として指定可能なメッセージオブジェクトを送信した場合のみ、レスポンスに含まれます。詳しくは、『Messaging APIドキュメント』の「[引用トークンを取得する](https://developers.line.biz/ja/docs/messaging-api/get-quote-tokens/)」を参照してください。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
HTTP/1.1 409 Conflict
x-line-request-id: 123e4567-e89b-12d3-a456-426655440002
x-line-accepted-request-id: 123e4567-e89b-12d3-a456-426655440001

{
  "message": "The retry key is already accepted",
  "sentMessages": [
    {
      "id": "461230966842064897",
      "quoteToken": "IStG5h1Tz7b..."
    }
  ]
}
```

<!-- tab end -->

## オーディエンス管理 

オーディエンスを作成、更新、有効化、削除できます。オーディエンスは、ナローキャストメッセージを配信する際に指定します。

なお、オーディエンスは、[LINE Official Account Manager](https://manager.line.biz/)でも作成できます。詳しくは、『LINEヤフー for Business』の「[オーディエンス](https://www.lycbiz.com/jp/manual/OfficialAccountManager/messages-audience/)」を参照してください。

| オーディエンス | 作成方法 |
| --- | --- |
| ユーザーIDアップロード用のオーディエンス | <ul><li>[Messaging API](https://developers.line.biz/ja/reference/messaging-api/#create-upload-audience-group)</li><li>[LINE Official Account Manager](https://manager.line.biz/)</li><li>[LINEポイントAD](https://www.lycbiz.com/jp/service/line-point-ad/)</li></ul> |
| メッセージクリックオーディエンス | <ul><li>[Messaging API](https://developers.line.biz/ja/reference/messaging-api/#create-click-audience-group)</li><li>[LINE Official Account Manager](https://manager.line.biz/)</li></ul> |
| メッセージインプレッションオーディエンス | <ul><li>[Messaging API](https://developers.line.biz/ja/reference/messaging-api/#create-imp-audience-group)</li><li>[LINE Official Account Manager](https://manager.line.biz/)</li></ul> |
| チャットタグオーディエンス | [LINE Official Account Manager](https://manager.line.biz/) |
| 追加経路オーディエンス | [LINE Official Account Manager](https://manager.line.biz/) |
| 予約オーディエンス | [LINE Official Account Manager](https://manager.line.biz/) |
| リッチメニューインプレッションオーディエンス | [LINE Official Account Manager](https://manager.line.biz/) |
| リッチメニュークリックオーディエンス | [LINE Official Account Manager](https://manager.line.biz/) |
| ウェブトラフィックオーディエンス（LINE Tag） | <ul><li>[LINE Official Account Manager](https://manager.line.biz/)</li><li>[LINE広告](https://admanager.line.biz/)</li></ul> |
| ウェブトラフィックオーディエンス（計測タグ） | [LINE Official Account Manager](https://manager.line.biz/) |
| アプリイベントオーディエンス | [LINE広告](https://admanager.line.biz/) |
| 動画視聴オーディエンス | [LINE広告](https://admanager.line.biz/) |
| 画像クリックオーディエンス | [LINE広告](https://admanager.line.biz/) |
| LINE Beacon Networkインプレッションオーディエンス \* | [LINE広告](https://admanager.line.biz/) |

\* LINE Beacon Networkインプレッションオーディエンスは、台湾のユーザーが作成したLINE公式アカウントの場合のみ利用できます。

<!-- note start -->

**注意**

- 日本（JP）、タイ（TH）、台湾（TW）のユーザーが作成したLINE公式アカウントの場合のみ、オーディエンスを利用できます。
- Messaging APIでは、次のタイプのオーディエンスは作成できません。
  - チャットタグオーディエンス
  - 追加経路オーディエンス
  - 予約オーディエンス
  - リッチメニューインプレッションオーディエンス
  - リッチメニュークリックオーディエンス
  - ウェブトラフィックオーディエンス（LINE Tag）
  - ウェブトラフィックオーディエンス（計測タグ）
  - アプリイベントオーディエンス
  - 動画視聴オーディエンス
  - 画像クリックオーディエンス
  - LINE Beacon Networkインプレッションオーディエンス

<!-- note end -->

### オーディエンス管理に関するエラーの詳細 

オーディエンス管理のエンドポイントでエラーが発生した際の詳細は、JSONレスポンスの`details[].message`プロパティに含まれます。主なエラーの詳細は以下のとおりです。

| メッセージ | 説明 |
| --- | --- |
| `AUDIENCE_GROUP_CAN_NOT_UPLOAD_STATUS_EXPIRED` | オーディエンスを作成してから180日（15,552,000秒）を超えたため、このオーディエンスは使用できません。 |
| `AUDIENCE_GROUP_COUNT_MAX_OVER` | 作成できるオーディエンス数の上限（合計1,000件）に達しています。 |
| `AUDIENCE_GROUP_NAME_SIZE_OVER` | オーディエンスの名前が長すぎます。 |
| `AUDIENCE_GROUP_NAME_WRONG` | オーディエンスの名前に、無効な文字（例：`\n`などの制御コード）を指定しました。 |
| `AUDIENCE_GROUP_NAME_EMPTY` | オーディエンスの名前が空であるか、空白文字のみを指定しました。 |
| `AUDIENCE_GROUP_NOT_FOUND` | オーディエンスが見つかりません。 |
| `AUDIENCE_GROUP_REQUESTID_DUPLICATE` | 既存のオーディエンスに指定したリクエストIDと同じ値を指定しました。 |
| `AUDIENCE_GROUP_UPLOAD_DESCRIPTION_SIZE_OVER` | オーディエンスの説明が長すぎます。 |
| `REQUEST_NOT_FOUND` | 指定したリクエストIDが誤っているか、指定したリクエストIDでオーディエンスを作成する準備ができていません。 |
| `TOO_OLD_MESSAGES` | メッセージを配信してから60日（5,184,000秒）を超えた場合、そのメッセージ（リクエストID）に対するオーディエンスは作成できません。 |
| `UPLOAD_AUDIENCE_GROUP_INVALID_AUDIENCE_ID_FORMAT` | <ul><li>`file`プロパティに指定したファイルに、無効なユーザーIDまたはIFAが入力されています。</li><li>`audiences[].id`プロパティに、無効なユーザーIDまたはIFAが指定されています。</li></ul>このメッセージが返ってきた場合は、[対処方法](https://developers.line.biz/ja/reference/messaging-api/#manage-audience-error-handling)を参照してください。 |
| `UPLOAD_AUDIENCE_GROUP_NO_VALID_AUDIENCE_IDS` | <ul><li>`file`プロパティに指定したファイルに、有効なユーザーIDまたはIFAが入力されていません。</li><li>`audiences[].id`プロパティに、有効なユーザーIDまたはIFAが指定されていません。</li></ul> |
| `UPLOAD_AUDIENCE_GROUP_TOO_MANY_AUDIENCE_IDS` | ユーザーIDまたはIFAの登録上限に達しています。 |
| `WRONG_BOT_ID` | 指定したリクエストIDに含まれるボットIDが、アクセストークンを発行したチャネルに関連付けられたボットと異なります。 |
| `ALREADY_ACTIVE` | オーディエンスグループは、すでに有効です。 |

#### 対処方法 

<!-- note start -->

**audiencesプロパティに無効なユーザーIDが含まれている場合**

`UPLOAD_AUDIENCE_GROUP_INVALID_AUDIENCE_ID_FORMAT`が返る場合は、[プロフィール情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-profile)エンドポイントを使って、JSONに指定しているすべてのユーザーIDのプロフィール情報を取得してください。ステータスコード`200`以外を返すユーザーIDをJSONから除外したうえで、失敗したエンドポイントを再実行してください。

<!-- note end -->

### ユーザーIDアップロード用のオーディエンスを作成する（JSON指定） 

Endpoint: `POST` `https://api.line.me/v2/bot/audienceGroup/upload`

ユーザーIDアップロード用のオーディエンスを作成します。

このエンドポイントでは、送信対象アカウントをJSONで指定します。[送信対象アカウントをテキストファイルで指定するエンドポイント](https://developers.line.biz/ja/reference/messaging-api/#create-upload-audience-group-by-file)も利用できます。

ユーザーIDの取得方法については、『Messaging APIドキュメント』の「[ユーザーIDを取得する](https://developers.line.biz/ja/docs/messaging-api/getting-user-ids/)」を参照してください。

#### オーディエンスに追加できるユーザーの条件 

ユーザーIDアップロード用のオーディエンスには、LINE公式アカウントと友だちになっているユーザーを追加できます。ただし、以下のユーザーをオーディエンスに追加した場合も、ステータスコード`202`が返され、オーディエンスに追加されます。

- LINEアカウントを削除したユーザー
- オーディエンスを作成したLINE公式アカウントをブロックしているユーザー
- オーディエンスを作成したLINE公式アカウントを友だち追加していないユーザー

なお、作成したオーディエンスを使ってメッセージを送信した場合、上記のユーザーにはメッセージは送信されません。

<!-- note start -->

**同時処理数の制限があります**

ユーザーIDアップロード用のオーディエンス作成およびオーディエンスへのユーザーID追加のエンドポイントでは、オーディエンスID（`audienceGroupId`）単位での同時処理数の制限があります。詳しくは、「[同時処理数の制限](https://developers.line.biz/ja/reference/messaging-api/#limit-on-the-number-of-concurrent-operations)」を参照してください。

<!-- note end -->

<!-- note start -->

**送信対象アカウントをIFA（Identifier For Advertisers）で指定するには手続きが必要です**

送信対象アカウントをIFAで指定することもできますが、この機能は、所定の申請等を行った法人ユーザーのみがご利用いただけます。自社のLINE公式アカウントでご利用になりたいお客様は、担当営業までご連絡いただくか、[弊社パートナー](https://www.lycbiz.com/jp/partner/sales/)にお問い合わせください。

<!-- note end -->

<!-- tip start -->

**ユーザーIDアップロード用のオーディエンスの仕様**

オーディエンスの仕様は以下のとおりです。

| 項目 | 条件 |
| --- | --- |
| チャネルあたりのオーディエンス数 | 最大1,000件 |
| オーディエンスの保存期間 | 最大180日間（15,552,000秒間） |
| オーディエンスに、1リクエストでアップロードできるユーザーIDまたはIFAの数 | JSONを使用する場合：最大10,000件<br>ファイルを使用する場合：最大1,500,000件 |
| オーディエンスあたりのユーザー数 | ユーザーIDアップロード用のオーディエンス：制限なし |

ナローキャストメッセージの使用制限については、「[属性情報やオーディエンスを利用したメッセージ送信の制限事項](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message-restrictions)」を参照してください。

<!-- tip end -->

<!-- note start -->

**有効なユーザーIDの確認方法**

JSONの`audiences`プロパティで無効なユーザーIDが指定されていた場合、エラーレスポンス（`details[].message`: `UPLOAD_AUDIENCE_GROUP_INVALID_AUDIENCE_ID_FORMAT`）が返り、オーディエンスの作成に失敗します。このエンドポイントを実行する前に、`audiences`プロパティに含まれるすべてのユーザーIDが有効であることを確認してください。

ユーザーIDが有効か確認するには、[プロフィール情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-profile)エンドポイントを使用してください。ユーザーIDが有効な場合は、HTTPステータスコード`200`が返ります。`200`以外が返ってきた場合、そのユーザーIDは無効のため、`audiences`プロパティには含めないようにしてください。

<!-- note end -->

<!-- note start -->

**ユーザーIDを含まないオーディエンスのステータス**

オーディエンス作成時にJSONの`audiences`プロパティが省略された、または空配列が指定された場合、ユーザーを含まない空のオーディエンスが作成されます。

空のオーディエンスは、オーディエンスに含まれるユーザーの数（`audienceGroup.audienceCount`）が0であり、配信に利用できません。そのため、レスポンスの`audienceGroup.status`は`IN_PROGRESS`のまま、`READY`にはなりません。

<!-- note end -->

<!-- note start -->

**LINEのプライバシーポリシー（2022年3月改定以降のもの）に同意済みのユーザーのみが対象となります**

ユーザーIDアップロード用のオーディエンスにユーザーIDを追加する際に、LINEのプライバシーポリシー（2022年3月改定以降のもの）に同意していないユーザーのユーザーIDが含まれている場合、未同意のユーザーは無視され同意済みのユーザーのみが追加されます。

そのため、指定したユーザーIDの数よりもオーディエンスの有効な送信対象アカウントの数が少なくなることがあります。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/audienceGroup/upload \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d '{
    "description": "audienceGroupName_01"
}'
```

<!-- tab end -->

#### レート制限 

60リクエスト/分

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

`application/json`

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

description

String

オーディエンスの名前。なお、大文字と小文字は区別されないため、`AUDIENCE`と`audience`は同じ名前と判定されます。\
最大文字数：120

<!-- parameter end -->
<!-- parameter start (props: optional) -->

isIfaAudience

Boolean

- 送信対象アカウントをIFAで指定する場合は、`true`を指定します。
- 送信対象アカウントをユーザーIDで指定する場合は、`false`を指定するか、`isIfaAudience`プロパティを省略します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

uploadDescription

String

ジョブ（`jobs[].description`）に登録する説明\
最大文字数：300

<!-- parameter end -->
<!-- parameter start (props: optional) -->

audiences

Array

ユーザーIDまたはIFAの配列。\
省略すると、空のオーディエンスが作成されます。\
最大件数：10,000

<!-- parameter end -->
<!-- parameter start (props: optional) -->

audiences\[].id

String

ユーザーIDまたはIFA。空配列も指定できます。\
空配列の場合、空のオーディエンスが作成されます。

<!-- parameter end -->

#### レスポンス 

ステータスコード`202`と以下の情報を含むJSONオブジェクトを返します。

<!-- note start -->

**オーディエンスの作成は非同期に行われます**

オーディエンスを利用する前に、[オーディエンスが配信に利用できることを確認](https://developers.line.biz/ja/docs/messaging-api/sending-messages/#get-audience-status)してください。

<!-- note end -->

<!-- parameter start -->

audienceGroupId

Number

オーディエンスID

<!-- parameter end -->
<!-- parameter start -->

createRoute

String

オーディエンスの作成方法。

- `MESSAGING_API`：Messaging APIで作成したオーディエンス

<!-- parameter end -->
<!-- parameter start -->

type

String

オーディエンスのタイプ。

- `UPLOAD`：ユーザーIDアップロード用のオーディエンス

<!-- parameter end -->
<!-- parameter start -->

description

String

オーディエンスの名前

<!-- parameter end -->
<!-- parameter start -->

created

Number

オーディエンスが作成された時刻。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

permission

String

作成したオーディエンスに対する更新権限。

- `READ_WRITE`：オーディエンスを利用、更新できます。

<!-- parameter end -->
<!-- parameter start -->

expireTimestamp

Number

オーディエンスの有効期限。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

isIfaAudience

Boolean

ユーザーIDアップロード用のオーディエンスを作成したときに指定した、送信対象アカウントの種類を示す値。以下のいずれかの値です。

- `true`：IFAで指定する
- `false`：ユーザーIDで指定する（デフォルト）

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "audienceGroupId": 1234567890123,
  "createRoute": "MESSAGING_API",
  "type": "UPLOAD",
  "description": "audienceGroupName_01",
  "created": 1613698278,
  "permission": "READ_WRITE",
  "expireTimestamp": 1629250278,
  "isIfaAudience": false
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>作成できるオーディエンス数の上限（合計1,000件）に達している。</li><li>`description`プロパティに最大文字数（120文字）より長い名前が指定されている。</li><li>`description`プロパティに無効な文字（例：`\n`などの制御コード）が指定されている。</li><li>`description`プロパティが空であるか、空白文字のみが指定されている。</li><li>`uploadDescription`プロパティに最大文字数（300文字）より長い文字列が指定されている。</li><li>`audiences[].id`プロパティに、無効なユーザーIDまたはIFAが指定されている。</li><li>`audiences`プロパティに最大件数（10,000件）より多いユーザーIDまたはIFAが指定されている。</li></ul> |
| `429` | 同時処理数の上限を超えています。詳しくは、「[同時処理数の制限](https://developers.line.biz/ja/reference/messaging-api/#limit-on-the-number-of-concurrent-operations)」を参照してください。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// descriptionプロパティに最大文字数（120文字）より長い名前を指定した場合（400 Bad Request）
{
  "message": "size over audienceGroupName",
  "details": [
    {
      "message": "AUDIENCE_GROUP_NAME_SIZE_OVER"
    }
  ]
}
```

<!-- tab end -->

### ユーザーIDアップロード用のオーディエンスを作成する（ファイル指定） 

Endpoint: `POST` `https://api-data.line.me/v2/bot/audienceGroup/upload/byFile`

<!-- note start -->

**他のエンドポイントとドメイン名が異なります**

このエンドポイントは、Messaging APIにおけるLINEプラットフォームへの大容量データ送受信用のドメイン名（`api-data.line.me`）です。他のエンドポイントのドメイン名（`api.line.me`）とは異なるため、利用時は注意してください。

<!-- note end -->

ユーザーIDアップロード用のオーディエンスを作成します。

このエンドポイントでは、送信対象アカウントをテキストファイルで指定します。[送信対象アカウントをJSONで指定するエンドポイント](https://developers.line.biz/ja/reference/messaging-api/#create-upload-audience-group)も利用できます。

ユーザーIDの取得方法については、『Messaging APIドキュメント』の「[ユーザーIDを取得する](https://developers.line.biz/ja/docs/messaging-api/getting-user-ids/)」を参照してください。

#### オーディエンスに追加できるユーザーの条件 

ユーザーIDアップロード用のオーディエンスには、LINE公式アカウントと友だちになっているユーザーを追加できます。ただし、以下のユーザーをオーディエンスに追加した場合も、ステータスコード`202`が返され、オーディエンスに追加されます。

- LINEアカウントを削除したユーザー
- オーディエンスを作成したLINE公式アカウントをブロックしているユーザー
- オーディエンスを作成したLINE公式アカウントを友だち追加していないユーザー

なお、作成したオーディエンスを使ってメッセージを送信した場合、上記のユーザーにはメッセージは送信されません。

<!-- note start -->

**同時処理数の制限があります**

ユーザーIDアップロード用のオーディエンス作成およびオーディエンスへのユーザーID追加のエンドポイントでは、オーディエンスID（`audienceGroupId`）単位での同時処理数の制限があります。詳しくは、「[同時処理数の制限](https://developers.line.biz/ja/reference/messaging-api/#limit-on-the-number-of-concurrent-operations)」を参照してください。

<!-- note end -->

<!-- note start -->

**送信対象アカウントをIFA（Identifier For Advertisers）で指定するには手続きが必要です**

送信対象アカウントをIFAで指定することもできますが、この機能は、所定の申請等を行った法人ユーザーのみがご利用いただけます。自社のLINE公式アカウントでご利用になりたいお客様は、担当営業までご連絡いただくか、[弊社パートナー](https://www.lycbiz.com/jp/partner/sales/)にお問い合わせください。

<!-- note end -->

<!-- tip start -->

**ユーザーIDアップロード用のオーディエンスの仕様**

オーディエンスの仕様は以下のとおりです。

| 項目 | 条件 |
| --- | --- |
| チャネルあたりのオーディエンス数 | 最大1,000件 |
| オーディエンスの保存期間 | 最大180日間（15,552,000秒間） |
| オーディエンスに、1リクエストでアップロードできるユーザーIDまたはIFAの数 | JSONを使用する場合：最大10,000件<br>ファイルを使用する場合：最大1,500,000件 |
| オーディエンスあたりのユーザー数 | ユーザーIDアップロード用のオーディエンス：制限なし |

ナローキャストメッセージの使用制限については、「[属性情報やオーディエンスを利用したメッセージ送信の制限事項](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message-restrictions)」を参照してください。

<!-- tip end -->

<!-- note start -->

**LINEのプライバシーポリシー（2022年3月改定以降のもの）に同意済みのユーザーのみが対象となります**

ユーザーIDアップロード用のオーディエンスにユーザーIDを追加する際に、LINEのプライバシーポリシー（2022年3月改定以降のもの）に同意していないユーザーのユーザーIDが含まれている場合、未同意のユーザーは無視され同意済みのユーザーのみが追加されます。

そのため、指定したユーザーIDの数よりもオーディエンスの有効な送信対象アカウントの数が少なくなることがあります。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api-data.line.me/v2/bot/audienceGroup/upload/byFile \
-H 'Authorization: Bearer {channel access token}' \
-F 'description=audienceGroupName_01' \
-F 'file=@audiences.txt;type=text/plain'
```

<!-- tab end -->

_テキストファイルの例_

<!-- tab start `File` -->

```
U4af4980627...
U4af4980628...
U4af4980629...
```

<!-- tab end -->

#### レート制限 

60リクエスト/分

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

`multipart/form-data`

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

description

String

オーディエンスの名前。なお、大文字と小文字は区別されないため、`AUDIENCE`と`audience`は同じ名前と判定されます。\
最大文字数：120

<!-- parameter end -->
<!-- parameter start (props: optional) -->

isIfaAudience

Boolean

- 送信対象アカウントをIFAで指定する場合は、`true`を指定します。
- 送信対象アカウントをユーザーIDで指定する場合は、`false`を指定するか、`isIfaAudience`プロパティを省略します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

uploadDescription

String

ジョブ（`jobs[].description`）に登録する説明\
最大文字数：300

<!-- parameter end -->
<!-- parameter start (props: required) -->

file

File

ユーザーIDまたはIFAを、1行に1件入力したテキストファイル。Content-Typeは、`text/plain`を指定してください。\
最大ファイル数：1\
最大行数：1,500,000

<!-- parameter end -->

#### レスポンス 

ステータスコード`202`と以下の情報を含むJSONオブジェクトを返します。

<!-- note start -->

**オーディエンスの作成は非同期に行われます**

オーディエンスを利用する前に、[オーディエンスが配信に利用できることを確認](https://developers.line.biz/ja/docs/messaging-api/sending-messages/#get-audience-status)してください。

<!-- note end -->

<!-- parameter start -->

audienceGroupId

Number

オーディエンスID

<!-- parameter end -->
<!-- parameter start -->

createRoute

String

オーディエンスの作成方法。

- `MESSAGING_API`：Messaging APIで作成したオーディエンス

<!-- parameter end -->
<!-- parameter start -->

type

String

オーディエンスのタイプ。

- `UPLOAD`：ユーザーIDアップロード用のオーディエンス

<!-- parameter end -->
<!-- parameter start -->

description

String

オーディエンスの名前

<!-- parameter end -->
<!-- parameter start -->

created

Number

オーディエンスが作成された時刻。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

permission

String

作成したオーディエンスに対する更新権限。

- `READ_WRITE`：オーディエンスを利用、更新できます。

<!-- parameter end -->
<!-- parameter start -->

expireTimestamp

Number

オーディエンスの有効期限。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

isIfaAudience

Boolean

ユーザーIDアップロード用のオーディエンスを作成したときに指定した、送信対象アカウントの種類を示す値。以下のいずれかの値です。

- `true`：IFAで指定する
- `false`：ユーザーIDで指定する（デフォルト）

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "audienceGroupId": 1234567890123,
  "createRoute": "MESSAGING_API",
  "type": "UPLOAD",
  "description": "audienceGroupName_01",
  "created": 1613700237,
  "permission": "READ_WRITE",
  "expireTimestamp": 1629252237,
  "isIfaAudience": false
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>`file`プロパティに指定したファイルに、無効なユーザーIDまたはIFAが入力されている。</li><li>`file`プロパティに最大件数（1,500,000件）より多いユーザーIDまたはIFAを入力したファイルが指定されている。</li><li>`file`プロパティに指定したファイルに、有効なユーザーIDまたはIFAが指定されていない。</li><li>作成できるオーディエンス数の上限（合計1,000件）に達している。</li><li>`description`プロパティに最大文字数（120文字）より長い名前が指定されている。</li><li>`description`プロパティに無効な文字（例：`\n`などの制御コード）が指定されている。</li><li>`description`プロパティが空であるか、空白文字のみが指定されている。</li><li>`uploadDescription`プロパティに最大文字数（300文字）より長い文字列が指定されている。</li></ul> |
| `415` | `file`プロパティに、サポートされていないメディア形式のファイルが指定されている。 |
| `429` | 同時処理数の上限を超えています。詳しくは、「[同時処理数の制限](https://developers.line.biz/ja/reference/messaging-api/#limit-on-the-number-of-concurrent-operations)」を参照してください。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// descriptionプロパティに最大文字数（120文字）より長い名前を指定した場合（400 Bad Request）
{
  "message": "size over audienceGroupName",
  "details": [
    {
      "message": "AUDIENCE_GROUP_NAME_SIZE_OVER"
    }
  ]
}
```

<!-- tab end -->

### ユーザーIDアップロード用のオーディエンスにユーザーIDまたはIFAを追加する（JSON指定） 

Endpoint: `PUT` `https://api.line.me/v2/bot/audienceGroup/upload`

ユーザーIDアップロード用のオーディエンスに、ユーザーIDまたはIFAを追加します。

このエンドポイントでは、送信対象アカウントをJSONで指定します。[送信対象アカウントをテキストファイルで指定するエンドポイント](https://developers.line.biz/ja/reference/messaging-api/#update-upload-audience-group-by-file)も利用できます。

#### オーディエンスに追加できるユーザーの条件 

ユーザーIDアップロード用のオーディエンスには、LINE公式アカウントと友だちになっているユーザーを追加できます。ただし、以下のユーザーをオーディエンスに追加した場合も、ステータスコード`202`が返され、オーディエンスに追加されます。

- LINEアカウントを削除したユーザー
- オーディエンスを作成したLINE公式アカウントをブロックしているユーザー
- オーディエンスを作成したLINE公式アカウントを友だち追加していないユーザー

なお、作成したオーディエンスを使ってメッセージを送信した場合、上記のユーザーにはメッセージは送信されません。

<!-- note start -->

**同時処理数の制限があります**

ユーザーIDアップロード用のオーディエンス作成およびオーディエンスへのユーザーID追加のエンドポイントでは、オーディエンスID（`audienceGroupId`）単位での同時処理数の制限があります。詳しくは、「[同時処理数の制限](https://developers.line.biz/ja/reference/messaging-api/#limit-on-the-number-of-concurrent-operations)」を参照してください。

<!-- note end -->

<!-- note start -->

**リクエストタイムアウト値について**

リクエストタイムアウトを30秒以上に設定することを強く推奨します。

<!-- note end -->

<!-- note start -->

**有効なユーザーIDの確認方法**

JSONの`audiences`プロパティで無効なユーザーIDが指定されていた場合、エラーレスポンス（`details[].message`: `UPLOAD_AUDIENCE_GROUP_INVALID_AUDIENCE_ID_FORMAT`）が返り、ユーザーIDの追加に失敗します。このエンドポイントを実行する前に、`audiences`プロパティに含まれるすべてのユーザーIDが有効であることを確認してください。

ユーザーIDが有効か確認するには、[プロフィール情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-profile)エンドポイントを使用してください。ユーザーIDが有効な場合は、HTTPステータスコード`200`が返ります。`200`以外が返ってきた場合、そのユーザーIDは無効のため、`audiences`プロパティには含めないようにしてください。

<!-- note end -->

<!-- note start -->

**ユーザーIDまたはIFAの種類は変更できません**

ユーザーIDアップロード用のオーディエンスを作成したときと同じ種類（ユーザーIDまたはIFA）のデータを追加してください。たとえば、初めにIFAを指定して作成したオーディエンスに、ユーザーIDを指定することはできません。

オーディエンスを作成したときに指定した送信対象アカウントの種類（ユーザーIDまたはIFA）は、オーディエンスの`isIfaAudience`プロパティで確認できます。詳しくは、「[オーディエンスの情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-audience-group)」を参照してください。

<!-- note end -->

<!-- note start -->

**ユーザーIDまたはIFAは削除できません**

一度追加したユーザーIDまたはIFAを削除することはできません。

<!-- note end -->

<!-- note start -->

**LINEのプライバシーポリシー（2022年3月改定以降のもの）に同意済みのユーザーのみが対象となります**

ユーザーIDアップロード用のオーディエンスにユーザーIDを追加する際に、LINEのプライバシーポリシー（2022年3月改定以降のもの）に同意していないユーザーのユーザーIDが含まれている場合、未同意のユーザーは無視され同意済みのユーザーのみが追加されます。

そのため、指定したユーザーIDの数よりもオーディエンスの有効な送信対象アカウントの数が少なくなることがあります。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X PUT https://api.line.me/v2/bot/audienceGroup/upload \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d '{
    "audienceGroupId": 4389303728991,
    "uploadDescription": "fileName",
    "audiences": [
        {
            "id": "U4af4980627..."
        },
        {
            "id": "U4af4980628..."
        }
    ]
}'
```

<!-- tab end -->

#### レート制限 

60リクエスト/分

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

`application/json`

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

audienceGroupId

Number

オーディエンスID

<!-- parameter end -->
<!-- parameter start (props: optional) -->

uploadDescription

String

ジョブ（`jobs[].description`）に登録する説明\
最大文字数：300

<!-- parameter end -->
<!-- parameter start (props: required) -->

audiences

Array

ユーザーIDまたはIFAの配列\
最大件数：10,000

<!-- parameter end -->
<!-- parameter start (props: required) -->

audiences\[].id

String

ユーザーIDまたはIFA

<!-- parameter end -->

#### レスポンス 

HTTPステータスコード`202`と空のJSONオブジェクトを返します。

<!-- note start -->

**オーディエンスの作成は非同期に行われます**

オーディエンスを利用する前に、[オーディエンスが配信に利用できることを確認](https://developers.line.biz/ja/docs/messaging-api/sending-messages/#get-audience-status)してください。

<!-- note end -->

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
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>`audiences[].id`プロパティに、無効なユーザーIDまたはIFAが指定されている。</li><li>`audiences`プロパティに最大件数（10,000件）より多いユーザーIDまたはIFAが指定されている。</li><li>`audiences[].id`プロパティに、有効なユーザーIDまたはIFAが指定されていない。</li><li>保存期間を超えたオーディエンスが指定されている。</li><li>存在しないオーディエンスが指定されている。</li><li>`uploadDescription`プロパティに最大文字数（300文字）より長い文字列が指定されている。</li></ul> |
| `429` | 同時処理数の上限を超えています。詳しくは、「[同時処理数の制限](https://developers.line.biz/ja/reference/messaging-api/#limit-on-the-number-of-concurrent-operations)」を参照してください。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// audiences[].idプロパティに、無効なユーザーIDを指定した場合（400 Bad Request）
{
  "message": "Invalid audience id format",
  "details": [
    {
      "message": "UPLOAD_AUDIENCE_GROUP_INVALID_AUDIENCE_ID_FORMAT",
      "property": "audiences"
    }
  ]
}
```

<!-- tab end -->

### ユーザーIDアップロード用のオーディエンスにユーザーIDまたはIFAを追加する（ファイル指定） 

Endpoint: `PUT` `https://api-data.line.me/v2/bot/audienceGroup/upload/byFile`

<!-- note start -->

**他のエンドポイントとドメイン名が異なります**

このエンドポイントは、Messaging APIにおけるLINEプラットフォームへの大容量データ送受信用のドメイン名（`api-data.line.me`）です。他のエンドポイントのドメイン名（`api.line.me`）とは異なるため、利用時は注意してください。

<!-- note end -->

ユーザーIDアップロード用のオーディエンスに、ユーザーIDまたはIFAを追加します。

このエンドポイントでは、送信対象アカウントをテキストファイルで指定します。[送信対象アカウントをJSONで指定するエンドポイント](https://developers.line.biz/ja/reference/messaging-api/#update-upload-audience-group)も利用できます。

#### オーディエンスに追加できるユーザーの条件 

ユーザーIDアップロード用のオーディエンスには、LINE公式アカウントと友だちになっているユーザーを追加できます。ただし、以下のユーザーをオーディエンスに追加した場合も、ステータスコード`202`が返され、オーディエンスに追加されます。

- LINEアカウントを削除したユーザー
- オーディエンスを作成したLINE公式アカウントをブロックしているユーザー
- オーディエンスを作成したLINE公式アカウントを友だち追加していないユーザー

なお、作成したオーディエンスを使ってメッセージを送信した場合、上記のユーザーにはメッセージは送信されません。

<!-- note start -->

**同時処理数の制限があります**

ユーザーIDアップロード用のオーディエンス作成およびオーディエンスへのユーザーID追加のエンドポイントでは、オーディエンスID（`audienceGroupId`）単位での同時処理数の制限があります。詳しくは、「[同時処理数の制限](https://developers.line.biz/ja/reference/messaging-api/#limit-on-the-number-of-concurrent-operations)」を参照してください。

<!-- note end -->

<!-- note start -->

**リクエストタイムアウト値について**

リクエストタイムアウトを30秒以上に設定することを強く推奨します。

<!-- note end -->

<!-- note start -->

**ユーザーIDまたはIFAの種類は変更できません**

ユーザーIDアップロード用のオーディエンスを作成したときと同じ種類（ユーザーIDまたはIFA）のデータを追加してください。たとえば、初めにIFAを指定して作成したオーディエンスに、ユーザーIDを指定することはできません。

オーディエンスを作成したときに指定した送信対象アカウントの種類（ユーザーIDまたはIFA）は、オーディエンスの`isIfaAudience`プロパティで確認できます。詳しくは、「[オーディエンスの情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-audience-group)」を参照してください。

<!-- note end -->

<!-- note start -->

**ユーザーIDまたはIFAは削除できません**

一度追加したユーザーIDまたはIFAを削除することはできません。

<!-- note end -->

<!-- note start -->

**LINEのプライバシーポリシー（2022年3月改定以降のもの）に同意済みのユーザーのみが対象となります**

ユーザーIDアップロード用のオーディエンスにユーザーIDを追加する際に、LINEのプライバシーポリシー（2022年3月改定以降のもの）に同意していないユーザーのユーザーIDが含まれている場合、未同意のユーザーは無視され同意済みのユーザーのみが追加されます。

そのため、指定したユーザーIDの数よりもオーディエンスの有効な送信対象アカウントの数が少なくなることがあります。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X PUT https://api-data.line.me/v2/bot/audienceGroup/upload/byFile \
-H 'Authorization: Bearer {channel access token}' \
-F 'audienceGroupId=4389303728991' \
-F 'uploadDescription=fileName' \
-F 'file=@audiences.txt;type=text/plain'
```

<!-- tab end -->

_テキストファイルの例_

<!-- tab start `File` -->

```sh
U4af4980627...
U4af4980628...
U4af4980629...
```

<!-- tab end -->

#### レート制限 

60リクエスト/分

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

`multipart/form-data`

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

audienceGroupId

Number

オーディエンスID

<!-- parameter end -->
<!-- parameter start (props: optional) -->

uploadDescription

String

ジョブ（`jobs[].description`）に登録する説明\
最大文字数：300

<!-- parameter end -->
<!-- parameter start (props: required) -->

file

File

ユーザーIDまたはIFAを、1行に1件入力したテキストファイル。Content-Typeは、`text/plain`を指定してください。\
最大ファイル数：1\
最大行数：1,500,000

<!-- parameter end -->

#### レスポンス 

HTTPステータスコード`202`と空のJSONオブジェクトを返します。

<!-- note start -->

**オーディエンスの作成は非同期に行われます**

オーディエンスを利用する前に、[オーディエンスが配信に利用できることを確認](https://developers.line.biz/ja/docs/messaging-api/sending-messages/#get-audience-status)してください。

<!-- note end -->

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
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>`file`プロパティに指定したファイルに、無効なユーザーIDまたはIFAが入力されている。</li><li>`file`プロパティに最大件数（1,500,000件）より多いユーザーIDまたはIFAを入力したファイルが指定されている。</li><li>`file`プロパティに指定したファイルに、有効なユーザーIDまたはIFAが指定されていない。</li><li>保存期間を超えたオーディエンスが指定されている。</li><li>存在しないオーディエンスが指定されている。</li><li>`uploadDescription`プロパティに最大文字数（300文字）より長い文字列が指定されている。</li></ul> |
| `415` | `file`プロパティに、サポートされていないメディア形式のファイルが指定されている。 |
| `429` | 同時処理数の上限を超えています。詳しくは、「[同時処理数の制限](https://developers.line.biz/ja/reference/messaging-api/#limit-on-the-number-of-concurrent-operations)」を参照してください。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// fileプロパティに無効なユーザーIDが入力されているファイルを指定した場合（400 Bad Request）
{
  "message": "UPLOAD_AUDIENCE_GROUP_INVALID_AUDIENCE_ID_FORMAT",
  "details": [
    {
      "message": "UPLOAD_AUDIENCE_GROUP_INVALID_AUDIENCE_ID_FORMAT",
      "property": "file"
    }
  ]
}
```

<!-- tab end -->

### メッセージクリックオーディエンスを作成する 

Endpoint: `POST` `https://api.line.me/v2/bot/audienceGroup/click`

メッセージクリックオーディエンスを作成します。

メッセージクリックオーディエンスは、ブロードキャストメッセージまたはナローキャストメッセージに記載されたURLをクリックしたユーザーを集めたオーディエンスです。少なくとも1つのリンクをクリックしたユーザーが送信対象になります。

対象のメッセージは、リクエストIDで指定します。

<!-- tip start -->

**メッセージクリックオーディエンスの仕様**

オーディエンスの仕様は以下のとおりです。

| 項目 | 条件 |
| --- | --- |
| チャネルあたりのオーディエンス数 | 最大1,000件 |
| オーディエンスの保存期間 | 最大180日間（15,552,000秒間） |
| オーディエンスあたりのユーザー数 | メッセージクリックオーディエンス：最小50件 |
| メッセージを配信してからリターゲティング用オーディエンス（※）を作成できる期間  |  最大60日間（5,184,000秒間） |

※メッセージクリックオーディエンスおよびメッセージインプレッションオーディエンスを指します。

ナローキャストメッセージの使用制限については、「[属性情報やオーディエンスを利用したメッセージ送信の制限事項](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message-restrictions)」を参照してください。

<!-- tip end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/audienceGroup/click \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d '{
    "description": "audienceGroupName_01",
    "requestId": "bb9744f9-47fa-4a29-941e-1234567890ab",
    "clickUrl": "https://developers.line.biz/"
}'
```

<!-- tab end -->

#### レート制限 

60リクエスト/分

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

`application/json`

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

description

String

オーディエンスの名前。なお、大文字と小文字は区別されないため、`AUDIENCE`と`audience`は同じ名前と判定されます。\
最大文字数：120

<!-- parameter end -->
<!-- parameter start (props: required) -->

requestId

String

配信から60日以内のブロードキャストメッセージまたはナローキャストメッセージのリクエストID。リクエストIDは、Messaging APIのリクエストごとに発行されるIDです。[レスポンスヘッダー](https://developers.line.biz/ja/reference/messaging-api/#response-headers)に含まれます。

<!-- note start -->

**注意**

応答メッセージ、プッシュメッセージ、およびマルチキャストメッセージのリクエストIDは、利用できません。

<!-- note end -->

<!-- parameter end -->
<!-- parameter start (props: optional) -->

clickUrl

String

ユーザーがクリックしたURL。省略した場合は、メッセージ内の任意のURLをクリックしたユーザーが送信対象になります。\
最大文字数：2,000

<!-- parameter end -->

#### レスポンス 

ステータスコード`202`と以下の情報を含むJSONオブジェクトを返します。

<!-- note start -->

**オーディエンスの作成は非同期に行われます**

オーディエンスを利用する前に、[オーディエンスが配信に利用できることを確認](https://developers.line.biz/ja/docs/messaging-api/sending-messages/#get-audience-status)してください。

<!-- note end -->

<!-- parameter start -->

audienceGroupId

Number

オーディエンスID

<!-- parameter end -->
<!-- parameter start -->

createRoute

String

オーディエンスの作成方法。

- `MESSAGING_API`：Messaging APIで作成したオーディエンス

<!-- parameter end -->
<!-- parameter start -->

type

String

オーディエンスのタイプ。

- `CLICK`：メッセージクリックオーディエンス

<!-- parameter end -->
<!-- parameter start -->

description

String

オーディエンスの名前

<!-- parameter end -->
<!-- parameter start -->

created

Number

オーディエンスが作成された時刻。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

permission

String

作成したオーディエンスに対する更新権限。

- `READ_WRITE`：オーディエンスを利用、更新できます。

<!-- parameter end -->
<!-- parameter start -->

expireTimestamp

Number

オーディエンスの有効期限。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

isIfaAudience

Boolean

ユーザーIDアップロード用のオーディエンスを作成したときに指定した、送信対象アカウントの種類を示す値。以下のいずれかの値です。

- `true`：IFAで指定する
- `false`：ユーザーIDで指定する（デフォルト）

<!-- parameter end -->
<!-- parameter start -->

requestId

String

オーディエンスを作成したときに指定したリクエストID

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

clickUrl

String

オーディエンスを作成したときに指定したURL。リクエスト時に`clickUrl`プロパティに値を指定した場合にのみ含まれます。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "audienceGroupId": 1234567890123,
  "createRoute": "MESSAGING_API",
  "type": "CLICK",
  "description": "audienceGroupName_01",
  "created": 1613705240,
  "permission": "READ_WRITE",
  "expireTimestamp": 1629257239,
  "isIfaAudience": false,
  "requestId": "bb9744f9-47fa-4a29-941e-1234567890ab",
  "clickUrl": "https://developers.line.biz/"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>作成できるオーディエンス数の上限（合計1,000件）に達している。</li><li>`description`プロパティに最大文字数（120文字）より長い名前が指定されている。</li><li>`description`プロパティに無効な文字（例：`\n`などの制御コード）が指定されている。</li><li>`requestID`プロパティと`clickUrl`プロパティに既存のオーディエンスと同じ組み合わせの値が指定されている。</li><li>オーディエンスを作成できる期間を超えている。</li><li>存在しないリクエストIDが指定されている。</li><li>指定したリクエストIDでオーディエンスを作成する準備ができていない。</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// descriptionプロパティに最大文字数（120文字）より長い名前を指定した場合（400 Bad Request）
{
  "message": "size over audienceGroupName",
  "details": [
    {
      "message": "AUDIENCE_GROUP_NAME_SIZE_OVER"
    }
  ]
}
```

<!-- tab end -->

### メッセージインプレッションオーディエンスを作成する 

Endpoint: `POST` `https://api.line.me/v2/bot/audienceGroup/imp`

メッセージインプレッションオーディエンスを作成します。

メッセージインプレッションオーディエンスは、ブロードキャストメッセージまたはナローキャストメッセージを表示したユーザーを集めたオーディエンスです。少なくとも1つの吹き出しを表示したユーザーが送信対象になります。

対象のメッセージは、リクエストIDで指定します。

<!-- tip start -->

**メッセージインプレッションオーディエンスの仕様**

オーディエンスの仕様は以下のとおりです。

| 項目 | 条件 |
| --- | --- |
| チャネルあたりのオーディエンス数 | 最大1,000件 |
| オーディエンスの保存期間 | 最大180日間（15,552,000秒） |
| オーディエンスあたりのユーザー数 | メッセージインプレッションオーディエンス：最小50件 |
| メッセージを配信してからリターゲティング用オーディエンス（※）を作成できる期間  |  最大60日間（5,184,000秒間） |

※メッセージクリックオーディエンスおよびメッセージインプレッションオーディエンスを指します。

ナローキャストメッセージの使用制限については、「[属性情報やオーディエンスを利用したメッセージ送信の制限事項](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message-restrictions)」を参照してください。

<!-- tip end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/audienceGroup/imp \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d '{
    "description": "audienceGroupName_01",
    "requestId": "bb9744f9-47fa-4a29-941e-1234567890ab"
}'
```

<!-- tab end -->

#### レート制限 

60リクエスト/分

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

`application/json`

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

description

String

オーディエンスの名前。なお、大文字と小文字は区別されないため、`AUDIENCE`と`audience`は同じ名前と判定されます。\
最大文字数：120

<!-- parameter end -->
<!-- parameter start (props: required) -->

requestId

String

配信から60日以内のブロードキャストメッセージまたはナローキャストメッセージのリクエストID。リクエストIDは、Messaging APIのリクエストごとに発行されるIDです。[レスポンスヘッダー](https://developers.line.biz/ja/reference/messaging-api/#response-headers)に含まれます。

<!-- parameter end -->

#### レスポンス 

ステータスコード`202`と以下の情報を含むJSONオブジェクトを返します。

<!-- note start -->

**オーディエンスの作成は非同期に行われます**

オーディエンスを利用する前に、[オーディエンスが配信に利用できることを確認](https://developers.line.biz/ja/docs/messaging-api/sending-messages/#get-audience-status)してください。

<!-- note end -->

<!-- parameter start -->

audienceGroupId

Number

オーディエンスID

<!-- parameter end -->
<!-- parameter start -->

createRoute

String

オーディエンスの作成方法。

- `MESSAGING_API`：Messaging APIで作成したオーディエンス

<!-- parameter end -->
<!-- parameter start -->

type

String

オーディエンスのタイプ。

- `IMP`：メッセージインプレッションオーディエンス

<!-- parameter end -->
<!-- parameter start -->

description

String

オーディエンスの名前

<!-- parameter end -->
<!-- parameter start -->

created

Number

オーディエンスが作成された時刻。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

permission

String

作成したオーディエンスに対する更新権限。

- `READ_WRITE`：オーディエンスを利用、更新できます。

<!-- parameter end -->
<!-- parameter start -->

expireTimestamp

Number

オーディエンスの有効期限。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

isIfaAudience

Boolean

ユーザーIDアップロード用のオーディエンスを作成したときに指定した、送信対象アカウントの種類を示す値。以下のいずれかの値です。

- `true`：IFAで指定する
- `false`：ユーザーIDで指定する（デフォルト）

<!-- parameter end -->
<!-- parameter start -->

requestId

String

オーディエンスを作成したときに指定したリクエストID

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "audienceGroupId": 1234567890123,
  "createRoute": "MESSAGING_API",
  "type": "IMP",
  "description": "audienceGroupName_01",
  "created": 1613707097,
  "permission": "READ_WRITE",
  "expireTimestamp": 1629259095,
  "isIfaAudience": false,
  "requestId": "bb9744f9-47fa-4a29-941e-1234567890ab"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>作成できるオーディエンス数の上限（合計1,000件）に達している。</li><li>`description`プロパティに最大文字数（120文字）より長い名前が指定されている。</li><li>`description`プロパティに無効な文字（例：`\n`などの制御コード）が指定されている。</li><li>既存のオーディエンスに指定したリクエストIDと同じ値が指定されている。</li><li>オーディエンスを作成できる期間を超えている。</li><li>存在しないリクエストIDが指定されている。</li><li>指定したリクエストIDでオーディエンスを作成する準備ができていない。</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// descriptionプロパティに最大文字数（120文字）より長い名前を指定した場合（400 Bad Request）
{
  "message": "size over audienceGroupName",
  "details": [
    {
      "message": "AUDIENCE_GROUP_NAME_SIZE_OVER"
    }
  ]
}
```

<!-- tab end -->

### オーディエンスの名前を更新する 

Endpoint: `PUT` `https://api.line.me/v2/bot/audienceGroup/{audienceGroupId}/updateDescription`

既存のオーディエンスの名前を変更します。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X PUT https://api.line.me/v2/bot/audienceGroup/{audienceGroupId}/updateDescription \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d '{
    "description": "audienceGroupName"
}'
```

<!-- tab end -->

#### レート制限 

60リクエスト/分

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

`application/json`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

audienceGroupId

オーディエンスID

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

description

String

オーディエンスの名前。なお、大文字と小文字は区別されないため、`AUDIENCE`と`audience`は同じ名前と判定されます。\
最大文字数：120

<!-- parameter end -->

#### レスポンス 

HTTPステータスコード`200`と空のJSONオブジェクトを返します。

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>`description`プロパティに最大文字数（120文字）より長い名前が指定されている。</li><li>`description`プロパティに無効な文字（例：`\n`などの制御コード）が指定されている。</li><li>存在しないオーディエンスが指定されている。</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// descriptionプロパティに最大文字数（120文字）より長い名前を指定した場合（400 Bad Request）
{
  "message": "size over audienceGroupName",
  "details": [
    {
      "message": "AUDIENCE_GROUP_NAME_SIZE_OVER"
    }
  ]
}
```

<!-- tab end -->

### オーディエンスを削除する 

Endpoint: `DELETE` `https://api.line.me/v2/bot/audienceGroup/{audienceGroupId}`

オーディエンスを削除します。

<!-- warning start -->

**削除したオーディエンスは元に戻せません**

削除する前に、オーディエンスが使用されていないことを確認してください。

<!-- warning end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X DELETE https://api.line.me/v2/bot/audienceGroup/{audienceGroupId} \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

60リクエスト/分

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

audienceGroupId

オーディエンスID

<!-- parameter end -->

#### レスポンス 

HTTPステータスコード`202`と空のJSONオブジェクトを返します。

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明                                         |
| ------ | -------------------------------------------- |
| `400`  | 存在しないオーディエンスが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 存在しないオーディエンスを指定した場合（400 Bad Request）
{
  "message": "audience group not found",
  "details": [
    {
      "message": "AUDIENCE_GROUP_NOT_FOUND"
    }
  ]
}
```

<!-- tab end -->

### オーディエンスの情報を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/audienceGroup/{audienceGroupId}`

オーディエンスの情報を取得します。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/audienceGroup/{audienceGroupId} \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

60リクエスト/分

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

audienceGroupId

オーディエンスID

<!-- parameter end -->

#### レスポンス 

HTTPステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

audienceGroup

Object

オーディエンスグループオブジェクト

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.audienceGroupId

Number

オーディエンスID

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.createRoute

String

オーディエンスの作成方法。以下のいずれかの値です。

- `OA_MANAGER`：[LINE Official Account Manager](https://manager.line.biz/)で作成したオーディエンス
- `MESSAGING_API`：Messaging APIで作成したオーディエンス
- `POINT_AD`：[LINEポイントAD](https://www.lycbiz.com/jp/service/line-point-ad/)で作成したオーディエンス
- `AD_MANAGER`：[LINE広告](https://admanager.line.biz/)で作成したオーディエンス

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.type

String

オーディエンスのタイプ。以下のいずれかの値です。

- `UPLOAD`：ユーザーIDアップロード用のオーディエンス
- `CLICK`：メッセージクリックオーディエンス
- `IMP`：メッセージインプレッションオーディエンス
- `CHAT_TAG`：チャットタグオーディエンス
- `FRIEND_PATH`：追加経路オーディエンス
- `RESERVATION`：予約オーディエンス
- `RICHMENU_IMP`：リッチメニューインプレッションオーディエンス
- `RICHMENU_CLICK`：リッチメニュークリックオーディエンス
- `APP_EVENT`：アプリイベントオーディエンス
- `VIDEO_VIEW`：動画視聴オーディエンス
- `WEBTRAFFIC`：ウェブトラフィックオーディエンス（LINE Tag）
- `TRACKINGTAG_WEBTRAFFIC`：ウェブトラフィックオーディエンス（計測タグ）
- `IMAGE_CLICK`：画像クリックオーディエンス
- `POP_AD_IMP`：LINE Beacon Networkインプレッションオーディエンス

詳しくは、『LINEヤフー for Business』の「[オーディエンス](https://www.lycbiz.com/jp/manual/OfficialAccountManager/messages-audience/)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.description

String

オーディエンスの名前

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.status

String

オーディエンスのステータス。以下のいずれかの値です。

- `IN_PROGRESS`：準備中。`READY`になるまで数時間かかる場合があります。ユーザー数の規定があるオーディエンスにおいて、オーディエンスに含まれるユーザーの数（最低50件）が不足している場合、ステータスは`IN_PROGRESS`のまま更新されません。
- `READY`：配信に利用可能。
- `FAILED`：作成時にエラーが発生。
- `EXPIRED`：有効期限切れ。有効期限切れ後、1か月後に自動で削除されます。
- `INACTIVE`：オーディエンスが無効です。
- `ACTIVATING`：オーディエンスを有効化しています。

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.audienceCount

Number

オーディエンスに含まれるユーザーの数。ユーザーのプライバシーを保護するため、有効な送信対象アカウントの数が20未満の場合は0が返ります。ただし、オーディエンスのタイプが以下の場合を除きます。

- ユーザーIDアップロード用のオーディエンス（送信対象アカウントをユーザーIDで指定する場合）
- チャットタグオーディエンス

オーディエンスには、既にLINE公式アカウントをブロックしたユーザーも含まれる可能性があるため、`audienceGroup.audienceCount`の値と、メッセージの送信対象となるユーザーの数は異なります。

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.created

Number

オーディエンスが作成された時刻。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.permission

String

オーディエンスに対する更新権限。現在のMessaging APIチャネルが、対象のオーディエンスを更新できる場合は`READ_WRITE`、更新できない場合は`READ`が返ります。

- `READ`：オーディエンスを利用できますが、更新はできません。
- `READ_WRITE`：オーディエンスを利用、更新できます。

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.isIfaAudience

Boolean

ユーザーIDアップロード用のオーディエンスを作成したときに指定した、送信対象アカウントの種類を示す値。以下のいずれかの値です。

- `true`：IFAで指定する
- `false`：ユーザーIDで指定する（デフォルト）

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroup.requestId

String

オーディエンスを作成したときに指定したリクエストID。`audienceGroup.type`が`CLICK`または`IMP`の場合にのみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroup.clickUrl

String

オーディエンスを作成したときに指定したURL。`audienceGroup.type`が`CLICK`で、リンク先URLが指定されている場合にのみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroup.failedType

String

失敗した原因。`audienceGroup.status`が`FAILED`の場合にのみ含まれます。以下のいずれかの値です。

- `AUDIENCE_GROUP_AUDIENCE_INSUFFICIENT`：オーディエンスに含まれるユーザーの数（最低50件）が不足しています。
- `INTERNAL_ERROR`：内部サーバーのエラーです。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroup.activated

Number

オーディエンスが有効化した時間。[LINE広告](https://admanager.line.biz/)や[LINEポイントAD](https://www.lycbiz.com/jp/service/line-point-ad/)で作成したオーディエンスの場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroup.inactivatedTimestamp

Number

オーディエンスが無効化した時間。[LINE広告](https://admanager.line.biz/)や[LINEポイントAD](https://www.lycbiz.com/jp/service/line-point-ad/)で作成したオーディエンスの場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroup.expireTimestamp

Number

オーディエンスの有効期限。UNIX時間（秒）で返されます。特定のオーディエンスの場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start -->

jobs

Array

ジョブの配列。ユーザーIDアップロード用のオーディエンスに、ユーザーIDまたはIFAを追加した最新履歴を管理する配列です。それ以外のオーディエンスの場合は空配列が返ります。<br />最大件数：50

<!-- parameter end -->
<!-- parameter start -->

jobs\[].audienceGroupJobId

Number

ジョブID

<!-- parameter end -->
<!-- parameter start -->

jobs\[].audienceGroupId

Number

オーディエンスID

<!-- parameter end -->
<!-- parameter start -->

jobs\[].description

String

ジョブの説明。ユーザーIDまたはIFAを追加する際に`uploadDescription`プロパティに値を指定しなかった場合は`null`が返されます。

<!-- parameter end -->
<!-- parameter start -->

jobs\[].type

String

ジョブの種類。以下のいずれかの値です。

- `DIFF_ADD`：Messaging APIでユーザーIDまたはIFAを追加したことを示します。

<!-- parameter end -->
<!-- parameter start -->

jobs\[].status

String

このプロパティの利用は非推奨です。ジョブのステータスは`jobs[].jobStatus`を参照してください。

<!-- parameter end -->
<!-- parameter start -->

jobs\[].failedType

String

失敗した原因。`jobs[].jobStatus`が`FAILED`の場合にのみ含まれます。以下のいずれかの値です。

- `AUDIENCE_GROUP_AUDIENCE_INSUFFICIENT`：オーディエンスに含まれるユーザーの数（最低50件）が不足しています。
- `INTERNAL_ERROR`：内部サーバーのエラーです。

`jobs[].jobStatus`が`FAILED`以外の場合は`null`が返されます。

<!-- parameter end -->
<!-- parameter start -->

jobs\[].audienceCount

Number

追加または削除された送信対象アカウントの数

<!-- parameter end -->
<!-- parameter start -->

jobs\[].created

Number

ジョブが作成された時刻。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

jobs\[].jobStatus

String

ジョブのステータス。以下のいずれかの値です。

- `QUEUED`：待機中
- `WORKING`：実行中
- `FINISHED`：成功
- `FAILED`：失敗

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

adaccount

Object

広告アカウントオブジェクト。[LINE広告](https://admanager.line.biz/)や[LINEポイントAD](https://www.lycbiz.com/jp/service/line-point-ad/)で作成したオーディエンスの場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start -->

adaccount\[].name

String

オーディエンスグループを作成した広告アカウント名

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
// ユーザーIDアップロード用のオーディエンスの例
{
    "audienceGroup": {
        "audienceGroupId": 1234567890123,
        "createRoute": "OA_MANAGER",
        "type": "UPLOAD",
        "description": "audienceGroupName_01",
        "status": "READY",
        "audienceCount": 1887,
        "created": 1608617466,
        "permission": "READ",
        "isIfaAudience": false,
        "expireTimestamp": 1624342266
    },
    "jobs": [
        {
            "audienceGroupJobId": 12345678,
            "audienceGroupId": 1234567890123,
            "description": "audience_list.txt",
            "type": "DIFF_ADD",
            "status": "FINISHED",
            "failedType": null,
            "audienceCount": 0,
            "created": 1608617472,
            "jobStatus": "FINISHED"
        }
    ]
}

// メッセージクリックオーディエンスの例
{
    "audienceGroup": {
        "audienceGroupId": 1234567890987,
        "createRoute": "OA_MANAGER",
        "type": "CLICK",
        "description": "audienceGroupName_02",
        "status": "IN_PROGRESS",
        "audienceCount": 8619,
        "created": 1611114828,
        "permission": "READ",
        "isIfaAudience": false,
        "expireTimestamp": 1626753228,
        "requestId": "c10c3d86-f565-...",
        "clickUrl": "https://example.com/"
    },
    "jobs": []
}

// アプリイベント用のオーディエンスの例
{
    "audienceGroup": {
        "audienceGroupId": 2345678909876,
        "createRoute": "AD_MANAGER",
        "type": "APP_EVENT",
        "description": "audienceGroupName_03",
        "status": "READY",
        "audienceCount": 8619,
        "created": 1608619802,
        "permission": "READ",
        "activated": 1610068515,
        "inactiveTimestamp": 1625620516,
        "isIfaAudience": false
    },
    "jobs": [],
    "adaccount": {
        "name": "Ad Account Name"
    }
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明                                         |
| ------ | -------------------------------------------- |
| `400`  | 存在しないオーディエンスが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 存在しないオーディエンスを指定した場合（400 Bad Request）
{
  "message": "audience group not found",
  "details": [
    {
      "message": "AUDIENCE_GROUP_NOT_FOUND"
    }
  ]
}
```

<!-- tab end -->

### 複数のオーディエンスの情報を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/audienceGroup/list`

複数のオーディエンスの情報を取得します。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/audienceGroup/list \
--data-urlencode 'page=1' \
--data-urlencode 'description=audienceGroupName' \
--data-urlencode 'size=40' \
--data-urlencode 'createRoute=OA_MANAGER' \
-G \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

60リクエスト/分

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: required) -->

page

取得するページ番号。`1`以上を指定してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

description

取得するオーディエンスの名前。部分一致で検索できます。なお、大文字と小文字は区別されないため、`AUDIENCE`と`audience`は同じ名前と判定されます。省略した場合は、オーディエンスの名前を検索条件として使用しません。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

status

取得するオーディエンスのステータス。省略した場合は、オーディエンスのステータスを検索条件として使用しません。以下のいずれかの値です。

- `IN_PROGRESS`：準備中。
- `READY`：配信に利用可能。
- `FAILED`：作成時にエラーが発生。
- `EXPIRED`：有効期限切れ。有効期限切れ後、1か月後に自動で削除されます。
- `INACTIVE`：オーディエンスが無効です。
- `ACTIVATING`：オーディエンスを有効化しています。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

size

1ページごとのオーディエンス数。デフォルト値は`20`です。\
最大値：`40`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

includesExternalPublicGroups

- `true`：同じボットに関連付けられた、すべてのチャネルで作成された公開オーディエンスを取得（デフォルト）
- `false`：同じチャネルに作成されたオーディエンスのみを取得

<!-- parameter end -->
<!-- parameter start (props: optional) -->

createRoute

オーディエンスの作成方法。省略した場合は、すべてのオーディエンスを取得します。

- `OA_MANAGER`：[LINE Official Account Manager](https://manager.line.biz/)で作成したオーディエンスのみを取得
- `MESSAGING_API`：Messaging APIで作成したオーディエンスのみを取得
- `POINT_AD`：[LINEポイントAD](https://www.lycbiz.com/jp/service/line-point-ad/)で作成したオーディエンスのみを取得
- `AD_MANAGER`：[LINE広告](https://admanager.line.biz/)で作成したオーディエンスのみを取得

複数のパラメータを指定した場合、OR条件となります。

<!-- parameter end -->

#### レスポンス 

HTTPステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

audienceGroups

Array

オーディエンスの情報の配列。指定した条件に該当するオーディエンスが存在しなかった場合は空配列が返ります。

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].audienceGroupId

Number

オーディエンスID

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].createRoute

String

オーディエンスの作成方法。以下のいずれかの値です。

- `OA_MANAGER`：[LINE Official Account Manager](https://manager.line.biz/)で作成したオーディエンス
- `MESSAGING_API`：Messaging APIで作成したオーディエンス
- `POINT_AD`：[LINEポイントAD](https://www.lycbiz.com/jp/service/line-point-ad/)で作成したオーディエンス
- `AD_MANAGER`：[LINE広告](https://admanager.line.biz/)で作成したオーディエンス

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].type

String

オーディエンスのタイプ。以下のいずれかの値です。

- `UPLOAD`：ユーザーIDアップロード用のオーディエンス
- `CLICK`：メッセージクリックオーディエンス
- `IMP`：メッセージインプレッションオーディエンス
- `CHAT_TAG`：チャットタグオーディエンス
- `FRIEND_PATH`：追加経路オーディエンス
- `RESERVATION`：予約オーディエンス
- `RICHMENU_IMP`：リッチメニューインプレッションオーディエンス
- `RICHMENU_CLICK`：リッチメニュークリックオーディエンス
- `APP_EVENT`：アプリイベントオーディエンス
- `VIDEO_VIEW`：動画視聴オーディエンス
- `WEBTRAFFIC`：ウェブトラフィックオーディエンス（LINE Tag）
- `TRACKINGTAG_WEBTRAFFIC`：ウェブトラフィックオーディエンス（計測タグ）
- `IMAGE_CLICK`：画像クリックオーディエンス
- `POP_AD_IMP`：LINE Beacon Networkインプレッションオーディエンス

詳しくは、『LINEヤフー for Business』の「[オーディエンス](https://www.lycbiz.com/jp/manual/OfficialAccountManager/messages-audience/)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].description

String

オーディエンスの名前

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].status

String

オーディエンスのステータス。以下のいずれかの値です。

- `IN_PROGRESS`：準備中。`READY`になるまで数時間かかる場合があります。ユーザー数の規定があるオーディエンスにおいて、オーディエンスに含まれるユーザーの数（最低50件）が不足している場合、ステータスは`IN_PROGRESS`のまま更新されません。
- `READY`：配信に利用可能。
- `FAILED`：作成時にエラーが発生。
- `EXPIRED`：有効期限切れ。有効期限切れ後、1か月後に自動で削除されます。
- `INACTIVE`：オーディエンスが無効です。
- `ACTIVATING`：オーディエンスを有効化しています。

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].audienceCount

Number

オーディエンスに含まれるユーザーの数。ユーザーのプライバシーを保護するため、有効な送信対象アカウントの数が20未満の場合は0が返ります。ただし、オーディエンスのタイプが以下の場合を除きます。

- ユーザーIDアップロード用のオーディエンス（送信対象アカウントをユーザーIDで指定する場合）
- チャットタグオーディエンス

オーディエンスには、既にLINE公式アカウントをブロックしたユーザーも含まれる可能性があるため、`audienceGroups[].audienceCount`の値と、メッセージの送信対象となるユーザーの数は異なります。

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].created

Number

オーディエンスが作成された時刻。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].permission

String

オーディエンスに対する更新権限。現在のMessaging APIチャネルが、対象のオーディエンスを更新できる場合は`READ_WRITE`、更新できない場合は`READ`が返ります。

- `READ`：オーディエンスを利用できますが、更新はできません。
- `READ_WRITE`：オーディエンスを利用、更新できます。

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].isIfaAudience

Boolean

ユーザーIDアップロード用のオーディエンスを作成したときに指定した、送信対象アカウントの種類を示す値。以下のいずれかの値です。

- `true`：IFAで指定する
- `false`：ユーザーIDで指定する（デフォルト）

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroups\[].activated

Number

オーディエンスが有効化した時間。[LINE広告](https://admanager.line.biz/)や[LINEポイントAD](https://www.lycbiz.com/jp/service/line-point-ad/)で作成したオーディエンスの場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroups\[].inactivatedTimestamp

Number

オーディエンスが無効化した時間。[LINE広告](https://admanager.line.biz/)や[LINEポイントAD](https://www.lycbiz.com/jp/service/line-point-ad/)で作成したオーディエンスの場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroups\[].expireTimestamp

Number

オーディエンスの有効期限。UNIX時間（秒）で返されます。特定のオーディエンスの場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroups\[].requestId

String

オーディエンスを作成したときに指定したリクエストID。`audienceGroups[].type`が`CLICK`または`IMP`の場合にのみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroups\[].clickUrl

String

オーディエンスを作成したときに指定したURL。`audienceGroups[].type`が`CLICK`で、リンク先URLが指定されている場合にのみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroups\[].failedType

String

失敗した原因。`audienceGroups[].status`が`FAILED`または`EXPIRED`の場合にのみ含まれます。以下のいずれかの値です。

- `AUDIENCE_GROUP_AUDIENCE_INSUFFICIENT`：オーディエンスに含まれるユーザーの数（最低50件）が不足しています。
- `INTERNAL_ERROR`：内部サーバーのエラーです。

<!-- parameter end -->
<!-- parameter start -->

hasNextPage

Boolean

次のページが存在する場合は、`true`

<!-- parameter end -->
<!-- parameter start -->

totalCount

Number

指定した条件で取得できるオーディエンスの総数

<!-- parameter end -->
<!-- parameter start -->

readWriteAudienceGroupTotalCount

Number

指定した条件で取得できるオーディエンスのうち、更新権限（`audienceGroups[].permission`）が`READ_WRITE`になっているオーディエンスの数

<!-- parameter end -->
<!-- parameter start -->

page

Number

現在のページ番号

<!-- parameter end -->
<!-- parameter start -->

size

Number

現在のページに含まれる最大のオーディエンス数

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
// 指定した条件に該当するオーディエンスが2件あった場合の例
{
    "audienceGroups": [
        {
            "audienceGroupId": 1234567890123,
            "createRoute": "OA_MANAGER",
            "type": "CLICK",
            "description": "audienceGroupName_01",
            "status": "IN_PROGRESS",
            "audienceCount": 8619,
            "created": 1611114828,
            "permission": "READ",
            "isIfaAudience": false,
            "expireTimestamp": 1626753228,
            "requestId": "c10c3d86-f565-...",
            "clickUrl": "https://example.com/"
        },
        {
            "audienceGroupId": 2345678901234,
            "createRoute": "AD_MANAGER",
            "type": "APP_EVENT",
            "description": "audienceGroupName_02",
            "status": "READY",
            "audienceCount": 3368,
            "created": 1608619802,
            "permission": "READ",
            "activated": 1610068515,
            "inactiveTimestamp": 1625620516,
            "isIfaAudience": false
        }
    ],
    "hasNextPage": false,
    "totalCount": 2,
    "readWriteAudienceGroupTotalCount": 0,
    "size": 40,
    "page": 1
}

// 指定した条件に該当するオーディエンスが存在しなかった場合の例
{
    "audienceGroups": [],
    "hasNextPage": false,
    "totalCount": 0,
    "readWriteAudienceGroupTotalCount": 0,
    "size": 40,
    "page": 1
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明                                           |
| ------ | ---------------------------------------------- |
| `400`  | クエリパラメータに無効な値が指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// クエリパラメータに無効な値を指定した場合（400 Bad Request）
{
  "message": "size: must be less than or equal to 40",
  "details": [
    {
      "message": "TOO_HIGH"
    }
  ]
}
```

<!-- tab end -->

### ビジネスマネージャーで共有されたオーディエンスの情報を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/audienceGroup/shared/{audienceGroupId}`

[ビジネスマネージャー](https://data.linebiz.com/solutions/business-manager)で共有されたオーディエンスの情報を取得します。

<!-- tip start -->

**ビジネスマネージャーについて**

ビジネスマネージャーを使うことで、特定のオーディエンスを複数のサービス間で共有できます。ビジネスマネージャーでオーディエンスを横断利用することで、エンドユーザーとのより良いコミュニケーションが実現できます。

詳しくは、『LINE DATA SOLUTION』の「[ビジネスマネージャー](https://data.linebiz.com/solutions/business-manager)」を参照してください。

<!-- tip end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/audienceGroup/shared/{audienceGroupId} \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

60リクエスト/分

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

audienceGroupId

情報を取得したいオーディエンスのオーディエンスID。

<!-- parameter end -->

#### レスポンス 

HTTPステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

audienceGroup

Object

オーディエンスグループオブジェクト

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.audienceGroupId

Number

オーディエンスID

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.createRoute

String

オーディエンスの作成方法。以下のいずれかの値です。

- `OA_MANAGER`：[LINE Official Account Manager](https://manager.line.biz/)で作成したオーディエンス
- `MESSAGING_API`：Messaging APIで作成したオーディエンス
- `POINT_AD`：[LINEポイントAD](https://www.lycbiz.com/jp/service/line-point-ad/)で作成したオーディエンス
- `AD_MANAGER`：[LINE広告](https://admanager.line.biz/)で作成したオーディエンス
- `BUSINESS_MANAGER`：[ビジネスマネージャー](https://data.linebiz.com/solutions/business-manager)で作成したオーディエンス
- `YAHOO_DISPLAY_ADS`：[LINEヤフー広告 ディスプレイ広告](https://www.lycbiz.com/jp/service/ly-ads/displayads-auc/)で作成したオーディエンス

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.type

String

オーディエンスのタイプ。以下のいずれかの値です。

- `UPLOAD`：ユーザーIDアップロード用のオーディエンス
- `CLICK`：メッセージクリックオーディエンス
- `IMP`：メッセージインプレッションオーディエンス
- `CHAT_TAG`：チャットタグオーディエンス
- `FRIEND_PATH`：追加経路オーディエンス
- `RESERVATION`：予約オーディエンス
- `RICHMENU_IMP`：リッチメニューインプレッションオーディエンス
- `RICHMENU_CLICK`：リッチメニュークリックオーディエンス
- `APP_EVENT`：アプリイベントオーディエンス
- `VIDEO_VIEW`：動画視聴オーディエンス
- `WEBTRAFFIC`：ウェブトラフィックオーディエンス（LINE Tag）
- `TRACKINGTAG_WEBTRAFFIC`：ウェブトラフィックオーディエンス（計測タグ）
- `IMAGE_CLICK`：画像クリックオーディエンス
- `POP_AD_IMP`：LINE Beacon Networkインプレッションオーディエンス

詳しくは、『LINEヤフー for Business』の「[オーディエンス](https://www.lycbiz.com/jp/manual/OfficialAccountManager/messages-audience/)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.description

String

オーディエンスの名前

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.status

String

オーディエンスのステータス。以下のいずれかの値です。

- `IN_PROGRESS`：準備中。`READY`になるまで数時間かかる場合があります。ユーザー数の規定があるオーディエンスにおいて、オーディエンスに含まれるユーザーの数（最低50件）が不足している場合、ステータスは`IN_PROGRESS`のまま更新されません。
- `READY`：配信に利用可能。
- `FAILED`：作成時にエラーが発生。
- `EXPIRED`：有効期限切れ。有効期限切れ後、1か月後に自動で削除されます。
- `INACTIVE`：オーディエンスが無効です。
- `ACTIVATING`：オーディエンスを有効化しています。

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.audienceCount

Number

オーディエンスに含まれるユーザーの数。ユーザーのプライバシーを保護するため、有効な送信対象アカウントの数が20未満の場合は0が返ります。ただし、オーディエンスのタイプが以下の場合を除きます。

- ユーザーIDアップロード用のオーディエンス（送信対象アカウントをユーザーIDで指定する場合）
- チャットタグオーディエンス

オーディエンスには、既にLINE公式アカウントをブロックしたユーザーも含まれる可能性があるため、`audienceGroup.audienceCount`の値と、メッセージの送信対象となるユーザーの数は異なります。

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.created

Number

オーディエンスが作成された時刻。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.permission

String

オーディエンスに対する更新権限。現在のMessaging APIチャネルが、対象のオーディエンスを更新できる場合は`READ_WRITE`、更新できない場合は`READ`が返ります。

- `READ`：オーディエンスを利用できますが、更新はできません。
- `READ_WRITE`：オーディエンスを利用、更新できます。

<!-- parameter end -->
<!-- parameter start -->

audienceGroup.isIfaAudience

Boolean

ユーザーIDアップロード用のオーディエンスを作成したときに指定した、送信対象アカウントの種類を示す値。以下のいずれかの値です。

- `true`：IFAで指定する
- `false`：ユーザーIDで指定する（デフォルト）

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroups\[].webtraffic

Object

[ウェブトラフィックオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#get-shared-audience-response-webtraffic)。`audienceGroups[].type`が`WEBTRAFFIC`または`TRACKINGTAG_WEBTRAFFIC`の場合にのみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroup.requestId

String

オーディエンスを作成したときに指定したリクエストID。`audienceGroup.type`が`CLICK`または`IMP`の場合にのみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroup.clickUrl

String

オーディエンスを作成したときに指定したURL。`audienceGroup.type`が`CLICK`で、リンク先URLが指定されている場合にのみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroup.failedType

String

失敗した原因。`audienceGroup.status`が`FAILED`の場合にのみ含まれます。以下のいずれかの値です。

- `AUDIENCE_GROUP_AUDIENCE_INSUFFICIENT`：オーディエンスに含まれるユーザーの数（最低50件）が不足しています。
- `INTERNAL_ERROR`：内部サーバーのエラーです。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroup.activated

Number

オーディエンスが有効化した時間。[LINE広告](https://admanager.line.biz/)や[LINEポイントAD](https://www.lycbiz.com/jp/service/line-point-ad/)で作成したオーディエンスの場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroup.inactivatedTimestamp

Number

オーディエンスが無効化した時間。[LINE広告](https://admanager.line.biz/)や[LINEポイントAD](https://www.lycbiz.com/jp/service/line-point-ad/)で作成したオーディエンスの場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroup.expireTimestamp

Number

オーディエンスの有効期限。UNIX時間（秒）で返されます。特定のオーディエンスの場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start -->

jobs

Array

ジョブの配列。ユーザーIDアップロード用のオーディエンスに、ユーザーIDまたはIFAを追加した最新履歴を管理する配列です。それ以外のオーディエンスの場合は空配列が返ります。<br />最大件数：50

<!-- parameter end -->
<!-- parameter start -->

jobs\[].audienceGroupJobId

Number

ジョブID

<!-- parameter end -->
<!-- parameter start -->

jobs\[].audienceGroupId

Number

オーディエンスID

<!-- parameter end -->
<!-- parameter start -->

jobs\[].description

String

ジョブの説明。ユーザーIDまたはIFAを追加する際に`uploadDescription`プロパティに値を指定しなかった場合は`null`が返されます。

<!-- parameter end -->
<!-- parameter start -->

jobs\[].type

String

ジョブの種類。以下のいずれかの値です。

- `DIFF_ADD`：Messaging APIでユーザーIDまたはIFAを追加したことを示します。

<!-- parameter end -->
<!-- parameter start -->

jobs\[].status

String

このプロパティの利用は非推奨です。ジョブのステータスは`jobs[].jobStatus`を参照してください。

<!-- parameter end -->
<!-- parameter start -->

jobs\[].failedType

String

失敗した原因。`jobs[].jobStatus`が`FAILED`の場合にのみ含まれます。以下のいずれかの値です。

- `AUDIENCE_GROUP_AUDIENCE_INSUFFICIENT`：オーディエンスに含まれるユーザーの数（最低50件）が不足しています。
- `INTERNAL_ERROR`：内部サーバーのエラーです。

`jobs[].jobStatus`が`FAILED`以外の場合は`null`が返されます。

<!-- parameter end -->
<!-- parameter start -->

jobs\[].audienceCount

Number

追加または削除された送信対象アカウントの数

<!-- parameter end -->
<!-- parameter start -->

jobs\[].created

Number

ジョブが作成された時刻。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

jobs\[].jobStatus

String

ジョブのステータス。以下のいずれかの値です。

- `QUEUED`：待機中
- `WORKING`：実行中
- `FINISHED`：成功
- `FAILED`：失敗

<!-- parameter end -->
<!-- parameter start -->

owner.serviceType

String

オーディエンスを作成したサービス名称。以下のいずれかの値を返します。

- `bm`：ビジネスマネージャー
- `lap`：LINE広告
- `account`：LINE公式アカウント
- `yda`：LINEヤフー広告

<!-- parameter end -->
<!-- parameter start -->

owner.id

String

オーディエンスを作成したアカウントのID。

<!-- parameter end -->
<!-- parameter start -->

owner.name

String

オーディエンスを作成したアカウントの名前。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
// ウェブトラフィックオーディエンスの例
{
  "audienceGroup": {
    "audienceGroupId": 1234567890123,
    "createRoute": "BUSINESS_MANAGER",
    "type": "WEBTRAFFIC",
    "description": "Web traffic audience",
    "status": "READY",
    "audienceCount": 0,
    "created": 1668179144,
    "permission": "READ",
    "isIfaAudience": true,
    "webtraffic": {
      "webtrafficIsMyTag": false,
      "webtrafficBmTagSharingStatus": "SHARED",
      "webtrafficIsTagDeleted": false,
      "webtrafficTagCreateRoute": "OA_MANAGER",
      "webtrafficVisitType": "VISIT_ALL",
      "webtrafficRetentionDays": 30,
      "webtrafficTagId": "01234567-8901-2345-6789-012345678901",
      "webtrafficConditionGroup": [],
      "webtrafficTagOwnerName": "LINE Developers (@linedevelopers)"
    }
  },
  "jobs": [],
  "owner": {
    "serviceType": "bm",
    "id": "0123456789ABCDEFGHIJKLMNOP",
    "name": "LINE Developers"
  }
}
```

<!-- tab end -->

##### ウェブトラフィックオブジェクト 

ウェブトラフィックオーディエンスについての情報を表すオブジェクトです。

<!-- parameter start -->

webtrafficIsMyTag

Boolean

- LINE Tagの場合：LINE TagがMessaging APIチャネルと紐づいているLINE公式アカウントで作成されている場合は`true`を返します。
- 計測タグの場合：常に`false`を返します。

<!-- parameter end -->
<!-- parameter start -->

webtrafficBmTagSharingStatus

String

ウェブトラフィックオーディエンスで使用されているLINE Tagまたは計測タグのビジネスマネージャーでの共有状態を表す値。

LINE Tagの場合、以下の値を返します。

- `SHARED`：ビジネスマネージャー上で共有されている
- `UNSHARED`：ビジネスマネージャー上で共有されていない
- `ERROR`：一時的なエラーのためタグの詳細が取得できない

計測タグの場合、以下の値を返します。

- `SHARED`：計測タグを作成したビジネスマネージャーの組織とLINE公式アカウントが連携済み
- `UNSHARED`：計測タグを作成したビジネスマネージャーの組織とLINE公式アカウントが未連携
- `ERROR`：一時的なエラーのためタグの詳細が取得できない

ビジネスマネージャーの組織とLINE公式アカウントの連携方法について詳しくは、『LINE for Business』の「[組織へのLINE公式アカウントの接続方法を教えてください](https://help.linebiz.com/lineadshelp/s/article/L000001362?language=ja)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

webtrafficIsTagDeleted

Boolean

- LINE Tagの場合：このウェブトラフィックオーディエンスで使用されているLINE Tagが既に削除されている場合は`true`を返します。
- 計測タグの場合：常に`false`を返します。

<!-- parameter end -->
<!-- parameter start -->

webtrafficTagCreateRoute

String

ウェブトラフィックオーディエンスの作成方法。以下のいずれかの値です。

- `OA_MANAGER`：[LINE Official Account Manager](https://manager.line.biz/)で作成したオーディエンス
- `AD_MANAGER`：[LINE広告](https://admanager.line.biz/)で作成したオーディエンス
- `BUSINESS_MANAGER`：[ビジネスマネージャー](https://data.linebiz.com/solutions/business-manager)で作成したオーディエンス

<!-- parameter end -->
<!-- parameter start -->

webtrafficVisitType

String

LINE Tagまたは計測タグのマッチング方法。以下のいずれかの値です。

- `VISIT_ALL`：すべての訪問ユーザー
- `URL_MATCHING`：URL条件
- `EVENT_MATCHING`：イベント指定

<!-- parameter end -->
<!-- parameter start -->

webtrafficRetentionDays

String

ウェブトラフィックオーディエンスの保有期間

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

webtrafficTagEventType

String

イベントコードの種類。`webtrafficVisitType`が`EVENT_MATCHING`の場合にのみ含まれます。以下のいずれかの値です。

- `CONVERSION_EVENT`：コンバージョンコード
- `CUSTOM_EVENT`：カスタムイベントコード

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

webtrafficCustomEventName

String

カスタムイベント名。`webtrafficVisitType`が`EVENT_MATCHING`かつ`webtrafficTagEventType`が`CUSTOM_EVENT`の場合にのみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

webtrafficMatchingType

String

LINE Tagまたは計測タグのイベント判定方法。`webtrafficVisitType`が`EVENT_MATCHING`または`URL_MATCHING`の場合にのみ含まれます。値は常に`NORMAL`です。

<!-- parameter end -->
<!-- parameter start -->

webtrafficConditionGroup

Array

マッチング条件を表す配列。

<!-- parameter end -->
<!-- parameter start -->

webtrafficConditionGroup\[].conditionType

String

`keywords`配列に含まれるキーワードとのマッチング条件。以下のいずれかの値です。

- `CONTAIN`：キーワードを含む
- `NOT_CONTAIN`：キーワードを含まない
- `EQUAL_TO`：キーワードと一致する

<!-- parameter end -->
<!-- parameter start -->

webtrafficConditionGroup[].keywords[]

Array of strings

マッチング条件に使用されるキーワードの配列。

<!-- parameter end -->
<!-- parameter start -->

webtrafficTagId

String

LINE Tagまたは計測タグのタグID。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

webtrafficTagOwnerName

String

LINE Tagを発行したアカウントの名前。ウェブトラフィックオーディエンスでLINE Tagが使用されている場合にのみ含まれます。

<!-- parameter end -->

_例_

<!-- tab start `json` -->

```json
{
  "webtrafficIsMyTag": false,
  "webtrafficBmTagSharingStatus": "SHARED",
  "webtrafficIsTagDeleted": false,
  "webtrafficTagCreateRoute": "OA_MANAGER",
  "webtrafficVisitType": "VISIT_ALL",
  "webtrafficRetentionDays": 30,
  "webtrafficTagId": "01234567-8901-2345-6789-012345678901",
  "webtrafficConditionGroup": [],
  "webtrafficTagOwnerName": "LINE Developers (@linedevelopers)"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明                                         |
| ------ | -------------------------------------------- |
| `400`  | 存在しないオーディエンスが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 存在しないオーディエンスを指定した場合（400 Bad Request）
{
  "message": "audience group not found",
  "details": [
    {
      "message": "AUDIENCE_GROUP_NOT_FOUND"
    }
  ]
}
```

<!-- tab end -->

### ビジネスマネージャーで共有されたオーディエンスのリストを取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/audienceGroup/shared/list`

[ビジネスマネージャー](https://data.linebiz.com/solutions/business-manager)で共有されたオーディエンスのリストを取得します。

「[ビジネスマネージャーで共有されたオーディエンスの情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-shared-audience)」エンドポイントを使うことで、それぞれのオーディエンスについて、より詳細な情報を取得できます。

<!-- tip start -->

**ビジネスマネージャーについて**

ビジネスマネージャーを使うことで、特定のオーディエンスを複数のサービス間で共有できます。ビジネスマネージャーでオーディエンスを横断利用することで、エンドユーザーとのより良いコミュニケーションが実現できます。

詳しくは、『LINE DATA SOLUTION』の「[ビジネスマネージャー](https://data.linebiz.com/solutions/business-manager)」を参照してください。

<!-- tip end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/audienceGroup/shared/list \
--data-urlencode 'page=1' \
--data-urlencode 'description=audienceGroupName' \
--data-urlencode 'size=40' \
--data-urlencode 'createRoute=OA_MANAGER' \
-G \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

60リクエスト/分

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: optional) -->

page

取得するページ番号。`1`以上を指定してください。省略した場合は、1ページ目を取得します。

オーディエンスをすべて取得する場合、レスポンスの`audienceGroups`配列が、1ページごとのオーディエンス数（`size`）未満の件数になるまで、`page`をインクリメントしてリクエストを繰り返します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

description

取得するオーディエンスの名前。部分一致で検索できます。なお、大文字と小文字は区別されないため、`AUDIENCE`と`audience`は同じ名前と判定されます。省略した場合は、オーディエンスの名前を検索条件として使用しません。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

status

取得するオーディエンスのステータス。以下のいずれかの値で指定します。省略した場合は、オーディエンスのステータスを検索条件として使用しません。

- `IN_PROGRESS`：準備中。
- `READY`：配信に利用可能。
- `FAILED`：作成時にエラーが発生。
- `EXPIRED`：有効期限切れ。有効期限切れ後、1か月後に自動で削除されます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

size

1ページごとのオーディエンス数。デフォルト値は`20`です。\
最大値：`40`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

createRoute

オーディエンスの作成方法。省略した場合は、すべてのオーディエンスを取得します。

- `OA_MANAGER`：[LINE Official Account Manager](https://manager.line.biz/)で作成したオーディエンスのみを取得
- `MESSAGING_API`：Messaging APIで作成したオーディエンスのみを取得
- `POINT_AD`：[LINEポイントAD](https://www.lycbiz.com/jp/service/line-point-ad/)で作成したオーディエンスのみを取得
- `AD_MANAGER`：[LINE広告](https://admanager.line.biz/)で作成したオーディエンスのみを取得
- `BUSINESS_MANAGER`：[ビジネスマネージャー](https://data.linebiz.com/solutions/business-manager)で作成したオーディエンスのみを取得
- `YAHOO_DISPLAY_ADS`：[LINEヤフー広告 ディスプレイ広告](https://www.lycbiz.com/jp/service/ly-ads/displayads-auc/)で作成したオーディエンスのみを取得

複数のパラメータを指定した場合、OR条件となります。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

includesOwnedAudienceGroups

ビジネスマネージャーで共有されたオーディエンスに加えて、LINE公式アカウントで作成したオーディエンスを含めるかどうかの設定。デフォルト値は`false`です。

- `true`：LINE公式アカウントで作成したオーディエンスを含めて取得
- `false`：ビジネスマネージャーで共有されたオーディエンスのみを取得

<!-- parameter end -->

#### レスポンス 

HTTPステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

audienceGroups

Array

オーディエンスの情報の配列。指定した条件に該当するオーディエンスが存在しなかった場合は空配列が返ります。

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].audienceGroupId

Number

オーディエンスID

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].createRoute

String

オーディエンスの作成方法。以下のいずれかの値です。

- `OA_MANAGER`：[LINE Official Account Manager](https://manager.line.biz/)で作成したオーディエンス
- `MESSAGING_API`：Messaging APIで作成したオーディエンス
- `POINT_AD`：[LINEポイントAD](https://www.lycbiz.com/jp/service/line-point-ad/)で作成したオーディエンス
- `AD_MANAGER`：[LINE広告](https://admanager.line.biz/)で作成したオーディエンス
- `BUSINESS_MANAGER`：[ビジネスマネージャー](https://data.linebiz.com/solutions/business-manager)で作成したオーディエンス
- `YAHOO_DISPLAY_ADS`：[LINEヤフー広告 ディスプレイ広告](https://www.lycbiz.com/jp/service/ly-ads/displayads-auc/)で作成したオーディエンス

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].type

String

オーディエンスのタイプ。以下のいずれかの値です。

- `UPLOAD`：ユーザーIDアップロード用のオーディエンス
- `CLICK`：メッセージクリックオーディエンス
- `IMP`：メッセージインプレッションオーディエンス
- `CHAT_TAG`：チャットタグオーディエンス
- `FRIEND_PATH`：追加経路オーディエンス
- `RESERVATION`：予約オーディエンス
- `RICHMENU_IMP`：リッチメニューインプレッションオーディエンス
- `RICHMENU_CLICK`：リッチメニュークリックオーディエンス
- `APP_EVENT`：アプリイベントオーディエンス
- `VIDEO_VIEW`：動画視聴オーディエンス
- `WEBTRAFFIC`：ウェブトラフィックオーディエンス（LINE Tag）
- `TRACKINGTAG_WEBTRAFFIC`：ウェブトラフィックオーディエンス（計測タグ）
- `IMAGE_CLICK`：画像クリックオーディエンス
- `POP_AD_IMP`：LINE Beacon Networkインプレッションオーディエンス

詳しくは、『LINEヤフー for Business』の「[オーディエンス](https://www.lycbiz.com/jp/manual/OfficialAccountManager/messages-audience/)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].description

String

オーディエンスの名前

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].status

String

オーディエンスのステータス。以下のいずれかの値です。

- `IN_PROGRESS`：準備中。`READY`になるまで数時間かかる場合があります。ユーザー数の規定があるオーディエンスにおいて、オーディエンスに含まれるユーザーの数（最低50件）が不足している場合、ステータスは`IN_PROGRESS`のまま更新されません。
- `READY`：配信に利用可能。
- `FAILED`：作成時にエラーが発生。
- `EXPIRED`：有効期限切れ。有効期限切れ後、1か月後に自動で削除されます。
- `INACTIVE`：オーディエンスが無効です。
- `ACTIVATING`：オーディエンスを有効化しています。

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].audienceCount

Number

オーディエンスに含まれるユーザーの数。ユーザーのプライバシーを保護するため、有効な送信対象アカウントの数が20未満の場合は0が返ります。ただし、オーディエンスのタイプが以下の場合を除きます。

- ユーザーIDアップロード用のオーディエンス（送信対象アカウントをユーザーIDで指定する場合）
- チャットタグオーディエンス

オーディエンスには、既にLINE公式アカウントをブロックしたユーザーも含まれる可能性があるため、`audienceGroups[].audienceCount`の値と、メッセージの送信対象となるユーザーの数は異なります。

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].created

Number

オーディエンスが作成された時刻。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].permission

String

オーディエンスに対する更新権限。現在のMessaging APIチャネルが、対象のオーディエンスを更新できる場合は`READ_WRITE`、更新できない場合は`READ`が返ります。

- `READ`：オーディエンスを利用できますが、更新はできません。
- `READ_WRITE`：オーディエンスを利用、更新できます。

<!-- parameter end -->
<!-- parameter start -->

audienceGroups\[].isIfaAudience

Boolean

ユーザーIDアップロード用のオーディエンスを作成したときに指定した、送信対象アカウントの種類を示す値。以下のいずれかの値です。

- `true`：IFAで指定する
- `false`：ユーザーIDで指定する（デフォルト）

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroups\[].activated

Number

オーディエンスが有効化した時間。[LINE広告](https://admanager.line.biz/)や[LINEポイントAD](https://www.lycbiz.com/jp/service/line-point-ad/)で作成したオーディエンスの場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroups\[].inactivatedTimestamp

Number

オーディエンスが無効化した時間。[LINE広告](https://admanager.line.biz/)や[LINEポイントAD](https://www.lycbiz.com/jp/service/line-point-ad/)で作成したオーディエンスの場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroups\[].expireTimestamp

Number

オーディエンスの有効期限。UNIX時間（秒）で返されます。特定のオーディエンスの場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroups\[].webtraffic

Object

[ウェブトラフィックオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#get-shared-audience-list-response-webtraffic)。`audienceGroups[].type`が`WEBTRAFFIC`または`TRACKINGTAG_WEBTRAFFIC`の場合にのみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroups\[].requestId

String

オーディエンスを作成したときに指定したリクエストID。`audienceGroups[].type`が`CLICK`または`IMP`の場合にのみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroups\[].clickUrl

String

オーディエンスを作成したときに指定したURL。`audienceGroups[].type`が`CLICK`で、リンク先URLが指定されている場合にのみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

audienceGroups\[].failedType

String

失敗した原因。`audienceGroups[].status`が`FAILED`または`EXPIRED`の場合にのみ含まれます。以下のいずれかの値です。

- `AUDIENCE_GROUP_AUDIENCE_INSUFFICIENT`：オーディエンスに含まれるユーザーの数（最低50件）が不足しています。
- `INTERNAL_ERROR`：内部サーバーのエラーです。

<!-- parameter end -->
<!-- parameter start -->

hasNextPage

Boolean

次のページが存在する場合は、`true`

<!-- parameter end -->
<!-- parameter start -->

totalCount

Number

指定した条件で取得できるオーディエンスの総数

<!-- parameter end -->
<!-- parameter start -->

readWriteAudienceGroupTotalCount

Number

指定した条件で取得できるオーディエンスのうち、更新権限（`audienceGroups[].permission`）が`READ_WRITE`になっているオーディエンスの数

<!-- parameter end -->
<!-- parameter start -->

page

Number

現在のページ番号

<!-- parameter end -->
<!-- parameter start -->

size

Number

現在のページに含まれる最大のオーディエンス数

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
// 指定した条件に該当するオーディエンスが2件あった場合の例
{
  "audienceGroups": [
    {
      "audienceGroupId": 1234567890123,
      "createRoute": "BUSINESS_MANAGER",
      "type": "WEBTRAFFIC",
      "description": "Web traffic audience",
      "status": "READY",
      "audienceCount": 4871,
      "created": 1668179144,
      "permission": "READ",
      "isIfaAudience": true,
      "webtraffic": {
        "webtrafficIsMyTag": false,
        "webtrafficBmTagSharingStatus": "SHARED",
        "webtrafficIsTagDeleted": false,
        "webtrafficTagCreateRoute": "OA_MANAGER"
      }
    },
    {
      "audienceGroupId": 3210987654321,
      "createRoute": "AD_MANAGER",
      "type": "IMAGE_CLICK",
      "description": "Image click audience",
      "status": "IN_PROGRESS",
      "audienceCount": 2234,
      "created": 1718895503,
      "permission": "READ",
      "isIfaAudience": true
    }
  ],
  "hasNextPage": false,
  "totalCount": 2,
  "readWriteAudienceGroupTotalCount": 0,
  "size": 40,
  "page": 1
}

// 指定した条件に該当するオーディエンスが存在しなかった場合の例
{
    "audienceGroups": [],
    "hasNextPage": false,
    "totalCount": 0,
    "readWriteAudienceGroupTotalCount": 0,
    "size": 40,
    "page": 1
}
```

<!-- tab end -->

##### ウェブトラフィックオブジェクト 

ウェブトラフィックオーディエンスについての情報を表すオブジェクトです。

<!-- parameter start -->

webtrafficIsMyTag

Boolean

- LINE Tagの場合：LINE TagがMessaging APIチャネルと紐づいているLINE公式アカウントで作成されている場合は`true`を返します。
- 計測タグの場合：常に`false`を返します。

<!-- parameter end -->
<!-- parameter start -->

webtrafficBmTagSharingStatus

String

ウェブトラフィックオーディエンスで使用されているLINE Tagまたは計測タグのビジネスマネージャーでの共有状態を表す値。

LINE Tagの場合、以下の値を返します。

- `SHARED`：ビジネスマネージャー上で共有されている
- `UNSHARED`：ビジネスマネージャー上で共有されていない
- `ERROR`：一時的なエラーのためタグの詳細が取得できない

計測タグの場合、以下の値を返します。

- `SHARED`：計測タグを作成したビジネスマネージャーの組織とLINE公式アカウントが連携済み
- `UNSHARED`：計測タグを作成したビジネスマネージャーの組織とLINE公式アカウントが未連携
- `ERROR`：一時的なエラーのためタグの詳細が取得できない

ビジネスマネージャーの組織とLINE公式アカウントの連携方法について詳しくは、『LINE for Business』の「[組織へのLINE公式アカウントの接続方法を教えてください](https://help.linebiz.com/lineadshelp/s/article/L000001362?language=ja)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

webtrafficIsTagDeleted

Boolean

- LINE Tagの場合：このウェブトラフィックオーディエンスで使用されているLINE Tagが既に削除されている場合は`true`を返します。
- 計測タグの場合：常に`false`を返します。

<!-- parameter end -->
<!-- parameter start -->

webtrafficTagCreateRoute

String

ウェブトラフィックオーディエンスの作成方法。以下のいずれかの値です。

- `OA_MANAGER`：[LINE Official Account Manager](https://manager.line.biz/)で作成したオーディエンス
- `AD_MANAGER`：[LINE広告](https://admanager.line.biz/)で作成したオーディエンス
- `BUSINESS_MANAGER`：[ビジネスマネージャー](https://data.linebiz.com/solutions/business-manager)で作成したオーディエンス

<!-- parameter end -->

_例_

<!-- tab start `json` -->

```json
{
  "webtrafficIsMyTag": false,
  "webtrafficBmTagSharingStatus": "UNSHARED",
  "webtrafficIsTagDeleted": false,
  "webtrafficTagCreateRoute": "BUSINESS_MANAGER"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明                                           |
| ------ | ---------------------------------------------- |
| `400`  | クエリパラメータに無効な値が指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// クエリパラメータに無効な値を指定した場合（400 Bad Request）
{
  "message": "size: must be less than or equal to 40",
  "details": [
    {
      "message": "TOO_HIGH"
    }
  ]
}
```

<!-- tab end -->

## 分析 

LINE公式アカウントから送信したメッセージの数や友だち数、統計情報などを取得できます。

### メッセージの送信数を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/insight/message/delivery?date={date}`

`date`に指定した日に、LINE公式アカウントから送信したメッセージの数を確認できます。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET 'https://api.line.me/v2/bot/insight/message/delivery?date=20190418' \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

60リクエスト/時

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: required) -->

date

メッセージの送信数を確認する日付

- フォーマット：`yyyyMMdd`（例：`20191231`）
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
- `out_of_service`：`date`に指定した日付が、集計システムの稼働開始日（2017年3月1日）より前です。

`broadcast`以降のプロパティは、`status`プロパティの値が`ready`の場合にのみレスポンスに含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

broadcast

Number

LINE Official Account Managerで配信先を［**すべての友だち**］にして送信したメッセージの数。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

targeting

Number

LINE Official Account Managerで配信先を［**絞り込み**］にして送信したメッセージの数。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

stepMessage

Number

LINE Official Account Managerでステップ配信を使って送信されたメッセージの数。

詳しくは、『LINEヤフー for Business』の「[ステップ配信](https://www.lycbiz.com/jp/manual/OfficialAccountManager/step-message/)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

autoResponse

Number

ユーザーからメッセージを受信した際に、自動的に送信された応答メッセージの数。

詳しくは、『LINEヤフー for Business』の「[応答メッセージ](https://www.lycbiz.com/jp/manual/OfficialAccountManager/Auto-response-messages/)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

welcomeResponse

Number

ユーザーがLINE公式アカウントを友だち追加した際に、自動的に送信されたあいさつメッセージの数。

詳しくは、『LINEヤフー for Business』の「[あいさつメッセージを設定する](https://www.lycbiz.com/jp/manual/OfficialAccountManager/greeting-message/)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

chat

Number

LINE Official Account Managerの「[チャット基本画面](https://www.lycbiz.com/jp/manual/OfficialAccountManager/chats/)」から送信されたメッセージの数。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

apiBroadcast

Number

「[ブロードキャストメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-broadcast-message)」エンドポイントを使って送信されたメッセージの数。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

apiPush

Number

「[プッシュメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-push-message)」エンドポイントを使って送信されたメッセージの数。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

apiMulticast

Number

「[マルチキャストメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-multicast-message)」エンドポイントを使って送信されたメッセージの数。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

apiNarrowcast

Number

「[ナローキャストメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message)」エンドポイントを使って送信されたメッセージの数。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

apiReply

Number

「[応答メッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)」エンドポイントを使って送信されたメッセージの数。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

ccAutoReply

Number

LINEチャットPlusの自動応答で送信されたメッセージの数。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

ccManualReply

Number

LINEチャットPlusの有人でのチャット対応で送信されたメッセージの数。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

pnpNoticeMessage

Number

法人ユーザー向けオプションの「[LINE通知メッセージ](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/overview/)」を使って送信されたメッセージの数。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

pnpCallToLine

Number

Call to LINE（※）で送信されたメッセージの数。

※ Call to LINEの新規利用受付は終了しています。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

thirdPartyChatTool

Number

外部チャットツールから送信されたメッセージの数。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
// 集計が完了していた場合
{
  "status": "ready",
  "broadcast": 5385,
  "targeting": 522
}

// まだ集計が完了していなかった場合
{
  "status": "unready"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明                           |
| ------ | ------------------------------ |
| `400`  | 無効な日付が指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効な日付を指定した場合（400 Bad Request）
{
  "message": "Bad Request"
}
```

<!-- tab end -->

### 友だち数を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/insight/followers?date={date}`

LINE公式アカウントの友だち数を確認できます。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET 'https://api.line.me/v2/bot/insight/followers?date=20190418' \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

60リクエスト/時

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: required) -->

date

友だち数を確認する日付

- フォーマット：`yyyyMMdd`（例：`20191231`）
- タイムゾーン：UTC+9

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

status

String

集計処理の状態。以下のいずれかの値です。

- `ready`：数値を取得できます。
- `unready`：`date`に指定した日付の友だち数の集計がまだ完了していません。しばらくしてからリクエストを再実行してください。通常、集計処理は翌日中に完了します。
- `out_of_service`：`date`に指定した日付が、集計システムの稼働開始日（2016年11月1日）より前です。

<!-- parameter end -->
<!-- parameter start -->

followers

Number

`date`に指定した日付までに、アカウントが友だち追加された回数。アカウントがブロックされたり、あなたを友だち追加したユーザーがLINEアカウントを削除したりしても、この値は減少しません。

`status`の値が`ready`以外の場合、`null`になります。

<!-- parameter end -->
<!-- parameter start -->

targetedReaches

Number

`date`に指定した日付時点の、性別や年齢、地域で絞り込んだターゲティングメッセージの配信先となりうる友だちの総数。LINEおよびその他のLINEサービスの利用頻度が高く、属性の高精度な推定が可能な友だちが含まれます。

`status`の値が`ready`以外の場合、`null`になります。

<!-- parameter end -->
<!-- parameter start -->

blocks

Number

`date`に指定した日付時点で、アカウントをブロックしているユーザーの数。ブロックが解除されると、この値は減少します。

`status`の値が`ready`以外の場合、`null`になります。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
// 集計が完了していた場合
{
  "status": "ready",
  "followers": 7620,
  "targetedReaches": 5848,
  "blocks": 237
}

// まだ集計が完了していなかった場合
{
  "status": "unready",
  "followers": null,
  "targetedReaches": null,
  "blocks": null
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | 日付が指定されていない、もしくは無効な日付が指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 日付を指定しなかった場合（400 Bad Request）
{
  "message": "date is required"
}

// 無効な日付を指定した場合（400 Bad Request）
{
  "message": "Bad Request"
}
```

<!-- tab end -->

### 友だちの属性情報に基づく統計情報を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/insight/demographic`

LINE公式アカウントの友だちの属性情報に基づく統計情報を取得します。友だちの属性情報に基づく統計情報を取得するには、以下の条件をすべて満たす必要があります。

- [ターゲットリーチ](https://developers.line.biz/ja/glossary/#target-reach)が20人以上である。
- 日本（JP）、タイ（TH）、台湾（TW）のユーザーが作成したLINE公式アカウントである。

<!-- note start -->

**リアルタイムデータではありません**

友だちの属性情報に基づく統計情報が反映されるまで約3日かかります。そのため、取得できる情報は約3日前の数値です。なお、反映されるタイミングは前後する可能性があります。

<!-- note end -->

<!-- tip start -->

**属性情報について**

友だちの属性情報は、LINEファミリーサービスにおいて、LINEユーザーが登録した性別、年代、エリア情報と行動履歴をもとに分類した「みなし属性」となります。携帯キャリアおよびOSは、みなし属性に含まれません。

みなし属性は、ユーザーがLINE上で購入、使用したスタンプや興味のあるコンテンツのほか、どのようなLINE公式アカウントと友だちになっているかといった傾向をもとに分類したものです。分類の元となる情報に電話番号、メールアドレス、アドレス帳、トーク内容などの機微情報は含みません。

属性情報の推定は統計的に実施され、特定の個人の識別は行っていません。また、特定の個人を識別可能な情報の第三者（広告主など）への提供は実施していません。

<!-- tip end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/insight/demographic \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

60リクエスト/時

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

available

Boolean

- `true`：友だちの属性情報に基づく統計情報が利用できる。
- `false`：次のような理由で、友だちの属性情報に基づく統計情報が利用できない。
  - [ターゲットリーチ](https://developers.line.biz/ja/glossary/#target-reach)が20人未満である。
  - 日本（JP）、タイ（TH）、台湾（TW）以外のユーザーが作成したLINE公式アカウントである。

レスポンス内の各配列（`genders`、`ages`、`areas`、`appTypes`、`subscriptionPeriods`）の要素は、`available`の値が`true`の場合にのみレスポンスに含まれます。

<!-- parameter end -->
<!-- parameter start -->

genders

Array

性別ごとの割合。統計情報が利用できない場合、空の配列を返します。

<!-- parameter end -->
<!-- parameter start -->

genders\[].gender

String

ユーザーの性別に基づいて、以下の値が返されます。

- `male`
- `female`
- `unknown`

<!-- parameter end -->
<!-- parameter start -->

genders\[].percentage

Number

割合

<!-- parameter end -->
<!-- parameter start -->

ages

Array

年齢ごとの割合。統計情報が利用できない場合、空の配列を返します。

<!-- parameter end -->
<!-- parameter start -->

ages\[].age

String

ユーザーの年齢に基づいて、以下の値が返されます。

<!-- note start -->

**タイのLINE公式アカウントを利用している場合**

タイのLINE公式アカウントの統計情報を取得する場合、レスポンス内の`ages[].age`の値として、`from0to14`と`from15to19`の割合は返されません。年齢が20歳未満のユーザーは、`unknown`として集計されます。

<!-- note end -->

- `from0to14`
- `from15to19`
- `from20to24`
- `from25to29`
- `from30to34`
- `from35to39`
- `from40to44`
- `from45to49`
- `from50`
  - 2024年9月5日より、[50歳から70歳までの割合を取得できるようになりました](https://developers.line.biz/ja/news/2024/09/05/age-percentage-subdivision/)。
- `from50to54`
- `from55to59`
- `from60to64`
- `from65to69`
- `from70`
- `unknown`

<!-- parameter end -->
<!-- parameter start -->

ages\[].percentage

Number

割合

<!-- parameter end -->
<!-- parameter start -->

areas

Array

地域ごとの割合。統計情報が利用できない場合、空の配列を返します。

<!-- parameter end -->
<!-- parameter start -->

areas\[].area

String

ユーザーの国や地域に基づいて、以下の値が返されます。\
**JP**

- `北海道`
- `青森`
- `岩手`
- `宮城`
- `秋田`
- `山形`
- `福島`
- `茨城`
- `栃木`
- `群馬`
- `埼玉`
- `千葉`
- `東京`
- `神奈川`
- `新潟`
- `富山`
- `石川`
- `福井`
- `山梨`
- `長野`
- `岐阜`
- `静岡`
- `愛知`
- `三重`
- `滋賀`
- `京都`
- `大阪`
- `兵庫`
- `奈良`
- `和歌山`
- `鳥取`
- `島根`
- `岡山`
- `広島`
- `山口`
- `徳島`
- `香川`
- `愛媛`
- `高知`
- `福岡`
- `佐賀`
- `長崎`
- `熊本`
- `大分`
- `宮崎`
- `鹿児島`
- `沖縄`
- `unknown`

**TW**

- `台北市`
- `新北市`
- `桃園市`
- `台中市`
- `台南市`
- `高雄市`
- `基隆市`
- `新竹市`
- `嘉義市`
- `新竹縣`
- `苗栗縣`
- `彰化縣`
- `南投縣`
- `雲林縣`
- `嘉義縣`
- `屏東縣`
- `宜蘭縣`
- `花蓮縣`
- `台東縣`
- `澎湖縣`
- `金門縣`
- `連江縣`
- `unknown`

**TH**

- `Bangkok`
- `Pattaya`
- `Northern`
- `Central`
- `Southern`
- `Eastern`
- `NorthEastern`
- `Western`
- `unknown`

<!-- parameter end -->
<!-- parameter start -->

areas\[].percentage

Number

割合

<!-- parameter end -->
<!-- parameter start -->

appTypes

Array

OSごとの割合。統計情報が利用できない場合、空の配列を返します。

<!-- parameter end -->
<!-- parameter start -->

appTypes\[].appType

String

ユーザーが使用するOSに基づいて、以下の値が返されます。

- `ios`
- `android`
- `others`

<!-- parameter end -->
<!-- parameter start -->

appTypes\[].percentage

Number

割合

<!-- parameter end -->
<!-- parameter start -->

subscriptionPeriods

Array

友だち期間ごとの割合。統計情報が利用できない場合、空の配列を返します。

<!-- parameter end -->
<!-- parameter start -->

subscriptionPeriods\[].subscriptionPeriod

String

ユーザーとの友だち期間に基づいて、以下の値が返されます。友だち期間とは、ユーザーがLINE公式アカウントを友だち追加してからの期間のことです。ユーザーがLINE公式アカウントを友だち追加した翌日を1日目として起算します。

- `within7days`：7日未満
- `within30days`：7日以上30日未満
- `within90days`：30日以上90日未満
- `within180days`：90日以上180日未満
- `within365days`：180日以上365日未満
- `over365days`：365日以上
- `unknown`：不明

<!-- parameter end -->
<!-- parameter start -->

subscriptionPeriods\[].percentage

Number

それぞれの`subscriptionPeriod`に対するユーザーの割合。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
// ターゲットリーチが20人未満で統計情報が利用できない場合
{
  "available": false,
  "genders": [],
  "ages": [],
  "areas": [],
  "appTypes": [],
  "subscriptionPeriods": []
}

// ターゲットリーチが20人以上で統計情報が利用できる場合
{
    "available": true,
    "genders": [
        {
            "gender": "unknown",
            "percentage": 37.6
        },
        {
            "gender": "male",
            "percentage": 31.8
        },
        {
            "gender": "female",
            "percentage": 30.6
        }
    ],
    "ages": [
        {
            "age": "unknown",
            "percentage": 37.6
        },
        {
            "age": "from50",
            "percentage": 17.3
        },
        ...
    ],
    "areas": [
        {
            "area": "unknown",
            "percentage": 42.9
        },
        {
            "area": "徳島",
            "percentage": 2.9
        },
        ...
    ],
    "appTypes": [
        {
            "appType": "ios",
            "percentage": 62.4
        },
        {
            "appType": "android",
            "percentage": 27.7
        },
        {
            "appType": "others",
            "percentage": 9.9
        }
    ],
    "subscriptionPeriods": [
        {
            "subscriptionPeriod": "over365days",
            "percentage": 96.4
        },
        {
            "subscriptionPeriod": "within365days",
            "percentage": 1.9
        },
        {
            "subscriptionPeriod": "within180days",
            "percentage": 1.2
        },
        {
            "subscriptionPeriod": "within90days",
            "percentage": 0.5
        },
        {
            "subscriptionPeriod": "within30days",
            "percentage": 0.1
        },
        {
            "subscriptionPeriod": "within7days",
            "percentage": 0
        }
    ]
}
```

<!-- tab end -->

#### エラーレスポンス 

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

### ユーザーの操作に基づく統計情報を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/insight/message/event?requestId={requestId}`

LINE公式アカウントから送信したナローキャストメッセージまたはブロードキャストメッセージに対して、ユーザーがどのように操作したかを示す統計情報を確認できます。

1メッセージ（message）単位、および1吹き出し（bubble）単位で統計情報を取得できます。

![message and bubbles](https://developers.line.biz/media/messaging-api/get-message-event.png)

<!-- note start -->

**記録される統計情報について**

統計情報は、メッセージの送信時刻から14日間（1,209,600秒間）のみ更新されます。それ以降は更新されません。

たとえば2021年2月1日の21:15:00に送信した場合、統計情報は2021年2月15日の21:15:00まで更新されます。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET 'https://api.line.me/v2/bot/insight/message/event?requestId=f70dd685-499a-4231-a441-f24b8d4fba21' \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

60リクエスト/時

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: required) -->

requestId

ナローキャストメッセージまたはブロードキャストメッセージのリクエストID。リクエストIDは、Messaging APIのリクエストごとに発行されるIDです。[レスポンスヘッダー](https://developers.line.biz/ja/reference/messaging-api/#response-headers)に含まれます。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- note start -->

**注意**

統計情報の数値は、多少の誤差を含むことがあります。

またプライバシーを保護するため、次のような場合、個人の操作に関するプロパティの値は`null`になります。

- プロパティの値が20未満だった場合
- プロパティの値が20以上であっても、そのイベントを発生させた実人数が20人未満だった場合（たとえば`messages[].mediaPlayed`は30だが、`messages[].uniqueMediaPlayed`が15だった場合は、どちらの値も`null`になります）

<!-- note end -->

<!-- parameter start -->

overview

Object

メッセージに関する統計情報。

<!-- parameter end -->
<!-- parameter start -->

overview.requestId

String

リクエストID。

<!-- parameter end -->
<!-- parameter start -->

overview.timestamp

Number

メッセージが配信された時刻。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

overview.delivered

Number

メッセージの送信数。この値は、20未満の数値も表示されます。ただし、メッセージの送信がすべて完了していない場合はnullになります。

<!-- parameter end -->
<!-- parameter start -->

overview.uniqueImpression

Number

メッセージを開封した人数。少なくとも1つの吹き出しを表示した人数です。

<!-- parameter end -->
<!-- parameter start -->

overview.uniqueClick

Number

メッセージ内のいずれかのURLをタップした人数。

<!-- parameter end -->
<!-- parameter start -->

overview.uniqueMediaPlayed

Number

メッセージ内のいずれかの動画または音声の再生を開始した人数。

<!-- parameter end -->
<!-- parameter start -->

overview.uniqueMediaPlayed100Percent

Number

メッセージ内のいずれかの動画または音声を最後まで視聴した人数。

<!-- parameter end -->
<!-- parameter start -->

messages

Array

吹き出しに関する情報を表す配列。統計情報が利用できない場合、空の配列を返します。

<!-- parameter end -->
<!-- parameter start -->

messages\[].seq

Number

吹き出しの通し番号。

<!-- parameter end -->
<!-- parameter start -->

messages\[].impression

Number

吹き出しが表示された回数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].mediaPlayed

Number

吹き出し内の動画または音声が再生開始された回数。動画が自動再生された場合も、回数に含まれます。

<!-- parameter end -->
<!-- parameter start -->

messages\[].mediaPlayed25Percent

Number

吹き出し内の動画または音声が再生開始され、25%再生された回数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].mediaPlayed50Percent

Number

吹き出し内の動画または音声が再生開始され、50%再生された回数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].mediaPlayed75Percent

Number

吹き出し内の動画または音声が再生開始され、75%再生された回数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].mediaPlayed100Percent

Number

吹き出し内の動画または音声が再生開始され、100%再生された回数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].uniqueMediaPlayed

Number

吹き出し内の動画または音声を再生開始した人数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].uniqueMediaPlayed25Percent

Number

吹き出し内の動画または音声を再生開始し、25%再生した人数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].uniqueMediaPlayed50Percent

Number

吹き出し内の動画または音声を再生開始し、50%再生した人数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].uniqueMediaPlayed75Percent

Number

吹き出し内の動画または音声を再生開始し、75%再生した人数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].uniqueMediaPlayed100Percent

Number

吹き出し内の動画または音声を再生開始し、100%再生した人数。

<!-- parameter end -->
<!-- parameter start -->

clicks

Array

タップしたURLに関する情報を表す配列。メッセージにURLが含まれていない場合や統計情報が利用できない場合は、空の配列を返します。

<!-- parameter end -->
<!-- parameter start -->

clicks\[].seq

Number

URLが含まれていた吹き出しの通し番号。

<!-- parameter end -->
<!-- parameter start -->

clicks\[].url

String

URL。

<!-- parameter end -->
<!-- parameter start -->

clicks\[].click

Number

吹き出し内のURLをタップした回数。

<!-- parameter end -->
<!-- parameter start -->

clicks\[].uniqueClick

Number

吹き出し内のURLをタップした人数。

<!-- parameter end -->
<!-- parameter start -->

clicks\[].uniqueClickOfRequest

Number

メッセージ内のURLのうち`url`と同じURLをタップした人数。ほかの吹き出しに同じURLが設定されている場合に、1人のユーザーが各URLをタップした場合でも、1回だけカウントされます。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
// 各プロパティの値が20未満で統計情報が利用できない場合
{
  "overview": {
    "requestId": "a425a5cd-6510-43fe-95be-a27f222e5dc0",
    "timestamp": 1711684800,
    "delivered": 1,
    "uniqueImpression": null,
    "uniqueClick": null,
    "uniqueMediaPlayed": null,
    "uniqueMediaPlayed100Percent": null
  },
  "messages": [],
  "clicks": []
}

// 各プロパティの値が20以上で統計情報が利用できる場合
{
  "overview": {
    "requestId": "f70dd685-499a-4231-a441-f24b8d4fba21",
    "timestamp": 1568214000,
    "delivered": 320,
    "uniqueImpression": 82,
    "uniqueClick": 51,
    "uniqueMediaPlayed": null,
    "uniqueMediaPlayed100Percent": null
  },
  "messages": [
    {
      "seq": 1,
      "impression": 136,
      "mediaPlayed": null,
      "mediaPlayed25Percent": null,
      "mediaPlayed50Percent": null,
      "mediaPlayed75Percent": null,
      "mediaPlayed100Percent": null,
      "uniqueMediaPlayed": null,
      "uniqueMediaPlayed25Percent": null,
      "uniqueMediaPlayed50Percent": null,
      "uniqueMediaPlayed75Percent": null,
      "uniqueMediaPlayed100Percent": null
    }
  ],
  "clicks": [
    {
      "seq": 1,
      "url": "https://line.me/",
      "click": 41,
      "uniqueClick": 30,
      "uniqueClickOfRequest": 30
    },
    {
      "seq": 1,
      "url": "https://www.lycorp.co.jp/",
      "click": 59,
      "uniqueClick": 38,
      "uniqueClickOfRequest": 38
    }
  ]
}
```

<!-- tab end -->

#### エラーレスポンス 

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

### ユニットごとの統計情報を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/insight/message/event/aggregation?customAggregationUnit={customAggregationUnit}&from={from}&to={to}`

LINE公式アカウントから送信したプッシュメッセージやマルチキャストメッセージに対して、ユーザーがどのように操作したかを示す統計情報をユニットごとに確認できます。

統計情報はユニットごとに、1メッセージ（message）単位、および1吹き出し（bubble）単位で取得できます。

![message and bubbles](https://developers.line.biz/media/messaging-api/get-message-event.png)

なお、ユニット名が同じメッセージを複数送った場合、メッセージの内容や吹き出し数、吹き出しの順番が異なっていても、統計情報はユニットごとにまとめて集計されます。

<!-- note start -->

**記録される統計情報について**

統計情報は、メッセージの送信時刻から14日間（1,209,600秒間）のみ更新されます。それ以降は更新されません。

たとえば2021年2月1日の21:15:00に送信した場合、統計情報は2021年2月15日の21:15:00まで更新されます。

<!-- note end -->

<!-- tip start -->

**メッセージごとの統計情報を取得したい場合**

ナローキャストメッセージまたはブロードキャストメッセージについて、メッセージごとの統計情報を取得したい場合は、次のエンドポイントを使用してください。

- [ユーザーの操作に基づく統計情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-message-event)

<!-- tip end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/insight/message/event/aggregation \
-H 'Authorization: Bearer {channel access token}' \
--data-urlencode 'customAggregationUnit=promotion_a' \
--data-urlencode 'from=20210301' \
--data-urlencode 'to=20210331' \
-G
```

<!-- tab end -->

#### レート制限 

60リクエスト/時

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: required) -->

customAggregationUnit

String

メッセージ送信時に付与した任意の集計単位のユニット名。大文字と小文字は区別されます。たとえば`promotion_a`と`promotion_A`は別のユニットとして扱われます。

ユニット名の付与について詳しくは、『Messaging APIドキュメント』の「[ユニット名を付与する](https://developers.line.biz/ja/docs/messaging-api/unit-based-statistics-aggregation/#assign-names-to-units-when-sending-messages)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

from

String

集計対象期間の開始日。

- フォーマット：`yyyyMMdd`（例：`20210301`）
- タイムゾーン：UTC+9

<!-- parameter end -->
<!-- parameter start (props: required) -->

to

String

集計対象期間の終了日。終了日は、開始日の30日後まで指定できます。たとえば、開始日が`20210301`の場合、終了日は`20210331`まで指定できます。

- フォーマット：`yyyyMMdd`（例：`20210331`）
- タイムゾーン：UTC+9

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- note start -->

**注意**

統計情報の数値は、多少の誤差を含むことがあります。

またプライバシーを保護するため、次のような場合、個人の操作に関するプロパティの値は`null`になります。

- プロパティの値が20未満だった場合
- プロパティの値が20以上であっても、そのイベントを発生させた実人数が20人未満だった場合（たとえば`messages[].mediaPlayed`は30だが、`messages[].uniqueMediaPlayed`が15だった場合は、どちらの値も`null`になります）

<!-- note end -->

<!-- parameter start -->

overview

Object

メッセージに関する統計情報。

<!-- parameter end -->
<!-- parameter start -->

overview.uniqueImpression

Number

メッセージを開封した人数。少なくとも1つの吹き出しを表示した人数です。

<!-- parameter end -->
<!-- parameter start -->

overview.uniqueClick

Number

メッセージ内のいずれかのURLをタップした人数。

<!-- parameter end -->
<!-- parameter start -->

overview.uniqueMediaPlayed

Number

メッセージ内のいずれかの動画または音声の再生を開始した人数。

<!-- parameter end -->
<!-- parameter start -->

overview.uniqueMediaPlayed100Percent

Number

メッセージ内のいずれかの動画または音声を最後まで視聴した人数。

<!-- parameter end -->
<!-- parameter start -->

messages

Array

吹き出しに関する情報を表す配列。統計情報が利用できない場合、空の配列を返します。

<!-- parameter end -->
<!-- parameter start -->

messages\[].seq

Number

吹き出しの通し番号。

<!-- parameter end -->
<!-- parameter start -->

messages\[].impression

Number

吹き出しが表示された回数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].uniqueImpression

Number

吹き出しを表示した人数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].mediaPlayed

Number

吹き出し内の動画または音声が再生開始された回数。動画が自動再生された場合も、回数に含まれます。

<!-- parameter end -->
<!-- parameter start -->

messages\[].mediaPlayed25Percent

Number

吹き出し内の動画または音声が再生開始され、25%再生された回数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].mediaPlayed50Percent

Number

吹き出し内の動画または音声が再生開始され、50%再生された回数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].mediaPlayed75Percent

Number

吹き出し内の動画または音声が再生開始され、75%再生された回数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].mediaPlayed100Percent

Number

吹き出し内の動画または音声が再生開始され、100%再生された回数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].uniqueMediaPlayed

Number

吹き出し内の動画または音声を再生開始した人数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].uniqueMediaPlayed25Percent

Number

吹き出し内の動画または音声を再生開始し、25%再生した人数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].uniqueMediaPlayed50Percent

Number

吹き出し内の動画または音声を再生開始し、50%再生した人数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].uniqueMediaPlayed75Percent

Number

吹き出し内の動画または音声を再生開始し、75%再生した人数。

<!-- parameter end -->
<!-- parameter start -->

messages\[].uniqueMediaPlayed100Percent

Number

吹き出し内の動画または音声を再生開始し、100%再生した人数。

<!-- parameter end -->
<!-- parameter start -->

clicks

Array

タップしたURLに関する情報を表す配列。メッセージにURLが含まれていない場合や統計情報が利用できない場合は、空の配列を返します。

<!-- parameter end -->
<!-- parameter start -->

clicks\[].seq

Number

URLが含まれていた吹き出しの通し番号。

<!-- parameter end -->
<!-- parameter start -->

clicks\[].url

String

URL。

<!-- parameter end -->
<!-- parameter start -->

clicks\[].click

Number

吹き出し内のURLをタップした回数。

<!-- parameter end -->
<!-- parameter start -->

clicks\[].uniqueClick

Number

吹き出し内のURLをタップした人数。

<!-- parameter end -->
<!-- parameter start -->

clicks\[].uniqueClickOfRequest

Number

メッセージ内のURLのうち`url`と同じURLをタップした人数。ほかの吹き出しに同じURLが設定されている場合に、1人のユーザーが各URLをタップした場合でも、1回だけカウントされます。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
// 集計対象期間に該当するユニットの統計情報が存在しなかった場合
{
  "overview": {
    "uniqueImpression": null,
    "uniqueClick": null,
    "uniqueMediaPlayed": null,
    "uniqueMediaPlayed100Percent": null
  },
  "messages": [],
  "clicks": []
}

// 集計対象期間に該当するユニットの統計情報が存在した場合
{
  "overview": {
    "uniqueImpression": 40,
    "uniqueClick": 30,
    "uniqueMediaPlayed": 25,
    "uniqueMediaPlayed100Percent": null
  },
  "messages": [
    {
      "seq": 1,
      "impression": 42,
      "uniqueImpression": 40,
      "mediaPlayed": 30,
      "mediaPlayed25Percent": null,
      "mediaPlayed50Percent": null,
      "mediaPlayed75Percent": null,
      "mediaPlayed100Percent": null,
      "uniqueMediaPlayed": 25,
      "uniqueMediaPlayed25Percent": null,
      "uniqueMediaPlayed50Percent": null,
      "uniqueMediaPlayed75Percent": null,
      "uniqueMediaPlayed100Percent": null
    }
  ],
  "clicks": [
    {
      "seq": 1,
      "url": "https://developers.line.biz/",
      "click": 35,
      "uniqueClick": 25,
      "uniqueClickOfRequest": null
    },
    {
      "seq": 1,
      "url": "https://api.line-status.info/",
      "click": 29,
      "uniqueClick": null,
      "uniqueClickOfRequest": null
    }
  ]
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | 統計情報が取得できませんでした。次のような理由が考えられます。<ul><li>ユニット名が指定されていない。</li><li>集計対象期間が指定されていない。</li><li>無効な集計対象期間が指定されている。</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 統計情報が取得できなかった場合（400 Bad Request）
{
  "message": null,
  "key": null,
  "stacktrace": null,
  "code": null
}
```

<!-- tab end -->

### 当月中に付与したユニット名の種類数を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/message/aggregation/info`

当月中にメッセージに付与したユニット名の種類数を取得します。メッセージ送信時にユニット名を付与する際の制限については、『Messaging APIドキュメント』の「[ユニット名の種類数の上限](https://developers.line.biz/ja/docs/messaging-api/unit-based-statistics-aggregation/#limit-to-the-number-of-units)」を参照してください。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/message/aggregation/info \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

numOfCustomAggregationUnits

Number

当月中にメッセージに付与したユニット名の種類数。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "numOfCustomAggregationUnits": 22
}
```

<!-- tab end -->

#### エラーレスポンス 

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

### 当月中に付与したユニット名のリストを取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/message/aggregation/list`

当月中にメッセージに付与したユニット名の、一意なリストを取得します。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/message/aggregation/list \
-H 'Authorization: Bearer {channel access token}' \
--data-urlencode 'limit=30' \
-G
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: optional) -->

limit

String

1回のリクエストで取得するユニット名の最大数です。デフォルト値は`100`です。\
最大値：`100`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

start

String

継続トークンの値。[レスポンス](https://developers.line.biz/ja/reference/messaging-api/#get-a-list-of-unit-names-assigned-during-this-month-response)で返されるJSONオブジェクトの`next`プロパティに含まれます。1回のリクエストでユニット名をすべて取得できない場合は、このパラメータを指定して残りの配列を取得します。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

customAggregationUnits

Array of strings

ユニット名を表す文字列の配列です。配列には、当月中にメッセージに付与したユニット名が一意に含まれています。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

next

String

継続トークン。ユニット名の次の配列を取得するために使用します。このプロパティは、前回までのレスポンスの`customAggregationUnits`プロパティで取得しきれなかったユニット名がある場合にのみ返されます。

継続トークンの有効期間は24時間（86,400秒間）です。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "customAggregationUnits": ["promotion_a", "promotion_b"],
  "next": "jxEWCEEP..."
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>無効な継続トークンを指定している。</li><li>`limit`プロパティに不正な値を指定している。</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 有効期限切れなどの無効な継続トークンを指定した場合（400 Bad Request）
{
  "message": "Invalid start param"
}
```

<!-- tab end -->

## クーポン 

LINE公式アカウントからユーザーに送信するクーポンを管理できます。

### クーポンを作成する 

Endpoint: `POST` `https://api.line.me/v2/bot/coupon`

クーポンを作成するAPIです。

クーポンは作成しただけではユーザーには配布されません。作成したクーポンをメッセージとして送信する必要があります。詳しくは、『Messaging APIドキュメント』の「[Messaging APIでクーポンを送る手順](https://developers.line.biz/ja/docs/messaging-api/send-coupons-to-users/#send-coupons-using-messaging-api)」を参照してください。

有効なクーポンを最大5,000件作成できます。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/coupon \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d \
'
{
  "title": "友だち限定クーポン",
  "description": "- クーポンを使用するには、この画面をスタッフに提示してください。\n- 使用済みのクーポンはご利用になれません。また、お客さまの操作で誤って「使用済み」にしてしまった場合も利用できなくなります。\n- 本クーポンは有効期間に関わらず、予告なく変更されたり、終了したりする場合があります。",
  "reward": {
    "type": "discount",
    "priceInfo": {
      "type": "fixed",
      "fixedAmount": 100
    }
  },
  "acquisitionCondition": {
    "type": "normal"
  },
  "startTimestamp": 0,
  "endTimestamp": 1924959599,
  "imageUrl": "https://developers.line.biz/media/messaging-api/coupon/sample-coupon-image-100-yen-off.jpg",
  "timezone": "ASIA_TOKYO",
  "visibility": "UNLISTED",
  "maxUseCountPerTicket": 1
}'
```

<!-- tab end -->

#### レート制限 

200リクエスト/秒

[LINE Official Account Manager](https://developers.line.biz/ja/glossary/#line-oa-manager)を使ってクーポンを作成する場合は制限の対象外です。

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

title

String

クーポンのクーポン名。\
最大文字数：60

<!-- parameter end -->
<!-- parameter start (props: optional) -->

description

String

クーポンの利用ガイド。クーポンの利用方法や注意事項などを設定します。改行文字（`\n`）を使って改行できます。\
最大文字数：1,000

<!-- parameter end -->
<!-- parameter start (props: required) -->

acquisitionCondition

Object

クーポンの獲得条件を含むオブジェクト。

<!-- parameter end -->
<!-- parameter start (props: required) -->

acquisitionCondition.type

String

クーポンの獲得条件のタイプ。\
以下のいずれかの値を指定します。

- `normal`：条件なし。すべてのユーザーが獲得できる。
- `lottery`：抽選。抽選で当選したユーザーのみが獲得できる。

なお獲得条件が「友だち紹介」のクーポンは、Messaging APIでは作成できません。LINE Official Account Managerからのみ作成できます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

acquisitionCondition.lotteryProbability

Number

クーポンの当選確率（％）。1〜99の整数を指定します。\
たとえば、50を指定したときの当選確率は50%となります。\
`acquisitionCondition.type`が`lottery`の場合は必須です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

acquisitionCondition.maxAcquireCount

Number

当選者数の上限。1〜999999の整数を指定します。\
上限なしの場合は`-1`を指定します。\
`acquisitionCondition.type`が`lottery`の場合は必須です。

<!-- parameter end -->
<!-- parameter start (props: required) -->

maxUseCountPerTicket

Number

クーポンの使用可能回数。\
以下のいずれかの値を指定します。

- `1`：1回のみ
- `-1`：上限なし

<!-- parameter end -->
<!-- parameter start (props: required) -->

startTimestamp

Number

クーポンの有効期間の開始日時。\
UNIX時間（秒）で指定します。

<!-- parameter end -->
<!-- parameter start (props: required) -->

endTimestamp

Number

クーポンの有効期間の終了日時。\
UNIX時間（秒）で指定します。\
現在日時よりも前、あるいは開始日時よりも前の日時は指定できません。

<!-- parameter end -->
<!-- parameter start (props: required) -->

timezone

String

有効期間の基準となるタイムゾーン。\
以下のいずれかの値を指定します。

- `ETC_GMT_MINUS_12`：（UTC-12:00） Etc/GMT-12
- `ETC_GMT_MINUS_11`：（UTC-11:00） Etc/GMT-11
- `PACIFIC_HONOLULU`：（UTC-10:00） Pacific/Honolulu
- `AMERICA_ANCHORAGE`：（UTC-09:00） America/Anchorage
- `AMERICA_LOS_ANGELES`：（UTC-08:00） America/Los_Angeles, Santa_Isabel
- `AMERICA_PHOENIX`：（UTC-07:00） America/Phoenix, Denver
- `AMERICA_CHICAGO`：（UTC-06:00） America/Chicago, Guatemala
- `AMERICA_NEW_YORK`：（UTC-05:00） America/New_York, Indiana/Indianapolis
- `AMERICA_CARACAS`：（UTC-04:30） America/Caracas
- `AMERICA_SANTIAGO`：（UTC-04:00） America/Santiago, Cuiaba
- `AMERICA_ST_JOHNS`：（UTC-03:30） America/St_Johns
- `AMERICA_SAO_PAULO`：（UTC-03:00） America/Sao_Paulo, Argentina/Buenos_Aires
- `ETC_GMT_MINUS_2`：（UTC-02:00） Etc/GMT-2
- `ATLANTIC_CAPE_VERDE`：（UTC-01:00） Atlantic/Cape_Verde, Azores
- `EUROPE_LONDON`：（UTC+00:00） Europe/London, Etc/GMT
- `EUROPE_PARIS`：（UTC+01:00） Europe/Paris, Berlin
- `EUROPE_ISTANBUL`：（UTC+02:00） Europe/Istanbul, Kiev
- `EUROPE_MOSCOW`：（UTC+03:00） Europe/Moscow, Minsk
- `ASIA_TEHRAN`：（UTC+03:30） Asia/Tehran
- `ASIA_TBILISI`：（UTC+04:00） Asia/Tbilisi, Yerevan
- `ASIA_KABUL`：（UTC+04:30） Asia/Kabul
- `ASIA_TASHKENT`：（UTC+05:00） Asia/Tashkent, Karachi
- `ASIA_COLOMBO`：（UTC+05:30） Asia/Colombo, Kolkata
- `ASIA_KATHMANDU`：（UTC+05:45） Asia/Kathmandu
- `ASIA_ALMATY`：（UTC+06:00） Asia/Almaty, Dhaka
- `ASIA_RANGOON`：（UTC+06:30） Asia/Rangoon
- `ASIA_BANGKOK`：（UTC+07:00） Asia/Bangkok, Jakarta
- `ASIA_TAIPEI`：（UTC+08:00） Asia/Taipei, Singapore
- `ASIA_TOKYO`：（UTC+09:00） Asia/Tokyo, Seoul
- `AUSTRALIA_DARWIN`：（UTC+09:30） Australia/Darwin, Adelaide
- `AUSTRALIA_SYDNEY`：（UTC+10:00） Australia/Sydney, Brisbane
- `ASIA_VLADIVOSTOK`：（UTC+11:00） Asia/Vladivostok, Pacific/Guadalcanal
- `ETC_GMT_PLUS_12`：（UTC+12:00） Etc/GMT+12
- `PACIFIC_TONGATAPU`：（UTC+13:00） Pacific/Tongatapu, Apia

<!-- parameter end -->
<!-- parameter start (props: required) -->

reward

Object

クーポンタイプの情報を含む[リワードオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#create-coupon-reward-object)。

<!-- parameter end -->
<!-- parameter start (props: required) -->

visibility

String

クーポンのLINEヤフーサービスへの掲載。\
以下のいずれかの値を指定します。

- `PUBLIC`：掲載する。
- `UNLISTED`：掲載しない。

詳しくは、『LINEヤフー for Business』の「[クーポンのLINEヤフーサービスへの掲載](https://www.lycbiz.com/jp/manual/OfficialAccountManager/coupons-service/)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

imageUrl

String

クーポンの画像のURL。\
最大文字数：2000\
プロトコル：HTTPS（TLS 1.2以降）\
画像フォーマット：JPEGまたはPNG\
最大ファイルサイズ：10MB（1MB以下推奨）

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- note start -->

**URLの画像を後から変更してもクーポンの画像は更新されません**

URLの画像は、クーポン作成時に取得されて、LINEプラットフォームに保存されます。URLの画像を後から変更しても、クーポンで表示される画像は更新されません。

<!-- note end -->

<!-- parameter end -->
<!-- parameter start (props: optional) -->

couponCode

String

クーポンの開封後に表示されるクーポンコード。\
最大文字数：16

<!-- parameter end -->
<!-- parameter start (props: optional) -->

barcodeImageUrl

String

クーポン開封後に表示されるバーコード画像のURL。\
最大文字数：2000\
プロトコル：HTTPS（TLS 1.2以降）\
画像フォーマット：JPEGまたはPNG\
最大ファイルサイズ：10MB

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- note start -->

**URLの画像を後から変更してもクーポンの画像は更新されません**

URLの画像は、クーポン作成時に取得されて、LINEプラットフォームに保存されます。URLの画像を後から変更しても、クーポンで表示される画像は更新されません。

<!-- note end -->

<!-- parameter end -->
<!-- parameter start (props: optional) -->

usageCondition

String

クーポンの利用条件。\
最大文字数：100

<!-- parameter end -->

##### リワードオブジェクト 

<!-- parameter start (props: required) -->

type

String

クーポンタイプ。\
以下のいずれかの値を指定します。

- `discount`：割引
- `free`：無料
- `gift`：プレゼント
- `cashBack`：キャッシュバック
- `others`：その他

<!-- parameter end -->
<!-- parameter start (props: optional) -->

priceInfo

Object

割引やキャッシュバックの詳細を含むオブジェクト。\
`type`が`discount`および`cashBack`の場合は必須です。

<!-- parameter end -->
<!-- parameter start (props: required) -->

priceInfo.type

String

クーポンの割引の詳細のタイプ。

`type`が`discount`の場合は、以下のいずれかの値を指定できます。

- `fixed`：値引きの金額を表示
- `percentage`：値引きのパーセンテージを表示
- `explicit`：元の価格を打ち消して値引き後の価格を表示

`type`が`cashBack`の場合は、以下のいずれかの値を指定できます。

- `fixed`：キャッシュバックの金額を表示
- `percentage`：キャッシュバックのパーセンテージを表示

<!-- parameter end -->
<!-- parameter start (props: optional) -->

priceInfo.fixedAmount

Number

値引きの金額を正の整数で指定します。\
`priceInfo.type`が`fixed`の場合は必須です。\
通貨単位は、LINE公式アカウントの国や地域に基づいて自動的に設定されます。

- 台湾：TWD（台湾ドル）
- タイ：THB（タイバーツ）
- 上記以外のすべての国や地域：JPY（日本円）

<!-- parameter end -->
<!-- parameter start (props: optional) -->

priceInfo.percentage

Number

割引率（%）を1〜99の整数で指定します。\
たとえば、50を指定したときの割引率は50%となります。\
`priceInfo.type`が`percentage`の場合は必須です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

priceInfo.originalPrice

Number

割引前の価格を正の整数で指定します。\
`priceInfo.type`が`explicit`の場合は必須です。\
通貨単位は、LINE公式アカウントの国や地域に基づいて自動的に設定されます。

- 台湾：TWD（台湾ドル）
- タイ：THB（タイバーツ）
- 上記以外のすべての国や地域：JPY（日本円）

<!-- parameter end -->
<!-- parameter start (props: optional) -->

priceInfo.priceAfterDiscount

Number

割引後の価格を正の整数で指定します。\
`priceInfo.type`が`explicit`の場合は必須です。\
通貨単位は、LINE公式アカウントの国や地域に基づいて自動的に設定されます。

- 台湾：TWD（台湾ドル）
- タイ：THB（タイバーツ）
- 上記以外のすべての国や地域：JPY（日本円）

<!-- parameter end -->

_リワードオブジェクトの例_

<!-- tab start `json` -->

```json
// 1,500円割引
{
  "type": "discount",
  "priceInfo": {
    "type": "fixed",
    "fixedAmount": 1500
  }
}

// 25%割引
{
  "type": "discount",
  "priceInfo": {
    "type": "percentage",
    "percentage": 25
  }
}

// 12,000円を打ち消して値引き後の9,500円を表示
{
  "type": "discount",
  "priceInfo": {
    "type": "explicit",
    "originalPrice": 12000,
    "priceAfterDiscount": 9500
  }
}

// 無料
{
  "type": "free"
}

// プレゼント
{
  "type": "gift"
}

// 100円キャッシュバック
{
  "type": "cashBack",
  "priceInfo": {
    "type": "fixed",
    "fixedAmount": 100
  }
}

// 30%キャッシュバック
{
  "type": "cashBack",
  "priceInfo": {
    "type": "percentage",
    "percentage": 30
  }
}

// その他
{
  "type": "others"
}
```

<!-- tab end -->

#### レスポンス 

ステータスコード`200`と以下のプロパティを含むJSONオブジェクトを返します。

<!-- parameter start -->

couponId

String

クーポンのID。クーポンをメッセージで送る際などに使用します。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "couponId": "01JYNW8JMQVFBNWF1APF8Z3FS7"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | クーポンを作成できませんでした。次のような理由が考えられます。<ul><li>無効なクーポンタイプが指定されている。</li><li>有効なクーポンの数が上限（最大5,000件）に達した。</li><li>リワードオブジェクトで`priceInfo.type`と一致しないプロパティが指定されている。</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// クーポン名の文字数が60文字を超えている場合
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Size must be between 1 and 60",
      "property": "title"
    }
  ]
}

// 無効なクーポンタイプを指定した場合
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Must be one of the following values: [discount,free,gift,cashBack,others]",
      "property": "reward.type"
    }
  ]
}

// 有効なクーポンの数が上限を超えた場合
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "You have too many coupons created.",
      "property": ""
    }
  ]
}

// リワードオブジェクトでpriceInfo.typeがpercentageなのにfixedAmountが指定されていた場合
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Must not be specified",
      "property": "reward.priceInfo.fixedAmount"
    }
  ]
}
```

<!-- tab end -->

### クーポンを終了する 

Endpoint: `PUT` `https://api.line.me/v2/bot/coupon/{couponId}/close`

指定したクーポンを終了するAPIです。

クーポンを終了させると、すでにクーポンをメッセージとして受信していたユーザーがクーポンを獲得できなくなると共に、そのクーポンを獲得済みのユーザーも利用できなくなります。

終了したクーポンを再び有効にすることはできません。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X PUT https://api.line.me/v2/bot/coupon/01JYNW8JMQVFBNWF1APF8Z3FS7/close \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json'
```

<!-- tab end -->

#### レート制限 

200リクエスト/秒

[LINE Official Account Manager](https://developers.line.biz/ja/glossary/#line-oa-manager)を使ってクーポンを終了する場合は制限の対象外です。

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

couponId

String

終了するクーポンのクーポンID。

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

| コード | 説明                                                       |
| ------ | ---------------------------------------------------------- |
| `410`  | すでに終了しているクーポンのクーポンIDが指定されています。 |
| `404`  | 指定したクーポンが存在しません。                           |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// すでに終了しているクーポンを指定した場合（410 Gone）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "The coupon has already been closed.",
      "property": ""
    }
  ]
}

// 存在しないクーポンを指定した場合（404 Not Found）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "coupon not found",
      "property": ""
    }
  ]
}
```

<!-- tab end -->

### クーポンの一覧を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/coupon`

クーポンの一覧（クーポンIDとクーポン名）を取得するAPIです。有効なクーポンのみ、あるいは終了したクーポンのみを取得することもできます。

このクーポンの一覧には、Messaging APIで作成したクーポンだけでなく、[LINE Official Account Manager](https://manager.line.biz/)で作成したクーポンも含まれており、同じ一覧がLINE Official Account Managerでも確認できます。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/coupon \
-H 'Authorization: Bearer {channel access token}'
-d 'limit=100' \
-d 'status=DRAFT,RUNNING' \
-G
```

<!-- tab end -->

#### レート制限 

200リクエスト/秒

[LINE Official Account Manager](https://developers.line.biz/ja/glossary/#line-oa-manager)を使ってクーポンの一覧を確認する場合は制限の対象外です。

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: optional) -->

limit

Number

1回のリクエストで取得するクーポンの最大数。デフォルト値は`20`です。\
最大値：`100`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

start

String

継続トークンの値。[レスポンス](https://developers.line.biz/ja/reference/messaging-api/#get-coupons-list-response)で返されるJSONオブジェクトの`next`プロパティに含まれます。1回のリクエストでクーポンをすべて取得できない場合は、このパラメータを指定して残りのクーポンを取得します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

status

取得するクーポンのステータス。省略した場合は、すべてのステータスのクーポンを取得対象とします。

- `DRAFT`：下書き保存されたクーポン。
- `RUNNING`：有効期間前、または有効期間中のクーポン。
- `CLOSED`：期限切れ、または終了したクーポン。

複数のパラメータを指定した場合、OR条件となります。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下のプロパティを含むJSONオブジェクトを返します。

<!-- parameter start -->

items

Array of objects

クーポンを表すオブジェクトの配列。\
最大数：`limit`で指定した数

<!-- parameter end -->
<!-- parameter start -->

items\[].couponId

String

クーポンID。

<!-- parameter end -->
<!-- parameter start -->

items\[].title

String

クーポン名。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

next

String

継続トークン。次のクーポンを取得するために使用します。このプロパティは、レスポンスの`items`プロパティで取得しきれなかったクーポンがある場合にのみ返されます。

継続トークンの有効期間は24時間（86,400秒間）です。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
// すべてのクーポンが取得できた場合
{
  "items": [
    {
      "couponId": "01JZMWQ9HMDW9ENJP4C167CXP8",
      "title": "年末年始クーポン"
    },
    {
      "couponId": "01JZA9NPPFDJ3RFG8NA9DJ0NQT",
      "title": "友だち限定クーポン"
    }
  ]
}

// 取得しきれなかったクーポンがまだある場合
{
  "next": "MTAwMDU3MjAxOjE3NTI1Njk5NDU2MjE6WXBPRHo1N3VjL3hPMkcxVEZPVGY1eW9YS3BqL2R2TGVEdit2V3J0ckczVT0=",
  "items": [
    {
      "couponId": "01JZMWQ9HMDW9ENJP4C167CXP8",
      "title": "年末年始クーポン"
    },
    {
      "couponId": "01JZA9NPPFDJ3RFG8NA9DJ0NQT",
      "title": "友だち限定クーポン"
    }
  ]
}

// 該当するクーポンがなかった場合
{
  "items": []
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | クーポンの一覧を取得できませんでした。次のような理由が考えられます。<ul><li>無効なステータスが指定されている。</li><li>取得するクーポンの最大値が100を越えている。</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なステータスを指定した場合（400 Bad Request）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Must be one of the following values: [DRAFT,RUNNING,CLOSED]",
      "property": "status"
    }
  ]
}

// 取得するクーポンの最大値が100を超えていた場合
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Must be less than or equal to 100",
      "property": "limit"
    }
  ]
}
```

<!-- tab end -->

### クーポンの詳細を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/coupon/{couponId}`

指定したクーポンの詳細情報を取得するAPIです。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/coupon/01JYNW8JMQVFBNWF1APF8Z3FS7 \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

200リクエスト/秒

[LINE Official Account Manager](https://developers.line.biz/ja/glossary/#line-oa-manager)を使ってクーポンの詳細を確認する場合は制限の対象外です。

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

couponId

String

詳細を取得するクーポンのクーポンID。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下のプロパティを含むJSONオブジェクトを返します。

<!-- parameter start -->

couponId

String

クーポンのクーポンID。

<!-- parameter end -->
<!-- parameter start -->

title

String

クーポンのクーポン名。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

description

String

クーポンの利用ガイド。

<!-- parameter end -->
<!-- parameter start -->

acquisitionCondition

Object

クーポンの獲得条件を含むオブジェクト。

<!-- parameter end -->
<!-- parameter start -->

acquisitionCondition.type

String

クーポンの獲得条件のタイプ。\
以下のいずれかの値が含まれます。

- `normal`：条件なし。すべてのユーザーが獲得できる。
- `lottery`：抽選。抽選で当選したユーザーのみが獲得できる。
- `referral`：友だち紹介。クーポンを紹介したユーザーと、紹介されたユーザーの両方が獲得できる。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

acquisitionCondition.lotteryProbability

Number

クーポンの当選確率（％）。1〜99の整数です。\
`acquisitionCondition.type`が`lottery`の場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

acquisitionCondition.maxAcquireCount

Number

当選者数の上限。1〜999999の整数。\
上限なしの場合は`-1`です。\
`acquisitionCondition.type`が`lottery`の場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start -->

maxUseCountPerTicket

Number

クーポンの使用可能回数。\
以下のいずれかの値が含まれます。

- `1`：1回のみ
- `-1`：上限なし

<!-- parameter end -->
<!-- parameter start -->

maxTicketPerUser

Number

クーポンの獲得可能枚数。\
`acquisitionCondition.type`が`referral`の場合のみ、1〜30の整数。それ以外の場合は、`1`です。

<!-- parameter end -->
<!-- parameter start -->

startTimestamp

Number

クーポンの有効期間の開始日時。UNIX時間（秒）です。

<!-- parameter end -->
<!-- parameter start -->

endTimestamp

Number

クーポンの有効期間の終了日時。UNIX時間（秒）です。

<!-- parameter end -->
<!-- parameter start -->

timezone

String

有効期間の基準となるタイムゾーン。\
以下のいずれかの値が含まれます。

- `ETC_GMT_MINUS_12`：（UTC-12:00） Etc/GMT-12
- `ETC_GMT_MINUS_11`：（UTC-11:00） Etc/GMT-11
- `PACIFIC_HONOLULU`：（UTC-10:00） Pacific/Honolulu
- `AMERICA_ANCHORAGE`：（UTC-09:00） America/Anchorage
- `AMERICA_LOS_ANGELES`：（UTC-08:00） America/Los_Angeles, Santa_Isabel
- `AMERICA_PHOENIX`：（UTC-07:00） America/Phoenix, Denver
- `AMERICA_CHICAGO`：（UTC-06:00） America/Chicago, Guatemala
- `AMERICA_NEW_YORK`：（UTC-05:00） America/New_York, Indiana/Indianapolis
- `AMERICA_CARACAS`：（UTC-04:30） America/Caracas
- `AMERICA_SANTIAGO`：（UTC-04:00） America/Santiago, Cuiaba
- `AMERICA_ST_JOHNS`：（UTC-03:30） America/St_Johns
- `AMERICA_SAO_PAULO`：（UTC-03:00） America/Sao_Paulo, Argentina/Buenos_Aires
- `ETC_GMT_MINUS_2`：（UTC-02:00） Etc/GMT-2
- `ATLANTIC_CAPE_VERDE`：（UTC-01:00） Atlantic/Cape_Verde, Azores
- `EUROPE_LONDON`：（UTC+00:00） Europe/London, Etc/GMT
- `EUROPE_PARIS`：（UTC+01:00） Europe/Paris, Berlin
- `EUROPE_ISTANBUL`：（UTC+02:00） Europe/Istanbul, Kiev
- `EUROPE_MOSCOW`：（UTC+03:00） Europe/Moscow, Minsk
- `ASIA_TEHRAN`：（UTC+03:30） Asia/Tehran
- `ASIA_TBILISI`：（UTC+04:00） Asia/Tbilisi, Yerevan
- `ASIA_KABUL`：（UTC+04:30） Asia/Kabul
- `ASIA_TASHKENT`：（UTC+05:00） Asia/Tashkent, Karachi
- `ASIA_COLOMBO`：（UTC+05:30） Asia/Colombo, Kolkata
- `ASIA_KATHMANDU`：（UTC+05:45） Asia/Kathmandu
- `ASIA_ALMATY`：（UTC+06:00） Asia/Almaty, Dhaka
- `ASIA_RANGOON`：（UTC+06:30） Asia/Rangoon
- `ASIA_BANGKOK`：（UTC+07:00） Asia/Bangkok, Jakarta
- `ASIA_TAIPEI`：（UTC+08:00） Asia/Taipei, Singapore
- `ASIA_TOKYO`：（UTC+09:00） Asia/Tokyo, Seoul
- `AUSTRALIA_DARWIN`：（UTC+09:30） Australia/Darwin, Adelaide
- `AUSTRALIA_SYDNEY`：（UTC+10:00） Australia/Sydney, Brisbane
- `ASIA_VLADIVOSTOK`：（UTC+11:00） Asia/Vladivostok, Pacific/Guadalcanal
- `ETC_GMT_PLUS_12`：（UTC+12:00） Etc/GMT+12
- `PACIFIC_TONGATAPU`：（UTC+13:00） Pacific/Tongatapu, Apia

<!-- parameter end -->
<!-- parameter start -->

reward

Object

クーポンタイプの情報を含む[リワードオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#get-coupon-reward-object)。

<!-- parameter end -->
<!-- parameter start -->

visibility

String

クーポンのLINEヤフーサービスへの掲載。\
以下のいずれかの値が含まれます。

- `PUBLIC`：掲載する。
- `UNLISTED`：掲載しない。

詳しくは、『LINEヤフー for Business』の「[クーポンのLINEヤフーサービスへの掲載](https://www.lycbiz.com/jp/manual/OfficialAccountManager/coupons-service/)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

imageUrl

String

クーポンの画像のURL。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

couponCode

String

クーポンの開封後に表示されるクーポンコード。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

barcodeImageUrl

String

クーポン開封後に表示されるバーコード画像のURL。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

usageCondition

String

クーポンの利用条件。

<!-- parameter end -->
<!-- parameter start -->

status

クーポンのステータス。

- `DRAFT`：下書き保存されたクーポン。
- `RUNNING`：有効期間前、または有効期間中のクーポン。
- `CLOSED`：期限切れ、または終了したクーポン。

<!-- parameter end -->
<!-- parameter start -->

createdTimestamp

Number

クーポンの作成日時。UNIX時間（秒）です。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "couponId": "01K0B456W5Y6SBD3YH74YM6QE6",
  "title": "友だち限定クーポン",
  "description": "- クーポンを使用するには、この画面をスタッフに提示してください。\n- 使用済みのクーポンはご利用になれません。また、お客さまの操作で誤って「使用済み」にしてしまった場合も利用できなくなります。\n- 本クーポンは有効期間に関わらず、予告なく変更されたり、終了したりする場合があります。",
  "acquisitionCondition": {
    "type": "lottery",
    "lotteryProbability": 50,
    "maxAcquireCount": -1
  },
  "startTimestamp": 1752678000,
  "endTimestamp": 1924959540,
  "timezone": "ASIA_TOKYO",
  "couponCode": "COUPONCODE123456",
  "maxUseCountPerTicket": 1,
  "maxTicketPerUser": 1,
  "visibility": "UNLISTED",
  "reward": {
    "type": "discount",
    "priceInfo": {
      "type": "fixed",
      "fixedAmount": 100,
      "currency": "JPY"
    }
  },
  "imageUrl": "https://oa-coupon.line-scdn-dev.net/0h9gbUqRVkZkhfLHhXMLYZHwdyaCosWGBAPFR7cD5tZidsTnofYDVfezt-ZAR3YER9OzRfK35XZwR6TH5uYDF2TnJ-cBNyfURpPRl2RSFSXQc0TiJhYCFiXiZ8XXk0",
  "usageCondition": "1,000円以上のお支払いで利用可能",
  "status": "RUNNING",
  "createdTimestamp": 1752720120
}
```

<!-- tab end -->

##### リワードオブジェクト 

<!-- parameter start -->

type

String

クーポンタイプ。\
以下のいずれかの値が含まれます。

- `discount`：割引
- `free`：無料
- `gift`：プレゼント
- `cashBack`：キャッシュバック
- `others`：その他

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

priceInfo

Object

割引やキャッシュバックの詳細を含むオブジェクト。\
`type`が`discount`および`cashBack`の場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start -->

priceInfo.type

String

クーポンの割引の詳細のタイプ。

`type`が`discount`の場合は、以下のいずれかの値が含まれます。

- `fixed`：値引きの金額を表示
- `percentage`：値引きのパーセンテージを表示
- `explicit`：元の価格を打ち消して値引き後の価格を表示

`type`が`cashBack`の場合は、以下のいずれかの値が含まれます。

- `fixed`：キャッシュバックの金額を表示
- `percentage`：キャッシュバックのパーセンテージを表示

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

priceInfo.fixedAmount

Number

値引きの金額。\
`priceInfo.type`が`fixed`の場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

priceInfo.percentage

Number

割引率（％）。\
`priceInfo.type`が`percentage`の場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

priceInfo.originalPrice

Number

割引前の価格。\
`priceInfo.type`が`explicit`の場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

priceInfo.priceAfterDiscount

Number

割引後の価格。\
`priceInfo.type`が`explicit`の場合のみ含まれます。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

priceInfo.currency

Number

通貨単位。LINE公式アカウントの国や地域に基づいて自動的に設定されます。\
`priceInfo.type`が`fixed`または`explicit`の場合のみ含まれます。

- `TWD`：台湾ドル（台湾）
- `THB`：タイバーツ（タイ）
- `JPY`：日本円（上記以外のすべての国や地域）

<!-- parameter end -->

_リワードオブジェクトの例_

<!-- tab start `json` -->

```json
// 1,500円割引
{
  "type": "discount",
  "priceInfo": {
    "type": "fixed",
    "fixedAmount": 1500,
    "currency": "JPY"
  }
}

// 25%割引
{
  "type": "discount",
  "priceInfo": {
    "type": "percentage",
    "percentage": 25
  }
}

// 12,000円を打ち消して値引き後の9,500円を表示
{
  "type": "discount",
  "priceInfo": {
    "type": "explicit",
    "originalPrice": 12000,
    "priceAfterDiscount": 9500,
    "currency": "JPY"
  }
}

// 無料
{
  "type": "free"
}

// プレゼント
{
  "type": "gift"
}

// 100円キャッシュバック
{
  "type": "cashBack",
  "priceInfo": {
    "type": "fixed",
    "fixedAmount": 100,
    "currency": "JPY"
  }
}

// 30%キャッシュバック
{
  "type": "cashBack",
  "priceInfo": {
    "type": "percentage",
    "percentage": 30
  }
}

// その他
{
  "type": "others"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `404` | 指定したクーポンが存在しません。次のような理由が考えられます。<ul><li>他のチャネルで作成したクーポンが指定されている。</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 存在しないクーポンを指定した場合（404 Not Found）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "coupon not found",
      "property": ""
    }
  ]
}
```

<!-- tab end -->

## ユーザー 

LINE公式アカウントを友だち追加したユーザーの情報を取得できます。

<!-- note start -->

**自分のユーザーIDを取得する**

自分のユーザーIDは、[LINE Developersコンソール](https://developers.line.biz/console/)のチャネルの［**チャネル基本設定**］タブにある［**あなたのユーザーID**］で確認できます。LINE Developersコンソールのアクセス権限について詳しくは、『[権限を管理する](https://developers.line.biz/ja/docs/line-developers-console/managing-roles/)』の「[チャネルの権限](https://developers.line.biz/ja/docs/line-developers-console/managing-roles/#roles-for-channel)」を参照してください。開発者が自分自身のユーザーIDを取得するためのAPIはありません。

<!-- note end -->

### プロフィール情報を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/profile/{userId}`

以下のいずれかの条件を満たすユーザーのプロフィール情報を取得できます。

- LINE公式アカウントを友だち追加しているユーザー
- LINE公式アカウントを友だち追加したことはないが、LINE公式アカウントにメッセージを送信したことがあるユーザー（LINE公式アカウントをブロックしているユーザーを除く）

なお取得できる情報はメインプロフィールのみです。ユーザーの[サブプロフィール](https://developers.line.biz/ja/glossary/#subprofile)は取得できません。

<!-- note start -->

**注意**

LINE公式アカウントをブロックしているユーザーのプロフィール情報は取得できません。

<!-- note end -->

<!-- tip start -->

**グループトークや複数人トークのメンバーのプロフィール情報**

グループトークや複数人トークのメンバーのプロフィール情報を取得するには、以下のエンドポイントを利用できます。

- [グループトークのメンバーのプロフィール情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-group-member-profile)
- [複数人トークのメンバーのプロフィールを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-room-member-profile)

<!-- tip end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/profile/{userId} \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

userId

[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)で返されるユーザーID。LINEに表示されるLINE IDは使用しないでください。

<!-- parameter end -->

#### レスポンス 

ユーザーIDが有効な場合、ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

displayName

String

ユーザーの表示名

<!-- parameter end -->
<!-- parameter start -->

userId

String

ユーザーID

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

language

String

ユーザーの言語。[BCP 47](https://www.rfc-editor.org/info/bcp47)言語タグに従った文字列が返されます。ユーザーがLINEのプライバシーポリシーに未同意の場合はレスポンスに含まれません。\
例：`en`（英語）。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

pictureUrl

String

プロフィール画像のURL。スキームはhttpsです。ユーザーがプロフィール画像を設定していない場合はレスポンスに含まれません。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

statusMessage

String

ユーザーのステータスメッセージ。ユーザーがステータスメッセージを設定していない場合はレスポンスに含まれません。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "displayName": "LINE taro",
  "userId": "U4af4980629...",
  "language": "en",
  "pictureUrl": "https://profile.line-scdn.net/ch/v2/p/uf9da5ee2b...",
  "statusMessage": "Hello, LINE!"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | 無効なユーザーIDが指定されています。 |
| `404` | プロフィール情報を取得できませんでした。次のような理由が考えられます。<ul><li>対象のユーザーIDが存在していない。</li><li>ユーザーがプロフィール情報の取得に同意していない。</li><li>ユーザーが対象のLINE公式アカウントを友だち追加していない。</li><li>ユーザーが対象のLINE公式アカウントを友だち追加した後にブロックした。</li></ul>詳しくは、『Messaging APIドキュメント』の「[ユーザーのプロフィール情報取得の同意](https://developers.line.biz/ja/docs/messaging-api/user-consent/)」を参照してください。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// プロフィール情報を取得できなかった場合（404 Not Found）
{
  "message": "Not found"
}
```

<!-- tab end -->

### LINE公式アカウントを友だち追加したユーザーのリストを取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/followers/ids`

<!-- note start -->

**注意**

この機能は認証済アカウントまたは[プレミアムアカウント](https://developers.line.biz/ja/glossary/#premium-account)でのみご利用いただけます。アカウント種別について詳しくは、『LINEヤフー for Business』の「[LINE公式アカウント アカウント種別](https://www.lycbiz.com/jp/service/line-official-account/account-type/)」を参照してください。

<!-- note end -->

LINE公式アカウントを友だち追加したユーザーの、[ユーザーID](https://developers.line.biz/ja/glossary/#user-id)のリストを取得します。

すべてのユーザーIDを取得するには、`next`プロパティが[レスポンス](https://developers.line.biz/ja/reference/messaging-api/#get-follower-ids-response)に含まれなくなるまでリクエストを繰り返す必要があります。レスポンスに含まれる`next`プロパティの値を次のリクエストの`start`に指定し、リクエストを繰り返してください。

#### 取得できるユーザーIDの制限について 

取得したユーザーIDのリストに、以下のユーザーのユーザーIDは含まれません。

- LINEアカウントを削除したユーザー。
- 対象のLINE公式アカウントを友だち追加した後にブロックしたユーザー。
- プロフィール情報の取得に同意していないユーザー。詳しくは、『Messaging APIドキュメント』の「[ユーザーのプロフィール情報取得の同意](https://developers.line.biz/ja/docs/messaging-api/user-consent/)」を参照してください。

そのため、このエンドポイントで取得したユーザーIDの数は、LINE公式アカウントのビジネスプロフィールや[LINE Official Account Manager](https://manager.line.biz/)に表示される友だち数と一致しない場合があります。

<!-- note start -->

**取得したユーザーIDは使用できない場合があります**

このエンドポイントで取得したユーザーIDに対してメッセージを送信しても、ユーザーの操作が原因でメッセージが送信できない場合があります。主な原因は以下のとおりです。

- ユーザーIDを取得してからメッセージを送信するまでの間に、ユーザーが対象のLINE公式アカウントをブロックした。
- ユーザーが対象のLINE公式アカウントを友だち追加した後に、[LINEアカウントを削除](https://guide.line.me/ja/account-and-settings/account-and-profile/line-account-delete.html)した。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/followers/ids \
-H 'Authorization: Bearer {channel access token}' \
-d 'limit=1000' \
-d 'start=yANU9IA...' \
-G
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: optional) -->

limit

Number

1回のリクエストで取得するユーザーIDの最大数。デフォルト値は`300`です。\
最大値：`1000`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

start

String

継続トークンの値。[レスポンス](https://developers.line.biz/ja/reference/messaging-api/#get-follower-ids-response)で返されるJSONオブジェクトの`next`プロパティに含まれます。1回のリクエストでユーザーIDをすべて取得できない場合は、このパラメータを指定して残りのユーザーIDを取得します。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下のプロパティを含むJSONオブジェクトを返します。

<!-- parameter start -->

userIds

Array of strings

LINE公式アカウントを友だち追加したユーザーのユーザーIDを示す文字列の配列です。[取得できるユーザーIDに制限](https://developers.line.biz/ja/reference/messaging-api/#get-follower-ids-obtainable-ids)があるため、`userIds`プロパティに含まれるユーザーIDの数は、`next`プロパティが返される場合でも、必ず`limit`で指定した最大数になるとは限りません。\
ユーザーIDの最大数：`limit`で指定した数

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

next

String

継続トークン。次のユーザーIDを取得するために使用します。このプロパティは、前回までのレスポンスの`userIds`プロパティで取得しきれなかったユーザーIDがある場合にのみ返されます。

継続トークンの有効期間は24時間（86,400秒間）です。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "userIds": ["U4af4980629...", "U0c229f96c4...", "U95afb1d4df..."],
  "next": "yANU9IA..."
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | 無効な継続トークンが指定されています。 |
| `403` | このエンドポイントを使う権限がありません。認証済アカウントまたは[プレミアムアカウント](https://developers.line.biz/ja/glossary/#premium-account)でのみご利用いただけます。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 有効期限切れなどの無効な継続トークンを指定した場合（400 Bad Request）
{
  "message": "Invalid start param"
}
```

<!-- tab end -->

## メンバーシップ 

LINE公式アカウントのメンバーシップの情報を取得できます。詳しくは、『Messaging APIドキュメント』の「[メンバーシップ機能を使う](https://developers.line.biz/ja/docs/messaging-api/use-membership-features/)」を参照してください。

### ユーザーのメンバーシップ加入状況を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/membership/subscription/{userId}`

ユーザーが加入しているメンバーシップの情報を取得できます。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/membership/subscription/{userId} \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

200リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

userId

メンバーシップ加入状況を確認したいユーザーのユーザーID。

ユーザーIDの取得方法については、『Messaging APIドキュメント』の「[ユーザーIDを取得する](https://developers.line.biz/ja/docs/messaging-api/getting-user-ids/)」を参照してください。

<!-- parameter end -->

#### レスポンス 

ユーザーがメンバーシップに加入している場合、ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

subscriptions

Array

メンバーシップの配列。

<!-- parameter end -->
<!-- parameter start -->

membership

Object

メンバーシッププランの情報を含むオブジェクト。

<!-- parameter end -->
<!-- parameter start -->

membership.membershipId

Number

メンバーシッププランのID。

<!-- parameter end -->
<!-- parameter start -->

membership.title

String

メンバーシッププランのプラン名。

<!-- parameter end -->
<!-- parameter start -->

membership.description

String

メンバーシッププランの説明。

<!-- parameter end -->
<!-- parameter start -->

membership.benefits

Array of strings

メンバーシッププランの特典のリスト。\
特典の最大数：5

<!-- parameter end -->
<!-- parameter start -->

membership.price

Number

メンバーシッププランの月額。（例：`1500.00`）

<!-- parameter end -->
<!-- parameter start -->

membership.currency

String

`membership.price`の通貨。以下のいずれかの値です。

- `JPY`：日本円
- `TWD`：台湾ドル
- `THB`：タイバーツ

<!-- parameter end -->
<!-- parameter start -->

user

Object

ユーザーのメンバーシップ加入情報を含むオブジェクト。

<!-- parameter end -->
<!-- parameter start -->

user.membershipNo

Number

メンバーシッププランにおけるユーザーのメンバー番号。

<!-- parameter end -->
<!-- parameter start -->

user.joinedTime

Number

ユーザーがメンバーシップに加入した時刻。UNIX時間（秒）で返されます。

<!-- parameter end -->
<!-- parameter start -->

user.nextBillingDate

String

メンバーシッププランの次回更新日。

- フォーマット：`yyyy-MM-dd`（例：`2024-02-08`）
- タイムゾーン：UTC+9

<!-- parameter end -->
<!-- parameter start -->

user.totalSubscriptionMonths

Number

メンバーシッププランに加入している月単位の期間。ユーザーが過去に同一のメンバーシッププランを解約して、再加入した場合、再加入後の期間のみがカウントされます。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "subscriptions": [
    {
      "membership": {
        "membershipId": 3189,
        "title": "ベーシックプラン",
        "description": "毎週土曜にメッセージとフォトが届きます。",
        "benefits": ["メンバー限定メッセージ", "メンバー限定フォト"],
        "price": 500.00,
        "currency": "JPY"
      },
      "user": {
        "membershipNo": 1,
        "joinedTime": 1707214784,
        "nextBillingDate": "2024-02-08",
        "totalSubscriptionMonths": 1
      }
    }
  ]
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | 無効なユーザーIDが指定されています。 |
| `404` | ユーザーが加入しているメンバーシップの情報が取得できませんでした。次のような理由が考えられます。<ul><li>ユーザーがメンバーシップに加入していない</li><li>対象のユーザーIDが存在していない</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なユーザーIDが指定されていた場合（400 Bad Request）
{
  "message": "The value for the 'userId' parameter is invalid"
}

// ユーザーがメンバーシップに加入していなかった場合（404 Not Found）
{
  "message": "Not found"
}
```

<!-- tab end -->

### メンバーシップに加入しているユーザーの一覧を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/membership/{membershipId}/users/ids`

LINE公式アカウントのメンバーシップに加入しているユーザーのユーザーIDの一覧を取得できます。

#### 取得できるユーザーIDに関する制限 

ユーザーがメンバーシップに加入している場合でも、以下のいずれかの条件を満たす場合は、そのユーザーのユーザーIDは一覧に含まれません。

- ユーザーがLINEアカウントを削除している。
- ユーザーがLINE公式アカウントをブロックしている。
- ユーザーがLINE公式アカウントを友だち追加していない。
- ユーザーがプロフィール情報の取得に同意していない。詳しくは、『Messaging APIドキュメント』の「[ユーザーのプロフィール情報取得の同意](https://developers.line.biz/ja/docs/messaging-api/user-consent/)」を参照してください。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/membership/{membershipId}/users/ids \
-H 'Authorization: Bearer {channel access token}' \
-d 'limit={limit}' \
-d 'start={start}' \
-G
```

<!-- tab end -->

#### レート制限 

200リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

membershipId

メンバーシップのID。

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: optional) -->

limit

Number

1回のリクエストで取得するユーザーIDの最大数。デフォルト値は`300`です。\
最大値：`1000`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

start

継続トークンの値。[レスポンス](https://developers.line.biz/ja/reference/messaging-api/#get-membership-user-ids-response)で返されるJSONオブジェクトの`next`プロパティに含まれます。1回のリクエストでユーザーIDをすべて取得できない場合は、このパラメータを指定して残りの配列を取得できます。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下のプロパティを含むJSONオブジェクトを返します。

<!-- parameter start -->

userIds

Array of strings

メンバーシップに加入しているユーザーのユーザーIDの配列。ユーザーの状況によってユーザーIDを取得できるかどうかが変わるため、`userIds`プロパティに含まれるユーザーIDの数は、`next`プロパティが返される場合でも、必ず`limit`クエリパラメータで指定した数になるとは限りません。詳しくは、「[取得できるユーザーIDに関する制限](https://developers.line.biz/ja/reference/messaging-api/#get-membership-user-ids-restrictions)」を参照してください。\
ユーザーIDの最大数：`limit`クエリパラメータで指定した数

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

next

String

継続トークン。次のユーザーIDの一覧を取得するために使用します。このプロパティは、前回までのレスポンスの`userIds`プロパティで取得しきれなかったユーザーIDがある場合にのみ返されます。

継続トークンの有効期限は24時間（86,400秒間）です。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "userIds": ["U4af4980629...", "U0c229f96c4...", "U95afb1d4df..."],
  "next": "yANU9IA..."
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>無効な継続トークンを指定している。</li><li>`limit`プロパティに不正な値を指定している。</li></ul> |
| `404` | `membershipId`パスパラメータに存在しないメンバーシップIDを指定しています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// membershipIdパスパラメータに存在しないメンバーシップIDを指定した場合（404 Not Found）
{
  "message": "Membership ID is not found"
}
```

<!-- tab end -->

### 提供中のメンバーシッププランを取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/membership/list`

LINE公式アカウントのメンバーシップで提供中の、メンバーシッププランを取得できます。

審査中のプランや終了後のプランは含まれません。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/membership/list \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

200リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下のプロパティを含むJSONオブジェクトを返します。

<!-- parameter start -->

memberships

Array

提供中のメンバーシッププランの配列です。\
プランの最大数：5

<!-- parameter end -->
<!-- parameter start -->

memberships\[].membershipId

Number

メンバーシッププランのID。

<!-- parameter end -->
<!-- parameter start -->

memberships\[].title

String

メンバーシッププランのプラン名。

<!-- parameter end -->
<!-- parameter start -->

memberships\[].description

String

メンバーシッププランの説明。

<!-- parameter end -->
<!-- parameter start -->

memberships\[].benefits

Array of strings

メンバーシッププランの特典のリスト。\
特典の最大数：5

<!-- parameter end -->
<!-- parameter start -->

memberships\[].price

Number

メンバーシッププランの月額。（例：`1500.00`）

<!-- parameter end -->
<!-- parameter start -->

memberships\[].currency

String

`memberships[].price`の通貨。以下のいずれかの値です。

- `JPY`：日本円
- `TWD`：台湾ドル
- `THB`：タイバーツ

<!-- parameter end -->
<!-- parameter start -->

memberships\[].memberCount

Number

加入しているメンバー数。

<!-- parameter end -->
<!-- parameter start -->

memberships\[].memberLimit

Number

加入できるメンバー数の上限。上限を設定していない場合は`null`になります。

<!-- parameter end -->
<!-- parameter start -->

memberships\[].isInAppPurchase

Boolean

加入ユーザーの支払い方法。

- `true`：App内課金
- `false`：Web決済

<!-- parameter end -->
<!-- parameter start -->

memberships\[].isPublished

Boolean

メンバーシッププランのステータス。

- `true`：公開中
- `false`：非公開（終了手続きを行い、プランが非公開になったが、まだ特典の提供は終了していない状態）

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "memberships": [
    {
      "membershipId": 3189,
      "title": "ベーシックプラン",
      "description": "毎週土曜にメッセージとフォトが届きます。",
      "benefits": ["メンバー限定メッセージ", "メンバー限定フォト"],
      "price": 500.00,
      "currency": "JPY",
      "memberCount": 1,
      "memberLimit": null,
      "isInAppPurchase": true,
      "isPublished": true
    },
    {
      "membershipId": 3213,
      "title": "プレミアムプラン",
      "description": "特別なパーティにご招待します。",
      "benefits": ["メンバー限定パーティー"],
      "price": 1500.00,
      "currency": "JPY",
      "memberCount": 0,
      "memberLimit": null,
      "isInAppPurchase": false,
      "isPublished": true
    }
  ]
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明                                       |
| ------ | ------------------------------------------ |
| `404`  | 提供中のメンバーシッププランがありません。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 提供中のメンバーシッププランがない場合（404 Not Found）
{
  "message": "Membership plan not found"
}
```

<!-- tab end -->

## ボット 

LINE公式アカウントのボットの基本情報を取得できます。

### ボットの情報を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/info`

ボットの基本情報を取得します。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -X GET \
-H 'Authorization: Bearer {channel access token}' \
https://api.line.me/v2/bot/info
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

userId

String

ボットのユーザーID

<!-- parameter end -->
<!-- parameter start -->

basicId

String

ボットのベーシックID

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

premiumId

String

ボットの[プレミアムID](https://developers.line.biz/ja/glossary/#premium-id)。プレミアムIDが未設定の場合、この値は含まれません。

<!-- parameter end -->
<!-- parameter start -->

displayName

String

ボットの表示名

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

pictureUrl

String

プロフィール画像のURL。「https://」から始まる画像URLです。ボットにプロフィール画像を設定していない場合は、レスポンスに含まれません。

<!-- parameter end -->
<!-- parameter start -->

chatMode

String

[LINE Official Account Manager](https://manager.line.biz)のチャットの設定。以下のいずれかの値が返ります。

- `chat`：チャットがオンに設定されています。
- `bot`：チャットがオフに設定されています。

<!-- parameter end -->
<!-- parameter start -->

markAsReadMode

String

メッセージの自動既読設定。チャットを「オフ」にしていれば`auto`、「オン」にしていれば`manual`が返ります。

- `auto`：自動既読設定が有効です。
- `manual`：自動既読設定が無効です。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "userId": "Ub9952f8...",
  "basicId": "@216ru...",
  "displayName": "Example name",
  "pictureUrl": "https://profile.line-scdn.net/0hbGgpkVAb...",
  "chatMode": "chat",
  "markAsReadMode": "manual"
}
```

<!-- tab end -->

#### エラーレスポンス 

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

## グループトーク 

LINE公式アカウントが参加しているグループトークの情報や、グループトークのメンバーの情報を取得できます。

### グループトークの概要を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/group/{groupId}/summary`

LINE公式アカウントが参加しているグループトークのグループID、グループ名、アイコンのURLを取得します。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/group/{groupId}/summary \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

groupId

グループID。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`source`オブジェクトで確認できます。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

groupId

String

グループID

<!-- parameter end -->
<!-- parameter start -->

groupName

String

グループ名

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

pictureUrl

String

グループのアイコンのURL。ユーザーがグループのプロフィール画像を設定していない場合はレスポンスに含まれません。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "groupId": "Ca56f94637c...",
  "groupName": "Group name",
  "pictureUrl": "https://profile.line-scdn.net/abcdefghijklmn"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | 無効なグループIDが指定されています。 |
| `404` | 存在しないグループやLINE公式アカウントが参加していないグループが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なグループIDを指定した場合（400 Bad Request）
{
  "message": "The value for the 'groupId' parameter is invalid"
}

// 存在しないグループやLINE公式アカウントが参加していないグループを指定した場合（404 Not Found）
{
  "message": "Not found"
}
```

<!-- tab end -->

### グループトークに参加しているユーザーの人数を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/group/{groupId}/members/count`

グループトークに参加しているユーザーの人数を取得します。参加しているユーザーが、LINE公式アカウントを友だち追加していない場合や、LINE公式アカウントをブロックしている場合でも、人数に含まれます。

人数に、LINE公式アカウントは含まれません。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/group/{groupId}/members/count \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

groupId

グループID。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`source`オブジェクトで確認できます。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

count

Number

グループトークに参加しているユーザーの人数。人数に、LINE公式アカウントは含まれません。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "count": 3
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | 無効なグループIDが指定されています。 |
| `404` | 存在しないグループやLINE公式アカウントが参加していないグループが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なグループIDを指定した場合（400 Bad Request）
{
  "message": "The value for the 'groupId' parameter is invalid"
}

// 存在しないグループやLINE公式アカウントが参加していないグループを指定した場合（404 Not Found）
{
  "message": "Not found"
}
```

<!-- tab end -->

### グループトークのメンバーのユーザーIDを取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/group/{groupId}/members/ids`

<!-- note start -->

**注意**

この機能は認証済アカウントまたは[プレミアムアカウント](https://developers.line.biz/ja/glossary/#premium-account)でのみご利用いただけます。アカウント種別について詳しくは、『LINEヤフー for Business』の「[LINE公式アカウント アカウント種別](https://www.lycbiz.com/jp/service/line-official-account/account-type/)」を参照してください。

<!-- note end -->

LINE公式アカウントが参加しているグループトークのメンバーの、ユーザーIDを取得するAPIです。LINE公式アカウントを友だちとして追加していないユーザーや、LINE公式アカウントをブロックしているユーザーのユーザーIDも取得します。

<!-- tip start -->

**WebhookからもユーザーIDを取得できます**

ユーザーがグループトークに参加したり、グループトークでメッセージを送ったりすると、ボットサーバーにWebhookが送信されます。WebhookにはユーザーIDが含まれているため、APIリクエストを実行せずにユーザーIDを取得できます。詳しくは、『Messaging APIドキュメント』の「[WebhookからユーザーIDを取得する](https://developers.line.biz/ja/docs/messaging-api/getting-user-ids/#get-user-ids-in-webhook)」を参照してください。

<!-- tip end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET 'https://api.line.me/v2/bot/group/{groupId}/members/ids?start={continuationToken}' \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

groupId

グループID。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`source`オブジェクトで返されます。

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: optional) -->

start

継続トークンの値。[レスポンス](https://developers.line.biz/ja/reference/messaging-api/#get-group-member-user-ids-response)で返されるJSONオブジェクトの`next`プロパティに含まれます。1回のリクエストでユーザーIDをすべて取得できない場合は、このパラメータを指定して残りの配列を取得します。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下のプロパティを含むJSONオブジェクトを返します。

<!-- parameter start -->

memberIds

Array of strings

グループトークのメンバーのユーザーIDのリスト。iOS版LINEまたはAndroid版LINEを使用しているユーザーのみ`memberIds`に含まれます。詳しくは、「[ユーザーのプロフィール情報取得の同意](https://developers.line.biz/ja/docs/messaging-api/user-consent/)」を参照してください。\
最大ユーザー数：100

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

next

String

継続トークン。グループトークのメンバーのユーザーIDの、次の配列を取得するために使用します。このプロパティは、前回までのレスポンスの`memberIds`で取得しきれなかったユーザーIDがある場合にのみ返されます。

継続トークンの有効期間は24時間（86,400秒間）です。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "memberIds": ["U4af4980629...", "U0c229f96c4...", "U95afb1d4df..."],
  "next": "jxEWCEEP..."
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>無効なグループIDを指定している。</li><li>`start`プロパティに無効な継続トークンを指定している。</li></ul> |
| `403` | このエンドポイントを使う権限がありません。認証済アカウントまたは[プレミアムアカウント](https://developers.line.biz/ja/glossary/#premium-account)でのみご利用いただけます。 |
| `404` | 存在しないグループやLINE公式アカウントが参加していないグループが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なグループIDを指定した場合（400 Bad Request）
{
  "message": "The value for the 'groupId' parameter is invalid"
}

// 有効期限切れなどの無効な継続トークンを指定した場合（400 Bad Request）
{
  "message": "Invalid start param"
}

// 存在しないグループやLINE公式アカウントが参加していないグループを指定した場合（404 Not Found）
{
  "message": "Not found"
}
```

<!-- tab end -->

### グループトークのメンバーのプロフィール情報を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/group/{groupId}/member/{userId}`

LINE公式アカウントが参加しているグループトークのメンバーのユーザーIDが既知である場合に、そのメンバーのプロフィール情報を取得するAPIです。

<!-- tip start -->

**ヒント**

LINE公式アカウントを友だちとして追加しているかどうかや、LINE公式アカウントをブロックしているかどうかに関わらず、そのグループトークに参加しているユーザーであればプロフィール情報を取得できます。

<!-- tip end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/group/{groupId}/member/{userId} \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

groupId

グループID。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`source`オブジェクトで返されます。

<!-- parameter end -->
<!-- parameter start (props: required) -->

userId

ユーザーID。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`source`オブジェクトで返されます。LINEに表示されるLINE IDは使用しないでください。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

displayName

String

表示名

<!-- parameter end -->
<!-- parameter start -->

userId

String

ユーザーID

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

pictureUrl

String

プロフィール画像のURL。ユーザーがプロフィール画像を設定していない場合はレスポンスに含まれません。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "displayName": "LINE taro",
  "userId": "U4af4980629...",
  "pictureUrl": "https://sprofile.line-scdn.net/0hHkIRkHJF..."
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>無効なグループIDを指定している。</li><li>無効なユーザーIDを指定している。</li></ul> |
| `404` | プロフィール情報を取得できませんでした。次のような理由が考えられます。<ul><li>存在しないグループやLINE公式アカウントが参加していないグループが指定されています。</li><li>存在しないユーザーやグループに参加していないユーザーが指定されています。</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なグループIDを指定した場合（400 Bad Request）
{
  "message": "The value for the 'groupId' parameter is invalid"
}

// 存在しないグループやユーザー、LINE公式アカウントが参加していないグループなどを指定した場合（404 Not Found）
{
  "message": "Not found"
}
```

<!-- tab end -->

### グループトークから退出する 

Endpoint: `POST` `https://api.line.me/v2/bot/group/{groupId}/leave`

[グループトーク](https://developers.line.biz/ja/docs/messaging-api/group-chats/#group)から退出するAPIです。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/group/{groupId}/leave \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

groupId

グループID。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`source`オブジェクトで返されます。

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
| `400` | 無効なグループIDが指定されています。 |
| `404` | 存在しないグループやLINE公式アカウントが参加していないグループが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なグループIDを指定した場合（400 Bad Request）
{
  "message": "The value for the 'groupId' parameter is invalid"
}

// 存在しないグループやLINE公式アカウントが参加していないグループを指定した場合（404 Not Found）
{
  "message": "Not found"
}
```

<!-- tab end -->

## 複数人トーク 

LINE公式アカウントが参加している複数人トークの情報や、複数人トークのメンバーの情報を取得できます。

### 複数人トークに参加しているユーザーの人数を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/room/{roomId}/members/count`

複数人トークに参加しているユーザーの人数を取得します。参加しているユーザーが、LINE公式アカウントを友だち追加していない場合や、LINE公式アカウントをブロックしている場合でも、人数に含まれます。

人数に、LINE公式アカウントは含まれません。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/room/{roomId}/members/count \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### Path parameters 

<!-- parameter start (props: required) -->

roomId

トークルームID。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`source`オブジェクトで確認できます。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

count

Number

複数人トークに参加しているユーザーの人数。人数に、LINE公式アカウントは含まれません。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "count": 3
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | 無効なトークルームIDが指定されています。 |
| `404` | 存在しない複数人トークやLINE公式アカウントが参加していない複数人トークが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なトークルームIDを指定した場合（400 Bad Request）
{
  "message": "The value for the 'roomId' parameter is invalid"
}

// 存在しない複数人トークやLINE公式アカウントが参加していない複数人トークを指定した場合（404 Not Found）
{
  "message": "Not found"
}
```

<!-- tab end -->

### 複数人トークのメンバーのユーザーIDを取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/room/{roomId}/members/ids`

<!-- note start -->

**注意**

この機能は認証済アカウントまたは[プレミアムアカウント](https://developers.line.biz/ja/glossary/#premium-account)でのみご利用いただけます。アカウント種別について詳しくは、『LINEヤフー for Business』の「[LINE公式アカウント アカウント種別](https://www.lycbiz.com/jp/service/line-official-account/account-type/)」を参照してください。

<!-- note end -->

LINE公式アカウントが参加している複数人トークのメンバーの、ユーザーIDを取得するAPIです。LINE公式アカウントを友だちとして追加していないユーザーや、LINE公式アカウントをブロックしているユーザーのユーザーIDも取得します。

<!-- tip start -->

**WebhookからもユーザーIDを取得できます**

ユーザーが複数人トークに参加したり、複数人トークでメッセージを送ったりすると、ボットサーバーにWebhookが送信されます。WebhookにはユーザーIDが含まれているため、APIリクエストを実行せずにユーザーIDを取得できます。詳しくは、『Messaging APIドキュメント』の「[WebhookからユーザーIDを取得する](https://developers.line.biz/ja/docs/messaging-api/getting-user-ids/#get-user-ids-in-webhook)」を参照してください。

<!-- tip end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET 'https://api.line.me/v2/bot/room/{roomId}/members/ids?start={continuationToken}' \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

roomId

トークルームID。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`source`オブジェクトで返されます。

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: optional) -->

start

継続トークンの値。[レスポンス](https://developers.line.biz/ja/reference/messaging-api/#get-room-member-user-ids-response)で返されるJSONオブジェクトの`next`プロパティに含まれます。1回のリクエストでユーザーIDをすべて取得できない場合は、このパラメータを指定して残りの配列を取得します。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下のプロパティを含むJSONオブジェクトを返します。

<!-- parameter start -->

memberIds

Array of strings

複数人トークのメンバーのユーザーIDのリスト。iOS版LINEまたはAndroid版LINEを使用しているユーザーのみ`memberIds`に含まれます。詳しくは、「[ユーザーのプロフィール情報取得の同意](https://developers.line.biz/ja/docs/messaging-api/user-consent/)」を参照してください。\
最大ユーザー数：100

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

next

String

継続トークン。複数人トークのメンバーのユーザーIDの、次の配列を取得するために使用します。このプロパティは、前回までのレスポンスの`memberIds`で取得しきれなかったユーザーIDがある場合にのみ返されます。

継続トークンの有効期間は24時間（86,400秒間）です。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "memberIds": ["U4af4980629...", "U0c229f96c4...", "U95afb1d4df..."],
  "next": "jxEWCEEP..."
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>無効なトークルームIDを指定している。</li><li>`start`プロパティに無効な継続トークンを指定している。</li></ul> |
| `403` | このエンドポイントを使う権限がありません。認証済アカウントまたは[プレミアムアカウント](https://developers.line.biz/ja/glossary/#premium-account)でのみご利用いただけます。 |
| `404` | 存在しない複数人トークやLINE公式アカウントが参加していない複数人トークが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 有効期限切れなどの無効な継続トークンを指定した場合（400 Bad Request）
{
  "message": "Invalid start param"
}
```

<!-- tab end -->

### 複数人トークのメンバーのプロフィールを取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/room/{roomId}/member/{userId}`

LINE公式アカウントが参加している複数人トークのメンバーのユーザーIDが既知である場合に、そのメンバーのプロフィール情報を取得するAPIです。

<!-- tip start -->

**ヒント**

LINE公式アカウントを友だちとして追加しているかどうかや、LINE公式アカウントをブロックしているかどうかに関わらず、その複数人トークに参加しているユーザーであればプロフィール情報を取得できます。

<!-- tip end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/room/{roomId}/member/{userId} \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

roomId

トークルームID。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`source`オブジェクトで返されます。

<!-- parameter end -->
<!-- parameter start (props: required) -->

userId

ユーザーID。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`source`オブジェクトで返されます。LINEに表示されるLINE IDは使用しないでください。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

displayName

String

表示名

<!-- parameter end -->
<!-- parameter start -->

userId

String

ユーザーID

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

pictureUrl

String

プロフィール画像のURL。ユーザーがプロフィール画像を設定していない場合はレスポンスに含まれません。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "displayName": "LINE taro",
  "userId": "U4af4980629...",
  "pictureUrl": "https://sprofile.line-scdn.net/0hHkIRkHJF..."
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リクエストに問題があります。次のような理由が考えられます。<ul><li>無効なトークルームIDを指定している。</li><li>無効なユーザーIDを指定している。</li></ul> |
| `404` | プロフィール情報を取得できませんでした。次のような理由が考えられます。<ul><li>存在しない複数人トークやLINE公式アカウントが参加していない複数人トークが指定されています。</li><li>存在しないユーザーや複数人トークに参加していないユーザーが指定されています。</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なトークルームIDを指定した場合（400 Bad Request）
{
  "message": "The value for the 'roomId' parameter is invalid"
}

// 存在しない複数人トークやユーザー、LINE公式アカウントが参加していない複数人トークなどを指定した場合（404 Not Found）
{
  "message": "Not found"
}
```

<!-- tab end -->

### 複数人トークから退出する 

Endpoint: `POST` `https://api.line.me/v2/bot/room/{roomId}/leave`

[複数人トーク](https://developers.line.biz/ja/docs/messaging-api/group-chats/#room)から退出するAPIです。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/room/{roomId}/leave \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

roomId

トークルームID。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`source`オブジェクトで返されます。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と空のJSONオブジェクトを返します。

LINE公式アカウントが参加していない複数人トークを指定した場合も、ステータスコード`200`を返します。

_レスポンスの例_

<!-- tab start `json` -->

```json
{}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明                                       |
| ------ | ------------------------------------------ |
| `400`  | 無効なトークルームIDが指定されています。   |
| `404`  | 存在しない複数人トークが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なトークルームIDを指定した場合（400 Bad Request）
{
  "message": "The value for the 'roomId' parameter is invalid"
}

// 存在しない複数人トークを指定した場合（404 Not Found）
{
  "message": "Not found"
}
```

<!-- tab end -->

## リッチメニュー 

LINE公式アカウントのトーク画面に表示される、カスタマイズ可能なメニューです。詳しくは、「[リッチメニューを使う](https://developers.line.biz/ja/docs/messaging-api/using-rich-menus/)」を参照してください。

### リッチメニューを作成する 

Endpoint: `POST` `https://api.line.me/v2/bot/richmenu`

リッチメニューを作成するAPIです。

リッチメニューを表示するには、[リッチメニューの画像をアップロード](https://developers.line.biz/ja/reference/messaging-api/#upload-rich-menu-image)し、さらに[デフォルトのリッチメニューを設定](https://developers.line.biz/ja/reference/messaging-api/#set-default-rich-menu)するか[リッチメニューをユーザーとリンク](https://developers.line.biz/ja/reference/messaging-api/#link-rich-menu-to-user)する必要があります。1つのLINE公式アカウントに対して、Messaging APIを使って最大で1000件のリッチメニューを作成できます。

<!-- tip start -->

**リッチメニューを作成する前に**

[リッチメニューオブジェクトを検証する](https://developers.line.biz/ja/reference/messaging-api/#validate-rich-menu-object)ためのエンドポイントもあります。

<!-- tip end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/richmenu \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d \
'{
    "size": {
      "width": 2500,
      "height": 1686
    },
    "selected": false,
    "name": "Nice rich menu",
    "chatBarText": "Tap to open",
    "areas": [
      {
        "bounds": {
          "x": 0,
          "y": 0,
          "width": 2500,
          "height": 1686
        },
        "action": {
          "type": "postback",
          "data": "action=buy&itemid=123"
        }
      }
   ]
}'
```

<!-- tab end -->

#### レート制限 

100リクエスト/時

[LINE Official Account Manager](https://developers.line.biz/ja/glossary/#line-oa-manager)を使ってリッチメニューを作成・削除する場合は制限の対象外です。

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->

#### リクエストボディ 

リッチメニューとして表示する[リッチメニューオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#rich-menu-object)を指定します。

#### レスポンス 

ステータスコード`200`と以下のプロパティを含むJSONオブジェクトを返します。

<!-- parameter start -->

richMenuId

String

リッチメニューのID。[リッチメニューの画像をアップロードする](https://developers.line.biz/ja/reference/messaging-api/#upload-rich-menu-image)際に使用します。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "richMenuId": "{richMenuId}"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | リッチメニューを作成できませんでした。次のような理由が考えられます。<ul><li>無効なリッチメニューオブジェクトが指定されている。</li><li>作成できるリッチメニューの上限（最大1000件）に達した。</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// リッチメニューオブジェクトのJSONで必須のキーが存在しない場合（400 Bad Request）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "must be specified",
      "property": "name"
    }
  ]
}

// URIアクションに無効なスキームを指定した場合（400 Bad Request）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "invalid uri",
      "property": "areas[0].action.uri"
    }
  ]
}
```

<!-- tab end -->

### リッチメニューオブジェクトを検証する 

Endpoint: `POST` `https://api.line.me/v2/bot/richmenu/validate`

リッチメニューオブジェクトを検証するAPIです。

[リッチメニューオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#rich-menu-object)が、[リッチメニューの作成](https://developers.line.biz/ja/reference/messaging-api/#create-rich-menu)のリクエストボディとして有効かを検証できます。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/richmenu/validate \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d \
'{
    "size": {
      "width": 2500,
      "height": 1686
    },
    "selected": false,
    "name": "Nice rich menu",
    "chatBarText": "Tap to open",
    "areas": [
      {
        "bounds": {
          "x": 0,
          "y": 0,
          "width": 2500,
          "height": 1686
        },
        "action": {
          "type": "postback",
          "data": "action=buy&itemid=123"
        }
      }
   ]
}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->

#### リクエストボディ 

検証したい[リッチメニューオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#rich-menu-object)を指定します。

#### レスポンス 

リクエストボディがリッチメニューオブジェクトとして有効な場合、ステータスコード`200`と空のJSONオブジェクトを返します。

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
| `400` | 無効なリッチメニューオブジェクトが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// リッチメニューオブジェクトのJSONで必須のキーが存在しない場合（400 Bad Request）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "must be specified",
      "property": "name"
    }
  ]
}

// URIアクションに無効なスキームを指定した場合（400 Bad Request）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "invalid uri",
      "property": "areas[0].action.uri"
    }
  ]
}
```

<!-- tab end -->

### リッチメニューの画像をアップロードする 

Endpoint: `POST` `https://api-data.line.me/v2/bot/richmenu/{richMenuId}/content`

<!-- note start -->

**他のエンドポイントとドメイン名が異なります**

このエンドポイントは、Messaging APIにおけるLINEプラットフォームへの大容量データ送受信用のドメイン名（`api-data.line.me`）です。他のエンドポイントのドメイン名（`api.line.me`）とは異なるため、利用時は注意してください。

<!-- note end -->

画像をアップロードしてリッチメニューに設定するAPIです。

#### リッチメニューの画像の要件 

リッチメニューの画像は以下の要件を満たす必要があります。

- 画像フォーマット：JPEGまたはPNG
- 画像の幅サイズ：800ピクセル以上、2500ピクセル以下
- 画像の高さサイズ：250ピクセル以上
- 画像のアスペクト比（幅÷高さ）：1.45以上
- 最大ファイルサイズ：1MB

<!-- note start -->

**注意**

リッチメニューに設定された画像を置き換えることはできません。リッチメニューの画像を更新するには、新しいリッチメニューオブジェクトを作成して、新しい画像をアップロードします。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api-data.line.me/v2/bot/richmenu/{richMenuId}/content \
-H "Authorization: Bearer {channel access token}" \
-H "Content-Type: image/jpeg" \
-T image.jpg
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

`image/jpeg`または`image/png`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

richMenuId

画像を設定するリッチメニューのID

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
| `400` | リッチメニューに画像を設定できませんでした。次のような理由が考えられます。<ul><li>画像が[要件](https://developers.line.biz/ja/reference/messaging-api/#upload-rich-menu-image-requirements)を満たしていない。</li><li>リッチメニューに既に画像が設定されている。</li></ul> |
| `404` | 存在しないリッチメニューが指定されています。 |
| `415` | `Content-Type`にサポートされていないメディア形式が指定されています（`image/jpeg`および`image/png`以外）。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 画像のサイズが要件を満たしていない場合（400 Bad Request）
{
  "message": "The image size is not allowed for richmenu"
}

// リッチメニューに既に画像が設定されている場合（400 Bad Request）
{
  "message": "An image has already been uploaded to the richmenu"
}
```

<!-- tab end -->

### リッチメニューの画像をダウンロードする 

Endpoint: `GET` `https://api-data.line.me/v2/bot/richmenu/{richMenuId}/content`

<!-- note start -->

**他のエンドポイントとドメイン名が異なります**

このエンドポイントは、Messaging APIにおけるLINEプラットフォームへの大容量データ送受信用のドメイン名（`api-data.line.me`）です。他のエンドポイントのドメイン名（`api.line.me`）とは異なるため、利用時は注意してください。

<!-- note end -->

リッチメニューの画像をダウンロードするAPIです。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api-data.line.me/v2/bot/richmenu/{richMenuId}/content \
-H 'Authorization: Bearer {channel access token}' \
-o picture.jpg
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

richMenuId

画像をダウンロードするリッチメニューのID

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`とリッチメニュー画像のバイナリデータを返します。リクエストの例に示すように、画像をダウンロードできます。

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `404` | 画像をダウンロードできませんでした。次のような理由が考えられます。<ul><li>存在しないリッチメニューが指定されている。</li><li>リッチメニューに画像が設定されていない。</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// リッチメニューが存在しない場合（404 Not Found）
{
  "message": "Not found"
}
```

<!-- tab end -->

### リッチメニューの配列を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/richmenu/list`

「[リッチメニューを作成する](https://developers.line.biz/ja/reference/messaging-api/#create-rich-menu)」で作成したすべてのリッチメニューのリッチメニューレスポンスオブジェクトを取得します。

<!-- note start -->

**注意**

LINE Official Account Managerで作成したリッチメニューは取得できません。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/richmenu/list \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下のプロパティを含むJSONオブジェクトを返します。

<!-- parameter start -->

richmenus

Array

[リッチメニューレスポンスオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#rich-menu-response-object)の配列

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "richmenus": [
    {
      "richMenuId": "{richMenuId}",
      "name": "Nice rich menu",
      "size": {
        "width": 2500,
        "height": 1686
      },
      "chatBarText": "Tap to open",
      "selected": false,
      "areas": [
        {
          "bounds": {
            "x": 0,
            "y": 0,
            "width": 2500,
            "height": 1686
          },
          "action": {
            "type": "postback",
            "data": "action=buy&itemid=123"
          }
        }
      ]
    }
  ]
}
```

<!-- tab end -->

#### エラーレスポンス 

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

### リッチメニューを取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/richmenu/{richMenuId}`

IDを指定してリッチメニューを取得するAPIです。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/richmenu/{richMenuId} \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

richMenuId

リッチメニューのID

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と、[リッチメニューレスポンスオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#rich-menu-response-object)を含むJSONレスポンスが返されます。

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "richMenuId": "{richMenuId}",
  "name": "Nice rich menu",
  "size": {
    "width": 2500,
    "height": 1686
  },
  "chatBarText": "Tap to open",
  "selected": false,
  "areas": [
    {
      "bounds": {
        "x": 0,
        "y": 0,
        "width": 2500,
        "height": 1686
      },
      "action": {
        "type": "postback",
        "data": "action=buy&itemid=123"
      }
    }
  ]
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明                                         |
| ------ | -------------------------------------------- |
| `404`  | 存在しないリッチメニューが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 存在しないリッチメニューを指定した場合（404 Not Found）
{
  "message": "Not found"
}
```

<!-- tab end -->

### リッチメニューを削除する 

Endpoint: `DELETE` `https://api.line.me/v2/bot/richmenu/{richMenuId}`

リッチメニューを削除します。

<!-- note start -->

**リッチメニュー数の上限について**

Messaging APIで作成できるリッチメニューの数の上限は、LINE公式アカウントあたり1,000件です。この上限を超過した場合は、新しいリッチメニューを作成する前に既存のリッチメニューを削除する必要があります。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X DELETE https://api.line.me/v2/bot/richmenu/{richMenuId} \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

100リクエスト/時

[LINE Official Account Manager](https://developers.line.biz/ja/glossary/#line-oa-manager)を使ってリッチメニューを作成・削除する場合は制限の対象外です。

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

richMenuId

リッチメニューのID

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

| コード | 説明                                         |
| ------ | -------------------------------------------- |
| `404`  | 存在しないリッチメニューが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 存在しないリッチメニューを指定した場合（404 Not Found）
{
  "message": "Not found"
}
```

<!-- tab end -->

### デフォルトのリッチメニューを設定する 

Endpoint: `POST` `https://api.line.me/v2/bot/user/all/richmenu/{richMenuId}`

デフォルトのリッチメニューを設定するAPIです。デフォルトのリッチメニューは、LINE公式アカウントとのトーク画面を開いたすべてのユーザーに表示されます。すでにデフォルトのリッチメニューが設定されていた場合は、新しく指定したリッチメニューに置き換えられます。

リッチメニューの表示優先順位は高い順に以下のとおりです。

1. [Messaging APIで設定するユーザー単位のリッチメニュー](https://developers.line.biz/ja/reference/messaging-api/#link-rich-menu-to-user)
1. Messaging APIで設定するデフォルトのリッチメニュー
1. [LINE Official Account Managerで設定するデフォルトのリッチメニュー](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/#creating-a-rich-menu-with-the-line-manager)

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/user/all/richmenu/{richMenuId} \
-H "Authorization: Bearer {channel access token}"
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

richMenuId

リッチメニューのID

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

| コード | 説明                                         |
| ------ | -------------------------------------------- |
| `400`  | リッチメニューに画像が設定されていません。   |
| `404`  | 存在しないリッチメニューが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// リッチメニューに画像が設定されていない場合（400 Bad Request）
{
  "message": "must upload richmenu image before applying it to user",
  "details": []
}

// リッチメニューが存在しない場合（404 Not Found）
{
  "message": "Not found"
}
```

<!-- tab end -->

### デフォルトのリッチメニューのIDを取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/user/all/richmenu`

Messaging APIで設定したデフォルトのリッチメニューのIDを取得するAPIです。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/user/all/richmenu \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下のプロパティを含むJSONオブジェクトを返します。

<!-- parameter start -->

richMenuId

String

リッチメニューのID

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "richMenuId": "{richMenuId}"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `403` | [LINE Official Account Manager](https://developers.line.biz/ja/glossary/#line-oa-manager)など、別のチャネルによってデフォルトのリッチメニューが設定されています。 |
| `404` | デフォルトのリッチメニューが設定されていません。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 別のチャネルによってデフォルトのリッチメニューが設定されてる場合（403 Forbidden）
{
  "message": "the richmenu is owned by another channel",
  "details": []
}

// デフォルトのリッチメニューが設定されていない場合（404 Not Found）
{
  "message": "no default richmenu",
  "details": []
}
```

<!-- tab end -->

### デフォルトのリッチメニューを解除する 

Endpoint: `DELETE` `https://api.line.me/v2/bot/user/all/richmenu`

Messaging APIで設定したデフォルトのリッチメニューを解除するAPIです。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X DELETE https://api.line.me/v2/bot/user/all/richmenu \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

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

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

## ユーザー単位のリッチメニュー 

ユーザーIDとリッチメニューのIDを指定することで、リッチメニューをユーザー単位で設定できます。詳しくは、『Messaging APIドキュメント』の「[ユーザー単位のリッチメニューを使う](https://developers.line.biz/ja/docs/messaging-api/use-per-user-rich-menus/)」を参照してください。

### リッチメニューとユーザーをリンクする 

Endpoint: `POST` `https://api.line.me/v2/bot/user/{userId}/richmenu/{richMenuId}`

リッチメニューとユーザーをリンクするAPIです。複数のリッチメニューを1人のユーザーに同時にリンクすることはできません。ユーザーにすでにリッチメニューがリンクされていた場合は、新しく指定したリッチメニューに置き換えられます。

リッチメニューの表示優先順位は高い順に以下のとおりです。

1. Messaging APIで設定するユーザー単位のリッチメニュー
1. [Messaging APIで設定するデフォルトのリッチメニュー](https://developers.line.biz/ja/reference/messaging-api/#set-default-rich-menu)
1. [LINE Official Account Managerで設定するデフォルトのリッチメニュー](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/#creating-a-rich-menu-with-the-line-manager)

#### リッチメニューをリンクできる条件 

リッチメニューは、LINE公式アカウントを友だち追加しているユーザーに対してリンクできます。

なお、以下のユーザーに対してリッチメニューをリンクしようとした場合、ステータスコード`200`が返されますが、実際にはリッチメニューはリンクされません。

- LINEアカウントを削除したユーザー
- LINE公式アカウントをブロックしているユーザー
- LINE公式アカウントを友だち追加していないユーザー
- 他のプロバイダー配下のチャネルで取得したユーザーIDなど、チャネルにユーザーIDが存在しないユーザー

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/user/{userId}/richmenu/{richMenuId} \
-H "Authorization: Bearer {channel access token}"
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

richMenuId

リッチメニューのID

<!-- parameter end -->
<!-- parameter start (props: required) -->

userId

ユーザーID。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`source`オブジェクトで返されます。LINEに表示されるLINE IDは使用しないでください。

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
| `400` | リッチメニューをリンクできませんでした。次のような理由が考えられます。<ul><li>無効なユーザーIDが指定されている。</li><li>リッチメニューに画像が設定されていない。</li></ul> |
| `404` | 存在しないリッチメニューが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

エラーが返された場合、リッチメニューはリンクされません。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なユーザーIDを指定した場合（400 Bad Request）
{
  "message": "The value for the 'userId' parameter is invalid"
}

// リッチメニューが存在しない場合（404 Not Found）
{
  "message": "Not found"
}
```

<!-- tab end -->

### リッチメニューと複数のユーザーをリンクする 

Endpoint: `POST` `https://api.line.me/v2/bot/richmenu/bulk/link`

リッチメニューと複数のユーザーをリンクします。

リッチメニューの表示優先順位は高い順に以下のとおりです。

1. Messaging APIで設定するユーザー単位のリッチメニュー
1. [Messaging APIで設定するデフォルトのリッチメニュー](https://developers.line.biz/ja/reference/messaging-api/#set-default-rich-menu)
1. [LINE Official Accountで設定するデフォルトのリッチメニュー](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/#creating-a-rich-menu-with-the-line-manager)

[リッチメニューと1人のユーザーをリンクする](https://developers.line.biz/ja/reference/messaging-api/#link-rich-menu-to-user)場合と異なり、このエンドポイントのリクエストはバックグラウンドで非同期に処理されます。通常、処理は数秒で完了します。

ステータスコード`202`が返されたとしても、リッチメニューがリンクされていない場合があります。リクエストの処理が成功したかどうかを検証するには、[ユーザーのリッチメニューのIDを取得](https://developers.line.biz/ja/reference/messaging-api/#get-rich-menu-id-of-user)して、リッチメニューがユーザーにリンクされていることを確認します。

なお、[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#bulk-link-rich-menu-error-response)が返された場合は、リッチメニューはどのユーザーにもリンクされません。

#### リッチメニューをリンクできる条件 

リッチメニューは、LINE公式アカウントを友だち追加しているユーザーに対してリンクできます。レスポンスでステータスコード`202`が返された場合、リクエストで指定したユーザーにはリッチメニューがリンクされます。

ステータスコード`202`が返されたとしても、以下のユーザーは対象のLINE公式アカウントと友だちではないため、処理の対象となりません。

- LINEアカウントを削除したユーザー
- LINE公式アカウントをブロックしているユーザー
- LINE公式アカウントを友だち追加していないユーザー
- 他のプロバイダー配下のチャネルで取得したユーザーIDなど、チャネルにユーザーIDが存在しないユーザー

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/richmenu/bulk/link \
-H "Authorization: Bearer {channel access token}" \
-H "Content-Type: application/json" \
-d '{
  "richMenuId":"{richMenuId}",
  "userIds":["{userId1}","{userId2}"]
}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

richMenuId

String

リッチメニューのID

<!-- parameter end -->
<!-- parameter start (props: required) -->

userIds

Array of strings

ユーザーIDの配列。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`source`オブジェクトで返されます。LINEに表示されるLINE IDは使用しないでください。\
最大ユーザーID数：500

<!-- parameter end -->

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
| `400` | リッチメニューをリンクできませんでした。次のような理由が考えられます。<ul><li>無効なユーザーIDが指定されている。</li><li>無効なリッチメニューのIDが指定されている。</li><li>リッチメニューに画像が設定されていない。</li></ul> |
| `404` | 存在しないリッチメニューが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なユーザーIDが含まれていた場合（400 Bad Request）
{
  "message": "The property, 'userIds[0]', in the request body is invalid (line: -, column: -)"
}

// 無効なリッチメニューのIDを指定した場合（400 Bad Request）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "invalid richMenuId",
      "property": "richMenuId"
    }
  ]
}

// リッチメニューが存在しない場合（404 Not Found）
{
    "message": "richmenu not found",
    "details": []
}
```

<!-- tab end -->

### ユーザーのリッチメニューのIDを取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/user/{userId}/richmenu`

ユーザーにリンクされたリッチメニューのIDを取得するAPIです。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/user/{userId}/richmenu \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

userId

ユーザーID。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`source`オブジェクトで返されます。LINEに表示されるLINE IDは使用しないでください。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下のプロパティを含むJSONオブジェクトを返します。

<!-- parameter start -->

richMenuId

String

リッチメニューのID

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "richMenuId": "{richMenuId}"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | 無効なユーザーIDが指定されています。 |
| `404` | リッチメニューのIDを取得できませんでした。次のような理由が考えられます。<ul><li>ユーザーにリッチメニューがリンクされていない。</li><li>存在しないユーザーが指定されている。</li><li>ユーザーが対象のLINE公式アカウントを友だち追加していない</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なユーザーIDを指定した場合（400 Bad Request）
{
  "message": "The value for the 'userId' parameter is invalid"
}

// リッチメニューがリンクされていないユーザーを指定した場合（404 Not Found）
{
  "message": "the user has no richmenu",
  "details": []
}
```

<!-- tab end -->

### リッチメニューとユーザーのリンクを解除する 

Endpoint: `DELETE` `https://api.line.me/v2/bot/user/{userId}/richmenu`

指定したユーザーにリンクされたユーザー単位のリッチメニューを解除するAPIです。

#### リッチメニューのリンクを解除できる条件 

リッチメニューのリンクの解除は、LINE公式アカウントを友だち追加しているユーザーに対して可能です。

なお、以下のユーザーに対してリッチメニューのリンクを解除しようとした場合、ステータスコード`200`が返されますが、実際にはリッチメニューのリンクは解除されません。

- LINEアカウントを削除したユーザー
- LINE公式アカウントをブロックしているユーザー
- LINE公式アカウントを友だち追加していないユーザー
- 他のプロバイダー配下のチャネルで取得したユーザーIDなど、チャネルにユーザーIDが存在しないユーザー

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X DELETE https://api.line.me/v2/bot/user/{userId}/richmenu \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

userId

ユーザーID。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`source`オブジェクトで返されます。LINEに表示されるLINE IDは使用しないでください。

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

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なユーザーIDを指定した場合（400 Bad Request）
{
  "message": "The value for the 'userId' parameter is invalid"
}
```

<!-- tab end -->

### 複数のユーザーのリッチメニューのリンクを解除する 

Endpoint: `POST` `https://api.line.me/v2/bot/richmenu/bulk/unlink`

複数のユーザーのリッチメニューのリンクを解除します。

[リッチメニューと1人のユーザーのリンクを解除する](https://developers.line.biz/ja/reference/messaging-api/#unlink-rich-menu-from-user)場合と異なり、このエンドポイントのリクエストはバックグラウンドで非同期に処理されます。通常、処理は数秒で完了します。

ステータスコード`202`が返されたとしても、リッチメニューのリンクが解除されていない場合があります。リクエストの処理が成功したかどうかを検証するには、[ユーザーのリッチメニューのIDを取得](https://developers.line.biz/ja/reference/messaging-api/#get-rich-menu-id-of-user)して、リンクを解除したはずのリッチメニューがユーザーにリンクされていないことを確認します。

なお、[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#bulk-unlink-rich-menu-error-response)が返された場合は、どのユーザーのリッチメニューのリンクも解除されません。

#### リッチメニューのリンクを解除できる条件 

リッチメニューのリンクの解除は、LINE公式アカウントを友だち追加しているユーザーに対して可能です。レスポンスでステータスコード`202`が返された場合、リクエストで指定したユーザーのリッチメニューのリンクが解除されます。

ステータスコード`202`が返されたとしても、以下のユーザーは対象のLINE公式アカウントと友だちではないため、処理の対象となりません。

- LINEアカウントを削除したユーザー
- LINE公式アカウントをブロックしているユーザー
- LINE公式アカウントを友だち追加していないユーザー
- 他のプロバイダー配下のチャネルで取得したユーザーIDなど、チャネルにユーザーIDが存在しないユーザー

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/richmenu/bulk/unlink \
-H "Authorization: Bearer {channel access token}" \
-H "Content-Type: application/json" \
-d '{
  "userIds":["{userId1}","{userId2}"]
}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

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

userIds

Array of strings

ユーザーIDの配列。[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の`source`オブジェクトで返されます。LINEに表示されるLINE IDは使用しないでください。\
最大ユーザーID数：500

<!-- parameter end -->

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

| コード | 説明                                 |
| ------ | ------------------------------------ |
| `400`  | 無効なユーザーIDが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なユーザーIDが含まれていた場合（400 Bad Request）
{
  "message": "The property, 'userIds[0]', in the request body is invalid (line: -, column: -)"
}
```

<!-- tab end -->

### リンク済みのリッチメニューを一括で置き換え・解除する 

Endpoint: `POST` `https://api.line.me/v2/bot/richmenu/batch`

[リッチメニューとユーザーをリンクする](https://developers.line.biz/ja/reference/messaging-api/#link-rich-menu-to-user)エンドポイントなどを利用して、ユーザーにリンクしたリッチメニューを一括操作するエンドポイントです。このエンドポイントでは、以下のような操作が可能です。

1. 特定のリッチメニューをリンク済みのすべてのユーザーを対象に、リッチメニューを別のリッチメニューに置き換える。
1. 特定のリッチメニューをリンク済みのすべてのユーザーを対象に、リッチメニューのリンクを解除する。
1. リッチメニューをリンク済みのすべてのユーザーを対象に、リッチメニューのリンクを解除する。

また、[リクエストボディ](https://developers.line.biz/ja/reference/messaging-api/#batch-control-rich-menus-of-users-request-body)の`operations`プロパティには、リッチメニューの一括操作を複数指定できます。リッチメニューの一括操作を複数指定した場合、それぞれの操作は独立に並行してユーザーごとに処理されます。指定した操作は互いに影響しません。

たとえば、`operations`プロパティに以下の配列を指定した場合、リクエスト前にリッチメニューAをリンク済みのユーザーのリッチメニューはBに、リクエスト前にリッチメニューBをリンク済みのユーザーのリッチメニューはCに置き換わります。操作は互いに影響しないため、リクエスト前にリッチメニューAをリンク済みのユーザーのリッチメニューはCには置き換わりません。

```json
[
  {
    "type": "link",
    "from": "{リッチメニューAのID}",
    "to": "{リッチメニューBのID}"
  },
  {
    "type": "link",
    "from": "{リッチメニューBのID}",
    "to": "{リッチメニューCのID}"
  }
]
```

リッチメニューの一括操作は、バックグラウンドで非同期に処理されます。処理の進行状況は、[リッチメニューの一括操作の進行状況を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-batch-control-rich-menus-progress-status)エンドポイントで確認できます。

#### リトライ時に意図しない操作を避けるための方法 

`resumeRequestKey`プロパティを使用することで、安全にリトライすることができます。

以下のような場合に、`resumeRequestKey`プロパティを使用せずにリトライをすると、意図しない内容でリッチメニューが置き換わってしまう可能性があります。

- タイムアウトやLINEプラットフォームの内部サーバーのエラーなどにより、リクエストが受理されたかどうかがわからない場合
- [リッチメニューの一括操作の進行状況を取得](https://developers.line.biz/ja/reference/messaging-api/#get-batch-control-rich-menus-progress-status)した結果、レスポンスの`phase`プロパティが`failed`の場合

このような状況でも、初回のリクエストで`resumeRequestKey`プロパティに任意のキーを指定していた場合、同じキーを指定して再度リクエストを送ることで、処理が完了していないユーザーに対してのみ再度処理が行われます。

`resumeRequestKey`プロパティの有効期間は14日間（336時間）です。有効期限が切れた場合、新しいリクエストとして扱われます。

_リッチメニューの置き換えと、リッチメニューのリンクを解除するリクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/richmenu/batch \
-H "Authorization: Bearer {channel access token}" \
-H "Content-Type: application/json" \
-d '{
  "operations": [
    {
      "type": "link",
      "from": "{置き換える前のリッチメニューのID}",
      "to": "{置き換え先のリッチメニューのID}"
    },
    {
      "type": "unlink",
      "from": "{リンクを解除するリッチメニューのID}"
    }
  ],
  "resumeRequestKey": "{[0-9a-zA-Z\-_]{1,100}の正規表現にマッチする任意の文字列}"
}'
```

<!-- tab end -->

_リンク済みのリッチメニューを、すべてのユーザーから解除するリクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/richmenu/batch \
-H "Authorization: Bearer {channel access token}" \
-H "Content-Type: application/json" \
-d '{
  "operations": [
    {
      "type": "unlinkAll"
    }
  ],
  "resumeRequestKey": "{[0-9a-zA-Z\-_]{1,100}の正規表現にマッチする任意の文字列}"
}'
```

<!-- tab end -->

#### レート制限 

3リクエスト/時

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

<!-- tip start -->

**事前にリクエストボディが有効かを検証できます**

事前にリクエストボディが有効かを検証できる、[リッチメニューの一括操作のリクエストを検証する](https://developers.line.biz/ja/reference/messaging-api/#validate-batch-control-rich-menus-request)エンドポイントもあります。

検証用のエンドポイントを使うことで、このエンドポイントのレート制限に適用されることなく、リクエストがエラーにならないことを事前に確認できます。

<!-- tip end -->

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

operations

[リッチメニュー操作オブジェクト](https://developers.line.biz/ja/reference/messaging-api/#batch-control-rich-menus-of-users-operations)の配列

リッチメニューの一括操作を指定します。\
最大件数：1,000件

<!-- parameter end -->
<!-- parameter start (props: optional) -->

resumeRequestKey

String

リトライ用のキー。`[0-9a-zA-Z\-_]{1,100}`の正規表現にマッチする文字列。

<!-- parameter end -->

##### リッチメニュー操作オブジェクト 

リッチメニュー操作オブジェクトは、ユーザーにリンク済みのリッチメニューへの一括操作を表すオブジェクトです。

<!-- parameter start (props: required) -->

type

String

ユーザーにリンク済みのリッチメニューへの操作内容。以下のいずれかの値を指定します。

- `link`：`from`プロパティで指定されたリッチメニューがリンク済みのすべてのユーザーを対象に、リッチメニューを`to`プロパティで指定されたリッチメニューに置き換える。
- `unlink`：`from`プロパティで指定されたリッチメニューがリンク済みのすべてのユーザーを対象に、リッチメニューのリンクを解除する。
- `unlinkAll`：リッチメニューがリンクされている、すべてのユーザーとリッチメニューのリンクを解除する。

`unlinkAll`を指定した場合、`unlinkAll`以外の`type`を`operations`プロパティに含めることはできません。

<!-- parameter end -->
<!-- parameter start (props: annotation="typeがlinkまたはunlinkの場合必須") -->

from

String

リッチメニューのID。

置き換える前のリッチメニューのID、またはリンクを解除するリッチメニューのIDを指定します。

`operations`プロパティに複数の操作を指定する際に、同じリッチメニューのIDを複数の`from`プロパティに指定することはできません。

<!-- parameter end -->
<!-- parameter start (props: annotation="typeがlinkの場合必須") -->

to

String

リッチメニューのID。

置き換え先のリッチメニューのIDを指定します。

<!-- parameter end -->

#### レスポンス 

ステータスコード`202`と空のJSONオブジェクトを返します。

リッチメニューの一括操作は、バックグラウンドで非同期に処理されます。処理の進行状況は、[リッチメニューの一括操作の進行状況を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-batch-control-rich-menus-progress-status)エンドポイントで確認できます。

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
| `400` | リッチメニューを操作できませんでした。次のような理由が考えられます。<ul><li>無効なリッチメニューのIDが指定されている。</li><li>置き換え先のリッチメニューに画像が設定されていない。</li><li>`operations`プロパティに1000件を超える操作が指定されている。</li><li>`type`プロパティに`unlinkAll`と、それ以外の値が同時に指定されている。</li><li>同じリッチメニューのIDが複数の`from`プロパティに指定されている。</li></ul> |
| `404` | 存在しないリッチメニューが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

エラーが返された場合、リッチメニューは操作されません。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 無効なリッチメニューのIDを指定した場合（400 Bad Request）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "invalid richMenuId",
      "property": "operations[0].from"
    }
  ]
}

// 同じリッチメニューのIDを複数のfromプロパティに指定した場合（400 Bad Request）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "from richmenu (richmenu-6fc298...) is duplicated",
      "property": "operations[].from"
    }
  ]
}

// リクエストのtypeプロパティにunlinkAllと、それ以外のtypeを同時に指定した場合（400 Bad Request）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "'unlinkAll' type can't be combined with other type",
      "property": "operations[].type"
    }
  ]
}
```

<!-- tab end -->

### リッチメニューの一括操作の進行状況を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/richmenu/progress/batch`

[リンク済みのリッチメニューを一括で置き換え・解除](https://developers.line.biz/ja/reference/messaging-api/#batch-control-rich-menus-of-users)したときの進行状況を取得します。

進行状況を取得できる期間は、`acceptedTime`プロパティの値（タイムスタンプ）から14日間（336時間）です。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET 'https://api.line.me/v2/bot/richmenu/progress/batch?requestId={request_id}' \
-H 'Authorization: Bearer {CHANNEL_ACCESS_TOKEN}'
```

<!-- tab end -->

#### レート制限 

100リクエスト/時

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: required) -->

requestId

ユーザーにリンク済みのリッチメニューを一括で操作したときのリクエストID。リクエストIDは、Messaging APIのリクエストごとに発行されるIDです。[レスポンスヘッダー](https://developers.line.biz/ja/reference/messaging-api/#response-headers)に含まれます。

<!-- parameter end -->

#### レスポンス 

HTTPステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

phase

String

進行状況。以下のいずれかの値です。

- `ongoing`：リッチメニューの一括操作が進行中です。
- `succeeded`：リッチメニューの一括操作が完了しました。
- `failed`：リッチメニューの一括操作に失敗しました。これは、1人以上のユーザーのリッチメニューを操作できなかったことを意味します。また、操作が正常に完了したユーザーも存在する可能性があります。

<!-- parameter end -->
<!-- parameter start -->

acceptedTime

String

リッチメニューの一括操作のリクエストを受け付けた時間をミリ秒で表します。

- フォーマット：[ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)（例：`2020-12-03T10:15:30.121Z`）
- タイムゾーン：UTC

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

completedTime

String

リッチメニューの一括操作が完了した時間をミリ秒で表します。`phase`プロパティが`succeeded`または`failed`の場合にのみ返されます。

- フォーマット：[ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)（例：`2020-12-03T10:15:30.121Z`）
- タイムゾーン：UTC

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "phase": "succeeded",
  "acceptedTime": "2023-06-26T07:37:21.083Z",
  "completedTime": "2023-06-26T09:12:12.197Z"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明 |
| --- | --- |
| `400` | 無効なリクエストIDが指定されています。 |
| `404` | 進行状況を所得できませんでした。次のような理由が考えられます。<ul><li>存在しないリクエストIDが指定されている。</li><li>進行状況を取得できる期間を超えている。</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 存在しないリクエストIDを指定した場合（404 Not Found）
{
  "message": "Not found"
}
```

<!-- tab end -->

### リッチメニューの一括操作のリクエストを検証する 

Endpoint: `POST` `https://api.line.me/v2/bot/richmenu/validate/batch`

[リンク済みのリッチメニューを一括で置き換え・解除する](https://developers.line.biz/ja/reference/messaging-api/#batch-control-rich-menus-of-users)エンドポイントの[リクエストボディ](https://developers.line.biz/ja/reference/messaging-api/#batch-control-rich-menus-of-users-request-body)が有効かを検証します。

このエンドポイントを利用することで、リンク済みのリッチメニューを一括で置き換え・解除するときと同様に、以下のようなエラーを検出できます。

- 指定したリッチメニューが存在しない場合
- 指定したリッチメニューに画像が設定されていない場合
- `operations`プロパティに複数の操作を指定し、その内容が誤っている場合
  - `operations`プロパティに1,000件を超える配列を指定している
  - `type`プロパティに`unlinkAll`と、それ以外`type`を同時に指定している
  - 同じリッチメニューのIDを複数の`from`プロパティに指定している
- `resumeRequestKey`プロパティに指定した文字列が無効な場合

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/richmenu/validate/batch \
-H "Authorization: Bearer {channel access token}" \
-H "Content-Type: application/json" \
-d '{
  "operations": [
    {
      "type": "link",
      "from": "{置き換える前のリッチメニューのID}",
      "to": "{置き換え先のリッチメニューのID}"
    },
    {
      "type": "unlink",
      "from": "{リンクを解除するリッチメニューのID}"
    }
  ],
  "resumeRequestKey": "{[0-9a-zA-Z-_]{1,100}の正規表現にマッチする任意の文字列}"
}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

operations

[リッチメニュー操作オブジェクト](https://developers.line.biz/ja/reference/messaging-api/#batch-control-rich-menus-of-users-operations)の配列

リッチメニューへの一括操作の内容を定義します。\
最大件数：1,000件

<!-- parameter end -->
<!-- parameter start (props: optional) -->

resumeRequestKey

String

リトライ用のキー。`[0-9a-zA-Z\-_]{1,100}`の正規表現にマッチする文字列。

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
| `400` | リクエストボディの検証に失敗しました。次のような理由が考えられます。<ul><li>無効なリッチメニューのIDが指定されている。</li><li>置き換え先のリッチメニューに画像が設定されていない。</li><li>`operations`プロパティに1000件を超える操作が指定されている。</li><li>`type`プロパティに`unlinkAll`と、それ以外の値が同時に指定されている。</li><li>同じリッチメニューのIDが複数の`from`プロパティに指定されている。</li></ul> |
| `404` | 存在しないリッチメニューが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 画像を設定していないリッチメニューを指定した場合（400 Bad Request）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "'to' richmenu (richmenu-0c757d...) must have image but it doesn't",
      "property": "operations[0].to"
    }
  ]
}

// 存在しないリッチメニューのIDを指定した場合（404 Not Found）
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Richmenu (richmenu-d3385e...) is not found",
      "property": "operations[0].to"
    }
  ]
}
```

<!-- tab end -->

## リッチメニューエイリアス 

[リッチメニューエイリアス](https://developers.line.biz/ja/glossary/#rich-menu-alias)と[リッチメニュー切替アクション](https://developers.line.biz/ja/reference/messaging-api/#richmenu-switch-action)を使うことで、タブ切り替えが可能なリッチメニューをユーザーに提供できます。詳しくは、『Messaging APIドキュメント』の「[リッチメニューでタブ切り替えを行う](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/)」を参照してください。

### リッチメニューエイリアスを作成する 

Endpoint: `POST` `https://api.line.me/v2/bot/richmenu/alias`

リッチメニューエイリアスを作成するAPIです。

リッチメニューエイリアスを作成するには、事前に以下の作業をしておく必要があります。詳しくは、『Messaging APIドキュメント』の「[リッチメニューでタブ切り替えを行う](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/)」を参照してください。

- [リッチメニューを作成する](https://developers.line.biz/ja/reference/messaging-api/#create-rich-menu)
- [リッチメニューの画像をアップロードする](https://developers.line.biz/ja/reference/messaging-api/#upload-rich-menu-image)

1つのLINE公式アカウントに対して、Messaging APIを使って最大で1000件のリッチメニューエイリアスを作成できます。

_リクエストの例_

<!-- tab start `shell` -->

```sh
# リッチメニューエイリアスAを作成したい場合の例
curl -v -X POST https://api.line.me/v2/bot/richmenu/alias \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d \
'{
    "richMenuAliasId": "richmenu-alias-a",
    "richMenuId": "richmenu-862e6ad6c267d2ddf3f42bc78554f6a4"
}'

# リッチメニューエイリアスBを作成したい場合の例
curl -v -X POST https://api.line.me/v2/bot/richmenu/alias \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d \
'{
    "richMenuAliasId":"richmenu-alias-b",
    "richMenuId":"richmenu-88c05ef6921ae53f8b58a25f3a65faf7"
}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

richMenuAliasId

String

リッチメニューエイリアスのID。チャネルごとに一意の、任意のIDを指定できます。

- 最大文字数：32
- 使用可能文字種：半角英数字（`a`〜`z`、`0`～`9`）、アンダースコア（`_`）、ハイフン（`-`）

<!-- parameter end -->
<!-- parameter start (props: required) -->

richMenuId

String

リッチメニューエイリアスと紐づけるリッチメニューのID。

<!-- note start -->

**紐づけられるリッチメニューについて**

リッチメニューエイリアスと紐づけられるのは、同じチャネルで作成されたリッチメニューのみです。

<!-- note end -->

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
| `400` | リッチメニューエイリアスを作成できませんでした。次のような理由が考えられます。<ul><li>画像を設定していないリッチメニューや、存在しないリッチメニューが指定されている。</li><li>無効なリッチメニューエイリアスIDが指定されている。</li><li>無効なリッチメニューIDが指定されている。</li><li>リッチメニューエイリアスを作成できる上限に達している。</li><li>既に存在するリッチメニューエイリアスと同じIDが指定されている。</li></ul> |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 画像を設定していないリッチメニューや、存在しないリッチメニューを指定した場合（400 Bad Request）
{
    "message": "richmenu not found",
    "details": []
}

// 無効なリッチメニューIDを指定した場合（400 Bad Request）
{
    "message": "The request body has 1 error(s)",
    "details": [
        {
            "message": "invalid richMenuId",
            "property": "richMenuId"
        }
    ]
}

// 既存のリッチメニューエイリアスと同じリッチメニューエイリアスIDを指定した場合（400 Bad Request）
{
    "message": "conflict richmenu alias id",
    "details": []
}
```

<!-- tab end -->

### リッチメニューエイリアスを削除する 

Endpoint: `DELETE` `https://api.line.me/v2/bot/richmenu/alias/{richMenuAliasId}`

リッチメニューエイリアスを削除するAPIです。

<!-- note start -->

**リッチメニューエイリアス数の上限について**

Messaging APIで作成できるリッチメニューエイリアスの数の上限は、LINE公式アカウントあたり1,000件です。この上限を超過した場合は、新しいリッチメニューエイリアスを作成する前に既存のリッチメニューエイリアスを削除する必要があります。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
# リッチメニューエイリアスAを削除する場合の例
curl -v -X DELETE https://api.line.me/v2/bot/richmenu/alias/richmenu-alias-a \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

100リクエスト/時

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

richMenuAliasId

削除したいリッチメニューエイリアスのID。

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

| コード | 説明                                                   |
| ------ | ------------------------------------------------------ |
| `400`  | 無効なリッチメニューエイリアスIDが指定されています。   |
| `404`  | 存在しないリッチメニューエイリアスが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 存在しないリッチメニューエイリアスを指定した場合（404 Not Found）
{
  "message": "richmenu alias not found",
  "details": []
}
```

<!-- tab end -->

### リッチメニューエイリアスを更新する 

Endpoint: `POST` `https://api.line.me/v2/bot/richmenu/alias/{richMenuAliasId}`

リッチメニューエイリアスを更新するAPIです。既存のリッチメニューエイリアスを指定して、紐づくリッチメニューを変更できます。

<!-- note start -->

**更新が反映されるタイミングについて**

リッチメニューエイリアスの更新は、キャッシュデータの影響により、直ちに反映されない可能性があります。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
# リッチメニューエイリアスAを更新したい場合の例
curl -v -X POST https://api.line.me/v2/bot/richmenu/alias/richmenu-alias-a \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d \
'{
    "richMenuId": "richmenu-862e6ad6c267d2ddf3f42bc78554f6a4"
}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

richMenuAliasId

更新したいリッチメニューエイリアスのID

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

richMenuId

String

リッチメニューエイリアスと紐づけるリッチメニューのID

<!-- note start -->

**紐づけられるリッチメニューについて**

リッチメニューエイリアスと紐づけられるのは、同じチャネルで作成されたリッチメニューのみです。

<!-- note end -->

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
| `400` | リッチメニューエイリアスを更新できませんでした。次のような理由が考えられます。<ul><li>画像を設定していないリッチメニューや、存在しないリッチメニューが指定されている。</li><li>無効なリッチメニューエイリアスIDが指定されている。</li><li>無効なリッチメニューIDが指定されている。</li></ul> |
| `404` | 存在しないリッチメニューエイリアスが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 画像を設定していないリッチメニューや、存在しないリッチメニューを指定した場合（400 Bad Request）
{
    "message": "richmenu not found",
    "details": []
}

// 無効なリッチメニューIDを指定した場合（400 Bad Request）
{
    "message": "The request body has 1 error(s)",
    "details": [
        {
            "message": "invalid richMenuId",
            "property": "richMenuId"
        }
    ]
}
```

<!-- tab end -->

### リッチメニューエイリアスの情報を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/richmenu/alias/{richMenuAliasId}`

リッチメニューエイリアスのIDを指定して、リッチメニューエイリアスの情報を取得するAPIです。

_リクエストの例_

<!-- tab start `shell` -->

```sh
# リッチメニューエイリアスAの情報を取得したい場合の例
curl -v -X GET https://api.line.me/v2/bot/richmenu/alias/richmenu-alias-a \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

richMenuAliasId

情報を取得したいリッチメニューエイリアスのID。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

richMenuAliasId

String

リッチメニューエイリアスのID。

<!-- parameter end -->
<!-- parameter start -->

richMenuId

String

リッチメニューエイリアスと紐づくリッチメニューのID。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "richMenuAliasId": "richmenu-alias-a",
  "richMenuId": "richmenu-88c05ef6921ae53f8b58a25f3a65faf7"
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のHTTPステータスコードと、エラーレスポンスを返します。

| コード | 説明                                                   |
| ------ | ------------------------------------------------------ |
| `400`  | 無効なリッチメニューエイリアスIDが指定されています。   |
| `404`  | 存在しないリッチメニューエイリアスが指定されています。 |

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
// 存在しないリッチメニューエイリアスを指定した場合（404 Not Found）
{
  "message": "richmenu alias not found",
  "details": []
}
```

<!-- tab end -->

### リッチメニューエイリアスの一覧を取得する 

Endpoint: `GET` `https://api.line.me/v2/bot/richmenu/alias/list`

リッチメニューエイリアスの一覧を取得するAPIです。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/bot/richmenu/alias/list \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### レート制限 

2,000リクエスト/秒

レート制限について詳しくは、「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

aliases\[].richMenuAliasId

String

リッチメニューエイリアスのID。

<!-- parameter end -->
<!-- parameter start -->

aliases\[].richMenuId

String

リッチメニューエイリアスと紐づくリッチメニューのID。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
// リッチメニューエイリアスが2件の場合
{
    "aliases": [
        {
            "richMenuAliasId": "richmenu-alias-a",
            "richMenuId": "richmenu-862e6ad6c267d2ddf3f42bc78554f6a4"
        },
        {
            "richMenuAliasId": "richmenu-alias-b",
            "richMenuId": "richmenu-88c05ef6921ae53f8b58a25f3a65faf7"
        }
    ]
}

// リッチメニューエイリアスが0件の場合
{
    "aliases": []
}
```

<!-- tab end -->

#### エラーレスポンス 

詳しくは、[共通仕様](https://developers.line.biz/ja/reference/messaging-api/#common-specifications)の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

## アカウント連携 

プロバイダー（企業や開発者）が提供するサービスのアカウントと、LINEユーザーのアカウントを連携できます。

### 連携トークンを発行する 

Endpoint: `POST` `https://api.line.me/v2/bot/user/{userId}/linkToken`

[アカウント連携](https://developers.line.biz/ja/docs/messaging-api/linking-accounts/)で使用する連携トークンを発行するAPIです。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -X POST https://api.line.me/v2/bot/user/{userId}/linkToken \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### パスパラメータ 

<!-- parameter start (props: required) -->

userId

連携対象のLINEアカウントのユーザーID。[アカウント連携イベント](https://developers.line.biz/ja/reference/messaging-api/#account-link-event)オブジェクトの`source`オブジェクトで返されます。LINEに表示されるLINE IDは使用しないでください。

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下のプロパティを含むJSONオブジェクトを返します。

<!-- parameter start -->

linkToken

String

連携トークン。連携トークンの有効期間は10分で、1回のみ使用できます。

<!-- note start -->

**注意**

有効期間は予告なく変わる可能性があります。

<!-- note end -->

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "linkToken": "NMZTNuVrPTqlr2IF8Bnymkb7rXfYv5EY"
}
```

<!-- tab end -->

## メッセージオブジェクト 

送信するメッセージの内容を表すJSONオブジェクトです。

<!-- tip start -->

**メッセージオブジェクトが有効かを検証する**

以下のエンドポイントを使用すると、メッセージオブジェクトが有効かを検証できます。

- [応答メッセージのメッセージオブジェクトを検証する](https://developers.line.biz/ja/reference/messaging-api/#validate-message-objects-of-reply-message)
- [プッシュメッセージのメッセージオブジェクトを検証する](https://developers.line.biz/ja/reference/messaging-api/#validate-message-objects-of-push-message)
- [マルチキャストメッセージのメッセージオブジェクトを検証する](https://developers.line.biz/ja/reference/messaging-api/#validate-message-objects-of-multicast-message)
- [ナローキャストメッセージのメッセージオブジェクトを検証する](https://developers.line.biz/ja/reference/messaging-api/#validate-message-objects-of-narrowcast-message)
- [ブロードキャストメッセージのメッセージオブジェクトを検証する](https://developers.line.biz/ja/reference/messaging-api/#validate-message-objects-of-broadcast-message)

<!-- tip end -->

### メッセージ共通プロパティ 

以下のプロパティはすべてのメッセージオブジェクトに指定できます。

#### クイックリプライ 

クイックリプライ機能で使用するプロパティです。詳しくは、「[クイックリプライを使う](https://developers.line.biz/ja/docs/messaging-api/using-quick-reply/)」を参照してください。

<!-- parameter start (props: optional) -->

quickReply

Object

[itemsオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#items-object)

<!-- parameter end -->

複数の[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)を受信したユーザーには、最後のメッセージオブジェクトの`quickReply`プロパティが表示されます。

##### itemsオブジェクト 

[クイックリプライボタン](https://developers.line.biz/ja/reference/messaging-api/#quick-reply-button-object)のコンテナです。

<!-- parameter start (props: required) -->

items

Array of objects

[クイックリプライボタンオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#quick-reply-button-object)。\
最大オブジェクト数：13

<!-- parameter end -->

_itemsオブジェクトの例_

<!-- tab start `json` -->

```json
"quickReply": {
  "items": [
    {
      "type": "action",
      "action": {
        "type": "cameraRoll",
        "label": "Send photo"
      }
    },
    {
      "type": "action",
      "action": {
        "type": "camera",
        "label": "Open camera"
      }
    }
  ]
}
```

<!-- tab end -->

##### クイックリプライボタンオブジェクト 

ボタン形式で表示される、クイックリプライの選択肢です。

<!-- parameter start (props: required) -->

type

String

`action`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

imageUrl

String

ボタンの先頭に表示するアイコンのURL（最大文字数：2000）\
プロトコル：HTTPS（TLS 1.2以降）\
画像フォーマット：PNG\
アスペクト比：1:1（幅：高さ）\
最大ファイルサイズ：1MB

画像サイズに制限はありません。\
`action`プロパティに指定するアクションが[カメラアクション](https://developers.line.biz/ja/reference/messaging-api/#camera-action)、[カメラロールアクション](https://developers.line.biz/ja/reference/messaging-api/#camera-roll-action)、または[位置情報アクション](https://developers.line.biz/ja/reference/messaging-api/#location-action)で、`imageUrl`プロパティが未指定の場合、デフォルトのアイコンが表示されます。

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

action

Object

タップされたときのアクション。[アクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#action-objects)を指定します。指定できるアクションの種類は以下のとおりです。

- [ポストバックアクション](https://developers.line.biz/ja/reference/messaging-api/#postback-action)
- [メッセージアクション](https://developers.line.biz/ja/reference/messaging-api/#message-action)
- [URIアクション](https://developers.line.biz/ja/reference/messaging-api/#uri-action)
- [日時選択アクション](https://developers.line.biz/ja/reference/messaging-api/#datetime-picker-action)
- [カメラアクション](https://developers.line.biz/ja/reference/messaging-api/#camera-action)
- [カメラロールアクション](https://developers.line.biz/ja/reference/messaging-api/#camera-roll-action)
- [位置情報アクション](https://developers.line.biz/ja/reference/messaging-api/#location-action)
- [クリップボードアクション](https://developers.line.biz/ja/reference/messaging-api/#clipboard-action)

<!-- parameter end -->

クイックリプライボタンが設定されたメッセージを未対応のLINEで受信すると、メッセージ本体のみが表示されます。

#### アイコンと表示名のカスタマイズ 

LINE公式アカウントからメッセージを送る際に、[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)に、`sender.name`プロパティと`sender.iconUrl`プロパティを指定できます。

<!-- parameter start (props: optional) -->

sender.name

String

表示名。`LINE`など弊社のサービスと誤認される可能性があるワードは使用できません。\
最大文字数：20

<!-- parameter end -->
<!-- parameter start (props: optional) -->

sender.iconUrl

String

メッセージ送信時にアイコンとして表示する画像のURL（最大文字数：2000）\
プロトコル：HTTPS（TLS 1.2以降）\
画像フォーマット：PNG\
アスペクト比：1:1（幅：高さ）\
最大ファイルサイズ：1MB

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- parameter end -->

_アイコンと表示名をカスタマイズするテキストメッセージの例_

<!-- tab start `json` -->

```json
{
  "type": "text",
  "text": "Hello, I am Cony!!",
  "sender": {
    "name": "Cony",
    "iconUrl": "https://line.me/conyprof"
  }
}
```

<!-- tab end -->

### テキストメッセージ 

<!-- note start -->

**文字数および絵文字の位置について**

プロパティに指定するテキストの文字数、および絵文字の位置は、UTF-16でエンコーディングしたときの符号単位の数および位置です。たとえば、サロゲートペアを使用する文字や、UTF-16で表現できる絵文字など、文字によっては、1文字ではなく複数文字としてカウントする必要があります。

詳しくは、『Messaging APIドキュメント』の「[テキストの文字数のカウント](https://developers.line.biz/ja/docs/messaging-api/text-character-count/)」を参照してください。

<!-- note end -->

<!-- parameter start (props: required) -->

type

String

`text`

<!-- parameter end -->
<!-- parameter start (props: required) -->

text

String

メッセージのテキスト。以下の絵文字を含めることができます。

- LINE絵文字。`$`をプレースホルダとして使用します。使用するLINE絵文字の`プロダクトID`と`絵文字ID`を、`emojis`プロパティに指定してください。詳しくは、「[LINE絵文字](https://developers.line.biz/ja/docs/messaging-api/emoji-list/)」を参照してください。
- Unicode絵文字。

最大文字数：5000

<!-- warning start -->

**「LINE独自のUnicode絵文字」は2022年3月31日をもって廃止されました**

「LINE独自のUnicode絵文字」の代わりに`emojis`プロパティを使った「LINE絵文字」を利用してください。

詳しくは、2022年4月1日のニュース、「[2022年3月31日をもって、Messaging APIの「LINE独自のUnicode絵文字」を廃止しました](https://developers.line.biz/ja/news/2022/04/01/line-original-unicode-emojis-has-been-discontinued/)」と「[LINE絵文字](https://developers.line.biz/ja/docs/messaging-api/emoji-list/)」を参照してください。

<!-- warning end -->

<!-- parameter end -->
<!-- parameter start (props: optional) -->

emojis

LINE絵文字オブジェクトの配列

1個以上のLINE絵文字\
最大個数：20

<!-- parameter end -->
<!-- parameter start (props: optional) -->

emojis.index

Number

テキストの先頭を`0`とした、`text`プロパティ内の`$`（LINE絵文字のプレースホルダ）の位置。詳しくは、「テキストメッセージの例」を参照してください。

<!-- note start -->

**注意**

ここで指定した位置と、`$`の位置が一致しない場合は、`400 Bad request`が返されます。

<!-- note end -->

<!-- parameter end -->
<!-- parameter start (props: optional) -->

emojis.productId

String

LINE絵文字の集合を示すプロダクトID。プロダクトIDについては、「[LINE絵文字](https://developers.line.biz/ja/docs/messaging-api/emoji-list/)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

emojis.emojiId

String

絵文字ID。Messaging APIで送信できるLINE絵文字の絵文字IDについては、「[LINE絵文字](https://developers.line.biz/ja/docs/messaging-api/emoji-list/)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

quoteToken

String

引用したいメッセージの引用トークン。詳しくは、『Messaging APIドキュメント』の「[引用トークンを取得する](https://developers.line.biz/ja/docs/messaging-api/get-quote-tokens/)」を参照してください。

<!-- parameter end -->

_テキストメッセージの例_

<!-- tab start `json` -->

```json
{
    "type": "text",
    "text": "Hello, world"
}
```

<!-- tab end -->

_LINE絵文字を含むテキストメッセージの例_

<!-- tab start `json` -->

```json
{
    "type": "text",
    "text": "$ LINE emoji $",
    "emojis": [
      {
        "index": 0,
        "productId": "5ac1bfd5040ab15980c9b435",
        "emojiId": "001"
      },
      {
        "index": 13,
        "productId": "5ac1bfd5040ab15980c9b435",
        "emojiId": "002"
      }
    ]
}
```

<!-- tab end -->

_過去のメッセージを引用したテキストメッセージの例_

<!-- tab start `json` -->

```json
{
    "type": "text",
    "text": "Yes, you can.",
    "quoteToken": "yHAz4Ua2wx7..."
}
```

<!-- tab end -->

### テキストメッセージ（v2） 

テキストメッセージ（v2）は、[テキストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#text-message)と異なり、`{`と`}`で囲まれた文字列をメンションや絵文字に置き換えることができます。

<!-- parameter start (props: required) -->

type

String

`textV2`

<!-- parameter end -->
<!-- parameter start (props: required) -->

text

String

メッセージのテキスト。

`{`と`}`で囲まれた文字列を、`substitution`プロパティを用いてメンションや絵文字に置き換えることができます。`{`および`}`を文字列として使用する場合は、`{{`および`}}`でエスケープしてください。また、`{`と`}`を使用する際は、以下のことに注意してください。

- `{`と`}`はペアで使用する必要があります。
- `{`と`}`で囲まれた文字列は、`substitution`プロパティを用いて置換内容を指定する必要があります。

最大文字数：5000

<!-- parameter end -->
<!-- parameter start (props: optional) -->

substitution

Object

`text`プロパティの`{`と`}`で囲まれた部分の置換内容を指定するオブジェクト。

オブジェクトのキーに使用できる文字は、半角英数字（`0-9a-zA-Z`）とアンダースコア（`_`）です。また、キーの文字数は、最大で20文字です。

オブジェクトの値には[メンションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#text-message-v2-mention-object)または[絵文字オブジェクト](https://developers.line.biz/ja/reference/messaging-api/#text-message-v2-emoji-object)を指定できます。

オブジェクトの最大数：100

<!-- parameter end -->
<!-- parameter start (props: optional) -->

quoteToken

String

引用したいメッセージの引用トークン。詳しくは、『Messaging APIドキュメント』の「[引用トークンを取得する](https://developers.line.biz/ja/docs/messaging-api/get-quote-tokens/)」を参照してください。

<!-- parameter end -->

_メンションと絵文字を指定したテキストメッセージ（v2）の例_

<!-- tab start `json` -->

```json
{
  "type": "textV2",
  "text": "Welcome, {user1}! {laugh}\n{everyone} There is a newcomer!",
  "substitution": {
    "user1": {
      "type": "mention",
      "mentionee": {
        "type": "user",
        "userId": "U49585cd0d5..."
      }
    },
    "laugh": {
      "type": "emoji",
      "productId": "5a8555cfe6256cc92ea23c2a",
      "emojiId": "002"
    },
    "everyone": {
      "type": "mention",
      "mentionee": {
        "type": "all"
      }
    }
  }
}
```

<!-- tab end -->

#### メンションオブジェクト 

テキスト内で置き換えるメンションの内容を指定します。メンションオブジェクトを使用する際は、以下のことに注意してください。

1. メンションオブジェクトは、[応答メッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)または[プッシュメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-push-message)でのみ使用できます。
1. メッセージの送信先は、[グループトーク](https://developers.line.biz/ja/docs/messaging-api/group-chats/#group)または[複数人トーク](https://developers.line.biz/ja/docs/messaging-api/group-chats/#room)である必要があります。
1. メッセージを送信するLINE公式アカウントは、送信先であるグループトークまたは複数人トークのメンバーである必要があります。
1. メンションされたすべてのユーザーは、そのメッセージの送信先であるグループトークまたは複数人トークのメンバーである必要があります。
1. ひとつのメッセージで置換可能なメンションは20個までです。

なお、上記の2から4までの項目は、「[応答メッセージのメッセージオブジェクトを検証する](https://developers.line.biz/ja/reference/messaging-api/#validate-message-objects-of-reply-message)」または「[プッシュメッセージのメッセージオブジェクトを検証する](https://developers.line.biz/ja/reference/messaging-api/#validate-message-objects-of-push-message)」エンドポイントでは検証できません。

<!-- parameter start (props: required) -->

type

String

`mention`

<!-- parameter end -->
<!-- parameter start (props: required) -->

mentionee

Object

メンション先のオブジェクト。[ユーザーオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#text-message-v2-mentionee-user)または[全体メンションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#text-message-v2-mentionee-all)を指定します。

<!-- parameter end -->

##### ユーザーオブジェクト 

<!-- parameter start (props: required) -->

type

String

`user`

<!-- parameter end -->
<!-- parameter start (props: required) -->

userId

String

メンションするユーザーのユーザーID。なお、LINEボットのユーザーIDは指定できません。

<!-- parameter end -->

##### 全体メンションオブジェクト 

<!-- parameter start (props: required) -->

type

String

`all`

<!-- parameter end -->

#### 絵文字オブジェクト 

テキスト内で置き換える絵文字の内容を指定します。ひとつのメッセージで置換可能な絵文字は20個までです。

<!-- parameter start (props: required) -->

type

String

`emoji`

<!-- parameter end -->
<!-- parameter start (props: required) -->

productId

String

LINE絵文字の集合を示すプロダクトID。プロダクトIDについて詳しくは、『Messaging APIドキュメント』の「[LINE絵文字](https://developers.line.biz/ja/docs/messaging-api/emoji-list/)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

emojiId

String

絵文字ID。Messaging APIで送信できるLINE絵文字の絵文字IDについて詳しくは、『Messaging APIドキュメント』の「[LINE絵文字](https://developers.line.biz/ja/docs/messaging-api/emoji-list/)」を参照してください。

<!-- parameter end -->

### スタンプメッセージ 

<!-- parameter start (props: required) -->

type

String

`sticker`

<!-- parameter end -->
<!-- parameter start (props: required) -->

packageId

String

スタンプセットのパッケージID。パッケージIDについては、[スタンプ](https://developers.line.biz/ja/docs/messaging-api/sticker-list/)を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

stickerId

String

スタンプID。Messaging APIで送信できるスタンプのスタンプIDについては、[スタンプ](https://developers.line.biz/ja/docs/messaging-api/sticker-list/)を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

quoteToken

String

引用したいメッセージの引用トークン。詳しくは、『Messaging APIドキュメント』の「[引用トークンを取得する](https://developers.line.biz/ja/docs/messaging-api/get-quote-tokens/)」を参照してください。

<!-- parameter end -->

_スタンプメッセージの例_

<!-- tab start `json` -->

```json
{
  "type": "sticker",
  "packageId": "446",
  "stickerId": "1988"
}
```
<!-- tab end -->

_過去のメッセージを引用したスタンプメッセージの例_

<!-- tab start `json` -->

```json
{
  "type": "sticker",
  "packageId": "789",
  "stickerId": "10855",
  "quoteToken": "yHAz4Ua2wx7..."
}
```

<!-- tab end -->

### 画像メッセージ 

<!-- parameter start (props: required) -->

type

String

`image`

<!-- parameter end -->
<!-- parameter start (props: required) -->

originalContentUrl

String

画像のURL（最大文字数：2000）\
プロトコル：HTTPS（TLS 1.2以降）\
画像フォーマット：JPEGまたはPNG\
最大ファイルサイズ：10MB

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

previewImageUrl

String

プレビュー画像のURL（最大文字数：2000）\
プロトコル：HTTPS（TLS 1.2以降）\
画像フォーマット：JPEGまたはPNG\
最大ファイルサイズ：1MB

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

なお、ユーザー端末の状況によっては、プレビュー画像として`originalContentUrl`プロパティの画像が使われる場合があります。

<!-- parameter end -->

_画像メッセージの例_

<!-- tab start `json` -->

```json
{
  "type": "image",
  "originalContentUrl": "https://example.com/original.jpg",
  "previewImageUrl": "https://example.com/preview.jpg"
}
```

<!-- tab end -->

### 動画メッセージ 

<!-- note start -->

**動画が正しく再生できない**

動画を含むメッセージの送信に成功したとしても、ユーザーの端末上で動画を正しく再生できない場合があります。詳しくは、FAQの「[メッセージとして送信した動画が再生できないのはなぜですか？](https://developers.line.biz/ja/faq/#why-cant-i-play-a-video-i-sent)」を参照してください。

<!-- note end -->

<!-- note start -->

**動画のアスペクト比**

- 一定以上に縦長・横長の動画を送信した場合、一部の環境では動画の一部が欠けて表示される場合があります。
- `originalContentUrl`で指定する動画と、`previewImageUrl`で指定するプレビュー画像のアスペクト比は一致させてください。アスペクト比が異なると、動画の背面にプレビュー画像が表示されることがあります。

![LINEのトークルームの動画メッセージ。アスペクト比16:9の映像の背面に、アスペクト比1:1のプレビュー映像が表示されています。](https://developers.line.biz/media/messaging-api/messages/image-overlapping-ja.png)

<!-- note end -->

<!-- parameter start (props: required) -->

type

String

`video`

<!-- parameter end -->
<!-- parameter start (props: required) -->

originalContentUrl

String

動画ファイルのURL（最大文字数：2000）\
プロトコル：HTTPS（TLS 1.2以降）\
動画フォーマット：mp4\
最大ファイルサイズ：200MB

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

previewImageUrl

String

プレビュー画像のURL（最大文字数：2000）\
プロトコル：HTTPS（TLS 1.2以降）\
画像フォーマット：JPEGまたはPNG\
最大ファイルサイズ：1MB

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

trackingId

String

[動画視聴完了イベント](https://developers.line.biz/ja/reference/messaging-api/#video-viewing-complete)が発生したときに、動画を識別するためのID。`trackingId`を付与した動画メッセージを送信した場合に限り、ユーザーが動画の視聴を完了すると動画視聴完了イベントが発生します。

複数のメッセージで同じIDを使用することができます。

- 最大文字数：100
- 使用可能文字種：半角英数字（`a`〜`z`、`A`～`Z`、`0`～`9`）、記号（`-.=,+*()%$&;:@{}!?<>[]`）

<!-- note start -->

**注意**

`trackingId`プロパティは、グループトークや複数人トーク宛てのメッセージでは使用できません。

<!-- note end -->

<!-- parameter end -->

_動画メッセージの例_

<!-- tab start `json` -->

```json
{
  "type": "video",
  "originalContentUrl": "https://example.com/original.mp4",
  "previewImageUrl": "https://example.com/preview.jpg",
  "trackingId": "track-id"
}
```

<!-- tab end -->

### 音声メッセージ 

<!-- parameter start (props: required) -->

type

String

`audio`

<!-- parameter end -->
<!-- parameter start (props: required) -->

originalContentUrl

String

音声ファイルのURL（最大文字数：2000）\
プロトコル：HTTPS（TLS 1.2以降）\
音声フォーマット：mp3またはm4a\
最大ファイルサイズ：200MB

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

duration

Number

音声ファイルの長さ（ミリ秒）

<!-- parameter end -->

_音声メッセージの例_

<!-- tab start `json` -->

```json
{
  "type": "audio",
  "originalContentUrl": "https://example.com/original.m4a",
  "duration": 60000
}
```

<!-- tab end -->

### 位置情報メッセージ 

<!-- parameter start (props: required) -->

type

String

`location`

<!-- parameter end -->
<!-- parameter start (props: required) -->

title

String

タイトル\
最大文字数：100

<!-- parameter end -->
<!-- parameter start (props: required) -->

address

String

住所\
最大文字数：100

<!-- parameter end -->
<!-- parameter start (props: required) -->

latitude

Decimal

緯度

<!-- parameter end -->
<!-- parameter start (props: required) -->

longitude

Decimal

経度

<!-- parameter end -->

_位置情報メッセージの例_

<!-- tab start `json` -->

```json
{
  "type": "location",
  "title": "my location",
  "address": "〒102-8282 東京都千代田区紀尾井町1番3号",
  "latitude": 35.67966,
  "longitude": 139.73669
}
```

<!-- tab end -->

### クーポンメッセージ 

クーポンメッセージは、クーポンIDを指定してユーザーにクーポンを送信するメッセージです。

<!-- parameter start (props: required) -->

type

String

`coupon`

<!-- parameter end -->
<!-- parameter start (props: required) -->

couponId

String

クーポンのクーポンID。\
クーポンID（`couponId`）は、[クーポンを作成](https://developers.line.biz/ja/reference/messaging-api/#create-coupon)した際に[レスポンス](https://developers.line.biz/ja/reference/messaging-api/#create-coupon-response)で渡されます。また、[クーポンの一覧を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-coupons-list)エンドポイントでも確認できます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

deliveryTag

String

クーポンの表示経路名。\
最大文字数：30\
使用可能文字種：半角英数字（`a`〜`z`、`A`～`Z`、`0`～`9`）、アンダースコア（`_`）

`deliveryTag`を指定しない場合、経路は`不明`になります。詳しくは、『LINEヤフー for Business』の「[分析 - クーポン](https://www.lycbiz.com/jp/manual/OfficialAccountManager/insight_coupon/)」を参照してください。

<!-- parameter end -->

_クーポンメッセージの例_

<!-- tab start `json` -->

```json
{
  "type": "coupon",
  "couponId": "01JYNW8JMQVFBNWF1APF8Z3FS7",
  "deliveryTag": "2025_winter_campaign"
}
```

<!-- tab end -->

### イメージマップメッセージ 

イメージマップメッセージは、複数のタップ領域を設定した画像を送信できるメッセージです。画像全体に1つのタップ領域を割り当てることも、画像を区切って複数のタップ領域を設定することもできます。

また、画像の上で動画を再生したり、動画再生後にリンク先を設定したラベルを表示したりできます。

<!-- note start -->

**動画が正しく再生できない**

動画を含むメッセージの送信に成功したとしても、ユーザーの端末上で動画を正しく再生できない場合があります。詳しくは、FAQの「[メッセージとして送信した動画が再生できないのはなぜですか？](https://developers.line.biz/ja/faq/#why-cant-i-play-a-video-i-sent)」を参照してください。

<!-- note end -->

<!-- note start -->

**動画のアスペクト比**

`originalContentUrl`で指定する動画と、`previewImageUrl`で指定するプレビュー画像のアスペクト比は一致させてください。アスペクト比が異なると、動画の背面にプレビュー画像が表示されることがあります。

![LINEのトークルームの動画メッセージ。アスペクト比16:9の映像の背面に、アスペクト比1:1のプレビュー映像が表示されています。](https://developers.line.biz/media/messaging-api/messages/image-overlapping-ja.png)

<!-- note end -->

<!-- parameter start (props: required) -->

type

String

`imagemap`

<!-- parameter end -->
<!-- parameter start (props: required) -->

baseUrl

String

画像のベースURL（最大文字数：2000）\
プロトコル：HTTPS（TLS 1.2以降）\
イメージマップメッセージで使える画像について詳しくは、「[画像の設定方法](https://developers.line.biz/ja/reference/messaging-api/#base-url)」を参照してください。

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

altText

String

代替テキスト。ユーザーがメッセージを受信した際に、端末の通知やトークリストで画像の代替として表示されます。\
Unicode絵文字を含めることができます。\
最大文字数：1500

<!-- parameter end -->
<!-- parameter start (props: required) -->

baseSize.width

Number

基本画像の幅（px単位）。1040を指定します。

<!-- parameter end -->
<!-- parameter start (props: required) -->

baseSize.height

Number

基本画像の幅を1040pxとした場合の高さ

<!-- parameter end -->
<!-- parameter start (props: annotation="※1") -->

video.originalContentUrl

String

動画ファイルのURL（最大文字数：2000）\
プロトコル：HTTPS（TLS 1.2以降）\
動画フォーマット：mp4\
最大ファイルサイズ：200MB

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- note start -->

**注意**

一定以上に縦長・横長の動画を送信した場合、一部の環境では動画の一部が欠けて表示される場合があります。

<!-- note end -->

<!-- parameter end -->
<!-- parameter start (props: annotation="※1") -->

video.previewImageUrl

String

プレビュー画像のURL（最大文字数：2000）\
プロトコル：HTTPS（TLS 1.2以降）\
画像フォーマット：JPEGまたはPNG\
最大ファイルサイズ：1MB

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="※1") -->

video.area.x

Number

イメージマップ領域の左端を基準とした動画領域の位置（横方向の相対位置）。`0`以上の値を設定してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="※1") -->

video.area.y

Number

イメージマップ領域の上端を基準とした動画領域の位置（縦方向の相対位置）。`0`以上の値を設定してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="※1") -->

video.area.width

Number

動画領域の幅

<!-- parameter end -->
<!-- parameter start (props: annotation="※1") -->

video.area.height

Number

動画領域の高さ

<!-- parameter end -->
<!-- parameter start (props: annotation="※2") -->

video.externalLink.linkUri

String

ウェブページのURL。動画再生後に表示されるラベルをタップしたときに呼び出されます。\
最大文字数：1000\
使用できるスキームは、`http`、`https`、`line`、および`tel`です。 LINE URLスキームについて詳しくは、「[LINE URLスキームでLINEの機能を使う](https://developers.line.biz/ja/docs/messaging-api/using-line-url-scheme/)」を参照してください。

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="※2") -->

video.externalLink.label

String

ラベル。動画の再生が終了した後に表示されます。\
最大文字数：30

<!-- parameter end -->
<!-- parameter start (props: required) -->

actions

[イメージマップアクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#imagemap-action-objects)の配列

画像がタップされたときのアクション\
最大件数：50

<!-- parameter end -->

※1 イメージマップで動画を再生する場合は必須です。\
※2 イメージマップで動画を再生し、動画再生後にラベルを表示する場合は必須です。

_2つのタップ領域を持つイメージマップメッセージの例_

<!-- tab start `json` -->

```json
{
  "type": "imagemap",
  "baseUrl": "https://example.com/bot/images/rm001",
  "altText": "This is an imagemap",
  "baseSize": {
    "width": 1040,
    "height": 1040
  },
  "video": {
    "originalContentUrl": "https://example.com/video.mp4",
    "previewImageUrl": "https://example.com/video_preview.jpg",
    "area": {
      "x": 0,
      "y": 0,
      "width": 1040,
      "height": 585
    },
    "externalLink": {
      "linkUri": "https://example.com/see_more.html",
      "label": "See More"
    }
  },
  "actions": [
    {
      "type": "uri",
      "linkUri": "https://example.com/",
      "area": {
        "x": 0,
        "y": 586,
        "width": 520,
        "height": 454
      }
    },
    {
      "type": "message",
      "text": "Hello",
      "area": {
        "x": 520,
        "y": 586,
        "width": 520,
        "height": 454
      }
    }
  ]
}
```

<!-- tab end -->

#### 画像の設定方法 

イメージマップメッセージで使用する画像は、以下の要件を満たす必要があります。

- 画像フォーマット： JPEGまたはPNG
- 画像の幅：240px、300px、460px、700px、および1040px
- 最大ファイルサイズ：10MB

<!-- tip start -->

**透過PNGの使用について**

イメージマップメッセージに、透過PNGを使用できます。

<!-- tip end -->

「`baseUrl/{image width}`」というURL形式で、5つの異なるサイズの画像にアクセスできるようにしてください。LINEはユーザーのデバイスに応じて、適切な解像度の画像を取得します。

たとえば、画像のベースURLが「`https://example.com/images/cats`」だった場合、幅が700pxの画像のURLは「`https://example.com/images/cats/700`」になります。すべての画像のURLにアクセスして、画像が表示されることを確認してください。

| 画像の幅 | URLの例                                     |
| -------- | ------------------------------------------- |
| 240px    | `https://example.com/bot/images/rm001/240`  |
| 300px    | `https://example.com/bot/images/rm001/300`  |
| 460px    | `https://example.com/bot/images/rm001/460`  |
| 700px    | `https://example.com/bot/images/rm001/700`  |
| 1040px   | `https://example.com/bot/images/rm001/1040` |

<!-- note start -->

**注意**

画像のURLには拡張子を含めないでください。「`https://example.com/bot/images/rm001/700.png`」のように、URLに拡張子が含まれている場合、イメージマップメッセージでは画像が表示されません。

<!-- note end -->

#### イメージマップアクションオブジェクト 

イメージマップに設定するアクションとタップ領域を表すオブジェクトです。領域がタップされると、アクションのタイプごとにそれぞれ以下のアクションが実行されます。

- `uri`：指定するURIにユーザーがリダイレクトされます。
- `message`：指定するメッセージが送信されます。
- `clipboard`：指定する文字列がユーザーの端末のクリップボードにコピーされます。

##### イメージマップURIアクションオブジェクト 

<!-- parameter start (props: required) -->

type

String

`uri`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

label

String

アクションのラベル。ユーザーデバイスのアクセシビリティ機能が有効な場合に読み上げられます。\
最大文字数：100

<!-- parameter end -->
<!-- parameter start (props: required) -->

linkUri

String

ウェブページのURL\
最大文字数：1000\
使用できるスキームは、`http`、`https`、`line`、および`tel`です。 LINE URLスキームについて詳しくは、「[LINE URLスキームでLINEの機能を使う](https://developers.line.biz/ja/docs/messaging-api/using-line-url-scheme/)」を参照してください。

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

area

[イメージマップ領域オブジェクト](https://developers.line.biz/ja/reference/messaging-api/#imagemap-area-object)

タップ領域の定義

<!-- parameter end -->

_イメージマップURIアクションオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "type": "uri",
  "label": "https://example.com/",
  "linkUri": "https://example.com/",
  "area": {
    "x": 0,
    "y": 0,
    "width": 520,
    "height": 1040
  }
}
```

<!-- tab end -->

##### イメージマップメッセージアクションオブジェクト 

<!-- parameter start (props: required) -->

type

String

`message`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

label

String

アクションのラベル。ユーザーデバイスのアクセシビリティ機能が有効な場合に読み上げられます。\
最大文字数：100

<!-- parameter end -->
<!-- parameter start (props: required) -->

text

String

送信するメッセージ\
最大文字数：400

<!-- parameter end -->
<!-- parameter start (props: required) -->

area

[イメージマップ領域オブジェクト](https://developers.line.biz/ja/reference/messaging-api/#imagemap-area-object)

タップ領域の定義

<!-- parameter end -->

_イメージマップメッセージアクションオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "type": "message",
  "label": "hello",
  "text": "hello",
  "area": {
    "x": 520,
    "y": 0,
    "width": 520,
    "height": 1040
  }
}
```

<!-- tab end -->

##### イメージマップクリップボードアクションオブジェクト 

iOS版LINEまたはAndroid版LINEのバージョン`14.0.0`以降で動作します。

<!-- parameter start (props: required) -->

type

String

`clipboard`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

label

String

アクションのラベル。ユーザーデバイスのアクセシビリティ機能が有効な場合に読み上げられます。\
最大文字数：100

<!-- parameter end -->
<!-- parameter start (props: required) -->

clipboardText

String

クリップボードにコピーされる文字列

- 最大文字数：1000

<!-- parameter end -->
<!-- parameter start (props: required) -->

area

[イメージマップ領域オブジェクト](https://developers.line.biz/ja/reference/messaging-api/#imagemap-area-object)

タップ領域の定義

<!-- parameter end -->

_イメージマップクリップボードアクションオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "type": "clipboard",
  "label": "Copy",
  "clipboardText": "3B48740B",
  "area": {
    "x": 520,
    "y": 0,
    "width": 520,
    "height": 1040
  }
}
```

<!-- tab end -->

###### イメージマップ領域オブジェクト 

タップ領域のサイズを表すオブジェクトです。画像の左上が座標の原点です。`baseSize.width`プロパティと`baseSize.height`プロパティに基づいて指定します。

<!-- parameter start (props: required) -->

x

Number

領域の左端を基準としたタップ領域の位置（横方向の相対位置）。`0`以上の値を設定してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

y

Number

領域の上端を基準としたタップ領域の位置（縦方向の相対位置）。`0`以上の値を設定してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

width

Number

タップ領域の幅

<!-- parameter end -->
<!-- parameter start (props: required) -->

height

Number

タップ領域の高さ

<!-- parameter end -->

_イメージマップ領域オブジェクトの例_

<!-- tab start `json` -->

```json
{
  "x": 520,
  "y": 0,
  "width": 520,
  "height": 1040
}
```

<!-- tab end -->

### テンプレートメッセージ 

テンプレートメッセージは、あらかじめレイアウトが定義されたテンプレートをカスタマイズして構築するメッセージです。詳しくは、「[テンプレートメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#template-messages)」を参照してください。

以下のタイプのテンプレートを利用できます。

- [ボタン](https://developers.line.biz/ja/reference/messaging-api/#buttons)
- [確認](https://developers.line.biz/ja/reference/messaging-api/#confirm)
- [カルーセル](https://developers.line.biz/ja/reference/messaging-api/#carousel)
- [画像カルーセル](https://developers.line.biz/ja/reference/messaging-api/#image-carousel)

より柔軟なレイアウトでメッセージを送りたい場合は、[Flex Message](https://developers.line.biz/ja/reference/messaging-api/#flex-message)を使用してください。

#### テンプレートメッセージオブジェクトの共通プロパティ 

以下のプロパティは、すべてのテンプレートメッセージオブジェクトで共通です。

<!-- parameter start (props: required) -->

type

String

`template`

<!-- parameter end -->
<!-- parameter start (props: required) -->

altText

String

代替テキスト。ユーザーがメッセージを受信した際に、端末の通知やトークリスト、[引用メッセージ](https://developers.line.biz/ja/docs/messaging-api/sending-messages/#send-quote-messages)でテンプレートメッセージの代替として表示されます。\
Unicode絵文字を含めることができます。\
最大文字数：1500

<!-- parameter end -->
<!-- parameter start (props: required) -->

template

Object

[ボタン](https://developers.line.biz/ja/reference/messaging-api/#buttons)、[確認](https://developers.line.biz/ja/reference/messaging-api/#confirm)、[カルーセル](https://developers.line.biz/ja/reference/messaging-api/#carousel)、または[画像カルーセル](https://developers.line.biz/ja/reference/messaging-api/#image-carousel)オブジェクト

<!-- parameter end -->

#### ボタンテンプレート 

画像、タイトル、テキストに加えて、複数のアクションボタンが含まれたテンプレートです。

<!-- parameter start (props: required) -->

type

String

`buttons`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

thumbnailImageUrl

String

画像のURL（最大文字数：2000）\
プロトコル：HTTPS（TLS 1.2以降）\
画像フォーマット：JPEGまたはPNG\
最大横幅サイズ：1024px\
最大ファイルサイズ：10MB

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- tip start -->

**推奨ファイルサイズ**

画像のファイルメッセージの表示が遅延することを防ぐために、個々の画像ファイルサイズを小さくしてください（1MB以下推奨）。

<!-- tip end -->

<!-- parameter end -->
<!-- parameter start (props: optional) -->

imageAspectRatio

String

画像のアスペクト比。以下のいずれかの値を指定します。

- `rectangle`：1.51:1
- `square`：1:1

デフォルト値は`rectangle`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

imageSize

String

画像の表示形式。以下のいずれかの値を指定します。

- `cover`：画像領域全体に画像を表示します。画像領域に収まらない部分は切り詰められます。
- `contain`：画像領域に画像全体を表示します。縦長の画像では左右に、横長の画像では上下に余白が表示されます。

デフォルト値は`cover`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

imageBackgroundColor

String

画像の背景色。RGB値で設定します。デフォルト値は`#FFFFFF`（白）です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

title

String

タイトル\
最大文字数：40

<!-- parameter end -->
<!-- parameter start (props: required) -->

text

String

メッセージテキスト\
画像もタイトルも指定しない場合の最大文字数：160\
画像またはタイトルを指定する場合の最大文字数：60

<!-- parameter end -->
<!-- parameter start (props: optional) -->

defaultAction

[アクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#action-objects)

画像、タイトル、テキストの領域全体に対して設定できる、タップされたときのアクション

<!-- parameter end -->
<!-- parameter start (props: required) -->

actions

[アクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#action-objects)の配列

タップされたときのアクション\
最大件数：4

<!-- parameter end -->

_ボタンテンプレートメッセージの例_

<!-- tab start `json` -->

```json
{
  "type": "template",
  "altText": "This is a buttons template",
  "template": {
    "type": "buttons",
    "thumbnailImageUrl": "https://example.com/bot/images/image.jpg",
    "imageAspectRatio": "rectangle",
    "imageSize": "cover",
    "imageBackgroundColor": "#FFFFFF",
    "title": "Menu",
    "text": "Please select",
    "defaultAction": {
      "type": "uri",
      "label": "View detail",
      "uri": "http://example.com/page/123"
    },
    "actions": [
      {
        "type": "postback",
        "label": "Buy",
        "data": "action=buy&itemid=123"
      },
      {
        "type": "postback",
        "label": "Add to cart",
        "data": "action=add&itemid=123"
      },
      {
        "type": "uri",
        "label": "View detail",
        "uri": "http://example.com/page/123"
      }
    ]
  }
}
```

<!-- tab end -->

#### 確認テンプレート 

2つのアクションボタンを表示するテンプレートです。

<!-- parameter start (props: required) -->

type

String

`confirm`

<!-- parameter end -->
<!-- parameter start (props: required) -->

text

String

メッセージのテキスト\
最大文字数：240

<!-- parameter end -->
<!-- parameter start (props: required) -->

actions

[アクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#action-objects)の配列

タップされたときのアクション\
2つのボタンに1つずつアクションを設定します。

<!-- parameter end -->

_確認テンプレートメッセージの例_

<!-- tab start `json` -->

```json
{
  "type": "template",
  "altText": "this is a confirm template",
  "template": {
    "type": "confirm",
    "text": "Are you sure?",
    "actions": [
      {
        "type": "message",
        "label": "Yes",
        "text": "yes"
      },
      {
        "type": "message",
        "label": "No",
        "text": "no"
      }
    ]
  }
}
```

<!-- tab end -->

#### カルーセルテンプレート 

複数のカラムを表示するテンプレートです。カラムは横にスクロールして順番に表示できます。

<!-- parameter start (props: required) -->

type

String

`carousel`

<!-- parameter end -->
<!-- parameter start (props: required) -->

columns

[カラムオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#column-object-for-carousel)の配列

カラムの配列\
最大カラム数：10

<!-- parameter end -->
<!-- parameter start (props: optional) -->

imageAspectRatio

String

画像のアスペクト比。以下のいずれかの値を指定します。

- `rectangle`：1.51:1
- `square`：1:1

すべてのカラムに適用されます。デフォルト値は`rectangle`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

imageSize

String

画像の表示形式。以下のいずれかの値を指定します。

- `cover`：画像領域全体に画像を表示します。画像領域に収まらない部分は切り詰められます。
- `contain`：画像領域に画像全体を表示します。縦長の画像では左右に、横長の画像では上下に余白が表示されます。

すべてのカラムに適用されます。デフォルト値は`cover`です。

<!-- parameter end -->

_カルーセルテンプレートメッセージの例_

<!-- tab start `json` -->

```json
{
  "type": "template",
  "altText": "this is a carousel template",
  "template": {
    "type": "carousel",
    "columns": [
      {
        "thumbnailImageUrl": "https://example.com/bot/images/item1.jpg",
        "imageBackgroundColor": "#FFFFFF",
        "title": "this is menu",
        "text": "description",
        "defaultAction": {
          "type": "uri",
          "label": "View detail",
          "uri": "http://example.com/page/123"
        },
        "actions": [
          {
            "type": "postback",
            "label": "Buy",
            "data": "action=buy&itemid=111"
          },
          {
            "type": "postback",
            "label": "Add to cart",
            "data": "action=add&itemid=111"
          },
          {
            "type": "uri",
            "label": "View detail",
            "uri": "http://example.com/page/111"
          }
        ]
      },
      {
        "thumbnailImageUrl": "https://example.com/bot/images/item2.jpg",
        "imageBackgroundColor": "#000000",
        "title": "this is menu",
        "text": "description",
        "defaultAction": {
          "type": "uri",
          "label": "View detail",
          "uri": "http://example.com/page/222"
        },
        "actions": [
          {
            "type": "postback",
            "label": "Buy",
            "data": "action=buy&itemid=222"
          },
          {
            "type": "postback",
            "label": "Add to cart",
            "data": "action=add&itemid=222"
          },
          {
            "type": "uri",
            "label": "View detail",
            "uri": "http://example.com/page/222"
          }
        ]
      }
    ],
    "imageAspectRatio": "rectangle",
    "imageSize": "cover"
  }
}
```

<!-- tab end -->

##### カルーセルのカラムオブジェクト 

<!-- parameter start (props: optional) -->

thumbnailImageUrl

String

画像のURL（最大文字数：2000）\
プロトコル：HTTPS（TLS 1.2以降）\
画像フォーマット：JPEGまたはPNG\
アスペクト比：1.51:1（幅：高さ）\
最大横幅サイズ：1024px\
最大ファイルサイズ：10MB

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- tip start -->

**推奨ファイルサイズ**

画像のファイルメッセージの表示が遅延することを防ぐために、個々の画像ファイルサイズを小さくしてください（1MB以下推奨）。

<!-- tip end -->

<!-- parameter end -->
<!-- parameter start (props: optional) -->

imageBackgroundColor

String

画像の背景色。RGB値で設定します。デフォルト値は`#FFFFFF`（白）です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

title

String

タイトル\
最大文字数：40

<!-- parameter end -->
<!-- parameter start (props: required) -->

text

String

メッセージテキスト\
画像もタイトルも指定しない場合の最大文字数：120\
画像またはタイトルを指定する場合の最大文字数：60

<!-- parameter end -->
<!-- parameter start (props: optional) -->

defaultAction

[アクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#action-objects)

画像、タイトル、テキストの領域全体に対して設定できる、タップされたときのアクション

<!-- parameter end -->
<!-- parameter start (props: required) -->

actions

[アクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#action-objects)の配列

タップされたときのアクション\
最大件数：3

<!-- parameter end -->

<!-- note start -->

**注意**

各カラムのアクションの数は同じにします。画像またはタイトルの有無も、各カラムで統一してください。

<!-- note end -->

#### 画像カルーセルテンプレート 

複数の画像を表示するテンプレートです。画像は横にスクロールして順番に表示できます。

<!-- parameter start (props: required) -->

type

String

`image_carousel`

<!-- parameter end -->
<!-- parameter start (props: required) -->

columns

[カラムオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#column-object-for-image-carousel)の配列

カラムの配列\
最大カラム数：10

<!-- parameter end -->

_画像カルーセルテンプレートメッセージの例_

<!-- tab start `json` -->

```json
{
  "type": "template",
  "altText": "this is a image carousel template",
  "template": {
    "type": "image_carousel",
    "columns": [
      {
        "imageUrl": "https://example.com/bot/images/item1.jpg",
        "action": {
          "type": "postback",
          "label": "Buy",
          "data": "action=buy&itemid=111"
        }
      },
      {
        "imageUrl": "https://example.com/bot/images/item2.jpg",
        "action": {
          "type": "message",
          "label": "Yes",
          "text": "yes"
        }
      },
      {
        "imageUrl": "https://example.com/bot/images/item3.jpg",
        "action": {
          "type": "uri",
          "label": "View detail",
          "uri": "http://example.com/page/222"
        }
      }
    ]
  }
}
```

<!-- tab end -->

##### 画像カルーセルのカラムオブジェクト 

<!-- parameter start (props: required) -->

imageUrl

String

画像のURL（最大文字数：2000）\
プロトコル：HTTPS（TLS 1.2以降）\
画像フォーマット：JPEGまたはPNG\
アスペクト比：1:1（幅：高さ）\
最大横幅サイズ：1024px\
最大ファイルサイズ：10MB

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- tip start -->

**推奨ファイルサイズ**

画像のファイルメッセージの表示が遅延することを防ぐために、個々の画像ファイルサイズを小さくしてください（1MB以下推奨）。

<!-- tip end -->

<!-- parameter end -->
<!-- parameter start (props: required) -->

action

[アクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#action-objects)

画像がタップされたときのアクション

<!-- parameter end -->

### Flex Message 

Flex Messageは、[CSS Flexible Box（CSS Flexbox）](https://www.w3.org/TR/css-flexbox-1/)の基礎知識を使って、レイアウトを自由にカスタマイズできるメッセージです。Flex Messageの概要については、『Messaging APIドキュメント』の「[Flex Messageを送信する](https://developers.line.biz/ja/docs/messaging-api/using-flex-messages/)」を参照してください。

- [コンテナ](https://developers.line.biz/ja/reference/messaging-api/#container)
  - [バブル](https://developers.line.biz/ja/reference/messaging-api/#bubble)
  - [カルーセル](https://developers.line.biz/ja/reference/messaging-api/#f-carousel)
- [コンポーネント](https://developers.line.biz/ja/reference/messaging-api/#flex-component)
  - [ボックス](https://developers.line.biz/ja/reference/messaging-api/#box)
  - [ボタン](https://developers.line.biz/ja/reference/messaging-api/#button)
  - [画像](https://developers.line.biz/ja/reference/messaging-api/#f-image)
  - [動画](https://developers.line.biz/ja/reference/messaging-api/#f-video)
  - [アイコン](https://developers.line.biz/ja/reference/messaging-api/#icon)
  - [テキスト](https://developers.line.biz/ja/reference/messaging-api/#f-text)
  - [スパン](https://developers.line.biz/ja/reference/messaging-api/#span)
  - [セパレータ](https://developers.line.biz/ja/reference/messaging-api/#separator)
  - [フィラー](https://developers.line.biz/ja/reference/messaging-api/#filler)（非推奨）

<!-- parameter start (props: required) -->

type

String

`flex`

<!-- parameter end -->
<!-- parameter start (props: required) -->

altText

String

代替テキスト。ユーザーがメッセージを受信した際に、端末の通知やトークリスト、[引用メッセージ](https://developers.line.biz/ja/docs/messaging-api/sending-messages/#send-quote-messages)でFlex Messageの代替として表示されます。\
Unicode絵文字を含めることができます。\
最大文字数：1500

<!-- parameter end -->
<!-- parameter start (props: required) -->

contents

Object

Flex Messageの[コンテナ](https://developers.line.biz/ja/reference/messaging-api/#container)

<!-- parameter end -->

_Flex Messageの例_

<!-- tab start `json` -->

```json
{
  "type": "flex",
  "altText": "this is a flex message",
  "contents": {
    "type": "bubble",
    "body": {
      "type": "box",
      "layout": "vertical",
      "contents": [
        {
          "type": "text",
          "text": "hello"
        },
        {
          "type": "text",
          "text": "world"
        }
      ]
    }
  }
}
```

<!-- tab end -->

#### 動作環境 

Flex Messageは、すべてのバージョンのLINEでサポートされます。なお、以下の機能は、LINEの特定のバージョンのみサポートしています。

| 機能 | iOS版LINE<br>Android版LINE | PC版LINE<br>（macOS版、Windows版） |
| --- | :-: | :-: |
| <ul><li>[ボックス](https://developers.line.biz/ja/reference/messaging-api/#box)の`maxWidth`プロパティ</li><li>[ボックス](https://developers.line.biz/ja/reference/messaging-api/#box)の`maxHeight`プロパティ</li><li>[テキスト](https://developers.line.biz/ja/reference/messaging-api/#f-text)の`lineSpacing`プロパティ</li><li>[動画](https://developers.line.biz/ja/reference/messaging-api/#f-video) ※1</li></ul> | 11.22.0以上 | 7.7.0以上 |
| <ul><li>[バブル](https://developers.line.biz/ja/reference/messaging-api/#bubble)の`size`プロパティの`deca`と`hecto` ※2</li><li>[ボタン](https://developers.line.biz/ja/reference/messaging-api/#button)、[テキスト](https://developers.line.biz/ja/reference/messaging-api/#f-text)、および[アイコン](https://developers.line.biz/ja/reference/messaging-api/#icon)の`scaling`プロパティ</li></ul> | 13.6.0以上 | 7.17.0以上 |

※1 動画をサポートしていないLINEのバージョンにおいてもコンテンツを適切に表示するには、`altContent`プロパティを指定します。このプロパティで指定した画像が動画の代わりに表示されます。

※2 LINEのバージョンが`deca`と`hecto`をサポートするバージョンに満たない場合、バブルのサイズは`kilo`として表示されます。

#### コンテナ 

コンテナは、Flex Messageの最上位の構造です。以下のタイプのコンテナを利用できます。

- [バブル](https://developers.line.biz/ja/reference/messaging-api/#bubble)
- [カルーセル](https://developers.line.biz/ja/reference/messaging-api/#f-carousel)

コンテナのJSONデータのサンプルや用途については、『Messaging APIドキュメント』の「[Flex Messageの要素](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/)」を参照してください。

##### バブル 

1つのメッセージバブルを構成するコンテナです。ヘッダー、ヒーロー、ボディ、およびフッターの4つのブロックを含めることができます。各ブロックの用途について詳しくは、『Messaging APIドキュメント』の「[ブロック](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/#block)」を参照してください。

バブルを定義するJSONデータの最大サイズは、30KBです。

<!-- parameter start (props: required) -->

type

String

`bubble`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

size

String

バブルの大きさ。`nano`、`micro`、`deca`、`hecto`、`kilo`、`mega`、`giga`のいずれかの値を指定できます。デフォルト値は`mega`です。

`deca`、`hecto`を使用できるLINEのバージョンは以下のとおりです。

- iOS版とAndroid版のLINE：13.6.0以降
- macOS版とWindows版のLINE：7.17.0以降

LINEのバージョンが`deca`と`hecto`をサポートするバージョンに満たない場合、バブルのサイズは`kilo`として表示されます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

direction

String

テキストの書字方向と、水平ボックス内でコンポーネントを配置する向き。以下のいずれかの値を指定します。

- `ltr`：テキストは左横書き、コンポーネントは左から右に配置
- `rtl`：テキストは右横書き、コンポーネントは右から左に配置

デフォルト値は`ltr`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

header

Object

ヘッダー。[ボックス](https://developers.line.biz/ja/reference/messaging-api/#box)を指定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

hero

Object

ヒーロー。[ボックス](https://developers.line.biz/ja/reference/messaging-api/#box)、[画像](https://developers.line.biz/ja/reference/messaging-api/#f-image)、[動画](https://developers.line.biz/ja/reference/messaging-api/#f-video)のいずれかを指定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

body

Object

ボディ。[ボックス](https://developers.line.biz/ja/reference/messaging-api/#box)を指定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

footer

Object

フッター。[ボックス](https://developers.line.biz/ja/reference/messaging-api/#box)を指定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

styles

Object

各ブロックのスタイル。[バブルスタイル](https://developers.line.biz/ja/reference/messaging-api/#bubble-style)を指定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

action

Object

バブルがタップされたときのアクション。[アクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#action-objects)を指定します。

<!-- parameter end -->

_バブルの例_

<!-- tab start `json` -->

```json
{
  "type": "bubble",
  "header": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "text",
        "text": "Header text"
      }
    ]
  },
  "hero": {
    "type": "image",
    "url": "https://example.com/flex/images/image.jpg"
  },
  "body": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "text",
        "text": "Body text"
      }
    ]
  },
  "footer": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "text",
        "text": "Footer text"
      }
    ]
  },
  "styles": {
    "comment": "See the example of a bubble style object"
  }
}
```

<!-- tab end -->

##### ブロックのスタイルを定義するオブジェクト 

バブル内のブロックのスタイルは、以下の2つのオブジェクトを使って定義します。

_バブルスタイルとブロックスタイルの例_

<!-- tab start `json` -->

```json
  "styles": {
    "header": {
      "backgroundColor": "#00ffff"
    },
    "hero": {
      "separator": true,
      "separatorColor": "#000000"
    },
    "footer": {
      "backgroundColor": "#00ffff",
      "separator": true,
      "separatorColor": "#000000"
    }
  }
```

<!-- tab end -->

###### バブルスタイル 

<!-- parameter start (props: optional) -->

header

Object

ヘッダーのスタイル。[ブロックスタイル](https://developers.line.biz/ja/reference/messaging-api/#block-style)を指定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

hero

Object

ヒーローのスタイル。[ブロックスタイル](https://developers.line.biz/ja/reference/messaging-api/#block-style)を指定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

body

Object

ボディのスタイル。[ブロックスタイル](https://developers.line.biz/ja/reference/messaging-api/#block-style)を指定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

footer

Object

フッターのスタイル。[ブロックスタイル](https://developers.line.biz/ja/reference/messaging-api/#block-style)を指定します。

<!-- parameter end -->

###### ブロックスタイル 

<!-- parameter start (props: optional) -->

backgroundColor

String

ブロックの背景色。16進数カラーコードで設定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

separator

Boolean

ブロックの上にセパレータを配置する場合は`true`を指定します。デフォルト値は`false`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

separatorColor

String

セパレータの色。16進数カラーコードで設定します。

<!-- parameter end -->

<!-- note start -->

**注意**

先頭のブロックの上にはセパレータを配置できません。

<!-- note end -->

##### カルーセル 

カルーセルは、子要素として1つ以上のバブルを持つコンテナです。カルーセル内のバブルは、横にスクロールして閲覧できます。

カルーセルを定義するJSONデータの最大サイズは、50KBです。

<!-- parameter start (props: required) -->

type

String

`carousel`

<!-- parameter end -->
<!-- parameter start (props: required) -->

contents

Array of objects

このカルーセル内の[バブル](https://developers.line.biz/ja/reference/messaging-api/#bubble)。最大バブル数：12

<!-- parameter end -->

<!-- note start -->

**バブルの幅**

1つのカルーセルに、異なる幅（`size`プロパティ）のバブルを含めることはできません。バブルの幅は、カルーセルごとに揃えてください。

<!-- note end -->

<!-- tip start -->

**バブルの高さ**

カルーセルの中で最大の高さのバブルと一致するように、各バブルのボディが伸長します。ただし、ボディがないバブルの大きさは変わりません。

<!-- tip end -->

_カルーセルの例_

<!-- tab start `json` -->

```json
{
  "type": "carousel",
  "contents": [
    {
      "type": "bubble",
      "body": {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "text",
            "text": "First bubble"
          }
        ]
      }
    },
    {
      "type": "bubble",
      "body": {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "text",
            "text": "Second bubble"
          }
        ]
      }
    }
  ]
}
```

<!-- tab end -->

#### コンポーネント 

コンポーネントは、ブロックを構成する要素です。以下のコンポーネントを利用できます。

- [ボックス](https://developers.line.biz/ja/reference/messaging-api/#box)
- [ボタン](https://developers.line.biz/ja/reference/messaging-api/#button)
- [画像](https://developers.line.biz/ja/reference/messaging-api/#f-image)
- [動画](https://developers.line.biz/ja/reference/messaging-api/#f-video)
- [アイコン](https://developers.line.biz/ja/reference/messaging-api/#icon)
- [テキスト](https://developers.line.biz/ja/reference/messaging-api/#f-text)
- [スパン](https://developers.line.biz/ja/reference/messaging-api/#span)
- [セパレータ](https://developers.line.biz/ja/reference/messaging-api/#separator)
- [フィラー](https://developers.line.biz/ja/reference/messaging-api/#filler)（非推奨）

各コンポーネントのJSONデータのサンプルや用途については、『Messaging APIドキュメント』の「[Flex Messageの要素](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/)」と「[Flex Messageのレイアウト](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/)」を参照してください。

##### ボックス 

ボックスは、水平または垂直のレイアウト方向を定義します。ボックスを含む、他のコンポーネントを含むことができます。

<!-- parameter start (props: required) -->

type

String

`box`

<!-- parameter end -->
<!-- parameter start (props: required) -->

layout

String

このボックス内のコンポーネントを配置する向き。詳しくは、『Messaging APIドキュメント』の「[ボックスコンポーネントの向き](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#box-component-orientation)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

contents

Array of objects

このボックス内のコンポーネント。以下のコンポーネントを指定できます。

- `layout`プロパティが`horizontal`または`vertical`の場合：[ボックス](https://developers.line.biz/ja/reference/messaging-api/#box)、[ボタン](https://developers.line.biz/ja/reference/messaging-api/#button)、[画像](https://developers.line.biz/ja/reference/messaging-api/#f-image)、[テキスト](https://developers.line.biz/ja/reference/messaging-api/#f-text)、[セパレータ](https://developers.line.biz/ja/reference/messaging-api/#separator)、および[フィラー](https://developers.line.biz/ja/reference/messaging-api/#filler)
- `layout`プロパティが`baseline`の場合：[アイコン](https://developers.line.biz/ja/reference/messaging-api/#icon)、[テキスト](https://developers.line.biz/ja/reference/messaging-api/#f-text)、および[フィラー](https://developers.line.biz/ja/reference/messaging-api/#filler)

なお、配列に指定した順に描画されます。空配列を指定することもできます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

backgroundColor

String

ボックスの背景色。RGBカラーに加えて、アルファチャネル（透明度）も設定できます。16進数カラーコードで設定します。（例：#RRGGBBAA）デフォルト値は`#00000000`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

borderColor

String

ボックスの境界線の色。16進数カラーコードで設定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

borderWidth

String

ボックスの境界線の太さ。ピクセルまたは`none`、`light`、`normal`、`medium`、`semi-bold`、`bold`のいずれかの値を指定できます。`none`では、境界線は描画されず、それ以外は列挙した順に太くなります。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

cornerRadius

String

ボックスの境界線の角を丸くするときの半径。ピクセル、または`none`、`xs`、`sm`、`md`、`lg`、`xl`、`xxl`のいずれかの値を指定できます。`none`では、角は丸くならず、それ以外は列挙した順に半径が大きくなります。デフォルト値は`none`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

width

String

ボックスの幅。%（親要素の幅を基準にした割合）またはピクセルを指定します。詳しくは、『Messaging APIドキュメント』の「[ボックスの幅](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#box-width)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

maxWidth

String

ボックスの最大幅。%（親要素の幅を基準にした割合）またはピクセルを指定します。詳しくは、『Messaging APIドキュメント』の「[ボックスの最大幅](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#box-max-width)」を参照してください。

このプロパティを使用できるLINEのバージョンは以下のとおりです。

- iOS版とAndroid版のLINE：11.22.0以降
- macOS版とWindows版のLINE：7.7.0以降

<!-- parameter end -->
<!-- parameter start (props: optional) -->

height

String

ボックスの高さ。%（親要素の高さを基準にした割合）またはピクセルを指定します。詳しくは、『Messaging APIドキュメント』の「[ボックスの高さ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#box-height)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

maxHeight

String

ボックスの最大高。%（親要素の高さを基準にした割合）またはピクセルを指定します。詳しくは、『Messaging APIドキュメント』の「[ボックスの最大高](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#box-max-height)」を参照してください。

このプロパティを使用できるLINEのバージョンは以下のとおりです。

- iOS版とAndroid版のLINE：11.22.0以降
- macOS版とWindows版のLINE：7.7.0以降

<!-- parameter end -->
<!-- parameter start (props: optional) -->

flex

Number

親要素内での、このコンポーネントの幅または高さの比率。詳しくは、『Messaging APIドキュメント』の「[コンポーネントのサイズ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-size)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

spacing

String

このボックス内のコンポーネント間の最小スペース。デフォルト値は`none`です。詳しくは、『Messaging APIドキュメント』の「[ボックスの`spacing`プロパティ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#spacing-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

margin

String

親要素内での、このコンポーネントの前に挿入する余白の最小サイズ。詳しくは、『Messaging APIドキュメント』の「[コンポーネントの`margin`プロパティ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#margin-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

paddingAll

String

このボックスの境界線と、子要素の間の余白。詳しくは、『Messaging APIドキュメント』の「[ボックスのパディングで子コンポーネントを配置する](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#padding-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

paddingTop

String

このボックスの上端の境界線と、子要素の上端の間の余白。詳しくは、『Messaging APIドキュメント』の「[ボックスのパディングで子コンポーネントを配置する](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#padding-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

paddingBottom

String

このボックスの下端の境界線と、子要素の下端の間の余白。詳しくは、『Messaging APIドキュメント』の「[ボックスのパディングで子コンポーネントを配置する](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#padding-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

paddingStart

String

- [バブル](https://developers.line.biz/ja/reference/messaging-api/#bubble)の書字方向がLTRの場合：このボックスの左端の境界線と、子要素の左端の間の余白
- [バブル](https://developers.line.biz/ja/reference/messaging-api/#bubble)の書字方向がRTLの場合：このボックスの右端の境界線と、子要素の右端の間の余白

詳しくは、『Messaging APIドキュメント』の「[ボックスのパディングで子コンポーネントを配置する](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#padding-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

paddingEnd

String

- [バブル](https://developers.line.biz/ja/reference/messaging-api/#bubble)の書字方向がLTRの場合：このボックスの右端の境界線と、子要素の右端の間の余白
- [バブル](https://developers.line.biz/ja/reference/messaging-api/#bubble)の書字方向がRTLの場合：このボックスの左端の境界線と、子要素の左端の間の余白

詳しくは、『Messaging APIドキュメント』の「[ボックスのパディングで子コンポーネントを配置する](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#padding-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

position

String

このボックスを配置する際の基準位置。以下のいずれかの値を指定します。

- `relative`：直前のボックスを基準にします。
- `absolute`：親要素の左上を基準にします。

デフォルト値は`relative`です。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetTop

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetBottom

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetStart

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetEnd

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

action

Object

タップされたときのアクション。[アクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#action-objects)を指定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

justifyContent

String

親要素の主軸に沿った子要素の配置。親要素が水平ボックスの場合、子要素の`flex`プロパティを0に指定したときのみ動作します。詳しくは、『Messaging APIドキュメント』の「[余白を使った子コンポーネントの配置](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#justify-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

alignItems

String

親要素の交差軸に沿った子要素の配置。詳しくは、『Messaging APIドキュメント』の「[余白を使った子コンポーネントの配置](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#justify-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

background.type

String

背景の種類。以下の値を指定します。

- `linearGradient`：線形グラデーション。詳しくは、『Messaging APIドキュメント』の「[線形グラデーション背景](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#linear-gradient-bg)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

background.angle

String

線形グラデーションの勾配の角度。0度以上、360度未満の範囲で、`90deg`（90度）や`23.5deg`（23.5度）のように整数または小数で角度を指定します。`0deg`は下から上、`45deg`は左下から右上、`90deg`は左から右、`180deg`は上から下のように数字が増えると時計回りで角度が変わります。詳しくは、『Messaging APIドキュメント』の「[線形グラデーションの角度](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#linear-gradient-bg-angle)」を参照してください。

`background.type`が`linearGradient`の場合は必須です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

background.startColor

String

グラデーションの開始点の色。`#RRGGBB`または`#RRGGBBAA`のような16進数カラーコードで設定します。

`background.type`が`linearGradient`の場合は必須です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

background.endColor

String

グラデーションの終了点の色。`#RRGGBB`または`#RRGGBBAA`のような16進数カラーコードで設定します。

`background.type`が`linearGradient`の場合は必須です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

background.centerColor

String

グラデーションの中間色。`#RRGGBB`または`#RRGGBBAA`のような16進数カラーコードで設定します。`background.centerColor`を指定すると3色のグラデーションになります。詳しくは、『Messaging APIドキュメント』の「[グラデーションの中間色](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#linear-gradient-bg-center-color)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

background.centerPosition

String

中間色の位置。開始点の`0%`から、終了点の`100%`の範囲で整数または小数を指定します。デフォルト値は`50%`です。詳しくは、『Messaging APIドキュメント』の「[グラデーションの中間色](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#linear-gradient-bg-center-color)」を参照してください。

<!-- parameter end -->

_ボックスの例_

<!-- tab start `json` -->

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "image",
        "url": "https://example.com/flex/images/image.jpg"
      },
      {
        "type": "separator"
      },
      {
        "type": "text",
        "text": "Text in the box"
      },
      {
        "type": "box",
        "layout": "vertical",
        "contents": [],
        "width": "30px",
        "height": "30px",
        "background": {
          "type": "linearGradient",
          "angle": "90deg",
          "startColor": "#FFFF00",
          "endColor": "#0080ff"
        }
      }
    ],
    "height": "400px",
    "justifyContent": "space-evenly",
    "alignItems": "center"
  }
}
```

<!-- tab end -->

##### ボタン 

ボタンを描画するコンポーネントです。ユーザーが、ボタンをタップしたときに実行される、[アクション](https://developers.line.biz/ja/docs/messaging-api/actions/)を指定できます。

<!-- parameter start (props: required) -->

type

String

`button`

<!-- parameter end -->
<!-- parameter start (props: required) -->

action

Object

タップされたときのアクション。[アクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#action-objects)を指定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

flex

Number

親要素内での、このコンポーネントの幅または高さの比率。水平ボックス内のコンポーネントでは、`flex`プロパティのデフォルト値は`1`です。垂直ボックス内のコンポーネントでは、`flex`プロパティのデフォルト値は`0`です。詳しくは、『Messaging APIドキュメント』の「[コンポーネントのサイズ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-size)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

margin

String

親要素内での、このコンポーネントの前に挿入する余白の最小サイズ。詳しくは、『Messaging APIドキュメント』の「[コンポーネントの`margin`プロパティ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#margin-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

position

String

`offsetTop`、`offsetBottom`、`offsetStart`、`offsetEnd`の基準。以下のいずれかの値を指定します。

- `relative`：直前のボックスを基準にします。
- `absolute`：親要素の左上を基準にします。

デフォルト値は`relative`です。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetTop

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetBottom

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetStart

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetEnd

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

height

String

ボタンの高さ。`sm`または`md`のいずれかの値を指定できます。デフォルト値は`md`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

style

String

ボタンの表示形式。以下のいずれかの値を指定します。

- `primary`：濃色のボタン向けのスタイル
- `secondary`：淡色のボタン向けのスタイル
- `link`：HTMLのリンクのスタイル。

デフォルト値は`link`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

color

String

`style`プロパティが`link`の場合は文字の色。`style`プロパティが`primary`または`secondary`の場合は背景色です。16進数カラーコードで設定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

gravity

String

垂直方向の位置合わせ方式。詳しくは、『Messaging APIドキュメント』の「[テキスト、画像、ボタンを垂直方向に整列させる](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#gravity-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

adjustMode

String

テキストのフォントサイズを調整する方式。以下の値を指定します。

- `shrink-to-fit`：コンポーネントの幅に合わせて自動縮小されます。このプロパティはベストエフォートで機能しますので、プラットフォームによって動作が異なる、あるいは動作しないことがあります。詳しくは、『Messaging APIドキュメント』の「[フォントサイズの自動縮小](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#adjusts-fontsize-to-fit)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

scaling

Boolean

`true`を指定すると、LINEアプリのフォントサイズ設定に応じて、テキストのフォントサイズが自動的に拡大縮小されます。デフォルト値は`false`です。詳しくは、『Messaging APIドキュメント』の「[フォントサイズ設定に応じたサイズへの拡大縮小](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#size-scaling)」を参照してください。

このプロパティを使用できるLINEのバージョンは以下のとおりです。

- iOS版とAndroid版のLINE：13.6.0以降
- macOS版とWindows版のLINE：7.17.0以降

<!-- parameter end -->

_ボタンの例_

<!-- tab start `json` -->

```json
{
  "type": "button",
  "action": {
    "type": "uri",
    "label": "Tap me",
    "uri": "https://example.com"
  },
  "style": "primary",
  "color": "#0000ff"
}
```

<!-- tab end -->

##### 画像 

画像を描画するコンポーネントです。

<!-- parameter start (props: required) -->

type

String

`image`

<!-- parameter end -->
<!-- parameter start (props: required) -->

url

String

画像のURL（最大文字数：2000）\
プロトコル：HTTPS（TLS 1.2以降）\
画像フォーマット：JPEGまたはPNG\
最大画像サイズ：1024 x 1024ピクセル\
最大ファイルサイズ：10MB（`animated`プロパティが`true`の場合は300KB）

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- tip start -->

**推奨ファイルサイズ**

メッセージの表示が遅延することを防ぐために、個々の画像ファイルサイズを小さくしてください（1MB以下推奨）。

<!-- tip end -->

<!-- parameter end -->
<!-- parameter start (props: optional) -->

flex

Number

親要素内での、このコンポーネントの幅または高さの比率。詳しくは、『Messaging APIドキュメント』の「[コンポーネントのサイズ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-size)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

margin

String

親要素内での、このコンポーネントの前に挿入する余白の最小サイズ。詳しくは、『Messaging APIドキュメント』の「[コンポーネントの`margin`プロパティ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#margin-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

position

String

`offsetTop`、`offsetBottom`、`offsetStart`、`offsetEnd`の基準。以下のいずれかの値を指定します。

- `relative`：直前のボックスを基準にします。
- `absolute`：親要素の左上を基準にします。

デフォルト値は`relative`です。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetTop

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetBottom

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetStart

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetEnd

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

align

String

水平方向の位置合わせ方式。詳しくは、『Messaging APIドキュメント』の「[テキストや画像を水平方向に整列させる](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#align-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

gravity

String

垂直方向の位置合わせ方式。詳しくは、『Messaging APIドキュメント』の「[テキスト、画像、ボタンを垂直方向に整列させる](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#gravity-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

size

String

画像の幅の最大サイズ。デフォルト値は`md`です。詳しくは、『Messaging APIドキュメント』の「[画像のサイズ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#image-size)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

aspectRatio

String

画像のアスペクト比。`{幅}:{高さ}`の形式で指定します。`{幅}`と`{高さ}`は、それぞれ1～100000の値で入力します。ただし、`{高さ}`には`{幅}`の3倍を超える値は指定できません。デフォルト値は`1:1`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

aspectMode

String

画像のアスペクト比と`aspectRatio`プロパティで指定されるアスペクト比が一致しない場合の、画像の表示方式。詳しくは、「[描画領域について](https://developers.line.biz/ja/reference/messaging-api/#drawing-area)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

backgroundColor

String

画像の背景色。16進数カラーコードで設定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

action

Object

タップされたときのアクション。[アクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#action-objects)を指定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

animated

Boolean

`true`を指定すると画像（APNG）のアニメーションを再生します。メッセージ全体で10枚の画像まで`true`を指定できます。上限を超えて指定した場合、メッセージは送信できません。デフォルト値は`false`です。データサイズが300KBを超える場合は再生されません。

<!-- parameter end -->

<!-- tip start -->

**アニメーション画像の作成方法**

アニメーションの画像はAPNG作成ツールを使用して作成してください。APNGの作成方法は、アニメーションスタンプの作成方法を参考にしてください。詳しくは、LINE Creators Marketにあるアニメーションスタンプの[制作ガイドライン](https://creator.line.me/ja/guideline/animationsticker/)を参照してください。

<!-- tip end -->

<!-- note start -->

**アニメーション画像が再生されないときは？**

「画像は表示されるがアニメーションが再生されない」というときは、以下を確認してください。

- `animated`プロパティの値を`true`にしているか
- 画像のデータサイズが300KB以下か

またメッセージを受信したLINEアプリの設定に起因して、アニメーションが再生されない場合もあります。併せて以下も確認してください。

- LINEアプリの設定で`GIF自動再生`がオンになっているか

アニメーションはAPNGの`acTL`チャンクの`num_plays`フィールドで指定した回数分、ループ再生されます。0を指定することで無限にループ再生も可能です。

<!-- note end -->

_画像の例_

<!-- tab start `json` -->

```json
{
  "type": "image",
  "url": "https://example.com/flex/images/image.jpg",
  "size": "full",
  "aspectRatio": "1.91:1"
}
```

<!-- tab end -->

###### 描画領域について 

`size`プロパティで画像の最大の幅を指定し、`aspectRatio`プロパティで画像のアスペクト比（幅：高さの比率）を指定します。`size`プロパティと`aspectRatio`プロパティで決定される矩形の領域を、**描画領域**と呼びます。この描画領域に画像が表示されます。

- `flex`プロパティによって算出された[コンポーネントの幅](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-size)が、`size`プロパティで指定された画像の幅よりも小さい場合、描画領域の幅はコンポーネントの幅に縮小されます。
- 画像のアスペクト比と`aspectRatio`プロパティで指定されるアスペクト比が一致しない場合、`aspectMode`プロパティに基づいて画像が表示されます。デフォルト値は`fit`です。
  - `aspectMode`が`cover`の場合：描画領域全体に画像を表示します。描画領域に収まらない部分は切り詰められます。
  - `aspectMode`が`fit`の場合：描画領域に画像全体を表示します。縦長の画像では左右に、横長の画像では上下に背景が表示されます。

##### 動画 

動画を描画するコンポーネントです。

動画を使用できるLINEのバージョンは以下のとおりです。

- iOS版とAndroid版のLINE：11.22.0以降
- macOS版とWindows版のLINE：7.7.0以降

LINEのバージョンが動画をサポートするバージョンに満たない場合、動画の`altContent`プロパティに指定したコンポーネントが代替コンテンツとして表示されます。

<!-- note start -->

**動画が正しく再生できない**

動画を含むメッセージの送信に成功したとしても、ユーザーの端末上で動画を正しく再生できない場合があります。詳しくは、FAQの「[メッセージとして送信した動画が再生できないのはなぜですか？](https://developers.line.biz/ja/faq/#why-cant-i-play-a-video-i-sent)」を参照してください。

<!-- note end -->

<!-- note start -->

**動画のアスペクト比**

一定以上に縦長・横長の動画を送信した場合、一部の環境では動画の一部が欠けて表示される場合があります。

また、`url`プロパティで指定する動画のアスペクト比と、以下の2つのアスペクト比は一致させてください。アスペクト比が異なると、予期せぬレイアウトになることがあります。

- `aspectRatio`プロパティで指定するアスペクト比
- `previewUrl`プロパティで指定するプレビュー画像のアスペクト比

![LINEのトークルームの動画。アスペクト比16:9の映像の背面に、アスペクト比1:1のプレビュー映像が表示されています。](https://developers.line.biz/media/messaging-api/messages/image-overlapping-ja.png)

<!-- note end -->

<!-- note start -->

**動画コンポーネントの使用条件**

動画コンポーネントを使うには、以下の条件をすべて満たす必要があります。

- 動画コンポーネントをヒーローの[ブロック](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/#block)直下に指定する。
- バブルの`size`プロパティに`kilo` `mega` `giga`のいずれかを指定する。
- バブルがカルーセルの子要素ではない。

<!-- note end -->

<!-- parameter start (props: required) -->

type

String

`video`

<!-- parameter end -->
<!-- parameter start (props: required) -->

url

String

動画ファイルのURL（最大文字数：2000）\
プロトコル：HTTPS（TLS 1.2以降）\
動画フォーマット：mp4\
最大ファイルサイズ：200MB

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

previewUrl

String

プレビュー画像のURL（最大文字数：2000）\
プロトコル：HTTPS（TLS 1.2以降）\
画像フォーマット：JPEGまたはPNG\
最大ファイルサイズ：1MB

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

altContent

component

代替コンテンツ。動画コンポーネントをサポートするバージョン未満のLINEで表示されます。[ボックス](https://developers.line.biz/ja/reference/messaging-api/#box)または[画像](https://developers.line.biz/ja/reference/messaging-api/#f-image)を指定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

aspectRatio

String

動画のアスペクト比。`{幅}:{高さ}`の形式で指定します。`{幅}`と`{高さ}`は、それぞれ1～100000の値で入力します。ただし、`{高さ}`には`{幅}`の3倍を超える値は指定できません。デフォルト値は`1:1`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

action

Object

[URIアクション](https://developers.line.biz/ja/reference/messaging-api/#uri-action)。詳しくは、『Messaging APIドキュメント』の「[URIアクション](https://developers.line.biz/ja/docs/messaging-api/create-flex-message-including-video/#uri-action)」を参照してください。

<!-- parameter end -->

_動画の例_

<!-- tab start `json` -->

```json
{
  "type": "bubble",
  "size": "mega",
  "hero": {
    "type": "video",
    "url": "https://example.com/video.mp4",
    "previewUrl": "https://example.com/video_preview.jpg",
    "altContent": {
      "type": "image",
      "size": "full",
      "aspectRatio": "20:13",
      "aspectMode": "cover",
      "url": "https://example.com/image.jpg"
    },
    "aspectRatio": "20:13"
  }
}
```

<!-- tab end -->

##### アイコン 

隣接するテキストを装飾するために、アイコンを描画するコンポーネントです。このコンポーネントは、[ベースラインボックス](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#baseline-box)内でのみ使用できます。

<!-- parameter start (props: required) -->

type

String

`icon`

<!-- parameter end -->
<!-- parameter start (props: required) -->

url

String

画像のURL（最大文字数：2000）\
プロトコル：HTTPS（TLS 1.2以降）\
画像フォーマット：JPEGまたはPNG\
最大画像サイズ：1024 x 1024ピクセル\
最大ファイルサイズ：1MB

URLはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

margin

String

親要素内での、このコンポーネントの前に挿入する余白の最小サイズ。詳しくは、『Messaging APIドキュメント』の「[コンポーネントの`margin`プロパティ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#margin-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

position

String

`offsetTop`、`offsetBottom`、`offsetStart`、`offsetEnd`の基準。以下のいずれかの値を指定します。

- `relative`：直前のボックスを基準にします。
- `absolute`：親要素の左上を基準にします。

デフォルト値は`relative`です。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetTop

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetBottom

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetStart

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetEnd

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

size

String

アイコンの幅の最大サイズ。デフォルト値は`md`です。詳しくは、『Messaging APIドキュメント』の「[アイコン、テキスト、スパンのサイズ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#other-component-size)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

scaling

Boolean

`true`を指定すると、LINEアプリのフォントサイズ設定に応じて、アイコンが自動的に拡大縮小されます。デフォルト値は`false`です。詳しくは、『Messaging APIドキュメント』の「[フォントサイズ設定に応じたサイズへの拡大縮小](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#size-scaling)」を参照してください。

このプロパティを使用できるLINEのバージョンは以下のとおりです。

- iOS版とAndroid版のLINE：13.6.0以降
- macOS版とWindows版のLINE：7.17.0以降

<!-- parameter end -->
<!-- parameter start (props: optional) -->

aspectRatio

String

アイコンのアスペクト比。`{幅}:{高さ}`の形式で指定します。`{幅}`と`{高さ}`は、それぞれ1～100000の値で入力します。ただし、`{高さ}`には`{幅}`の3倍を超える値は指定できません。デフォルト値は`1:1`です。

<!-- parameter end -->

アイコンの`flex`プロパティの値は、`0`に固定されます。

_アイコンの例_

<!-- tab start `json` -->

```json
{
  "type": "icon",
  "url": "https://example.com/icon/png/caution.png",
  "size": "lg",
  "aspectRatio": "1.91:1"
}
```

<!-- tab end -->

##### テキスト 

文字列を描画するコンポーネントです。色、サイズ、および太さを指定できます。

<!-- parameter start (props: required) -->

type

String

`text`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

text

String

テキスト。`text`プロパティまたは`contents`プロパティのいずれかを必ず設定してください。`contents`プロパティを設定すると、`text`は無視されます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

contents

Array of objects

[スパン](https://developers.line.biz/ja/reference/messaging-api/#span)の配列。`text`プロパティまたは`contents`プロパティのいずれかを必ず設定してください。`contents`プロパティを設定すると、`text`は無視されます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

adjustMode

String

テキストのフォントサイズを調整する方式。以下の値を指定します。

- `shrink-to-fit`：コンポーネントの幅に合わせて自動縮小されます。このプロパティはベストエフォートで機能しますので、プラットフォームによって動作が異なる、あるいは動作しないことがあります。詳しくは、『Messaging APIドキュメント』の「[フォントサイズの自動縮小](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#adjusts-fontsize-to-fit)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

flex

Number

親要素内での、このコンポーネントの幅または高さの比率。詳しくは、『Messaging APIドキュメント』の「[コンポーネントのサイズ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-size)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

margin

String

親要素内での、このコンポーネントの前に挿入する余白の最小サイズ。詳しくは、『Messaging APIドキュメント』の「[コンポーネントの`margin`プロパティ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#margin-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

position

String

`offsetTop`、`offsetBottom`、`offsetStart`、`offsetEnd`の基準。以下のいずれかの値を指定します。

- `relative`：直前のボックスを基準にします。
- `absolute`：親要素の左上を基準にします。

デフォルト値は`relative`です。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetTop

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetBottom

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetStart

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

offsetEnd

String

オフセット。詳しくは、『Messaging APIドキュメント』の「[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

size

String

フォントサイズ。デフォルト値は`md`です。詳しくは、『Messaging APIドキュメント』の「[アイコン、テキスト、スパンのサイズ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#other-component-size)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

scaling

Boolean

`true`を指定すると、LINEアプリのフォントサイズ設定に応じて、テキストのフォントサイズが自動的に拡大縮小されます。デフォルト値は`false`です。詳しくは、『Messaging APIドキュメント』の「[フォントサイズ設定に応じたサイズへの拡大縮小](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#size-scaling)」を参照してください。

このプロパティが`true`の場合、`contents`プロパティで指定した[スパン](https://developers.line.biz/ja/reference/messaging-api/#span)のテキストも、フォントサイズが自動的に拡大縮小されます。

このプロパティを使用できるLINEのバージョンは以下のとおりです。

- iOS版とAndroid版のLINE：13.6.0以降
- macOS版とWindows版のLINE：7.17.0以降

<!-- parameter end -->
<!-- parameter start (props: optional) -->

align

String

水平方向の位置合わせ方式。詳しくは、『Messaging APIドキュメント』の「[テキストや画像を水平方向に整列させる](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#align-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

gravity

String

垂直方向の位置合わせ方式。デフォルト値は`top`です。詳しくは、『Messaging APIドキュメント』の「[テキスト、画像、ボタンを垂直方向に整列させる](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#gravity-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

wrap

Boolean

`true`を指定するとテキストを折り返します。デフォルト値は`false`です。`true`に設定した場合、改行文字（`\n`）を使って改行できます。詳しくは、『Messaging APIドキュメント』の「[テキストを折り返す](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/#text-wrap)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

lineSpacing

String

折り返したテキスト内の行間。0より大きい整数または小数をピクセルで指定します。開始行の上部と最終行の下部には適用されません。詳しくは、『Messaging APIドキュメント』の「[テキスト内の行間を広げる](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/#text-line-spacing)」を参照してください。

このプロパティを使用できるLINEのバージョンは以下のとおりです。

- iOS版とAndroid版のLINE：11.22.0以降
- macOS版とWindows版のLINE：7.7.0以降

<!-- parameter end -->
<!-- parameter start (props: optional) -->

maxLines

Number

最大行数。テキストがこの行数に収まらない場合は、最終行の末尾に省略記号（…）が表示されます。`0`ではすべてのテキストが表示されます。デフォルト値は`0`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

weight

String

フォントの太さ。`regular`、`bold`のいずれかの値を指定できます。`bold`を指定すると太字になります。デフォルト値は`regular`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

color

String

フォントの色。16進数カラーコードで設定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

action

Object

タップされたときのアクション。[アクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#action-objects)を指定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

style

String

テキストのスタイル。以下のいずれかの値を指定します。

- `normal`：標準
- `italic`：斜体デフォルト

値は`normal`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

decoration

String

テキストの装飾。以下のいずれかの値を指定します。

- `none`：装飾なし
- `underline`：下線
- `line-through`：取り消し線

デフォルト値は`none`です。

<!-- parameter end -->

_テキストの例_

<!-- tab start `json` -->

```json
{
  "type": "text",
  "text": "Hello, World!",
  "size": "xl",
  "weight": "bold",
  "color": "#0000ff"
}
```

<!-- tab end -->

##### スパン 

スタイルが異なる複数の文字列を描画するコンポーネントです。色、サイズ、太さ、および装飾を指定できます。スパンは、[テキスト](https://developers.line.biz/ja/reference/messaging-api/#f-text)の`contents`プロパティに設定します。

<!-- parameter start (props: required) -->

type

String

`span`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

text

String

テキスト。親のテキストの`wrap`プロパティを`true`に設定した場合は、改行文字（`\n`）を使って改行できます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

color

String

フォントの色。16進数カラーコードで設定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

size

String

フォントサイズ。詳しくは、『Messaging APIドキュメント』の「[アイコン、テキスト、スパンのサイズ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#other-component-size)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

weight

String

フォントの太さ。`regular`、`bold`のいずれかの値を指定できます。`bold`を指定すると太字になります。デフォルト値は`regular`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

style

String

テキストのスタイル。以下のいずれかの値を指定します。

- `normal`：標準
- `italic`：斜体

デフォルト値は`normal`です。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

decoration

String

テキストの装飾。以下のいずれかの値を指定します。

- `none`：装飾なし
- `underline`：下線
- `line-through`：取り消し線

デフォルト値は`none`です。

<!-- note start -->

**注意**

[テキスト](https://developers.line.biz/ja/reference/messaging-api/#f-text)の`decoration`プロパティで設定した装飾は、スパンの`decoration`プロパティで上書きできません。

<!-- note end -->

<!-- parameter end -->

_スパンの例_

<!-- tab start `json` -->

```json
{
  "type": "span",
  "text": "蛙",
  "size": "xxl",
  "weight": "bold",
  "style": "italic",
  "color": "#4f8f00"
}
```

<!-- tab end -->

##### セパレータ 

[ボックス](https://developers.line.biz/ja/reference/messaging-api/#box)内に分割線を描画するコンポーネントです。水平ボックスに含めた場合は垂直線、垂直ボックスに含めた場合は水平線が描画されます。

<!-- parameter start (props: required) -->

type

String

`separator`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

margin

String

親要素内での、このコンポーネントの前に挿入する余白の最小サイズ。詳しくは、『Messaging APIドキュメント』の「[コンポーネントの`margin`プロパティ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#margin-property)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

color

String

セパレータの色。16進数カラーコードで設定します。

<!-- parameter end -->

_セパレータの例_

<!-- tab start `json` -->

```json
{
  "type": "separator",
  "color": "#000000"
}
```

<!-- tab end -->

##### フィラー 

<!-- warning start -->

**フィラーは非推奨のコンポーネントです**

スペースを作るには、フィラーの代わりに各コンポーネントのプロパティを使用してください。詳しくは、『Messaging APIドキュメント』の「[コンポーネントの位置](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-position)」を参照してください。

<!-- warning end -->

スペースを作るためのコンポーネントです。ボックス内のコンポーネントの間、前、または後にスペースを入れることができます。

<!-- parameter start (props: required) -->

type

String

`filler`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

flex

Number

親要素内での、このコンポーネントの幅または高さの比率。詳しくは、『Messaging APIドキュメント』の「[コンポーネントのサイズ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-size)」を参照してください。

<!-- parameter end -->

フィラーでは親要素の`spacing`プロパティが無視されます。

_フィラーの例_

<!-- tab start `json` -->

```json
{
  "type": "filler"
}
```

<!-- tab end -->

## アクションオブジェクト 

ユーザーがメッセージ内のボタンまたは画像をタップしたときに、ボットが実行できるアクションのタイプです。

- [ポストバックアクション](https://developers.line.biz/ja/reference/messaging-api/#postback-action)
- [メッセージアクション](https://developers.line.biz/ja/reference/messaging-api/#message-action)
- [URIアクション](https://developers.line.biz/ja/reference/messaging-api/#uri-action)
- [日時選択アクション](https://developers.line.biz/ja/reference/messaging-api/#datetime-picker-action)
- [カメラアクション](https://developers.line.biz/ja/reference/messaging-api/#camera-action)
- [カメラロールアクション](https://developers.line.biz/ja/reference/messaging-api/#camera-roll-action)
- [位置情報アクション](https://developers.line.biz/ja/reference/messaging-api/#location-action)
- [リッチメニュー切替アクション](https://developers.line.biz/ja/reference/messaging-api/#richmenu-switch-action)
- [クリップボードアクション](https://developers.line.biz/ja/reference/messaging-api/#clipboard-action)

### ポストバックアクション 

このアクションが関連づけられたコントロールがタップされると、`data`プロパティに指定された文字列を含む[ポストバックイベント](https://developers.line.biz/ja/reference/messaging-api/#postback-event)が、Webhookを介して返されます。

<!-- parameter start (props: required) -->

type

String

`postback`

<!-- parameter end -->
<!-- parameter start (props: annotation="説明を参照") -->

label

String

アクションのラベル。アクションを設定するオブジェクトごとに、仕様が異なります。詳しくは、「[ラベルの仕様](https://developers.line.biz/ja/reference/messaging-api/#action-object-label-spec)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

data

String

Webhookを介して、[ポストバックイベント](https://developers.line.biz/ja/reference/messaging-api/#postback-event)の`postback.data`プロパティで返される文字列\
最大文字数：300

<!-- parameter end -->
<!-- parameter start (props: optional) -->

displayText

String

アクションの実行時に、ユーザーのメッセージとしてLINEのトーク画面に表示されるテキスト。\
最大文字数：300\
`displayText`プロパティと`text`プロパティは、同時に設定できません。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

text

String

【廃止予定】アクションの実行時に、ユーザーのメッセージとしてLINEのトーク画面に表示されるテキスト。Webhookを介してサーバーに返されます。クイックリプライボタンでは使用しないでください。\
最大文字数：300\
`displayText`プロパティと`text`プロパティは、同時に設定できません。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

inputOption

String

アクションに応じた、リッチメニューなどの表示方法。以下のいずれかの値を指定します。

- `closeRichMenu`：リッチメニューを閉じる
- `openRichMenu`：リッチメニューを開く
- `openKeyboard`：キーボードを開く
- `openVoice`：ボイスメッセージ入力モードを開く

iOS版LINEまたはAndroid版LINEのバージョン`12.6.0`以降で動作します。

<!-- parameter end -->
<!-- parameter start (props: annotation="説明を参照") -->

fillInText

String

キーボードを開いたときに、入力欄にあらかじめ入力しておく文字列。`inputOption`が`openKeyboard`の場合にのみ有効です。文字列は、改行文字（`\n`）により改行できます。\
最大文字数：300

iOS版LINEまたはAndroid版LINEのバージョン`12.6.0`以降で動作します。

<!-- parameter end -->

#### ラベルの仕様 

以下のアクションにおける`label`プロパティは、アクションを設定するオブジェクトごとに、仕様が異なります。

- [ポストバックアクション](https://developers.line.biz/ja/reference/messaging-api/#postback-action)
- [メッセージアクション](https://developers.line.biz/ja/reference/messaging-api/#message-action)
- [URIアクション](https://developers.line.biz/ja/reference/messaging-api/#uri-action)
- [日時選択アクション](https://developers.line.biz/ja/reference/messaging-api/#datetime-picker-action)
- [クリップボードアクション](https://developers.line.biz/ja/reference/messaging-api/#clipboard-action)

上記のアクションにおけるラベルの仕様は次のとおりです。なお、上記以外のアクションにおけるラベルの仕様については、各アクションの仕様を参照してください。

<table>
  <thead>
    <tr>
      <th colspan="2">オブジェクト</th>
      <th>必須</th>
      <th>最大文字数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2"><a href="#template-messages">テンプレートメッセージ</a></td>
      <td>画像カルーセル</td>
      <td>任意</td>
      <td>12</td>
    </tr>
    <tr>
      <td>画像カルーセル以外</td>
      <td>必須</td>
      <td>20</td>
    </tr>
    <tr>
      <td colspan="2"><a href="#rich-menu-object">リッチメニュー</a> *1</td>
      <td>任意</td>
      <td>20</td>
    </tr>
    <tr>
      <td colspan="2"><a href="#quick-reply-button-object">クイックリプライボタン</a></td>
      <td>必須</td>
      <td>20</td>
    </tr>
    <tr>
      <td rowspan="2"><a href="#flex-message">Flex Message</a></td>
      <td>ボタン</td>
      <td>必須</td>
      <td>40</td>
    </tr>
    <tr>
      <td>ボタン以外 *2</td>
      <td>任意</td>
      <td>40</td>
    </tr>
  </tbody>
</table>

※1 ユーザーデバイスのアクセシビリティ機能が有効な場合に読み上げられます。

※2 ラベルを指定しても表示されません。

_ポストバックアクションオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "type": "postback",
  "label": "Buy",
  "data": "action=buy&itemid=111",
  "displayText": "Buy",
  "inputOption": "openKeyboard",
  "fillInText": "---\nName: \nPhone: \nBirthday: \n---"
}
```

<!-- tab end -->

### メッセージアクション 

このアクションが関連づけられたコントロールがタップされると、`text`プロパティの文字列がユーザーからのメッセージとして送信されます。

<!-- parameter start (props: required) -->

type

String

`message`

<!-- parameter end -->
<!-- parameter start (props: annotation="説明を参照") -->

label

String

アクションのラベル。アクションを設定するオブジェクトごとに、仕様が異なります。詳しくは、「[ラベルの仕様](https://developers.line.biz/ja/reference/messaging-api/#action-object-label-spec)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

text

String

アクションの実行時に送信されるテキスト\
最大文字数：300

<!-- parameter end -->

_メッセージアクションオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "type": "message",
  "label": "Yes",
  "text": "Yes"
}
```

<!-- tab end -->

### URIアクション 

このアクションが関連づけられたコントロールがタップされると、LINE内ブラウザで`uri`プロパティのURIが開きます。

<!-- parameter start (props: required) -->

type

String

`uri`

<!-- parameter end -->
<!-- parameter start (props: annotation="説明を参照") -->

label

String

アクションのラベル。アクションを設定するオブジェクトごとに、仕様が異なります。詳しくは、「[ラベルの仕様](https://developers.line.biz/ja/reference/messaging-api/#action-object-label-spec)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

uri

String

アクションの実行時に開かれるURI（最大文字数：1000）\
使用できるスキームは、`http`、`https`、`line`、および`tel`です。LINE URLスキームについて詳しくは、「[LINE URLスキームでLINEの機能を使う](https://developers.line.biz/ja/docs/messaging-api/using-line-url-scheme/)」を参照してください。

URIはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

altUri.desktop

String

macOS版とWindows版のLINEでアクションを実行したときに開かれるURI（最大文字数：1000）\
`altUri.desktop`を指定した場合は、macOS版とWindows版のLINEでは`uri`が無視されます。\
使用できるスキームは、`http`、`https`、`line`、および`tel`です。LINE URLスキームについて詳しくは、「[LINE URLスキームでLINEの機能を使う](https://developers.line.biz/ja/docs/messaging-api/using-line-url-scheme/)」を参照してください。

URIはUTF-8を用いてパーセントエンコードしてください。詳しくは、「[リクエストボディのプロパティに指定するURLのエンコードについて](https://developers.line.biz/ja/reference/messaging-api/#url-encoding)」を参照してください。

<!-- note start -->

**注意**

`altUri.desktop`は、Flex MessageにURIアクションを関連付けた場合にのみ有効です。クイックリプライでは動作しません。

<!-- note end -->

<!-- parameter end -->

_URIアクションオブジェクトの例_

<!-- tab start `json` -->

```json
// LINE内ブラウザで指定のURLを開く例
{
    "type": "uri",
    "label": "メニューを見る",
    "uri": "https://example.com/menu"
}

// スマートフォン版LINEとデスクトップ版LINEで異なるURLを開く例
{
   "type":"uri",
   "label":"詳しくはこちら",
   "uri":"http://example.com/page/222",
   "altUri": {
      "desktop" : "http://example.com/pc/page/222"
   }
}

// 電話番号を指定して通話アプリを開く例
{
    "type": "uri",
    "label": "電話注文",
    "uri": "tel:09001234567"
}

// LINE URLスキームでLINE公式アカウントをシェアする例
{
    "type": "uri",
    "label": "友だちに勧める",
    "uri": "https://line.me/R/nv/recommendOA/%40linedevelopers"
}
```

<!-- tab end -->

### 日時選択アクション 

このアクションが関連づけられたコントロールがタップされると、日時選択ダイアログでユーザーが選択した日時を含む[ポストバックイベント](https://developers.line.biz/ja/reference/messaging-api/#postback-event)が、Webhookを介して返されます。日時選択アクションはタイムゾーンの違いに対応していません。

<!-- parameter start (props: required) -->

type

String

`datetimepicker`

<!-- parameter end -->
<!-- parameter start (props: annotation="説明を参照") -->

label

String

アクションのラベル。アクションを設定するオブジェクトごとに、仕様が異なります。詳しくは、「[ラベルの仕様](https://developers.line.biz/ja/reference/messaging-api/#action-object-label-spec)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

data

String

Webhookを介して、[ポストバックイベント](https://developers.line.biz/ja/reference/messaging-api/#postback-event)の`postback.data`プロパティで返される文字列\
最大文字数：300

<!-- parameter end -->
<!-- parameter start (props: required) -->

mode

String

アクションモード\
`date`：日付を選択します。\
`time`：時刻を選択します。\
`datetime`：日付と日時を選択します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

initial

String

日付または時刻の初期値

<!-- parameter end -->
<!-- parameter start (props: optional) -->

max

String

選択可能な日付または時刻の最大値。`min`の値より大きい必要があります。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

min

String

選択可能な日付または時刻の最小値。`max`の値より小さい必要があります。

<!-- parameter end -->

_日時選択アクションオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "type": "datetimepicker",
  "label": "Select date",
  "data": "storeId=12345",
  "mode": "datetime",
  "initial": "2017-12-25t00:00",
  "max": "2018-01-24t23:59",
  "min": "2017-12-25t00:00"
}
```

<!-- tab end -->

#### 日付と日時の形式 

`initial`、`max`、および`min`の値の日付と日時の形式は以下のとおりです。`full-date`、`time-hour`、および`time-minute`の形式は、[RFC3339](https://www.ietf.org/rfc/rfc3339.txt)プロトコルで定義されています。

| モード | 形式 | 例 |
| --- | --- | --- |
| date | `full-date`<br />最大値：2100-12-31<br />最小値：1900-01-01 | 2017-06-18 |
| time | `time-hour`:`time-minute`<br />最大値：23:59<br />最小値：00:00 | 00:00<br />06:15<br />23:59 |
| datetime | `full-date`T`time-hour`:`time-minute`または`full-date`t`time-hour`:`time-minute`<br />最大値：2100-12-31T23:59<br />最小値：1900-01-01T00:00 | 2017-06-18T06:15<br />2017-06-18t06:15 |

### カメラアクション 

クイックリプライボタンにのみ設定できるアクションです。このアクションが関連づけられたボタンがタップされると、LINE内のカメラが起動します。

<!-- parameter start (props: required) -->

type

String

`camera`

<!-- parameter end -->
<!-- parameter start (props: required) -->

label

String

アクションのラベル\
最大文字数：20

<!-- parameter end -->

_カメラアクションオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "type": "camera",
  "label": "Camera"
}
```

<!-- tab end -->

### カメラロールアクション 

クイックリプライボタンにのみ設定できるアクションです。このアクションが関連づけられたボタンがタップされると、LINEのカメラロール画面が開きます。

<!-- parameter start (props: required) -->

type

String

`cameraRoll`

<!-- parameter end -->
<!-- parameter start (props: required) -->

label

String

アクションのラベル\
最大文字数：20

<!-- parameter end -->

_カメラロールアクションオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "type": "cameraRoll",
  "label": "Camera roll"
}
```

<!-- tab end -->

### 位置情報アクション 

クイックリプライボタンにのみ設定できるアクションです。このアクションが関連づけられたボタンがタップされると、LINEの位置情報画面が開きます。

<!-- parameter start (props: required) -->

type

String

`location`

<!-- parameter end -->
<!-- parameter start (props: required) -->

label

String

アクションのラベル\
最大文字数：20

<!-- parameter end -->

_位置情報アクションオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "type": "location",
  "label": "Location"
}
```

<!-- tab end -->

### リッチメニュー切替アクション 

リッチメニューにのみ設定できるアクションです。Flex Messageやクイックリプライでは利用できません。このアクションが関連づけられたリッチメニューがタップされると、リッチメニューの切替が行われ、ユーザーが選択したリッチメニューエイリアスIDを含む[ポストバックイベント](https://developers.line.biz/ja/reference/messaging-api/#postback-event)が、Webhookを介して返されます。詳しくは、『Messaging APIドキュメント』の「[リッチメニューでタブ切り替えを行う](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/)」を参照してください。

<!-- parameter start (props: required) -->

type

String

`richmenuswitch`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

label

String

アクションのラベル。リッチメニューでは省略可能です。ユーザーデバイスのアクセシビリティ機能が有効な場合に読み上げられます。

- 最大文字数：20

<!-- parameter end -->
<!-- parameter start (props: required) -->

richMenuAliasId

String

切替先のリッチメニューエイリアスID。

<!-- parameter end -->
<!-- parameter start (props: required) -->

data

String

Webhookを介して、[ポストバックイベント](https://developers.line.biz/ja/reference/messaging-api/#postback-event)の`postback.data`プロパティで返される文字列

- 最大文字数：300

<!-- parameter end -->

_リッチメニュー切替アクションオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "type": "richmenuswitch",
  "richMenuAliasId": "richmenu-alias-b",
  "data": "richmenu-changed-to-b"
}
```

<!-- tab end -->

### クリップボードアクション 

ユーザーがこのアクションが関連づけられたコントロールをタップすると、`clipboardText`プロパティに指定されたテキストが、端末のクリップボードにコピーされます。

iOS版LINEまたはAndroid版LINEのバージョン`14.0.0`以降で動作します。

<!-- parameter start (props: required) -->

type

String

`clipboard`

<!-- parameter end -->
<!-- parameter start (props: annotation="説明を参照") -->

label

String

アクションのラベル。アクションを設定するオブジェクトごとに、仕様が異なります。詳しくは、「[ラベルの仕様](https://developers.line.biz/ja/reference/messaging-api/#action-object-label-spec)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

clipboardText

String

クリップボードにコピーされる文字列

- 最大文字数：1000

<!-- parameter end -->

_クリップボードアクションオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "type": "clipboard",
  "label": "Copy",
  "clipboardText": "3B48740B"
}
```

<!-- tab end -->

## リッチメニューの構造 

リッチメニューは以下のどちらかのオブジェクトで表されます。

- リッチメニューIDを含まない[リッチメニューオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#rich-menu-object)。[リッチメニューの作成時](https://developers.line.biz/ja/reference/messaging-api/#create-rich-menu)にこのオブジェクトを使用します。
- リッチメニューIDを含む[リッチメニューレスポンスオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#rich-menu-response-object)。[リッチメニューの取得時](https://developers.line.biz/ja/reference/messaging-api/#get-rich-menu)または[リッチメニューの配列の取得時](https://developers.line.biz/ja/reference/messaging-api/#get-rich-menu-list)にこのオブジェクトが返されます。

これらのオブジェクトは[領域オブジェクト](https://developers.line.biz/ja/reference/messaging-api/#area-object)と[アクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#action-objects)から構成されます。

### リッチメニューオブジェクト 

<!-- tip start -->

**リッチメニューオブジェクトが有効か確認したい場合**

リッチメニューオブジェクトが有効かを確認したい場合、[リッチメニューオブジェクトを検証する](https://developers.line.biz/ja/reference/messaging-api/#validate-rich-menu-object)エンドポイントで検証できます。

<!-- tip end -->

<!-- parameter start (props: required) -->

size

Object

[`size`オブジェクト](https://developers.line.biz/ja/reference/messaging-api/#size-object)。トークルームに表示されるリッチメニューの幅と高さを表します。使用できるリッチメニューの画像の幅サイズは800px以上2500px以下で、高さサイズは250px以上です。ただし、アスペクト比（幅÷高さ）が1.45以上になるようにします。

<!-- parameter end -->
<!-- parameter start (props: required) -->

selected

Boolean

デフォルトでリッチメニューを表示する場合は`true`です。それ以外は`false`です。

<!-- parameter end -->
<!-- parameter start (props: required) -->

name

String

リッチメニューの名前。リッチメニューの管理に役立ちます。ユーザーには表示されません。\
最大文字数：300

<!-- parameter end -->
<!-- parameter start (props: required) -->

chatBarText

String

トークルームメニューに表示されるテキストです。\
最大文字数：14

<!-- parameter end -->
<!-- parameter start (props: required) -->

areas

Array

タップ領域の座標とサイズを定義する、[領域オブジェクト](https://developers.line.biz/ja/reference/messaging-api/#area-object)の配列。\
最大領域オブジェクト数：20

<!-- parameter end -->

_リッチメニューオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "size": {
    "width": 2500,
    "height": 1686
  },
  "selected": false,
  "name": "Nice rich menu",
  "chatBarText": "Tap to open",
  "areas": [
    {
      "bounds": {
        "x": 0,
        "y": 0,
        "width": 2500,
        "height": 1686
      },
      "action": {
        "type": "postback",
        "data": "action=buy&itemid=123"
      }
    }
  ]
}
```

<!-- tab end -->

### リッチメニューレスポンスオブジェクト 

<!-- parameter start -->

richMenuId

String

リッチメニューのID

<!-- parameter end -->
<!-- parameter start -->

size

Object

[`size`オブジェクト](https://developers.line.biz/ja/reference/messaging-api/#size-object)。トークルームに表示されるリッチメニューの幅と高さを表します。使用できるリッチメニューの画像の幅サイズは800px以上2500px以下で、高さサイズは250px以上です。ただし、アスペクト比（幅÷高さ）が1.45以上になるようにします。

<!-- parameter end -->
<!-- parameter start -->

selected

Boolean

デフォルトでリッチメニューを表示する場合は`true`です。それ以外は`false`です。

<!-- parameter end -->
<!-- parameter start -->

name

String

リッチメニューの名前。リッチメニューの管理に役立ちます。ユーザーには表示されません。\
最大文字数：300

<!-- parameter end -->
<!-- parameter start -->

chatBarText

String

トークルームメニューに表示されるテキストです。\
最大文字数：14

<!-- parameter end -->
<!-- parameter start -->

areas

Array

タップ領域の座標とサイズを定義する、[領域オブジェクト](https://developers.line.biz/ja/reference/messaging-api/#area-object)の配列。\
最大領域オブジェクト数：20

<!-- parameter end -->

_リッチメニューレスポンスオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "richMenuId": "{richMenuId}",
  "size": {
    "width": 2500,
    "height": 1686
  },
  "selected": false,
  "name": "Nice rich menu",
  "chatBarText": "Tap to open",
  "areas": [
    {
      "bounds": {
        "x": 0,
        "y": 0,
        "width": 2500,
        "height": 1686
      },
      "action": {
        "type": "postback",
        "label": "Buy",
        "data": "action=buy&itemid=123"
      }
    }
  ]
}
```

<!-- tab end -->

#### `size`オブジェクト 

<!-- parameter start (props: required) -->

width

Number

リッチメニューの幅。`800`以上、`2500`以下の値を指定します。ただし、アスペクト比（幅÷高さ）が1.45以上になるようにします。

<!-- parameter end -->
<!-- parameter start (props: required) -->

height

Number

リッチメニューの高さ。`250`以上の値を指定します。ただし、アスペクト比（幅÷高さ）が1.45以上になるようにします。

<!-- parameter end -->

_sizeオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "width": 2500,
  "height": 1686
}
```

<!-- tab end -->

#### 領域オブジェクト 

<!-- parameter start (props: required) -->

bounds

Object

領域の境界をピクセルで表すオブジェクト。「[`bounds`オブジェクト](https://developers.line.biz/ja/reference/messaging-api/#bounds-object)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

action

Object

領域がタップされたときに実行されるアクション。「[アクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#action-objects)」を参照してください。

<!-- parameter end -->

_領域オブジェクトの例_

<!-- tab start `json` -->

```json
{
  "bounds": {
    "x": 0,
    "y": 0,
    "width": 2500,
    "height": 1686
  },
  "action": {
    "type": "postback",
    "label": "Buy",
    "data": "action=buy&itemid=123"
  }
}
```

<!-- tab end -->

##### `bounds`オブジェクト 

<!-- parameter start (props: required) -->

x

Number

画像の左端を基準としたタップ領域の位置（横方向の相対位置）。`0`以上の値を設定してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

y

Number

画像の上端を基準としたタップ領域の位置（縦方向の相対位置）。`0`以上の値を設定してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

width

Number

タップ領域の幅

<!-- parameter end -->
<!-- parameter start (props: required) -->

height

Number

タップ領域の高さ

<!-- parameter end -->

_boundsオブジェクトの例_

<!-- tab start `json` -->

```json
{
  "x": 0,
  "y": 0,
  "width": 2500,
  "height": 1686
}
```

<!-- tab end -->
