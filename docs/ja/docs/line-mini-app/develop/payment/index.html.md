# 決済システムを利用する

ユーザーに決済システムを提供するために、LINEミニアプリにLINE Payや他の決済システムを利用できます。また日本のみ、[LINEミニアプリのアプリ内課金](https://developers.line.biz/ja/docs/line-mini-app/develop/payment/#in-app-purchase)機能を利用できます。

<!-- note start -->

**日本国内におけるLINE Payのサービスを終了しました**

2025年4月30日をもって、日本国内におけるLINE Payのサービスを終了しました。詳しくは、「[LINE Payサービス終了に関するお知らせ](https://line-pay-info.landpress.line.me/payment-info/)」を参照してください。

なお、台湾、タイ現地のLINE Payのサービスは引き続き利用できます。

<!-- note end -->

<!-- tip start -->

**ヒント**

クレジットカードの情報などをLINEミニアプリで入力することを避けるために、決済はLINE Payで処理することをお勧めします。

<!-- tip end -->

## LINE Pay 

### LINE Pay加盟店アカウントの準備 

LINEミニアプリでLINE Payを利用するには、まずLINE Pay加盟店のアカウントが必要です。LINE Pay加盟店のアカウントがない場合は、[LINE Payの公式ホームページ](https://pay.line.me/portal/jp/main)から申し込んでください。

### LINE Payを利用するサービスの開発 

加盟店のアカウントの申請が承認を受けたら、LINEミニアプリでLINE Payを利用するように実装します。LINE Payについて詳しくは、LINE Pay Developersの『[Online paymentドキュメント](https://developers-pay.line.me/online)』を参照してください。

LINE Payを利用する際は、以下のような流れで決済を処理します。

1. LINEミニアプリでユーザーが決済を開始するときに、LINE Payの処理を開始します。

   LINEミニアプリが表示する画面：<br>![](https://developers.line.biz/media/line-mini-app/mini_linepay_flow01.png)

2. ユーザーがLINE Payで決済内容を確認して、LINE Payの認証情報を入力します。

   LINE Payが表示する画面：<br>![](https://developers.line.biz/media/line-mini-app/mini_linepay_flow02.png)

3. 注文の確認ページを表示します。

   LINEミニアプリが表示する画面：<br>![](https://developers.line.biz/media/line-mini-app/mini_linepay_flow03.png)

### LINE Payテスト 

決済に関するテストは、LINE Payが提供している[Sandbox](https://developers-pay.line.me/sandbox)を利用できます。

## LINEミニアプリのアプリ内課金 

[アプリ内課金](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/overview/)とは、LINEミニアプリ内で提供するデジタルコンテンツを、ユーザーが購入できる仕組みです。LINEアプリ内でLINEミニアプリを起動してデジタルコンテンツの購入を開始し、App StoreまたはGoogle Playの決済機構を利用して決済するというものです。

現在、アプリ内課金を利用できるのは日本のみです。利用条件等について詳しくは、「[アプリ内課金の概要](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/overview/)」を参照してください。

## 他の決済方法 

LINEミニアプリで、LINE Pay以外の決済方法を提供するには、一般のウェブページで決済を提供して処理するのと同様に実装してください。なお、外部のドメインや外部のアプリで決済を完了した後、ユーザーがLINEミニアプリのページに戻るようにしてください。
