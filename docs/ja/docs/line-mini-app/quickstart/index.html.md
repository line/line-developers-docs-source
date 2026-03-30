# はじめに

LINEミニアプリは、LINE上で動作するウェブアプリです。

開発者がこのプラットフォームを活用すれば、ネイティブアプリを開発することなく、自社のサービスをユーザーに提供できます。

ユーザーは、新たにアプリをダウンロードすることなく、LINEアカウントを使って、LINE上で多種多様なサービスを楽しめます。

## LINEミニアプリ開発から公開までの流れ 

LINEミニアプリの開発および公開に関して、全体的な流れは次のとおりです。

1. [LINEミニアプリチャネルを作成し、LINEミニアプリを開発します](https://developers.line.biz/ja/docs/line-mini-app/develop/develop-overview/)。この段階で、未認証ミニアプリとして公開されます。
2. [LINEミニアプリの審査を依頼します](https://developers.line.biz/ja/docs/line-mini-app/submit/submission-guide/)。
3. 審査に通過したら、認証済ミニアプリとして[サービスを提供できます](https://developers.line.biz/ja/docs/line-mini-app/service/service-operation/)。

## 共通ガイド 

以下の内容については、役割にかかわらず読んでください。

- [**LINEミニアプリの基本を学ぶ**](https://developers.line.biz/ja/docs/line-mini-app/discover/introduction/)：LINEミニアプリに標準で搭載されているビルトイン機能や、自分で実装できるカスタム機能を理解します。
  - [仕様](https://developers.line.biz/ja/docs/line-mini-app/discover/specifications/)
  - [ビルトイン機能](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/)
  - [カスタム機能](https://developers.line.biz/ja/docs/line-mini-app/discover/custom-features/)
  - [LINEミニアプリの構造](https://developers.line.biz/ja/docs/line-mini-app/discover/ui-components/)

## 役割別ガイド 

役割に応じて提供されるガイドに従って、LINEミニアプリの開発の作業の流れを確認してください。

### サービス企画者向けガイド 

LINEミニアプリを使って提供するサービスを企画する場合は、以下の内容を確認してください。

- [**LINEミニアプリポリシーを確認する**](https://terms2.line.me/LINE_MINI_App?lang=ja)：企画段階では、LINEミニアプリポリシーについて検討してください。また、LINEミニアプリを審査に提出する際は、LINEミニアプリがLINEミニアプリポリシーを遵守していることを確認してください。

### 開発者向けガイド 

LINEミニアプリの実装および開発を行う場合は、次のガイドが役に立ちます。

- [**LINEミニアプリの仕様を確認する**](https://developers.line.biz/ja/docs/line-mini-app/discover/specifications/)：どのプラットフォームのどのバージョンでどの機能がサポートされているかといった情報や、LIFFの対応バージョンについて確認してください。
- **開発者ガイド**
  - [**開発を始めよう**](https://developers.line.biz/ja/docs/line-mini-app/develop/develop-overview/)：LINEミニアプリを開発するときに読みましょう。
  - [**カスタムアクションボタンを実装する**](https://developers.line.biz/ja/docs/line-mini-app/develop/share-messages/)：LINEミニアプリを友だちと共有するときに送信するシェアメッセージをカスタマイズできます。
  - [**サービスメッセージを送信する**](https://developers.line.biz/ja/docs/line-mini-app/develop/service-messages/)：ユーザーのアクションに対する確認や応答として、サービスメッセージを送信できます。
  - [**決済システムを利用する**](https://developers.line.biz/ja/docs/line-mini-app/develop/payment/)：ユーザーに決済システムを提供するために、LINEミニアプリにLINE Payや他の決済システムを連動することができます。
  - [**パーマネントリンクを作成する**](https://developers.line.biz/ja/docs/line-mini-app/develop/permanent-links/)：ユーザーがLINEミニアプリにすぐにアクセスできるように、LINEミニアプリのパーマネントリンクを使用できます。
  - [**LINE DevelopersコンソールでLINEミニアプリの設定を管理する**](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/)：LINEミニアプリでは、LINE Developersコンソールで設定したデータを使用します。LINE Developersコンソールに正しいデータを設定してください。
  - [**外部ブラウザでLINEミニアプリを開く**](https://developers.line.biz/ja/docs/line-mini-app/develop/external-browser/)：外部ブラウザでLINEミニアプリを開く場合の注意点を確認してください。
  - [**パフォーマンスガイドを確認する**](https://developers.line.biz/ja/docs/line-mini-app/develop/performance-guidelines/)：LINEミニアプリのパフォーマンスを考慮することをお勧めします。
- **APIリファレンス**
  - [サービスメッセージAPI](https://developers.line.biz/ja/reference/line-mini-app/#service-messages)
  - [LIFF API](https://developers.line.biz/ja/reference/liff/)
  - [LINE Pay API](https://developers-pay.line.me/online-api-v3)
- [**審査を依頼する**](https://developers.line.biz/ja/docs/line-mini-app/submit/submission-guide/)：ガイドラインに基づいて認定されたLINEミニアプリだけが、認証済ミニアプリになります。LINEミニアプリを認証済ミニアプリにするために、審査を依頼します。

### デザイナー向けガイド 

LINEミニアプリのページをデザインする場合は、次を参照してください。

- [**LINEミニアプリのアイコンの仕様とガイドライン**](https://developers.line.biz/ja/docs/line-mini-app/design/line-mini-app-icon/)：ガイドラインに従ってアイコンを作成し、LINE Developersコンソールでチャネルアイコンに設定してください。詳しくは、「[LINE DevelopersコンソールでLINEミニアプリの設定を管理する](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/)」を参照してください。
- [**ランドスケープモードのセーフエリアを確認する**](https://developers.line.biz/ja/docs/line-mini-app/design/landscape/)：ノッチがある端末でもLINEミニアプリのすべてを表示するために、LINEミニアプリがセーフエリアに収まるようにしてください。
- [**読み込み中アイコンを確認する**](https://developers.line.biz/ja/docs/line-mini-app/design/loading-icon/)：読み込み中アイコンは、LINEミニアプリで推奨されているUI要素です。指定されたファイルを使用してください。

### サービス運営者およびマーケティング担当者向けガイド 

LINEミニアプリで提供サービスを運営する際の注意点を覚えましょう。

- [**運営ガイドを確認する**](https://developers.line.biz/ja/docs/line-mini-app/service/service-operation/)：実際にサービスを運営、運用する際は、パーマネントリンクによるLINEミニアプリのシェアや、サービス通知メッセージの送信などについて、注意すべき点を確認しておきましょう。
  - [サービス事業主のためのノウハウ](https://developers.line.biz/ja/docs/line-mini-app/service/service-operation/)
  - [LINEミニアプリに広告を掲載する](https://developers.line.biz/ja/docs/line-mini-app/service/line-mini-app-ads/)
  - [認証済ミニアプリ更新後の再審査](https://developers.line.biz/ja/docs/line-mini-app/service/update-service/)
  - [LINE公式アカウントを活用する](https://developers.line.biz/ja/docs/line-mini-app/service/line-mini-app-oa/)
