# LINE Ads API development guidelines

Follow the development guidelines below when developing using LINE Ads API:

<!-- table of contents -->

## Prohibiting mass requests to the LINE Platform 

Don't send a large number of requests to the LINE Platform for the purpose of load testing or operation testing.

Don't send requests beyond the specified rate limits for any purpose. For more information about rate limits, see [Ad Tech API documentation](https://ads.line.me/public-docs/certificated-ad-tech-general-partner) and [Data Provider API documentation](https://ads.line.me/public-docs/data-general-partner).

<!-- note start -->

**Note**

If you send requests exceeding the rate limit, you will receive an error message saying, `429 Too Many Requests`.

<!-- note end -->

## Prohibiting requests for non-existent IDs 

When sending a request, don't specify a non-existent ID (`Ad account ID`, `Ad ID`, etc.).

## Saving logs 

We recommend saving logs for requests to API for a certain period of time so that developers themselves can smoothly investigate the cause and scope of a problem when it occurs.

### Logs for LINE Ads API request 

We recommend saving the following information as a log when making a request to LINE Ads API:

- Time of API request
- Request method
- API endpoint
- Status code returned in response by the LINE Platform

More specifically, save it in a log file using the following format.

| Time of API request | Request method | API Endpoint | Status code |
| --- | --- | --- | --- |
| Mon, 05 Jul 2022 08:14:35 GMT | GET | `https://ads.line.me/api/v3/codes/ssps` | 200 |
