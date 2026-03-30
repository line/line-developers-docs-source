# Mobile experience demo

<!-- tip start -->

**About this page**

This page contains articles migrated from the LINE API Use Case site (closed on March 31, 2026) to the LINE Developers site. Note that the content of the articles reflects the information available at the time of publication.

<!-- tip end -->

Personalized mobility experiences can be delivered by combining MaaS Tech Japan’s integrated mobility data platform, [TraISARE](https://traisare.maas.co.jp/) (only available in Japanese), with LINE.

From the end user perspective, this enables the purchase of excursion tickets, transit updates, and access to personalized recommendations and coupons based on usage history—all conveniently available on LINE, an app users already use daily.

For service providers, integrating and analyzing transportation, human flow, and behavioral data helps them propose optimized travel options that take usage patterns and crowd levels into account, encouraging users to shift their behavior.

By using LINE to lower the barrier to MaaS (Mobility as a Service) adoption and leveraging TraISARE’s various mobility data, we aim to enhance the user experience in ways tailored to each individual. This is our vision for personalized mobility.

<!-- table of contents -->

## View the demo 

- [Let’s experience a real mobility journey using a LINE MINI App on the demo site.](https://lineapiusecase.com/en/traisare/index.html)

## Benefits 

### End user benefits 

#### 1. No app downloads or complicated registration required 

By using a LINE MINI App, there is no need to download a dedicated app or enter personal information—start using MaaS right away.

#### 2. Receive useful information tailored to your situation while on the go 

Get relevant updates and special coupons for travel based on transport ticket usage.

#### 3. Travel comfortably without worrying about delays or crowding 

Receive real-time updates on public transit delays and congestion hotspots, so you can enjoy your outing without having to search for information yourself.

### Service provider benefits 

#### 1. Easily implement a PDCA cycle for MaaS initiatives 

By using LINE MINI Apps and the TraISARE data platform and dashboards, you can reduce the burden of providing a dedicated MaaS app and developing an infrastructure for data accumulation and effectiveness verification. This allows for easy implementation of a PDCA cycle.

#### 2. Promote behavioral change to avoid congestion and encourage service use 

Distribute coupons to help users avoid crowded areas and send information based on behavioral predictions to encourage changes in user actions. Also, analyze accumulated data to track user movement and dwell time after coupon delivery.

#### 3. Provide more convenient and comfortable travel through integrated transportation information 

TraISARE enables integration with external services for traffic and congestion data. Furthermore, providing timely information via LINE contributes to improved service quality and is expected to extend user dwell time in specific areas.

## System and sequence diagram of the demo application 

This figure shows how the demo app uses the LINE API.

\* The figure includes functions that are not implemented in the demo app.

**System diagram**

![](https://developers.line.biz/media/line-mini-app/demo/traisare-demo/traisare-system-diagram-en.png)

**Sequence diagram**

![](https://developers.line.biz/media/line-mini-app/demo/traisare-demo/traisare-sequence-diagram-en.png)

## Related links 

- [Messaging API documentation](https://developers.line.biz/en/docs/messaging-api/)
- [LINE MINI App documentation](https://developers.line.biz/en/docs/line-mini-app/)
