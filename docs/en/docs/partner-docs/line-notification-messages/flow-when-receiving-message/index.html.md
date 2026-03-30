# Flow when receiving a LINE notification message

<!-- note start -->

**Use of optional functions requires an application**

Only corporate users who have submitted the required applications can use the functions described in this document. To use these functions with your LINE Official Account, contact your sales representative or contact [our Sales partners](https://www.lycbiz.com/jp/partner/sales/).

<!-- note end -->

## User flow when receiving LINE notification messages 

In addition to agreeing to receive LINE notification messages, users must authenticate their phone number by SMS (SMS verification) once every 180 days to receive LINE notification messages.

![User flow when receiving LINE notification messages](https://developers.line.biz/media/line-notification-message/pnp-receive-flow-en.png)

- [Flow for the case where a user has already agreed to receive LINE notification messages and doesn't need SMS authentication](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#receiving-line-notification-messages)
- [Flow for the case where a user hasn't agreed to receive LINE notification messages and doesn't need SMS authentication](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-1)
- [Flow for the case where a user hasn't agreed to receive LINE notification messages and SMS authentication is needed](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-2)
- [Flow for the case where a user has already agreed to receive LINE notification messages and SMS authentication is needed](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-3)
- [Note: Flow for changing the phone number registered to the LINE account](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#when-changing-your-phone-number)

<!-- note start -->

**Settings for receiving LINE notification messages are comprehensive**

Once a user agrees to receive LINE notification messages, they're considered to have agreed to receive LINE notification messages from all LINE Official Accounts.

For example, if a user who has agreed to receive LINE notification messages in response to a LINE notification message sent from LINE Official Account A also receives a LINE notification message sent from a different LINE Official Account B, the user will have agreed to receive LINE notification messages and won't need to give consent again.

<!-- note end -->

<!-- note start -->

**SMS authentication must be done once every 180 days for each user's LINE account**

Once a user performs SMS authentication, SMS authentication isn't needed when receiving LINE notification messages sent from all LINE Official Accounts for 180 days.

For example, if a user who has performed SMS authentication in response to a LINE notification message sent from LINE Official Account A receives a LINE notification message sent from another LINE Official Account B within 180 days, the user will have already been SMS authenticated and won't be needed to perform SMS authentication again.

<!-- note end -->

<!-- note start -->

**Cases where SMS authentication isn't needed**

SMS authentication isn't needed when receiving a LINE notification message in these cases:

- Within 180 days of creating a new LINE account
- Within 180 days of changing the phone number registered to the user's LINE account.

<!-- note end -->

### Flow for the case where a user has already agreed to receive LINE notification messages and doesn't need SMS authentication 

| Number | Image | Description |
| --- | --- | --- |
| 1 | ![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-3-ja.png)<br><br>![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-4-ja.png) | If a user has already agreed to receive LINE notification messages and doesn't need SMS authentication, the "LINE" system account will send a "LINE Notification Message Received" message to the user. At the same time, the requested LINE notification message will be sent to the user. |

### Flow for the case where a user hasn't agreed to receive LINE notification messages and doesn't need SMS authentication 

| Number | Image | Description |
| --- | --- | --- |
| 1 | ![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-1-ja.png) | If a user hasn't agreed to receive LINE notification messages and doesn't need SMS authentication, when the user receives a LINE notification message, the user will receive a "You have received a LINE notification message" and "Set up to receive LINE notification messages" message from the "LINE" system account. |
| 2 | ![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-2-ja.png) | Clicking the "Set" button under "Set up to receive LINE notification messages" will take the user to the consent screen for receiving LINE notification messages. |
| 3 | ![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-3-ja.png)<br><br>![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-4-ja.png) | If the user agrees to the "Set up to receive LINE notification messages", the user will receive a message from the "LINE" system account stating that you've received a LINE notification message. The requested LINE notification message is then sent to the user. |

### Flow for the case where a user hasn't agreed to receive LINE notification messages and SMS authentication is needed 

| Number | Image | Description |
| --- | --- | --- |
| 1 | ![](https://developers.line.biz/media/line-notification-message/type3-pnpflow-1-ja.png) | If a user hasn't agreed to receive LINE notification messages and SMS authentication is needed, the "LINE" system account will send the user a "You have received a LINE notification message" and "Set up to receive LINE notification messages" message when the user receives a LINE notification message. |
| 2 | ![](https://developers.line.biz/media/line-notification-message/type3-pnpflow-2-ja.png) | Clicking the "Set" button under "Set up to receive LINE notification messages" will take the user to the consent screen for receiving LINE notification messages. |
| 3 | ![](https://developers.line.biz/media/line-notification-message/type3-pnpflow-3-ja.png) | If the user agrees to the "Set up to receive LINE notification messages", a confirmation dialog box for sending an SMS message to the phone number registered in the LINE account will be displayed. At this time, the user can also change the phone number to which the SMS is sent (the phone number registered in the LINE account). |
| 4 | ![](https://developers.line.biz/media/line-notification-message/type3-pnpflow-4-ja.png) | An SMS message will be sent to the specified phone number. Enter the PIN number provided in the message. |
| 5 | ![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-3-ja.png)<br><br>![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-4-ja.png) | Once the SMS verification is completed, the "LINE" system account will send a "LINE Notification Message Received" message to the user. At the same time, the requested LINE notification message will be sent to the user. |

### Flow for the case where a user has already agreed to receive LINE notification messages and SMS authentication is needed 

| Number | Image | Description |
| --- | --- | --- |
| 1 | ![](https://developers.line.biz/media/line-notification-message/type2-pnpflow-1-ja.png) | If a user has already agreed to receive LINE notification messages and SMS authentication is needed, the "LINE" system account will send the user a "LINE notification message received" message and a "phone number authentication" message when the user receives a LINE notification message. |
| 2 | ![](https://developers.line.biz/media/line-notification-message/type2-pnpflow-2-ja.png) | Clicking "Set" in the "Phone number authentication" message will take the user to the phone number authentication screen. |
| 3 | ![](https://developers.line.biz/media/line-notification-message/type2-pnpflow-3-ja.png) | When the "Send SMS" button is pressed, a confirmation dialog box for sending an SMS message to the phone number registered in the LINE account will be displayed. At this time, the user can also change the phone number to which the SMS is sent (the phone number registered in the LINE account). |
| 4 | ![](https://developers.line.biz/media/line-notification-message/type2-pnpflow-4-ja.png) | An SMS message will be sent to the specified phone number. Enter the PIN number provided in the message. |
| 5 | ![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-3-ja.png)<br><br>![](https://developers.line.biz/media/line-notification-message/type1-pnpflow-4-ja.png) | Once the SMS verification is completed, the "LINE" system account will send a "LINE Notification Message Received" message to the user. At the same time, the requested LINE notification message will be sent to the user. |

## Note: Flow for changing the phone number registered to the LINE account 

To change the phone number registered with the LINE account, the user taps **Change** during SMS authentication when receiving a LINE notification message, taps **Next**, and then enters the phone number.

<!-- tip start -->

**Change the phone number registered in the LINE account**

You can also change your phone number by going to **Settings** > **Profile** > **Phone number** in the LINE app. For more information, see [Checking/changing your phone number](https://help.line.me/line/smartphone/pc?lang=en&contentId=20000120) in the LINE Help Center.

<!-- tip end -->

| Number | Image | Description |
| --- | --- | --- |
| 1 | ![](https://developers.line.biz/media/line-notification-message/change-phone-number-1-en.png) | Enter the phone number you wish to change and click "Next". |
| 2 | ![](https://developers.line.biz/media/line-notification-message/change-phone-number-2-en.png) | An SMS message will be sent to the specified phone number. Enter the PIN code provided in the message. |
| 3 | ![](https://developers.line.biz/media/line-notification-message/change-phone-number-3-ja.png) | After successfully authenticating your phone number via SMS, you'll receive a "Your phone number has been changed" message from your LINE account. |

<style scoped>
.table-user-content-flow td:nth-child(2) {
    min-width: 160px;
}
.table-user-content-flow td:nth-child(3) {
    min-width: 200px;
}
</style>
