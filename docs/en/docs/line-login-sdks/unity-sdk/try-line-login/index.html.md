# Trying the starter app

The LINE Login starter app for Unity lets you quickly see how [LINE Login](https://developers.line.biz/en/docs/line-login/overview/) works in a Unity game.

## Prerequisites 

Before building and running the starter app, follow the [Setting up your project](https://developers.line.biz/en/docs/line-login-sdks/unity-sdk/project-setup/) guide to set up your environment correctly for Unity, iOS, and Android.

## Trying the starter app with the predefined sample channel 

To try the starter app with our sample channel, follow these steps:

1. Clone the [LINE SDK for Unity open-source repository](https://github.com/line/line-sdk-unity).

    ```sh
    $ git clone https://github.com/line/line-sdk-unity.git
    ```

1. In Unity, open the project in the folder `LINE_SDK_Unity`.
1. Build and export the scene under `Assets/LineSDK/Demo/Scenes/Main` to either iOS or Android.
1. Install the exported project/binary to your device.

<!-- note start -->

**Note**

You may need to modify the certification to install the sample app to an iOS device. If you do not have one, you can go to **Player Settings > Settings for iOS > Other Settings** and set **Target SDK** to **Simulator SDK**, then run the sample app on an iOS simulator.

<!-- note end -->

### Trying the starter app with your own channel 

You can also link the starter app to your own channel. If you don't have a channel yet, [create one now](https://developers.line.biz/console/register/line-login/channel/). You'll also have to select or create a [provider](https://developers.line.biz/en/glossary/#provider).

To link the starter app with your channel, make the following changes in your Unity project:

1. Select **File** > **Build Settings**.
1. Click **Player Settings**.
1. Select ![iPhone, iPod Touch and iPad settings tab](https://developers.line.biz/media/unity-sdk/ios-settings-tab.png) > **Other Settings**, and set **Bundle Identifier** to the same value as **iOS bundle ID** in the **LINE Login** tab of your LINE Login channel in the LINE Developers Console.

    ![Bundle Identifier](https://developers.line.biz/media/unity-sdk/bundle-identifier-settings.png)

1. In the next two fields, set the same value as Android **Package Name** in the **LINE Login** tab of your LINE Login channel in the LINE Developers Console.
    - **Product Name**
    - ![Android settings tab](https://developers.line.biz/media/unity-sdk/android-settings-tab.png) > **Other Settings** > **Package Name**

    ![Package Name](https://developers.line.biz/media/unity-sdk/package-name-settings.png)

1. From the main page, select **LineSDK** object.
1. Enter your LINE Login channel ID in the **Channel ID** field under **Line SDK (Script)**.

    ![Channel ID](https://developers.line.biz/media/unity-sdk/channel-id-settings.png)

## Running the starter app 

Run the starter app using an iOS/Android device or Simulator. When you first log in, you must agree to let the app access your profile information.

Tap **Log in with LINE** to log in using app-to-app login.

If LINE is installed on the device and you are logged in, you will be able to log in to the starter app automatically without entering your LINE credentials. Otherwise, you'll be asked to log in using the browser. In the second scenario, you'll need to enter your LINE credentials.

### Trying out the features available on the LINE SDK 

Once you have logged in to the app, you can tap the menu items to try out the following features of the LINE SDK.

Features available to general users:

- Log out user
- Get user profile
- Verify access token
- Get the friendship status between a LINE Official Account linked to the channel and user

Any other features shown are available only to limited users.
