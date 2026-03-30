# インプレッションを計測する

Messaging APIの統計情報には、ユーザーのさまざまな操作についての情報が含まれます。このページではその中からインプレッションについて解説します。

- [集計の対象となる環境](https://developers.line.biz/ja/docs/messaging-api/measure-impressions/#environment-for-aggregation)
- [統計情報を取得するエンドポイント](https://developers.line.biz/ja/docs/messaging-api/measure-impressions/#endpoints-for-statistics)
- [インプレッションとは](https://developers.line.biz/ja/docs/messaging-api/measure-impressions/#what-is-impression)
- [インプレッションの計測ロジック](https://developers.line.biz/ja/docs/messaging-api/measure-impressions/#impression-logic)
- [利用上の注意点](https://developers.line.biz/ja/docs/messaging-api/measure-impressions/#precautions)

## 集計の対象となる環境 

インプレッションを含む統計情報は、iOS版およびAndroid版のLINEアプリを対象に集計されます。

PC版LINEやChrome版LINEでメッセージを確認しても、統計情報に集計されません。

## 統計情報を取得するエンドポイント 

送信したメッセージに対してユーザーがどのように操作したかについて、以下のエンドポイントで統計情報を取得できます。

- [ユーザーの操作に基づく統計情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-message-event)
- [ユニットごとの統計情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-statistics-per-unit)

## インプレッションとは 

Messaging APIにおけるインプレッションとは、LINE公式アカウントから送信されたメッセージを、ユーザーがトークルームに入室して確認したことを指します。インプレッションは、メッセージの開封と表現される場合もあります。

### インプレッションの種類 

インプレッションには、ユニークインプレッションとインプレッションの2種類があります。本ドキュメントで説明する[インプレッションの計測ロジック](https://developers.line.biz/ja/docs/messaging-api/measure-impressions/#impression-logic)は、どちらにも共通して適用されます。ただし、計測される回数には違いがあるので、注意が必要です。

[統計情報を取得するエンドポイント](https://developers.line.biz/ja/docs/messaging-api/measure-impressions/#endpoints-for-statistics)で取得できるインプレッションは以下のとおりです。

| プロパティ | インプレッションの種類 | 説明 |
| --- | --- | --- |
| `overview.uniqueImpression` ※1 | ユニークインプレッション | メッセージを開封した人数。少なくとも1つの吹き出しを表示した人数です。<br>1つのメッセージにつき、1ユーザーあたり1回のみ計測されます。 |
| `messages[].uniqueImpression` ※2 | ユニークインプレッション | 吹き出しを表示した人数。<br>1つの吹き出しにつき、1ユーザーあたり1回のみ計測されます。 |
| `messages[].impression` ※1 | インプレッション | 吹き出しが表示された回数。<br>条件を満たしていれば、1つの吹き出しにつき、1ユーザーあたり複数回計測されることがあります。 |

※1 [ユーザーの操作に基づく統計情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-message-event)および[ユニットごとの統計情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-statistics-per-unit)エンドポイントのレスポンスにおいて、インプレッションの値が含まれるプロパティ

※2 [ユニットごとの統計情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-statistics-per-unit)エンドポイントのレスポンスにおいて、インプレッションの値が含まれるプロパティ

#### メッセージと吹き出しの概念 

[メッセージ](https://developers.line.biz/ja/docs/messaging-api/sending-messages/)は、1つまたは複数の[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)で構成されます。メッセージオブジェクトは、1回のリクエストで最大5つまで送信できます。

Messaging APIにおける吹き出しとは、1つのメッセージオブジェクトを指します。メッセージオブジェクトにはスタンプメッセージオブジェクトや画像メッセージオブジェクトなども含まれ、見た目が吹き出しの形状をしているかどうかは関係ありません。

下の図は3つの吹き出しで構成されるメッセージの例です。吹き出し2と3は、吹き出し1のテキストメッセージオブジェクトのような吹き出しの形状をしていませんが、それぞれ吹き出しとしてインプレッションの計測に利用されます。

![](https://developers.line.biz/media/messaging-api/measure-impressions/message-and-bubbles-ja.png)

このメッセージを送信した場合、ユーザーがトークルームに入室してメッセージを確認すると、1つの吹き出しが表示された段階で`overview.uniqueImpression`が計測されます。`messages[].uniqueImpression`と`messages[].impression`は、吹き出しごとに個別で計測されます。

詳しくは、『Messaging APIリファレンス』の「[ユーザーの操作に基づく統計情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-message-event)」および「[ユニットごとの統計情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-statistics-per-unit)」を参照してください。

### インプレッションとして計測されない操作 

インプレッションとして計測されるのは、LINE公式アカウントから送信されたメッセージを、ユーザーがトークルームに入室して確認した場合のみです。

一方で、以下のような操作を行い、トークルームに入室せずにメッセージを既読にした場合は、インプレッションには計測されません。

| OS | 操作 |
| --- | --- |
| Android | <ul><li>トークリストで既読にしたいトークルームを長押しし、表示されるメニューから［<b>既読にする</b>］を選択して一括で既読にする。</li><li>トークリスト上部のオプションメニューから［<b>すべて既読にする</b>］を選択して一括で既読にする。</li></ul> |
| iOS | <ul><li>トークリストで既読にしたいトークルームを左スワイプし、表示されるメニューから［<b>既読</b>］を選択して一括で既読にする。</li><li>トークリスト上部のハンバーガーメニューからトークリスト編集画面を開き、トークルームを選択して［<b>既読</b>］を押し、一括で既読にする。</li></ul> |

## インプレッションの計測ロジック 

このセクションでは、インプレッションの具体的な計測ロジックについて説明します。

- [メッセージの吹き出しを100％表示する](https://developers.line.biz/ja/docs/messaging-api/measure-impressions/#must-show-all-messages)
- [スクロールによる重複計測は行われない](https://developers.line.biz/ja/docs/messaging-api/measure-impressions/#no-duplicate-by-scrolling)
- [カルーセルを使用したメッセージについて](https://developers.line.biz/ja/docs/messaging-api/measure-impressions/#carousel-message)

### メッセージの吹き出しを100％表示する 

インプレッションは、LINE公式アカウントから送信されたメッセージを、ユーザーがトークルームに入室して確認した場合に計測されます。その際、メッセージの吹き出しが100％表示される必要があります。

以下に、吹き出しが100％表示されている例と、そうでない例を示します。

| 説明 | 画像 |
| --- | --- |
| このエリアの吹き出しは、100％表示されていることを示します。 | ![green](https://developers.line.biz/media/messaging-api/measure-impressions/100per-area.png) |
| このエリアの吹き出しは、100％は表示されていないことを示します。 | ![red](https://developers.line.biz/media/messaging-api/measure-impressions/not-100per-area.png) |

| 表示 | 説明 | 画像 |
| --- | --- | --- |
| ✅️ 100％表示されている | 緑色の部分に表示されている吹き出しは、100％表示されているため、インプレッションとして計測されます。 | ![吹き出し全体が表示されている](https://developers.line.biz/media/messaging-api/measure-impressions/impression-100per.png) |
| ❌️ 100％表示されていない | 赤色の部分に表示されている吹き出しは、リッチメニューと重なり、100％表示されていないため、インプレッションとして計測されません。 | ![リッチメニューと重なったため吹き出し全体が表示されていない](https://developers.line.biz/media/messaging-api/measure-impressions/impression-not-100per-richmenu.png) |
| ❌️ 100％表示されていない | 赤色の部分に表示されている吹き出しは、[サービスメニューバー](https://www.lycbiz.com/jp/manual/OfficialAccountManager/servicemenubar/)と重なり、100％表示されていないため、インプレッションとして計測されません。 | ![サービスメニューバーと重なったため吹き出し全体が表示されていない](https://developers.line.biz/media/messaging-api/measure-impressions/impression-not-100per-service-menu-ber.png) |
| ❌️ 100％表示されていない | 赤色の部分に表示されている吹き出しは、縦長であるためトーク画面に収まらず、100％表示されていないため、インプレッションとして計測されません。 | ![メッセージが縦長過ぎて吹き出し全体が表示されていない](https://developers.line.biz/media/messaging-api/measure-impressions/impression-not-100per-too-long.png) |

<!-- tip start -->

**吹き出し全体を一度に表示できない場合のインプレッション計測**

「100％表示される」とは、トークルームから退出するまでの間に、計測対象となる吹き出しの上端と下端の両方が、ユーザーのトークルーム内で表示されることを指します。

上記の例のように全体を一度に表示できない場合でも、ユーザーがスクロールしたり、リッチメニューを閉じたりなどして、隠れている吹き出しの上端と下端を表示すると100％表示されたとみなされ、インプレッションとして計測されます。

<!-- tip end -->

### スクロールによる重複計測は行われない 

一度インプレッションが計測されると、ユーザーがトークルームから退出するまでは、同じメッセージを再度スクロールして表示しても、複数回計測されることはありません。

ただし、ユーザーがいったんトークリストに戻り、再度トークルームに入室してメッセージを100％表示した場合は、新たにインプレッションとして計測されます。

なお、ユニークインプレッションは1ユーザーあたり1回のみ計測されるため、ユーザーがトークルームに再入室しても増加しません。

### カルーセルを使用したメッセージについて 

Flex Messageなどを利用し、[カルーセル](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/#carousel)を使用したメッセージを送信した場合、カルーセル部分を横にスクロールして表示しても、インプレッションが複数回計測されることはありません。

カルーセルを使用したメッセージでは、吹き出しの上端、下端、左端、右端のすべてが表示されると100％表示されたとみなされ、1回のインプレッションとして計測されます。

![](https://developers.line.biz/media/messaging-api/measure-impressions/carousel-100per-scroll.png)

## 利用上の注意点 

インプレッションの計測を行う際には、以下の点に注意してください。

- [計測期間内であることを確認する](https://developers.line.biz/ja/docs/messaging-api/measure-impressions/#ensure-measurement-period)
- [メッセージが縦長になりすぎないようにする](https://developers.line.biz/ja/docs/messaging-api/measure-impressions/#avoid-too-tall-messages)
- [リッチメニューやサービスメニューバーに干渉しないようにする](https://developers.line.biz/ja/docs/messaging-api/measure-impressions/#avoid-interference)

### 計測期間内であることを確認する 

インプレッションを含め、統計情報は、メッセージの送信時刻から14日間（1,209,600秒間）のみ集計されます。それ以降は更新されません。 [ユニットごとの統計情報を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-statistics-per-unit)エンドポイントを利用する場合は、集計対象期間を指定できるため、指定した日付が集計期間内であることを確認してください。

### メッセージが縦長になりすぎないようにする 

極端に縦長のメッセージを送信すると、トークルーム内でメッセージ全体が表示されず、期待どおりにインプレッションが計測されないことがあります。メッセージは適切な長さに調整してください。

### リッチメニューやサービスメニューバーに干渉しないようにする 

LINE公式アカウントに[リッチメニュー](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/)を設定していると、トークルーム内で吹き出しと重なって表示される場合があり、吹き出し全体が表示できなくなることがあります。その結果、期待どおりにインプレッションが計測されないことがあります。

また、トークルーム上部に表示される[サービスメニューバー](https://www.lycbiz.com/jp/manual/OfficialAccountManager/servicemenubar/)を使用している場合も、同様の干渉が発生する場合があります。

メッセージの長さやリッチメニューのサイズを調整し、干渉が起きないようにしてください。
