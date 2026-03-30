# LINE notification messages overview

<!-- note start -->

**Use of optional functions requires an application**

Only corporate users who have submitted the required applications can use the functions described in this document. To use these functions with your LINE Official Account, contact your sales representative or contact [our Sales partners](https://www.lycbiz.com/jp/partner/sales/).

<!-- note end -->

## Overview 

LINE notification messages is a service that allows you to send messages to users by specifying their phone numbers. Even if a user hasn't added your LINE Official Account as a friend, you can send them messages from your LINE Official Account.

LINE notification messages can only be used on LINE Official Accounts in Japan, Thailand and Taiwan.

There are two types of LINE notification messages: [LINE notification messages (template)](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/template/), which allow you to easily create messages by combining premade templates and items, and [LINE notification messages (flexible)](https://developers.line.biz/en/reference/line-notification-messages/#flexible), which require prior UX review. Each type has different API endpoints.

The following is a sample of a LINE notification message (template):

![Sample of LINE notification messages (template)](https://developers.line.biz/media/line-notification-message/line-notification-messages-sample-ja.png)

For more information, see [Technical specifications of the LINE notification messages API](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/) and the [LINE notification messages API reference](https://developers.line.biz/en/reference/line-notification-messages/).

<!-- tip start -->

**The purpose of use for LINE notification messages**

The purpose of use for LINE notification messages is limited to those that we deem useful and appropriate for users. It can't be sent for commercial or advertising purposes. For more information, see [LINE notification messages (template) UX guidelines](https://www.lycbiz.com/sites/default/files/media/jp/download/LINE_Official_Notification_Template_UXGuideline.pdf) (only available in Japanese) and [LINE notification messages (flexible) UX guidelines](https://www.lycbiz.com/sites/default/files/media/jp/download/LINE%E9%80%9A%E7%9F%A5%E3%83%A1%E3%83%83%E3%82%BB%E3%83%BC%E3%82%B8UX%E3%82%AC%E3%82%A4%E3%83%89%E3%83%A9%E3%82%A4%E3%83%B3.pdf) (only available in Japanese) in LINE for Business.

<!-- tip end -->

## Difference in appearance from other messages 

LINE notification messages are displayed with “Important notification” to the right of the LINE Official Account icon to distinguish them from other messages. This function is available in LINE version 15.9.0 or later for iOS, Android, and iPad.

![LINE notification messages are displayed with “Important notification” to the right of the icon](https://developers.line.biz/media/line-notification-message/notification-messages-important-en.jpg)

The text displayed may vary depending on the language settings of the LINE app that received the LINE notification message.

| LINE app language settings       | Text displayed           |
| -------------------------------- | ------------------------ |
| Japanese                         | `重要なお知らせ`         |
| Thai                             | `การแจ้งเตือนสำคัญ`      |
| Chinese (Simplified/Traditional) | `重要通知`               |
| Other                            | `Important notification` |

For more information about the language setting of the LINE app, see [Changing the LINE app language setting](https://help.line.me/line/?contentId=20007465&lang=en) in the Help Center.

## Related pages 

- [Technical specifications of the LINE notification messages API](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/)
- [LINE notification messages API reference](https://developers.line.biz/en/reference/line-notification-messages/)
- [Webhook delivery completion event](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/)
- [Flow when receiving a LINE notification message](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/flow-when-receiving-message/)
