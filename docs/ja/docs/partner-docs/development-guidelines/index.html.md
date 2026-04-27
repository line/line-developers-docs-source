# 法人ユーザー向け開発ガイドライン

法人ユーザー向けの開発ガイドラインです。LINEプラットフォームを利用した開発をする際は、以下の内容に従ってください。

**目次**

<!-- table of contents -->

## LINEボットについて 

### LINE Developersとは 

LINEヤフー株式会社では、外部の企業や開発者に向けて、LINEヤフー株式会社のサービスとの連携が可能になるAPIを提供しています。LINE Developersサイトでは、そうしたLINE APIの仕様や、開発手順を解説したドキュメント、設定を行うためのコンソールを開発者向けに提供しています。詳しくは、「[LINE Developersサイトとは](https://developers.line.biz/ja/about/)」を参照してください。

### LINEボットのしくみ 

LINEボットは、Messaging APIを用いて情報の送受信を行います。詳しくは、『Messaging APIドキュメント』の「[Messaging APIの仕組み](https://developers.line.biz/ja/docs/messaging-api/overview/#how-messaging-api-works)」を参照してください。

### LINEボットとチャネルの関係性について 

LINE公式アカウントの構成要素としてのボットと、チャネルの関係性は以下のようになっています。

![ボットとチャネルの関係](https://developers.line.biz/media/partner-docs/bot-and-channel-relations-ja.png)

### 各種用語について 

各種用語について詳しくは、[用語集](https://developers.line.biz/ja/glossary/)を参照してください。

### LINEボット開発手順 

1. LINE公式アカウント（ボット）およびMessaging APIチャネルを作成する。

   以下のいずれかのサイトから作成できます。
   - LINE Official Account Manager
   - LINE AGP

   Messaging APIチャネルの作成方法について詳しくは、『Messaging APIドキュメント』の「[Messaging APIを始めよう](https://developers.line.biz/ja/docs/messaging-api/getting-started/)」を参照してください。

1. 以下のシステムや仕組みを用意する。
   - [TLS 1.2以上に対応](https://developers.line.biz/ja/docs/partner-docs/development-guidelines/#use-higher-TLS1-2)した、Messaging APIを呼び出すサーバーなどの環境
   - [TLS 1.2以上に対応](https://developers.line.biz/ja/docs/partner-docs/development-guidelines/#https-communication-compatible)した、Webhookイベントを受信するボットサーバーなどの環境

   なお、Messaging APIを呼び出すサーバーなどの環境と、Webhookイベントを受信するボットサーバーなどの環境は、必ずしもそれぞれ独立した環境を用意する必要はありません。

1. ボットサーバーでWebhookイベントを受信するための準備と実装をする。

1. LINE Developersコンソールで［**Messaging API設定**］ > ［**Webhook設定**］の［**Webhook URL**］にボットサーバーのURLを設定し、［**Webhookの利用**］を有効にする。

1. 作成したLINE公式アカウントを友だち追加して、Webhookイベントをボットサーバーが受信できているかを確認する。

### LINEボットリリース前のご確認事項 

LINEボットのリリース前には、以下を必ず確認してください。

1. LINE Developersコンソールへのアクセスが必要なメンバーにチャネルの[権限](https://developers.line.biz/ja/docs/line-developers-console/managing-roles/)やLINE Official Account Managerの[権限](https://www.lycbiz.com/jp/manual/OfficialAccountManager/account-settings_permission/?list=7171)が付与されている。

1. LINE Developersコンソールの［**Messaging API設定**］ > ［**Webhook設定**］の［**Webhook URL**］に正しいURLが設定され、ボットサーバーでWebhookイベントを正常に処理できることを確認している。

1. 後述の[APIリクエスト送信時の注意](https://developers.line.biz/ja/docs/partner-docs/development-guidelines/#send-api-requests)に記載された注意点を考慮した実装がされている。

1. 「[LINEボットセキュリティガイドライン](https://vos.line-scdn.net/line-developers/docs/media/partner-docs/LINE_BOT_Security_Guidelines.pdf)」「[LINEボットセキュリティチェックリスト](https://vos.line-scdn.net/line-developers/docs/media/partner-docs/LINE_BOT_Security_Checklist.xlsx)」のセキュリティ基準を遵守、または同等以上の環境を構築している。

## ボットサーバーにおけるWebhookイベント受信時の注意 

### セキュリティを考慮した通信およびボットサーバー環境 

#### TLS 1.2以上に対応したHTTPS通信 

ボットサーバーでLINEプラットフォームから送信されるWebhookイベントを受信する際の通信は、TLS 1.2以上に対応したHTTPS通信で行う必要があります。HTTPS通信するためのSSL証明書は、公的な認証局で発行されたSSL証明書を用意してください。SSL証明書は有償で購入する他、[Let's Encrypt](https://letsencrypt.org/)などの無償で発行したものも利用できます。Webhookの設定について詳しくは、『Messaging APIドキュメント』の「[Webhook URLを設定する](https://developers.line.biz/ja/docs/messaging-api/building-bot/#setting-webhook-url)」を参照してください。

#### セキュリティガイドラインに準拠した環境構築 

ボットサーバーを構築するにあたり、満たすべきセキュリティ基準を以下のセキュリティガイドラインおよびセキュリティチェックリストにて記載しています。LINEボットを用いたサービスを提供する際には、記載されているセキュリティ基準を遵守、または同等以上の環境をご準備いただいた上で実施してください。

- [LINEボットセキュリティガイドライン](https://vos.line-scdn.net/line-developers/docs/media/partner-docs/LINE_BOT_Security_Guidelines.pdf)
- [LINEボットセキュリティチェックリスト](https://vos.line-scdn.net/line-developers/docs/media/partner-docs/LINE_BOT_Security_Checklist.xlsx)

### 受信したWebhookイベントの検証 

受信したWebhookイベントがLINEプラットフォームから送られたことを確認するために、リクエストヘッダーの[`x-line-signature`](https://developers.line.biz/ja/reference/messaging-api/#webhooks)には署名が含まれています。ボットサーバーでは、受信したリクエストボディから定められたアルゴリズムを使用してダイジェスト値を取得し、`x-line-signature`リクエストヘッダーに含まれている署名と一致するか検証します。署名が一致することを検証することで、受け取ったリクエストがLINEプラットフォームから送信された正しいWebhookイベントであるかどうかを確認できます。

署名の計算鍵にはチャネルシークレットを利用します。そのため、チャネルシークレットのお取り扱いにはご注意ください。詳細とコードサンプルについては、『Messaging APIリファレンス』の「[署名を検証する](https://developers.line.biz/ja/reference/messaging-api/#signature-validation)」を参照してください。

<!-- note start -->

**LINEプラットフォームのIPアドレスは開示していません**

Webhookリクエスト送信元のLINEプラットフォームのIPアドレスについては開示していません。セキュリティの担保はIPアドレスによるアクセス制御ではなく、[署名の検証](https://developers.line.biz/ja/reference/messaging-api/#signature-validation)にて実施いただきますようお願いします。

<!-- note end -->

![署名の検証のイメージ](https://developers.line.biz/media/partner-docs/webbhook-signature-verification-ja.png)

### 大量かつ集中的なWebhookイベント送信への対応 

LINE公式アカウントの特性上、突発的に大量のアクセス（Webhookイベント送信）が発生する場合があります。ボットサーバーの処理能力を超えるWebhookリクエストが送信された場合、ユーザーへのメッセージの遅延や不達が発生する場合があります。

<!-- tip start -->

**アクセスが集中しやすいケースの例**

- LINE公式アカウントの[検索結果での表示](https://www.lycbiz.com/jp/manual/OfficialAccountManager/tutorial-step5/)を「表示」設定にした直後
- [スポンサードスタンプ](https://www.lycbiz.com/jp/service/line-promotion-sticker/)などの施策の実施直後
- [ブロードキャストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-broadcast-message)などですべての友だちへの一斉送信でメッセージを送信した直後（特にキャンペーン等の施策を含む場合）
- ニュースやテレビなどのメディアに取り上げられた直後

なお時間帯としては、昼12時台、または17時〜24時までの間は特にアクセスが集中する可能性があります。

<!-- tip end -->

<!-- note start -->

**注意**

- LINEヤフー株式会社では、ボットサーバーの負荷テストを実施するための環境は提供していません。LINEプラットフォームを含む形での負荷テストは実施しないでください。
- 非常に友だち数が多い（100万人〜）LINE公式アカウントにおいて、ユーザーの反応が大きいと考えられるキャンペーン等の告知メッセージの送信が行われると、LINEプラットフォーム全体のパフォーマンスに影響する可能性があります。このような場合はメッセージの一斉配信は避け、ユーザーからのアクセスが集中しないように段階的に配信を行うなどの対応を行ってください。

<!-- note end -->

### WebhookのON/OFF設定 

LINE Developersコンソールの［**Messaging API設定**］ > ［**Webhook設定**］から［**Webhookの利用**］のオン/オフの設定が可能です。また、LINE Official Account Managerの［**設定**］ > ［**応答設定**］からも［**Webhook**］のオン/オフの設定が可能です。

<!-- note start -->

**Webhook利用開始時の注意**

Webhookの設定を有効にする際には、必ず検証用のアカウント等を用いてテスト環境で動作の検証等を実施した上で、目的のLINE公式アカウントへ設定を適用してください。

<!-- note end -->

<!-- tip start -->

**Webhookの設定の同期**

LINE DevelopersコンソールとLINE Official Account Managerで行ったWebhookの設定はそれぞれ同期しています。

<!-- tip end -->

### WebhookのON/OFFおよび自動応答メッセージの設定について 

［**Webhook**］の利用設定と、LINE Official Account Managerの［**応答メッセージ**］および［**あいさつメッセージ**］の組み合わせは、以下のとおりです。

| ［**Webhook**］ | ［**応答メッセージ**］および［**あいさつメッセージ**］ | 設定の可否 |
| --- | --- | --- |
| 利用する（ON） | 利用する | ✅ |
| 利用する（ON） | 利用しない | ✅ |
| 利用しない（OFF） | 利用する | ✅ |
| 利用しない（OFF） | 利用しない | ❌ |

<!-- note start -->

**許可されていない設定の組み合わせ**

［**Webhook**］を利用せず、LINE Official Account Managerの［**応答メッセージ**］および［**あいさつメッセージ**］を利用しない設定は、ユーザーに対してLINE公式アカウントからメッセージが送信されない設定となるため、ユーザーエクスペリエンスの観点から許可していません。

<!-- note end -->

<!-- note start -->

**［あいさつメッセージ］が送信されるタイミング**

LINE Official Account Managerの［**あいさつメッセージ**］は、LINE公式アカウントが友だち追加されたときに自動で送信されるメッセージです。［**あいさつメッセージ**］は、ブロック解除した際にも送信されます。

<!-- note end -->

### Webhookリクエスト受信時の処理フロー 

ボットサーバーがWebhookイベントを受信してから、2秒以内を目安にHTTPステータスコード`200`をレスポンスしてください。

Webhookリクエストの処理が後続の処理に遅延を与えないよう、Webhookリクエストをボットサーバーが受信した際のイベント処理は非同期化することを推奨しています。イベント処理を非同期化した場合は、イベントの前後関係を維持して処理できるように実装します。

以下は、非同期で処理を行う際のイメージです。

![Webhookリクエスト受信時の処理フロー](https://developers.line.biz/media/partner-docs/flow-when-receiving-a-webhook-ja.png)

### Webhookリクエスト送信時に問題が発生した場合 

認証プロバイダー配下に存在するMessaging APIチャネルにおいては、Webhookイベントを受信してから2秒以内にHTTPステータスコード`200`番台がレスポンスされなかった場合、チャネルの管理者に対し、[`request_timeout`](https://developers.line.biz/ja/docs/messaging-api/check-webhook-error-statistics/#check-error-reason)の[エラー通知](https://developers.line.biz/ja/docs/partner-docs/error-notification/)が送信されます。

<!-- note start -->

**エラー通知機能の利用**

エラー通知機能は、認証プロバイダー配下に存在するMessaging APIチャネルでのみ利用できます。

<!-- note end -->

### その他注意事項 

#### 1つのWebhookに複数のWebhookイベントオブジェクトが含まれる場合があります 

LINEプラットフォームから送信されるWebhookには、複数のWebhookイベントオブジェクトが含まれる場合があります。また1つのWebhookにつき一人のユーザーとは限らず、Aさんからの[メッセージイベント](https://developers.line.biz/ja/reference/messaging-api/#message-event)と、Bさんからの[フォローイベント](https://developers.line.biz/ja/reference/messaging-api/#follow-event)が同じWebhookに入ることもあります。

複数のWebhookイベントオブジェクトを含むWebhookを受信した場合も、ボットサーバーは適切な処理を行えるようにしてください。Webhookイベントオブジェクトについて詳しくは、『Messaging APIリファレンス』の「[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)」を参照してください。

#### Webhookイベントオブジェクトの構造変更への対応 

Messaging APIの機能に追加または変更があったときに、Webhookイベントオブジェクトにプロパティが追加される場合があります。新しいプロパティを含むWebhookイベントオブジェクトを受信しても不具合が発生しないようにボットサーバーを実装してください。Webhookイベントオブジェクトについて詳しくは、『Messaging APIリファレンス』の「[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)」を参照してください。

#### Webhookリクエストに含まれるヘッダーについて 

『Messaging APIリファレンス』の「[リクエストヘッダー](https://developers.line.biz/ja/reference/messaging-api/#request-headers)」を参照してください。

#### 想定しないトーク送信に対する処理について 

ユーザーからLINE公式アカウントに対しトークおよび、対応するWebhookイベントが送信されないように制限を行うことはできません。特定のユーザーから想定しないトーク送信が行われた場合、状況によって処理を変更するなどの対応が行えるようにシステムを実装してください。

## APIリクエスト送信時の注意 

### チャネルアクセストークンの発行 

Messaging APIのリクエストにおいて、チャネルを使用する権限を持っているかどうかを確認するために、[チャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/)を利用します。現在、有効期間や発行方法が異なる[4種類のチャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/#channel-access-token-types)を提供しています。

<!-- note start -->

**長期のチャネルアクセストークンについて**

LINE Developersコンソールから有効期間が非常に長い長期のチャネルアクセストークンの発行が可能ですが、セキュリティの観点から長期のチャネルアクセストークンの発行は推奨しておりません。チャネルアクセストークンを発行する際には、有効期間30日の短期のチャネルアクセストークン、任意の有効期間を指定できるチャネルアクセストークン（チャネルアクセストークンv2.1）、ステートレスチャネルアクセストークンのいずれかを利用いただくことを推奨しています。

<!-- note end -->

### チャネルアクセストークンの再発行 

短期のチャネルアクセストークンおよび任意の有効期間を指定できるチャネルアクセストークン、ステートレスチャネルアクセストークンには有効期間が存在し、それを過ぎると利用できなくなってしまいます。また、一度発行したチャネルアクセストークンの有効期間は延長（更新）できません。そのため、残りの有効期間を考慮し、定期的に新たなチャネルアクセストークンを再発行する仕組みを構築する必要があります。

なお、チャネルアクセストークンは複数個発行することができますが、チャネルアクセストークンの種類によっては、発行できる数には上限があります。Messaging APIを複数のサーバーやシステムから利用する際には、それぞれが利用するチャネルアクセストークンを正しく管理してください。

短期のチャネルアクセストークンまたは任意の有効期間を指定できるチャネルアクセストークンについては、新しいチャネルアクセストークンを発行した後は、古い利用しなくなったチャネルアクセストークンは取り消し（Revoke）することを推奨します。詳しくは、『LINEプラットフォームの基礎知識』の「[チャネルアクセストークンの運用例](https://developers.line.biz/ja/docs/basics/channel-access-token/#how-to-operate-channel-access-token)」も参照してください。

### チャネルアクセストークンの発行上限 

チャネルアクセストークンの種類における発行上限は以下のとおりです。

| 種類 | 発行上限 | 上限を超過した場合の動作 | チャネルアクセストークンが無効化される条件 |
| --- | --- | --- | --- |
| 短期のチャネルアクセストークン | 30 | 発行順に既存の短期のチャネルアクセストークンが無効化 | <ul><li>有効期間の超過</li><li>発行上限の超過</li><li>チャネルアクセストークンの取り消し（revoke API）の実行</li></ul> |
| 長期のチャネルアクセストークン | 1 | 既存の長期のチャネルアクセストークンが無効化 | <ul><li>発行上限の超過</li><li>チャネルアクセストークンの取り消し（revoke API）の実行</li></ul> |
| 任意の有効期間を指定できるチャネルアクセストークン | 30 | APIがエラーとなり追加で発行ができない | <ul><li>有効期間の超過</li><li>チャネルアクセストークンの取り消し（revoke API）の実行</li></ul> |
| ステートレスチャネルアクセストークン | 無制限 | - | <ul><li>有効期間の超過</li></ul> |

### メッセージ送信リクエスト 

メッセージの送信に成功すると、HTTPステータスコード`200`（ナローキャストAPIのみ`202`）とともに、空のJSONオブジェクトが返されます。

メッセージの送信に失敗した際には、[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)として、エラーメッセージなどのJSONデータを含むレスポンスボディが返されます。

<!-- note start -->

**エラーレスポンスについて**

エラーレスポンス中に含まれるエラーメッセージについては保証されておらず、予告なく変更される場合があります。エラー発生時の例外処理は受信したHTTPステータスコードによって行ってください。

<!-- note end -->

<!-- tip start -->

**ログの保存**

Messaging APIに対するリクエストを行った際は、リクエストしたAPIのログや、受信したレスポンスのログは、一定期間保存してください。ログの保存について詳しくは、『Messaging APIドキュメント』の「[ログ保存の推奨](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/#save-logs)」を参照してください。

<!-- tip end -->

### メッセージ送信リクエストのリトライ 

LINEプラットフォームに障害が発生していない時でも、ボットサーバーのネットワーク接続状況やその他の要因により、次のような問題が起こる可能性があります。

- APIリクエストが正常に完了しない
- LINEプラットフォームからのレスポンスが正常に得られない

このような場合、同じAPIリクエストを続けて実行してしまうと、最初のAPIリクエストが正しく受理されていた場合、ユーザーは同じメッセージを二度も受信することになります。これを防ぐため、リトライキー（`X-Line-Retry-Key`）を用いて安全にリクエストをリトライできるよう実装してください。メッセージ送信リクエストについて詳しくは、『Messaging APIドキュメント』の「[失敗したAPIリクエストを再試行する](https://developers.line.biz/ja/docs/messaging-api/retrying-api-request/)」を参照してください。

![失敗したAPIリクエストを再試行するイメージ](https://developers.line.biz/media/partner-docs/retrying-a-failed-api-request-ja.png)

### リクエストの制限 

LINEボットが送信可能なメッセージには、1回のリクエストで送信できるメッセージの長さや、一定時間内に送信できるメッセージ数に制限があります。

#### テキストメッセージの制限 

[テキストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#text-message)や[テキストメッセージ（v2）](https://developers.line.biz/ja/reference/messaging-api/#text-message-v2)で指定可能な文字の上限は5000文字です。

#### リクエストサイズの制限 

リクエストのサイズの上限は2MBとなります。

#### リクエストレートの制限 

Messaging APIでは、エンドポイントごとに[レート制限](https://developers.line.biz/ja/reference/messaging-api/#rate-limits)が適用されます。

本番アカウント、テストアカウントに関わらず、[動作テストを目的に大量のリクエストを送信することは禁止](https://developers.line.biz/ja/docs/messaging-api/development-guidelines/#prohibiting-mass-requests-to-line-platform)されています。メッセージ送信における負荷テストを行う場合は、LINEプラットフォームを含めない形で実施してください。

### メッセージの送信方法 

メッセージの送信方法について詳しくは、以下のドキュメントを参照してください。

- [ユーザーからのメッセージやアクションに応答する（応答メッセージ）](https://developers.line.biz/ja/docs/messaging-api/sending-messages/#reply-messages)
- [任意のタイミングでメッセージを送信する](https://developers.line.biz/ja/docs/messaging-api/sending-messages/#send-messages-at-any-time)

<!-- tip start -->

**応答トークンの有効期間**

[応答メッセージ](https://developers.line.biz/ja/docs/messaging-api/sending-messages/#reply-messages)で利用する応答トークンの有効期間について詳しくは、『Messaging APIリファレンス』の「[応答トークン](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message-reply-token)」を参照してください。

<!-- tip end -->

### HTTPS（TLS 1.2以上）の利用 

Messaging API呼び出し元のシステムと、LINE APIサーバーとの通信は、HTTPS（TLS 1.2以上）で行う必要があります。また、[画像メッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#image-messages)や[画像コンポーネント](https://developers.line.biz/ja/reference/messaging-api/#f-image)を含むFlex Messageなどを送信する場合、ファイルを保存するサーバーはHTTPS（TLS 1.2以上）での通信に対応している必要があります。

### 大量のアクセスへの対応 

メッセージの送信対象のユーザー数や、送信したメッセージの内容によっては、メッセージに含まれるURLや画像などのコンテンツに対し、大量のアクセスが発生する場合があります。

そのような場合に備え、CDNやロードバランサーなどの負荷分散の仕組みを利用したり、メッセージの送信を段階的に行ったりして、コンテンツ保存元のサーバーが大量のアクセスによってダウンしないように対応してください。

![大量のリクエスト](https://developers.line.biz/media/partner-docs/large-volume-of-requests-ja.png)

## LINEログイン利用時の注意 

LINEログインを利用することで、ユーザーが持つLINEアカウントの情報を利用したログイン機能をお客様のウェブサービスやネイティブアプリに実装できます。

例えば、ウェブアプリにLINEログインを組み込み、取得した情報を自社の会員情報などと紐づけることで、Messaging APIを利用してよりパーソナライズしたメッセージをユーザーに送信できます。

LINEログインについて詳しくは、[LINEログインの概要](https://developers.line.biz/ja/docs/line-login/overview/)を参照してください。

### LINEログインの認可と認証のプロセス 

ウェブアプリ向けのLINEログインの処理（ウェブログイン）は、[OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749)の認可コード付与のフローと[OpenID® Connect](https://openid.net/specs/openid-connect-core-1_0.html)プロトコルに基づきます。ウェブアプリ向けのLINEログインについて詳しくは、『LINEログインドキュメント』の「[ログインのフロー](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#login-flow)」を参照してください。

### コールバックURLについて 

コールバックURL（`redirect_uri`）は、ユーザーがLINEログインの認証と認可の操作を行ったあとで、[ウェブアプリが認可コードとstateを受け取る](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#receiving-the-authorization-code-or-error-response-with-a-web-app)URLとして使用されます。コールバックURLはLINE Developersコンソールのチャネル設定の［**LINEログイン設定**］より設定できます。

コールバックURLについて詳しくは、『LINEログインドキュメント』の「[コールバックURLを設定する](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#setting-callback-url)」を参照してください。

<!-- note start -->

**コールバックURL設定時の注意**

- コールバックURLには最大400個のURLを登録できます。
- コールバックURLにはクエリパラメータを含んだURLを登録できます。
- 認可リクエスト時に指定する`redirect_uri`は、コールバックURLに登録したURLをURLエンコードした文字列。任意のクエリパラメータを付与できます。
  - コールバックURLに`https://example.com`を登録し、認可リクエスト時に指定する`redirect_uri`に`https://example.com?key=value`といった指定が可能です。

<!-- note end -->

### ウェブアプリで認可レスポンスまたはエラーレスポンスを受け取る 

ユーザーによる認証と認可のプロセスが終了すると、ユーザーはコールバックURLにリダイレクトされます。

ユーザーがアプリにアクセス権を付与したときは、認可コードを含む認可レスポンスが渡されます。また、アクセス権の付与を拒否したときは、エラーレスポンスが渡されます。詳しくは、『LINEログインドキュメント』の「[ウェブアプリで認可レスポンスまたはエラーレスポンスを受け取る](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#receiving-the-authorization-code-or-error-response-with-a-web-app)」を参照してください。

### アクセストークンを発行する 

LINEログインの認可リクエストにより取得した認可コードを用いてアクセストークンを発行します。アクセストークンの発行について詳しくは、『LINEログインv2.1 APIリファレンス』の「[アクセストークンを発行する](https://developers.line.biz/ja/reference/line-login/#issue-access-token)」を参照してください。

<!-- note start -->

**アクセストークンを発行する際の注意**

- アクセストークンを発行する際に指定する`redirect_uri`パラメータは、認可リクエスト時に指定したものと同じ値にする必要があります。
- 認可コードは、アクセストークン発行の成功の有無に関係なく1度のみ利用可能です。

<!-- note end -->

### IDトークンを検証する 

スコープに`openid`を指定したLINEログインの認可リクエストにより取得したトークンエンドポイントの[ペイロード](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#response)にはIDトークンが含まれます。取得したIDトークンを検証することで、ユーザーのプロフィール情報を取得できます。詳しくは、『LINEログインドキュメント』の「[IDトークンからプロフィール情報を取得する](https://developers.line.biz/ja/docs/line-login/verify-id-token/)」を参照してください。

### その他のLINEログインAPI 

取得したアクセストークンを用いることで、ユーザーとLINE公式アカウントとの友だち関係を確認したり、ユーザーのプロフィール情報を取得したりできます。LINEログインのAPIについて詳しくは、「[LINEログイン v2.1 APIリファレンス](https://developers.line.biz/ja/reference/line-login/)」を参照してください。

### LINEログインで取得した情報と自社で管理する情報との紐づけ（ID連携） 

LINEログインを行い取得したユーザーの情報（ユーザーIDなど）と、自社で管理する会員情報などを紐づけることで、よりパーソナライズされたメッセージの配信などが可能となります。

![ID連携の流れ](https://developers.line.biz/media/partner-docs/flow-for-linking-ids-ja.png)

<!-- note start -->

**会員情報などとの紐づけと管理について**

- LINEログインで取得したユーザー情報と、自社で管理する会員情報などを紐づけの仕組みはLINEヤフー株式会社からは提供していません。
- 会員情報などを紐づけを行う際には、なりすましによる紐づけ等が行われないようにセキュリティを考慮した設計にしてください。
- LINEプラットフォームのユーザー情報と、会員情報などを紐づけを解除する動線を設けてください。
- LINEアプリの［**設定**］ > ［**アカウント**］ > ［**連動アプリ**］より［**連動を解除**］した場合、LINEログインの[チャネルの同意](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#authorization-process)が取り下げられますが、ユーザー情報の紐づけは解除されません。LINEログインで取得した情報と自社で管理する情報の紐づけ処理は、別途お客様で行う必要があります。

![unlink](https://developers.line.biz/media/partner-docs/unlink.png)

<!-- note end -->

### 友だち追加オプション 

LINEログインでは、LINEログインしたときにLINE公式アカウントを友だち追加するオプションを利用できます。これを、友だち追加オプションと呼びます。友だち追加オプションで使用するLINE公式アカウントは、LINE Developersコンソールで設定できます。詳しくは、『LINEログインドキュメント』の「[LINEログインしたときにLINE公式アカウントを友だち追加する（友だち追加オプション）](https://developers.line.biz/ja/docs/line-login/link-a-bot/)」を参照してください。

<!-- note start -->

**友だち追加オプションを利用する際の注意事項**

- リンクするLINE公式アカウントは、LINEログインチャネルと関係するものに限定されます。例えば、企業AのLINE公式アカウントを、企業Aと関係がない企業BのLINEログインチャネルにリンクしないでください。
- 設定の変更は即時に反映されるため、誤って意図しないLINE公式アカウント（テスト用など）を設定することがないよう、操作には十分にご注意ください。
- LINEログインチャネルが認証プロバイダー配下に存在する場合、LINEログインの同意画面に表示される［**友だち追加（ブロック解除）**］はデフォルトで選択（チェック）された状態となります。

<!-- note end -->

### stateの検証 

LINEログインの認可リクエスト要求時に指定する`state`パラメータは[クロスサイトリクエストフォージェリ](https://ja.wikipedia.org/wiki/%E3%82%AF%E3%83%AD%E3%82%B9%E3%82%B5%E3%82%A4%E3%83%88%E3%83%AA%E3%82%AF%E3%82%A8%E3%82%B9%E3%83%88%E3%83%95%E3%82%A9%E3%83%BC%E3%82%B8%E3%82%A7%E3%83%AA)防止のため、指定は必須となります。 認可リクエストのセッションごとにウェブアプリでランダムに生成し、[認可レスポンスまたはエラーレスポンス受信](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#receiving-the-authorization-code-or-error-response-with-a-web-app)時に検証してください。

![stateの検証](https://developers.line.biz/media/partner-docs/state-verification-ja.png)

## LINE Front-end Framework（LIFF） 

LINE Front-end Framework（LIFF）は、LINEヤフー株式会社が提供するウェブアプリのプラットフォームです。このプラットフォームで動作するウェブアプリを、LIFFアプリと呼びます。

LIFFアプリを使うと、LINEのユーザーIDなどをLINEプラットフォームから取得できます。LIFFアプリではこれらを利用して、ユーザー情報を活用した機能を提供したり、ユーザーの代わりにメッセージを送信したりできます。

LIFFアプリについて詳しくは、「[LIFFの概要](https://developers.line.biz/ja/docs/liff/overview/)」を参照してください。

## その他の機能 

### 遷移先ブラウザの設定方法について 

トークルームや、LINEアプリ内ブラウザからURLにアクセスする際、特殊なクエリパラメータを付与したURLを開くことで、URLを開くブラウザを外部ブラウザに変更できます。クエリパラメータ について詳しくは、「[URLを外部ブラウザで開く](https://developers.line.biz/ja/docs/line-login/using-line-url-scheme/#opening-url-in-external-browser)」を参照してください。

### URLスキームについて 

LINE公式アカウントとのトークルームなどで利用可能なURLスキームを提供しています。URLスキームについて詳しくは、「[LINE URLスキームでLINEの機能を使う](https://developers.line.biz/ja/docs/line-login/using-line-url-scheme/)」を参照してください。

### チャネルの権限について 

LINEログインチャネルおよびLINEミニアプリチャネルはチャネルの作成直後ではステータスが「開発中」となっています。「開発中」ステータスのチャネルにおける、LINEログインやLIFFアプリへのアクセスには、チャネルのAdmin権限もしくはテスター権限を付与したLINEアカウントが必要です。

権限について詳しくは、『LINE Developersコンソールドキュメント』の「[チャネルの権限](https://developers.line.biz/ja/docs/line-developers-console/managing-roles/#roles-for-channel)」を参照してください。

### Messaging APIで利用可能なスタンプや絵文字について 

Messaging APIでは、スタンプは[パッケージIDやスタンプIDといった識別子](https://developers.line.biz/ja/docs/messaging-api/sticker-list/#sticker-definitions)を利用してやり取りが行なわれます。

#### Messaging APIでスタンプを送信する 

Messaging APIで送信できるスタンプについて詳しくは、『Messaging APIドキュメント』の「[スタンプ](https://developers.line.biz/ja/docs/messaging-api/sticker-list/)」を参照してください。

#### ユーザーから送信されたスタンプを確認する 

ユーザーからLINE公式アカウントに対してスタンプが送信された場合、[Webhookのメッセージイベント](https://developers.line.biz/ja/reference/messaging-api/#wh-sticker)として、送信されたスタンプのパッケージIDおよびスタンプIDが送信されます。

受信したWebhookイベントに含まれるスタンプIDを利用して、送信されたスタンプの画像を取得する仕組みは公開しておりません。弊社の[Technology Partner](https://www.lycbiz.com/jp/partner/technology/line/)がユーザーと直接やり取りが可能なチャットツール（CRMツールなど）を作成する場合や、LINEヤフー株式会社が適切であると判断した場合に限って提供しております。詳しくは弊社担当者までお問い合わせください。

#### LINE絵文字の送信 

[テキストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#text-message)や[テキストメッセージ（v2）](https://developers.line.biz/ja/reference/messaging-api/#text-message-v2)を送信する際に、LINE絵文字を送信できます。LINE絵文字について詳しくは、『Messaging APIドキュメント』の「[LINE絵文字](https://developers.line.biz/ja/docs/messaging-api/emoji-list/)」を参照してください。

#### LINE絵文字の受信 

ユーザーからLINE公式アカウントにLINE絵文字が送信された場合、メッセージイベントのテキストオブジェクト内の[emojisオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#wh-text)に配列として格納されます。

<!-- note start -->

**送信されたLINE絵文字がemojisオブジェクトに含まれないことがあります**

- Android版LINEから送信されたデフォルトのLINE絵文字は、含まれません。
- Unicodeで定義された絵文字や古いバージョンのLINE絵文字は、含まれないことがあります。

<!-- note end -->
