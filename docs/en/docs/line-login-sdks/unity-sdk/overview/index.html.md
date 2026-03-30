# LINE SDK for Unity overview

The LINE SDK for Unity provides a modern way of implementing the LINE Platform APIs. The features included in this SDK will help you develop a Unity game with an engaging and personalized user experience.

## Features 

The LINE SDK for Unity is a wrapper for [LINE SDK for iOS Swift](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/) and [LINE SDK for Android](https://developers.line.biz/en/docs/line-login-sdks/android-sdk/). It provides the following features in a Unity game running on iOS or Android.

### User authentication 

This feature allows users to log in to your Unity game with their LINE accounts. With the help of the LINE SDK for Unity, it has never been easier to integrate LINE Login into your app. Your users will automatically log in to your app without entering their LINE credentials if they are already logged in to LINE on their Android devices. This offers a great way for users to get started with your app without having to go through a registration process.

### Utilizing user data with OpenID support 

Once the user is authorized, you can get their LINE profile. You can make use of the user's information registered in LINE without building your own user system.

The LINE SDK supports the [OpenID Connect](https://openid.net/developers/how-connect-works/) 1.0 specification. You can get ID tokens that contain the user’s LINE profile when you retrieve the access token.

### API calls 

Use the methods included in the LINE SDK to get user profile information, log out users, and manage access tokens.

## Open-sourced SDK 

The LINE SDK for Unity is an open-source project. Visit [our repository](https://github.com/line/line-sdk-unity) to check the provided code and samples.

## Using the SDK 

To use the LINE SDK with your Unity game, follow the steps below.

1. Create a channel. For more information, see [Getting started with LINE Login](https://developers.line.biz/en/docs/line-login/getting-started/) in the LINE Login documentation.
2. Use the SDK to add LINE Login support to your Unity game. For more information, see [Integrating LINE Login with your Unity game](https://developers.line.biz/en/docs/line-login-sdks/unity-sdk/integrate-line-login/).
3. Make API calls from your app using the SDK or from server-side code through the LINE Login API. For more information, see the [LINE SDK for Unity API reference](https://developers.line.biz/en/reference/unity-sdk/) and the [LINE Login v2.1 API reference](https://developers.line.biz/en/reference/line-login/).

### Trying the starter app 

You can see how LINE Login works using our starter app. See [Trying the starter app](https://developers.line.biz/en/docs/line-login-sdks/unity-sdk/try-line-login/).

## What's in this guide 

This guide explains how to integrate the LINE SDK with your Unity game and use the available API functions in the SDK from your app. The table below lists the topics and their contents in this guide.

Title | Content
-|-
[LINE SDK for Unity overview](https://developers.line.biz/en/docs/line-login-sdks/unity-sdk/overview/) | SDK features and high-level steps for using the SDK.
[Setting up project](https://developers.line.biz/en/docs/line-login-sdks/unity-sdk/project-setup/) | The prerequisites and environment needed for integrating the LINE SDK for Unity.
[Trying the starter app](https://developers.line.biz/en/docs/line-login-sdks/unity-sdk/try-line-login/) | How to run our starter app.
[Integrating LINE Login with your Unity game](https://developers.line.biz/en/docs/line-login-sdks/unity-sdk/integrate-line-login/) | How to integrate the LINE SDK into your project and leverage LINE Login to improve your app's user experience.
[Using the SDK](https://developers.line.biz/en/docs/line-login-sdks/unity-sdk/using-sdk/) | Usage and other details of LINE SDK for Unity.
[LINE SDK for Unity reference](https://developers.line.biz/en/reference/unity-sdk/) | Detailed information on the interfaces and classes available in the SDK.

## Other resources 

You can access the following information from the [top page](https://developers.line.biz/en/docs/line-login-sdks/unity-sdk/) of the LINE SDK for Unity guide.

Title | Content
-|-
[Release notes](https://developers.line.biz/en/docs/line-login-sdks/unity-sdk/release-notes/) | Change log for the SDK.
