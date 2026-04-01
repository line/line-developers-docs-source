# Play with rich menus

Rich Menu Playground is a LINE Official Account where you can test rich menu features. This account is serviced only in Japanese. You can get your hands on rich menu features, such as date selection with the [datetime picker action](https://developers.line.biz/en/reference/messaging-api/#datetime-picker-action) and switching between rich menus with [rich menu aliases](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/).

![Rich Menu Playground main screen](https://developers.line.biz/media/messaging-api/rich-menu-playground/richmenu-playground-bot-overview.png)

## Add Rich Menu Playground 

Add Rich Menu Playground as a friend to your LINE account, to test rich menu features. You have different ways to add Rich Menu Playground as instructed below.

<!-- tip start -->

**Use Rich Menu Playground on smartphone**

Rich menus aren't displayed on LINE for PC (macOS, Windows). Use a smartphone to try Rich Menu Playground.

<!-- tip end -->

| Add through | How to add |
| --- | --- |
| URL | Open [https://lin.ee/7ALASDvA](https://lin.ee/7ALASDvA) on your smartphone browser and add. |
| QR code | Scan this QR code for Rich Menu Playground and add. [^qrcode]</br></br>![QR code of Rich Menu Playground](https://qr-official.line.me/sid/M/976nukmg.png) |
| ID | Search for the ID `@try_richmenu` from LINE and add the account.[^search-line-id] |

[^qrcode]: Learn [how to add a friend via link or QR code](https://guide.line.me/ja/friends-and-groups/add-qrurl.html) (only available in Japanese) in the LINE user's guide.
[^search-line-id]: Learn [how to add a friend from ID search](https://guide.line.me/ja/friends-and-groups/search-line-id.html) (only available in Japanese) in the LINE user's guide.

## Common features of Rich Menu Playground 

If you added Rich Menu Playground as a friend, now you can try the actions set on the rich menus. Learn the [layout of the rich menus](https://developers.line.biz/en/docs/messaging-api/try-rich-menu/#main-rich-menu) and how to check the [action detail](https://developers.line.biz/en/docs/messaging-api/try-rich-menu/#message-from-rich-menu-playground) after you try an action.

### Rich menu layout 

The rich menus of Rich Menu Playground have four main components:

1. Tabs: Contains menus to try different actions.
2. Navigation button: Moves between tab groups.
3. Action button: Triggers the action set on the button. If an action requires parameters, a parameter gets a button each for you to try.
4. Help button: Opens the document for the target action.

![Main Menu](https://developers.line.biz/media/messaging-api/rich-menu-playground/menu-descriptions.png)

### Action detail 

When you trigger an action, Rich Menu Playground does the action and then shows you the detail of the action you triggered. This helps you to know that the action was triggered, especially when the action doesn't render any visual result. The action detail includes the description of the action, action settings (parameters) and the webhook events the LINE Platform sent to the bot server.

![Message after the action is executed](https://developers.line.biz/media/messaging-api/rich-menu-playground/message.png)

## Actions available on Rich Menu Playground 

With Rich Menu Playground you can test:

- [Message action](https://developers.line.biz/en/docs/messaging-api/try-rich-menu/#try-message-action)
- [Postback action (1)](https://developers.line.biz/en/docs/messaging-api/try-rich-menu/#try-postback-1-action)
- [Postback action (2)](https://developers.line.biz/en/docs/messaging-api/try-rich-menu/#try-postback-2-action)
- [Postback action (3)](https://developers.line.biz/en/docs/messaging-api/try-rich-menu/#try-postback-3-action)
- [URI action](https://developers.line.biz/en/docs/messaging-api/try-rich-menu/#try-uri-action)
- [Datetime picker action](https://developers.line.biz/en/docs/messaging-api/try-rich-menu/#try-datetime-picker-action)
- [Rich menu switch action](https://developers.line.biz/en/docs/messaging-api/try-rich-menu/#try-richmenu-switch-action)

### Test message action 

This tab lets you trigger a [message action](https://developers.line.biz/en/reference/messaging-api/#message-action) to send a message from the rich menu.

![Try Message Action](https://developers.line.biz/media/messaging-api/rich-menu-playground/01-message-action-ja.png)

<!-- tip start -->

**Message action**

When a user sends a message through the rich menu in a chat with your LINE Official Account, the LINE Platform sends a corresponding [message event](https://developers.line.biz/en/reference/messaging-api/#message-event) to your bot server. Your bot server can then send a [reply message](https://developers.line.biz/en/reference/messaging-api/#send-reply-message) with the reply token returned through the message event.

<!-- tip end -->

| Button label | Action | Action object |
| --- | --- | --- |
| Send message | Sends a message | `{"type":"message", "label":"メッセージを送信する","text":"message sent successfully!"}` |

### Test postback action (1) 

This tab lets you trigger a [postback action](https://developers.line.biz/en/reference/messaging-api/#postback-action) from the rich menu. When you trigger this action, the LINE Platform sends the bot server a [postback event](https://developers.line.biz/en/reference/messaging-api/#postback-event) with the string specified in the `data` property of the postback action object.

![Try Postback Action (1)](https://developers.line.biz/media/messaging-api/rich-menu-playground/02-postback-action-ja.png)

<!-- tip start -->

**Postback action**

When a user taps on a rich menu with a [postback action](https://developers.line.biz/en/reference/messaging-api/#postback-action), the LINE Platform sends a [postback event](https://developers.line.biz/en/reference/messaging-api/#postback-event) to your bot server. This postback event has the string you specify in the `data` property of the postback action.

The content you specify in the `data` property is not shown to the user. This guarantees that data such as unique parameters and identifiers is sent securely to your bot server. You can send a [response message](https://developers.line.biz/en/reference/messaging-api/#send-reply-message) with the reply token you get from the postback event.

<!-- tip end -->

| Button label | Action | Action object |
| --- | --- | --- |
| With `displayText`  | Triggers a postback action and shows a text in the chat | `{"type":"postback","label":"ディスプレイテキストあり","data":"actionId=21","displayText":"ディスプレイテキストです。トーク画面に表示されます。"}` |
| No `displayText` | Triggers a postback action and shows no text in the chat | `{"type":"postback","label":"ディスプレイテキストなし","data":"actionId=22"}` |

<!-- tip start -->

**Text in the chat (displayText)**

To show text in a chat as a message from the user when a postback action is triggered, specify the `displayText` property in the postback action object. The text is displayed in the chat but not sent as a [message event](https://developers.line.biz/en/reference/messaging-api/#message-event) to the bot server.

<!-- tip end -->

### Test postback action (2) 

In this tab you can try the [postback actions](https://developers.line.biz/en/reference/messaging-api/#postback-action) of opening and closing the rich menu. When the postback action is executed, a [postback event](https://developers.line.biz/en/reference/messaging-api/#postback-event) containing the string specified in the `data` property is sent from the LINE Platform to the bot server.

![Try Postback Action (2)](https://developers.line.biz/media/messaging-api/rich-menu-playground/02-2-postback-action-ja.png)

| Button label | Action | Action object |
| --- | --- | --- |
| Open rich menu | Executes a postback action with `inputOption:openRichMenu` set. | `{"type":"postback","label":"リッチメニューを開く","data":"actionId=","inputOption":"openRichMenu"}` |
| Close rich menu | Executes a postback action with `inputOption:closeRichMenu` set. | `{"type":"postback","label":"リッチメニューを閉じる","data":"actionId=","inputOption":"closeRichMenu"}` |

### Test postback action (3) 

In this tab, you can try out the rich menu with [postback actions](https://developers.line.biz/en/reference/messaging-api/#postback-action) set to open keyboard and voice message input modes. Once the postback action is executed, a [postback event](https://developers.line.biz/en/reference/messaging-api/#postback-event) containing the string specified in the `data` property is sent from the LINE Platform to the bot server.

![Try Postback Action (3)](https://developers.line.biz/media/messaging-api/rich-menu-playground/02-3-postback-action-ja.png)

| Button label | Action | Action object |
| --- | --- | --- |
| Open keyboard | Executes a postback action with `inputOption:openKeyboard` set. | `{"type":"postback","label":"キーボードを開く","data":"actionId=","inputOption":"openKeyboard"}` |
| Open keyboard with fillinText | Executes a postback action with `inputOption:openKeyboard` and `fillInText` set. | `{"type":"postback","label":"キーボードを開くフィルインテキストあり","data":"actionId=","inputOption":"openKeyboard","fillInText":"---\予約番号: \予約メニュー番号: \n予約日時: \n---"}` |
| Open voice message input mode | Executes a postback action with `inputOption:openVoice` set. | `{"type":"postback","label":"ボイスメッセージ入力モードを開く","data":"actionId=","inputOption":"openVoice"}` |

### Test URI Action 

In this tab, you can trigger a [URI action](https://developers.line.biz/en/reference/messaging-api/#uri-action) from the rich menu. When you trigger this action, the `uri` set for the action is opened in a web browser.

![Try URI action](https://developers.line.biz/media/messaging-api/rich-menu-playground/03-uri-action-ja.png)

| Button label | Action | Action object |
| --- | --- | --- |
| Open a URL | Opens the specified URI | `{"type":"uri","label":"URLを開く","uri":"https://developers.line.biz/docs/messaging-api/actions/#uri-action"}` |
| Open in an external browser | Opens the URI in an [external browser](https://developers.line.biz/en/docs/messaging-api/using-line-url-scheme/#opening-url-in-external-browser) (`openExternalBrowser=0`) | `{"type":"uri","label":"外部ブラウザで開く","uri":"https://developers.line.biz/docs/messaging-api/actions/?openExternalBrowser=1#uri-action"}` |
| Open in a Chrome custom tab (Android only) | Opens the URI in the [in-app browser](https://developers.line.biz/en/docs/messaging-api/using-line-url-scheme/#opening-url-in-external-browser), if supported (`openInAppBrowser=0`) | `{"type":"uri","label":"Chromeカスタムタブで開く","uri":"https://developers.line.biz/docs/messaging-api/actions/?openInAppBrowser=0#uri-action"}` |
| Check configuration (The white buttons) | Doesn't open a URI but shows you the values set in the URI action object | Not applicable |

<!-- tip start -->

**About openInAppBrowser**

The `openInAppBrowser` parameter opens LINE's in-app browser only in LINE for Android. For the specification on the `openInAppBrowser` parameter, see [Opening a URL in an external browser](https://developers.line.biz/en/docs/messaging-api/using-line-url-scheme/#opening-url-in-external-browser).

<!-- tip end -->

### Test datetime picker action 

In this tab, you can trigger a [datetime picker action](https://developers.line.biz/en/reference/messaging-api/#datetime-picker-action) from the rich menu. When you trigger this action, the date and time selection dialog is displayed. Once you select a date, the LINE Platform sends your bot server a [postback event](https://developers.line.biz/en/reference/messaging-api/#postback-event) with selected date and time.

![Try Datetime Picker Action](https://developers.line.biz/media/messaging-api/rich-menu-playground/04-datetime-picker-action-ja.png)

| Button label | Action | Action object |
| --- | --- | --- |
| Date and time selection (datetime mode) | Opens the date time picker set to the current date and time (`mode` set to `datetime`) | `{"type":"datetimepicker","label":"datetimeモード","data":"actionId=31","mode":"datetime"}` |
| With initial value set (with `initial` property) | Opens the date time picker set to the value of the `initial` property | `{"type":"datetimepicker","label":"初期値設定あり","data":"actionId=32","initial:"2021-11-01t00:00","mode":"datetime"}` |
| With max and min values set (with `min`, `max` properties) | Opens the date time picker with min and max dates set | `{"type":"datetimepicker","label":"最大・最小値設定あり","data":"actionId=33","mode":"datetime","max":"2021-12-31t23:59","min":"2021-11-01t00:00"}` |
| Select date (date mode) | Opens the date time picker set to the current date | `{"type":"datetimepicker","label":"dateモード","data":"actionId=34","mode":"date"}` |
| Select time (time mode) | Opens the date time picker set to the current time | `{"type":"datetimepicker","label":"timeモード","data":"actionId=35","mode":"time"}` |

### Test rich menu switch action 

In this tab, you can trigger a [rich menu switch action](https://developers.line.biz/en/reference/messaging-api/#richmenu-switch-action) from the rich menu. When you trigger this action, the rich menu is switched to the menu defined in [rich menu aliases](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/). When the rich menu is switched, the LINE Platform sends your bot server a [postback event](https://developers.line.biz/en/reference/messaging-api/#postback-event). This event has values you specify for the `data` property and `postback.params` object in the postback action object.

![Try Rich Menu Switching Action](https://developers.line.biz/media/messaging-api/rich-menu-playground/05-rich-menu-switch-action-ja.png)

| Button label | Action | Action object |
| --- | --- | --- |
| Switch rich menu | Switches the rich menu | `{"type":"richmenuswitch","label":"リッチメニューを切り替える","richMenuAliasId":"richmenu-richmenuswitch_2","data":"actionId=42"}` |
| Switch rich menu to a smaller size | Switches the rich menu to the smaller size specified by the `height` of the `size` property in the rich menu object | `{"type":"richmenuswitch","label":"小さいサイズのリッチメニューに切り替える","richMenuAliasId":"richmenu-richmenuswitch_3","data":"actionId=43"}` |
