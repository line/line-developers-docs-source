# テキストの文字数のカウント

Messaging APIでは、テキストの文字数は、UTF-16の符号単位（16ビット）でカウントします。複数の符号単位で表現する文字（例：一部の漢字やUnicode絵文字）は、複数の文字としてカウントします。たとえば、Unicode絵文字の🍎は、2つの符号単位で表現されます。そのため、1文字ではなく、2文字としてカウントします。

また、[LINE絵文字](https://developers.line.biz/ja/docs/messaging-api/emoji-list/)を含むテキストの文字数は、テキスト中の絵文字プレースホルダ（`$`）を、使用するLINE絵文字の代替テキストで差し替えた状態でカウントします。代替テキストとは、LINE絵文字の表示ができない端末向けのテキストのことです。そのため、LINE絵文字を含むテキストメッセージを送信する場合に、テキストの文字数が意図せず最大文字数を超えてしまい、メッセージの送信に失敗することがあります。なお、各LINE絵文字に対応する代替テキストは開示しておりません。

ただし、以下のプロパティは、UTF-16の符号単位ではなく、[書記素クラスタ](https://unicode.org/reports/tr29/)単位でカウントします。

| 種別 | プロパティ |
| --- | --- |
| すべての[アクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#action-objects) | <ul><li>`label`</li></ul> |
| [ポストバックアクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#postback-action) | <ul><li>`displayText`</li><li>`fillInText`</li><li>`label`</li><li>`text`</li></ul> |
| [メッセージアクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-action) | <ul><li>`label`</li><li>`text`</li></ul> |
| [ボタンテンプレートメッセージ](https://developers.line.biz/ja/reference/messaging-api/#buttons) | <ul><li>`text`</li><li>`title`</li></ul> |
| [確認テンプレートメッセージ](https://developers.line.biz/ja/reference/messaging-api/#confirm) | <ul><li>`text`</li></ul> |
| [カルーセルテンプレートメッセージ](https://developers.line.biz/ja/reference/messaging-api/#carousel) | <ul><li>`text`</li><li>`title`</li></ul> |
| [リッチメニューオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#rich-menu-object) | <ul><li>`chatBarText`</li><li>`name`</li></ul> |
