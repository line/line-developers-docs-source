# エラー通知

<!-- note start -->

**オプション機能を利用するには手続きが必要です**

本ドキュメントに記載の機能は、所定の申請等を行った法人ユーザーのみがご利用いただけます。自社のLINE公式アカウントでご利用になりたいお客様は、担当営業までご連絡いただくか、[弊社パートナー](https://www.lycbiz.com/jp/partner/sales/)にお問い合わせください。

<!-- note end -->

## 概要 

ユーザーが、LINE公式アカウントを友だち追加したり、LINE公式アカウントにメッセージを送ったりすると、[LINE Developersコンソール](https://developers.line.biz/console/)の「Webhook URL」で指定したURL（ボットサーバー）に対して、LINEプラットフォームからWebhookイベントが送られます。

このWebhookイベント送信に対して、ボットサーバーが応答を返さない、あるいはステータスコード`200`番台以外の応答を返したとき、チャネルの管理者はエラーの発生を知らせる通知メールを受け取れます。このオプション機能を「エラー通知」と呼びます。

![ボットサーバーからエラーが返ってくると通知メールが送られます](https://developers.line.biz/media/partner-docs/normal-error-notification-ja.jpg)

## 送信されるメール 

エラー通知で送信されるメールについて説明します。

### メールの宛先 

エラー通知のメールは、以下のメールアドレス宛に送信されます。

- 対象チャネルの［**チャネル基本設定**］ページに登録されているメールアドレス
- 対象チャネルに対してAdmin権限を持つユーザーの登録メールアドレス

### メールの種類 

エラー通知のメールには、以下の種類があります。

- [LINEプラットフォームがエラーの発生を検知したとき](https://developers.line.biz/ja/docs/partner-docs/error-notification/#detected-error)
- [LINEプラットフォームがWebhookの再送を停止したとき](https://developers.line.biz/ja/docs/partner-docs/error-notification/#webhook-redelivery-stopped)（Webhookの再送が有効の場合のみ）

#### LINEプラットフォームがエラーの発生を検知したとき 

LINEプラットフォームがエラーの発生を検知したときは、以下のようなメールを送信します。なお、メールの内容やエラーメッセージの表記は、予告なく変更される可能性があります。

| | |
| --- | --- |
| 件名 | Messaging API: Your bot server returned no response or an error - `<Channel name>` |
| 本文 | LINE Platform sent a webhook, but your bot server did not respond or returned an error.<br/>Check the reason and details for the error and your bot server's configuration. Then make any necessary changes so that it can receive webhooks properly. |
| エラーの詳細 | エラーの原因や発生日時などが状況に応じて記載されます。詳細については、[メール本文](https://developers.line.biz/ja/docs/partner-docs/error-notification/#content)を参照してください。 |

<!-- tip start -->

**エラーはLINE Developersコンソールでも確認できます**

通知メールで受け取ったエラーの情報は、[LINE Developersコンソール](https://developers.line.biz/console/)でも確認できます。詳しくは、「[LINE Developersコンソールの［Webhookエラー］](https://developers.line.biz/ja/docs/partner-docs/error-notification/#line-developers-console)タブ」を参照してください。

<!-- tip end -->

#### LINEプラットフォームがWebhookの再送を停止したとき 

Messaging APIチャネルの設定で[Webhookの再送を有効](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#enable-webhook-redelivery)にしていた場合、LINEプラットフォームは、ボットサーバーが受け取りに失敗したWebhookを再送します。

そして、一定の期間ボットサーバーの応答がなかった場合に、Webhookの再送を停止し、以下のようなメールを送信します。なお、メールの件名および本文は、予告なく変更される可能性があります。

| | |
| --- | --- |
| 件名 | Messaging API: Webhook redelivery stopped - `<Channel name>` |
| 本文 | The LINE Platform tried to send the webhook for the event(s), but stopped redelivery due to no response from your bot server.<br>Please visit the LINE Developers site for details. |
| エラーの詳細 | エラーの原因や発生日時などが状況に応じて記載されます。詳細については、[メール本文](https://developers.line.biz/ja/docs/partner-docs/error-notification/#content)を参照してください。 |

Webhookの再送について詳しくは、[受け取りに失敗したWebhookを再送する](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#webhook-redelivery)を参照してください。

### 通知メールの例 

![通知メールの例](https://developers.line.biz/media/partner-docs/error-notification-email-sample.png)

### メール本文 

メールの内容は以下のとおりです。

| 項目 | 説明 |
| --- | --- |
| Channel ID | 対象のチャネルID |
| Channel name | 対象のチャネル名 |
| Reason for error  | エラー発生原因の概要。詳しくは、『Messaging APIドキュメント』の「[エラーが発生した原因を確認する](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#check-error-reason)」を参照してください。 |
| Detail for error | エラー発生原因の詳細。詳しくは、『Messaging APIドキュメント』の「[エラーの詳細を確認する](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#check-detail-for-error)」を参照してください。 |
| Error count | エラーの発生回数 |
| Time detected | エラーの発生日時 |

## 通知メール受信時の対応例 

たとえば、受信したエラー通知の内容が[通知メールの例](https://developers.line.biz/ja/docs/partner-docs/error-notification/#sample-mail)だった場合、Reason for errorが`error_status_code`、Detail for errorが`500`であるため、[エラーが発生した原因を確認する](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#check-error-reason)ことで「ボットサーバーがWebhookリクエストに対して、HTTPステータスコード`500`をレスポンスした」ということが分かります。

この場合、ボットサーバーは受信したWebhookイベントを正常に処理することができなかったと考えられます。ボットサーバーのWebhookイベントの処理に関するログなどを調査し、問題の発生原因を調査してください。

<!-- note start -->

**エラーの調査について**

LINEヤフー株式会社では、エラーに関する個別の調査や確認は行っていません。エラーの原因については、チャネルやボットサーバーを管理する開発者自身で対応を行う必要があります。

<!-- note end -->

## LINE Developersコンソールの［Webhookエラー］タブ 

通知メールで受け取ったエラーの情報は、[LINE Developersコンソール](https://developers.line.biz/console/)のMessaging APIチャネルの［**Webhookエラー**］タブでも確認できます。

［**Webhookエラー**］タブは、［**Messaging API設定**］タブで［**エラーの統計情報**］を有効にしたチャネルでのみ表示されます。エラーの統計情報を有効にする方法について詳しくは、『Messaging APIドキュメント』の「[エラーの統計情報を有効にする](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#enable-error-statistics)」を参照してください。

![エラーの統計情報](https://developers.line.biz/media/messaging-api/receiving-messages/error-statistics-ja.png)
