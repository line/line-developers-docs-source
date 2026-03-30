# Actions

You can set different types of actions to be triggered when a user taps a control in a message. Available actions depend on the message type. For more information, see [Message objects](https://developers.line.biz/en/reference/messaging-api/#message-objects) in the Messaging API reference.

Available actions are:

- [Postback action](https://developers.line.biz/en/docs/messaging-api/actions/#postback-action)
- [Message action](https://developers.line.biz/en/docs/messaging-api/actions/#message-action)
- [URI action](https://developers.line.biz/en/docs/messaging-api/actions/#uri-action)
- [Datetime picker action](https://developers.line.biz/en/docs/messaging-api/actions/#datetime-picker-action)
- [Camera action](https://developers.line.biz/en/docs/messaging-api/actions/#camera-action)
- [Camera roll action](https://developers.line.biz/en/docs/messaging-api/actions/#camera-roll-action)
- [Location action](https://developers.line.biz/en/docs/messaging-api/actions/#location-action)
- [Rich menu switch action](https://developers.line.biz/en/docs/messaging-api/actions/#richmenu-switch-action)
- [Clipboard action](https://developers.line.biz/en/docs/messaging-api/actions/#clipboard-action)

## Postback action 

The postback action sends your server a [postback event](https://developers.line.biz/en/reference/messaging-api/#postback-event) with the text that you specified in the action. You can set to have the text displayed as a message from the user.

You can also specify how to display such as rich menu based on user action. The following display methods can be specified:

- Close rich menu
- Open rich menu
- Open keyboard
- Open voice message input mode

Specifying how to display based on user action is available on LINE version `12.6.0` or later for iOS or Android. For more information, see [Postback action](https://developers.line.biz/en/reference/messaging-api/#postback-action) in the Messaging API reference.

## Message action 

The message action returns you a text as a user's message. For more information, see [Message action](https://developers.line.biz/en/reference/messaging-api/#message-action) in the Messaging API reference.

## URI action 

The URI action opens a URL in LINE's in-app browser. You can also use the [LINE URL scheme](https://developers.line.biz/en/docs/messaging-api/using-line-url-scheme/) in the URI action to launch a call app with a given number or open the screen to share any LINE Official Account.

![URI action](https://developers.line.biz/media/messaging-api/actions/quick-reply-uri-action-en.png)

This is a request body set with URI actions for the quick reply buttons shown in the example above. For more information, see [URI action](https://developers.line.biz/en/reference/messaging-api/#uri-action) in the Messaging API reference.

```json
{
  "messages": [
    {
      "type": "text",
      "text": "Have you decided on your order?",
      "quickReply": {
        "items": [
          {
            "type": "action",
            "action": {
              "type": "uri",
              "label": "Menu",
              "uri": "https://example.com/menu"
            }
          },
          {
            "type": "action",
            "action": {
              "type": "uri",
              "label": "Phone order",
              "uri": "tel:09001234567"
            }
          },
          {
            "type": "action",
            "action": {
              "type": "uri",
              "label": "Recommend to friend",
              "uri": "https://line.me/R/nv/recommendOA/%40linedevelopers"
            }
          }
        ]
      }
    }
  ]
}
```

## Datetime picker action 

The datetime picker action prompts users to choose a date, time, or date and time from a picker. When the user selects a date and time, you'll get the date and time information in the [postback event](https://developers.line.biz/en/reference/messaging-api/#postback-event) via a webhook. For more information, see [Datetime picker action](https://developers.line.biz/en/reference/messaging-api/#datetime-picker-action) in the Messaging API reference.

![Datetime picker action](https://developers.line.biz/media/messaging-api/actions/datetime-picker.png)

## Camera action 

The camera action opens a camera screen in LINE. You can set this action only on quick reply buttons. For more information, see [Camera action](https://developers.line.biz/en/reference/messaging-api/#camera-action) in the Messaging API reference.

## Camera roll action 

The camera roll action opens the camera roll screen in LINE. You can set this action only on quick reply buttons. For more information, see [Camera roll action](https://developers.line.biz/en/reference/messaging-api/#camera-roll-action) in the Messaging API reference.

## Location action 

The location action opens the location screen in LINE. You can set this action only on quick reply buttons. For more information, see [Location action](https://developers.line.biz/en/reference/messaging-api/#location-action) in the Messaging API reference.

## Rich menu switch action 

The rich menu switch action makes rich menus switchable. You can set this action only on rich menus. For more information, see [Rich menu switch action](https://developers.line.biz/en/reference/messaging-api/#richmenu-switch-action) in the Messaging API reference.

## Clipboard action 

The clipboard action copies text to the clipboard. When a user taps a control associated with this action, the text specified in the `clipboardText` property is copied to the device clipboard.

![](https://developers.line.biz/media/news/2024/clipbord-action-example-en.png)

This is a request body set with the clipboard action for the message shown in the example above. For more information, see [Clipboard action](https://developers.line.biz/en/reference/messaging-api/#clipboard-action) in the Messaging API reference.

```json
{
  "messages":[
    {
      "type": "template",
      "altText": "This is your coupon code.",
      "template": {
        "type": "buttons",
        "thumbnailImageUrl": "{your coupon image}",
        "imageAspectRatio": "rectangle",
        "imageSize": "cover",
        "imageBackgroundColor": "#FFFFFF",
        "title": "Your exclusive coupon!",
        "text": "Period: Feb 2024.\nCopy and use the code from the button.",
        "actions": [
          {
            "type": "clipboard",
            "label": "Copy",
            "clipboardText": "3B48740B"
          }
        ]
      }
    }
  ]
}
```
