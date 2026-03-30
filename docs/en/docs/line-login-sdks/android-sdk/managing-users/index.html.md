# Managing users

This topic explains how to perform the following user management tasks:

- [Getting user profiles](https://developers.line.biz/en/docs/line-login-sdks/android-sdk/managing-users/#get-profile)
- [Using ID tokens to verify user identities](https://developers.line.biz/en/docs/line-login-sdks/android-sdk/managing-users/#get-id-token)
- [Logging out users](https://developers.line.biz/en/docs/line-login-sdks/android-sdk/managing-users/#logout)

<!-- tip start -->

**Creating a secure login process**

For general recommendations on how to securely handle user registration and login, see [Creating a secure login process between your app and server](https://developers.line.biz/en/docs/line-login/secure-login-process/).

<!-- tip end -->

## Getting user profiles 

If the login request is sent with the `Scope.PROFILE` scope, you can get the user's LINE profile information. The user profile includes the user ID, display name, profile media (image or video), and status message.

Call the `LineApiClient.getProfile()` method as below:

```java
LineProfile profile = lineApiClient.getProfile().getResponseData()
Log.i(TAG, profile.getDisplayName());
Log.i(TAG, profile.getUserId());
Log.i(TAG, profile.getStatusMessage());
Log.i(TAG, profile.getPictureUrl().toString());
```

The `getDisplayName()`, `getPictureURL()`, and `getStatusMessage()` methods get the values at the time of login while users can change those values anytime in LINE. To identify users, use the `getUserId()` method, whose return value, user ID, doesn't change.

You can change the size of the user’s profile image by adding a suffix to the URL.

Image Size | Suffix
-|-
200 x 200 | /large
51 x 51 | /small

## Using ID tokens to verify user identity 

The [OpenID Connect](https://openid.net/developers/how-connect-works/) 1.0 specification is an identity layer on top of the OAuth 2.0 protocol. With OpenID Connect, you can securely exchange information with the LINE Platform. Currently, you can get the user profile and email address from the LINE Platform by issuing ID tokens that conform to the OpenID Connect specification.

### Applying for email permission 

You can request users who log in using LINE Login to grant your app the permission to get their email address. To do so, apply for the permission in the [LINE Developers Console](https://developers.line.biz/console/). For more information, see [Applying for email permission](https://developers.line.biz/en/docs/line-login/integrate-line-login/#applying-for-email-permission) in the LINE Login guide.

### Login with the OpenID and email scopes 

Once your channel has the email permission, you can let users log in with the `Scope.OPENID_CONNECT` and `Scope.OC_EMAIL` scopes to get the user's email address from the ID token as below:

```java
import java.util.Arrays;

private static final int REQUEST_CODE = 1;

LineAuthenticationParams params = new LineAuthenticationParams.Builder()
                                    .scopes(Arrays.asList(Scope.OPENID_CONNECT, Scope.OC_EMAIL))
                                    .build();

Intent loginIntent = LineLoginApi.getLoginIntent(
                        view.getContext(),
                        Constants.CHANNEL_ID,
                        params);

startActivityForResult(loginIntent, REQUEST_CODE);
```

An ID token is a signed [JSON Web Token](https://datatracker.ietf.org/doc/html/rfc7519). The LINE SDK validates the token by checking its signature and validity period for you, to prevent any malformed data in it. If the validation passes, you can get a `LineIdToken` instance in the `onActivityResult()` callback as below:

```java
public void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (requestCode != REQUEST_CODE) {
        Log.e("ERROR", "Unsupported Request");
        return;
    }

    LineLoginResult result = LineLoginApi.getLoginResultFromIntent(data);

    switch (result.getResponseCode()) {
        case SUCCESS:
            // Login successful
            LineIdToken lineIdToken = result.getLineIdToken();
            Log.v("INFO", lineIdToken.getEmail());
    ...
    }
}
```

### Using ID tokens on your server 

<!-- warning start -->

**User spoofing**

Do not trust user IDs or other information sent by a client to your backend server. A malicious client can send an arbitrary user ID or malformed information to your server to impersonate a user.

Instead, the client should send the raw ID token string to your server. After verifying the token against the ID token verification API, the server can retrieve the user ID or any other information.

<!-- warning end -->

#### Sending raw ID token string 

When logging in with the `Scope.OPENID_CONNECT` scope, you can assign a custom value to the `nonce` parameter:

```java
private static final int REQUEST_CODE = 1;
...
LineAuthenticationParams params = new LineAuthenticationParams.Builder()
                                  ...
                                  .nonce("<a randomly-generated string>")
                                  .build();

Intent loginIntent = LineLoginApi.getLoginIntent(
                        view.getContext(),
                        Constants.CHANNEL_ID,
                        params);

startActivityForResult(loginIntent, REQUEST_CODE);
```

Even though the LINE SDK automatically assigns a value to `nonce` if you don't specify one yourself, we recommend generating a random value for `nonce` and specifying it for the `nonce` parameter. You can use the value given for `nonce` here when [verifying ID tokens](https://developers.line.biz/en/docs/line-login-sdks/android-sdk/managing-users/#verify-id-token-on-server) with the LINE Login API. Using a `nonce` to verify ID tokens helps prevent [replay attacks](https://en.wikipedia.org/wiki/Replay_attack).

After a successful login with the `Scope.OPENID_CONNECT` scope, you can get the raw ID token string like this:

```java
public void onActivityResult(int requestCode, int resultCode, Intent data) {
    ...
    LineLoginResult result = LineLoginApi.getLoginResultFromIntent(data);

    switch (result.getResponseCode()) {
        case SUCCESS:
            // Login successful
            LineIdToken lineIdToken = result.getLineIdToken();
            String idTokenStr = lineIdToken.getRawString();
            if (idTokenStr != null) {
                // Send `idTokenStr` to your server.
            } else {
                // Something went wrong. You should fail the login.
            }
    ...
}
```

Send the `idTokenStr` obtained here to your backend server to [verify ID tokens](https://developers.line.biz/en/docs/line-login-sdks/android-sdk/managing-users/#verify-id-token-on-server).

#### Verify ID tokens on your backend server 

After receiving the ID token, your server should send both the token and the corresponding `nonce` value to the LINE Platform's ID token verification endpoint. If the token is valid, the API returns a JSON-formatted object containing ID token claims.

To learn more about what APIs to call from your backend server, see:

- [Verify ID token](https://developers.line.biz/en/reference/line-login/#verify-id-token) (LINE Login v2.1 API reference)

### Handling user data responsibly 

Do not save any sensitive user data in plain text in your app or server, or transfer them through non-secure HTTP communication. Such data includes the access token, user ID, username, and any information in the ID token. The LINE SDK will store the user's access token for you. If needed, you can access it after authorization with the code below:

```java
LineAccessToken accessToken = lineApiClient.getCurrentAccessToken().getResponseData();
```

ID tokens are issued only at the time of login. To update the ID token, you need to have the user log in again. However, if you set the `Scope.PROFILE` scope in the login request, you can call the `LineApiClient.getProfile()` method to get the user's profile information.

## Logging out users 

You can log out users from your app. To create a better user experience, we recommend providing a way for users to log out of your app.

To invalidate the access token and log out the user from your app, call the `logout()` method. The user is logged out of your app when you invalidate the access token. After logging out, the user must go through the login process again to log in.

```java
lineApiClient.logout();
```
