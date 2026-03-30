# 動画を含むFlex Messageを作成する

Flex Messageの動画コンポーネントを使うと、ヒーローの[ブロック](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/#block)に動画を表示できます。Flex Messageの送信について詳しくは、「[Flex Messageを送信する](https://developers.line.biz/ja/docs/messaging-api/using-flex-messages/)」を参照してください。

<!-- table of contents -->

## 動画コンポーネントの使用条件 

[動画](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/#video)コンポーネントを使うには、以下の条件をすべて満たす必要があります。

- ヒーローの[ブロック](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/#block)のタイプに`video`を指定する。
- バブルのサイズに`kilo`、`mega`、`giga`のいずれかを指定する。
- バブルがカルーセルの子要素ではない。

## 動画のアスペクト比 

動画が横長すぎたり、縦長すぎたりすると、端末によっては動画の全体が表示されず、一部が欠けて表示される場合があります。動画を正しく表示するには、以下のアスペクト比がすべて同じであることを確認してください。

- `url`プロパティで指定する動画のアスペクト比
- `aspectRatio`プロパティで指定するアスペクト比
- `previewUrl`プロパティで指定するプレビュー画像のアスペクト比

![LINEのトークルームの動画。アスペクト比16:9の映像の背面に、アスペクト比1:1のプレビュー映像が表示されています。](https://developers.line.biz/media/messaging-api/messages/image-overlapping-ja.png)

## 動画のURIアクション 

動画コンポーネントの`action`プロパティを使うと、[URIアクション](https://developers.line.biz/ja/reference/messaging-api/#uri-action)を指定できます。URIアクションを指定すると、ラベルのタップ時にLINE内ブラウザで指定のURLを開いたり、通話アプリで指定の電話番号に電話をかけたりできます。URIアクションのラベルは以下の3箇所で表示されます。

- [トークルーム（動画再生終了時）](https://developers.line.biz/ja/docs/messaging-api/create-flex-message-including-video/#chat-room-screen)
- [動画プレーヤー（動画再生時）](https://developers.line.biz/ja/docs/messaging-api/create-flex-message-including-video/#video-player-screen1)
- [動画プレーヤー（動画再生終了時）](https://developers.line.biz/ja/docs/messaging-api/create-flex-message-including-video/#video-player-screen2)

![動画再生終了時のトークルーム](https://developers.line.biz/media/messaging-api/create-flex-message-including-video/label-in-chat-room-ja.png)
![動画再生時の動画プレーヤー](https://developers.line.biz/media/messaging-api/create-flex-message-including-video/label-in-video-player1-ja.png)
![動画終了時の動画プレーヤー](https://developers.line.biz/media/messaging-api/create-flex-message-including-video/label-in-video-player2-ja.png)

## 動画を含むFlex Messageの定義 

以下のFlex Messageは、動画だけを含む最も基本的なレイアウトです。

![動画コンポーネントの例](https://developers.line.biz/media/messaging-api/flex-message-elements/video-sample.png)

動画を含めるには、`hero`ブロックを使う必要があります。動画コンポーネントをサポートしていないバージョンのLINE向けには、ヒーローのブロックの`altContent`プロパティに、代替コンテンツを指定します。上のFlex Messageを表現するには以下のようなJSONデータを指定します。

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

また、[動画メッセージ](https://developers.line.biz/ja/reference/messaging-api/#video-message)とは異なり、動画を含む複雑なレイアウトのメッセージを構築できます。

![動画コンポーネントの例](https://developers.line.biz/media/messaging-api/create-flex-message-including-video/video.png)

上のFlex Messageを表現するには以下のようなJSONデータを指定します。

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
      "label": "詳細はこちら",
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

## 動画の再生方法 

Flex Messageで送信された動画は、[トークルーム](https://developers.line.biz/ja/docs/messaging-api/create-flex-message-including-video/#chat-room)上や[動画プレーヤー](https://developers.line.biz/ja/docs/messaging-api/create-flex-message-including-video/#video-player)上で再生できます。

<!-- note start -->

**動画が正しく再生できない**

動画を含むメッセージの送信に成功したとしても、ユーザーの端末上で動画を正しく再生できない場合があります。詳しくは、FAQの「[メッセージとして送信した動画が再生できないのはなぜですか？](https://developers.line.biz/ja/faq/#why-cant-i-play-a-video-i-sent)」を参照してください。

<!-- note end -->

### トークルーム上での自動再生 

トークルーム上で動画が自動再生されるかどうかは、LINEの［**設定**］ > ［**写真と動画**］ > ［**動画自動再生**］で確認できます。PC版LINE（macOS版とWindows版）では動画は自動再生されません。

| ［**動画自動再生**］の設定        | 自動再生                            |
| --------------------------------- | ----------------------------------- |
| ［**モバイルデータ通信とWi-Fi**］ | 動画が自動再生される                |
| ［**Wi-Fiのみ**］                 | Wi-Fi接続時のみ動画が自動再生される |
| ［**自動再生しない**］            | 動画が自動再生されない              |

#### 動画再生終了時の画面 

動画再生が終了すると、動画の上に最大2つのボタンが表示されます。1つ目のボタンは［**再生**］で、タップすると、動画プレーヤーを開き、もう一度動画を再生します。詳しくは「[動画プレーヤー上での手動再生](https://developers.line.biz/ja/docs/messaging-api/create-flex-message-including-video/#video-player)」を参照してください。

2つ目のボタンは［**詳細はこちら**］で、動画コンポーネントに指定したURIアクションのラベルです。任意のテキストに変更できます。動画コンポーネントにURIアクションを指定しない場合は、［**再生**］だけが表示されます。詳しくは、「[動画のURIアクション](https://developers.line.biz/ja/docs/messaging-api/create-flex-message-including-video/#uri-action)」を参照してください。

![動画再生終了時の画面](https://developers.line.biz/media/messaging-api/create-flex-message-including-video/auto-play-finished-ja.png)

### 動画プレーヤー上での手動再生 

ユーザーがトークルーム上の動画をタップすると、動画プレーヤーが起動し、ビデオが再生されます。[再生時](https://developers.line.biz/ja/docs/messaging-api/create-flex-message-including-video/#video-player-screen1)と[再生終了時](https://developers.line.biz/ja/docs/messaging-api/create-flex-message-including-video/#video-player-screen2)では表示されるボタンが異なります。

#### 動画再生時の画面 

動画再生時には、動画の上に最大2つのボタンが表示されます。1つ目のボタンは［**完了**］で、タップすると、動画プレーヤーを閉じ、トークルームに戻ります。このとき、動画の自動再生の条件を満たす場合は、トークルーム上で動画の続きが再生されます。詳しくは、「[トークルーム上での自動再生](https://developers.line.biz/ja/docs/messaging-api/create-flex-message-including-video/#chat-room)」を参照してください。

2つ目のボタンは［**詳細はこちら**］で、動画コンポーネントに指定したURIアクションのラベルです。任意のテキストに変更できます。動画コンポーネントにURIアクションを指定しない場合は、［**完了**］だけが表示されます。詳しくは、「[動画のURIアクション](https://developers.line.biz/ja/docs/messaging-api/create-flex-message-including-video/#uri-action)」を参照してください。

![動画再生時の画面](https://developers.line.biz/media/messaging-api/create-flex-message-including-video/video-player-ja.png)

#### 動画再生終了時の画面 

動画再生時には、動画の上に最大2つのボタンが表示されます。1つ目のボタンは［**リプレイ**］で、タップすると、動画プレーヤー上で動画をもう一度再生します。

2つ目のボタンは［**詳細はこちら**］で、動画コンポーネントに指定したURIアクションのラベルです。任意のテキストに変更できます。動画コンポーネントにURIアクションを指定しない場合は、［**リプレイ**］だけが表示されます。詳しくは、「[動画のURIアクション](https://developers.line.biz/ja/docs/messaging-api/create-flex-message-including-video/#uri-action)」を参照してください。

![動画再生終了時の画面](https://developers.line.biz/media/messaging-api/create-flex-message-including-video/video-player-finished-ja.png)

## 動画コンポーネントをサポートするバージョン未満のLINEでの表示 

LINEのバージョンが動画コンポーネントをサポートするバージョンに満たない場合、動画コンポーネントの`altContent`プロパティに指定したコンポーネントが代替コンテンツとして表示されます。`altContent`プロパティには[ボックス](https://developers.line.biz/ja/reference/messaging-api/#box)か[画像](https://developers.line.biz/ja/reference/messaging-api/#f-image)を指定します。

## Flex Message Simulatorでの表示 

[Flex Message Simulator](https://developers.line.biz/flex-simulator/)では動画のプレビューはできません。Flex Message Simulatorのプレビューエリアでは、「[動画コンポーネントをサポートするバージョン未満のLINEでの表示](https://developers.line.biz/ja/docs/messaging-api/create-flex-message-including-video/#alt-content)」と同様に、代替コンテンツが表示されます。

Flex Message Simulatorで作成したメッセージに含まれる動画を確認するには、テストメッセージを送信し、LINE上で確認してください。テストメッセージは、Flex Message Simulatorの右上の［**Send...**］から送信できます。

![Flex Message SimulatorのSend...ボタン](https://developers.line.biz/media/messaging-api/create-flex-message-including-video/send.png)

## 関連ページ 

- [Flex Messageを送信する](https://developers.line.biz/ja/docs/messaging-api/using-flex-messages/)
- [Flex Messageの要素](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/)
- [Flex Messageのレイアウト](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/)
- [Flex Message](https://developers.line.biz/ja/reference/messaging-api/#flex-message)（Messaging APIリファレンス）
- [Flex Message Simulator](https://developers.line.biz/flex-simulator/)
