# リッチメニューの表示を終了する

展開中のキャンペーンが終了するときや、季節商品の取り扱いが終わるときなど、現在のリッチメニューの表示を終了したい場合があります。リッチメニューはその種類や解除方法によって、解除の対象や反映されるタイミングが異なります。そのため、終了の操作後もそのリッチメニューが意図せず表示され続けてしまうことがあります。

このページでは、リッチメニューの表示を終了する方法と、その注意点について説明します。

<!-- table of contents -->

## デフォルトのリッチメニューの表示を終了する 

すべてのユーザーに表示されるデフォルトのリッチメニューの表示を終了するには、リッチメニューを設定した方法にあわせて解除します。

- [Messaging APIで設定した場合](https://developers.line.biz/ja/docs/messaging-api/stop-displaying-rich-menu/#stop-displaying-default-rich-menu-messaging-api)
- [LINE Official Account Managerで設定した場合](https://developers.line.biz/ja/docs/messaging-api/stop-displaying-rich-menu/#stop-displaying-default-rich-menu-oa)

ただし、デフォルトのリッチメニューを解除しても、ユーザー単位のリッチメニューがリンクされているユーザーには、引き続きユーザー単位のリッチメニューが表示されます。

### Messaging APIで設定した場合 

リッチメニューをMessaging APIで設定した場合は、[デフォルトのリッチメニューを解除する](https://developers.line.biz/ja/reference/messaging-api/#clear-default-rich-menu)エンドポイントを使用します。

リッチメニューを解除しても、ユーザーがトーク画面に再入室するまではユーザーのリッチメニューには反映されません。また、変更が適用されるまで1分ほどかかる場合があります。

### LINE Official Account Managerで設定した場合 

リッチメニューを[LINE Official Account Manager](https://manager.line.biz/)で設定した場合は、LINE Official Account Managerから設定を変更または削除してください。Messaging APIからは、LINE Official Account Managerで設定したリッチメニューの表示を終了することはできません。

## ユーザー単位のリッチメニューの表示を終了する 

ユーザー単位のリッチメニューの表示を終了するには、ユーザーとリッチメニューのリンクを解除します。対象となるユーザーの範囲にあわせて、以下のいずれかのエンドポイントを使用します。

| 対象 | 使用するエンドポイント | 解除のタイミング |
| --- | --- | --- |
| 単一のユーザー | [リッチメニューとユーザーのリンクを解除する](https://developers.line.biz/ja/reference/messaging-api/#unlink-rich-menu-from-user) | 即時 |
| 複数のユーザー | [複数のユーザーのリッチメニューのリンクを解除する](https://developers.line.biz/ja/reference/messaging-api/#unlink-rich-menu-from-users)など | 非同期 |
| 特定のリッチメニューにリンクしているすべてのユーザー | [リンク済みのリッチメニューを一括で置き換え・解除する](https://developers.line.biz/ja/reference/messaging-api/#batch-control-rich-menus-of-users) | 非同期 |

ただし、ユーザー単位のリッチメニューのリンクを解除しても、デフォルトのリッチメニューがリンクされているユーザーには、引き続きデフォルトのリッチメニューが表示されます。

## タブ切り替え（リッチメニューエイリアス）を利用している場合 

リッチメニューエイリアスを利用してタブの切り替えを行っている場合、ユーザーとリッチメニューのリンクを解除している最中に、ユーザーがタブをタップして別のリッチメニューへ切り替える可能性があります。この場合、切り替え先のリッチメニューとのリンクが解除されずに残ってしまうことがあります。

![](https://developers.line.biz/media/messaging-api/rich-menu/stop-displaying-rich-menu-tab-switching.webp)

リッチメニューを完全に非表示にするためには、以下の手順で表示を終了することを推奨します。

1. [リッチメニューエイリアスを削除する](https://developers.line.biz/ja/reference/messaging-api/#delete-rich-menu-alias)エンドポイントを使用して、ユーザーが別のタブへ切り替えられないようにする。
1. [リンク済みのリッチメニューを一括で置き換え・解除する](https://developers.line.biz/ja/reference/messaging-api/#batch-control-rich-menus-of-users)エンドポイントなどを使用して、対象のリッチメニューとユーザーとのリンクを解除する。
1. タブ切り替えにより解除されず残ってしまったリンクを解除するために、時間をおいてリンクの解除を再実行する。

なお、手順1で削除したリッチメニューエイリアスを使用しているリッチメニューでは、リンクの解除が完了するまではタブの切り替えができなくなるため、一時的にユーザー体験が低下する可能性があります。

## 不要になったリッチメニューを削除する 

ユーザーへのリッチメニューの表示が完全に終了し、ユーザーのトーク画面に表示されなくなったことを確認したら、不要になったリッチメニューを[リッチメニューを削除する](https://developers.line.biz/ja/reference/messaging-api/#delete-rich-menu)エンドポイントで削除することを推奨します。

Messaging APIで作成できるリッチメニューの数には上限（LINE公式アカウントあたり1,000件）があるため、不要なリッチメニューを削除することで、上限を圧迫することなく運用できます。

なお、[ユーザーとのリンクを解除](https://developers.line.biz/ja/docs/messaging-api/stop-displaying-rich-menu/#stop-displaying-per-user-rich-menu)せずにリッチメニューだけを削除しても、ユーザーのトーク画面からはすぐには消えません。ユーザーがトーク画面に再入室するまでは、削除したリッチメニューが表示され続けます。もし、ユーザーがトーク画面にいる状態でもすぐに非表示にしたい場合は、リッチメニューを削除するのではなく、まずはリンクの解除を行ってください。

また、[リッチメニューを削除した後もリッチメニューの統計情報を取得](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/#rich-menu-insight-after-deletion)できますが、Messaging API経由で[リッチメニューIDを取得](https://developers.line.biz/ja/reference/messaging-api/#get-rich-menu-list)することはできなくなります。リッチメニューを削除した後も統計情報を取得する可能性がある場合は、削除前に必ずリッチメニューIDを保管しておいてください。
