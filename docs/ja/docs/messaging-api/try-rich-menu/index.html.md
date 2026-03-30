# リッチメニューを試す

リッチメニュープレイグラウンドは、リッチメニューの機能を試すことができるLINE公式アカウントです。本アカウントは、日本語のみに対応しています。[日時選択アクション](https://developers.line.biz/ja/reference/messaging-api/#datetime-picker-action)による日付選択、[リッチメニューエイリアス](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/)によるリッチメニューの切り替えなど、リッチメニューのさまざまな機能を試すことができます。

<!-- tip start -->

**リッチメニューを利用するメリットとは？**

サービス提供者とエンドユーザー、それぞれの視点から見たリッチメニューのメリットを[LINE API Use Case](https://lineapiusecase.com/ja/api/msgapi.html)サイトで確認できます。

<!-- tip end -->

![リッチメニュープレイグラウンドメイン画面](https://developers.line.biz/media/messaging-api/rich-menu-playground/richmenu-playground-bot-overview.png)

## リッチメニュープレイグラウンドを友だちとして追加する 

リッチメニューの機能を試すために、LINEアカウントにリッチメニュープレイグラウンドを友だちとして追加します。リッチメニュープレイグラウンドの追加方法は、以下のとおりです。

<!-- tip start -->

**リッチメニュープレイグラウンドはスマートフォンで試してください**

リッチメニューは、デスクトップ版（macOS、Windows）のLINEでは表示されません。リッチメニュープレイグラウンドはスマートフォン版のLINEで試してください。

<!-- tip end -->

| 追加する経路 | 追加する方法 |
| --- | --- |
| URL | スマートフォンのブラウザで[https://lin.ee/7ALASDvA](https://lin.ee/7ALASDvA)を開いて、友だち追加します。 |
| QRコード | リッチメニュープレイグラウンドのQRコードをLINEで読み込んで、友だち追加します。[^qrcode]</br></br>![リッチメニュープレイグラウンドのQRコード](https://qr-official.line.me/sid/M/976nukmg.png) |
| ID | リッチメニュープレイグラウンドのLINE ID（`@try_richmenu`）をLINEで検索して、友だち追加します。[^search-line-id] |

[^qrcode]: 詳しくは、『LINEみんなの使い方ガイド』の「[リンクやQRコードで友だち追加する](https://guide.line.me/ja/friends-and-groups/add-qrurl.html)」を参照してください。
[^search-line-id]: 詳しくは、『LINEみんなの使い方ガイド』の「[ID検索から友だちを追加する](https://guide.line.me/ja/friends-and-groups/search-line-id.html)」を参照してください。

## リッチメニュープレイグラウンドの共通機能 

リッチメニュープレイグラウンドを友だちに追加すると、リッチメニューに設定されているアクションを試せるようになります。[リッチメニューのレイアウト](https://developers.line.biz/ja/docs/messaging-api/try-rich-menu/#main-rich-menu)や、アクションを試した後の[アクションの詳細](https://developers.line.biz/ja/docs/messaging-api/try-rich-menu/#message-from-rich-menu-playground)を確認する方法などを説明します。

### リッチメニューのレイアウト 

リッチメニュープレイグラウンドのメインとなるリッチメニューでは、4種類の機能を提供しています。

1. タブ：さまざまな動作を試すためのメニュー。
2. ナビゲーションボタン：タブグループ間を移動する。
3. アクションボタン：ボタンに設定されたアクションを実行する。設定可能なパラメータがアクションにある場合は、パラメータごとのボタンが表示されます。
4. ヘルプボタン：対象のアクションのドキュメントを開く。

![メインメニュー](https://developers.line.biz/media/messaging-api/rich-menu-playground/menu-descriptions.png)

### アクションの詳細 

アクションを試すと、リッチメニュープレイグラウンドはそのアクションを実行し、実行されたアクションの詳細を表示します。これは、特にアクションが視覚的な結果を表示しない場合に、アクションが実行されたことを確認するのに役立ちます。アクションの詳細には、アクションの説明、アクションの設定（パラメータ）、LINEプラットフォームがボットサーバーに送信したWebhookイベントなどが含まれます。

![アクション実行後のメッセージ](https://developers.line.biz/media/messaging-api/rich-menu-playground/message.png)

## リッチメニュープレイグラウンドで試せるアクション 

リッチメニュープレイグラウンドでは、以下のアクションを試せます。

- [メッセージアクションを試す](https://developers.line.biz/ja/docs/messaging-api/try-rich-menu/#try-message-action)
- [ポストバックアクションを試す(1)](https://developers.line.biz/ja/docs/messaging-api/try-rich-menu/#try-postback-1-action)
- [ポストバックアクションを試す(2)](https://developers.line.biz/ja/docs/messaging-api/try-rich-menu/#try-postback-2-action)
- [ポストバックアクションを試す(3)](https://developers.line.biz/ja/docs/messaging-api/try-rich-menu/#try-postback-3-action)
- [URIアクションを試す](https://developers.line.biz/ja/docs/messaging-api/try-rich-menu/#try-uri-action)
- [日時選択アクションを試す](https://developers.line.biz/ja/docs/messaging-api/try-rich-menu/#try-datetime-picker-action)
- [リッチメニュー切替アクションを試す](https://developers.line.biz/ja/docs/messaging-api/try-rich-menu/#try-richmenu-switch-action)

### メッセージアクションを試す 

このタブでは、リッチメニューからメッセージを送信するための[メッセージアクション](https://developers.line.biz/ja/reference/messaging-api/#message-action)を実行することができます。

![メッセージアクションを試す](https://developers.line.biz/media/messaging-api/rich-menu-playground/01-message-action-ja.png)

<!-- tip start -->

**メッセージアクション**

LINE公式アカウントとのトークで、ユーザーがリッチメニューからメッセージを送信すると、LINEプラットフォームは対応する[メッセージイベント](https://developers.line.biz/ja/reference/messaging-api/#message-event)をボットサーバーに送信します。ボットサーバーは、メッセージイベントで返された応答トークンを使って[応答メッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)を送信することができます。

<!-- tip end -->

| ボタン | 説明 | 設定値（アクションオブジェクトの値） |
| --- | --- | --- |
| メッセージ送信 | メッセージを送信します。 | `{"type":"message","label":"メッセージを送信する","text":"message sent successfully!"}` |

### ポストバックアクションを試す(1) 

このタブでは、リッチメニューから[ポストバックアクション](https://developers.line.biz/ja/reference/messaging-api/#postback-action)を実行することができます。このアクションを実行すると、LINEプラットフォームはポストバックアクションオブジェクトの`data`プロパティに指定された文字列を含む[ポストバックイベント](https://developers.line.biz/ja/reference/messaging-api/#postback-event)をボットサーバーに対して送信します。

![ポストバックアクションを試す(1)](https://developers.line.biz/media/messaging-api/rich-menu-playground/02-postback-action-ja.png)

<!-- tip start -->

**ポストバックアクション**

ポストバックアクションを持つリッチメニューをユーザーがタップすると、LINEプラットフォームはボットサーバーに[ポストバックイベント](https://developers.line.biz/ja/reference/messaging-api/#postback-event)を送信します。このポストバックイベントには、ポストバックアクションの`data`プロパティに指定した文字列が含まれます。

`data`プロパティに指定した内容は、ユーザーには表示されません。これにより、一意のパラメータや識別子などのデータがボットサーバーに安全に送信されることが保証されます。ポストバックイベントから取得した応答トークンを使って、[応答メッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)を送信することができます。

<!-- tip end -->

| ボタン | 説明 | 設定値（アクションオブジェクトの値） |
| --- | --- | --- |
| displayTextあり | displayTextを設定したポストバックアクションを実行します。 | `{"type":"postback","label":"ディスプレイテキストあり","data":"actionId=21","displayText":"ディスプレイテキストです。トーク画面に表示されます。"}` |
| displayTextなし | displayTextを設定していないポストバックアクションを実行します。 | `{"type":"postback","label":"ディスプレイテキストなし","data":"actionId=22"}` |

<!-- tip start -->

**displayTextについて**

`displayText`プロパティにテキストを設定しておくと、ポストバックアクションが設定されたリッチメニューをユーザーがタップした場合に、そのテキストがユーザーからのメッセージとしてLINEのトーク画面に表示されます。`displayText`プロパティに設定したテキストは、トーク画面に表示されるだけで、[メッセージイベント](https://developers.line.biz/ja/reference/messaging-api/#message-event)としてボットサーバーに送信されることはありません。

<!-- tip end -->

### ポストバックアクションを試す(2) 

このタブでは、リッチメニューを開く、および閉じる[ポストバックアクション](https://developers.line.biz/ja/reference/messaging-api/#postback-action)を試せます。ポストバックアクションを実行すると、`data`プロパティに指定された文字列を含む[ポストバックイベント](https://developers.line.biz/ja/reference/messaging-api/#postback-event)がLINEプラットフォームからボットサーバーへ送信されます。

![ポストバックアクションを試す(2)](https://developers.line.biz/media/messaging-api/rich-menu-playground/02-2-postback-action-ja.png)

| ボタン | 説明 | 設定値（アクションオブジェクトの値） |
| --- | --- | --- |
| リッチメニューを開く | `inputOption:openRichMenu`が設定されたポストバックアクションを実行します。 | `{"type":"postback","label":"リッチメニューを開く","data":"actionId=","inputOption":"openRichMenu"}` |
| リッチメニューを閉じる | `inputOption:closeRichMenu`が設定されたポストバックアクションを実行します。 | `{"type":"postback","label":"リッチメニューを閉じる","data":"actionId=","inputOption":"closeRichMenu"}` |

### ポストバックアクションを試す(3) 

このタブでは、キーボードおよびボイスメッセージ入力モードを開く[ポストバックアクション](https://developers.line.biz/ja/reference/messaging-api/#postback-action)が設定されたリッチメニューを試せます。ポストバックアクションの実行と同時に、`data`プロパティに指定された文字列を含む[ポストバックイベント](https://developers.line.biz/ja/reference/messaging-api/#postback-event)がLINEプラットフォームからボットサーバーへ送信されます。

![ポストバックアクションを試す(3)](https://developers.line.biz/media/messaging-api/rich-menu-playground/02-3-postback-action-ja.png)

| ボタン | 説明 | 設定値（アクションオブジェクトの値） |
| --- | --- | --- |
| キーボードを開く | `inputOption:openKeyboard`が設定されたポストバックアクションを実行します。 | `{"type":"postback","label":"キーボードを開く","data":"actionId=","inputOption":"openKeyboard"}` |
| キーボードを開く（fillinTextあり） | `inputOption:openKeyboard`と`fillInText`が設定されたポストバックアクションを実行します。 | `{"type":"postback","label":"キーボードを開くフィルインテキストあり","data":"actionId=","inputOption":"openKeyboard","fillInText":"---\予約番号: \予約メニュー番号: \n予約日時: \n---"}` |
| ボイスメッセージ入力を開く | `inputOption:openVoice`が設定されたポストバックアクションを実行します。 | `{"type":"postback","label":"ボイスメッセージ入力モードを開く","data":"actionId=","inputOption":"openVoice"}` |

### URIアクションを試す 

このタブでは、リッチメニューから[URIアクション](https://developers.line.biz/ja/reference/messaging-api/#uri-action)を実行することができます。このアクションを実行すると、アクションに設定されたURIがウェブブラウザで開かれます。

![URIアクションを試す](https://developers.line.biz/media/messaging-api/rich-menu-playground/03-uri-action-ja.png)

| ボタン | 説明 | 設定値（アクションオブジェクトの値） |
| --- | --- | --- |
| URLを開く | URIアクションを実行します。 | `{"type":"uri","label":"URLを開く","uri":"https://developers.line.biz/docs/messaging-api/actions/#uri-action"}` |
| 外部ブラウザで開く | クエリパラメータに`openExternalBrowser=1`を付与した状態でURIアクションを実行します。詳しくは、「[URLを外部ブラウザで開く](https://developers.line.biz/ja/docs/messaging-api/using-line-url-scheme/#opening-url-in-external-browser)」を参照してください。 | `{"type":"uri","label":"外部ブラウザで開く","uri":"https://developers.line.biz/docs/messaging-api/actions/?openExternalBrowser=1#uri-action"}` |
| Chromeカスタムタブで開く（Androidのみ） | クエリパラメータに`openInAppBrowser=0`を付与した状態でURIアクションを実行します。詳しくは、「[URLを外部ブラウザで開く](https://developers.line.biz/ja/docs/messaging-api/using-line-url-scheme/#opening-url-in-external-browser)」を参照してください。 | `{"type":"uri","label":"Chromeカスタムタブで開く","uri":"https://developers.line.biz/docs/messaging-api/actions/?openInAppBrowser=0#uri-action"}` |
| 設定を確認する | URIアクションを実行せず、URIアクションオブジェクトの設定値だけ確認します。 | - |

<!-- tip start -->

**openInAppBrowserについて**

`openInAppBrowser`パラメータは、Android版LINEにおいてのみLINE内ブラウザを開くことができます。`openInAppBrowser`パラメータの仕様について詳しくは、「[URLを外部ブラウザで開く](https://developers.line.biz/ja/docs/messaging-api/using-line-url-scheme/#opening-url-in-external-browser)」を参照してください。

<!-- tip end -->

### 日時選択アクションを試す 

このタブでは、リッチメニューから[日時選択アクション](https://developers.line.biz/ja/reference/messaging-api/#datetime-picker-action)を実行することができます。このアクションを実行すると、日付と時刻の選択ダイアログが表示されます。日付を選択すると、LINEプラットフォームは選択した日付と時刻の[ポストバックイベント](https://developers.line.biz/ja/reference/messaging-api/#postback-event)をボットサーバーに送信します。

![日時選択アクションを試す](https://developers.line.biz/media/messaging-api/rich-menu-playground/04-datetime-picker-action-ja.png)

| ボタン | 説明 | 設定値（アクションオブジェクトの値） |
| --- | --- | --- |
| 日付と時刻を選択（datetimeモード） | `mode`プロパティに`datetime`が設定された日時選択アクションを実行します。 | `{"type":"datetimepicker","label":"datetimeモード","data":"actionId=31","mode":"datetime"}` |
| 初期値設定あり（initialプロパティあり） | `initial`プロパティが設定された日時選択アクションを実行します。 | `{"type":"datetimepicker","label":"初期値設定あり","data":"actionId=32","initial:"2021-11-01t00:00","mode":"datetime"}` |
| 最大・最小値設定あり（min、maxプロパティあり） | `min`および`max`プロパティが設定された日時選択アクションを実行します。 | `{"type":"datetimepicker","label":"最大・最小値設定あり","data":"actionId=33","mode":"datetime","max":"2021-12-31t23:59","min":"2021-11-01t00:00"}` |
| 日付を選択（dateモード） | `mode`プロパティに`date`が設定された日時選択アクションを実行します。 | `{"type":"datetimepicker","label":"dateモード","data":"actionId=34","mode":"date"}` |
| 時刻を選択（timeモード） | `mode`プロパティに`time`が設定された日時選択アクションを実行します。 | `{"type":"datetimepicker","label":"timeモード","data":"actionId=35","mode":"time"}` |

### リッチメニュー切替アクションを試す 

このタブでは、リッチメニューから[リッチメニュー切替アクション](https://developers.line.biz/ja/reference/messaging-api/#richmenu-switch-action)を実行することができます。このアクションを実行すると、リッチメニューは[リッチメニューエイリアス](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/)で定義されたメニューに切り替わります。リッチメニューが切り替わると、LINEプラットフォームはボットサーバーに[ポストバックイベント](https://developers.line.biz/ja/reference/messaging-api/#postback-event)を送信します。このイベントには、ポストバックアクションオブジェクトの`data`プロパティと`postback.params`オブジェクトに指定した値が含まれます。

![リッチメニュー切替アクションを試す](https://developers.line.biz/media/messaging-api/rich-menu-playground/05-rich-menu-switch-action-ja.png)

| ボタン | 説明 | 設定値（アクションオブジェクトの値） |
| --- | --- | --- |
| リッチメニューを切り替える | リッチメニュー切替アクションを実行します。 | `{"type":"richmenuswitch","label":"リッチメニューを切り替える","richMenuAliasId":"richmenu-richmenuswitch_2","data":"actionId=42"}` |
| 小さいサイズのリッチメニューに切り替える | リッチメニュー切替アクションを実行します。リッチメニューオブジェクトの`size`プロパティの`height`を低く設定したリッチメニューに切り替えます。 | `{"type":"richmenuswitch","label":"小さいサイズのリッチメニューに切り替える","richMenuAliasId":"richmenu-richmenuswitch_3","data":"actionId=43"}` |
