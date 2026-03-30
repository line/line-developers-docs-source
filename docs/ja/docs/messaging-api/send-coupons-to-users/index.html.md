# クーポンを作成してユーザーに送る

Messaging APIでクーポンを作成して、LINE公式アカウントからユーザーにメッセージとして送信できます。

![](https://developers.line.biz/media/messaging-api/coupon/several-coupons.jpg)

<!-- table of contents -->

## Messaging APIでクーポンを送る手順 

Messaging APIでは、次の2つの手順でユーザーにクーポンが送れます。

1. [クーポンを作成する](https://developers.line.biz/ja/docs/messaging-api/send-coupons-to-users/#create-coupon)
2. [クーポンを送信する](https://developers.line.biz/ja/docs/messaging-api/send-coupons-to-users/#send-coupon)

<!-- tip start -->

**クーポンはLINE Official Account Managerでも送信できます**

クーポンはMessaging APIの他に、[LINE Official Account Manager](https://manager.line.biz/)でも作成して送信できます。詳しくは、『LINEヤフー for Business』の「[クーポン](https://www.lycbiz.com/jp/manual/OfficialAccountManager/coupons-create/)」を参照してください。

<!-- tip end -->

## クーポンを作成する 

まずは「[クーポンを作成する](https://developers.line.biz/ja/reference/messaging-api/#create-coupon)」エンドポイントでクーポンを作成します。

```sh
curl -v -X POST https://api.line.me/v2/bot/coupon \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d \
'
{
  "title": "友だち限定クーポン",
  "description": "- クーポンを使用するには、この画面をスタッフに提示してください。\n- 使用済みのクーポンはご利用になれません。また、お客さまの操作で誤って「使用済み」にしてしまった場合も利用できなくなります。\n- 本クーポンは有効期間に関わらず、予告なく変更されたり、終了したりする場合があります。",
  "reward": {
    "type": "discount",
    "priceInfo": {
      "type": "fixed",
      "fixedAmount": 100
    }
  },
  "acquisitionCondition": {
    "type": "normal"
  },
  "startTimestamp": 0,
  "endTimestamp": 1924959599,
  "imageUrl": "https://developers.line.biz/media/messaging-api/coupon/sample-coupon-image-100-yen-off.jpg",
  "timezone": "ASIA_TOKYO",
  "visibility": "UNLISTED",
  "maxUseCountPerTicket": 1
}'
```

クーポンを作成すると、レスポンスでクーポンIDが返されます。

```json
{
  "couponId": "01JYNW8JMQVFBNWF1APF8Z3FS7"
}
```

クーポンを作成する際は、リクエストボディの`acquisitionCondition.type`を`lottery`にして「抽選形式で当選したユーザーのみ獲得できる」という獲得条件を設けたり、[リワードオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#create-coupon-reward-object)（`reward`）で「50%割引」や「100円キャッシュバック」といった特典を細かく設定したりできます。

詳しくは、『Messaging APIリファレンス』の「[クーポンを作成する](https://developers.line.biz/ja/reference/messaging-api/#create-coupon)」を参照してください。

クーポンを作成したら、続いて[クーポンを送信する](https://developers.line.biz/ja/docs/messaging-api/send-coupons-to-users/#send-coupon)手順に進みます。

### 作成したクーポンは修正できません 

作成したクーポンは、後から内容を修正できません。クーポンの内容を変更したい場合は、[クーポンを終了](https://developers.line.biz/ja/docs/messaging-api/send-coupons-to-users/#discontinue-coupon)させて、新たに作成しなおしてください。

なお、LINE Official Account Managerを使ってクーポンを作成する場合は、「下書き」の状態で保存できますが、Messaging APIでクーポンを作成するときは「下書き」状態にはできません。

## クーポンを送信する 

クーポンを作成してクーポンIDを取得したら、そのクーポンIDを[クーポンメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#coupon-messages)で指定して送信します。クーポンIDが分からなくなってしまった場合は、[クーポンの一覧を取得](https://developers.line.biz/ja/docs/messaging-api/send-coupons-to-users/#check-coupon-list)して確認できます。

```sh
curl -v -X POST https://api.line.me/v2/bot/message/broadcast \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d '
{
  "messages": [
    {
      "type": "coupon",
      "couponId": "01JYNW8JMQVFBNWF1APF8Z3FS7"
    }
  ]
}'
```

クーポンメッセージは、以下のすべてのメッセージとして送信できます。また、Messaging APIで作成したクーポンをLINE Official Account Managerでメッセージとして送信することもできます。

- [プッシュメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-push-message)
- [マルチキャストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-multicast-message)
- [ブロードキャストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-broadcast-message)
- [ナローキャストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message)
- [応答メッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)

ユーザーは届いたクーポンを開いて獲得することで、有効期間内にクーポンを使用できます。

![](https://developers.line.biz/media/messaging-api/coupon/coupon-message-ja.jpg)

## クーポンを終了する 

クーポンは、作成時に指定した有効期間を過ぎると自動的に終了しますが、有効期間中に「[クーポンを終了する](https://developers.line.biz/ja/reference/messaging-api/#discontinue-coupon)」エンドポイントを用いて手動で終了させることもできます。

```sh
curl -v -X PUT https://api.line.me/v2/bot/coupon/01JYNW8JMQVFBNWF1APF8Z3FS7/close \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json'
```

クーポンを終了させると、すでにクーポンをメッセージとして受信していたユーザーがクーポンを獲得できなくなると共に、そのクーポンを獲得済みのユーザーも利用できなくなります。

終了したクーポンを再び有効にすることはできません。

詳しくは、『Messaging APIリファレンス』の「[クーポンを終了する](https://developers.line.biz/ja/reference/messaging-api/#discontinue-coupon)」を参照してください。

## 作成済みのクーポン一覧を確認する 

作成したクーポンのクーポンIDとクーポン名は、「[クーポンの一覧を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-coupons-list)」エンドポイントで確認できます。

```sh
curl -v -X GET https://api.line.me/v2/bot/coupon \
-H 'Authorization: Bearer {channel access token}'
```

このクーポンの一覧には、Messaging APIで作成したクーポンだけでなく、[LINE Official Account Manager](https://manager.line.biz/)で作成したクーポンも含まれており、同じ一覧がLINE Official Account Managerでも確認できます。

```json
{
  "items": [
    {
      "couponId": "01JZMWQ9HMDW9ENJP4C167CXP8",
      "title": "年末年始クーポン"
    },
    {
      "couponId": "01JZA9NPPFDJ3RFG8NA9DJ0NQT",
      "title": "友だち限定クーポン"
    }
  ]
}
```

クエリパラメータの`status`を用いて、有効なクーポンのみ、あるいは終了したクーポンのみを取得することもできます。詳しくは、『Messaging APIリファレンス』の「[クーポンの一覧を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-coupons-list)」を参照してください。

## クーポンの詳細を確認する 

「[クーポンの詳細を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-coupon)」エンドポイントを使うと、クーポンIDを指定して特定のクーポンの詳細を確認できます。

```sh
curl -v -X GET https://api.line.me/v2/bot/coupon/01JYNW8JMQVFBNWF1APF8Z3FS7 \
-H 'Authorization: Bearer {channel access token}'
```

Messaging APIで作成したクーポンだけでなく、LINE Official Account Managerで作成したクーポンの詳細も取得できます。

```json
{
  "couponId": "01K0B456W5Y6SBD3YH74YM6QE6",
  "title": "友だち限定クーポン",
  "description": "- クーポンを使用するには、この画面をスタッフに提示してください。\n- 使用済みのクーポンはご利用になれません。また、お客さまの操作で誤って「使用済み」にしてしまった場合も利用できなくなります。\n- 本クーポンは有効期間に関わらず、予告なく変更されたり、終了したりする場合があります。",
  "acquisitionCondition": {
    "type": "lottery",
    "lotteryProbability": 50,
    "maxAcquireCount": -1
  },
  "startTimestamp": 1752678000,
  "endTimestamp": 1924959540,
  "timezone": "ASIA_TOKYO",
  "couponCode": "COUPONCODE123456",
  "maxUseCountPerTicket": 1,
  "maxTicketPerUser": 1,
  "visibility": "UNLISTED",
  "reward": {
    "type": "discount",
    "priceInfo": {
      "type": "fixed",
      "fixedAmount": 100,
      "currency": "JPY"
    }
  },
  "imageUrl": "https://oa-coupon.line-scdn-dev.net/0h9gbUqRVkZkhfLHhXMLYZHwdyaCosWGBAPFR7cD5tZidsTnofYDVfezt-ZAR3YER9OzRfK35XZwR6TH5uYDF2TnJ-cBNyfURpPRl2RSFSXQc0TiJhYCFiXiZ8XXk0",
  "usageCondition": "1,000円以上のお支払いで利用可能",
  "status": "RUNNING",
  "createdTimestamp": 1752720120
}
```

詳しくは、『Messaging APIリファレンス』の「[クーポンの詳細を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-coupon)」を参照してください。

## 送信したクーポンの表示回数や使用回数を確認する 

メッセージとして送信したクーポンが表示された回数や、使用された回数などは[LINE Official Account Manager](https://manager.line.biz/)で確認できます。詳しくは、『LINEヤフー for Business』の「[分析 - クーポン](https://www.lycbiz.com/jp/manual/OfficialAccountManager/insight_coupon/)」を参照してください。

## クーポンの画像が表示されるサイズ 

クーポンの画像は、クーポンの作成時に`imageUrl`で画像のURLを指定することで表示できます。正方形の画像を指定した場合、トーク画面ではアスペクト比が1.51:1（幅：高さ）になるため、画像の上下が一部切れた状態で表示されます。

![](https://developers.line.biz/media/messaging-api/coupon/how-images-look.jpg)

<!-- tip start -->

**クーポンの画像はどうやって作ればいい？**

クーポンの画像は『LINEヤフーマーケティングキャンパス』の「[無料でもらえるテンプレート画像まとめ](https://lymcampus.jp/line-official-account/courses/template/lessons/6-1-1)」や、[LINE Creative Lab](https://creativelab.line.biz/)のテンプレートを利用することもできます。

![Sample coupon image](https://developers.line.biz/media/messaging-api/coupon/sample-coupon-image-100-yen-off.jpg)

<!-- tip end -->
