# Create a channel

To develop a LIFF app, you must first create a provider and a channel on the [LINE Developers Console](https://developers.line.biz/console/).

## Log in to the LINE Developers Console 

To create a provider and a channel, you must first log in to the LINE Developers Console. For more information on how to log in, see [Log in to the LINE Developers Console](https://developers.line.biz/en/docs/line-developers-console/login-account/).

## Creating a provider and channel 

Log in to the [LINE Developers Console](https://developers.line.biz/console/) and create a provider and a channel.

### 1. Create a provider 

If you already have a provider you want to use, go to [2. Create a channel](https://developers.line.biz/en/docs/liff/getting-started/#step-two-create-channel).

1. From the Console home, click the **Create a new provider** button.

   <!-- note start -->

   **If you can't find the Create a new provider button**

   If you've already created a provider, the **Create a new provider** button won't be displayed on the Console home. If you want to create another one, click the **Create** button in the **Providers** section on the Console home.

   ![Create button in the Providers section](https://developers.line.biz/media/liff/getting-started/providers-section-en.png)

   <!-- note end -->

1. Enter any **Provider name** on the **Create a new provider** screen, and click the **Create** button.

   A **provider** can be an individual, company, or organization that provides services through the LINE Platform. Enter your own name or company name as the provider name.

   ![Create a provider](https://developers.line.biz/media/liff/getting-started/create-provider-en.png)

### 2. Create a channel 

A **channel** is a communication path between the LINE Platform's functions and a provider's services. Channels must have a name, description, and icon image.

LIFF app can be added for these two channel types:

| Type | Description |
| --- | --- |
| [LINE Login](https://developers.line.biz/en/docs/line-login/) | If you want to create a LIFF app, or [try the LIFF starter app](https://developers.line.biz/en/docs/liff/trying-liff-app/) in the next step, or [build a LIFF app development environment with Create LIFF App](https://developers.line.biz/en/docs/liff/cli-tool-create-liff-app/), create a LINE Login channel. |
| [LINE MINI App](https://developers.line.biz/en/docs/line-mini-app/)  | If you want to create a LIFF app with [LINE MINI App](https://developers.line.biz/en/docs/line-mini-app/quickstart/), create a LINE MINI App channel. |

<!-- tip start -->

**We recommend creating a LIFF app as a LINE MINI App**

In the future, LIFF and the LINE MINI App will be integrated into a single brand. As a result of this integration, LIFF will be integrated into the LINE MINI App. For this reason, we recommend that you create a new LIFF app as a LINE MINI App. For more information, see the news from [February 12, 2025](https://developers.line.biz/en/news/2025/02/12/line-mini-app/).

<!-- tip end -->

In this section, we'll show you how to create a LINE Login channel, assuming that you want to [Try the LIFF starter app](https://developers.line.biz/en/docs/liff/trying-liff-app/) in the next step. Click the provider under which you want to add your LINE Login channel, and create your channel. If there is already a LINE Login channel you want to use, select it. For more information on how to create a channel, see [Creating a channel](https://developers.line.biz/en/docs/line-developers-console/overview/#creating-a-channel).

<!-- note start -->

**Channel name restrictions**

"LINE" or a similar string can't be included in the channel name.

<!-- note end -->

<!-- note start -->

**About channel's App types**

When developing a LIFF app, select **Web app** in App types.

<!-- note end -->

<!-- note start -->

**You can't add LIFF apps to channels other than LINE Login and LINE MINI App**

You can't add LIFF apps to these channel types:

- Messaging API
- Blockchain Service

Previously, LIFF apps could be added to Messaging API channels or Blockchain Service channels. However, new LIFF features aren't available for LIFF apps that have already been added to the Messaging API and Blockchain service channels. For more information, see these news articles.

- News on February 5, 2020, [Users can no longer add LIFF apps to Messaging API channels](https://developers.line.biz/en/news/2020/02/05/liff-channel-type/)
- News on July 20, 2021, [Users can no longer add LIFF apps to Blockchain Service channels](https://developers.line.biz/en/news/2021/07/20/liff-cannot-be-used-with-blockchain-service-channels/)

<!-- note end -->

#### Precautions for channel and provider linkage 

Once you create a channel, you can't move the channel to another provider later.

When developing a service that links a LINE Login channel with a Messaging API channel, create both channels within the same provider.

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

## Next steps 

You have now created a channel for your LIFF app. Next, do one of the following:

- [Try the LIFF starter app](https://developers.line.biz/en/docs/liff/trying-liff-app/)
- [Develop a LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/)
