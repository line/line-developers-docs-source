# LINE notification messages API reference

<!-- note start -->

**Use of optional functions requires an application**

Only corporate users who have submitted the required applications can use the functions described in this document. To use these functions with your LINE Official Account, contact your sales representative or contact [our Sales partners](https://www.lycbiz.com/jp/partner/sales/).

<!-- note end -->

<!-- table of contents -->

## Common specifications 

### Status codes 

For more information, see [Status codes](https://developers.line.biz/en/reference/messaging-api/#status-codes) in the Messaging API reference.

### Response headers 

The following HTTP headers are included in LINE notification messages API responses:

| Response header   | Description                                   |
| ----------------- | --------------------------------------------- |
| x-line-request-id | Request ID. An ID is issued for each request. |

## LINE notification messages (template) 

- [Send a LINE notification message (template)](https://developers.line.biz/en/reference/line-notification-messages/#send-line-notification-message-template)
- [Get number of sent LINE notification messages (template)](https://developers.line.biz/en/reference/line-notification-messages/#get-number-of-sent-line-notification-messages-template)

### Send a LINE notification message (template) 

API for sending a LINE notification message (template) by specifying the user's phone number.

For more information, see [LINE notification messages (template)](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/template/) in the LINE notification messages documentation.

<!-- warning start -->

**Don't restrict the request source IP addresses**

When sending LINE notification messages, don't register server IP addresses that can call LINE Platform APIs in the [**Security Settings**] tab of the Messaging API channel. Sending a LINE notification message with the source IP addresses restricted may result in sending failure.

For more information about how to check if you are restricting the requesting IP addresses, see [Restrict who can call the API when using a long-lived channel access token (optional)](https://developers.line.biz/en/docs/messaging-api/building-bot/#configure-security-settings) in the Messaging API documentation.

<!-- warning end -->

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/message/pnp/templated/push \
-H 'Authorization: Bearer {channel_access_token}' \
-H 'Content-Type:application/json' \
-H 'X-Line-Delivery-Tag:15034552939884E28681A7D668CEA94C147C716C0EC9DFE8B80B44EF3B57F6BD0602366BC3menu01' \
-d '{
    "to": "c9fb9ae95bff879cbcdfc9edf6716640bc40841f3b7352140daa1431af4c319e",
    "templateKey": "shipment_completed_ja",
    "body": {
        "emphasizedItem": {
            "itemKey": "date_002_ja",
            "content": "Saturday, August 10, 2024"
        },
        "items": [
            {
                "itemKey": "time_range_001_ja",
                "content": "A.M."
            },
            {
                "itemKey": "number_001_ja",
                "content": "1234567"
            },
            {
                "itemKey": "price_001_ja",
                "content": "120 USD"
            },
            {
                "itemKey": "name_010_ja",
                "content": "Frozen Soup Set"
            }
        ],
        "buttons": [
            {
                "buttonKey": "check_delivery_status_ja",
                "url": "https://example.com/CheckDeliveryStatus/"
            },
            {
                "buttonKey": "contact_ja",
                "url": "https://example.com/ContactUs/"
            }
        ]
    }
}'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/v2/bot/message/pnp/templated/push`

#### Rate limit 

2,000 requests per second

#### Request headers 

<!-- note start -->

**Unsupported features**

The LINE notification messages API doesn't allow API request retries using [retry keys](https://developers.line.biz/en/reference/messaging-api/#retry-api-request) (`X-Line-Retry-Key`).

<!-- note end -->

<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

X-Line-Delivery-Tag

String returned in the `delivery.data` property of the [delivery completion event](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#receive-delivery-event) via webhook. For more information, see [Get message delivery notifications](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#receive-delivery-event).\
Minimum character count: 16\
Max character count: 100

<!-- parameter end -->

_Example X-Line-Delivery-Tag_

<!-- tab start `shell` -->

```sh
15034552939884E28681A7D668CEA94C147C716C0EC9DFE8B80B44EF3B57F6BD0602366BC3menu01
```

<!-- tab end -->

#### Request body 

<!-- parameter start (props: required) -->

to

String

Message destination. Specify a phone number that has been normalized to [E.164](https://developers.line.biz/en/glossary/#e164) format and [hashed with SHA256](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#phone-number-hashed).

For more information about conditions for sending a message, see [Conditions for sending LINE notification messages](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#conditions-for-sending-line-notification-messages).

<!-- note start -->

**Note**

- You can't specify [group chats or multi-person chats](https://developers.line.biz/en/docs/messaging-api/group-chats/#group-chat-types).
- You can't specify multiple phone numbers as the transmission target.

<!-- note end -->

<!-- parameter end -->
<!-- parameter start (props: required) -->

templateKey

String

Specify the `Key` of the template you want to send.

See [Templates](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/template/#templates) for available `Key`.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

body

Object

The body object of the template you want to send. Specify the content of the message with three objects. You can't specify the same item more than once in a single message.

- `emphasizedItem`: The [item](https://developers.line.biz/en/reference/line-notification-messages/#send-line-notification-message-template-items) to emphasize.
- `items`: The array of [items](https://developers.line.biz/en/reference/line-notification-messages/#send-line-notification-message-template-items).
- `buttons`: The array of [buttons](https://developers.line.biz/en/reference/line-notification-messages/#send-line-notification-message-template-buttons).

<!-- parameter end -->
<!-- parameter start (props: optional) -->

body.emphasizedItem

Object

Specify the [item](https://developers.line.biz/en/reference/line-notification-messages/#send-line-notification-message-template-items) you want to emphasize in the message.\
Max number of objects: 1

<!-- parameter end -->
<!-- parameter start (props: optional) -->

body.items

Array of objects

Specify the array of [items](https://developers.line.biz/en/reference/line-notification-messages/#send-line-notification-message-template-items) you want to include in the message. \
Min number of objects: 0\
Max number of objects: 15

<!-- parameter end -->
<!-- parameter start (props: optional) -->

body.buttons

Array of objects

Specify the array of [buttons](https://developers.line.biz/en/reference/line-notification-messages/#send-line-notification-message-template-buttons) you want to include in the message. \
Min number of objects: 0\
Max number of objects: 2

<!-- parameter end -->

##### Items 

<!-- parameter start (props: required) -->

itemKey

String

Specify the `Key` of the item you want to include.

See [Items](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/template/#items) for available `Key`.

<!-- parameter end -->
<!-- parameter start (props: required) -->

content

String

Specify the string to be displayed as the value of the item.\
Max number of characters: 15 for `body.emphasizedItem`, 300 for `body.items`

<!-- parameter end -->

_Example item_

<!-- tab start `json` -->

```json
{
  "itemKey": "time_range_001_ja",
  "content": "A.M."
}
```

<!-- tab end -->

##### Buttons 

<!-- parameter start (props: required) -->

buttonKey

String

Specify the `Key` of the button you want to include.

See [Buttons](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/template/#buttons) for available `Key`.

<!-- parameter end -->
<!-- parameter start (props: required) -->

url

String

Specify the URL of the page to be opened when the user presses the button.\
Max number of characters: 1000

<!-- parameter end -->

_Example button_

<!-- tab start `json` -->

```json
{
  "buttonKey": "contact_ja",
  "url": "https://example.com/ContactUs/"
}
```

<!-- tab end -->

#### Response 

Returns status code `202` and an empty JSON object.

_Example response_

<!-- tab start `json` -->

```json
{}
```

<!-- tab end -->

#### Error response 

Returns the following HTTP status code and an error response:

| Code | Description |
| --- | --- |
| `400` | Problem with the request. Consider these reasons:<ul><li>An invalid message destination is specified.</li><li>An invalid message object is specified.</li><li>Your LINE Official Account can't use the specified template.</li></ul> |
| `403` | Not authorized to use this endpoint. |
| `422` | Failed to send a LINE notification message using the LINE notification messages API. Consider these reasons:<ul><li>There is no LINE user associated with the phone number specified as the target for sending messages.</li><li>The phone number specified as the message sending target wasn't issued in LINE notification message service target country. For more information, see [Conditions for sending LINE notification messages](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#conditions-for-sending-line-notification-messages).</li><li>The LINE user associated with the phone number specified as the message sending target has [refused to receive LINE notification messages](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#how-to-consent-for-line-notification-messages).</li><li>The LINE user associated with the phone number specified as the message sending target hasn't agreed to LINE's Privacy Policy (revised in March 2022 or later).</li></ul> |

For more information, see [Status codes](https://developers.line.biz/en/reference/messaging-api/#status-codes) and [Error responses](https://developers.line.biz/en/reference/messaging-api/#error-responses) in the Messaging API reference.

_Example error response_

<!-- tab start `json` -->

```json
// If you specify a template that doesn't exist or that you aren't authorized to use (400 Bad Request)
{
  "message": "Invalid templateKey: reserve_004",
  "details": [
    {
      "message": "The specified template doesn't exist, or you don't have the permission",
      "property": "templateKey"
    }
  ]
}

// If you specify a non-existent item (400 Bad Request)
{
  "message": "The request body has 1 invalid key(s).",
  "details": [
    {
      "message": "The specified item key does not exist: datetime_000",
      "property": "body.items[0].itemKey"
    }
  ]
}

// If you specify the duplicate items (400 Bad Request)
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "Duplicate itemKey in items or between emphasizedItem and items are not allowed: date_002_ja",
      "property": "body.emphasizedItem.itemKey"
    }
  ]
}

// If you specify an invalid message destination (400 Bad Request)
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "The value must be a valid SHA-256 digest.",
      "property": "to"
    }
  ]
}

// If you don't have permission to send LINE notification messages (template) (403 Forbidden)
{
  "message": "Access to this API is not available for your account"
}

// If sending a LINE notification message fails (422 Unprocessable Entity)
{
  "message": "Failed to send messages"
}
```

<!-- tab end -->

### Get number of sent LINE notification messages (template) 

Gets the number of LINE notification messages (template) sent using the [Send a LINE notification message (template)](https://developers.line.biz/en/reference/line-notification-messages/#send-line-notification-message-template) endpoint.

For more information, see [Get the number of sent LINE notification messages](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#get-number-of-sent-line-notification-messages) in the LINE notification messages documentation.

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X GET 'https://api.line.me/v2/bot/message/delivery/pnp/templated?date=20240916' \
-H 'Authorization: Bearer {channel_access_token}'
```

<!-- tab end -->

#### HTTP request 

`GET https://api.line.me/v2/bot/message/delivery/pnp/templated`

#### Rate limit 

2,000 requests per second

#### Request header 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### Query parameter 

<!-- parameter start (props: required) -->

date

Date the message was sent

- Format: `yyyyMMdd` (Example:`20240916`)
- Time zone: UTC+9

<!-- parameter end -->

#### Response 

Returns status code `200` and a JSON object with this information.

<!-- parameter start -->

status

String

Aggregation processing status. One of:

- `ready`: You can get the number of messages.
- `unready`: The total number of messages for the date specified in `date` isn't yet complete. Try the request again after a short time. The aggregation process is usually completed within the next day.
- `out_of_service`: The date specified in `date` is before the aggregation system operation's start date (03/31/2018).

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

success

Number

Number of messages sent using the LINE notification messages API on the date specified in `date`. Only included in the response if the value of `status` is `ready`.

<!-- parameter end -->

_Example response_

<!-- tab start `json` -->

```json
{
  "status": "ready",
  "success": 3
}
```

<!-- tab end -->

#### Error response 

Returns the following HTTP status code and an error response:

| Code | Description |
| --- | --- |
| `400` | Problem with the request. Consider these reasons:<ul><li>An invalid date is specified.</li><li>The date is not specified.</li></ul> |

For more information, see [Status codes](https://developers.line.biz/en/reference/messaging-api/#status-codes) and [Error responses](https://developers.line.biz/en/reference/messaging-api/#error-responses) in the Messaging API reference.

_Example error response_

<!-- tab start `json` -->

```json
// If you specify an invalid date (400 Bad Request)
{
  "message": "The value for the 'date' parameter is invalid"
}
```

<!-- tab end -->

## LINE notification messages (flexible) 

- [Send a LINE notification message (flexible)](https://developers.line.biz/en/reference/line-notification-messages/#send-line-notification-message-flexible)
- [Get number of sent LINE notification messages (flexible)](https://developers.line.biz/en/reference/line-notification-messages/#get-number-of-sent-line-notification-messages-flexible)

### Send a LINE notification message (flexible) 

API for sending a LINE notification message (flexible) by specifying the user's phone number.

<!-- tip start -->

**The name of the existing &quot;LINE notification messages&quot; has been changed to &quot;LINE notification messages (flexible)&quot;**

A new feature called "LINE notification messages (template)" has been added, allowing you to easily create messages by combining premade templates, items, etc.

Consequently, the previous "LINE notification messages" that required UX review have been renamed "LINE notification messages (flexible)".

For more information, see the notice for corporate customers from June 2, 2025, [LINE notification messages (template) now available](https://developers.line.biz/en/docs/partner-docs/notice/#partner-news-20250602).

<!-- tip end -->

<!-- warning start -->

**Don't restrict the request source IP addresses**

When sending LINE notification messages, don't register server IP addresses that can call LINE Platform APIs in the [**Security Settings**] tab of the Messaging API channel. Sending a LINE notification message with the source IP addresses restricted may result in sending failure.

For more information about how to check if you are restricting the requesting IP addresses, see [Restrict who can call the API when using a long-lived channel access token (optional)](https://developers.line.biz/en/docs/messaging-api/building-bot/#configure-security-settings) in the Messaging API documentation.

<!-- warning end -->

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/bot/pnp/push \
-H 'Authorization: Bearer {channel_access_token}' \
-H 'Content-Type:application/json' \
-d '{
    "to": "{hashed_phone_number}",
    "messages":[
        {
            "type":"text",
            "text":"Hello, world1"
        },
        {
            "type":"text",
            "text":"Hello, world2"
        }
    ]
}'

#Example request (with X-Line-Delivery-Tag)
curl -v -X POST https://api.line.me/bot/pnp/push \
-H 'Authorization: Bearer {channel_access_token}' \
-H 'Content-Type:application/json' \
-H 'X-Line-Delivery-Tag:{delivery_tag}' \
-d '{
    "to": "{hashed_phone_number}",
    "messages":[
        {
            "type":"text",
            "text":"Hello, world1"
        },
        {
            "type":"text",
            "text":"Hello, world2"
        }
    ]
}'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/bot/pnp/push`

#### Rate limit 

2,000 requests per second

#### Request header 

<!-- note start -->

**Unsupported features**

The LINE notification messages API doesn't allow API request retries using [retry keys](https://developers.line.biz/en/reference/messaging-api/#retry-api-request) (`X-Line-Retry-Key`).

<!-- note end -->

<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

X-Line-Delivery-Tag

String returned in the `delivery.data` property of the [delivery completion event](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#receive-delivery-event) via Webhook. For more information, see [Get message delivery notifications](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#receive-delivery-event).\
Minimum character count: 16\
Max character count: 100

<!-- parameter end -->

_Example X-Line-Delivery-Tag_

<!-- tab start `shell` -->

```sh
15034552939884E28681A7D668CEA94C147C716C0EC9DFE8B80B44EF3B57F6BD0602366BC3menu01
```

<!-- tab end -->

#### Request body 

<!-- parameter start (props: required) -->

to

String

Message destination. Specify a phone number that has been normalized to [E.164](https://developers.line.biz/en/glossary/#e164) format and [hashed with SHA256](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#phone-number-hashed).

For more information about conditions for sending a message, see [Conditions for sending LINE notification messages](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#conditions-for-sending-line-notification-messages).

<!-- note start -->

**Note**

- You can't specify [group chats and chats with multiple users](https://developers.line.biz/en/docs/messaging-api/group-chats/#group-chat-types).
- You can't specify multiple phone numbers as the transmission target.

<!-- note end -->

<!-- parameter end -->

<!-- parameter start (props: required) -->

messages

Array of [message objects](https://developers.line.biz/en/reference/messaging-api/#message-objects)

Message to be sent. Max: 5

For more information, see [Message types that can be sent in LINE notification messages](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#message-types-that-can-be-sent).

<!-- parameter end -->

#### Response 

Returns status code `200` and an empty JSON object.

_Example response_

<!-- tab start `json` -->

```json
{}
```

<!-- tab end -->

#### Error response 

Returns the following HTTP status code and an error response:

| Code | Description |
| --- | --- |
| `400` | Problem with the request. Consider these reasons:<ul><li>An invalid message destination is specified.</li><li>An invalid message object is specified.</li></ul> |
| `422` | Failed to send a LINE notification message using the LINE notification messages API. Consider these reasons:<ul><li>There is no LINE user associated with the phone number specified as the target for sending messages.</li><li>The phone number specified as the message sending target wasn't issued in LINE notification message service target country. For more information, see [Conditions for sending LINE notification messages](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#conditions-for-sending-line-notification-messages).</li><li>The LINE user associated with the phone number specified as the message sending target has [refused to receive LINE notification messages](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#how-to-consent-for-line-notification-messages).</li><li>The LINE user associated with the phone number specified as the message sending target hasn't agreed to LINE's Privacy Policy (revised in March 2022 or later).</li></ul> |

For more information, see [Status codes](https://developers.line.biz/en/reference/messaging-api/#status-codes) and [Error responses](https://developers.line.biz/en/reference/messaging-api/#error-responses) in the Messaging API reference.

_Example error response_

<!-- tab start `json` -->

```json
// If you specify an invalid message destination (400 Bad Request)
{
  "message": "The request body has 1 error(s)",
  "details": [
    {
      "message": "The value must be a valid SHA-256 digest.",
      "property": "to"
    }
  ]
}

// When sending a LINE notification message fails (422 Unprocessable Entity)
{
  "message": "Failed to send messages"
}
```

<!-- tab end -->

### Get number of sent LINE notification messages (flexible) 

Gets the number of LINE notification messages (flexible) sent using the [Send a LINE notification message (flexible)](https://developers.line.biz/en/reference/line-notification-messages/#send-line-notification-message-flexible) endpoint.

For more information, see [Get the number of sent LINE notification messages](https://developers.line.biz/en/docs/partner-docs/line-notification-messages/technical-specs/#get-number-of-sent-line-notification-messages) in the LINE notification messages documentation.

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X GET 'https://api.line.me/v2/bot/message/delivery/pnp?date=20211231' \
-H 'Authorization: Bearer {channel_access_token}'
```

<!-- tab end -->

#### HTTP request 

`GET https://api.line.me/v2/bot/message/delivery/pnp`

#### Rate limit 

2,000 requests per second

#### Request header 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### Query parameter 

<!-- parameter start (props: required) -->

date

Date the message was sent

- Format: `yyyyMMdd` (Example:`20211231`)
- Time zone: UTC+9

<!-- parameter end -->

#### Response 

Returns status code `200` and a JSON object with this information.

<!-- parameter start -->

status

String

Aggregation processing status. One of:

- `ready`: You can get the number of messages.
- `unready`: The total number of messages for the date specified in `date` isn't yet complete. Try the request again after a short time. The aggregation process is usually completed within the next day.
- `out_of_service`: The date specified in `date` is before the aggregation system operation's start date (03/31/2018).

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

success

Number

Number of messages sent using the LINE notification messages API on the date specified in `date`. Only included in the response if the value of `status` is `ready`.

<!-- parameter end -->

_Example response_

<!-- tab start `json` -->

```json
{
  "status": "ready",
  "success": 3
}
```

<!-- tab end -->

#### Error response 

Returns the following HTTP status code and an error response:

| Code | Description |
| --- | --- |
| `400` | Problem with the request. Consider these reasons:<ul><li>An invalid date is specified.</li><li>The date is not specified.</li></ul> |

For more information, see [Status codes](https://developers.line.biz/en/reference/messaging-api/#status-codes) and [Error responses](https://developers.line.biz/en/reference/messaging-api/#error-responses) in the Messaging API reference.

_Example error response_

<!-- tab start `json` -->

```json
// If you specify an invalid date (400 Bad Request)
{
  "message": "The value for the 'date' parameter is invalid"
}
```

<!-- tab end -->
