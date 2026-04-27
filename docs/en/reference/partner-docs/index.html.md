# Options for corporate customers API reference

<!-- note start -->

**Use of optional functions requires an application**

Only corporate users who have submitted the required applications can use the functions described in this document. To use these functions with your LINE Official Account, contact your sales representative or contact [our Sales partners](https://www.lycbiz.com/jp/partner/sales/).

<!-- note end -->

<!-- table of contents -->

## Common specifications 

### Status codes 

For more information, see [Status codes](https://developers.line.biz/en/reference/messaging-api/#status-codes) in the Messaging API reference.

### Response headers 

The following HTTP headers are included in Options for corporate customers API responses:

| Response header   | Description                                   |
| ----------------- | --------------------------------------------- |
| x-line-request-id | Request ID. An ID is issued for each request. |

## Mission Sticker API 

Mission stickers are provided to users upon completion of certain objectives. Using stickers as an incentive, users are encouraged to "link ID information," "register as a member," or "answer a questionnaire."

### Provide mission stickers to the users 

Grants permission for users who have completed a certain objective to download your mission sticker.

_Example request_

<!-- tab start `shell` -->

```sh
curl -X POST https://api.line.me/shop/v3/mission \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {channel access token}" \
-d '{
    "to": "U4af4980629...",
    "productType": "STICKER",
    "productId": "0000",
    "sendPresentMessage": false
}'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/shop/v3/mission`

#### Request headers 

<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### Request body 

<!-- parameter start (props: required) -->

to

String

User ID of a user to grant download permission

<!-- parameter end -->
<!-- parameter start (props: required) -->

productType

String

`STICKER`

<!-- parameter end -->
<!-- parameter start (props: required) -->

productId

String

Package ID for a set of stickers

<!-- parameter end -->
<!-- parameter start (props: required) -->

sendPresentMessage

Boolean

`false`

<!-- parameter end -->

#### Response 

Returns status code `200` and an empty response body.

#### Error response 

An HTTP status code corresponding to the error and this JSON data are returned in the response body when an error occurs.

<!-- parameter start -->

message

String

Message containing error information. For more information, see [Error messages](https://developers.line.biz/en/reference/partner-docs/#send-mission-stickers-v3-error-messages).

<!-- parameter end -->

_Error response example_

<!-- tab start `json` -->

```json
// If you specify an invalid user ID (400 Bad Request)
{
  "message": "invalid request"
}
```

<!-- tab end -->

##### Error messages 

The HTTP status code for the main errors and the error message that is found in the `message` property of the JSON data are as follows:

| Code | Message | Description |
| --- | --- | --- |
| `400` | invalid request | The destination user ID specified for `to` is invalid. |
| `400` | illegal argument | The sticker set specified for `productId` isn't set as a mission sticker. |
| `400` | not in sales period | The sticker set specified for `productId` is out of validity period. |
| `400` | sticker set not available for channel | The channel doesn't have the permission to use the sticker set specified for `productId`. |
| `400` | not available | Unable to grant the sticker for one of the following reasons: <ul><li>The sticker set specified for `productId` isn't available for purchase in the country or region of the destination user specified for `to`.</li><li>The device of the destination user specified for `to` doesn't support the sticker set specified for `productId`.</li><li>The version of the LINE app used by the destination user specified for `to` doesn't support the sticker set specified for `productId`.</li></ul> |
| `403` | not allowed to use the API | The channel isn't granted the required permission for the mission sticker API. |
| `404` | not found | The sticker set specified for `productId` doesn't exist. |
| `500` | internal error | An internal server error occurred. Wait a while and try again later. |
| `502` | upstream error | An internal network error occurred. Wait a while and try again later. |

## Mark as read API (old) 

### Mark messages from users as read 

All messages sent from a specific user can display "Read".

<!-- tip start -->

**Use the new endpoint to mark as read**

The Mark as read API (old) remains available for use. However, if you're implementing functionality to mark messages as read from users going forward, use the Messaging API's [Mark messages as read](https://developers.line.biz/en/reference/messaging-api/#mark-as-read) endpoint. The "Mark messages as read" endpoint requires no application and can be used in conjunction with chat feature.

<!-- tip end -->

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/message/markAsRead \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {channel_access_token}' \
-d '{
    "chat": {
        "userId": "Uxxxxxxxxxxxxxxxxxx"
    }
}'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/v2/bot/message/markAsRead`

#### Rate limit 

2,000 requests per second

#### Request headers 

<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

<!-- parameter end -->

#### Request body 

<!-- parameter start (props: required) -->

chat.userId

String

The target user ID

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

| Code  | Description                      |
| ----- | -------------------------------- |
| `400` | An invalid user ID is specified. |

For more information, see [Status codes](https://developers.line.biz/en/reference/messaging-api/#status-codes) and [Error responses](https://developers.line.biz/en/reference/messaging-api/#error-responses) in the Messaging API reference.

_Example error response_

<!-- tab start `json` -->

```json
// If you specify an invalid user ID (400 Bad Request)
{
  "message": "The property, 'chat.chatId', in the request body is invalid (line: -, column: -)"
}
```

<!-- tab end -->

## Module 

### Attach by operation of the module channel provider 

Attach the module channel to the LINE Official Account. In order to attach, you most request authorization from the admin of the LINE Official Account and obtain an authorization code. For more information about the module authorization flow, see [Attach Module Channel](https://developers.line.biz/en/docs/partner-docs/module-technical-attach-channel/) in the module documentation.

When using this API, you need to specify the channel ID and channel secret of the module channel using either the `Authorization` header or the request body.

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://manager.line.biz/module/auth/v1/token \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=authorization_code' \
-d 'code=1234567890abcde' \
--data-urlencode 'redirect_uri=https://example.com/auth?key=value' \
-d 'code_verifier=ayjtZgTunh96nHCvgLEiXzqVQOOC0SwMRs39bh1l5dx' \
-d 'client_id=1234567890' \
-d 'client_secret=1234567890abcdefghij1234567890ab' \
-d 'region=JP' \
-d 'basic_search_id=@linedevelopers' \
-d 'scope=message%3Asend%20message%3Areceive' \
-d 'brand_type=premium'
```

<!-- tab end -->

#### HTTP request 

`POST https://manager.line.biz/module/auth/v1/token`

#### Request headers 

<!-- parameter start (props: required) -->

Content-Type

`application/x-www-form-urlencoded`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

Authorization

`Basic {base64({Channel ID}:{Channel Secret})}`

For `{base64({Channel ID}:{Channel Secret})}`, specify a Base64-encoded string by concatenating "Module Channel ID" and "Module Channel Secret" with `:`. You can find the module channel's channel ID and channel secret in the [LINE Developers Console](https://developers.line.biz/console/).

Instead of using `client_id` and `client_secret` in request body, you can use this header to specify the channel ID and the channel secret of the module channel.

<!-- parameter end -->

#### Request body 

<!-- parameter start (props: required) -->

grant_type

String

`authorization_code`

<!-- parameter end -->
<!-- parameter start (props: required) -->

code

String

[Authorization code](https://developers.line.biz/en/docs/partner-docs/module-technical-attach-channel/#receive-authorization-code) received from the LINE Platform.

<!-- parameter end -->
<!-- parameter start (props: required) -->

redirect_uri

String

Specify the `redirect_uri` specified in [the URL for authentication and authorization](https://developers.line.biz/en/docs/partner-docs/module-technical-attach-channel/#request-auth-from-line-oa-admin-query-parameters).

<!-- parameter end -->
<!-- parameter start (props: optional) -->

code_verifier

String

Specify when using PKCE (Proof Key for Code Exchange) defined in the OAuth 2.0 extension specification as a countermeasure against authorization code interception attacks.

Compliant with [RFC 7636](https://datatracker.ietf.org/doc/html/rfc7636).

<!-- parameter end -->
<!-- parameter start (props: optional) -->

client_id

String

Instead of using `Authorization` header, you can use this parameter to specify the channel ID of the module channel. You can find the channel ID of the module channel in the [LINE Developers Console](https://developers.line.biz/console/).

<!-- parameter end -->
<!-- parameter start (props: optional) -->

client_secret

String

Instead of using `Authorization` header, you can use this parameter to specify the channel secret of the module channel. You can find the channel secret of the module channel in the [LINE Developers Console](https://developers.line.biz/console/).

<!-- parameter end -->
<!-- parameter start (props: optional) -->

region

String

If you specified a value for `region` in [the URL for authentication and authorization](https://developers.line.biz/en/docs/partner-docs/module-technical-attach-channel/#request-auth-from-line-oa-admin-query-parameters), specify the same value.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

basic_search_id

String

If you specified a value for `basic_search_id` in the URL for authentication and authorization, specify the same value.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

scope

String

If you specified a value for `scope` in the URL for authentication and authorization, specify the same value.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

brand_type

String

If you specified a value for `brand_type` in the URL for authentication and authorization, specify the same value.

<!-- parameter end -->

#### Response 

Returns a JSON object with status code `200` and this information on success.

<!-- parameter start -->

bot_id

String

User ID of the bot on the LINE Official Account.

The bot's user ID is used when calling the [Messaging API](https://developers.line.biz/en/reference/messaging-api/) or the [Acquire Control API](https://developers.line.biz/en/reference/partner-docs/#acquire-control-api).

<!-- note start -->

**Note**

The bot's user ID isn't the **Your user ID** displayed on the **Basic Settings** tab of the [LINE Developers Console](https://developers.line.biz/console/) for the Messaging API channel.

<!-- note end -->

<!-- parameter end -->
<!-- parameter start -->

scope

String

Permissions (scope) granted by the LINE Official Account admin.

<!-- parameter end -->

_Example response_

<!-- tab start `json` -->

```json
{
  "bot_id": "U45c5c51f0050ef0f0ee7261d57fd3c56",
  "scopes": [
    "message:send",
    "message:receive"
  ]
}
```

<!-- tab end -->

#### Error response 

Returns the following HTTP status code:

- `400 Bad Request`
- `403 Forbidden`

### Unlink (detach) the module channel by the operation of the module channel administrator 

The module channel admin calls the Detach API to detach the module channel from a LINE Official Account.

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/channel/detach \
-H 'Content-Type:application/json' \
-H 'Authorization: Bearer {channel access token}' \
-d '{"botId":"U45c5c51f0050ef0f0ee7261d57fd3c56"}'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/v2/bot/channel/detach`

#### Rate limit 

2,000 requests per second

#### Request headers 

<!-- parameter start (props: required) -->

Content-Type

`application/json`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

`Bearer {channel access token}`

For `{channel access token}`, specify the channel access token of your module channel.

<!-- parameter end -->

#### Request body 

<!-- parameter start (props: required) -->

botId

String

The user ID of the LINE Official Account bot attached to the module channel.

You can get the user ID of the bot from the response of the [Attach by operation of the module channel provider](https://developers.line.biz/en/reference/partner-docs/#link-attach-by-operation-module-channel-provider) or the [Attached event](https://developers.line.biz/en/reference/partner-docs/#attached-event).

<!-- parameter end -->

#### Response 

Returns a `200` status code on success.

#### Error Response 

Returns the following HTTP status code and an error response:

| Code | Description |
| --- | --- |
| `400` | Couldn't unlink (detach) the module channel. Consider these reasons:<ul><li>An invalid user ID of the LINE Official Account bot is specified.</li><li>A non-existent LINE Official Account bot is specified.</li><li>The module channel isn't linked (attached).</li><li>A channel access token is specified for a non-module channel.</li></ul> |

For more information, see [Status codes](https://developers.line.biz/en/reference/messaging-api/#status-codes) and [Error responses](https://developers.line.biz/en/reference/messaging-api/#error-responses) in the Messaging API reference.

_Example error response_

<!-- tab start `json` -->

```json
// If you specify an invalid user ID of the LINE Official Account bot (400 Bad Request)
{
  "message": "user/group/room Id is not available."
}

// If the module channel isn't linked (attached) (400 Bad Request)
{
  "message": "Specified channel is not detachable"
}
```

<!-- tab end -->

### Acquire Control API 

If the Standby Channel wants to take the initiative (Chat Control), it calls the Acquire Control API.

The channel that was previously an Active Channel will automatically switch to a Standby Channel.

<!-- warning start -->

**Warning**

It isn't necessary to call this API in the currently provided module structure. So, the implementation of this API is optional.

This API is currently used only when the chat initiative switches due to unexpected problems.

<!-- warning end -->

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/chat/{chatId}/control/acquire \
-H 'Content-Type:application/json' \
-H 'Authorization: Bearer {channel access token}' \
-H 'Header specifying the bot user ID:xxxxxx' \
-d '{"expired":true,"ttl":3600}'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/v2/bot/chat/{chatId}/control/acquire`

#### Rate limit 

2,000 requests per second

#### Request headers 

<!-- parameter start (props: required) -->

Content-Type

`application/json`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

`Bearer {channel access token}`

For `{channel access token}`, specify the channel access token of your module channel.

<!-- parameter end -->
<!-- parameter start (props: required) -->

Header specifying the bot's user ID

The user ID of the LINE Official Account bot attached to the module channel.

You can get the user ID of the bot from the response of the [Attach by operation of the module channel provider](https://developers.line.biz/en/reference/partner-docs/#link-attach-by-operation-module-channel-provider) or the [Attached event](https://developers.line.biz/en/reference/partner-docs/#attached-event).

<!-- note start -->

**The specific header will be provided when after participation**

The name (parameter name) of this header is open only to customers who participate in the [LINE Marketplace](https://line-marketplace.com/jp/inquiry) (only available in Japanese).

<!-- note end -->

<!-- parameter end -->

#### Path parameter 

<!-- parameter start (props: required) -->

chatId

The `userId`, `roomId`, or `groupId`

<!-- parameter end -->

#### Request body 

<!-- parameter start (props: optional) -->

expired

Boolean

- `True`: After the time limit (ttl) has passed, the initiative (Chat Control) will return to the Primary Channel. (Default)
- `False`: There's no time limit and the initiative (Chat Control) doesn't change over time.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

ttl

Number

The time it takes for initiative (Chat Control) to return to the Primary Channel (the time that the module channel stays on the Active Channel). The value is specified in seconds. The maximum value is one year (3600 \* 24 \* 365). The default value is `3600` (1 hour).

\* Ignored if the value of `expired` is `false`.

<!-- parameter end -->

#### Response 

Returns a 200 status code on success.

#### Error response 

Returns the following HTTP status code and an error response:

| Code | Description |
| --- | --- |
| `400` | An invalid ID is specified in the `chatId` parameter. |
| `404` | Couldn't take the initiative (Chat Control). Consider these reasons:<ul><li>A user is specified who hasn't added the LINE Official Account attached to the module as a friend.</li><li>A group is specified that the LINE Official Account attached to the module doesn't participate in.</li><li>A multi-person chat is specified that the LINE Official Account attached to the module doesn't participate in.</li></ul> |
| `423` | Another channel has acquired the initiative (Chat Control) within a certain period of time (a few seconds or so). |

For more information, see [Status codes](https://developers.line.biz/en/reference/messaging-api/#status-codes) and [Error responses](https://developers.line.biz/en/reference/messaging-api/#error-responses) in the Messaging API reference.

_Example error response_

<!-- tab start `json` -->

```json
// If you specfy an invalid ID is specified in the chatId parameter (400 Bad Request)
{
  "message": "The value for the 'chatId' parameter is invalid"
}
```

<!-- tab end -->

### Release Control API 

To return the initiative (Chat Control) of Active Channel to Primary Channel, call the Release Control API.

<!-- warning start -->

**Warning**

It isn't necessary to call this API in the currently provided module structure. So, the implementation of this API is optional.

This API is currently used only when the chat initiative switches due to unexpected problems.

<!-- warning end -->

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/bot/chat/{chatId}/control/release \
-H 'Content-Type:application/json' \
-H 'Authorization: Bearer {channel access token}' \
-H 'Header specifying the bot user ID:xxxxxx'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/v2/bot/chat/{chatId}/control/release`

#### Rate limit 

2,000 requests per second

#### Request headers 

<!-- parameter start (props: required) -->

Content-Type

`application/json`

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

`Bearer {channel access token}`

For `{channel access token}`, specify the channel access token of your module channel.

<!-- parameter end -->
<!-- parameter start (props: required) -->

Header specifying the bot's user ID

The user ID of the LINE Official Account bot attached to the module channel.

You can get the user ID of the bot from the response of the [Attach by operation of the module channel provider](https://developers.line.biz/en/reference/partner-docs/#link-attach-by-operation-module-channel-provider) or the [Attached event](https://developers.line.biz/en/reference/partner-docs/#attached-event).

<!-- note start -->

**The specific header will be provided when after participation**

The name (parameter name) of this header is open only to customers who participate in the [LINE Marketplace](https://line-marketplace.com/jp/inquiry) (only available in Japanese).

<!-- note end -->

<!-- parameter end -->

#### Path parameter 

<!-- parameter start (props: required) -->

chatId

The `userId`, `roomId`, or `groupId`

<!-- parameter end -->

#### Response 

Returns a `200` status code on success.

#### Error response 

Returns the following HTTP status code and an error response:

| Code  | Description                                           |
| ----- | ----------------------------------------------------- |
| `400` | An invalid ID is specified in the `chatId` parameter. |

For more information, see [Status codes](https://developers.line.biz/en/reference/messaging-api/#status-codes) and [Error responses](https://developers.line.biz/en/reference/messaging-api/#error-responses) in the Messaging API reference.

_Example error response_

<!-- tab start `json` -->

```json
// If you specfy an invalid ID is specified in the chatId parameter (400 Bad Request)
{
  "message": "The value for the 'chatId' parameter is invalid"
}
```

<!-- tab end -->

### Module channel-specific webhook events 

#### Attached event 

This event indicates that the module channel has been attached to the LINE Official Account. Sent to the webhook URL server of the module channel.

<!-- parameter start -->

timestamp, etc.

See [Common properties](https://developers.line.biz/en/reference/messaging-api/#common-properties).

However, `mode` is fixed to `active`.

<!-- parameter end -->
<!-- parameter start -->

type

String

`module`

<!-- parameter end -->
<!-- parameter start -->

module.type

String

`attached`

<!-- parameter end -->
<!-- parameter start -->

module.botId

String

User ID of the bot on the attached LINE Official Account

<!-- parameter end -->
<!-- parameter start -->

module.scopes

Array of strings

An array of strings indicating the scope permitted by the admin of the LINE Official Account.

<!-- parameter end -->

_Example Attached event_

<!-- tab start `json` -->

```sh
{
  "destination": "U53387d54817...",
  "events": [
    {
      "type": "module",
      "module": {
        "type": "attached",
        "botId": "U53387d54817...",
        "scopes": [
          "message:send",
          "message:receive"
        ]
      },
      "webhookEventId": "01G3GCEEXNWREGSSFVTPYH8465",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1653038594997,
      "mode": "active"
    }
  ]
}
```

<!-- tab end -->

#### Detached event 

This event indicates that the module channel has been detached from the LINE Official Account. Sent to the webhook URL server of the module channel.

<!-- note start -->

**Detach isn't done when you delete the LINE Official Account**

The module channel won't be detached when the LINE Official Account Manager is used to delete the LINE Official Account.

After three months have passed since the operation to delete the account, and all information including the LINE Official Account's analysis data has been completely deleted, the account will automatically be detached.

<!-- note end -->

<!-- parameter start -->

timestamp, etc.

See [Common properties](https://developers.line.biz/en/reference/messaging-api/#common-properties).

However, `mode` is fixed to `active`.

<!-- parameter end -->
<!-- parameter start -->

type

String

`module`

<!-- parameter end -->
<!-- parameter start -->

module.type

String

`detached`

<!-- parameter end -->
<!-- parameter start -->

module.botId

String

Detached LINE Official Account bot user ID

<!-- parameter end -->
<!-- parameter start -->

module.reason

String

Reason for detaching

`bot_deleted`: All information, including analysis data for the LINE Official Account, has been completely deleted.

<!-- parameter end -->

_Example Detached event_

<!-- tab start `json` -->

```sh
{
  "destination": "U5fac33f633e72c192759f09afc41fa28",
  "events": [
    {
      "type": "module",
      "module": {
        "type": "detached",
        "botId": "U5fac33f633e72c192759f09afc41fa28"
      },
      "webhookEventId": "01G4CPSV08QGNT1DWFC4DSWDNP",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1653988977672,
      "mode": "active"
    }
  ]
}
```

<!-- tab end -->

#### Activated event 

This event indicates that the module channel has been switched to Active Channel by calling the Acquire Control API. Sent to the webhook URL server of the module channel.

<!-- note start -->

**Note**

The activated event won't be sent if the validity period specified in the Acquire Control API has expired and the initiative (Chat Control) has been switched.

<!-- note end -->

<!-- parameter start -->

timestamp, etc.

See [Common properties](https://developers.line.biz/en/reference/messaging-api/#common-properties).

However, `mode` is fixed to `active`.

<!-- parameter end -->
<!-- parameter start -->

type

String

`activated`

<!-- parameter end -->
<!-- parameter start -->

chatControl.expireAt

Number

The time limit for maintaining "active."

<!-- parameter end -->

_Example Activated event_

<!-- tab start `json` -->

```sh
  {
  "destination": "U5fac33f633e72c192759f09afc41fa28",
  "events": [
    {
      "type": "activated",
      "chatControl": {
        "expireAt": 1653994422933
      },
      "webhookEventId": "01G4CRJ54J7TT4WN190KKHBXXT",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1653990823058,
      "source": {
        "type": "user",
        "userId": "LUb577ef3cbe..."
      },
      "mode": "active"
    }
  ]
}
```

<!-- tab end -->

#### Deactivated event 

This event indicates that the module channel has been switched to Standby Channel by calling Acquire Control API or Release Control API. Sent to the webhook URL server of the module channel.

<!-- note start -->

**Note**

The deactivated event won't be sent if the validity period specified in the Acquire Control API has expired and the initiative (Chat Control) has been switched.

<!-- note end -->

<!-- parameter start -->

timestamp, etc.

See [Common properties](https://developers.line.biz/en/reference/messaging-api/#common-properties).

However, `mode` is fixed to `active`.

<!-- parameter end -->
<!-- parameter start -->

type

String

`deactivated`

<!-- parameter end -->

_Example Deactivated event_

<!-- tab start `json` -->

```sh
{
  "destination": "U5fac33f633e72c192759f09afc41fa28",
  "events": [
    {
      "type": "deactivated",
      "webhookEventId": "01G4CRJ51100K1D1791KC9J4G4",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1653990822945,
      "source": {
        "type": "user",
        "userId": "LUb577ef3cbe..."
      },
      "mode": "active"
    }
  ]
}
```

<!-- tab end -->

#### botSuspend event 

This event indicates that the LINE Official Account has been suspended (Suspend). Sent to the webhook URL server of the module channel.

When you receive this event, it's recommended that you do the following:

- Display a message such as "This admin screen can't be used because the LINE Official Account is unavailable" on the module channel admin screen, and stop using the admin screen.
- Even if it goes into the paused state, it may return from the paused state (it may receive a botResume event). It is recommended that all information be kept.

<!-- note start -->

**Note**

The botSuspend event isn't sent to the Primary Channel.

If you receive the Detached event after receiving the botSuspend event, it means that the LINE Official Account has stopped using the module channel and canceled the contract.

<!-- note end -->

<!-- parameter start -->

timestamp, etc.

See [Common properties](https://developers.line.biz/en/reference/messaging-api/#common-properties).

However, `mode` is fixed to `active`.

<!-- parameter end -->
<!-- parameter start -->

type

String

`botSuspended`

<!-- parameter end -->

_Example botSuspend event_

<!-- tab start `json` -->

```sh
{
  "destination": "U53387d548170020e6cedef5f41d1e01d",
  "events": [
    {
      "type": "botSuspended",
      "webhookEventId": "01G4CRJ54J7TT4WN190KKHBXXT",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1616390574119,
      "mode": "active"
    }
  ]
}
```

<!-- tab end -->

#### botResumed event 

This event indicates that the LINE Official Account has returned from the suspended state. Sent to the webhook URL server of the module channel.

When you receive this event, it's recommended that you hide the message "This admin page is unavailable due to the LINE Official Account being unavailable" from the module channel admin page and resume using the admin page.

<!-- note start -->

**Note**

The botResumed event isn't sent to the Primary Channel.

<!-- note end -->

<!-- parameter start -->

timestamp, etc.

See [Common properties](https://developers.line.biz/en/reference/messaging-api/#common-properties).

However, `mode` is fixed to `active`.

<!-- parameter end -->
<!-- parameter start -->

type

String

`botResumed`

<!-- parameter end -->

_Example botResumed event_

<!-- tab start `json` -->

```sh
{
  "destination": "U5fac33f633e72c192759f09afc41fa28",
  "events": [
    {
      "type": "botResumed",
      "webhookEventId": "01G4CS8T91R1V1JCE0G43DQND8",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1653991565601,
      "mode": "active"
    }
  ]
}
```

<!-- tab end -->

### Get a list of bots to which the module is attached 

Gets a list of basic information about the bots of multiple LINE Official Accounts that have attached module channels.

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X GET "https://api.line.me/v2/bot/list?limit={limit}&start={continuationToken}" \
-H 'Authorization: Bearer {channel access token}'
```

<!-- tab end -->

#### HTTP request 

`GET https://api.line.me/v2/bot/list?limit={limit}&start={continuationToken}`

#### Rate limit 

2,000 requests per second

#### Request headers 

<!-- parameter start (props: required) -->

Authorization

`Bearer {channel access token}`

For `{channel access token}`, specify the channel access token of your module channel.

<!-- parameter end -->

#### Query parameters 

<!-- parameter start (props: optional) -->

limit

Specify the maximum number of bots that you get basic information from. The default value is `100`.\
Max value: `100`

<!-- parameter end -->
<!-- parameter start (props: optional) -->

start

Value of the continuation token found in the `next` property of the JSON object returned in the response. If you can't get all basic information about the bots in one request, include this parameter to get the remaining array.

<!-- parameter end -->

#### Response 

Returns a JSON object with status code `200` and this information on success.

<!-- parameter start -->

bots

Array

Array of Bot list Item objects representing basic information about the bot.

<!-- parameter end -->
<!-- parameter start -->

bots\[].userId

String

Bot's user ID

<!-- parameter end -->
<!-- parameter start -->

bots\[].basicId

String

Bot's basic ID

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

bots\[].premiumId

String

Bot's [premium ID](https://developers.line.biz/en/glossary/#premium-id). Not included in the response if the premium ID isn't set.

<!-- parameter end -->
<!-- parameter start -->

bots\[].displayName

String

Bot's display name

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

bots\[].pictureUrl

String

Profile image URL. Image URL starting with "https://". Not included in the response if the bot doesn't have a profile image.

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

next

String

Continuation token. Used to get the next array of basic bot information. This property is only returned if there are more unreturned results.

The continuation token expires in 24 hours (86,400 seconds).

<!-- parameter end -->

_Example response_

<!-- tab start `json` -->

```json
{
  "bots": [
    {
      "userId": "Uf2dd6e8b081d2ff9c05c98a8a8b269c9",
      "basicId": "@628...",
      "displayName": "Test01",
      "pictureUrl": "https://profile.line-scdn.net/0hyxytJNAlJldEDQzlatVZAHhIKDoz..."
    },
    {
      "userId": "Ua831d37bfe8232808202b85127663f70",
      "basicId": "@076lu...",
      "displayName": "Test02",
      "pictureUrl": "https://profile.line-scdn.net/0hohnizdyzMEdTECbnVo9PEG9VPiok..."
    },
    {
      "userId": "Ub77ea431fba86f7c159a0c0f5be43d9f",
      "basicId": "@290n...",
      "displayName": "Test03"
    },
    {
      "userId": "Ub8ec80a14e879e9c6833fb4cee0e632b",
      "basicId": "@793j...",
      "displayName": "Test04"
    }
  ]
}
```

<!-- tab end -->

#### Error response 

Returns the following HTTP status code and an error response:

| Code  | Description                                 |
| ----- | ------------------------------------------- |
| `400` | An invalid continuation token is specified. |

For more information, see [Status codes](https://developers.line.biz/en/reference/messaging-api/#status-codes) and [Error responses](https://developers.line.biz/en/reference/messaging-api/#error-responses) in the Messaging API reference.

_Error response example_

<!-- tab start `json` -->

```json
// If you specify an invalid continuation token, such as expired (400 Bad Request)
{
  "message": "Invalid start param"
}
```

<!-- tab end -->
