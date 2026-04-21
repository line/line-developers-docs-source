# Technical specifications of the LINE notification messages API

<!-- note start -->

**Use of optional functions requires an application**

Only corporate users who have submitted the required applications can use the functions described in this document. To use these functions with your LINE Official Account, contact your sales representative or contact [our Sales partners](https://www.lycbiz.com/jp/partner/sales/).

<!-- note end -->

## Send LINE notification messages to users 

Based on the customer's phone number held by the company, a message request is sent to the LINE Platform server, and a LINE notification message is sent to the account of the user whose phone number is registered to LINE. Phone numbers sent by companies are hashed, and LY Corporation uses the received information only for matching the destination of message transmission, and immediately destroys it after matching. It may also be necessary to verify your identity by SMS to confirm the content of notifications including personal information, and to continue the procedure.

There are two types of LINE notification messages: LINE notification messages (template) and LINE notification messages (flexible). Each type has different API endpoints.

- LINE notification messages (template)
  - [Send a LINE notification message (template)](https://developers.line.biz/en/reference/line-notification-messages/#send-line-notification-message-template)
  - [Get number of sent LINE notification messages (template)](https://developers.line.biz/en/reference/line-notification-messages/#get-number-of-sent-line-notification-messages-template)
- LINE notification messages (flexible)
  - [Send a LINE notification message (flexible)](https://developers.line.biz/en/reference/line-notification-messages/#send-line-notification-message-flexible)
  - [Get number of sent LINE notification messages (flexible)](https://developers.line.biz/en/reference/line-notification-messages/#get-number-of-sent-line-notification-messages-flexible)

For more information, see the [LINE notification messages API reference](https://developers.line.biz/en/reference/line-notification-messages/).

### Message types that can be sent in LINE notification messages 

With LINE notification messages (template), you can easily create messages by combining premade templates, items, and buttons. When creating messages, follow the [LINE notification messages (template) UX guidelines](https://www.lycbiz.com/sites/default/files/media/jp/download/LINE_Official_Notification_Template_UXGuideline.pdf) (only available in Japanese).

![Sample of a LINE notification message (template)](https://developers.line.biz/media/line-notification-message/notification-messages-template.png)

With LINE notification messages (flexible), you can use [Flex Message](https://developers.line.biz/en/docs/messaging-api/message-types/#flex-messages) and other similar message types for more flexible message creation. However, messages containing images, videos, or audio aren't permitted. Additionally, LINE notification messages (flexible) require prior UX review, and only messages that pass the review can be sent. When creating messages, follow the [LINE notification messages (flexible) UX guidelines](https://www.lycbiz.com/sites/default/files/media/jp/download/LINE%E9%80%9A%E7%9F%A5%E3%83%A1%E3%83%83%E3%82%BB%E3%83%BC%E3%82%B8UX%E3%82%AC%E3%82%A4%E3%83%89%E3%83%A9%E3%82%A4%E3%83%B3.pdf) (only available in Japanese).

### Phone number hashing 

When specifying the destination `to` in the LINE notification messages API, specify a string that is a phone number normalized to [E.164](https://developers.line.biz/en/glossary/#e164) format, such as `+818000001234` hashed with SHA256. Don't include hyphens. Here is an example of hashing a phone number using Python3.

```python
import hashlib

phone_number = "+818000001234"
hashed_phone_number = hashlib.sha256(phone_number.encode()).hexdigest()
print(hashed_phone_number)

# d41e0ad70dddfeb68f149ad6fc61574b9c5780ab7bcb2fba5517771ffbb2409c
```

### Get message delivery notifications 

When you request the LINE notification messages API and send a LINE notification message to the user, a dedicated webhook event ([delivery completion event](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#receive-delivery-event)) will be sent from the LINE Platform.

If you specify any string in the `X-Line-Delivery-Tag` of the request header when making a request, that string will be returned in the `delivery.data` property of the webhook's [delivery completion event](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#receive-delivery-event). `X-Line-Delivery-Tag` can be used for purposes such as determining which message has been delivered when a webhook is received.

See [Webhook delivery completion event](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/) for more information.

### Get the number of sent LINE notification messages 

You can get the number of sent LINE notification messages using the following APIs:

- [Get number of sent LINE notification messages (template)](https://developers.line.biz/en/reference/line-notification-messages/#get-number-of-sent-line-notification-messages-template)
- [Get number of sent LINE notification messages (flexible)](https://developers.line.biz/en/reference/line-notification-messages/#get-number-of-sent-line-notification-messages-flexible)

<!-- note start -->

**Note**

Only the number of LINE notification messages actually sent to the user is counted in the number of messages sent. For more information on sending conditions, see [Conditions for sending LINE notification messages](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#conditions-for-sending-line-notification-messages).

<!-- note end -->

## Conditions for sending LINE notification messages 

The LINE Notification Message API sends a message to the user if all of the following conditions are met:

- The phone number you specify as the destination of a LINE notification message matches the phone number registered in the user's LINE account.
- The phone number registered in the user's LINE account is valid (the user has authenticated the phone number by SMS within a certain period of time).
- User agrees to receive LINE notification messages.
- User hasn't blocked your LINE Official Account.
- The phone number is issued in Japan, Thailand, and Taiwan, and [the phone number can be used to authenticate by phone number in the LINE app](https://help.line.me/line/smartphone/pc?lang=en&contentId=20000104).
- User agrees to LINE's Privacy Policy (revised in March 2022 or later).

For more information on setting up LINE notification messages in the LINE app, see [How to receive LINE notification messages](https://guide.line.me/ja/services/notification-message.html) (only available in Japanese) in the LINE user's guide.

## Additional information about LINE notification messages and API 

- [About the "LINE notification message received" message](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#about-recive-the-new-line-notification-message)
- [LINE notification message reception settings](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#how-to-consent-for-line-notification-messages)
- [Messages sent when you haven't consented to get LINE notification messages](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#user-has-not-given-consent-when-receive-line-notification-messages)
- [About LINE notification messages API requests for users who have blocked the LINE Official Account](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#about-pnp-api-block-response)
- [When the LINE notification messages API request is successful but the message isn't sent](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#why-i-cant-receive-line-notification-messages)
- [About adding and blocking friends when sending LINE notification messages to users who aren't friends with the LINE Official Account](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#when-user-add-or-block-oa)
- [Rich menu display when sending LINE notification messages to users who aren't friends with the LINE Official Account](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#about-richmenu-displayed)
- [For what will be billed for usage fees in the LINE notification messages API](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#about-delivered-pnp-messages)

### About the "LINE notification message received" message 

When sending a LINE notification message, the following message will be sent from the LINE Official Account (system account) named "LINE". This message is always sent each time a LINE notification message is sent. The sender of a LINE notification message can't prevent this message from being sent or reduce the number of times it's sent.

![Message received notification](https://developers.line.biz/media/line-notification-message/type1-pnpflow-3-ja.png)

<!-- note start -->

**Behavior when blocking**

If the user designated by the LINE notification messages API as the receiver of a notification message has blocked the LINE Official Account from which the message was sent, the notification message and the "LINE notification message received" message from the "LINE" system account won't be sent.

Additionally, LINE notification messages sent while the user had blocked the LINE Official Account won't be delivered even after the user unblock it.

<!-- note end -->

### LINE notification message reception settings 

When a LINE notification message is sent to users, they can consent (or refuse) to get LINE notification messages. Users can also consent (or refuse) at any time from the LINE app by going to **Settings** > **Privacy** > **Provide usage data** > **LINE notification messages**, even when no LINE notification message has been sent.

![Agree to receive LINE notification messages](https://developers.line.biz/media/line-notification-message/consent-line-notification-message-en.png)

#### States of reception settings 

There are three states for setting up the receipt of LINE notification messages.

| State | Description |
| --- | --- |
| Agree (on) | Consented to receive. LINE notification messages will be sent. |
| Reject (off) | Refused to receive. LINE notification messages won't be sent. |
| Not set | Neither consented nor refused yet. When getting a LINE notification message, a message will be sent asking for consent to get LINE notification messages.<ul><li>If you created a new LINE account in the LINE app version 8.0.0 or earlier, your consent to get LINE notification messages will be "not set".</li><li>If you change the status to anything other than "not set" even once, you can't return to the "not set" state.</li></ul> |

### Messages sent when you haven't consented to get LINE notification messages 

| State | Description |
| --- | --- |
| Reject (off) | The requested LINE notification message won't be sent and will be deleted. |
| Not set | If you agree to get LINE notification messages within 24 hours after receiving the [setting to get LINE notification messages](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-1), the message will be sent. If you don't give your consent to get LINE notification messages within 24 hours, the requested message won't be sent and will be deleted. |

### About LINE notification messages API requests for users who have blocked the LINE Official Account 

If a request is made to send a LINE notification message via the LINE notification messages API to a user who has blocked the LINE Official Account, a response with the HTTP status code `200` or `202` will be returned. However, in this case, the LINE notification message isn't actually sent, and the [Webhook delivery completion event](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/) isn't sent.

### When the LINE notification messages API request is successful but the message isn't sent 

If you have successfully requested a LINE notification messages API (received HTTP status code `200` or `202`) to a user who didn't block the LINE Official Account, but the LINE notification message isn't actually sent to the user, these reasons may be why:

- The user associated with the phone number specified when requesting the LINE notification messages API has not set the [setting to get LINE notification messages](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-1), and when the setting for getting LINE notification messages was received, it was changed to "reject".
- The user associated with the phone number specified when requesting the LINE notification messages API has not set the [setting to get LINE notification messages](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-1), and when the setting for getting LINE notification messages was received, it was left unconfigured.
- SMS authentication is required for the user associated with the phone number specified when requesting the LINE notification messages API, but the user didn't perform SMS authentication when the [phone number authentication](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-3) message was received.

### About adding and blocking friends when sending LINE notification messages to users who aren't friends with the LINE Official Account 

If a user who isn't friends with the LINE Official Account of the sender of the LINE notification message gets a LINE notification message, they can choose whether or not to add the LINE official account as a friend. A [follow event](https://developers.line.biz/en/reference/messaging-api/#follow-event) is sent when you add a friend. An [unfollow event](https://developers.line.biz/en/reference/messaging-api/#unfollow-event) is sent if you block. When using LINE notification messages, unfollow events may be sent from users who have never received follow events.

### Rich menu display when sending LINE notification messages to users who aren't friends with the LINE Official Account 

Users who receive a LINE notification message can open a one-on-one chat and use the rich menu without adding the LINE Official Account as a friend. The default rich menu, which is set either in the [LINE Official Account Manager](https://developers.line.biz/en/docs/messaging-api/rich-menus-overview/#creating-a-rich-menu-with-the-line-manager) or with the [Messaging API](https://developers.line.biz/en/docs/messaging-api/using-rich-menus/#set-the-default-rich-menu) will be displayed. However, the [per-user rich menu](https://developers.line.biz/en/reference/messaging-api/#link-rich-menu-to-user) set with the Messaging API for users who aren't adding the LINE Official Account as a friend won't be displayed.

![Users can access the rich menu without adding the LINE Official Account as a friend](https://developers.line.biz/media/line-notification-message/about-richmenu-displayed.png)

Users who receive a LINE notification message can also send messages to the LINE Official Account without adding it as a friend. Therefore, you may receive a [postback event](https://developers.line.biz/en/reference/messaging-api/#postback-event) or a [message event](https://developers.line.biz/en/reference/messaging-api/#message-event) from a user who isn't your LINE Official Account's friend via webhooks.

### What is billed for LINE notification messages usage fees 

Only messages **actually sent to the user** will be billed for LINE notification messages usage fees.

You can check the number of messages actually sent to the user by using the API. For more information, see [Get the number of sent LINE notification messages](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#get-number-of-sent-line-notification-messages).
