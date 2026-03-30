# 失敗したAPIリクエストを再試行する

メッセージの送信処理は失敗する可能性があり、その場合は500番台のエラーが発生したり、リクエストがタイムアウトしたりします。ただし、このようなエラーが発生した場合でも、メッセージは送信されている可能性があります。つまり、エラーが起きたからといって同じリクエストを再送信すると、以下の図のように、ユーザーは同じメッセージを2回受信することになります。

![](https://developers.line.biz/media/messaging-api/retry-api-request/retry-api-request-bad.svg)

同じメッセージを重複して送信することを避けるために、リトライキー（`X-Line-Retry-Key`）を使用します。リトライキーを指定すると、リクエストを何度送信しても一度しか実行されません。一度リクエストが受け付けられると、それ以降の再送信は拒否され、ステータスコード`409`が返されます。

同じAPIリクエストが重複して実行されるのを防ぐため、再試行を行う際にはリトライキーを使用することを推奨します。

![](https://developers.line.biz/media/messaging-api/retry-api-request/retry-api-request-good.svg)

<!-- note start -->

**注意**

`X-Line-Retry-Key`により、メッセージの重複を気にせず安全にAPIリクエストを再試行することができますが、メッセージの確実な配信を保証するものではありません。もしAPIリクエストが一度でもLINEプラットフォームに受理（HTTPステータスコード200番台）された場合、その後ユーザがLINE公式アカウントをブロックしたなどの理由で正しく配信ができなかったとしても、同じリクエストを再試行することはできません。

<!-- note end -->

## APIリクエストの再試行の流れ 

リトライキーをサポートするAPIを使用するには、以下の流れでリクエストを行います。

![Retry API Request Flowchart](https://developers.line.biz/media/messaging-api/retry-api-request/retry-key-flowchart.png)

### リトライキーを常に指定する 

リトライキーをサポートするAPIを使ってメッセージを送信する際は、常にリクエストヘッダーにリトライキー`X-Line-Retry-Key`を指定してください。リトライキーは任意の方法で生成した16進数のUUIDです。

<!-- note start -->

**最初のAPIリクエストでリトライキーを指定する**

`X-Line-Retry-Key`を指定しなかったAPIリクエストは再試行できません。最初のリクエスト時にリトライキーを指定してください。

<!-- note end -->

再試行をサポートするAPIは以下のとおりです。

| 送信方法 | APIリファレンス |
| --- | --- |
| プッシュメッセージ | [プッシュメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-push-message) |
| マルチキャストメッセージ | [マルチキャストメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-multicast-message) |
| ナローキャストメッセージ | [ナローキャストメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message) |
| ブロードキャストメッセージ | [ブロードキャストメッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-broadcast-message) |

<!-- note start -->

**サポートされているAPIでのみ再試行できます**

上記以外のAPIのリクエストヘッダーに`X-Line-Retry-Key`を指定した場合、リクエストは拒否され、ステータスコード`400`が返されます。

<!-- note end -->

以下は、リトライキー（`123e4567-e89b-12d3-a456-426614174000`）を指定してプッシュメッセージを送信するリクエストの例です。

```sh
curl -v -X POST https://api.line.me/v2/bot/message/push \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {CHANNEL_ACCESS_TOKEN}' \
-H 'X-Line-Retry-Key: 123e4567-e89b-12d3-a456-426614174000' \
-d '{
  "messages": [
    {
      "type": "text",
      "text": "Hello, user"
    }
  ]
}'
```

### ステータスコードに応じたAPIリクエストの再試行 

APIリクエストを再試行するかどうかは、返されたステータスコードによって判断します。

| ステータスコード | 説明 | 再試行要否 |
| --- | --- | --- |
| 500 Internal Server Error | 内部サーバーのエラーです。 | ✅ 再試行します。次のリクエストは成功する可能性があります。 |
| タイムアウト | ネットワーク障害などでリクエストが失敗しています。 | ✅ 再試行します。次のリクエストは成功する可能性があります。 |
| 200番台 | APIリクエストが受理されました。 | ❌ 再試行しません。これ以降の再試行は受理されません。 |
| 409 Conflict | 同じリトライキーを持つAPIリクエストがすでに受理されています。 | ❌ 再試行しません。すでにリクエストは受理されています。 |
| その他の400番台 | リクエストに問題があります。 | ❌ 再試行しません。再試行しても結果は変わりません。 |

<!-- note start -->

**注意**

- リトライキーは、最初のリクエストから24時間有効です。24時間以内にリクエストを再試行するようにサービスを設計してください。
- 再試行するリクエストは、元のリクエストと同じにします。内容や送信先を変更しないでください。内容や送信先を変更したリクエストに同じリトライキーを使用すると、再試行が期待通りに動作しない場合があります。

<!-- note end -->

<!-- tip start -->

**再試行の間隔について**

- リトライキーによる再試行は1つのAPIリクエストとしてカウントされるため、再試行の頻度が高すぎると、APIのレート制限に達する可能性があります。
- サーバーやネットワークの障害時の負荷を抑えるために、再試行の間隔は[指数バックオフ](https://en.wikipedia.org/wiki/Exponential_backoff)にすることをお勧めします。

<!-- tip end -->

#### 再試行のレスポンス 

再試行されたAPIリクエストに対して受け取るレスポンスは、APIリクエストが受理されたかどうかで異なります。

<!-- tip start -->

**異なるリクエストIDが発行されます**

同じリトライキーで複数のリクエストを実行した場合、それぞれのリクエストには異なるリクエストIDが割り当てられます。

<!-- tip end -->

##### 受理されたリクエストに対するレスポンス 

再試行に成功したリクエストには、正常にリクエストが受理された場合と同じレスポンスが返されます。以下はその例です。

```sh
HTTP/1.1 200 OK
x-line-request-id: 123e4567-e89b-12d3-a456-426655440001
```

##### 受理されたリクエストを再試行した場合のレスポンス 

LINEプラットフォームがHTTPステータスコード200番台を返したAPIリクエストを再試行すると、ステータスコード`409`が返されます。レスポンスには、すでに受理されていたリクエストのリクエストID`x-line-accepted-request-id`が返されます。

```sh
HTTP/1.1 409 Conflict
x-line-request-id: 123e4567-e89b-12d3-a456-426655440002
x-line-accepted-request-id: 123e4567-e89b-12d3-a456-426655440001

{
  "message": "The retry key is already accepted"
}
```

さらにプッシュメッセージの場合は、APIリクエストが受理されたときと同じ`sentMessages.id`や`sentMessages.quoteToken`を含むJSONオブジェクトを返します。

```sh
HTTP/1.1 409 Conflict
x-line-request-id: 123e4567-e89b-12d3-a456-426655440002
x-line-accepted-request-id: 123e4567-e89b-12d3-a456-426655440001

{
  "message": "The retry key is already accepted",
  "sentMessages": [
    {
      "id": "461230966842064897",
      "quoteToken": "IStG5h1Tz7b..."
    }
  ]
}
```

## 関連ページ 

再試行について詳しくは、『Messaging APIリファレンス』の「[APIリクエストを再試行する](https://developers.line.biz/ja/reference/messaging-api/#retry-api-request)」を参照してください。
