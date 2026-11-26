# Messaging APIのHTTPステータスコード429への対処の基本

このページでは、HTTPステータスコード429が返された場合に、レスポンスボディのエラーメッセージから原因を特定し、基本的な対処を行う方法を説明します。

## Messaging APIにおける`429 Too Many Requests`について 

Messaging APIでは、レート制限やメッセージ通数の上限を超過した場合など、以下のようなケースでHTTPステータスコード`429 Too Many Requests`が返されます。

- APIコールのレート制限を超過した場合
- 同時処理数の制限を超過した場合
- 無料メッセージ通数を超過した場合
- 追加メッセージ数の上限目安を超過した場合

このように、`429 Too Many Requests`は複数の原因によって返されるため、再試行に必要な対処もそれぞれ異なります。このため、`429 Too Many Requests`が返された場合は、まずは[原因を特定する](https://developers.line.biz/ja/docs/messaging-api/handling-http-429-errors/#identify-the-cause)必要があります。

<!-- note start -->

**Messaging APIでHTTPステータスコード429が返されたリクエストは処理されません**

- メッセージを送信するエンドポイントの場合、そのリクエストのどの宛先のユーザーにもメッセージは送信されません。
- ユーザー情報を取得したり、何らかの処理を行うエンドポイントの場合、情報は取得されず、予定していた処理も行われません。
- LINEプラットフォームが、HTTPステータスコード429を返したAPIリクエストを、自動的に再試行することはありません。

<!-- note end -->

<!-- tip start -->

**429 Too Many Requestsを防ぐためには**

`429 Too Many Requests`が返されるのを防ぐための具体的な実装や運用について詳しくは、「[Messaging APIのHTTPステータスコード429対策のベストプラクティス](https://developers.line.biz/ja/docs/messaging-api/preventing-http-429-errors/)」を参照してください。

<!-- tip end -->

## HTTPステータスコード429が返された状況を記録する 

HTTPステータスコード429が返された場合に原因を切り分けることができるように、APIリクエストの実行時に次の情報をログに記録してください。

<!-- note start -->

**問題の切り分けは開発者自身で行ってください**

LINEヤフー株式会社では、Messaging APIに対するAPIリクエストのログを提供していません。HTTPステータスコード429が返された原因の特定や再発防止のために、開発者自身で必要なログを保存し、問題を切り分けてください。詳しくは、「[ログ保存の推奨](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/#save-logs)」も参照してください。

<!-- note end -->

<!-- warning start -->

**ログへのアクセス権限は必要最小限にしてください**

開発者は、ログにリクエストボディやレスポンスボディなどの保護すべき情報を記録する場合、ログへのアクセス権限を必要最小限に設定してください。

<!-- warning end -->

**記録する情報**

- APIリクエストを実行した日時
- チャネルIDなどリクエスト送信元チャネルの情報
- リクエストしたHTTPメソッドとエンドポイント
- 受け取った[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)
- 受け取ったレスポンスボディの`message`の内容
- [レスポンスヘッダー](https://developers.line.biz/ja/reference/messaging-api/#response-headers)の`x-line-request-id`

**必要に応じて記録する情報**

- リクエスト頻度と同時処理数
- （実施した場合のみ）再試行回数と再試行間隔
- HTTPステータスコード429が返されたときの[メッセージ通数の上限目安](https://developers.line.biz/ja/reference/messaging-api/#get-quota)と[利用状況](https://developers.line.biz/ja/reference/messaging-api/#get-consumption)

## 原因を特定する 

Messaging APIでは、レート制限の超過以外でも`429 Too Many Requests`が返されるため、HTTPステータスコードのみで、原因を特定することは困難です。

エラーの原因を特定するためには、まずエラー発生時のレスポンスボディに含まれる`message`プロパティ（エラーメッセージ）を確認します。エラーメッセージの内容を元に原因を特定します。

なお、同じエラーメッセージでも複数の原因が考えられるケースがあるため、APIリクエストの実行状況やメッセージ送信の利用状況も確認する必要があります。

`429 Too Many Requests`が発生した時の`message`プロパティには、主に以下のエラーメッセージが含まれます。

| エラーメッセージ | 説明 |
| --- | --- |
| `The API rate limit has been exceeded. Try again later.` | 短時間に多数のAPIリクエストを送信した場合などに返されることがあります。詳しくは、「[レート制限に関するエラー](https://developers.line.biz/ja/docs/messaging-api/handling-http-429-errors/#identify-rate-limit-error)」を参照してください。 |
| `You have reached your monthly limit.` | 当月に多くのメッセージを送信している場合や、複数の配信を並行して行っている場合などに返されることがあります。詳しくは、「[メッセージ通数に関するエラー](https://developers.line.biz/ja/docs/messaging-api/handling-http-429-errors/#identify-message-quota-error)」を参照してください。 |
| `There are too many running upload jobs for the audience group id.` | 同じオーディエンスに対して、アップロード処理を短時間に繰り返した場合などに返されることがあります。詳しくは、「[同時処理数の制限に関するエラー](https://developers.line.biz/ja/docs/messaging-api/handling-http-429-errors/#identify-concurrent-operations-error)」を参照してください。 |

### レート制限に関するエラー 

```
The API rate limit has been exceeded. Try again later.
```

このエラーメッセージは、エンドポイントのレート制限を超過した場合に発生します。以下の内容を確認し、必要な対処を行ってください。

| 項目 | 内容 |
| --- | --- |
| 確認すること | エラーが発生したエンドポイントへのリクエスト頻度を確認し、[レート制限の仕組みと上限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)と照らし合わせてください。 |
| 対処方法と再試行 | しばらく時間をおき、レート制限を超過しないようにリクエスト頻度を下げてから、APIリクエストを再試行してください。 |

### メッセージ通数に関するエラー 

```
You have reached your monthly limit.
```

このエラーメッセージは、[任意のタイミングでメッセージを送信する](https://developers.line.biz/ja/docs/messaging-api/sending-messages/#send-messages-at-any-time)際に、送信に必要なメッセージ通数を確保できない場合に返されます。

当月の上限や利用済みの通数によって、配信に必要な通数が不足する場合があります。また、別の配信による一時予約で、通数が不足する場合もあります。

#### 原因を切り分ける 

次の情報を確認し、通数が不足している原因を切り分けてください。

- [ほかのメッセージ配信の実行状況を確認する](https://developers.line.biz/ja/docs/messaging-api/handling-http-429-errors/#check-ongoing-message-delivery)
- [当月の上限と利用状況を確認する](https://developers.line.biz/ja/docs/messaging-api/handling-http-429-errors/#check-message-quota-and-consumption)
- [配信に必要な通数を確認する](https://developers.line.biz/ja/docs/messaging-api/handling-http-429-errors/#check-message-quota-for-recipients)
- [料金プランと追加メッセージ数の上限目安を確認する](https://developers.line.biz/ja/docs/messaging-api/handling-http-429-errors/#check-message-plan-and-additional-quota)

##### ほかのメッセージ配信の実行状況を確認する 

エラーが発生した時点で、ナローキャストメッセージや[LINE Official Account Manager](https://manager.line.biz/)による別の配信が実行中だったか確認してください。

これらの配信では、実際の送信件数が確定するまで、配信予定分のメッセージ通数が一時的に予約されます。配信の完了後に、配信されなかった分の通数は予約から解除されます。

ただし、ほかの配信が実行中であることだけでは、一時予約がエラーの原因だと断定できません。当月の上限と利用状況、今回の配信に必要な通数も併せて確認してください。

##### 当月の上限と利用状況を確認する 

次のエンドポイントを使って、当月に送信できるメッセージ通数の上限目安と、利用状況を確認してください。

- [当月に送信できるメッセージ数の上限目安を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-quota)
- [当月のメッセージ利用状況を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-consumption)

上限目安を取得するエンドポイントのレスポンスの`type`が`limited`の場合は、`value`から、利用状況を取得するエンドポイントの`totalUsage`を差し引くことで、配信可能な通数の目安を算出できます。`type`が`none`の場合は`value`が返されないため、この方法では残数を算出できません。

`totalUsage`には、配信予定のメッセージの一時的な予約分が含まれる場合があります。このため、実際に送信したメッセージ数より大きくなり、配信可能な通数が一時的に少なくなることがあります。

##### 配信に必要な通数を確認する 

プッシュメッセージ、マルチキャストメッセージ、ブロードキャストメッセージを利用してメッセージを送信する際には、**送信対象のユーザーすべて**に配信できるだけのメッセージ通数が残っている必要があります。配信可能な通数が送信対象のユーザー数を下回ると、APIリクエストはエラーになり、メッセージは送信されません。

たとえば、次のような場合にAPIリクエストがエラーになります。

- [マルチキャストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-multicast-message)で指定したユーザー数よりも、配信可能なメッセージ通数が少ない場合
- [プッシュメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-push-message)の送信先にグループを指定し、そのグループ内の送信対象となるユーザー数よりも、配信可能なメッセージ通数が少ない場合
- [ブロードキャストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-broadcast-message)を送信する際に、送信対象であるLINE公式アカウントと友だちになっているすべてのユーザー数よりも、配信可能なメッセージ通数が少ない場合

<!-- note start -->

**ナローキャストメッセージにおける送信について**

[ナローキャストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message)では、実際の送信対象となるユーザー数にかかわらず、LINE公式アカウントの[ターゲットリーチ](https://developers.line.biz/ja/glossary/#target-reach)分の通数が予約される場合があります。必要な通数は、リミットオブジェクトの設定によって異なります。

リミットオブジェクトに次のいずれかを指定すると、送信対象全員分の通数が残っていなくても、指定した上限または配信可能なメッセージ通数の範囲内で送信できます。送信先のユーザーはランダムに抽出されます。

- `limit.max`プロパティの最大送信数を配信可能なメッセージ通数以下に指定する。
- `limit.upToRemainingQuota`を`true`にする。

なお、`limit.upToRemainingQuota`と併せて`limit.forbidPartialDelivery`に`true`を指定すると、`limit.max`や配信可能なメッセージ通数による制限で送信対象の一部にしか配信できない場合は、配信自体が中止されます。無作為に抽出された一部のユーザーにも配信されません。詳しくは、「[リミットオブジェクトによる最大送信数の制御](https://developers.line.biz/ja/docs/messaging-api/sending-messages/#maximum-send-numbers-control)」を参照してください。

<!-- note end -->

##### 料金プランと追加メッセージ数の上限目安を確認する 

[LINE Official Account Manager](https://manager.line.biz/)で、利用中の料金プランの無料メッセージ通数と、追加メッセージを利用できるかを確認してください。追加メッセージを利用できるプランの場合は、追加メッセージ数の上限目安も確認してください。

料金プランと追加メッセージについて詳しくは、「[料金の仕組み](https://developers.line.biz/ja/docs/messaging-api/pricing/#pricing-system)」を参照してください。

#### 状況に応じて対処する 

確認した状況に応じて、次のように対処してください。

| 確認した状況 | 対処方法と再試行 |
| --- | --- |
| ほかの配信による一時予約の影響が考えられる。 | 先行する配信の完了を待ち、配信可能な通数を再確認してください。今回の配信に必要な通数を確保できていれば、APIリクエストを再試行できます。 |
| 一時的なメッセージ予約の影響がない場合や、先行する配信が完了した後も、今回の配信に必要な通数が不足している。 | 送信対象を減らすか、[料金プラン](https://developers.line.biz/ja/docs/messaging-api/pricing/#pricing-system)や[追加メッセージ数の上限目安](https://www.lycbiz.com/jp/manual/OfficialAccountManager/account-settings_plan/?list=7171)を見直してください。無料メッセージ通数が追加される翌月まで待つ方法もあります。ナローキャストメッセージでは、[リミットオブジェクトによる最大送信数の制御](https://developers.line.biz/ja/docs/messaging-api/sending-messages/#maximum-send-numbers-control)も検討してください。必要な通数を確保するまでは再試行しないでください。 |

### 同時処理数の制限に関するエラー 

```
There are too many running upload jobs for the audience group id.
```

このエラーメッセージは、オーディエンスID（`audienceGroupId`）単位での同時処理数の制限を超過した場合に返されます。以下の内容を確認し、必要な対処を行ってください。

| 項目 | 内容 |
| --- | --- |
| 確認すること | エラーが発生したエンドポイントが[同時処理数の制限](https://developers.line.biz/ja/reference/messaging-api/#limit-on-the-number-of-concurrent-operations)の対象かを確認してください。[オーディエンスの情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-audience-group)エンドポイントで、対象のオーディエンスの`jobs[].jobStatus`が待機中（`QUEUED`）または実行中（`WORKING`）のジョブ数を調べてください。 |
| 対処方法と再試行 | 処理の完了を待ち、待機中と実行中のジョブの合計が上限を下回ってから、APIリクエストを再試行してください。 |

## HTTPステータスコード429の再発を防ぐには 

HTTPステータスコード429が返されるのを防ぐためのリクエスト制御と再試行の設計について詳しくは、「[Messaging APIのHTTPステータスコード429対策のベストプラクティス](https://developers.line.biz/ja/docs/messaging-api/preventing-http-429-errors/)」を参照してください。
