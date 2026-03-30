# チャットの主導権を制御する（Chat Control）

<!-- warning start -->

**警告**

現在提供しているモジュールチャネルは、LINE公式アカウントにアタッチすると自動的にチャットの主導権を取得します（[Default Active](https://developers.line.biz/ja/docs/partner-docs/module-technical-chat-control/#default-active)）。そのため、チャットの主導権を制御する必要はありません。

<!-- warning end -->

<!-- note start -->

**オプション機能を利用するには手続きが必要です**

本ドキュメントに記載の機能は、所定の申請等を行った法人ユーザーのみがご利用いただけます。モジュールを利用した拡張機能の公開を希望するお客様は、担当営業までご連絡いただくか、[LINEマーケットプレイス お問い合わせ](https://line-marketplace.com/jp/inquiry)よりお問い合わせください。

<!-- note end -->

## チャットの主導権（Chat Control）とは 

エンドユーザーのアクションに応じて、複数のモジュールチャネルが同時に返信したり処理をしたりするのを防ぐために、モジュールチャネルには主導権（Chat Control）と呼ばれる概念を導入しています。

![Chat control](https://developers.line.biz/media/partner-docs/module-technical/chat-control-ja.png)

| 主導権（Chat Control） | 説明 |
| --- | --- |
| Active Channel | 主導権（Chat Control）を持つチャネルです。デフォルトでは、Primary CH（LINE公式アカウントに紐づいた標準のMessaging APIチャネル）が「Active Channel」です。<br>このチャネルから、返信メッセージやプッシュメッセージなどを送信できます。<br>1つのLINE公式アカウントに対して、「Active Channel」は1つのみ存在できます。 |
| Standby Channel | 主導権（Chat Control）を持たないチャネルです。<br>このチャネルからは、メッセージの送信を控えてください。<br>Active Channel以外のチャネルは、すべて「Standby Channel」です。 |

<!-- note start -->

**主導権（Chat Control）はモジュールチャネルごとに、一括して設定するものではありません**

主導権（Chat Control）は、ユーザー、トークルーム、またはグループごとに管理されています。

<!-- note end -->

<!-- note start -->

**「Default Active」の機能が付与されたモジュールチャネル**

「Default Active」の機能が付与されたモジュールチャネルは、LINE公式アカウントにアタッチすると自動的にActive Channelになるモジュールチャネルです。

詳しくは、「[Default Active](https://developers.line.biz/ja/docs/partner-docs/module-technical-chat-control/#default-active)」を参照してください。

<!-- note end -->

## API reference 

- [Acquire Control API](https://developers.line.biz/ja/reference/partner-docs/#acquire-control-api)
- [Release Control API](https://developers.line.biz/ja/reference/partner-docs/#release-control-api)

## Default active 

LINEマーケットプレイスで提供するモジュールチャネルには、「Default Active」の機能が付与されています。

<!-- note start -->

**LINEマーケットプレイス専用の機能です**

「Default Active」の機能は、[LINEマーケットプレイス](https://line-marketplace.com/jp/inquiry)で公開するモジュールチャネルでのみ利用できます。

<!-- note end -->

「Default Active」の機能が付与されたモジュールチャネルの特徴は、以下のとおりです。

### 自動Active 

通常のモジュールチャネルは、LINE公式アカウントにアタッチするとStandby Channelになります。その後、（ユーザーの操作などを契機として）必要に応じてAcquire Control APIを利用してモジュールチャネルが主導権（Chat Control）を取得し、Active Channelになります。

「Default Active」の機能が付与されたモジュールチャネルは、LINE公式アカウントにアタッチすると自動的にActive Channelになります。そのため、Acquire Control APIを呼び出す必要がありません。

### 排他制御 

1つのLINE公式アカウントには、「Default Active」の機能が付与されたモジュールチャネルを1つだけアタッチできます。

すでに「Default Active」の機能が付与されたモジュールチャネルがアタッチされているLINE公式アカウントには、そのほかの「Default Active」の機能が付与されたモジュールチャネルをアタッチすることはできません。

なお、「Default Active」の機能が付与されていないモジュールチャネルは、複数アタッチできますが、現在LINEマーケットプレイスでは提供していません。
