# Notice for corporate customers

Notice for corporate customers. See also the [News](https://developers.line.biz/en/news/).

2026/02/19

## Changes to some error responses in the Mission stickers API 

We've modified the content of certain error responses in the [Provide mission stickers to the users](https://developers.line.biz/en/reference/partner-docs/#send-mission-stickers-v3) endpoint of the Mission stickers API to prevent the inference of user attribute information.

For more information, see the [Error messages](https://developers.line.biz/en/reference/partner-docs/#send-mission-stickers-v3-error-messages) section of the provide mission stickers to the users endpoint.

2025/06/30

## The subject and body of the emails sent for error notifications have changed 

As of June 30, 2025, we updated the subject and body of emails sent for webhook error notifications.

For more information, see [Notification email example](https://developers.line.biz/en/docs/partner-docs/error-notification/#sample-mail).

2025/06/18

## LINE notification messages are now displayed as “Important notification” 

LINE notification messages are now displayed with “Important notification” to the right of the LINE Official Account icon to distinguish them from other messages.

![LINE notification messages are displayed with “Important notification” to the right of the icon](https://developers.line.biz/media/line-notification-message/notification-messages-important-en.jpg)

For more information, see [Difference in appearance from other messages](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/overview/#difference-from-other-messages) in the LINE notification messages documentation.

2025/06/18

## We've changed the endpoint name of the Mission stickers API 

To improve clarity, we've renamed the "Send mission stickers (v3)" endpoint of the Mission stickers API. There are no changes to its functionality.

| Name before change         | Name after change (current)           |
| -------------------------- | ------------------------------------- |
| Send mission stickers (v3) | Provide mission stickers to the users |

For more information, see [Mission stickers API](https://developers.line.biz/en/reference/partner-docs/#mission-stickers) in the options for corporate customers API reference.

2025/06/02

## LINE notification messages (template) now available 

A new feature called "[LINE notification messages (template)](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/template/)" has been added, allowing you to easily create messages by combining premade templates, items, etc.

Consequently, the previous "LINE notification messages" that required UX review have been renamed "LINE notification messages (flexible)".

For more information, see the [LINE notification messages overview](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/overview/).

2025/01/28

## Source property in the webhook event of LINE notification messages has been removed 

As announced on [August 9, 2024](https://developers.line.biz/en/docs/partner-docs/notice/#partner-news-20240809), as of January 28, 2025, the `source` property in the [Webhook delivery completion event](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#receive-delivery-event) of LINE notification messages has been removed.

Until now, when you request the LINE notification messages API and the delivery of a LINE notification message to a user is completed, the following webhook event was sent from the LINE Platform to the bot server:

```json
{
  "destination": "Uc7472b39e21dab71c2347e02714630d6",
  "events": [
    {
      "type": "delivery",
      "delivery": {
        "data": "68df277462529930889fab80ecffdc0883906320591df93c25efc08300410fc2"
      },
      "webhookEventId": "01G17DAF0QJ7A3ERC5EJ9MAMH8",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1650590038721,
      // The following source property has been removed
      "source": {
        "type": "user",
        "userId": "U8189cf6745fc0d808977bdb0b9f22995"
      },
      "mode": "active"
    }
  ]
}
```

The `source` property in the above webhook event has been removed as of January 28, 2025.

We'll continue to work to further improve its service to our customers. Thank you for your understanding.

2024/10/18

## Add Quick-fill docs 

Quick-fill is a feature that automatically fills in the necessary profile information by tapping the **Auto-fill** button on the LINE MINI App. You can easily use the Common Profile information that a user has set in the Account Center in the LINE MINI App.

![](https://developers.line.biz/media/line-mini-app/quick-fill/quick-fill-3-steps.png)

By integrating Quick-fill into your LINE MINI App, users can automatically enter an address or phone number with a single tap. For example, when making a reservation at a restaurant or ordering from an online store, users can save themselves the hassle of entering the information manually.

Only certain corporate customers who have been contacted by us can use the Quick-fill feature.

For more information on how to integrate Quick-fill with your LINE MINI App, see [Overview of Quick-fill](https://developers.line.biz/en/docs/partner-docs/quick-fill/overview/).

2024/08/09

## As of January 28, 2025, source property in the webhook event of LINE notification messages will be removed 

As of January 28, 2025, the `source` property in the [Webhook delivery completion event](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#receive-delivery-event) of LINE notification messages will be removed.

When you request the LINE notification messages API and the delivery of a LINE notification message to a user is completed, the following webhook event will be sent from the LINE Platform to the bot server:

```json
{
  "destination": "Uc7472b39e21dab71c2347e02714630d6",
  "events": [
    {
      "type": "delivery",
      "delivery": {
        "data": "68df277462529930889fab80ecffdc0883906320591df93c25efc08300410fc2"
      },
      "webhookEventId": "01G17DAF0QJ7A3ERC5EJ9MAMH8",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1650590038721,
      // The following source property will be removed
      "source": {
        "type": "user",
        "userId": "U8189cf6745fc0d808977bdb0b9f22995"
      },
      "mode": "active"
    }
  ]
}
```

The `source` property in the above webhook event will be removed as of January 28, 2025. The date and time of property removal may change without notice.

We'll continue to work to further improve its service to our customers. Thank you for your understanding.

2024/05/07

## Module maintenance notice 

Maintenance is scheduled for June 5, 2024 around 2:00 - around 3:00 (UTC+9) on the module. For more information, see the news from May 7, 2024, [Maintenance notice for Messaging API, module, and LINE Developers Console](https://developers.line.biz/en/news/2024/05/07/maintenance-notice/).

2024/04/26

## Notification email is now be sent when webhook redelivery stopped 

In [error notification](https://developers.line.biz/en/docs/partner-docs/error-notification/) feature of the Messaging API, a notification email is now sent when webhook redelivery stopped.

If you've [enabled webhook redelivery](https://developers.line.biz/en/docs/messaging-api/receiving-messages/#enable-webhook-redelivery) in the Messaging API channel settings, the LINE Platform will redeliver the webhook that your bot server failed to receive. However, if there's no response from your server even after a certain period of time of redelivery, the LINE Platform will stop redelivery.

Previously, when an error has been detected, the LINE Platform sent an error notification email only once. With this change, a notification email will be sent both when the webhook redelivery is started and stopped.

For more information, see [When the LINE Platform stopped webhook redelivery](https://developers.line.biz/en/docs/partner-docs/error-notification/#webhook-redelivery-stopped).

2023/11/01

## As of October 31, 2023, the audience match API has been discontinued 

As announced on [July 18, 2023](https://developers.line.biz/en/docs/partner-docs/notice/#partner-news-20230718), we've discontinued the audience match API as of October 31, 2023.

LY Corporation will continue to improve the quality of its services for its customers. Thank you for your understanding.

2023/08/31

## Stateless channel access token released 

Stateless channel tokens are channel tokens that are only valid for 15 minutes. There is no limit to the number of stateless channel access tokens that can be issued. Stateless channel access tokens can be used, for example, when using Messaging API channels or module channels.

For more information about stateless channel access tokens, see the news from August 31, 2023, [Stateless channel access token released](https://developers.line.biz/en/news/2023/08/31/stateless-channel-access-token/).

2023/07/18

## As of October 31, 2023, the feature for sending messages using phone number will be discontinued 

As of October 31, 2023, the feature for sending messages using phone number of the audience match API will no longer be available. The audience match API will also be discontinued.

Related documentation and API references will be deleted without notice after the discontinuation.

### Target endpoints 

With the discontinuation, the following endpoints will also be gradually discontinued:

- [Send a message using phone number](https://developers.line.biz/en/reference/partner-docs/#phone-audience-match)
- [Get result of message delivery using phone number](https://developers.line.biz/en/reference/partner-docs/#get-phone-audience-match)

### Scheduled date of discontinuation 

October 31, 2023

The date is subject to change without notice.

LINE will continue to improve the quality of its services for its customers. Thank you for your understanding.

2023/05/31

## The Send mission stickers (v2) endpoint has been discontinued 

As announced on [February 2, 2023](https://developers.line.biz/en/docs/partner-docs/notice/#partner-news-20230202), we've discontinued the Send mission stickers (v2) endpoint as of May 31, 2023. From now on, use the [Send mission stickers (v3)](https://developers.line.biz/en/reference/partner-docs/#send-mission-stickers-v3) endpoint.

2023/04/11

## Module maintenance notice 

Maintenance is scheduled for May 11, 2023 around 2:00 - around 3:00 (UTC+9) on the module. For more information, see the news from April 11, 2023, [Maintenance notice for Messaging API, module, and LINE Developers Console](https://developers.line.biz/en/news/2023/04/11/messaging-api-module-and-console-maintenance/).

2023/02/20

## We've changed the name of the Mark-as-Read API to "Mark as read API" 

We've changed the name of the Mark-as-Read API to "Mark as read API". There is no change in features.

| Language | Name before change | Name after change |
| -------- | ------------------ | ----------------- |
| Japanese | Mark-as-Read API   | 既読API           |
| English  | Mark-as-Read API   | Mark as read API  |

For more information on the Mark as read API, see [Mark as read API](https://developers.line.biz/en/docs/partner-docs/mark-as-read/).

2023/02/02

## The Send mission stickers (v2) endpoint will be discontinued on May 31, 2023 

We'll discontinue the Send mission stickers (v2) endpoint on May 31, 2023. After the discontinuation, use the [Send mission stickers (v3)](https://developers.line.biz/en/reference/partner-docs/#send-mission-stickers-v3) endpoint.

Related documentation and API references will be deleted without notice after the discontinuation.

2022/12/20

## Notification of changes to how the Module reference is provided 

The Module reference, which was previously provided as PDF files, will now be provided as documentation on the LINE Developers site. Refer to the [documentation](https://developers.line.biz/en/docs/partner-docs/#module) and [API reference](https://developers.line.biz/en/reference/partner-docs/#module) on Module from now on.

2022/09/28

## Information on "Feature for getting statistics per aggregation unit" 

"[Feature for getting statistics per aggregation unit](https://developers.line.biz/en/docs/messaging-api/unit-based-statistics-aggregation/)" has been integrated into Messaging API.

For more information, see the news from September 28, 2022, ["Feature for getting statistics per aggregation unit" is now available in the Messaging API](https://developers.line.biz/en/news/2022/09/28/messaging-api-updated/).

2022/08/23

## LINE API Policy Handbook released 

LINE API Policy Handbook is now available. This handbook is a document related to the [LINE Official Account Terms of Use](https://terms2.line.me/official_account_terms_jp?country=JP&lang=en) and [LINE Official Account API Terms of Use](https://terms2.line.me/official_account_api_terms_jp?lang=ja&country=JP) (only available in Japanese), and is intended to help you better understand and properly use the LINE API.

For more information, see [LINE API Policy Handbook](https://developers.line.biz/en/docs/partner-docs/api-policy-handbook/).

2022/06/28

## The documentation for the LINE notification messages released 

LINE notification messages is a service that enables you to send messages to users by specifying their phone numbers, even if you don't know their [User IDs](https://developers.line.biz/en/glossary/#user-id). Even if a user hasn't added your LINE Official Account as a friend, you can send the user messages from your LINE Official Account.

In addition to the previously released overview of LINE notification messages, documentation such as [Technical Specifications of the LINE notification messages API](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/) (Only available in Japanese) and [LINE notification messages API Reference](https://developers.line.biz/en/reference/line-notification-messages/) (Only available in Japanese) has been released.

For more information about the LINE notification messages, see [LINE notification messages overview](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/overview/).

2022/03/24

## The documentation for the module released 

By using the module, advanced features using the Messaging API can be easily added to LINE Official Account that don't use the Messaging API channel. The documentation for this module is now available. For more information about the module, see [Module](https://developers.line.biz/en/docs/partner-docs/module/).

2022/01/05

## Sending messages using IFA discontinued 

As announced on [December 1, 2021](https://developers.line.biz/en/docs/partner-docs/notice/#partner-news-20211201), sending messages using the IFA (Identifier for Advertisers) of the audience match API is scheduled to be discontinued at the end of December 2021.

LINE will continue to improve the quality of its services for its customers. Thank you for your understanding.

2021/12/06

## Notification of changes to how the LINE Bot Development Guidelines are provided 

The LINE Bot Development Guidelines, which were previously provided as PDF files, will now be provided as documentation on the LINE Developers site. In addition, the name of the guidelines has been changed to [Development guidelines for corporate customers](https://developers.line.biz/en/docs/partner-docs/development-guidelines/). Refer to this documentation from now on.

2021/12/01

## Sending messages using IFA discontinued 

As of December 31, 2021, sending messages using the IFA (Identifier for Advertisers) of the audience match API will no longer be available.

Related documentation and API references will be deleted without notice after the discontinuation.

### Target endpoints 

With the discontinuation, the following endpoints will also be gradually discontinued:

- Send a message using mobile advertising ID
- Get message delivery result using mobile advertising ID

### Scheduled date of discontinuation 

December 31, 2021

The date is subject to change without notice.

LINE will continue to improve the quality of its services for its customers. Thank you for your understanding.

2021/07/09

## Corrections to the "Get statistics per aggregation unit" document 

In the API reference for "[Get statistics per aggregation unit](https://developers.line.biz/en/docs/messaging-api/unit-based-statistics-aggregation/)", there was a mistake in the description of the request body. We've already corrected the mistake but apologize for any inconvenience caused by this error.

See this table for the differences before and after the correction:

- **Assign a unit name to any aggregation unit when sending messages**

  | Items                                            | Incorrect | Correct |
  | ------------------------------------------------ | --------- | ------- |
  | Max character limit for `customAggregationUnits` | 100       | 30      |

Note that if you specify a name of aggregation unit that exceeds the maximum characters limit when sending a message, the request won't fail but the unit name won't be assigned to the target message.

2021/04/28

## The subject of the email sent upon error notification will be changed 

<!-- note start -->

**Updated on May 25, 2021**

We've updated the [Changes](https://developers.line.biz/en/docs/partner-docs/notice/#partner-news-20210428-01) and [Estimated date of change](https://developers.line.biz/en/docs/partner-docs/notice/#partner-news-20210428-02).

<!-- note end -->

These changes are planned for [Error notification](https://developers.line.biz/en/docs/partner-docs/error-notification/) provided as a Messaging API function.

### Changes 

The subject of the [Notification email](https://developers.line.biz/en/docs/partner-docs/error-notification/#mail) will be changed as follows. We'll also change some of the text in the body of the mail to make it easier to understand.

| Items | Before change | After change |
| --- | --- | --- |
| **Subject** | Messaging API: Webhook transmission failed - `<Channel name>` | Messaging API: Your server did not return \[200 OK\] - `<Channel name>` |

The `<Channel name>` section displays the channel name of the target channel.

### Estimated date of change 

May 25, 2021

For more information, see [Error notification](https://developers.line.biz/en/docs/partner-docs/error-notification/) under the options for corporate customers documentation.

2021/03/10

## We've released a feature for getting statistics per aggregation unit 

You can now obtain statistics per aggregation unit for multiple push messages and multicast messages. You can assign a unit name before sending messages so that you can see statistics for each unit at a later time.

<!-- tip start -->

**When is the feature for getting statistics per aggregation unit useful?**

When sending a narrowcast or broadcast message to multiple users, you can specify a request ID to [get user interaction statistics](https://developers.line.biz/en/reference/messaging-api/#get-message-event) of that particular message.

![User interaction statistics](https://developers.line.biz/media/news/old_statistics_en.png)

When sending a message to fewer than 20 users, you can't obtain statistics because users' privacy must be protected. However, with the newly-released [Get statistics per aggregation unit](https://developers.line.biz/en/docs/messaging-api/unit-based-statistics-aggregation/) feature, even if you send a message to a small number of users, by assigning a unit name before sending the message, you can obtain per-unit statistics on multiple messages.

![Aggregating statistics per unit](https://developers.line.biz/media/news/new_statistics_en.png)

<!-- tip end -->

For more information, see [Get statistics per aggregation unit](https://developers.line.biz/en/docs/messaging-api/unit-based-statistics-aggregation/) under the options for corporate customers documentation.

2020/03/17

## Information on Icon/Nickname Switch 

Icon/Nickname Switch has been integrated into Messaging API.

For more information, see "[You can now change the icon and display name of your LINE Official Account (2020/3/17)](https://developers.line.biz/en/news/2020/03/17/icon-nickname-switch/)".
