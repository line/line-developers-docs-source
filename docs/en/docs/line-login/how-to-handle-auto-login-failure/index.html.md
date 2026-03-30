# How to handle auto login failure

## Overview 

For web apps that have integrated LINE Login, [auto login](https://developers.line.biz/en/docs/line-login/integrate-line-login/#line-auto-login) may fail when private browsing is enabled. In addition, depending on the specifications of the user's OS, auto login may fail.

- [When auto login on the LINE app fails](https://developers.line.biz/en/docs/line-login/how-to-handle-auto-login-failure/#case-auto-login-on-line-app-fails)
- [When Universal Links or App Links don't work and the LINE app won't launch](https://developers.line.biz/en/docs/line-login/how-to-handle-auto-login-failure/#case-line-app-will-not-launch)

## When auto login on the LINE app fails 

Auto login on the LINE app may fail when private browsing is enabled. If the login fails, the user is still be redirected to the callback URL with the `code` and `state` parameters.

In this case, the `code` parameter is an invalid value, so you can't issue an access token. Also, the `state` parameter doesn't match the value associated with the login session.

![](https://developers.line.biz/media/line-login/handle-auto-login-failure/auto-login-failure-case-1-en.png)

This section explains how to detect auto login failures and examples of responses that should be displayed to users when login fails.

### Detecting auto login failure 

You can detect auto login failure using the `state` parameter explained in [Authenticating users and making authorization requests](https://developers.line.biz/en/docs/line-login/integrate-line-login/#making-an-authorization-request).

When the login fails on the LINE app, this will lead to a mismatch between the value of the `state` parameter given to the callback URL and the value of the `state` parameter set in the authorization URL. Your web app design should take into account that auto login fails when there is a mismatch between the values of the `state` parameters.

<!-- tip start -->

**Cases of &quot;state&quot; parameter mismatch**

With LINE Login, a `state` parameter mismatch may occur due to attacks by third parties such as [Cross site request forgery (CSRF)](https://datatracker.ietf.org/doc/html/rfc6749#section-10.12). Accordingly, it's impossible to determine whether the cause of the `state` parameter mismatch is auto login failure or an attack by a third party such as CSRF.

Therefore, when there is a `state` parameter mismatch, consider how to deal with the situation where the user unintentionally failed at auto login.

<!-- tip end -->

### When auto login fails 

In environments where auto login fails, if the user who failed LINE Login is prompted to reattempt with an authorization URL where auto login is enabled, the user will continue to fail at LINE Login repeatedly. In order to prevent continuous login failures, once auto login fails, you can use the `disable_auto_login` parameter to prompt the user to reattempt LINE Login with an authorization URL that has auto login disabled.

These are the two recommended responses.

- [Display an error message to users and prompt them to reattempt login](https://developers.line.biz/en/docs/line-login/how-to-handle-auto-login-failure/#recommended-to-log-in-again)
- [Redirect user to an authorization URL without auto login](https://developers.line.biz/en/docs/line-login/how-to-handle-auto-login-failure/#redirect-to-authorization-url)

#### Display an error message to users and prompt them to reattempt login 

Display a login failure message to users and prompt them to reattempt login.

Since this screen is displayed [when automatic login fails](https://developers.line.biz/en/docs/line-login/how-to-handle-auto-login-failure/#when-automatic-login-fails), you need to disable auto login when prompting users to reattempt login. To disable auto login, set the `disable_auto_login` parameter to `true` in the query parameter of the authorization URL and redirect the user as follows.

<pre class="language-text">
<code>https://access.line.me/oauth2/v2.1/authorize?<b style="color:#06C755;">disable_auto_login=true</b>&response_type=code&client_id=1234567890&redirect_uri=https%3A%2F%2Fexample.com%2Fauth%3Fkey%3Dvalue&state=12345abcde&scope=profile%20openid&nonce=09876xyz</code>
</pre>

We recommend including on this screen a link to the [I can't automatically log in to a website with LINE](https://help.line.me/line/ios/sp?lang=en&contentId=20020693) page (`https://help.line.me/line/ios/sp?lang=en&contentId=20020693`) from the LINE Help center.

The following is a sample screen that prompts the user to reattepmt login.

![Example of a screen that displays error messages to the user](https://developers.line.biz/media/line-login/handle-auto-login-failure/auto-login-failure-message-en.png)

#### Redirect users to an authorization URL without auto login 

Directly redirect users who have failed auto login to the authorization URL where auto login has been disabled. By redirecting users directly, you can display the login screen without making the user aware that auto login has failed. To disable auto login, set the `disable_auto_login` parameter to `true` in the query parameter of the authorization URL and redirect the user as follows.

<pre class="language-text">
<code>https://access.line.me/oauth2/v2.1/authorize?<b style="color:#06C755;">disable_auto_login=true</b>&response_type=code&client_id=1234567890&redirect_uri=https%3A%2F%2Fexample.com%2Fauth%3Fkey%3Dvalue&state=12345abcde&scope=profile%20openid&nonce=09876xyz</code>
</pre>

If you want to let users know in advance that a redirection will occur, you can display a redirection message.

The following is a sample screen displaying a redirect message.

![Redirect users to an authorization URL without auto login](https://developers.line.biz/media/line-login/handle-auto-login-failure/auto-login-redirect-to-login-en.png)

## When Universal Links or App Links don't work and the LINE app won't launch 

We use [Universal Links](https://developer.apple.com/documentation/xcode/allowing-apps-and-websites-to-link-to-your-content/) and [App Links](https://developer.android.com/training/app-links) features to perform auto login on [external browsers](https://developers.line.biz/en/glossary/#external-browser).

Universal Links or App Links may not work in external browsers or in some in-app browsers, and auto login may not work. In this case, the LINE app won't launch and the [email address login](https://developers.line.biz/en/docs/line-login/integrate-line-login/#mail-or-qrcode-login) screen will appear on the external browser or on the in-app browser. This may happen depending on the specifications of the user's OS. Since the specifications of the OS aren't fully disclosed, it may be difficult for the LINE Platform to avoid the conditions under which auto login fails.

![](https://developers.line.biz/media/line-login/handle-auto-login-failure/auto-login-failure-case-2-en.png)

### Notes on making Universal Links work on iOS 

Universal Links may not work in the following cases:

- Redirects a user to an authorization URL by JavaScript.
- A user types the URL and goes directly to the authorization URL.

You may be able to work around the problem of Universal Links not working by attending to the above. For example, let users tap a button to go to the authorization URL and start the login process.
