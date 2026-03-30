# モジュール

<!-- note start -->

**オプション機能を利用するには手続きが必要です**

本ドキュメントに記載の機能は、所定の申請等を行った法人ユーザーのみがご利用いただけます。モジュールを利用した拡張機能の公開を希望するお客様は、担当営業までご連絡いただくか、[LINEマーケットプレイス お問い合わせ](https://line-marketplace.com/jp/inquiry)よりお問い合わせください。

<!-- note end -->

## 概要 

モジュールは、LINE公式アカウントに連携（アタッチ）することで、LINE公式アカウントにMessaging APIを利用した機能を追加できる仕組みです。モジュールは、[チャネルの1種（モジュールチャネル）](https://developers.line.biz/ja/docs/line-developers-console/overview/#channel)として提供されます。LINE公式アカウントがMessaging APIチャネルを作成していなくても、モジュールチャネルからMessaging APIを呼び出し、ユーザーにメッセージを送信したり、リッチメニューを設定することができます。

![module channel](https://developers.line.biz/media/partner-docs/module/module-channel.png)

### モジュールチャネルとLINE公式アカウントの関係性 

通常、1つのMessaging APIチャネルは1つのLINE公式アカウントにのみ作成（開設）できます。一方、モジュールチャネルは、複数のLINE公式アカウントと連携できます。

![同じサービスをアタッチする](https://developers.line.biz/media/partner-docs/module-technical/attach-same-service-ja.png)

- OA "X"、OA "Y"、OA "Z"：LINE公式アカウント
- Module CH：モジュールチャネル
- System：Module CHのWebhook送信先およびボットサーバー

<!-- tip start -->

**モジュールチャネルで利用するサーバーについて**

モジュールチャネルにおいて、LINEプラットフォームとやりとりを行うサーバーはモジュールチャネルの開発担当企業が用意する必要があります。モジュールチャネルのWebhook送信先として設定するサーバーは、Messaging APIを呼び出すサーバーと同一である必要はありません。

<!-- tip end -->

### モジュールの利用例 

たとえば、LINE Official Account Managerのチャット機能を利用して、ユーザーとコミュニケーションを行っているLINE公式アカウントがあるとします。このLINE公式アカウントに「来店予約機能を持つモジュールチャネル」を連携した場合、LINE Official Account Manager上でユーザーとチャットを行いつつ、来店予約の手続きをモジュールにより自動化する、といったことが可能になります。

<!-- tip start -->

**モジュールチャネルに対してはWebhookが有効になります**

LINE公式アカウントの応答設定で[Webhookの利用を無効](https://developers.line.biz/ja/reference/messaging-api/#get-webhook-endpoint-information)にしていた場合、Messaging APIチャネルに対するWebhookイベントの送信は行われません。このような設定下においても、モジュールチャネルに対してはWebhookイベントが送信されます。

受信したWebhookイベントの内容に応じて、モジュールチャネルからユーザーに対してメッセージを送信するといった実装が可能です。

<!-- tip end -->

![サンプル](https://developers.line.biz/media/partner-docs/module/module-sample.png)

| 番号 | 説明 |
| --- | --- |
| 1 | ユーザーがメッセージを送信する |
| 2 | LINE Official Account Managerのチャット機能を利用し、オペレーターがユーザーに対してメッセージを送信する |
| 3 | 来店予約機能を持ったモジュールを実行するためのリッチメニューをユーザーが押す |
| 4 | 来店予約機能のボットが応答し、予約手続きが始まる |

## リファレンス 

モジュールで提供されるREST API等の技術的な仕様については、『法人ユーザー向けオプションAPIリファレンス』の「[モジュール](https://developers.line.biz/ja/reference/partner-docs/#module)」を参照してください。

## 必要なシステムや仕組みの用意 

<!-- note start -->

**注意**

現在、モジュールは[LINEマーケットプレイス](https://line-marketplace.com/)に有償の拡張機能として公開する場合のみご利用いただけます。

<!-- note end -->

モジュールにおいて、LINEヤフー株式会社から提供する機能は以下のとおりです。

| 機能名 | 説明 |
| --- | --- |
| LINE公式アカウントにモジュールチャネルを連携する仕組み | OAuth2.0の認可の仕組み、およびREST APIを利用してLINE公式アカウントにモジュールチャネルを連携する仕組みを提供します。詳しくは、「[OAuth 2.0の認可の仕組みを利用してモジュールチャネルをアタッチする](https://developers.line.biz/ja/docs/partner-docs/module-technical-attach-channel/#attach-module-channels-using-oauth-2-0-auth-mechanism)」を参照してください。 |
| LINE公式アカウントとモジュールチャネルとの連携を解除するAPI | LINE公式アカウントとモジュールチャネルの連携を解除するREST APIを提供します。詳しくは、『法人ユーザー向けオプションAPIリファレンス』の「[モジュールチャネルの管理者の操作でモジュールチャネルを連携解除（デタッチ）する](https://developers.line.biz/ja/reference/partner-docs/#unlink-detach-module-channel-by-operation-mc-admin)」を参照してください。 |
| チャットの主導権を制御するAPI | モジュールチャネルには、チャットの主導権（Chat Control）と呼ばれる概念が存在します。ユーザー、グループ、またはトークルームに対する[応答メッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)の送信は、主導権を持つチャネルから行います。<br>通常、LINEマーケットプレイスで提供されるモジュールチャネルでは、主導権を制御する必要はありませんが、想定外の事象によりチャットの主導権が変更された場合の対応のために、チャットの主導権を制御するREST APIを提供します。<br>詳しくは、「[チャットの主導権を制御する（Chat Control）](https://developers.line.biz/ja/docs/partner-docs/module-technical-chat-control/)」を参照してください。 |
| モジュールチャネルからMessaging APIを利用する仕組み | モジュールチャネルからMessaging APIを呼び出す場合、モジュール専用の特別なリクエストヘッダーを指定する必要があります。詳しくは、「[モジュールチャネルからMessaging APIを利用する](https://developers.line.biz/ja/docs/partner-docs/module-technical-using-messaging-api/)」を参照してください。 |
| モジュールチャネル専用のWebhookイベント | モジュールチャネルでは、専用のWebhookイベントを提供しています。詳しくは、「[モジュールチャネル専用のWebhookイベントを受信する](https://developers.line.biz/ja/docs/partner-docs/module-technical-using-messaging-api/#get-module-channel-specific-webhook-events)」を参照してください。 |
| モジュールチャネルに連携されているLINE公式アカウントの情報を取得するAPI | モジュールチャネルに連携されているLINE公式アカウントの情報を取得するREST APIを提供します。詳しくは、「[モジュールチャネルからLINE公式アカウントの情報を取得する](https://developers.line.biz/ja/docs/partner-docs/module-technical-using-messaging-api/#get-line-oa-info-from-module-channel)」を参照してください。 |

上記以外の、LINEマーケットプレイスで拡張機能を公開する際に必要なシステム（サーバー等）や仕組みはすべてお客様で用意（開発）いただく必要があります。例えば以下のとおりです。

- [モジュールで提供される機能を利用するための仕組み](https://developers.line.biz/ja/docs/partner-docs/module/#develop-your-system)
- [モジュールチャネルからMessaging APIを利用する仕組み ](https://developers.line.biz/ja/docs/partner-docs/module/#develop-messaging-api-and-backend)
- [ユーザーが拡張機能を利用するために必要な管理画面や操作コンソールの仕組み](https://developers.line.biz/ja/docs/partner-docs/module/#develop-cms)
- [モジュールの利用料金の決済と管理のための仕組み](https://developers.line.biz/ja/docs/partner-docs/module/#manage-payment-system)
- [利用ユーザーへのサポートの仕組み](https://developers.line.biz/ja/docs/partner-docs/module/#user-support)

### モジュールで提供される機能を利用するための仕組み 

モジュールチャネルは、[OAuth 2.0の認可コード付与のフロー](https://datatracker.ietf.org/doc/html/rfc6749)に基づき、LINE公式アカウントに連携して利用します。OAuth 2.0の認可コード付与（認可リクエスト）を行うために必要なシステムをはじめとした、[必要なシステムや仕組みの用意](https://developers.line.biz/ja/docs/partner-docs/module/#module-functions)に記載されている機能を利用するための各種仕組みはお客様で用意いただく必要があります。

### モジュールチャネルからMessaging APIを利用する仕組み 

LINE公式アカウントに連携したモジュールチャネルからMessaging APIを利用するには、モジュールチャネル専用の特別なリクエストヘッダーを指定した状態で、Messaging APIをリクエストする必要があります。Messaging APIをリクエストする仕組みや、モジュールで提供する拡張機能（チャットボット等）の仕組みについては、お客様で用意いただく必要があります。

<!-- tip start -->

**メッセージの配信には別途費用が必要な場合があります**

モジュールチャネルからMessaging APIを呼び出し、ユーザーにメッセージを送信する場合、モジュールチャネルと連携したLINE公式アカウントの運営者は、[Messaging APIの料金](https://developers.line.biz/ja/docs/messaging-api/pricing/)のお支払いが必要になる場合があります。これはMessaging APIチャネルからMessaging APIを用いてメッセージを送信した場合と同様になります。

<!-- tip end -->

### ユーザーが拡張機能を利用するために必要な管理画面や操作コンソールの仕組み 

ユーザーがモジュールに実装した拡張機能を利用するために必要な、管理画面や操作コンソール等の仕組みについては、お客様で用意いただく必要があります。

### モジュールの利用料金の決済と管理のための仕組み 

モジュールは[LINEマーケットプレイス](https://line-marketplace.com/)において、有償の拡張機能として公開されます。拡張機能を利用するユーザーの管理や利用料金の決済の仕組みについては、お客様で用意いただく必要があります。

### 利用ユーザーへのサポートの仕組み 

モジュールの拡張機能を利用するユーザーに対するサポートの仕組みについては、お客様で準備いただく必要があります。 LINEヤフー株式会社では、[LINEマーケットプレイスで公開されている拡張機能を利用するユーザーへのサポートは行っていません。](https://line-marketplace.com/jp/inquiry)

## 注意事項 

LINEマーケットプレイスでは、モジュールチャネルの機能を利用する場合に、以下の事項を遵守いただく必要があります。

- [Messaging APIチャネルからのMessaging APIの呼び出し（併用）](https://developers.line.biz/ja/docs/partner-docs/module/#restrict-messaging-api-request)
- [連携できるモジュールチャネルの上限](https://developers.line.biz/ja/docs/partner-docs/module/#attach-limit)
- [モジュールチャネルが利用可能なMessaging APIの種類](https://developers.line.biz/ja/docs/partner-docs/module/#module-scopes)
- [Webhookイベントの受信](https://developers.line.biz/ja/docs/partner-docs/module/#bot-module-channel-receive-webhook)

### Messaging APIチャネルからのMessaging APIの呼び出し（併用） 

モジュールチャネルと連携しているLINE公式アカウントにおいては、Messaging APIチャネルからのMessaging APIの利用は推奨していません。これは、システムの実装によっては、モジュールで提供する拡張機能において想定しない挙動が発生する可能性があるためです。

たとえば、以下のような問題が発生することが考えられます。

- [Messaging API経由でユーザーにリッチメニューを設定](https://developers.line.biz/ja/reference/messaging-api/#link-rich-menu-to-user)しているため、モジュールで提供するリッチメニューが表示されなかった
- Messaging APIチャネルから送信したメッセージに対して、ユーザーがメッセージの送信やアクションの実行をし、[Webhookイベントが送信された](https://developers.line.biz/ja/docs/partner-docs/module/#bot-module-channel-receive-webhook)。このWebhookイベントはモジュールのシステムにおいては想定していない内容であったため、正しく処理できなかった

### 連携できるモジュールチャネルの上限 

LINEマーケットプレイスでは、1つのLINE公式アカウントに同時に連携できるモジュールチャネル（拡張機能）は1つのみです。

### モジュールチャネルが利用可能なMessaging APIの種類 

モジュールチャネルが利用可能なMessaging APIの種類は、モジュールチャネルの連携時に許可した権限（スコープ）に応じます。詳しくは、「モジュールチャネルを連携（アタッチ）する」の「[スコープ](https://developers.line.biz/ja/docs/partner-docs/module-technical-attach-channel/#scopes)」を参照してください。

### Webhookイベントの受信 

モジュールチャネルでは、Webhookイベントを受信するためのエンドポイントURLを1つ設定できます。

LINE公式アカウントにモジュールチャネルを連携すると、LINE公式アカウントのトークルームに送信された内容に対応するWebhookイベントが、モジュールチャネルで設定するエンドポイントにも送信されます。モジュールチャネルにおけるWebhookイベントについて詳しくは、「[Webhookを受信する](https://developers.line.biz/ja/docs/partner-docs/module-technical-using-messaging-api/#get-webhook)」を参照してください。

<!-- tip start -->

**モジュールチャネル専用のWebhookイベント**

モジュールチャネルに対してのみ送信されるWebhookイベントが存在します。詳しくは、「[モジュールチャネル専用のWebhookイベントを受信する](https://developers.line.biz/ja/docs/partner-docs/module-technical-using-messaging-api/#get-module-channel-specific-webhook-events)」を参照してください。

<!-- tip end -->

<!-- note start -->

**Messaging APIチャネルにおけるWebhookイベントについて**

モジュールチャネルを連携しているLINE公式アカウントが[Messaging APIチャネルを利用](https://developers.line.biz/ja/docs/messaging-api/getting-started/)しており、かつ[Webhookの利用が有効](https://developers.line.biz/ja/docs/messaging-api/building-bot/#set-up-bot-on-line-developers-console)である場合、モジュールチャネルとMessaging APIチャネルに設定したエンドポイントURLの両方にWebhookイベントが送信されます。このとき、Messaging APIチャネルのエンドポイントURLに送信されるWebhookイベントは、[`mode`プロパティが`standby`](https://developers.line.biz/ja/reference/messaging-api/#common-properties)になり、またWebhookに[応答メッセージを送る](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)ための応答トークンは含まれません。

<!-- note end -->
