# メッセージに既読をつける

LINEのトークにおいて、ユーザーが送ったメッセージを相手が閲覧した場合、メッセージに既読がつきます。LINE公式アカウントでチャット機能を利用する場合、ユーザーからのメッセージには自動で既読がつきませんが、Messaging APIを利用することで、チャット機能を利用しつつ任意のメッセージに既読をつけることができます。

このページでは、ユーザーから送られたメッセージにMessaging APIを通して既読をつける方法について説明します。

<!-- table of contents -->

## Messaging APIでメッセージに既読をつけるための条件 

[LINE Official Account Manager](https://manager.line.biz/)の［**応答設定**］において、［**チャット**］がオフになっている場合、ユーザーから送られたメッセージには自動で既読がつきます。Messaging APIを通して既読をつけたい場合は、［**チャット**］がオンである必要があります。

## Messaging APIでメッセージに既読をつける方法 

ユーザーから送られたメッセージに既読をつけるには、以下の手順に従ってください。

1. [メッセージの既読トークンを取得する](https://developers.line.biz/ja/docs/messaging-api/mark-as-read/#get-token)
2. [「メッセージに既読をつける」エンドポイントを使用する](https://developers.line.biz/ja/docs/messaging-api/mark-as-read/#use-endpoint)

それぞれの手順について説明します。

### 1. メッセージの既読トークンを取得する 

ユーザーがLINE公式アカウントに対してメッセージを送ると、LINEプラットフォームからボットサーバーに対してWebhookの[メッセージイベント](https://developers.line.biz/ja/reference/messaging-api/#message-event)が送信されます。このイベントオブジェクトに、メッセージに既読をつけるための`markAsReadToken`プロパティ（既読トークン）が含まれています。

Webhookのメッセージイベントオブジェクトの例を以下に示します。なお、既読トークンに有効期限はありません。

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "type": "message",
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "message": {
        "id": "444573844083572737",
        "type": "text",
        "quoteToken": "q3Plxr4AgKd...",
        "markAsReadToken": "30yhdy232...", // 既読トークン
        "text": "Hello, world!"
      },
      // 省略
    }
  ]
}
```

### 2. 「メッセージに既読をつける」エンドポイントを使用する 

メッセージに既読をつけるには、手順1で取得した既読トークンを用いて、「[メッセージに既読をつける](https://developers.line.biz/ja/reference/messaging-api/#mark-as-read)」エンドポイントを使用します。以下のようなリクエストを実行することで、指定したメッセージと、それ以前に送られたすべてのメッセージに既読をつけることができます。

```sh
curl -v -X POST https://api.line.me/v2/bot/chat/markAsRead \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {channel access token}' \
-d '{
  "markAsReadToken": "{mark as read token}"
}'
```
