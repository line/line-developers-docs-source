# Webhook URLを検証する

Messaging APIのWebhookを利用する場合、LINEプラットフォームからWebhook URL（ボットサーバー）へ疎通できることを、以下のいずれかの方法で検証してください。

- [検証方法1. Webhook URL検証用のエンドポイントで検証する](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-url/#verify-method-01)
- [検証方法2. LINE DevelopersコンソールからWebhook URLの［検証］ボタンで検証する](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-url/#verify-method-02)

<!-- tip start -->

**疎通確認のリクエストにはステータスコード200を返してください**

疎通確認の際は、Webhookイベントが含まれないHTTP POSTリクエストが送信されます。この場合も、ステータスコード`200`を返してください。

Webhookイベントが含まれないHTTP POSTリクエストの例：

```json
{
  "destination": "xxxxxxxxxx",
  "events": []
}
```

<!-- tip end -->

Webhook URLを検証した結果、ボットサーバーがWebhookを受信できていない場合は、[Webhookの受信に失敗する原因を調査](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-url/#investigate-webhook-reception-failure)してください。

## 検証方法1. Webhook URL検証用のエンドポイントで検証する 

Webhook URL検証用のエンドポイントで検証してください。

- [Webhookエンドポイントを検証する](https://developers.line.biz/ja/reference/messaging-api/#test-webhook-endpoint)

## 検証方法2. LINE DevelopersコンソールからWebhook URLの［検証］ボタンで検証する 

[LINE Developersコンソール](https://developers.line.biz/console/)からWebhook URLの［**検証**］ボタンで検証してください。

![send target](https://developers.line.biz/media/news/webhook-url.png)

## Webhookの受信に失敗する原因を調査する 

Webhook URLを検証した結果、ボットサーバーがWebhookを受信できていない場合は、以下の方法で原因を調査してください。

- Webhook URL検証用のエンドポイントから返ってきた[レスポンス](https://developers.line.biz/ja/reference/messaging-api/#test-webhook-endpoint-response)や[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#test-webhook-endpoint-error-response)を確認する
- [Webhookのエラーの原因と統計情報を確認する](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/)
- [Webhook送信元のSSL/TLS仕様](https://developers.line.biz/ja/docs/messaging-api/ssl-tls-spec-of-the-webhook-source/)を確認する
