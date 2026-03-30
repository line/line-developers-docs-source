# Adding a LIFF app to your channel

When you add a LIFF app to a LINE Login channel on the [LINE Developers Console](https://developers.line.biz/console/), the LIFF app can run either in LINE or in an external browser.

<!-- tip start -->

**We recommend creating a LIFF app as a LINE MINI App**

In the future, LIFF and the LINE MINI App will be integrated into a single brand. As a result of this integration, LIFF will be integrated into the LINE MINI App. For this reason, we recommend that you create a new LIFF app as a LINE MINI App. For more information, see the news from [February 12, 2025](https://developers.line.biz/en/news/2025/02/12/line-mini-app/).

<!-- tip end -->

## Before you begin 

Make sure you've done the following:

- [Created a channel](https://developers.line.biz/en/docs/liff/getting-started/) for your app.
- Deployed the LIFF app on any server according to the instructions in [Trying a LIFF starter app](https://developers.line.biz/en/docs/liff/trying-liff-app/) or [Developing a LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/).

## Adding the LIFF app to your channel 

You can add up to 30 LIFF apps to each channel.

1. On the [LINE Developers Console](https://developers.line.biz/console/), select the LINE Login channel to which you want to add the LIFF app, then click the **LIFF** tab.

1. Click **Add**.

1. Concatenate the following items in the order listed. You can always change your settings later:

   **Basic information**

   | Item | Description | Location displayed to users |
   | --- | --- | --- |
   | LIFF app name | Name of the LIFF app. The LIFF app name can't include "LINE" or similar strings, or inappropriate strings. | <ul><li>[Message displayed when another LIFF app is opened](https://developers.line.biz/en/docs/liff/opening-liff-app/#messages-liff-to-liff)</li><li>[Multi-tab view](https://developers.line.biz/en/docs/liff/overview/#multi-tab-view)</li></ul> |
   | Size | Size of the LIFF app view. Select one of:<ul><li>`Compact`</li><li>`Tall`</li><li>`Full`</li></ul><br/><img src="/media/liff/overview/viewTypes.png" width="375px"> | - |
   | Endpoint URL | The URL of the LIFF web app (e.g. `https://example.com`). This URL will be used when the LIFF app is launched using the LIFF URL.<br />The URL scheme must be **https**. URL fragments (#URL-fragment) can't be specified. | [LIFF browser](https://developers.line.biz/en/docs/liff/overview/#liff-browser) header (domain name only) |
   | Scopes \*1 | Scope required for some LIFF SDK methods to function.<ul><li>`openid`: Scope required to use [`liff.getIDToken()`](https://developers.line.biz/en/reference/liff/#get-id-token) and [`liff.getDecodedIDToken()`](https://developers.line.biz/en/reference/liff/#get-decoded-id-token).</li><li>`email`: Scope required to get the user's email address using [`liff.getIDToken()`](https://developers.line.biz/en/reference/liff/#get-id-token) or [`liff.getDecodedIDToken()`](https://developers.line.biz/en/reference/liff/#get-decoded-id-token). \*2 <li>`profile`: Scope required to use [`liff.getProfile()`](https://developers.line.biz/en/reference/liff/#get-profile) or [`liff.getFriendship()`](https://developers.line.biz/en/reference/liff/#get-friendship).</li><li>`chat_message.write`: Scope required to use [`liff.sendMessages()`](https://developers.line.biz/en/reference/liff/#send-messages). Depending on your account type, this option may appear under **View all**. \*3</li></ul> | Permission consent screen when launching LIFF app |
   | Add friend option \*4 | The setting for [add friend option](https://developers.line.biz/en/docs/line-login/link-a-bot/)<ul><li>`On (normal)`: Adds the option of adding the LINE Official Account as a friend on the LIFF app permission consent screen.</li><li>`On (aggressive)`: Displays a screen after the LIFF app permission consent screen to confirm whether the user wants to add the LINE Official Account as a friend.</li><li>`Off`: Doesn't display the option of adding the LINE Official Account as a friend.</li></ul> | Permission consent screen when launching LIFF app |

   **Options**

   | Item | Description |
   | --- | --- |
   | Scan QR | Enable this setting when using [`liff.scanCodeV2()`](https://developers.line.biz/en/reference/liff/#scan-code-v2) in the LIFF apps added to this channel. |
   | Module mode  | Enable this setting when using the LIFF app in module mode. When **Module mode** is enabled, the action button in the header is hidden. This option will be displayed only if you have selected **Full** for size of the LIFF app view. |

   \*1 For more information on scopes displayed to corporate customers who are registered to use the scopes, see [LINE Profile+](https://developers.line.biz/en/docs/partner-docs/line-profile-plus/) under the options for corporate customers documentation.</br> \*2 Displayed only if you applied for OpenId Connect email permission in a LINE Login channel.<br> \*3 The `chat_message.write` scope may be disabled in a LIFF app after the LIFF-to-LIFF transition. For more information, see [About the "chat_message.write" scope after transitioning between LIFF apps](https://developers.line.biz/en/docs/liff/opening-liff-app/#about-chat-message-write-scope).<br> \*4 Displayed only for LINE Login channels.

1. Click **Add**.

   When adding the LIFF app, a LIFF ID and LIFF URL are created.

   | Item | Description |
   | --- | --- |
   | LIFF ID | LIFF app ID.<br>e.g. `1234567890-AbcdEfgh` |
   | LIFF URL | The URL to access to LIFF apps. When users access the LIFF URL, they are redirected through the LIFF server provided by LY Corporation to the LIFF app server (endpoint URL) provided by the developer.<br>e.g. `https://liff.line.me/1234567890-AbcdEfgh` |

## The order of LIFF apps on the LIFF tab 

On the **LIFF** tab of LINE Login channels, the LIFF apps will be displayed in the following order:

1. The LIFF apps added to the LINE Login channel on or after May 23, 2023 will be displayed in descending order of the date added
1. The LIFF apps added to the LINE Login channel before May 23, 2023 will be displayed in no particular order

![Examples of LIFF apps displayed on the LIFF tab](https://developers.line.biz/media/liff/order-of-liff-apps-en.png)

## Other operations 

You can also perform these operations from the **LIFF** tab of the LINE Developers Console.

- Edit LIFF app settings
- Delete the LIFF app from your channel

## Next steps 

After adding the LIFF app to your channel, try opening it.

- [Open the LIFF app](https://developers.line.biz/en/docs/liff/opening-liff-app/)
