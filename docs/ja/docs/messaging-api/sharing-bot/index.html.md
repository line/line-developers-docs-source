# LINE公式アカウントの友だちを増やす

LINE公式アカウントを作成したら、次はLINE公式アカウントを宣伝して友だちを増やしましょう。LINE公式アカウントをユーザーに露出する方法を紹介します。

- [QRコードを使う](https://developers.line.biz/ja/docs/messaging-api/sharing-bot/#use-qr-code)
- [LINE公式アカウントのLINE IDをシェアする](https://developers.line.biz/ja/docs/messaging-api/sharing-bot/#share-the-line-id-of-your-line-official-account)
- [［友だち追加］ボタンまたはリンクを使う](https://developers.line.biz/ja/docs/messaging-api/sharing-bot/#use-the-add-friend-button-or-link)
- [ユーザーからLINE上の友だちにLINE公式アカウントをおすすめしてもらう](https://developers.line.biz/ja/docs/messaging-api/sharing-bot/#encourage-users-to-recommend-your-bot-to-friends-on-line)
- [LINEログイン時にLINE公式アカウントの友だち追加を促す](https://developers.line.biz/ja/docs/messaging-api/sharing-bot/#prompt-users-to-add-your-line-official-account-at-line-login)

## QRコードを使う 

LINE公式アカウントのQRコードをウェブサイトや印刷物でシェアしましょう。ユーザーはQRコードを読み取るだけで、LINE公式アカウントを友だち追加できます。QRコードは、[LINE Developersコンソール](https://developers.line.biz/console/)や[LINE Official Account Manager](https://manager.line.biz/)から取得できます。

LINE Developersコンソールでは、チャネル設定の［**Messaging API設定**］タブをクリックします。

![](https://developers.line.biz/media/messaging-api/sharing-bot/qr-code-console-ja.png)

LINE Official Account Managerでは、［**ホーム**］>［**友だちを増やす**］>［**友だち追加ガイド**］>［**友だち追加QRコードを作成**］をクリックします。HTMLスニペットをコピーして、ご自身のサイトに貼り付けるとQRコードが表示されます。

![](https://developers.line.biz/media/messaging-api/sharing-bot/qr-code-oa-manager-ja.png)

## LINE公式アカウントのLINE IDをシェアする 

LINE公式アカウントのLINE IDをシェアすると、ユーザーはLINE上でLINE公式アカウントを検索して友だち追加できます。LINE公式アカウントのLINE IDは、[LINE Official Account Manager](https://manager.line.biz/)のヘッダーで確認できます。アットマーク（@）で始まる文字列がLINE公式アカウントのLINE IDです。

また、プレミアムIDを購入することで、ユーザーが覚えやすいカスタマイズされたLINE IDを作成することができます。プレミアムIDについて詳しくは、『LINEヤフー for Business』の「[料金プラン](https://www.lycbiz.com/jp/service/line-official-account/plan/)」を参照してください。

![](https://developers.line.biz/media/messaging-api/sharing-bot/oa-manager-line-id.png)

## ［友だち追加］ボタンまたはリンクを使う 

アプリまたはウェブサイトにボタンまたはリンクを追加すると、ユーザーはデバイスからワンタップでLINE公式アカウントを友だち追加できます。以下のボタンまたはリンクを追加できます。

- [LINE Social Pluginsの［友だち追加］ボタン](https://developers.line.biz/ja/docs/messaging-api/sharing-bot/#add-friend-button-by-line-social-plugins)
- [LINE Official Account Managerの［友だち追加］ボタン](https://developers.line.biz/ja/docs/messaging-api/sharing-bot/#add-friend-button-by-the-line-manager)
- [プロフィールページを開くLINE URLスキーム](https://developers.line.biz/ja/docs/messaging-api/sharing-bot/#line-url-scheme-for-profile-page)

### LINE Social Pluginsの［友だち追加］ボタン 

LINE Social Pluginsで、[［友だち追加］ボタン](https://developers.line.biz/ja/docs/line-social-plugins/install-guide/using-add-friend-buttons/)用のコードを生成します。コードをアプリやウェブサイトにコピー＆ペーストするだけで［**友だち追加**］ボタンを追加できます。このボタンは複数の言語で利用できます。また、LINE公式アカウントの友だち数を表示するようにボタンを設定したり、LINE公式アカウントのホームへのリンクを追加したりできます。LINE公式アカウントを友だち追加すると、ボタンテキストが「友だち追加」から「友だち済み」に変化します。

LINE Social Pluginsが生成する［**友だち追加**］ボタンを利用するには、「[ボタンを作成](https://developers.line.biz/ja/docs/line-social-plugins/install-guide/using-add-friend-buttons/#create-button)」の手順を参照してください。

![](https://developers.line.biz/media/messaging-api/sharing-bot/add-friend-button-types.png)

### LINE Official Account Managerの［友だち追加］ボタン 

[LINE Official Account Manager](https://manager.line.biz/)で［**友だち追加**］用のコードを生成します。［**ホーム**］ > ［**友だちを増やす**］ > ［**友だち追加ガイド**］>［**ボタンを作成**］をクリックします。HTMLコードをウェブサイトにコピー＆ペーストすると、ボタンが表示されます。

![](https://developers.line.biz/media/messaging-api/sharing-bot/add-friend-button-oa-manager-ja.png)

### プロフィールページを開くLINE URLスキーム 

ウェブアプリやネイティブアプリで以下のLINE URLスキームを使って、LINE公式アカウントの友だち追加を促します。iOS版LINEやAndroid版LINEでタップすると、LINE公式アカウントのビジネスプロフィールが表示されます。

- https://line.me/R/ti/p/`{Percent-encoded LINE ID}`&nbsp;

たとえば、[`https://line.me/R/ti/p/%40linedevelopers`](https://line.me/R/ti/p/%40linedevelopers)を開くと、LINE DevelopersのLINE公式アカウントのビジネスプロフィールページが表示されます。このLINE URLスキームについて詳しくは、「[LINE公式アカウントをシェアする](https://developers.line.biz/ja/docs/messaging-api/using-line-url-scheme/#sharing-line-official-account)」を参照してください。

![](https://developers.line.biz/media/messaging-api/sharing-bot/add-line-developers-oa-ja.png)

## ユーザーからLINE上の友だちにLINE公式アカウントをおすすめしてもらう 

ユーザーがLINE公式アカウントを友だち追加済みである場合は、以下のLINE URLスキームを使ってユーザーからLINE上の友だちにLINE公式アカウントをおすすめしてもらうことができます。

- https://line.me/R/nv/recommendOA/`{LINE ID with @}`&nbsp;

たとえば、[リッチメニュー](https://developers.line.biz/ja/docs/messaging-api/using-rich-menus/)または[テンプレートメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#template-messages)の[URIアクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#uri-action)にこのURLスキームを指定します。このLINE URLスキームついて詳しくは、「[LINE公式アカウントをシェアする](https://developers.line.biz/ja/docs/messaging-api/using-line-url-scheme/#sharing-line-official-account)」を参照してください。

![](https://developers.line.biz/media/messaging-api/sharing-bot/recommend-line-developers-rich-menu.png)

## LINEログイン時にLINE公式アカウントの友だち追加を促す 

ウェブアプリやネイティブアプリで[LINEログイン](https://developers.line.biz/ja/docs/line-login/overview/)を利用している場合は、LINE公式アカウントをLINEログインのチャネルにリンクすることによって、ユーザーがログインするときにLINE公式アカウントを友だち追加するオプションを表示できます。権限の付与に同意する画面にオプションを追加するか、ユーザーが同意した後で、LINE公式アカウントの追加画面を別途開くかを選択できます。

LINE公式アカウントをLINEログインチャネルにリンクする方法について詳しくは、『LINEログインドキュメント』の「[LINEログインしたときにLINE公式アカウントを友だち追加する（友だち追加オプション）](https://developers.line.biz/ja/docs/line-login/link-a-bot/)」を参照してください。

![bot_prompt=normalの場合は、同意画面に友だち追加するためのオプションが表示されます。bot_prompt=aggressiveの場合は、ユーザーが同意した後で友だち追加するためのオプションが表示されます。](https://developers.line.biz/media/line-login/link-a-bot/bot-prompt-ja.png)

## 関連ページ 

- [LINE URLスキームでLINEの機能を使う](https://developers.line.biz/ja/docs/messaging-api/using-line-url-scheme/)
- [Messaging APIリファレンス](https://developers.line.biz/ja/reference/messaging-api/)
- [LINE Social Plugins](https://developers.line.biz/ja/docs/line-social-plugins/)
- [LINE Official Account Manager](https://manager.line.biz/)
