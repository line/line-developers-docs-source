# メールや通知センターでお知らせを受け取る

[LINE Developersコンソール](https://developers.line.biz/console/)の通知センターでは、リアルタイムでさまざまな更新情報を受け取ることができます。このページでは、受信できる通知の種類や通知を受信するための設定方法について説明します。

## 受信できる通知の種類 

受信できる通知の種類は以下のとおりです。

| 通知の種類 | 概要 |
| --- | --- |
| [重要なお知らせ](https://developers.line.biz/ja/docs/line-developers-console/notification/#notification-important-announcements) | LINEプラットフォームに関する重要なお知らせ |
| [アクティビティ](https://developers.line.biz/ja/docs/line-developers-console/notification/#notification-activity) | あなたのLINE Developersコンソールでのアクティビティ |
| [ニュース](https://developers.line.biz/ja/docs/line-developers-console/notification/#notification-news) | LINE Developersサイトからのお知らせ |
| [チャネルアクティビティ](https://developers.line.biz/ja/docs/line-developers-console/notification/#notification-channel-activity) | あなたがAdmin権限を持つチャネルに関するアクティビティ |
| [プロバイダーアクティビティ](https://developers.line.biz/ja/docs/line-developers-console/notification/#notification-provider-activity) | あなたがAdmin権限を持つプロバイダーに関するアクティビティ |

### 重要なお知らせ 

LINEプラットフォームに関する重要なお知らせを通知します。

例：「[グループ再編に伴う情報利用に関する通知（シェアターゲットピッカー）](https://developers.line.biz/ja/news/2023/09/21/notice-concerning-use-of-information-for-liff/)」

### アクティビティ 

あなたのLINE Developersコンソールでのアクティビティを通知します。通知されるアクティビティは以下のとおりです。

| 操作の種類 | アクティビティの詳細 |
| --- | --- |
| プロバイダーに関する操作 | <ul><li>プロバイダーの作成</li><li>プロバイダーの削除</li><li>プロバイダーへの招待メールの送信</li><li>あなたの開発者アカウントへのプロバイダーの権限付与</li></ul> |
| チャネルに関する操作 | <ul><li>チャネルの作成</li><li>チャネルの削除</li><li>チャネルへの招待メールの送信</li><li>あなたの開発者アカウントへのチャネルの権限付与</li></ul> |

### ニュース 

LINE Developersサイトからのお知らせを通知します。[ニュース](https://developers.line.biz/ja/news/)が公開されると、ニュースタイトルが英語で通知されます。

### チャネルアクティビティ 

あなたがAdmin権限を持つチャネルに関するアクティビティを通知します。通知されるアクティビティは以下のとおりです。

| チャネルの種類 | アクティビティの詳細 |
| --- | --- |
| チャネル全般 | <ul><li>チャネルの削除</li><li>チャネルへの新しいメンバーの追加</li></ul> |
| LINEミニアプリチャネル | <ul><li>審査によるチャネルのステータスの更新</li><li>LINEミニアプリの検索の有効化</li><li>チャネルに添付された審査用ファイルの自動削除（審査終了時やアップロード後30日が経過しても審査が申請されない場合）</li></ul> |

### プロバイダーアクティビティ 

あなたがAdmin権限を持つプロバイダーに関するアクティビティを通知します。通知されるアクティビティは以下のとおりです。

- プロバイダーの削除
- プロバイダーへの新しいメンバーの追加

## 通知の種類や受信方法を設定する 

受け取りたい通知の種類や受信方法を設定できます。LINE Developersコンソールのプロフィールにアクセスし、［**設定**］セクションで、通知オプションの横にあるトグルボタンをオン（右）またはオフ（左）にして、その設定を有効または無効にします。なお、［**重要なお知らせ**］をオフにすることはできません。

![LINE Developersコンソールのプロフィールの設定セクション](https://developers.line.biz/media/line-developers-console/console-notification-center-settings-ja.png)

<!-- note start -->

**通知メール**

通知メールを受信するには、LINE Developersコンソールのプロフィールに登録されているメールアドレスが認証済みである必要があります。プロフィールのメールアドレスに［**未認証**］と表示されていた場合は、［**認証用のリンクを取得**］をクリックして、メールアドレスの認証を行ってください。

通知センターの設定で有効にした通知のみがメールで届きます。

<!-- note end -->

## 通知を確認する 

通知センターを表示するには、LINE Developersコンソールの右上にあるベルのアイコンをクリックします。未読の通知がある場合は、アイコンの横に緑色の点が表示されます。

![LINE Developersコンソールの通知センターのアイコン](https://developers.line.biz/media/news/console-notification-center-icon.png)

アイコンをクリックすると、通知センターが表示されます。ここでは、最近の更新やアクティビティを確認することができます。

![LINE Developersコンソールの通知センターのドロップダウンメニュー](https://developers.line.biz/media/news/notification-center-drop-down-ja.png)
