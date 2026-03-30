# Error notification

<!-- note start -->

**Use of optional functions requires an application**

Only corporate users who have submitted the required applications can use the functions described in this document. To use these functions with your LINE Official Account, contact your sales representative or contact [our Sales partners](https://www.lycbiz.com/jp/partner/sales/).

<!-- note end -->

## Summary 

If the user adds your LINE Official Account as a friend or sends a message to your LINE Official Account, LINE Platform sends a webhook event to the URL (bot server) specified in the [LINE Developers Console](https://developers.line.biz/console/) "Webhook URL".

If the bot server doesn't respond or returns a response other than status code `2xx` to this webhook event request, the channel administrator will receive a notification email informing them of the occurrence of the error. This option is called the "error notification" function.

![You will receive a notification email when an error is returned from the bot server](https://developers.line.biz/media/partner-docs/normal-error-notification-en.jpg)

## Notification email 

This topic explains the email sent by the error notification function.

### Email recipients 

Notification email will be sent to the following email addresses:

- Email address registered on the **Basic settings** page of the target channel
- Registered email address of a user with the Admin role for the target channel

### Email types 

Notification emails can be of the following types:

- [When the LINE Platform detected an error](https://developers.line.biz/en/docs/partner-docs/error-notification/#detected-error)
- [When the LINE Platform stopped webhook redelivery](https://developers.line.biz/en/docs/partner-docs/error-notification/#webhook-redelivery-stopped) (only if Webhook redelivery is enabled)

#### When the LINE Platform detected an error 

When the LINE Platform detected that an error has occurred, the following email will be sent. The contents of the email and error messages are subject to change without notice.

| | |
| --- | --- |
| Subject | Messaging API: Your bot server returned no response or an error - `<Channel name>` |
| Main text | LINE Platform sent a webhook, but your bot server did not respond or returned an error.<br/>Check the reason and details for the error and your bot server's configuration. Then make any necessary changes so that it can receive webhooks properly. |
| Error details | The reason for the error and the date and time of occurrence will be described per situation. For details, see [Email content](https://developers.line.biz/en/docs/partner-docs/error-notification/#content). |

<!-- tip start -->

**You can also check error information in the LINE Developers Console**

You can also check the error information you received in the notification email in the [LINE Developers Console](https://developers.line.biz/console/). For more information, see ["Webhook errors" tab in the LINE Developers Console](https://developers.line.biz/en/docs/partner-docs/error-notification/#line-developers-console).

<!-- tip end -->

#### When the LINE Platform stopped webhook redelivery 

If you've [enabled Webhook redelivery](https://developers.line.biz/en/docs/messaging-api/receiving-messages/#enable-webhook-redelivery) in the Messaging API channel settings, the LINE Platform will redeliver the webhook that your bot server failed to receive.

Then, if the bot server doesn't respond after a certain period of time, the LINE Platform will stop redelivering the webhook and send the following email. The subject and content of the email may change without notice.

| | |
| --- | --- |
| Subject | Messaging API: Webhook redelivery stopped - `<Channel name>` |
| Main text | The LINE Platform tried to send the webhook for the event(s), but stopped redelivery due to no response from your bot server.<br>Please visit the LINE Developers site for details. |
| Error details | The reason for the error and the date and time of occurrence will be described per situation. For details, see [Email content](https://developers.line.biz/en/docs/partner-docs/error-notification/#content). |

For more information about the webhook redelivery, see [Redeliver a webhook that failed to be received](https://developers.line.biz/en/docs/messaging-api/receiving-messages/#webhook-redelivery).

### Notification email sample 

![sample mail](https://developers.line.biz/media/partner-docs/error-notification-email-sample.png)

### Email content 

These are the contents of the email.

| Item | Description |
| --- | --- |
| Channel ID | Target channel ID. |
| Channel name | Target channel name. |
| Reason for error  | Overview of reason for error. For more information, see [Check the reason for errors](https://developers.line.biz/en/docs/messaging-api/check-webhook-error-statistics/#check-error-reason) in the Messaging API documentation. |
| Detail for error | Details on reason for error. For more information, see [Check the detail for errors](https://developers.line.biz/en/docs/messaging-api/check-webhook-error-statistics/#check-detail-for-error) in the Messaging API documentation. |
| Error count | Number of times error occurred. |
| Time detected | Time when error occurred. |

## How to resolve a notification message 

Suppose you received the same error notification content as in the [Notification email sample](https://developers.line.biz/en/docs/partner-docs/error-notification/#sample-mail). Since the reason for error is `error_status_code` and detail for error is `500`, so [check the reason for errors](https://developers.line.biz/en/docs/messaging-api/check-webhook-error-statistics/#check-error-reason), you can assume that the bot server responded to the webhook request with the HTTP status code `500`.

In this case, the bot server may not have been able to properly process the webhook events it received. Investigate the cause of the problem by examining the bot server's webhook events processing log.

<!-- note start -->

**On error investigation**

LY Corporation doesn't provide individual investigation or confirmation of errors. The reason of the error should be addressed directly by the developer managing the channel or bot server.

<!-- note end -->

## "Webhook errors" tab in the LINE Developers Console 

You can also check the error information received in the notification email on the **Webhook errors** tab of the Messaging API channel on the [LINE Developers Console](https://developers.line.biz/console/).

The **Webhook errors** tab is displayed only for channels where **Error statistics aggregation** is enabled on the **Messaging API** tab. For more information, see [Enable error statistics](https://developers.line.biz/en/docs/messaging-api/check-webhook-error-statistics/#enable-error-statistics).

![Error statistics aggregation](https://developers.line.biz/media/messaging-api/receiving-messages/error-statistics-en.png)
