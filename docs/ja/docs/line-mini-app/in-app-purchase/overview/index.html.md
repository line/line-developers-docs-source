# アプリ内課金の概要

このページでは、LINEミニアプリにおけるアプリ内課金機能の概要について説明します。

アプリ内課金は、ユーザーが[認証済ミニアプリ](https://developers.line.biz/ja/docs/line-mini-app/discover/introduction/#verified-mini-app)内でデジタルコンテンツを購入できる仕組みです。

本機能はオプション機能であり、利用するには[LINE Developersコンソール](https://developers.line.biz/console/)から申請し、承認を受けることが必要です。申請について詳しくは、「[アプリ内課金の利用を申請する](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/request-iap-review/)」を参照してください。

## アプリ内課金とは 

アプリ内課金とは、LINEミニアプリが提供するデジタルコンテンツを、ユーザーが認証済ミニアプリ内で購入できる仕組みです。

現在、取り扱い可能なデジタルコンテンツは、消耗型（consumable）のみとなっています。

アプリ内課金には、以下の特徴があります。

- App StoreおよびGoogle Playの決済機構を利用する。
- LINEプラットフォームによる決済検証と通知機能を提供する。
- LIFF SDKを利用してクライアント実装を行う。
- Webhookを利用したサーバーサイド連携を行う。

実装について詳しくは、「[LINEミニアプリにアプリ内課金を組み込む](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/)」を参照してください。

## アプリ内課金を利用開始するまでの流れ 

アプリ内課金を利用開始するまでの流れは、次のとおりです。詳しくは、各ドキュメントを参照してください。

| ステップ | 内容 |
| --- | --- |
| Step 1：[アプリ内課金の利用を申請する](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/request-iap-review/) | [LINE Developersコンソール](https://developers.line.biz/console/)で、LINEミニアプリチャネルの［**アプリ内課金**］タブから利用申請を行います。申請時は、事業者名を含むすべての情報を正確に入力してください。<br>実際にユーザーがアプリ内課金を利用できるのは、認証済ミニアプリのみです。ただし、アプリ内課金の利用申請は、未認証ミニアプリでも可能です。 |
| Step 2：[アプリ内課金の設定](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-settings/)を行う | アプリ内課金の利用申請が「承認済み」のステータスになったら、［**アプリ内課金**］タブ内の［**アプリ内課金の設定**］タブで、Webhook URLやテスト決済のテスターを登録します。 |
| Step 3：開発用LINEミニアプリチャネルで[アプリ内課金を組み込み](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/)、[テスト決済する](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#test-payment-guide) | 開発用LINEミニアプリチャネルでアプリ内課金を組み込み、テスト決済を実施します。 |
| Step 4：[認証審査を申請](https://developers.line.biz/ja/docs/line-mini-app/submit/submission-guide/)する | LINE Developersコンソールの［**審査申請**］タブから、認証審査（認証済ミニアプリとして公開するための審査）を申請します。申請の際は、［**審査申請**］タブ内の［**アプリ内課金機能を公開する**］のトグルボタンをオンにしてください。<br>すでに認証済ミニアプリとして公開していたアプリにアプリ内課金を組み込んだ場合も、再度認証審査を受ける必要があります。 |
| Step 5：アプリ内課金機能が組み込まれたLINEミニアプリをリリースする | Step 4の認証審査が承認されると、アプリ内課金機能が組み込まれたLINEミニアプリがリリースできます。<br />すでに認証済ミニアプリだった場合は、手順が異なります。詳しくは、「[審査を依頼する](https://developers.line.biz/ja/docs/line-mini-app/submit/submission-guide/)」を参照してください。 |

## システム構成 

アプリ内課金は、以下の要素で構成されています。

| 要素 | 役割 |
| --- | --- |
| LINEミニアプリ | ユーザー操作を受け取り、購入処理を開始します。 |
| LINEミニアプリのサーバー | 購入処理の予約、Webhookの受信、購入結果の管理を行います。 |
| LINEプラットフォーム | ストア決済の検証、Webhookイベントの送信を行います。 |
| アプリストア | 実際の決済処理を行います。<ul><li>iOS：App Store</li><li>Android：Google Play</li></ul> |

## 対応環境 

アプリ内課金の利用条件と動作条件は次のとおりです。

### アプリ内課金の利用条件 

LINEミニアプリチャネルの「サービスを提供する地域」と「会社・事業者の所在国・地域」がいずれも「日本」のLINEミニアプリである。

### アプリ内課金の動作条件 

- 認証済ミニアプリである（※）
- LINEミニアプリのLIFF SDKのバージョンが2.26.0以上である
- LINEミニアプリがLIFFブラウザで開かれている
- ユーザーがLINEアプリに日本の電話番号を登録している
- ユーザーのLINEバージョンが15.6.0以降である

※ 未認証ミニアプリでは、開発用と審査用のLINEミニアプリでのみ動作します。

## 利用可能なアイテムと価格 

アプリ内課金で購入可能なアイテムは、LINEプラットフォーム側で事前に定義されています。

アイテムの基準価格は日本円で定義されています。

アプリ内課金で購入可能なアイテムをユーザーに表示する際は、ユーザー体験を損なわないよう、ユーザーが使用するアプリストアのリージョンにローカライズされた通貨で価格を表示する必要があります。

ユーザーが使用しているアプリストアのリージョンに合わせてローカライズされた価格は、[`liff.iap.getPlatformProducts()`](https://developers.line.biz/ja/reference/line-mini-app/#get-platform-products)メソッドで取得できます。このメソッドを使うことで、LINEミニアプリで表示される価格と、アプリストアでの決済の際に表示される価格との差異を最小限に抑えることができます。

## アプリ内課金のキャンセルについて 

LINEヤフー株式会社では、アプリ内課金を使用して完了した決済のキャンセルには対応していません。不正利用や誤操作による決済については、App StoreやGoogle Playなどの各アプリストアの最新の払い戻しポリシーを確認の上、ユーザーが直接払い戻しをリクエストするように案内してください。

- [Appleから購入したアプリやコンテンツの返金手続きをする](https://support.apple.com/ja-jp/118223)
- [Google Play の払い戻しポリシーについて](https://support.google.com/googleplay/answer/2479637?hl=ja)

## 処理フローの例 

アプリ内課金の基本的な処理フローの一例です。

![](https://developers.line.biz/media/line-mini-app/in-app-purchase/flow.png)

- 1～5：[アプリ内課金が利用可能な環境かを確認](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#check-the-environment)する
- 6～9：[購入可能なアイテムの一覧を取得](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#get-item-information)し、ユーザーに表示する
- 10～13：ユーザーから[アプリ内課金利用に関する同意を取得](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#get-user-consent)する
- 14～21：LINEミニアプリのサーバーから[購入処理の予約](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#reserve-payment)を行う
- 22～30：アプリストア（App Store、Google Play）での[購入処理を開始](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#start-transaction)する
- 31～36：[Webhookを受信し、購入完了を確認してアイテムを付与](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#receive-webhook)する
