# Purchase experience demo

<!-- tip start -->

**About this page**

This page contains articles migrated from the LINE API Use Case site (closed on March 31, 2026) to the LINE Developers site. Note that the content of the articles reflects the information available at the time of publication.

<!-- tip end -->

Leverage smartphones, the devices closest to the end user, to drive DX (Digital Transformation) for retailers. In particular, providing a customer experience that combines online and offline (OMO: Online Merges with Offline) is expected to become the new retail standard. In the past, the customer experience was mainly limited to the in-store experience, but now, it won't be limited to just in-store, but can be highly designed as a seamless customer experience from before to after the in-store experience, providing significant benefits to the end user.

By using LINE MINI Apps, you can complete all of the following value provisions with one LINE. User behavior data acquired with LINE Official Accounts and LINE MINI Apps can be stored in CRMs prepared by service providers to realize the finest and seamless customer experience customized for each end user.

- Provide special deals before visiting the store using LINE Ads, LINE Official Accounts, LINE Flyers, and a unique reservation system
- Improve the purchasing experience through smartphone checkout, digital membership cards, and functions for checking purchase history (receipts)
- Post-purchase communication using the LINE Official Account

Furthermore, by incorporating [GS1 standard 2D symbols](https://www.gs1jp.org/standard/industry/2d-in-retail/) (only available in Japanese) into smartphone registers, you can create new shopping experiences and achieve store DX.

<!-- table of contents -->

## OMO concept powered by LINE 

In the new digital-era purchasing experience (OMO) powered by LINE, a consistent journey is delivered from pre-visit to post-purchase. Prior to visiting the store, information is provided through LINE Ads, LINE Official Accounts, and LINE Flyers, while in-store promotions are conducted using LINE POP Media and digital signage. At the time of purchase, procedures are simplified through smartphone self-checkout, LINE-based campaign entries, and e-commerce sites, followed by post-purchase engagement via LINE Official Accounts. This creates a seamless purchasing experience that integrates online and offline touchpoints.

![](https://developers.line.biz/media/line-mini-app/demo/smartretail-demo/smartretail-image-data-en.webp)

## View the smartphone register demo 

- [Let’s try experiencing an actual purchasing journey using a LINE MINI App through the demo site.](https://lineapiusecase.com/en/omo/index.html)

## Benefits 

### End user benefits 

#### 1. No need to download the app or deal with a complicated enrollment process 

There's no need to go through a complicated enrollment process to use the services provided by the retailer. You can immediately receive a superior customer experience.

#### 2. Complete everything from getting store deals to making payments on LINE 

You can use the LINE flyer to get information about special deals before you visit the store. You can also complete your payment on LINE, removing the need to stand in line when the cash register is crowded. This can help prevent infections and greatly reduce shopping time.

#### 3. Seamless access to all services, including membership cards 

You can issue a digital membership card and receive a digital purchase certificate (receipt) on LINE. You can also obtain and use member benefits and points on LINE. You can even use LINE as a self-checkout system to easily check the purchase history, freeing end users from complicated membership card and receipt management.

### Service provider benefits 

#### 1. No complicated procedures are required and people can easily start using the service 

Not only can users start using the system just by reading the QR code, but there's also no need for them to enter their name and address if they don't want to. Since the hurdle to start using the service is lowered, it's highly likely that users will adopt the system.

#### 2. Communicate with end users offline and online 

For example, you can send campaign information and distribute coupons tailored to each end user through your LINE Official Account. In addition, since the LINE Official Account can send notifications to end users in real time, you can attract customers to your stores according to the sales status of your products.

#### 3. It can reduce congestion in front of the cash register, prevent infections, and save money 

Since end users can make payments using their smartphones, there's no need to introduce self-checkout systems and the number of cashiers can be reduced, saving money. Also, by reducing the number of people waiting at the cash register, the system can help prevent infections.

## System and sequence diagram of the demo application 

This figure shows how the demo app uses the LINE API.

\* The figure includes functions that are not implemented in the demo app.

**System diagram**

![](https://developers.line.biz/media/line-mini-app/demo/smartretail-demo/smartretail-system-diagram-en.webp)

- System diagram for using the other services
  - [System diagram using AWS](https://developers.line.biz/media/line-mini-app/demo/smartretail-demo/smartretail-system-diagram-aws-en.webp)
  - [System diagram using Azure](https://developers.line.biz/media/line-mini-app/demo/smartretail-demo/smartretail-system-diagram-azure-en.webp)

**Sequence diagram**

![](https://developers.line.biz/media/line-mini-app/demo/smartretail-demo/smartretail-sequence-diagram-en.webp)

- Sequence diagram for using the other services
  - [Sequence diagram using AWS](https://developers.line.biz/media/line-mini-app/demo/smartretail-demo/smartretail-sequence-diagram-aws_en.webp)
  - [Sequence diagram using Azure](https://developers.line.biz/media/line-mini-app/demo/smartretail-demo/smartretail-sequence-diagram-azure-en.webp)

## Related links 

- [Messaging API documentation](https://developers.line.biz/en/docs/messaging-api/)
- [LINE MINI App documentation](https://developers.line.biz/en/docs/line-mini-app/)
