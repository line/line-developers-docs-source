# 法人ユーザー向けのお知らせ

法人ユーザー向けのお知らせです。[ニュース](https://developers.line.biz/ja/news/)もあわせてご参照ください。

2026/02/19

## ミッションスタンプAPIにおいて一部のエラーレスポンスを変更しました 

ミッションスタンプAPIの「[ユーザーにミッションスタンプを提供する](https://developers.line.biz/ja/reference/partner-docs/#send-mission-stickers-v3)」エンドポイントにおいて、ユーザーの属性情報が推測できないようエラーレスポンスの内容を一部変更しました。

詳しくは、「ユーザーにミッションスタンプを提供する」エンドポイントの「[エラーメッセージ](https://developers.line.biz/ja/reference/partner-docs/#send-mission-stickers-v3-error-messages)」を参照してください。

2025/06/30

## エラー通知で送信されるメールの件名と本文を変更しました 

2025年6月30日より、Webhookのエラー通知で送信されるメールの件名と本文を変更しました。

詳しくは、「[通知メールの例](https://developers.line.biz/ja/docs/partner-docs/error-notification/#sample-mail)」を参照してください。

2025/06/18

## LINE通知メッセージに「重要なお知らせ」と表示されるようになりました 

LINE通知メッセージは、通常のメッセージと区別できるようLINE公式アカウントのアイコンの右側に「重要なお知らせ」と表示されるようになりました。

![LINE通知メッセージはアイコンの右側に「重要なお知らせ」と表示される](https://developers.line.biz/media/line-notification-message/notification-messages-important-ja.jpg)

詳しくは、『LINE通知メッセージドキュメント』の「[LINE通知メッセージ以外のメッセージとの見た目の差異](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/overview/#difference-from-other-messages)」を参照してください。

2025/06/18

## ミッションスタンプAPIのエンドポイント名を変更しました 

ミッションスタンプAPIの「ミッションスタンプを送る（v3）」エンドポイントについて、名称がよりわかりやすくなるようエンドポイント名を変更しました。機能に変更はありません。

| 変更前の名称                   | 変更後の名称（現在）                   |
| ------------------------------ | -------------------------------------- |
| ミッションスタンプを送る（v3） | ユーザーにミッションスタンプを提供する |

詳しくは、『法人ユーザー向けオプションAPIリファレンス』の「[ミッションスタンプAPI](https://developers.line.biz/ja/reference/partner-docs/#mission-stickers)」を参照してください。

2025/06/02

## LINE通知メッセージ（テンプレート）の提供を開始しました 

LINE通知メッセージに、用意されたテンプレートやアイテムを組み合わせて簡単にメッセージを作成できる「[LINE通知メッセージ（テンプレート）](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/template/)」が新たに加わりました。

これに伴い、UX審査を要する従来の「LINE通知メッセージ」は、名称が「LINE通知メッセージ（フレキシブル）」に変更されました。

詳しくは、「[LINE通知メッセージの概要](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/overview/)」を参照してください。

2025/01/28

## LINE通知メッセージのWebhookイベントにおけるsourceプロパティを削除しました 

[2024年8月9日](https://developers.line.biz/ja/docs/partner-docs/notice/#partner-news-20240809)にお知らせしたとおり、2025年1月28日をもって、LINE通知メッセージの[Webhookの配信完了イベント](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#receive-delivery-event)における`source`プロパティを削除しました。

これまでは、LINE通知メッセージAPIをリクエストし、ユーザーに対するLINE通知メッセージの配信が完了したときに、以下のようなWebhookイベントがLINEプラットフォームからボットサーバーに送信されていました。

```json
{
  "destination": "Uc7472b39e21dab71c2347e02714630d6",
  "events": [
    {
      "type": "delivery",
      "delivery": {
        "data": "68df277462529930889fab80ecffdc0883906320591df93c25efc08300410fc2"
      },
      "webhookEventId": "01G17DAF0QJ7A3ERC5EJ9MAMH8",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1650590038721,
      // 以下のsourceプロパティが削除されました
      "source": {
        "type": "user",
        "userId": "U8189cf6745fc0d808977bdb0b9f22995"
      },
      "mode": "active"
    }
  ]
}
```

このWebhookイベントに含まれる`source`プロパティが、2025年1月28日をもって削除されました。

LINEヤフー株式会社は、今後もお客様への一層のサービス向上に取り組んでまいります。何卒ご理解を賜りますよう、よろしくお願い申し上げます。

2024/10/18

## クイック入力のドキュメントを公開しました 

クイック入力とは、LINEミニアプリ上で［**自動入力**］をタップすることで、必要なプロフィール情報が自動で入力される機能です。ユーザーがアカウントセンターで設定した共通プロフィールの情報が、LINEミニアプリで簡単に利用できます。

![](https://developers.line.biz/media/line-mini-app/quick-fill/quick-fill-3-steps.png)

LINEミニアプリにクイック入力を導入すると、住所や電話番号の登録が必要な場面で、ボタンをタップするだけで必要な情報が自動で入力されます。これにより、たとえばお店の予約やオンラインストアでの注文時に、ユーザーは面倒な手入力の手間を省くことができます。

クイック入力は、弊社からご案内している特定の法人ユーザーのみがご利用いただけます。

LINEミニアプリでクイック入力を組み込む方法について詳しくは、「[クイック入力の概要](https://developers.line.biz/ja/docs/partner-docs/quick-fill/overview/)」を参照してください。

2024/08/09

## 2025年1月28日をもって、LINE通知メッセージのWebhookイベントにおけるsourceプロパティを削除します 

2025年1月28日をもって、LINE通知メッセージの[Webhookの配信完了イベント](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#receive-delivery-event)における`source`プロパティを削除します。

LINE通知メッセージAPIをリクエストし、ユーザーに対するLINE通知メッセージの配信が完了したときに、以下のようなWebhookイベントがLINEプラットフォームからボットサーバーに送信されます。

```json
{
  "destination": "Uc7472b39e21dab71c2347e02714630d6",
  "events": [
    {
      "type": "delivery",
      "delivery": {
        "data": "68df277462529930889fab80ecffdc0883906320591df93c25efc08300410fc2"
      },
      "webhookEventId": "01G17DAF0QJ7A3ERC5EJ9MAMH8",
      "deliveryContext": {
        "isRedelivery": false
      },
      "timestamp": 1650590038721,
      // 以下のsourceプロパティが削除されます
      "source": {
        "type": "user",
        "userId": "U8189cf6745fc0d808977bdb0b9f22995"
      },
      "mode": "active"
    }
  ]
}
```

このWebhookイベントに含まれる`source`プロパティが、2025年1月28日をもって削除されます。なお、プロパティを削除する日時は、予告なく変更される可能性があります。

LINEヤフー株式会社は、今後もお客様への一層のサービス向上に取り組んでまいります。何卒ご理解を賜りますよう、よろしくお願い申し上げます。

2024/05/07

## モジュール メンテナンスのお知らせ 

2024年6月5日 2:00頃 ～ 3:00頃（UTC+9）に、モジュールにおいてメンテナンスを予定しています。詳しくは、2024年5月7日のニュース、「[Messaging API、モジュール、およびLINE Developersコンソール メンテナンスのお知らせ](https://developers.line.biz/ja/news/2024/05/07/maintenance-notice/)」を参照してください。

2024/04/26

## Webhook再送を停止した際に通知メールが送信されるようになりました 

Messaging APIの機能として提供している「[エラー通知](https://developers.line.biz/ja/docs/partner-docs/error-notification/)」において、Webhook再送を停止する際に通知メールが送信されるようになりました。

Messaging APIチャネルの設定で[Webhookの再送を有効](https://developers.line.biz/ja/docs/messaging-api/receiving-messages/#enable-webhook-redelivery)にしていた場合、LINEプラットフォームは、ボットサーバーが受け取りに失敗したWebhookを再送します。しかし、一定の期間Webhookを再送し続けてもボットサーバーからの応答がなかった場合、LINEプラットフォームは再送を停止します。

従来はLINEプラットフォームがエラー発生を検知した際に1回だけエラー通知のメールを送信していましたが、この変更によりWebhook再送の開始時と停止時の両方において通知メールが送信されます。

詳しくは、「[LINEプラットフォームがWebhookの再送を停止したとき](https://developers.line.biz/ja/docs/partner-docs/error-notification/#webhook-redelivery-stopped)」を参照してください。

2023/11/01

## 2023年10月31日をもちまして、オーディエンスマッチAPIの提供を終了しました 

[2023年7月18日](https://developers.line.biz/ja/docs/partner-docs/notice/#partner-news-20230718)にお知らせしたとおり、2023年10月31日をもちまして、オーディエンスマッチAPIの提供を終了しました。

LINEヤフー株式会社は今後もお客様への一層のサービス向上に取り組んでまいります。何卒ご理解を賜りますよう、よろしくお願い申し上げます。

2023/08/31

## ステートレスチャネルアクセストークンをリリースしました 

ステートレスチャネルアクセストークンは、15分間だけ有効なチャネルアクセストークンです。発行できる数に制限はありません。ステートレスチャネルアクセストークンは、Messaging APIチャネルやモジュールチャネルを使用する際などに使用できます。

ステートレスチャネルアクセストークンについて詳しくは、2023年8月31日のニュース、「[ステートレスチャネルアクセストークンをリリースしました](https://developers.line.biz/ja/news/2023/08/31/stateless-channel-access-token/)」を参照してください。

2023/07/18

## 2023年10月31日をもちまして、電話番号を利用したメッセージ送信機能の提供を終了します 

2023年10月31日をもちまして、オーディエンスマッチAPIの電話番号を利用したメッセージ送信機能の提供を終了します。これに伴い、オーディエンスマッチAPIの提供も終了します。

関連するドキュメントおよびAPIリファレンスは、提供終了後に予告なく削除される予定です。

### 対象となるエンドポイント 

提供終了に伴い、以下のエンドポイントは順次利用できなくなります。

- [電話番号を利用してメッセージを送る](https://developers.line.biz/ja/reference/partner-docs/#phone-audience-match)
- [電話番号を利用したメッセージ配信の結果を取得する](https://developers.line.biz/ja/reference/partner-docs/#get-phone-audience-match)

### 提供終了予定日 

2023年10月31日

なお提供終了の日時は、予告なく変更される可能性があります。

LINEは今後もお客様への一層のサービス向上に取り組んでまいります。何卒ご理解を賜りますよう、よろしくお願い申し上げます。

2023/05/31

## 「ミッションスタンプを送る（v2）」エンドポイントを廃止しました 

[2023年2月2日](https://developers.line.biz/ja/docs/partner-docs/notice/#partner-news-20230202)にお知らせしたとおり、2023年5月31日をもって、「ミッションスタンプを送る（v2）」エンドポイントを廃止しました。今後は、「[ミッションスタンプを送る（v3）](https://developers.line.biz/ja/reference/partner-docs/#send-mission-stickers-v3)」エンドポイントをご利用ください。

2023/04/11

## モジュール メンテナンスのお知らせ 

2023年5月11日 2:00頃 ～ 3:00頃（UTC+9）に、モジュールにおいてメンテナンスを行います。詳しくは、2023年4月11日のニュース、「[Messaging API、モジュール、およびLINE Developersコンソール メンテナンスのお知らせ](https://developers.line.biz/ja/news/2023/04/11/messaging-api-module-and-console-maintenance/)」を参照してください。

2023/02/20

## Mark-as-Read APIの名称を「既読API」に変更しました 

Mark-as-Read APIについて、名称がよりわかりやすくなるよう、「既読API」に変更しました。機能に変更はありません。

| 言語   | 変更前の名称     | 変更後の名称     |
| ------ | ---------------- | ---------------- |
| 日本語 | Mark-as-Read API | 既読API          |
| 英語   | Mark-as-Read API | Mark as read API |

既読APIについて詳しくは、「[既読API](https://developers.line.biz/ja/docs/partner-docs/mark-as-read/)」を参照してください。

2023/02/02

## 2023年5月31日をもって、「ミッションスタンプを送る（v2）」エンドポイントを廃止します 

2023年5月31日をもって、「ミッションスタンプを送る（v2）」エンドポイントを廃止いたします。廃止後は、「[ミッションスタンプを送る（v3）](https://developers.line.biz/ja/reference/partner-docs/#send-mission-stickers-v3)」エンドポイントをご利用ください。

関連するドキュメントおよびAPIリファレンスは、廃止後に予告なく削除される予定です。

2022/12/20

## モジュール Referenceの提供方法変更のお知らせ 

モジュール Referenceは、これまでPDFファイルで提供しておりましたが、これからはLINE Developersサイト内のドキュメントとして提供いたします。今後はモジュールの「[ドキュメント](https://developers.line.biz/ja/docs/partner-docs/#%E3%83%A2%E3%82%B7%E3%82%99%E3%83%A5%E3%83%BC%E3%83%AB)」および「[APIリファレンス](https://developers.line.biz/ja/reference/partner-docs/#module)」をご参照ください。

2022/09/28

## 「任意の集計単位で統計情報を取得する機能」についてのお知らせ 

「[任意の集計単位で統計情報を取得する機能](https://developers.line.biz/ja/docs/messaging-api/unit-based-statistics-aggregation/)」は、Messaging APIに統合されました。

詳しくは、2022年9月28日のニュース、「[Messaging APIで「任意の集計単位で統計情報を取得する機能」が利用できるようなりました](https://developers.line.biz/ja/news/2022/09/28/messaging-api-updated/)」を参照してください。

2022/08/23

## LINE API Policy Handbookを公開しました 

LINE API Policy Handbookを公開しました。本ハンドブックは、LINE APIについて、より理解を深めて正しくご利用いただけるよう、[LINE公式アカウント利用規約](https://terms2.line.me/official_account_terms_jp?lang=ja&country=JP)および[LINE公式アカウントAPI利用規約](https://terms2.line.me/official_account_api_terms_jp?lang=ja&country=JP)の関連文書として定めたものです。

詳しくは、「[LINE API Policy Handbook](https://developers.line.biz/ja/docs/partner-docs/api-policy-handbook/)」を参照してください。

2022/06/28

## LINE通知メッセージのドキュメントを公開しました 

LINE通知メッセージは、ユーザーの[ユーザーID](https://developers.line.biz/ja/glossary/#user-id)を知らなくても、ユーザーの電話番号を指定してメッセージを送信できるサービスです。ユーザーがLINE公式アカウントを友だち追加していなくても、LINE公式アカウントからメッセージを送信できます。

従来から公開していたLINE通知メッセージの概要に加えて、「[LINE通知メッセージAPIの技術仕様](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/)」や「[LINE通知メッセージAPIリファレンス](https://developers.line.biz/ja/reference/line-notification-messages/)」などのドキュメントを公開しました。

LINE通知メッセージについて詳しくは、「[LINE通知メッセージの概要](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/overview/)」を参照してください。

2022/03/24

## モジュールのドキュメントを公開しました 

モジュールを利用することで、Messaging APIチャネルを利用していないLINE公式アカウントにおいても、Messaging APIを利用した高度な機能を簡単に追加することができます。このモジュールのドキュメントを公開しました。モジュールについて詳しくは、「[モジュール](https://developers.line.biz/ja/docs/partner-docs/module/)」を参照してください。

2022/01/05

## IFAを利用したメッセージ送信機能の提供を終了しました 

[2021年12月1日](https://developers.line.biz/ja/docs/partner-docs/notice/#partner-news-20211201)にお知らせしたとおり、2021年12月31日をもちまして、オーディエンスマッチAPIのIFA（Identifier for Advertisers）を利用したメッセージ送信機能の提供は終了しました。

LINEは今後もお客様への一層のサービス向上に取り組んでまいります。何卒ご理解を賜りますよう、よろしくお願い申し上げます。

2021/12/06

## LINEボット開発ガイドラインの提供方法変更のお知らせ 

LINEボット開発ガイドラインは、これまでPDFファイルで提供しておりましたが、これからはLINE Developersサイト内のドキュメントとして提供いたします。また、あわせてガイドラインの名称を「[法人ユーザー向け開発ガイドライン](https://developers.line.biz/ja/docs/partner-docs/development-guidelines/)」に変更しております。今後はこちらをご参照ください。

2021/12/01

## IFAを利用したメッセージ送信機能の提供を終了します 

2021年12月31日をもちまして、オーディエンスマッチAPIのIFA（Identifier for Advertisers）を利用したメッセージ送信機能の提供を終了します。

関連するドキュメントおよびAPIリファレンスは、提供終了後に予告なく削除される予定です。

### 対象となるエンドポイント 

提供終了に伴い、以下のエンドポイントは順次利用できなくなります。

- モバイル広告IDを利用してメッセージを送る
- モバイル広告IDを利用したメッセージ配信の結果を取得する

### 提供終了予定日 

2021年12月31日

なお提供終了の日時は、予告なく変更される可能性があります。

LINEは今後もお客様への一層のサービス向上に取り組んでまいります。何卒ご理解を賜りますよう、よろしくお願い申し上げます。

2021/07/09

## 「任意の集計単位で統計情報を取得する機能」のドキュメント訂正のお知らせ 

「[任意の集計単位で統計情報を取得する](https://developers.line.biz/ja/docs/messaging-api/unit-based-statistics-aggregation/)」機能のAPIリファレンスにおいて、リクエストボディの記載に誤りがありました。お詫びして訂正いたします。

正誤については、以下の表を参照してください。

- **メッセージ送信時に任意の集計単位のユニット名を付与する**

  | 項目                                 | 誤  | 正  |
  | ------------------------------------ | --- | --- |
  | `customAggregationUnits`の最大文字数 | 100 | 30  |

なおメッセージを送信する際に、最大文字数を超えた任意の集計単位のユニット名を指定した場合、リクエストは失敗しませんが、対象のメッセージに対してユニット名が付与されない状態となります。

2021/04/28

## エラー通知で送信されるメールの件名を変更します 

<!-- note start -->

**2021年5月25日追記**

「[変更点](https://developers.line.biz/ja/docs/partner-docs/notice/#partner-news-20210428-01)」と「[変更予定日](https://developers.line.biz/ja/docs/partner-docs/notice/#partner-news-20210428-02)」を更新しました。

<!-- note end -->

Messaging APIの機能として提供している「[エラー通知](https://developers.line.biz/ja/docs/partner-docs/error-notification/)」において、以下の変更を予定しています。

### 変更点 

[送信されるメール](https://developers.line.biz/ja/docs/partner-docs/error-notification/#mail)の件名を以下の通り変更します。またメール本文につきましても、より分かりやすい文になるように一部変更を予定しています。

| 項目 | 変更前 | 変更後 |
| --- | --- | --- |
| **件名** | Messaging API: Webhook transmission failed - `<Channel name>` | Messaging API: Your server did not return \[200 OK\] - `<Channel name>` |

`<Channel name>`の部分には、対象チャネルのチャネル名が入ります。

### 変更予定日 

2021年5月25日

エラー通知について詳しくは、『法人ユーザー向けオプションドキュメント』の「[エラー通知](https://developers.line.biz/ja/docs/partner-docs/error-notification/)」を参照してください。

2021/03/10

## 任意の集計単位で統計情報を取得する機能がリリースされました 

複数のプッシュメッセージやマルチキャストメッセージをまとめて、任意の集計単位で統計情報を取得できるようになりました。メッセージの配信時にユニット名を付与して送ることで、後からユニットごとの統計情報が確認できます。

<!-- tip start -->

**任意の集計単位で統計情報を取得する機能はどんなときに便利？**

多人数を対象としたナローキャストメッセージやブロードキャストメッセージの配信時は、リクエストIDを指定することで、そのメッセージについて「[ユーザーの操作に基づく統計情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-message-event)」ことができます。

![ユーザーの操作に基づく統計情報](https://developers.line.biz/media/news/old_statistics_ja.png)

一方で配信対象の人数が20人未満の場合は、ユーザーのプライバシーを保護するため、統計情報が取得できません。しかし今回リリースされた「[任意の集計単位で統計情報を取得する](https://developers.line.biz/ja/docs/messaging-api/unit-based-statistics-aggregation/)」機能を使えば、少人数を対象としたメッセージ配信であっても、メッセージの配信時にユニット名を付与して送ることで、複数のメッセージをまとめたユニットごとの統計情報が取得できます。

![ユニットごとの統計情報集計](https://developers.line.biz/media/news/new_statistics_ja.png)

<!-- tip end -->

詳しくは、『法人ユーザー向けオプションドキュメント』の「[任意の集計単位で統計情報を取得する](https://developers.line.biz/ja/docs/messaging-api/unit-based-statistics-aggregation/)」を参照してください。

2020/03/17

## Icon/Nickname Switchについてのお知らせ 

Icon/Nickname Switchは、Messaging APIに統合されました。

詳細は、「[アイコンおよび表示名が変更できるようになりました（2020年3月17日）](https://developers.line.biz/ja/news/2020/03/17/icon-nickname-switch/)」をご参照ください。
