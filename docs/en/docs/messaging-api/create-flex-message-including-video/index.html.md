# Create a Flex Message including a video

Using the video component of Flex Message, you can display a video in the hero [block](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#block). For more information on sending a Flex Message, see [Send Flex Messages](https://developers.line.biz/en/docs/messaging-api/using-flex-messages/).

<!-- table of contents -->

## Requirements to include videos in Flex Messages 

To include a [video](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#video) component in a Flex Message, you must:

- Specify the type of a hero [block](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#block) as `video`.
- Specify the size of the bubble to `kilo`, `mega` or `giga`.
- The bubble isn't the child element of a carousel.

## Video aspect ratio 

If your video is too wide or too tall, your video may not be displayed in full but cropped, depending on the device. To display your video properly, make sure the aspect ratio of all of these are the same:

- The aspect ratio of the video specified in the `url` property
- The aspect ratio specified in the `aspectRatio` property
- The aspect ratio of the preview image specified in the `previewUrl` property

![A video in a LINE chat room. A preview image with a 1:1 aspect ratio is displayed behind the video that has an aspect ratio of 16:9.](https://developers.line.biz/media/messaging-api/messages/image-overlapping-en.png)

## URI actions for videos 

Using the `action` property, you can specify a [URI action](https://developers.line.biz/en/reference/messaging-api/#uri-action). This action lets users open a URL in LINE's in-app browser or call a given number with the device's call app. The label for a URI action will be displayed in the following three places:

- [Chat room (after video playback)](https://developers.line.biz/en/docs/messaging-api/create-flex-message-including-video/#chat-room-screen)
- [Video player (during video playback)](https://developers.line.biz/en/docs/messaging-api/create-flex-message-including-video/#video-player-screen1)
- [Video player (after video playback)](https://developers.line.biz/en/docs/messaging-api/create-flex-message-including-video/#video-player-screen2)

![A chat room when a video finishes playing](https://developers.line.biz/media/messaging-api/create-flex-message-including-video/label-in-chat-room-en.png)
![A video player while a video is playing](https://developers.line.biz/media/messaging-api/create-flex-message-including-video/label-in-video-player1-en.png)
![A video player when a video finishes playing](https://developers.line.biz/media/messaging-api/create-flex-message-including-video/label-in-video-player2-en.png)

## Define a Flex Message with a video 

The most basic layout of a Flex Message with a video is having the video only, as shown below.

![Video component example](https://developers.line.biz/media/messaging-api/flex-message-elements/video-sample.png)

You have to use the `hero` block to insert a video. To make Flex Messages with video appear well on LINE versions that don't support video components, specify alternative content. Specify the hero block's `altContent` property with the content to show instead of the video. The JSON definition of this Flex Message example is as follows.

```json
{
  "type": "bubble",
  "size": "mega",
  "hero": {
    "type": "video",
    "url": "https://example.com/video.mp4",
    "previewUrl": "https://example.com/video_preview.jpg",
    "altContent": {
      "type": "image",
      "size": "full",
      "aspectRatio": "20:13",
      "aspectMode": "cover",
      "url": "https://example.com/image.jpg"
    },
    "aspectRatio": "20:13"
  }
}
```

Flex Messages that contain only a video looks like [video messages](https://developers.line.biz/en/reference/messaging-api/#video-message). With Flex Message, you can build a message with a video in more complex layout.

![Video component example](https://developers.line.biz/media/messaging-api/create-flex-message-including-video/video.png)

The JSON definition of this Flex Message example is as follows.

```json
{
  "type": "bubble",
  "size": "mega",
  "hero": {
    "type": "video",
    "url": "https://example.com/video.mp4",
    "previewUrl": "https://example.com/video_preview.png",
    "altContent": {
      "type": "image",
      "size": "full",
      "aspectRatio": "20:13",
      "aspectMode": "cover",
      "url": "https://example.com/image.png"
    },
    "action": {
      "type": "uri",
      "label": "More information",
      "uri": "http://example.com/"
    },
    "aspectRatio": "20:13"
  },
  "body": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "text",
        "text": "Brown Cafe",
        "weight": "bold",
        "size": "xl"
      },
      {
        "type": "box",
        "layout": "baseline",
        "margin": "md",
        "contents": [
          {
            "type": "icon",
            "size": "sm",
            "url": "https://example.com/star.png"
          },
          {
            "type": "icon",
            "size": "sm",
            "url": "https://example.com/star.png"
          },
          {
            "type": "icon",
            "size": "sm",
            "url": "https://example.com/star.png"
          },
          {
            "type": "icon",
            "size": "sm",
            "url": "https://example.com/star.png"
          },
          {
            "type": "icon",
            "size": "sm",
            "url": "https://example.com/gray_star.png"
          },
          {
            "type": "text",
            "text": "4.0",
            "size": "sm",
            "color": "#999999",
            "margin": "md",
            "flex": 0
          }
        ]
      },
      {
        "type": "box",
        "layout": "vertical",
        "margin": "lg",
        "spacing": "sm",
        "contents": [
          {
            "type": "box",
            "layout": "baseline",
            "spacing": "sm",
            "contents": [
              {
                "type": "text",
                "text": "Place",
                "color": "#aaaaaa",
                "size": "sm",
                "flex": 1
              },
              {
                "type": "text",
                "text": "1-3 Kioicho, Chiyoda-ku, Tokyo",
                "wrap": true,
                "color": "#666666",
                "size": "sm",
                "flex": 5
              }
            ]
          },
          {
            "type": "box",
            "layout": "baseline",
            "spacing": "sm",
            "contents": [
              {
                "type": "text",
                "text": "Time",
                "color": "#aaaaaa",
                "size": "sm",
                "flex": 1
              },
              {
                "type": "text",
                "text": "10:00 - 23:00",
                "wrap": true,
                "color": "#666666",
                "size": "sm",
                "flex": 5
              }
            ]
          }
        ]
      }
    ]
  },
  "footer": {
    "type": "box",
    "layout": "vertical",
    "spacing": "sm",
    "contents": [
      {
        "type": "button",
        "style": "link",
        "height": "sm",
        "action": {
          "type": "uri",
          "label": "CALL",
          "uri": "https://example.com"
        }
      },
      {
        "type": "button",
        "style": "link",
        "height": "sm",
        "action": {
          "type": "uri",
          "label": "WEBSITE",
          "uri": "https://example.com"
        }
      },
      {
        "type": "box",
        "layout": "vertical",
        "contents": [],
        "margin": "sm"
      }
    ],
    "flex": 0
  }
}
```

## Playback behavior 

You can play a video sent in a Flex Message from a [chat room](https://developers.line.biz/en/docs/messaging-api/create-flex-message-including-video/#chat-room) or with a [video player](https://developers.line.biz/en/docs/messaging-api/create-flex-message-including-video/#video-player).

<!-- note start -->

**If the video doesn't play properly**

Even if a message that contains a video is successfully sent, the video may not play properly on the user's device. For more information, see [Why can't I play a video that I sent as a message?](https://developers.line.biz/en/faq/#why-cant-i-play-a-video-i-sent) in the FAQ.

<!-- note end -->

### Playback in a chat room 

How the playback starts depends on the user's settings on LINE, at **Settings** > **Photos & videos** > **Auto-play videos**. Auto-play isn't supported on LINE for PC (macOS and Windows).

| Settings              | Video playback                                    |
| --------------------- | ------------------------------------------------- |
| **On mobile & Wi-Fi** | Video playback starts automatically               |
| **On Wi-Fi only**     | Video playback starts automatically only on Wi-Fi |
| **Never**             | Video playback never starts automatically         |

#### Screen when video playback finishes 

When video playback finishes, you can have up to two buttons displayed over the video. The first one is **Play** that launches a video player when a user taps the button and starts playback. For more information, see [Playback in a video player](https://developers.line.biz/en/docs/messaging-api/create-flex-message-including-video/#video-player).

The second button is **More information** that shows the label for a URI action you specify in the video component. You can change the text. If you don't specify a URI action for the video component, only **Play** is displayed. For more information, see [URI actions for videos](https://developers.line.biz/en/docs/messaging-api/create-flex-message-including-video/#uri-action).

![Screen when a video finishes playing](https://developers.line.biz/media/messaging-api/create-flex-message-including-video/auto-play-finished-en.png)

### Playback in a video player 

When the user taps a video in a chat room, a video player is launched and starts the video playback. The buttons you see [during playback](https://developers.line.biz/en/docs/messaging-api/create-flex-message-including-video/#video-player-screen1) and [after playback](https://developers.line.biz/en/docs/messaging-api/create-flex-message-including-video/#video-player-screen2) differ.

#### Screen during playback 

While a video is playing, you can have up to two buttons displayed at the top of the video player. The first one is **Done** that closes the video player when a user taps the button, and takes the user to the chat room. If the conditions for [auto playback](https://developers.line.biz/en/docs/messaging-api/create-flex-message-including-video/#chat-room) is met, the video playback continues in the chat room.

The second button is **More information** that shows the label for a URI action you specify in the video component. You can change the text. If you don't specify a URI action for the video component, only **Done** is displayed. For more information, see [URI actions for videos](https://developers.line.biz/en/docs/messaging-api/create-flex-message-including-video/#uri-action).

![Screen while a video is playing](https://developers.line.biz/media/messaging-api/create-flex-message-including-video/video-player-en.png)

#### Screen when playback is complete 

When video playback finishes, you can have up to two buttons displayed over the video. The first one is **Replay** that starts the playback again in the video player, when a user taps the button.

The second button is **More information** that shows the label for a URI action you specify in the video component. You can change the text. If you don't specify a URI action for the video component, only **Replay** is displayed. For more information, see [URI actions for videos](https://developers.line.biz/en/docs/messaging-api/create-flex-message-including-video/#uri-action).

![Screen when a video finishes playing](https://developers.line.biz/media/messaging-api/create-flex-message-including-video/video-player-finished-en.png)

## Display on version of LINE that doesn't support the video component 

If the version of LINE is lower than the version that supports the video component, the component specified as the value of the `altContent` property will be displayed. Use a [box](https://developers.line.biz/en/reference/messaging-api/#box) component or an [image](https://developers.line.biz/en/reference/messaging-api/#f-image) component for the `altContent` property.

## Videos in Flex Message Simulator 

You can't preview a video on [Flex Message Simulator](https://developers.line.biz/flex-simulator/). Instead, the alternative content you set is displayed in the preview area of Flex Message Simulator, like in [Display on version of LINE that doesn't support the video component](https://developers.line.biz/en/docs/messaging-api/create-flex-message-including-video/#alt-content).

To check the video in Flex Messages you composed with the Flex Message Simulator, send the message from the simulator to your LINE. You can send a test message from the simulator with the **Send...** menu at the top right section of the Flex Message Simulator.

![The Send... button on Flex Message Simulator](https://developers.line.biz/media/messaging-api/create-flex-message-including-video/send.png)

## Related pages 

- [Send Flex Messages](https://developers.line.biz/en/docs/messaging-api/using-flex-messages/)
- [Flex Message elements](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/)
- [Flex Message layout](https://developers.line.biz/en/docs/messaging-api/flex-message-layout/)
- [Flex Message](https://developers.line.biz/en/reference/messaging-api/#flex-message) (Messaging API reference)
- [Flex Message Simulator](https://developers.line.biz/flex-simulator/)
