# メッセージ（Webhook）を受信する

ユーザーが、LINE公式アカウントを友だち追加したり、LINE公式アカウントにメッセージを送ったりすると、[LINE Developersコンソール](https://developers.line.biz/console/)の「Webhook URL」に指定したURL（ボットサーバー）に対して、LINEプラットフォームからWebhookイベントオブジェクトを含むHTTP POSTリクエストが送られます。

ボットサーバーがWebhookイベントオブジェクトを適切に処理していることを確認してください。なお、ボットサーバーがWebhookの受信に長期間失敗している場合、LINEプラットフォームからボットサーバーへのWebhookの送信を停止する可能性があります。

<!-- warning start -->

**セキュリティ上の警告**

ボットサーバーが受信したHTTP POSTリクエストは、LINEプラットフォームから送信されていない危険なリクエストの可能性があります。必ず署名を検証してから、Webhookイベントオブジェクトを処理してください。

<!-- warning end -->

<!-- tip start -->

**イベントは非同期で処理することを推奨します**

現在のリクエストが処理されるまで後続のリクエストが待たされるのを防ぐため、Webhookイベントは非同期で処理することを推奨します。

<!-- tip end -->

## 署名を検証する 

ボットサーバーにWebhookのリクエストが届いたら、[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)を処理する前に、リクエストヘッダーに含まれる署名を検証してください。署名の検証は、開発者のボットサーバーに届いたリクエストが「LINEプラットフォームから送信されたWebhookか」および「通信経路で改ざんされていないか」などを確認するための重要な手順です。

詳しくは、「[Webhookの署名を検証する](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-signature/)」を参照してください。

## Webhookイベントのタイプ 

Webhookイベントオブジェクトに含まれるデータに基づいて、ボットがどのように反応するかを制御できます。また、ボットに何かアクションを起こさせたり、ユーザーに応答させることもできます。[トーク](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#webhook-event-in-one-on-one-talk-or-group-chat)、[ビーコン、アカウント連携](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#other-webhook-events)のWebhookイベントを取得できます。詳しくは、『Messaging APIリファレンス』の「[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)」を参照してください。

### トークでのWebhookイベント 

1対1のトーク、および[グループトークと複数人トーク](https://developers.line.biz/ja/docs/messaging-api/group-chats/)において、ボットサーバーが受信するWebhookイベントは以下のとおりです。

| Webhookイベント | 受信するタイミング | 1対1のトーク | グループトークと複数人トーク |
| --- | --- | --- | --- |
| [メッセージイベント](https://developers.line.biz/ja/reference/messaging-api/#message-event) | ユーザーがメッセージを送信した時。このイベントには応答できます。 | ✅ | ✅ |
| [送信取消イベント](https://developers.line.biz/ja/reference/messaging-api/#unsend-event) | ユーザーがメッセージの送信を取り消した時。このイベントの処理について詳しくは、[送信取消イベント受信時の処理](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#webhook-unsend-message)を参照してください。 | ✅ | ✅ |
| [フォローイベント](https://developers.line.biz/ja/reference/messaging-api/#follow-event) | LINE公式アカウントが友だち追加またはブロック解除された時。このイベントには応答できます。 | ✅ | ❌ |
| [フォロー解除イベント](https://developers.line.biz/ja/reference/messaging-api/#unfollow-event) | LINE公式アカウントがブロックされた時 | ✅ | ❌ |
| [参加イベント](https://developers.line.biz/ja/reference/messaging-api/#join-event) | LINE公式アカウントがグループトークまたは複数人トークに参加した時。このイベントには応答できます。 | ❌ | ✅ |
| [退出イベント](https://developers.line.biz/ja/reference/messaging-api/#leave-event) | ユーザーがグループトークからLINE公式アカウントを削除したか、LINE公式アカウントがグループトークまたは複数人トークから退出した時 | ❌ | ✅ |
| [メンバー参加イベント](https://developers.line.biz/ja/reference/messaging-api/#member-joined-event) | LINE公式アカウントがメンバーになっているグループトークまたは複数人トークに、ユーザーが参加した時。このイベントには応答できます。 | ❌ | ✅ |
| [メンバー退出イベント](https://developers.line.biz/ja/reference/messaging-api/#member-left-event) | LINE公式アカウントがメンバーになっているグループトークまたは複数人トークから、ユーザーが退出した時 | ❌ | ✅ |
| [ポストバックイベント](https://developers.line.biz/ja/reference/messaging-api/#postback-event) | ユーザーが、[ポストバックアクション](https://developers.line.biz/ja/reference/messaging-api/#postback-action)を実行した時。このイベントには応答できます。 | ✅ | ✅ |
| [動画視聴完了イベント](https://developers.line.biz/ja/reference/messaging-api/#video-viewing-complete) | ユーザーが、LINE公式アカウントから送信された`trackingId`が指定された動画メッセージの視聴が完了した時。このイベントには応答できます。 | ✅ | ❌ |

✅ ボットサーバーはイベントを受信する&nbsp;&nbsp;&nbsp;&nbsp;❌ ボットサーバーはイベントを受信しない

#### liff.sendMessages()でメッセージが送信されたときのWebhook 

ユーザーはLINEアプリを用いて自分から[テンプレートメッセージ](https://developers.line.biz/ja/reference/messaging-api/#template-messages)や[Flex Message](https://developers.line.biz/ja/reference/messaging-api/#flex-message)を送ることができませんが、開発者が[`liff.sendMessages()`](https://developers.line.biz/ja/reference/liff/#send-messages)を利用することで、ユーザーの代わりに、LINEミニアプリやLIFFアプリが開かれているトーク画面にユーザーからのメッセージを送信できます。

この`liff.sendMessages()`によってユーザーからテンプレートメッセージまたはFlex Messageが送信された場合、LINEプラットフォームからWebhookは送信されません。それ以外の[メッセージタイプ](https://developers.line.biz/ja/docs/messaging-api/message-types/)であれば、Webhookは送信されます。

#### ユーザーが送った引用メッセージをWebhookで受け取る 

ユーザーが過去のメッセージを引用してメッセージを送った場合、Webhookの`message`プロパティに含まれる`quotedMessageId`で引用対象となったメッセージのIDを確認できます。このとき、引用対象となったメッセージのIDは確認できますが、メッセージの内容（テキストやスタンプなど）は再取得できません。

![](https://developers.line.biz/media/messaging-api/receiving-messages/chat-reply.png)

以下は、ユーザーが過去のメッセージを引用したメッセージを送った際に、ボットサーバーに届くWebhookの例です。

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "type": "message",
      "message": {
        "type": "text",
        "id": "468789577898262530", // 送られてきたメッセージのID
        "quotedMessageId": "468789532432007169", // 引用対象となったメッセージのID
        "quoteToken": "q3Plxr4AgKd...",
        "text": "Chicken, please." // 送られてきたメッセージのテキスト
      },
      "webhookEventId": "01H810YECXQQZ37VAXPF6H9E6T",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1692251666727,
      "source": {
        "type": "group",
        "groupId": "Ca56f94637c...",
        "userId": "U4af4980629..."
      },
      "replyToken": "38ef843bde154d9b91c21320ffd17a0f",
      "mode": "active"
    }
  ]
}
```

`quotedMessageId`プロパティについて詳しくは、『Messaging APIリファレンス』の「[メッセージイベント](https://developers.line.biz/ja/reference/messaging-api/#message-event)」の「[テキスト](https://developers.line.biz/ja/reference/messaging-api/#wh-text)」および「[スタンプ](https://developers.line.biz/ja/reference/messaging-api/#wh-sticker)」を参照してください。

ユーザーが引用メッセージを送る方法について詳しくは、『LINEみんなの使い方ガイド』の「[トークのリプライ機能を利用する](https://guide.line.me/ja/chats-calls-notifications/chats/chat-reply.html)」を参照してください。

#### ボットへのメンションを含むメッセージが送信されたときのWebhook 

ユーザーが送信したメッセージに自分のボットへのメンションがあった場合、ボットサーバーに送信されるWebhookイベント内の[テキストメッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#wh-text)において、次の値が設定されます。

- `mention.mentionees[].type`に`user`が設定される。
- `mention.mentionees[].userId`にボットのユーザーIDが設定される。
- `mention.mentionees[].isSelf`に`true`が設定される。

たとえば、次のようなメッセージイベントを含むWebhookイベントオブジェクトがボットサーバーに送信されます。

```json
"message": {
  "id": "444573844083572737",
  "type": "text",
  "quoteToken": "q3Plxr4AgKd...",
  "text": "@example_bot Good Morning!!",
  "mention": {
    "mentionees": [
      {
        "index": 0,
        "length": 12,
        "userId": "{ボットのユーザーID}",
        "type": "user",
        "isSelf": true
      }
    ]
  }
}
```

なお、ボットのユーザーIDは、[Webhookのリクエストボディ](https://developers.line.biz/ja/reference/messaging-api/#request-body)にある`destination`プロパティや、「[ボットの情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-bot-info)」エンドポイントで取得できる`userId`プロパティで確認できます。

### その他のWebhookイベント 

Webhookイベントは、以下のようにビーコンやアカウント連携にも利用できます。

| Webhookイベント | 受信するタイミング |
| --- | --- |
| [ビーコンイベント](https://developers.line.biz/ja/reference/messaging-api/#beacon-event) | ビーコンの電波の受信圏にユーザーが入った時。このイベントには応答できます。詳しくは、「[LINEでビーコンを使う](https://developers.line.biz/ja/docs/messaging-api/using-beacons/)」を参照してください。 |
| [アカウント連携イベント](https://developers.line.biz/ja/reference/messaging-api/#account-link-event) | ユーザーがLINEアカウントとプロバイダーが提供するサービスのアカウントを連携した時。このイベントには応答できます。詳しくは、「[ユーザーアカウントの連携](https://developers.line.biz/ja/docs/messaging-api/linking-accounts/)」を参照してください。 |

## 送信取消イベント受信時の処理 

ユーザーは、送信後の一定期間内であれば、自分が送ったメッセージの送信を取り消すことができます。

ユーザーがメッセージの送信を取り消すと、ボットサーバーに[送信取消イベント](https://developers.line.biz/ja/reference/messaging-api/#unsend-event)が届きます。送信取消イベントを受け取った場合、サービス提供者はユーザーがメッセージの送信を取り消した意図を尊重し、以降は対象のメッセージを見たり利用したりできないよう、最大限の配慮を持って対象のメッセージを適切に扱うことを推奨します。

たとえば、送信が取り消されたメッセージを以下のように取り扱ってください。

- 独自の管理画面などで表示している対象のメッセージの表示を取り消す
- データベースなどに保存している対象のメッセージを削除する

LINEアプリでのメッセージの送信取消について詳しくは、『LINEみんなの使い方ガイド』の「[トークの送信取消機能を利用する](https://guide.line.me/ja/chats-calls-notifications/chats/chat-delete.html)」を参照してください。

## 受け取りに失敗したWebhookを再送する 

Messaging APIでは、ボットサーバー側が受け取りに失敗したWebhookを再送する機能を提供しています。ボットサーバーが一時的なアクセス過多などの理由でWebhookに対して正常に応答できなかった場合でも、一定の期間、LINEプラットフォームから再送されるため、ボットサーバーの復旧後にWebhookを受け取ることができます。

Webhookの再送は、すべてのMessaging APIチャネルで利用可能です。

<!-- note start -->

**Webhookの再送を有効にする前に確認してください**

- ネットワーク経路上の問題等により、同じWebhookイベントが重複して送信される可能性があります。これが問題になる場合は、Webhookイベントオブジェクトの`webhookEventId`を利用し、重複の検出を行ってください。
- Webhookが再送されることにより、Webhookを受信する順序がイベントの発生順序と異なる可能性があります。これが問題になる場合は、Webhookイベントオブジェクトの`timestamp`を確認することによって、前後関係を確認してください。

<!-- note end -->

### 再送されるWebhook 

再送される[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)の内容は、`deliveryContext.isRedelivery`の値を除き、元のWebhookイベントオブジェクトと同じになります。WebhookイベントIDや応答トークンなどの値は変更されません。

なお、再送されるWebhookイベントオブジェクトに含まれる応答トークンは、特定の場合を除き使用できます。応答トークンについて詳しくは、『Messaging APIリファレンス』の「[応答トークン](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message-reply-token)」を参照してください。

### Webhookの再送を有効にする 

Webhookの再送は、デフォルトでは無効になっています。Webhookの再送を有効にするには、次の手順を行います。

1. [LINE Developersコンソール](https://developers.line.biz/console/)からチャネルの設定画面を開く。
1. ［**Messaging API設定**］タブをクリックする。
1. ［**Webhookの利用**］を有効にする。
1. ［**Webhookの再送**］を有効にする。

［**Webhookの再送**］を有効にする際、Webhook再送の利用に際する注意事項が表示されます。注意事項を確認し、理解した上でWebhook再送を有効にしてください。

![](https://developers.line.biz/media/messaging-api/receiving-messages/enable-webhook-redelivery-ja.png)

### Webhookが再送される条件 

LINEプラットフォームから送信されたWebhookは、次の2つの条件を満たすときに、一定の期間内に、一定の時間を空けて再送されます。

- [Webhookの再送を有効にしている](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#enable-webhook-redelivery)。
- Webhookに対して、ボットサーバーがステータスコード`200`番台を返さなかった。

Webhookを再送する回数、間隔は開示しておりません。また回数、間隔については、予告なく変更される可能性があります。

<!-- note start -->

**Webhookを再送できない場合があります**

Webhookの再送は、Webhookの確実な再送を保証するものではありません。また、Webhook再送の件数が急激に増加し、LINEプラットフォームの動作に影響を与えると判断された場合、Webhookの再送設定が強制的に無効になる可能性があります。

<!-- note end -->

## Webhookのエラーの原因を確認する 

Messaging APIでは、Webhookの送信におけるエラーの原因と統計情報を確認できる機能を提供しています。ボットサーバー側の不具合などによりWebhookを受け取ることができなかった場合において、Webhookの送信状況を把握するときなどに役立ちます。

詳しくは、「[Webhookのエラーの原因と統計情報を確認する](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/)」を参照してください。

## ユーザーが送ったコンテンツを取得する 

[Webhook](https://developers.line.biz/ja/reference/messaging-api/#webhooks)で受信したメッセージIDを使って、ユーザーが送信したコンテンツを取得できます。取得できるコンテンツは、次のとおりです。

- [画像、動画、音声、ファイル](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#getting-content-file-sent-by-users)
- [画像または動画のプレビュー画像](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#getting-content-preview-image)

<!-- note start -->

**注意**

- ユーザーが送ったコンテンツは一定期間後、自動的に削除されます。
- ユーザーが送ったテキストは、Webhookの[テキスト](https://developers.line.biz/ja/reference/messaging-api/#wh-text)メッセージオブジェクトで受信できます。Webhookを受信した後で、あらためてテキストを取得するためのAPIはありません。

<!-- note end -->

### 画像、動画、音声、ファイルを取得する 

Webhookで受信したメッセージIDを使って、ユーザーが送信した[画像](https://developers.line.biz/ja/reference/messaging-api/#wh-image)、[動画](https://developers.line.biz/ja/reference/messaging-api/#wh-video)、[音声](https://developers.line.biz/ja/reference/messaging-api/#wh-audio)、および[ファイル](https://developers.line.biz/ja/reference/messaging-api/#wh-file)を取得できます。

リクエストの例

```sh
curl -v -X GET https://api-data.line.me/v2/bot/message/{messageId}/content \
-H 'Authorization: Bearer {channel access token}'
```

詳しくは、『Messaging APIリファレンス』の「[コンテンツを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-content)」を参照してください。

### 画像または動画のプレビュー画像を取得する 

Webhookで受信したメッセージIDを使って、ユーザーが送信した画像、動画のプレビュー画像を取得できます。

リクエストの例

```sh
curl -v -X GET https://api-data.line.me/v2/bot/message/{messageId}/content/preview \
-H 'Authorization: Bearer {channel access token}'
```

プレビュー画像は、実際のコンテンツよりも軽量なデータサイズに変換された画像データです。

たとえば、プレビュー画像はサムネイルとして使用できます。CRMのようなサイトを構築する際には、大きな画像や動画のダウンロード中にサムネイルを表示できます。これにより、ユーザーはすばやくコンテンツの概要を確認でき、システムのユーザーエクスペリエンスを向上させることができます。

詳しくは、『Messaging APIリファレンス』の「[画像または動画のプレビュー画像を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-image-or-video-preview)」を参照してください。

## ユーザープロフィール情報を取得する 

[Webhook](https://developers.line.biz/ja/reference/messaging-api/#webhooks)に含まれるユーザーIDを使って、ユーザーのLINEプロフィール情報（ユーザーの表示名、ユーザーID、プロフィール画像のURL、ステータスメッセージなど）を取得できます。

リクエストの例

```sh
curl -v -X GET https://api.line.me/v2/bot/profile/{userId} \
-H 'Authorization: Bearer {channel access token}'
```

成功した場合、JSONオブジェクトが返されます。

```json
{
  "displayName": "LINE Botto",
  "userId": "U4af4980629...",
  "pictureUrl": "https://profile.line-scdn.net/ch/v2/p/uf9da5ee2b...",
  "statusMessage": "Hello world!"
}
```

詳しくは、『Messaging APIリファレンス』の「[プロフィールを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-profile)」を参照してください。
