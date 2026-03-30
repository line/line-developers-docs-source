# モバイルオーダーデモ

<!-- tip start -->

**このページについて**

このページは、LINE API Use Caseサイト（2026年3月31日に閉鎖）に掲載していた記事を、LINE Developersサイトへ移管したものです。なお、記事の内容は掲載時点のものです。

<!-- tip end -->

飲食店内外でLINEミニアプリ上から商品の事前注文～決済（＋デリバリー）ができます。

LINEミニアプリとLINE公式アカウントとの連携により、サービスを利用する中でスムーズにLINE公式アカウントの友だちを獲得することが可能になり、LINEミニアプリを通じて取得したユーザーデータを活用し、より効率的な販促活動を実現することができます。（※同じプロバイダー内で提供する場合のみ）

※ LINEアカウントと紐づいた行動データの取得・活用にはユーザーの許諾が必須となります。

<!-- table of contents -->

## デモを見る 

お使いのスマートフォンでLINEを起動し、以下のQRコードを読み込むとデモを見ることができます。

![](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-qr-demo.png)

<!-- note start -->

**デモアプリで取得するデータについて**

デモアプリでは、皆さまのLINEアカウントの「プロフィール情報（表示名、ユーザーID）」を取得します。ユーザーIDのみサーバーに保存しますが、保存したデータは毎日削除されます。上記をご理解のうえ、ご利用ください。本デモアプリが用意したLINE Pay残高から決済が行われます。実際の決済手段の選択および決済は行われません。

上記をご理解のうえ、ご利用ください。

<!-- note end -->

## デモアプリ利用の流れ 

※お使いのバージョンによって画面のデザインが異なる場合があります。

| | | | |
| --- | --- | --- | --- |
|![](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-image1.webp)|![](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-image2.webp)|![](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-image3.webp)|![](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-image4.webp)|
| 1.QRコード読取 | 2.必要な権限を認可 | 3.商品を選択して注文 | 4.決済 |

<!-- tip start -->

**導入のポイント**

1. 注文から会計までをスマホで完結します。店員との接触機会が減り感染症対策にもなります。
2. 割り勘の手間を省くことができます。
3. アプリの導入で省人化/人件費/端末リース費用の削減が可能です。
4. ユーザーからの問い合わせを受け付ける等も可能です。
5. ユーザーのモバイルオーダーアプリでの操作履歴や来店履歴をもとにメッセージ配信可能です。

<!-- tip end -->

## 導入におけるメリット 

### エンドユーザー視点でのメリット 

#### 1. 注文から会計までがスマホで完結するため、店員との接触機会が減り感染症対策に期待できます 

テーブルに備え付けのQRコードを読み込むと、LINEミニアプリが起動できます。LINEミニアプリを使ってテーブルから注文し、決済方法を選択して会計を済ませれば、対面での接触を伴わないため、感染症対策にも役立てることができます。

#### 2. 割り勘の手間を省くことができます 

大人数で来店したときもモバイルオーダーアプリは非常に便利です。店舗には、テーブルごとに1台の端末が備え付けられていることが多いですが、この場合、一度に一人しか操作できません。モバイルオーダーアプリを使うと、それぞれが自分のスマートフォンで同時に注文できます。さらにそれぞれ個別に会計することになるため、割り勘の手間を省けます。

### サービス提供者視点でのメリット 

#### 1. アプリの導入で省人化/人件費/端末リース費用の削減が可能 

従業員の注文や決済への対応負担を減らし、作業効率をUPさせることができます。対面での接触機会を減らすことができるため感染症対策にも役立てることができます。また、専用タブレット等でのモバイルオーダーを導入する場合は、オーダー端末のリース費用が必要です。モバイルオーダーアプリでは、オーダー端末の代わりにユーザーのスマートフォンを使用するため、オーダー端末のリース費用は不要です。

#### 2. ユーザーからの問い合わせを受け付けなども可能 

ユーザーに対して、初回の認証画面でLINE公式アカウントの友だち追加を促すことができます。LINE公式アカウントを友だち追加したユーザーには、後日、販売促進等のプッシュメッセージを送信したり、ユーザーからの問い合わせを受け付けたりできます。

#### 3. ユーザーのモバイルオーダーアプリでの操作履歴や来店履歴をもとにメッセージ配信可能 

モバイルオーダーアプリでの操作履歴や来店履歴を、LINEアカウントに紐づけて記録できます。これらの記録をもとに、リピート率を上げるなどの販売促進施策として、ユーザーに有益な情報をLINEで配信できます。

※ LINEアカウントと紐づいた行動データの取得・活用にはユーザーの許諾が必須となります。

## デモアプリケーションのシステム図とシーケンス図 

デモアプリケーションで、どのようにLINE APIを利用しているかを示した図です。

※デモアプリケーションでは実装されていない機能も図に含まれています。

**システム図**

![](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-system-diagram.webp)

- その他のサービスを利用した場合のシステム図
  - [AWSを利用したシステム図](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-system-diagram-aws.webp)
  - [Azureを利用したシステム図](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-system-diagram-azure.webp)

**シーケンス図**

![](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-sequence-diagram.webp)

- その他のサービスを利用した場合のシーケンス図
  - [AWSを利用したシーケンス図](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-sequence-diagram-aws.webp)
  - [Azureを利用したシーケンス図](https://developers.line.biz/media/line-mini-app/demo/tableorder-demo/tableorder-sequence-diagram-azure.webp)

## 関連リンク 

- [Messaging APIドキュメント](https://developers.line.biz/ja/docs/messaging-api/)
- [LINEミニアプリドキュメント](https://developers.line.biz/ja/docs/line-mini-app/)
