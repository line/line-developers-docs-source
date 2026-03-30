# Character counting in a text

The Messaging API counts text characters in UTF-16 code units (16-bit). Characters made up of multiple code units (e.g. some Kanji characters, Unicode emojis) are counted as more than one character. For example, a Unicode emoji 🍎 is expressed in two code units. Thus 🍎 is two characters long, not one.

When the Messaging API counts a text that has a [LINE emoji](https://developers.line.biz/en/docs/messaging-api/emoji-list/), the emoji placeholder (`$`) is replaced with the emoji's alternative text. Alternative text is the text displayed instead of the emoji on devices that can't display LINE emojis. Therefore, when sending a text message that has a LINE emoji, the text length may unintentionally exceed the maximum length and sending the message may fail. Note that LINE doesn't disclose the alternative text for LINE emojis.

However, the properties listed below are counted in [grapheme cluster](https://unicode.org/reports/tr29/) units, not in UTF-16 code units:

| Type | Property |
| --- | --- |
| All [action objects](https://developers.line.biz/en/reference/messaging-api/#action-objects) | <ul><li>`label`</li></ul> |
| [Postback action objects](https://developers.line.biz/en/reference/messaging-api/#postback-action) | <ul><li>`displayText`</li><li>`fillInText`</li><li>`label`</li><li>`text`</li></ul> |
| [Message action objects](https://developers.line.biz/en/reference/messaging-api/#message-action) | <ul><li>`label`</li><li>`text`</li></ul> |
| [Buttons template messages](https://developers.line.biz/en/reference/messaging-api/#buttons) | <ul><li>`text`</li><li>`title`</li></ul> |
| [Confirm template messages](https://developers.line.biz/en/reference/messaging-api/#confirm) | <ul><li>`text`</li></ul> |
| [Carousel template messages](https://developers.line.biz/en/reference/messaging-api/#carousel) | <ul><li>`text`</li><li>`title`</li></ul> |
| [Rich menu objects](https://developers.line.biz/en/reference/messaging-api/#rich-menu-object) | <ul><li>`chatBarText`</li><li>`name`</li></ul> |
