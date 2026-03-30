# Integrating LINE Login with your Unity game

After you [set up your project](https://developers.line.biz/en/docs/line-login-sdks/unity-sdk/project-setup/), you can start importing LINE SDK for Unity into your existing Unity game and leverage LINE Login to improve your app's user experience.

## Getting the SDK 

### Download from GitHub 

To get the latest LINE SDK for Unity, download the `.unitypackage` file from our [GitHub Releases page](https://github.com/line/line-sdk-unity/releases).

### Import into your project 

<!-- note start -->

**Note**

Before you import LINE SDK for Unity into your project, backup your project and/or store it in a version control system.

<!-- note end -->

With your Unity project open, double-click on the downloaded `.unitypackage` file. Import everything in the package, as seen here:

![Import Unity package](https://developers.line.biz/media/unity-sdk/importing.png)

## Add LineSDK prefab to your scene 

After importing the package, in your **Project** panel, you'll find a **LineSDK** prefab under `Assets/LineSDK/`. Drag it to the **Hierarchy** panel of the scene to which you want to add LINE Login:

![Add LineSDK prefab](https://developers.line.biz/media/unity-sdk/adding-prefab.png)

Then, click on the LineSDK GameObject in the scene, and update the **Channel ID** field with your LINE Login channel ID:

![Set Channel ID](https://developers.line.biz/media/unity-sdk/setting-channel-id.png)

Find your LINE Login channel ID in the [LINE Developers Console](https://developers.line.biz/console/). If you don't have a channel yet, [create one](https://developers.line.biz/console/register/line-login/channel/) in the LINE Developers Console. You'll also have to select or create a [provider](https://developers.line.biz/en/glossary/#provider).

## Update player settings 

Before you continue to implement LINE Login or use LINE APIs in your game, follow the steps below to make sure your project player setting is correct.

### Settings for Android export 

1. Select **File > Build Settings**.
1. Click **Player Settings**.
1. Set **Company Name** and **Product Name** to the same value as **Package names** in your channel settings in the LINE Developers Console (**LINE Login** tab).
1. Select ![Android settings tab](https://developers.line.biz/media/unity-sdk/android-settings-tab.png) > **Other Settings**.
1. Set **Package Name** to the same value as **Package names** in the **LINE Login** tab of your channel in LINE Developer Console.
1. Set **Minimum API Level** to at least **API level 19**.
1. Under **Publishing Settings**, enable **Custom Gradle Template**.

### Settings for iOS export 

1. Select **File > Build Settings**.
1. Click **Player Settings**.
1. Select ![iPhone, iPod Touch and iPad settings tab](https://developers.line.biz/media/unity-sdk/ios-settings-tab.png) > **Other Settings**.
1. Set **Bundle Identifier** to the same value as **iOS bundle ID** in the **LINE Login** tab of your channel in the LINE Developers Console.
1. Set **Target minimum iOS Version** to at least `11.0`.

For more about the dependency manager used in LINE SDK for Unity iOS, see [Setting up your project](https://developers.line.biz/en/docs/line-login-sdks/unity-sdk/project-setup/).

## Implement login with LINE 

Now, you can implement login with LINE in the scene where the LineSDK (GameObject) exists. For example:

```csharp
using Line.LineSDK;

public class MyController : MonoBehaviour {
    public void LoginButtonClicked() {
        var scopes = new string[] {"profile", "openid"};
        LineSDK.Instance.Login(scopes, result => {
            result.Match(
                value => {
                    Debug.Log("Login OK. User display name: " + value.UserProfile.DisplayName);
                },
                error => {
                    Debug.Log("Login failed, reason: " + error.Message);
                }
            );
        });
    }
}
```

LINE SDK for Unity supports only iOS and Android for now. It will always return an error if you run it in Unity Editor play mode. To test it, you need to export your scene to either an iOS or Android device.
