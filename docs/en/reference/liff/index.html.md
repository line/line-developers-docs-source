# LIFF API reference

## Common specifications 

### Operating environment 

For more information about supported operating environments for LIFF, see [LIFF overview](https://developers.line.biz/en/docs/liff/overview/) in the LIFF documentation.

Which functions you can use depends on whether the LIFF app is opened in a LIFF browser or an external browser. For example, you can't use `liff.scanCode()` in an external browser. For more information, see the descriptions for each client API.

<!-- note start -->

**LIFF apps are not compatible with OpenChat**

For example, retrieving a user's profile information through a LIFF app isn't possible in most cases.

<!-- note end -->

### LIFF SDK errors 

LIFF SDK errors are returned in LiffError objects.

<!-- note start -->

**When identifying errors, refer to both the error code and the error message**

Since the error messages are subject to change without notice, identifying errors based on an exact match of the error message may cause your LIFF app to malfunction. To ensure that your LIFF app continues to work properly even when error messages change, identify errors by referring to both the error code and the error message.

We plan to make improvements so that errors can be uniquely identified by error codes.

<!-- note end -->

_Example_

<!-- tab start `json` -->

```json
{
  "code": "INIT_FAILED",
  "message": "Failed to init LIFF SDK"
}
```

<!-- tab end -->

#### LiffError object 

<!-- parameter start -->

code

String

Error code

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

message

String

Error message

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

cause

Unknown

Error cause

<!-- parameter end -->

#### Error details 

| Error code | Description |
| --- | --- |
| 400 | Problem with the request. Check the request parameters and JSON format. |
| 401 | Check that the authorization header is correct. |
| 403 | Not authorized to use the API. Confirm that your account or plan is authorized to use the API. |
| 429 | Make sure that you are within the rate limit for requests. |
| 500 | Temporary error on the API server. |
| INIT_FAILED | Failed to init LIFF SDK. |
| INVALID_ARGUMENT | An invalid argument was specified. |
| UNAUTHORIZED | <ul><li>The user did not authorize.</li><li>Call the server api without access token.</li><li>Call the share target picker before logging in.</li></ul> |
| FORBIDDEN | <ul><li>You don't have the required permission.</li><li>You attempted to use a feature in an environment that's not supported.</li></ul> |
| INVALID_CONFIG | An invalid setting.<ul><li>Specify the liffId to initialize LIFF apps using [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app).</li><li>The URL of the page that executes the [`liff.permanentLink.createUrl()`](https://developers.line.biz/en/reference/liff/#permanent-link-create-url) method doesn't start with the URL specified in the **Endpoint URL**.</li></ul> |
| INVALID_ID_TOKEN | Failed to verify the ID token. |
| EXCEPTION_IN_SUBWINDOW | Problem with subwindow. <ul><li>For example, if the target picker (group or friend selection screen) is displayed and has been idle for more than 10 minutes, for example.</li></ul> |
| UNKNOWN | Unknown error. |

## LIFF SDK properties 

### liff.id 

The property that holds the LIFF app ID (`String` type) passed to [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app).

The value of `liff.id` is `null` until you run `liff.init()`.

_Example_

<!-- tab start `javascript` -->

```javascript
const liffId = "my-liff-id";
liff.init({ liffId });

// liff.id equals to liffId
```

<!-- tab end -->

### liff.ready 

A property holding the `Promise` object that resolves when you run [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app) for the first time after starting the LIFF app.

If you use `liff.ready`, you can execute any process after the completion of `liff.init()`.

<!-- tip start -->

**This property can be used before the LIFF app is initialized**

You can use `liff.ready` even before the initialization of the LIFF app by `liff.init()` has finished.

<!-- tip end -->

_Example_

<!-- tab start `javascript` -->

```javascript
liff.ready.then(() => {
  // do something you want when liff.init finishes
});
```

<!-- tab end -->

<!-- note start -->

**Note**

If `liff.init()` fails, `liff.ready` will not be rejected. Also, it doesn't return a `LiffError` object.

<!-- note end -->

## Initialization 

### liff.init() 

Initializes a LIFF app.

You can only call other LIFF SDK methods after executing the `liff.init()` method. LIFF apps must be initialized each time a page is opened. Even if the transition is within the same LIFF app, you should execute the `liff.init()` method when you open a new page.

If you use LIFF features without properly initializing the LIFF app, we don't guarantee that the features will work.

The LIFF SDK obtains the access token and ID token of the user from the LINE Platform when you execute the `liff.init()` method.

- To use the access token obtained by the LIFF SDK, call [liff.getAccessToken()](https://developers.line.biz/en/reference/liff/#get-access-token).
- To use the ID token payload obtained by the LIFF SDK, call [liff.getDecodedIDToken()](https://developers.line.biz/en/reference/liff/#get-decoded-id-token).

#### Important points to consider when initializing the LIFF app 

The following are important points to consider when initializing your LIFF app. Read and understand these points before you start developing your LIFF app.

- [Execute `liff.init()` at the endpoint URL or at a lower level](https://developers.line.biz/en/reference/liff/#initializing-liff-app-notes-1)
- [Execute `liff.init()` once for the primary redirect URL and once for the secondary redirect URL](https://developers.line.biz/en/reference/liff/#initializing-liff-app-notes-2)
- [Process URL changes after `liff.init()` completes](https://developers.line.biz/en/reference/liff/#initializing-liff-app-notes-3)
- [Use caution when handling the primary redirect URL](https://developers.line.biz/en/reference/liff/#initializing-liff-app-notes-4)

##### Execute `liff.init()` at the endpoint URL or at a lower level 

The `liff.init()` method will only work on URLs that are exactly the same as the endpoint URL, or on URLs that are at a lower level than the endpoint URL. If the LIFF app transitions to a URL other than these, the `liff.init()` method isn't guaranteed to work.

The following example shows whether the behavior is guaranteed for the URL that executes the `liff.init()` method when the endpoint URL is `https://example.com/path1/`. Some LIFF app features, such as the [multi-tab view](https://developers.line.biz/en/docs/liff/overview/#multi-tab-view), may not work properly on URLs where the behavior isn't guaranteed.

| URL to execute `liff.init()`          | Guaranteed to work |
| ------------------------------------- | ------------------ |
| `https://example.com/`                | ❌                 |
| `https://example.com/path1/`          | ✅                 |
| `https://example.com/path1/language/` | ✅                 |
| `https://example.com/path2/`          | ❌                 |

<!-- note start -->

**When executing the liff.init() method, the warning message &quot;liff.init() was called with a current URL that is not related to the endpoint URL.&quot; appears in a console**

In LIFF v2.27.2 or later, a warning message will appear when the `liff.init()` method is executed on a URL where the behavior isn't guaranteed.

For example, if the endpoint URL of a LIFF app is `https://example.com/path1/path2/` and the URL where the `liff.init()` method is executed is `https://example.com/path1/`, the following warning message will appear:

```
liff.init() was called with a current URL that is not related to the endpoint URL.
https://example.com/path1/ is not under https://example.com/path1/path2/
```

If you see the warning message above, consider changing the endpoint URL to `https://example.com/` or `https://example.com/path1/`. Changing to these URLs guarantees the `liff.init()` method works correctly.

<!-- note end -->

##### Execute `liff.init()` once for the primary redirect URL and once for the secondary redirect URL 

The `liff.init()` method performs initialization processing based on information such as `liff.state` and `access_token=xxx` given to the primary redirect URL. If your endpoint URL includes a query parameter or path, to properly initialize the LIFF app, execute the `liff.init()` method once for both the primary redirect URL and the secondary redirect URL. For more information, see [Behaviors from accessing the LIFF URL to opening the LIFF app](https://developers.line.biz/en/docs/liff/opening-liff-app/#redirect-flow) in the LIFF documentation.

##### Process URL changes after `liff.init()` completes 

Execute processes that change URLs after the `Promise` object returned by the `liff.init()` method is resolved.

```javascript
// Example using window.location.replace()
liff
  .init({
    liffId: "1234567890-AbcdEfgh", // Use own liffId
  })
  .then(() => {
    // Redirect to another page after the returned Promise object has been resolved
    window.location.replace(location.href + "/entry/");
  });
```

If you execute any of the following URL manipulations before the `Promise` object resolves, the LIFF app may not open properly:

- Change the URL using the [`Document.location`](https://developer.mozilla.org/en-US/docs/Web/API/Document/location) property or the [`Window.location`](https://developer.mozilla.org/en-US/docs/Web/API/Window/location) property
- Change the URL using the [`history.pushState()`](https://developer.mozilla.org/en-US/docs/Web/API/History/pushState) method or the [`history.replaceState()`](https://developer.mozilla.org/en-US/docs/Web/API/History/replaceState) method of the [History API](https://developer.mozilla.org/en-US/docs/Web/API/History_API)
- Return status code `301` or `302` on the server-side and redirect to another URL

##### Use caution when handling the primary redirect URL 

The `access_token=xxx` automatically granted to the primary redirect URL is the user's access token (confidential information). Don't send the primary redirect URL to an external logging tool such as Google Analytics.

Note that in LIFF v2.11.0 or later, credential information is excluded from URLs when the `liff.init()` method is resolved. Therefore, you can prevent leaking credential information by sending the page view in the `then()` method as follows. If you want to use logging tools, we recommend that you upgrade your LIFF app to v2.11.0 or later. For more information about the updates in LIFF v2.11.0, see [Release Notes](https://developers.line.biz/en/docs/liff/release-notes/#liff-v2-11-0) in the LIFF documentation.

```javascript
liff
  .init({
    liffId: "1234567890-AbcdEfgh", // Use own liffId
  })
  .then(() => {
    ga("send", "pageview");
  });
```

<!-- note start -->

**LIFF app's query parameters**

When you access a LIFF URL or perform a transition between LIFF apps, the URL may be given query parameters that begin with `liff.*`.

e.g.

- `liff.state` (indicates additional information specified in LIFF URL)
- `liff.referrer` (indicates where the referrer came from when transitioning between LIFF apps. For more information, see [Get URL from before LIFF-to-LIFF transition](https://developers.line.biz/en/docs/liff/opening-liff-app/#using-liff-referrer).)

The above query parameters are given by the SDK so that LIFF apps can function properly. When you independently alter the above query parameters, proper opening of the LIFF app and a transition between LIFF apps may not be guaranteed. Implement your app so that the `liff.*` query parameter is altered after `liff.init()` is resolved.

<!-- note end -->

<!-- tip start -->

**Functions that can be executed even before the LIFF app is initialized**

This property or methods are available even before the `liff.init()` method is executed.

You can get the environment in which the LIFF app is running before initializing the LIFF app, or close the LIFF app when the LIFF app initialization fails.

- [liff.ready](https://developers.line.biz/en/reference/liff/#ready)
- [liff.getOS()](https://developers.line.biz/en/reference/liff/#get-os)
- [liff.getAppLanguage()](https://developers.line.biz/en/reference/liff/#get-app-language)
- [liff.getLanguage()](https://developers.line.biz/en/reference/liff/#get-language) (deprecated)
- [liff.getVersion()](https://developers.line.biz/en/reference/liff/#get-version)
- [liff.getLineVersion()](https://developers.line.biz/en/reference/liff/#get-line-version)
- [liff.isInClient()](https://developers.line.biz/en/reference/liff/#is-in-client)
- [liff.closeWindow()](https://developers.line.biz/en/reference/liff/#close-window)
- [liff.use()](https://developers.line.biz/en/reference/liff/#use)
- [liff.i18n.setLang()](https://developers.line.biz/en/reference/liff/#i18n-set-lang)

To use the `liff.closeWindow()` method before the initialization of the LIFF app by `liff.init()` has finished, your LIFF SDK version must be v2.4.0 or later.

<!-- tip end -->

_Example_

<!-- tab start `javascript` -->

```javascript
// Using a Promise object
liff
  .init({
    liffId: "123456-abcedfg", // Use own liffId
  })
  .then(() => {
    // Start to use liff's api
  })
  .catch((err) => {
    // Error happens during initialization
    console.log(err.code, err.message);
  });

// Using a callback
liff.init({ liffId: "123456-abcedfg" }, successCallback, errorCallback);
```

<!-- tab end -->

#### Syntax 

```javascript
liff.init(config, successCallback, errorCallback);
```

#### Arguments 

<!-- parameter start (props: required) -->

config

Object

LIFF app configurations

<!-- parameter end -->
<!-- parameter start (props: required) -->

config.liffId

String

LIFF app ID. Can be obtained when you add the LIFF app to your channel. For more information, see [Adding a LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/).\
The LIFF app ID specified here can be obtained with [`liff.id`](https://developers.line.biz/en/reference/liff/#id).

<!-- parameter end -->
<!-- parameter start (props: optional) -->

config.withLoginOnExternalBrowser

Boolean

Using either of the following values, specify whether or not to automatically execute the `liff.login()` method when initializing a LIFF app in an external browser. The default value is `false`.

- `true`: Automatically execute the `liff.login()` method in external browsers.
- `false`: Don't automatically execute the `liff.login()` method in external browsers.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

successCallback

Function

Callback to return a data object upon successful initialization of the LIFF app.

<!-- note start -->

**Note**

successCallback is processed at the same time that the `Promise` object of the return value is resolved. However, there is no set order to which is processed first.

<!-- note end -->

<!-- parameter end -->
<!-- parameter start (props: optional) -->

errorCallback

Function

Callback to return an error object upon failure to initialize the LIFF app.

<!-- note start -->

**Note**

errorCallback is processed at the same time that the `Promise` object of the return value is rejected. However, there is no set order to which is processed first.

<!-- note end -->

<!-- parameter end -->

#### Return value 

Returns a `Promise` object.

##### Error response 

When the `Promise` is rejected, [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-errors) is passed.

## Getting environment 

### liff.getOS() 

Gets the environment in which the user is running the LIFF app.

<!-- tip start -->

**This method can be used before the LIFF app is initialized**

You can use this method even before the initialization of the LIFF app by `liff.init()` has finished.

<!-- tip end -->

#### Syntax 

```javascript
liff.getOS();
```

#### Arguments 

None

#### Return value 

The environment in which the user is running the LIFF app is returned as a string. Since the return value is based on the name of the OS in the user agent string, the return value is independent of the browser type ([LIFF browser](https://developers.line.biz/en/glossary/#liff-browser), [LINE's in-app browser](https://developers.line.biz/en/glossary/#line-iab), [external browser](https://developers.line.biz/en/glossary/#external-browser)).

For example, if the user is using iOS, `ios` will be returned, regardless of whether the user is using LIFF browser or Safari.

| Return value | Description          |
| ------------ | -------------------- |
| ios          | iOS or iPadOS        |
| android      | Android              |
| web          | Other than the above |

For more information about LIFF app supported operating systems and browsers, see [Operating environment](https://developers.line.biz/en/docs/liff/overview/#operating-environment).

### liff.getAppLanguage() 

Gets the language setting of the LINE app running the LIFF app.

<!-- tip start -->

**This method can be used before the LIFF app is initialized**

You can use this method even before the initialization of the LIFF app by `liff.init()` has finished.

<!-- tip end -->

#### Conditions of use 

LIFF SDK versions v2.24.0 or later

#### Operating conditions 

All of the following conditions must be met for the `liff.getAppLanguage()` method to work correctly:

- The LIFF application is running on the [LIFF browser](https://developers.line.biz/en/glossary/#liff-browser).
- The LINE app version is 14.11.0 or later.

If the above conditions aren't met, the `liff.getAppLanguage()` method behaves the same as the [`liff.getLanguage()`](https://developers.line.biz/en/reference/liff/#get-language) method.

#### Syntax 

```javascript
liff.getAppLanguage();
```

#### Arguments 

None

#### Return value 

The language setting of the LINE app running the LIFF app is returned as a string that follows [RFC 5646](https://datatracker.ietf.org/doc/html/rfc5646).

### liff.getLanguage() 

<!-- note start -->

**The liff.getLanguage() method is deprecated**

The `liff.getLanguage()` method is deprecated. To get the language setting of the environment in which the LIFF app is running, use the [`liff.getAppLanguage()`](https://developers.line.biz/en/reference/liff/#get-app-language) method. For more information, see the news from [July 23, 2024](https://developers.line.biz/en/news/2024/07/23/release-liff-2-24-0/).

<!-- note end -->

Gets the language setting of the environment in which the LIFF app is running.

<!-- tip start -->

**This method can be used before the LIFF app is initialized**

You can use this method even before the initialization of the LIFF app by `liff.init()` has finished.

<!-- tip end -->

#### Syntax 

```javascript
liff.getLanguage();
```

#### Arguments 

None

#### Return value 

String containing language settings specified in `navigator.language` in the LIFF app's running environment.

### liff.getVersion() 

Gets the version of the LIFF SDK.

<!-- tip start -->

**This method can be used before the LIFF app is initialized**

You can use this method even before the initialization of the LIFF app by `liff.init()` has finished.

<!-- tip end -->

#### Syntax 

```javascript
liff.getVersion();
```

#### Arguments 

None

#### Return value 

The version of the LIFF SDK is returned as a string.

### liff.getLineVersion() 

Gets the user's LINE version.

<!-- tip start -->

**This method can be used before the LIFF app is initialized**

You can use this method even before the initialization of the LIFF app by `liff.init()` has finished.

<!-- tip end -->

#### Syntax 

```javascript
liff.getLineVersion();
```

#### Arguments 

None

#### Return value 

If a user opens the LIFF app using a LIFF browser, the LINE version of the user is returned as a string. If a user opens the LIFF app using an external browser, `null` is returned.

### liff.getContext() 

Gets the screen type (1-on-1 chat, group chat, multi-person chat, or external browser) from which the LIFF app is launched.

<!-- warning start -->

**We've discontinued providing company internal identifiers of chat rooms to LIFF apps**

We've discontinued providing company internal identifiers of chat rooms (one-on-one chat ID, group ID, and room ID) to LIFF apps. For more information, see the news from February 6, 2023, [We've discontinued providing company internal identifiers of chat rooms to LIFF apps as of February 6, 2023](https://developers.line.biz/en/news/2023/02/06/liff-spec-change/).

<!-- warning end -->

_Example_

<!-- tab start `javascript` -->

```javascript
const context = liff.getContext();
console.log(context);
```

<!-- tab end -->

#### Syntax 

```javascript
liff.getContext();
```

#### Arguments 

None

#### Return value 

A data object that contains the information necessary to make various API calls.

<!-- parameter start -->

type

String

The type of screen from where the LIFF app was launched. One of:

- `utou`: 1-on-1 chat.
- `group`: Group chat.
- `room`: Multi-person chat.
- `external`: External browser.
- `none`: A screen other than a 1-on-1 chat, group chat, multi-person chat, or external browser. For example, Wallet tab.

This property is also returned for LIFF apps after transitioning between LIFF apps.

<!-- parameter end -->
<!-- parameter start -->

userId

String

User ID. Included when the `type` property is `utou`, `room`, `group`, `none` or `external`. However, null may be returned when `type` is `external`.

<!-- parameter end -->
<!-- parameter start -->

liffId

String

LIFF ID.

<!-- parameter end -->
<!-- parameter start -->

viewType

String

Size of the LIFF app view, only returned if the `type` property isn't `external`. One of:

- `compact`
- `tall`
- `full`

For more information, see [Adding a LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/).

<!-- parameter end -->
<!-- parameter start -->

endpointUrl

String

URL of the service endpoint.

<!-- parameter end -->
<!-- parameter start -->

accessTokenHash

String

First half of the hashed SHA256 value of the access token. Used to validate the access token.

<!-- parameter end -->
<!-- parameter start -->

availability

Object

Returns the [`availability` object](https://developers.line.biz/en/reference/liff/#get-context-return-value-availability) that indicates whether the LIFF features are available in the environment in which the LIFF app was launched.

<!-- parameter end -->
<!-- parameter start -->

scope

Array of strings

Returns which of the scopes the LIFF app has within the scope required to use some of the LIFF SDK methods:

- `openid`: Scope required to use [`liff.getIDToken()`](https://developers.line.biz/en/reference/liff/#get-id-token) and [`liff.getDecodedIDToken()`](https://developers.line.biz/en/reference/liff/#get-decoded-id-token)
- `email`: Scope required to get the user's email address using [`liff.getIDToken()`](https://developers.line.biz/en/reference/liff/#get-id-token) or [`liff.getDecodedIDToken()`](https://developers.line.biz/en/reference/liff/#get-decoded-id-token)
- `profile`: Scope required to use [`liff.getProfile()`](https://developers.line.biz/en/reference/liff/#get-profile) or [`liff.getFriendship()`](https://developers.line.biz/en/reference/liff/#get-friendship)
- `chat_message.write`: Scope required to use [`liff.sendMessages()`](https://developers.line.biz/en/reference/liff/#send-messages)

For more information about scope, see [Adding the LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/#registering-liff-app) in the LIFF documentation.

<!-- tip start -->

**Difference between liff.getContext() and liff.permission.getGrantedAll()**

The `liff.getContext()` method gets a list of scopes for the LIFF app (\*).

On the other hand, the [`liff.permission.getGrantedAll()`](https://developers.line.biz/en/reference/liff/#permission-get-granted-all) method gets a list of scopes for which the user has agreed to grant permission among the scopes for the LIFF app.

\* The scopes specified in the "Scope" section under the **LIFF** tab in a LINE Login channel

<!-- tip end -->

<!-- parameter end -->
<!-- parameter start -->

menuColorSetting

Object

Returns the color setting of the LIFF browser header as a [`menuColorSetting` object](https://developers.line.biz/en/reference/liff/#get-context-return-value-menucolorsetting).

Note that we currently don't provide the ability to change the header color setting.

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

miniAppId

String

Returns the string set by the Custom Path feature of the LINE MINI App. For more information about the Custom Path feature, see [Configuring Custom Path](https://developers.line.biz/en/docs/line-mini-app/develop/custom-path/) in the LINE MINI App documentation.

<!-- parameter end -->
<!-- parameter start -->

miniDomainAllowed

Boolean

Returns whether the LINE MINI App is available on the `miniapp.line.me` domain.

<!-- parameter end -->
<!-- parameter start -->

permanentLinkPattern

String

How additional information in LIFF URLs is handled. `concat` is returned.

For more information, see [Opening a LIFF app](https://developers.line.biz/en/docs/liff/opening-liff-app/) in the LIFF documentation.

<!-- parameter end -->
<!-- parameter start (props: annotation="Discontinued") -->

utouId

String

This property was discontinued. For more information, see the news from February 6, 2023, [We've discontinued providing company internal identifiers of chat rooms to LIFF apps as of February 6, 2023](https://developers.line.biz/en/news/2023/02/06/liff-spec-change/).

<!-- parameter end -->
<!-- parameter start (props: annotation="Discontinued") -->

groupId

String

This property was discontinued. For more information, see the news from February 6, 2023, [We've discontinued providing company internal identifiers of chat rooms to LIFF apps as of February 6, 2023](https://developers.line.biz/en/news/2023/02/06/liff-spec-change/).

<!-- parameter end -->
<!-- parameter start (props: annotation="Discontinued") -->

roomId

String

This property was discontinued. For more information, see the news from February 6, 2023, [We've discontinued providing company internal identifiers of chat rooms to LIFF apps as of February 6, 2023](https://developers.line.biz/en/news/2023/02/06/liff-spec-change/).

<!-- parameter end -->

_Example (LIFF browser)_

<!-- tab start `json` -->

```json
{
  "type": "utou",
  "utouId": "e2bff570-...",
  "userId": "U850014438e...",
  "liffId": "123456-abcedfg",
  "viewType": "full",
  "endpointUrl": "https://example.com/",
  "accessTokenHash": "EVWYWo1yYA...",
  "availability": {
    "shareTargetPicker": {
      "permission": true,
      "minVer": "10.3.0"
    },
    "multipleLiffTransition": {
      "permission": true,
      "minVer": "10.18.0"
    },
    "subwindowOpen": {
      "permission": true,
      "minVer": "11.7.0"
    },
    "scanCode": {
      "permission": false,
      "minVer": "9.4.0",
      "unsupportedFromVer": "9.19.0"
    },
    "scanCodeV2": {
      "permission": true,
      "minVer": "11.7.0",
      "minOsVer": "14.3.0"
    },
    "getAdvertisingId": {
      "permission": false,
      "minVer": "7.14.0"
    },
    "addToHomeScreen": {
      "permission": false,
      "minVer": "9.16.0"
    },
    "bluetoothLeFunction": {
      "permission": false,
      "minVer": "9.14.0",
      "unsupportedFromVer": "9.19.0"
    },
    "skipChannelVerificationScreen": {
      "permission": false,
      "minVer": "11.14.0"
    },
    "addToHomeV2": {
      "permission": false,
      "minVer": "13.20.0"
    },
    "addToHomeHideDomain": {
      "permission": false,
      "minVer": "13.20.0"
    },
    "addToHomeLineScheme": {
      "permission": false,
      "minVer": "13.20.0"
    }
  },
  "scope": [
    "chat_message.write",
    "openid",
    "profile"
  ],
  "menuColorSetting": {
    "adaptableColorSchemes": [
      "light"
    ],
    "lightModeColor": {
      "iconColor": "#111111",
      "statusBarColor": "black",
      "titleTextColor": "#111111",
      "titleSubtextColor": "#B7B7B7",
      "titleButtonColor": "#111111",
      "titleBackgroundColor": "#FFFFFF",
      "progressBarColor": "#06C755",
      "progressBackgroundColor": "#FFFFFF"
    },
    "darkModeColor": {
      "iconColor": "#FFFFFF",
      "statusBarColor": "white",
      "titleTextColor": "#FFFFFF",
      "titleSubtextColor": "#949494",
      "titleButtonColor": "#FFFFFF",
      "titleBackgroundColor": "#111111",
      "progressBarColor": "#06C755",
      "progressBackgroundColor": "#111111"
    }
  },
  "miniDomainAllowed": false,
  "permanentLinkPattern": "concat"
}
```

<!-- tab end -->

_Example (external browser)_

<!-- tab start `json` -->

```json
{
  "type": "external",
  "liffId": "123456-abcedfg",
  "endpointUrl": "https://example.com/",
  "accessTokenHash": "EVWYWo1yYA...",
  "availability": {
    "shareTargetPicker": {
      "permission": true,
      "minVer": "10.3.0"
    },
    "multipleLiffTransition": {
      "permission": true,
      "minVer": "10.18.0"
    },
    "subwindowOpen": {
      "permission": true,
      "minVer": "11.7.0"
    },
    "scanCode": {
      "permission": true,
      "minVer": "9.4.0",
      "unsupportedFromVer": "9.19.0"
    },
    "scanCodeV2": {
      "permission": true,
      "minVer": "11.7.0",
      "minOsVer": "14.3.0"
    },
    "getAdvertisingId": {
      "permission": false,
      "minVer": "7.14.0"
    },
    "addToHomeScreen": {
      "permission": false,
      "minVer": "9.16.0"
    },
    "bluetoothLeFunction": {
      "permission": false,
      "minVer": "9.14.0",
      "unsupportedFromVer": "9.19.0"
    },
    "skipChannelVerificationScreen": {
      "permission": false,
      "minVer": "11.14.0"
    },
    "addToHomeV2": {
      "permission": false,
      "minVer": "13.20.0"
    },
    "addToHomeHideDomain": {
      "permission": false,
      "minVer": "13.20.0"
    },
    "addToHomeLineScheme": {
      "permission": false,
      "minVer": "13.20.0"
    }
  },
  "scope": [
    "chat_message.write",
    "openid",
    "profile"
  ],
  "menuColorSetting": {
    "adaptableColorSchemes": [
      "light"
    ],
    "lightModeColor": {
      "iconColor": "#111111",
      "statusBarColor": "black",
      "titleTextColor": "#111111",
      "titleSubtextColor": "#B7B7B7",
      "titleButtonColor": "#111111",
      "titleBackgroundColor": "#FFFFFF",
      "progressBarColor": "#06C755",
      "progressBackgroundColor": "#FFFFFF"
    },
    "darkModeColor": {
      "iconColor": "#FFFFFF",
      "statusBarColor": "white",
      "titleTextColor": "#FFFFFF",
      "titleSubtextColor": "#949494",
      "titleButtonColor": "#FFFFFF",
      "titleBackgroundColor": "#111111",
      "progressBarColor": "#06C755",
      "progressBackgroundColor": "#111111"
    }
  },
  "miniDomainAllowed": false,
  "permanentLinkPattern": "concat"
}
```

<!-- tab end -->

#### `availability` object 

The `availability` object contains the following properties:

<!-- parameter start -->

shareTargetPicker

Object

Returns the [object](https://developers.line.biz/en/reference/liff/#get-context-return-value-availability-common) that indicates whether [`liff.shareTargetPicker()`](https://developers.line.biz/en/reference/liff/#share-target-picker) is available in the environment in which the LIFF app was launched.

\* To get information about the availability of `liff.shareTargetPicker()`, we highly recommend using [liff.isApiAvailable('shareTargetPicker')](https://developers.line.biz/en/reference/liff/#is-api-available) instead.

<!-- parameter end -->
<!-- parameter start -->

multipleLiffTransition

Object

Returns the [object](https://developers.line.biz/en/reference/liff/#get-context-return-value-availability-common) that indicates whether it's possible to [transition to another LIFF app](https://developers.line.biz/en/docs/liff/opening-liff-app/#move-liff-to-liff) with [`liff.openWindow()`](https://developers.line.biz/en/reference/liff/#open-window) without closing the LIFF app within the LIFF browser in the environment in which the LIFF app was launched.

\* To get information about the availability of a transition between multiple LIFF apps, we highly recommend using [liff.isApiAvailable('multipleLiffTransition')](https://developers.line.biz/en/reference/liff/#is-api-available) instead.

<!-- parameter end -->
<!-- parameter start -->

subwindowOpen

Object

Returns the [object](https://developers.line.biz/en/reference/liff/#get-context-return-value-availability-common) that indicates whether the subwindow is available in the environment in which the LIFF app was launched.

<!-- parameter end -->
<!-- parameter start -->

scanCode

Object

Returns the [object](https://developers.line.biz/en/reference/liff/#get-context-return-value-availability-common) that indicates whether [`liff.scanCode()`](https://developers.line.biz/en/reference/liff/#scan-code) is available in the environment in which the LIFF app was launched.

<!-- parameter end -->
<!-- parameter start -->

scanCodeV2

Object

Returns the [object](https://developers.line.biz/en/reference/liff/#get-context-return-value-availability-common) that indicates whether [`liff.scanCodeV2()`](https://developers.line.biz/en/reference/liff/#scan-code-v2) is available in the environment in which the LIFF app was launched.

<!-- parameter end -->
<!-- parameter start -->

getAdvertisingId

Object

Returns the [object](https://developers.line.biz/en/reference/liff/#get-context-return-value-availability-common) that indicates whether `liff.getAid()` is available in the environment in which the LIFF app was launched.

Note that we currently don't provide `liff.getAid()`.

<!-- parameter end -->
<!-- parameter start -->

addToHomeScreen

String

Returns the [object](https://developers.line.biz/en/reference/liff/#get-context-return-value-availability-common) that indicates whether `liff.addToHomeScreen()` is available in the environment in which the LIFF app was launched.

Note that we currently don't provide `liff.addToHomeScreen()`.

<!-- parameter end -->
<!-- parameter start -->

bluetoothLeFunction

Object

Returns the [object](https://developers.line.biz/en/reference/liff/#get-context-return-value-availability-common) that indicates whether Bluetooth® Low Energy for LINE Things is available in the environment in which the LIFF app was launched.

Note that we currently don't provide this feature.

<!-- parameter end -->
<!-- parameter start -->

skipChannelVerificationScreen

Object

Returns the [object](https://developers.line.biz/en/reference/liff/#get-context-return-value-availability-common) that indicates whether the "Channel consent simplification" feature is available in the environment in which the LIFF app was launched. For more information, see [Skipping the channel consent process](https://developers.line.biz/en/docs/line-mini-app/develop/channel-consent-simplification/) in the LINE MINI App documentation.

<!-- parameter end -->
<!-- parameter start -->

addToHomeV2

Object

Returns the [object](https://developers.line.biz/en/reference/liff/#get-context-return-value-availability-common) that indicates whether [`liff.createShortcutOnHomeScreen()`](https://developers.line.biz/en/reference/liff/#create-shortcut-on-home-screen) is available in the environment in which the LIFF app was launched.

\* To get information about the availability of `liff.createShortcutOnHomeScreen()`, we highly recommend using [liff.isApiAvailable('createShortcutOnHomeScreen')](https://developers.line.biz/en/reference/liff/#is-api-available) instead.

<!-- parameter end -->
<!-- parameter start -->

addToHomeHideDomain

Object

Returns the [object](https://developers.line.biz/en/reference/liff/#get-context-return-value-availability-common) that indicates whether the endpoint URL can be hidden when displaying a screen for adding a shortcut to the home screen of the user's device.

Note that we currently don't provide this feature.

<!-- parameter end -->
<!-- parameter start -->

addToHomeLineScheme

Object

Returns the [object](https://developers.line.biz/en/reference/liff/#get-context-return-value-availability-common) that indicates whether creating a shortcut specifying the [LINE URL scheme](https://developers.line.biz/en/docs/line-login/using-line-url-scheme/) is available.

Note that we currently don't provide this feature.

<!-- parameter end -->

_Example_

<!-- tab start `json` -->

```json
{
  "shareTargetPicker": {
    "permission": true,
    "minVer": "10.3.0"
  }
}
```

<!-- tab end -->

#### Common properties of the `availability` object 

<!-- parameter start -->

permission

Boolean

Specifies whether the feature specified by the property name of the `availability` object is available in the environment in which the LIFF app was launched.

- `true`: The feature is available.
- `false`: The feature isn't available.

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

minVer

String

The minimum LINE version that supports the corresponding feature.

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

maxVer

String

The maximum LINE version that supports the corresponding feature.

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

unsupportedFromVer

String

The LINE version for which the corresponding feature is no longer supported.

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

minOsVer

String

The minimum OS version that supports the corresponding feature.

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

maxOsVer

String

The maximum OS version that supports the corresponding feature.

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

unsupportedFromOsVer

String

The OS version for which the corresponding feature is no longer supported.

<!-- parameter end -->

#### `menuColorSetting` object 

The `menuColorSetting` object contains the following properties:

<!-- parameter start -->

adaptableColorSchemes

Array of strings

Always returns `light`.

<!-- parameter end -->
<!-- parameter start -->

lightModeColor

Object

Returns the header color setting as [object](https://developers.line.biz/en/reference/liff/#get-context-return-value-menucolorsetting-common) when `adaptableColorSchemes` is `light`.

<!-- parameter end -->
<!-- parameter start -->

darkModeColor

Object

Returns the header color setting as [object](https://developers.line.biz/en/reference/liff/#get-context-return-value-menucolorsetting-common) when `adaptableColorSchemes` is `dark`.

Note that we currently don't provide the header color setting.

<!-- parameter end -->

_Example_

<!-- tab start `json` -->

```json
{
  "adaptableColorSchemes": [
    "light"
  ],
  "lightModeColor": {
    "iconColor": "#111111",
    "statusBarColor": "black",
    "titleTextColor": "#111111",
    "titleSubtextColor": "#B7B7B7",
    "titleButtonColor": "#111111",
    "titleBackgroundColor": "#FFFFFF",
    "progressBarColor": "#06C755",
    "progressBackgroundColor": "#FFFFFF"
  },
  "darkModeColor": {
    "iconColor": "#FFFFFF",
    "statusBarColor": "white",
    "titleTextColor": "#FFFFFF",
    "titleSubtextColor": "#949494",
    "titleButtonColor": "#FFFFFF",
    "titleBackgroundColor": "#111111",
    "progressBarColor": "#06C755",
    "progressBackgroundColor": "#111111"
  }
}
```

<!-- tab end -->

#### Common properties of the `menuColorSetting` object 

<!-- parameter start -->

iconColor

String

The color of the header icon. The color is represented by a hexadecimal color code in the `#RRGGBB` format.

<!-- parameter end -->
<!-- parameter start -->

statusBarColor

String

Always returns `white`.

<!-- parameter end -->
<!-- parameter start -->

titleTextColor

String

The color of the header title text. The color is represented by a hexadecimal color code in the `#RRGGBB` format.

<!-- parameter end -->
<!-- parameter start -->

titleSubtextColor

String

The color of the header subtitle text. The color is represented by a hexadecimal color code in the `#RRGGBB` format.

<!-- parameter end -->
<!-- parameter start -->

titleButtonColor

String

The color of the header button. The color is represented by a hexadecimal color code in the `#RRGGBB` format.

<!-- parameter end -->
<!-- parameter start -->

titleBackgroundColor

String

The header background color. The color is represented by a hexadecimal color code in the `#RRGGBB` format.

<!-- parameter end -->
<!-- parameter start -->

progressBarColor

String

The color of the header progress bar. The color is represented by a hexadecimal color code in the `#RRGGBB` format.

<!-- parameter end -->
<!-- parameter start -->

progressBackgroundColor

String

The background color of the header progress bar. The color is represented by a hexadecimal color code in the `#RRGGBB` format.

<!-- parameter end -->

### liff.isInClient() 

Determines whether the LIFF app is running in a LIFF browser.

<!-- tip start -->

**This method can be used before the LIFF app is initialized**

You can use this method even before the initialization of the LIFF app by `liff.init()` has finished.

<!-- tip end -->

#### Syntax 

```javascript
liff.isInClient();
```

#### Arguments 

None

#### Return value 

- `true`: Running in [LIFF browser](https://developers.line.biz/en/glossary/#liff-browser)
- `false`: Running in [external browser](https://developers.line.biz/en/glossary/#external-browser) or [LINE's in-app browser](https://developers.line.biz/en/glossary/#line-iab)

### liff.isLoggedIn() 

Checks whether the user is logged in.

_Example_

<!-- tab start `javascript` -->

```javascript
if (liff.isLoggedIn()) {
  // The user can use an API that requires an access token, such as liff.getProfile().
}
```

<!-- tab end -->

#### Syntax 

```javascript
liff.isLoggedIn();
```

#### Arguments 

None

#### Return value 

- `true`: The user is logged in.
- `false`: The user is not logged in.

### liff.isApiAvailable() 

Checks whether the specified API or feature is available in the environment where you started the LIFF app. Specifically, it verifies whether the current LINE version supports the API and whether the terms and conditions for the API have been accepted.

_Example_

<!-- tab start `javascript` -->

```javascript
// Check if shareTargetPicker is available
if (liff.isApiAvailable('shareTargetPicker')) {
  liff.shareTargetPicker([
    {
      type: "text",
      text: "Hello, World!"
    }
  ])
    .then(
      console.log("ShareTargetPicker was launched")
    ).catch(function(res) {
      console.log("Failed to launch ShareTargetPicker")
    })
}

// Check if the LIFF-to-LIFF transition is available
if (liff.isApiAvailable('multipleLiffTransition')) {
  window.location.href = "https://line.me/{liffId}", // URL for another LIFF app
}
```

<!-- tab end -->

#### Syntax 

```javascript
liff.isApiAvailable(apiName);
```

#### Arguments 

<!-- parameter start (props: required) -->

apiName

String

The name of the LIFF client API or feature. You can specify one of the following:

- `createShortcutOnHomeScreen`: Whether the [`liff.createShortcutOnHomeScreen()`](https://developers.line.biz/en/reference/liff/#create-shortcut-on-home-screen) method is available
- `scanCodeV2`: Whether the [`liff.scanCodeV2()`](https://developers.line.biz/en/reference/liff/#scan-code-v2) method is available
- `scanCode`: Whether the [`liff.scanCode()`](https://developers.line.biz/en/reference/liff/#scan-code) method is available
- `shareTargetPicker`: Whether the [`liff.shareTargetPicker()`](https://developers.line.biz/en/reference/liff/#share-target-picker) method is available
- `iap`: Whether the [in-app purchase](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/overview/) feature for the LINE MINI App is available
- `multipleLiffTransition`: Whether the [LIFF-to-LIFF transition](https://developers.line.biz/en/docs/liff/opening-liff-app/#move-liff-to-liff) is available
- `skipChannelVerificationScreen`: Whether the [channel consent simplification](https://developers.line.biz/en/docs/line-mini-app/develop/channel-consent-simplification/#what-is-channel-consent-simplification) feature for the LINE MINI App is available

<!-- parameter end -->

#### Return value 

Returns whether the specified API or feature is available in the current environment. If available, `true` is returned. If not, `false` is returned. Examples of `false` returned are as follows:

- If the LIFF app was launched with a LINE version that doesn't support the API
- If the LIFF app was launched in an external browser, even though the API isn't available in an external browser
- If the terms and conditions haven't been accepted, even though you must accept them to use the API
- If the user isn't logged in, even though the user must be logged in to use the API
- If the access token is expired, even though the access token must be valid to use the API

## Authentication 

### liff.login() 

Performs the login process in the [LINE's in-app browser](https://developers.line.biz/en/glossary/#line-iab) or [external browser](https://developers.line.biz/en/glossary/#external-browser).

<!-- note start -->

**Note**

You can't use `liff.login()` in a LIFF browser, as it is automatically executed when `liff.init()` is executed.

<!-- note end -->

<!-- note start -->

**Authorization requests within LIFF browser**

The behavior of LINE Login authorization requests within the LIFF browser isn't guaranteed. Also, when opening LIFF apps from an external browser or LINE's in-app browser, make sure to use this method for the login process, not the [authorization requests with LINE Login](https://developers.line.biz/en/docs/line-login/integrate-line-login/#making-an-authorization-request).

<!-- note end -->

_Example_

<!-- tab start `javascript` -->

```javascript
if (!liff.isLoggedIn()) {
  liff.login({ redirectUri: "https://example.com/path" });
}
```

<!-- tab end -->

#### Syntax 

```javascript
liff.login(loginConfig);
```

#### Arguments 

<!-- parameter start (props: optional) -->

loginConfig

Object

Login configurations

<!-- parameter end -->
<!-- parameter start (props: optional) -->

loginConfig.redirectUri

String

URL to open in the LIFF app after logging in. The default value is the URL set in **Endpoint URL**. For more information on how to set **Endpoint URL**, see [Adding a LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/#registering-liff-app) in the LIFF documentation.

If the URL specified in `redirectUri` doesn't start with the URL specified in **Endpoint URL**, the login process fails and an error screen is displayed.

![](https://developers.line.biz/media/liff/liff_login_error_screen.png)

For example, if **Endpoint URL** is `https://example.com/path1/path2?query1=value1`, the success or failure of the login process is as follows. Query parameters and URL fragments don't affect the success or failure of the login process.

<table>
  <thead>
    <tr>
      <th>redirectUri</th>
      <th>Login process</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <ul>
          <li>https://example.com/path1/path2?query1=value1</li>
          <li>https://example.com/path1/path2?query2=value2</li>
          <li>https://example.com/path1/path2#URL-fragment</li>
          <li>https://example.com/path1/path2</li>
          <li>https://example.com/path1/path2/</li>
          <li>https://example.com/path1/path2/path3</li>
        </ul>
      </td>
      <td>✅ Success</td>
    </tr>
    <tr>
      <td>
        <ul>
          <li>https://example.com/path1</li>
          <li>https://example.com/</li>
          <li>https://example.com/path2/path1</li>
        </ul>
      </td>
      <td>❌ Failure</td>
    </tr>
  </tbody>
</table>

<!-- parameter end -->

#### Return value 

None

### liff.logout() 

Logs out.

_Example_

<!-- tab start `javascript` -->

```javascript
if (liff.isLoggedIn()) {
  liff.logout();
}
```

<!-- tab end -->

#### Syntax 

```javascript
liff.logout();
```

#### Arguments 

None

#### Return value 

None

### liff.getAccessToken() 

Gets the current user's access token.

You can use the access token obtained with this API to send user data from the LIFF app to the server. For more information, see [Using user data in LIFF apps and servers](https://developers.line.biz/en/docs/liff/using-user-profile/) in the LIFF documentation.

<!-- note start -->

**Validity period of the access token**

The access token is valid for 12 hours after being issued. When the user closes the LIFF app, the access token may be revoked even if it hasn't expired yet. For more information, see [Behavior when closing the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#behavior-when-closing-liff-app) in the LIFF documentation.

<!-- note end -->

<!-- tip start -->

**Getting an access token**

- If the user starts the LIFF app in a LIFF browser, the LIFF SDK will get an access token when you call [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app).
- If the user starts the LIFF app in an external browser, the LIFF SDK will get an access token when these steps are satisfied:
  1. You call [`liff.login()`](https://developers.line.biz/en/reference/liff/#login).
  2. The user logs in.
  3. You call [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app).

<!-- tip end -->

_Example_

<!-- tab start `javascript` -->

```javascript
const accessToken = liff.getAccessToken();
if (accessToken) {
  fetch("https://api...", {
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${accessToken}`,
    },
    //...
  });
}
```

<!-- tab end -->

#### Syntax 

```javascript
liff.getAccessToken();
```

#### Arguments 

None

#### Return value 

Returns the current user's access token as a string.

### liff.getIDToken() 

Get the ID token of the current user obtained by the LIFF SDK. An ID token is a JSON Web Token (JWT) that contains user data.

You can use the ID token obtained with this API when sending the user data from the LIFF app to the server. For more information, see [Using user data in LIFF apps and servers](https://developers.line.biz/en/docs/liff/using-user-profile/) in the LIFF documentation.

<!-- note start -->

**Select a scope**

When [adding a LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/), select the `openid` scope. You can't get the ID tokens if you don't select the scope, or the users don't grant permission. The scope selections can be changed in the LIFF tab of the [LINE Developers Console](https://developers.line.biz/console/) even after adding the LIFF app.

<!-- note end -->

<!-- tip start -->

**Getting an ID token**

- If the user starts the LIFF app in a LIFF browser, the LIFF SDK will get an ID token when you call [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app).
- If the user starts the LIFF app in an external browser, the LIFF SDK will get an ID token when these steps are satisfied:

  1. You call [`liff.login()`](https://developers.line.biz/en/reference/liff/#login).
  2. The user logs in.
  3. You call [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app).

<!-- tip end -->

<!-- tip start -->

**You can get the user's email address**

To get the email addresses of users, select the `email` scope when [adding a LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/). You will get the email addresses once the users grant permission. The scope selections can be changed in the LIFF tab of the [LINE Developers Console](https://developers.line.biz/console/) even after adding the LIFF app.

<!-- tip end -->

_Example_

<!-- tab start `javascript` -->

```javascript
liff
  .init({
    liffId: "123456-abcedfg", // Use own liffId
  })
  .then(() => {
    const idToken = liff.getIDToken();
    console.log(idToken); // print idToken object
  });
```

<!-- tab end -->

#### Syntax 

```javascript
liff.getIDToken();
```

#### Argument 

None

#### Return value 

Returns an ID token.

### liff.getDecodedIDToken() 

Gets the payload of the ID token that's acquired by the LIFF SDK. The payload includes information such as user display name, profile image URL, email address, etc.

Use this method when you want to use the display name of the user in the LIFF app.

You can only get the main profile information. You can't get the user's [subprofile](https://developers.line.biz/en/glossary/#subprofile).

<!-- warning start -->

**Don't send user info to server**

Don't send the user data obtained by this method to the server. For more information, see [Using user data in LIFF apps and servers](https://developers.line.biz/en/docs/liff/using-user-profile/) in the LIFF documentation.

<!-- warning end -->

<!-- note start -->

**Select a scope**

When [adding a LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/), select the `openid` scope. You can't get the ID tokens if you don't select the scope, or users don't grant permission. The scope selections can be changed in the LIFF tab of the [LINE Developers Console](https://developers.line.biz/console/) even after adding the LIFF app.

<!-- note end -->

<!-- tip start -->

**Getting an ID token**

- If the user starts the LIFF app in a LIFF browser, the LIFF SDK will get an ID token when you call [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app).
- If the user starts the LIFF app in an external browser, the LIFF SDK will get an ID token when these steps are satisfied:

  1. You call [`liff.login()`](https://developers.line.biz/en/reference/liff/#login).
  2. The user logs in.
  3. You call [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app).

<!-- tip end -->

<!-- tip start -->

**You can get the user's email address**

To get the email addresses of users, select the `email` scope when [adding a LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/). You will get the email addresses once the users grant permission. The scope selections can be changed in the LIFF tab of the [LINE Developers Console](https://developers.line.biz/console/) even after adding the LIFF app.

<!-- tip end -->

_Example_

<!-- tab start `javascript` -->

```javascript
liff
  .init({
    liffId: "123456-abcedfg", // Use own liffId
  })
  .then(() => {
    const idToken = liff.getDecodedIDToken();
    console.log(idToken); // print decoded idToken object
  });
```

<!-- tab end -->

#### Syntax 

```javascript
liff.getDecodedIDToken();
```

#### Arguments 

None

#### Return value 

Gets the ID token payload.

For more information on ID token payloads, see the **Payload** section of [Get profile information from ID tokens](https://developers.line.biz/en/docs/line-login/verify-id-token/) in the Integrate LINE Login documentation.

_Example_

<!-- tab start `json` -->

```json
{
  "iss": "https://access.line.me",
  "sub": "U1234567890abcdef1234567890abcdef ",
  "aud": "1234567890",
  "exp": 1504169092,
  "iat": 1504263657,
  "amr": ["pwd"],
  "name": "Taro Line",
  "picture": "https://sample_line.me/aBcdefg123456"
}
```

<!-- tab end -->

### liff.permission.getGrantedAll() 

Gets a list of scopes for which the user has agreed to grant permission.

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

_Example_

<!-- tab start `javascript` -->

```javascript
liff.permission.getGrantedAll().then((scopes) => {
  // ["profile", "chat_message.write", "openid", "email"]
  console.log(scopes);
});
```

<!-- tab end -->

#### Syntax 

```javascript
liff.permission.getGrantedAll();
```

#### Arguments 

None

#### Return value 

When the `Promise` is resolved, an array of scopes for which the user has agreed to grant permission is passed.

##### Error response 

When the `Promise` is rejected, [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-errors) is passed.

### liff.permission.query() 

Verifies whether the user agrees to grant the specified permission.

_Example_

<!-- tab start `javascript` -->

```javascript
liff.permission.query("profile").then((permissionStatus) => {
  // permissionStatus = { state: 'granted' }
});
```

<!-- tab end -->

#### Syntax 

```javascript
liff.permission.query(permission);
```

#### Arguments 

<!-- parameter start (props: required) -->

permission

String

The permission to be checked. Specify one of the following scopes:

- [`profile`](https://developers.line.biz/en/docs/liff/registering-liff-apps/#registering-liff-app)
- [`chat_message.write`](https://developers.line.biz/en/docs/liff/registering-liff-apps/#registering-liff-app)
- [`openid`](https://developers.line.biz/en/docs/liff/registering-liff-apps/#registering-liff-app)
- [`email`](https://developers.line.biz/en/docs/liff/registering-liff-apps/#registering-liff-app)

<!-- parameter end -->

#### Return value 

`Promise` object returned.

When `Promise` is resolved, an object containing the following properties is returned.

<!-- parameter start -->

state

String

Contains one of the following values:

- `granted`: User has consented to the authorization.
- `prompt`: User hasn't consented to authorization.
- `unavailable`: Not available because the channel does not have the specified scope.

<!-- parameter end -->

### liff.permission.requestAll() 

Displays the "Verification screen" for the permissions requested by LINE MINI Apps.

![verification screen](https://developers.line.biz/media/line-mini-app/verification-screen-en.png)

<!-- note start -->

**Operating environment of liff.permission.requestAll()**

`liff.permission.requestAll()` only operates on [LINE MINI Apps](https://developers.line.biz/en/docs/line-mini-app/).

To execute this method, you need to turn on **Channel consent simplification** in advance on the [LINE Developers Console](https://developers.line.biz/console/). For more information on setting up the Channel consent simplification feature, see [The "Channel consent simplification" feature setup](https://developers.line.biz/en/docs/line-mini-app/develop/channel-consent-simplification/#simplification-feature-setup) of the LINE MINI App documentation.

<!-- note end -->

<!-- note start -->

**Make sure that the user has consented to all the permissions before executing this method**

If the user has already consented to all the permissions and you execute `liff.permission.requestAll()`, `Promise` will be rejected and [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-errors) will be returned. Therefore, use [`liff.permission.query()`](https://developers.line.biz/en/reference/liff/#permission-query) to check whether the user has consented to all the permissions, and execute `liff.permission.requestAll()` only if the user has unconsented permissions.

<!-- note end -->

_Example_

<!-- tab start `javascript` -->

```javascript
liff.permission.query("profile").then((permissionStatus) => {
  if (permissionStatus.state === "prompt") {
    liff.permission.requestAll();
  }
});
```

<!-- tab end -->

#### Syntax 

```javascript
liff.permission.requestAll();
```

#### Arguments 

None

#### Return value 

Returns a `Promise` object.

##### Error response 

If **Channel consent simplification** isn't turned on, and the user has already consented to all the permissions, `Promise` will be rejected and [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-errors) will be returned.

## Profile 

### liff.getProfile() 

Gets the current user's [profile information](https://developers.line.biz/en/glossary/#profile-information).

You can only get the main profile information. You can't get the user's [subprofile](https://developers.line.biz/en/glossary/#subprofile).

<!-- warning start -->

**Don't send user info to server**

Don't send the user data obtained by this method to the server. For more information, see [Using user data in LIFF apps and servers](https://developers.line.biz/en/docs/liff/using-user-profile/) in the LIFF documentation.

<!-- warning end -->

<!-- note start -->

**Select a scope**

When [adding a LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/), select the `profile` scope. You can't get user profiles if you don't select the scope, or the user doesn't grant permission. The scope selections can be changed in the LIFF tab of the [LINE Developers Console](https://developers.line.biz/console/) even after adding the LIFF app.

<!-- note end -->

_Example_

<!-- tab start `javascript` -->

```javascript
liff
  .getProfile()
  .then((profile) => {
    const name = profile.displayName;
  })
  .catch((err) => {
    console.log("error", err);
  });
```

<!-- tab end -->

#### Syntax 

```javascript
liff.getProfile();
```

#### Arguments 

None

#### Return value 

Returns a `Promise` object.

When the `Promise` is resolved, the object containing the user's profile information is passed.

<!-- parameter start -->

userId

String

User ID

<!-- parameter end -->
<!-- parameter start -->

displayName

String

Display name

<!-- parameter end -->
<!-- parameter start -->

pictureUrl

String

Image URL. This property is not returned if it has not been set by the user.

<!-- parameter end -->
<!-- parameter start -->

statusMessage

String

Status message. This property is not returned if it has not been set by the user.

<!-- parameter end -->

##### Error response 

When the `Promise` is rejected, [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-errors) is passed.

_Example_

<!-- tab start `json` -->

```json
{
  "userId": "U4af4980629...",
  "displayName": "Brown",
  "pictureUrl": "https://profile.line-scdn.net/abcdefghijklmn",
  "statusMessage": "Hello, LINE!"
}
```

<!-- tab end -->

### liff.getFriendship() 

Gets the friendship status between a user and a LINE Official Account.

However, you can only get the friendship status between a user and a LINE Official Account that has been linked to the same LINE Login channel to which your LIFF app has been added. To learn how to link a LINE Official Account to a LINE Login channel, see [Add a LINE Official Account as a friend when logged in (add friend option)](https://developers.line.biz/en/docs/line-login/link-a-bot/) in the LINE Login documentation.

<!-- note start -->

**Select a scope**

When [adding a LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/), select the `profile` scope. You can't get the friendship statuses if you don't select the scope, or the users don't grant permission. The scope selections can be changed in the LIFF tab of the [LINE Developers Console](https://developers.line.biz/console/) even after adding the LIFF app.

<!-- note end -->

_Example_

<!-- tab start `javascript` -->

```javascript
liff.getFriendship().then((data) => {
  if (data.friendFlag) {
    // something you want to do
  }
});
```

<!-- tab end -->

#### Syntax 

```javascript
liff.getFriendship();
```

#### Arguments 

None

#### Return value 

Returns a `Promise` object.

When acquiring the status of friendship, the `Promise` is resolved and the information about friendship is passed.

<!-- parameter start -->

friendFlag

Boolean

- `true`: The user has added the LINE Official Account as a friend and has not blocked it.
- Otherwise, `false`.

<!-- parameter end -->

##### Error response 

When the `Promise` is rejected, [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-errors) is passed.

_Example_

<!-- tab start `json` -->

```json
{
  "friendFlag": true
}
```

<!-- tab end -->

### liff.requestFriendship() 

Displays a subwindow that prompts the user to add the LINE Official Account as a friend, or to unblock it.

![](https://developers.line.biz/media/liff/request-friendship/request-friendship-add-friend-en.png)

- If the user has not added the LINE Official Account as a friend, a subwindow that prompts the user to add it as a friend is displayed.
- If the user has blocked the LINE Official Account, a subwindow that prompts the user to unblock it is displayed.
- If the user is already friends with the LINE Official Account, the subwindow is displayed and then automatically closed.

The LINE Official Account to prompt the user to add as a friend or unblock can be specified by [linking a LINE Official Account with your channel](https://developers.line.biz/en/docs/line-login/link-a-bot/#link-a-line-official-account). For more information, see [Add a LINE Official Account as a friend when logged in (add friend option)](https://developers.line.biz/en/docs/line-login/link-a-bot/) in the LINE Login documentation.

Only available when the screen size of the LIFF browser is `Full`. For more information, see [Size of the LIFF browser](https://developers.line.biz/en/docs/liff/overview/#screen-size) in the LIFF documentation.

_Example_

<!-- tab start `javascript` -->

```javascript
try {
  await liff.requestFriendship();
} catch (error) {
  console.log(error);
}
```

<!-- tab end -->

#### Syntax 

```javascript
liff.requestFriendship();
```

#### Arguments 

None

#### Return value 

Returns a `Promise` object.

<!-- note start -->

**The result of the user's action cannot be confirmed from the return value**

It isn't possible to confirm from the return value whether the user has added the LINE Official Account as a friend or unblocked it. To check the friendship status after calling the `liff.requestFriendship()` method, use the [`liff.getFriendship()`](https://developers.line.biz/en/reference/liff/#get-friendship) method.

<!-- note end -->

##### Error response 

When the `Promise` is rejected, [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-errors) is passed.

If the **Linked LINE Official Account** in the add friend option isn't set, or if the screen size of the LIFF app isn't `Full`, the error code `FORBIDDEN` is returned.

## Window 

### liff.openWindow() 

Opens the specified URL in the LINE's in-app browser or external browser.

<!-- note start -->

**Operating environment of liff.openWindow()**

Use of `liff.openWindow()` in an external browser isn't guaranteed.

<!-- note end -->

_Example_

<!-- tab start `javascript` -->

```javascript
liff.openWindow({
  url: "https://line.me",
  external: true,
});
```

<!-- tab end -->

#### Behavioral differences by LINE version 

The behavior of the `liff.openWindow()` method when opening URLs that support [Universal Links](https://developer.apple.com/documentation/xcode/allowing-apps-and-websites-to-link-to-your-content/) or [App Links](https://developer.android.com/training/app-links) varies depending on the LINE version and the setting of the [`params.external`](https://developers.line.biz/en/reference/liff/#open-window-arguments) parameter. The differences in behavior are as follows:

|  | `params.external = false`<br>(default) | `params.external = true` |
| --- | --- | --- |
| LINE earlier than 14.20.0 (\*) | <ul><li>iOS: Opens the URL in LINE's in-app browser</li><li>Android: Transitions to the corresponding app</li></ul> | <ul><li>iOS: Transitions to the corresponding app</li><li>Android: Opens the URL in the default browser</li></ul> |
| LINE 14.20.0 or later,<br>or earlier than 15.20.0| Transitions to the corresponding app | Transitions to the corresponding app |
| LINE 15.20.0 or later | Opens the URL in LINE's in-app browser | Transitions to the corresponding app |

\* On LINE version 14.20.0 or later, behavior no longer differs by OS.

#### Syntax 

```javascript
liff.openWindow(params);
```

#### Arguments 

<!-- parameter start (props: required) -->

params

Object

Parameter object

<!-- parameter end -->
<!-- parameter start (props: required) -->

params.url

String

URL. Specify a full URL.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

params.external

Boolean

Whether to open the URL in an external browser. Specify one of the following values. The default value is `false`.

- `true`: Opens the URL in an external browser.
- `false`: Opens the URL in the LINE's in-app browser.

<!-- parameter end -->

#### Return value 

None

### liff.closeWindow() 

Closes the LIFF app.

The behavior when closing the LIFF app depends on the LINE app version and the settings of the LIFF app. For more information, see [Behavior when closing the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#behavior-when-closing-liff-app) in the LIFF documentation.

<!-- tip start -->

**This method can be used before the LIFF app is initialized**

To use the `liff.closeWindow()` method before the initialization of the LIFF app by `liff.init()` has finished, your LIFF SDK version must be v2.4.0 or later.

<!-- tip end -->

<!-- note start -->

**Note**

`liff.closeWindow()` isn't guaranteed to work in an external browser.

<!-- note end -->

_Example_

<!-- tab start `javascript` -->

```javascript
liff.closeWindow();
```

<!-- tab end -->

#### Syntax 

```javascript
liff.closeWindow();
```

#### Arguments 

None

#### Return value 

None

## Message 

### liff.sendMessages() 

Sends messages on behalf of the user to the chat room where the LIFF app is opened.

To use this feature, the following conditions must be met:

- Within the LIFF browser for a LIFF app launched from a one-on-one chat, [group chat](https://developers.line.biz/en/glossary/#group), or [multi-person chat](https://developers.line.biz/en/glossary/#room)
- The [`chat_message.write` scope](https://developers.line.biz/en/docs/liff/registering-liff-apps/#registering-liff-app) is enabled
- The LIFF app hasn't been reloaded from the [recently used services](https://developers.line.biz/en/docs/liff/overview/#multi-tab-view-recent-service) section

If the conditions aren't met, the `liff.sendMessages()` method isn't available and `user doesn't grant required permissions yet` error with error code `403` will occur. The following are examples of cases that cause the error:

- When accessing the LIFF app using the [Keep Memo](https://help.line.me/line/smartphone/pc?lang=en&contentId=20017696) feature.
- When accessing a URL scheme for [opening a LIFF app](https://developers.line.biz/en/docs/line-login/using-line-url-scheme/#opening-a-liff-app) through a website redirection process, etc.
- When the `chat_message.write` scope is disabled after the LIFF-to-LIFF transition. For more information, see [About the "chat_message.write" scope after transitioning between LIFF apps](https://developers.line.biz/en/docs/liff/opening-liff-app/#about-chat-message-write-scope) in the LIFF documentation.
- When the user doesn't grant the `chat_message.write` scope.

You can get the screen type from which the LIFF app is launched using the [`liff.getContext()`](https://developers.line.biz/en/reference/liff/#get-context) method.

_Example_

<!-- tab start `javascript` -->

```javascript
liff
  .sendMessages([
    {
      type: "text",
      text: "Hello, World!",
    },
  ])
  .then(() => {
    console.log("message sent");
  })
  .catch((err) => {
    console.log("error", err);
  });
```

<!-- tab end -->

#### Syntax 

```javascript
liff.sendMessages(messages);
```

#### Arguments 

<!-- parameter start (props: required) -->

messages

Array of objects

[Message objects](https://developers.line.biz/en/reference/messaging-api/#message-objects)\
Max: 5\
You can send the following types of Messaging API messages:

- [Text message](https://developers.line.biz/en/docs/messaging-api/message-types/#text-messages). However, the `emojis` property and the `quoteToken` property aren't available.
- [Sticker message](https://developers.line.biz/en/docs/messaging-api/message-types/#sticker-messages). However, the `quoteToken` property isn't available.
- [Image message](https://developers.line.biz/en/docs/messaging-api/message-types/#image-messages).
- [Video message](https://developers.line.biz/en/docs/messaging-api/message-types/#video-messages). However, the `trackingId` property isn't available.
- [Audio message](https://developers.line.biz/en/docs/messaging-api/message-types/#audio-messages).
- [Location message](https://developers.line.biz/en/docs/messaging-api/message-types/#location-messages).
- [Template message](https://developers.line.biz/en/docs/messaging-api/message-types/#template-messages). However, only a [URI action](https://developers.line.biz/en/docs/messaging-api/actions/#uri-action) can be set as an action.
- [Flex Message](https://developers.line.biz/en/docs/messaging-api/message-types/#flex-messages). However, only a [URI action](https://developers.line.biz/en/docs/messaging-api/actions/#uri-action) can be set as an action.

<!-- parameter end -->

When a template message or a Flex Message is sent from the user using the `liff.sendMessages()` method, no webhook is sent from the LINE Platform. For all other [message types](https://developers.line.biz/en/docs/messaging-api/message-types/), a webhook is sent. When image, video, and audio messages are sent using the `liff.sendMessages()` method, resulting webhook events contain the `contentProvider.type` property whose value is `external`. For more information, see [Message event](https://developers.line.biz/en/reference/messaging-api/#message-event) in the Messaging API reference.

#### Return value 

Returns a `Promise` object.

- If the message is sent successfully, the `Promise` is resolved. No value is passed.
- If you fail to send the message, the `Promise` is rejected and [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-errors) is passed.

### liff.shareTargetPicker() 

Displays the target picker (a screen for selecting a group or friend) and sends a message created by the developer to the selected target. The message appears to the group or friend as if it were sent by the user.

In the target picker, only friends (including LINE Official Accounts) and groups that the user participates in can be selected. OpenChats are not included.

#### Conditions for using the liff.shareTargetPicker() method 

To use the `liff.shareTargetPicker()` method, all of the following conditions must be met:

- The user is logged in.
- The share target picker is enabled in the [LINE Developers Console](https://developers.line.biz/console/). For more information, see [Using the share target picker](https://developers.line.biz/en/docs/liff/developing-liff-apps/#using-share-target-picker) in the LIFF documentation.

<!-- note start -->

**The email address login screen may be displayed when executing the liff.shareTargetPicker() method in a smartphone's external browser**

To display the target picker in an [external browser](https://developers.line.biz/en/glossary/#external-browser), a [Single Sign On (SSO) login](https://developers.line.biz/en/docs/line-login/integrate-line-login/#line-sso-login) session is required.

In the login process using [auto login](https://developers.line.biz/en/docs/line-login/integrate-line-login/#line-auto-login), an SSO login session isn't issued. As a result, when the `liff.shareTargetPicker()` method is executed, the target picker may not be displayed, and the [email address login](https://developers.line.biz/en/docs/line-login/integrate-line-login/#mail-or-qrcode-login) screen may be displayed instead.

After the user logs in by entering their email address and password, an SSO login session is issued, and the target picker will be displayed properly.

<!-- note end -->

<!-- note start -->

**We don't retrieve the number of people to whom a user has sent a message using the share target picker**

In order to protect user privacy, we neither collect nor provide information on how many people received a message from a user through the share target picker.

<!-- note end -->

_Example_

<!-- tab start `javascript` -->

```javascript
liff
  .shareTargetPicker(
    [
      {
        type: "text",
        text: "Hello, World!",
      },
    ],
    {
      isMultiple: true,
    },
  )
  .then(function (res) {
    if (res) {
      // succeeded in sending a message through TargetPicker
      console.log(`[${res.status}] Message sent!`);
    } else {
      // sending message canceled
      console.log("TargetPicker was closed!");
    }
  })
  .catch(function (error) {
    // something went wrong before sending a message
    console.log("something wrong happen");
  });
```

<!-- tab end -->

#### Syntax 

```javascript
liff.shareTargetPicker(messages, options);
```

#### Arguments 

<!-- parameter start (props: required) -->

messages

Array of objects

[Message objects](https://developers.line.biz/en/reference/messaging-api/#message-objects)\
Max: 5\
You can send the following types of Messaging API messages:

- [Text message](https://developers.line.biz/en/docs/messaging-api/message-types/#text-messages). However, the `emojis` property and the `quoteToken` property aren't available.
- [Image message](https://developers.line.biz/en/docs/messaging-api/message-types/#image-messages).
- [Video message](https://developers.line.biz/en/docs/messaging-api/message-types/#video-messages). However, the `trackingId` property isn't available.
- [Audio message](https://developers.line.biz/en/docs/messaging-api/message-types/#audio-messages).
- [Location message](https://developers.line.biz/en/docs/messaging-api/message-types/#location-messages).
- [Template message](https://developers.line.biz/en/docs/messaging-api/message-types/#template-messages). However, only a [URI action](https://developers.line.biz/en/docs/messaging-api/actions/#uri-action) can be set as an action.
- [Flex Message](https://developers.line.biz/en/docs/messaging-api/message-types/#flex-messages). However, only a [URI action](https://developers.line.biz/en/docs/messaging-api/actions/#uri-action) can be set as an action.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

options

Object

Share target picker options

<!-- parameter end -->
<!-- parameter start (props: optional) -->

options.isMultiple

Boolean

Specifies whether or not to allow users to select multiple message recipients through the target picker, using either of these values. The default value is `true`.

- `true`: Users can select multiple recipients from their groups, friends, and chats.
- `false`: Users can select only one of their friends as the recipient.

<!-- parameter end -->

<!-- note start -->

**Setting isMultiple to false doesn't guarantee that the message will be sent to only one friend**

Even if you set the `isMultiple` property to `false`, you can still send a message to multiple users by calling the share target picker multiple times, or by re-sharing the same message to different recipients. To strictly allow a user to send a message to one friend only once, add a restriction when implementing the LIFF app.

Here's an example of sending a message containing a URL and restricting access to the URL.

1. Give the URL a unique token and send the message.
2. When the URL in the message is accessed, the server side verifies the token and restricts access by multiple users.

<!-- note end -->

#### Return value

Returns a `Promise` object.

- If the message is sent correctly, `Promise` is resolved and an object with these properties will be passed.

    <!-- parameter start -->

  status

  String

  `success`

    <!-- parameter end -->

- If the user cancels and closes the target picker before sending the message, `Promise` is resolved but the object isn't passed.

- If a problem occurs before the target picker is displayed, `Promise` is rejected and `LiffError` is passed. For more information on the LiffError object, see [LIFF SDK errors](https://developers.line.biz/en/reference/liff/#liff-errors).

<!-- note start -->

**Note**

In the callback function where `Promise` has been resolved and rejected, the LIFF app won't work on some devices if the developer uses `alert()`.

<!-- note end -->

## Camera 

### liff.scanCodeV2() 

Launch the 2D code reader and obtain string. To activate the 2D code reader, turn on **Scan QR** on the [LINE Developers Console](https://developers.line.biz/console/).

<!-- note start -->

**Operating environments of liff.scanCodeV2()**

`liff.scanCodeV2()` works in these environments.

- iOS: iOS 14.3 or later
- Android: All versions
- External browser: Web browsers that support [WebRTC API](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API)

<table>
  <thead>
    <tr>
      <th>OS</th>
      <th>Version</th>
      <th>LIFF browser</th>
      <th>External browser</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">iOS</td>
      <td>11-14.2</td>
      <td>❌</td>
      <td>✅ *1</td>
    </tr>
    <tr>
      <td>14.3 or later</td>
      <td>✅ *2</td>
      <td>✅ *1</td>
    </tr>
    <tr>
      <td>Android</td>
      <td>All versions</td>
      <td>✅ *2</td>
      <td>✅ *1</td>
    </tr>
    <tr>
      <td>PC</td>
      <td>All versions</td>
      <td>❌</td>
      <td>✅ *1</td>
    </tr>
  </tbody>
</table>

\*1 You can only use web browsers that support [WebRTC API](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API).

\*2 Only available when the screen size of the LIFF browser is `Full`. For details, see [Size of the LIFF browser](https://developers.line.biz/en/docs/liff/overview/#screen-size) in the LIFF documentation.

<!-- note end -->

<!-- note start -->

**Turn [Scan QR] on to launch the 2D code reader**

When [Adding a LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/), turn on **Scan QR**. The **Scan QR** setting can be updated from the LIFF tab on the [LINE Developers Console](https://developers.line.biz/console/), even after adding a LIFF app to your channel.

<!-- note end -->

<!-- note start -->

**The operation specification of liff.scanCodeV2()**

`liff.scanCodeV2()` internally uses an external library called [jsQR](https://github.com/cozmo/jsQR). Therefore, the 2D code reader to be launched when the `liff.scanCodeV2()` method is executed depends on the operation specification of [jsQR](https://github.com/cozmo/jsQR). Libraries used may be updated or changed without notice.

<!-- note end -->

_Example_

<!-- tab start `javascript` -->

```javascript
liff
  .scanCodeV2()
  .then((result) => {
    // result = { value: "" }
  })
  .catch((error) => {
    console.log("error", error);
  });
```

<!-- tab end -->

#### Syntax 

```javascript
liff.scanCodeV2();
```

#### Arguments 

None

#### Return value 

Returns a `Promise` object.

When the string is read by the 2D code reader, `Promise` is resolved and the object containing the character string is passed.

<!-- parameter start -->

value

String

String scanned by the 2D code reader

<!-- parameter end -->

##### Error response 

When the `Promise` is rejected, [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-errors) is passed.

### liff.scanCode() 

<!-- note start -->

**liff.scanCode() method deprecated**

The traditional `liff.scanCode()` method has been [deprecated](https://developers.line.biz/en/glossary/#deprecated). We recommend using the [`liff.scanCodeV2()`](https://developers.line.biz/en/reference/liff/#scan-code-v2) method for implementing a 2D code reader.

<!-- note end -->

<br>

Starts a 2D code reader and gets the string read by the user. To start the 2D code reader, turn on `ScanQR` on the [LINE Developers Console](https://developers.line.biz/console/).

<!-- note start -->

**Not available on LINE for iOS**

`liff.scanCode()` works in these environments.

<table>
  <thead>
    <tr>
      <th>OS</th>
      <th>Version</th>
      <th>LIFF browser</th>
      <th>External browser</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>iOS</td>
      <td>All versions</td>
      <td>❌</td>
      <td>❌</td>
    </tr>
    <tr>
      <td>Android</td>
      <td>All versions</td>
      <td>✅</td>
      <td>❌</td>
    </tr>
    <tr>
      <td>PC</td>
      <td>All versions</td>
      <td>❌</td>
      <td>❌</td>
    </tr>
  </tbody>
</table>

Due to technical issues, `liff.scanCode` is `undefined` in LINE for iOS. Use it after confirming that the function exists, as shown in the sample code. To use the 2D code reader with LINE for iOS or external browsers, see [`liff.scanCodeV2()`](https://developers.line.biz/en/reference/liff/#scan-code-v2).

<!-- note end -->

<!-- note start -->

**Turn [Scan QR] on to launch the 2D code reader**

- When [Adding a LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/), turn on **Scan QR**. The **Scan QR** setting can be updated from the LIFF tab on the [LINE Developers Console](https://developers.line.biz/console/), even after adding a LIFF app to your channel.
- You can't use `liff.scanCode()` in an external browser.

<!-- note end -->

_Example_

<!-- tab start `javascript` -->

```javascript
if (liff.scanCode) {
  liff.scanCode().then((result) => {
    // result = { value: "" }
  });
}
```

<!-- tab end -->

#### Syntax 

```javascript
liff.scanCode();
```

#### Arguments 

None

#### Return value 

Returns a `Promise` object.

When reading a string by a 2D code reader, the `Promise` is resolved and the object containing the string read is passed.

<!-- parameter start -->

value

String

String read by the 2D code reader

<!-- parameter end -->

## Permanent link 

### liff.permanentLink.createUrlBy() 

Get the permanent link of any page in the LIFF app.

Permanent link format:

```
https://liff.line.me/{liffId}/{path}?{query}#{URL fragment}
```

_Example_

<!-- tab start `javascript` -->

```javascript
// For example, if the endpoint URL of the LIFF app
// is https://example.com/path1?q1=v1
// and its LIFF ID is 1234567890-AbcdEfgh
liff.permanentLink
  .createUrlBy("https://example.com/path1?q1=v1")
  .then((permanentLink) => {
    // https://liff.line.me/1234567890-AbcdEfgh
    console.log(permanentLink);
  });

liff.permanentLink
  .createUrlBy("https://example.com/path1/path2?q1=v1&q2=v2")
  .then((permanentLink) => {
    // https://liff.line.me/1234567890-AbcdEfgh/path2?q=2=v2
    console.log(permanentLink);
  });

liff.permanentLink
  .createUrlBy("https://example.com/")
  .catch((error) => {
  // Error: currentPageUrl must start with endpoint URL of LIFF App.
  console.log(error);
});
```

<!-- tab end -->

#### Syntax 

```javascript
liff.permanentLink.createUrlBy(url);
```

#### Arguments 

<!-- parameter start (props: required) -->

url

String

URL to get the permanent link. You can add any query parameter or URL fragment.

<!-- parameter end -->

#### Return value 

Returns a `Promise` object.

Returns the string of the permanent link when `Promise` is resolved.

##### Error responsee 

If the URL to get the permanent link doesn't begin with the URL specified for **Endpoint URL** on the [LINE Developers Console](https://developers.line.biz/console/), `Promise` will be rejected and [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-errors) will be returned.

For example, if the URL to get the permanent link (e.g. `https://example.com/`) is above **Endpoint URL** (e.g. `https://example.com/path1?q1=v1`), `Promise` will be rejected.

### liff.permanentLink.createUrl() 

<!-- note start -->

**liff.permanentLink.createUrl() may be deprecated in the next major version update**

Due to technical issues, `liff.permanentLink.createUrl()` may be deprecated in the next major version update. To get the permanent link of the current page, we recommend using [`liff.permanentLink.createUrlBy()`](https://developers.line.biz/en/reference/liff/#permanent-link-create-url-by).

<!-- note end -->

Gets the permanent link for the current page.

Permanent link format:

```
https://liff.line.me/{liffId}/{path}?{query}#{URL fragment}
```

_Example_

<!-- tab start `javascript` -->

```javascript
// For example, if current location is
// /shopping?item_id=99#details
// (LIFF ID = 1234567890-AbcdEfgh)
const myLink = liff.permanentLink.createUrl();

// myLink equals "https://liff.line.me/1234567890-AbcdEfgh/shopping?item_id=99#details"
```

<!-- tab end -->

#### Syntax 

```javascript
liff.permanentLink.createUrl();
```

#### Arguments 

None

#### Return value 

Returns the current page's permanent link as a string.

A `LiffError` exception is thrown if the current page URL doesn't start with the URL specified in **Endpoint URL** of the LINE Developers console.

### liff.permanentLink.setExtraQueryParam() 

<!-- note start -->

**liff.permanentLink.setExtraQueryParam() may be deprecated in the next major version update**

Due to technical issues, `liff.permanentLink.setExtraQueryParam()` may be deprecated in the next major version update. To add any query parameter to a permanent link on the current page, we recommend using [`liff.permanentLink.createUrlBy()`](https://developers.line.biz/en/reference/liff/#permanent-link-create-url-by).

<!-- note end -->

You can add any query parameter to a permanent link on the current page.

Each time you execute `liff.permanentLink.setExtraQueryParam()`, the query parameters added last time are overwritten.

<!-- tip start -->

**Delete added query parameters**

- To delete the added query parameters, execute `liff.permanentLink.setExtraQueryParam("")`.
- The added query parameters will be discarded when the user navigates to another page.

<!-- tip end -->

_Example_

<!-- tab start `javascript` -->

```javascript
// For example, if current location is
// /food?menu=pizza
// (LIFF ID = 1234567890-AbcdEfgh)
liff.permanentLink.setExtraQueryParam("user_tracking_id=8888");
const myLink = liff.permanentLink.createUrl();

// myLink equals "https://liff.line.me/1234567890-AbcdEfgh/food?menu=pizza&user_tracking_id=8888"
```

<!-- tab end -->

#### Syntax 

```javascript
liff.permanentLink.setExtraQueryParam(extraString);
```

#### Arguments 

<!-- parameter start (props: required) -->

extraString

String

Query parameters to add

<!-- parameter end -->

#### Return value 

None

## LIFF plugin 

### liff.use() 

Activates and initializes LIFF API in the [pluggable SDK](https://developers.line.biz/en/docs/liff/pluggable-sdk/) or a [LIFF plugin](https://developers.line.biz/en/docs/liff/liff-plugin/).

_Example of LIFF API in the pluggable SDK_

<!-- tab start `javascript` -->

```javascript
import liff from "@line/liff/core";
import GetOS from "@line/liff/get-os";

liff.use(new GetOS());

liff.init({
  liffId: "123456-abcedfg", // Use own liffId
});
```

<!-- tab end -->

_Example of LIFF plugin_

<!-- tab start `javascript` -->

```javascript
class greetPlugin {
  constructor() {
    this.name = "greet";
  }

  install() {
    return {
      hello: this.hello,
    };
  }

  hello() {
    console.log("Hello, World!");
  }
}

liff.use(new greetPlugin());
```

<!-- tab end -->

#### Syntax 

```javascript
liff.use(module, option);
```

#### Arguments 

<!-- parameter start (props: required) -->

module

Object

A LIFF API module in the pluggable SDK or a LIFF plugin.

If you pass a LIFF API module, you need to instantiate the LIFF API module. For more information, see [How to use the pluggable SDK](https://developers.line.biz/en/docs/liff/pluggable-sdk/#how-to-use) in the LIFF documentation.

If you pass a LIFF plugin and the LIFF plugin is a class, you need to instantiate the LIFF plugin. For more information, see [Using a LIFF plugin](https://developers.line.biz/en/docs/liff/liff-plugin/#use-liff-plugin) in the LIFF documentation.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

option

Any value

Value to pass to the LIFF plugin specified by the `module` property. The value is passed as the second argument of the LIFF plugin's [`install()`](https://developers.line.biz/en/docs/liff/liff-plugin/#install) method. For more information, see [option](https://developers.line.biz/en/docs/liff/liff-plugin/#option) in the LIFF documentation.

<!-- parameter end -->

#### Return value 

Returns the `liff` object.

## Internationalization 

### liff.i18n.setLang() 

Specify the language of the text displayed by the LIFF SDK.

_Example_

<!-- tab start `javascript` -->

```javascript
liff.i18n.setLang("en");
```

<!-- tab end -->

#### Syntax 

```javascript
liff.i18n.setLang(language);
```

#### Arguments 

<!-- parameter start (props: required) -->

language

String

Language tag as defined in [RFC 5646 (BCP 47)](https://datatracker.ietf.org/doc/html/rfc5646). If there is no translation for the specified language tag, `en` is used as a fallback.

<!-- parameter end -->

#### Return value 

Returns a `Promise` object.

##### Error response 

When the `Promise` is rejected, [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-errors) is passed.

## Others 

### liff.createShortcutOnHomeScreen() 

<!-- tip start -->

**This feature can only be used for verified MINI Apps**

This feature is only available for verified MINI Apps. For unverified MINI Apps, you can test the feature on the internal channel for Developing, but you can't use the feature on the internal channel for Published.

<!-- tip end -->

Displays a screen for adding a shortcut to your [LINE MINI App](https://developers.line.biz/en/docs/line-mini-app/) to the home screen of the user's device.

![](https://developers.line.biz/media/line-mini-app/develop/add-to-home-screen/add-shortcut-screen-ios-en.png)

For more information, see [Add a shortcut to your LINE MINI App to the home screen of the user's device](https://developers.line.biz/en/docs/line-mini-app/develop/add-to-home-screen/) in the LINE MINI App documentation.

<!-- note start -->

**When to execute the liff.createShortcutOnHomeScreen() method**

The `liff.createShortcutOnHomeScreen()` method should be executed in response to a user action (e.g. tap) on your LINE MINI App so as not to spoil the user experience.

<!-- note end -->

_Example_

<!-- tab start `javascript` -->

```javascript
// If the endpoint URL of the LINE MINI App
// is https://example.com/path1/path2
// and its LIFF ID is 1234567890-AbcdEfgh

// Example of specifying the LIFF URL
liff
  .createShortcutOnHomeScreen({
    url: "https://miniapp.line.me/1234567890-AbcdEfgh",
  })
  .then(() => { /* ... */ });

liff
  .createShortcutOnHomeScreen({
    url: "https://liff.line.me/1234567890-AbcdEfgh",
  })
  .then(() => { /* ... */ });

// Example of specifying a permanent link
liff
  .createShortcutOnHomeScreen({
    url: "https://liff.line.me/1234567890-AbcdEfgh/path3",
  })
  .then(() => { /* ... */ });

// Example of specifying the endpoint URL of the LINE MINI App
liff
  .createShortcutOnHomeScreen({
    url: "https://example.com/path1/path2",
  })
  .then(() => { /* ... */ });

// Example of specifying a URL that begins with the endpoint URL of the LINE MINI App
liff
  .createShortcutOnHomeScreen({
    url: "https://example.com/path1/path2/path3",
  })
  .then(() => { /* ... */ });

// Example of specifying a URL that results in an error
liff
  .createShortcutOnHomeScreen({
    url: "https://example.com/invalid-path",
  })
  .then(() => { /* ... */ })
  .catch((error) => {
    // invalid URL.
    console.log(error.message);
  });
```

<!-- tab end -->

#### Conditions of use 

To use the `liff.createShortcutOnHomeScreen()` method, all of the following conditions must be met:

- It's a LINE MINI App.
- The LIFF SDK version of the LINI MINI App is v2.23.0 or later.
- The LINE app version on the user's device is 13.20.0 or later.

#### Operating conditions 

If the OS of the user's device is iOS, the conditions for the `liff.createShortcutOnHomeScreen()` method to work are as follows. If this method is executed in a non-working environment, an error page will be displayed.

| Default browser | iOS version | Whether it works or not |
| --- | --- | --- |
| Safari | All versions | Works |
| Chrome | 16.4 or later | Works |
| Browsers other than Safari and Chrome | 16.4 or later | Not guaranteed to work |
| Browsers other than Safari | Earlier than 16.4 | Doesn't work |

For example, if you execute the `liff.createShortcutOnHomeScreen()` method in Chrome on earlier than iOS 16.4, the following error page will be displayed:

![](https://developers.line.biz/media/line-mini-app/develop/add-to-home-screen/add-shortcut-screen-ios-error-en.png)

#### Syntax 

```javascript
liff.createShortcutOnHomeScreen(params);
```

#### Arguments 

<!-- parameter start (props: required) -->

params

Object

Parameter object

<!-- parameter end -->
<!-- parameter start (props: required) -->

params.url

String

URL. You can specify the following URLs:

- [LIFF URL](https://developers.line.biz/en/glossary/#liff-url)
- [Permanent link](https://developers.line.biz/en/glossary/#permanent-link-liff)
- The endpoint URL of the LINE MINI App
- URL that begins with the endpoint URL of the LINE MINI App

<!-- parameter end -->

#### Return value 

Returns a `Promise` object.

When the Add Shortcut screen is displayed, the `Promise` is resolved. No value is passed.

You can't confirm whether the user has actually added a shortcut to your LINE MINI app to the home screen of the user's device.

##### Error response 

When the `Promise` is rejected, [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-errors) is passed.
