# ボットを作成する

このガイドでは、Messaging APIを使ってLINEボットを作成する方法を説明します。

## 始める前に 

ボットの設定と作成を始める前に、以下を用意していることを確認します。

- ボット用の[Messaging APIチャネル](https://developers.line.biz/ja/docs/messaging-api/getting-started/)
- ボットをホストするサーバー

## LINE Developersコンソールでの設定 

[チャネルアクセストークン](https://developers.line.biz/ja/docs/messaging-api/building-bot/#issue-a-channel-access-token)を発行し、[Webhook URL](https://developers.line.biz/ja/docs/messaging-api/building-bot/#setting-webhook-url)を設定します。チャネルアクセストークンは、ボットがMessaging APIを呼び出すために必要です。Webhook URLは、LINEプラットフォームからのWebhookペイロードをボットが受信するために必要です。設定が完了したら、[LINE公式アカウントを友だち追加し](https://developers.line.biz/ja/docs/messaging-api/building-bot/#add-your-line-official-account-as-friend)、[動作を確認](https://developers.line.biz/ja/docs/messaging-api/building-bot/#confirm-webhook-behavior)します。

### チャネルアクセストークンを準備する 

チャネルアクセストークンをまだ持っていない場合は、発行してください。チャネルアクセストークンは、Messaging APIで使用するアクセストークンです。以下のいずれかのトークンを発行できます。

- [任意の有効期間を指定できるチャネルアクセストークン（チャネルアクセストークンv2.1）](https://developers.line.biz/ja/docs/basics/channel-access-token/#user-specified-expiration)（推奨）
- [ステートレスチャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/#stateless-channel-access-token)
- [短期のチャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/#short-lived-channel-access-token)
- [長期のチャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/#long-lived-channel-access-token)

### Webhook URLを設定する 

Webhook URLはボットサーバーのエンドポイントで、Webhookペイロードの送信先です。なお、Webhook URLに設定できるボットサーバーのエンドポイントは1つだけです。

Webhook URLは、以下の手順で設定してください。

1. [LINE Developersコンソール](https://developers.line.biz/console/)にログインし、Messaging APIのチャネルがあるプロバイダーをクリックします。
1. Messaging APIのチャネルをクリックします。
1. ［**Messaging API設定**］タブをクリックします。
1. ［**Webhook URL**］の［**編集**］をクリックし、Webhook URL（LINEプラットフォームからボットにイベントを送信する際の送信先URL）を入力して、［**更新**］をクリックします。

   Webhook URLにはHTTPSを使用し、一般的なブラウザ等で広く信頼されている認証局で発行されたSSL/TLS証明書を設定する必要があります。また、自己署名証明書は利用できない点に注意してください。SSL/TLSの設定で問題が発生した場合は、SSL/TLS証明書チェーンが完全で、中間証明書がサーバーに正しくインストールされていることを確かめてください。

1. ［**検証**］をクリックします。設定したWebhook URLでWebhookイベントを受け取ると、「**成功**」と表示されます。
1. ［**Webhookの利用**］を有効にします。

![](https://developers.line.biz/media/messaging-api/build-bot/webhook-url-example-com.png)

### LINE公式アカウントを友だち追加する 

Messaging APIチャネルに紐づいたLINE公式アカウントをLINEアカウントに友だち追加しておくと、後で検証できます。[LINE Developersコンソール](https://developers.line.biz/console/)の［**Messaging API設定**］タブにあるQRコードを読み込むと、簡単に追加できます。

### 長期のチャネルアクセストークン利用時にAPIの呼び出し元を制限する（任意） 

長期のチャネルアクセストークンを利用する場合、LINEプラットフォームのAPIを呼び出すことができるサーバーを、IPアドレスで制限できます。

IPアドレスを登録するには、[LINE Developersコンソール](https://developers.line.biz/console/)のチャネル設定の［**セキュリティ設定**］タブを開きます。IPアドレスは、1つずつ個別に登録するか、CIDR（Classless Inter-Domain Routing）記法を使用して、ネットワークアドレスで登録もできます。

なおMessaging APIで使用するチャネルアクセストークンは、[任意の有効期間を指定できるチャネルアクセストークン（チャネルアクセストークンv2.1）](https://developers.line.biz/ja/docs/basics/channel-access-token/#user-specified-expiration)を推奨しています。

![](https://developers.line.biz/media/messaging-api/build-bot/security-settings-input-ja.png)

## Webhookの動作を確認する 

ユーザーがLINE公式アカウントを友だち追加したり、LINE公式アカウントにメッセージを送ったりすると、LINEプラットフォームからボットサーバーにHTTP POSTリクエストが送信されます。リクエスト先は、[LINE Developersコンソール](https://developers.line.biz/console/)の［**Messaging API設定**］タブで登録した［**Webhook URL**］です。リクエストにはWebhookイベントオブジェクトが含まれ、ヘッダーには署名が含まれます。

ここでは、サーバーが[Webhookイベントを受信](https://developers.line.biz/ja/docs/messaging-api/building-bot/#receive-webhook-events)できるかを確認する方法について説明します。

### Webhookイベントを受信する 

ボットサーバーがWebhookイベントを受信しているかを確認するには、まず、[先の手順](https://developers.line.biz/ja/docs/messaging-api/building-bot/#set-up-bot-on-line-developers-console)で追加したLINE公式アカウントをブロックします。そして、ボットサーバーがLINEプラットフォームから[フォロー解除イベント](https://developers.line.biz/ja/reference/messaging-api/#unfollow-event)を受信したことをサーバーのログで確認します。以下はログの例です。

```sh
2017-07-21T09:18:46.755256+00:00 app[web.1]: 2017-07-21 09:18:46.737  INFO 4 --- [io-13386-exec-2] c.e.bot.spring.KitchenSinkController     : unfollowed this bot: UnfollowEvent(source=UserSource(userId=Uxxxxxxxxxx...), timestamp=2017-07-21T09:18:46.031Z)
```

同様のログが表示された場合、ボットサーバーはLINEプラットフォームからWebhookイベントを受信しています。ログを確認した後、LINE公式アカウントのブロックを解除してください。

## LINE Official Account Managerでの設定 

[LINE Official Account Manager](https://manager.line.biz/)は、LINE公式アカウントを管理するためのツールです。Messaging APIが提供する機能を利用できるほか、[ビジネスプロフィールをカスタマイズ](https://developers.line.biz/ja/docs/messaging-api/building-bot/#customize-profile)してユーザー体験を向上させたり、LINE VOOMの投稿を作成したりなど、さまざまな機能を利用できます。

LINE公式アカウントのすべての機能については、『[LINEヤフー for Business](https://www.lycbiz.com/jp/)』を参照してください。

<!-- tip start -->

**あいさつメッセージと応答メッセージ**

チャネルの［**Messaging API設定**］タブで［**あいさつメッセージ**］や［**応答メッセージ**］の設定が［**有効**］になっていると、ユーザーがLINE公式アカウントを友だち追加したときや、メッセージを送ってきたときに、LINE公式アカウントが自動で応答します。この［**あいさつメッセージ**］と［**応答メッセージ**］は、チャネルを作成したときにデフォルトの設定が［**有効**］になっています。

応答の処理はMessaging APIで行うのであいさつメッセージや応答メッセージを自動で送りたくないという場合は、[LINE Official Account Manager](https://manager.line.biz/)で、［**あいさつメッセージ**］や［**応答メッセージ**］の設定を［**オフ**］にしてください。

友だち追加されたときの応答はあいさつメッセージに任せて、それ以外の応答をMessaging APIで行う、というように併用することも可能です。しかし、ユーザーに送られたメッセージがあいさつメッセージや応答メッセージによる応答なのか、それともMessaging APIを使ったボットによる応答なのか、開発者自身が混乱してしまうことがあります。Messaging APIを使って初めてLINEボットを作成するときは、［**あいさつメッセージ**］や［**応答メッセージ**］の設定を［**オフ**］にしておくことをお勧めします。

<!-- tip end -->

### ビジネスプロフィールをカスタマイズする 

ビジネスプロフィールには、LINE公式アカウントの基本情報を設定します。プロフィール画像、背景画像、ボタン、パーツをカスタマイズできます。プロフィールの設定は、LINE Official Account Managerから行います。

プロフィールのカスタマイズについて詳しくは、『LINEヤフー for Business』の「[プロフィール](https://www.lycbiz.com/jp/manual/OfficialAccountManager/profile/)」を参照してください。

### あいさつメッセージを設定する（任意） 

ユーザーがLINE公式アカウントを初めて友だち追加した際に、あいさつメッセージを送信できます。あいさつメッセージを設定するには、[LINE Developersコンソール](https://developers.line.biz/console/)のチャネル設定の［**Messaging API設定**］タブに表示されている［**あいさつメッセージ**］の［**編集**］をクリックし、LINE Official Account Managerを開きます。LINE Official Account Manager上で、あいさつメッセージを設定します。別の方法として、Webhook[フォローイベント](https://developers.line.biz/ja/reference/messaging-api/#follow-event)を受け取ってからユーザーへプログラム的に応答することもできます。

### 応答メッセージを設定する（任意） 

ユーザーがLINE公式アカウントにメッセージを送信した際に、応答メッセージを送信できます。応答メッセージを設定するには、[LINE Developersコンソール](https://developers.line.biz/console/)のチャネル設定の［**Messaging API設定**］タブに表示されている［**応答メッセージ**］の［**編集**］をクリックし、LINE Official Account Managerを開きます。LINE Official Account Manager上で、応答メッセージを設定します。ただし、Messaging APIを使用すれば、Webhookイベントの内容に合わせた応答を返すようにボットをプログラムできるため、より多くの処理を実行できます。

## 次のステップ 

ボットを設定すると、LINE公式アカウントがユーザーからのメッセージを受信したり、ユーザーにメッセージを送信したりできます。また、リッチメニューやクイックリプライを利用することで、パーソナライズされた体験を提供できます。Messaging APIで利用できる機能について詳しくは、『[Messaging APIドキュメント](https://developers.line.biz/ja/docs/messaging-api/)』の各ページを参照してください。
