# The differences between native apps and LINE MINI Apps

<!-- tip start -->

**About this page**

This page contains articles migrated from the LINE API Use Case site (closed on March 31, 2026) to the LINE Developers site. Note that the content of the articles reflects the information available at the time of publication.

<!-- tip end -->

LINE MINI Apps are web applications that run in a [LIFF browser](https://developers.line.biz/en/glossary/#liff-browser) within the LINE app. Because the same user experiences and features that can be delivered through web applications can also be implemented with LINE MINI Apps, they have been adopted across a wide range of services. When companies consider providing services through digital channels, LINE MINI Apps and native apps are often compared as potential delivery options.

The purpose of LINE MINI Apps is to offer services such as mobile ordering, digital membership cards, and reservation management directly on LINE, enabling functionality within the LINE environment that is almost equivalent to that of native apps. Companies can expand the scope of their services by combining LINE Official Accounts and LINE MINI Apps, which are used to improve repeat usage through messaging between companies and users and coupon distribution, with other LINE APIs such as LINE Login and LINE notification messages.

In this article, we compare LINE MINI Apps and native apps and introduce the benefits, features, and costs of LINE MINI Apps.

![](https://developers.line.biz/media/basics/native-mini/en/native-mini-img-8.webp)

<!-- table of contents -->

## Experiences that can be realized with LINE MINI Apps 

We compare the differences between LINE MINI Apps and native apps across three factors: the barrier to use, notification delivery rate, and retention rate. The results of this comparison are shown below. Native apps have a higher barrier to use and lower notification delivery and retention rates, whereas LINE MINI Apps have a lower barrier to use and higher notification delivery and retention rates.

![](https://developers.line.biz/media/basics/native-mini/en/native-mini-img-1.webp)

### 1. Barrier to use 

For users who already use LINE, LINE MINI Apps and LINE Official Accounts can be accessed easily, without the need to download an additional app. In contrast, native apps present a much higher barrier to entry, starting with the need to download the app itself. For example, in in-store scenarios where users are required to download the app and complete membership registration on the spot, the level of difficulty is significantly higher compared with LINE MINI Apps.

![](https://developers.line.biz/media/basics/native-mini/en/native-mini-img-2.webp)

The Initial launch flow differs between LINE MINI Apps and native apps as follows:

For native apps:

For native apps, users access an app store via links on websites, QR codes displayed in various media, advertisement links, or links on social media, then download the native app and launch it. Before users install the app, companies need to create touchpoints and pathways to connect with customers.

For LINE MINI Apps:

The initial launch paths for LINE MINI Apps are similar to those of native apps, such as links on websites, QR codes displayed in various media, advertisement links, and links on social media. However, LINE MINI Apps can be launched directly without going through an app store. In addition, companies can place launch paths for LINE MINI Apps in the rich menus and rich messages of a LINE Official Account. By offering user-to-user sharing functionality using the share target picker available in LINE MINI Apps, users can also launch LINE MINI Apps directly from LINE chat rooms, which they use daily to communicate with family and friends.

If you’re a regular user of LINE Official Accounts, you might have wondered whether the pathways to launch rich menus and rich messages are only available to users who have already added the LINE Official Account as a friend. However, by using LINE notification messages—which allow messages to be delivered via phone numbers to users who have not yet added the LINE Official Account as a friend—users can launch LINE MINI Apps from the LINE Official Account’s rich menu after receiving a LINE notification message, and can also add the LINE Official Account as a friend as a result of receiving the notification.

### 2. Notification delivery rate 

The strengths of native apps lie in their high level of customization and support for rich media. However, notifications are more likely to be disabled by users, which can result in lower delivery rates. LINE MINI Apps require operation in accordance with notification restrictions and other guidelines, but their strengths lie in high notification delivery rates and strong integration with the LINE ecosystem.

Native app notifications are delivered using the smartphone’s push notification feature. They allow for advanced control over design and content and can guide users to specific functions or pages within the app. One disadvantage is that, while push notifications are highly effective for users who frequently use the app, delivery rates tend to decrease when usage frequency is low.

Notifications from LINE MINI Apps are sent through LINE Official Accounts. They can reliably deliver important information to users, such as reservation reminders, queue call notifications, and product completion notices. Because LINE is used on a daily basis, notifications are less likely to be missed, resulting in a higher notification delivery rate.

### 3. Retention 

The strengths of native apps lie in advanced personalization and offline functionality. However, when notifications are disabled, it becomes difficult to promote continued usage. On the other hand, while LINE MINI Apps offer less flexibility for advanced feature customization than native apps, their high notification delivery rates and low barrier to use make it easier to support retention efforts.

For native apps, when notifications are disabled, there is no way to encourage users to reuse the app, making it difficult to re-engage them. In some cases, users may even forget that the app exists. To keep users interested, it is necessary to continuously provide new features or content.

As described in "Functions available in native apps and LINE MINI Apps" below, while LINE MINI Apps cannot offer the same level of advanced functionality as native apps, they are effective in encouraging continued service usage. Users can smoothly add the service’s LINE Official Account as a friend on first use, enabling the service to continuously deliver messages that promote repeat usage. This, in turn, makes it possible to strengthen relationships with users and improve repeat usage.

## Features available in native apps and LINE MINI Apps 

LINE MINI Apps and native apps each have distinct characteristics in terms of convenience and functionality. LINE MINI Apps support features such as camera and microphone access and adding icons to the home screen, making them easy to access. However, there are limitations on GPS accuracy and the use of Bluetooth functions. Native apps can fully leverage all device features and deliver advanced services, but they require initial setup and greater user involvement. It is important to choose the most appropriate platform based on the characteristics of the service and the needs of users.

![](https://developers.line.biz/media/basics/native-mini/en/native-mini-img-3.webp)

### Camera / microphone 

Native apps can fully utilize the device's camera and microphone. This makes it possible to create high-quality media content; however, these features come with high app development and maintenance costs.

LINE MINI Apps can also provide features that use the device’s camera and microphone through WebRTC. However, compared with native apps, advanced camera and microphone functionality may be limited.

### GPS 

Native apps can utilize the device's GPS function to obtain accurate location information and provide services accordingly. However, using GPS requires user permission due to concerns about battery consumption and privacy.

LINE MINI Apps can obtain location information while the app is running. For example, in a takeout app, it is possible to offer features such as "find nearby stores". However, because location information cannot be continuously obtained in the background, applications such as running tracker apps must be delivered as native apps.

### Bluetooth 

Native apps can leverage Bluetooth functionality to enable short-range communication, data transfer between devices, and integration with IoT devices.

LINE MINI Apps cannot access the device’s Bluetooth functionality and therefore cannot search for or connect to Bluetooth devices. Scenarios such as connecting to IoT devices require native apps.

### Adding icons to home screen 

When a native app is installed, an icon is automatically added to the device's home screen.

LINE MINI Apps can also be added to the device’s home screen. While users need to be guided through the process of adding the icon to the home screen, this can be done without downloading an app, allowing LINE MINI Apps to be added in a way that is almost equivalent to native apps.

## Development costs of native apps and LINE MINI Apps 

There are clear differences in development costs between native apps and LINE MINI Apps. Native apps offer advanced functionality and a high level of customization. However, their disadvantages include high development costs and longer update cycles. In contrast, while LINE MINI Apps have certain limitations in advanced features and customization, they allow for faster development and updates at a lower cost.

![](https://developers.line.biz/media/basics/native-mini/en/native-mini-img-4.webp)

### Development costs 

Native apps can fully leverage device capabilities and support custom features and complex interactions. However, development is required separately for iOS and Android, which increases both workload and costs.

While LINE MINI Apps have some functional limitations, they are web applications and thus can be developed using a common program regardless of the operating system. As a result, effort required for implementation and testing is reduced, and development costs are often lower than those of native apps.

### Ease of updates 

Native apps require ongoing updates for adding new services and maintaining existing functionality. Updates to the underlying program must be handled continuously, which increases development costs.

For LINE MINI Apps, changes that do not involve configuration updates in the LINE Developers Console do not require re-review (for items requiring re-review, see [here](https://developers.line.biz/en/docs/line-mini-app/service/update-service/)). This makes it possible to roll out updates quickly in response to service usage trends and business conditions.

## FAQ 

### Q: Unlike native apps, you can't add an icon to the device’s home screen, right? 

A: By using the browser’s shortcut-adding feature, a shortcut icon can be added to the device’s home screen. As a result, frequently used services—such as membership cards or takeout ordering—can be accessed directly again from the shortcut icon without opening LINE.

\* The feature that allows the addition of a shortcut to a LINE MINI App on the home screen is available only for verified MINI Apps. For more information, see [Introducing LINE MINI App](https://developers.line.biz/en/docs/line-mini-app/discover/introduction/).

![](https://developers.line.biz/media/basics/native-mini/en/native-mini-img-5.webp)

### Q: If we provide services through LINE MINI Apps or a LINE Official Account, won’t notifications cost money? 

A: No. Messages sent from a LINE Official Account are charged based on the number of messages delivered, in accordance with the [LINE Official Account pricing plans](https://developers.line.biz/en/docs/messaging-api/pricing/). However, with LINE MINI Apps, you can use the service message feature to send the notifications required for service delivery reliably and at no cost.

\* The service message feature is available only for verified MINI Apps.

![](https://developers.line.biz/media/basics/native-mini/en/native-mini-img-6.webp)

### Q: LINE isn’t widely used by users outside of Japan, so LINE MINI Apps can’t be used for services that may be accessed by users outside of Japan, right? 

A: No. When non-LINE users in markets with low LINE usage—such as markets other than Japan, Thailand, and Taiwan—attempt to launch a LINE MINI App, a dedicated landing page is displayed, allowing the service to be provided through a web browser. As a result, international visitors to Japan who do not use LINE can access LINE MINI App services via a web browser without installing the LINE app.

### Q: Is it possible to change from a web application or a LIFF app to LINE MINI Apps? 

A: Web applications can be converted into LINE MINI Apps. For more information, see [Implementing web apps in operation as LINE MINI Apps](https://developers.line.biz/en/docs/line-mini-app/develop/web-to-mini-app/). However, LIFF apps created under a LINE Login channel cannot be migrated to a LINE MINI App channel to become either an unverified MINI App or a verified MINI App. Unverified MINI Apps can be published without undergoing a review process. When there is uncertainty about whether to create a LIFF app or a LINE MINI App, or when there is a possibility that the app may become a verified MINI App in the future, creating an unverified MINI App is recommended.

### Q: Is there any benefit to using LINE MINI Apps alongside an existing native app? 

A: Due to their low barrier to use, an increasing number of companies are adopting LINE MINI Apps and LINE Official Accounts to engage customers with low to medium loyalty, while continuing to operate native apps as the service channel for highly loyal customers. For example, in the case of a membership card service, offering the service through a native app requires users to install the app and complete membership registration, which can be a significant hurdle. With LINE, however, a card can be issued in just a few taps, making membership registration unnecessary. In other words, because services can be delivered after removing many of the typical barriers, LINE can be effectively used as an entry point for service experiences aimed at light customers.

![](https://developers.line.biz/media/basics/native-mini/en/native-mini-img-7.webp)
