# Create coupons and send them to users

You can create coupons using the Messaging API and send them to users as messages from your LINE Official Account.

![](https://developers.line.biz/media/messaging-api/coupon/several-coupons.jpg)

<!-- table of contents -->

## Steps to send coupons using the Messaging API 

Using the Messaging API, you can send coupons to users in two steps:

1. [Create a coupon](https://developers.line.biz/en/docs/messaging-api/send-coupons-to-users/#create-coupon)
2. [Send a coupon](https://developers.line.biz/en/docs/messaging-api/send-coupons-to-users/#send-coupon)

<!-- tip start -->

**You can also send coupons using LINE Official Account Manager**

In addition to the Messaging API, you can also create and send coupons using [LINE Official Account Manager](https://manager.line.biz/). For more information, see [Coupons](https://www.lycbiz.com/jp/manual/OfficialAccountManager/coupons-create/) (only available in Japanese) in LINE for Business.

<!-- tip end -->

## Create a coupon 

First, create a coupon using the [Create a coupon](https://developers.line.biz/en/reference/messaging-api/#create-coupon) endpoint.

```sh
curl -v -X POST https://api.line.me/v2/bot/coupon \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d \
'
{
  "title": "Friends-only coupon",
  "description": "- To use this coupon, please show this screen to the staff.\n- Used coupons cannot be used again. If you accidentally mark it as \"used\", it will also become unavailable.\n- This coupon may be changed or terminated without notice regardless of the validity period.",
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

When you create a coupon, the coupon ID will be returned in the response.

```json
{
  "couponId": "01JYNW8JMQVFBNWF1APF8Z3FS7"
}
```

When creating a coupon, you can set acquisition conditions such as "only users who won the lottery can acquire it" by setting `acquisitionCondition.type` to `lottery` in the request body. You can also specify the coupon's benefits using the [reward object](https://developers.line.biz/en/reference/messaging-api/#create-coupon-reward-object) (`reward`), such as "50% discount" or "100 yen cashback".

For more information, see [Create a coupon](https://developers.line.biz/en/reference/messaging-api/#create-coupon) in the Messaging API reference.

Once you have created a coupon, proceed to the [Send a coupon](https://developers.line.biz/en/docs/messaging-api/send-coupons-to-users/#send-coupon) step.

### You can't edit coupons you have created 

Once a coupon has been created, it can't be modified. To change the content of the coupon, you must first [discontinue a coupon](https://developers.line.biz/en/docs/messaging-api/send-coupons-to-users/#discontinue-coupon) and then create a new one.

When creating coupons using the LINE Official Account Manager, you can save them as drafts. However, you can't put coupons in a "draft" state when creating them using the Messaging API.

## Send a coupon 

After creating a coupon and receiving the coupon ID, specify that coupon ID in a [coupon message](https://developers.line.biz/en/docs/messaging-api/message-types/#coupon-messages) and send it. If you don't know the coupon ID, you can [get the coupon list](https://developers.line.biz/en/docs/messaging-api/send-coupons-to-users/#check-coupon-list) to check it.

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

Coupon messages can be sent as any of the following types of messages. You can also send coupons created using the Messaging API as messages in LINE Official Account Manager.

- [Push message](https://developers.line.biz/en/reference/messaging-api/#send-push-message)
- [Multicast message](https://developers.line.biz/en/reference/messaging-api/#send-multicast-message)
- [Broadcast message](https://developers.line.biz/en/reference/messaging-api/#send-broadcast-message)
- [Narrowcast message](https://developers.line.biz/en/reference/messaging-api/#send-narrowcast-message)
- [Reply message](https://developers.line.biz/en/reference/messaging-api/#send-reply-message)

Users can open and get the delivered coupon and use it within the validity period.

![](https://developers.line.biz/media/messaging-api/coupon/coupon-message-ja.jpg)

## Discontinue a coupon 

Coupons automatically expire after the validity period specified when they were created, but you can also manually discontinue them before then using the [Discontinue a coupon](https://developers.line.biz/en/reference/messaging-api/#discontinue-coupon) endpoint.

```sh
curl -v -X PUT https://api.line.me/v2/bot/coupon/01JYNW8JMQVFBNWF1APF8Z3FS7/close \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json'
```

Once a coupon is discontinued, users who have already received it as a message will no longer be able to get it, and users who have already obtained it will no longer be able to use it.

Discontinued coupons can't be reactivated.

For more information, see [Discontinue a coupon](https://developers.line.biz/en/reference/messaging-api/#discontinue-coupon) in the Messaging API reference.

## Check the list of created coupons 

You can use the [Get a list of coupons](https://developers.line.biz/en/reference/messaging-api/#get-coupons-list) endpoint to check the coupon ID and title of the coupons you've created.

```sh
curl -v -X GET https://api.line.me/v2/bot/coupon \
-H 'Authorization: Bearer {channel access token}'
```

This coupon list includes coupons created with both the Messaging API and [LINE Official Account Manager](https://manager.line.biz/). You can view the same list in LINE Official Account Manager.

```json
{
  "items": [
    {
      "couponId": "01JZMWQ9HMDW9ENJP4C167CXP8",
      "title": "Year-end and New Year coupon"
    },
    {
      "couponId": "01JZA9NPPFDJ3RFG8NA9DJ0NQT",
      "title": "Friends-only coupon"
    }
  ]
}
```

You can also use the query parameter `status` to retrieve only valid coupons or only expired coupons. For more information, see [Get a list of coupons](https://developers.line.biz/en/reference/messaging-api/#get-coupons-list) in the Messaging API reference.

## Get details of a coupon 

You can get the details of a specific coupon using the [Get details of a coupon](https://developers.line.biz/en/reference/messaging-api/#get-coupon) endpoint.

```sh
curl -v -X GET https://api.line.me/v2/bot/coupon/01JYNW8JMQVFBNWF1APF8Z3FS7 \
-H 'Authorization: Bearer {channel access token}'
```

You can retrieve details not only for coupons created using the Messaging API, but also for coupons created using LINE Official Account Manager.

```json
{
  "couponId": "01K0B456W5Y6SBD3YH74YM6QE6",
  "title": "Friends-only coupon",
  "description": "- To redeem your coupon, present this screen at checkout.\n- Redeemable once only, even if previously redeemed only unintentionally by the customer.\n- The validity period of this coupon may change or it may be canceled without notice.",
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
  "usageCondition": "Usable for payments of 1,000 yen or more",
  "status": "RUNNING",
  "createdTimestamp": 1752720120
}
```

For more information, see [Get details of a coupon](https://developers.line.biz/en/reference/messaging-api/#get-coupon) in the Messaging API reference.

## Check the number of views and uses of sent coupons 

You can check the number of times sent coupons were viewed and used in [LINE Official Account Manager](https://manager.line.biz/). For more information, see [Insight - Coupons](https://www.lycbiz.com/jp/manual/OfficialAccountManager/insight_coupon/) (only available in Japanese) in LINE for Business.

## Coupon image display size 

Coupon images can be displayed by specifying the image URL in `imageUrl` when creating the coupon. If you specify a square image, the aspect ratio will be 1.51:1 (width:height) in the chat screen, so the top and bottom of the image will be partially cut off.

![](https://developers.line.biz/media/messaging-api/coupon/how-images-look.jpg)

<!-- tip start -->

**How do I create coupon images**

You can use the coupon images provided from [Free template image collection](https://lymcampus.jp/line-official-account/courses/template/lessons/6-1-1) (only available in Japanese) in LINE Marketing Campus or the templates available at [LINE Creative Lab](https://creativelab.line.biz/) (only available in Japanese).

![Sample coupon image](https://developers.line.biz/media/messaging-api/coupon/sample-coupon-image-100-yen-off.jpg)

<!-- tip end -->
