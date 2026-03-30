# Store reservation demo

<!-- tip start -->

**About this page**

This page contains articles migrated from the LINE API Use Case site (closed on March 31, 2026) to the LINE Developers site. Note that the content of the articles reflects the information available at the time of publication.

<!-- tip end -->

You can use LINE MINI Apps to make reservations, such as at hair salons and restaurants.

To prevent users from forgetting their appointment, LINE MINI Apps can send reminders via LINE message when the appointment time is approaching. Also, if the conditions are met, the user ID obtained from the LINE MINI App can be used to send not only reservation notifications, but also push messages for sales promotions, etc.

\* You must obtain the user's consent to collect and utilize behavioral data linked to their LINE account.

<!-- table of contents -->

## View the demo 

You can view the demo by launching LINE on your smartphone and scanning this QR code.

![](https://developers.line.biz/media/line-mini-app/demo/reservation-demo/reserve-en-qr-img.webp)

<!-- note start -->

**Data that the demo app retrieves**

Before using the demo app, please note that the app will access your LINE account profile information, including your display name and user ID. Your user ID will be stored on the server, but this data will be deleted daily.

<!-- note end -->

## How to use 

\* The screen design may vary depending on your version.

| | | | |
| --- | --- | --- | --- |
|![](https://developers.line.biz/media/line-mini-app/demo/reservation-demo/reserve-en-image1.webp)|![](https://developers.line.biz/media/line-mini-app/demo/reservation-demo/reserve-en-image2.webp)|![](https://developers.line.biz/media/line-mini-app/demo/reservation-demo/reserve-en-image3.webp)|![](https://developers.line.biz/media/line-mini-app/demo/reservation-demo/reserve-en-image4.webp)|
| 1.Scan the QR code | 2.Authorize the required permissions | 3.Make a reservation by specifying the date and time | 4.Reminder notification |

<!-- tip start -->

**Point**

1. No need to download the app or register as a member
2. Help users remember reservations with reminder notifications
3. Deliver messages based on the operation and store visit history of the user's reservation app

<!-- tip end -->

## Benefits 

### End user benefits 

#### 1. No need to download the app or register as a member 

LINE MINI Apps require no download or installation on your smartphone and no personal information input, so you can make a reservation right away.

#### 2. Prevent users from forgetting with reminder notifications 

A service message will be sent to your chat room as a reminder notification before your visit. You can freely select the notification date. Even if you're busy with work or private life, you won't forget your reservation date.

### Service provider benefits 

#### 1. Help users remember reservations with reminder notifications 

To prevent users from forgetting to come to the store, users can be reminded by LINE message on the day of their visit, the day before their visit, or any other day they wish.

#### 2. Deliver messages based on the operation and store visit history of the user's reservation app 

You can record the operation and store visit history of the reservation app by linking them to the user ID. You can use these records to send out useful information to users via LINE as a sales promotion measure, such as increasing the rate of repeat visits.

## System and sequence diagram of the demo application 

This figure shows how the demo app uses the LINE API.

\* The figure includes functions that are not implemented in the demo app.

### Hair salon 

**System diagram**

![](https://developers.line.biz/media/line-mini-app/demo/reservation-demo/reserve-system-diagram-en.webp)

- System diagram for using the other services
  - [System diagram using AWS](https://developers.line.biz/media/line-mini-app/demo/reservation-demo/reserve-system-diagram-aws-en.webp)
  - [System diagram using Azure](https://developers.line.biz/media/line-mini-app/demo/reservation-demo/reserve-system-diagram-azure-en.webp)

**Sequence diagram**

![](https://developers.line.biz/media/line-mini-app/demo/reservation-demo/reserve-sequence-diagram-en.webp)

- Sequence diagram for using the other services
  - [Sequence diagram using AWS](https://developers.line.biz/media/line-mini-app/demo/reservation-demo/reserve-sequence-diagram-aws_en.webp)
  - [Sequence diagram using Azure](https://developers.line.biz/media/line-mini-app/demo/reservation-demo/reserve-sequence-diagram-azure_en.webp)

### Restaurant 

**System diagram**

![](https://developers.line.biz/media/line-mini-app/demo/reservation-demo/reserve-2-system-diagram-en.webp)

- System diagram for using the other services
  - [System diagram using AWS](https://developers.line.biz/media/line-mini-app/demo/reservation-demo/reserve-2-system-diagram-aws-en.webp)
  - [System diagram using Azure](https://developers.line.biz/media/line-mini-app/demo/reservation-demo/reserve-2-system-diagram-azure_en.webp)

**Sequence diagram**

![](https://developers.line.biz/media/line-mini-app/demo/reservation-demo/reserve-2-sequence-diagram-en.webp)

- Sequence diagram for using the other services
  - [Sequence diagram using AWS](https://developers.line.biz/media/line-mini-app/demo/reservation-demo/reserve-2-sequence-diagram-aws_en.webp)
  - [Sequence diagram using Azure](https://developers.line.biz/media/line-mini-app/demo/reservation-demo/reserve-2-sequence-diagram-azure_en.webp)

## Related links 

- [Messaging API documentation](https://developers.line.biz/en/docs/messaging-api/)
- [LINE MINI App documentation](https://developers.line.biz/en/docs/line-mini-app/)
