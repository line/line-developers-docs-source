# Receive messages (webhook)

Every time a user adds your LINE Official Account as a friend or sends it a message, the LINE Platform sends an HTTP POST request with a webhook event object to the webhook URL (bot server) you register in the [LINE Developers Console](https://developers.line.biz/console/).

Make sure that your bot server processes the webhook event objects properly. The LINE Platform may suspend sending webhooks to your bot server if your bot server fails to receive webhooks for a long time.

<!-- warning start -->

**Security warning**

Your bot server may receive HTTP POST requests from sources other than the LINE Platform, and such requests can be malicious. Be sure to [verify the signature](https://developers.line.biz/en/docs/messaging-api/receiving-messages/#verify-signature) before processing webhook event objects.

<!-- warning end -->

<!-- tip start -->

**We recommend processing events asynchronously**

We recommend that you process webhook events asynchronously. This is to prevent subsequent requests to wait until the current request is processed.

<!-- tip end -->

## Verify signature 

When the bot server receives a webhook event, verify the signature included in the request header before processing the [webhook event objects](https://developers.line.biz/en/reference/messaging-api/#webhook-event-objects). This verification step is important to confirm that the webhook came from the LINE Platform and wasn’t tampered with during transmission.

For more information, see [Verify webhook signature](https://developers.line.biz/en/docs/messaging-api/verify-webhook-signature/).

## Webhook event types 

You can control how your bot reacts based on the data in the webhook event object. You can also make your bot act on something or respond to users. You can get webhook events for [chats](https://developers.line.biz/en/docs/messaging-api/receiving-messages/#webhook-event-in-one-on-one-talk-or-group-chat) and [beacon and account links](https://developers.line.biz/en/docs/messaging-api/receiving-messages/#other-webhook-events). For more information, see [Webhook Event Objects](https://developers.line.biz/en/reference/messaging-api/#webhook-event-objects) in the Messaging API reference.

### Webhook events for chats 

The webhook events that your bot server receives in one-on-one chats or [group chats and multi-person chats](https://developers.line.biz/en/docs/messaging-api/group-chats/) are as follows:

| Webhook event | Receive when | one-on-one chats | Group chats and multi-person chats |
| --- | --- | --- | --- |
| [Message event](https://developers.line.biz/en/reference/messaging-api/#message-event) | When a user sends a message. You can reply to this event. | ✅ | ✅ |
| [Unsend event](https://developers.line.biz/en/reference/messaging-api/#unsend-event) | When a user unsends a message. For more information on handling this event, see [Processing on receipt of unsend event](https://developers.line.biz/en/docs/messaging-api/receiving-messages/#webhook-unsend-message). | ✅ | ✅ |
| [Follow event](https://developers.line.biz/en/reference/messaging-api/#follow-event) | When a user adds your LINE Official Account as a friend, or unblocks your LINE Official Account. You can reply to this event. | ✅ | ❌ |
| [Unfollow event](https://developers.line.biz/en/reference/messaging-api/#unfollow-event) | When a user blocks your LINE Official Account | ✅ | ❌ |
| [Join event](https://developers.line.biz/en/reference/messaging-api/#join-event) | When your LINE Official Account joins a group chat or multi-person chat. You can reply to this event. | ❌ | ✅ |
| [Leave event](https://developers.line.biz/en/reference/messaging-api/#leave-event) | When a user deletes your LINE Official Account or your LINE Official Account leaves, from a group chat or multi-person chat | ❌ | ✅ |
| [Member join event](https://developers.line.biz/en/reference/messaging-api/#member-joined-event) | When a user joins a group chat or multi-person chat that your LINE Official Account is a member of. You can reply to this event. | ❌ | ✅ |
| [Member leave event](https://developers.line.biz/en/reference/messaging-api/#member-left-event) | When a user leaves a group chat or multi-person chat that your LINE Official Account is a member of | ❌ | ✅ |
| [Postback event](https://developers.line.biz/en/reference/messaging-api/#postback-event) | When a user triggers a [postback action](https://developers.line.biz/en/reference/messaging-api/#postback-action). You can reply to this event. | ✅ | ✅ |
| [Video viewing complete event](https://developers.line.biz/en/reference/messaging-api/#video-viewing-complete) | When a user finishes watching a video message that has a `trackingId` specified sent from the LINE Official Account. You can reply to this event. | ✅ | ❌ |

✅ Your bot server receives this event&nbsp;&nbsp;&nbsp;&nbsp;❌ Your bot server doesn't receive this event

#### Webhook when sending a message using liff.sendMessages() 

Users can't send a [template message](https://developers.line.biz/en/reference/messaging-api/#template-messages) or a [Flex Message](https://developers.line.biz/en/reference/messaging-api/#flex-message) from the LINE app. However, developers can use [`liff.sendMessages()`](https://developers.line.biz/en/reference/liff/#send-messages) to send messages on behalf of the users to the currently open chat screens where the LINE MINI Apps or LIFF apps are open.

When a template message or a Flex Message is sent from the user using `liff.sendMessages()`, no webhook is sent from the LINE Platform. For all other [message types](https://developers.line.biz/en/docs/messaging-api/message-types/), a webhook is sent.

#### Receive quote messages sent by users via webhook 

When a user sends a message quoting a past message, you can check the ID of the quoted message in the `quotedMessageId` property included in the `message` property of the webhook. In this case, you can check the ID of the quoted message, but you can't retrieve the content of the message (such as text or stickers).

![](https://developers.line.biz/media/messaging-api/receiving-messages/chat-reply.png)

Here is an example of a webhook that arrives at your bot server when a user sends a message quoting a past message.

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "type": "message",
      "message": {
        "type": "text",
        "id": "468789577898262530", // ID of the sent message
        "quotedMessageId": "468789532432007169", // ID of the quoted message
        "quoteToken": "q3Plxr4AgKd...",
        "text": "Chicken, please." // Text of the sent message
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

For more information about the `quotedMessageId` property, see [text](https://developers.line.biz/en/reference/messaging-api/#wh-text) and [sticker](https://developers.line.biz/en/reference/messaging-api/#wh-sticker) of the [Message event](https://developers.line.biz/en/reference/messaging-api/#message-event) in the Messaging API reference.

For more information about how users can send quote messages, see [Using the chat reply feature](https://guide.line.me/ja/friends-and-groups/create-groups.html) (only available in Japanese) in the LINE user's guide.

#### Webhook when a message including a mention to a bot is sent 

If a message sent by a user mentions your bot, the following values will be set in the text message object in the webhook event sent to the bot server:

- `mention.mentionees[].type` will be set to `user`.
- `mention.mentionees[].userId` will be set to the user ID of the bot.
- `mention.mentionees[].isSelf` is set to `true`.

For example, a webhook event object containing the following message event will be sent to the bot server:

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
        "userId": "{user ID of the bot}",
        "type": "user",
        "isSelf": true
      }
    ]
  }
}
```

You can check the user ID of the bot in the `destination` property in the [request body of the webhook](https://developers.line.biz/en/reference/messaging-api/#request-body) and in the `userId` property which can be obtained using the [Get bot info](https://developers.line.biz/en/reference/messaging-api/#get-bot-info) endpoint.

### Other webhook events 

Webhook events are also available for beacon and account linking as follows:

| Webhook event | Receive when |
| --- | --- |
| [Beacon event](https://developers.line.biz/en/reference/messaging-api/#beacon-event) | When a user enters the reception range of a Beacon. You can reply to this event. For more information, see [Use beacons with LINE](https://developers.line.biz/en/docs/messaging-api/using-beacons/). |
| [Account link event](https://developers.line.biz/en/reference/messaging-api/#account-link-event) | When a user links their LINE account with their account of your service (as a provider). You can reply to this event. For more information, see [User account linking](https://developers.line.biz/en/docs/messaging-api/linking-accounts/). |

## Processing on receipt of unsend event 

Users can unsend a message for a limited time after sending it.

When a user unsends a sent message, an [unsend event](https://developers.line.biz/en/reference/messaging-api/#unsend-event) is sent to the bot server. When the unsend event is received, we recommend that service providers respect the user's intent to unsend a sent message and handle the message appropriately with the utmost care so that the target message can't be seen or used in the future.

For example, you should handle a message that a user has unsent as follows:

- Cancel the target message displayed on your own management screen, etc.
- Delete the target message stored in a database or other storage device.

For more information about how to unsend a sent message in the LINE app, see [Using the unsend message function](https://guide.line.me/ja/chats-calls-notifications/chats/chat-delete.html) (only available in Japanese) in the LINE user's guide.

## Redeliver a webhook that failed to be received 

The Messaging API provides a feature to redeliver webhooks that your bot server fails to receive. Even if your bot server fails to respond normally to a webhook due to temporary over-access or other reasons, the webhook will be redelivered from the LINE Platform for a certain period of time, so your bot server can receive the webhook after recovery.

Webhook redelivery is available for all Messaging API channels.

<!-- note start -->

**Check before enabling webhook redelivery**

- The same webhook event may be sent to your bot server more than once by different reasons such as network routing problem. To detect duplicates, use `webhookEventId` in the webhook event object.
- If the LINE Platform redelivers webhooks, the order of webhook events you receive can be different from the order the events occurred. If this is a problem, check the `timestamp` of webhook event objects to confirm the context.

<!-- note end -->

### Redelivered webhooks 

The content of a redelivered [webhook event object](https://developers.line.biz/en/reference/messaging-api/#webhook-event-objects) is the same as the original webhook event object, except for the value of `deliveryContext.isRedelivery`. Values such as webhook event ID and reply token remain unchanged.

The reply token included in a redelivered webhook event object can be used except in certain cases. For more information on reply tokens, see [Reply token](https://developers.line.biz/en/reference/messaging-api/#send-reply-message-reply-token) in the Messaging API reference.

### Enable webhook redelivery 

By default, webhook redelivery is disabled. To enable webhook redelivery:

1. Open the channel settings screen from the [LINE Developers Console](https://developers.line.biz/console/).
1. Click the **Messaging API** tab.
1. Enable **Use webhook**.
1. Enable **Webhook redelivery**.

When you enable **Webhook redelivery**, a note on webhook redelivery is displayed for you to reference. Read and understand the note before enabling.

![](https://developers.line.biz/media/messaging-api/receiving-messages/enable-webhook-redelivery-en.png)

### Conditions for webhook redelivery 

The LINE Platform sends failed webhooks again if these conditions are met, for a pre-defined number of times with a time interval:

- [Webhook redelivery is enabled](https://developers.line.biz/en/docs/messaging-api/receiving-messages/#enable-webhook-redelivery).
- The bot server didn't return `2xx` status code for the webhook.

The number and interval of the webhook redelivery aren't disclosed. In addition, the number and interval are subject to change without notice.

<!-- note start -->

**May not be able to redeliver webhooks**

Be aware that webhook redelivery doesn't guarantee that webhooks will be reliably delivered. In addition, if the number of webhook redeliveries suddenly increases and is determined to affect the operation of the LINE Platform, webhook redelivery may be forced to be disabled.

<!-- note end -->

## Check the cause of the webhook errors 

The Messaging API provides a feature to check error causes and statistics when sending webhooks. This is useful for understanding the status of sending webhooks when a webhook wasn't received due to a problem on the bot server, etc.

For more information, see [Check webhook error causes and statistics](https://developers.line.biz/en/docs/messaging-api/check-webhook-error-statistics/).

## Get user-sent content with webhook 

You can get content sent by users with a message ID in the [webhook](https://developers.line.biz/en/reference/messaging-api/#webhooks). The types of content that can be retrieved are as follows:

- [Images, videos, audio, files](https://developers.line.biz/en/docs/messaging-api/receiving-messages/#getting-content-file-sent-by-users)
- [Preview image of the image or video](https://developers.line.biz/en/docs/messaging-api/receiving-messages/#getting-content-preview-image)

<!-- note start -->

**Note**

- Content that users send is automatically deleted after a certain period of time.
- You can get the text that users sent through the [text](https://developers.line.biz/en/reference/messaging-api/#wh-text) message object of the webhook. There is no API available to get the text again after receiving the webhook.

<!-- note end -->

### Get images, videos, audio, and files 

You can get [images](https://developers.line.biz/en/reference/messaging-api/#wh-image), [videos](https://developers.line.biz/en/reference/messaging-api/#wh-video), [audio](https://developers.line.biz/en/reference/messaging-api/#wh-audio), and [files](https://developers.line.biz/en/reference/messaging-api/#wh-file) that users send, with a message ID in webhook.

Example request

```sh
curl -v -X GET https://api-data.line.me/v2/bot/message/{messageId}/content \
-H 'Authorization: Bearer {channel access token}'
```

For more information, see [Get content](https://developers.line.biz/en/reference/messaging-api/#get-content) in the Messaging API reference.

### Get a preview image of the image or video 

You can get a preview image of the image or video sent by users with a message ID in the webhook.

Example request

```sh
curl -v -X GET https://api-data.line.me/v2/bot/message/{messageId}/content/preview \
-H 'Authorization: Bearer {channel access token}'
```

The preview image is image data converted to a smaller data size than the original content.

For example, a preview image can be used as a thumbnail. When building a site like a CRM, you can display thumbnails while downloading large images or videos. This allows users to quickly assess the content overview, improving the system's user experience.

For more information, see [Get a preview image of the image or video](https://developers.line.biz/en/reference/messaging-api/#get-image-or-video-preview) in the Messaging API reference.

## Get user profile 

You can get a user's LINE profile (user's display name, user ID, profile image URL, status message, etc.) with the user's ID contained in a [webhook](https://developers.line.biz/en/reference/messaging-api/#webhooks).

Example request

```sh
curl -v -X GET https://api.line.me/v2/bot/profile/{userId} \
-H 'Authorization: Bearer {channel access token}'
```

If successful, a JSON object is returned.

```json
{
  "displayName": "LINE Botto",
  "userId": "U4af4980629...",
  "pictureUrl": "https://profile.line-scdn.net/ch/v2/p/uf9da5ee2b...",
  "statusMessage": "Hello world!"
}
```

For more information, see [Get profile](https://developers.line.biz/en/reference/messaging-api/#get-profile) in the Messaging API reference.
