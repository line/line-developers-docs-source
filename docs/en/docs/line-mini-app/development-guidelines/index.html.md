# LINE MINI App development guidelines

When developing web applications using LIFF, follow these development guidelines.

- [Prohibiting mass requests to the LINE Platform](https://developers.line.biz/en/docs/line-mini-app/development-guidelines/#prohibiting-mass-requests-to-line-platform)
- [Saving logs](https://developers.line.biz/en/docs/line-mini-app/development-guidelines/#save-logs)
- [Deauthorize your app when a user unregisters from your app](https://developers.line.biz/en/docs/line-mini-app/development-guidelines/#deauthorize)

LINE MINI App uses a system provided by LIFF. Therefore, abide by the [LIFF app development guidelines](https://developers.line.biz/en/docs/liff/development-guidelines/) in the LIFF documentation.

<!-- note start -->

**Note**

The basic rules for LINE MINI App development are based on the content described in [Terms and Policies](https://developers.line.biz/en/terms-and-policies/).

<!-- note end -->

## Prohibiting mass requests to the LINE Platform 

Don't over-access LINE MINI Apps via the [LIFF scheme](https://developers.line.biz/en/docs/line-login/using-line-url-scheme/#opening-a-liff-app) (`https://miniapp.line.me/{liffId}`), or send a large number of requests to the [LIFF API](https://developers.line.biz/en/reference/liff/) or the [Service message API](https://developers.line.biz/en/reference/line-mini-app/), for load testing purposes. For load testing LINE MINI Apps, prepare a test environment that doesn't generate a large number of requests to the LINE Platform.

<!-- note start -->

**Note**

If the rate limit is exceeded, `429 Too Many Requests` will be returned and an error will occur.

<!-- note end -->

## Saving logs 

We recommend saving logs for [Service message API](https://developers.line.biz/en/reference/line-mini-app/) requests for a certain period of time so that developers themselves can smoothly investigate the cause and scope of a problem when it occurs.

### Service message API request logs 

We recommend saving the following information in a log, in addition to the [service notification token](https://developers.line.biz/en/reference/line-mini-app/#issue-notification-token-response) `notificationToken` which is included in the response, when making a request to the [Service message API](https://developers.line.biz/en/reference/line-mini-app/).

- Time when API request was made
- Request method
- API endpoint
- [Status codes](https://developers.line.biz/en/reference/line-mini-app/) returned by the LINE Platform

More specifically, save it in a log file using the following format.

| Time when API request was made | Request method | API endpoint | Status code |
| --- | --- | --- | --- |
| Mon, 16 Jul 2021 10:20:23 GMT | POST | `https://api.line.me/message/v3/notifier/send?target=service` | 200 |

<!-- tip start -->

**Additional information that would be useful to keep in log**

Depending on the requirements of the LINE MINI App you're running, the following information, in addition to the above, can be stored for investigation when problems occur.

- Service message API request body
- Response body, other than the service notification token `notificationToken`, returned by the LINE Platform after the API request

<!-- tip end -->

<!-- note start -->

**We don't provide logs**

We don't provide logs of service message API requests, etc. despite inquiries. Logs should be saved by the developers who are developing the LINE MINI Apps themselves.

<!-- note end -->

## Deauthorize your app when a user unregisters from your app 

When a user unregisters from your LINE MINI App, or when a user terminates the link between your app and the LINE app, you must do the following:

1. The permissions that the user has granted to the authorized app must be deauthorized using the [Deauthorize your app to which the user has granted permissions](https://developers.line.biz/en/reference/line-login/#deauthorize) endpoint on behalf of the user.
1. Write what happens when a user unregisters from your app or terminates the link between your app and the LINE app as follows near the function or in the terms and conditions that the user agrees to at the time of registration or authorization.
   - e.g. If you unsubscribe from the service, LY Corporation will be notified that you have unsubscribed and the link between the service and LINE app will be terminated.
   - e.g. If you do this, LY Corporation will be notified and the link between the service and LINE app will be terminated.

The following use cases require deauthorization.

![Steps from linking your account to deauthorize app](https://developers.line.biz/media/line-login/development-guidelines/deauthorize-your-app-en.png)

When a user logs in to the app that integrates LINE Login with their LINE account and [authorize the app](https://developers.line.biz/en/docs/line-login/integrate-line-login/#authorization-process) on the channel consent screen, the target app will appear in **Settings** > **Account** > **Authorized apps** in the LINE app. Deauthorize the app so that the permissions don't remain authorized after the user unregisters from your app.

For more information about how a user can deauthorize the permissions that the user has granted to the app, see [Managing authorized apps](https://developers.line.biz/en/docs/line-login/managing-authorized-apps/) in the LINE Login documentation.
