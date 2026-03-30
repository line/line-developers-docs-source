# LINE Beacon

<!-- note start -->

**An application is required to use optional features**

The features in this document are only available to corporate users who have submitted the required application. To use this service for your company's LINE Official Account, contact your sales representative or [our Sales partners](https://www.lycbiz.com/jp/partner/sales/).

<!-- note end -->

## About user settings 

To receive LINE Beacon, users must meet these conditions:

- The version of the OS that you use for LINE must meet the requirements.
- The smartphone's Bluetooth setting is on.
- You've agreed to use LINE Beacon on LINE. ("Settings" > **Privacy** > **Provide usage data** > **LINE Beacon**)

For more information, including OS version requirements, see [Using LINE Beacon](https://help.line.me/line/?contentId=50001493) in the Help Center.

## About LINE Beacon reception conditions 

LINE Beacon reception conditions are different for each OS type and LINE app running status.

Here are the meanings of "foreground" and "background" used in the reception conditions:

| Term       | Description                    |
| ---------- | ------------------------------ |
| Foreground | LINE is running and in use     |
| Background | LINE is running but not in use |

<!-- note start -->

**Behavior when LINE isn't running**

The behavior when LINE isn't running is undefined. It isn't included in the "background."

<!-- note end -->

### LINE Beacon reception conditions (iOS) 

The reception conditions for each LINE app running status on iOS are as follows:

| LINE app running status | Reception conditions |
| --- | --- |
| Foreground | The [user settings](https://developers.line.biz/en/docs/partner-docs/line-beacon/#about-user-settings-for-line-beacon) meet the condition |
| Background | All of the following conditions must be met:<ul><li>The [user settings](https://developers.line.biz/en/docs/partner-docs/line-beacon/#about-user-settings-for-line-beacon) meet the condition</li><li>**Location Services** (\*1) is ON</li><li>LINE app's **ALLOW LOCATION ACCESS** (\*2) is set to "Always"</li><li>LINE app's **Precise location** (\*2\*3) is ON</li></ul> |

\*1 **Settings** > **Privacy & Security** > **Location Services**\
\*2 **Settings** > **LINE** > **Location**\
\*3 Displayed only when **ALLOW LOCATION ACCESS** is ON

### LINE Beacon reception conditions (Android) 

The reception conditions for each LINE app running status on Android are as follows:

| LINE app running status | Reception conditions |
| --- | --- |
| Foreground | All of the following conditions must be met:<ul><li>The [user settings](https://developers.line.biz/en/docs/partner-docs/line-beacon/#about-user-settings-for-line-beacon) meet the condition</li><li>**Use location** (\*1) is ON</li><li>LINE app's **Location permission** (\*2) is set to "Allow only while using the app"</li><li>LINE app's **Use precise location** (\*2) is ON</li><li>LINE app's **Nearby devices permission** (\*3) is set to "Allow"</li></ul> |
| Background | Background receiving isn't available on Android. |

\*1 **Settings** > **Location** > **Use location**\
\*2 **Settings** > **Apps** > **LINE** > **Permissions** > **Location**\
\*3 **Settings** > **Apps** > **LINE**

### Beacon banner display conditions 

<!-- note start -->

**Note**

These conditions also apply to test accounts.

<!-- note end -->

#### If your LINE Official Account is searchable 

| LINE Official Account<br>and friends | Agree to LINE Beacon<br>Terms of Use | Beacon banner display |
| --- | --- | --- |
| Friend added | Agreed | Hidden |
| Friend added | Not agreed | Hidden |
| Friend not added | Agreed | Display |
| Friend not added | Not agreed | Hidden |

#### If your LINE Official Account isn't searchable 

Beacon banners won't be displayed regardless of whether you're friends with the LINE Official Account or agree to the LINE Beacon Terms of Use.
