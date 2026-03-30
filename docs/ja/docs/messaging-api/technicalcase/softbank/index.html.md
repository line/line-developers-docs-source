# LINEを活用したサービス開発に Infrastructure as “Low” Code を導入！ CNAPによる開発効率化事例

<!-- tip start -->

**このページについて**

このページは、LINE API Use Caseサイト（2026年3月31日に閉鎖）に掲載していた記事を、LINE Developersサイトへ移管したものです。LINEプラットフォームを導入した企業の事例を紹介しています。なお、記事の内容は掲載時点のものです。

<!-- tip end -->

![ソフトバンク株式会社](https://developers.line.biz/media/messaging-api/technicalcase/softbank/ja/softbank-logo.webp)

**ソフトバンク株式会社**

ソフトバンク株式会社は、通信事業をはじめ、クラウド・セキュリティ・AI・ロボティクスなど幅広い事業を展開しています。情報革命で人々の幸せに貢献し、「世界に最も必要とされる会社」になることを目指しており、これまで築き上げた事業基盤と、デジタルテクノロジーの力で、誰もが便利で、快適・安全に過ごせる理想の社会を実現していきます。

## アプリの開発期間を短縮するCNAPとは？ 

従来のアプリケーション開発においては、次のような課題がありました。

- 開発とインフラ運用部門が分かれており、リリースの度に変更作業の依頼が必要で、リリースに時間を要する
- 開発・実行環境、設計、ポリシーなどが統一されておらず、ガバナンスが確保されていない
- 作業が人依存で標準化されておらず、作業ミスのリスクがある

これらの課題は、DevOpsの考え方に従い、構築・運用の自動化、構成の標準化などによって解消できます。しかし、これらを満たす環境を自前で準備するには、学習コストが高い、技術蓄積に時間がかかる、頻繁なバージョンアップに追従し維持管理が必要であることから、非常に困難です。クラウドネイティブ・アプリケーションプラットフォーム（以下、CNAP）は、ソフトバンクが実践するDevOpsノウハウを凝縮した標準化・自動化環境をプラットフォーム提供するサービスです。あらかじめ設計を標準化、構築プロセスを自動化したLow Code構成パッケージをご提供し、当社がパッケージを維持管理することで、従来の課題から解放され、お客さまは本来注力すべき開発業務に集中できます。今回は、LINEのMessaging APIを活用したお問い合わせ管理システムの開発でのCNAP活用事例をご紹介します。

### スクリーンショット 

![これからの開発の流れ](https://developers.line.biz/media/messaging-api/technicalcase/softbank/ja/softbank-overview_1.webp)

![CNAPのメリット](https://developers.line.biz/media/messaging-api/technicalcase/softbank/ja/softbank-overview_2.webp)

![CNAPとは](https://developers.line.biz/media/messaging-api/technicalcase/softbank/ja/softbank-overview_3.webp)

![サービスイメージ](https://developers.line.biz/media/messaging-api/technicalcase/softbank/ja/softbank-overview_4.webp)

## システムの解説 

![システム構成図](https://developers.line.biz/media/messaging-api/technicalcase/softbank/ja/softbank-system-diagram.webp)

### CNAPによるAzure環境へのデプロイ自動化 

フロントエンドからバックエンドまで、インフラはすべてAzure上に構築しています。当社ではMicrosoft Azure / Google Cloud / Amazon Web Services（AWS）の各パブリッククラウドに対応したMSPサービスをご提供しています。同サービスは内製開発しており、その経験から各パブリッククラウドに関する幅広いスキルを有しております。中でもAzureは、2019年10月からいち早くMSPサービスの提供を開始しており、最も得意とするパブリッククラウドです。そのため、今回の事例ではAzureを採用しました。CNAPでは、システムの構成情報を抽象化して記述したYAMLファイルをGitリポジトリにPushするだけで、Kubernetes領域だけでなく周辺の関連リソースまで一括でデプロイ・管理することができます。Google CloudやAWSもサポートしております。

### Azure Kubernetes Serviceを利用したパフォーマンスおよびコストの最適化 

アプリケーションはKubernetesクラスター上で動作させていることから、Azure Kubernetes Serviceのコストが最も多くを占めています。一方で、クラスターを構成するノード上には複数のPodを配置できることから、ノードの処理量が許す限り、複数のサービスを同居させることも可能です。またKubernetesを使用することで負荷に応じて動的にスケーリングすることも可能です。このため、各サービスの負荷に応じてアプリケーションのパフォーマンスを最適化しつつ、コストを最小限に抑えることができます。

### AKSをはじめとするCNAPの構成要素 

CNAPはAKSをはじめとするマネージドサービスをコアに、複数のOSS群を高度に統合して構成された、インフラ運用の自動化を強力にサポートするプラットフォームです。アプリケーションのパッケージング基盤としてHelmを採用し、GitOpsを実現するCD（Continuous Delivery）基盤としてFlux CDを採用しています。また、アプリケーションのメトリクスやログ、エラーの監視のためには、PrometheusとGrafanaを採用しています。CNAPでは、当社のアプリケーション開発や運用において蓄積されたノウハウに基づいて、運用実績のあるOSS群を推奨の設定値にてご提供することで、お客さまご自身でセルフサービスでの管理・運用・モニタリングが可能な構成になっております。

### 今後どうしていきたいか？ 

CNAPではアプリケーションのインフラレイヤーを抽象化、さらにマネージドな基盤をご提供することで、お客さまがアプリケーションの開発に注力できる環境をご提供しています。CNAPをご活用いただくことで、LINEのAPIを使ったアプリケーション開発をはじめ、多くのアプリケーション開発をご支援できるものと考えており、今後もサービスを拡張し、お客さまに寄り添ったサービスをご提供できるよう、努めてまいります。

### これからサービスを開発される方に一言 

先にも述べましたが、LINEは圧倒的なアクティブユーザー数を誇るため、LINEのプラットフォーム上でサービスを展開することで、エンドユーザーへのリーチの可能性が広がります。LINEのプラットフォームには非常に多くのAPIが用意されており、それらの組み合わせによっては、アイデア次第でさまざまなアプリケーションを開発することができます。アプリケーション開発の際には、ぜひCNAPのことを思い出していただき、導入をご検討いただけますと幸いです。

---

## ユーザー導入事例関連リンク 

- [クラウドネイティブ・アプリケーションプラットフォーム（CNAP）](https://www.softbank.jp/biz/services/platform/msp-service/cnap/)
- [MSPサービス](https://www.softbank.jp/biz/services/platform/msp-service/)
- [ソフトバンク株式会社](https://www.softbank.jp/business/)
