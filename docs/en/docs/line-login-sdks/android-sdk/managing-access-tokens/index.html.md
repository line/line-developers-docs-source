# Managing access tokens

This topic explains how to perform the following access token management tasks:

- [Refreshing access tokens](https://developers.line.biz/en/docs/line-login-sdks/android-sdk/managing-access-tokens/#refresh-token)
- [Getting the current access token](https://developers.line.biz/en/docs/line-login-sdks/android-sdk/managing-access-tokens/#get-current-token)
- [Verifying access tokens](https://developers.line.biz/en/docs/line-login-sdks/android-sdk/managing-access-tokens/#verify-access-token)

<!-- tip start -->

**Creating a secure login process**

For general recommendations on how to securely handle user registration and login, see [Creating a secure login process between your app and server](https://developers.line.biz/en/docs/line-login/secure-login-process/).

<!-- tip end -->

## Refreshing access tokens 

The LINE SDK stores the user's valid access token after successful authorization and uses it to make API requests. You can get the validity period of access tokens as below:

```java
LineAccessToken accessToken = lineApiClient.getCurrentAccessToken().getResponseData();
Log.i(TAG, accessToken.getExpiresInMillis());
```

When making an API request, the LINE SDK automatically refreshes any expired access token through the `LineApiClient` interface. However, the refresh operation fails if the token has been expired for a long time. In that case, an error occurs and you need to have the user log in again.

It is **not recommended** to refresh access tokens by yourself. Automatic access token management by the LINE SDK is easier and safer for future upgrading. However, you can manually refresh access tokens as below:

```java
LineAccessToken newAccessToken = lineApiClient.refreshAccessToken().getResponseData();
```

## Getting the current access token 

When building a client-server application, use access tokens to send user data between your app and the server. If you obtain an access token in your app and send it to a server, you can then make LINE Login API calls from that server. To learn more, see the [LINE Login v2.1 API reference](https://developers.line.biz/en/reference/line-login/).

To get the access token that the LINE SDK has saved in your app, call the `getCurrentAccessToken()` method.

```java
String accessToken = lineApiClient.getCurrentAccessToken().getResponseData().getTokenString();
```

<!-- note start -->

**Note**

We recommend that you encrypt your access tokens before sending them to your server via an SSL connection.

Verify that these conditions are true before using an access token on your server.

- The server has received the same access token that is used to make LINE Login API calls.
- The channel ID used to make LINE Login API calls matches your own channel ID.

<!-- note end -->

## Verifying access tokens 

Call the `verifyToken()` method in your app to verify that the access token saved by the LINE SDK is valid. This method returns a `LineApiResponse` object that contains the result. You can then call the `isSuccess()` method to check if the token is valid.

If the `isSuccess()` method returns `true`, the token is valid. Otherwise, the access token is either invalid or expired, or a LINE Login API call in the LINE SDK failed for some reason.

If the `isSuccess()` method returns `false`, you can use the `LineApiResponse.getErrorData()` method to determine why the `verifyToken()` method failed. In this case, the `getResponseData()` method returns `null`.

```java
LineApiResponse verifyResponse = lineApiClient.verifyToken();

if (verifyResponse.isSuccess()) {

    Log.i(TAG, "getResponseData: " + verifyResponse.getResponseData().toString());
    Log.i(TAG, "getResponseCode: " + verifyResponse.getResponseCode().toString());

    return true;
} else {

    Log.i(TAG, "getResponseCode: " + verifyResponse.getResponseCode());
    Log.i(TAG, "getErrorData: " + verifyResponse.getErrorData());

    return false;

}
```

To get a list of scopes that are associated with the access token, call `LineApiResponse.getResponseData().getScopes()`. The following example demonstrates how to display a list of scopes in a toast.

```java
protected void onPostExecute(LineApiResponse response){
    if (response.isSuccess()){
        LineCredential lineCredential = response.getResponseData();
        List<Scope> scopes = lineCredential.getScopes();
        String scopesString = Scope.join(scopes);
        Toast.makeText(getApplicationContext(), scopesString, Toast.LENGTH_SHORT).show();
    }
}
```
