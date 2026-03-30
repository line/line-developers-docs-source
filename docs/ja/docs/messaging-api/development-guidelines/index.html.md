# Messaging API開発ガイドライン

ボット開発を始める前に、Messaging APIを使ったボット開発について、何が禁止され、何が推奨されているかを学びましょう。

**禁止事項**

- [LINEプラットフォームへの大量リクエストの禁止](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/#prohibiting-mass-requests-to-line-platform)
- [LINEプラットフォームを経由した負荷テストの禁止](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/#prohibiting-line-platform-load-tests)
- [同一ユーザーへの大量送信の禁止](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/#prohibiting-mass-transmissions-to-same-user)
- [存在しないユーザーIDへのリクエストの禁止](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/#prohibiting-requests-for-non-existent-user-ids)
- [ユーザーの属性を特定する行為の禁止](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/#prohibiting-identify-users-attribute)
- [IPアドレスによるアクセス制限の禁止](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/#prohibiting-ip-address-restrictions)

**推奨事項**

- [送信取消イベント受信時に推奨する処理](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/#webhook-unsend-message)
- [Webhook受信時の署名検証の推奨](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/#verify-webhook-signature)
- [非破壊的な変更を想定した実装の推奨](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/#assume-non-breaking-changes)
- [ログ保存の推奨](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/#save-logs)

<!-- note start -->

**注意**

ボット開発における基本ルールは[規約とポリシー](https://developers.line.biz/ja/terms-and-policies/)に基づきます。

<!-- note end -->

## 禁止事項 

### LINEプラットフォームへの大量リクエストの禁止 

負荷テストや動作テストを目的に、LINEプラットフォームへ、大量のリクエストを送信しないでください。いかなる場合でも、リクエスト数は指定された[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)以下に抑えてください。レート制限を超えて送信を行った場合、`429 Too Many Requests`エラーとなります。

<!-- note start -->

**レート制限内の動作テスト**

レート制限内であっても以下のようなリクエストを高頻度で行わないでください。

- 実際にナローキャスト配信に利用しないにもかかわらず[オーディエンスの作成](https://developers.line.biz/ja/docs/messaging-api/using-audience/#create-audience)と削除を高頻度で繰り返し行う行為
- Messaging APIの機能を利用しないリクエストを高頻度で繰り返し行う行為

<!-- note end -->

### LINEプラットフォームを経由した負荷テストの禁止 

LINEプラットフォームから、ボットサーバーの負荷テストを行うサービスはありません。ボットサーバーの負荷テストを目的に、LINEプラットフォームを経由して大量のメッセージを送信しないでください。ボットサーバーの負荷テストを行うための環境は、別途用意してください。

### 同一ユーザーへの大量送信の禁止 

いかなる場合でも、同一ユーザーへメッセージを大量送信しないでください。

### 存在しないユーザーIDへのリクエストの禁止 

存在しない[ユーザーID](https://developers.line.biz/ja/glossary/#user-id)へのリクエストを送信しないでください。

### ユーザーの属性を特定する行為の禁止 

特定のユーザーIDに対して、ユーザーの[属性](https://developers.line.biz/ja/reference/messaging-api/#narrowcast-demographic-filter)を特定する行為は行わないでください。また、ユーザーの属性を特定する目的で[オーディエンス管理](https://developers.line.biz/ja/reference/messaging-api/#manage-audience-group)のAPIを利用したり、[ナローキャストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message)を配信したりしないでください。

### IPアドレスによるアクセス制限の禁止 

Webhookを受信するボットサーバーにおいて、Webhookリクエスト送信元のLINEプラットフォームのIPアドレスでアクセス制限をしないでください。LINEプラットフォームのIPアドレスは開示していません。また、IPアドレスは予告なく変更される場合があります。不正なアクセス元からのリクエストを拒否したい場合は、IPアドレスによる制限ではなく、Webhookの[署名の検証](https://developers.line.biz/ja/reference/messaging-api/#signature-validation)を実施してください。

## 推奨事項 

### 送信取消イベント受信時に推奨する処理 

ユーザーがメッセージの送信を取り消すと、ボットサーバーに[送信取消イベント](https://developers.line.biz/ja/reference/messaging-api/#unsend-event)が届きます。

送信取消イベントを受け取った場合、サービス提供者はユーザーがメッセージの送信を取り消した意図を尊重し、以降は対象のメッセージを見たり利用したりできないよう、最大限の配慮を持って対象のメッセージを適切に扱うことを推奨します。

詳しくは、「[送信取消イベント受信時の処理](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#webhook-unsend-message)」を参照してください。

### Webhook受信時の署名検証の推奨 

ボットサーバーでWebhookを受信した際は、[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)を処理する前に、リクエストヘッダーに含まれる署名を検証することを推奨します。署名の検証は、開発者のボットサーバーに届いたリクエストが「LINEプラットフォームから送信されたWebhookか」および「通信経路で改ざんされていないか」などを確認するための重要な手順です。

詳しくは、「[Webhookの署名を検証する](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-signature/)」を参照してください。

### 非破壊的な変更を想定した実装の推奨 

Messaging APIでは、非破壊的な機能追加が行われることがあります。これらの変更は、既存の機能を壊すことなく、APIを拡張することを目的としています。このため以下のような変更は、事前の予告なく実施されることがあります。

- 新しいエンドポイントの追加
- APIリクエストにおける省略可能なパラメータやフィールド、ヘッダーの追加
- APIレスポンスにおけるフィールドやヘッダーの追加
- Webhookイベントオブジェクトへのプロパティの追加
- APIレスポンスおよびWebhookイベントオブジェクトのプロパティの順序の変更
- 列挙型の値の追加（例：[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#common-properties)の`type`プロパティの値の追加）
- データの要素間の空白や改行の有無

これらの非破壊的な機能追加に対しても不具合なく動作するよう、ボットサーバーを実装してください。

### ログ保存の推奨 

送信した[Messaging APIに対するリクエスト](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/#messaging-api-logs)や受信した[Webhook](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/#webhook-logs)のログを一定期間保存することを推奨します。これらのログは問題の原因を調査する際に役立ちます。

<!-- tip start -->

**ログに保存しておくと有用な情報**

このセクションで推奨している基本的なログ情報に加えて、以下の情報も役に立ちます。ボットの要件に応じて、以下の情報の保存を検討してください。

- 呼び出したMessaging APIのリクエストボディ
- APIリクエストに対してLINEプラットフォームから返却されたレスポンスボディ
- LINEプラットフォームからWebhookが送信された際の[リクエストヘッダー](https://developers.line.biz/ja/reference/messaging-api/#request-headers)の署名（`x-line-signature`）
- LINEプラットフォームから送信された[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)

<!-- tip end -->

<!-- note start -->

**ログの提供は行っておりません**

Messaging APIに対するリクエストのログや、LINEプラットフォームからボットサーバーへのWebhook送信時のログ等は、お問い合わせいただいても提供は行っておりません。ログの保存は、開発者自身の責任で行ってください。

<!-- note end -->

#### Messaging APIに対するリクエストのログ保存 

Messaging APIに対するリクエストを行った際は、以下の情報をログとして保存することを推奨します。

- [レスポンスヘッダー](https://developers.line.biz/ja/reference/messaging-api/#response-headers)のリクエストID（`x-line-request-id`）
- APIリクエストを行った時間
- リクエストのHTTPメソッド
- 呼ばれたAPIエンドポイント
- LINEプラットフォームから返された[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)

以下のような形式でログファイルに保存します。

| リクエストID（`x-line-request-id`） | APIリクエストを行った時間 | HTTPメソッド | APIエンドポイント | ステータスコード |
| --- | --- | --- | --- | --- |
| 8e36bade-c5d6-4d00-9e69-72244675a9a1 | Mon, 05 Jul 2021 08:14:35 GMT | POST | `https://api.line.me/v2/bot/message/push` | 200 |

#### 受信したWebhookのログ保存 

ボットサーバーでLINEプラットフォームからの[Webhook](https://developers.line.biz/ja/reference/messaging-api/#webhooks)を受信した際は、以下の情報をログとして保存することを推奨します。

- Webhook送信元のIPアドレス
- Webhookを受信した時間
- リクエストのHTTPメソッド
- リクエストのパス
- 受信したWebhookに対し、ボットサーバーが[レスポンス](https://developers.line.biz/ja/reference/messaging-api/#response)として返したステータスコード

以下のような形式でログファイルに保存します。

| 送信元IPアドレス | Webhookを受信した時間 | HTTPメソッド | リクエストのパス | ステータスコード |
| --- | --- | --- | --- | --- |
| 203.0.113.1 | Mon, 05 Jul 2021 08:10:00 GMT | POST | `/linebot/webhook` | 200 |
