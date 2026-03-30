# Introducing LINE MINI App

LINE MINI App is a web application that runs on LINE. LINE MINI App enables users to enjoy services without installing a separate native app.

"LINE MINI App" is the official name.

LINE MINI App is a web browser, so most HTML5 specs can be used. For more information, see the [Specifications](https://developers.line.biz/en/docs/line-mini-app/discover/specifications/).

## Introduction 

Anyone who is a permitted customer in the [LINE MINI App Policy](https://terms2.line.me/LINE_MINI_App?lang=en) can develop LINE MINI Apps. See [Quick Start Guide](https://developers.line.biz/en/docs/line-mini-app/quickstart/) first.

To start developing the LINE MINI App channel, you need a [LINE Developers Console](https://developers.line.biz/console/) account. Many tasks, from LINE MINI App configuration to app submission for review, are carried out on the LINE Developers Console.

## Things you can do with LINE MINI App 

LINE MINI App provides these [built-in features](https://developers.line.biz/en/docs/line-mini-app/discover/builtin-features/).

- A feature for sharing LINE MINI App with other users
- A feature for requesting user access to services.

You can also add these [custom features](https://developers.line.biz/en/docs/line-mini-app/discover/custom-features/) on your LINE MINI App to further enhance user experience.

- Service Messages
- Using Payment Systems
- Custom action button

<!-- tip start -->

**Try out the LINE MINI App**

LY Corporation provides a LINE MINI App called [LINE MINI App Playground](https://miniapp.line.me/lineminiapp_playground) for developers. By opening the LINE MINI App Playground on a smartphone with the LINE app installed, you can actually try out some of the features of the LINE MINI App.

<!-- tip end -->

## Unverified MINI Apps and verified MINI Apps 

LINE MINI Apps are divided into unverified MINI Apps and verified MINI Apps depending on whether they've passed our verification review. Check the following sections for the differences between them:

### What are unverified MINI Apps 

Unverified MINI Apps are LINE MINI Apps that haven't yet passed our verification review. After you've created a LINE MINI App channel, the LINE MINI App will be an unverified MINI App until it passes the verification review.

Anyone can create an unverified MINI App, but as shown in the following section "[What are verified MINI Apps](https://developers.line.biz/en/docs/line-mini-app/discover/introduction/#verified-mini-app)", some features are restricted. To make your LINE MINI App a verified MINI App, [submit your LINE MINI App for review](https://developers.line.biz/en/docs/line-mini-app/submit/submission-guide/).

### What are verified MINI Apps 

If your LINE MINI App passes our verification review, it'll become a verified MINI App. Once it becomes a verified MINI App, it'll have a verified badge in the header, etc., as shown in the image below:

![](https://developers.line.biz/media/news/2024/line-mini-app-header-after.png)

In addition, you'll be able to use such as the following features:

- [Add a shortcut to your LINE MINI App to the home screen of the user's device](https://developers.line.biz/en/docs/line-mini-app/develop/add-to-home-screen/)
- [Custom Path](https://developers.line.biz/en/docs/line-mini-app/develop/custom-path/)
- [Channel consent simplification](https://developers.line.biz/en/docs/line-mini-app/develop/channel-consent-simplification/)

As described above, by making your LINE MINI App a verified MINI App, you can enhance the user experience in terms of reliability and convenience. For more information about the features that can be used for verified MINI Apps, see [Custom Features](https://developers.line.biz/en/docs/line-mini-app/discover/custom-features/).

## LINE MINI App Components 

LINE MINI App page consists of (A) Header (B) Body. For details, see [LINE MINI App Components](https://developers.line.biz/en/docs/line-mini-app/discover/ui-components/).

![LINE MINI App structure](https://developers.line.biz/media/line-mini-app/mini_concept.png)

## Ways in which users can access LINE MINI Apps 

Users can access LINE MINI Apps, not only within LINE but also from outside of LINE. There are several ways to access LINE MINI Apps within LINE.

### Access from outside of LINE 

If you have access to the [LINE MINI App Permanent Link](https://developers.line.biz/en/docs/line-mini-app/develop/permanent-links/), you can access the LINE MINI App from outside of LINE. You can share the permanent link of the LINE MINI App with users in these ways:

- By posting on websites, e-mails, text messages, etc.
- By creating a QR code for various media

In addition, by [adding a shortcut to the LINE MINI App to the home screen of the user's device](https://developers.line.biz/en/docs/line-mini-app/develop/add-to-home-screen/), the user can access the LINE MINI App directly from the home screen.

### LINE Official Account 

Users can also access LINE MINI Apps from the LINE Official Account. For example, a link to the LINE MINI App will be added to the rich message that you send to friends on the LINE Official Account and to the rich menu displayed on the talk screen. For details, see [Use LINE Official Account](https://developers.line.biz/en/docs/line-mini-app/service/line-mini-app-oa/).

![You can promote your LINE MINI App on the LINE Official Account](https://developers.line.biz/media/line-mini-app/mini_with_oa.png)

### Home Tab 

<!-- note start -->

**The feature to pin LINE MINI Apps to the Home tab in LINE has been discontinued**

For more information, see the news from January 9, 2024, [Users can now access recently used LINE MINI Apps from the LINE Home tab](https://developers.line.biz/en/news/2024/01/09/line-mini-app-history/).

<!-- note end -->

Users can access recently used LINE MINI Apps from **Services** on the **Home** tab of LINE. The **Services** section displays up to 8 recently used LINE MINI Apps in the order of their last use. This feature is only available for verified MINI Apps.

The Home tab display policy varies by region to provide the service.

![](https://developers.line.biz/media/line-mini-app/mini-access-home-tab-en.png)

### Searching on LINE 

You can also access LINE MINI Apps from the LINE search feature. This feature is only available for verified MINI Apps.

![Access from search](https://developers.line.biz/media/line-mini-app/mini_access_search.png)

### LINE Message 

Users can easily share LINE MINI Apps with their friends. The [built-in action button](https://developers.line.biz/en/docs/line-mini-app/discover/builtin-features/#action-button) is provided to enable users to easily share LINE MINI Apps among friends, but there's also the option of [implementing a custom action button](https://developers.line.biz/en/docs/line-mini-app/develop/share-messages/).

![Share message](https://developers.line.biz/media/line-mini-app/mini_access_share.png)

## Features available on LIFF apps but not on LINE MINI Apps 

| Item | Description |
| --- | --- |
| Hiding the action button (Module mode) | You can't hide the [action button](https://developers.line.biz/en/docs/line-mini-app/discover/builtin-features/#action-button) on the LINE MINI App. **Module Mode** can't be configured for LIFF apps that have been added to the LINE MINI App channel. |
| Adding multiple LIFF apps to the same channel | It isn't possible to add multiple web apps to the same channel in the LINE MINI App channel. |

<!-- tip start -->

**We recommend creating a LIFF app as a LINE MINI App**

In the future, LIFF and the LINE MINI App will be integrated into a single brand. As a result of this integration, LIFF will be integrated into the LINE MINI App. For this reason, we recommend that you create a new LIFF app as a LINE MINI App. For more information, see the news from [February 12, 2025](https://developers.line.biz/en/news/2025/02/12/line-mini-app/).

<!-- tip end -->
