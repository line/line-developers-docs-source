# Mark messages as read

In LINE chats, when the recipient views a message sent by the user, a read is added to the message. When using chat feature in LINE Official Account, messages from users are not automatically marked as read. However, by using the Messaging API, you can enable chat feature while manually marking specific messages as read.

This page explains how to add read to messages sent by users via the Messaging API.

<!-- table of contents -->

## Conditions for marking messages as read in the Messaging API 

If **Chat** is turned off in the **Response settings** of the [LINE Official Account Manager](https://manager.line.biz/), messages sent by users will automatically be marked as read. To mark messages as read via the Messaging API, **Chat** must be turned on.

## How to mark messages as read using the Messaging API 

To mark messages as read that were sent by a user, follow these steps:

1. [Get the read token of the message](https://developers.line.biz/en/docs/messaging-api/mark-as-read/#get-token)
2. [Use the "Mark messages as read" endpoint](https://developers.line.biz/en/docs/messaging-api/mark-as-read/#use-endpoint)

Each step is explained below.

### 1. Get the read token of the message 

When a user sends a message to a LINE Official Account, the LINE Platform sends a webhook [message event](https://developers.line.biz/en/reference/messaging-api/#message-event) to the bot server. This event object contains the `markAsReadToken` property (read token) used to mark messages as read.

Below is an example of a message event object for a webhook. Read tokens have no expiration date.

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "type": "message",
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "message": {
        "id": "444573844083572737",
        "type": "text",
        "quoteToken": "q3Plxr4AgKd...",
        "markAsReadToken": "30yhdy232...", // Read token
        "text": "Hello, world!"
      },
      // omitted
    }
  ]
}
```

### 2. Use the "Mark messages as read" endpoint 

To mark messages as read, use the read token obtained in step 1 with the [Mark messages as read](https://developers.line.biz/en/reference/messaging-api/#mark-as-read) endpoint. You can mark all messages prior to the specified message as read by executing a request like the following:

```sh
curl -v -X POST https://api.line.me/v2/bot/chat/markAsRead \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {channel access token}' \
-d '{
  "markAsReadToken": "{mark as read token}"
}'
```
