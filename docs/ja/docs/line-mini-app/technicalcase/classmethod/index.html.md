# モバイルオーダーシステム「CX ORDER」の開発事例

<!-- tip start -->

**このページについて**

このページは、LINE API Use Caseサイト（2026年3月31日に閉鎖）に掲載していた記事を、LINE Developersサイトへ移管したものです。LINEプラットフォームを導入した企業の事例を紹介しています。なお、記事の内容は掲載時点のものです。

<!-- tip end -->

![クラスメソッド株式会社](https://developers.line.biz/media/line-mini-app/technicalcase/classmethod/classmethod_logo.webp)

**クラスメソッド株式会社**

クラスメソッドは「すべての人々の創造活動に貢献し続ける」という理念のもと、クラウド、データ分析、モバイル、IoT、AI／機械学習などの技術支援を行っています。LINE活用支援にも注力し、LINEミニアプリ開発やモバイルオーダー用LINEミニアプリ作成サービス「CX ORDER」などを提供しています。

## サービス提供者様の今回のシステム開発への想い 

クラスメソッド株式会社はIT企業ですが、秋葉原で完全キャッシュレスのカフェ店舗「[DevelopersIO CAFE](https://cafe.classmethod.jp/)」を運営しております。※

さまざまなオンラインの販売チャネル（LINE, Web, ネイティブアプリ）を開発・運用した経験をもとに、モバイルオーダー機能をLINEミニアプリとして提供するクラウドサービス「[CX ORDER](https://cxorder.jp/lp/)」としてリリースしました。

直近は（主に飲食店の）時短営業や休業による売り上げ減少のためテイクアウトチャネルの拡充による売り上げカバーを目的とし、中長期的には業務効率化・省人化、LINEを通じたユーザーとの継続的なコミュニケーション支援を目指しています。

モバイルオーダーは注目こそされていますがまだまだ新規性が高いサービスのため、ユーザーの利用ハードルをとにかく下げることが必要です。その点においてもLINEを活用していることでフリクションレスのCXを創出できると考えています。

※「DevelopersIO CAFE」は2022年12月20日に閉店しました。

### スクリーンショット 

| 商品一覧 | 商品詳細 | 注文確認 | 注文完了 |
| --- | --- | --- | --- |
| ![商品一覧](https://developers.line.biz/media/line-mini-app/technicalcase/classmethod/classmethod_screenshot_1.webp) | ![商品詳細](https://developers.line.biz/media/line-mini-app/technicalcase/classmethod/classmethod_screenshot_2.webp) | ![注文確認](https://developers.line.biz/media/line-mini-app/technicalcase/classmethod/classmethod_screenshot_3.webp) | ![注文完了](https://developers.line.biz/media/line-mini-app/technicalcase/classmethod/classmethod_screenshot_4.webp) |

## システムの解説 

![システム構成図](https://developers.line.biz/media/line-mini-app/technicalcase/classmethod/classmethod_system_diagram.webp)

### AWSをメインにGoogle Cloudの活用もスタート 

クラスメソッド株式会社が最も得意としているAWSをメインに利用しています。ユーザーはAmazon CloudFrontを経由し各アプリ、APIヘアクセスします。コア機能はAmazon ECS / Amazon Auroraを用いトラフィックの増加に伴うオートスケーリングを設定しています。

他にもアクセス頻度が高いデータはAmazon DynamoDBを活用したり、AWS LambdaやAmazon SQSを利用したりしています。完全AWSというわけではなく、一部機能においてはGoogle Cloudの活用もスタートしています。

### クラウドインフラのランニングコスト 

コア機能はAmazon ECS/ Amazon Auroraにて提供しているためサーバーレス環境と比べてコストは発生しています。機能の実装コストや中長期的な運用コストを鑑みると現構成が妥当と考えていますが、状況に応じてサーバーレス環境への機能単位での移行や構成変更を模索していきたいと考えています。

### インフラを支える運用ツールは何を使用しているのか？ 

インフラ構成管理にAWS CDK（TypeScript）を利用しています。CX ORDERはアプリ、APIもTypeScriptで書いているため、インフラレイヤーから一気通貫でエンジニアが対応できるようにしています。またSentryを導入しアプリエラーを監視し、Slackへ通知しています。短期間に同じテナントにて複数回のイベントが発生する場合は、カスタマーサクセスチームと連携してお客様の状況ヒアリング・エラー解消に役立てています。Google Analyticsではユーザー行動をトラッキングし、アプリの改善活動・メッセージ配信用セグメントの作成などに利用しています。

### 導入店舗の売り上げ向上・業務改善・省人化を目指す 

導入店舗の売り上げ向上・業務改善・省人化がトッププライオリティです。より多くの導入企業からのフィードバックをもとに機能開発・改善を繰り返していきます。またLINEを活用したコミュニケーション領域においても、クラスメソッド株式会社での実験をもとに機能追加・カスタマーサクセスで寄与できないかと考えています。

### LINE APIに対する要望 

LINE APIは導入が簡単かつ機能もコアに絞られていてシンプルです。APIについてはシンプルさをそのままにできること、安定稼働を続けることが、将来的にLINEに各種サービスを統合していく上で必要不可欠だと思います。また顧客理解の観点ではLINE側で持っている属性情報・サービス側で持っている情報の組み合わせでより詳細な施策実施ができると思います。

### これからサービスを開発される方に一言 

LINEのAPI/SDKを活用することで開発工数を下げることができます。またLINEをID基盤として利用することでユーザーの利用ハードルの軽減に寄与できます。サービス利用後はLINE公式アカウントによるコミュニケーションを通じてユーザーを自社のロイヤルカスタマー化できるという観点でも非常に有用です。さまざまなチャネルがあり、特性も当然異なりますがLINEを軸にサービス開発することの恩恵は大きいと思います。

---

## 関連リンク 

- [クラスメソッド株式会社 | LINEヤフー for Business](https://www.lycbiz.com/jp/partner/technology/line/classmethod/)
- [クラスメソッド株式会社](https://classmethod.jp/)
- [CX ORDER](https://cxorder.jp/lp/)
