# LINE Front-end Framework (LIFF)

LINE Front-end Framework (LIFF) is a platform for web apps provided by LY Corporation. The web apps running on this platform are called LIFF apps.

LIFF apps can get data from the LINE Platform such as the LINE user ID. The LIFF app can use such data to provide features that utilize user data and send messages on the user's behalf.

For more information on functions added to LIFF v2, see the [Release Notes](https://developers.line.biz/en/docs/liff/release-notes/).

<!-- tip start -->

**Try out LIFF features on the web**

LY Corporation provides a web application (LIFF app) for developers called [LIFF Playground](https://liff-playground.netlify.app/). LIFF Playground allows you to try out basic LIFF features on the web. [The source code for LIFF Playground](https://github.com/line/liff-playground) is available on GitHub.

<!-- tip end -->

<!-- note start -->

**LIFF apps not compatible with OpenChat**

Currently, LIFF apps are not officially supported in OpenChat, which means some functions don't work. For example, retrieving a user's profile information through a LIFF app isn't possible in most cases.

<!-- note end -->

## Experience LIFF app for demo 

[LINE API Use Case](https://lineapiusecase.com/en/top.html) provides LIFF app for demo and its source code. Open the LIFF app for demo to experience store reservations and table orders.

- [Experience making restaurant or hair salon reservations with LIFF app for demo](https://lineapiusecase.com/en/usecase/reservation.html)
- [Experience a digital membership card with LIFF app for demo](https://lineapiusecase.com/en/usecase/membership.html)
- [Experience table ordering with LIFF app for demo](https://lineapiusecase.com/en/usecase/tableorder.html)
- [Experience smartphone self-checkout with LIFF app for demo](https://lineapiusecase.com/en/usecase/smartretail.html)

## Recommended operating environment 

The recommended versions of operating systems and LINE for LIFF are as follows.

Which functions you can use depends on whether the LIFF app is opened in a [LIFF browser](https://developers.line.biz/en/docs/liff/overview/#liff-browser) or an [external browser](https://developers.line.biz/en/glossary/#external-browser). For example, you can't use `liff.scanCode()` in an external browser. For more information, see the [LIFF v2 API reference](https://developers.line.biz/en/reference/liff/).

### When the LIFF app is opened in a LIFF browser 

| Item | Recommended environment | Minimum operating environment |
| --- | --- | --- |
| iOS | Latest version. [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) is used. | In accordance with the recommended system specifications for LINE. \* |
| Android | Latest version. [Android WebView](https://developer.android.com/reference/android/webkit/WebView) is used. | In accordance with the recommended system specifications for LINE. \* |
| LINE | Latest version | In accordance with the recommended system specifications for LINE. \* |

<!-- note start -->

**We recommend using the latest versions of OS and LINE for LIFF apps**

We recommend that you use the latest versions of OS and LINE for LIFF apps. Even on versions later than the "Minimum operating environment" listed above, some features may not work or the screen may not be displayed properly depending on the settings.

<!-- note end -->

\* For more information on the recommended system specifications for LINE, see [Recommended system specifications for LINE](https://help.line.me/line/ios/pc?lang=en&contentId=10002433) in Help Center.

### When the LIFF app is opened in an external browser 

LIFF apps run on the latest version of these browsers:

Microsoft Edge, Google Chrome, Firefox, Safari

## LIFF browser 

LIFF browser is a browser specifically for LIFF apps. When a user opens a LIFF URL in LINE, the LIFF app opens in a LIFF browser.

![LIFF browser](https://developers.line.biz/media/liff/overview/liffBrowser.png)

Since LIFF browser runs within LINE, the LIFF app can access user data without having to prompt users to log in. The LIFF browser also provides features that are specific to LINE, such as being able to share the LIFF app and sending a message to a friend.

## LIFF browser specifications 

The LIFF browser uses [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) in iOS, and [Android WebView](https://developer.android.com/reference/android/webkit/WebView) in Android. As such, the specifications and behavior of the LIFF browser will also be in accordance with these schemes.

The LIFF browser doesn't support some of the web technologies supported by external browsers. For more information, see [The differences between the LIFF browser and external browser](https://developers.line.biz/en/docs/liff/differences-between-liff-browser-and-external-browser/).

## LIFF browser cache 

[WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) and [Android WebView](https://developer.android.com/reference/android/webkit/WebView), which are used by the LIFF browser, may save and use displayed content as a cache as instructed by HTTP headers, such as [Cache-Control](https://developer.mozilla.org/ja/docs/Web/HTTP/Reference/Headers/Cache-Control).

Control caching in the LIFF browser, using HTTP headers such as [Cache-Control](https://developer.mozilla.org/ja/docs/Web/HTTP/Reference/Headers/Cache-Control).

<!-- note start -->

**On deleting cache**

There is no way to explicitly delete cache stored in the LIFF browser.

<!-- note end -->

## Size of the LIFF browser 

The LIFF browser can be displayed in one of these three sizes.

![View size](https://developers.line.biz/media/liff/overview/viewTypes.png)

Set the view size when you add the LIFF app to your LINE Login channel. For more information, see [Adding a LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/#registering-liff-app).

## Action button 

LIFF apps with the size of the LIFF app view set to `Full` display an action button in the header by default.

![](https://developers.line.biz/media/news/2025/liff-action-button-after.png)

<!-- tip start -->

**Hide the action button**

Enable **Module mode** of the LIFF app in the LINE Developers Console to hide the action button. For more information, see [Adding a LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/).

<!-- tip end -->

When the user taps the action button, either the [multi-tab view](https://developers.line.biz/en/docs/liff/overview/#multi-tab-view) or the [options](https://developers.line.biz/en/docs/liff/overview/#multi-tab-view-option) will be displayed depending on the LINE app version. In LINE version 15.12.0 or later, the multi-tab will be displayed, and in LINE version earlier than 15.12.0, the options will be displayed.

## Multi-tab view 

The multi-tab view displays options for the LIFF app currently in use and recently used services.

1. [Options](https://developers.line.biz/en/docs/liff/overview/#multi-tab-view-option)
1. [Recently used services](https://developers.line.biz/en/docs/liff/overview/#multi-tab-view-recent-service)

![](https://developers.line.biz/media/liff/overview/liff-multi-tab-view-en.png)

### Options 

The following options appear in the language settings of the user's LINE app:

| Item | Description |
| --- | --- |
| **Refresh** | Reloads the current page. |
| **Share** | Shares the [permanent link](https://developers.line.biz/en/glossary/#permanent-link-liff) of the current page via a LINE message. |
| **Minimize browser** | Minimizes LIFF browser. For more information, see [Minimizing LIFF browser](https://developers.line.biz/en/docs/liff/minimizing-liff-browser/). |
| **Permission setting** | Opens the Permission Settings screen. The Permission Settings screen allows the user to view the camera and microphone permissions of the currently open LIFF app. No changes can be made. Available in LINE versions 14.6.0 or later. |

<!-- note start -->

**Permanent link sharing may fail**

If the URL of the current page doesn't start with the URL specified in **Endpoint URL** of the LINE Developers Console, the permanent link can't be obtained and sharing will fail.

<!-- note end -->

### Recently used services 

The recently used services section includes LIFF apps opened by the user, displayed in order of most recent use, up to a maximum of 50 items.

When a user closes a LIFF app or open a new LIFF app, a screenshot taken at that point will be displayed as usage history. The user can use the usage history to reopen the LIFF app.

When the LIFF app is opened again from the usage history, the LIFF app is resumed or reloaded. The specifications for resuming and reloading are as follows:

| Behavior when reopened | Conditions | Specifications |
| --- | --- | --- |
| LIFF apps will resume | <p>LIFF apps that meet both of the following conditions:</p><ul><li>LIFF apps used within the last 12 hours</li><li>LIFF apps included in the 10 most recent usage items</li></ul> | The LIFF app will resume from the screen where the user left off. The access token, browsing history, and screen scroll position will be retained. |
| LIFF apps will reload | If the conditions for resuming are not met | The LIFF app will be initialized at the URL where the user left off. The access token, browsing history, and screen scroll position will be discarded. |

#### Conditions for appearing in recently used services 

To display LIFF apps in recently used services, all of the following conditions must be met:

- The LINE app version is 15.12.0 or later
- `Full` is specified as the [screen size](https://developers.line.biz/en/docs/liff/overview/#screen-size) for your LIFF app
- Your LIFF app's module mode is off

#### Units displayed for recently used services 

In recently used services, LIFF apps are displayed by LIFF ID. If the user reopens the same LIFF app from somewhere other than the recently used services section, a new LIFF app will open and the old LIFF app will discard.

Note that if the user opens another LIFF app during a LIFF-to-LIFF transition, even if the LIFF IDs are different, the LIFF apps will be grouped and displayed as a single LIFF app.

#### The `liff.sendMessages()` method can't be used after reloading a LIFF app 

If you use the [`liff.sendMessages()`](https://developers.line.biz/en/reference/liff/#send-messages) method in a LIFF app that has been reloaded from the recently used services section, an error will occur. For this reason, you can't use the `liff.sendMessages()` method when a LIFF app is reloaded.

To use the `liff.sendMessages()` method after reloading a LIFF app, reopen the LIFF app by tapping the LIFF URL in the chat room, etc.

## Development guidelines 

When developing web apps using LIFF, follow these [LIFF app development guidelines](https://developers.line.biz/en/docs/liff/development-guidelines/).

## Tools to support LIFF app development 

LY Corporation provides the following tools to help developers develop LIFF apps more smoothly.

| Tool name | What this tool can do |
| --- | --- |
| [LIFF starter app](https://developers.line.biz/en/docs/liff/trying-liff-app/) | This is a starter app for those new to learning about LIFF. The LIFF starter app is only a demo of the LIFF app initialization to help you understand how to start developing LIFF apps. It's recommended for those who want to build something that works first and get a rough idea of what LIFF is all about. |
| [Create LIFF App](https://developers.line.biz/en/docs/liff/cli-tool-create-liff-app/) | This CLI tool allows you to build a development environment for LIFF apps with a single command. Like [Create React App](https://github.com/facebook/create-react-app) by React or [Create Next App](https://nextjs.org/docs/pages/api-reference/cli/create-next-app) by Next.js, by answering questions from Create LIFF App, a development environment including the LIFF app template for you is generated and development can begin immediately. |
| [LIFF CLI](https://developers.line.biz/en/docs/liff/liff-cli/) | <p>A CLI tool to help you develop LIFF apps more smoothly. The LIFF CLI allows you to do the following:</p><ul><li>Create, update, list, and delete LIFF apps</li><li>Create a LIFF app development environment</li><li>Debug your LIFF app with the [LIFF Inspector](https://developers.line.biz/en/docs/liff/liff-plugin/#liff-inspector)</li><li>Launch a local develpment server with HTTPS</li></ul>The [LIFF Mock](https://developers.line.biz/en/docs/liff/liff-plugin/#liff-mock) feature will be added in a future update. |
| [LIFF Playground](https://liff-playground.netlify.app/) | You can try out LIFF's features online. [The source code for LIFF Playground](https://github.com/line/liff-playground) is available on GitHub, so developers can set their LIFF ID and deploy their own LIFF Playground on the server. |

## Workflow 

To enable the use of the LIFF app by the end user, follow these steps:

1. [Create a channel](https://developers.line.biz/en/docs/liff/getting-started/) to add your LIFF app to.
1. [Try the LIFF starter app](https://developers.line.biz/en/docs/liff/trying-liff-app/), or [develop a LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/).
