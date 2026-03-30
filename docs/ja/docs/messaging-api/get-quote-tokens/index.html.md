# 引用トークンを取得する

Messaging APIで、過去のメッセージを引用したメッセージを送りたいときは、引用トークンを使用します。このページでは、引用トークンの取得方法について解説します。

<!-- table of contents -->

## 引用トークンとは 

引用トークンとは、`IStG5h1Tz7bsH6xinEQtKQ9IdtcN5wLE15-LwtIDCEYAqDkV741O-XkOhZo1GYxw2UCURKnpHujpZuZaBaeQZVOVpKiaEeAz1Ye3-3ZYbPQVjuXZ4x8ZpISG7WhJDCE8o-hhHh8uMBRyp3b0L_Cxlg`のような文字列です。引用トークンは、[引用メッセージを送信する](https://developers.line.biz/ja/docs/messaging-api/sending-messages/#send-quote-messages)際に必要となります。

引用トークンは、引用対象となるメッセージが送られた1対1のトーク、グループトーク、複数人トークにおいてのみ使用できます。引用トークンには有効期限はなく、同じ引用トークンを複数回使用できます。

## 引用トークンを取得する 

引用トークンを取得する方法は2つあります。

1. [引用トークンをWebhookで取得する](https://developers.line.biz/ja/docs/messaging-api/get-quote-tokens/#get-quote-tokens-via-webhook)
1. [引用トークンをメッセージ送信時のレスポンスで取得する](https://developers.line.biz/ja/docs/messaging-api/get-quote-tokens/#get-quote-tokens-in-the-response)

### 引用トークンをWebhookで取得する 

1対1のトークや、LINE公式アカウントが追加されているグループトークや複数人トークでユーザーがメッセージを送ると、Webhookの[メッセージイベント](https://developers.line.biz/ja/reference/messaging-api/#message-event)がボットサーバーに送られます。このメッセージイベントの中で、以下のメッセージオブジェクトに引用トークン（`quoteToken`）が含まれています。

- [テキスト](https://developers.line.biz/ja/reference/messaging-api/#wh-text)
- [スタンプ](https://developers.line.biz/ja/reference/messaging-api/#wh-sticker)
- [画像](https://developers.line.biz/ja/reference/messaging-api/#wh-image)
- [動画](https://developers.line.biz/ja/reference/messaging-api/#wh-video)

```json
"message": {
  "type": "text",
  "id": "468789577898262530",
  "quoteToken": "q3Plxr4AgKd...", // 引用トークン
  "text": "Can I reserve a table for dinner tonight?"
}
```

Webhookについて詳しくは、「[メッセージ（Webhook）を受信する](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/)」を参照してください。

### 引用トークンをメッセージ送信時のレスポンスで取得する 

Messaging APIで、[応答メッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)または[プッシュメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-push-message)を送ると、レスポンスとして`sentMessages`プロパティを含むJSONオブジェクトが返ってきます。

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

ただし、レスポンスに引用トークン（`sentMessages[].quoteToken`）が含まれるのは、引用対象として指定可能な以下のメッセージオブジェクトを送信したときのみです。

- [テキストメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#text-messages)
- [テキストメッセージ（v2）](https://developers.line.biz/ja/docs/messaging-api/message-types/#text-messages-v2)
- [スタンプメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#sticker-messages)
- [画像メッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#image-messages)
- [動画メッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#video-messages)
- [テンプレートメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#template-messages)（引用時に表示されるのは`altText`です）
- [Flex Message](https://developers.line.biz/ja/docs/messaging-api/message-types/#flex-messages)（引用時に表示されるのは`altText`です）

上記のメッセージオブジェクトを複数指定してメッセージを送った場合、同じ個数の引用トークンが返ってきます。このとき、`sentMessages`配列内の要素の順番は、送信時のメッセージオブジェクトと同じ順番であることが保証されます。

```json
{
  "sentMessages": [
    {
      "id": "471875397094211585",
      "quoteToken": "YKPDqjc2jmW..."
    },
    {
      "id": "471875397127766017",
      "quoteToken": "eG5SfLhgiFX..."
    }
  ]
}
```
