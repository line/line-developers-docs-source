# An example of a JSON file that adheres to guidelines

- [Standard type](https://developers.line.biz/en/docs/line-mini-app/develop/share-messages-standard/#standard)
- [Image list type](https://developers.line.biz/en/docs/line-mini-app/develop/share-messages-standard/#image-list)

## Standard type 

```json
{
  "type": "bubble",
  "hero": {
    "type": "image",
    "url": "https://example.com/hero-image.png", // Specify the appropriate image URL
    "size": "full",
    "aspectRatio": "20:13",
    "aspectMode": "cover"
  },
  "body": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "text",
            "text": "Main title",
            "size": "lg",
            "color": "#000000",
            "weight": "bold",
            "wrap": true
          }
        ],
        "spacing": "none"
      },
      {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "text",
            "text": "Sub-title",
            "size": "sm",
            "color": "#999999",
            "wrap": true
          }
        ],
        "spacing": "none"
      },
      {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "box",
            "layout": "horizontal",
            "contents": [
              {
                "type": "text",
                "text": "Label 1",
                "size": "sm",
                "color": "#555555",
                "wrap": false,
                "flex": 20
              },
              {
                "type": "text",
                "text": "Description 1",
                "size": "sm",
                "color": "#111111",
                "wrap": false,
                "flex": 55
              }
            ],
            "flex": 1,
            "spacing": "sm"
          },
          {
            "type": "box",
            "layout": "horizontal",
            "contents": [
              {
                "type": "text",
                "text": "Label 2",
                "size": "sm",
                "color": "#555555",
                "wrap": false,
                "flex": 20
              },
              {
                "type": "text",
                "text": "Description 2",
                "size": "sm",
                "color": "#111111",
                "wrap": false,
                "flex": 55
              }
            ],
            "flex": 1,
            "spacing": "sm"
          }
        ],
        "spacing": "sm",
        "margin": "lg",
        "flex": 1
      },
      {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "button",
            "action": {
              "type": "uri",
              "label": "View details",
              "uri": "https://miniapp.line.me/123456-abcedfg" // Specify the LINE MINI App page.
            },
            "style": "primary",
            "height": "md",
            "color": "#17c950"
          },
          {
            "type": "button",
            "action": {
              "type": "uri",
              "label": "Share",
              "uri": "https://miniapp.line.me/123456-abcedfg/share" // Specify the LINE MINI App page.
            },
            "style": "link",
            "height": "md",
            "color": "#469fd6"
          }
        ],
        "spacing": "xs",
        "margin": "lg"
      }
    ],
    "spacing": "md"
  },
  "footer": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "separator",
        "color": "#f0f0f0"
      },
      {
        "type": "box",
        "layout": "horizontal",
        "contents": [
          {
            "type": "image",
            "url": "https://example.com/line-mini-app-icon.png", // Specify the LINE MINI App icon.
            "flex": 1,
            "gravity": "center"
          },
          {
            "type": "text",
            "text": "Service name",
            "flex": 19,
            "size": "xs",
            "color": "#999999",
            "weight": "bold",
            "gravity": "center",
            "wrap": false
          },
          {
            "type": "image",
            "url": "https://vos.line-scdn.net/service-notifier/footer_go_btn.png",
            "flex": 1,
            "gravity": "center",
            "size": "xxs",
            "action": {
              "type": "uri",
              "label": "action",
              "uri": "https://miniapp.line.me/123456-abcedfg" // Specify the top page of the LINE MINI App.
            }
          }
        ],
        "flex": 1,
        "spacing": "md",
        "margin": "md"
      }
    ]
  }
}
```

## Image list type 

```json
{
  "type": "bubble",
  "hero": {
    "type": "image",
    "url": "https://example.com/hero-image.png", // Specify the appropriate image URL
    "size": "full",
    "aspectRatio": "20:13",
    "aspectMode": "cover"
  },
  "body": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "text",
            "text": "Main title",
            "size": "lg",
            "color": "#000000",
            "weight": "bold",
            "wrap": true
          }
        ],
        "spacing": "none"
      },
      {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "text",
            "text": "Sub-title",
            "size": "sm",
            "color": "#999999",
            "wrap": true
          }
        ],
        "spacing": "none"
      },
      {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "box",
            "layout": "horizontal",
            "contents": [
              {
                "type": "image",
                "url": "https://example.com/hero-image.png", // Specify an appropriate image URL
                "flex": 3,
                "size": "sm",
                "aspectRatio": "1:1",
                "aspectMode": "cover"
              },
              {
                "type": "box",
                "layout": "vertical",
                "contents": [
                  {
                    "type": "text",
                    "text": "General text",
                    "size": "md",
                    "color": "#111111"
                  },
                  {
                    "type": "text",
                    "text": "Text to emphasize",
                    "size": "md",
                    "color": "#111111"
                  },
                  {
                    "type": "box",
                    "layout": "horizontal",
                    "contents": [
                      {
                        "type": "image",
                        "url": "https://example.com/hero-image.png", // Specify an appropriate image URL
                        "flex": 8,
                        "gravity": "center",
                        "size": "xxs",
                        "aspectRatio": "1:1"
                      },
                      {
                        "type": "text",
                        "text": "Text 3",
                        "flex": 85,
                        "gravity": "center",
                        "size": "sm",
                        "color": "#17c950",
                        "margin": "xs"
                      }
                    ],
                    "flex": 1
                  }
                ],
                "flex": 8,
                "spacing": "xs",
                "margin": "md"
              }
            ],
            "flex": 1
          },
          {
            "type": "box",
            "layout": "horizontal",
            "contents": [
              {
                "type": "image",
                "url": "https://example.com/hero-image.png", // Specify an appropriate image URL
                "flex": 3,
                "size": "sm",
                "aspectRatio": "1:1",
                "aspectMode": "cover"
              },
              {
                "type": "box",
                "layout": "vertical",
                "contents": [
                  {
                    "type": "text",
                    "text": "General text",
                    "size": "md",
                    "color": "#111111"
                  },
                  {
                    "type": "text",
                    "text": "Text to emphasize",
                    "size": "md",
                    "color": "#111111"
                  },
                  {
                    "type": "box",
                    "layout": "horizontal",
                    "contents": [
                      {
                        "type": "image",
                        "url": "https://example.com/hero-image.png", // Specify an appropriate image URL
                        "flex": 8,
                        "gravity": "center",
                        "size": "xxs",
                        "aspectRatio": "1:1"
                      },
                      {
                        "type": "text",
                        "text": "Text",
                        "flex": 85,
                        "gravity": "center",
                        "size": "sm",
                        "color": "#17c950",
                        "margin": "xs"
                      }
                    ],
                    "flex": 1
                  }
                ],
                "flex": 8,
                "spacing": "xs",
                "margin": "md"
              }
            ],
            "flex": 1
          }
        ],
        "spacing": "xl",
        "margin": "lg"
      },
      {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "button",
            "action": {
              "type": "uri",
              "label": "View details",
              "uri": "https://miniapp.line.me/123456-abcedfg" // Specify the LINE MINI App page.
            },
            "style": "primary",
            "height": "md",
            "color": "#17c950"
          },
          {
            "type": "button",
            "action": {
              "type": "uri",
              "label": "Share",
              "uri": "https://miniapp.line.me/123456-abcedfg/share" // Specify the LINE MINI App page.
            },
            "style": "link",
            "height": "md",
            "color": "#469fd6"
          }
        ],
        "spacing": "xs"
      }
    ],
    "spacing": "md"
  },
  "footer": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "separator",
        "color": "#f0f0f0"
      },
      {
        "type": "box",
        "layout": "horizontal",
        "contents": [
          {
            "type": "image",
            "url": "https://example.com/line-mini-app-icon.png", // Specify the LINE MINI App icon.
            "flex": 1,
            "gravity": "center"
          },
          {
            "type": "text",
            "text": "Service name",
            "flex": 19,
            "size": "xs",
            "color": "#999999",
            "weight": "bold",
            "gravity": "center",
            "wrap": false
          },
          {
            "type": "image",
            "url": "https://vos.line-scdn.net/service-notifier/footer_go_btn.png",
            "flex": 1,
            "gravity": "center",
            "size": "xxs",
            "action": {
              "type": "uri",
              "label": "action",
              "uri": "https://miniapp.line.me/123456-abcedfg" // Specify the top page of the LINE MINI App.
            }
          }
        ],
        "flex": 1,
        "spacing": "md",
        "margin": "md"
      }
    ]
  }
}
```
