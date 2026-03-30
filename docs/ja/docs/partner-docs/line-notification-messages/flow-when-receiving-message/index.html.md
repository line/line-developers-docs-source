# LINE通知メッセージ受信時のフロー

<!-- note start -->

**オプション機能を利用するには手続きが必要です**

本ドキュメントに記載の機能は、所定の申請等を行った法人ユーザーのみがご利用いただけます。自社のLINE公式アカウントでご利用になりたいお客様は、担当営業までご連絡いただくか、[弊社パートナー](https://www.lycbiz.com/jp/partner/sales/)にお問い合わせください。

<!-- note end -->

## LINE通知メッセージ受信時のユーザーのフロー 

LINE通知メッセージをユーザーが受信するには、LINE通知メッセージの受信への同意に加え、180日に一回SMSによる電話番号認証（SMS認証）が必要です。

![LINE通知メッセージ受信時のユーザーのフロー](https://developers.line.biz/media/line-notification-message/pnp-receive-flow-ja.png)

- [LINE通知メッセージの受信に同意済みかつSMS認証が不要な場合](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#receiving-line-notification-messages)
- [LINE通知メッセージの受信に未同意かつSMS認証が不要な場合](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-1)
- [LINE通知メッセージの受信に未同意かつSMS認証が必要な場合](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-2)
- [LINE通知メッセージの受信に同意済みかつSMS認証が必要な場合](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-3)
- [（参考）LINEアカウントに登録されている電話番号を変更する際のフロー](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#when-changing-your-phone-number)

<!-- note start -->

**LINE通知メッセージの受信設定は包括的に行われます**

ユーザーが一度LINE通知メッセージの受信同意を行うと、すべてのLINE公式アカウントからのLINE通知メッセージの受信に同意したとみなされます。

たとえば、LINE公式アカウントAから送信されたLINE通知メッセージに応じてLINE通知メッセージの受信同意を行ったユーザーは、別のLINE公式アカウントBから送信されたLINE通知メッセージを受信した場合は、LINE通知メッセージの受信に同意した状態となるため、再度の同意は必要ありません。

<!-- note end -->

<!-- note start -->

**SMS認証はユーザーのLINEアカウントごとに180日に一回行う必要があります**

ユーザーが一度SMS認証を行うと、180日間はすべてのLINE公式アカウントから送信されたLINE通知メッセージを受信した際に、SMS認証は行われません。

たとえば、LINE公式アカウントAから送信されたLINE通知メッセージに応じてSMS認証を行ったユーザーは180日以内に別のLINE公式アカウントBから送信されたLINE通知メッセージを受信した場合は、SMS認証済みの状態となるため、再度のSMS認証は発生しません。

<!-- note end -->

<!-- note start -->

**SMS認証が不要なケース**

以下のような場合においても、LINE通知メッセージを受信した際に、SMS認証は発生しません。

- LINEアカウントを新規に作成してから180日以内である
- LINEアカウントに登録されている電話番号を変更してから180日以内である

<!-- note end -->

### LINE通知メッセージの受信に同意済みかつSMS認証が不要な場合 

| 番号 | 画像 | 説明 |
| --- | --- | --- |
| 1 | ![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-3-ja.png)<br><br>![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-4-ja.png) | LINE通知メッセージの受信に同意済みであり、SMS認証が不要な場合、「LINE」システムアカウントから、「LINE通知メッセージが届きました」メッセージが送信されます。同じタイミングで、リクエストしたLINE通知メッセージがユーザーに送信されます。 |

### LINE通知メッセージの受信に未同意かつSMS認証が不要な場合 

| 番号 | 画像 | 説明 |
| --- | --- | --- |
| 1 | ![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-1-ja.png) | LINE通知メッセージの受信に未同意の場合かつSMS認証が不要の場合に、LINE通知メッセージを受信した際には「LINE」システムアカウントから、「LINE通知メッセージが届きました」および「LINE通知メッセージの受信設定」メッセージが送信されます。 |
| 2 | ![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-2-ja.png) | 「LINE通知メッセージの受信設定」の「設定する」ボタンを押下すると、LINE通知メッセージの受信の同意画面に遷移します。 |
| 3 | ![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-3-ja.png)<br><br>![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-4-ja.png) | 「LINE通知メッセージの受信設定」に同意すると、「LINE」システムアカウントから、「LINE通知メッセージが届きました」メッセージが送信されます。その後、リクエストしたLINE通知メッセージがユーザーに送信されます。 |

### LINE通知メッセージの受信に未同意かつSMS認証が必要な場合 

| 番号 | 画像 | 説明 |
| --- | --- | --- |
| 1 | ![](https://developers.line.biz/media/line-notification-message/type3-pnpflow-1-ja.png) | LINE通知メッセージの受信に未同意であり、SMS認証が必要な場合に、LINE通知メッセージを受信した際には「LINE」システムアカウントから、「LINE通知メッセージが届きました」および「LINE通知メッセージの受信設定」メッセージが送信されます。 |
| 2 | ![](https://developers.line.biz/media/line-notification-message/type3-pnpflow-2-ja.png) | 「LINE通知メッセージの受信設定」の「設定する」ボタンを押下すると、LINE通知メッセージの受信の同意画面に遷移します。 |
| 3 | ![](https://developers.line.biz/media/line-notification-message/type3-pnpflow-3-ja.png) | 「LINE通知メッセージの受信設定」に同意すると、LINEアカウントに登録されている電話番号に対し、SMSメッセージ送信の確認ダイアログが表示されます。この際にSMS送信先の電話番号（LINEアカウントに登録してある電話番号）を変更することもできます。 |
| 4 | ![](https://developers.line.biz/media/line-notification-message/type3-pnpflow-4-ja.png) | 指定した電話番号に対してSMSによるメッセージが送信されます。メッセージに記載されている暗証番号を入力します。 |
| 5 | ![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-3-ja.png)<br><br>![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-4-ja.png) | SMSによる認証が完了すると、「LINE」システムアカウントから、「LINE通知メッセージが届きました」メッセージが送信されます。同じタイミングで、リクエストしたLINE通知メッセージがユーザーに送信されます。 |

### LINE通知メッセージの受信に同意済みかつSMS認証が必要な場合 

| 番号 | 画像 | 説明 |
| --- | --- | --- |
| 1 | ![](https://developers.line.biz/media/line-notification-message/type2-pnpflow-1-ja.png) | LINE通知メッセージの受信に同意済みであり、SMS認証が必要の場合に、LINE通知メッセージを受信した際には「LINE」システムアカウントから、「LINE通知メッセージが届きました」メッセージおよび「電話番号の認証」メッセージが送信されます。 |
| 2 | ![](https://developers.line.biz/media/line-notification-message/type2-pnpflow-2-ja.png) | 「電話番号の認証」メッセージの「設定する」ボタンを押下すると、電話番号の認証画面に遷移します。 |
| 3 | ![](https://developers.line.biz/media/line-notification-message/type2-pnpflow-3-ja.png) | 「SMSを送信する」ボタンを押下すると、LINEアカウントに登録されている電話番号に対し、SMSメッセージ送信の確認ダイアログが表示されます。この際にSMS送信先の電話番号（LINEアカウントに登録してある電話番号）を変更することもできます。 |
| 4 | ![](https://developers.line.biz/media/line-notification-message/type2-pnpflow-4-ja.png) | 指定した電話番号に対してSMSによるメッセージが送信されます。メッセージに記載されている暗証番号を入力します。 |
| 5 | ![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-3-ja.png)<br><br>![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-4-ja.png) | SMSによる認証が完了すると、「LINE」システムアカウントから、「LINE通知メッセージが届きました」メッセージが送信されます。同じタイミングで、リクエストしたLINE通知メッセージがユーザーに送信されます。 |

## （参考）LINEアカウントに登録されている電話番号を変更する際のフロー 

ユーザーがLINEアカウントに登録済みの電話番号を変更するには、LINE通知メッセージ受信時のSMS認証の際に［**変更**］ボタンをタップし、［**次へ**］ボタンをタップして電話番号を入力します。

<!-- tip start -->

**LINEアカウントに登録している電話番号の変更**

電話番号の変更は、LINEアプリの［**設定**］>［**プロフィール**］>［**電話番号**］からも行うことができます。詳しくは、LINEヘルプセンターの「[電話番号を確認／変更する](https://help.line.me/line/smartphone/pc?lang=ja&contentId=20000120)」を参照してください。

<!-- tip end -->

| 番号 | 画像 | 説明 |
| --- | --- | --- |
| 1 | ![](https://developers.line.biz/media/line-notification-message/change-phone-number-1-ja.png) | 変更したい電話番号を入力し「次へ」ボタンを押下します。 |
| 2 | ![](https://developers.line.biz/media/line-notification-message/change-phone-number-2-ja.png) | 「指定した電話番号に対してSMSによるメッセージが送信されます。メッセージに記載されている暗証番号を入力します。 |
| 3 | ![](https://developers.line.biz/media/line-notification-message/change-phone-number-3-ja.png) | SMSによる電話番号の認証に成功すると、「LINE」アカウントから「電話番号が変更されました。」メッセージが送信されます。 |

<style scoped>
.table-user-content-flow td:nth-child(2) {
    min-width: 160px;
}
.table-user-content-flow td:nth-child(3) {
    min-width: 200px;
}
</style>
