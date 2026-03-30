# Measure impressions

In the Messaging API, the statistics include information about various user actions. This page focuses on impressions among them.

- [Aggregation environment](https://developers.line.biz/en/docs/messaging-api/measure-impressions/#environment-for-aggregation)
- [Endpoints for obtaining statistics](https://developers.line.biz/en/docs/messaging-api/measure-impressions/#endpoints-for-statistics)
- [What is an impression?](https://developers.line.biz/en/docs/messaging-api/measure-impressions/#what-is-impression)
- [Impression measurement logic](https://developers.line.biz/en/docs/messaging-api/measure-impressions/#impression-logic)
- [Usage precautions](https://developers.line.biz/en/docs/messaging-api/measure-impressions/#precautions)

## Aggregation environment 

Statistics, including impressions, are aggregated based on the LINE app for iOS and Android.

Messages viewed on the PC version or Chrome version of LINE aren't counted in the statistics.

## Endpoints for obtaining statistics 

You can use these endpoints to get statistics about how users interacted with messages you sent:

- [Get user interaction statistics](https://developers.line.biz/en/reference/messaging-api/#get-message-event)
- [Get statistics per unit](https://developers.line.biz/en/reference/messaging-api/#get-statistics-per-unit)

## What is an impression? 

An impression in the Messaging API refers to when a user enters a chat room and views a message sent from a LINE Official Account. Impressions are sometimes also referred to as message opens.

### Impression types 

There are two types of impressions: unique impressions and impressions. The [impression measurement logic](https://developers.line.biz/en/docs/messaging-api/measure-impressions/#impression-logic) described in this document applies to both types. However, note that the number of times they are measured differs.

The impressions that can be retrieved through the [endpoints for obtaining statistics](https://developers.line.biz/en/docs/messaging-api/measure-impressions/#endpoints-for-statistics) are as follows:

| Property | Impression type | Description |
| --- | --- | --- |
| `overview.uniqueImpression` \*1 | Unique impression | Number of users who opened the message. The number of people who displayed at least one bubble.<br>Each message is counted only once per user. |
| `messages[].uniqueImpression` \*2 | Unique impression | Number of users who displayed the bubble.<br>Each bubble is counted only once per user. |
| `messages[].impression` \*1 | Impression | Number of times the bubble was displayed.<br>If the conditions are met, each bubble may be counted multiple times per user. |

\*1 The property containing the impression value in the response of the [Get user interaction statistics](https://developers.line.biz/en/reference/messaging-api/#get-message-event) and [Get statistics per unit](https://developers.line.biz/en/reference/messaging-api/#get-statistics-per-unit) endpoints.

\*2 The property containing the impression value in the response of the [Get statistics per unit](https://developers.line.biz/en/reference/messaging-api/#get-statistics-per-unit) endpoint.

#### Message and bubble concept 

A [message](https://developers.line.biz/en/docs/messaging-api/sending-messages/) consists of one or more [message objects](https://developers.line.biz/en/reference/messaging-api/#message-objects). You can send up to five message objects in a single request.

In the Messaging API, a bubble refers to a single message object. Message objects include various types such as sticker message objects and image message objects. Whether they visually appear as a speech bubble or not doesn’t matter.

This illustration shows an example of a message composed of three bubbles. Although bubble 2 and 3 don't have the same speech bubble shape as the text message object in bubble 1, each is treated as bubbles for impression measurement.

![](https://developers.line.biz/media/messaging-api/measure-impressions/message-and-bubbles-en.png)

When this message is sent and the user opens the chat to view it, the single bubble that's displayed triggers the counting of `overview.uniqueImpression`. `messages[].uniqueImpression` and `messages[].impression` are counted separately for each bubble.

For more information, see [Get user interaction statistics](https://developers.line.biz/en/reference/messaging-api/#get-message-event) and [Get statistics per unit](https://developers.line.biz/en/reference/messaging-api/#get-statistics-per-unit) in the Messaging API reference.

### Actions that aren't counted as impressions 

Impressions are counted only when a user enters the chat room and views a message sent from a LINE Official Account.

However, if the user perform one of these actions that marks a message as read without entering the chat room, it won't be counted as an impression.

| OS | Operation |
| --- | --- |
| Android | <ul><li>Long-press the chat rooms you want to mark as read in the chat list and then select <b>Mark as read</b> from the menu that appears to mark them as read in bulk.</li><li>Select <b>Mark all as read</b> from the options menu at the top of the chat list to mark them all as read.</li></ul> |
| iOS | <ul><li>Swipe left on a chat in the chat list and select <b>Read</b> from the menu to mark it as read in bulk.</li><li>Tap the hamburger menu, open the chat list edit screen, select chats, and then tap <b>Read</b> to mark multiple chats as read at once.</li></ul> |

## Impression measurement logic 

This section explains the specific measurement logic for impressions.

- [Display message bubbles at 100%](https://developers.line.biz/en/docs/messaging-api/measure-impressions/#must-show-all-messages)
- [Duplicate counting doesn't occur when scrolling](https://developers.line.biz/en/docs/messaging-api/measure-impressions/#no-duplicate-by-scrolling)
- [About carousel messages](https://developers.line.biz/en/docs/messaging-api/measure-impressions/#carousel-message)

### Display message bubbles at 100% 

Impressions are counted when a user enters a chat room and views a message sent from a LINE Official Account. At that time, the message bubble must be 100% visible on the screen.

These are examples of bubbles that are 100% visible and those that aren't.

| Description | Image |
| --- | --- |
| This area's bubble is 100% visible. | ![green](https://developers.line.biz/media/messaging-api/measure-impressions/100per-area.png) |
| This area's bubble isn't 100% visible. | ![red](https://developers.line.biz/media/messaging-api/measure-impressions/not-100per-area.png) |

| Display | Description | Image |
| --- | --- | --- |
| ✅️ 100% visible | The bubble displayed in the green area is fully visible, so it's counted as an impression. | ![The entire bubble is displayed](https://developers.line.biz/media/messaging-api/measure-impressions/impression-100per.png) |
| ❌️ Not 100% visible | The bubble displayed in the red area overlaps with the rich menu and isn't fully visible, so it isn't counted as an impression. | ![The entire bubble isn't displayed because it overlaps with the rich menu](https://developers.line.biz/media/messaging-api/measure-impressions/impression-not-100per-richmenu.png) |
| ❌️ Not 100% visible | The bubble in the red area overlaps with the [service menu bar](https://www.lycbiz.com/jp/manual/OfficialAccountManager/servicemenubar/) and isn't fully visible, so it isn't counted as an impression. | ![The entire bubble isn't displayed because it overlaps with the service menu bar](https://developers.line.biz/media/messaging-api/measure-impressions/impression-not-100per-service-menu-ber.png) |
| ❌️ Not 100% visible | The bubble in the red area is too tall to fit within the chat window, so it isn't fully visible and therefore not counted as an impression. | ![The message is too tall to fit entirely within the bubble](https://developers.line.biz/media/messaging-api/measure-impressions/impression-not-100per-too-long.png) |

<!-- tip start -->

**Impression counting when the entire bubble can't be displayed at once**

"100% displayed" means that both the top and bottom edges of the target bubble are visible within the user's window at some point before leaving the chat room.

Even if the entire bubble can't be displayed at once, as in the previous examples, scrolling or closing the rich menu so that both the top and bottom edges of the hidden bubble become visible will count as 100% displayed and the impression will be recorded.

<!-- tip end -->

### Duplicate counting doesn't occur when scrolling 

Once an impression is recorded, it isn't counted again while the user remains in the same chat room, even if they scroll back to display the same message multiple times.

However, if the user returns to the chat list and then re-enters the chat room to view 100% of the messages, it's counted as a new impression.

A unique impression is measured only once per user, so it doesn't increase even if the user re-enters the chat room.

### About carousel messages 

If you send a message that uses a [carousel](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#carousel) using Flex Message, impressions aren't counted multiple times even if a user scrolls horizontally to display the carousel.

For messages using a carousel, the impression is counted once when all edges (top, bottom, left, and right) of the bubble are displayed.

![](https://developers.line.biz/media/messaging-api/measure-impressions/carousel-100per-scroll.png)

## Usage precautions 

Note these points when measuring impressions:

- [Make sure that it's within the measurement period](https://developers.line.biz/en/docs/messaging-api/measure-impressions/#ensure-measurement-period)
- [Avoid making the message too tall](https://developers.line.biz/en/docs/messaging-api/measure-impressions/#avoid-too-tall-messages)
- [Avoid interfering with the rich menus or the service menu bar](https://developers.line.biz/en/docs/messaging-api/measure-impressions/#avoid-interference)

### Make sure that it's within the measurement period 

Statistics, including impressions, are only collected for 14 days (1,209,600 seconds) from the time the message was sent. It isn't updated after that. When using the [Get statistics per unit](https://developers.line.biz/en/reference/messaging-api/#get-statistics-per-unit) endpoint, you can specify the aggregation period, so make sure that the specified date is within the measurement period.

### Avoid making the message too tall 

If you send a message that is extremely tall, the entire message may not be displayed in the chat room, and impressions may not be counted as expected. Adjust the message to an appropriate length.

### Avoid interfering with the rich menus or the service menu bar 

If your LINE Official Account uses a [rich menu](https://developers.line.biz/en/docs/messaging-api/rich-menus-overview/), bubbles may overlap with it in the chat room and prevent the full bubble from being visible. As a result, impressions may not be counted as expected.

Also, if you're using the [service menu bar](https://www.lycbiz.com/jp/manual/OfficialAccountManager/servicemenubar/) displayed at the top of the chat room, similar issues may occur.

Adjust the length of messages and the size of rich menus to prevent these issues.
