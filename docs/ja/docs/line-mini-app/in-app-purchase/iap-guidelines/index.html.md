# アプリ内課金 開発ガイドライン

このページでは、LINEミニアプリでアプリ内課金機能を利用する際の仕様上の制約、設計上の注意点、および推奨される実装方針について説明します。

アプリ内課金機能を利用する際は、以下の開発ガイドラインに従ってください。また、[LINEミニアプリ開発ガイドライン](https://developers.line.biz/ja/docs/line-mini-app/development-guidelines/)も必ず参照してください。

**禁止事項**

- [IPアドレスによるアクセス制限の禁止](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-guidelines/#prohibit-ip-address-restriction)

**必須事項**

- [アクセストークンを検証する](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-guidelines/#verify-access-token)

**推奨事項**

- [Webhookの署名検証を行う](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-guidelines/#verify-webhook-signature)
- [重複を排除する](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-guidelines/#eliminate-duplicates)
- [適切なエラーハンドリングを行う](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-guidelines/#error-handling)
- [決済通知を重複して送信しない](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-guidelines/#payment-notifications)

## 禁止事項 

### IPアドレスによるアクセス制限の禁止 

Webhookを受信するサーバーにおいて、Webhookリクエスト送信元のLINEプラットフォームのIPアドレスでアクセス制限をしないでください。LINEプラットフォームのIPアドレスは開示していません。また、IPアドレスは予告なく変更される場合があります。不正なアクセス元からのリクエストを拒否したい場合は、IPアドレスによる制限ではなく、[Webhookの署名の検証](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-guidelines/#verify-webhook-signature)を実施してください。

## 必須事項 

### アクセストークンを検証する 

購入予約を行う際は、[アクセストークンの有効性を検証する](https://developers.line.biz/ja/reference/line-login/#verify-access-token)エンドポイントを使用して、LINEミニアプリのサーバー側でアクセストークンの有効性、チャネルID、アクセストークンの有効期間を必ず検証してください。

## 推奨事項 

### 非破壊的な変更を想定した実装を行う 

LINEミニアプリのアプリ内課金では、非破壊的な機能追加が行われることがあります。これらの変更は、既存の機能を壊すことなく、APIを拡張することを目的としています。このため以下のような変更は、事前の予告なく実施されることがあります。

- 新しいエンドポイントの追加
- APIリクエストにおける省略可能なパラメータやフィールド、ヘッダーの追加
- APIレスポンスにおけるフィールドやヘッダーの追加
- 列挙型の値の追加
- Webhookイベントオブジェクトへのプロパティの追加
- APIレスポンスおよびWebhookイベントオブジェクトのプロパティの順序の変更
- データの要素間の空白や改行の有無

これらの非破壊的な機能追加に対しても不具合なく動作するよう、サーバーを実装してください。

### Webhookの署名検証を行う 

偽装リクエストを防ぐため、リクエストヘッダーの`x-line-signature`を使用して署名の検証を行ってください。

- リクエストボディのダイジェストを計算します。チャネルシークレットを秘密鍵としてHMAC-SHA256アルゴリズムを使用します。
- ダイジェストをBase64エンコードし、リクエストヘッダーの`x-line-signature`に含まれる署名と一致するかどうかを確認します。

Javaでの署名検証の例

```java
class WebhookProcessor {
    void verify(String httpRequestBody) { // Request body string
        String channelSecret = '...'; // Channel secret string
        SecretKeySpec key = new SecretKeySpec(channelSecret.getBytes(), "HmacSHA256");
        Mac mac = Mac.getInstance("HmacSHA256");
        mac.init(key);

        byte[] source = httpRequestBody.getBytes("UTF-8");
        String signature = Base64.encodeBase64String(mac.doFinal(source));
        // Compare x-line-signature request header string and the signature
    }
}
```

Webhookの署名検証については、『Messaging APIドキュメント』の「[Webhookの署名を検証する](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-signature/)」を参照してください。

### 重複を排除する 

ネットワーク状況により、同一のWebhookイベントが複数回通知される可能性があります。注文ID（`orderId`）を用いて、1つの購入に対して重複してアイテムを付与しないよう実装してください。また、ユーザーがアプリストアでの決済をキャンセルした場合も、重複して処理しないようにしてください。

### 適切なエラーハンドリングを行う 

購入予約は、課金の完了を保証するものではありません。ネットワークエラーなどが発生した場合は、リトライやユーザーに再試行を促す案内を適切に行ってください。

### 決済通知を重複して送信しない 

購入完了時には、LINE公式アカウント「LINEアプリ内課金お知らせ」からユーザーに自動的にメッセージが送信されます。また、ユーザーがアプリストアでの決済をキャンセルした場合も、同様にユーザーに自動的にメッセージが送られます。

これとは別に他のLINE公式アカウントから決済通知を送信した場合、ユーザーとしては何度も同様の通知を受け取ることになります。ユーザー体験の悪化を避けるため、二重に通知することは控えてください。
