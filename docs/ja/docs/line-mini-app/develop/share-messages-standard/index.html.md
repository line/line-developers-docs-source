# ガイドラインに従ったJSONファイルの例

- [標準タイプ](https://developers.line.biz/ja/docs/line-mini-app/develop/share-messages-standard/#standard)
- [画像リストタイプ](https://developers.line.biz/ja/docs/line-mini-app/develop/share-messages-standard/#image-list)

## 標準タイプ 

```json
{
  "type": "bubble",
  "hero": {
    "type": "image",
    "url": "https://example.com/hero-image.png", // 適切な画像のURLを指定してください
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
              "uri": "https://miniapp.line.me/123456-abcedfg" // LINEミニアプリのページを指定してください
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
              "uri": "https://miniapp.line.me/123456-abcedfg/share" // LINEミニアプリのページを指定してください
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
            "url": "https://example.com/line-mini-app-icon.png", // LINEミニアプリのアイコンを指定してください
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
              "uri": "https://miniapp.line.me/123456-abcedfg" // LINEミニアプリのトップページを指定してください
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

## 画像リストタイプ 

```json
{
  "type": "bubble",
  "hero": {
    "type": "image",
    "url": "https://example.com/hero-image.png", // 適切な画像のURLを指定してください
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
                "url": "https://example.com/item-image01.png", // 適切な画像のURLを指定してください
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
                        "url": "https://example.com/item-image02.png", // 適切な画像のURLを指定してください
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
                "url": "https://example.com/item-image03.png", // 適切な画像のURLを指定してください
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
                        "url": "https://example.com/item-image04.png", // 適切な画像のURLを指定してください
                        "flex": 8,
                        "gravity": "center",
                        "size": "xxs",
                        "aspectRatio": "1:1"
                      },
                      {
                        "type": "text",
                        "text": "Image + text",
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
              "uri": "https://miniapp.line.me/123456-abcedfg" // LINEミニアプリのページを指定してください
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
              "uri": "https://miniapp.line.me/123456-abcedfg/share" // LINEミニアプリのページを指定してください
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
            "url": "https://example.com/line-mini-app-icon.png", // LINEミニアプリのアイコンを指定してください
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
              "uri": "https://miniapp.line.me/123456-abcedfg" // LINEミニアプリのトップページを指定してください
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
