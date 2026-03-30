# Running your service

We strongly recommend that Service Designers, Operators, and Marketers read this guideline and prepare acccordingly.

<!-- table of contents -->

## Sharing the LINE MINI App Link 

When sharing your LINE MINI App or its page, you need to [create a permanent link](https://developers.line.biz/en/docs/line-mini-app/develop/permanent-links/). Use a permanent link, especially when considering sharing your LINE MINI App in the following ways:

- When sharing the link outside of LINE, such as via web pages, emails, and social media.
- [When sharing via rich messages or rich menus on the LINE Official Account](https://developers.line.biz/en/docs/line-mini-app/service/line-mini-app-oa/)
- [When implementing a custom action button](https://developers.line.biz/en/docs/line-mini-app/develop/share-messages/)
- When using a [service message](https://developers.line.biz/en/docs/line-mini-app/develop/service-messages/) to share.
- When using LINE MINI Apps [POP template](https://creativelab-tips.line.me/ja/line-miniapp/creative/) (only available in Japanese) with a QR code on it

## Conditions for service messages 

You are allowed to send [service messages](https://developers.line.biz/en/docs/line-mini-app/develop/service-messages/) only as a confirmation or response to a user action on LINE MINI App.

### Notifications allowed by service messages 

Service messages allow the following notifications:

| Type | Use Case |
| --- | --- |
| Action Confirmation Notification | <ul><li>Confirmation notification of reservations at restaurants and accommodations</li><li>Confirmation notification of purchased tickets and merchandise</li></ul> |
| Action Result Notification | <ul><li>Check-in completion notification</li><li>Notification of shipment completion of an order</li></ul> |
| Reminder Notification | <ul><li>Reminder notification of reservations at restaurants and accommodations</li><li>Reminder for a play, movie, or concert for which ticket was purchased</li></ul> |

### Notifications disallowed by service messages 

Service messages disallow the following notifications:

- Notifications that are not confirmations or responses to user actions on the LINE MINI Apps, such as purchase completion notifications and reminder notifications when tickets are purchased from ticket vending machines.
- Advertisements and event notifications including information on discounts, shopping rewards, new products, discount coupons or promotions.

If a service message is sent with unacceptable content, the use of the service message API will be prohibited for a period of time. Repeated violations of the terms and conditions may cause your LINE MINI App to be removed from LINE.

### Message Count Limit 

- You can send up to 5 messages per user action. This limit applies to the respective use cases of action confirmation, action result, and reminder notifications.
- The message count limit is subject to change depending on the use scenario. If the limit is changed, LY Corporation will notify you at the time of [review](https://developers.line.biz/en/docs/line-mini-app/submit/submission-guide/).

### Service Message Templates 

- [Add a service message template](https://developers.line.biz/en/docs/line-mini-app/develop/service-messages/#service-message-templates) to your LINE MINI App channel.
- You can configure up to 20 templates for each LINE MINI App channel.

## Channel consent simplification 

For a LIFF app to get user information or send messages to users, users need to consent to the corresponding permissions on the channel consent screen when they access the LIFF app for the first time.

In LINE MINI Apps, with the "Channel consent simplification" feature, users only need to consent to the simplification once. After that, when users access another LINE MINI App for the first time, the channel consent screen is skipped, allowing them to start using the LINE MINI App immediately.

However, based on LY Corporation’s privacy policy, the only permission whose consent is skipped by the "Channel consent simplification" feature is getting the [user ID](https://developers.line.biz/en/glossary/#user-id). For permissions required to get user profile information or send messages, the verification screen is displayed within each LINE MINI App at the time those permissions are needed.

Enabling the "Channel consent simplification" feature makes it easier for users to access LINE MINI Apps. To improve the user experience, we recommend enabling the "Channel consent simplification" feature.

For new LINE MINI App channels in Japan, the "Channel consent simplification" feature is always enabled.

For more information, see [LINE MINI App authorization flow](https://developers.line.biz/en/docs/line-mini-app/develop/channel-consent-simplification/).
