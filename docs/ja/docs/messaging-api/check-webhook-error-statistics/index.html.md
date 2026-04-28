# Webhookのエラーの原因と統計情報を確認する

Messaging APIでは、Webhookの送信におけるエラーの原因と統計情報を確認できる機能を提供しています。ボットサーバー側の不具合などによりWebhookを受け取ることができなかった場合において、Webhookの送信状況を把握するときなどに役立ちます。

![ボットサーバーからエラーが返ってくるとエラーの統計情報で表示されます](https://developers.line.biz/media/messaging-api/receiving-messages/webhook-error-ja.jpg)

## エラーの統計情報を有効にする 

エラーの統計情報の表示は、初期設定では無効になっています。エラーの統計情報を表示するには、[LINE Developersコンソール](https://developers.line.biz/console/)より次の手順を行います。

1. エラーの統計情報を表示したいチャネルの設定画面を開く
1. ［**Messaging API設定**］タブをクリックする
1. ［**Webhookの利用**］をオンにする
1. ［**エラーの統計情報**］をオンにする

［**エラーの統計情報**］をオンにした後、統計情報を確認するには、［**Webhookエラー**］タブをクリックしてください。なおエラーは、［**エラーの統計情報**］をオンにしている期間だけ集計されるため、オフだった期間の分はさかのぼって表示されません。表示されるエラーの、日付や時刻の基準となるタイムゾーンはUTC+9です。また［**TSVファイルをダウンロード**］をクリックして、過去に発生したエラーの情報をTSV形式でダウンロードできます。

![エラーの統計情報](https://developers.line.biz/media/messaging-api/receiving-messages/error-statistics-ja.png)

<!-- tip start -->

**Webhook URLを検証した際のリクエストはエラーの統計情報に含まれません**

エラーの統計情報には実際に送信を試みたWebhookのみが表示されます。[Webhook URLを検証](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-url/)した際の疎通確認用のリクエストは成功、失敗にかかわらずエラーの統計情報には含まれません。

<!-- tip end -->

## エラーが発生した原因を確認する 

エラーの統計情報では、エラーが発生した原因とその詳細を確認できます。原因には、次の4種類があります。

| 原因 | 説明 |
| --- | --- |
| `could_not_connect` | LINEプラットフォームからボットサーバーに対してWebhookを送信しようとしましたが、ボットサーバーに正常に接続できませんでした。詳しくは、「[原因が「could_not_connect」の場合](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#reason-could-not-connect)」を参照してください。 |
| `request_timeout` | LINEプラットフォームからボットサーバーに対してWebhookを送信しましたが、ボットサーバーから2秒以内にレスポンスが返されませんでした。詳しくは、「[原因が「request_timeout」の場合](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#reason-request-timeout)」を参照してください。 |
| `error_status_code` | LINEプラットフォームからボットサーバーに対してWebhookを送信しましたが、ボットサーバーからHTTPステータスコード200番台以外のレスポンスが返されました。詳しくは、「[原因が「error_status_code」の場合](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#reason-status-code)」を参照してください。 |
| `unclassified` | 上記に分類できない、不明なエラーが発生しました。詳しくは、「[原因が「unclassified」の場合](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#reason-unclassified)」を参照してください。 |

## エラーの詳細を確認する 

エラーが発生した原因ごとの詳細は、次のとおりです。

- [原因が「could_not_connect」の場合](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#reason-could-not-connect)
- [原因が「request_timeout」の場合](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#reason-request-timeout)
- [原因が「error_status_code」の場合](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#reason-status-code)
- [原因が「unclassified」の場合](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#reason-unclassified)

### 原因が「`could_not_connect`」の場合 

LINEプラットフォームからボットサーバーに対してWebhookを送信しようとしたが、ボットサーバーに正常に接続できなかった場合、原因は`could_not_connect`になります。この場合における詳細は次のとおりです。

| 詳細 | 説明 |
| --- | --- |
| `Connection failed` | ボットサーバーへの接続に失敗しました。 |
| `Connection failed (received GOAWAY)` | ボットサーバーへの接続時に、接続が拒否されました。 |
| `Connection failed (session closed)` | ボットサーバーへの接続が予期せず終了されました。 |
| `Connection timeout` | ボットサーバーへの接続が一定時間内に完了しませんでした。 |
| `DNS Query timeout` | Webhook URLの名前解決を行いましたが、一定時間内に名前解決を完了できませんでした。 |
| `Invalid URL syntax` | 不正なWebhook URLが指定されています（RFC違反等）。 |
| `Session protocol negotiation failure` | ボットサーバーへ接続しましたが、プロトコルネゴシエーションが失敗しました。 |
| `No SSL/TLS record` | ボットサーバーの応答がSSL/TLSで暗号化されていません。 |
| `TLS handshake failure` | ボットサーバーへ接続しましたが、TLSハンドシェイクが失敗しました。ボットサーバーが「[Webhook送信元のSSL/TLS仕様](https://developers.line.biz/ja/docs/messaging-api/ssl-tls-spec-of-the-webhook-source/)」に対応しているか確認してください。 |
| `Unknown host` | Webhook URLに指定されたホストが見つかりませんでした。 |

### 原因が「`request_timeout`」の場合 

LINEプラットフォームからボットサーバーに対してWebhookを送信したが、LINEプラットフォームがレスポンスを受け取れなかった、または送信が途中で失敗した場合、原因は`request_timeout`になります。この場合における詳細は次のとおりです。なお、ボットサーバー側ではWebhookが正常に受信できている可能性があります。

| 詳細 | 説明 |
| --- | --- |
| `Request timeout` | ボットサーバーに対してWebhookを送信しましたが、一定期間内にレスポンスが返されませんでした。 |

### 原因が「`error_status_code`」の場合 

原因が`error_status_code`の場合、詳細にはHTTPステータスコードが入ります。

### 原因が「`unclassified`」の場合 

分類できないエラーが発生した場合、原因は`unclassified`になります。この場合における詳細は次のとおりです。

| 詳細 | 説明 |
| --- | --- |
| `Session closed unexpectedly` | ボットサーバーに対してWebhookを送信しましたが、接続が予期せず途中で切断されました。 |
| `Stream closed unexpectedly` | ボットサーバーに対してWebhookを送信しましたが、ストリームが予期せず途中で切断されました。 |
| `Unclassified webhook dispatch error` | 分類できない想定外のエラーが発生しました。 |

## エラーに備えてWebhookの再送を有効にしておく 

あらかじめWebhookの再送を有効にしておくことで、エラーの発生時にWebhookが再送されます。詳しくは、「[受け取りに失敗したWebhookを再送する](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#webhook-redelivery)」を参照してください。
