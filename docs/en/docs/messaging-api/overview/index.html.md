# Messaging API overview

Use the Messaging API to build bots to provide personalized experiences on LINE to your users.

<!-- tip start -->

**What is LINE Official Account**

If you are unfamiliar with LINE Official Account, visit the comprehensive learning platform, [LINE Campus](https://lymcampus.jp/) (only available in Japanese).

<!-- tip end -->

## How the Messaging API works 

With the Messaging API, a bot server can send and receive data to and from the LINE Platform. Requests are sent over HTTPS in JSON. The communication flow between a bot server and the LINE Platform is as follows:

1. A user sends a message to a LINE Official Account.
1. The LINE Platform sends a webhook event to the webhook URL of the bot server.
1. The bot server checks the webhook event and responds to the user through the LINE Platform.

![](https://developers.line.biz/media/messaging-api/overview/messaging-api-architecture.png)

## Try the demo 

The [LINE API Use Case](https://lineapiusecase.com/en/top.html) site lets you try LINE Official Accounts and features that are implemented with the Messaging API. You can also see the code for the demo samples. Add different LINE Official Accounts from the site, as a friend on your smartphone and experience the Messaging API. For more information, see [Chatbot (Messaging API)](https://lineapiusecase.com/en/api/msgapi.html).

## What you can do with the Messaging API 

Here are the things you can do with the Messaging API.

### Send reply messages 

With the Messaging API, you can send reply messages to users who added your LINE Official Account as a friend. For more information, see [Sending messages](https://developers.line.biz/en/docs/messaging-api/sending-messages/).

### Send messages at any time 

With the Messaging API, you can send messages directly to users at all times. For more information, see [Sending messages](https://developers.line.biz/en/docs/messaging-api/sending-messages/).

### Send different message types 

With the Messaging API, you can send different types of messages to users as listed below. For more information about the specification of these messages, see [Message types](https://developers.line.biz/en/docs/messaging-api/message-types/).

- [Text message](https://developers.line.biz/en/docs/messaging-api/message-types/#text-messages)
- [Text message (v2)](https://developers.line.biz/en/docs/messaging-api/message-types/#text-messages-v2)
- [Sticker message](https://developers.line.biz/en/docs/messaging-api/message-types/#sticker-messages)
- [Image message](https://developers.line.biz/en/docs/messaging-api/message-types/#image-messages)
- [Video message](https://developers.line.biz/en/docs/messaging-api/message-types/#video-messages)
- [Audio message](https://developers.line.biz/en/docs/messaging-api/message-types/#audio-messages)
- [Location message](https://developers.line.biz/en/docs/messaging-api/message-types/#location-messages)
- [Coupon message](https://developers.line.biz/en/docs/messaging-api/message-types/#coupon-messages)
- [Imagemap message](https://developers.line.biz/en/docs/messaging-api/message-types/#imagemap-messages)
- [Template message](https://developers.line.biz/en/docs/messaging-api/message-types/#template-messages)
- [Flex Message](https://developers.line.biz/en/docs/messaging-api/message-types/#flex-messages)

### Get content sent by users 

With the Messaging API, you can get images, videos, audio, and files sent by users. Content that users send is automatically deleted after a period of time. For more information, see [Get content](https://developers.line.biz/en/reference/messaging-api/#get-content) in the Messaging API reference.

### Get user profiles 

With the Messaging API, you can get profile information of a user who interacts with your LINE Official Account, in one-on-one and group chats. The types of profile information you can get are user's display name, language, profile image and status message. For more information, see [Get profile](https://developers.line.biz/en/reference/messaging-api/#get-profile) in the Messaging API reference.

### Join group chats 

With the Messaging API, you can send messages in group chats and get information of the group chat members. For more information, see [Group chats and multi-person chats](https://developers.line.biz/en/docs/messaging-api/group-chats/).

### Use rich menus 

With the Messaging API, you can set and customize a rich menu in a chat. Rich menus help users find how they can interact with your LINE Official Account. Users can use this menu from the chat at all times. For more information, see [Use rich menus](https://developers.line.biz/en/docs/messaging-api/using-rich-menus/).

### Use beacons 

With LINE Beacon, you can set your LINE Official Account to interact with the user who enters a beacon region. For more information, see [Use beacons with LINE](https://developers.line.biz/en/docs/messaging-api/using-beacons/).

### Use account link 

With the Messaging API, you can securely link user accounts in your service to their LINE accounts, if they friended your LINE Official Account. For more information, see [User account linking](https://developers.line.biz/en/docs/messaging-api/linking-accounts/).

### Get the number of sent messages 

With the Messaging API, you can get the number of messages you sent from your LINE Official Account. The API returns only the number of messages sent through the Messaging API, not LINE Official Account Manager. For more information, see the following references:

- [Get the target limit for sending messages this month](https://developers.line.biz/en/reference/messaging-api/#get-quota)
- [Get number of messages sent this month](https://developers.line.biz/en/reference/messaging-api/#get-consumption)
- [Get number of sent reply messages](https://developers.line.biz/en/reference/messaging-api/#get-number-of-reply-messages)
- [Get number of sent push messages](https://developers.line.biz/en/reference/messaging-api/#get-number-of-push-messages)
- [Get number of sent multicast messages](https://developers.line.biz/en/reference/messaging-api/#get-number-of-multicast-messages)
- [Get number of sent broadcast messages](https://developers.line.biz/en/reference/messaging-api/#get-number-of-broadcast-messages)

## Messaging API pricing 

You can get started with the Messaging API for free. Anyone can use the Messaging API to send a message from a LINE Official Account.

You can send a certain number of messages each month for free. The number of free messages depends on the [subscription plan](https://www.lycbiz.com/jp/service/line-official-account/plan/) (only available in Japanese) of your LINE Official Account. The subscription plan may vary by country or region. See your region's subscription plan for more information.

For more information on Messaging API pricing, see [Messaging API pricing](https://developers.line.biz/en/docs/messaging-api/pricing/).

## Next steps 

As the next step, [get started with the Messaging API](https://developers.line.biz/en/docs/messaging-api/getting-started/) to create a bot. First, create a LINE Official Account. Once you've created a LINE Official Account, you can create a Messaging API channel for that LINE Official Account.

## Learn more 

- [Messaging API development guidelines](https://developers.line.biz/en/docs/messaging-api/development-guidelines/)
- [LINE Messaging API SDKs](https://developers.line.biz/en/docs/messaging-api/line-bot-sdk/)
- [Messaging API reference](https://developers.line.biz/en/reference/messaging-api/)
