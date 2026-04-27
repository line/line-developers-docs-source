# Release notes for LINE SDK for Android

<!-- note start -->

**Release notes for version 5.0.0 or later are available on the GitHub repository**

Release notes for LINE SDK for Android version 5.0.0 or later are available on the GitHub repository. For more information, see [Releases](https://github.com/line/line-sdk-android/releases).

<!-- note end -->

November 30, 2018

## LINE SDK 4.0.10 for Android released

The LINE SDK 4.0.10 for Android has been released. For more information on downloading the LINE SDK, see below.

- [Download LINE SDK](https://developers.line.biz/en/docs/downloads/)

Changes:

- Fixed an issue where an activity is not found when authenticating with LINE Login after LINE is invalidated on the device.

We will continue to provide improvements so that you can code more easily.

November 20, 2018

## LINE SDK 5.0.0 for Android released

The LINE SDK 5.0.0 for Android has been released. For installation and usage instructions, see the [LINE SDK for Android guide](https://developers.line.biz/en/docs/line-login-sdks/android-sdk/).

#### Changes

##### LINE Login v2.1 and Social API v2.1 are supported

You can set permissions to be granted to your app as scopes when users log in to your app with the LINE Login. By setting scopes, you can get ID tokens when you get access tokens. Those tokens contain user data according to the scopes you set with the login request.

You can display an option to add your bot as a friend to users logging in to your app. You can get the friendship status between users and your bot with login responses and the Social API.

##### Open-source SDK

From version 5.0.0, the LINE SDK for Android is open-sourced. Visit [our repository](https://github.com/line/line-sdk-android) to check the provided code and samples.

##### Detailed reference

Now you can access detailed reference based on the source code. For more information, see the [LINE SDK for Android reference](https://developers.line.biz/en/reference/android-sdk/).

March 12, 2018

## LINE SDK 4.0.8 for Android released

The LINE SDK 4.0.8 for Android has been released. For more information on downloading the LINE SDK, see below.

- [Download LINE SDK](https://developers.line.biz/en/docs/downloads/)

Changes:

- Fixed an infinite loading indicator problem that occurs if the user attempts to log in before LINE has been opened for the first time.

We will continue to provide improvements so that you can code more easily.

February 6, 2018

## LINE SDK 4.0.7 for Android released

The LINE SDK 4.0.7 for Android has been released. For more information on downloading the LINE SDK, see below.

- [Download LINE SDK](https://developers.line.biz/en/docs/downloads/)

Changes:

- Fixed a crash that occurs if the user exits LINE using the home button and then opens the SDK app before LINE finishes the authentication process.

We will continue to provide improvements so that you can code more easily.

September 29, 2017

## LINE SDK 4.0.6 for Android released

The LINE SDK 4.0.6 for Android has been released. For more information on downloading the LINE SDK, see below.

- [Download LINE SDK](https://developers.line.biz/en/docs/downloads/)

Changes:

- Fixed an infinite loading indicator problem that occurs when the user presses the back button while LINE's passcode prompt is on screen.

We will continue to provide improvements so that you can code more easily.

June 2, 2017

## LINE SDK 4.0.5 for Android released

The LINE SDK 4.0.5 for Android has been released. For more information on downloading the LINE SDK, see below.

- [Download LINE SDK](https://developers.line.biz/en/docs/downloads/)

Changes:

- Fixed an issue where a runtime error occurs upon calling `startActivityForActivity` with a login intent when using `appcompat` version 25.0.0 or higher.

April 26, 2017

## LINE SDK 4.0.4 for Android released

The LINE SDK 4.0.4 for Android has been released. For more information on download the LINE SDK, see below.

- [Download LINE SDK](https://developers.line.biz/en/docs/downloads/)

Changes:

- Made a minor change to the SDK’s authentication logic to fix a problem where `onActivityResult` does not get executed during app-to-app login.
- Fixed a known issue in 4.0.2 where `onActivityResult` returns a result of "CANCEL" on the first time that a user logs into an application using app-to-app login.

April 10, 2017

## LINE SDK 4.0.2 for Android released

The LINE SDK 4.0.2 for Android has been released. You can download the SDK from the following page.

- [Download LINE SDK](https://developers.line.biz/en/docs/downloads/)

Changes:

- Fixed an issue where browser login fails with an INTERNAL_ERROR on Android 4.x devices.

Known issues:

- On Android 4.x devices, onActivityResult returns a result of "CANCEL" the first time that a user logs into an application using the app-to-app login. However, the user will be able to successfully log in from their second attempt. This issue is caused by a problem in LINE and will be resolved in a future update.

October 14, 2016

## LINE SDK 3.1.21 for Android released

The LINE SDK for Android has been updated to version 3.1.21. You can download it from the LINE SDK archives on the following page:

- [Download LINE SDK](https://developers.line.biz/en/docs/downloads/)

Changes:

- Updated to prevent build warnings.

October 11, 2016

## LINE SDK 3.1.20 for Android released

The LINE SDK for Android has been updated to version 3.1.20. You can download it from the LINE SDK archives on the following page:

- [Download LINE SDK](https://developers.line.biz/en/docs/downloads/)

Changes:

- Updated build with Java 1.7 for compatibility.

March 15, 2016

## LINE SDK 3.1.19 for Android version released

The LINE SDK for Android has been updated to version 3.1.19. You can download it from the LINE SDK archives on the following page:

- [Download LINE SDK](https://developers.line.biz/en/docs/downloads/)

Changes:

- Fixed login error issue when user attempts to login again

March 9, 2016

## LINE SDK 3.1.18 for Android released

The LINE SDK for Android has been updated to version 3.1.18. You can download it from the LINE SDK archives on the following page:

- [Download LINE SDK](https://developers.line.biz/en/docs/downloads/)

Changes:

- Added support for 64-bit architecture
- Added the locale property to the login method
- Fixed some bugs
