# 購買体験デモ

<!-- tip start -->

**このページについて**

このページは、LINE API Use Caseサイト（2026年3月31日に閉鎖）に掲載していた記事を、LINE Developersサイトへ移管したものです。なお、記事の内容は掲載時点のものです。

<!-- tip end -->

エンドユーザーに最も近いデバイスであるスマートフォンを活用して、小売事業者のDX（デジタルトランスフォーメーション）を推進しましょう。特にオンラインとオフラインを融合（OMO：Online Merges with Offline）させた顧客体験の提供は、新しい小売業のスタンダードになると考えられています。従来の顧客体験は主に来店中に限定されていましたが、これからは来店中だけにとどまらず、来店前から来店後までをシームレスな顧客体験として高度にデザインし、エンドユーザーに大きなメリットを提供できます。

LINEミニアプリを使うことで、以下のような価値提供をすべてLINE一つで完結できます。LINE公式アカウントやLINEミニアプリで取得したユーザー行動データを、サービス提供企業で用意するCRMなどに蓄積し、エンドユーザーごとにカスタマイズされた極上のシームレスな顧客体験を実現できます。

- LINE広告、LINE公式アカウント、LINEチラシ、独自の予約システムを使った来店前のお得情報の提供
- スマホレジ、デジタル会員証、購買履歴（レシート）確認機能などによる購買体験の向上
- LINE公式アカウントを利用した購買後のコミュニケーション

さらに[GS1標準の二次元シンボル](https://www.gs1jp.org/standard/industry/2d-in-retail/)をスマホレジに取り入れることで新しい購買体験や店舗DXを実現することができます。

<!-- table of contents -->

## LINEを活用したOMOのイメージ 

LINEを活用したデジタル時代の新しい購買体験（OMO）では、来店前から購入後まで一貫した体験が可能です。来店前にはLINE広告や公式アカウント、LINEチラシで情報を提供し、店内ではLINE POP Mediaやサイネージを活用した告知が行われます。購入時にはスマホレジやLINEでの応募、ECサイトで簡単に手続きができ、購入後もLINE公式アカウントを通じてフォローアップを行います。これにより、オンラインとオフラインがシームレスに連携した購買体験を実現します。

![](https://developers.line.biz/media/line-mini-app/demo/smartretail-demo/smartretail-image-data.webp)

## スマホレジデモを見る 

- [デモサイトで実際にLINEミニアプリによる購買体験を体験してみましょう。](https://lineapiusecase.com/ja/omo/index.html)

## 導入におけるメリット 

### エンドユーザー視点でのメリット 

#### 1. アプリのダウンロードや煩雑な入会手続きは不要 

小売事業者様が提供するサービスを利用するために、新たなアプリをダウンロードしたりインストールしたりする必要も、煩雑な入会手続きの必要もありません。すぐに優れた顧客体験を実感できます。

#### 2. 店舗のお得情報の入手から支払いまでをLINE上で完結 

LINEチラシを使って来店前にお得情報を入手できます。また、支払いをLINEで完結できるため、レジ混雑時に並ぶ必要がありません。感染症対策、買い物時間の短縮が期待できます。

#### 3. 会員証なども含め各サービスをシームレスに利用可能 

LINEでデジタル会員証を発行し、デジタル購買証明（レシート）を受領できます。さらにLINE上で、会員特典やポイントの取得・利用も可能です。また、LINEをセルフレジとして利用し、購買履歴を簡単に確認できます。エンドユーザーは、煩雑な会員証の管理やレシートの管理から解放されます。

### サービス提供者視点でのメリット 

#### 1. 難しい手続きが必要なく、簡単に利用を開始可能 

QRコード読み込みのみで利用を開始してもらえるだけでなく、ユーザーが希望しない場合は名前や住所などを入力せずに使い始めることもできます。このように、利用を開始するまでのハードルを下げられるため、導入してもらえる可能性が高まります。

#### 2. オフライン・オンラインを問わずエンドユーザーとのコミュニケーションが可能 

たとえば、LINE公式アカウントを通じてエンドユーザーに対して、エンドユーザー1人1人に合わせたキャンペーン案内の送付やクーポンの配布が可能です。また、LINE公式アカウントからエンドユーザーにリアルタイム性の高い通知ができるため、商品の販売状況に合わせた店舗への集客効果も期待できます。

#### 3. レジ前での混雑が軽減でき、感染症対策や経費削減に期待できます 

エンドユーザーが持つスマートフォンで決済できるため、セルフレジを導入する必要がなく、またレジを担当するスタッフも削減でき、経費削減効果が期待できます。また、レジ待ちをする人が減ることで、感染症対策に役立てることもできます。

## デモアプリケーションのシステム図とシーケンス図 

デモアプリケーションで、どのようにLINE APIを利用しているかを示した図です。

※デモアプリケーションでは実装されていない機能も図に含まれています。

**システム図**

![](https://developers.line.biz/media/line-mini-app/demo/smartretail-demo/smartretail-system-diagram.webp)

- その他のサービスを利用した場合のシステム図
  - [AWSを利用したシステム図](https://developers.line.biz/media/line-mini-app/demo/smartretail-demo/smartretail-system-diagram-aws.webp)
  - [Azureを利用したシステム図](https://developers.line.biz/media/line-mini-app/demo/smartretail-demo/smartretail-system-diagram-azure.webp)

**シーケンス図**

![](https://developers.line.biz/media/line-mini-app/demo/smartretail-demo/smartretail-sequence-diagram.webp)

- その他のサービスを利用した場合のシーケンス図
  - [AWSを利用したシーケンス図](https://developers.line.biz/media/line-mini-app/demo/smartretail-demo/smartretail-sequence-diagram-aws.webp)
  - [Azureを利用したシーケンス図](https://developers.line.biz/media/line-mini-app/demo/smartretail-demo/smartretail-sequence-diagram-azure.webp)

## 関連リンク 

- [Messaging APIドキュメント](https://developers.line.biz/ja/docs/messaging-api/)
- [LINEミニアプリドキュメント](https://developers.line.biz/ja/docs/line-mini-app/)
