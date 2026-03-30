# Get user IDs

To send a message to a user with the Messaging API, you need to specify the user with a user ID. Learn how to get user IDs.

<!-- table of contents -->

## What is user ID 

User IDs are unique identifiers for users and are different from display names or the LINE ID users register to become searchable by friends. The LINE Platform issues a user ID as a string, formatted as `U[0-9a-f]{32}` (regular expression). An example of a user ID is `U8189cf6745fc0d808977bdb0b9f22995`.

![](https://developers.line.biz/media/messaging-api/getting-user-ids/display-name-and-id-and-user-id-en.png)

### Unit for issuing user IDs 

User IDs are issued different values for each provider, even for the same user. If the provider is the same, the user ID is the same regardless of the channel type (LINE Login channel or Messaging API channel).

For example, if there is a Messaging API channel and a LINE Login channel under the same provider, the user ID of the user A that you get for each channel is the same value. But, the user ID of the user A that you get for a channel under a different provider is a different value.

![](https://developers.line.biz/media/messaging-api/getting-user-ids/user-id-for-each-provider-en.png)

## Getting a user ID 

You can get user IDs by using the four methods:

1. [Developer gets their own user ID](https://developers.line.biz/en/docs/messaging-api/getting-user-ids/#get-own-user-id)
1. [Get a user ID from webhook](https://developers.line.biz/en/docs/messaging-api/getting-user-ids/#get-user-ids-in-webhook)
1. [Get user IDs of all of your friends](https://developers.line.biz/en/docs/messaging-api/getting-user-ids/#get-all-friends-user-ids)
1. [Get user IDs of group and multi-person chat members](https://developers.line.biz/en/docs/messaging-api/getting-user-ids/#get-member-user-ids)

### Developer gets their own user ID 

You can find your own user ID as a developer in **Your user ID** of the **Basic settings** tab of a channel on the [LINE Developers Console](https://developers.line.biz/console/). For more information, see [Channel roles](https://developers.line.biz/en/docs/line-developers-console/managing-roles/#roles-for-channel) in the LINE Developers Console documentation. No API is available to get your user ID as a developer.

<!-- tip start -->

**You need to link your LINE account with your Business ID**

**Your user ID** of the **Basic settings** tab won't be displayed if your Business ID isn't linked to a LINE account. The display differences based on LINE account link status are as follows:

| LINE account linked | LINE account not linked |
| --- | --- |
| ![](https://developers.line.biz/media/messaging-api/getting-user-ids/get-own-user-id-linked-line-account-en.png) | ![](https://developers.line.biz/media/messaging-api/getting-user-ids/get-own-user-id-unlinked-line-account-en.png) |

For more information on how to link your LINE account, see [Link your Business ID with your LINE account](https://developers.line.biz/en/docs/line-developers-console/login-account/#link-business-account-with-line-account) in the LINE Developers Console documentation.

<!-- tip end -->

### Get a user ID from webhook 

When a user adds your LINE Official Account as a friend or sends a message to your LINE Official Account, the LINE Platform sends the webhook to the URL (bot server) specified in the **Webhook URL** in the LINE Developers Console. The user ID is included in the webhook.

Here is an example of the [webhook event object](https://developers.line.biz/en/reference/messaging-api/#webhook-event-objects) the LINE Platform sends when a user adds a LINE Official Account as a friend:

```json
{
  "destination": "xxxxxxxxxx",
  "events": [
    {
      "type": "follow",
      "timestamp": 1462629479859,
      "source": {
        // You can get the user ID from the userId property of the source object
        "type": "user",
        "userId": "U8189cf6745fc0d808977bdb0b9f22995"
      },
      "replyToken": "nHuyWiB7yP5Zw52FIkcQobQuGDXCTA",
      "mode": "active",
      "webhookEventId": "01FZ74A0TDDPYRVKNK77XKC3ZR",
      "deliveryContext": {
        "isRedelivery": false
      }
    }
  ]
}
```

If a user gave no consent to access their user profile information, the webhook contains no user ID. For more information, see [Consent on getting user profile information](https://developers.line.biz/en/docs/messaging-api/user-consent/).

### Get user IDs of all of your friends 

You can get the user IDs of all users who added your LINE Official Account as a friend with the [Get a list of users who added your LINE Official Account as a friend](https://developers.line.biz/en/reference/messaging-api/#get-follower-ids) endpoint.

<!-- note start -->

**Note**

This feature is available only for verified or [premium accounts](https://developers.line.biz/en/glossary/#premium-account). For more information on account types, see [Account Types of LINE Official Account](https://www.linebiz.com/jp-en/service/line-official-account/account-type/) on LINE for Business.

<!-- note end -->

### Get all user IDs of group and multi-person chat members 

You can use the following endpoints to get user IDs of all members of a group or multi-person chat that your LINE Official Account is participating in:

- [Get group chat member user IDs](https://developers.line.biz/en/reference/messaging-api/#get-group-member-user-ids)
- [Get multi-person chat member user IDs](https://developers.line.biz/en/reference/messaging-api/#get-room-member-user-ids)

<!-- note start -->

**Note**

This feature is available only for verified or [premium accounts](https://developers.line.biz/en/glossary/#premium-account). For more information on account types, see [Account Types of LINE Official Account](https://www.linebiz.com/jp-en/service/line-official-account/account-type/) on LINE for Business.

<!-- note end -->

<!-- tip start -->

**You can also get user IDs from webhooks**

When a user joins or sends a message in a group or multi-person chat, a webhook is sent to the bot server. The webhook includes the user ID, so you can get the user ID without making an API request. For more information, see [Get a user ID from webhook](https://developers.line.biz/en/docs/messaging-api/getting-user-ids/#get-user-ids-in-webhook).

<!-- tip end -->

## User ID validation 

Even if you have a user ID, you can't send a message if the user ID is invalid.

To check if a user ID is valid, use the [Get profile](https://developers.line.biz/en/reference/messaging-api/#get-profile) endpoint. If the user ID is valid, the HTTP status code `200` is returned. If anything other than `200` is returned, the user ID is invalid and you can't send a message to this user.
