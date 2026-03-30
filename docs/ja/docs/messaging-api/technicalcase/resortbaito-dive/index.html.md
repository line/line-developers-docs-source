# 派遣スタッフの満足度を高める「リゾートバイトダイブ」の開発事例

<!-- tip start -->

**このページについて**

このページは、LINE API Use Caseサイト（2026年3月31日に閉鎖）に掲載していた記事を、LINE Developersサイトへ移管したものです。LINEプラットフォームを導入した企業の事例を紹介しています。なお、記事の内容は掲載時点のものです。

<!-- tip end -->

![株式会社ダイブ](https://developers.line.biz/media/messaging-api/technicalcase/resortbaito-dive/ja/resortbaito-dive-logo.png)

**株式会社ダイブ**

株式会社ダイブは、観光施設に特化した人材サービス（リゾートバイト）を基幹事業として展開しているベンチャー企業です。観光産業の大課題である「人手不足」の解決に寄与しており、サービスサイトの登録者数は年間4万人以上、LINE友だち数は15万人を突破。働き手と地域をつなぐ雇用機会を提供し、地方創生や観光産業の発展に取り組んでいます。

## サービス概要と解決したい課題 

株式会社ダイブが運営するリゾートバイト専門の人材派遣サービス「リゾートバイトダイブ」では、LINE公式アカウントを通して派遣スタッフと営業担当、カスタマーサポートが日々コミュニケーションを行っています。コミュニケーションの内容は勤務中の日々の困りごとからお仕事探しの相談まで多岐に渡り、コミュニケーションの件数はピーク月では月間送信数63,000件におよびます。1つ1つ丁寧なコミュニケーションを心がけ、派遣スタッフからは非常に良い評価をいただいています。

### スクリーンショット 

![service-image](https://developers.line.biz/media/messaging-api/technicalcase/resortbaito-dive/ja/resortbaito-dive-ui-img.png)

![service-cms-image](https://developers.line.biz/media/messaging-api/technicalcase/resortbaito-dive/ja/resortbaito-dive-ui-img-2.png)

## システムの概要 

![システム構成図](https://developers.line.biz/media/messaging-api/technicalcase/resortbaito-dive/ja/resortbaito-dive-system.png)

### 「リゾートバイトダイブ」を支える技術と効果 

株式会社ダイブのインフラは、AWS上に構築されています。フロントエンドは、CloudFrontとS3を活用して配信し、バックエンドのAPIは、ALB（Application Load Balancer）とECS on Fargateを利用して構築しています。

ユーザーからのチャットメッセージを受信するWebhookは、API GatewayとSQS（Simple Queue Service）を組み合わせてメッセージを受け取り、Lambdaでその後の処理を行う構成です。これにより、ユーザーからのメッセージを確実に受信できる仕組みを実現しています。データベースにはAurora Serverless v2を採用し、プロビジョニングを自動化することで運用効率を向上させています。さらに、これらのインフラ構成はAWS CDKを用いてコードベースで管理し、GitHub Actionsを使って自動デプロイを行っています。

開発言語としては、フロントエンド、バックエンド、インフラすべてにTypeScriptを採用し、エンジニアの認知的負荷を軽減する環境を整えています。この統一的なアプローチにより、効率的かつ高品質なシステム運用を実現しています。リリースした結果、前日の業務終了後から翌営業日にかけて届いたチャットの対応に、リリース前は午後まで時間がかかっていたものが、リリース後は午前中で対応が完了するようになりました。また、1日に数回実施しているチャットの対応漏れのチェックについても、検索機能が向上したことで、1回あたり約1時間かかっていた作業が30分程度で完了できるようになり、大幅な業務効率化を実現しています。

### 今後の展望 

チャットのデータが自社内に溜まるようになったため、今後はこのデータを分析に活用してユーザー満足度の向上を図りたいと考えています。

### LINE API開発における要望 

グループトーク、複数人トークのメンバーのユーザーID取得APIが、認証済みアカウントでしか実行できないため、開発用アカウントなどでテストができずに困りました。 テストのため、特別な申請をすると未認証アカウントでも実行できるようになると嬉しいです。

- [グループトークのメンバーのユーザーIDを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-group-member-user-ids)

- [複数人トークのメンバーのユーザーIDを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-room-member-user-ids)

### これから開発される方に一言 

チャットなどユーザーからのメッセージを確実に受け取る必要がある場合、Webhookで受け取ったメッセージをキューに積み、メッセージ受信と処理を分離すると拡張性の高いアーキテクチャになります。

---

## ユーザー導入事例関連リンク 

- [株式会社ダイブ](https://resortbaito-dive.com/)
- [開発会社：クラスメソッド株式会社](https://classmethod.jp/)
