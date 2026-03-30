# ユーザー単位のリッチメニューを使う

このページでは、「ユーザー単位のリッチメニュー」の設定方法について説明します。

<!-- table of contents -->

## ユーザー単位のリッチメニューとは 

Messaging APIでは、リッチメニューをユーザー単位で設定できます。そのため、複数のリッチメニューを用意し、ユーザーごとに異なるリッチメニューを設定することで、ユーザー体験を向上させることもできます。

ユーザー単位のリッチメニューには、以下のような特徴があります。

1. 表示優先度がデフォルトのリッチメニューよりも高い
   - ユーザー単位のリッチメニューは、表示優先度がデフォルトのリッチメニューよりも高く設定されています。そのため、LINE公式アカウントにデフォルトのリッチメニューを設定している場合に、あるユーザーに対して、ユーザー単位のリッチメニューを設定したときには、ユーザー単位のリッチメニューが優先して表示されます。詳しくは、「[リッチメニューの表示優先度](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/#rich-menu-display)」を参照してください。
1. 即時に設定が反映され表示が切り替わる
   - ユーザー単位のリッチメニューは、ユーザーがトーク画面に再入室しなくても、即時に設定が反映され表示が切り替わります。詳しくは、「[リッチメニューの設定変更が反映されるタイミング](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/#when-setting-change-takes-effect)」を参照してください。

## ユーザー単位のリッチメニューを設定する 

ユーザー単位のリッチメニューの基本的な設定手順は以下のとおりです。

1. [リッチメニューを作成し、画像を添付する](https://developers.line.biz/ja/docs/messaging-api/use-per-user-rich-menus/#create-a-rich-menu)
1. [ユーザーIDを準備する](https://developers.line.biz/ja/docs/messaging-api/use-per-user-rich-menus/#prepare-user-id)
1. [リッチメニューとユーザーをリンクする](https://developers.line.biz/ja/docs/messaging-api/use-per-user-rich-menus/#link-the-rich-menu-to-user)
1. [リッチメニューとユーザーのリンクを解除](https://developers.line.biz/ja/docs/messaging-api/use-per-user-rich-menus/#unlink-the-rich-menu-from-user)して、ユーザー単位のリッチメニューの表示を終了する（任意）

### 1. リッチメニューを作成し、画像を添付する 

まずはリッチメニューを作成します。リッチメニューの作成方法について詳しくは、「[リッチメニューを使う](https://developers.line.biz/ja/docs/messaging-api/using-rich-menus/)」を参照してください。

ここでは、以下のリッチメニュー用のテンプレート画像（`richmenu-template-guide-07.png`）を使用します。任意のディレクトリに保存してください。

![このガイドで使用するリッチメニュー用のテンプレート画像](https://developers.line.biz/media/messaging-api/rich-menu/richmenu-template-guide-07.png)

以下のコマンドをターミナルで実行して、[リッチメニューを作成](https://developers.line.biz/ja/reference/messaging-api/#create-rich-menu)してください。

```sh
curl -v -X POST https://api.line.me/v2/bot/richmenu \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d \
'{
    "size": {
        "width": 2500,
        "height": 1686
    },
    "selected": true,
    "name": "ユーザー単位のリッチメニューのテスト",
    "chatBarText": "Tap to open",
    "areas": [
        {
            "bounds": {
                "x": 0,
                "y": 0,
                "width": 2500,
                "height": 1686
            },
            "action": {
                "type": "uri",
                "label": "タップ領域A",
                "uri": "https://developers.line.biz/ja/news/"
            }
        }
    ]
}'
```

次に、以下のコマンドをターミナルで実行して、[リッチメニューに画像をアップロードして添付](https://developers.line.biz/ja/reference/messaging-api/#upload-rich-menu-image)してください。

```sh
curl -v -X POST https://api-data.line.me/v2/bot/richmenu/{richMenuId}/content \
-H "Authorization: Bearer {channel access token}" \
-H "Content-Type: image/png" \
-T richmenu-template-guide-07.png
```

### 2. ユーザーIDを準備する 

リッチメニューを表示するユーザーのユーザーIDを準備します。ここでは、実際に表示を確認するために自分のユーザーIDを用意してください。

ユーザーIDの例：`U8189cf6745fc0d808977bdb0b9f22995`

ユーザーIDの取得について詳しくは、「[ユーザーIDを取得する](https://developers.line.biz/ja/docs/messaging-api/getting-user-ids/)」の「[開発者が自分自身のユーザーIDを取得する](https://developers.line.biz/ja/docs/messaging-api/getting-user-ids/#get-own-user-id)」を参照してください。

### 3. リッチメニューとユーザーをリンクする 

リッチメニューとユーザーIDが用意できたら、[ユーザーとリッチメニューをリンク](https://developers.line.biz/ja/reference/messaging-api/#link-rich-menu-to-user)します。以下のコマンドをターミナルで実行してください。

```sh
curl -v -X POST https://api.line.me/v2/bot/user/{userId}/richmenu/{richMenuId} \
-H "Authorization: Bearer {channel access token}"
```

#### 3-1. リッチメニューの表示を確認する 

手順3.で設定したユーザー単位のリッチメニューが表示されることを確認します。リッチメニューを設定したLINE公式アカウントのトーク画面を開きます。

![](https://developers.line.biz/media/messaging-api/rich-menu/per-user-rich-menu-example.png)

### 4. リッチメニューとユーザーのリンクを解除する 

最後に[リッチメニューとユーザーのリンクを解除](https://developers.line.biz/ja/reference/messaging-api/#unlink-rich-menu-from-user)し、リッチメニューの表示を終了します。手順4.で開いたトーク画面を表示したまま、以下のコマンドをターミナルで実行してください。

```sh
curl -v -X DELETE https://api.line.me/v2/bot/user/{userId}/richmenu \
-H 'Authorization: Bearer {channel access token}'
```

ユーザー単位のリッチメニューは設定が即時に反映されるため、実行が完了したタイミングで、ユーザー単位のリッチメニューの表示が終了します。

なお、デフォルトのリッチメニューが設定されている場合は、デフォルトのリッチメニューが代わりに表示されます。

## ユーザーがリッチメニューを切り替えられるようにする 

ユーザー単位のリッチメニューを活用して、タブ切り替えが可能なリッチメニューをユーザーに提供できます。[リッチメニューエイリアス](https://developers.line.biz/ja/glossary/#rich-menu-alias)と[リッチメニュー切替アクション](https://developers.line.biz/ja/reference/messaging-api/#richmenu-switch-action)を使うことで、簡単にリッチメニューの切り替えを実装できます。

![](https://developers.line.biz/media/messaging-api/rich-menu/switching-richmenu-ja.png)

詳しくは、「[リッチメニューでタブ切り替えを行う](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/)」を参照してください。
