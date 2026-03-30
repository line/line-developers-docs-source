# Get started with the Messaging API

To use the Messaging API, you must have a channel. To create a channel, create a [LINE Official Account](https://developers.line.biz/en/glossary/#line-official-account) and enable the use of Messaging API for your LINE Official Account.

This page describes how to create a Messaging API channel using the two steps described below:

1. [Create a LINE Official Account](https://developers.line.biz/en/docs/messaging-api/getting-started/#create-oa)
1. [Enable the Messaging API for your LINE Official Account](https://developers.line.biz/en/docs/messaging-api/getting-started/#using-oa-manager)

To enable the Messaging API for an existing LINE Official Account, see step 2.

<!-- tip start -->

**What is a channel?**

A **channel** is a communication path for providers to use the LINE Platform's features such as Messaging API and LINE Login in their services. To use the LINE Platform, you must have a channel. Then you can use functions of the Messaging API, with the channel's information such as access token.

![](https://developers.line.biz/media/messaging-api/getting-started/channel.png)

<!-- tip end -->

## 1. Create a LINE Official Account 

To use the Messaging API, you must first create a LINE Official Account. LINE Official Accounts can be created by following the steps below:

- [Step 1-1. Register for Business ID](https://developers.line.biz/en/docs/messaging-api/getting-started/#create-oa-business-id)
- [Step 1-2. Fill in the entry form](https://developers.line.biz/en/docs/messaging-api/getting-started/#create-oa-entry-form)
- [Step 1-3. Check your LINE Official Account](https://developers.line.biz/en/docs/messaging-api/getting-started/#create-oa-check)

### Step 1-1. Register for Business ID 

To create a LINE Official Account, you need to register for [Business ID](https://account.line.biz/signup?redirectUri=https://entry.line.biz/form/entry/unverified). You can register for Business ID using your LINE account or email address.

![](https://developers.line.biz/media/messaging-api/getting-started/sign-up-business-id-en.png)

### Step 1-2. Fill in the entry form 

Once you've registered for Business ID, the [entry form](https://entry.line.biz/form/entry/unverified) for a LINE Official Account will appear. Fill in the required information on this form. Once you've completed the form, your LINE Official Account will be created.

![](https://developers.line.biz/media/messaging-api/getting-started/oa-entry-form-en.png)

### Step 1-3. Check your LINE Official Account 

The above steps will create your LINE Official Account. You can check the created LINE Official Account on the [LINE Official Account Manager](https://manager.line.biz/).

![](https://developers.line.biz/media/messaging-api/getting-started/oa-manager-list-en.png)

Once you have confirmed that your LINE Official Account has been created, proceed to step 2.

## 2. Enable the Messaging API for your LINE Official Account 

By enabling the use of the Messaging API for the LINE Official Account you created, a Messaging API channel will be created. Follow the steps below to enable the use of the Messaging API from the [LINE Official Account Manager](https://manager.line.biz/):

- [Step 2-1. Enable the use of the Messaging API](https://developers.line.biz/en/docs/messaging-api/getting-started/#step-one-enable-use-of-messaging-api)
- [Step 2-2. Log in to the LINE Developers Console](https://developers.line.biz/en/docs/messaging-api/getting-started/#step-two-log-in-to-line-developers-console)
- [Step 2-3. Check that you have a channel](https://developers.line.biz/en/docs/messaging-api/getting-started/#step-three-confirm-channel)

### Step 2-1. Enable the use of the Messaging API 

When enabling the use of the Messaging API in the [LINE Official Account Manager](https://manager.line.biz/), a Messaging API channel is created. For more information, see [Messaging API](https://www.lycbiz.com/jp/manual/OfficialAccountManager/account-settings_messaging_api/) (only available in Japanese) in LINE for Business.

If your account used to login on the [LINE Official Account Manager](https://manager.line.biz/) is never used on the [LINE Developers Console](https://developers.line.biz/console/), a screen for registering developer information will appear. Enter your name and email to create a developer account.

![](https://developers.line.biz/media/messaging-api/getting-started/developer-registration-en.png)

Next, select a provider to manage your LINE Official Account. If you plan to integrate your LINE Official Account with existing channels like LINE Login channel, select the provider the channel to integrate belongs to.

<!-- note start -->

**Be careful when you select a provider**

Once you assign a provider to manage your LINE Official Account, you can't change or de-assign the provider.

<!-- note end -->

<!-- warning start -->

**Cases that require special attention when selecting a provider**

For example, the following cases require special attention:

- Channels and providers are managed by individuals or companies.
- Create channels of unrelated services or companies under one provider.
- Channels are created under a provider managed by a service (company) that operates channel management tools, etc.

In such cases, problems may arise in the future due to the inability to move channels later between providers and the fact that a user is given different user IDs for different providers. After considering the risks involved, select an appropriate provider.

<!-- warning end -->

### Step 2-2. Log in to the LINE Developers Console 

The created Messaging API channel can be configured in the LINE Developers Console. Log in to the [LINE Developers Console](https://developers.line.biz/console/) with the account you used to login for the [LINE Official Account Manager](https://manager.line.biz/).

![](https://developers.line.biz/media/messaging-api/getting-started/login-dialog.png)

### Step 2-3. Check that you have a channel 

Select the provider you selected in [Step 2-1](https://developers.line.biz/en/docs/messaging-api/getting-started/#step-one-enable-use-of-messaging-api). Make sure that a channel is created for the provider.

![](https://developers.line.biz/media/messaging-api/getting-started/console-home-en.png)

## [End-of-life] Create a channel in the LINE Developers Console 

It's no longer possible to create Messaging API channels directly from the LINE Developers Console. For more information, see the news from September 4, 2024, [As of September 4, 2024, it's no longer possible to create Messaging API channels directly from the LINE Developers Console](https://developers.line.biz/en/news/2024/09/04/no-longer-possible-to-create-messaging-api-channels-from-console/).

## Next steps 

Now that you have a channel, you're ready to use the Messaging API. In the following page, you will configure the channel to build a bot:

- [Building a bot](https://developers.line.biz/en/docs/messaging-api/building-bot/)
