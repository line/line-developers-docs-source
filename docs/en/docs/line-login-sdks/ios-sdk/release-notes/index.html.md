# Release notes for LINE SDK for iOS

<!-- note start -->

**Release notes for version 5.0.0 or later are available on the GitHub repository**

Release notes for LINE SDK for iOS version 5.0.0 or later are available on the GitHub repository. For more information, see [Releases](https://github.com/line/line-sdk-ios-swift/releases).

<!-- note end -->

November 20, 2018

## LINE SDK 5.0.0 for iOS released

The LINE SDK 5.0.0 for iOS has been released. For installation and usage instructions, see the [LINE SDK for iOS guide](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/).

#### Changes

##### LINE Login v2.1 and Social API v2.1 are supported

You can set permissions to be granted to your app as scopes when users log in to your app with the LINE Login. By setting scopes, you can get ID tokens when you get access tokens. Those tokens contain user data according to the scopes you set with the login request.

You can display an option to add your bot as a friend to users logging in to your app. You can get the friendship status between users and your bot with login responses and the Social API.

##### New SDK version in Swift

Developed in Swift, the LINE SDK for iOS Swift provides a modern way of implementing LINE APIs. The LINE SDK 5.0.0 for iOS Objective-C is the last version of our Objective-C SDK.

##### Open-source SDK

The LINE SDK for iOS Swift is open-sourced. Visit [our repository](https://github.com/line/line-sdk-ios-swift) to check the provided code and samples.

##### Detailed reference

Now you can access detailed reference based on the source code. For more information, see the followings:

- [LINE SDK for iOS Swift reference](https://developers.line.biz/en/reference/ios-sdk-swift/)
- [LINE SDK for iOS Objective-C reference](https://developers.line.biz/en/reference/ios-sdk-objc/)

April 13, 2018

## LINE SDK 4.1.1 for iOS released

The LINE SDK 4.1.1 for iOS has been released. You can download the SDK from the following page.

- [Download LINE SDK](https://developers.line.biz/en/docs/downloads/)

Changes:

- Fixed an issue that the `LineSDKLogin` object has the access token in cache even after logout.

January 29, 2018

## LINE SDK 4.1.0 for iOS released

The LINE SDK 4.1.0 for iOS has been released. You can download the SDK from the following page.

- [Download LINE SDK](https://developers.line.biz/en/docs/downloads/)

Changes:

- The web login process now uses a Safari View Controller instead of an external browser.

March 22, 2017

##  LINE SDK for iOS CocoaPod released

We have released the LINE SDK for iOS on CocoaPods. You can now download the LINE SDK for iOS using CocoaPods for your Objective-C and Swift projects.

For information on how to download the SDK with CocoaPods, see the link below.

- Download with [CocoaPods](https://cocoapods.org/)

January 27, 2017

## LINE SDK 4.0.1 for iOS released

The LINE SDK 4.0.1 for iOS has been released. You can download the SDK from the following page.

- [Download LINE SDK](https://developers.line.biz/en/docs/downloads/)

Changes:

- Fixed an issue which causes an authentication error when using Web Login.

December 13, 2016

## Change to requirement on whitelisting LINE domains

Whitelisting LINE domains is no longer a requirement for using the LINE SDK for iOS. As such, the documentation on whitelisting LINE domains found in the Settings for iOS 9 or later section has been removed.

October 7, 2016

## The LINE SDK 3.2.1 for iOS released

The LINE SDK for iOS has been updated to version 3.2.1. You can download it from the LINE SDK archives on the following page:

- [Download LINE SDK](https://developers.line.biz/en/docs/downloads/)

Changes:

- `LineAdapter+Login.framework` and `LineAdapterUI.framework` merged to `LineAdapter.framework`.
- Definition changed for swift.

In addition, the LINE SDK starter application has been revised to be compatibility with this version of the SDK. You can clone or download it from the GitHub repository below.

- [https://github.com/line/line-sdk-starter-ios](https://github.com/line/line-sdk-starter-ios)
