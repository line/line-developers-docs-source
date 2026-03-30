# Membership card demo

<!-- tip start -->

**About this page**

This page contains articles migrated from the LINE API Use Case site (closed on March 31, 2026) to the LINE Developers site. Note that the content of the articles reflects the information available at the time of publication.

<!-- tip end -->

You can use the LINE MINI App to provide membership cards for your own services on LINE.

For example, companies that provide membership cards at offline stores, such as supermarkets, drugstores, and apparel stores, can also shift to online membership cards. It's possible to build a communication channel with users that can't be achieved with physical membership cards alone. Specifically, you can use the user ID obtained with the LINE MINI App to send push messages such as sales promotions.

\* You must obtain the user's consent to collect and utilize behavioral data linked to their LINE account.

<!-- table of contents -->

## View the demo 

You can view the demo by launching LINE on your smartphone and scanning this QR code.

![](https://developers.line.biz/media/line-mini-app/demo/membership-demo/membership-en-qr-img.webp)

<!-- note start -->

**Data that the demo app retrieves**

Before using the demo app, please note that the app will access your LINE account profile information, including your display name and user ID. Your user ID will be stored on the server, but this data will be deleted daily.

<!-- note end -->

## How to use the demo app 

\* The screen design may vary depending on your version.

| | | | |
| --- | --- | --- | --- |
|![](https://developers.line.biz/media/line-mini-app/demo/membership-demo/membership-en-image1.webp)|![](https://developers.line.biz/media/line-mini-app/demo/membership-demo/membership-en-image2.webp)|![](https://developers.line.biz/media/line-mini-app/demo/membership-demo/membership-en-image3.webp)|![](https://developers.line.biz/media/line-mini-app/demo/membership-demo/membership-en-image4.webp)|
| 1.Scan the QR code | 2.Authorize the required permissions | 3.Issue membership card | 4.Electronic receipt |

<!-- tip start -->

**Point**

1. No more need for physical membership cards
2. No physical cards to deliver, reducing physical contact
3. Membership cards can be issued immediately without entering any personal information
4. Messages can be delivered based on the activity history associated with the online membership card

<!-- tip end -->

## Benefits 

### End-user benefits 

#### 1. No more need for physical membership cards 

Online membership cards are not bulky in your wallet like physical membership cards. You can simply issue your membership card by scanning the QR code at the store. You can also present your online membership card by simply opening LINE.

#### 2. No physical cards to deliver, reducing physical contact 

The membership card can be displayed on the LINE app, eliminating the need to hand over a physical card. This can help reduce the chance of contact and therefore help prevent infections.

### Service provider benefits 

#### 1. Membership cards can be issued immediately without entering any personal information 

Generally, when issuing a membership card, personal information such as name and address is required to identify the individual. However, online membership cards using the LINE MINI App can be linked to the user's registered information on LINE. In other words, since there is no need to receive personal information from users, membership cards can be issued safely without incurring unnecessary costs to prevent personal information leakage.

#### 2. Messages can be delivered based on the activity history associated with the online membership card 

You can record behavioral history by linking it to the user ID. If the conditions are met, you can use these records to send out useful information to users via LINE as a sales promotion measure, such as increasing the rate of repeat business.

## System and sequence diagram of the demo application 

This figure shows how the demo app uses the LINE API.

\* The figure includes functions that are not implemented in the demo app.

**System diagram**

![](https://developers.line.biz/media/line-mini-app/demo/membership-demo/membership-system-diagram-en.webp)

- System diagram for using the other services
  - [System diagram using AWS](https://developers.line.biz/media/line-mini-app/demo/membership-demo/membership-system-diagram-aws-en.webp)
  - [System diagram using Azure](https://developers.line.biz/media/line-mini-app/demo/membership-demo/membership-system-diagram-azure-en.webp)

**Sequence diagram**

![](https://developers.line.biz/media/line-mini-app/demo/membership-demo/membership-sequence-diagram-en.webp)

- Sequence diagram for using the other services
  - [Sequence diagram using AWS](https://developers.line.biz/media/line-mini-app/demo/membership-demo/membership-sequence-diagram-aws_en.webp)
  - [Sequence diagram using Azure](https://developers.line.biz/media/line-mini-app/demo/membership-demo/membership-sequence-diagram-azure_en.webp)

## Related links 

- [Messaging API documentation](https://developers.line.biz/en/docs/messaging-api/)
- [LINE MINI App documentation](https://developers.line.biz/en/docs/line-mini-app/)
