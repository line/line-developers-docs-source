# Creating a secure login process between your app and server

This page explains how to securely handle user registration and login when implementing LINE Login in your native app using the [LINE SDK](https://developers.line.biz/en/docs/line-login/overview/#native-app).

## Information that's safe to send and receive 

When a user logs in to your app via LINE Login, the client app and server can send and receive this information from the LINE Platform:

- ❌ User profile details
- ❌ Channel IDs

However, information such as the above is vulnerable to spoofing and other kinds of attacks. For example, it's dangerous for your server to blindly trust this information when your client sends it. Instead, your client should send this data to your server:

- ✅ Access tokens
- ✅ ID tokens

These tokens enable your server to get reliable information directly from the LINE Platform.

<!-- tip start -->

**How to use this page**

This section explains the design concepts we recommend for using the LINE SDK. They are guides, not templates. Be sure to build a safe system with a full understanding of the dangers.

<!-- tip end -->

## Using access tokens to register new users 

When a new user logs in to your app using LINE Login, you'll want to use their LINE profile details to create a new user in your database.

However, if you allow the client app to send you profile information directly to your server, you make yourself vulnerable to attacks.

<!-- note start -->

**Note**

The following example highlights a potential vulnerability in the user registration and login process.

<!-- note end -->

![](https://developers.line.biz/media/line-login/new-user-login-bad.svg)

Instead of profile information, the client app sends an access token to the server. The server should verify the access token and retrieve the user profile directly from the LINE Platform:

![Interactive SVG](https://developers.line.biz/media/line-login/new-user-login-standard.svg)

To learn more about the API calls in the diagram, see these topics in the LINE Login v2.1 API reference:

- [Verify that an access token is valid (GET /oauth2/v2.1/verify)](https://developers.line.biz/en/reference/line-login/#verify-access-token)
- [Get user profile (GET /v2/profile)](https://developers.line.biz/en/reference/line-login/#get-user-profile)

<!-- note start -->

**Further confirmation is required after verifying the access token**

When the LINE Login API successfully verifies an access token, the response contains a `client_id` property (the channel ID) and an `expires_in` property (the amount of time until the token expires). Make sure that these properties satisfy the following criteria before you use the access token.

| Property | Criteria |
| --- | --- |
| `client_id` | Same as the channel ID of the LINE Login channel linked to the native app |
| `expires_in` | Positive value |

<!-- note end -->

## Using OpenID to register new users 

If your app supports [OpenID Connect](https://openid.net/developers/how-connect-works/), it's not necessary to verify the access token. Instead, the client app sends the ID token to the server. The server should use an endpoint provided by the LINE Platform to validate your ID token to get a user profile information:

<!-- tip start -->

**nonce: number used once**

The nonce is a randomly generated number used to make each login attempt uniquely identifiable.

Using nonce correctly helps prevent [replay attacks](https://en.wikipedia.org/wiki/Replay_attack).

<!-- tip end -->

![Interactive SVG](https://developers.line.biz/media/line-login/new-user-login-openid.svg)

For more information on the API call in the diagram, see this topic in the LINE Login API reference:

- [Verify ID token (POST /oauth2/v2.1/verify)](https://developers.line.biz/en/reference/line-login/#verify-id-token)

For details about how to handle the ID token and nonce on your server, see these items:

- [Using ID tokens on your server](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/managing-users/#get-id-token) (LINE SDK for iOS Swift)
- [Using ID token on your server ](https://developers.line.biz/en/docs/line-login-sdks/android-sdk/managing-users/#get-id-token) (LINE SDK for Android)

## Next steps 

The preceding examples show in general terms how to design a secure user registration and login process. But for specific instructions on integrating LINE Login into your app, see these items:

- LINE SDK for iOS Swift:
  - [Integrating LINE Login with your iOS app](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/integrate-line-login/)
    - [Managing users](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/managing-users/)
    - [Managing access tokens](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/managing-access-tokens/)
- LINE SDK for Android:
  - [Integrating LINE Login with your Android app](https://developers.line.biz/en/docs/line-login-sdks/android-sdk/integrate-line-login/)
    - [Managing users](https://developers.line.biz/en/docs/line-login-sdks/android-sdk/managing-users/)
    - [Managing access tokens](https://developers.line.biz/en/docs/line-login-sdks/android-sdk/managing-access-tokens/)
