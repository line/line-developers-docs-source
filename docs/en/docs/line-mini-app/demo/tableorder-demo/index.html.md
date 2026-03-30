# Table order demo

<!-- tip start -->

**About this page**

This page contains articles migrated from the LINE API Use Case site (closed on March 31, 2026) to the LINE Developers site. Note that the content of the articles reflects the information available at the time of publication.

<!-- tip end -->

Users can complete everything from pre-ordering to payment (including delivery) for products via the LINE MINI App, both inside and outside the store.

By linking the LINE MINI App with a LINE Official Account, it becomes possible to seamlessly acquire friends for the LINE Official Account while users are engaging with the service. Furthermore, by utilizing user data obtained through the LINE MINI App, more efficient promotional activities can be achieved. (\* Only when provided within the same provider.)

\* You must obtain the user's consent to collect and utilize behavioral data linked to their LINE account.

<!-- table of contents -->

## View the demo 

You can view the demo by launching LINE on your smartphone and scanning this QR code.

![](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-en-qr-img.webp)

<!-- note start -->

**Data that the demo app retrieves**

Please note that the demo app will access your LINE account profile information, including your display name and user ID. Your user ID will be stored on the server, but this data will be deleted daily. Payment will be made from the LINE Pay balance prepared by this demo app. No actual payment method is selected or payment is made.

Please use this service with the above points in mind.

<!-- note end -->

## How to use 

\* The screen design may vary depending on your version.

| | | | |
| --- | --- | --- | --- |
|![](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-en-image1.webp)|![](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-en-image2.webp)|![](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-en-image3.webp)|![](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-en-image4.webp)|
| 1.Scan the QR code | 2.Authorize the required permissions | 3.Select a product and place an order | 4.Checkout |

<!-- tip start -->

**Point**

1. Complete everything from ordering to checkout with a smartphone, which reduces contact with store clerks and helps prevent infections
2. Multiple people can order and pay separately
3. Reduce labor, labor costs, and terminal leasing costs by introducing an app
4. Communicate with end users online
5. Deliver messages based on the user's operation and store visit history with the table order app

<!-- tip end -->

## Benefits 

### End user benefits 

#### 1. Complete everything from ordering to checkout with a smartphone, which reduces contact with store clerks and helps prevent infections 

You can launch a LINE MINI App by scanning the QR code on the table. If you place an order and complete checkout at your table using the LINE MINI App, you won’t need face-to-face contact, which is helpful for infection control.

#### 2. Multiple people can order and pay separately 

Table order apps are also useful when you come to a restaurant with a large group. Stores are often equipped with one terminal per table, but in this case, only one person can operate it at a time. With the table order app, each person can order at the same time with their own smartphone. Also, each person can pay the bill separately, saving you the trouble of splitting the bill.

### Service provider benefits 

#### 1. Reduce labor, labor costs, and terminal leasing costs by introducing an app 

Reduce the burden of handling orders and payments on employees and improve work efficiency. It can also help prevent infectious diseases by reducing the need for face-to-face contact. Also, if you want to introduce table ordering using a dedicated tablet, you need to pay for the lease of the ordering terminal. With the table order app, the user's smartphone is used instead of the order terminal, so there is no need to pay for the order terminal lease.

#### 2. You can also provide customer support by handling user inquiries 

You can prompt users to add the LINE Official Account as a friend on the first authentication screen. You can send push messages, such as sales promotions, and accept inquiries at a later date to users who add the LINE Official Account as a friend.

#### 3. Deliver messages based on the user's operation and store visit history with the table order app 

You can record the operation and store visit history of the table order app by linking it to the user ID. If the conditions are met, you can send useful information to users via LINE based on these records as a sales promotion measure, such as increasing the rate of repeat visits.

\* You must obtain the user's consent to collect and utilize behavioral data linked to their LINE account.

## System and sequence diagram of the demo application 

This figure shows how the demo app uses the LINE API.

\* The figure includes functions that are not implemented in the demo app.

**System diagram**

![](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-system-diagram-en.webp)

- System diagram for using the other services
  - [System diagram using AWS](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-system-diagram-aws-en.webp)
  - [System diagram using Azure](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-system-diagram-azure-en.webp)

**Sequence diagram**

![](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-sequence-diagram-en.webp)

- Sequence diagram for using the other services
  - [Sequence diagram using AWS](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-sequence-diagram-aws-en.webp)
  - [Sequence diagram using Azure](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-sequence-diagram-azure-en.webp)

## Related links 

- [Messaging API documentation](https://developers.line.biz/en/docs/messaging-api/)
- [LINE MINI App documentation](https://developers.line.biz/en/docs/line-mini-app/)
