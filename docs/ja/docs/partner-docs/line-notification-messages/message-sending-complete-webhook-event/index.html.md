# Webhookの配信完了イベント

<!-- note start -->

**オプション機能を利用するには手続きが必要です**

本ドキュメントに記載の機能は、所定の申請等を行った法人ユーザーのみがご利用いただけます。自社のLINE公式アカウントでご利用になりたいお客様は、担当営業までご連絡いただくか、[弊社パートナー](https://www.lycbiz.com/jp/partner/sales/)にお問い合わせください。

<!-- note end -->

## Webhookの配信完了イベントの概要 

LINE通知メッセージAPIをリクエストし、ユーザーに対してLINE通知メッセージの配信が完了した際に、専用のWebhookイベント（配信完了イベント）がLINEプラットフォームからボットサーバーのWebhook URLに送信されます。

- [Webhookの配信完了イベントの仕様](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#receive-delivery-event)
- [Webhookの配信完了イベントに関する補足事項](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#we-cant-receive-a-delivery-webhook-event)

### Webhookの配信完了イベントの仕様 

| プロパティ名 | タイプ | 説明 |
| --- | --- | --- |
| type | String | `delivery` |
| mode | Object | 「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。 |
| timestamp | Number | 「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。 |
| webhookEventId | String | 「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。 |
| deliveryContext | Object | 「[共通プロパティ](https://developers.line.biz/ja/reference/messaging-api/#common-properties)」を参照してください。 |
| delivery | Object | ハッシュ化した電話番号の文字列もしくは、[`X-Line-Delivery-Tag`](https://developers.line.biz/ja/reference/line-notification-messages/#send-line-notification-message-template-request-headers)で指定した文字列を含むデリバリーオブジェクト |
| delivery.data | String | ハッシュ化した電話番号の文字列もしくは、[`X-Line-Delivery-Tag`](https://developers.line.biz/ja/reference/line-notification-messages/#send-line-notification-message-template-request-headers)で指定した文字列 |

_Webhookイベントの例_

<!-- tab start `json` -->

```json
// Webhookの配信完了イベントの例(X-Line-Delivery-Tagヘッダ指定なし)
{
  "destination": "Uc7472b39e21dab71c2347e02714630d6",
  "events": [
    {
      "type": "delivery",
      "delivery": {
        "data": "68df277462529930889fab80ecffdc0883906320591df93c25efc08300410fc2"
      },
      "webhookEventId": "01G17DAF0QJ7A3ERC5EJ9MAMH8",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1650590038721,
      "mode": "active"
    }
  ]
}

// Webhookの配信完了イベントの例(X-Line-Delivery-Tagヘッダ指定あり)
{
  "destination": "Uc7472b39e21dab71c2347e02714630d6",
  "events": [
    {
      "type": "delivery",
      "delivery": {
        "data": "15034552939884E28681A7D668CEA94C147C716C0EC9DFE8B80B44EF3B57F6BD0602366BC3menu01"
      },
      "webhookEventId": "01G17EJCGAVV66J5WNA7ZCTF6H",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1650591346705,
      "mode": "active"
    }
  ]
}
```

<!-- tab end -->

<!-- note start -->

**Webhookの配信完了イベントの示す状態について**

Webhookの配信完了イベントは、**LINE通知メッセージがユーザーに配信され、メッセージを確認できる状態になったことを示す**ものです。以下を示すものではありません。

- LINE通知メッセージAPIのリクエスト成功
- [LINE通知メッセージの受信への同意を求めるメッセージの受信](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-1)
- LINE通知メッセージの受信への同意
- [SMS認証を求めるメッセージの受信](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-3)
- SMS認証の実施
- ユーザーによるLINE通知メッセージの開封（既読）

<!-- note end -->

<!-- note start -->

**Webhookイベントの署名検証**

配信完了イベント受信時の[署名の検証](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#verify-signature)についてはチャネルシークレットを用いて行ってください。なお、LINEチャットPlusを利用しているチャネルにおいては、Switcher Secretを用いて署名の検証を行ってください。

<!-- note end -->

## Webhookの配信完了イベントに関する補足事項 

LINE通知メッセージAPIをリクエストし、HTTPステータスコード`200`または`202`でレスポンスが行われた場合でも、ユーザーの[LINE通知メッセージの受信設定](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#how-to-consent-for-line-notification-messages)やSMS認証の状況によっては、LINE通知メッセージがユーザーに配信されなかったり、LINE通知メッセージの送信が保留されたりする場合があります。

LINE通知メッセージAPIをリクエストし、HTTPステータスコード`200`または`202`でレスポンスが行われてから24時間以内に[Webhookの配信完了イベント](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/)を受信しなかった場合は、以下のいずれかの理由により、LINE通知メッセージがユーザーに配信されなかったことを意味します。

- [ユーザーがLINE公式アカウントをブロックしている](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#user-blocked-your-account)
- [ユーザーが必要な同意や認証を行わなかった](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#user-didnt-action-taken)

### ユーザーがLINE公式アカウントをブロックしている 

ユーザーがLINE通知メッセージ送信元のLINE公式アカウントをブロックしている場合でも、[LINE通知メッセージAPIのリクエスト](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#about-pnp-api-block-response)は、HTTPステータスコード`200`または`202`でレスポンスされます。

### ユーザーが必要な同意や認証を行わなかった 

LINE通知メッセージの受信設定が未設定であったり、SMS認証が必要な状況であるが、それらの設定や操作を行わなかった可能性があります。詳しくは[LINE通知メッセージAPIのリクエストが成功したがメッセージが配信されない場合について](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#why-i-cant-receive-line-notification-messages)を参照してください。
