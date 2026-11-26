# Best practices for preventing HTTP status code 429 errors in the Messaging API

<!-- tip start -->

**Who should read this page**

This page provides technical guidance for operating large LINE Official Accounts with many friends (1 million or more as a guideline) and frequent message deliveries through the Messaging API.

Decide whether you need to apply this guidance if any of the following describes your LINE Official Account:

- Your LINE Official Account is relatively small.
- You mainly use LINE Official Account Manager to send messages.
- You use the Messaging API to send messages only within the [free message allowance](https://developers.line.biz/en/docs/messaging-api/pricing/#examples-of-subscription-plans).

<!-- tip end -->

This page explains how developers and operators of systems that use the Messaging API can prevent and recover from HTTP status code 429 (Too Many Requests). It covers controlling and retrying API requests, checking the number of messages, and checking when and how errors occur.

For more information about identifying the cause and taking basic action, see [Handle HTTP status code 429 errors in the Messaging API](https://developers.line.biz/en/docs/messaging-api/handling-http-429-errors/).

<!-- note start -->

**This guidance assumes access to logs**

This page assumes that you can check your own logs or other records to investigate the circumstances in which HTTP status code 429 occurred. For more information about what to record and precautions to take, see [Record details when HTTP status code 429 occurs](https://developers.line.biz/en/docs/messaging-api/handling-http-429-errors/#record-http-429-errors).

<!-- note end -->

## Take action based on your goal 

Take the following action based on your goal:

| Goal | Reference |
| --- | --- |
| Control the API request rate and number of concurrent operations | [Control API requests](https://developers.line.biz/en/docs/messaging-api/preventing-http-429-errors/#control-api-requests) |
| Check the number of messages available to send and adjust your delivery plan and message volume | [Monitor the number of messages](https://developers.line.biz/en/docs/messaging-api/preventing-http-429-errors/#monitor-message-quota) |
| Design a retry strategy for failed API requests | [Retry requests after you exceed a rate limit or the limit on the number of concurrent operations](https://developers.line.biz/en/docs/messaging-api/preventing-http-429-errors/#retry-rate-limit-errors) |

## Control API requests 

For more information about the rate limit mechanism, scope, and limits for each endpoint, see [Rate limits](https://developers.line.biz/en/reference/messaging-api/#rate-limits) in the Messaging API reference.

<!-- tip start -->

**You can't change the rate limits**

You can't change or relax the Messaging API rate limits for individual channels. Design your system to send API requests within the defined limits.

<!-- tip end -->

Control API requests in these ways:

- [Configure a rate limiter in your app](https://developers.line.biz/en/docs/messaging-api/preventing-http-429-errors/#configure-a-rate-limiter)
- [Control concurrent operations](https://developers.line.biz/en/docs/messaging-api/preventing-http-429-errors/#control-concurrent-operations)

### Configure a rate limiter in your app 

Configure a rate limiter in the app or system that sends API requests. Base the rate limiter on the [token bucket algorithm](https://developers.line.biz/en/reference/messaging-api/#rate-limits-mechanism) and the Messaging API rate limits. Keep the request rate for each endpoint within its rate limit.

<!-- note start -->

**Leave a margin below the rate limit**

Leave a margin below the rate limit. Requests from multiple apps and their arrival times at the LINE Platform can cause you to exceed the limit. This can happen even if you set your rate limiter to the same value as the rate limit.

Control the combined request rate across all sources if multiple apps or systems send requests. Use a shared counter if you need one. Don't rely only on separate controls for each source.

<!-- note end -->

### Control concurrent operations 

Some endpoints have a [limit on the number of concurrent operations](https://developers.line.biz/en/reference/messaging-api/#limit-on-the-number-of-concurrent-operations) for each audience ID (`audienceGroupId`), in addition to a rate limit. In the app or system that sends API requests, manage these operations with a queue or similar mechanism. Keep the total number of jobs queued or running on the LINE Platform within the limit.

Check `jobs[].jobStatus` in the response from the [Get audience data](https://developers.line.biz/en/reference/messaging-api/#get-audience-group) endpoint. Count both queued (`QUEUED`) and running (`WORKING`) jobs.

If you exceed this limit, the Messaging API returns the error message `There are too many running upload jobs for the audience group id.` with HTTP status code 429.

## Retry requests after you exceed a rate limit or the limit on the number of concurrent operations 

Take the following action based on the cause. Then retry the API request:

- Lower the request rate or wait before retrying if you exceeded a rate limit.
- If you exceeded the limit on the number of concurrent operations, wait for jobs to finish and confirm that the number of concurrent operations has fallen below the limit.

<!-- note start -->

**Don't retry requests with errors related to the number of messages in the same way**

Don't retry immediately after you receive the `You have reached your monthly limit.` error. Check the message limit and any temporary reservations. For more information, see [Errors related to the number of messages](https://developers.line.biz/en/docs/messaging-api/handling-http-429-errors/#identify-message-quota-error).

<!-- note end -->

### Set the retry timing based on the cause 

<!-- note start -->

**The Messaging API doesn't return the Retry-After header**

The Messaging API doesn't return the `Retry-After` header. Set the retry timing in the system that sends API requests.

<!-- note end -->

Use your [configured rate limiter](https://developers.line.biz/en/docs/messaging-api/preventing-http-429-errors/#configure-a-rate-limiter) to control retries when a rate limit causes the error. The Messaging API uses the [token bucket algorithm](https://developers.line.biz/en/reference/messaging-api/#rate-limits-mechanism) as the basis for its rate limits. The LINE Platform adds tokens over time.

Don't retry immediately after receiving HTTP status code 429. Lower the request rate to leave a margin below the endpoint's rate limit, and wait for the LINE Platform to replenish tokens before retrying. Add random jitter to the retry interval and, if you continue to receive HTTP status code 429, gradually increase the interval using exponential backoff or a similar method.

If the limit on the number of concurrent operations causes the error, [check the number of queued and running jobs](https://developers.line.biz/en/docs/messaging-api/preventing-http-429-errors/#control-concurrent-operations). Retry when their total falls below the limit.

### Set the maximum number of retries 

HTTP status code `429 Too Many Requests` has [several possible causes](https://developers.line.biz/en/docs/messaging-api/handling-http-429-errors/#identify-the-cause). If the error is related to the number of messages, retrying the request alone may not resolve the error.

Set a maximum number of retries. Use three retries as a guideline. Stop processing if the error continues after the maximum number of retries.

Then investigate the request rate and the number of concurrent operations. Identify and resolve the cause before you retry again.

### Use retry keys with endpoints that send messages 

Specify the `X-Line-Retry-Key` header in the first API request to an endpoint that supports retry keys. Use the same retry key within 24 hours of the first request to prevent duplicate processing.

For more information about supported endpoints and implementation, see [Retry failed API requests](https://developers.line.biz/en/docs/messaging-api/retrying-api-request/).

---

## Considerations for HTTP status code 429 errors 

- The Messaging API doesn't process API requests that return HTTP status code 429. The LINE Platform also doesn't retry them automatically.
- Don't send large numbers of API requests for load testing or functional testing. Don't [send large numbers of messages to the same user](https://developers.line.biz/en/docs/messaging-api/development-guidelines/#prohibiting-mass-transmissions-to-same-user). The LINE Platform may return HTTP status code 429 for requests outside normal use. This can happen even when you stay within the [rate limits](https://developers.line.biz/en/reference/messaging-api/#rate-limits) and [limits on the number of concurrent operations](https://developers.line.biz/en/reference/messaging-api/#limit-on-the-number-of-concurrent-operations). For more information, see [Messaging API development guidelines](https://developers.line.biz/en/docs/messaging-api/development-guidelines/).
- You may not have enough messages available to send near the end of the month. The Messaging API may return HTTP status code 429 in this case. See these sections:
  - [Check the number of messages needed for the delivery](https://developers.line.biz/en/docs/messaging-api/handling-http-429-errors/#check-message-quota-for-recipients)
  - [Check the status of other message deliveries](https://developers.line.biz/en/docs/messaging-api/handling-http-429-errors/#check-ongoing-message-delivery)
