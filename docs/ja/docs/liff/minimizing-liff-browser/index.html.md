# LIFFブラウザを最小化する

ここでは、LIFFブラウザの最小化について説明します。

<!-- table of contents -->

## LIFFブラウザの最小化とは 

[LIFFブラウザ](https://developers.line.biz/ja/glossary/#liff-browser)の最小化とは、LIFFブラウザの閲覧を中断し、別の操作を行うための機能です。

ユーザーがトークルーム上でLIFFブラウザを閲覧しているとき、トークルームにメッセージを送信するといった別の操作を行いたいことがあります。このとき、LIFFブラウザを最小化すると、LIFFブラウザの閲覧を中断し、別の操作を行うことができます。また、別の操作を行った後、LIFFブラウザを最大化することで、中断したLIFFブラウザの閲覧を再開できます。

LIFFブラウザは、最小化するとアイコンで表示されます。

![LIFFブラウザの最小化](https://developers.line.biz/media/liff/minimizing-liff-app/liff-minimize-ja.png)

<!-- tip start -->

**LINE内ブラウザを最小化する**

LIFFブラウザと同様に、[LINE内ブラウザ](https://developers.line.biz/ja/glossary/#line-iab)も最小化に対応しています。詳しくは、『LINEみんなの使い方ガイド』の「[閲覧中のWEBページを最小化する](https://guide.line.me/ja/chats-calls-notifications/chats/minimizebrowser.html)」を参照してください。

<!-- tip end -->

## LIFFブラウザの最小化の使用条件 

LIFFブラウザを最小化するには、以下の条件をすべて満たす必要があります。

- iOS版LINEバージョン12.18.0以降またはAndroid版LINEバージョン15.0.0以降
- 端末の［**設定**］ > ［**アプリ**］ > ［**LINE**］ > ［**他のアプリの上に重ねて表示**］がオン（Android版LINEのみ）
- LIFFアプリの[画面サイズ](https://developers.line.biz/ja/docs/liff/overview/#screen-size)に`Full`を指定
- LIFFアプリの[`chat_message.write`スコープ](https://developers.line.biz/ja/docs/liff/registering-liff-apps/#registering-liff-app)がオフ
- LIFFブラウザがモーダルの上に重なっていない

<!-- note start -->

**LIFF間遷移後のLIFFアプリが使用条件を満たす必要があります**

[LIFF間遷移](https://developers.line.biz/ja/docs/liff/opening-liff-app/#move-liff-to-liff)後のLIFFブラウザを最小化するには、遷移後のLIFFアプリが使用条件を満たす必要があります。

たとえば、「[LIFFアプリの画面サイズによる動作](https://developers.line.biz/ja/docs/liff/opening-liff-app/#behavior-by-screen-size)」にあるように、遷移後のLIFFアプリは画面サイズの指定にかかわらず`Full`で表示されます。しかし、遷移後のLIFFアプリの画面サイズに`Tall`や`Compact`を指定している場合、遷移後のLIFFアプリはLIFFブラウザの最小化の使用条件を満たしません。

<!-- note end -->

なお、iPadOS版LINEについては、LIFFブラウザの最小化に対応予定ですが、時期は未定です。

## LIFFブラウザを最小化する 

LIFFブラウザを最小化するには、以下の3つの方法があります。

- [アクションボタンからオプションをタップする](https://developers.line.biz/ja/docs/liff/minimizing-liff-browser/#tap-action-button-option)
- [アプリ内通知をタップする](https://developers.line.biz/ja/docs/liff/minimizing-liff-browser/#tap-in-app-alert)
- [LIFFブラウザをスワイプする](https://developers.line.biz/ja/docs/liff/minimizing-liff-browser/#swipe-liff-browser)

### アクションボタンからオプションをタップする 

[アクションボタン](https://developers.line.biz/ja/docs/liff/overview/#action-button)から[マルチタブビュー](https://developers.line.biz/ja/docs/liff/overview/#multi-tab-view)を開き、［**ページを最小化**］オプションをタップします。

![LIFFブラウザの最小化（アクションボタンのオプションをタップする）](https://developers.line.biz/media/liff/minimizing-liff-app/tap-action-button-option-ja.png)

### アプリ内通知をタップする 

アプリ内通知をタップします。

![LIFFブラウザの最小化（アプリ内通知をタップする）](https://developers.line.biz/media/liff/minimizing-liff-app/tap-in-app-alert.png)

### LIFFブラウザをスワイプする 

LIFFブラウザを下方向へスワイプします。

![LIFFブラウザの最小化（LIFFブラウザをスワイプする）](https://developers.line.biz/media/liff/minimizing-liff-app/swipe-liff-browser-ja.png)

## LIFFブラウザを最大化する 

LIFFブラウザを最大化するには、最小化したLIFFブラウザをタップします。

![LIFFブラウザの最大化](https://developers.line.biz/media/liff/minimizing-liff-app/maximize-liff-browser-ja.png)

## 最小化したLIFFブラウザを移動する 

最小化したLIFFブラウザを移動するには、ドラッグします。

![最小化したLIFFブラウザの移動](https://developers.line.biz/media/liff/minimizing-liff-app/move-minimized-liff-browser-ja.png)

## 最小化したLIFFブラウザを閉じる（LINEバージョン15.20.0未満の場合） 

LINEバージョン15.20.0未満の場合、最小化したLIFFブラウザを閉じるには、以下の2つの方法があります。

- [LIFFブラウザを画面外にスワイプする（iOS版LINEのみ）](https://developers.line.biz/ja/docs/liff/minimizing-liff-browser/#close-minimized-liff-browser-1)
- [LIFFブラウザを閉じるアイコンにドラッグする ](https://developers.line.biz/ja/docs/liff/minimizing-liff-browser/#close-minimized-liff-browser-2)

### LIFFブラウザを画面外にスワイプする（iOS版LINEのみ） 

最小化したLIFFブラウザを、画面外にスワイプします。

![最小化したLIFFブラウザを閉じる](https://developers.line.biz/media/liff/minimizing-liff-app/close-minimized-liff-browser-ja.png)

### LIFFブラウザを閉じるアイコンにドラッグする 

最小化したLIFFブラウザをドラッグすると、画面下に閉じるアイコンが表示されます。閉じるアイコンに最小化したLIFFブラウザをドラッグし、指を離します。

![最小化したLIFFブラウザを閉じる](https://developers.line.biz/media/liff/minimizing-liff-app/close-minimized-liff-browser-ios-12-12-0-or-later-ja.png)

## 最小化したLIFFブラウザを閉じる（LINEバージョン15.20.0以降の場合） 

LINEバージョン15.20.0以降の場合、最小化したLIFFブラウザの右上に表示される閉じるボタンを押すと、LIFFブラウザを閉じることができます。

![最小化したLIFFブラウザを閉じる](https://developers.line.biz/media/liff/minimizing-liff-app/close-minimized-liff-browser-line-15-20-0-or-later-ja.png)

## LIFFブラウザのアイコン表示の優先順位 

LIFFブラウザは、最小化するとアイコンで表示されます。アイコン表示の優先順位は以下のとおりです。

1. チャネルアイコン：LINEログインチャネルのチャネルアイコン
1. ファビコン：LIFFアプリのファビコン
1. 共通アイコン：リンクマークのアイコン
