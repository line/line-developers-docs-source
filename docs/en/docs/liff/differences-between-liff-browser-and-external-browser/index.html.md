# The differences between the LIFF browser and external browser

<!-- tip start -->

**LIFF browser specifications**

For more information, see [LIFF browser specifications](https://developers.line.biz/en/docs/liff/overview/#liff-browser-spec).

<!-- tip end -->

The [LIFF browser](https://developers.line.biz/en/glossary/#liff-browser) doesn't support some of the web technologies supported by [external browsers](https://developers.line.biz/en/glossary/#external-browser). The web technologies that aren't supported by the LIFF browser include the following:

| Web technology | Description |
| --- | --- |
| [theme-color Meta Tag](https://caniuse.com/meta-theme-color) | A feature to specify the color of the user interface |
| [Download attribute](https://caniuse.com/download) | A feature to use a hyperlink for downloading the resource, not for navigating to the resource |
| [Add to home screen (A2HS)](https://caniuse.com/sr_web-app-manifest) | <p>A feature that allows the user to add a web application to the home screen on the user's device.</p><p>In the LINE MINI App, a shortcut to a LINE MINI App can be added to the home screen on the user's device using **Add to Home** in the [multi-tab view](https://developers.line.biz/en/docs/line-mini-app/discover/builtin-features/#multi-tab-view) or the [`liff.createShortcutOnHomeScreen()`](https://developers.line.biz/en/reference/liff/#create-shortcut-on-home-screen) method. For more information, see [Add a shortcut to your LINE MINI App to the home screen of the user's device](https://developers.line.biz/en/docs/line-mini-app/develop/add-to-home-screen/) in the LINE MINI App documentation.</p> |
| [Service Workers](https://caniuse.com/serviceworkers) | A feature that enables offline support, background synchronization, push notifications, etc. in a web application |

The web technologies listed above may be supported by the LIFF browser in the future.

Whether or not the LIFF browser supports web technologies other than those listed above is in accordance with the specifications of [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) and [Android WebView](https://developer.android.com/reference/android/webkit/WebView). For more information, see [Can I use...](https://caniuse.com/).
