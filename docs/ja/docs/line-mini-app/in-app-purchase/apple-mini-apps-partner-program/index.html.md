# Mini Apps Partner ProgramによるApp Store決済の手数料減額

このページでは、Apple Inc.が提供するMini Apps Partner Programについて、LINEミニアプリのアプリ内課金における手数料減額の仕組み、申し込み条件と方法、およびプログラム適用後の影響を説明します。

<!-- table of contents -->

## Mini Apps Partner Programとは 

[Mini Apps Partner Program](https://developer.apple.com/jp/programs/mini-apps-partner/)は、アプリ内課金にかかる手数料を減額できるプログラムです。アプリ内課金の利用が承認されたLINEミニアプリであれば、任意で申し込むことができます。

Mini Apps Partner ProgramがLINEミニアプリに適用されると、App Store（iOS）での決済による販売代金の支払いにかかるApple Inc.に対する手数料が減額されます。Mini Apps Partner Programの適用により、手数料が減額された場合、LINEヤフー株式会社がApp Storeに支払う手数料相当額も減額されるため、「[LINEアプリ内課金利用規約（LINEミニアプリ提供者向け）](https://terms2.line.me/LINE_MINI_App_IAP?lang=ja)」に基づき、販売総額から控除される金額も減額されます。

## Mini Apps Partner Programの申し込み条件 

Mini Apps Partner Programには、[アプリ内課金](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/overview/)の利用申請が承認されているLINEミニアプリのみ申し込むことができます。

アプリ内課金の利用を申請していない場合は、「[アプリ内課金の利用を申請する](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/request-iap-review/)」の手順に従って申請してください。

## Mini Apps Partner Programへの申し込み 

Mini Apps Partner Programへの申し込みは、LINE DevelopersコンソールでLINEミニアプリの認証審査を申請する際に行うことができます。プログラムを適用したいLINEミニアプリごとに申請してください。

詳しくは、「[Mini Apps Partner Programに申し込む](https://developers.line.biz/ja/docs/line-mini-app/submit/submission-guide/#apply-for-program)」を参照してください。

## 手数料減額の適用について 

Mini Apps Partner ProgramはLINEミニアプリ単位で適用されますが、手数料の減額は個々の決済単位で判定されます。

なお、プログラムが適用されないApp Storeでの決済、Google Playでの決済、およびテスト決済には、手数料の減額は適用されません。

### 年齢範囲の確認について 

Mini Apps Partner Programが適用されたLINEミニアプリでは、ユーザーがLINEミニアプリを起動するときに年齢範囲の確認が行われる場合があります。年齢範囲の確認には、Apple Inc.が提供する[Declared Age Range API](https://developer.apple.com/documentation/declaredagerange)が使用される場合があります。LINEミニアプリでの実装は不要です。

ユーザーが年齢範囲の共有を拒否するなど、年齢範囲を確認できない場合や、ユーザーが利用している端末で年齢範囲の確認に対応していない場合に、次の制限が適用されることがあります。

- そのユーザーによる決済にかかる手数料が、減額の対象とならないことがあります。
- そのユーザーによるLINEミニアプリの利用が制限され、LINEミニアプリが起動せずに閉じられることがあります。

<!-- note start -->

**年齢範囲の確認に使用された情報はサービス事業主に提供されません**

Mini Apps Partner Programの適用に伴う年齢範囲の確認で使用または確認された、ユーザーの年齢、生年月日、年齢範囲などの年齢関連情報は、LINEミニアプリのサービス事業主には提供されません。

<!-- note end -->

## 手数料減額が適用された決済の実装について 

決済に手数料の減額が適用されるかどうかの判定は、LINEプラットフォームが行います。そのため、Mini Apps Partner Programの適用有無によって、アプリ内課金の購入処理を分ける必要はありません。すでにアプリ内課金機能を実装している場合は、プログラム適用に伴うコードの変更は不要です。

購入処理について詳しくは、「[LINEミニアプリにアプリ内課金を組み込む](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/)」を参照してください。

## 手数料減額が適用された決済のWebhookイベント 

[購入完了イベント](https://developers.line.biz/ja/reference/line-mini-app/#purchase-complete-event)および[返金イベント](https://developers.line.biz/ja/reference/line-mini-app/#refund-event)では、決済にMini Apps Partner Programによる手数料の減額が適用された場合、`paymentBenefitProgram`プロパティの値として`APPLE_MINI_APPS_PARTNER_PROGRAM`が返されます。手数料の減額が適用されていない場合、このプロパティは含まれません。

`paymentBenefitProgram`プロパティは、手数料の減額が適用された決済を識別するための補助情報です。購入結果や、ユーザーに付与するアイテムには影響しません。

以下は、手数料の減額が適用された決済の購入完了イベントの例です。

```json
{
  "type": "purchaseComplete",
  "orderId": "T2025020710000002126002",
  "productId": "iap_ln_002",
  "userId": "U91FC5A...",
  "purchaseTimestamp": 1738672496,
  "channelId": "12345...",
  "paymentBenefitProgram": "APPLE_MINI_APPS_PARTNER_PROGRAM"
}
```

## LINEミニアプリ間を遷移する際の注意事項 

別のLINEミニアプリからMini Apps Partner Programが適用されたLINEミニアプリへ遷移する場合は、年齢範囲の確認を適切なタイミングで行うため、ウェブアプリのエンドポイントURLではなく、遷移先の[LIFF URL](https://developers.line.biz/ja/glossary/#liff-url)または[パーマネントリンク](https://developers.line.biz/ja/docs/line-mini-app/develop/permanent-links/)を使用してください。
