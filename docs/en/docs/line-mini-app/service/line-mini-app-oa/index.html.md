# Use LINE Official Account

This page introduces how to use a LINE Official Account to promote your LINE MINI App. For more information about how to create a LINE Official Account, see [Create a LINE Official Account](https://developers.line.biz/en/docs/messaging-api/getting-started/#create-oa) in the Messaging API documentation.

![Promote your LINE MINI App on LINE Official Account](https://developers.line.biz/media/line-mini-app/mini_with_oa.png)

## Send rich messages 

Sending visually engaging rich messages helps users quickly understand the value of your LINE MINI App and encourages more users to access it.

For more information about rich messages, see [Rich messages](https://www.lycbiz.com/jp/manual/OfficialAccountManager/rich-messages/) (only available in Japanese) in LINE for Business.

## Set a link to your LINE MINI App in a rich menu 

By setting your LINE MINI App's [LIFF URL](https://developers.line.biz/en/glossary/#liff-url) or [permanent link](https://developers.line.biz/en/glossary/#permanent-link-liff) in a rich menu, users can easily access your LINE MINI App from the LINE Official Account chat screen.

For more information about rich menus, see [Rich menus overview](https://developers.line.biz/en/docs/messaging-api/rich-menus-overview/) in the Messaging API documentation.

## Add the LINE Official Account as a friend on the LINE MINI App 

You can use either of the following features to encourage users to add your LINE Official Account as a friend on the LINE MINI App:

- [Add friend option](https://developers.line.biz/en/docs/line-mini-app/service/line-mini-app-oa/#link-a-line-official-account-with-your-channel)
- [`liff.requestFriendship()` method](https://developers.line.biz/en/docs/line-mini-app/service/line-mini-app-oa/#use-liff-request-friendship)

### Add friend option 

You can display an option to add your LINE Official Account as a friend on the [verification screen](https://developers.line.biz/en/docs/line-mini-app/develop/configure-console/#verification-screen) or the [channel consent screen](https://developers.line.biz/en/docs/line-mini-app/develop/configure-console/#consent-screen-settings) of your LINE MINI App. This is called the add friend option.

To link a LINE MINI App to a LINE Official Account using the add friend option, all of the following conditions must be met:

- The LINE Official Account uses the Messaging API (\*1).
- The Messaging API channel linked to the LINE Official Account and the LINE MINI App channel belong to the same provider.
- The account used to perform the operation has both the Admin role for the LINE MINI App channel (\*2) and the Administrator role for the LINE Official Account (\*3).

\*1 For more information about how to use the Messaging API with a LINE Official Account, see [Enable the Messaging API for your LINE Official Account](https://developers.line.biz/en/docs/messaging-api/getting-started/#using-oa-manager) in the Messaging API documentation.\
\*2 You can check the Admin role for a LINE MINI App channel in the [LINE Developers Console](https://developers.line.biz/console/).\
\*3 You can check the Administrator role for a LINE Official Account in the [LINE Official Account Manager](https://manager.line.biz).

#### How to set the add friend option 

1. In the [LINE Developers Console](https://developers.line.biz/console/), click the **Basic settings** tab of the LINE MINI App channel.
1. In the "Linked LINE Official Account" section, click **Edit**.
1. Select the LINE Official Account to link to the LINE MINI App channel, then click **Update**.
1. Click the **Web app settings** tab of the LINE MINI App channel.
1. In the "Add friend option" section, click **Edit**.
1. Select **On (normal)**, then click **Update**.

<!-- tip start -->

**For certified providers, the add friend option on authorization screens is enabled by default**

If a LINE MINI App channel belongs to a [certified provider](https://developers.line.biz/en/docs/line-developers-console/overview/#certified-provider), the add friend option on the verification screen and the channel consent screen is enabled by default.

Unless users manually turn off the option, the LINE Official Account specified for the add friend option will be added as a friend when users grant authorization on the verification screen or the channel consent screen.

<!-- tip end -->

#### Important points about using the "Channel consent simplification" feature concurrently 

If you use the "[Channel consent simplification](https://developers.line.biz/en/docs/line-mini-app/develop/channel-consent-simplification/#what-is-channel-consent-simplification)" feature (\*) together with the add friend option, the verification screen and the channel consent screen may not be displayed.

For more information, see [Important points about using the "Channel consent simplification" feature together with the add friend option](https://developers.line.biz/en/docs/line-mini-app/develop/channel-consent-simplification/#add-friend-option).

\* For new LINE MINI App channels in Japan, [the use of the "Channel consent simplification" feature has been mandatory since January 8, 2026](https://developers.line.biz/en/news/2026/01/08/channel-consent-simplification/).

### `liff.requestFriendship()` method 

By calling the [`liff.requestFriendship()`](https://developers.line.biz/en/reference/liff/#request-friendship) method, you can display a subwindow that prompts users to add your LINE Official Account as a friend or unblock it.

For more information, see [Requesting the user to add the LINE Official Account as a friend or unblock it](https://developers.line.biz/en/docs/liff/developing-liff-apps/#request-friendship) in the LIFF documentation.
