# Managing roles

By managing provider and channel roles, you can control the information that developers can view and edit on the [LINE Developers Console](https://developers.line.biz/console/). This page describes the types of roles that can be assigned to developers registered on providers and channels.

The provider and channel each have respective roles.

- [Provider roles](https://developers.line.biz/en/docs/line-developers-console/managing-roles/#roles-for-provider)
- [Channel roles](https://developers.line.biz/en/docs/line-developers-console/managing-roles/#roles-for-channel)

## Provider roles 

A developer who is registered as a provider can be given either the Admin role or Member role.

It's possible to grant channel access to a developer without granting provider access. In this case, the developer's role in the provider will be "No role".

|                                          | Admin | Member | No role \*1 |
| ---------------------------------------- | ----- | ------ | ----------- |
| View provider name                       | ✅    | ✅     | ✅          |
| View provider ID                         | ✅    | ✅ \*2 | ✅ \*2      |
| Edit provider name                       | ✅    | ❌     | ❌          |
| Delete provider \*3                      | ✅    | ❌     | ❌          |
| View list of channels linked to provider | ✅    | ❌     | ❌          |
| Create a channel under provider          | ✅    | ❌     | ❌          |
| Add or delete developer to/from provider | ✅    | ❌     | ❌          |
| View or edit provider role settings      | ✅    | ❌     | ❌          |

\*1 Only with access to the channel linked to the provider.

\*2 Cannot view the **Provider settings** screen, but provider ID will be included in the URL when developer selects a provider.

\*3 Cannot delete a provider with existing channels.

<!-- note start -->

**On provider roles and channel roles**

Note the following points on provider roles and channel roles:

- Even with the Admin role on the provider, without channel access, you can't see detailed information of the channel that is linked to the provider
- Even if you grant provider access to a developer, the developer won't automatically be given access to the channel(s) linked to the provider
- When deleting a developer from the provider, even if **Also delete the selected developer(s) from the channels that belong to this provider.** is checked, the developer won't be deleted from the channel(s) with the status "Pending"

<!-- note end -->

<!-- tip start -->

**What is the difference between &quot;Member&quot; and &quot;No role&quot; on the provider?**

Both "Member" and "No role" on the provider can only view the provider name.

If you grant the Member role to a developer on a provider, you can add the developer to a channel linked to the provider, simply by clicking **Import from provider** on the **Roles** tab of the channel.

**Import from provider** is only available to a developer account with the Admin role both in the channel and the provider.

![Import from provider](https://developers.line.biz/media/line-developers-console/managing-roles-en.png)

<!-- tip end -->

### Adding developers, editing roles, and deleting developers on provider 

Follow these steps to open the **Roles** tab.

1. Select provider from the [LINE Developers Console](https://developers.line.biz/console/) sidebar.
1. Click **Roles** tab.

   | Action | Steps |
   | --- | --- |
   | Add | Click **Invite by email**, register the email address, set the role of the developer, and then click **Send invitation**. The developer will receive an email with the title, "You have received an invitation to join a provider". If the developer accepts the invitation, the developer will be added to the provider. |
   | Edit | Click **Edit** and then select a role from the dropdown list. |
   | Delete | Select the checkbox next to a member's name and click **Delete selected**. |

## Channel roles 

A developer can be given the Admin, Member, or Tester role on a channel. The operations that these roles can perform for each channel type are as follows:

- [Common to all channel types](https://developers.line.biz/en/docs/line-developers-console/managing-roles/#roles-for-channel-common)
- [LINE Login channel](https://developers.line.biz/en/docs/line-developers-console/managing-roles/#roles-for-channel-line-login)
- [Messaging API channel](https://developers.line.biz/en/docs/line-developers-console/managing-roles/#roles-for-channel-messaging-api)
- [LINE MINI App channel](https://developers.line.biz/en/docs/line-developers-console/managing-roles/#roles-for-channel-line-mini-app)

### Common to all channel types 

#### **Basic settings** tab 

|  | Admin | Member | Tester | No role |
| --- | --- | --- | --- | --- |
| View **Channel ID** | ✅ | ✅ | ✅ | ❌ |
| View **Region to provide the service** \*1 | ✅ | ❌ | ❌ | ❌ |
| View or edit **Company or owner's country or region** \*1 | ✅ | ❌ | ❌ | ❌ |
| View **Channel icon** | ✅ | ✅ | ✅ | ❌ |
| Edit **Channel icon** | ✅ | ❌ | ❌ | ❌ |
| View **Channel name** | ✅ | ✅ | ✅ | ❌ |
| Edit **Channel name** | ✅ | ❌ | ❌ | ❌ |
| View **Channel description** | ✅ | ✅ | ❌ | ❌ |
| Edit **Channel description** | ✅ | ❌ | ❌ | ❌ |
| View or edit **Email address** | ✅ | ❌ | ❌ | ❌ |
| View **Privacy policy URL** | ✅ | ✅ | ❌ | ❌ |
| Edit **Privacy policy URL** | ✅ | ❌ | ❌ | ❌ |
| View **Terms of use URL** | ✅ | ✅ | ❌ | ❌ |
| Edit **Terms of use URL** | ✅ | ❌ | ❌ | ❌ |
| View **App types** | ✅ | ❌ | ❌ | ❌ |
| View **Permissions** | ✅ | ❌ | ❌ | ❌ |
| View **Channel secret** | ✅ | ❌ | ❌ | ❌ |
| View or edit **Assertion Signing Key** | ✅ | ❌ | ❌ | ❌ |
| View **Your user ID** \*2 | ✅ | ✅ | ✅ | ❌ |
| View or edit **Require two-factor authentication** \*3 | ✅ | ❌ | ❌ | ❌ |
| View or edit **Localization (multi-language support)** \*1 | ✅ | ❌ | ❌ | ❌ |
| View or edit **Linked LINE Official Account** \*1 | ✅ | ❌ | ❌ | ❌ |
| View or edit **Email address permission** \*1 | ✅ | ❌ | ❌ | ❌ |
| Perform **Delete this channel** \*4 | ✅ | ❌ | ❌ | ❌ |
| Perform **Leave channel** | ❌ | ✅ | ✅ | ❌ |

\*1 Only displayed in the LINE Login channel or the LINE MINI App channel.<br>\*2 Only displayed in the LINE Login channel or the Messaging API channel. In either role, **Your user ID** won't be displayed if your Business ID that isn't linked to a LINE account. For more information, see [Available features](https://developers.line.biz/en/docs/line-developers-console/login-account/#available-features).<br>\*3 Only displayed in the LINE MINI App channel.<br>\*4 You can't delete the Blockchain Service channel or the LINE MINI App channel.

#### **Roles** tab 

|                            | Admin | Member | Tester | No role |
| -------------------------- | ----- | ------ | ------ | ------- |
| View or edit **Roles** tab | ✅    | ❌     | ❌     | ❌      |

#### Test on a channel set to "Developing" 

| Admin | Member | Tester | No role |
| ----- | ------ | ------ | ------- |
| ✅    | ❌     | ✅     | ❌      |

Only the LINE Login channel, the LINE MINI App channel, and the Blockchain service channel have a status. For testing methods after you've granted Tester role to your developer account in the LINE Login channel, see [How to test with a LINE Login channel with the "Developing" status](https://developers.line.biz/en/docs/line-login/getting-started/#how-to-test-login-channel).

### LINE Login channel 

|                                 | Admin | Member | Tester | No role |
| ------------------------------- | ----- | ------ | ------ | ------- |
| View or edit **LINE Login** tab | ✅    | ❌     | ❌     | ❌      |
| View or edit **LIFF** tab       | ✅    | ❌     | ❌     | ❌      |

### Messaging API channel 

|                                    | Admin | Member | Tester | No role |
| ---------------------------------- | ----- | ------ | ------ | ------- |
| View or edit **Messaging API** tab | ✅    | ❌     | ❌     | ❌      |
| View **LIFF** tab                  | ✅    | ❌     | ❌     | ❌      |
| View or edit **Security** tab      | ✅    | ❌     | ❌     | ❌      |
| View **Webhook errors** tab \*1    | ✅    | ✅     | ❌     | ❌      |
| View **QR code** \*2               | ✅    | ✅     | ✅     | ❌      |

\*1 The **Webhook errors** tab is displayed only for channels where **Error statistics aggregation** is enabled on the **Messaging API** tab.

\*2 For developers with the Admin role, it appears under the **Messaging API** tab. For developers with the Member role or Tester role, it appears under the **Basic settings** tab.

### LINE MINI App channel 

|                                               | Admin | Tester | No role |
| --------------------------------------------- | ----- | ------ | ------- |
| View or edit **Web app settings** tab         | ✅    | ❌     | ❌      |
| View or edit **Review request** tab           | ✅    | ❌     | ❌      |
| View or edit **Business information** tab     | ✅    | ❌     | ❌      |
| View or edit **Contact information** tab      | ✅    | ❌     | ❌      |
| View or edit **Service message template** tab | ✅    | ❌     | ❌      |
| View **LIFF URL** \*                          | ✅    | ✅     | ❌      |

\* For developers with the Admin role, it appears under the **Web app settings** tab. For developers with the Tester role, it appears under the **Basic settings** tab. Note that developers with the Tester role can view only the LIFF URL for Developing.

### Adding developers, editing roles, and deleting developers on channel 

Open the **Roles** tab of the channel on the [LINE Developers Console](https://developers.line.biz/console/).

| Action | Steps |
| --- | --- |
| Add | <ul><li>Click **Invite by email**, register the email address, set the role of the developer, and then click **Send inivitaion**. The developer will receive an email with the title, "You have received an invitation to join a channel". If the developer accepts the invitation, the developer will be added to the channel.</li><li>Click **Import from provider** and select previously registered members under the same provider. The role is assigned to the developer immediately after you click **Import**. It isn't necessary for the developer to accept your invitation.</li></ul> |
| Edit | Click **Edit** and select a role from the dropdown list. |
| Delete | Select the checkbox next to a member's name and click **Delete selected**. |

<!-- note start -->

**Restrictions on adding a developer with an Admin role in Messaging API channels**

If developer A is registered as an Admin in 100 Messaging API channels, developer A cannot be added as an Admin to Messaging API channels created by developer B, but can be added as a Member or Tester.

This is because it conflicts with the "LINE Official Account Manager restrictions" described in [The number of channels that can be created](https://developers.line.biz/en/docs/line-developers-console/overview/#number-of-channels).

<!-- note end -->

#### "The email address entered when sending an invitation" will be used only for the invitation 

The email address you enter when clicking **Invite by email** will be used only for an invitation to the channel. The role specified at the time of the invitation will be granted to the developer account that logs in to the LINE Developers Console after clicking **Accept the invitation** in the email.

"The email address entered when sending an invitation" doesn't have to be the same as "the email address of the developer account to which a role is granted". Therefore, note that a role may be unintentionally granted to a developer account that is registered with an email address different from the one used for the invitation.

<!-- note start -->

**Note when you receive an invitation**

When receiving an invitation and granting a role to your developer account, take note of the following:

- If you haven't logged in to the LINE Developers Console, log in to the LINE Developers Console with a developer account that should be given the role
- If you've already logged in to the LINE Developers Console, make sure that the developer account you are logging in is the one which should be given the role

<!-- note end -->
