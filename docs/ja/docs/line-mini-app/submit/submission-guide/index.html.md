# 審査を依頼する

LINEミニアプリチャネルを作成した段階では、LINEミニアプリは未認証ミニアプリであり、一部機能が制限されています。開発したLINEミニアプリを認証済ミニアプリにするには、LINEヤフー株式会社による審査を受ける必要があります。このページでは、審査の依頼について説明します。

<!-- tip start -->

**台湾またはタイ向けのLINEミニアプリの審査について**

サービスを提供する国や地域が台湾またはタイの場合は、[認証プロバイダー](https://developers.line.biz/ja/docs/line-developers-console/overview/#certified-provider)配下のLINEミニアプリチャネルのみ認証審査を申請できます。認証プロバイダーになるための申請方法について詳しくは、以下を参照してください。

- 台湾：[LINE Biz-Solutions](https://tw.linebiz.com/service/other-solutions/line-mini-app/)
- タイ：[LINE for Business](https://lineforbusiness.com/th/service/mini-app)

<!-- tip end -->

## LINEミニアプリの審査依頼前の確認事項 

LINEミニアプリの審査を依頼する前に、以下の内容を確認してください。

- LINEミニアプリが、すべてのガイドラインやルールに従っていること。<br>特に、以下のガイドラインおよびルールを確認してください。
  - [LINEミニアプリのアイコンの仕様とガイドライン](https://developers.line.biz/ja/docs/line-mini-app/design/line-mini-app-icon/)
  - [ランドスケープモードのセーフエリア](https://developers.line.biz/ja/docs/line-mini-app/design/landscape/)
  - [読み込み中アイコン](https://developers.line.biz/ja/docs/line-mini-app/design/loading-icon/)
  - [カスタムアクションボタンを実装する](https://developers.line.biz/ja/docs/line-mini-app/develop/share-messages/)
  - [パフォーマンスガイドライン](https://developers.line.biz/ja/docs/line-mini-app/develop/performance-guidelines/)
- LINEミニアプリが、「[LINEミニアプリポリシー](https://terms2.line.me/LINE_MINI_App?lang=ja)」を遵守していること。
- [LINE Developersコンソール](https://developers.line.biz/console/)でLINEミニアプリチャネルに登録した情報が、正しく、最新であること。
  - プロバイダー名は、「サービス提供者」と同一であること。
  - 「[チャネル説明](https://developers.line.biz/ja/docs/line-mini-app/discover/console-guide/#channel-description)」に、正しいサービス内容が記載されていること。
  - プライバシーポリシーでは、ユーザー情報を取得する会社をプロバイダー名と同じ会社に設定する必要があります。
- 本番用のチャネルのLIFF URLと、審査用のチャネルのLIFF URLが同じサービスを反映しているかどうかを確認してください。
  - 審査時、LINEヤフー株式会社は審査用のチャネルのLIFF URLを確認します。チャネルやLIFF内の各種設定は自動的に審査用のチャネルへコピーされ、提供されます。ただし、審査用チャネルのLIFF URLが本番用のチャネルのLIFF URLと同じサービス内容を提供しているか、念のために事前確認してください。

### 審査期間について 

LINEヤフー株式会社による審査が終了するまでに、1～2週間程度かかります。却下された場合、再申請と再審査にはさらに数日かかります。審査の完了日は事前に指定することはできません。審査にはお時間がかかりますので、あらかじめご了承ください。

### 複数のLINEミニアプリの審査を希望する場合 

複数のLINEミニアプリ（同一パッケージの複数、同一ブランドの複数など）の審査を同時に依頼する場合は、重複を避け、審査時間を短縮するために、以下のワークフローに従うことを推奨します。

1. まずは1つのLINEミニアプリのみ審査を依頼します。
2. そのLINEミニアプリが承認されたら、一括して他のLINEミニアプリの審査を依頼します。

## 審査のプロセス 

審査の大まかなプロセスは、以下のとおりです。

### 1. LINE Developersコンソールで審査申請する 

[LINE Developersコンソール](https://developers.line.biz/console/)の［**審査申請**］タブで必要な情報を入力して、審査を依頼します。

LINEヤフー株式会社による審査が終了すると、[LINE Developersコンソール](https://developers.line.biz/console/)に審査結果が表示され、LINE Developersコンソールに登録したメールアドレスにメールで審査結果が通知されます。

審査対象のLINEミニアプリにベーシック認証によるアクセス制限をかけている場合は、審査を依頼する際に［**審査申請**］タブの［**審査のための補足資料**］でユーザー名とパスワードをお知らせください。詳しくは、「[公開前のLINEミニアプリにベーシック認証でアクセス制限をかける](https://developers.line.biz/ja/docs/line-mini-app/develop/develop-overview/#use-basic-authentication)」を参照してください。

#### 審査に関する注意点 

- 審査依頼後、審査が始まる前であれば、［**審査申請**］タブの［**審査申請をキャンセルする**］ボタンからキャンセルできます。
- LINEヤフー株式会社が審査を開始したら、審査依頼をキャンセルしたり、入力した情報を変更したりできません。
- 審査が開始されてステータスが「審査中」になると、審査用チャネルのLIFF URLにアクセスできます。

#### 予約、支払、注文などのアクションを含むサービスの場合 

予約、支払、注文などのアクションを含むサービスの場合は、審査の申し込みを送信するときに［**審査のための補足資料**］にテストシナリオ（アカウント、製品、店舗など）を入力する必要があります。

#### チャネル説明について 

LINEヤフー株式会社による審査は、[LINE Developersコンソール](https://developers.line.biz/console/)の［**チャネル基本設定**］タブにある［**チャネル説明**］に記載された内容をもとに行われます。このため、以下の例を参考に、正しいサービス内容を記載してください。

|  | チャネル名 | チャネル説明 |
| --- | --- | --- |
| 悪い例 | LINE FRIENDSストア | LINE FRIENDSストアは、LINEキャラクターグッズのお店です。 |
| 良い例 | LINE FRIENDSストア | LINE FRIENDSストアにおいて、事前注文・決済ができ、店舗で商品を受け取れるモバイルオーダーサービスです。 |

［**チャネル説明**］について詳しくは、「[チャネル説明](https://developers.line.biz/ja/docs/line-mini-app/discover/console-guide/#channel-description)」を参照してください。

#### アプリ内課金を利用する場合 

[アプリ内課金](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/overview/)を利用する場合は、事前に、[アプリ内課金の利用申請](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/request-iap-review/)が必要です。

アプリ内課金の利用申請が承認されたら、［**審査申請**］タブ内の［**アプリ内課金 公開申請**］のトグルボタンをオンにして、審査を申請してください。アプリ内課金の利用申請が未承認の場合は、トグルボタンをオンにしても、認証審査の申請はできません。

![](https://developers.line.biz/media/line-mini-app/in-app-purchase/in-app-purchase-toggle-ja.png)

アプリ内課金の審査中は、認証審査の申請はできません。

また、認証審査中は、アプリ内課金の利用申請はできません。

### 2. 承認された後の操作 

審査で承認された後に行う作業は、[初めて審査を受けた場合](https://developers.line.biz/ja/docs/line-mini-app/submit/submission-guide/#first-time)と、[すでに認証済ミニアプリとして公開中の場合](https://developers.line.biz/ja/docs/line-mini-app/submit/submission-guide/#verified-mini-app)とで異なります。

#### 初めて審査を受けた場合 

LINEミニアプリが承認されると、チャネルのステータスが自動的に「承認済み」になった後、すぐに「反映済み」になります。[LINE Developersコンソール](https://developers.line.biz/console/)の［**審査申請**］タブにある［**検索可能にする**］ボタンを使うと、LINE内でLINEミニアプリが検索できる状態になります。

「反映済み」になっても、LINE内での検索がまだ有効になっていないため、ユーザーがサービスを検索して見つけることはできません。

検索を可能にしたいタイミングで［**検索可能にする**］ボタンを押すことで、LINE内でLINEミニアプリの検索が可能になります。ただし、ステータスが「反映済み」になってから30日以内（土日祝日を含む）に手動で検索可能にしなかった場合は、31日目の午前9:00（JST）に自動的に検索可能となります。

たとえば、8月1日にLINEミニアプリのステータスが「反映済み」になった場合、8月31日の午前9:00（JST）に自動的に検索可能となります。

LINEミニアプリの検索が有効になると、LINEミニアプリチャネルのステータスは「審査前」に戻り、設定の変更や審査の再申請が改めて可能になります。このとき、設定を変更しても、再度審査を通過して［**変更内容を公開する**］ボタンを押すまでは、公開中のLINEミニアプリに影響はありません。

<!-- note start -->

**ステータス変更に若干の遅れが生じる場合があります**

31日目の午前9:00（JST）に自動的にステータス変更の処理が開始されますが、完了までには1～2時間の遅れが生じる場合があります。

<!-- note end -->

#### すでに認証済ミニアプリとして公開中の場合 

すでに公開中のLINEミニアプリの場合は、作業の流れが少し異なります。

LINEミニアプリが承認されると、チャネルのステータスが「承認済み」に変わります。[LINE Developersコンソール](https://developers.line.biz/console/)の［**審査申請**］タブにある［**変更内容を公開する**］ボタンを使って、手動でチャネルのステータスを「反映済み」に変更する必要があります。

ステータスが「反映済み」になると、審査をリクエストした際に行った変更が、公開中のチャネルおよびそのチャネルのLIFF（LINEミニアプリ名、チャネル設定、LIFF設定など）に反映されます。

公開したいタイミングで［**変更内容を公開する**］ボタンを押すことで、ステータスが即時に「反映済み」になります。ただし、ステータスが「承認済み」になってから30日以内（土日祝日を含む）に手動で変更内容の公開を行わなかった場合は、31日目の午前9:00（JST）に自動的に公開されます。

たとえば、8月1日にLINEミニアプリのステータスが「承認済み」になった場合、8月31日の午前9:00（JST）に新しい変更が自動的に公開されます。

新しい変更が公開されると、LINEミニアプリチャネルのステータスは「審査前」に戻り、設定の変更や審査の再申請が改めて可能になります。このとき、設定を変更しても、再度審査を通過して［**変更内容を公開する**］ボタンを押すまでは、公開中のLINEミニアプリに影響はありません。

<!-- note start -->

**ステータス変更に若干の遅れが生じる場合があります**

31日目の午前9:00（JST）に自動的にステータス変更の処理が開始されますが、完了までには1～2時間の遅れが生じる場合があります。

<!-- note end -->

## 審査を通過したLINEミニアプリチャネルのプロバイダー 

[LINE Developersコンソール](https://developers.line.biz/console/)の［**チャネル基本設定**］タブの［**サービスを提供する地域**］に「日本」が設定されている場合、LINEミニアプリチャネルが審査を通過すると、そのプロバイダーは[認証プロバイダー](https://developers.line.biz/ja/docs/line-developers-console/overview/#certified-provider)になります。
