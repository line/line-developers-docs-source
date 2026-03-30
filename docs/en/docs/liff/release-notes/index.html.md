# Release notes

## LIFF version and release date

Beginning with LIFF v2.2.0, LIFF will follow [Semantic Versioning](https://semver.org/) (SemVer). For more information, see [LIFF versioning policy](https://developers.line.biz/en/docs/liff/versioning-policy/).

<!-- tip start -->

**CDN path**

We provide two CDN paths: fixed and edge. If you use the CDN edge path, you are always up-to-date with the latest MINOR and PATCH updates. If you use the CDN fixed path, you need to manually update your URL with each update.

For more information, see [LIFF SDK (sdk.js) update policy](https://developers.line.biz/en/docs/liff/versioning-policy/#update-policy) in the LIFF versioning policy documentation.

<!-- tip end -->

### Current version

When you use the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you can always use the latest features of LIFF v2.

[LIFF v2.28.0: March 24, 2026](https://developers.line.biz/en/docs/liff/release-notes/#liff-v2-28-0)

### Version list 

When you use the CDN fixed path (e.g. `https://static.line-scdn.net/liff/edge/versions/2.28.0/sdk.js`), you can use the features of the specified LIFF version.

:toc{maxDepth=2}

2026/03/24

## LIFF v2.28.0 released 

We've released LIFF v2.28.0.

In LIFF v2.28.0, we've made the following change.

### We've added the `liff.requestFriendship()` method which prompts the user to add the LINE Official Account as a friend 

We've added the [`liff.requestFriendship()`](https://developers.line.biz/en/reference/liff/#request-friendship) method which displays a subwindow that prompts the user to add the LINE Official Account as a friend, or to unblock it.

For more information, see [Requesting the user to add the LINE Official Account as a friend or unblock it](https://developers.line.biz/en/docs/liff/developing-liff-apps/#request-friendship) in the LIFF documentation.

### How to update to LIFF v2.28.0 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.28.0.

If you're using an npm package, you can update to v2.28.0 by executing either `npm install @line/liff@2.28.0` or `yarn add @line/liff@2.28.0`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2025/11/17

## LIFF v2.27.3 released 

We've released LIFF v2.27.3.

In LIFF v2.27.3, we've made changes to the internal behavior of the LIFF SDK. There is no change in features.

### How to update to LIFF v2.27.3 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.27.3.

If you're using an npm package, you can update to v2.27.3 by executing either `npm install @line/liff@2.27.3` or `yarn add @line/liff@2.27.3`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2025/09/08

## LIFF v2.27.2 released 

We've released LIFF v2.27.2.

In LIFF v2.27.2, we've made the following improvement.

### A warning message will now appear in a browser console if the URL of the page where the `liff.init()` method is executed doesn't start with the endpoint URL 

The [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app) method will only work on URLs that are the same as the endpoint URL (\*), or on URLs that are at a lower level than the endpoint URL. Therefore, if the `liff.init()` method is executed on any other URL, some LIFF app features, such as the [multi-tab view](https://developers.line.biz/en/docs/liff/overview/#multi-tab-view), may not work properly.

To help developers identify this issue more easily, a warning message will now appear in a console if the URL of the page where the `liff.init()` method is executed doesn't start with the endpoint URL.

For example, if the endpoint URL of a LIFF app is `https://example.com/path1/path2/` and the URL where the `liff.init()` method is executed is `https://example.com/path1/`, the following warning message will appear:

```
liff.init() was called with a current URL that is not related to the endpoint URL.
https://example.com/path1/ is not under https://example.com/path1/path2/
```

If you see the warning message above, consider changing the endpoint URL to `https://example.com/` or `https://example.com/path1/`. Changing to these URLs guarantees the `liff.init()` method works correctly.

\* The URL specified in the **Endpoint URL** of the LINE Developers Console.

### How to update to LIFF v2.27.2 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.27.2.

If you're using an npm package, you can update to v2.27.2 by executing either `npm install @line/liff@2.27.2` or `yarn add @line/liff@2.27.2`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2025/07/24

## LIFF v2.27.1 released 

We've released LIFF v2.27.1.

In LIFF v2.27.1, we've made changes to the internal behavior of the LIFF SDK. There is no change in features.

### How to update to LIFF v2.27.1 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.27.1.

If you're using an npm package, you can update to v2.27.1 by executing either `npm install @line/liff@2.27.1` or `yarn add @line/liff@2.27.1`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2025/6/25

## LIFF v2.27.0 released 

We've released LIFF v2.27.0.

In LIFF v2.27.0, we've added the following feature.

### You can now get a list of scopes for which the user has agreed to grant permission 

We've added the [`liff.permission.getGrantedAll()`](https://developers.line.biz/en/reference/liff/#permission-get-granted-all) method to the LIFF SDK. Using the `liff.permission.getGrantedAll()` method allows you to get all scopes for which the user has agreed to grant permission.

```javascript
liff.permission.getGrantedAll().then((scopes) => {
  // ["profile", "chat_message.write", "openid", "email"]
  console.log(scopes);
});
```

The scopes that you can get with this method are as follows:

- [`profile`](https://developers.line.biz/en/docs/liff/registering-liff-apps/#registering-liff-app)
- [`chat_message.write`](https://developers.line.biz/en/docs/liff/registering-liff-apps/#registering-liff-app)
- [`openid`](https://developers.line.biz/en/docs/liff/registering-liff-apps/#registering-liff-app)
- [`email`](https://developers.line.biz/en/docs/liff/registering-liff-apps/#registering-liff-app)

<!-- tip start -->

**Difference between liff.getContext() and liff.permission.getGrantedAll()**

The [`liff.getContext()`](https://developers.line.biz/en/reference/liff/#get-context) method gets a list of scopes for the LIFF app (\*).

On the other hand, the `liff.permission.getGrantedAll()` method gets a list of scopes for which the user has agreed to grant permission among the scopes for the LIFF app.

\* The scopes specified in the "Scope" section under the **LIFF** tab in a LINE Login channel

<!-- tip end -->

For more information, see [liff.permission.getGrantedAll()](https://developers.line.biz/en/reference/liff/#permission-get-granted-all) in the LIFF API reference.

### How to update to LIFF v2.27.0 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.27.0.

If you're using an npm package, you can update to v2.27.0 by executing either `npm install @line/liff@2.27.0` or `yarn add @line/liff@2.27.0`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2025/5/26

## LIFF v2.26.1 released 

We've released LIFF v2.26.1.

In LIFF v2.26.1, we've fixed the following bugs.

### We've fixed a bug where accessing a LIFF URL caused the LIFF app to navigate to an unintended secondary redirect URL 

In a LIFF app, when accessing the [LIFF URL](https://developers.line.biz/en/glossary/#liff-url), the LIFF app first navigates to the primary redirect URL and then to the secondary redirect URL. There was a bug in the conditions that append a slash (`/`) to the end of the path of the secondary redirect URL, which caused the LIFF app to navigate to an unintended secondary redirect URL.

#### Conditions that append a slash (`/`) to the end of the path of the secondary redirect URL 

In LIFF v2.26.0 or earlier, a slash (`/`) is appended to the end of the path of the secondary redirect URL if any of the following conditions are met:

- The endpoint URL ends with a slash (`/`)
- `liff.state` ends with a slash (`/`)

For example, if the LIFF app's endpoint URL is `https://example.com/?key=value/` and the LIFF URL being accessed is `https://liff.line.me/1234567890-AbcdEfgh/foo/bar`, the correct secondary redirect URL is `https://example.com/foo/bar?key=value/`.

However, since the condition "the endpoint URL ends with a slash (`/`)" is met in this situation, the LIFF app actually navigates to `https://example.com/foo/bar/?key=value/` which has a slash (`/`) added to the end of the path.

| Correct secondary redirect URL | Actual secondary redirect URL |
| --- | --- |
| https://example.com/foo/bar?key=value/ | https://example.com/foo/bar<b style="color: red">/</b>?key=value/ |

In LIFF v2.26.1, we've applied a fix so that a slash (`/`) is appended to the end of the secondary redirect URL if any of the following conditions are met. As a result, LIFF apps now navigate to the correct secondary redirect URL.

- The endpoint URL's path ends with a slash (`/`)
- `liff.state`'s path ends with a slash (`/`)

For more information about the behavior when accessing a LIFF URL, see [Behaviors from accessing the LIFF URL to opening the LIFF app](https://developers.line.biz/en/docs/liff/opening-liff-app/#redirect-flow) in the LIFF documentation.

### We've fixed a bug where the `liff.init()` method replaced POST requests with GET requests in the browser's session history when excluding credential information 

In LIFF apps, when the [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app) method is resolved, credential information such as access tokens is excluded from URLs. At this time, there was a bug in some environments where POST requests were replaced with GET requests in the browser's session history.

In LIFF v2.26.1, we've fixed the bug so that the correct history is retained.

#### Example of a POST request in the browser's session history being replaced by a GET request 

For example, suppose you interact with a LIFF app in the following order:

1. Open a LIFF app
1. Navigate to `/path1` with a POST request
1. Navigate to `/path2` with a GET request
1. Click the browser's back button

In this situation, the LIFF app is expected to navigate to `/path1` with a POST request, but in some environments, the LIFF app navigates to `/path1` with a GET request.

### How to update to LIFF v2.26.1 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.26.1.

If you're using an npm package, you can update to v2.26.1 by executing either `npm install @line/liff@2.26.1` or `yarn add @line/liff@2.26.1`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2025/4/22

## LIFF v2.26.0 released 

We've released LIFF v2.26.0.

In LIFF v2.26.0, we've fixed the following bug.

### We've fixed a bug where an incorrect error message was returned when a certain method is executed in an external browser while not logged in 

There was a bug where an incorrect error message was returned when the following methods are executed in an [external browser](https://developers.line.biz/en/glossary/#external-browser) while the user isn't logged in.

- The [`liff.getProfile()`](https://developers.line.biz/en/reference/liff/#get-profile) method
- The [`liff.getFriendship()`](https://developers.line.biz/en/reference/liff/#get-friendship) method
- The [`liff.sendMessages()`](https://developers.line.biz/en/reference/liff/#send-messages) method

In LIFF v2.26.0, we've fixed the bug so that the correct error message is returned.

| Error message before the fix | Error message after the fix |
| --- | --- |
| `LiffId is not found.` | `Need access_token for api call, Please login first` |

### How to update to LIFF v2.26.0 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.26.0.

If you're using an npm package, you can update to v2.26.0 by executing either `npm install @line/liff@2.26.0` or `yarn add @line/liff@2.26.0`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2024/12/13

## LIFF v2.25.1 released 

We've released LIFF v2.25.1.

In LIFF v2.25.1, we've made changes to the internal behavior of the LIFF SDK. There is no change in features.

### How to update to LIFF v2.25.1 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.25.1.

If you're using an npm package, you can update to v2.25.1 by executing either `npm install @line/liff@2.25.1` or `yarn add @line/liff@2.25.1`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2024/11/12

## LIFF v2.25.0 released 

We've released LIFF v2.25.0.

In LIFF v2.25.0, we've made the following change.

### We've changed the URLs generated by the `liff.permanentLink.createUrlBy()` method

As announced on [November 11, 2024](https://developers.line.biz/en/news/2024/11/11/liff-server-update/), we've made changes to the LIFF server side to ensure that URL processing complies with [RFC 3986](https://datatracker.ietf.org/doc/html/rfc3986). As a result, the processing results for characters and codes in the queries of the URLs generated by the [`liff.permanentLink.createUrlBy()`](https://developers.line.biz/en/reference/liff/#permanent-link-create-url-by) method have changed as follows:

| Characters and codes | Before change | After change (current) |
| -------------------- | ------------- | ---------------------- |
| `+`                  | `+`           | `%2B`                  |
| `*`                  | `*`           | `%2A`                  |
| `%7E`                | `%7E`         | `~`                    |
| `%20`                | `+`           | `%20`                  |
| `;` \*               | Deleted       | `%3B`                  |

\* The result of processing `;` is only applied when `;` is at the end of the query.

For more information, see [As of November 11, 2024, the results of URLs generated by some LIFF features changed in certain versions of the LINE app and LIFF SDK](https://developers.line.biz/en/news/2024/11/11/liff-server-update/).

### How to update to LIFF v2.25.0 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.25.0.

If you're using an npm package, you can update to v2.25.0 by executing either `npm install @line/liff@2.25.0` or `yarn add @line/liff@2.25.0`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2024/7/23

## LIFF v2.24.0 released 

We've released LIFF v2.24.0.

In LIFF v2.24.0, we've added the following feature.

### We've added the `liff.getAppLanguage()` method which gets the language setting of the LINE app running the LIFF app 

We've added the [`liff.getAppLanguage()`](https://developers.line.biz/en/reference/liff/#get-app-language) method which gets the language setting of the LINE app running the LIFF app.

The LIFF SDK has a similar method, [`liff.getLanguage()`](https://developers.line.biz/en/reference/liff/#get-language). You can use the `liff.getLanguage()` method to get the language setting of the environment running the LIFF app, but in some iOS environments there is a bug where the language setting of the OS is reflected instead of the language setting of the LINE app.

Therefore, with the addition of the `liff.getAppLanguage()` method, the `liff.getLanguage()` method has been deprecated. Use the `liff.getAppLanguage()` method from now on.

For more information about the language setting of the LINE app, see [Changing the LINE app language setting](https://help.line.me/line/?contentId=20007465&lang=en) in the Help Center.

### How to update to LIFF v2.24.0 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.24.0.

If you're using an npm package, you can update to v2.24.0 by executing either `npm install @line/liff@2.24.0` or `yarn add @line/liff@2.24.0`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2024/2/15

## LIFF v2.23.2 released 

We've released LIFF v2.23.2.

In LIFF v2.23.2, we've made the following improvement and a bug fix.

### The cause of the LIFF SDK loading failures can now be checked in a log and `LiffError` 

When the LIFF SDK fails to load, the cause can now be checked in a console log or in the `cause` property of the [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-errors) object.

### We've fixed a bug that caused some parameters of the URL fragment to be unintentionally removed when initializing a LIFF app 

In LIFF apps, for security reasons, the following string-keyed parameters are removed from the URL fragment of the [primary redirect URL](https://developers.line.biz/en/docs/liff/opening-liff-app/#redirect-flow) at the time the [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app) method is resolved.

- `access_token`
- `client_id`
- `context_token`
- `feature_token`
- `id_token`

There was a bug that caused parameters whose keys were strings ending with these strings (e.g. `prefix_access_token`) to be unintentionally removed from the URL fragment. In v2.23.2, we've fixed the bug so that only parameters keyed by the above strings are be removed.

### How to update to LIFF v2.23.2 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.23.2.

If you're using an npm package, you can update to v2.23.2 by executing either `npm install @line/liff@2.23.2` or `yarn add @line/liff@2.23.2`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2024/1/15

## LIFF v2.23.1 released 

<!-- note start -->

**Updated on January 23, 2024**

Due to a bug that caused a decrease in the reading accuracy of 2D codes in some devices, the [`liff.scanCodeV2()`](https://developers.line.biz/en/reference/liff/#scan-code-v2) method has been reverted to the state before this release. There is no need to update the LIFF SDK or modify the code in your LIFF apps. We apologize for any inconvenience.

<!-- note end -->

We've released LIFF v2.23.1.

In LIFF v2.23.1, we've made the following improvement. We've also made changes to the internal behavior of the LIFF SDK to improve security.

### We've improved the reading accuracy of the `liff.scanCodeV2()` method 

We've improved the reading accuracy of 2D codes in the [`liff.scanCodeV2()`](https://developers.line.biz/en/reference/liff/#scan-code-v2) method. Note that the reading accuracy depends on the camera performance of a device, so there may not be a noticeable improvement depending on the user's device.

This improvement is automatically applied to all LIFF apps, so there is no need to update the LIFF SDK or modify the code in your LIFF apps.

### How to update to LIFF v2.23.1 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.23.1.

If you're using an npm package, you can update to v2.23.1 by executing either `npm install @line/liff@2.23.1` or `yarn add @line/liff@2.23.1`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2023/11/30

## LIFF v2.23.0 released 

We've released LIFF v2.23.0.

In LIFF v2.23.0, we've made changes to the internal behavior of the LIFF SDK. There is no change in features.

### How to update to LIFF v2.23.0 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.23.0.

If you're using an npm package, you can update to v2.23.0 by executing either `npm install @line/liff@2.23.0` or `yarn add @line/liff@2.23.0`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2023/10/2

## LIFF v2.22.4 released 

We've released LIFF v2.22.4.

In LIFF v2.22.4, we've made changes to the internal behavior of the LIFF SDK. We've also made the following change and fix.

### Due to the intra-group reorganization, we've changed the company name and copyright of the LIFF SDK and open source projects 

As announced on [October 2, 2023](https://developers.line.biz/en/news/2023/10/02/merger-announcement/), due to the intra-group reorganization, LINE Corporation became LY Corporation. With this, we've changed the company name and copyright of the LIFF SDK and the following open source projects:

- [LIFF starter app](https://github.com/line/line-liff-v2-starter)
- [LIFF Playground](https://github.com/line/liff-playground)
- [Create LIFF App](https://github.com/line/create-liff-app)
- [LIFF Inspector](https://github.com/line/liff-inspector)
- [LIFF Mock](https://github.com/line/liff-mock)

### We've fixed a bug where an error might not be returned correctly when the `liff.permission.requestAll()` method failed to execute 

There was a bug where an error might not be returned correctly when the [`liff.permission.requestAll()`](https://developers.line.biz/en/reference/liff/#permission-request-all) method failed to execute. This bug was fixed in LIFF v2.22.4 so that an error would be returned correctly.

### How to update to LIFF v2.22.4 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.22.4.

If you're using an npm package, you can update to v2.22.4 by executing either `npm install @line/liff@2.22.4` or `yarn add @line/liff@2.22.4`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2023/8/24

## LIFF v2.22.3 released 

We've released LIFF v2.22.3.

In LIFF v2.22.3, we've made changes to the internal behavior of the LIFF SDK. There is no change in features.

### How to update to LIFF v2.22.3 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.22.3.

If you're using an npm package, you can update to v2.22.3 by executing either `npm install @line/liff@2.22.3` or `yarn add @line/liff@2.22.3`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2023/6/27

## LIFF v2.22.2 released 

We've released LIFF v2.22.2.

In LIFF v2.22.2, we've made the following improvements and a bug fix.

### We've improved the auto login process on external browsers on Android 

As announced on [July 6, 2022](https://developers.line.biz/en/news/2022/07/06/release-liff-2-20-3/#android-external-browser-20220706), starting with LIFF v2.20.3, an alert was displayed after [auto login](https://developers.line.biz/en/docs/line-login/integrate-line-login/#line-auto-login) as a temporary measure to solve a bug that auto login on [external browsers](https://developers.line.biz/en/glossary/#external-browser) on Android didn't work properly.

On LINE for Android version 13.10.0, the auto login process on external browsers will be improved, so that the temporary measure is no longer required. As a result, the alert displayed after auto login will no longer be displayed in LIFF v2.22.2 or later.

Note that even if the LIFF SDK version of your LIFF app is v2.22.2 or later, the alert will continue to be displayed if the user's version of LINE for Android is earlier than 13.10.0.

<table>
  <thead>
    <tr>
      <th></th>
      <th>LIFF v2.20.3 - v2.22.1</th>
      <th>LIFF v2.22.2 or later</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>LINE for Android version earlier than 13.10.0</th>
      <td>Display the alert</td>
      <td>Display the alert</td>
    </tr>
    <tr>
      <th>LINE for Android version 13.10.0 or later</th>
      <td>Display the alert</td>
      <td>Not display the alert</td>
    </tr>
  </tbody>
</table>

### The LIFF SDK npm package can now be imported in non-browser environments 

The LIFF SDK npm package can now be imported in non-browser environments such as Node.js.

### We've fixed a bug where an invalid URL would be opened after login when executing the `liff.login()` method with a URL with no query parameter specified in the redirectUri property on external browsers on Android 

On external browsers on Android, when executing the [`liff.login()`](https://developers.line.biz/en/reference/liff/#login) method with a URL with no query parameter specified in the `redirectUri` property, an invalid URL was opened after login.

This bug was fixed in LIFF v2.22.2 so that the correct URL would be opened after login.

<table>
  <tbody>
    <tr>
      <th>Example of a URL specified in the <code>redirectUri</code> property</th>
      <td><code>https://example.com/path</code></td>
    </tr>
    <tr>
      <th>Example of an invalid URL opened after login</th>
      <td><code>https://example.com/path&liffIsEscapedFromApp=true</code></td>
    </tr>
    <tr>
      <th>Example of the correct URL after login</th>
      <td><code>https://example.com/path?liffIsEscapedFromApp=true</code></td>
    </tr>
  </tbody>
</table>

### How to update to LIFF v2.22.2 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.22.2.

If you're using an npm package, you can update to v2.22.2 by executing either `npm install @line/liff@2.22.2` or `yarn add @line/liff@2.22.2`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2023/5/24

## LIFF v2.22.1 released 

We've released LIFF v2.22.1.

In LIFF v2.22.1, we've refactored the LIFF SDK. Also, we've made the following fix.

### We've fixed the TypeScript type definitions for LIFF API modules in the pluggable SDK 

We've fixed the TypeScript type definitions for LIFF API modules in the [pluggable SDK](https://developers.line.biz/en/docs/liff/pluggable-sdk/).

The LIFF API modules for which TypeScript type definitions have been fixed and the details are as follows:

| LIFF API module | Detail |
| --- | --- |
| `@line/liff/get-id-token` | Corrected `getIdToken` to `getIDToken`. |
| `@line/liff/get-decoded-id-token` | Corrected `getDecodedIdToken` to `getDecodedIDToken`. |

### How to update to LIFF v2.22.1 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.22.1.

If you're using an npm package, you can update to v2.22.1 by executing either `npm install @line/liff@2.22.1` or `yarn add @line/liff@2.22.1`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2023/3/29

## LIFF v2.22.0 released 

We've released LIFF v2.22.0.

In LIFF v2.22.0, the following feature has been added.

### We've added the pluggable SDK feature that can reduce the LIFF SDK file size by up to about 34% 

In the npm package of the LIFF SDK, we've added the pluggable SDK feature that allows you to choose which LIFF APIs to include in the LIFF SDK.

By including only the LIFF APIs used by your LIFF app, you can reduce the LIFF SDK file size by up to about 34%. As a result, you can improve the display speed of your LIFF app.

#### How to use the pluggable SDK 

First, import the `liff` object from `@line/liff/core`. Note that it's different from `@line/liff`, which is the conventional source for importing the `liff` object.

```js
import liff from "@line/liff/core";
```

This `liff` object differs from the conventional `liff` object in that it contains only the following properties and methods:

- [`liff.id`](https://developers.line.biz/en/reference/liff/#id) property
- [`liff.ready`](https://developers.line.biz/en/reference/liff/#ready) property
- [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app) method
- [`liff.getVersion()`](https://developers.line.biz/en/reference/liff/#get-version) method
- [`liff.use()`](https://developers.line.biz/en/reference/liff/#use) method

To use LIFF APIs other than those listed above, import the corresponding modules. In the following example, the corresponding modules are imported for the [`liff.getOS()`](https://developers.line.biz/en/reference/liff/#get-os) method and the [`liff.getLanguage()`](https://developers.line.biz/en/reference/liff/#get-language) method:

```js
import liff from "@line/liff/core";
import GetOS from "@line/liff/get-os";
import GetLanguage from "@line/liff/get-language";
```

Next, pass the imported LIFF API modules to the `liff.use()` method to active the LIFF APIs. Since the LIFF API modules are defined as classes, you need to pass the instances to the `liff.use()` method.

Once the LIFF APIs are activated, you can use the LIFF APIs.

```js
import liff from "@line/liff/core";
import GetOS from "@line/liff/get-os";
import GetLanguage from "@line/liff/get-language";

liff.use(new GetOS());
liff.use(new GetLanguage());

liff.init({
  liffId: "123456-abcedfg",
});

liff.getOS();
liff.getLanguage();
```

For more information on the pluggable SDK, see [Pluggable SDK](https://developers.line.biz/en/docs/liff/pluggable-sdk/) in the LIFF documentation.

<!-- tip start -->

**Using the conventional LIFF SDK**

You can use the conventional LIFF SDK. There is no change in how to use the LIFF SDK.

```js
// The conventional liff object
import liff from "@line/liff";

// The liff object in the pluggable SDK
import liff from "@line/liff/core";
```

<!-- tip end -->

2022/12/13

## LIFF v2.21.4 released 

We've released LIFF v2.21.4.

### We've officially released the LIFF SDK npm package 

We've officially released the LIFF SDK npm package, which has been available on a trial basis since [July 2020](https://developers.line.biz/en/news/2020/07/01/published-liff-npm-package/).

The LIFF SDK npm packages earlier than v2.21.4 are still available as before. There is no change in usage.

For more information on the LIFF SDK npm package, see [Use the npm package](https://developers.line.biz/en/docs/liff/developing-liff-apps/#use-npm-package) in the LIFF documentation.

### How to update to LIFF v2.21.4 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.21.4.

If you're using an npm package, you can update to v2.21.4 by executing either `npm install @line/liff@2.21.4` or `yarn add @line/liff@2.21.4`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2022/11/10

## LIFF v2.21.3 released 

We've released LIFF v2.21.3.

In LIFF v2.21.3, we've fixed the following bug.

### We've fixed a bug where an error would occur when importing the npm package of the LIFF SDK as an ES module 

There was a bug where an error `Uncaught ReferenceError: require is not defined` would occur when importing the npm package of the LIFF SDK as an ES module.

This bug was fixed in LIFF v2.21.3 so that even in the above case, an error wouldn't occurred.

### How to update to LIFF v2.21.3 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.21.3.

If you're using an npm package, you can update to v2.21.3 by executing either `npm install @line/liff@2.21.3` or `yarn add @line/liff@2.21.3`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2022/10/12

## LIFF v2.21.2 released 

We've released LIFF v2.21.2.

In LIFF v2.21.2, we've refactored the LIFF SDK to improve the stability of the LIFF SDK. There is no change in features.

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.21.2.

If you're using an npm package, you can update to v2.21.2 by executing either `npm install @line/liff@2.21.2` or `yarn add @line/liff@2.21.2`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2022/9/5

## LIFF v2.21.1 released 

We've released LIFF v2.21.1.

In LIFF v2.21.1, we've refactored the LIFF SDK. There is no change in features.

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.21.1.

If you're using an npm package, you can update to v2.21.1 by executing either `npm install @line/liff@2.21.1` or `yarn add @line/liff@2.21.1`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2022/8/4

## LIFF v2.21.0 released 

We've released LIFF v2.21.0.

In LIFF v2.21.0, we've added and improved the following features:

- [The text displayed by the LIFF SDK now supports multiple languages](https://developers.line.biz/en/docs/liff/release-notes/#i18n-20220804)
- [The language of the text displayed by the LIFF SDK can now be specified](https://developers.line.biz/en/docs/liff/release-notes/#liff-i18n-setLang-20220804)
- [We've fixed a bug where the `liff.init()` method could succeed with an invalid LIFF ID](https://developers.line.biz/en/docs/liff/release-notes/#liff-init-20220804)
- [The Typescript type definition for profile information retrieved by the `liff.getProfile()` method is now available](https://developers.line.biz/en/docs/liff/release-notes/#liff-get-profile-20220804)

### The text displayed by the LIFF SDK now supports multiple languages 

The text displayed by the LIFF SDK now supports multiple languages. This means that each text displayed by the LIFF SDK will be displayed in the user's language obtained from [`navigator.language`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/language).

However, at this time, no translations have been applied, so all of the text will be displayed in English. Translation will be applied gradually.

### The language of the text displayed by the LIFF SDK can now be specified 

We've added the [`liff.i18n.setLang()`](https://developers.line.biz/en/reference/liff/#i18n-set-lang) method, through which you can specify the language of the text displayed by the LIFF SDK. With the `liff.i18n.setLang()` method, the text of the LIFF SDK will be displayed in a specified language, regardless of the users's language.

```js
liff.i18n.setLang("en");
```

Text with no translation isn't affected by this method.

For more information, see [liff.i18n.setLang()](https://developers.line.biz/en/reference/liff/#i18n-set-lang) in the LIFF API reference.

### We've fixed a bug where the `liff.init()` method could succeed with an invalid LIFF ID 

There was a bug where the [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app) could succeed with an invalid LIFF ID. In LIFF v2.21.0, this bug was fixed so that the `liff.init()` method fails with an invalid LIFF ID.

### The Typescript type definition for profile information retrieved by the `liff.getProfile()` method is now available 

In the npm package of the LIFF SDK, the Typescript type definition for [profile information](https://developers.line.biz/en/glossary/#profile-information) retrieved by the `liff.getProfile()` method is now available. You can import the `Profile` type from the `@liff/get-profile` package.

```ts
import { Profile } from "@liff/get-profile";
```

2022/7/6

## LIFF v2.20.3 released 

We've released LIFF v2.20.3.

In LIFF v2.20.3, we've fixed the following bug.

### An alert is now displayed after auto login as a temporary measure to solve a bug that auto login on external browsers on Android doesn't work properly 

There were instances where auto login on [external browsers](https://developers.line.biz/en/glossary/#external-browser) on Android didn't work properly. As a temporary measure, the following alert is now displayed after auto login on external browsers on Android:

```
Login successfully!
```

We plan to improve the display of the alert in a future update of the LIFF SDK.

### How to update to LIFF v2.20.3 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), LIFF will automatically update to v2.20.3.

If you're using an npm package, update to v2.20.3 by executing either `npm install @line/liff@2.20.3` or `yarn add @line/liff@2.20.3`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2022/6/8

## LIFF v2.20.2 released 

We've released LIFF v2.20.2.

In LIFF v2.20.2, we've made internal improvements.

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.20.2.

If you're using an npm package, you can update to v2.20.2 by executing either `npm install @line/liff@2.20.2` or `yarn add @line/liff@2.20.2`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2022/5/24

## LIFF v2.20.1 released 

<!-- note start -->

**Added on May 25, 2022**

The problem that the npm package for LIFF v2.20.1 can't be installed due to a bug on the npm side has been resolved.

For more information, see [the npm status page](https://status.npmjs.org/incidents/4zkt80fxq1nb).

<!-- note end -->

We've released LIFF v2.20.1.

In LIFF v2.20.1, we've made the following improvement.

### An error is now returned when executing the liff.scanCodeV2() method in an external browser without login 

To execute the [`liff.scanCodeV2()`](https://developers.line.biz/en/reference/liff/#scan-code-v2) method, user login is required.

In LIFF v2.19.1 or earlier, when executing the `liff.scanCodeV2()` method in an [external browser](https://developers.line.biz/en/glossary/#external-browser) without login, a sub-window will open and show a blank page. Also, the `Promise` will remain pending.

In LIFF 2.20.1, the sub-window will no longer open in the above case. Also, the `Promise` will be rejected and [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-errors) will be passed.

For more information on `liff.scanCodeV2()` method, see [liff.scanCodeV2()](https://developers.line.biz/en/reference/liff/#scan-code-v2) in the LIFF API reference.

<!-- note start -->

**LIFF v2.20.0 has been deprecated**

LIFF v2.20.0 has been [deprecated](https://developers.line.biz/en/glossary/#deprecated) due to a bug where some users using an external browser on Android can't log in. If you are using LIFF v2.20.0, update to LIFF v2.20.1.

<!-- note end -->

2022/4/18

## LIFF v2.19.1 released 

<!-- note start -->

** Added on April 25, 2022**

As previously announced, we've released LIFF Inspector and LIFF Mock today. For more information, see the news from April 25, 2022, [LIFF Inspector and LIFF Mock released](https://developers.line.biz/en/news/2022/04/25/liff-plugin/).

<!-- note end -->

We've released LIFF v2.19.1.

In LIFF v2.19.1, the following feature has been added.

### We've added the LIFF plugin feature that can extend the LIFF SDK 

We've added the LIFF plugin feature introduced in the session entitled "[For Improvement of Developer Experience of All LIFF App Developers](https://linedevday.linecorp.com/2021/en/sessions/142/)" at LINE DEVELOPER DAY 2021, held last November.

LIFF plugin is a feature to extend the LIFF SDK. Using a LIFF plugin, you can add your own APIs to the LIFF SDK or change the behavior of LIFF APIs.

Also, as previously announced, the following LIFF plugins are now available:

- [LIFF Inspector](https://developers.line.biz/en/docs/liff/release-notes/#liff-inspector-20220418)
- [LIFF Mock](https://developers.line.biz/en/docs/liff/release-notes/#liff-mock-20220418)

#### LIFF Inspector 

LIFF Inspector is a LIFF plugin to debug your LIFF app. Using LIFF Inspector, you can debug your LIFF app with [Chrome DevTools](https://developer.chrome.com/docs/devtools/) on a different PC than the device on which you are running the LIFF app.

#### LIFF Mock 

LIFF Mock is a LIFF plugin to make testing your LIFF app easy. Using LIFF Mock, you can add the mock mode to the LIFF SDK. In the mock mode, your LIFF app is independent of the LIFF server and the LIFF API returns mock data. Therefore, you can perform unit testing or load testing more easily.

For more information on LIFF plugin, see [LIFF plugin](https://developers.line.biz/en/docs/liff/liff-plugin/) in the LIFF documentation.

2022/3/22

## LIFF v2.19.0 released 

We've released LIFF v2.19.0.

In LIFF v2.19.0, we've made internal improvements.

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.19.0.

If you're using an npm package, you can update to v2.19.0 by executing either `npm install @line/liff@2.19.0` or `yarn add @line/liff@2.19.0`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2022/2/14

## LIFF v2.18.2 released 

We've released LIFF v2.18.2.

In LIFF v2.18.2, the following improvements have been made:

- [An alert to encourage users to update LINE will be displayed on LINE for iOS or iPadOS version 12.0.0](https://developers.line.biz/en/docs/liff/release-notes/#liff-send-messages-2022-02-14)
- [We've fixed a bug where scanning a 2D code encoded in UTF-8 with the liff.scanCodeV2() method would cause character corruption](https://developers.line.biz/en/docs/liff/release-notes/#scan-code-v2-2022-02-14)
- [We've fixed a bug where the correct permanent link couldn't be obtained when passing a URL containing a percent-encoded path to the liff.permanentLink.createUrlBy() method](https://developers.line.biz/en/docs/liff/release-notes/#permanent-link-create-url-by-2022-02-14)

### An alert to encourage users to update LINE will be displayed on LINE for iOS or iPadOS version 12.0.0 

As announced on [January 14, 2022](https://developers.line.biz/en/news/2022/01/14/liff-outage/), there was a bug where the [`liff.sendMessages()`](https://developers.line.biz/en/reference/liff/#send-messages) didn't work properly and returned an error with status code `403` under certain conditions. Updating the user's LINE version to 12.0.1 or later will resolve the bug.

In order to encourage users to update to the fixed version of LINE, an alert will be displayed if an error with status code `403` occurs when executing the `liff.sendMessages()` method on LINE for iOS or iPadOS version 12.0.0.

The alerts that will be displayed is as follows:

![LINEアプリをLINE 12.0.1以降にアップデートしてください。Please update your LINE app to LINE 12.0.1 or later.](https://developers.line.biz/media/news/liff-send-messages-v2-18-2.png)

### We've fixed a bug where scanning a 2D code encoded in UTF-8 with the liff.scanCodeV2() method would cause character corruption 

We've fixed a bug where scanning a 2D code encoded in UTF-8 with the [`liff.scanCodeV2()`](https://developers.line.biz/en/reference/liff/#scan-code-v2) method would cause character corruption.

This bug fix is automatically applied to all LIFF apps, so there is no need to update the LIFF SDK or modify the code in your LIFF apps.

### We've fixed a bug where the correct permanent link couldn't be obtained when passing a URL containing a percent-encoded path to the liff.permanentLink.createUrlBy() method 

We've fixed a bug where passing a URL containing a [percent-encoded](https://en.wikipedia.org/wiki/Percent-encoding) path to the [`liff.permanentLink.createUrlBy()`](https://developers.line.biz/en/reference/liff/#permanent-link-create-url-by) method would return an incorrect permanent link or cause an error with status code `500`.

This bug fix is automatically applied to all LIFF apps, so there is no need to update the LIFF SDK or modify the code in your LIFF apps.

### How to update to LIFF v2.18.2 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you'll automatically update LIFF to v2.18.2.

If you're using an npm package, you can update to v2.18.2 by executing either `npm install @line/liff@2.18.2` or `yarn add @line/liff@2.18.2`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2021/12/21

## LIFF v2.18.1 released 

We've released LIFF v2.18.1.

In LIFF v2.18.1, the following bugs have been fixed.

### Fixed a bug in TypeScript that caused an error when building 

We've fixed a bug in LIFF v2.18.0, where using TypeScript to build codes containing [URI action](https://developers.line.biz/en/docs/messaging-api/actions/#uri-action) in [Message objects](https://developers.line.biz/en/reference/messaging-api/#message-objects) caused an error.

#### Target methods 

- [`liff.sendMessages()`](https://developers.line.biz/en/reference/liff/#send-messages)
- [`liff.shareTargetPicker()`](https://developers.line.biz/en/reference/liff/#share-target-picker)

### How to update to LIFF v2.18.1

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you will automatically be updated to v2.18.1.

If you're using an npm package, you can update to v2.18.1 by executing either `npm install @line/liff@2.18.1` or `yarn add @line/liff@2.18.1`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk).

2021/12/9

## LIFF v2.18.0 released 

We've released LIFF v2.18.0.

In LIFF v2.18.0, the following feature has been added.

### It's now possible to get the permanent link of any page in the LIFF app 

We've added the [`liff.permanentLink.createUrlBy()`](https://developers.line.biz/en/reference/liff/#permanent-link-create-url-by) method, through which you can get permanent link of any page in the LIFF app.

With the [`liff.permanentLink.createUrl()`](https://developers.line.biz/en/reference/liff/#permanent-link-create-url) method, you can only get the permanent link of the current page. But with the `liff.permanentLink.createUrlBy()` method, you can get the permanent link of any page in the LIFF app, in addition to the current page.

In addition, with the `liff.permanentLink.createUrl()` method, in order to get a permanent link with a query parameter added, you need to have executed the [`liff.permanentLink.setExtraQueryParam()`](https://developers.line.biz/en/reference/liff/#permanent-linke-set-extra-query-param) method in advance. But with the `liff.permanentLink.createUrlBy()` method, you can specify the query parameter you want to add at the same time that you execute the method. Also, the `liff.permanentLink.createUrlBy()` method isn't affected by the `liff.permanentLink.setExtraQueryParam()` method.

#### Difference between `liff.permanentLink.createUrl()` method and `liff.permanentLink.createUrlBy()` method 

||`liff.permanentLink.createUrl()`|`liff.permanentLink.createUrlBy()`|
|---|---|---|
|The LIFF app page that the permanent link can be obtained|The current page|Any page|
|How to add any query parameter to a permanent link|Execute the `liff.permanentLink.setExtraQueryParam()` method in advance|Specify when you execute the `liff.permanentLink.createUrlBy()` method|
|Return value|String|`Promise` object|

#### Sample code of the `liff.permanentLink.createUrlBy()` method 

```javascript
// For example, if the endpoint URL of the LIFF app is https://example.com/path1?q1=v1
// and its LIFF ID is 1234567890-AbcdEfgh
liff.permanentLink
  .createUrlBy('https://example.com/path1?q1=v1')
  .then((permanentLink) => {
    // https://liff.line.me/1234567890-AbcdEfgh
    console.log(permanentLink);
  });

liff.permanentLink
  .createUrlBy('https://example.com/path1/path2?q1=v1&q2=v2')
  .then((permanentLink) => {
    // https://liff.line.me/1234567890-AbcdEfgh/path2?q=2=v2
    console.log(permanentLink);
  });
```

<!-- note start -->

**The liff.permanentLink.createUrl() method may be deprecated in the next major version update**

Due to technical issues, the `liff.permanentLink.createUrl()` method may be deprecated in the next major version update. To get the permanent link of the current page, we recommend using `liff.permanentLink.createUrlBy()` method.

<!-- note end -->

For more information, see [liff.permanentLink.createUrlBy()](https://developers.line.biz/en/reference/liff/#permanent-link-create-url-by) in the LIFF API reference.

2021/11/11

## LIFF v2.17.0 released 

We've released LIFF v2.17.0.

In LIFF v2.17.0, the following bug has been fixed.

### We've fixed a bug where executing the `liff.openWindow()` method in LINE for iOS would open URLs with unintended query parameters added to the end of the URL fragment 

If the `url` property doesn't contain a query parameter but contains a URL fragment, executing the [`liff.openWindow()`](https://developers.line.biz/en/reference/liff/#open-window) method in LINE for iOS would open URLs with unintended query parameters added to the end of the URL fragment.

This bug was fixed in LIFF v2.17.0 so that even in the above case, the correct URL would be opened.

#### Examples of URL opened when executing the `liff.openWindow()` method 

| LIFF SDK version | `url` property | URL opened |
| ---- | ---- | ---- |
| v2.16.1 | `https://example.com#URL-fragment` | `https://example.com#URL-fragment?is_liff_external_open_window=false` |
| v2.17.0 | `https://example.com#URL-fragment` | `https://example.com#URL-fragment` |

For more information on the `liff.openWindow()` method, see [liff.openWindow()](https://developers.line.biz/en/reference/liff/#open-window) in the LIFF API reference.

2021/10/26

## LIFF v2.16.1 released 

We've released LIFF v2.16.1.

In LIFF v2.16.1, the following bugs have been fixed.

### We've fixed the bug that caused the file size to become enlarged in the CDN version of LIFF v2.14.0 or later 

Due to an internal source code change in [LIFF v2.14.0](https://developers.line.biz/en/docs/liff/release-notes/#liff-v2-14-0), the CDN version of LIFF v2.14.0 or later had a bug that caused the file size to become enlarged. This bug has been fixed in LIFF v2.16.1 so that the file size isn't enlarged.

### We've fixed the bug that caused an error when building a project using webpack v5 

[Node.js polyfill has been removed from webpack v5.](https://webpack.js.org/blog/2020-10-10-webpack-5-release/#automatic-nodejs-polyfills-removed) Accordingly, if you use the npm version of LIFF v2.16.0 or earlier in a project using webpack v5, an error will occur during the build and the following message will be displayed.

```
Module not found: Error: Can't resolve 'crypto' in 'node_modules/js-crypto-env/dist'

BREAKING CHANGE: webpack < 5 used to include polyfills for node.js core modules by default.
This is no longer the case. Verify if you need this module and configure a polyfill for it.

If you want to include a polyfill, you need to:
- add a fallback 'resolve.fallback: { "crypto": require.resolve("crypto-browserify") }'
- install 'crypto-browserify'
If you don't want to include a polyfill, you can use an empty module like this:
resolve.fallback: { "crypto": false }
```

This is because the implementation in LIFF v2.16.0 or earlier depended on Node.js polyfill within the LIFF SDK. In LIFF v2.16.1, the implementation doesn't depend on Node.js polyfill, so the above error no longer occurs.

#### Using the npm version of LIFF v2.16.0 or earlier in a project using webpack v5 

To fix the bug while maintaining the same LIFF SDK version, you need to install Node.js polyfill and configure `webpack.config.js`.

First, install Node.js polyfill, `crypto-browserify` and `stream-browserify`.

```bash
# For npm
$ npm install crypto-browserify stream-browserify

# For Yarn
$ yarn add crypto-browserify stream-browserify
```

Next, set the `resolve.fallback` of the `webpack.config.js` as shown below:

```js
module.exports = {
  resolve: {
    fallback: {
      crypto: require.resolve('crypto-browserify'),
      stream: require.resolve('stream-browserify'),
    },
  },
};
```

<br>

### How to update to LIFF v2.16.1 

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), you will automatically be updated to v2.16.1.

If you're using an npm package, you can update to v2.16.1 by executing either `npm install @line/liff@2.16.1` or `yarn add @line/liff@2.16.1`.

For more information on integrating the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk).

2021/10/12

## LIFF v2.16.0 released 

We've released LIFF v2.16.0.

In LIFF v2.16.0, the following features have been added.

### The share target picker now has an option to control whether to send to multiple recipients or just one 

The `isMultiple` property has been added to the `liff.shareTargetPicker()` method. By setting the `isMultiple` property, the user can now control whether or not to allow selection of multiple message recipients in the target picker.

If you set the `isMultiple` property to `true`, the user can select multiple message recipients in the target picker. If you set it to `false`, the user can select only one friend as the message recipient. The default value is `true`.

|  `isMultiple` value  |  Available target recipients |  Available number of selection  |
| ---- | ---- | ---- |
|  `true`  |  Groups, friends, chats |  Can select multiple recipients |
|  `false`  |  Friend  |  Can select only 1 recipient  |

<!-- note start -->

**Setting isMultiple to false doesn't guarantee that the message will be sent to only one friend**

Even if you set the `isMultiple` property to `false`, you can still send a message to multiple users by calling the share target picker multiple times, or by re-sharing the same message to different recipients. To strictly allow a user to send a message to one friend only once, add a restriction when implementing the LIFF app.

Here's an example of sending a message containing a URL and restricting access to the URL.
1. Give the URL a unique token and send the message.
2. When the URL in the message is accessed, the server side verifies the token and restricts access by multiple users.

<!-- note end -->

<!-- note start -->

**We don't retrieve the number of people to whom a user has sent a message using the share target picker**

In order to protect user privacy, we neither collect nor provide information on how many people received a message from a user through the share target picker.

<!-- note end -->

**Sample code with the `isMultiple` property added to the `liff.shareTargetPicker()` method:**

```js
if (liff.isApiAvailable('shareTargetPicker')) {
  liff.shareTargetPicker(
      [
        {
          type: "text",
          text: "Hello, World!",
        },
      ],
      {
        isMultiple: true,
      }
    )
    .then(function (res) {
      if (res) {
        // succeeded in sending a message through TargetPicker
        console.log(`[${res.status}] Message sent!`)
      } else {
        const [majorVer, minorVer] = (liff.getLineVersion() || "").split('.');
        if (parseInt(majorVer) == 10 && parseInt(minorVer) < 11) {
          // LINE 10.3.0 - 10.10.0
          // Old LINE will access here regardless of user's action
          console.log('TargetPicker was opened at least. Whether succeeded to send message is unclear')
        } else {
          // LINE 10.11.0 -
          // sending message canceled
          console.log('TargetPicker was closed!')
        }
      }
    }).catch(function (error) {
      // something went wrong before sending a message
      console.log('something wrong happen')
    })
}
```

For more information, see [liff.shareTargetPicker()](https://developers.line.biz/en/reference/liff/#share-target-picker) in the LIFF API reference.

2021/10/01

## LIFF v1 has been discontinued on October 1, 2021 

As announced on [September 17, 2021](https://developers.line.biz/en/news/2021/09/17/liff-v1-discontinue/), October 1, 2021 marks the [end-of-life](https://developers.line.biz/en/glossary/#end-of-life) for LIFF v1.

However, since the [Server API](https://developers.line.biz/en/reference/liff-server/) is managed on a different schedule than that of LIFF v1, it won't be impacted by this discontinuation.

### Target version

LIFF v1

<!-- warning start -->

**If you're using LIFF v1, migrate to LIFF v2**

For more information on migrating to LIFF v2, see [Migrate to LIFF v2](https://developers.line.biz/en/news/2021/04/05/liff-v1-deprecated/#migrate-to-v2) in the news from [April 5, 2021](https://developers.line.biz/en/news/2021/04/05/liff-v1-deprecated/).

<!-- warning end -->

### Scheduled date of discontinuation

October 1, 2021

### Impact

Gradually, you won't be able to refer to the LIFF SDK URL (`https://d.line-scdn.net/liff/1.0/sdk.js`) or use the [LIFF v1 API](https://developers.line.biz/en/reference/liff-v1/).

LINE will continue to improve the quality of its services for its customers. Thank you for your understanding.

2021/09/30

## LIFF v2.15.0 released 

We've released LIFF v2.15.0.

In LIFF v2.15.0, the following features have been added.

- [The 2D code reader feature has been added](https://developers.line.biz/en/docs/liff/release-notes/#liff-scan-code-v2-2021-09-30)
- [The option of automatically executing the `liff.login()` method when initializing LIFF apps in external browsers has been added](https://developers.line.biz/en/docs/liff/release-notes/#liff-init-auto-login-2021-09-30)

### The 2D code reader feature has been added 

The [`liff.scanCodeV2()`](https://developers.line.biz/en/reference/liff/#scan-code-v2) method, which can launch a 2D code reader within a LIFF app, has been added.

Due to technical problems, [`liff.scanCode()`](https://developers.line.biz/en/reference/liff/#scan-code) isn't available for use on LINE for iOS version 9.19.0 or later, or on external browsers, but with [`liff.scanCodeV2()`](https://developers.line.biz/en/reference/liff/#scan-code-v2), you can now launch a 2D code reader even on the newest version of LINE for iOS, and on external browsers.

<!-- note start -->

**The operation specification of liff.scanCodeV2()**

`liff.scanCodeV2()` internally uses an external library called [jsQR](https://github.com/cozmo/jsQR).
Therefore, the 2D code reader to be launched when the `liff.scanCodeV2()` method is executed depends on the operation specification of [jsQR](https://github.com/cozmo/jsQR). Libraries used may be updated or changed without notice.

<!-- note end -->

<!-- note start -->

**liff.scanCode() method deprecated**

The traditional `liff.scanCode()` method has been [deprecated](https://developers.line.biz/en/glossary/#deprecated). We recommend using the `liff.scanCodeV2()` method for implementing a 2D code reader.

<!-- note end -->

#### Implementing a 2D code reader with `liff.scanCodeV2()` 

Implementing a 2D code reader using `liff.scanCodeV2()` is the same as that of `liff.scanCode()`. Turn on **Scan QR** from the LIFF tab on the [LINE Developers Console](https://developers.line.biz/console/) before following these steps to implement `liff.scanCodeV2()`.

<br>

###### `liff.scanCodeV2()` sample code: 

```javascript
liff.scanCodeV2().then(result => {
  // result = { value: '' }
});
```

<!-- note start -->

**2D code reader support on the LINE MINI App is scheduled for October 7, 2021**

Using `liff.scanCodeV2()` to launch a 2D code reader requires turning on **Scan QR** from the LIFF tab of the LINE Login channel on the [LINE Developers Console](https://developers.line.biz/console/). The **Scan QR** setting is scheduled to be added for LINE MINI App channels on **October 7, 2021**. Currently, as of **September 30, 2021**, `liff.scanCodeV2()` isn't available for LINE MINI App channels.

![Scan QR](https://developers.line.biz/media/liff/console-scanqr-en.png)

<!-- note end -->

#### The operating environment of the `liff.scanCodeV2()` method 

These are the operating environments of the `liff.scanCodeV2()` method and the 2D code reader that is displayed:

- [Operating environments](https://developers.line.biz/en/docs/liff/release-notes/#operating-environments-of-scan-code-v2)
- [2D code reader](https://developers.line.biz/en/docs/liff/release-notes/#two-dimensional-code-reader)

##### Operating environments 

Due to technical problems, the traditional [`liff.scanCode()`](https://developers.line.biz/en/reference/liff/#scan-code) method isn't available for use on LINE for iOS version 9.19.0 or later, or on external browsers. The newly added [`liff.scanCodeV2()`](https://developers.line.biz/en/reference/liff/#scan-code-v2) method, however, is available both on the newest version of LINE for iOS and on external browsers.

<table>
  <thead>
    <tr>
      <th rowspan="2">OS</th>
      <th rowspan="2">Version</th>
      <th colspan="3">LINE app version</th>
      <th rowspan="2">External browser</th>
    </tr>
    <tr>
      <th>9.18.0 or earlier</th>
      <th>9.19.0-11.6.x</th>
      <th>11.7.0 or later</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">iOS</td>
      <td>11-14.2</td>
      <td>✅</td>
      <td>❌</td>
      <td>❌</td>
      <td>✅ *1</td>
    </tr>
    <tr>
      <td>14.3 or later</td>
      <td>❌</td>
      <td>❌</td>
      <td>✅ *2</td>
      <td>✅ *1</td>
    </tr>
    <tr>
      <td>Android</td>
      <td>All versions</td>
      <td>❌</td>
      <td>❌</td>
      <td>✅ *2</td>
      <td>✅ *1</td>
    </tr>
    <tr>
      <td>PC</td>
      <td>All versions</td>
      <td>❌</td>
      <td>❌</td>
      <td>❌</td>
      <td>✅ *1</td>
    </tr>
  </tbody>
</table>

*1 You can only use web browsers that support [WebRTC API](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API).

*2 Only available when the screen size of the LIFF browser is `Full`. For details, see [Size of the LIFF browser](https://developers.line.biz/en/docs/liff/overview/#screen-size) in the LIFF documentation.

##### 2D code reader 

For the `liff.scanCode()` method, Android and iOS each had different 2D code reader screens, but for the `liff.scanCodeV2()` method, the following same screen is displayed, regardless of OS.

![2D code reader screen](https://developers.line.biz/media/liff/two_dimensional_code_reader_en.png)

If you launch the 2D code reader, a `Tall` size sub-window will be displayed on the bottom of the `Full` size LIFF app screen. Also, if you click on the ![2D code selection](https://developers.line.biz/media/liff/two-dimensional-code-file-selection.png) icon located at the bottom-right of the screen, you can select a 2D code to be read from a photo.

<br>

For more information on implementing a 2D code reader using `liff.scanCodeV2()`, see [Opening the 2D code reader](https://developers.line.biz/en/docs/liff/developing-liff-apps/#opening-two-dimensional-code-reader) in the LIFF documentation.

### The option of automatically executing the `liff.login()` method when initializing LIFF apps in external browsers has been added 

The `withLoginOnExternalBrowser` property has been added to the `liff.init()` method. Normally, when you access LIFF application on an [external browser](https://developers.line.biz/en/glossary/#external-browser), you need to explicitly go through the login process using the `liff.login()` method. By specifying `true` in the newly added `withLoginOnExternalBrowser` property, you can automatically execute the `liff.login()` method when the LIFF app is initialized.

![Login](https://developers.line.biz/media/liff/liff_autologin_en.png)

**Sample code with the `withLoginOnExternalBrowser` property added to the `liff.init()` method:**

```js
liff.init({
  liffId: "123456-abcdef",
  withLoginOnExternalBrowser: true, // Enable automatic login process
}).then(() =>
  // Start to use liff's api
});
```

For more information, see [liff.init()](https://developers.line.biz/en/reference/liff/#initialize-liff-app) in the LIFF API reference.

2021/09/17

## LIFF v1 discontinue 

As announced on [April 5, 2021](https://developers.line.biz/en/news/2021/04/05/liff-v1-deprecated/), LIFF v1 will be [end-of-life](https://developers.line.biz/en/glossary/#end-of-life) on October 1, 2021, which marks the end of its [deprecation](https://developers.line.biz/en/glossary/#deprecated) period.

### Target version

LIFF v1

<!-- warning start -->

**If you're using LIFF v1, migrate to LIFF v2**

For more information on migrating to LIFF v2, see [Migrate to LIFF v2](https://developers.line.biz/en/news/2021/04/05/liff-v1-deprecated/#migrate-to-v2) in the news from [April 5, 2021](https://developers.line.biz/en/news/2021/04/05/liff-v1-deprecated/).

<!-- warning end -->

### Scheduled date of discontinuation

October 1, 2021

### Impact

Gradually after the discontinuation of LIFF v1 on October 1, 2021, you won't be able to refer to the LIFF SDK URL (`https://d.line-scdn.net/liff/1.0/sdk.js`) or use the [LIFF v1 API](https://developers.line.biz/en/reference/liff-v1/).

LINE will continue to improve the quality of its services for its customers. Thank you for your understanding.

2021/09/14

## LIFF v2.14.0 released 

We've released LIFF v2.14.0.

This update only includes refactoring of the SDK. There is no change in features.

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), it will automatically update to v2.14.0.

If you're using the npm package, you can upgrade to v2.14.0 by running `npm install @line/liff@2.14.0` or `yarn add @line/liff@2.14.0`.

For more information on how to integrate the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2021/08/12

## LIFF v2.13.0 released 

We've released LIFF v2.13.0.

In LIFF v2.13.0, the following feature has been added, and bugs have been fixed.

- [The "Channel consent simplification" feature has been added to enable skipping the LINE MINI App consent screen](https://developers.line.biz/en/docs/liff/release-notes/#channel-consent-simplification-2021-8-12)
- [We've fixed bugs in the npm package version of the LIFF SDK](https://developers.line.biz/en/docs/liff/release-notes/#npm-bug-fix-2021-8-12)

### The "Channel consent simplification" feature has been added to enable skipping the LINE MINI App consent screen 

In order to use the "Channel consent simplification" feature  [released today (August 12, 2021)](https://developers.line.biz/en/news/2021/08/12/channel-consent-simplification/), you need to upgrade your LINE MINI App's LIFF SDK to v.2.13.0.

When you enable the "Channel consent simplification" feature, users can skip the "consent screen" that is displayed when they access a LINE MINI App for the first time.

For more information on usage conditions other than LIFF SDK version, such as behaviors and configuration, see [Skipping the consent screen](https://developers.line.biz/en/docs/line-mini-app/develop/channel-consent-simplification/) in the LINE MINI App documentation.

### We've fixed bugs in the npm package version of the LIFF SDK 

Some bugs inside the npm package version have been fixed.

If you're using the npm package version, we recommend executing `npm install @line/liff@2.13.0` or `yarn add @line/liff@2.13.0` to upgrade to v2.13.0.

For more information on how to integrate the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2021/07/12

## LIFF v2.12.0 released 

We've released LIFF v2.12.0.

In this update, only the internal behavior of the SDK has been changed. There is no change in functionality.

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), it will automatically update to v2.12.0.

If you're using the npm package, you can upgrade to v2.12.0 by running `npm install @line/liff@2.12.0` or `yarn add @line/liff@2.12.0`.

For more information on how to integrate the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2021/06/24

## LIFF v2.11.1 released 

We've released LIFF v2.11.1.

In LIFF v2.11.1, this bug has been fixed.

### We fixed the bug that caused URL fragments to be URL-encoded after the LIFF app is initialized 

In [LIFF v2.11.0](https://developers.line.biz/en/docs/liff/release-notes/#liff-v2-11-0), when you access LIFF URLs containing URL fragments (e.g. `#url-fragment`), there was a bug that caused the URL fragments to be URL-encoded after the LIFF app is initialized (after [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app) is executed).

We've fixed this bug in LIFF v2.11.1 so that even after `liff.init()` URL fragments aren't URL-encoded.

#### Example of URL fragment after liff.init() 

In the LIFF v2.11.0 example below, the slash (`/`) in the URL fragment (`#url/fragment`) is URL-encoded (`%2F`).

| LIFF version | LIFF URL | URL after `liff.init()` |
| --- | --- | --- |
| v2.11.0 | https://liff.line.me/{liffId}<b style="color:blue">#url</b><b style="color:red">/</b><b style="color:blue">fragment</b> | https://liff.line.me/{liffId}<b style="color:blue">#url</b><b style="color:red">%2F</b><b style="color:blue">fragment</b> |
| v2.11.1 | https://liff.line.me/{liffId}<b style="color:blue">#url</b><b style="color:red">/</b><b style="color:blue">fragment</b> | https://liff.line.me/{liffId}<b style="color:blue">#url</b><b style="color:red">/</b><b style="color:blue">fragment</b> |

<!-- note start -->

**We recommend updating to LIFF v2.11.1**

In LIFF v2.11.0 of the LIFF app, the bug occurs regardless of browser type ([LIFF browser](https://developers.line.biz/en/glossary/#liff-browser), [LINE's in-app browser](https://developers.line.biz/en/glossary/#line-iab), [external browser](https://developers.line.biz/en/glossary/#external-browser)). The same bug also occurs when you directly access not only a LIFF URL (e.g. `https://liff.line.me/{liffId}/#url/fragment`), but also an endpoint URL (e.g. `https://example.com/#url/fragment`).

If you're using v2.11.0, we recommend that you update to v2.11.1 to avoid unintended behaviors.

<!-- note end -->

For more information on how to integrate the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk).

2021/06/14

## LIFF v2.11.0 released 

We've released LIFF v2.11.0.

In LIFF v2.11.0, these security improvements have been made.

### Credential information is now excluded from the primary redirect URL after liff.init() 

For security reasons, URL fragments that contain credential information such as access tokens are now excluded from primary redirect URLs when `liff.init()` is resolved. Therefore, the primary redirect URL that doesn't contain credential information is processed as the current URL in the `then()` method of the method chain.

#### Redirect example 

If the LIFF URL is `https://liff.line.me/{liffId}/path` and the endpoint URL is `https://example.com`, you'll be redirected as follows:

![When confidential information is excluded](https://developers.line.biz/media/news/remove_credential_information-en.png)

| Number | Item | URL |
| --- | --- | --- |
| (1) | LIFF URL | https://liff.line.me/{liffId}<span style="color:blue">/path</span> |
| (2) | Primary redirect URL | https://example.com/<span style="color:blue">?liff.state=path</span><br/><b style="color:red">#access_token=xxx&context_token=xxx&<br/>feature_token=xxx&id_token=xxx&client_id=xxx</b> |
| (3) | URL after `liff.init()` | https://example.com/<span style="color:blue">?liff.state=path</span> |
| (4) | Secondary redirect URL | https://example.com<span style="color:blue">/path</span> |

#### liff.init() sample code 

Credential information is excluded within the `liff.init().then()` method.

``` js
console.log(window.location.href);
// https://example.com/?liff.state=path#access_token=xxx&context_token=xxx&feature_token=xxx&id_token=xxx&client_id=xxx

liff.init({liffId: myLiffId}).then(() => {
  console.log(window.location.href);
  // https://example.com/?liff.state=path
});
```

<!-- note start -->

**About using external logging tools like Google Analytics**

To use an external logging tool such as Google Analytics, we recommend updating to LIFF v2.11.0 to better secure the credential information of users who access the LIFF app. Make sure to send a URL that doesn't contain credential information to external logging tools after `liff.init()` is executed.

``` js
liff.init({liffId: myLiffId}).then(() => {
    ga('send', 'pageview');
})
```

<!-- note end -->

For more information on how to integrate the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk).

2021/05/17

## LIFF v2.10.0 released 

We've released LIFF v2.10.0.

In LIFF v2.10.0, these bugs have been fixed.

### We fixed the bug that caused old context tokens to be referenced when initializing the LIFF app in external browsers 

When users log in to a LIFF app using LIFF v2.9.1 or earlier in an [external browser](https://developers.line.biz/en/glossary/#external-browser), old context tokens stored in the localStorage when the LIFF app is initialized (when `liff.init()` method is executed) in previous sessions are referenced, causing unexpected behaviors, but we fixed this bug.

<!-- tip start -->

**What is a context token?**

A context token holds information about the environment in which the LIFF app is launched, such as screen size and user ID, which can be retrieved using the [`liff.getContext()`](https://developers.line.biz/en/reference/liff/#get-context) method. When your LIFF app is initialized (the [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app) method is executed), it is stored as a `context` key in the browser's localStorage.

<!-- tip end -->

#### Updated the timing of checking access token expiration 

When your LIFF app is initialized (when `liff.init()` is executed), the expiration of the access token generated in the previous session is checked, and if it has expired, the context token is discarded. However, in LIFF v2.9.1 or earlier, this expiration check takes place at the tail end of the LIFF app initialization, so old tokens that haven't been discarded are referenced when the initialization takes place, leading to unexpected behaviors.

In LIFF v2.10.0, the access token expiration check takes place at the beginning of the LIFF app initialization, ensuring that initialization takes place after the old context tokens have been discarded.

<!-- note start -->

**There is no guarantee that the information obtained through the liff.getContext() method is up-to-date**

Context tokens are discarded when access tokens expire. Even in LIFF v2.10.0, as long as the access token hasn't expired, the context information you can obtain through the [`liff.getContext()`](https://developers.line.biz/en/reference/liff/#get-context) method doesn't change. Therefore, there is no guarantee that the information obtained through the `liff.getContext()` method is always up-to-date.

<!-- note end -->

#### When to discard context tokens for each version 

Below is a comparison between LIFF v2.9.1 or earlier and LIFF v2.10.0 of when access token expiration is checked and context tokens are discarded.

| LIFF <br> version | Flow of storing context tokens in the localStorage |
| --- | --- |
| v2.9.1 or earlier | ![Previous timing of when context tokens were discarded](https://developers.line.biz/media/news/context_token_v2-9-1-en.png) |
| v2.10.0 | ![Timing of when context tokens are discarded in v2.10.0 or later](https://developers.line.biz/media/news/context_token_v2-10-0-en.png) |

<!-- note start -->

**In the case of LIFF browser and LINE's in-app browser**

[LIFF browser](https://developers.line.biz/en/glossary/#liff-browser) and [LINE's in-app browser](https://developers.line.biz/en/glossary/#line-iab) aren't affected by this version update.

<!-- note end -->

For details on information stored by context tokens, see [liff.getContext()](https://developers.line.biz/en/reference/liff/#get-context) in the LIFF API reference.

2021/04/27

## LIFF v2.9.1 released 

In LIFF v2.9.1, these bugs have been fixed, but there are no changes to the features.

### We fixed the bug that occurs when using the npm package of the LIFF SDK 

When attempting to use the npm package of the LIFF SDK on TypeScript, an error had occured during compilation, but this bug has been fixed. In LIFF v2.9.1, there is no issue with compilation, even when using TypeScript.

This fix applies to both the npm version and the CDN version of the LIFF SDK.

For more information on the npm package of the LIFF SDK, see [Use the npm package](https://developers.line.biz/en/docs/liff/developing-liff-apps/#use-npm-package).

<!-- tip start -->

**How to handle compilation errors**

We recommend upgrading to LIFF v2.9.1 as a workaround for compilation errors when using TypeScript, but if you can't, use this method to resolve the compilation errors:

If you enable the [`skipLibCheck`](https://www.typescriptlang.org/ja/tsconfig#skipLibCheck) option using TypeScript setting files such as `tsconfig.json`, compilation errors won't occur.

<!-- tip end -->

<br>

If you're using the CDN edge path(`https://static.line-scdn.net/liff/edge/2/sdk.js`), your LIFF will be automatically upgraded to v2.9.1.

If you're using the npm package, your LIFF will be upgraded to v2.9.1 if you execute either `npm install @line/liff@2.9.1` or `yarn add @line/liff@2.9.1`.

For more information on how to integrate the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk).

2021/04/13

## LIFF v2.9.0 released 

We've released LIFF v2.9.0.

In this update, only the internal behavior of the SDK has been changed. There is no change in functionality.

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), it will automatically update to v2.9.0.

If you're using the npm package, you can upgrade to v2.9.0 by running `npm install @line/liff@2.9.0` or `yarn add @line/liff@2.9.0`.

For more information on how to integrate the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2021/03/16

## LIFF v2.8.1 released 

We've released LIFF v2.8.1.

This update only includes refactoring of the SDK. There is no change in features.

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), it will automatically update to v2.8.1.

If you're using the npm package, you can upgrade to v2.8.1 by running `npm install @line/liff@2.8.1` or `yarn add @line/liff@2.8.1`.

For more information on how to integrate the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2021/02/15

## LIFF v2.8.0 released 

We've released LIFF v2.8.0.

These bugs have been fixed in LIFF v2.8.0.

- [Fixed bug of liff.init() being resolved before being redirected to a secondary redirect URL](https://developers.line.biz/en/docs/liff/release-notes/#liff-resolve-fix)
- [Fixed bug of unintentional decoding of URL encoded query parameters](https://developers.line.biz/en/docs/liff/release-notes/#liff-decode-fix)

There are no feature changes or additions.

### Fixed bug of liff.init() being resolved before being redirected to a secondary redirect URL 

In versions earlier than LIFF v2.7.1, there was a bug of `liff.init()` being resolved before being redirected to the secondary redirect URL. Because of this bug, there would be duplicate processing of the `then()` method, once before and once after being redirected to the secondary redirect URL.

In the code example below, the alert `liff.init() is resolved.` is displayed twice, because `liff.init()` is resolved once each, before and after being redirected to the secondary redirect URL.

**Code sample for displaying alerts when liff.init() is resolved:**

```javascript
liff.init(myLiffId).then(() => {
  // This process is executed after liff.init() is resolved.
  window.alert("liff.init() is resolved.");
});
```

Because in LIFF v2.8.0, `liff.init()` is resolved for the first time after being redirected to a secondary redirect URL, duplicate processing of the `then()` method has been fixed. In the code sample above, an alert is displayed only once.

| LIFF Version | Timing when `liff.init()` is resolved |
| --- | --- |
| v2.7.1 or earlier | ![resolve-timing-v2-7-0](https://developers.line.biz/media/news/resolve_timing_v2-7-0_en.png) |
| v2.8.0 | ![resolve-timing-v2-8-0](https://developers.line.biz/media/news/resolve_timing_v2-8-0_en.png) |

### Fixed bug of unintentional decoding of URL encoded query parameters 

In versions earlier than LIFF v2.7.1, if a developer gave the LIFF URL a URL encoded query parameter (e.g. `?t=http%3A%2F%2Fexample.com`), the query parameter was decoded when being redirected (e.g. `?t=http://example.com`). As a result, it would lead to a secondary redirect URL unintended by the developer.

In LIFF v2.8.0, query parameters aren't decoded but redirected remaining URL encoded.

**Redirect flow when you open the LIFF URL `https://liff.line.me/{liffId}?t=http%3A%2F%2Fexample.com`:**

| LIFF Version | Primary redirect URL | Secondary redirect URL |
| --- | --- | --- |
| v2.7.1 or earlier | https://endpoint.example.jp/?liff.state=<br /><b style="color:blue">?t=http%3A%2F%2Fexample.com</b> | https://endpoint.example.jp/<br /><b style="color:red">?t=http:</b><b style="color:red">//example.com</b> |
| v2.8.0 | https://endpoint.example.jp/?liff.state=<br /><b style="color:blue">%3Ft%3Dhttp%253A%252F%252Fexample.com</b> | https://endpoint.example.jp/<br /><b style="color:blue">?t=http%3A%2F%2Fexample.com</b> |

<!-- tip start -->

**LIFF URL that contains a query parameter**

When using LIFF URLs with URL encoded query parameters, upgrade to v2.8.0 to avoid unintended redirections to URLs.

<!-- tip end -->

For more information on redirects on LIFF apps, see [Behaviors from accessing the LIFF URL to opening the LIFF app](https://developers.line.biz/en/docs/liff/opening-liff-app/#redirect-flow) in the LIFF documentation.

2021/01/20

## LIFF v2.7.1 released 

We've released LIFF v2.7.1.

This bug has been fixed in LIFF v2.7.1:

### Fixed a bug that might prevent LIFF apps using LIFF v2.7.0 from launching in external browsers 

We’ve fixed a bug that might cause LIFF apps using [LIFF v2.7.0](https://developers.line.biz/en/docs/liff/release-notes/#liff-v2-7-0) to fail to launch when opened in [external browsers](https://developers.line.biz/en/glossary/#external-browser). In LIFF v2.7.1, the LIFF app can launch correctly in external browsers.

<!-- note start -->

**When already using LIFF v2.7.0**

If you are already using LIFF v2.7.0, we recommend that you update your LIFF apps to LIFF v2.7.1.

When you are using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), it will be automatically updated to v2.7.1. When you are using the CDN fixed path or the npm package version of LIFF SDK, update it to LIFF v2.7.1 manually.

<!-- note end -->

For more information about the different ways to embed the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2021/01/14

## LIFF v2.7.0 released 

We've released LIFF v2.7.0.

These are the changes in this update:

- [The npm package version of LIFF SDK can now be referenced by RequireJS](https://developers.line.biz/en/docs/liff/release-notes/#require-js)
- [Fixed a bug in which the name property of the ID token retrieved by the liff.getDecodedIDToken() method became unreadable](https://developers.line.biz/en/docs/liff/release-notes/#get-decoded-id-token)

### The npm package version of LIFF SDK can now be referenced by RequireJS 

The npm package version of LIFF SDK can now be referenced by [RequireJS](https://requirejs.org/).

For information on how to integrate the npm package version of the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

### Fixed a bug in which the name property of the ID token retrieved by the liff.getDecodedIDToken() method became unreadable 

In LIFF v2.6.0 or earlier, when a decoded ID token was retrieved using the `liff.getDecodedIDToken()` method, the value of the `name` property was unreadable if the username contained Unicode characters other than ASCII characters, such as Japanese.

In LIFF v2.7.0, the bug was fixed and usernames written in Unicode characters such as Japanese can now be retrieved correctly.

**If you get an ID token with `コニー` as the user name**

![user profile of conny](https://developers.line.biz/media/news/conny_en.png)

| LIFF v2.6.0 or earlier | LIFF v2.7.0 |
| :---: | :---: |
| <pre class="language-json"><code><span class="token punctuation">{</span><br/><span class="token property">"iss"</span><span class="token operator">:</span> <span class="token string">"https://access.line.me"</span><span class="token punctuation">,</span><br/><span class="token property">"sub"</span><span class="token operator">:</span> <span class="token string">"U272cada9c6f4c0c933b0713bc2f90f68"</span><span class="token punctuation">,</span><br/><span class="token property">"aud"</span><span class="token operator">:</span> <span class="token string">"1234567890"</span><span class="token punctuation">,</span><br/><span class="token property">"exp"</span><span class="token operator">:</span> <span class="token number">1513142487</span><span class="token punctuation">,</span><br/><span class="token property">"iat"</span><span class="token operator">:</span> <span class="token number">1513138887</span><span class="token punctuation">,</span><br/><span class="token property">"name"</span><span class="token operator">:</span> <span class="token string">"<b style="color:white">ã³ãã¼</b>"</span><span class="token punctuation">,</span><span class="token comment"> //Unreadable</span><br/><span class="token property">"picture"</span><span class="token operator">:</span> <span class="token string">"https://profile.line-scdn.net/..."</span><br/><span class="token punctuation">}</span></code></pre> | <pre class="language-json"><code><span class="token punctuation">{</span><br/><span class="token property">"iss"</span><span class="token operator">:</span> <span class="token string">"https://access.line.me"</span><span class="token punctuation">,</span><br/><span class="token property">"sub"</span><span class="token operator">:</span> <span class="token string">"U272cada9c6f4c0c933b0713bc2f90f68"</span><span class="token punctuation">,</span><br/><span class="token property">"aud"</span><span class="token operator">:</span> <span class="token string">"1234567890"</span><span class="token punctuation">,</span><br/><span class="token property">"exp"</span><span class="token operator">:</span> <span class="token number">1513142487</span><span class="token punctuation">,</span><br/><span class="token property">"iat"</span><span class="token operator">:</span> <span class="token number">1513138887</span><span class="token punctuation">,</span><br/><span class="token property">"name"</span><span class="token operator">:</span> <span class="token string">"<b style="color:white">コニー</b>"</span><span class="token punctuation">,</span><span class="token comment"> //Correctly received</span><br/><span class="token property">"picture"</span><span class="token operator">:</span> <span class="token string">"https://profile.line-scdn.net/..."</span><br/><span class="token punctuation">}</span></code></pre> |

For more information on `liff.getDecodedIDToken()`, see [`liff.getDecodedIDToken()`](https://developers.line.biz/en/reference/liff/#get-decoded-id-token) in the LIFF API reference.

2020/12/01

## LIFF v2.6.0 released 

We've released LIFF v2.6.0.

In this update, only the internal behavior of the SDK has been changed. There is no change in functionality.

If you're using the CDN edge path (`https://static.line-scdn.net/liff/edge/2/sdk.js`), it will automatically update to v2.6.0.

If you're using the npm package, you can upgrade to v2.6.0 by running `npm install @line/liff@2.6.0` or `yarn add @line/liff@2.6.0`.

For more information on how to integrate the LIFF SDK, see [Integrating the LIFF SDK with the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk) in the LIFF documentation.

2020/10/29

## LIFF v2.5.0 released 

We've released LIFF v2.5.0.

These are the changes in LIFF v2.5.0.

- [Improved performance of liff.init()](https://developers.line.biz/en/docs/liff/release-notes/#improve-liff-init-performance)
- [Security enhancements](https://developers.line.biz/en/docs/liff/release-notes/#security-enhancement)

There is no change in LIFF functionality in this update.

### Improved performance of liff.init() 

The speed from running `liff.init()` to the completion of LIFF app initialization has been improved, providing a more pleasant user experience with less waiting time to open the LIFF app.

For more information on `liff.init()`, see [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app) in the LIFF API Reference.

### Security enhancements 

We've strengthened security as a preventive measure against unknown attacks.

<!-- tip start -->

**About updating your LIFF app**

Since this is a minor security enhancement, an update is not required.

<!-- tip end -->

2020/09/28

## LIFF v2.3.3 released 

We've released LIFF v2.3.3.
This bug has been fixed in LIFF v2.3.3:

- [Fixed a bug that redirects users to unintended URLs when the endpoint URL ends with /](https://developers.line.biz/en/docs/liff/release-notes/#liff-url-including-path-bug-fix)

There are no feature updates in this release.

### Fixed a bug that redirects users to unintended URLs when the endpoint URL ends with / 

Under these conditions, accessing a LIFF URL causes a redirect to an unintended URL with a double path separator (`//`).

- The URL specified in **Endpoint URL** contains a path and ends in `/`. e.g. `https://example.com/campaign/`
- **Methods for converting additional information in the LIFF URL** is set to **Concatenate**.
- The LIFF URL contains a path (`/path`). e.g. `https://liff.line.me/{liffId}/path`

In LIFF v2.3.3, the bug has been fixed so that the user is redirected to the correct URL even under the above conditions.

| Item | LIFF URL | Primary redirect URL | Secondary redirect URL |
| --- | --- | --- | --- |
| Before spec change | https://liff.line.me/{liffId}/path | https://example.com/campaign<b style="color:red">/</b>?liff.state={urlEncode(/path)} | https://example.com/campaign<b style="color:red">//</b>path |
| After spec change | https://liff.line.me/{liffId}/path | https://example.com/campaign?liff.state={urlEncode(path)} | https://example.com/campaign<b style="color:red">/</b>path |

<!-- note start -->

**Impact on other versions**

- If you are using LIFF v2.3.x, we recommend that you update to this patch version.
- This bug has already been fixed in LIFF v2.4.1.

<!-- note end -->

For more information on what happens when accessing LIFF URLs, see [Operation from accessing LIFF URL to opening LIFF App](https://developers.line.biz/en/docs/liff/opening-liff-app/#redirect-flow) in the LIFF documentation.

2020/09/24

## LIFF v2.4.1 released 

We have released LIFF v2.4.1.
The changes in LIFF v2.4.1 are as follows:

- [Fixed an issue with the feature to open another LIFF app without closing a LIFF app](https://developers.line.biz/en/docs/liff/release-notes/#liff-transition-bug-fix)
- [Added a feature to liff.isApiAvailable() to check whether the transition between LIFF apps is possible](https://developers.line.biz/en/docs/liff/release-notes/#liff-transition-state)
- [Fixed behavior of liff.init() being called twice](https://developers.line.biz/en/docs/liff/release-notes/#call-init-twice-fix)

### Fixed an issue with the feature to open another LIFF app without closing a LIFF app 

We've found that the feature to open another LIFF app without closing the LIFF app, which we [announced on August 31, 2020](https://developers.line.biz/en/news/2020/08/31/release-liff-2-4-0/#liff-transition), has a bug and didn't work correctly even if the operating conditions were met.

In LIFF v2.4.1, the operating conditions have been changed as follows and the bug has been fixed.

| Items | Before the changes | After the changes |
| --- | --- | --- |
| LIFF SDK | 2.4.0 | 2.4.1 |
| LINE | 10.16.0 | 10.18.0 |

<!-- note start -->

**The use of LIFF v2.4.0 is no longer recommended**

Due to the above bug, the use of LIFF v2.4.0 is no longer recommended.
If you are using LIFF v2.4.0, we recommend that you update to v2.4.1.

<!-- note end -->

For more information, see [Opening a LIFF app from another LIFF app](https://developers.line.biz/en/docs/liff/opening-liff-app/#move-liff-to-liff) in the LIFF document.

### Added a feature to liff.isApiAvailable() to check whether the transition between LIFF apps is possible 

[`liff.isApiAvailable()`](https://developers.line.biz/en/reference/liff/#is-api-available), a method which checks if an API is available, can now be used to check if transitioning between LIFF apps is possible.

You can now execute `liff.isApiAvailable('multipleLiffTransition')` to confirm whether transitioning between LIFF apps is possible before opening another LIFF app.
By using this feature, you can prevent an error when opening another app.

```js
if (liff.isApiAvailable('multipleLiffTransition')) {
  window.location.href = "https://line.me/{liffId}", // URL for another LIFF app
}
```

<!-- tip start -->

**Get information about transitioning between LIFF apps with liff.getContext()**

You can now also use [`liff.getContext()`](https://developers.line.biz/en/reference/liff/#get-context), a method which obtains information about a LIFF app, to obtain information such as whether transitioning between LIFF app is possible, and the executable LINE version.
- `availability.multipleLiffTransition.permission`: Indicates whether transitioning between LIFF apps is possible.
- `availability.multipleLiffTransition.minVer`: Indicates the minimum LINE version that supports the transition between LIFF apps.

Below is an example of the return value of `liff.getContext()`.
```json
{
    "type": "utou",
    "utouId": "UU29e6eb36812f484fd275d41b5af4e760926c516d8c9faa35…b1e8de8fbb6ecb263ee8724e48118565e3368d39778fe648d",
    "userId": "U70e153189a29f1188b045366285346bc",
    "viewType": "full",
    "accessTokenHash": "ArIXhlwQMAZyW7SDHm7L2g",
    "availability": {
        "shareTargetPicker": {
            "permission": true,
            "minVer": "10.3.0"
        },
        "multipleLiffTransition": {
            "permission": true,
            "minVer": "10.18.0"
        }
    }
}
```

<!-- tip end -->

For more information, see [liff.isApiAvailable()](https://developers.line.biz/en/reference/liff/#is-api-available) or [liff.getContext()](https://developers.line.biz/en/reference/liff/#get-context) in the LIFF API reference.

### Fixed behavior of liff.init() being called twice 

If you execute [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app) more than once under the condition that the LIFF App is successfully initialized, a rejected `Promise` object was returned with an error message.

In LIFF v2.4.1, the error has been fixed so that if you execute `liff.init()` more than once under the condition that `liff.init()` succeeds, a resolved `Promise` object will be returned, and a warning message will be displayed.

For more information on initializing your LIFF App, see the LIFF document [Initializing LIFF App](https://developers.line.biz/en/docs/liff/developing-liff-apps/#initializing-liff-app).

2020/09/14

## LIFF v2.1.14, v2.2.1, v2.3.2 released 

LIFF v2.1.14, v2.2.1, v2.3.2 were released. The changes are as follows:

- [Fixed error in which the URL fragment entered in the LIFF endpoint URL was not correctly handled by liff.permanentLink.createUrl() (v2.3.2)](https://developers.line.biz/en/docs/liff/release-notes/#liff-create-url-error-fix-endpoint-v-2-3-2)
- [Fixed error in which the query parameter entered in the LIFF endpoint URL was not correctly handled by liff.permanentLink.createUrl() (v2.3.2)](https://developers.line.biz/en/docs/liff/release-notes/#liff-create-url-error-fix-query-parameter-v-2-3-2)
- [Fixed error in which the path entered in the LIFF endpoint URL was not correctly handled by liff.permanentLink.createUrl() (v2.3.2)](https://developers.line.biz/en/docs/liff/release-notes/#liff-create-url-redirect-url-fix-2-3-2)
- [Fixed error in which fragment was not included in the secondary redirect URL (v2.3.2)](https://developers.line.biz/en/docs/liff/release-notes/#liff-url-fragment-error-fix-v-2-3-2)
- [Fixed bug in which LIFF URLs were redirected to unintended URLs (v2.1.14, v2.2.1, v2.3.2)](https://developers.line.biz/en/docs/liff/release-notes/#bug-fix-redirect-2-3-2)

### Fixed error in which the URL fragment entered in the LIFF endpoint URL was not correctly handled by liff.permanentLink.createUrl() 

<br />

**Affected version**

- LIFF v2.3.2

**Changes**

When the LIFF endpoint URL contained a URL fragment (`#URL-fragment`), despite the **Methods for converting additional information in the LIFF URL** being set to **Replace (Backward compatibility mode)**, the URL fragment was included in the permanent link returned after executing [`liff.permanentLink.createUrl()`](https://developers.line.biz/en/reference/liff/#permanent-link-create-url).

<!-- tip start -->

**Conditions under which this problem occurs**

- A URL fragment is included in the LIFF endpoint URL
- **Methods for converting additional information in the LIFF URL** is set to **Replace (Backward compatibility mode)**

<!-- tip end -->

For example, when the **Endpoint URL** is set to `https://example.com/path#section` and `liff.permanentLink.createUrl()` is executed, `https://liff.line.me/{liffId}/path?liff.state=#section` would be returned as the permanent link. In LIFF v.2.3.2, the bug is fixed so that `https://liff.line.me/{liffId}` would be correctly returned.

### Fixed error in which the query parameter entered in the LIFF endpoint URL was not correctly handled by liff.permanentLink.createUrl() 

<br />

**Affected version**

- LIFF v2.3.2

**Changes**

When the LIFF endpoint URL contained a query parameter (`?key=value`), the query parameter would infinitely multiply in the permanent link returned after executing `liff.permanentLink.createUrl()`.

<!-- tip start -->

**Conditions under which this problem occurs**

- The query parameter in the LIFF endpoint URL matches the query parameter in the LIFF URL when executing `liff.permanentLink.createUrl()`.
- **Methods for converting additional information in the LIFF URL** is set to **Concatenate**

<!-- tip end -->

For example, when the **Endpoint URL** is set to `https://example.com/path1/?q1=v1&q2=v2` and `liff.permanentLink.createUrl()` is executed in `https://liff.line.me/{liffid}/?q1=v1&q2=v2`, a permanent link with the query parameter infinitely multiplied such as `https://liff.line.me/{liffid}/?q1=v1&q1=v1&q2=v2&q2=v2` would be returned.

In LIFF v.2.3.2, the bug is fixed so that `https://liff.line.me/{liffid}/?q1=v1&q2=v2` would be correctly returned.

### Fixed error in which the path entered in the LIFF Endpoint URL was not correctly handled by liff.permanentLink.createUrl() 

<br />

**Affected versions**

- LIFF v2.3.2

**Changes**

When path is included in the LIFF endpoint URL and a slash (`/`) is used at the end of the path, the permanent link obtained by executing `liff.permanentLink.createUrl()` would redirect you to URL without the ending slash as shown below.

<!-- tip start -->

**Conditions under which this problem occurs**

- Path (`/path/`) is included in the LIFF endpoint URL, and a slash (`/`) is used at the end of the path
- Query parameter (`?key=value`) or URL fragment (`#URL-fragment`) is included in the LIFF endpoint URL
- **Methods for converting additional information in the LIFF URL** is set to **Concatenate**

<!-- tip end -->

For example, if **Endpoint URL** is set to`https://example.com/path/?id=xxxxxxx`, accessing a permanent link obtained by executing `liff.permanentLink.createUrl()` would redirect you to a URL without the ending slash, such as `https://example.com/path?id=xxxxxxx`.

In LIFF v2.3.2, the error has been fixed so that you are correctly redirected to `https://example.com/path/?id=xxxxxxx`.

<!-- note start -->

**LIFF v2.4.0 has already been fixed**

As announced on [August 31, 2020](https://developers.line.biz/en/news/2020/08/31/release-liff-2-4-0/#liff-create-url-error-fix), this bug fix has already been reflected in LIFF v2.4.0.

<!-- note end -->

### Fixed error in which fragment was not included in the secondary redirect URL 

<br />

**Affected version**

- LIFF v2.3.2

**Changes**

When a fragment was included in the LIFF endpoint URL or LIFF URL, regardless of settings based on **Methods for converting additional information in the LIFF URL**, the secondary redirect URL would not include a fragment. This error has been fixed.

For more details on the secondary redirect URL or how it is affected by settings based on **Methods for converting additional information in the LIFF URL**, see the LIFF document [Operation from accessing LIFF URL to opening LIFF App](https://developers.line.biz/en/docs/liff/opening-liff-app/#redirect-flow).

### Fixed bug in which LIFF URLs were redirected to unintended URLs 

<br />

**Affected versions**

- LIFF v2.1.14
- LIFF v2.2.1
- LIFF v2.3.2

**Changes**

In the primary redirect destination URL, additional information specified in the LIFF URL (e.g. `path/?key=value`) is included in the `liff.state` query parameter. When additional information was included in the `liff.state` query parameter, there was bug in which you were redirected to unintended URLs as shown below.

<!-- tip start -->

**Conditions under which this problem occurs**

- There is no `/` at the beginning of the `liff.state` query parameter
- **Methods for converting additional information in the LIFF URL** is set to **Replace (Backward compatibility mode)**

<!-- tip end -->

For example, when **Endpoint URL** is set to `https://example.com`, and the `liff.state` query parameter was `path`, the domain name and path would not be separated by `/`, resulting in being redirected to `https://example.compath`.
In LIFF v2.1.14, v2.2.1, v2.3.2, the bug has been fixed so that you are correctly redirected to `https://example.com/path`.

<!-- note start -->

**Regarding vulnerability caused by unintended redirects**

There is a possibility that users are redirected to malicious websites due to this bug. If you are using a LIFF SDK version before v2.4.0, we recommend that you update it.

<!-- note end -->

For more information on what happens when accessing LIFF URLs, see the LIFF document [Operation from accessing LIFF URL to opening LIFF App](https://developers.line.biz/en/docs/liff/opening-liff-app/#redirect-flow).

2020/08/31

## LIFF v2.4.0 released 

<!-- note start -->

**Added on September 24, 2020**

LIFF v2.4.0 is no longer recommended due to a bug in the [transition to another LIFF app without closing your current LIFF app](https://developers.line.biz/en/docs/liff/release-notes/#liff-transition) feature.

| Items | Before the changes | After the changes |
| --- | --- | --- |
| LIFF SDK | 2.4.0 | 2.4.1 |
| LINE | 10.16.0 | 10.18.0 |

If you are using LIFF v2.4.0, we recommend that you update to v2.4.1.

<!-- note end -->

We have released LIFF v2.4.0. The changes in LIFF v2.4.0 are as follows:

- [You can now use `liff.closeWindow()` before the LIFF app is initialized](https://developers.line.biz/en/docs/liff/release-notes/#liff-close-window)
- [You can now transition to another LIFF app without closing your current LIFF app](https://developers.line.biz/en/docs/liff/release-notes/#liff-transition)
- [The error that LIFF URLs are redirected to unexpected URLs was fixed](https://developers.line.biz/en/docs/liff/release-notes/#bug-fix-redirect)
- [liff.permanentLink.createUrl() error was fixed](https://developers.line.biz/en/docs/liff/release-notes/#liff-create-url-error-fix)
- [The error of fragment not being included in the secondary redirect URL was fixed](https://developers.line.biz/en/docs/liff/release-notes/#liff-url-fragment-error-fix)

### You can now use `liff.closeWindow()` before the LIFF app is initialized 

You can now use the `liff.closeWindow()` method before the initialization of the LIFF app, even before the initialization of the LIFF app by `liff.init()` has finished.

<!-- note start -->

**Condition to execute the liff.closeWindow() method before initializing the LIFF app**

To use the `liff.closeWindow()` method before the initialization of the LIFF app by `liff.init()` has finished, your LIFF SDK version must be v2.4.0 or later, and the user's LINE version must be 10.15.0 or later.

<!-- note end -->

You can close the LIFF app with the `liff.closeWindow()` method if the LIFF app fails to initialize due to a network error, the user's LINE version, etc., as shown below.

``` js
liff
  .init({
    liffId: "123456-abcedfg" // Use own liffId
  })
  .then(() => {
    // Start to use liff's api
  })
  .catch((err) => {
    // Error happens during initialization
    console.log(err.code, err.message);
    liff.closeWindow();
  });
```

For more information, see [liff.closeWindow()](https://developers.line.biz/en/reference/liff/#close-window) in the LIFF API Reference.

### You can now transition to another LIFF app without closing your current LIFF app 

If you click the link to another LIFF app within a LIFF app whose screen is on `Full` display, you can display the other app while still having the LIFF browser open.
The LIFF browser doesn't close, so you can return to the original LIFF app with the return button from the LIFF browser.

<!-- note start -->

**Conditions for moving to another LIFF app without closing the current LIFF app (added on September 24, 2020)**

There was a bug in LIFF v2.4.0 that prevented the feature from working properly. These changes have been made to the operating conditions for this feature:

- LIFF SDK v2.4.1 or later and LINE 10.18.0 or later
- The original LIFF app screen is set to `Full` display
- The LIFF app to which you are moving is correctly initialized by `liff.init()`

<!-- note end -->

![LIFF-apps-transition](https://developers.line.biz/media/liff/liff_transition.png)

For more information, see [Opening a LIFF app from another LIFF app](https://developers.line.biz/en/docs/liff/opening-liff-app/#move-liff-to-liff) in the LIFF Document.

### The error that LIFF URLs are redirected to unexpected URLs was fixed 

An additional information (`path/?key=value`) specified in a LIFF URL is included in the `liff.state` query parameter for the primary redirected URL. When the `liff.state` query parameter contains an additional information, it might be redirected to an unexpected secondary redirected URL as follows.

<!-- tip start -->

**Conditions that cause this error**

- When the `liff.state` query parameter doesn't begin with `/`
- When setting **Methods for converting additional information in the LIFF URL** to **Replace (Backward compatibility mode)**

<!-- tip end -->

For example, if **Endpoint URL** is set to `https://example.com` and the `liff.state` query parameter is assigned to `path`, it was redirected to `https://example.compath` because the domain name and the path were not separated by `/`.
In the LIFF v2.4.0, this error has been fixed so that the URL above is now correctly redirected to `https://example.com/path`.

For more information on behaviors when accessing a LIFF URL, see [Behaviors from accessing the LIFF URL to opening the LIFF app](https://developers.line.biz/en/docs/liff/opening-liff-app/#redirect-flow).

### liff.permanentLink.createUrl() error was fixed

When information, such as query parameter (`?key=value`) or URL fragment (`#URL-fragment`), was included in the LIFF endpoint URL, on occasion, the additional information section was not accurately reflected in the permanent link when [`liff.permanentLink.createUrl()`](https://developers.line.biz/en/reference/liff/#permanent-link-create-url) was executed. This error has been fixed.

### The error of fragment not being included in the secondary redirct URL was fixed 

When a fragment was included in the LIFF endpoint URL or LIFF URL, regardless of settings based on **Methods for converting additional information in the LIFF URL**, the secondary redirect URL would not include a fragment. This error has been fixed.

For more details on the secondary redirect URL or how it is affected by settings based on **Methods for converting additional information in the LIFF URL**, see the LIFF document [Operation from accessing LIFF URL to opening LIFF App](https://developers.line.biz/en/docs/liff/opening-liff-app/#redirect-flow).

2020/07/16

## LIFF v2.3.1 released 

We've now released LIFF v2.3.1.
The changes in LIFF v2.3.1 are as follows:

- [Problems with the LIFF SDK npm package documentation were fixed](https://developers.line.biz/en/docs/liff/release-notes/#liff-npm-docs-fix)
- [Installation and usage instructions of the LIFF SDK npm package were moved from the npm official website to LINE Developers site](https://developers.line.biz/en/docs/liff/release-notes/#liff-npm-docs-move)

There are no feature updates in this release.

### Problems with the LIFF SDK npm package documentation were fixed 

We fixed an issue with [the npm official site documentation](https://www.npmjs.com/package/@line/liff) for the LIFF SDK npm package that was experimentally released.

### Installation and usage instructions of the LIFF SDK npm package were moved 

We moved the installation and usage instructions of the LIFF SDK npm package from the [npm official website](https://www.npmjs.com/package/@line/liff) to the LINE Developers site.
For more information, see [Use the npm package](https://developers.line.biz/en/docs/liff/developing-liff-apps/#use-npm-package).

2020/07/15

## New feature has been added to the LIFF header

As announced on [July 6, 2020](https://developers.line.biz/en/news/2020/07/06/liff-header-design-improvement/), a new feature has been added to the LIFF header.

![LIFF header design to be improved](https://developers.line.biz/media/news/liff-header-design-improvement.png)

- [The LIFF app icon is no longer displayed](https://developers.line.biz/en/docs/liff/release-notes/#remove-liff-app-icon-07-15)
- [The share button has been added](https://developers.line.biz/en/docs/liff/release-notes/#liff-share-button-07-15)

### The LIFF app icon is no longer displayed 

The icon in the upper left corner of the LIFF app is no longer displayed.

### The share button has been added 

LIFF apps with the [size of the LIFF app view](https://developers.line.biz/en/docs/liff/overview/#screen-size) set to `Full` include a share button in the header.
When a user taps the share button, the following options appear:

<ParameterTable>

**Share**:
  description: |
    Shares the URL of the current page via a LINE message.
**Refresh**:
  description: |
    Reloads the current page.

</ParameterTable>

Enable **Module mode** of the LIFF app in the LINE Developers Console to hide the share button.
For more information, see [Adding a LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/).

<!-- note start -->

**Operating environment**

The share button will be available on LINE versions 10.12.0 or later for iOS and Android.

<!-- note end -->

We will continue to improve the quality of the services we provide to our developers and we greatly appreciate your understanding.

2020/07/01

## LIFF SDK released as an npm package

Until now, to include the LIFF SDK in a LIFF app, it was necessary to [Specify the CDN path](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk).

Today, we released the LIFF SDK npm package on a trial basis. Now you can use npm and Yarn to install the LIFF SDK.

For more information on the LIFF SDK npm package, see [https://www.npmjs.com/package/@line/liff](https://www.npmjs.com/package/@line/liff).

The available LIFF SDK versions as an npm package is v2.3.0 or later. The features of future LIFF SDK versions will be announced in [Release Notes](https://developers.line.biz/en/docs/liff/release-notes/) in the LIFF Documentation.

<!-- note start -->

**npm package trial**

The npm package is available on a trial basis. It may be changed or deleted in the future without notice.

<!-- note end -->

2020/06/29

## LIFF v2.3.0 released 

We've now released LIFF v2.3.0.
The changes in LIFF v2.3.0 are as follows:

- [You can now use paths and query parameters in the LIFF endpoint URL](https://developers.line.biz/en/docs/liff/release-notes/#endpoint-url)
- [A condition for the liff.permanentLink.createUrl() method to throw an exception added](https://developers.line.biz/en/docs/liff/release-notes/#permanentLink)
- [You can now get the send results of liff.shareTargetPicker()](https://developers.line.biz/en/docs/liff/release-notes/#shareTargetPicker)
- [An error code returned by liff.sendMessages() added](https://developers.line.biz/en/docs/liff/release-notes/#sendMessage)

## You can now use paths and query parameters in the LIFF endpoint URL 

[As announced before](https://developers.line.biz/en/news/2020/05/20/liff-endpoint-url-improvement/), you can now use paths (`/path`) and query parameters (`?key=value`) added to the LIFF endpoint URL in the LIFF tab of the [LINE Developers Console](https://developers.line.biz/console/).

<!-- note start -->

**Existing LIFF apps aren't effected until the setting is changed**

It's necessary to change the setting in LINE Developers Console to use the new specs in existing LIFF apps. Existing LIFF apps aren't affected by the new spec until the setting is changed.

![Methods for converting additional information in the LIFF URL](https://developers.line.biz/media/liff/preserve-full-endpoint-url-en.png)

To use the new specs, set **Methods for converting additional information in the LIFF URL** to **Concatenate**.
Don't change the setting if your existing LIFF app doesn't support the new specs. If setting to **Replace (Backward compatibility mode)**, the LIFF app isn't affected by the new specs.

<!-- note end -->

For more information, see [Opening a LIFF app](https://developers.line.biz/en/docs/liff/opening-liff-app/) in the LIFF documentation.

## A condition for the liff.permanentLink.createUrl() method to throw an exception added 

When executing the `liff.permanentLink.createUrl()` method, an exception is thrown if the current page URL doesn't start with the URL specified in **Endpoint URL**.

```javascript
try {
    const myLink = liff.permanentLink.createUrl()
}
catch (err) {
    console.log(err.code + ':' + err.message);
}
```

Especially when setting **Methods for converting additional information in the LIFF URL** to **Replace (Backward compatibility mode)**, the paths and query parameters (`/2020campaign/?key=value`) specified in **Endpoint URL** may not be included in the secondary redirect URL.
In this case, you can't get a permanent link because the `liff.permanentLink.createUrl()` method meets the above conditions.

For more information, see [`liff.permanentLink.createUrl()`](https://developers.line.biz/en/reference/liff/#permanent-link-create-url) in the LIFF v2 API reference.

## You can now get the send results of liff.shareTargetPicker() 

As announced on [April 21, 2020](https://developers.line.biz/en/news/2020/04/21/notice-return-value-of-sharetargetpicker/), you can now get the send results of `liff.shareTargetPicker()`.

Before the spec change, the LIFF app was able to confirm whether the target picker was displayed, but not whether the message was sent after that.

After the change, the LIFF app is able to check whether the message has been sent, so you can change the behavior of the LIFF app depending on the user's situation.

<!-- note start -->

**Note**

- The return value of `liff.shareTargetPicker()` is changed due to this spec change.
- This spec change doesn't affect users using LINE 10.3.0 - 10.10.0.

<!-- note end -->

### Sample code for this spec change

We recommend you to handle the return value according to the LINE versions that users are using as shown below:

```javascript
if (liff.isApiAvailable('shareTargetPicker')) {
  liff.shareTargetPicker([
    {
      'type': 'text',
      'text': 'Hello, World!'
    }
  ])
    .then(function (res) {
      if (res) {
        // succeeded in sending a message through TargetPicker
        console.log(`[${res.status}] Message sent!`)
      } else {
        const [majorVer, minorVer] = (liff.getLineVersion() || "").split('.');
        if (parseInt(majorVer) == 10 && parseInt(minorVer) < 11) {
          // LINE 10.3.0 - 10.10.0
          // Old LINE will access here regardless of user's action
          console.log('TargetPicker was opened at least. Whether succeeded to send message is unclear')
        } else {
          // LINE 10.11.0 -
          // sending message canceled
          console.log('TargetPicker was closed!')
        }
      }
    }).catch(function (error) {
      // something went wrong before sending a message
      console.log('something wrong happen')
    })
}
```

For more information, see [`liff.shareTargetPicker()`](https://developers.line.biz/en/reference/liff/#share-target-picker) in the LIFF v2 API reference.

## An error code returned by liff.sendMessages() added 

Previously, if passing the wrong parameters to `liff.sendMessages()`, `400` was returned as the error code of `LiffError`. After the spec change, `INVALID_ARGUMENT` is returned instead.

As long as the processing isn't split by error codes, this spec change doesn't effect your LIFF app.

Before the spec change:

```javascript
liff.sendMessages([
  {
    type: 'text',
    text: 'Hello, World!'
  }
])
  .then(() => {
    console.log('message sent');
  })
  .catch((err) => {
    // Returns "400" if invalid arguments are passed
    if (err.code === "400") {
      console.log("message format error!");
    }
  });
```

After the spec change:

```javascript
liff.sendMessages([
  {
    type: 'text',
    text: 'Hello, World!'
  }
])
  .then(() => {
    console.log('message sent');
  })
  .catch((err) => {
    // Returns "INVALID_ARGUMENT" if invalid arguments are passed
    if (err.code === "INVALID_ARGUMENT") {
      console.log("message format error!");
    }
  });
```

For more information, see [Error details](https://developers.line.biz/en/reference/liff/#error-details) in the LIFF v2 API reference.

2020/06/15

## LIFF v2.2.0: LIFF error codes added 

The `LiffError` codes passed when `Promise` is rejected in the following methods have been made more detailed, making the cause of the problem easier to understand.

For more information, view the **Error Response** descriptions for these methods:

- [liff.init()](https://developers.line.biz/en/reference/liff/#initialize-liff-app)
- [liff.getProfile()](https://developers.line.biz/en/reference/liff/#get-profile)
- [liff.getFriendship()](https://developers.line.biz/en/reference/liff/#get-friendship)

2020/04/30

## LIFF v2.1.13: liff.getLineVersion() and liff.id added to LIFF v2 

We added the `liff.getLineVersion()` method and the `liff.id` property to LIFF v2.

`liff.getLineVersion()` allows you to get the user's LINE version.

If a user opens the LIFF app using the LIFF browser, the LINE version of the user is returned as a string. If a user opens the LIFF app using an external browser, `null` is returned.

`liff.id` is the property that holds the LIFF app ID (String type) passed to `liff.init()`.

Learn more about [`liff.getLineVersion()`](https://developers.line.biz/en/reference/liff/#get-line-version) and [`liff.id`](https://developers.line.biz/en/reference/liff/#id) in the LIFF v2 API reference.

2020/04/03

## liff.isApiAvailable() added to LIFF v2

We added the method `liff.isApiAvailable()` to LIFF v2. This method checks whether a specified API can be used in the environment where the LIFF app was launched.

<!-- note start -->

**Note**

The number of APIs you can specify is limited. Currently, you can only specify `liff.shareTargetPicker()`. We'll notify you when more APIs can be checked with `liff.isApiAvailable()` in the future.

<!-- note end -->

## Check if share target picker is available

By executing `liff.isApiAvailable()` before you execute `liff.shareTargetPicker()`, you can avoid the user getting an error message on their screen if the share target picker isn't available in their device environment.

```javascript
if (liff.isApiAvailable('shareTargetPicker')) {
  liff.shareTargetPicker([
    {
      type: "text",
      text: "Hello, World!"
    }
  ])
    .then(
      alert("ShareTargetPicker was launched")
    ).catch(function(res) {
      alert("Failed to launch ShareTargetPicker")
    })
}
```

Learn more from [liff.isApiAvailable()](https://developers.line.biz/en/reference/liff/#is-api-available) in the LIFF v2 API reference.

2020/03/03

## liff.shareTargetPicker() and liff.ready added to LIFF v2

We added `liff.shareTargetPicker()` and `liff.ready` to LIFF v2.

## liff.shareTargetPicker()

Execute the `liff.shareTargetPicker()` method to display the target picker (screen for selecting a group or friend) and send the message created by the developer to the selected target. This message appears to your group or friends as if you had sent it.

![target picker](https://developers.line.biz/media/news/share-target-picker.png)

For more information, see [Sending messages to a user's friend (share target picker)](https://developers.line.biz/en/docs/liff/developing-liff-apps/#share-target-picker) in the LIFF documentation.

<!-- note start -->

**Target picker operating environment**

Target picker is supported by LINE 10.3.0 for iOS and Android.

<!-- note end -->

## liff.ready

With `liff.ready`, you can get the `Promise` object that resolves when you run [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app) for the first time after starting the LIFF app. If you use `liff.ready`, you can execute any process after the completion of `liff.init()`.

For more information, see [liff.ready](https://developers.line.biz/en/reference/liff/#ready) in the LIFF v2 API reference.

2020/02/07

## Notice about LIFF v1 APIs and discontinuation schedule change

We [announced that the end-of-life of LINE Front-end Framework (LIFF) server API was scheduled for March 31, 2020](https://developers.line.biz/en/news/2020/01/21/liff-server-api-deprecation/). Due to feedback received, we will continue to provide the API.

As for LIFF v1, we will announce the discontinuation schedule as soon as it is decided. In the meantime, we recommend that you migrate from v1 to v2 as soon as possible.

Feature | Schedule before this update | Schedule after this update
-|-|-
[LIFF v1 Client API](https://developers.line.biz/en/reference/liff-v1/#client-api) | Scheduled for discontinuation | Scheduled for discontinuation (This has not changed)
[LIFF v1 Server API](https://developers.line.biz/en/reference/liff-v1/#server-api)  | Scheduled for discontinuation on March 31, 2020 | **Support continues**

<!-- note start -->

**LIFF v1 will still be discontinued**

As announced on [October 16, 2019](https://developers.line.biz/en/news/2019/10/16/liff-v2-released/), LIFF v1 will be discontinued. Use the latest version of LIFF.

<!-- note end -->

2020/02/05

## Users can no longer add LIFF apps to Messaging API channels

As announced on [November 11, 2019](https://developers.line.biz/en/news/2019/11/11/liff-cannot-be-used-with-messaging-api-channels/), due to a function enhancement with LIFF v2, users can no longer add LIFF apps to Messaging API channels.

To find out about restrictions on LIFF apps already added to the Messaging API channel, and how to transition to the LINE Login channel, see the above news article.

2020/01/21

## LIFF v1 Server API end-of-life on March 31, 2020

March 31, 2020 marks the end-of-life date for **LINE Front-end Framework (LIFF) v1 Server API**. On that date, these features will be removed:

- [Server API](https://developers.line.biz/en/reference/liff-server/)
    - [Adding the LIFF app to a channel](https://developers.line.biz/en/reference/liff-server/#add-liff-app)
    - [Update LIFF app settings](https://developers.line.biz/en/reference/liff-server/#update-liff-app)
    - [Get all LIFF apps](https://developers.line.biz/en/reference/liff-server/#get-all-liff-apps)
    - [Delete LIFF app from a channel](https://developers.line.biz/en/reference/liff-server/#delete-liff-app)

<!-- note start -->

**Use the latest version of LIFF**

As announced on [October 16, 2019](https://developers.line.biz/en/news/2019/10/16/liff-v2-released/), LIFF v1 will be discontinued.

<!-- note end -->

## Use LIFF v2

All discontinued Server API functions can be used in the [LINE Developers Console](https://developers.line.biz/console/). For more information on how to add a LIFF app to a channel, read this:

- [Adding a LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/)

You can use other features with the same process.

LINE will continue to improve the quality of its services. Thank you for your understanding.

2020/01/14

## Update your code that uses the suspended LIFF SDK API

As announced on [November 29, 2019](https://developers.line.biz/en/news/2019/11/29/liff-functions-suspended/), these APIs on LINE v9.19.0 and later for iOS were temporarily suspended due to technical issues.

* liff.scanCode()
* liff.bluetooth.*

Starting today, for end users using the LIFF app on **LINE v9.19.0 and later for iOS**, each API works as follows.

API | Function
-|-
liff.scanCode() | API is `undefined`
liff.bluetooth.* | If the Bluetooth plug-in fails to initialize when calling `liff.initPlugins(['bluetooth'])`, a `FORBIDDEN` error is returned.

If you use `liff.scanCode()`, we recommend that you also consider the above case and verify that the function exists.

Before modification:

```
liff.scanCode().then(result => {
  // result = { value: '' }
});
```

Modified:

```
if (liff.scanCode) {
  liff.scanCode().then(result => {
    // result = { value: '' }
  });
}
```

For more information, see [LIFF v2 API reference](https://developers.line.biz/en/reference/liff/).

LINE will continue to improve the quality of its services. Thank you for your understanding.

2019/11/29

## Some LIFF functions suspended

Due to a technical issue, we've temporarily suspended the following LIFF functions. We'll let you know as soon as this situation changes.

- `liff.scanCode()`
- `liff.bluetooth.*`

## Impacted environments

Environment | Version
-- | --
LINE for iOS | On version 9.19.0 and later, the functions listed above are temporarily unavailable.
LINE for Android | Not affected for now, but more news will follow soon.

We apologize for the inconvenience and are working hard to solve the problem.

2019/11/11

## Users can no longer add LIFF apps to Messaging API channels

LIFF v2 is scheduled to be updated with LINE Login as the core channel. Additionally, an upcoming change will prevent users from adding LIFF apps to Messaging API channels entirely. We strongly recommend users to add LIFF apps to the LINE Login channel.

## Scheduled change date

Early February 2020

## Impact

Channel type | Impact
-|-
LINE Login channel | Not affected.
Messaging API channel| After the specification change, LIFF apps **cannot be added** to the Messaging API channel. LIFF apps added to Messaging API channels at the time of specification change are still usable.

<!-- note start -->

**Do not add LIFF apps to the Messaging API channel**

At this time, users can add LIFF apps to the Messaging API channel. However, we strongly advise against it due to the following restrictions:

- The bot link feature can't be used.
- LIFF feature expansion may not be supported.
- The LIFF app may not be usable in the future.

LIFF apps added to the LINE Login channel have no restrictions and can use all LIFF v2 functions.

<!-- note end -->

## Transition to the LINE Login channel

To continue using the LIFF app added to the Messaging API channel, re-add the LIFF app to the LINE Login channel. Once re-added, LINE Developers Console will issue a new LIFF app ID. As a result, please take note of the following:

- If you're using LIFF v2, change the LIFF app ID specified in `liff.init()`.
- The LIFF URL used to launch LIFF (e.g.: line://app/1234567890-AbcdEfgh) will change.

<!-- note start -->

**Remove LIFF apps added to Messaging API channel**

To avoid confusion, delete the LIFF app added to the Messaging API channel after adding to the LINE Login channel.

<!-- note end -->

2019/10/16

## LIFF v2 released 

LINE Front-end Framework (LIFF) v2 is a platform for web apps provided by LINE.

<!-- note start -->

**Use the latest version of LIFF**

LIFF v1 will be deprecated.

<!-- note end -->

### LIFF apps now run in external browsers

With LIFF v1, LIFF apps ran only in a LIFF browser. With LIFF v2, LIFF apps can also run in external browsers. This means you can develop LIFF apps using the same development environment as general web applications.

### Get user profile and email

Because compatibility with LINE Login v2.1 has improved, you can retrieve a user's ID and email address from the LINE Platform. Your LIFF app can use this data to provide features related to user information and sending emails.

Furthermore, you can use LINE Login (web login flow) even when your LIFF app is running in an external browser. This means you can use the same information even when the LIFF app is running in an external browser.

### Read QR codes

You can start LINE's QR code reader and get the strings read by the user.

### Get LIFF app environment information

You can get the following details about the environment in which your LIFF app is running:

- Operating system in which the LIFF app is running (iOS, Android, external browser)
- Whether the LIFF app is running in a LIFF browser (true, false)
- Language settings

For more information, see [LINE Front-end Framework](https://developers.line.biz/en/docs/liff/overview/).

2019/04/23

## Improved consent screen in LINE Front-end Framework

We have improved the consent screen bundled with the LINE Front-end Framework (LIFF). The improvement is automatically applied to all LIFF apps. There's no need for additional development work.

![New consent screen](https://developers.line.biz/media/news/liff-consent-screen-changed-01.png)

As before this update, the user can choose to not allow the LIFF app to send messages to chats. But if they do so, unlike before, the consent screen will reappear the next time the user launches the LIFF app.

2019/02/07

## You can get access tokens through LIFF SDK

We added the `liff.getAccessToken()` method to the LIFF SDK.

Use the access token to interact with the [Social API](https://developers.line.biz/en/docs/social-api/overview/) to access user profile data on the LINE Platform.

For more information, see [Getting the user's access token](https://developers.line.biz/en/docs/liff/developing-liff-apps/#getting-tokens).

2018/11/16

## Renewed LIFF server API

Now you can set the following properties to your LIFF apps.

 - `description` property
 - `features.ble` property

The HTTP request to the API endpoint to update a LIFF app is changed from `PUT` to `PATCH`. Now you can partially update the properties of your LIFF apps.

For more information, see the following sections:

 - [Add LIFF app](https://developers.line.biz/en/reference/liff-server/#add-liff-app)
 - [Update LIFF app](https://developers.line.biz/en/reference/liff-server/#update-liff-app)

2018/10/30

## LIFF apps can now be added with the LINE Developers Console

Now you can add LIFF apps with the [LINE Developers Console](https://developers.line.biz/console/). As before, you can still add LIFF apps with the LIFF server API.

For more information, see [Adding a LIFF app](https://developers.line.biz/en/docs/liff/registering-liff-apps/).

2018/07/19

## The maximum number of LIFF apps has been increased

Now you can add up to 30 LIFF apps for one channel. The previous maximum number was 10.

For more information, see [Add LIFF app](https://developers.line.biz/en/reference/liff-server/#add-liff-app) in the LIFF API reference documentation.

2018/06/06

## LINE Front-end Framework released

LINE Front-end Framework (LIFF) is a platform for web apps that run within LINE.

When launching a web app (LIFF app) registered in LIFF in LINE, the LIFF app can get data from the LINE Platform such as the LINE user ID. The LIFF app can use such data to provide features that utilize user information and send messages on behalf of the user.

For more information, see [LINE Front-end Framework](https://developers.line.biz/en/docs/liff/overview/).
