# Webhook delivery completion event

<!-- note start -->

**Use of optional functions requires an application**

Only corporate users who have submitted the required applications can use the functions described in this document. To use these functions with your LINE Official Account, contact your sales representative or contact [our Sales partners](https://www.lycbiz.com/jp/partner/sales/).

<!-- note end -->

## Overview of webhook delivery completion events 

When a request is made to the LINE notification messages API and delivery of the LINE notification message to the user is completed, a dedicated webhook event (delivery completion event) is sent from the LINE Platform to the webhook URL of the bot server.

- [Webhook delivery completion event specifications](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#receive-delivery-event)
- [Additional information on webhook delivery completion events](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#we-cant-receive-a-delivery-webhook-event)

### Webhook delivery completion event specifications 

| Property name | Type | Description |
| --- | --- | --- |
| type | String | `delivery` |
| mode | Object | See [Common properties](https://developers.line.biz/en/reference/messaging-api/#common-properties). |
| timestamp | Number | See [Common properties](https://developers.line.biz/en/reference/messaging-api/#common-properties). |
| webhookEventId | String | See [Common properties](https://developers.line.biz/en/reference/messaging-api/#common-properties). |
| deliveryContext | Object | See [Common properties](https://developers.line.biz/en/reference/messaging-api/#common-properties). |
| delivery | Object | A delivery object containing a hashed phone number string or a string specified by [`X-Line-Delivery-Tag`](https://developers.line.biz/en/reference/line-notification-messages/#send-line-notification-message-template-request-headers). |
| delivery.data | String | A hashed phone number string or a string specified by [`X-Line-Delivery-Tag`](https://developers.line.biz/en/reference/line-notification-messages/#send-line-notification-message-template-request-headers). |

_Example webhook event_

<!-- tab start `json` -->

```json
// Example webhook delivery completion event (without X-Line-Delivery-Tag header specified)
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
      "mode": "active"
    }
  ]
}

// Example webhook delivery completion event (with X-Line-Delivery-Tag header specified)
{
  "destination": "Uc7472b39e21dab71c2347e02714630d6",
  "events": [
    {
      "type": "delivery",
      "delivery": {
        "data": "15034552939884E28681A7D668CEA94C147C716C0EC9DFE8B80B44EF3B57F6BD0602366BC3menu01"
      },
      "webhookEventId": "01G17EJCGAVV66J5WNA7ZCTF6H",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1650591346705,
      "mode": "active"
    }
  ]
}
```

<!-- tab end -->

<!-- note start -->

**About the status of webhook delivery completion events**

The webhook delivery completion event **indicates that the LINE notification message has been delivered to the user and the message can now be viewed**. It doesn't indicate the following:

- Successful LINE notification messages API request
- [User gets "Set up to get LINE notification messages" message](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-1)
- Consent to get LINE notification messages
- [User gets a message asking for SMS authentication](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-3)
- User performs SMS authentication
- User opens the LINE notification message (read)

<!-- note end -->

<!-- note start -->

**Signature verification of webhook events**

Use the channel secret for [Verify signature](https://developers.line.biz/en/docs/messaging-api/receiving-messages/#verify-signature) upon receipt of the delivery completion event. For channels using LINE Chat Plus, use Switcher Secret to verify signatures.

<!-- note end -->

## Additional information on Webhook delivery completion events 

Even if a LINE notification messages API request is sent and a response is made with the HTTP status code `200` or `202`, depending on the user's [LINE notification message reception settings](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#how-to-consent-for-line-notification-messages) and SMS authentication status, LINE notification messages may not be delivered to the user or the sending of LINE notification messages may be suspended.

If a LINE notification messages API request is sent and a [Webhook delivery completion event](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/) isn't received within 24 hours after the response is made with the HTTP status code `200` or `202`, it means that the LINE notification message wasn't delivered to the user for one of these reasons.

- [The user has blocked the LINE Official Account](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#user-blocked-your-account)
- [The user didn't give required consent or authentication](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#user-didnt-action-taken)

### The user has blocked the LINE Official Account 

Even if the user has blocked the LINE Official Account that sent the LINE notification message, [requests for the LINE notification messages API](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#about-pnp-api-block-response) will be responded with HTTP status code `200` or `202`.

### The user didn't give required consent or authentication 

It's possible that the settings for receiving LINE notification messages haven't been set, or that SMS authentication is required, but these settings or operations haven't been performed. For more information, see [When the LINE notification messages API request is successful but the message isn't sent](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#why-i-cant-receive-line-notification-messages).
