# Messaging APIの利用を停止する

<!-- tip start -->

**LINE公式アカウントの利用を停止する**

Messaging APIチャネルと紐づいているLINE公式アカウントの利用を停止したい場合は、「[LINE公式アカウントの利用を停止する](https://developers.line.biz/ja/docs/messaging-api/stop-using-line-official-account/)」を参照してください。

<!-- tip end -->

Messaging APIチャネルに紐づいているLINE公式アカウントの利用は継続したいが、Messaging APIの利用は停止したい場合は、以下の作業を行うことを推奨します。なお、Messaging APIチャネルに紐づいているLINE公式アカウントを残し、Messaging APIチャネルのみを削除することはできません。

<!-- table of contents -->

## Webhookの利用を停止する 

1. [LINE Developersコンソール](https://developers.line.biz/console/)で、利用を停止するMessaging APIチャネルを選択します。
1. ［**Messaging API設定**］タブをクリックします。
1. ［**Webhook設定**］セクションの［**Webhookの利用**］を無効にします。

![［Webhook設定］セクションの［Webhookの利用］](https://developers.line.biz/media/messaging-api/stop-using-messaging-api/disable-use-webhook-ja.png)

## チャネルアクセストークンを取り消す 

チャネルアクセストークンの種類によって、取り消すためのエンドポイントが異なります。利用しているチャネルアクセストークンに対応するエンドポイントを使用し、チャネルアクセストークンを取り消してください。なお、[ステートレスチャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/#stateless-channel-access-token)は取り消せません。

- [チャネルアクセストークンv2.1を取り消す](https://developers.line.biz/ja/reference/messaging-api/#revoke-channel-access-token-v2-1)エンドポイント
- [短期または長期のチャネルアクセストークンを取り消す](https://developers.line.biz/ja/reference/messaging-api/#revoke-longlived-or-shortlived-channel-access-token)エンドポイント

## Messaging APIの利用停止後の表示 

上記の手順でWebhookを無効にし、チャネルアクセストークンを取り消すことで、Messaging APIの利用を停止できます。

ただし、この手順でMessaging APIの利用を停止しても、Messaging APIチャネルそのものは引き続き存在します。そのため、利用停止したチャネルをLINE Developersコンソールのチャネル一覧で確認した場合、他の利用中のMessaging APIチャネルとの見た目の違いはありません。

また、LINE Official Account Managerの設定画面で［**Messaging API**］を選択した際も、ステータスは「**利用中**」のままとなります。
