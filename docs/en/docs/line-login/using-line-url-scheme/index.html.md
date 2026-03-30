# Using LINE features with the LINE URL scheme

You can open Sticker Shop, LIFF app or camera with the LINE URL scheme. The LINE URL scheme works with LINE Official Accounts too. You can let users see LINE contents from [rich menus](https://developers.line.biz/en/docs/messaging-api/using-rich-menus/) with the [action](https://developers.line.biz/en/reference/messaging-api/#uri-action) to open the LINE URL scheme.

## Supported LINE URL schemes 

The following LINE URL schemes are supported:

| URL scheme | Description |
| --- | --- |
| URL schemes beginning with `https://line.me/R/` | URL scheme for using LINE app features |
| URL schemes beginning with `https://liff.line.me/` | URL scheme for opening the [LIFF app](https://developers.line.biz/en/docs/liff/overview/) |
| URL schemes beginning with `https://miniapp.line.me/` | URL scheme for opening the [LINE MINI App](https://developers.line.biz/en/docs/line-mini-app/discover/introduction/) |

<!-- warning start -->

**&quot;line://&quot; is deprecated**

The scheme `line://` is deprecated to prevent takeover attacks that launch a non-LINE app when the URL is clicked, against LY Corporation's or the user's intention. This attack can take place under certain conditions.

No exact date is set for the URL scheme `line://` to become obsolete.

<!-- warning end -->

<!-- note start -->

**LY Corporation doesn't provide a URL scheme for launching native apps other than LINE**

LY Corporation offers no URL scheme to launch native apps other than LINE. However, if a native app from another company has a URL scheme for launching the native app, you can use the URL scheme in the URI action object for [rich menus](https://developers.line.biz/en/docs/messaging-api/using-rich-menus/) or [Flex Messages](https://developers.line.biz/en/docs/messaging-api/using-flex-messages/).

<!-- note end -->

## What happens when a LINE URL scheme is clicked 

When a user clicks a URL using the LINE URL scheme on a device with LINE installed, LINE is automatically launched showing the content specified by the URL. If LINE isn't installed, what happens differ by the scheme:

| LINE URL scheme | What happens when there is no LINE installed |
| --- | --- |
| `https://line.me/R/` | A web browser is launched and prompts the user to download LINE. |
| `line://` (Deprecated) | Nothing happens or the user is redirected to an error page. |

## Supported platforms 

The LINE URL scheme is supported in LINE for iOS and LINE for Android.

<!-- note start -->

**Note**

The LINE URL scheme isn't supported in LINE for PC (macOS, Windows).

<!-- note end -->

## Available LINE URL schemes 

Things you can do with LINE URL schemes are as follows. The LINE URL schemes that are supported only in certain platforms are specified so in each section:

- [Opening the camera and camera roll](https://developers.line.biz/en/docs/line-login/using-line-url-scheme/#opening-the-camera-and-camera-roll)
- [Sending location information](https://developers.line.biz/en/docs/line-login/using-line-url-scheme/#sending-the-location-screen)
- [Sharing a LINE Official Account](https://developers.line.biz/en/docs/line-login/using-line-url-scheme/#sharing-line-official-account)
- [Opening the LINE Official Account's LINE VOOM and business profile](https://developers.line.biz/en/docs/line-login/using-line-url-scheme/#opening-line-voom-and-profile)
- [Opening a chat screen with a LINE Official Account](https://developers.line.biz/en/docs/line-login/using-line-url-scheme/#opening-chat-screen)
- [Sending text messages](https://developers.line.biz/en/docs/line-login/using-line-url-scheme/#sending-text-messages)
- [Opening profile information](https://developers.line.biz/en/docs/line-login/using-line-url-scheme/#opening-profile-information)
- [Opening common LINE screens](https://developers.line.biz/en/docs/line-login/using-line-url-scheme/#opening-common-line-app-screens)
- [Opening LINE settings](https://developers.line.biz/en/docs/line-login/using-line-url-scheme/#opening-line-app-settings-screens)
- [Opening Sticker Shop](https://developers.line.biz/en/docs/line-login/using-line-url-scheme/#opening-the-sticker-shop)
- [Opening Theme Shop](https://developers.line.biz/en/docs/line-login/using-line-url-scheme/#opening-the-theme-shop)
- [Opening a LIFF app](https://developers.line.biz/en/docs/line-login/using-line-url-scheme/#opening-a-liff-app)
- [Opening a URL in an external browser](https://developers.line.biz/en/docs/line-login/using-line-url-scheme/#opening-url-in-external-browser)

### Opening the camera and camera roll 

With the LINE URL scheme, you can let users open the camera or the camera roll. Camera roll is where the users can select images to share in a chat.

<!-- note start -->

**Restriction on opening the camera or the camera roll**

You can open the camera or camera roll with the URL scheme only from LINE chats, including LINE OpenChat. These URL schemes aren't supported in LINE features other than chatting, LIFF apps or apps other than LINE.

<!-- note end -->

![](https://developers.line.biz/media/messaging-api/using-line-url-scheme/camera-screen.png)

![](https://developers.line.biz/media/messaging-api/using-line-url-scheme/camera-roll.png)

| LINE URL scheme | Description |
| --- | --- |
| `https://line.me/R/nv/camera/` | Opens the camera. For smartphones that have multiple cameras, such as front (in-camera) and rear (out-camera), you can't specify which camera to open. |
| `https://line.me/R/nv/cameraRoll/single` | Opens the camera roll. Users can select an image to share in a chat. |
| `https://line.me/R/nv/cameraRoll/multi` | Opens the camera roll. Users can select images to share in a chat. |

### Sending location information 

With the LINE URL scheme, you can open the location information screen and let users send their location information to your LINE Official Account.

<!-- note start -->

**Restriction on opening the location information screen**

You can let users view location information with this URL scheme only in one-on-one chats between the user and your LINE Official Account. This URL scheme isn't supported in other chat types, LIFF apps or apps other than LINE.

<!-- note end -->

![](https://developers.line.biz/media/messaging-api/using-line-url-scheme/location.png)

| LINE URL scheme | Description |
| --- | --- |
| `https://line.me/R/nv/location/` | Opens the location screen. Users can drop a pin on the map to select the location to share. |

### Sharing a LINE Official Account 

With the LINE URL scheme, you can recommend and encourage users and their friends to add your LINE Official Account.

![](https://developers.line.biz/media/messaging-api/using-line-url-scheme/bot-add-friend-en.png)

| LINE URL scheme | Description |
| --- | --- |
| https://line.me/R/ti/p/`{Percent-encoded LINE ID}` | Opens the LINE Official Account's profile page. If the user is a friend with your LINE Official Account, a one-on-one chat is displayed instead. |
| https://line.me/R/nv/recommendOA/`{Percent-encoded LINE ID}` | Opens the "Share with" screen. Users can select friends, group chats, or multi-person chats to share your LINE Official Account with. |

<!-- note start -->

**&quot;Percent-encoded LINE ID&quot; must be percent encoded**

Make sure `{Percent-encoded LINE ID}` is [percent encoded](https://developer.mozilla.org/en-US/docs/Glossary/Percent-encoding) in UTF-8. For example, if the LINE ID is `@linedevelopers` use `https://line.me/R/ti/p/%40linedevelopers` and `https://line.me/R/nv/recommendOA/%40linedevelopers`. If you replaced with the LINE ID that isn't percent encoded, it will also work, but is deprecated.

However, if you percent encode the LINE ID in the URL scheme that opens the "Share with" screen (`https://line.me/R/nv/recommendOA/%40linedevelopers`), it won't work on LINE versions earlier than 13.8.0 for Android.

You can specify either [a Basic ID or a Premium ID](https://help.linebiz.com/lineadshelp/s/article/L000001191?language=ja) (only available in Japanese) as the LINE ID for your LINE Official Account.

<!-- note end -->

<!-- tip start -->

**Verify the LINE ID of the LINE Official Account**

Find the LINE ID of your LINE Official Account in [LINE Official Account Manager](https://manager.line.biz/). For more information, see [Share the LINE ID of your LINE Official Account](https://developers.line.biz/en/docs/messaging-api/sharing-bot/#share-the-line-id-of-your-line-official-account).

<!-- tip end -->

<!-- tip start -->

**LINE URL schemes on a PC browser**

When users open `https://line.me/R/ti/p/{Percent-encoded LINE ID}` from a PC, they see the public URL of the business profile of the LINE Official Account (e.g. [LINE FRIENDS profile page](https://line.me/R/ti/p/@linecharacter)) or only a QR code. What users see depends on these conditions:

- Your LINE Official Account is a verified account
- The public URL of the LINE Official Account profile is set to be available

If both conditions are met, users see the public URL of your LINE Official Account, with a QR code. If not, the user sees only the QR code for your LINE Official Account. You can adjust settings on [LINE Official Account Manager](https://manager.line.biz/) to change an unverified account to a verified account, or to use the public URL of your profile.

<!-- tip end -->

### Opening the LINE Official Account's LINE VOOM and business profile 

With the LINE URL scheme, you can let users open LINE VOOM and the business profile page of your LINE Official Account.

![](https://developers.line.biz/media/messaging-api/using-line-url-scheme/bot-line-voom.png)

| LINE URL scheme | Description |
| --- | --- |
| https://line.me/R/home/public/main?id=`{LINE ID without @}` | Opens the LINE Official Account's LINE VOOM. |
| https://line.me/R/home/public/profile?id=`{LINE ID without @}` | Opens the LINE Official Account's business profile. |
| https://line.me/R/home/public/post?id=`{LINE ID without @}`&postId=`{postId}` | Opens the LINE Official Account's LINE VOOM post. Find the post ID of individual posts in the [LINE VOOM Studio](https://voom-studio.line.biz/). |

<!-- note start -->

**Exclude the at-sign (@) prefix in the URL scheme**

Replace `{LINE ID without @}` in the URL scheme with the LINE ID of your LINE Official Account. You can specify either a basic ID or a [premium ID](https://developers.line.biz/en/glossary/#premium-id). Exclude the at-sign (`@`) prefix from the LINE ID of your LINE Official Account. For example, if the LINE ID is `@linedevelopers`, use `https://line.me/R/home/public/main?id=linedevelopers`.

<!-- note end -->

<!-- tip start -->

**Verify the LINE ID of the LINE Official Account**

Find the LINE ID of your LINE Official Account in [LINE Official Account Manager](https://manager.line.biz/). For more information, see [Share the LINE ID of your LINE Official Account](https://developers.line.biz/en/docs/messaging-api/sharing-bot/#share-the-line-id-of-your-line-official-account).

<!-- tip end -->

<!-- tip start -->

**Posting on LINE VOOM & customizing business profile**

To post on LINE VOOM or customize the business profile for your LINE Official Account, use the [LINE VOOM Studio](https://voom-studio.line.biz/) or the [LINE Official Account Manager](https://manager.line.biz/).

<!-- tip end -->

### Opening a chat screen with a LINE Official Account 

With the LINE URL scheme, you can let users open a chat screen with your LINE Official Account.

| LINE URL scheme | Description |
| --- | --- |
| https://line.me/R/oaMessage/`{Percent-encoded LINE ID}` | Opens a chat screen with your LINE Official Account. |
| https://line.me/R/oaMessage/`{Percent-encoded LINE ID}`/?`{text_message}` | Opens a chat screen with your LINE Official Account and enters the text message set in `{text_message}` into the message input field. |

<!-- note start -->

**&quot;Percent-encoded LINE ID&quot; and &quot;text_message&quot; must be percent encoded**

Make sure `{Percent-encoded LINE ID}` and `{text_message}` are [percent encoded](https://developer.mozilla.org/en-US/docs/Glossary/Percent-encoding) in UTF-8. For example, if you are sending a text message "Hi there!" to a LINE Official Account with the LINE ID `@linedevelopers`, use `https://line.me/R/oaMessage/%40linedevelopers/?Hi%20there%21`. If you replaced with the LINE ID that isn't percent encoded, it will also work, but is deprecated.

You can specify either [a Basic ID or a Premium ID](https://help.linebiz.com/lineadshelp/s/article/L000001191?language=ja) (only available in Japanese) as the LINE ID for your LINE Official Account.

<!-- note end -->

<!-- tip start -->

**Verify the LINE ID of the LINE Official Account**

Find the LINE ID of your LINE Official Account in [LINE Official Account Manager](https://manager.line.biz/). For more information, see [Share the LINE ID of your LINE Official Account](https://developers.line.biz/en/docs/messaging-api/sharing-bot/#share-the-line-id-of-your-line-official-account).

<!-- tip end -->

### Sending text messages 

With the LINE URL scheme, you can set a text message for a user to send to their friends or to LINE Official Accounts.

| LINE URL scheme | Description |
| --- | --- |
| https://line.me/R/share?text=`{text_message}` | Opens the "Share with" screen. Users can select friends, group chats, or multi-person chats to send a text message specified with `{text_message}`. Users can send the text also to Keep Memo, LINE VOOM, and other apps. |

<!-- note start -->

**&quot;text_message&quot; must be percent encoded**

Make sure `{text_message}` is [percent encoded](https://developer.mozilla.org/en-US/docs/Glossary/Percent-encoding) in UTF-8. For example, if you are sending a text message "Hi there!", use `https://line.me/R/share?text=Hi%20there%21`.

<!-- note end -->

### Opening profile information 

With the LINE URL scheme, you can let users open their "My profile" screen. On this screen, users can update their display name and status message, set their LINE ID and view profile settings.

![](https://developers.line.biz/media/messaging-api/using-line-url-scheme/my-profile.png)

| LINE URL scheme | Description |
| --- | --- |
| `https://line.me/R/nv/profile` | Opens the user's "My profile" screen. |
| `https://line.me/R/nv/profileSetId` | Opens the user's "LINE ID" screen. With this URL scheme, you can let users set their LINE ID if they didn't set the ID yet. |

### Opening common LINE screens 

With the LINE URL scheme, you can let users open different LINE screens, including the Chats tab.

![](https://developers.line.biz/media/messaging-api/using-line-url-scheme/shopping-tab-en.png)

| LINE URL scheme | Description |
| --- | --- |
| `https://line.me/R/nv/chat` | Opens the Chats tab. |
| `https://line.me/R/nv/commerce` | Opens the Shopping tab. |
| `https://line.me/R/nv/wallet` | Opens the Wallet tab. |
| `https://line.me/R/nv/addFriends` | Opens the "Add friends" screen. |
| `https://line.me/R/nv/officialAccounts` | Opens the "LINE Official Accounts" screen. |
| `https://line.me/R/nv/timeline` | Opens the LINE VOOM "Following" screen. |

### Opening LINE settings 

With the LINE URL scheme, you can open different settings menu.

![](https://developers.line.biz/media/messaging-api/using-line-url-scheme/settings.png)

| LINE URL scheme | Description |
| --- | --- |
| `https://line.me/R/nv/settings` | Opens Settings. |
| `https://line.me/R/nv/settings/account` | Opens Account settings. Displays the user's LINE account information. |
| `https://line.me/R/nv/connectedApps` | Opens Account > Authorized apps. Shows the permissions granted to authorized apps and lets users unlink apps. |
| `https://line.me/R/nv/connectedDevices` | Opens Account > Connected devices. |
| `https://line.me/R/nv/settings/privacy` | Opens Privacy settings. |
| `https://line.me/R/nv/settings/sticker` | Opens Stickers settings. |
| `https://line.me/R/nv/stickerShop/mySticker` | Opens Stickers > My Stickers. |
| `https://line.me/R/nv/settings/themeSettingsMenu` (iOS), `https://line.me/R/nv/settings/theme` (Android) | Opens Themes settings.<br />The scheme is different for iOS and Android. |
| `https://line.me/R/nv/themeSettings` | Opens Themes > My Themes. |
| `https://line.me/R/nv/notificationServiceDetail` | Opens Notification > Authorized apps. Lets users set notification for authorized apps. |
| `https://line.me/R/nv/settings/chatSettings` | Opens Chats settings. |
| `https://line.me/R/nv/suggestSettings` | Opens Chats > Display suggestions. |
| `https://line.me/R/nv/settings/callSettings` | Opens Calls settings. |
| `https://line.me/R/nv/settings/addressBookSync` | Opens Friends settings. |
| `https://line.me/R/nv/settings/timelineSettings` | Opens LINE VOOM settings. |

### Opening Sticker Shop 

With the LINE URL scheme, you can let users open Sticker Shop in LINE to encourage purchase of official and creators' sticker sets.

![](https://developers.line.biz/media/messaging-api/using-line-url-scheme/sticker-shop-categories.png)

| LINE URL scheme | Description |
| --- | --- |
| https://line.me/R/shop/sticker/detail/`{package_id}` | Opens a Sticker set info screen. Specify `{package_id}` to the number specified in the sticker's page URL in [LINE STORE](https://store.line.me/). |
| https://line.me/R/shop/category/`{category_id}` | Opens a popularity ranking for the given category. Specify `{category_id}` to the number specified in the category page URL in [LINE STORE](https://store.line.me/) > Official stickers. |
| https://line.me/R/shop/sticker/author/`{author_id}` | Opens a list of sticker sets from the given author. Specify `{author_id}` to the number specified in the creator's page URL in [LINE STORE](https://store.line.me/). |
| `https://line.me/R/nv/stickerShop` | Opens Sticker Shop > HOME tab. |
| `https://line.me/R/shop/sticker/hot` | Opens Sticker Shop > RANK tab. |
| `https://line.me/R/shop/sticker/new` | Opens Sticker Shop > NEW tab. |
| `https://line.me/R/shop/sticker/event` | Opens Sticker Shop > FREE tab. |
| `https://line.me/R/shop/sticker/category` | Opens Sticker Shop > CATEGORIES tab. |

<!-- tip start -->

**Create your own sticker set**

To create your own sticker sets for users, visit [LINE Creators Market](https://creator.line.me/en/) and use the [LINE Sticker Maker](https://creator.line.me/en/stickermaker/) app.

<!-- tip end -->

### Opening Theme Shop 

With the LINE URL scheme, you can let user open Theme Shop in LINE to encourage purchase of official and creators' theme.

![](https://developers.line.biz/media/messaging-api/using-line-url-scheme/theme-shop.png)

| LINE URL scheme | Description |
| --- | --- |
| https://line.me/R/shop/theme/detail?id=`{product_id}` | Opens a Theme info screen. Specify `{product_id}` to the ID specified in the theme page URL in [LINE STORE](https://store.line.me/). For example, if you open [Matte White](https://store.line.me/themeshop/product/0bac8fed-4c75-40c5-9982-e9ecc3b9d191/en)`https://store.line.me/themeshop/product/0bac8fed-4c75-40c5-9982-e9ecc3b9d191/en`, specify `0bac8fed-4c75-40c5-9982-e9ecc3b9d191`. |

### Opening a LIFF app 

With the LINE URL scheme, you can let users open a LIFF app. A LIFF app is a web app built using the [LINE Front-end Framework (LIFF)](https://developers.line.biz/en/docs/liff/overview/).

![](https://developers.line.biz/media/messaging-api/using-line-url-scheme/liff-app.png)

| LINE URL scheme | Description |
| --- | --- |
| https://liff.line.me/`{liffId}` | Opens the LIFF app with the given LIFF ID. This URL scheme is called a LIFF URL. |
| https://liff.line.me/`{liffId}`/path_A/path_B/?key1=value1&key2=value2 | Opens the LIFF app with the given LIFF ID. You can pass `/path_A/path_B/?key1=value1&key2=value2` as extra information. |

For more information on the process of opening a LIFF app, see [Opening a LIFF app](https://developers.line.biz/en/docs/liff/opening-liff-app/) in the LIFF documentation.

<!-- note start -->

**&quot;https://line.me/R/app/{liffId}&quot; and &quot;line://app/{liffId}&quot; are deprecated**

The following LIFF URL formats used in [LIFF v1](https://developers.line.biz/en/docs/liff/versioning-policy/#life-cycle-schedule) are [deprecated](https://developers.line.biz/en/glossary/#deprecated):

- `https://line.me/R/app/{liffId}`&nbsp;
- `line://app/{liffId}`&nbsp;

<!-- note end -->

### Opening a URL in an external browser 

With the query parameters, you can let users open a URL in an [external browser](https://developers.line.biz/en/glossary/#external-browser) instead of [LINE's in-app browser](https://developers.line.biz/en/glossary/#line-iab).

<!-- note start -->

**These query parameters aren't supported on LIFF apps**

These query parameters work for all URLs accessed from the LINE app, except for on LIFF apps. Even if you add these query parameters to a LIFF URL, it won't open in an external browser.

<!-- note end -->

| URL with the query parameter | Description |
| --- | --- |
| https://example.com/?`openExternalBrowser=1` | Opens target URL, in an external browser. |
| https://example.com/?`openInAppBrowser=0` | Opens target URL, in a Chrome custom tab (only available in LINE for Android). |
