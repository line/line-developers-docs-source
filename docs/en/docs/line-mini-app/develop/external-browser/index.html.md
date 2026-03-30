# Open a LINE MINI App in an external browser

<!-- tip start -->

**As of October 2025, LINE MINI Apps can be used in an external browser**

For more information, see the news from September 26, 2025, [On October 1, 2025, all LINE MINI App users will be able to use the service in a web browser](https://developers.line.biz/en/news/2025/09/26/mini-app-browser/).

<!-- tip end -->

When developing a LINE MINI App, make sure that the LINE MINI App service is also available when users access the endpoint URL with an [external browser](https://developers.line.biz/en/glossary/#external-browser).

When using the LINE MINI App with an external browser, note the following:

<!-- table of contents -->

## Explicitly handle logging in for services that require LINE Login 

When opening the LINE MINI App in an external browser, unlike the LIFF browser, simply executing the [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app) method will not execute the LINE Login.

Therefore, if LINE Login is required to use your service, explicitly execute LINE Login using one of the following methods:

### 1. Automatic execution of LINE Login at initialization 

By specifying `true` in the `withLoginOnExternalBrowser` property of the `config` object of the [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app) method, the [`liff.login()`](https://developers.line.biz/en/reference/liff/#login) method can be executed automatically when the LIFF app is initialized in external browsers.

Example:

```js
liff
  .init({
    liffId: "1234567890-AbcdEfgh", // Use own liffId
    withLoginOnExternalBrowser: true, // Enable automatic login process
  })
  .then(() => {
    // Start to use liff's api
  });
```

### 2. Execute LINE Login when a user isn't logged in 

If the user isn't logged in with LINE Login and the service requires it, you can just execute LINE Login.

Check the user's login status using the [`liff.isLoggedIn()`](https://developers.line.biz/en/reference/liff/#is-logged-in) method, and if the user isn't logged in, execute the [`liff.login()`](https://developers.line.biz/en/reference/liff/#login) method.

Example:

```js
if (!liff.isLoggedIn()) {
  liff.login();
}
```

For more information, see [To use LINE Login in an external browser](https://developers.line.biz/en/docs/liff/developing-liff-apps/#to-use-line-login-in-external-browser) in the LIFF documentation.

## Direct users to the LINE app when using features that aren't available in an external browser 

If your LINE MINI App needs to use a feature that isn't available in external browsers, a user needs to open the LINE MINI App on the LINE app.

Features that can't be used with external browsers and aren't guaranteed to work are as follows:

- [liff.sendMessages()](https://developers.line.biz/en/reference/liff/#send-messages)
- [liff.openWindow()](https://developers.line.biz/en/reference/liff/#open-window)
- [liff.closeWindow()](https://developers.line.biz/en/reference/liff/#close-window)
- [liff.scanCode()](https://developers.line.biz/en/reference/liff/#scan-code) (deprecated)
- [liff.iap.\* (in-app purchase)](https://developers.line.biz/en/reference/line-mini-app/#in-app-purchase)

When opening your LINE MINI App that uses these features in an external browser, it's recommended to place a link to the LINE MINI App on the screen with the text "To use this feature, you must open the LINE MINI App in LINE app".

Note that the methods [`liff.getContext()`](https://developers.line.biz/en/reference/liff/#get-context) and [`liff.isInClient()`](https://developers.line.biz/en/reference/liff/#is-in-client) can be used to get the environment of the LINE MINI App. We recommend to use these methods if you want to change the display according to the environment of the LINE MINI App.

## Assume that non-LINE users will open the LINE MINI App 

To enable the LINE MINI App for users who don't use LINE, ensure that the service works without requiring LINE Login after opening the LINE MINI App in an external browser.

The LIFF API properties and methods that can be used without LINE Login in an external browser are as follows:

- [liff.id](https://developers.line.biz/en/reference/liff/#id)
- [liff.ready](https://developers.line.biz/en/reference/liff/#ready)
- [liff.init()](https://developers.line.biz/en/reference/liff/#initialize-liff-app)
- [liff.getOS()](https://developers.line.biz/en/reference/liff/#get-os)
- [liff.getAppLanguage()](https://developers.line.biz/en/reference/liff/#get-app-language)
- [liff.getLanguage()](https://developers.line.biz/en/reference/liff/#get-language) (deprecated)
- [liff.getVersion()](https://developers.line.biz/en/reference/liff/#get-version)
- [liff.getLineVersion()](https://developers.line.biz/en/reference/liff/#get-line-version)
- [liff.isInClient()](https://developers.line.biz/en/reference/liff/#is-in-client)
- [liff.isLoggedIn()](https://developers.line.biz/en/reference/liff/#is-logged-in)
- [liff.permanentLink.createUrlBy()](https://developers.line.biz/en/reference/liff/#permanent-link-create-url-by)
- [liff.use()](https://developers.line.biz/en/reference/liff/#use)
