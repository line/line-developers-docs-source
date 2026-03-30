# LINE Developers Console overview

LY Corporation provides the following features to third-party developers through the **LINE Platform**:

- A feature that authenticates users with the credentials of their LINE account (LINE Login)
- A feature that enables exchanging of LINE messages with users (Messaging API)

By creating a **channel** for using the features on a managing tool such as the **LINE Developers Console**, developers are given permission to use the features provided through the LINE Platform.

[LINE Developers Console Login](https://developers.line.biz/console/)

On the LINE Developers Console, you can manage **Developer**, **Provider**, and **Channel**.

![Overview](https://developers.line.biz/media/line-developers-console/overview-01.png)

## Developer 

On the LINE Developers site, someone who accesses the LINE Developers Console is referred to as a **Developer**.

When you register developers on providers and channels, you can control the information that each developer can view or edit on the LINE Developers Console.

For example, you can assign roles on a channel created by one developer to another developer. For details on assigning roles, see [Managing roles](https://developers.line.biz/en/docs/line-developers-console/managing-roles/).

## Provider 

On the LINE Developers site, an individual developer, company, or organization that provides service and acquires information of users to that end is referred to as a **Service provider** (**Service company** in LINE MINI App).

A service provider is registered as a **Provider** on the LINE Developers Console.

### Creating a provider 

1. From the Providers page on the Console home, click the **Create** button.

1. Enter your desired **Provider name** in the **Create a new provider** screen, and confirm by clicking **Create**.

<!-- tip start -->

**Tip**

- The provider name is displayed on the user consent screen. The user identifies the service provider based on the provider name. Therefore, provider names should not be temporary names (e.g. brand names used only in your organization, project names, etc.).

  ![Sample Provider](https://developers.line.biz/media/line-developers-console/consent-screen-sample-provider.png)

- When you are providing service as a company or organization, create a provider using the name of the company or organization.
- A channel used by the service provider must be created within the same provider.

<!-- tip end -->

### Deleting a provider 

Based on your provider role, you can delete your provider by clicking the **Delete** button at the bottom of the **Settings** tab. For information on provider roles, see [Provider roles](https://developers.line.biz/en/docs/line-developers-console/managing-roles/#roles-for-provider).

### The number of providers that can be created 

These restrictions apply to the number of providers that can be created.

| Restrictions when creating channels | Description |
| --- | --- |
| LINE Developers Console restrictions | Each developer can create up to 10 providers. The 11th provider can't be created. |

### Certified provider 

Once you become a certified provider, "Certified" is displayed as text on the channel consent screen that users review. You can also configure and publish a [Provider page](https://developers.line.biz/en/docs/partner-docs/provider-page/).

![](https://developers.line.biz/media/line-developers-console/consent-screen-certified-provider-en.png)

A certified provider indicates that LY Corporation has confirmed the authenticity of the service provider that created the provider. LY Corporation checks the following:

- Whether the organization is a real entity
- Whether the application was submitted by someone who belongs to the organization (or a representative)
- Whether the organization has an established privacy policy that has been disclosed

<!-- note start -->

**Required procedure to become a certified provider**

In principle, only corporate users are eligible for certification as a provider. If you would like to become a certified provider, a specific application is required. Contact your sales representative, or submit your inquiry to [our Sales partners](https://www.lycbiz.com/jp/partner/sales/).

<!-- note end -->

<!-- note start -->

**Note**

- The "Certified" text display does not indicate LY Corporation's support or warranty for the service provided by the service provider.
- To change a certified provider name, you must submit an application for review to LY Corporation.

<!-- note end -->

## Channel 

**Channel** enables service providers to use the features provided by the LINE Platform.

To develop a service that uses the LINE Platform, you must create a channel.

![Channel](https://developers.line.biz/media/messaging-api/getting-started/channel.png)

LINE Platform uses the credentials associated with the channel to confirm that the developer has permission to use the LINE Platform.

<!-- warning start -->

**Prohibitions set for protecting user data**

When using the LINE Platform for multiple services, don't link the LINE user data obtained from each individual service.

<!-- warning end -->

### Creating a channel 

Messaging API channels can be created by creating LINE Official Accounts. For more information, see [Get started with the Messaging API](https://developers.line.biz/en/docs/messaging-api/getting-started/) in the Messaging API documentation.

To create any other channel, follow these steps:

1. From the **Channels** tab on your provider page, choose the channel type you would like to create. These types of channels can be created on the LINE Developers Console:

   | Type | Description |
   | --- | --- |
   | [LINE Login](https://developers.line.biz/en/docs/line-login/) | You can use LINE Account credentials to authenticate users of the service you develop. |
   | Blockchain Service | You can provide a service that uses blockchain service. |
   | LINE MINI App  | You can provide a service through a [LINE MINI App](https://developers.line.biz/en/docs/line-mini-app/quickstart/) without developing a native app. |

1. Enter your channel name along with any required/optional information, and click **Create**.

   <!-- note start -->

   **Channel name restrictions**

   "LINE" or a similar string can't be included in the channel name.

   <!-- note end -->

   <!-- note start -->

   **Precautions for using a LINE Login channel**

   - Immediately after you create a LINE Login channel, the channel is set to **Developing** mode.
   - When the channel is set to **Developing**, only the developers who are registered as the channel Admin or Tester can use LINE Login.
   - To let the end users use LINE Login, set the LINE Login channel to **Published**.

   <!-- note end -->

#### Precautions for channel and provider linkage 

Once you create a channel, you can't move the channel to another provider later.

If you [use the Messaging API with your existing LINE Official Account](https://developers.line.biz/en/docs/messaging-api/getting-started/#using-oa-manager) created by the [LINE Official Account Manager](https://manager.line.biz/), you must create a new provider or select an existing provider to which the channel belongs during the initial setup. In this case as well, you can't move the channel to another provider later.

When developing a service that links a Messaging API channel with a LINE Login channel, create both channels within the same provider.

A LINE user who uses services provided by developers is given a different user ID for each provider. User IDs can't be used to identify the same user across channels under different providers.

![](https://developers.line.biz/media/line-developers-console/different-user-ids.png)

<!-- warning start -->

**Cases that require special attention when creating a channel**

For example, the following cases require special attention:

- Channels and providers are managed by individuals or companies.
- Create channels of unrelated services or companies under one provider.
- Channels are created under a provider managed by a service (company) that operates channel management tools, etc.

In such cases, problems may arise in the future due to the inability to move channels later between providers and the fact that a user is given different user IDs for different providers. After considering the risks involved, create a channel under the appropriate provider.

<!-- warning end -->

### Deleting a channel 

Based on your channel role, you can delete your channel by clicking the **Delete** button at the bottom of the **Basic Settings** tab.

For information on channel roles, see [Channel roles](https://developers.line.biz/en/docs/line-developers-console/managing-roles/#roles-for-channel).

### The number of channels that can be created 

These restrictions and specifications apply to the number of channels that can be created.

| Restrictions or specifications when creating channels | Description |
| --- | --- |
| LINE Developers Console restrictions | Developers can own a maximum of 100 channels with an Admin role under one provider, regardless of the channel type. |
| LINE Official Account Manager restrictions | Developers can own a maximum of 100 LINE Official Accounts for each account logged in to the LINE Official Account Manager. |

<!-- tip start -->

**About LINE Official Account Manager**

You can log in to [LINE Official Account Manager](https://manager.line.biz/) with the same account you are using in the LINE Developers Console to check and configure your LINE Official Account.

<!-- tip end -->
