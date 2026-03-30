# Add a shortcut to your LINE MINI App to the home screen of the user's device

<!-- tip start -->

**This feature can only be used for verified MINI Apps**

This feature is only available for verified MINI Apps. For unverified MINI Apps, you can test the feature on the internal channel for Developing, but you can't use the feature on the internal channel for Published.

<!-- tip end -->

The user can add a shortcut to your LINE MINI App to the home screen of the user's device.

Tapping **Add to Home** option after opening the [multi-tab view](https://developers.line.biz/en/docs/line-mini-app/discover/builtin-features/#multi-tab-view) from the [action button](https://developers.line.biz/en/docs/line-mini-app/discover/builtin-features/#action-button) or using the [`liff.createShortcutOnHomeScreen()`](https://developers.line.biz/en/reference/liff/#create-shortcut-on-home-screen) method will display the Add Shortcut screen. The user can add a shortcut to your LINE MINI App to the home screen of the user's device by following the instructions on the screen. This allows the user to access your LINE MINI App directly from the home screen of the user's device.

**Display on Android device**

<!-- note start -->

**On some Android devices, the existing shortcuts may be removed**

On some Android devices, if a user changes the icon from **Settings** > **App icon** of the LINE app, the existing shortcuts may be removed. For more information, see [\[Android\] If you have problems with the LINE shortcut after changing the LINE app icon](https://help.line.me/line/smartphone/pc?lang=ja&contentId=200000315) (only available in Japanese) in the LINE Help Center.

<!-- note end -->

![](https://developers.line.biz/media/line-mini-app/develop/add-to-home-screen/add-shortcut-screen-android-en.png)
![](https://developers.line.biz/media/line-mini-app/develop/add-to-home-screen/shortcut-android.png)

**Display on iOS device**

![](https://developers.line.biz/media/line-mini-app/develop/add-to-home-screen/add-shortcut-screen-ios-en.png)
![](https://developers.line.biz/media/line-mini-app/develop/add-to-home-screen/shortcut-ios-en.png)

Using this feature for services that users frequently use, such as membership cards and mobile ordering, can improve the user experience.

## Operating conditions 

If the OS of the user's device is iOS, the conditions for **Add to Home** and the `liff.createShortcutOnHomeScreen()` method to work are as follows. If **Add to Home** is tapped or the `liff.createShortcutOnHomeScreen()` method is executed in a non-working environment, an error page will be displayed.

| Default browser | iOS version | Whether it works or not |
| --- | --- | --- |
| Safari | All versions | Works |
| Chrome | 16.4 or later | Works |
| Browsers other than Safari and Chrome | 16.4 or later | Not guaranteed to work |
| Browsers other than Safari | Earlier than 16.4 | Doesn't work |

For example, if you execute the `liff.createShortcutOnHomeScreen()` method in Chrome on earlier than iOS 16.4, the following error page will be displayed:

![](https://developers.line.biz/media/line-mini-app/develop/add-to-home-screen/add-shortcut-screen-ios-error-en.png)
