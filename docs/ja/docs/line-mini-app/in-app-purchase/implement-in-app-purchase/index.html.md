# LINEミニアプリにアプリ内課金を組み込む

このページでは、LINEミニアプリにアプリ内課金機能を組み込む方法について説明します。

## 事前準備 

実装を開始する前に、以下が完了していることを確認してください。

- LINEミニアプリが認証済ミニアプリとして公開されている、または未認証ミニアプリの場合は開発用のチャネルが使用できる
- [アプリ内課金機能の利用申請](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/request-iap-review/)が承認されている
- LINEミニアプリのサーバーが用意されている
- Webhookの受信エンドポイント（Webhook URL）が用意されている （※）

※ Webhook URLは、アプリ内課金の利用申請が承認された後に、[LINE Developersコンソール](https://developers.line.biz/console/)で登録します。登録方法について詳しくは、「[Webhook URLを登録する](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-settings/#register-webhook-url)」を参照してください。

## 実装の流れ 

アプリ内課金は、以下の流れで組み込みます。

1. [アプリ内課金が利用可能な環境かを確認する](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#check-the-environment)
1. [購入可能なアイテムの情報を取得する](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#get-item-information)
1. [ユーザーからアプリ内課金利用の同意を取得する](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#get-user-consent)
1. [LINEミニアプリのサーバーから購入処理を予約する](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#reserve-payment)
1. [ストアでの購入処理を開始する](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#start-transaction)
1. [Webhookを受信して購入完了を処理する](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#receive-webhook)

### 1. アプリ内課金が利用可能な環境かを確認する 

[`liff.isApiAvailable()`](https://developers.line.biz/ja/reference/liff/#is-api-available)メソッドを呼び出して、アプリ内課金が利用可能な環境かを確認します。

```javascript
liff.isApiAvailable("iap");
```

外部ブラウザを使用している場合や、ユーザーが使用しているLINEアプリのバージョンがアプリ内課金に非対応である場合などは、LINEミニアプリを利用不可にしたり、購入導線を表示しないようにしたりするなどの制御をしてください。

`liff.isApiAvailable()`メソッドを使い、アプリ内課金に対応している環境であることが確認できた場合でも、「[3. ユーザーからアプリ内課金利用の同意を取得する](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#get-user-consent)」においてユーザーからの同意を得ることができない場合や、後から同意が撤回された場合は、アプリ内課金を利用できません。

### 2. 購入可能なアイテムの情報を取得する 

購入可能なアイテム情報を取得し、ユーザーに表示します。

アプリ内課金で購入可能なアイテムは、日本円を基準にしてLINEヤフー株式会社によって事前に定義されています。アプリ内課金で購入可能なアイテムをユーザーに表示する際には、ユーザー体験を損ねないように、ユーザーが使用するアプリストアのリージョンにローカライズされた価格と通貨の値を用いて表示してください。

事前に定義されているアイテムのうち、LINEミニアプリでサポートするアイテムは、アプリ内課金を利用するサービス事業主のポリシーに従って定めることができます。[`liff.iap.getPlatformProducts()`](https://developers.line.biz/ja/reference/line-mini-app/#get-platform-products)メソッドに指定して呼び出すことで、それらのアイテムについて、ローカライズされた価格、通貨、およびアイテム名を取得できます。

```javascript
const productIds = ["iap_ln_002", "iap_ln_003"];
await liff.iap.getPlatformProducts({ productIds });
```

例:

```json
{
  "iap_ln_002": {
    "currency": "JPY",
    "price": 100,
    "productName": "LINE Purchase 100"
  },
  "iap_ln_003": {
    "currency": "JPY",
    "price": 150,
    "productName": "LINE Purchase 150"
  }
}
```

### 3. ユーザーからアプリ内課金利用の同意を取得する 

[`liff.iap.requestConsentAgreement()`](https://developers.line.biz/ja/reference/line-mini-app/#request-consent-agreement)メソッドを使用して、「[LINEアプリ内課金利用規約](https://terms.line.me/line_iap_tou_1)」に対するユーザーの同意を取得します。

```javascript
await liff.iap.requestConsentAgreement();
```

このプロセスは、LINEミニアプリごとではなく、ユーザーごとに一度だけ完了する必要があります。ユーザーが他のLINEミニアプリですでにアプリ内課金の利用に同意している場合は、再同意は不要です。起動中のLINEミニアプリですでに同意が得られている場合も、再同意は必要ありません。

ただし、LINEアプリ内課金利用規約が更新された場合、再度の同意が必要になることがあります。同意を得ていないユーザーが、購入処理の予約および購入処理を開始することはできません。したがって、アプリ内課金を開始する際には、常に`liff.iap.requestConsentAgreement()`メソッドを呼び出して、最新の同意状況を確認する必要があります。

`liff.iap.requestConsentAgreement()`メソッドの実行時に、ユーザーによる同意が完了しておらず、同意が新たに必要な場合は、その場で同意画面が表示されます。同意画面の表示に伴うユーザーの離脱を避けるために、適切なタイミングで同意のリクエストを行うことを推奨します。

### 4. LINEミニアプリのサーバーから購入処理を予約する 

アプリストア（App Store、Google Play）での購入処理を開始する前に、LINEミニアプリのサーバーから「[購入処理を予約する](https://developers.line.biz/ja/reference/line-mini-app/#reserve-purchase)」エンドポイントで購入処理の予約を行います。

LINEミニアプリのサーバーから購入処理の予約は、「ユーザーがLINEミニアプリ上でアイテムの購入ボタンを押した」等のタイミングで行ってください。

購入処理の予約時に追加で必要となるパラメータについては、以下の方法で取得します。

- 認証時のアクセストークンは[`liff.getAccessToken()`](https://developers.line.biz/ja/reference/liff/#get-access-token)メソッドで取得されるユーザーアクセストークンを取得して指定してください。
- `clientIp`はLINEミニアプリのサーバーで取得したユーザーのIPアドレスを指定してください。
- `clientOs`は[`liff.getOS()`](https://developers.line.biz/ja/reference/liff/#get-os)メソッドで取得される値を指定してください。

この時点では、購入はまだ完了していません。たとえば、購入処理の予約が成功した場合でも、その後ユーザーがLINEミニアプリから離脱したり、アプリストアの購入処理をキャンセルしたりした場合は、実際の購入は完了しないということに注意してください。

購入処理の予約時にレスポンスから取得できる注文ID（`orderId`の値）は、決済の完了時にLINEプラットフォームから送信されるWebhookのパラメータとしても含まれます。この`orderId`の値については当社への問い合わせや調査等に必要であるため、ログやストレージに記録してください。

また、レスポンスに含まれる`x-line-request-id`ヘッダーの値についても同様に記録し、`orderId`の値と合わせてお問い合わせください。

### 5. ストアでの購入処理を開始する 

購入予約が完了したら、LINEミニアプリから[アプリストア決済](https://developers.line.biz/ja/reference/line-mini-app/#create-payment)を開始します。

```javascript
await liff.iap.createPayment({
  productId,
  orderId,
});
```

購入処理が成功すると、LINEプラットフォーム側でストアに問い合わせが行われ、決済が正しく行われたことを検証します。決済が正しく行われたことが検証された場合に、事前に設定されたWebhookのエンドポイントURLに対し、LINEプラットフォームから購入完了のWebhookイベントを通知します。通知されるWebhookイベントについて詳しくは、『LINEミニアプリAPIリファレンス』の「[購入完了イベント](https://developers.line.biz/ja/reference/line-mini-app/#purchase-complete-event)」を参照してください。

購入がキャンセルされた場合や購入処理が失敗した場合は、例外が発生します。必要に応じてエラーハンドリングを実装してください。

```javascript
try {
  await liff.iap.createPayment({
    productId,
    orderId,
  });
} catch (e) {
  // e => { code: "CANCELED", message: "Transaction was canceled." }
  console.error({
    code: e.code,
    message: e.message,
  });
}
```

### 6. Webhookを受信して購入完了を処理する 

LINEプラットフォームから通知された[購入完了](https://developers.line.biz/ja/reference/line-mini-app/#purchase-complete-event)のWebhookイベントを受信したら、LINEミニアプリのサーバーで中身を確認し、ユーザーにアイテムを付与してください。ユーザーにアイテムを付与する具体的な処理については、開発しているLINEミニアプリの実装によって異なります。

Webhookイベントの特性上、ネットワークやアプリケーションに起因するエラーなどにより、同一のイベントが複数回通知される可能性があります。また、LINEミニアプリのサーバーで特定の購入完了イベントを正常に受信した場合でも、LINEプラットフォーム側で受信されたことを確認できなかった場合については、同一のイベントが再通知される可能性があります。

ユーザーの購入については、[購入の予約](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#reserve-payment)時に発行されたユニークな`orderId`が割り当てられています。`orderId`を使用して処理済みかどうかを判定してください。また、1つの購入に対して、アイテム付与は1回のみ行ってください。

購入完了の判断は、必ずWebhookイベントを基準に行ってください。

#### Webhookの署名を検証する 

Webhookを受信したら、偽装リクエストを防ぐため、リクエストヘッダーの`x-line-signature`を使用して署名の検証を行ってください。詳しくは、「[Webhookの署名検証を行う](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-guidelines/#verify-webhook-signature)」を参照してください。

#### Webhookへのレスポンス 

LINEプラットフォームでは、LINEミニアプリのサーバーからのレスポンスの内容は確認しないため、任意のペイロードを返すことができます。

ただし、サーバーでWebhookを正常に受信した場合は、200番台のステータスコードを返す必要があります。

他のステータスコード（300番台、400番台、500番台など）が返されると、LINEプラットフォームは失敗として認識し、Webhookの再送を試みます。再送は30分以内に複数回行われます。

#### Webhookイベントの履歴を取得する 

「[Webhookイベントの履歴を取得する](https://developers.line.biz/ja/reference/line-mini-app/#webhook-events-history)」エンドポイントを利用すると、過去に送信されたWebhookイベントの履歴を取得できます。

受信に失敗したWebhookイベントについて開発者側でリカバリーなどの実施が必要な場合は、このエンドポイントを利用してください。

詳しくは、『LINEミニアプリAPIリファレンス』の「[Webhookイベントの履歴を取得する](https://developers.line.biz/ja/reference/line-mini-app/#webhook-events-history)」を参照してください。

## テスト決済のガイド 

LINEミニアプリにアプリ内課金機能を組み込むための実装が終わると、開発用LINEミニアプリチャネルにおいてテスト決済が可能になります。テスト決済では、アイテムの購入、[購入履歴の確認](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#purchase-history)など、一連の動作をLINEアプリ上で確認できます。

テスター権限を持つアカウントが開発用チャネルで決済処理を行うと、システム側でテスト決済として扱うため、実際の決済処理を伴わずに課金フローをテストできます。

テスト決済を行うユーザーは、次の条件をすべて満たしている必要があります。

- [当該LINEミニアプリチャネルのAdminまたはTester権限](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#channel-permission)を持っている
- [テスト決済機能のテスター権限](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#tester-permission)を持っている

### LINEミニアプリチャネルの権限 

LINEミニアプリのテスト決済機能を利用するには、LINEミニアプリチャネルのAdmin権限またはTester権限が必要です。権限の設定は、[LINE Developersコンソール](https://developers.line.biz/console/)の［**権限設定**］タブで行います。

権限の設定方法について詳しくは、『LINE Developersコンソールドキュメント』の「[チャネルで開発者の追加、開発者権限の編集、または開発者の削除をする](https://developers.line.biz/ja/docs/line-developers-console/managing-roles/#role-settings-for-channel)」を参照してください。

なお、チャネルの権限を追加／編集できるのは、チャネルのAdmin権限を持つ開発者のみです。権限の違いについて詳しくは、『LINE Developersコンソールドキュメント』の「[LINEミニアプリチャネル](https://developers.line.biz/ja/docs/line-developers-console/managing-roles/#roles-for-channel-line-mini-app)」を参照してください。

### テスト決済機能のテスター権限 

テスト決済機能のテスター権限を付与できる対象は、当該LINEミニアプリチャネルのAdminまたはTester権限を持つ開発者です。テスター権限は、LINE Developersコンソールの［**アプリ内課金**］タブ内にある［**アプリ内課金の設定**］タブで設定します。

設定方法について詳しくは、「[テスターを登録する](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-settings/#register-testers)」を参照してください。

### テスト決済の手順

テスト決済を行うと、実際の金銭の決済処理を発生させずに、動作を確認することができます。

テストの手順は次のとおりです。

1. 当該LINEミニアプリチャネルで[テスターを登録](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-settings/#register-testers)します。
1. テスターに、開発用LINEミニアプリのLIFF URLを共有します。LIFF URLは、LINE Developersコンソールの［**ウェブアプリ設定**］タブで確認できます。
1. テスターは、指定されたLIFF URLからLINEミニアプリを起動し、決済を行います。

## 運用のための確認事項 

実際にアプリ内課金サービスを運用する場合の確認事項は次のとおりです。

### 決済成功時のユーザーへの通知 

決済が完了すると、LINEヤフー株式会社の「LINEアプリ内課金お知らせ」LINE公式アカウントから、購入したユーザーに自動的にメッセージが送信されます。そのため、開発者側で追加の対応を行う必要はありません。

このアカウントは、ユーザーがブロックしたり、通知設定を変更することはできません。ただし、まれにユーザーの利用環境やサーバーの状況により、通知が届かない場合があります。あらかじめご了承ください。

### ユーザーが購入履歴を確認する方法 

ユーザーは、LINEアプリの「設定」画面の［**アプリ内課金**］を開くか、LINE公式アカウント「LINEアプリ内課金お知らせ」から送信されたメッセージからアプリ内課金の履歴を確認できます。最大1年間の決済履歴が確認可能です。

下図の「アプリ内課金」画面における赤枠の値については、[アプリ内課金の利用を申請する](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/request-iap-review/)時点や、[購入予約リクエスト](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#reserve-payment)時点、ユーザーがストアで購入する際の実際の価格と通貨が反映されます。

![](https://developers.line.biz/media/line-mini-app/in-app-purchase/purchase-history-ja.png)

| 番号 | 内容 |
| --- | --- |
| 1 | 購入処理の予約時に指定されたアイテム名（[`shopProductName`](https://developers.line.biz/ja/reference/line-mini-app/#reserve-purchase-request-body)）をそのまま表示します。ユーザーが購入したアイテムを認識できるように適切な値を設定してください。 |
| 2 | アプリ内課金を利用した当社のサービス名と、アプリ内課金を利用するサービス事業主のサービス名を表示します。なお、サービス事業主のサービス名については、現時点では多言語対応していません。<br><ul><li>言語設定が日本語の場合：`LINEミニアプリ <サービス事業主のサービス名>`</li><li>その他の場合：`LINE MINI App <サービス事業主のサービス名>`</li></ul> |
| 3 | アプリストアに関連する情報を表示します。決済したアプリストア（App Store、Google Playのいずれか）、アプリストアに登録されているアイテム名が表示されます。 |
| 4 | 決済時間を表示します。LINEプラットフォームがストアでの決済処理を確認した時刻が表示されます。 |
| 5 | 決済時の通貨と価格が表示されます。ストアの決済処理において、ユーザーが使用するアプリストアのリージョンに基づいて通貨変換が行われ決済処理が行われますが、その際に実際に決済した通貨および価格が表示されます。 |
