# モジュールチャネルの設定を行う

<!-- note start -->

**オプション機能を利用するには手続きが必要です**

本ドキュメントに記載の機能は、所定の申請等を行った法人ユーザーのみがご利用いただけます。モジュールを利用した拡張機能の公開を希望するお客様は、担当営業までご連絡いただくか、[LINEマーケットプレイス お問い合わせ](https://line-marketplace.com/jp/inquiry)よりお問い合わせください。

<!-- note end -->

モジュールチャネルでは、[LINE Developersコンソール](https://developers.line.biz/console/)に専用の［**モジュール**］タブが表示されます。

［**モジュール**］タブでは、モジュールチャネルのWebhook URLおよびWebhook利用のオン・オフと、[LINE公式アカウントの管理者に認可を要求する](https://developers.line.biz/ja/docs/partner-docs/module-technical-attach-channel/#request-auth-from-line-oa-admin)際に指定する`redirect_uri`を設定できます。

![LINE Developersコンソール上のモジュールタブ](https://developers.line.biz/media/partner-docs/module-technical/module-tab-in-console-ja.png)

## 1. モジュールタブ 

［**モジュール**］タブはモジュールチャネル専用の設定項目です。

## 2. Webhook設定 

### Webhook URL 

モジュールチャネルのWebhook URLを1つ設定できます。[Webhookを受信する](https://developers.line.biz/ja/docs/partner-docs/module-technical-using-messaging-api/#get-webhook)も参照してください。

### Webhookの利用 

モジュールチャネルがWebhookイベントを受信するかどうかを設定できます。

### Webhookの再送 

モジュールチャネルのWebhook URLにおいてWebhookイベントの受信に失敗した際に、LINEプラットフォームからWebhookイベントを再送するかどうかを設定できます。

### エラーの統計情報 

Webhookイベントの受信失敗に関する統計情報を［**Webhookエラー**］タブで表示するかどうかを設定できます。

## 3. リダイレクト設定 

### リダイレクトURL 

リダイレクトURLには、[LINE公式アカウントの管理者に認可を要求](https://developers.line.biz/ja/docs/partner-docs/module-technical-attach-channel/#request-auth-from-line-oa-admin)する際に使用する、`redirect_uri`パラメータの値を指定してください。リダイレクトURLのスキームは、`https`である必要があります。

なお、1つのチャネルに対して、複数のリダイレクトURLを指定できます。
