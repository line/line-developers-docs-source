# オーディエンスを使う

オーディエンス機能を使うと、高度なターゲティングができます。たとえば、メッセージを開封したユーザーや、メッセージのURLをクリックしたユーザーのグループをターゲットにできます。

<!-- note start -->

**注意**

日本、タイ、台湾のユーザーが作成したLINE公式アカウントの場合のみ、オーディエンスを作成できます。

<!-- note end -->

<!-- note start -->

**Identifier for Advertisers（IFA）を使用するには**

送信対象アカウントをIFAで指定することもできますが、この機能は、所定の申請等を行った法人ユーザーのみがご利用いただけます。自社のLINE公式アカウントでご利用になりたいお客様は、担当営業までご連絡いただくか、[弊社パートナー](https://www.lycbiz.com/jp/partner/sales/)にお問い合わせください。

<!-- note end -->

## オーディエンスを作成する 

オーディエンスはMessaging APIで作成できます。作成できるオーディエンスは次のとおりです。

| オーディエンス | 説明 |
| --- | --- |
| [ユーザーIDアップロード用のオーディエンス](https://developers.line.biz/ja/reference/messaging-api/#create-upload-audience-group) | [ユーザーID](https://developers.line.biz/ja/glossary/#user-id)やIFA（Identifier For Advertisers）で特定できるユーザーの集合 |
| [メッセージクリックオーディエンス](https://developers.line.biz/ja/reference/messaging-api/#create-click-audience-group) | 過去に配信したメッセージのURLをクリックしたユーザーの集合 |
| [メッセージインプレッションオーディエンス](https://developers.line.biz/ja/reference/messaging-api/#create-imp-audience-group) | 過去に配信したメッセージを開封したユーザーの集合 |

なお、Messaging APIでは、次のタイプのオーディエンスは作成できません。

- チャットタグオーディエンス
- 追加経路オーディエンス
- 予約オーディエンス
- リッチメニューインプレッションオーディエンス
- リッチメニュークリックオーディエンス
- ウェブトラフィックオーディエンス（LINE Tag）
- ウェブトラフィックオーディエンス（計測タグ）
- アプリイベントオーディエンス
- 動画視聴オーディエンス
- 画像クリックオーディエンス
- LINE Beacon Networkインプレッションオーディエンス

<!-- note start -->

**同時処理数の制限があります**

ユーザーIDアップロード用のオーディエンス作成およびオーディエンスへのユーザーID追加のエンドポイントでは、オーディエンスID（`audienceGroupId`）単位での同時処理数の制限があります。詳しくは、「[同時処理数の制限](https://developers.line.biz/ja/reference/messaging-api/#limit-on-the-number-of-concurrent-operations)」を参照してください。

<!-- note end -->

## オーディエンスを使う 

オーディエンスは、ナローキャストメッセージの送信で使用できます。詳しくは、「[ナローキャストメッセージを送信する](https://developers.line.biz/ja/docs/messaging-api/sending-messages/#send-narrowcast-message)」を参照してください。

## オーディエンスを共有する 

Messaging APIと[LINE Official Account Manager](https://manager.line.biz/)では、同じLINE公式アカウントにおいて作成したオーディエンスを相互に利用できます。オーディエンスの相互利用に際して、必要な初期設定はありません。

Messaging APIとLINE Official Account Manager以外のツール（[LINE広告マネージャ](https://admanager.line.biz/)など）でオーディエンスを相互に利用したい場合は、オーディエンスを共有する設定が必要です。オーディエンスを共有する方法について詳しくは、「[ビジネスマネージャーでオーディエンスを共有する](https://developers.line.biz/ja/docs/messaging-api/using-audience/#audience-sharing-business-manager)」を参照してください。

| オーディエンスを作成するツール | オーディエンスを利用するツール | オーディエンスの利用可否 |
| --- | --- | --- |
| Messaging API | LINE Official Account Manager | ✅ |
| LINE Official Account Manager | Messaging API | ✅ |
| Messaging API | LINE Official Account Manager以外のツール | ✅ \*1 |
| LINE Official Account Manager以外のツール | Messaging API | ✅ \*1 |

\*1 ビジネスマネージャでオーディエンスを共有すれば利用可能

### ビジネスマネージャーでオーディエンスを共有する 

[ビジネスマネージャー](https://data.linebiz.com/solutions/business-manager)を使うことで、特定のオーディエンスを複数のサービス（LINE広告マネージャなど）で共有して、相互に利用できるようになります。

またビジネスマネージャーのオーディエンス共有機能を使うことで、同一プロバイダー配下のMessaging APIチャネル間でもオーディエンスを共有できます。ただしビジネスマネージャーでオーディエンスの共有を設定できるLINE公式アカウントは、認証済アカウントと[プレミアムアカウント](https://developers.line.biz/ja/glossary/#premium-account)のみです。

ビジネスマネージャーで共有されたオーディエンスの情報は、以下のエンドポイントで取得できます。

- [ビジネスマネージャーで共有されたオーディエンスのリストを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-shared-audience-list)
- [ビジネスマネージャーで共有されたオーディエンスの情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-shared-audience)

オーディエンスの共有方法について詳しくは、『ビジネスマネージャーマニュアル』の「[リソースの共有](https://data.linebiz.com/business-manager/manual/bmmaniyuarushare003)」を参照してください。

## オーディエンスの仕様について 

オーディエンスの仕様は以下のとおりです。

| 項目 | 仕様 |
| --- | --- |
| チャネルあたりのオーディエンス数 | 最大1,000件 |
| オーディエンスの保存期間 | 最大180日間（15,552,000秒間） |
| ユーザーIDアップロード用のオーディエンスに1リクエストでアップロードできるユーザーIDまたはIFAの数 | <ul><li>JSONを使用する場合：最大10,000件</li><li>ファイルを使用する場合：最大1,500,000件</li></ul> |
| オーディエンスあたりのユーザー数 | <ul><li>ユーザーIDアップロード用のオーディエンス：制限なし</li><li>メッセージクリックオーディエンス：最小50件</li><li>メッセージインプレッションオーディエンス：最小50件</li></ul> |
| メッセージを配信してからリターゲティング用オーディエンス[^retargeting-audiences]を作成できる期間  |  最大60日間（5,184,000秒間） |

[^retargeting-audiences]: メッセージクリックオーディエンスおよびメッセージインプレッションオーディエンスを指します。

ナローキャストメッセージの使用制限について詳しくは、『Messaging APIリファレンス』の「[属性情報やオーディエンスを利用したメッセージ送信の制限事項](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message-restrictions)」を参照してください。
