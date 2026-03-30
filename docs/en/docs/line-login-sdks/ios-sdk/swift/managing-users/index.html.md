# Managing users

This topic explains how to perform the following user management tasks:

- [Getting user profiles](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/managing-users/#get-profile)
- [Using ID tokens to verify user identities](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/managing-users/#get-id-token)
- [Logging out users](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/managing-users/#logout)

<!-- tip start -->

**Creating a secure login process**

For general recommendations on how to securely handle user registration and login, see [Creating a secure login process between your app and server](https://developers.line.biz/en/docs/line-login/secure-login-process/).

<!-- tip end -->

## Getting user profiles 

If the login request is sent with the `.profile` scope, you can get the user's LINE profile information. The user profile includes the user ID, display name, profile media (image or video), and status message.

Call the `API.getProfile` method as below:

```swift
API.getProfile { result in
    switch result {
    case .success(let profile):
        print("User ID: \(profile.userID)")
        print("User Display Name: \(profile.displayName)")
        print("User Status Message: \(profile.statusMessage)")
        print("User Icon: \(String(describing: profile.pictureURL))")
    case .failure(let error):
        print(error)
    }
}
```

The `API.getProfile` method gets the values at the time of login while users can change their display name, profile media, and status message anytime in LINE. To identify users, use the value of the `userID` property that doesn't change.

## Using ID tokens to verify user identities 

The [OpenID Connect](https://openid.net/developers/how-connect-works/) 1.0 specification is an identity layer on top of the OAuth 2.0 protocol. With OpenID Connect, you can securely exchange information with the LINE Platform. Currently, you can get the user profile and email address from the LINE Platform by issuing ID tokens that conform to the OpenID Connect specification.

### Applying for email permission 

You can request users who log in using LINE Login to grant your app the permission to get their email address. To do so, apply for the permission in the [LINE Developers Console](https://developers.line.biz/console/). For more information, see [Applying for email permission](https://developers.line.biz/en/docs/line-login/integrate-line-login/#applying-for-email-permission) in the LINE Login guide.

### Login with the OpenID and email scopes 

Once your channel has the email permission, you can let users log in with the `.openID` and `.email` scopes to get the user's email address from the ID token as below:

```swift
LoginManager.shared.login(permissions: [.openID, .email], in: self) {
    result in
    switch result {
    case .success(let loginResult):
        if let email = loginResult.accessToken.IDToken?.payload.email {
            print("User Email: \(email)")
        }
    case .failure(let error):
        print(error)
    }
}
```

An ID token is a signed [JSON Web Token](https://datatracker.ietf.org/doc/html/rfc7519). The LINE SDK validates the token by checking its signature and validity period for you, to prevent any malformed data in it.

### Using ID tokens on your server 

<!-- warning start -->

**User impersonation**

Do not trust user IDs or other information sent by a client to your backend server. A malicious client can send an arbitrary user ID or malformed information to your server to impersonate a user.

Instead, the client should send the raw ID token string to your server. After verifying the token against the ID token verification API, the server can retrieve the user ID or any other information.

<!-- warning end -->

#### Sending raw ID token string 

When logging in with the `.openID` permission, you can assign a custom value to the `IDTokenNonce` parameter:

```swift
var parameters = LoginManager.Parameters()
parameters.IDTokenNonce = "<a randomly-generated string>"
LoginManager.shared.login(permissions: [.profile, .openID], parameters: parameters) {
    result in
    // ...
}
```

Although LINE SDK automatically assigns a value to `IDTokenNonce` if no value is specified, we recommend randomly generating a nonce value on your server and also storing it there. You can later use the original nonce to [verify the ID token](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/managing-users/#verify-id-token-on-server) using LINE Login. Using `nonce` to verify ID tokens helps prevent [replay attacks](https://en.wikipedia.org/wiki/Replay_attack).

After a successful login with the `.openID` permission, you can get the raw ID token string like this:

```swift
LoginManager.shared.login(permissions: [.profile, .openID], parameters: parameters) {
    result in
    switch result {
    case .success(let loginResult):
        if let idToken = loginResult.accessToken.IDTokenRaw {
            // Send `idToken` to your server.
        } else {
            // Something went wrong. You should fail the login.
        }

    case .failure(let error):
        print(error)
```

You can then send the `idToken` to your server to be [verified](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/managing-users/#verify-id-token-on-server).

#### Verify ID token on your server 

After receiving the ID token, your server should send both the token and the corresponding `nonce` value to the LINE Platform's ID token verification endpoint. If the token is valid, the API returns a JSON-formatted object containing ID token claims.

Learn more about what APIs to call from your backend on these pages:

- [Verify the ID token](https://developers.line.biz/en/reference/line-login/#verify-id-token)

### Treating user data carefully 

Do not save any sensitive user data in plain text in your app or server, or transfer them through non-secure HTTP communication. Such data includes the access token, user ID, username, and any information in the ID token. The LINE SDK will store the user's access token for you. If needed, you can access it after authorization with the code below:

```swift
if let token = AccessTokenStore.shared.current {
    print(token.value)
}
```

ID tokens are issued only at the time of login. To update the ID token, you need to have the user log in again. However, if you set the `.profile` scope in the login request, you can call the `API.getProfile` method to get the user's profile information.

## Logging out users 

You can log out users from your app. To create a better user experience, we recommend providing a way for users to log out of your app.

To invalidate the access token and log out the user from your app, call the `logout` method. The user is logged out of your app when you invalidate the access token. After logging out, the user must go through the login process again to log in.

```swift
LoginManager.shared.logout { result in
    switch result {
    case .success:
        print("Logout from LINE")
    case .failure(let error):
        print(error)
    }
}
```
