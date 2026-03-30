# イベント体験デモ

<!-- tip start -->

**このページについて**

このページは、LINE API Use Caseサイト（2026年3月31日に閉鎖）に掲載していた記事を、LINE Developersサイトへ移管したものです。なお、記事の内容は掲載時点のものです。

<!-- tip end -->

複合経路検索サービス「[mixway API](https://mixway.ekispert.net/lp/api)」とLINEを組み合わせることで、ライブやお祭り、花火大会などのイベントに参加する体験がよりスマートになります。

エンドユーザーから見ると「イベントに参加する」という一つの大きなプロセスのはずが、実は、イベントの予約（チケットの購入）、会場までの経路の確認、移動手段の手配、参加（チケットの提示など）、というように多くの小さなプロセスの集合となっています。これまでは、プロセスごとに専用アプリが分かれていたため、アプリごとに専用アカウントを作成し、管理する必要がありました。

これら多くのプロセスを、すべて1つのLINEミニアプリに、また1つのアカウントに集約することで、エンドユーザーがイベントに参加するときの小さな壁を取り払うことができます。これが、私たちが考えるスマートなイベント体験です。

<!-- table of contents -->

## デモを見る 

デモアプリでは「友人と花火大会に行く」という状況を想定した、新たな「イベントへの参加」を疑似体験できます。お使いのスマートフォンでLINEを起動し、以下のQRコードを読み込むとデモを見ることができます。

![](https://developers.line.biz/media/line-mini-app/demo/mixwayapi-demo/maas-mixwayapi-qr-demo.webp)

<!-- note start -->

**デモアプリで取得するデータについて**

デモアプリでは、皆さまのLINEアカウントの「プロフィール情報（ユーザーID）」を取得します。ユーザーIDはサーバーに保存しますが、保存したデータは毎日削除されます。以上をご理解のうえ、ご利用ください。

<!-- note end -->

## デモアプリ利用の流れ 

※お使いのバージョンによって画面のデザインが異なる場合があります。

| | | | |
| --- | --- | --- | --- |
|![](https://developers.line.biz/media/line-mini-app/demo/mixwayapi-demo/maas-mixwayapi-image1.webp)|![](https://developers.line.biz/media/line-mini-app/demo/mixwayapi-demo/maas-mixwayapi-image2.webp)|![](https://developers.line.biz/media/line-mini-app/demo/mixwayapi-demo/maas-mixwayapi-image3.webp)|![](https://developers.line.biz/media/line-mini-app/demo/mixwayapi-demo/maas-mixwayapi-image4.webp)|
| 1.アプリ起動 | 2.イベントチケット購入 | 3.経路検索・選択 | 4.通知 |

<!-- tip start -->

**導入のポイント**

1. イベント参加に必要なプロセスをLINE上で完結します。
2. 予約したイベントの開催予定や交通手段の遅延情報がLINEで届きます。
3. イベント専用バスなど独自の交通手段（デマンドモビリティ）も考慮した経路検索が可能です。
4. 公共交通とデマンドモビリティを組み合わせた経路検索の開発が容易です。
5. 難しい手続きが必要なく、簡単に利用を開始できます。
6. 安全対策やイベント会場への混雑緩和が期待できます。

<!-- tip end -->

## 導入におけるメリット 

### エンドユーザー視点でのメリット 

#### 1. イベント参加に必要なプロセスをLINE上で完結 

普段から慣れ親しんだLINE上で、予約、決済、会場までの経路の確認、移動手段の手配、チケット提示が完結します。プロセスごとの専用アプリを利用したり、専用アカウントを作成および管理したり、チケットを印刷する煩わしさがありません。

#### 2. 予約したイベントの開催予定や交通手段の遅延情報がLINEに届く 

イベントの開催予定や、予約した交通手段の遅延情報は、LINEに届きます（プッシュ通知）。イベントをうっかり忘れたり、普段生活していない場所での交通手段の遅延状況がわからずに不安になったりすることはありません。

#### 3. イベント専用バスなど独自の交通手段（デマンドモビリティ）も考慮した経路検索が可能 

普段使う経路検索アプリでは対応していないような、イベント開催日だけ運行するデマンドモビリティや臨時バス、臨時シェアサイクルも含めた経路検索が可能です。デマンドモビリティの運行時間も考慮した経路を検索できるため、より綿密なスケジュールを作成できます。

### サービス提供者視点でのメリット 

#### 1. 公共交通とデマンドモビリティを組み合わせた経路検索の開発が容易 

MaaS向け複合経路検索API「mixway API」を利用すると、公共交通はもちろん徒歩、自動車、シェアサイクル、デマンドモビリティなどを組み合わせたマルチモーダルなナビゲーションを実現できます。

#### 2. 難しい手続きが必要なく、簡単に利用を開始可能 

エンドユーザーが普段から慣れ親しんだLINEで、予約、決済、経路検索、チケット提示ができるため、イベントへの参加ハードルを下げることができます。LINEで新しいイベント体験を提供できます。

#### 3. 安全対策やイベント会場への混雑緩和に期待できます 

大規模なイベントでは会場と周辺地域の混雑が課題になります。LINEを通じて参加人数を把握し、さらに行き帰りの移動手段までサポートすることで、安心安全なイベント体験が提供できます。

## デモアプリケーションのシステム図とシーケンス図 

デモアプリケーションで、どのようにLINE APIを利用しているかを示した図です。

※デモアプリケーションでは実装されていない機能も図に含まれています。

**システム図**

![](https://developers.line.biz/media/line-mini-app/demo/mixwayapi-demo/maas-mixwayapi-system-diagram.webp)

- その他のサービスを利用した場合のシステム図
  - [AWSを利用したシステム図](https://developers.line.biz/media/line-mini-app/demo/mixwayapi-demo/maas-mixwayapi-system-diagram-aws.webp)
  - [Azureを利用したシステム図](https://developers.line.biz/media/line-mini-app/demo/mixwayapi-demo/maas-mixwayapi-system-diagram-azure.webp)

**シーケンス図**

![](https://developers.line.biz/media/line-mini-app/demo/mixwayapi-demo/maas-mixwayapi-sequence-diagram.webp)

- その他のサービスを利用した場合のシーケンス図
  - [AWSを利用したシーケンス図](https://developers.line.biz/media/line-mini-app/demo/mixwayapi-demo/maas-mixwayapi-sequence-diagram-aws.webp)
  - [Azureを利用したシーケンス図](https://developers.line.biz/media/line-mini-app/demo/mixwayapi-demo/maas-mixwayapi-sequence-diagram-azure.webp)

## 関連リンク 

- [Messaging APIドキュメント](https://developers.line.biz/ja/docs/messaging-api/)
- [LINEミニアプリドキュメント](https://developers.line.biz/ja/docs/line-mini-app/)
