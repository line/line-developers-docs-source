# アクション

ユーザーがメッセージ内のコントロールをタップしたときに実行されるアクションのタイプを設定できます。メッセージのタイプによって使用できるアクションは異なります。詳しくは、『Messaging APIリファレンス』の「[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)」を参照してください。

以下のアクションを使用できます。

- [ポストバックアクション](https://developers.line.biz/ja/docs/messaging-api/actions/#postback-action)
- [メッセージアクション](https://developers.line.biz/ja/docs/messaging-api/actions/#message-action)
- [URIアクション](https://developers.line.biz/ja/docs/messaging-api/actions/#uri-action)
- [日時選択アクション](https://developers.line.biz/ja/docs/messaging-api/actions/#datetime-picker-action)
- [カメラアクション](https://developers.line.biz/ja/docs/messaging-api/actions/#camera-action)
- [カメラロールアクション](https://developers.line.biz/ja/docs/messaging-api/actions/#camera-roll-action)
- [位置情報アクション](https://developers.line.biz/ja/docs/messaging-api/actions/#location-action)
- [リッチメニュー切替アクション](https://developers.line.biz/ja/docs/messaging-api/actions/#richmenu-switch-action)
- [クリップボードアクション](https://developers.line.biz/ja/docs/messaging-api/actions/#clipboard-action)

## ポストバックアクション 

特定の文字列を含む[ポストバックイベント](https://developers.line.biz/ja/reference/messaging-api/#postback-event)をサーバーに返すアクションです。ユーザーからのメッセージとして送信されるテキストを含めることができます。

また、リッチメニューなどに対して、ユーザーのアクションに応じた表示方法を指定することもできます。指定できる表示方法は次のとおりです。

- リッチメニューを閉じる
- リッチメニューを開く
- キーボードを開く
- ボイスメッセージ入力モードを開く

なお、ユーザーのアクションに応じた表示方法の指定は、iOS版LINEまたはAndroid版LINEのバージョン`12.6.0`以降で利用できます。詳しくは、『Messaging APIリファレンス』の「[ポストバックアクション](https://developers.line.biz/ja/reference/messaging-api/#postback-action)」を参照してください。

## メッセージアクション 

ユーザーからのテキストメッセージとして特定の文字列を送信するアクションです。詳しくは、『Messaging APIリファレンス』の「[メッセージアクション](https://developers.line.biz/ja/reference/messaging-api/#message-action)」を参照してください。

## URIアクション 

LINE内ブラウザで指定のURLを開くアクションです。URIアクションで[LINE URLスキーム](https://developers.line.biz/ja/docs/messaging-api/using-line-url-scheme/)を使うと、通話アプリで指定の電話番号を開いたり、任意のLINE公式アカウントをシェアする画面を開いたりすることもできます。

![URIアクション](https://developers.line.biz/media/messaging-api/actions/quick-reply-uri-action-ja.png)

上記の例で示した、クイックリプライボタンにURIアクションを設定したリクエストボディは以下のようになります。詳しくは、『Messaging APIリファレンス』の「[URIアクション](https://developers.line.biz/ja/reference/messaging-api/#uri-action)」を参照してください。

```json
{
  "messages": [
    {
      "type": "text",
      "text": "ご注文はお決まりですか？",
      "quickReply": {
        "items": [
          {
            "type": "action",
            "action": {
              "type": "uri",
              "label": "メニューを見る",
              "uri": "https://example.com/menu"
            }
          },
          {
            "type": "action",
            "action": {
              "type": "uri",
              "label": "電話注文",
              "uri": "tel:09001234567"
            }
          },
          {
            "type": "action",
            "action": {
              "type": "uri",
              "label": "友だちに勧める",
              "uri": "https://line.me/R/nv/recommendOA/%40linedevelopers"
            }
          }
        ]
      }
    }
  ]
}
```

## 日時選択アクション 

ユーザーにピッカーから特定の日付、時刻、または日時を選択させるアクションです。ユーザーが選択した日時は、Webhookを介して[ポストバックイベント](https://developers.line.biz/ja/reference/messaging-api/#postback-event)で返されます。詳しくは、『Messaging APIリファレンス』の「[日時選択アクション](https://developers.line.biz/ja/reference/messaging-api/#datetime-picker-action)」を参照してください。

![日時選択アクション](https://developers.line.biz/media/messaging-api/actions/datetime-picker.png)

## カメラアクション 

LINE内のカメラを起動するアクションです。このアクションはクイックリプライボタンにのみ設定できます。詳しくは、『Messaging APIリファレンス』の「[カメラアクション](https://developers.line.biz/ja/reference/messaging-api/#camera-action)」を参照してください。

## カメラロールアクション 

LINEのカメラロール画面を開くアクションです。このアクションはクイックリプライボタンにのみ設定できます。詳しくは、『Messaging APIリファレンス』の「[カメラロールアクション](https://developers.line.biz/ja/reference/messaging-api/#camera-roll-action)」を参照してください。

## 位置情報アクション 

LINEの位置情報画面を開くアクションです。このアクションはクイックリプライボタンにのみ設定できます。詳しくは、『Messaging APIリファレンス』の「[位置情報アクション](https://developers.line.biz/ja/reference/messaging-api/#location-action)」を参照してください。

## リッチメニュー切替アクション 

リッチメニューを切り替えるアクションです。このアクションはリッチメニューにのみ設定できます。詳しくは、『Messaging APIリファレンス』の「[リッチメニュー切替アクション](https://developers.line.biz/ja/reference/messaging-api/#richmenu-switch-action)」を参照してください。

## クリップボードアクション 

クリップボードにテキストをコピーするためのアクションです。ユーザーがこのアクションが関連づけられたコントロールをタップすると、`clipboardText`プロパティに指定されたテキストが、端末のクリップボードにコピーされます。

![](https://developers.line.biz/media/news/2024/clipbord-action-example-ja.png)

上記の例で示した、メッセージにクリップボードアクションを設定したリクエストボディは以下のようになります。詳しくは、『Messaging APIリファレンス』の「[クリップボードアクション](https://developers.line.biz/ja/reference/messaging-api/#clipboard-action)」を参照してください。

```json
{
  "messages": [
    {
      "type": "template",
      "altText": "クーポンコードをお送りします。",
      "template": {
        "type": "buttons",
        "thumbnailImageUrl": "{your coupon image}",
        "imageAspectRatio": "rectangle",
        "imageSize": "cover",
        "imageBackgroundColor": "#FFFFFF",
        "title": "限定クーポン配布中！",
        "text": "有効期限：2024年2月末日\nクーポンコード（3B48740B）を下記のボタンからコピーしてお使いください。",
        "actions": [
          {
            "type": "clipboard",
            "label": "コピー",
            "clipboardText": "3B48740B"
          }
        ]
      }
    }
  ]
}
```
