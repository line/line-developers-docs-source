# LINE Login development guidelines

When developing web apps using LINE Login, follow these development guidelines.

**Prohibited matters**

- [Prohibiting mass requests to the LINE Platform](https://developers.line.biz/en/docs/line-login/development-guidelines/#prohibiting-mass-requests-to-line-platform)

**Required matters**

- [Deauthorize your app when a user unregisters from your app](https://developers.line.biz/en/docs/line-login/development-guidelines/#deauthorize)

**Recommended matters**

- [Saving logs](https://developers.line.biz/en/docs/line-login/development-guidelines/#save-logs)

<!-- note start -->

**Note**

The basic rules for LINE Login development are based on the content described in [Terms and Policies](https://developers.line.biz/en/terms-and-policies/).

<!-- note end -->

## Prohibited matters 

### Prohibiting mass requests to the LINE Platform 

Don't send a large number of [authorization requests](https://developers.line.biz/en/docs/line-login/integrate-line-login/#making-an-authorization-request) or [LINE Login API](https://developers.line.biz/en/reference/line-login/) requests to the LINE Platform for load testing purposes. For load testing web apps, prepare a test environment that doesn't generate a large number of requests to the LINE Platform.

<!-- note start -->

**Note**

If the rate limit is exceeded, `429 Too Many Requests` will be returned and an error will occur.

<!-- note end -->

## Required matters 

### Deauthorize your app when a user unregisters from your app 

When a user unregisters from your app (website, smartphone app, etc.) that integrates LINE Login, or when a user terminates the link between your app and the LINE app, you must do the following:

1. The permissions that the user has granted to the authorized app must be deauthorized using the [Deauthorize your app to which the user has granted permissions](https://developers.line.biz/en/reference/line-login/#deauthorize) endpoint on behalf of the user.
1. Write what happens when a user unregisters from your app or terminates the link between your app and the LINE app as follows near the function or in the terms and conditions that the user agrees to at the time of registration or authorization.
   - e.g. If you unsubscribe from the service, LY Corporation will be notified that you have unsubscribed and the link between the service and LINE app will be terminated.
   - e.g. If you do this, LY Corporation will be notified and the link between the service and LINE app will be terminated.

The following use cases require deauthorization.

![Steps from linking your account to deauthorize app](https://developers.line.biz/media/line-login/development-guidelines/deauthorize-your-app-en.png)

When a user logs in to the app that integrates LINE Login with their LINE account and [authorize the app](https://developers.line.biz/en/docs/line-login/integrate-line-login/#authorization-process) on the channel consent screen, the target app will appear in **Settings** > **Account** > **Authorized apps** in the LINE app. Deauthorize the app so that the permissions don't remain authorized after the user unregisters from your app.

For more information about how a user can deauthorize the permissions that the user has granted to the app, see [Managing authorized apps](https://developers.line.biz/en/docs/line-login/managing-authorized-apps/) in the LINE Login documentation.

## Recommended matters 

### Saving logs 

We recommend saving logs for [Authorization requests](https://developers.line.biz/en/docs/line-login/integrate-line-login/#making-an-authorization-request) and [LINE Login API](https://developers.line.biz/en/reference/line-login/) requests for a certain period of time so that developers themselves can smoothly investigate the cause and scope of a problem when it occurs.

#### Authorization request logs 

We recommend saving the following information as a log when making an [Authorization request](https://developers.line.biz/en/docs/line-login/integrate-line-login/#making-an-authorization-request).

- Time when authorization request was made
- Parameter of the authorization request

More specifically, save it in a log file using the following format.

| Time when authorization request was made | Parameter of the authorization request |
| --- | --- |
| Mon, 16 Jul 2021 10:20:10 GMT | `https://access.line.me/oauth2/v2.1/authorize?response_type=code&client_id=xxxxxxxxxx...` |

#### Authorization code or error response 

We recommend saving the following information as a log when you receive an [Authorization code](https://developers.line.biz/en/docs/line-login/integrate-line-login/#receiving-the-authorization-code) or an [Error response](https://developers.line.biz/en/docs/line-login/integrate-line-login/#receiving-an-error-response) through an [Authorization request](https://developers.line.biz/en/docs/line-login/integrate-line-login/#making-an-authorization-request).

- Time when the authorization code or error response was received
- Request method
- Log of authorization codes or error responses

More specifically, save it in a log file using the following format.

| Time when response was received | Request Method | Log of authorization codes or error responses |
| --- | --- | --- |
| Mon, 16 Jul 2021 10:20:20 GMT | GET | `/callback?code=Zfl2WjsWcn2XBBWApcty&state=n5B9b9FR2BWjloDzEskZMmGysITRTYpjLkM6oD5qfmA` |

#### Time logs for LINE Login API request 

We recommend saving the following information as a log when making a [LINE Login API](https://developers.line.biz/en/reference/line-login/) request.

- Request ID (`x-line-request-id`) of the [Response headers](https://developers.line.biz/en/reference/line-login/#response-headers)
- Time when API request was made
- Request method
- API endpoint
- [Status codes](https://developers.line.biz/en/reference/line-login/#status-codes) returned by the LINE Platform

More specifically, save it in a log file using the following format.

| Request ID (`x-line-request-id`) | Time when API request was made | Request method | API endpoint | Status code |
| --- | --- | --- | --- | --- |
| 8d48c8577e739b9c | Mon, 16 Jul 2021 10:20:22 GMT | POST | `https://api.line.me/oauth2/v2.1/token` | 200 |

<!-- tip start -->

**Additional information that would be useful to keep in log**

Depending on the requirements of the web app you're running, the following information, in addition to the above, can be stored for investigation when problems occur.

- LINE Login API request body
- Response body returned by the LINE Platform after the API request

<!-- tip end -->

<!-- note start -->

**We don't provide logs**

We don't provide logs of authorization requests or logs of LINE Login API requests, etc. despite inquiries. Logs should be saved by the developers who are developing web apps using LINE Login.

<!-- note end -->
