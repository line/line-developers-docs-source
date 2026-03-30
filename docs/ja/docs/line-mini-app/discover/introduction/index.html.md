# LINEミニアプリとは

LINEミニアプリは、[LIFF（LINE Front-end Framework）](https://developers.line.biz/ja/docs/liff/)上で実行されるウェブアプリです。LINEミニアプリを使えば、ユーザーはアプリをインストールしなくてもサービスを利用できます。

「LINEミニアプリ」が公式名です。

LINEミニアプリはウェブアプリですので、HTML5のほとんどの仕様が使用できます。詳しくは、「[仕様](https://developers.line.biz/ja/docs/line-mini-app/discover/specifications/)」を参照してください。

## はじめに 

LINEミニアプリは[LINEミニアプリポリシー](https://terms2.line.me/LINE_MINI_App?lang=ja)における「本サービスのご利用対象者」であれば、どなたでも開発することができます。はじめに「[クイックスタートガイド](https://developers.line.biz/ja/docs/line-mini-app/quickstart/)」をお読みください。

LINEミニアプリチャネルを作成するには、[LINE Developersコンソール](https://developers.line.biz/console/)のアカウントが必要です。LINEミニアプリの設定から審査申請まで、多くの作業をLINE Developersコンソール上で行います。

## LINEミニアプリでできること 

LINEミニアプリには、以下のような便利な[ビルトイン機能](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/)が用意されています。

- LINEミニアプリをほかのユーザーにシェアする機能
- ユーザーに対してサービスへのアクセス権限の付与を依頼する機能

また、さらに充実したユーザー体験を提供するために、以下のような[カスタム機能](https://developers.line.biz/ja/docs/line-mini-app/discover/custom-features/)をLINEミニアプリに追加できます。

- サービスメッセージ
- 決済システムの利用
- カスタムアクションボタン

<!-- tip start -->

**LINEミニアプリを試す**

LINEヤフー株式会社では、開発者向けに[LINEミニアプリプレイグラウンド](https://miniapp.line.me/lineminiapp_playground)というLINEミニアプリを公開しています。LINEアプリがインストールされたスマートフォンでLINEミニアプリプレイグラウンドを開くと、LINEミニアプリの一部機能を実際に試すことができます。

<!-- tip end -->

## 未認証ミニアプリと認証済ミニアプリ 

LINEミニアプリは、弊社による認証審査に通過しているかどうかによって、未認証ミニアプリと認証済ミニアプリに分かれます。それぞれの違いについては、以下の各セクションを確認してください。

### 未認証ミニアプリとは 

未認証ミニアプリとは、弊社による認証審査に通過していないLINEミニアプリのことをいいます。LINEミニアプリチャネルを作成した後から、認証審査に通過するまでは、未認証ミニアプリとなります。

未認証ミニアプリはどなたでも作成できますが、次の「[認証済ミニアプリとは](https://developers.line.biz/ja/docs/line-mini-app/discover/introduction/#verified-mini-app)」に示すように、一部機能が制限されます。認証済ミニアプリにするためには、[認証審査を申請](https://developers.line.biz/ja/docs/line-mini-app/submit/submission-guide/)してください。

### 認証済ミニアプリとは 

弊社による認証審査に通過すると、そのLINEミニアプリは認証済ミニアプリとなります。認証済ミニアプリになると、以下の画像のように、ヘッダーなどに認証バッジがつきます。

![](https://developers.line.biz/media/news/2024/line-mini-app-header-after.png)

また、以下の各機能などが利用できるようになります。

- [ユーザー端末のホーム画面にショートカットを追加する](https://developers.line.biz/ja/docs/line-mini-app/develop/add-to-home-screen/)
- [Custom Path](https://developers.line.biz/ja/docs/line-mini-app/develop/custom-path/)
- [チャネル同意の簡略化](https://developers.line.biz/ja/docs/line-mini-app/develop/channel-consent-simplification/)

以上のように、LINEミニアプリを認証済ミニアプリにすることで、信頼性や利便性などの面で、ユーザー体験を高めることができます。認証済ミニアプリで利用できる機能について詳しくは、「[カスタム機能](https://developers.line.biz/ja/docs/line-mini-app/discover/custom-features/)」を参照してください。

## LINEミニアプリの構造 

LINEミニアプリのページは、（A）ヘッダーおよび（B）ボディで構成されています。詳しくは、「[LINEミニアプリの構造](https://developers.line.biz/ja/docs/line-mini-app/discover/ui-components/)」を参照してください。

![LINEミニアプリの構造](https://developers.line.biz/media/line-mini-app/mini_concept.png)

## ユーザーがLINEミニアプリにアクセスする方法 

ユーザーは、LINEからだけでなく、LINE外部からもLINEミニアプリにアクセスできます。LINE内には、LINEミニアプリにアクセスするためのポイントがいくつも用意されています。

### LINE外部からアクセスする 

[LINEミニアプリのパーマネントリンク](https://developers.line.biz/ja/docs/line-mini-app/develop/permanent-links/)にアクセスすると、LINE外部からもLINEミニアプリにアクセスできます。LINEミニアプリのパーマネントリンクは、以下の方法でユーザーにシェアできます。

- ウェブサイト、メール、テキストメッセージなどに掲載する
- QRコードを作成して各種媒体に掲載する

また、[ユーザー端末のホーム画面にLINEミニアプリへのショートカットを追加する](https://developers.line.biz/ja/docs/line-mini-app/develop/add-to-home-screen/)と、ホーム画面からLINEミニアプリに直接アクセスできます。

### LINE公式アカウント 

LINE公式アカウントからもLINEミニアプリにアクセスできます。たとえば、LINE公式アカウントの友だちに送信するリッチメッセージや、LINE公式アカウントとのトーク画面に表示されるリッチメニューに、LINEミニアプリを開くリンクを追加できます。詳しくは、[LINE公式アカウントを活用する](https://developers.line.biz/ja/docs/line-mini-app/service/line-mini-app-oa/)を参照してください。

![LINE公式アカウントでLINEミニアプリのプロモーションができる](https://developers.line.biz/media/line-mini-app/mini_with_oa.png)

### ホームタブ 

<!-- note start -->

**LINEミニアプリをLINEのホームタブに固定する機能は廃止されました**

詳しくは、2024年1月9日のニュース、「[最近利用したLINEミニアプリにLINEのホームタブからアクセスできるようになりました](https://developers.line.biz/ja/news/2024/01/09/line-mini-app-history/)」を参照してください。

<!-- note end -->

LINEの［**ホーム**］タブの［**サービス**］から、最近利用したLINEミニアプリにアクセスできます。［**サービス**］には、最近利用したLINEミニアプリが、利用履歴の新しい順に最大で8件まで表示されます。この機能は、認証済ミニアプリでのみ利用できます。

ホームタブの表示ポリシーは、サービスを提供する地域によって異なります。

![](https://developers.line.biz/media/line-mini-app/mini-access-home-tab-ja.png)

### LINEで探す 

LINEの検索機能からも、LINEミニアプリにアクセスできます。この機能は、認証済ミニアプリでのみ利用できます。

![検索機能からアクセス](https://developers.line.biz/media/line-mini-app/mini_access_search.png)

### LINEメッセージ 

友だち同士で、LINEミニアプリを簡単にシェアできます。[ビルトインのアクションボタン](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#action-button)を使用するだけでなく、[カスタムアクションボタン](https://developers.line.biz/ja/docs/line-mini-app/develop/share-messages/)を使用して、LINEミニアプリのページをLINEメッセージでシェアできます。

![シェアメッセージ](https://developers.line.biz/media/line-mini-app/mini_access_share.png)

## LIFFアプリでできてLINEミニアプリでできないこと 

| 項目 | 説明 |
| --- | --- |
| アクションボタンの非表示（モジュールモード） | LINEミニアプリでは、[アクションボタン](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#action-button)を非表示にすることはできません。LINEミニアプリチャネルに追加されているLIFFアプリでは、［**モジュールモード**］は設定できません。 |
| 同一チャネルへの複数のLIFFアプリの追加 | LINEミニアプリチャネルでは、同一チャネルに複数のウェブアプリを追加することはできません。 |

<!-- tip start -->

**LINEミニアプリとしての作成を推奨します**

今後、LIFFとLINEミニアプリは、ブランド統合を予定しています。この統合により、LIFFはLINEミニアプリに統合されます。そのため、LIFFアプリを新規作成する際は、LINEミニアプリとして作成することを推奨します。詳しくは、「[2025年2月12日のニュース](https://developers.line.biz/ja/news/2025/02/12/line-mini-app/)」を参照してください。

<!-- tip end -->
