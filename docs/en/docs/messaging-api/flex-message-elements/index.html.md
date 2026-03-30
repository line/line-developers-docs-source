# Flex Message elements

Flex Messages have a hierarchical structure for building blocks, in three levels. The top level is [container](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#container), followed by [blocks (header, hero, body, footer)](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#block) and then [components](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#component). This page explains elements constituting a Flex Message through an example.

![Structure of a Flex Message](https://developers.line.biz/media/messaging-api/using-flex-messages/overviewSample.png)

## Container 

Container is the top-level building block of Flex Messages. Available container types are:

| Type | Description |
| --- | --- |
| [Bubble](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#bubble) | A container that displays a single message bubble |
| [Carousel](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#carousel) | A container that displays multiple message bubbles, laid out side by side |

### Bubble 

Bubble is a container that contains only one instance of a message bubble. For more information about the JSON schema, see [Bubble](https://developers.line.biz/en/reference/messaging-api/#bubble) in the Messaging API reference.

![Bubble example](https://developers.line.biz/media/messaging-api/flex-message-elements/bubbleSample.png)

### Carousel 

Carousel is a container that contains multiple bubbles. You can browse the bubbles in a carousel by scrolling sideways.

![Carousel example](https://developers.line.biz/media/messaging-api/flex-message-elements/carouselSample.png)

The JSON definition of this Flex Message example is as follows. For more information about the JSON schema, see [Carousel](https://developers.line.biz/en/reference/messaging-api/#f-carousel) in the Messaging API reference.

```json
{
  "type": "carousel",
  "contents": [
    {
      "type": "bubble",
      "body": {
        "type": "box",
        "layout": "horizontal",
        "contents": [
          {
            "type": "text",
            "text": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
            "wrap": true
          }
        ]
      },
      "footer": {
        "type": "box",
        "layout": "horizontal",
        "contents": [
          {
            "type": "button",
            "style": "primary",
            "action": {
              "type": "uri",
              "label": "Go",
              "uri": "https://example.com"
            }
          }
        ]
      }
    },
    {
      "type": "bubble",
      "body": {
        "type": "box",
        "layout": "horizontal",
        "contents": [
          {
            "type": "text",
            "text": "Hello, World!",
            "wrap": true
          }
        ]
      },
      "footer": {
        "type": "box",
        "layout": "horizontal",
        "contents": [
          {
            "type": "button",
            "style": "primary",
            "action": {
              "type": "uri",
              "label": "Go",
              "uri": "https://example.com"
            }
          }
        ]
      }
    }
  ]
}
```

## Block 

Block is a unit that composes a bubble. Available block types are:

| Type   | Description                                               |
| ------ | --------------------------------------------------------- |
| Header | Block that displays the message subject or header         |
| Hero   | Block that displays the main image                        |
| Body   | Block that displays the main message                      |
| Footer | Block that displays buttons and supplementary information |

The order of placement is from header, hero, body, and footer. You don't have to use all block types in one message bubble. But if used, the block type can be used only once in a message bubble. For more information about the JSON schema, see the properties `header`, `hero`, `body`, and `footer` in the [Bubble](https://developers.line.biz/en/reference/messaging-api/#bubble) in the Messaging API reference.

![Block style example](https://developers.line.biz/media/messaging-api/flex-message-elements/blockStylesSample.png)

The JSON definition of this Flex Message example is as follows:

```json
{
  "type": "bubble",
  "styles": {
    "header": {
      "backgroundColor": "#ffaaaa"
    },
    "body": {
      "backgroundColor": "#aaffaa"
    },
    "footer": {
      "backgroundColor": "#aaaaff"
    }
  },
  "header": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "text",
        "text": "header"
      }
    ]
  },
  "hero": {
    "type": "image",
    "url": "https://example.com/flex/images/image.jpg",
    "size": "full",
    "aspectRatio": "2:1"
  },
  "body": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "text",
        "text": "body"
      }
    ]
  },
  "footer": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "text",
        "text": "footer"
      }
    ]
  }
}
```

## Component 

Component is a unit that composes a [block](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#block). Available components are:

| Component | Description |
| --- | --- |
| [Box](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#box) | This component defines a horizontal or vertical layout orientation and holds components together. |
| [Button](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#button) | This component renders a button. When the user taps a button, a specified action is performed. |
| [Image](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#image) | This component renders an image. |
| [Video](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#video) | This component renders a video. |
| [Icon](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#icon) | This component renders an icon. |
| [Text](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#text) | This component renders a text string. You can specify the font color, size, and weight. |
| [Span](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#span) | This component renders multiple text strings in different styles. You can specify the font color, size, weight, and decoration. |
| [Separator](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#separator) | This component renders a separating line. |
| [Filler](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#filler) (deprecated) | This component renders an empty space. |

### Box 

This component defines a horizontal or vertical layout orientation and holds components together. Any component can be contained, including a box. For more information on layout information, see [Flex Message layout](https://developers.line.biz/en/docs/messaging-api/flex-message-layout/). For more information on the JSON schema, see [Box](https://developers.line.biz/en/reference/messaging-api/#box) in the Messaging API reference.

### Button 

This component renders a button. You can set an [action](https://developers.line.biz/en/docs/messaging-api/actions/) to be executed when a user taps the button. You have three button styles to choose from as shown below. You can change the color of the button of all button styles.

![Button example](https://developers.line.biz/media/messaging-api/flex-message-elements/buttonSample.png)

The JSON definition of this Flex Message example is as follows. For more information about the JSON schema, see [Button](https://developers.line.biz/en/reference/messaging-api/#button) in the Messaging API reference.

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "vertical",
    "spacing": "md",
    "contents": [
      {
        "type": "button",
        "style": "primary",
        "action": {
          "type": "uri",
          "label": "Primary style button",
          "uri": "https://example.com"
        }
      },
      {
        "type": "button",
        "style": "secondary",
        "action": {
          "type": "uri",
          "label": "Secondary style button",
          "uri": "https://example.com"
        }
      },
      {
        "type": "button",
        "style": "link",
        "action": {
          "type": "uri",
          "label": "Link style button",
          "uri": "https://example.com"
        }
      }
    ]
  }
}
```

### Image 

This component renders an image.

![Image example](https://developers.line.biz/media/messaging-api/flex-message-elements/imageSample.png)

The JSON definition of this Flex Message example is as follows. For more information about the JSON schema, see [Image](https://developers.line.biz/en/reference/messaging-api/#f-image) in the Messaging API reference.

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "horizontal",
    "contents": [
      {
        "type": "image",
        "url": "https://example.com/flex/images/image.jpg",
        "size": "md"
      }
    ]
  }
}
```

### Video 

This component renders a video. For more information on using videos, see [Create a Flex Message including a video](https://developers.line.biz/en/docs/messaging-api/create-flex-message-including-video/).

![Video example](https://developers.line.biz/media/messaging-api/flex-message-elements/video-sample.png)

The JSON definition of this Flex Message example is as follows. For more information about the JSON schema, see [Video](https://developers.line.biz/en/reference/messaging-api/#f-video) in the Messaging API reference.

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

### Icon 

This component renders an icon for decorating the adjacent text. You can use this component only in a [baseline box](https://developers.line.biz/en/docs/messaging-api/flex-message-layout/#baseline-box).

![Icon example](https://developers.line.biz/media/messaging-api/flex-message-elements/iconSample.png)

The JSON definition of this Flex Message example is as follows. For more information about the JSON schema, see [Icon](https://developers.line.biz/en/reference/messaging-api/#icon) in the Messaging API reference.

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "box",
        "layout": "baseline",
        "contents": [
          {
            "type": "icon",
            "url": "https://example.com/flex/images/icon.png",
            "size": "md"
          },
          {
            "type": "text",
            "text": "The quick brown fox jumps over the lazy dog",
            "size": "md"
          }
        ]
      },
      {
        "type": "box",
        "layout": "baseline",
        "contents": [
          {
            "type": "icon",
            "url": "https://example.com/flex/images/icon.png",
            "size": "lg"
          },
          {
            "type": "text",
            "text": "The quick brown fox jumps over the lazy dog",
            "size": "lg"
          }
        ]
      },
      {
        "type": "box",
        "layout": "baseline",
        "contents": [
          {
            "type": "icon",
            "url": "https://example.com/flex/images/icon.png",
            "size": "xl"
          },
          {
            "type": "text",
            "text": "The quick brown fox jumps over the lazy dog",
            "size": "xl"
          }
        ]
      },
      {
        "type": "box",
        "layout": "baseline",
        "contents": [
          {
            "type": "icon",
            "url": "https://example.com/flex/images/icon.png",
            "size": "xxl"
          },
          {
            "type": "text",
            "text": "The quick brown fox jumps over the lazy dog",
            "size": "xxl"
          }
        ]
      },
      {
        "type": "box",
        "layout": "baseline",
        "contents": [
          {
            "type": "icon",
            "url": "https://example.com/flex/images/icon.png",
            "size": "3xl"
          },
          {
            "type": "text",
            "text": "The quick brown fox jumps over the lazy dog",
            "size": "3xl"
          }
        ]
      }
    ]
  }
}
```

### Text 

This component renders a text string. You can specify the color, size, and weight of the text. You can [wrap](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#text-wrap) long text and adjust the line spacing for wrapped text.

![Text example](https://developers.line.biz/media/messaging-api/flex-message-elements/textSample.png)

The JSON definition of this Flex Message example is as follows. For more information about the JSON schema, see [Text](https://developers.line.biz/en/reference/messaging-api/#f-text) in the Messaging API reference.

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "text",
        "text": "Closing the distance",
        "size": "md",
        "align": "center",
        "color": "#ff0000"
      },
      {
        "type": "text",
        "text": "Closing the distance",
        "size": "lg",
        "align": "center",
        "color": "#00ff00"
      },
      {
        "type": "text",
        "text": "Closing the distance",
        "size": "xl",
        "align": "center",
        "weight": "bold",
        "color": "#0000ff"
      }
    ]
  }
}
```

#### Text wrapping 

By default, overflowing text is truncated with an ellipsis. This is an example of how a long text gets displayed.

![Example without text wrapping](https://developers.line.biz/media/messaging-api/flex-message-elements/nowrapSample.png)

The JSON definition of this Flex Message example is as follows.

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "horizontal",
    "contents": [
      {
        "type": "text",
        "text": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
      }
    ]
  }
}
```

To avoid truncation, you can wrap long text. To apply text wrapping, set the `wrap` property to `true`. You can make a part of the text begin from a new line, with a new line character (`\n`). This is an example of a Flex Message with text wrapping and a new line character.

![Example with text wrapping](https://developers.line.biz/media/messaging-api/flex-message-elements/wrap-sample.png)

<!-- note start -->

**Note**

The new line character (`\n`) at the end of a text can be rendered differently by the device environment.

<!-- note end -->

The JSON definition of the text wrapping example is as follows. The `wrap` property is added with a value of `true`.

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "horizontal",
    "contents": [
      {
        "type": "text",
        "text": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod\n tempor incididunt ut labore et dolore magna aliqua.",
        "wrap": true
      }
    ]
  }
}
```

##### Line spacing in a text 

When you wrap a text, you can specify the line spacing of a wrapped text with the `lineSpacing` property.

<!-- note start -->

**Line spacing scope**

Line spacing isn't applied to the top of the first line and the bottom of the last line.

<!-- note end -->

![Example of increasing the line spacing in a text](https://developers.line.biz/media/messaging-api/flex-message-elements/line-spacing-sample.png)

The JSON definition of this Flex Message example is as follows. The `lineSpacing` property is added with a value of `20px`.

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "horizontal",
    "contents": [
      {
        "type": "text",
        "text": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod\n tempor incididunt ut labore et dolore magna aliqua.",
        "wrap": true,
        "lineSpacing": "20px"
      }
    ]
  }
}
```

### Span 

This component renders multiple text strings in different styles. You can specify the color, size, weight, and decoration of each text. Span is set to `contents` property of [texts](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#text).

![Span examples](https://developers.line.biz/media/messaging-api/flex-message-elements/spanSample.png)

The JSON definition of this Flex Message example is as follows. For more information about the JSON schema, see [Span](https://developers.line.biz/en/reference/messaging-api/#span) in the Messaging API reference.

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "horizontal",
    "contents": [
      {
        "type": "text",
        "text": "hello, world",
        "contents": [
          {
            "type": "span",
            "text": "Hello, world!",
            "decoration": "line-through"
          },
          {
            "type": "span",
            "text": "\nClosing",
            "color": "#ff0000",
            "size": "sm",
            "weight": "bold",
            "decoration": "none"
          },
          {
            "type": "span",
            "text": " "
          },
          {
            "type": "span",
            "text": "the",
            "size": "lg",
            "color": "#00ff00",
            "decoration": "underline",
            "weight": "bold"
          },
          {
            "type": "span",
            "text": " "
          },
          {
            "type": "span",
            "text": "distance",
            "color": "#0000ff",
            "weight": "bold",
            "size": "xxl"
          }
        ],
        "wrap": true,
        "align": "center"
      }
    ]
  }
}
```

### Separator 

This component renders a separating line inside a [box](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#box). A vertical line is drawn if included in a box with the horizontal layout. Similarly, a horizontal line is drawn if included in a box with the vertical layout.

![Separator example](https://developers.line.biz/media/messaging-api/flex-message-elements/separatorSample.png)

The JSON definition of this Flex Message example is as follows. For more information about the JSON schema, see [Separator](https://developers.line.biz/en/reference/messaging-api/#separator) in the Messaging API reference.

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "vertical",
    "spacing": "md",
    "contents": [
      {
        "type": "box",
        "layout": "horizontal",
        "spacing": "md",
        "contents": [
          {
            "type": "text",
            "text": "orange"
          },
          {
            "type": "separator"
          },
          {
            "type": "text",
            "text": "apple"
          }
        ]
      },
      {
        "type": "separator"
      },
      {
        "type": "box",
        "layout": "horizontal",
        "spacing": "md",
        "contents": [
          {
            "type": "text",
            "text": "grape"
          },
          {
            "type": "separator"
          },
          {
            "type": "text",
            "text": "lemon"
          }
        ]
      }
    ]
  }
}
```

### Filler 

<!-- warning start -->

**Filler is deprecated**

To add a space, use the properties of each component instead of adding fillers. For more information, see [Component position](https://developers.line.biz/en/docs/messaging-api/flex-message-layout/#component-position).

<!-- warning end -->

This component renders an empty space. You can put a space in between, before, or after components within a [box](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#box). The example below illustrates a box with two [images](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#image) and a filler in between the images.

![Filler example](https://developers.line.biz/media/messaging-api/flex-message-elements/fillerSample.png)

The JSON definition of this Flex Message example is as follows. For more information about the JSON schema, see [Filler](https://developers.line.biz/en/reference/messaging-api/#filler) in the Messaging API reference.

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "horizontal",
    "contents": [
      {
        "type": "image",
        "url": "https://example.com/flex/images/image.jpg"
      },
      {
        "type": "filler"
      },
      {
        "type": "image",
        "url": "https://example.com/flex/images/image.jpg"
      }
    ]
  }
}
```

## Learn more 

- [Send Flex Messages](https://developers.line.biz/en/docs/messaging-api/using-flex-messages/)
- [Flex Message layout](https://developers.line.biz/en/docs/messaging-api/flex-message-layout/)
- [Flex Message](https://developers.line.biz/en/reference/messaging-api/#flex-message) (Messaging API reference)
