# Webhookの署名を検証する

ボットサーバーにWebhookのリクエストが届いたら、[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)を処理する前に、リクエストヘッダーに含まれる署名を検証してください。署名の検証は、開発者のボットサーバーに届いたリクエストが「LINEプラットフォームから送信されたWebhookか」および「通信経路で改ざんされていないか」などを確認するための重要な手順です。

![署名の検証のイメージ](https://developers.line.biz/media/partner-docs/webbhook-signature-verification-ja.png)

<!-- tip start -->

**Webhookの署名を検証を行うことを推奨します**

Webhookの署名を検証は、セキュリティ担保のための重要な手段のひとつです。Webhookの署名を検証を行うことは、[Messaging API開発ガイドライン](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/#verify-webhook-signature)でも推奨しています。

<!-- tip end -->

<!-- tip start -->

**LINEプラットフォームのIPアドレスは開示していません**

Webhookの送信元であるLINEプラットフォームのIPアドレスは開示していません。IPアドレスによるアクセス制御ではなく、署名の検証によってセキュリティを担保してください。

<!-- tip end -->

## 署名検証に必要な事前準備 

Webhookの署名の検証を行うには、Messaging APIチャネルのチャネルシークレットが必要です。

### チャネルシークレットを取得する 

[LINE Developersコンソール](https://developers.line.biz/console/)でチャネルの［**チャネル基本設定**］タブを開き、チャネルシークレットを取得してください。チャネルシークレットを取得するには、チャネルのAdmin権限が必要です。

![](https://developers.line.biz/media/messaging-api/verify-webhook-signature/channel-secret-ja.png)

チャネルシークレットは、LINEプラットフォームと開発者だけが知っている秘密鍵です。このチャネルシークレットを署名検証のハッシュ鍵として用いますので、ボットサーバーで適切に管理してください。

#### チャネルシークレットの再発行 

チャネルシークレットは、[LINE Developersコンソール](https://developers.line.biz/console/)の［**チャネル基本設定**］タブで［**発行**］を押すことで再発行できます。チャネルシークレットが漏えいした懸念がある場合は、チャネルシークレットを再発行してください。チャネルシークレットを再発行するには、チャネルのAdmin権限が必要です。

新しいチャネルシークレットを発行すると、現在のチャネルシークレットは無効になります。チャネルシークレットの再発行は、既存のチャネルシークレットを利用していたサービスへの影響を十分に調査してから行ってください。

LINEプラットフォームが、開発者に断りなくチャネルシークレットを再発行することはありません。

## 署名検証の仕組み 

ここでの署名の検証とは、Webhookの送信者（LINEプラットフォーム）と受信者（開発者が運営するボットサーバー）の双方が、同じハッシュ鍵を用いて計算を行い、計算結果である署名の一致をもってそのWebhookの正当性を確認することを指します。

![](https://developers.line.biz/media/messaging-api/verify-webhook-signature/webhook-validation-flow.png)

署名検証の仕組みを順を追って説明します。

1. [LINEプラットフォームがボットサーバーにWebhookを送信する](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-signature/#line-platform-sends-webhook-request)
1. [ボットサーバーがWebhookを受信する](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-signature/#receiving-webhook-request)
1. [ボットサーバーでWebhookの署名を検証する](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-signature/#signature-validation)

### LINEプラットフォームがボットサーバーにWebhookを送信する 

LINEプラットフォームは、Webhookを送信する際に、以下の手順で署名を作成します。

1. [Webhookイベント](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)を入力データ、チャネルシークレットをハッシュ鍵として、HMAC-SHA256で署名を生成します。
2. 生成した署名を`x-line-signature`ヘッダーにセットします。
3. Webhookイベントと署名（`x-line-signature`）を、ボットサーバーに送信します。

![](https://developers.line.biz/media/messaging-api/verify-webhook-signature/line-platform-sends-webhook-request.png)

### ボットサーバーがWebhookを受信する 

ボットサーバーは、LINEプラットフォームからのWebhookを受信します。

受信したWebhookの[リクエストヘッダー](https://developers.line.biz/ja/reference/messaging-api/#request-headers)に含まれる署名（`x-line-signature`）、およびリクエストボディの文字列には変更を加えず、そのままメモリやデータベースに保存してください。

<!-- note start -->

**署名の検証を行う前にデータの変更をしないでください**

署名の検証を行う前に、署名やリクエストボディの文字列に何らかの変更（文字列の置換、デシリアライズ、エスケープ処理など）をしてしまうと、第三者によって改ざんされたリクエストと区別ができなくなり、署名の検証に失敗します。リクエストボディの文字列にバックスラッシュ（`\`）や改行（`\n`）といった特殊なエスケープ文字が含まれているか否かは関係ありません。どのようなリクエストであっても署名の検証を行うより前にデータを変更しないでください。

<!-- note end -->

### ボットサーバーでWebhookの署名を検証する 

ボットサーバーは、LINEプラットフォームから送信されたWebhookを、以下の手順で検証します。

1. 受信したWebhookのリクエストボディの文字列を入力データ、ボットサーバーで管理していたチャネルシークレットをハッシュ鍵として、HMAC-SHA256で署名を生成します。
1. 受信した署名（`x-line-signature`）と、生成した署名を比較します。
1. 署名が一致した場合、受信したWebhookはLINEプラットフォームから送信され、改ざんされることなくボットサーバーに到達したものであることが保証されます。
1. 署名が一致した場合は、Webhookイベントの内容に応じた処理を行ってください。

![](https://developers.line.biz/media/messaging-api/verify-webhook-signature/signature-validation.png)

2つの署名が不一致だった場合や、Webhookのリクエストヘッダーに署名が含まれていなかった場合は、Webhookイベントの内容に応じた処理は行わず、エラーとして終了してください。署名が不一致だった場合は、以下の理由が考えられます。

- ボットサーバーに届いたリクエストがLINEプラットフォーム以外から送信されたものである
- ボットサーバーに届いたWebhookが第三者によって改ざんされたものである
- ボットサーバーで署名を検証する方法に誤りがある

LINEプラットフォームから送信されたWebhookであれば、LINE Developersコンソールの［**エラーの統計情報**］で送信を試みたWebhookの履歴が確認できます。エラーの統計情報を確認する方法について詳しくは、「[Webhookのエラーの原因と統計情報を確認する](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/)」を参照してください。

LINEプラットフォームから送信されたWebhookであるにも関わらず署名が不一致になる場合は、ボットサーバーで署名を検証する方法に誤りがあると考えられます。詳しくは、「[署名検証のよくある失敗とその解決方法](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-signature/#common-signature-verification-failures-and-their-solutions)」を参照してください。

## 署名検証の手順

`openssl`コマンドを使用して、署名検証の手順を確認してみましょう。

まずは[LINE Developersコンソール](https://developers.line.biz/console/)からチャネルの［**Messaging API設定**］タブを開き、Webhook URLの［**検証**］ボタンを押して、LINEプラットフォームから疎通確認のWebhookを送信します。

![検証ボタンを押すと疎通確認のWebhookが送信される](https://developers.line.biz/media/news/webhook-url.png)

1. ボットサーバーに届いたWebhookのリクエストボディ
   ```json
   {"destination":"U8e742f61d673b39c7fff3cecb7536ef0","events":[]}
   ```
1. ボットサーバーに届いたWebhookの署名（`x-line-signature`）
   ```
   GhRKmvmHys4Pi8DxkF4+EayaH0OqtJtaZxgTD9fMDLs=
   ```
1. 当該チャネルのチャネルシークレット
   ```
   8c570fa6dd201bb328f1c1eac23a96d8
   ```
1. ボットサーバーで署名を検証するコマンド
   ```sh
   echo -n '{"destination":"U8e742f61d673b39c7fff3cecb7536ef0","events":[]}' | openssl dgst -sha256 -hmac '8c570fa6dd201bb328f1c1eac23a96d8' -binary | openssl base64
   ```
1. ボットサーバーで生成された署名
   ```
   GhRKmvmHys4Pi8DxkF4+EayaH0OqtJtaZxgTD9fMDLs=
   ```

LINEプラットフォームから届いた2の署名と、ボットサーバーで生成した5の署名が一致しているため、ボットサーバーに届いたWebhookはLINEプラットフォームから送信されたものであり、改ざんされていないことが確認できました。

なお実際の開発では、[LINE Messaging API SDK](https://developers.line.biz/ja/docs/messaging-api/line-bot-sdk/)を用いることで、署名の検証を簡単に行うことができます。各言語での実装例については、『Messaging APIリファレンス』の「[署名を検証する](https://developers.line.biz/ja/reference/messaging-api/#signature-validation)」を参照してください。

## 署名検証のよくある失敗とその解決方法 

LINEプラットフォームから送信されたWebhookであるにも関わらず署名が不一致となる場合は、ボットサーバーで署名を検証する方法に誤りがあると考えられます。

以下は、署名検証のよくある失敗とその解決方法です。

- [ボットサーバーの手前でWebhookを変更してしまった](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-signature/#modified-webhook-request-before-it-reaches-the-bot-server)
- [Webhookをパースしたりデシリアライズしたりしてしまった](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-signature/#parsing-or-deserializing-webhook-request)
- [Webhookのリクエストボディの文字列（JSON）を整形してしまった](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-signature/#formatted-webhook-event)
- [署名の検証にHMAC-SHA256ではないアルゴリズムを使ってしまった](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-signature/#used-incorrect-algorithm-for-signature-validation)
- [異なるチャネルのチャネルシークレットを使ってしまった](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-signature/#used-wrong-channel-secret)
- [他の開発者がチャネルシークレットを再発行してしまった](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-signature/#reissued-channel-secret)
- [エスケープ文字を解釈してしまった](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-signature/#interpreted-escape-characters)
- [Webhookを処理する際の文字エンコーディングがUTF-8以外になっていた](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-signature/#non-utf8-encoding-for-webhook-processing)

### ボットサーバーの手前でWebhookを変更してしまった 

署名検証前に、受信したWebhookの`x-line-signature`やリクエストボディの文字列に少しでも変更を加えてしまうと、署名検証は失敗します。

Webhookがボットサーバーに到達する前に、プロキシやロードバランサーなどでリクエストのヘッダーやボディに変更が加えられていないか確認してください。

### Webhookをパースしたりデシリアライズしたりしてしまった 

署名検証前に、受信したWebhookのリクエストボディの文字列をパース、あるいはデシリアライズして、オブジェクトや配列に変換してしまうと署名検証は失敗します。

1. ボットサーバーに届いたWebhookのリクエストボディ
   ```json
   {"destination":"U8e742f61d673b39c7fff3cecb7536ef0","events":[]}
   ```
1. Webhookのリクエストボディをデシリアライズして出力する
   ```python
   decoded_data = json.loads('{"destination":"U8e742f61d673b39c7fff3cecb7536ef0","events":[]}')
   print(decoded_data)
   ```
1. デシリアライズしたことでダブルクォートがシングルクォートに変わったり、空白が入ったりしてしまっている
   ```python
   {'destination': 'U8e742f61d673b39c7fff3cecb7536ef0', 'events': []}
   ```

署名検証には、受信したWebhookのリクエストボディの文字列をそのまま使用してください。

### Webhookのリクエストボディの文字列（JSON）を整形してしまった 

署名検証前に、受信したWebhookのリクエストボディの文字列（JSON）を、開発者にとって見やすくするために整形してしまうと署名検証は失敗します。

1. ボットサーバーに届いたWebhookのリクエストボディ
   ```json
   {"destination":"U8e742f61d673b39c7fff3cecb7536ef0","events":[]}
   ```
1. Webhookのリクエストボディの文字列（JSON）を整形すると、署名検証に失敗する
   ```json
   {
     "destination": "U8e742f61d673b39c7fff3cecb7536ef0",
     "events": []
   }
   ```

署名検証には、受信したWebhookのリクエストボディの文字列をそのまま使用してください。

### 署名の検証にHMAC-SHA256ではないアルゴリズムを使ってしまった 

署名検証時にHMAC-SHA256以外のアルゴリズムを使用すると、署名検証は失敗します。

誤ってHMAC-SHA1など、HMAC-SHA256以外のアルゴリズムを使用して署名を生成していないか確認してください。

### 異なるチャネルのチャネルシークレットを使ってしまった 

受信したWebhookの`destination`で指定されているボットとは異なるチャネルのチャネルシークレットを使うと、署名検証は失敗します。

署名の検証では、Webhookの送信者（LINEプラットフォーム）と受信者（開発者が運営するボットサーバー）の双方が、同じハッシュ鍵を用いて計算を行う必要があります。チャネルシークレットはこのハッシュ鍵にあたり、チャネルごとにすべて異なります。

[LINE Developersコンソール](https://developers.line.biz/console/)の［**チャネル基本設定**］タブで、チャネルシークレットの値を確認してください。

### 他の開発者がチャネルシークレットを再発行してしまった 

[LINE Developersコンソール](https://developers.line.biz/console/)の［**チャネル基本設定**］タブで新しいチャネルシークレットを発行すると、それまで使用していたチャネルシークレットは無効になります。

今まで問題なく動いていた署名の検証が突然失敗するようになった場合、同じチャネルのAdmin権限を持つ他の開発者がチャネルシークレットを再発行した可能性があります。

[LINE Developersコンソール](https://developers.line.biz/console/)の［**チャネル基本設定**］タブで、現在のチャネルシークレットの値を確認してください。チャネルシークレットが再発行されていた場合は、ボットサーバーで署名検証に使用するチャネルシークレットを新しいものに差し替える必要があります。

### エスケープ文字を解釈してしまった 

受信したWebhookのリクエストボディには、バックスラッシュ（`\`）や改行（`\n`）などの特殊なエスケープ文字が含まれていることがあります。エスケープ文字をそのまま扱わず、解釈してしまうと署名検証は失敗します。

たとえば、ローカル環境で`echo`コマンドを使って署名検証の動作確認を行う際は、ダブルクォートではなくシングルクォートで囲うことで、エスケープ文字をそのままの形で扱うことができます。

```sh
echo -n '{"destination":"U8e742f61d673b39c7fff3cecb7536ef0","events":[]}' | openssl dgst -sha256 -hmac '8c570fa6dd201bb328f1c1eac23a96d8' -binary | openssl base64
```

Pythonであれば、raw文字列リテラル（`r"..."`）を使うことで、エスケープ文字をそのままの形で扱うことができます。

```python
body = r'{"destination":"U8e742f61d673b39c7fff3cecb7536ef0","events":[{"type":"message","text":"hello\ntest1\ntest2"}]}'
```

署名検証を行う際は、エスケープ文字を解釈せず、受信したWebhookのリクエストボディの文字列をそのまま使用してください。

### Webhookを処理する際の文字エンコーディングがUTF-8以外になっていた 

LINEプラットフォームからのWebhookは、UTF-8エンコーディング（`Content-Type: application/json; charset=utf-8`）で送信されます。

受信したWebhookのリクエストボディを使って署名の検証を行う際に、データがUTF-8以外のエンコーディングで処理されると、改行コードがLF（`\n`）からCRLF（`\r\n`）に変わったり、絵文字や特殊文字（タブ、制御文字など）が誤って解釈されたりして、署名の検証に失敗します。

署名検証を行う際は、文字エンコーディングがUTF-8であることを確認してください。
