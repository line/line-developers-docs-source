# リッチメニューの概要

このページでは、LINE公式アカウントのトーク画面で表示される、リッチメニューについて説明します。

## リッチメニューとは 

リッチメニューはLINE公式アカウントのトーク画面下部に表示されるメニュー機能です。リッチメニューに、LINE公式アカウントの各機能や、外部サイトや予約ページなどへのリンクを設定することで、よりリッチなユーザー体験を提供できます。[リッチメニューの構造](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/#rich-menu-structure)に基づいて、[リッチメニューを作成するツール](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/#choosing-tool-for-creating-rich-menus)を使ってみましょう。

<!-- note start -->

**リッチメニューはデスクトップ版では表示されません**

リッチメニューは、デスクトップ版（macOS、Windows）のLINEでは表示されません。

<!-- note end -->

## リッチメニューの構造 

リッチメニューは、リッチメニュー画像、タップ領域、およびトークルームメニューで構成されます。

![](https://developers.line.biz/media/messaging-api/rich-menu/bot-demo-rich-menu-image.png)

1. リッチメニュー画像：メニューの項目を含む1枚の画像（JPEGまたはPNG）ファイルです。画像の要件について詳しくは、『Messaging APIリファレンス』の「[リッチメニューの画像の要件](https://developers.line.biz/ja/reference/messaging-api/#upload-rich-menu-image-requirements)」を参照してください。
1. タップ領域：メニューの項目として分割した領域。ポストバックイベントを返したり、URLを開いたりするさまざまなアクションを各項目に設定します。
1. トークルームメニュー：リッチメニューの開閉に使うメニューです。トークルームメニューのテキストは、カスタマイズできます。

## リッチメニューを設定するツール 

リッチメニューの設定には、[LINE Official Account Manager](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/#creating-a-rich-menu-with-the-line-manager) 、または[Messaging API](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/#creating-a-rich-menu-using-the-messaging-api)を使用します。ニーズに合わせてツールを選びましょう。

<!-- note start -->

**1つのリッチメニューに使用できるのは1つのツールのみ**

1つのリッチメニューの取得や編集に、2つのツールを使うことはできません。LINE Official Account Managerで作成したリッチメニューは、LINE Official Account Managerでのみ取得と編集ができます。また、Messaging APIで作成したリッチメニューについては、LINE Official Account Managerは使用できません。

<!-- note end -->

| ツール | 利点 |
| --- | --- |
| [LINE Official Account Manager](https://manager.line.biz/) | <ul><li>開発期間が短く済みます</li><li>操作が簡単なGUIで開発できます</li><li>表示期間を設定できます</li><li>表示された回数やクリック率などの統計情報が確認できます</li></ul><p>詳しくは、『LINEヤフー for Business』の「[リッチメニューの活用方法](https://www.lycbiz.com/jp/column/line-official-account/technique/20180731-01/)」および「[分析 - リッチメニュー](https://www.lycbiz.com/jp/manual/OfficialAccountManager/insight_rich-menus/)」を参照してください。</p> |
| Messaging API | <ul><li>高度なカスタマイズが可能です</li><li>[ポストバックアクション](https://developers.line.biz/ja/reference/messaging-api/#postback-action)や[日時選択アクション](https://developers.line.biz/ja/reference/messaging-api/#datetime-picker-action)などの[アクションオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#action-objects)を利用できます</li><li>[リッチメニューでタブ切り替えを行う](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/)ことができます</li></ul><p>リッチメニューの機能を実際に使って試したい場合は、「[リッチメニューを試す](https://developers.line.biz/ja/docs/messaging-api/try-rich-menu/)」を参照してください。</p> |

なおMessaging APIで設定したリッチメニューについては、表示された回数やクリック率などの統計情報は取得できません。

### LINE Official Account Managerでリッチメニューを設定する 

LINE Official Account Managerではデフォルトのリッチメニューを設定できます。より[優先順位](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/#rich-menu-display)の高いリッチメニューが既に設定されていなければ、ユーザーにはデフォルトのリッチメニューが表示されます。

LINE Official Account Managerを使うと、あらかじめタップ領域が定義されたテンプレートをもとに、GUIを使ってタップ領域を設定できます。詳しくは、[LINE Official Account Managerのマニュアル](https://www.lycbiz.com/jp/manual/OfficialAccountManager/rich-menus/)を参照してください。

### Messaging APIでリッチメニューを設定する 

Messaging APIでリッチメニューを設定する場合は、必要となるエンドポイントを順番に呼び出す必要があります。基本的には以下の手順で行います。

1. リッチメニューの画像を準備する。
1. [リッチメニューを作成する](https://developers.line.biz/ja/reference/messaging-api/#create-rich-menu)エンドポイントを使用する。
1. [リッチメニューの画像をアップロードする](https://developers.line.biz/ja/reference/messaging-api/#upload-rich-menu-image)エンドポイントを使用する。
1. [デフォルトのリッチメニューを設定する](https://developers.line.biz/ja/reference/messaging-api/#set-default-rich-menu)エンドポイントを使用する。

Messaging APIでリッチメニューを設定する方法について詳しくは、「[リッチメニューを使う](https://developers.line.biz/ja/docs/messaging-api/using-rich-menus/)」を参照してください。

## リッチメニューの適用範囲 

リッチメニューには、2つの適用範囲があり、それぞれで設定できるツールが異なります。

| 適用範囲 | 設定できるツール |
| --- | --- |
| LINE公式アカウントとのトーク画面を開いたすべてのユーザー（デフォルトのリッチメニュー） | <ul><li>LINE Official Account Manager</li><li>Messaging API</li></ul> |
| ユーザー単位（ユーザー単位のリッチメニュー） | Messaging API |

適用範囲と設定したツールによって、リッチメニューの表示優先度や、ユーザーのトーク画面に反映されるタイミングが異なります。

- [リッチメニューの表示優先度](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/#rich-menu-display)
- [リッチメニューの設定変更が反映されるタイミング](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/#when-setting-change-takes-effect)

### リッチメニューの表示優先度 

リッチメニューは、設定したツールと適用範囲によって表示優先度が異なります。リッチメニューの表示優先順位（1が最優先で表示）は以下のとおりです。

1. Messaging APIで設定するユーザー単位のリッチメニュー
1. Messaging APIで設定するデフォルトのリッチメニュー
1. [LINE Official Account Manager](https://manager.line.biz)で設定するデフォルトのリッチメニュー

### リッチメニューの設定変更が反映されるタイミング 

リッチメニューの設定を変更したとき、リッチメニューの適用範囲と設定したツールによって、ユーザーのトーク画面に反映されるタイミングが異なります。

| 適用範囲と設定したツール | 反映されるタイミング |
| --- | --- |
| Messaging APIで設定するユーザー単位のリッチメニュー | 即時。ただし、[ユーザーとのリンクを解除](https://developers.line.biz/ja/reference/messaging-api/#unlink-rich-menu-from-user)せずにリッチメニューを削除した場合は、トーク画面に再入室したときに削除が反映されます。 |
| Messaging APIで設定するデフォルトのリッチメニュー | トーク画面に再入室したとき。変更が反映されるまで、1分程度掛かる場合があります。 |
| LINE Official Account Managerで設定するデフォルトのリッチメニュー | トーク画面に再入室したとき。 |

### LINE公式アカウントと友だちではないユーザーがトーク画面を開いた場合 

LINE公式アカウントと友だちではないユーザーがトーク画面を開いた場合、LINE Official Account Managerもしくは、Messaging APIで設定したデフォルトのリッチメニューが表示されます。

なお、LINE公式アカウントと友だちではないユーザーに対して、ユーザー単位のリッチメニューはリンクできません。詳しくは、『Messaging APIリファレンス』の「[リッチメニューをリンクできる条件](https://developers.line.biz/ja/reference/messaging-api/#link-rich-menu-to-user-conditions)」を参照してください。

## リッチメニューのAPIリファレンス 

- [リッチメニュー](https://developers.line.biz/ja/reference/messaging-api/#rich-menu)
- [ユーザー単位のリッチメニュー](https://developers.line.biz/ja/reference/messaging-api/#per-user-rich-menu)
- [リッチメニューエイリアス](https://developers.line.biz/ja/reference/messaging-api/#rich-menu-alias)
