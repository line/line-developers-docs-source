# Use beacons with LINE

With LINE Beacon, your bot receives [beacon webhook events](https://developers.line.biz/en/reference/messaging-api/#beacon-event) whenever a LINE user enters a beacon region. You can customize your bot app to interact with users with LINE Beacon in the context that suits your business needs.

<!-- note start -->

**Note**

LINE Beacon is available in Japan, Taiwan, and Thailand.

<!-- note end -->

<!-- tip start -->

**Use the latest LINE for LINE Beacon**

We recommend that you use the latest version of LINE to use LINE Beacon.

<!-- tip end -->

## Prepare beacon devices 

To use LINE Beacon, you need a Bluetooth® Low Energy beacon device to link to your LINE Official Account. You can use one of the following types of devices:

- A beacon device that supports [LINE Beacon](https://developers.line.biz/en/docs/messaging-api/beacon-device-spec/). These devices are only supported in their countries.
  - Supported devices in Japan are available [here](https://beacon.theshop.jp/items/6617930).
  - Supported devices in Thailand are available [here](https://linedevth.line.me/th/tech-partner?filterTech=Beacon).
- A Bluetooth® Low Energy device that uses the [LINE Simple Beacon](https://github.com/line/line-simple-beacon) specification.

## Link beacon to LINE Official Account 

To link your LINE Official Account to a beacon, open the beacon registration page from the [LINE Official Account Manager](https://manager.line.biz/beacon/register). From the registration page, link a LINE Beacon compatible device to your LINE Official Account. You can also issue a **LINE Simple Beacon hardware ID** for the device.

<!-- note start -->

**Note**

You can link more than one beacon to a LINE Official Account. But you can link only one LINE Official Account to a beacon.

<!-- note end -->

## Receive a webhook event 

When a user who meets the following conditions enters your beacon region, your bot server receives [beacon webhook events](https://developers.line.biz/en/reference/messaging-api/#beacon-event):

- The user who have Bluetooth and the LINE Beacon settings on the user's LINE activated
- The user who added the LINE Official Account that was linked to the bot app as a friend in advance

To try to trigger a beacon webhook event:

1. Make sure that Bluetooth is activated on your smartphone.
2. Enable **Use LINE Beacon** from **Settings** > **Privacy** on LINE.
3. Make sure that the beacon device is powered on. Bring your smartphone into the beacon range.
4. See if your bot server receives a beacon event object.

Here is an example of a [beacon event object](https://developers.line.biz/en/reference/messaging-api/#beacon-event):

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "replyToken": "nHuyWiB7yP5Zw52FIkcQobQuGDXCTA",
      "type": "beacon",
      "mode": "active",
      "timestamp": 1462629479859,
      "source": {
        "type": "user",
        "userId": "U4af4980629..."
      },
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      },
      "beacon": {
        "hwid": "d41d8cd98f",
        "type": "enter"
      }
    }
  ]
}
```

## Beacon banner 

The beacon banner is a banner that appears over the user's Chats screen when your beacon detects a LINE user.

With a tap on the banner, you can let users add your LINE Official Account linked to the beacon as a friend if they haven't added the account as a friend.

When the users tap the beacon banner, the web page specified by the LINE Official Account opens. Also, you can make the users receive a message from your LINE Official Account at the very spot they tapped the banner.

<!-- note start -->

**Note**

The beacon banner is available only to corporate users. To use the beacon banner, contact your LINE representative or make an inquiry through the [LINE for Business](https://www.linebiz.com/jp-en/) website.

<!-- note end -->

![](https://developers.line.biz/media/messaging-api/using-beacons/beacon-banner_en.png)
