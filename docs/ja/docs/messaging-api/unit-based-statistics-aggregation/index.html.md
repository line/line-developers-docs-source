# 送信したメッセージの統計情報を取得する

Messaging APIでは、LINE公式アカウントから送信したメッセージを、ユーザーがどのように操作したかを統計情報として取得できます。統計情報の取得方法は、送信するメッセージの種類によって異なります。

- [すべての友だち、またはオーディエンスや属性で絞り込んだ友だちに送信したメッセージの統計情報](https://developers.line.biz/ja/docs/messaging-api/unit-based-statistics-aggregation/#get-statistics-on-narrowcast-or-broadcast)
  - ブロードキャストメッセージ
  - ナローキャストメッセージ
- [特定の友だちやグループトーク、または電話番号を指定して送信したメッセージの統計情報](https://developers.line.biz/ja/docs/messaging-api/unit-based-statistics-aggregation/#get-statistics-on-push-multicast-or-line-notification-messages)
  - プッシュメッセージ
  - マルチキャストメッセージ
  - LINE通知メッセージ

## すべての友だち、またはオーディエンスや属性で絞り込んだ友だちに送信したメッセージの統計情報 

[ナローキャストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message)または[ブロードキャストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-broadcast-message)では、ユーザーがメッセージをどのように操作したかを、送信リクエストごとの統計情報として取得できます。詳しくは、『Messaging APIリファレンス』の「[ユーザーの操作に基づく統計情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-message-event)」を参照してください。

## 特定の友だちやグループトーク、または電話番号を指定して送信したメッセージの統計情報 

[プッシュメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-push-message)、[マルチキャストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-multicast-message)、[LINE通知メッセージ](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/overview/)では、ユーザーがメッセージをどのように操作したかを、ユニットごとの統計情報として取得できます。

通常、プッシュメッセージ、マルチキャストメッセージ、およびLINE通知メッセージでは、ユーザーのプライバシー保護の観点から、メッセージの開封やURLのタップなど、ユーザーがメッセージに対して行った操作については、統計情報を取得できません。しかし、任意の「ユニット」単位で情報を集計し、個人が特定できない形にすることで、統計情報の取得が可能です。

<!-- tip start -->

**LINE通知メッセージでユニット名を指定する**

Messaging APIのプッシュメッセージとマルチキャストメッセージだけでなく、法人ユーザー向けオプションであるLINE通知メッセージでも、メッセージの送信時にユニット名を指定できます。詳しくは、『LINE通知メッセージドキュメント』の「[LINE通知メッセージの統計情報を取得する](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/statistics/)」を参照してください。

<!-- tip end -->

下図のように、ユニット名を付与してメッセージを送信することで、ユニットごとのメッセージの統計情報を取得できるようになります。

![](https://developers.line.biz/media/news/customAggregationUnits_ja.png)

### ユニットごとの統計情報とは 

メッセージについて、ユニットごとに以下のような統計情報が取得できます。

- メッセージを開封した人数
- メッセージ内のいずれかのURLをタップした人数
- メッセージ内のいずれかの動画または音声の再生を開始した人数

メッセージの統計情報を取得することで、送信したメッセージに対してユーザーがどのような操作をしたかを知ることができます。このような統計情報を用いることで、以下のような情報を確認できます。

**取得した統計情報を用いた例**

| 送信対象の人数 | 開封数 | 開封率 | URLタップ数 | URLタップ率 |
| -------------- | ------ | ------ | ----------- | ----------- |
| 500            | 433    | 87%    | 323         | 65%         |

#### 集計される統計情報についての注意点 

統計情報の数値は、多少の誤差を含むことがあります。またプライバシーを保護するため、次のような場合、個人の操作に関する統計情報の値は`null`になります。

- 集計された統計情報の値が20未満だった場合。
- 集計された統計情報の値が20以上であっても、そのイベントを発生させた実人数が20人未満だった場合。
  - たとえば、動画が再生開始された回数が30回だったとしても、動画を再生開始した人数が15人だった場合は、どちらの値も`null`になります。

「[ユニットごとの統計情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-statistics-per-unit)」エンドポイントのレスポンスには、送信通数および送信対象となったユーザー数は含まれません。また、`overview.uniqueImpression`は、集計対象期間中にメッセージを1回以上開封したユニークユーザー数です。そのため、このレスポンスだけでは、送信通数を分母とする開封率や、送信対象のユーザー数を分母とするリーチ率を算出できません。

### ユニット名を付与する 

統計情報を取得するには、プッシュメッセージ、マルチキャストメッセージ、またはLINE通知メッセージを送信する際に、任意の集計単位のユニット名を付与する必要があります。ユニット名を付与するには、メッセージ送信時にリクエストボディの`customAggregationUnits`プロパティにユニット名を指定してください。メッセージ送信時に指定できるユニット名は1つだけです。プッシュメッセージやマルチキャストメッセージの送信方法について詳しくは、『Messaging APIリファレンス』の「[メッセージ](https://developers.line.biz/ja/reference/messaging-api/#messages)」を参照してください。

以下の例では、`promotion_a`というユニット名を付与してプッシュメッセージを送信しています。

```sh
curl -v -X POST https://api.line.me/v2/bot/message/push \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {channel access token}' \
-d '{
    "to": "U4af4980629...",
    "messages":[
        {
            "type": "text",
            "text": "Hello, world1"
        }
    ],
    "customAggregationUnits": [
        "promotion_a"
    ]
}'
```

<!-- tip start -->

**ユニット名の後付けや変更について**

既に送信したメッセージに後からユニット名を付与したり、ユニット名を変更したりすることはできません。

<!-- tip end -->

#### ユニット名の種類数の上限 

当月中（その月の1日から末日）に、最大で1,000種類のユニット名を付与してメッセージを送信できます。

たとえば3月に`promotion_0001`から`promotion_1000`まで1,000種類のユニット名を付与してメッセージを送信したとします。その場合、翌月（4月）に同じ`promotion_0001`から`promotion_1000`までの1,000種類のユニット名を付与してメッセージを送信することも可能ですし、新しいユニット名である`promotion_1001`から`promotion_2000`までの1,000種類を付与してメッセージを送信することも可能です。

なお、1,001種類目以降のユニット名を付与してメッセージを送信すると、メッセージ自体は送られますが、1,001種類目以降のユニット名は付与されません。たとえば、`promotion_0001`から`promotion_1500`までの1,500種類を付与して送信した場合、`promotion_1001`以降のユニット名はメッセージに付与されません。

ユニット名の種類が多い場合は、以下のいずれかの方法でユニット名が付与できる、あるいは付与できたことを確認してください。

- 当月のユニット名がまだ1,000種類に達していないことを、メッセージの送信前に「[当月中に付与したユニット名の種類数を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-the-number-of-unit-name-types-assigned-during-this-month)」エンドポイントで確認する
- メッセージの送信後に「[当月中に付与したユニット名のリストを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-a-list-of-unit-names-assigned-during-this-month)」エンドポイントで、付与したユニット名が存在することを確認する

同じユニット名を付与して送信したプッシュメッセージ、マルチキャストメッセージ、LINE通知メッセージ（テンプレート）、LINE通知メッセージ（フレキシブル）の統計情報はまとめて集計されます。また、月間のユニット名の種類数は、これらの送信方法をまたいで、一意のユニット名をカウントした数です。

<!-- tip start -->

**ユニット名の制限について**

ユニット名を付与する際には「当月中に最大で1,000種類まで」という制限がありますが、メッセージの送信後に[ユニットごとの統計情報を取得する](https://developers.line.biz/ja/docs/messaging-api/unit-based-statistics-aggregation/#get-statistics-per-unit)際には、`from`から`to`までの集計対象期間に存在するすべてのユニットの統計情報が取得できます。

<!-- tip end -->

### ユニットごとの統計情報を取得する 

ユニット名を付与して送信したメッセージの統計情報は、「[ユニットごとの統計情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-statistics-per-unit)」エンドポイントで取得できます。以下の例では、`promotion_a`という名前のユニットの統計情報を取得しています。

```sh
curl -v -X GET https://api.line.me/v2/bot/insight/message/event/aggregation \
-H 'Authorization: Bearer {channel access token}' \
--data-urlencode 'customAggregationUnit=promotion_a' \
--data-urlencode 'from=20210301' \
--data-urlencode 'to=20210331' \
-G
```

なお、当月中に付与したユニット名は、「[当月に付与したユニット名のリストを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-a-list-of-unit-names-assigned-during-this-month)」エンドポイントで取得できます。前月以前に付与したユニット名を確認するためのエンドポイントはありません。

### URLを含むメッセージの統計情報を取得する例 

以下の手順は、URLを含むメッセージの統計情報をユニットごとに取得する例です。

#### 1. ユニット名を付与してメッセージを送信する 

まず、複数のユーザーに同じ内容のメッセージを送ります。

![](https://developers.line.biz/media/messaging-api/insight/new-item-message-example-ja.png)

ここでは、マルチキャストメッセージを使って、150人のユーザーにメッセージを送るとします。このとき、`customAggregationUnits`プロパティでユニット名を指定します。

```sh
curl -v -X POST https://api.line.me/v2/bot/message/multicast \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {channel access token}' \
-d '{
    "to": ["U4af4980629...","U0c229f96c4...",...], // 150件のユーザーID
    "messages":[
        {
            "type": "text",
            "text": "🆕 新商品が入荷しました！\nhttps://example.com/new-item/"
        }
    ],
    "customAggregationUnits": [
        "new-item-message-yyyymmdd"
    ]
}'
```

#### 2. 統計情報を取得して集計する 

メッセージを送信してから数日待ち、ユニットごとの統計情報を取得します。

```sh
curl -v -X GET https://api.line.me/v2/bot/insight/message/event/aggregation \
-H 'Authorization: Bearer {channel access token}' \
--data-urlencode 'customAggregationUnit=new-item-message-yyyymmdd' \
--data-urlencode 'from=20210301' \
--data-urlencode 'to=20210331' \
-G
```

この例では、以下のような統計情報が取得できます。

```json
{
  "overview": {
    "uniqueImpression": 111,
    "uniqueClick": 74,
    "uniqueMediaPlayed": null,
    "uniqueMediaPlayed100Percent": null
  },
  "messages": [
    {
      "seq": 1,
      "impression": 111,
      "uniqueImpression": 111,
      "mediaPlayed": null,
      "mediaPlayed25Percent": null,
      "mediaPlayed50Percent": null,
      "mediaPlayed75Percent": null,
      "mediaPlayed100Percent": null,
      "uniqueMediaPlayed": null,
      "uniqueMediaPlayed25Percent": null,
      "uniqueMediaPlayed50Percent": null,
      "uniqueMediaPlayed75Percent": null,
      "uniqueMediaPlayed100Percent": null
    }
  ],
  "clicks": [
    {
      "seq": 1,
      "url": "https://example.com/new-item/",
      "click": 74,
      "uniqueClick": 74,
      "uniqueClickOfRequest": 74
    }
  ]
}
```

これらの情報を用いて、メッセージの開封率や、URLのタップ率などを確認できます。

| 送信対象の人数 | 開封数 | 開封率 | URLタップ数 | URLタップ率 |
| -------------- | ------ | ------ | ----------- | ----------- |
| 150            | 111    | 74%    | 74          | 67%         |
