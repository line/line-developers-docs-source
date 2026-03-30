# メッセージタイプ

Messaging APIを使うことで、ボットから以下のようなメッセージを送信できます。メッセージをインタラクティブにするには、ユーザーがトリガーするアクションを指定します。各メッセージタイプの仕様については、『Messaging APIリファレンス』の[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects) を参照してください。

- [テキストメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#text-messages)
- [テキストメッセージ（v2）](https://developers.line.biz/ja/docs/messaging-api/message-types/#text-messages-v2)
- [スタンプメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#sticker-messages)
- [画像メッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#image-messages)
- [動画メッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#video-messages)
- [音声メッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#audio-messages)
- [位置情報メッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#location-messages)
- [クーポンメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#coupon-messages)
- [イメージマップメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#imagemap-messages)
- [テンプレートメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#template-messages)
- [Flex Message](https://developers.line.biz/ja/docs/messaging-api/message-types/#flex-messages)

## テキストメッセージ 

テキストメッセージには、テキストや絵文字を含めることができます。テキストメッセージを送信するには、Messaging APIで送信する[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)にテキストを追加します。詳しくは、『Messaging APIリファレンス』の「[テキストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#text-message)」を参照してください。

![](https://developers.line.biz/media/messaging-api/messages/text.png)

テキストメッセージではLINE絵文字とUnicode絵文字を使うことができます。送信できるLINE絵文字について詳しくは、「[LINE絵文字](https://developers.line.biz/ja/docs/messaging-api/emoji-list/)」を参照してください。

![](https://developers.line.biz/media/messaging-api/messages/emoji.png)

<!-- tip start -->

**テキストの装飾とサイズの変更**

テキストの装飾やサイズの変更には、[Flex Message](https://developers.line.biz/ja/reference/messaging-api/#flex-message)を使用してください。

<!-- tip end -->

## テキストメッセージ（v2） 

テキストメッセージ（v2）を使うと、ユーザーにテキストを送信できます。[テキストメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#text-messages)と異なり、`{`と`}`で囲まれた文字列をメンションや絵文字に置き換えることができます。詳しくは、『Messaging APIリファレンス』の「[テキストメッセージ（v2）](https://developers.line.biz/ja/reference/messaging-api/#text-message-v2)」を参照してください。

![](https://developers.line.biz/media/messaging-api/messages/text-v2.png)

以前より提供しているテキストメッセージについては、今後も引き続き使用できます。ただし、今後は新しい機能をテキストメッセージ（v2）にのみ追加する可能性があります。

## スタンプメッセージ 

スタンプを利用することで、ボットをより魅力的で楽しいものにできます。Messaging APIでスタンプを送信するには、[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)にスタンプのパッケージIDとスタンプIDを指定します。送信できるスタンプについては、「[スタンプ](https://developers.line.biz/ja/docs/messaging-api/sticker-list/)」を参照してください。詳しくは、『Messaging APIリファレンス』の「[スタンプメッセージ](https://developers.line.biz/ja/reference/messaging-api/#sticker-message)」を参照してください。

![スタンプメッセージ](https://developers.line.biz/media/messaging-api/messages/sticker.png)

## 画像メッセージ 

画像メッセージは、1つの画像ファイルをユーザーに送信します。画像を送信する際は、[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)に2つのURLを指定します。1つはオリジナルの画像用、もう1つはプレビュー用です。プレビュー用の画像はトーク画面に表示される画像で、オリジナルの画像よりも小さい画像を指定します。

ユーザーがプレビュー用の画像をタップすると、以下のようにオリジナルの画像が表示されます。URLのプロトコルがHTTPS（TLS 1.2以降）であることを確認してください。詳しくは、『Messaging APIリファレンス』の「[画像メッセージ](https://developers.line.biz/ja/reference/messaging-api/#image-message)」を参照してください。

![画像メッセージ](https://developers.line.biz/media/messaging-api/messages/image.png) ![フルサイズの画像メッセージ](https://developers.line.biz/media/messaging-api/messages/image-full.png)

## 動画メッセージ 

動画メッセージは、1つの動画ファイルをユーザーに送信します。動画メッセージを送信する際は、[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)に動画のURLとプレビュー用の画像のURLを指定します。

ユーザーがプレビュー用の画像をタップすると、LINEが動画を再生します。URLのプロトコルがHTTPS（TLS 1.2以降）であることを確認してください。詳しくは、『Messaging APIリファレンス』の「[動画メッセージ](https://developers.line.biz/ja/reference/messaging-api/#video-message)」を参照してください。

![動画メッセージ](https://developers.line.biz/media/messaging-api/messages/video.png)

## 音声メッセージ 

音声メッセージは、1つの音声ファイルをユーザーに送信します。音声ファイルを送信するには、[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)にファイルのURLと音声ファイルの長さを指定してください。

URLのプロトコルがHTTPS（TLS 1.2以降）であることを確認してください。詳しくは、『Messaging APIリファレンス』の「[音声メッセージ](https://developers.line.biz/ja/reference/messaging-api/#audio-message)」を参照してください。

![音声メッセージ](https://developers.line.biz/media/messaging-api/messages/audio.png)

## 位置情報メッセージ 

位置情報メッセージは、ユーザーに位置情報を送信するメッセージです。[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)にタイトルと住所、緯度と経度の座標を指定します。詳しくは、『Messaging APIリファレンス』の「[位置情報メッセージ](https://developers.line.biz/ja/reference/messaging-api/#location-message)」を参照してください。

![位置情報メッセージ](https://developers.line.biz/media/messaging-api/messages/location-ja.png)

## クーポンメッセージ 

クーポンメッセージは、クーポンIDを指定してユーザーにクーポンを送信するメッセージです。

![](https://developers.line.biz/media/messaging-api/coupon/several-coupons.jpg)

詳しくは、『Messaging APIリファレンス』の「[クーポンメッセージ](https://developers.line.biz/ja/reference/messaging-api/#coupon-message)」を参照してください。

## イメージマップメッセージ 

イメージマップメッセージは、複数のタップ可能な領域を設定した画像を送信するメッセージです。タップ可能な領域を設定して、ウェブページを開いたり、ユーザーに代わってメッセージを送信したりできます。また、画像の上で動画を再生し、再生が終わるとリンクテキストを表示するように設定することもできます。詳しくは、『Messaging APIリファレンス』の「[イメージマップメッセージ](https://developers.line.biz/ja/reference/messaging-api/#imagemap-message)」を参照してください。

![イメージマップメッセージ](https://developers.line.biz/media/messaging-api/messages/imagemap.png)

## テンプレートメッセージ 

テンプレートメッセージにはあらかじめ定義されたレイアウトがあり、ユーザーによりよい体験を提供できます。[アクション](https://developers.line.biz/ja/docs/messaging-api/actions/)を使って、ユーザーとボットのインタラクションを実現できます。ユーザーがアクションを起こすのに必要なのはタップだけであり、メッセージを入力するよりも簡単に行うことができます。

利用可能なテンプレートは以下のとおりです。

- [ボタン](https://developers.line.biz/ja/docs/messaging-api/message-types/#buttons-template)
- [確認](https://developers.line.biz/ja/docs/messaging-api/message-types/#confirm-template)
- [カルーセル](https://developers.line.biz/ja/docs/messaging-api/message-types/#carousel-template)
- [画像カルーセル](https://developers.line.biz/ja/docs/messaging-api/message-types/#image-carousel-template)

テンプレートメッセージについて詳しくは、『Messaging APIリファレンス』の「[テンプレートメッセージ](https://developers.line.biz/ja/reference/messaging-api/#template-messages)」を参照してください。また、より柔軟なレイアウトでメッセージを送りたい場合は、[Flex Message](https://developers.line.biz/ja/docs/messaging-api/message-types/#flex-messages)を使用してください。

### ボタンテンプレート 

ボタンテンプレートには、画像やタイトル、テキスト、[アクション](https://developers.line.biz/ja/docs/messaging-api/actions/)ボタンが含まれます。ボタンに加えて、画像、タイトル、テキストにもアクションを設定できます。アクションを設定した領域をユーザーがタップすると、アクションがトリガーされます。詳しくは、『Messaging APIリファレンス』の「[ボタンテンプレート](https://developers.line.biz/ja/reference/messaging-api/#buttons)」を参照してください。

![ボタンテンプレートメッセージ](https://developers.line.biz/media/messaging-api/messages/buttons.png)

### 確認テンプレート 

確認テンプレートには、テキストと2つのボタンが含まれています。詳しくは、『Messaging APIリファレンス』の「[確認テンプレート](https://developers.line.biz/ja/reference/messaging-api/#confirm)」を参照してください。

![確認テンプレートメッセージ](https://developers.line.biz/media/messaging-api/messages/confirm.png)

### カルーセルテンプレート 

カルーセルテンプレートは、ユーザーがスクロールできる複数のカラムを含んでいます。ボタンに加えて、各カラムオブジェクトに[アクション](https://developers.line.biz/ja/docs/messaging-api/actions/)を設定できます。

アクションは、ユーザーがカラムオブジェクトの画像やタイトル、テキストエリアのどこかをタップしたときにトリガーされます。詳しくは、『Messaging APIリファレンス』の「[カルーセルテンプレート](https://developers.line.biz/ja/reference/messaging-api/#carousel)」を参照してください。

![カルーセルテンプレートメッセージ](https://developers.line.biz/media/messaging-api/messages/carousel.png)

### 画像カルーセルテンプレート 

画像カルーセルテンプレートは、ユーザーがスクロールできる複数の画像を含んでいます。詳しくは、『Messaging APIリファレンス』の「[画像カルーセルテンプレート](https://developers.line.biz/ja/reference/messaging-api/#image-carousel)」を参照してください。

![画像カルーセルテンプレートメッセージ](https://developers.line.biz/media/messaging-api/messages/image-carousel.png)

## Flex Message 

Flex Messageはレイアウトをカスタマイズできるメッセージです。[CSS Flexible Box（CSS Flexbox）](https://www.w3.org/TR/css-flexbox-1/)の仕様の範囲内でレイアウトをカスタマイズできます。詳しくは、「[Flex Messageを送信する](https://developers.line.biz/ja/docs/messaging-api/using-flex-messages/)」と『Messaging APIリファレンス』の「[Flex Message](https://developers.line.biz/ja/reference/messaging-api/#flex-message)」を参照してください。

![Flex Messageのサンプル](https://developers.line.biz/media/messaging-api/using-flex-messages/bubbleSamples-Update1.png)

## メッセージタイプ共通機能 

以下の機能は、すべてのメッセージタイプに適用できます。

### クイックリプライ 

クイックリプライボタンはすべてのメッセージタイプで利用可能で、チャットの下部に表示されます。ユーザーは、ボタンのいずれかをタップすると、ボットに返信できます。詳しくは、「[クイックリプライを使う](https://developers.line.biz/ja/docs/messaging-api/using-quick-reply/)」と『Messaging APIリファレンス』の「[クイックリプライ](https://developers.line.biz/ja/reference/messaging-api/#quick-reply)」を参照してください。

![クイックリプライのサンプル](https://developers.line.biz/media/messaging-api/using-quick-reply/quickReplySample.png)

## 関連ページ 

Messaging APIについての詳細は、以下を参照してください。

- [メッセージを送信する](https://developers.line.biz/ja/docs/messaging-api/sending-messages/)
- [メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)
- [アクション](https://developers.line.biz/ja/docs/messaging-api/actions/)
