# Enabling the add friend option with the SDK

You can display an option to add the LINE Official Account as a friend when a user logs in to your app. This is called the **add friend option**. Developers can specify the LINE Official Account to be added as a friend.

Before getting started with the configuration, see [Add a LINE Official Account as a friend when logged in (add friend option)](https://developers.line.biz/en/docs/line-login/link-a-bot/) in the LINE Login documentation to understand the add friend option and the following specifics:

- Linking a LINE Official Account with your channel on the LINE Developers Console
- The bot prompt parameter sent to the LINE Platform and its behavior
- The friendship status flag returned from the LINE Platform and its meaning

This topic explains how to enable these features related to the add friend option with the LINE SDK:

- [Setting the bot prompt parameter in the login request](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/link-a-bot/#bot_prompt)
- [Checking the friendship status between the user and the LINE Official Account](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/link-a-bot/#get_friendship)

## Setting the bot prompt parameter in the login request 

The following sample code shows how to set `.botPromptNormal` or `.botPromptAggressive` as the bot prompt parameter in the login request:

```swift
// Includes an option to add a LINE Official Account as a friend in the consent screen.
var parameters = LoginManager.Parameters()
parameters.botPromptStyle = .normal
LoginManager.shared.login(permissions: [.profile], parameters: parameters) {
    // ...
}

// Opens a new screen to add the LINE Official Account as a friend after the user agrees to the permissions in the consent screen.
parameters.botPromptStyle = .aggressive
LoginManager.shared.login(permissions: [.profile], parameters: parameters) {
    // ...
}
```

For more information about the parameter values, see [LoginManager.Parameters](https://developers.line.biz/en/reference/ios-sdk-swift/Classes/LoginManager/Parameters.html) and [LoginManager.BotPrompt](https://developers.line.biz/en/reference/ios-sdk-swift/Classes/LoginManager/BotPrompt.html) in the LINE SDK for iOS Swift reference.

## Checking the friendship status between the user and the LINE Official Account 

You can check the friendship status between the user and the LINE Official Account using the following methods.

- [Check the `friendshipStatusChanged` property in the login response](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/link-a-bot/#use-friendship_status_changed): This method checks whether the friendship status has changed during login.
- [Use LINE Login to get friendship status](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/link-a-bot/#use-line-login-api): This method gets the friendship status between the user and the LINE Official Account.

### Check the `friendshipStatusChanged` property in the login response 

After successful login, the `friendshipStatusChanged` property of the `LoginResult` object contains a boolean value that indicates whether the friendship status has changed.

The following conditions must be met to get the friendship status flag:

- The bot prompt option is specified in the login request.
- The consent screen with the option to add your LINE Official Account as a friend is displayed to the user.

The following sample code shows how to get the `friendshipStatusChanged` property.

```swift
var parameters = LoginManager.Parameters()
parameters.botPromptStyle = .normal
LoginManager.shared.login(permissions: [.profile], parameters: parameters) {
    result in
    switch result {
    case .success(let value):
        print(value.friendshipStatusChanged)
    case .failure(let error):
        print(error)
    }
}
```

For more information about the `friendshipStatusChanged` property, see [friendshipStatusChanged](https://developers.line.biz/en/reference/ios-sdk-swift/Structs/LoginResult.html#/s:7LineSDK11LoginResultV23friendshipStatusChangedSbSgvp) in the LINE SDK for iOS Swift reference.

### Use LINE Login to get friendship status 

Call the `getBotFriendshipStatus` method after the user has logged in to your app and an access token has been returned.

```swift
API.getBotFriendshipStatus { result in
    switch result {
    case .success(let value): print(value.friendFlag)
    case .failure(let error): print(error)
    }
}
```

For more information about the return values, see [getBotFriendshipStatus](https://developers.line.biz/en/reference/ios-sdk-swift/Enums/API.html#/s:7LineSDK3APIO22getBotFriendshipStatus13callbackQueue17completionHandleryAA08CallbackI0O_ys6ResultOyAA03GetefG7RequestV8ResponseVAA0A8SDKErrorOGctFZ) in the LINE SDK for iOS Swift reference.
