# Message types

With the Messaging API, you can make your bot send these types of messages. To make a message interactive, you can specify an action on a message for users to trigger. For the specification of each message type, see [Message objects](https://developers.line.biz/en/reference/messaging-api/#message-objects) in the Messaging API reference.

- [Text message](https://developers.line.biz/en/docs/messaging-api/message-types/#text-messages)
- [Text message (v2)](https://developers.line.biz/en/docs/messaging-api/message-types/#text-messages-v2)
- [Sticker message](https://developers.line.biz/en/docs/messaging-api/message-types/#sticker-messages)
- [Image message](https://developers.line.biz/en/docs/messaging-api/message-types/#image-messages)
- [Video message](https://developers.line.biz/en/docs/messaging-api/message-types/#video-messages)
- [Audio message](https://developers.line.biz/en/docs/messaging-api/message-types/#audio-messages)
- [Location message](https://developers.line.biz/en/docs/messaging-api/message-types/#location-messages)
- [Coupon message](https://developers.line.biz/en/docs/messaging-api/message-types/#coupon-messages)
- [Imagemap message](https://developers.line.biz/en/docs/messaging-api/message-types/#imagemap-messages)
- [Template message](https://developers.line.biz/en/docs/messaging-api/message-types/#template-messages)
- [Flex Message](https://developers.line.biz/en/docs/messaging-api/message-types/#flex-messages)

## Text message 

Text messages contain text, including emojis. To send a text message, add the text in the [message object](https://developers.line.biz/en/reference/messaging-api/#message-objects) you send with the Messaging API. For more information, see [Text message](https://developers.line.biz/en/reference/messaging-api/#text-message) in the Messaging API reference.

![Text message](https://developers.line.biz/media/messaging-api/messages/text.png)

You can use LINE emojis and Unicode emojis in text messages. Check a list of [LINE emojis](https://developers.line.biz/en/docs/messaging-api/emoji-list/) you can send with the Messaging API.

![Emoji](https://developers.line.biz/media/messaging-api/messages/emoji.png)

<!-- tip start -->

**Text decoration and resizing**

To decorate or resize your text, use [Flex Messages](https://developers.line.biz/en/reference/messaging-api/#flex-message).

<!-- tip end -->

## Text message (v2) 

You can send text by using text messages (v2). Unlike [text messages](https://developers.line.biz/en/docs/messaging-api/message-types/#text-messages), you can substitute strings enclosed in `{` and `}` with mentions and emojis. For more information, see [Text message (v2)](https://developers.line.biz/en/reference/messaging-api/#text-message-v2) in the Messaging API reference.

![](https://developers.line.biz/media/messaging-api/messages/text-v2.png)

You can continue to use text messages that we've been providing up until now. However, we may only add new features to text messages (v2) from now on.

## Sticker message 

Stickers help you to make your bot more appealing and enjoyable to users. To send a sticker with the Messaging API, specify the sticker's package ID and sticker ID in the [message object](https://developers.line.biz/en/reference/messaging-api/#message-objects). Check a list of available [stickers](https://developers.line.biz/en/docs/messaging-api/sticker-list/) you can send. For more information, see the [Sticker message](https://developers.line.biz/en/reference/messaging-api/#sticker-message) in the Messaging API reference.

![Sticker message](https://developers.line.biz/media/messaging-api/messages/sticker.png)

## Image message 

Image messages deliver a single image file to users. When you send an image, specify two URLs in the [message object](https://developers.line.biz/en/reference/messaging-api/#message-objects). One is for the original image and one is for preview. The preview image is the image displayed in a chat, so specify an image smaller than the original image.

When the user taps the preview image, the full image is displayed as shown below. Make sure the URLs have the HTTPS (TLS 1.2 or later) protocol. For more information, see the [Image message](https://developers.line.biz/en/reference/messaging-api/#image-message) in the Messaging API reference.

![Image message](https://developers.line.biz/media/messaging-api/messages/image.png) ![Full image message](https://developers.line.biz/media/messaging-api/messages/image-full.png)

## Video message 

Video messages deliver a single video file to users. When you send a video message, specify two URLs in the [message object](https://developers.line.biz/en/reference/messaging-api/#message-objects), one for the video file and one for the preview.

LINE plays the video when the user taps the preview. Make sure the URLs have the HTTPS (TLS 1.2 or later) protocol. For more information, see the [Video message](https://developers.line.biz/en/reference/messaging-api/#video-message) in the Messaging API reference.

![Video message](https://developers.line.biz/media/messaging-api/messages/video.png)

## Audio message 

Audio messages deliver a single audio file to users. To send an audio file, specify a URL to the file and the duration in the [message object](https://developers.line.biz/en/reference/messaging-api/#message-objects).

Make sure the URL has the HTTPS (TLS 1.2 or later) protocol. For more information, see [Audio message](https://developers.line.biz/en/reference/messaging-api/#audio-message) in the Messaging API reference.

![Audio message](https://developers.line.biz/media/messaging-api/messages/audio.png)

## Location message 

Location messages deliver location information to users. Specify in the [message object](https://developers.line.biz/en/reference/messaging-api/#message-objects) the title, address, latitude coordinate, and longitude coordinate. For more information, see [Location message](https://developers.line.biz/en/reference/messaging-api/#location-message) in the Messaging API reference.

![Location message](https://developers.line.biz/media/messaging-api/messages/location-en.png)

## Coupon message 

Coupon messages deliver coupons to users by specifying a coupon ID.

![](https://developers.line.biz/media/messaging-api/coupon/several-coupons.jpg)

For more information, see [Coupon message](https://developers.line.biz/en/reference/messaging-api/#coupon-message) in the Messaging API reference.

## Imagemap message 

Imagemap messages are messages with an image that has multiple tappable areas. You can set a tappable area to open a webpage or send a message on the user's behalf. You can also set to play a video over the image and display a link text when the playback is finished. For more information, see [Imagemap message](https://developers.line.biz/en/reference/messaging-api/#imagemap-message) in the Messaging API reference.

![Imagemap message](https://developers.line.biz/media/messaging-api/messages/imagemap.png)

## Template message 

Template messages have predefined layouts that help you create richer experiences for your users. Use [actions](https://developers.line.biz/en/docs/messaging-api/actions/) to make users to interact with your bot. A tap is all that is required for users to trigger an action. This is much simpler than having to type in a message.

Available templates are:

- [Buttons](https://developers.line.biz/en/docs/messaging-api/message-types/#buttons-template)
- [Confirm](https://developers.line.biz/en/docs/messaging-api/message-types/#confirm-template)
- [Carousel](https://developers.line.biz/en/docs/messaging-api/message-types/#carousel-template)
- [Image carousel](https://developers.line.biz/en/docs/messaging-api/message-types/#image-carousel-template)

For more information about template messages, see [Template messages](https://developers.line.biz/en/reference/messaging-api/#template-messages) in the Messaging API reference. In addition, if you want to send messages with more flexible layouts, use [Flex Message](https://developers.line.biz/en/docs/messaging-api/message-types/#flex-messages).

### Buttons template 

Buttons templates contain slots for an image, title, text and [action](https://developers.line.biz/en/docs/messaging-api/actions/) buttons. In addition to buttons, you can set an action also on image, title, or text area. An action is triggered when a user taps the entity set with an action. For more information, see [Buttons template](https://developers.line.biz/en/reference/messaging-api/#buttons) in the Messaging API reference.

![Buttons template message](https://developers.line.biz/media/messaging-api/messages/buttons.png)

### Confirm template 

Confirm templates contain slots for text and two buttons. For more information, see [Confirm template](https://developers.line.biz/en/reference/messaging-api/#confirm) in the Messaging API reference.

![Confirm template message](https://developers.line.biz/media/messaging-api/messages/confirm.png)

### Carousel template 

Carousel templates contain multiple columns that users can cycle through. In addition to buttons, you can set an [action](https://developers.line.biz/en/docs/messaging-api/actions/) in each column object.

An action is triggered when a user taps anywhere in the image, title, or text area of a column object. For more information, see [Carousel template](https://developers.line.biz/en/reference/messaging-api/#carousel) in the Messaging API reference.

![Carousel template message](https://developers.line.biz/media/messaging-api/messages/carousel.png)

### Image carousel template 

Image carousel templates contain multiple images that users can cycle through. For more information, see [Image carousel template](https://developers.line.biz/en/reference/messaging-api/#image-carousel) in the Messaging API reference.

![Image carousel template message](https://developers.line.biz/media/messaging-api/messages/image-carousel.png)

## Flex Message 

Flex Messages are messages with a customizable layout. You can customize the layout within the boundary of the [CSS Flexible Box (CSS Flexbox)](https://www.w3.org/TR/css-flexbox-1/) specification. For more information, see [Send Flex Messages](https://developers.line.biz/en/docs/messaging-api/using-flex-messages/) and [Flex Message](https://developers.line.biz/en/reference/messaging-api/#flex-message) in the Messaging API reference.

![Flex Message examples](https://developers.line.biz/media/messaging-api/using-flex-messages/bubbleSamples-Update1.png)

## Common features 

This feature is applicable on all message types.

### Quick reply 

Quick reply buttons are available on all message types and displayed at the bottom of a chat. Users can tap one of the buttons to reply to your bot. For more information, see [Use quick replies](https://developers.line.biz/en/docs/messaging-api/using-quick-reply/), and [Quick reply](https://developers.line.biz/en/reference/messaging-api/#quick-reply) in the Messaging API reference.

![Quick reply sample](https://developers.line.biz/media/messaging-api/using-quick-reply/quickReplySample.png)

## Related pages 

Learn more about the Messaging API:

- [Sending messages](https://developers.line.biz/en/docs/messaging-api/sending-messages/)
- [Message objects](https://developers.line.biz/en/reference/messaging-api/#message-objects)
- [Actions](https://developers.line.biz/en/docs/messaging-api/actions/)
