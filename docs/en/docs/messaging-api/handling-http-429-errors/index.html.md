# Handle HTTP status code 429 errors in the Messaging API

This page explains how to identify the cause of HTTP status code 429 from the error message in the response body and take basic action.

## `429 Too Many Requests` in the Messaging API 

The Messaging API returns HTTP status code `429 Too Many Requests` when you exceed a rate limit, a message limit, or another limit. For example:

- You exceed an API rate limit.
- You exceed the limit on the number of concurrent operations.
- You exceed the number of free messages.
- You exceed the target limit for additional messages.

The action you need to take before retrying depends on the cause of `429 Too Many Requests`. First, [identify the cause](https://developers.line.biz/en/docs/messaging-api/handling-http-429-errors/#identify-the-cause).

<!-- note start -->

**The Messaging API doesn't process requests that return HTTP status code 429**

- An endpoint that sends messages doesn't send messages to any recipient in the request.
- An endpoint that gets user information or performs another operation doesn't get the information or perform the operation.
- The LINE Platform doesn't automatically retry an API request that returns HTTP status code 429.

<!-- note end -->

<!-- tip start -->

**Preventing 429 Too Many Requests**

For more information about preventing `429 Too Many Requests` in your implementation and operations, see [Best practices for preventing HTTP status code 429 errors in the Messaging API](https://developers.line.biz/en/docs/messaging-api/preventing-http-429-errors/).

<!-- tip end -->

## Record details when HTTP status code 429 occurs 

To help identify the cause of HTTP status code 429 errors, record the following information when you make API requests.

<!-- note start -->

**Investigate errors using your own logs**

LY Corporation doesn't provide logs for requests to the Messaging API. Save the logs you need to identify the cause and prevent another occurrence. Use those logs to investigate the issue. For more information, see [Save logs](https://developers.line.biz/en/docs/messaging-api/development-guidelines/#save-logs).

<!-- note end -->

<!-- warning start -->

**Restrict log access permissions to the minimum necessary**

Grant only the minimum necessary access permissions for logs that contain protected information, such as request or response bodies.

<!-- warning end -->

**Information to record**

- Date and time of the API request
- Information about the source channel, such as its channel ID
- HTTP method and endpoint for the request
- [Status code](https://developers.line.biz/en/reference/messaging-api/#status-codes) in the response
- `message` in the response body
- `x-line-request-id` in the [response headers](https://developers.line.biz/en/reference/messaging-api/#response-headers)

**Information to record when needed**

- Request rate and number of concurrent operations
- Number of retries and retry intervals, if you retried the request
- [Target limit](https://developers.line.biz/en/reference/messaging-api/#get-quota) and [usage](https://developers.line.biz/en/reference/messaging-api/#get-consumption) when the Messaging API returned HTTP status code 429

## Identify the cause 

The Messaging API returns `429 Too Many Requests` for reasons other than exceeding a rate limit. It's difficult to identify the cause from the HTTP status code alone.

To identify the cause, first check the `message` property (the error message) in the response body.

The same error message can indicate several causes. Also check the status of your API requests and message usage.

The following table lists common error messages in the `message` property when the Messaging API returns `429 Too Many Requests`:

| Error message | Description |
| --- | --- |
| `The API rate limit has been exceeded. Try again later.` | The Messaging API may return this error if you send many API requests in a short period. For more information, see [Rate limit errors](https://developers.line.biz/en/docs/messaging-api/handling-http-429-errors/#identify-rate-limit-error). |
| `You have reached your monthly limit.` | The Messaging API may return this error if you've sent many messages in the current month or have multiple deliveries in progress. For more information, see [Errors related to the number of messages](https://developers.line.biz/en/docs/messaging-api/handling-http-429-errors/#identify-message-quota-error). |
| `There are too many running upload jobs for the audience group id.` | The Messaging API may return this error if you repeatedly upload data to the same audience in a short period. For more information, see [Errors related to the limit on the number of concurrent operations](https://developers.line.biz/en/docs/messaging-api/handling-http-429-errors/#identify-concurrent-operations-error). |

### Rate limit errors 

```
The API rate limit has been exceeded. Try again later.
```

This error occurs when you exceed an endpoint's rate limit. Check the following and take the appropriate action:

| Item | Details |
| --- | --- |
| What to check | Check the request rate for the endpoint that returned the error, taking into account the [rate limit mechanism and limits](https://developers.line.biz/en/reference/messaging-api/#rate-limits). |
| How to retry | Before retrying the API request, wait for a while and lower the request rate to stay within the rate limit. |

### Errors related to the number of messages 

```
You have reached your monthly limit.
```

This error occurs when you [send messages at any time](https://developers.line.biz/en/docs/messaging-api/sending-messages/#send-messages-at-any-time) without enough messages available for the delivery.

You may not have enough messages available for the current delivery because of the monthly limit and the number of messages you've already used. Messages temporarily reserved for another delivery can also reduce the number available.

#### Identify the cause of the message shortage 

Check the following information to identify why you don't have enough messages available:

- [Check the status of other message deliveries](https://developers.line.biz/en/docs/messaging-api/handling-http-429-errors/#check-ongoing-message-delivery)
- [Check the target limit and usage for the current month](https://developers.line.biz/en/docs/messaging-api/handling-http-429-errors/#check-message-quota-and-consumption)
- [Check the number of messages needed for the delivery](https://developers.line.biz/en/docs/messaging-api/handling-http-429-errors/#check-message-quota-for-recipients)
- [Check your pricing plan and the target limit for additional messages](https://developers.line.biz/en/docs/messaging-api/handling-http-429-errors/#check-message-plan-and-additional-quota)

##### Check the status of other message deliveries 

Check whether another narrowcast delivery or a delivery from [LINE Official Account Manager](https://manager.line.biz/) was in progress when the error occurred.

The LINE Platform temporarily reserves the planned number of messages for these deliveries until it finalizes the actual number of messages sent. It releases reservations for unsent messages after the delivery finishes.

Another delivery in progress doesn't necessarily mean that temporary reservations caused the error. Also check the target limit and usage for the current month and the number of messages needed for the current delivery.

##### Check the target limit and usage for the current month 

Use these endpoints to check the target limit and usage for the current month:

- [Get the target limit for sending messages this month](https://developers.line.biz/en/reference/messaging-api/#get-quota)
- [Get number of messages sent this month](https://developers.line.biz/en/reference/messaging-api/#get-consumption)

If `type` in the target limit response is `limited`, estimate the number of messages available to send by subtracting `totalUsage` in the usage response from `value` in the target limit response. If `type` is `none`, the target limit response doesn't include `value`, so you can't calculate the number of messages remaining this way.

`totalUsage` may include messages temporarily reserved for planned deliveries. These reservations can make `totalUsage` higher than the actual number of messages sent and temporarily reduce the number of messages available to send.

##### Check the number of messages needed for the delivery 

When you send push, multicast, or broadcast messages, keep enough messages available to send to **every recipient**. The Messaging API returns an error if the number of messages available to send is lower than the number of recipients. The Messaging API doesn't send any messages.

For example, the Messaging API returns an error in these cases:

- You specify more recipients in a [multicast message](https://developers.line.biz/en/reference/messaging-api/#send-multicast-message) than the number of messages available to send.
- You send a [push message](https://developers.line.biz/en/reference/messaging-api/#send-push-message) to a group that has more recipients than the number of messages available to send.
- You send a [broadcast message](https://developers.line.biz/en/reference/messaging-api/#send-broadcast-message), but your LINE Official Account has more friends than the number of messages available to send.

<!-- note start -->

**Sending narrowcast messages**

The LINE Platform may reserve messages equal to your LINE Official Account's [target reach](https://developers.line.biz/en/glossary/#target-reach) for [narrowcast messages](https://developers.line.biz/en/reference/messaging-api/#send-narrowcast-message), regardless of the actual number of recipients. The number of messages needed depends on the limit object settings.

Specify one of the following options in the limit object for narrowcast messages. The Messaging API can then send messages within the specified maximum or the number of messages available to send. You don't need enough messages for all recipients. The Messaging API selects the recipients at random.

- Set the maximum number of messages in `limit.max` to a value that doesn't exceed the number of messages available to send.
- Set `limit.upToRemainingQuota` to `true`.

If you set both `limit.upToRemainingQuota` and `limit.forbidPartialDelivery` to `true`, the Messaging API cancels the entire delivery when `limit.max` or the number of messages available to send would restrict delivery to only some recipients. It doesn't send messages to a randomly selected subset. For more information, see [Controlling the maximum number of messages to send with limit objects](https://developers.line.biz/en/docs/messaging-api/sending-messages/#maximum-send-numbers-control).

<!-- note end -->

##### Check your pricing plan and the target limit for additional messages 

In [LINE Official Account Manager](https://manager.line.biz/), check the number of free messages in your current pricing plan and whether your plan supports additional messages. If your plan supports additional messages, also check the target limit for additional messages.

For more information about pricing plans and additional messages, see [Pricing system](https://developers.line.biz/en/docs/messaging-api/pricing/#pricing-system).

#### Take action based on the situation 

Take the following action based on what you find:

| Situation | Action and retry timing |
| --- | --- |
| Temporary reservations for another delivery may be causing the error. | Wait for the earlier delivery to finish. Then check the number of messages available to send again. Retry the API request if enough messages are available for the current delivery. |
| Temporary reservations aren't affecting the number of messages available to send, or the earlier delivery has finished, but you still don't have enough messages for the current delivery. | Reduce the number of recipients, or review your [pricing plan](https://developers.line.biz/en/docs/messaging-api/pricing/#pricing-system) or [target limit for additional messages](https://www.lycbiz.com/jp/manual/OfficialAccountManager/account-settings_plan/?list=7171) (only available in Japanese). You can also wait until you can send free messages again next month. For narrowcast messages, also consider [Controlling the maximum number of messages to send with limit objects](https://developers.line.biz/en/docs/messaging-api/sending-messages/#maximum-send-numbers-control). Don't retry until enough messages are available for the delivery. |

### Errors related to the limit on the number of concurrent operations 

```
There are too many running upload jobs for the audience group id.
```

This error occurs when you exceed the limit on the number of concurrent operations for an audience ID (`audienceGroupId`). Check the following and take the appropriate action:

| Item | Details |
| --- | --- |
| What to check | Check whether the endpoint has a [limit on the number of concurrent operations](https://developers.line.biz/en/reference/messaging-api/#limit-on-the-number-of-concurrent-operations). Use the [Get audience data](https://developers.line.biz/en/reference/messaging-api/#get-audience-group) endpoint for the affected audience, and count jobs whose `jobs[].jobStatus` is `QUEUED` (queued) or `WORKING` (running). |
| How to retry | Wait for jobs to finish. Retry the API request when the total number of queued and running jobs falls below the limit. |

## Prevent HTTP status code 429 from recurring 

For more information about controlling requests and designing retries, see [Best practices for preventing HTTP status code 429 errors in the Messaging API](https://developers.line.biz/en/docs/messaging-api/preventing-http-429-errors/).
