# LIFF app development guidelines

When developing web apps using LIFF, follow these development guidelines.

- [Be sure to securely handle user data](https://developers.line.biz/en/docs/liff/development-guidelines/#liff-development-rules1)
- [Cautions for initializing LIFF apps](https://developers.line.biz/en/docs/liff/development-guidelines/#liff-development-rules2)
- [LIFF app development rules](https://developers.line.biz/en/docs/liff/development-guidelines/#liff-development-rules3)
- [Prohibiting mass requests to the LINE Platform](https://developers.line.biz/en/docs/liff/development-guidelines/#prohibiting-mass-requests-to-line-platform)
- [Deauthorize your app when a user unregisters from your app](https://developers.line.biz/en/docs/liff/development-guidelines/#deauthorize)

LIFF uses a system provided by LINE Login. Therefore, abide by the [LINE Login development guidelines](https://developers.line.biz/en/docs/line-login/development-guidelines/) in the LINE Login documentation.

<!-- note start -->

**Note**

The basic rules for LIFF development are based on the content described in [Terms and Policies](https://developers.line.biz/en/terms-and-policies/).

<!-- note end -->

## Be sure to securely handle user data 

- When using user data in LIFF apps and servers, the LIFF app will be vulnerable to spoofing and other types of attacks if it doesn't properly handle the user data. For more information on how LIFF apps and servers can securely use user data obtained from LIFF apps, see [Using user data in LIFF apps and servers](https://developers.line.biz/en/docs/liff/using-user-profile/).
- LIFF endpoint URLs and URL fragments of LIFF URLs contain sensitive information such as access tokens and user IDs, so be careful of data leakage.

## Cautions for initializing LIFF apps 

See [Important points to consider when initializing the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#initializing-liff-app-notes).

## LIFF app development rules 

- To build a LIFF app as an SPA (single page application), use the [History API](https://html.spec.whatwg.org/multipage/nav-history-apis.html#the-history-interface). LIFF has limited compatibility with routing using fragments.
- When you implement an API that uses any of the device or OS functions listed below, implement the API so that user actions trigger API calls.
  - Getting location information
  - Accessing the camera
  - Accessing the microphone
- Do not track a user with cookies, localStorage, or sessionStorage or link LINE user data with external session information without getting the user's consent.
- During your application's test phase, limit access privileges for the LIFF app through your web app.
- The URL scheme of the LIFF app and any content that is opened in the LIFF app must be **https**. If the URL scheme is http, the content is displayed in [LINE's in-app browser](https://developers.line.biz/en/glossary/#line-iab). In this case, even if the web app has been registered as a LIFF app, it does not function as a LIFF app.

<!-- note start -->

**Use of cookies, localStorage, or sessionStorage in your LIFF app**

You can use cookies, localStorage, or sessionStorage in your LIFF app. However, changes in OS may restrict their use in the future.

<!-- note end -->

## Prohibiting mass requests to the LINE Platform 

Do not access the LIFF app via the [LIFF scheme](https://developers.line.biz/en/docs/line-login/using-line-url-scheme/#opening-a-liff-app) (`https://liff.line.me/{liffId}`) or request a large amount of [LIFF API](https://developers.line.biz/en/reference/liff/) for load testing purposes. For load testing LIFF apps, prepare a test environment that doesn't generate a large number of requests to the LINE Platform.

<!-- note start -->

**Note**

If the rate limit is exceeded, `429 Too Many Requests` will be returned and an error will occur.

<!-- note end -->

## Deauthorize your app when a user unregisters from your app 

When a user unregisters from your LIFF app, or when a user terminates the link between your app and the LINE app, you must do the following:

1. The permissions that the user has granted to the authorized app must be deauthorized using the [Deauthorize your app to which the user has granted permissions](https://developers.line.biz/en/reference/line-login/#deauthorize) endpoint on behalf of the user.
1. Write what happens when a user unregisters from your app or terminates the link between your app and the LINE app as follows near the function or in the terms and conditions that the user agrees to at the time of registration or authorization.
   - e.g. If you unsubscribe from the service, LY Corporation will be notified that you have unsubscribed and the link between the service and LINE app will be terminated.
   - e.g. If you do this, LY Corporation will be notified and the link between the service and LINE app will be terminated.

The following use cases require deauthorization.

![Steps from linking your account to deauthorize app](https://developers.line.biz/media/line-login/development-guidelines/deauthorize-your-app-en.png)

When a user logs in to the app that integrates LINE Login with their LINE account and [authorize the app](https://developers.line.biz/en/docs/line-login/integrate-line-login/#authorization-process) on the channel consent screen, the target app will appear in **Settings** > **Account** > **Authorized apps** in the LINE app. Deauthorize the app so that the permissions don't remain authorized after the user unregisters from your app.

For more information about how a user can deauthorize the permissions that the user has granted to the app, see [Managing authorized apps](https://developers.line.biz/en/docs/line-login/managing-authorized-apps/) in the LINE Login documentation.
