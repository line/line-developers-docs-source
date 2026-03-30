# LINE Login security checklist

When developing an application using LINE Login, you must prepare for potential attacks by third parties and implement the login function without any security flaws.

We provide a checklist to ensure that there are no security flaws when integrating LINE Login into your application. Use the checklist to validate your application before publishing.

We also recommend confirming the session "[Implementing safe and secure LINE Login](https://linedevday.linecorp.com/2020/en/sessions/7159/)" at LINE DEVELOPER DAY 2020.

<!-- tip start -->

**Be sure to build a safe system with an understanding of the purpose of the checklist**

The checklist contains excerpts of points that require special attention when using LINE Login. Conforming to the contents of the checklist does not guarantee security. Be sure to build a safe system with a full understanding of the dangers.

<!-- tip end -->

<!-- table of contents -->

## Checklist for query parameters passed to the authorization URL 

The following checklist is for the query parameters to the authorization URL, when initiating the authentication and authorization process. For more information on the authorization URL, see [Authenticating users and making authorization requests](https://developers.line.biz/en/docs/line-login/integrate-line-login/#making-an-authorization-request).

<!-- tip start -->

**Callback URL**

**Callback URL** refers to the **Callback URL** on the **LINE Login tab** of the LINE Login channel in the [LINE Developers Console](https://developers.line.biz/console/). For more information on how to set the **Callback URL**, see [Getting started with LINE Login](https://developers.line.biz/en/docs/line-login/getting-started/).

<!-- tip end -->

| Check contents | Related pages |
| --- | --- |
| Is the URL schema specified in `redirect_uri` HTTPS? (Unless there is a specific reason not to specify it.) | <ul><li>[RFC6749 3.1.2.1.](https://datatracker.ietf.org/doc/html/rfc6749#section-3.1.2.1)</li></ul> |
| Do you understand a valid URL as `redirect_uri` is one of the following URLs?<ul><li>URL that exactly matches the URL registered in the **Callback URL**</li><li>URL registered in the **Callback URL** with optional query parameters added</li></ul> | <ul><li>[RFC6749 3.1.2.](https://datatracker.ietf.org/doc/html/rfc6749#section-3.1.2)</li><li>[Authenticating users and making authorization requests](https://developers.line.biz/en/docs/line-login/integrate-line-login/#making-an-authorization-request)</li></ul> |
| Is there a query parameter that receives an arbitrary URL and redirects in the query parameter received by the URL registered in the **Callback URL**? If such a parameter exists, do you verify that Open Redirector vulnerability does not exist? | <ul><li>[RFC6749 10.15](https://datatracker.ietf.org/doc/html/rfc6749#section-10.15)</li></ul> |
| Is the value specified in `state` randomly generated and unique in a cryptographically secure and unpredictable way, such as SecureRandom, and in a way that can't be predicted by third parties? | <ul><li>[RFC6749 10.12.](https://datatracker.ietf.org/doc/html/rfc6749#section-10.12)</li><li>[Authenticating users and making authorization requests](https://developers.line.biz/en/docs/line-login/integrate-line-login/#making-an-authorization-request)</li></ul> |
| Is the value specified for `state` stored in a location inaccessible to a third party, such as follows?<ul><li>Server session information</li><li>Cookies protected by the same-origin policy, etc</li></ul> | <ul><li>[RFC6749 10.12.](https://datatracker.ietf.org/doc/html/rfc6749#section-10.12)</li></ul> |
| Is the different value specified for `state` each time a login is attempted, even if the same user tries to log in? | <ul><li>[RFC6749 10.12.](https://datatracker.ietf.org/doc/html/rfc6749#section-10.12)</li></ul> |

## Checklist for query parameters returned to the callback URL 

The following checklist is for the query parameters returned to the callback URL. For more information on the query parameters returned to the callback URL, see [Receiving the authorization response or error response with a web app](https://developers.line.biz/en/docs/line-login/integrate-line-login/#receiving-the-authorization-code-or-error-response-with-a-web-app).

| Check contents | Related pages |
| --- | --- |
| Do you confirm that the value of `state` matches the `state` specified in the authentication URL? | <ul><li>[RFC6749 10.12.](https://datatracker.ietf.org/doc/html/rfc6749#section-10.12)</li><li>[Receiving the authorization response or error response with a web app](https://developers.line.biz/en/docs/line-login/integrate-line-login/#receiving-the-authorization-code-or-error-response-with-a-web-app)</li></ul> |

## Checklist for issuing the access token 

The following checklist is for issuing the access token using the [LINE Login API](https://developers.line.biz/en/reference/line-login/). For more information on issuing the access token, see [Issue access token](https://developers.line.biz/en/reference/line-login/#issue-access-token) and [Managing authorized apps](https://developers.line.biz/en/docs/line-login/managing-access-tokens/).

| Check contents | Related pages |
| --- | --- |
| Do you understand that the channel secret you specify in `client_secret` is confidential information and can't be known by third parties? | <ul><li>[OpenID Connect 1.0 16.19](https://openid.net/specs/openid-connect-core-1_0.html#rfc.section.16.19)</li></ul> |

## Checklist for using ID tokens and access tokens 

The following checklist is for using the ID tokens and access tokens issued by the LINE Platform. For more information on issuing ID tokens and access tokens, see [Get profile information from ID tokens](https://developers.line.biz/en/docs/line-login/verify-id-token/) and [Managing authorized apps](https://developers.line.biz/en/docs/line-login/managing-access-tokens/).

| Check contents | Related pages |
| --- | --- |
| Have you verified ID tokens and access tokens? | <ul><li>[Verify access token validity](https://developers.line.biz/en/reference/line-login/#verify-access-token)</li><li>[Verify ID token](https://developers.line.biz/en/reference/line-login/#verify-id-token)</li></ul> |
| Have you checked the values of the `client_id` and `expires_in` properties meet the following conditions, after successfully verifying the access token?<ul><li>`client_id`: Same value as the channel ID of the LINE Login channel linked to the native app</li><li>`expires_in`: Positive value</li></ul> | <ul><li>[Using access tokens to register new users](https://developers.line.biz/en/docs/line-login/secure-login-process/#using-access-tokens)</li></ul> |

## Checklist for sending ID tokens and access tokens to the backend server for processing 

The following checklist is for user registration and login for using user information obtained by the LINE Platform. For more information on secure user registration and concepts of the login process, see [Creating a secure login process between your app and server](https://developers.line.biz/en/docs/line-login/secure-login-process/).

| Check contents | Related pages |
| --- | --- |
| Have you sent the raw ID tokens or access tokens from the client to the backend server, instead of user IDs or other information?<br>\* After using APIs that verify ID tokens and access tokens, the backend server can retrieve user IDs and other information. | <ul><li>[Using access tokens to register new users](https://developers.line.biz/en/docs/line-login/secure-login-process/#using-access-tokens)</li><li>[Verify access token validity](https://developers.line.biz/en/reference/line-login/#verify-access-token)</li><li>[Verify ID token](https://developers.line.biz/en/reference/line-login/#verify-id-token)</li></ul> |
| Have you verified ID tokens and access tokens that are sent from the client to the backend server? | <ul><li>[Using access tokens to register new users](https://developers.line.biz/en/docs/line-login/secure-login-process/#using-access-tokens)</li></ul> |
