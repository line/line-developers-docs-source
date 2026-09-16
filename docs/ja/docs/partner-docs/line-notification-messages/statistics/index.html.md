# LINE通知メッセージの統計情報を取得する

<!-- note start -->

**オプション機能を利用するには手続きが必要です**

本ドキュメントに記載の機能は、所定の申請等を行った法人ユーザーのみがご利用いただけます。自社のLINE公式アカウントでご利用になりたいお客様は、担当営業までご連絡いただくか、[弊社パートナー](https://www.lycbiz.com/jp/partner/sales/)にお問い合わせください。

<!-- note end -->

## 概要 

LINE通知メッセージ（テンプレート）とLINE通知メッセージ（フレキシブル）では、ユニット名を指定してメッセージを送信することで、統計情報をユニットごとに取得できます。

取得できる統計情報、ユニット名の制限、統計情報を取得する方法などについて詳しくは、『Messaging APIドキュメント』の「[送信したメッセージの統計情報を取得する](https://developers.line.biz/ja/docs/messaging-api/unit-based-statistics-aggregation/)」を参照してください。

## ユニット名を指定する 

LINE通知メッセージを送信するときに、`customAggregationUnits`プロパティにユニット名を指定します。指定方法について詳しくは、『LINE通知メッセージAPIリファレンス』の以下の項目を参照してください。

- [LINE通知メッセージ（テンプレート）を送る](https://developers.line.biz/ja/reference/line-notification-messages/#send-line-notification-message-template)
- [LINE通知メッセージ（フレキシブル）を送る](https://developers.line.biz/ja/reference/line-notification-messages/#send-line-notification-message-flexible)

## LINE通知メッセージでユニット名を指定する際の注意点 

LINE通知メッセージでユニット名を指定する際は、次の2点に注意してください。

- [同じ用途のLINE通知メッセージに対して同じユニット名を継続的に使用する](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/statistics/#use-the-same-unit-name-for-the-same-purpose)
- [統計情報は実際にメッセージが送信されてから更新される](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/statistics/#statistics-are-aggregated-when-the-message-is-sent)

### 同じ用途のLINE通知メッセージに対して同じユニット名を継続的に使用する 

プライバシーを保護するため、集計された統計情報の値が20未満だった場合などは、個人の操作に関する統計情報の値は`null`になります。LINE通知メッセージは1人のユーザーに対して送信されるため、同じユニット名を付与してメッセージを送った対象のユーザー数が少ない場合、あるいは集計の対象期間が短い場合は統計情報が`null`になりやすくなります。

同じ用途のLINE通知メッセージに同じユニット名を継続して使用し、週次や月次など、より長い期間で統計情報を確認することを検討してください。統計情報が`null`になる条件について詳しくは、『Messaging APIドキュメント』の「[集計される統計情報についての注意点](https://developers.line.biz/ja/docs/messaging-api/unit-based-statistics-aggregation/#notes-about-message-statistics)」を参照してください。

### 統計情報は実際にメッセージが送信されてから更新される 

LINE通知メッセージでは、APIで送信リクエストを行った時点ではなく、実際にメッセージがユーザーへ送信されたタイミングで、統計情報やユニット名に関する以下の更新が行われます。

- 統計情報の更新が始まり、14日間（1,209,600秒間）継続する。
- 指定したユニット名が、当月中に付与したユニット名の種類数としてカウントされる。
- 指定したユニット名が、当月中に付与したユニット名の一覧に含まれる。

たとえば、ユーザーの[LINE通知メッセージの受信設定が未設定](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-1)の場合は、ユーザーが受信に同意した後にメッセージが送信されます。この場合、メッセージが実際に送信されるまでは、「[当月中に付与したユニット名の種類数を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-the-number-of-unit-name-types-assigned-during-this-month)」および「[当月中に付与したユニット名のリストを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-a-list-of-unit-names-assigned-during-this-month)」エンドポイントの結果に反映されません。
