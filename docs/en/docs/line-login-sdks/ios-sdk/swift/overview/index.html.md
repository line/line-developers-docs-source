# LINE SDK for iOS Swift overview

Developed in Swift, the LINE SDK for iOS Swift provides a modern way of implementing the LINE Platform APIs. The features included in this SDK will help you develop an iOS app with an engaging and personalized user experience.

## Features 

The LINE SDK for iOS Swift provides the following features.

### User authentication 

This feature allows users to log in to your app or service with their LINE accounts. With the help of the LINE SDK for iOS Swift, it has never been easier to integrate LINE Login into your app. Your users will automatically log in to your app without entering their LINE credentials if they are already logged in to LINE on their iOS devices. This offers a great way for users to get started with your app without having to go through a registration process.

### Utilizing user data with OpenID support 

Once the user is authorized, you can get the user’s LINE profile. You can utilize the user's information registered in LINE without building your user system.

The LINE SDK supports the [OpenID Connect](https://openid.net/developers/how-connect-works/) 1.0 specification. You can get ID tokens that contain the user’s LINE profile when you retrieve the access token.

### API calls 

Use the methods included in the LINE SDK to get user profile information, log out users, and manage access tokens.

## Open-source SDK 

The LINE SDK for iOS Swift is an open-source project. Visit [our repository](https://github.com/line/line-sdk-ios-swift) to view the code and samples that we have provided for you to use.

## Using the LINE SDK 

To use the LINE SDK with your iOS app, follow the steps below.

1. Create a channel.

    For more information, see [Getting started with LINE Login](https://developers.line.biz/en/docs/line-login/getting-started/) in the LINE Login documentation.

2. Use the LINE SDK to add LINE Login support to your iOS app.

    For more information, see [Setting up your project](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/setting-up-project/) and [Integrating LINE Login with your iOS app](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/integrate-line-login/).

3. Use LINE Login.

    To learn more about using LINE Login in your app, see [Managing users](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/managing-users/) and the [LINE SDK for iOS Swift reference](https://developers.line.biz/en/reference/ios-sdk-swift/).

    To learn more about using LINE Login on your server, see [Managing access tokens](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/managing-access-tokens/) and the [LINE Login v2.1 API reference](https://developers.line.biz/en/reference/line-login/).

### Trying the starter app 

You can see how LINE Login works using our starter app. See [Trying the starter app](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/try-line-login/).

## What's in this guide 

This guide explains how to integrate the LINE SDK with your app and use the available API functions in the SDK from your app. See the following table for an overview of the topics that are discussed in this guide.

Title | Content
-|-
[LINE SDK for iOS Swift overview](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/overview/) | The SDK features and the high-level steps for using the SDK.
[Trying the starter app](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/try-line-login/) | How to run our starter app.
[Setting up your project](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/setting-up-project/) | How to integrate the LINE SDK into your project.
[Integrating LINE Login with your iOS app](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/integrate-line-login/) | How to leverage LINE Login to improve your app's user experience.
[Enabling the add friend option with the SDK](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/link-a-bot/) | How to display an option to add the LINE Official Account as a friend to users and get the friendship status between the LINE Official Account and the user.
[Managing users](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/managing-users/) | How to get user profiles, use ID tokens to get user data, and log out users.
[Managing access tokens](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/managing-access-tokens/) | How to refresh and verify access tokens and get the current access token.
[Handling errors](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/error-handling/) | How to handle errors returned by the SDK.
[Using the SDK with Objective-C code](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/using-objc/) | How to integrate the LINE SDK for iOS Swift into your Objective-C project.
[Upgrading the SDK](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/migration-guide/) | How to upgrade from the LINE SDK v4.1 for iOS to the LINE SDK v5 for iOS Swift.
[LINE SDK v5 for iOS Swift reference](https://developers.line.biz/en/reference/ios-sdk-swift/) | Detailed information on the protocols and classes available in the SDK.

## Other resources 

You can find the following information on the [top page](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/) of the LINE SDK for iOS guide.

Title | Content
-|-
[Release notes](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/release-notes/) | SDK changelog.
[Downloads](https://developers.line.biz/en/docs/downloads/) | Links to download the LINE SDKs.
