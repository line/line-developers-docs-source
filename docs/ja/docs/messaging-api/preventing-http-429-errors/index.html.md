# Messaging APIのHTTPステータスコード429対策のベストプラクティス

<!-- tip start -->

**このページの対象者について**

このページでは、非常に友だち数が多い（目安として100万人以上）大規模で、かつMessaging APIを利用したメッセージ配信の頻度が高いLINE公式アカウントの運用に役立つ技術的な内容を説明します。

以下のようなLINE公式アカウントを運用している場合は、開発者自身が本ページの内容に対応する必要があるかを判断してください。

- 比較的小規模なLINE公式アカウントを運用している。
- LINE Official Account Managerを利用したメッセージ配信が中心である。
- Messaging APIを利用したメッセージの配信は、[無料メッセージ通数](https://developers.line.biz/ja/docs/messaging-api/pricing/#examples-of-subscription-plans)の範囲内で行っている。

<!-- tip end -->

このページでは、Messaging APIを利用するシステムの開発者や運用担当者向けに、HTTPステータスコード429（Too Many Requests）の発生防止と復旧に必要なリクエスト制御、再試行、メッセージ通数や発生状況の確認について説明します。

原因を特定して基本的な対処を行う方法について詳しくは、「[Messaging APIのHTTPステータスコード429への対処の基本](https://developers.line.biz/ja/docs/messaging-api/handling-http-429-errors/)」を参照してください。

<!-- note start -->

**ログを確認できることを前提としています**

このページでは、HTTPステータスコード429が返された状況を、開発者自身のログなどで確認できることを前提に説明します。記録する情報や注意事項について詳しくは、「[HTTPステータスコード429が返された状況を記録する](https://developers.line.biz/ja/docs/messaging-api/handling-http-429-errors/#record-http-429-errors)」を参照してください。

<!-- note end -->

## 解決したいことに応じた対応 

解決したいことに応じて、次の対応を行ってください。

| 解決したいこと | 参照先 |
| --- | --- |
| APIリクエストの頻度や同時処理数を制御したい。 | [APIリクエストを制御する](https://developers.line.biz/ja/docs/messaging-api/preventing-http-429-errors/#control-api-requests)。 |
| 配信可能な通数を把握し、配信計画や送信数を調整したい。 | [メッセージ通数を確認する](https://developers.line.biz/ja/docs/messaging-api/preventing-http-429-errors/#monitor-message-quota)。 |
| エラー発生時のAPIリクエストの再試行を設計したい。 | [レート制限または同時処理数の制限で失敗したAPIリクエストを再試行する](https://developers.line.biz/ja/docs/messaging-api/preventing-http-429-errors/#retry-rate-limit-errors)。 |

## APIリクエストを制御する 

Messaging APIのレート制限の仕組み、適用範囲、エンドポイントごとの上限について詳しくは、『Messaging APIリファレンス』の「[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)」を参照してください。

<!-- tip start -->

**レート制限を個別に変更できません**

Messaging APIのレート制限を、チャネルごとに変更または緩和できません。規定の範囲内でAPIリクエストを実行するように設計してください。

<!-- tip end -->

次の方法でAPIリクエストを制御します。

- [APIリクエスト元でリミッターを設定する](https://developers.line.biz/ja/docs/messaging-api/preventing-http-429-errors/#configure-a-rate-limiter)
- [同時処理数を制御する](https://developers.line.biz/ja/docs/messaging-api/preventing-http-429-errors/#control-concurrent-operations)

### APIリクエスト元でリミッターを設定する 

開発者は、APIリクエスト元のアプリケーションなどに、Messaging APIのレート制限を参考に、[トークンバケット方式](https://developers.line.biz/ja/reference/messaging-api/#rate-limits-mechanism)をベースにしたリミッターを設定し、エンドポイントごとのレート制限を超えないようにしてください。

<!-- note start -->

**レート制限に対して余裕を持たせてください**

複数のアプリケーションからのAPIリクエストや、LINEプラットフォームへの到達タイミングによっては、リミッターを上限と同じ値に設定してもレート制限を超過する可能性があります。上限に対して余裕を持たせてください。

また、APIリクエスト元のアプリケーションやシステムが複数で構成されている場合、アプリケーションやシステムごとに個別に制御するのではなく、必要に応じて共有カウンターなどを使い、リクエスト元全体で頻度を制御してください。

<!-- note end -->

### 同時処理数を制御する 

一部のエンドポイントには、レート制限とは別にオーディエンスID（`audienceGroupId`）単位での[同時処理数の制限](https://developers.line.biz/ja/reference/messaging-api/#limit-on-the-number-of-concurrent-operations)があります。APIリクエスト元のアプリケーションなどでは、対象となる処理をキューなどで管理し、LINEプラットフォーム側で待機中または実行中のジョブの合計が上限を超えないようにしてください。

[オーディエンスの情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-audience-group)エンドポイントのレスポンスに含まれる`jobs[].jobStatus`で、待機中（`QUEUED`）と実行中（`WORKING`）のジョブ数を確認できます。

この制限を超過した場合は、HTTPステータスコード429と、`There are too many running upload jobs for the audience group id.`のエラーメッセージが返されます。

## レート制限または同時処理数の制限で失敗したAPIリクエストを再試行する 

レート制限または同時処理数の制限によるエラーでは、原因に応じて次のように対処した後、APIリクエストを再試行できます。

- レート制限を超過した場合は、リクエスト頻度を下げるか時間を空ける。
- 同時処理数の制限を超過した場合は、処理の完了を待ち、同時処理数が上限を下回ったことを確認する。

<!-- note start -->

**メッセージ通数に関するエラーは同じ方法で再試行しないでください**

`You have reached your monthly limit.`エラーが返された場合は、すぐに再試行せず、メッセージ通数の上限や一時予約の状況を確認してください。詳しくは、「[メッセージ通数に関するエラー](https://developers.line.biz/ja/docs/messaging-api/handling-http-429-errors/#identify-message-quota-error)」を参照してください。

<!-- note end -->

### 原因に応じて再試行のタイミングを決める 

<!-- note start -->

**Retry-Afterヘッダーは返されません**

Messaging APIでは`Retry-After`ヘッダーは返されません。再試行のタイミングは、APIリクエスト元で決めてください。

<!-- note end -->

レート制限が原因の場合は、再試行するリクエストも[APIリクエスト元で設定したリミッター](https://developers.line.biz/ja/docs/messaging-api/preventing-http-429-errors/#configure-a-rate-limiter)で制御してください。Messaging APIのレート制限は[トークンバケット方式](https://developers.line.biz/ja/reference/messaging-api/#rate-limits-mechanism)をベースにしており、使用可能なトークンは時間の経過に応じて補充されます。

HTTPステータスコード429が返された直後の再試行は避け、対象のエンドポイントへのリクエスト頻度を上限に対して余裕のある値まで下げ、トークンが補充されるまで時間を空けてから再試行してください。再試行の際には、間隔にランダムなジッターを加えます。再試行してもHTTPステータスコード429が続く場合は、指数バックオフなどで間隔を段階的に長くしてください。

同時処理数の制限が原因の場合は、[待機中と実行中のジョブ数](https://developers.line.biz/ja/docs/messaging-api/preventing-http-429-errors/#control-concurrent-operations)を確認し、その合計が上限を下回ってから再試行してください。

### 再試行の最大回数を設定する 

Messaging APIにおいて`429 Too Many Requests`エラーの[原因は複数](https://developers.line.biz/ja/docs/messaging-api/handling-http-429-errors/#identify-the-cause)考えられます。原因がメッセージ通数に関するエラーの場合は、リクエストの再試行だけではエラーが解消しないこともあります。

開発者は、最大3回を目安にAPIリクエストの再試行回数を設定してください。再試行してもエラーが解消しない場合は、処理を停止するようにしてください。

その後、開発者または運用担当者がリクエスト頻度と同時処理数を調査し、HTTPステータスコード429のエラー発生の原因を特定および解消した後、再試行してください。

### メッセージ送信エンドポイントではリトライキーを使用する 

開発者は、リトライキーをサポートするメッセージ送信エンドポイントを使用する場合、最初のAPIリクエストから`X-Line-Retry-Key`ヘッダーを指定してください。最初のAPIリクエストから24時間以内の再試行で同じリトライキーを使用すると、同じAPIリクエストが重複して実行されるのを防ぐことができます。

リトライキーを利用できるエンドポイントと実装方法について詳しくは、「[失敗したAPIリクエストを再試行する](https://developers.line.biz/ja/docs/messaging-api/retrying-api-request/)」を参照してください。

---

## HTTPステータスコード429エラーに関する注意事項 

- HTTPステータスコード429が返されたAPIリクエストは処理されず、LINEプラットフォームによる自動再試行も行われません。
- 負荷テストや動作テストを目的とした大量のAPIリクエストや、[同一ユーザーへの大量のメッセージ送信](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/#prohibiting-mass-transmissions-to-same-user)は行わないでください。[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)や[同時処理数の制限](https://developers.line.biz/ja/reference/messaging-api/#limit-on-the-number-of-concurrent-operations)以内でも、通常の利用の範囲ではないと判断された場合はHTTPステータスコード429が返されることがあります。詳しくは、「[Messaging API開発ガイドライン](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/)」を参照してください。
- 月末などは配信可能なメッセージ通数が少なくなり、必要な通数を確保できずにHTTPステータスコード429が返されることがあります。以下のドキュメントを参照してください。
  - [配信に必要な通数を確認する](https://developers.line.biz/ja/docs/messaging-api/handling-http-429-errors/#check-message-quota-for-recipients)
  - [ほかのメッセージ配信の実行状況を確認する](https://developers.line.biz/ja/docs/messaging-api/handling-http-429-errors/#check-ongoing-message-delivery)
