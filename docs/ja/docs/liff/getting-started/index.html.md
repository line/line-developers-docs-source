# チャネルを作成する

LIFFアプリを開発するには、まず[LINE Developersコンソール](https://developers.line.biz/console/)でプロバイダーとチャネルを作成します。

## LINE Developersコンソールへログインする 

プロバイダーとチャネルを作成するため、まずはLINE Developersコンソールへログインします。ログイン方法について詳しくは、「[LINE Developersコンソールへのログイン](https://developers.line.biz/ja/docs/line-developers-console/login-account/)」を参照してください。

## プロバイダーとチャネルを作成する 

LINE Developersコンソールへログインできたら、プロバイダーとチャネルを作成します。

### 1. プロバイダーを作成する 

適当なプロバイダーがある場合は、「[2. チャネルを作成する](https://developers.line.biz/ja/docs/liff/getting-started/#step-two-create-channel)」へ進みます。

1. ホーム画面の［**新規プロバイダー作成**］をクリックします。

   <!-- note start -->

   **[新規プロバイダー作成]が見つからない場合**

   プロバイダーを作成済みの場合は、ホーム画面に［**新規プロバイダー作成**］は表示されません。別のプロバイダーを作成する場合は、［**プロバイダー**］セクションの［**作成**］をクリックします。

   ![プロバイダーの作成ボタン](https://developers.line.biz/media/liff/getting-started/providers-section-ja.png)

   <!-- note end -->

1. ［**新規プロバイダー作成**］画面で任意の［**プロパイダー名**］を入力し、［**作成**］をクリックします。

   **プロバイダー**は、LINEプラットフォームを通じてサービスを提供する個人、企業、またはそのほかの組織を意味する情報です。プロバイダー名には、あなたの名前や企業名を入力してください。

   ![プロバイダー作成画面](https://developers.line.biz/media/liff/getting-started/create-provider-ja.png)

### 2. チャネルを作成する 

**チャネル**は、LINEプラットフォームが提供する機能を、プロバイダーが開発するサービスで利用するための通信路です。チャネルを作成するには、名前、説明文、およびアイコン画像が必要です。

LIFFアプリを追加できるチャネルタイプは以下の2つです。

| 種類 | 説明 |
| --- | --- |
| [LINEログイン](https://developers.line.biz/ja/docs/line-login/) | LIFFアプリを作成する場合や、次のステップで[LIFFスターターアプリを試してみる](https://developers.line.biz/ja/docs/liff/trying-liff-app/)場合、[Create LIFF AppでLIFFアプリの開発環境を構築する](https://developers.line.biz/ja/docs/liff/cli-tool-create-liff-app/)場合は、こちらのチャネルを作成してください。 |
| [LINEミニアプリ](https://developers.line.biz/ja/docs/line-mini-app/)  | [LINEミニアプリ](https://developers.line.biz/ja/docs/line-mini-app/quickstart/)でLIFFのアプリを作成する場合は、こちらのチャネルを作成してください。 |

<!-- tip start -->

**LINEミニアプリとしての作成を推奨します**

今後、LIFFとLINEミニアプリは、ブランド統合を予定しています。この統合により、LIFFはLINEミニアプリに統合されます。そのため、LIFFアプリを新規作成する際は、LINEミニアプリとして作成することを推奨します。詳しくは、「[2025年2月12日のニュース](https://developers.line.biz/ja/news/2025/02/12/line-mini-app/)」を参照してください。

<!-- tip end -->

ここでは、次のステップで[LIFFスターターアプリを試してみる](https://developers.line.biz/ja/docs/liff/trying-liff-app/)ことを想定して、LINEログインのチャネルを作成します。チャネルを作成するプロバイダーをクリックし、LINEログインのチャネルを作成してください。既に適当なLINEログインのチャネルが存在していた場合は、そのチャネルを選択しても構いません。チャネルの作成方法について詳しくは、「[チャネルを作成する](https://developers.line.biz/ja/docs/line-developers-console/overview/#creating-a-channel)」を参照してください。

<!-- note start -->

**チャネル名の制限について**

チャネル名には、「LINE」またはそれに類する文字列は含められません。

<!-- note end -->

<!-- note start -->

**チャネルのアプリタイプについて**

LIFFアプリを開発する場合、チャネルのアプリタイプは［**ウェブアプリ**］を選択してください。

<!-- note end -->

<!-- note start -->

**LINEログインとLINEミニアプリ以外のチャネルにはLIFFアプリを追加できません**

以下のチャネルタイプにはLIFFアプリは追加できません。

- Messaging API
- ブロックチェーンサービス

以前は、Messaging APIチャネルやブロックチェーンサービスチャネルに、LIFFアプリを追加することができました。しかし、すでにMessaging APIチャネルやブロックチェーンサービスチャネルに追加したLIFFアプリの場合、今後LIFFに追加される新機能は利用できません。詳しくは、以下のニュースを参照してください。

- 2020年2月5日のニュース「[Messaging APIのチャネルにはLIFFアプリを追加できなくなりました](https://developers.line.biz/ja/news/2020/02/05/liff-channel-type/)」
- 2021年7月20日のニュース「[ブロックチェーンサービスのチャネルにはLIFFアプリを追加できなくなりました](https://developers.line.biz/ja/news/2021/07/20/liff-cannot-be-used-with-blockchain-service-channels/)」

<!-- note end -->

#### チャネルとプロバイダーの連携に関する注意点 

一度作成したチャネルを、後から他のプロバイダーに移動することはできません。

LINEログインチャネルとMessaging APIチャネルを連携するサービスを開発する場合は、これらのチャネルを同じプロバイダーの配下に作成してください。

開発者が提供するサービスを利用するLINEユーザーには、プロバイダーごとに異なるユーザーIDが割り当てられます。異なるプロバイダーに属するチャネル間では、ユーザーIDを利用して同一ユーザーであることを確認できません。

![](https://developers.line.biz/media/line-developers-console/different-user-ids.png)

<!-- warning start -->

**チャネル作成時に特に注意が必要なケース**

たとえば、以下のような場合には特に注意してください。

- チャネルとプロバイダーを別々の個人または企業が管理している。
- 1つのプロバイダー配下に、相互に関係がないサービスや企業のチャネルを作成する。
- チャネルの運用ツール等を運営するサービス（企業）が管理するプロバイダーの配下にチャネルを作成する。

このようなケースでは、後からチャネルをプロバイダー間で移動できないことや、プロバイダーごとに異なるユーザーIDが割り当てられることに起因して、将来的に問題が発生する可能性があります。そのリスクを十分検討した上で、適切なプロバイダーの配下にチャネルを作成してください。

<!-- warning end -->

## 次のステップ 

これで、LIFFアプリを追加するチャネルが作成されました。続いて、以下のいずれかを行います。

- [LIFFスターターアプリを試してみる](https://developers.line.biz/ja/docs/liff/trying-liff-app/)
- [LIFFアプリを開発する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/)
