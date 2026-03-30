# グループトークと複数人トーク

LINE公式アカウントは、Messaging APIを使用してグループトークや複数人トーク内のユーザーと対話できます。このページでは、グループトークや複数人トークでのLINE公式アカウントの使い方について説明します。

## 複数のユーザーとのトークの種類 

LINEには、複数のユーザーとのトークとして、**グループトーク**と**複数人トーク**の2種類があります。グループトークまたは複数人トークのユーザーは**メンバー**と呼びます。

<!-- tip start -->

**複数人トークはグループトークに統合されました**

LINEバージョン10.17.0以降、複数人トークはグループトークに統合されました。統合以前に作成された複数人トークは引き続き利用できますが、バージョン10.17.0以降のLINEで複数の友だちとのトークを新規作成した場合は、必ずグループトークになります。詳しくは、『LINEみんなの使い方ガイド』の「[グループを作成・管理する](https://guide.line.me/ja/friends-and-groups/create-groups.html)」を参照してください。

<!-- tip end -->

### グループトーク 

グループトークは、複数人での継続的な利用を想定して設計されたトークです。グループトークには識別子として[グループID](https://developers.line.biz/ja/glossary/#group-id)が発行されます。ユーザーはグループトークを作成して、特定の名前をつけられます。グループトークはアルバム、ノートなどの機能に対応しています。

<!-- tip start -->

**ヒント**

ユーザーが1対1のトークに3人目のユーザーを招待した場合は、グループトークが作成されます。グループトークでは、グループに招待されたユーザーの承認フローの有無を設定できます。設定方法について詳しくは、『LINEみんなの使い方ガイド』の「[グループを作成・管理する](https://guide.line.me/ja/friends-and-groups/create-groups.html)」を参照してください。

<!-- tip end -->

### 複数人トーク 

複数人トークは、複数人での一時的な利用を想定して設計されたトークです。複数人トークには識別子として[トークルームID](https://developers.line.biz/ja/glossary/#room-id)が発行されます。複数人トークでは、参加しているメンバーの名前がトークルームの名前として自動的に設定されます。複数人トークはアルバム、ノートなどの機能には対応していません。

LINEバージョン10.17.0以降、複数人トークはグループトークに統合されました。統合以前に作成された複数人トークは引き続き利用できますが、バージョン10.17.0以降のLINEで複数の友だちとのトークを新規作成した場合は、必ずグループトークになります。

## グループトークや複数人トークにLINE公式アカウントを招待する 

LINEユーザーは、グループトークや複数人トークにLINE公式アカウントを招待できます。招待されるためには、[LINE Developersコンソール](https://developers.line.biz/console/)のチャネル設定にある［**Messaging API設定**］タブで、［**グループトーク・複数人トークへの参加を許可する**］を有効にしておく必要があります。この設定は、デフォルトでは無効になっています。また、グループトークや複数人トークに同時に複数のLINE公式アカウントは参加できないことに注意してください。

## Webhookイベントを受け取る 

1対1のトークと同様に、グループトークや複数人トークでもWebhookイベントを受信できます。詳しくは、「[トークでのWebhookイベント](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#webhook-event-in-one-on-one-talk-or-group-chat)」および『Messaging APIリファレンス』の「[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)」を参照してください。

### メッセージイベント利用時のヒント 

1対1のトークと同様に、LINE公式アカウントが追加されているグループトークや複数人トークにメッセージが送られた場合も、メッセージイベントがボットサーバーに送られます。

[メッセージイベント](https://developers.line.biz/ja/reference/messaging-api/#message-event)の`source`プロパティには、送信元グループトークのグループID（`groupId`）または送信元複数人トークのトークルームID（`roomId`）が含まれます。

```json
"source": {
    "type": "group",
    "groupId": "Ca56f94637c...",
    "userId": "U4af4980629..."
}
```

グループIDおよびトークルームIDについて詳しくは、「[ユーザーID、グループID、トークルームIDとはどのような値ですか？](https://developers.line.biz/ja/faq/#what-are-userid-groupid-and-roomid)」を参照してください。

## エンドポイントにリクエストを送る 

グループトークおよび複数人トークの特有の操作は以下のとおりです。詳しくは、『[Messaging APIリファレンス](https://developers.line.biz/ja/reference/messaging-api/)』を参照してください。

- **グループトーク**
  - [グループトークの概要を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-group-summary)
  - [グループトークに参加しているユーザーの人数を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-members-group-count)
  - [グループトークのメンバーのユーザーIDを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-group-member-user-ids)
  - [グループトークのメンバーのプロフィールを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-group-member-profile)
  - [グループトークから退出する](https://developers.line.biz/ja/reference/messaging-api/#leave-group)
- **複数人トーク**
  - [複数人トークに参加しているユーザーの人数を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-members-room-count)
  - [複数人トークのメンバーのユーザーIDを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-room-member-user-ids)
  - [複数人トークのメンバーのプロフィールを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-room-member-profile)
  - [複数人トークから退出する](https://developers.line.biz/ja/reference/messaging-api/#leave-room)

### メッセージ送信時のヒント 

1対1のトークと同様に、LINE公式アカウントが追加されているグループトークや複数人トークに[応答メッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)と[プッシュメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-push-message)を送信できます。

プッシュメッセージを送るときは、送信先として、リクエストボディの`to`プロパティにグループIDまたはルームIDを指定します。送信先のIDは、[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)に含まれています。メッセージはグループトークや複数人トークのすべてのメンバーに表示されます。

<!-- tip start -->

**ヒント**

グループトークや複数人トークで、複数のユーザーを指定して[マルチキャストメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-multicast-message)ことはできません。

<!-- tip end -->
