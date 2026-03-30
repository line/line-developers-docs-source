# Setting up your project

The LINE SDK for Unity provides an interface for using LINE SDK on either iOS or Android platform. To use LINE SDK in Unity Editor and export it to a platform, your development environment needs a few things.

## Unity requirements 

- Unity 2020.3.15 or later, with iOS and Android modules installed
- A valid subscription for Unity Personal, Unity Plus, or Unity Pro

## Installation on iOS 

To integrate LINE SDK for Unity on iOS, you need:

- iOS 13.0 or higher as the deployment target
- Xcode 14.1 or higher

On iOS, LINE SDK for Unity works as a wrapper for the LINE SDK for iOS Swift. It adds the necessary libraries when you export your project to Xcode.

## Installation on Android 

You must have the Android SDK installed, because Unity will use it to build your project to the Android platform. If you have previously [configured Unity for Android development](https://docs.unity3d.com/Manual/android-sdksetup.html), you already have the Android SDK.
