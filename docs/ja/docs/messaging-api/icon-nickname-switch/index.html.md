# アイコンと表示名をカスタマイズする

APIを使って以下のメッセージを送る際には、LINE公式アカウントのアイコンや表示名をカスタマイズできます。[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の種類に制限はありません。

- [プッシュメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-push-message)
- [マルチキャストメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-multicast-message)
- [ナローキャストメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message)
- [ブロードキャストメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-broadcast-message)
- [応答メッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)

メッセージのアイコンや表示名を指定しない場合は、デフォルトのアイコンとLINE公式アカウント名が表示されます。

アイコンや表示名をカスタマイズする場合は、まず開発者自身のLINEアカウントに対してアイコンと表示名をカスタマイズしたプッシュメッセージを送信して、メッセージの見た目を確認することを推奨します。

## アイコンと表示名をカスタマイズする 

デフォルトのメッセージと、アイコンと表示名を指定したメッセージの見た目の違いは下図のとおりです。表示名には`from 'アカウント名'`が付いています。これは、LINE公式アカウントを識別しやすくし、他のアカウントとの誤認を防ぐためのものです。トーク画面上部に表示されるアカウント名は、どのような場合でも変わりません。

![](https://developers.line.biz/media/messaging-api/icon-nickname-switch/icon-nickname-switch.jpg)

### リクエストの例 

以下は、アイコンと表示名をカスタマイズしてメッセージを送信するリクエストの例です。

```sh
curl -v -X POST https://api.line.me/v2/bot/message/push \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {CHANNEL_ACCESS_TOKEN}' \
-d '{
    "to": "U1234....",
    "messages": [
        {
            "type": "text",
            "text": "Hello, I am Cony!!",
            "sender": {
                "name": "Cony",
                "iconUrl": "https://line.me/conyprof"
            }
        }
    ]
}'
```

## アイコンと表示名のカスタマイズ範囲 

このセクションでは、アイコンと表示名のカスタマイズが適用される場所について説明します。

### トークルーム 

メッセージに指定したアイコンと表示名は、そのメッセージのアイコンと表示名のみに影響します。

- メッセージバブル：カスタマイズされたアイコンと表示名（`表示名 from 'アカウント名'`）が表示されます。
- トークルームの名前：上部に表示されるトークルーム名はLINE公式アカウントのままです。
- ビジネスプロフィールページ：LINE公式アカウントのビジネスプロフィールページに表示されるプロフィール画像や表示名はカスタマイズできません。

### メッセージ検索結果 

アイコンと表示名がカスタマイズされたメッセージが検索結果に表示される場合、カスタマイズされたアイコンと表示名が`from 'アカウント名'`と共に表示されます。

### トークリストとプレビュー 

トークリストに表示されるLINE公式アカウントのアイコンや表示名はカスタマイズできません。ただし、テキスト以外のメッセージのプレビューには、カスタマイズされたアイコンと表示名が表示されます。たとえば、表示名をカスタマイズして写真を送信した場合、プレビューメッセージには「（表示名）が写真を送信しました」と表示されます。

### トークリスト検索画面 

トークリスト検索画面に表示されるLINE公式アカウントは、デフォルトのアイコンと表示名で表示されます。

### 友だちリスト 

友だちリストに表示されるLINE公式アカウントは、デフォルトのアイコンと表示名で表示されます。

## 関連ページ 

アイコンと表示名のカスタマイズの仕様について詳しくは、『Messaging APIリファレンス』の「[アイコンと表示名のカスタマイズ](https://developers.line.biz/ja/reference/messaging-api/#icon-nickname-switch)」を参照してください。
