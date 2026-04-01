# リッチメニューでタブ切り替えを行う

ユーザー単位のリッチメニューを活用して、タブ切り替えが可能なリッチメニューをユーザーに提供できます。[リッチメニューエイリアス](https://developers.line.biz/ja/glossary/#rich-menu-alias)と[リッチメニュー切替アクション](https://developers.line.biz/ja/reference/messaging-api/#richmenu-switch-action)を使うことで、タブ切り替えのように、複数のリッチメニューを簡単に切り替えられます。

![](https://developers.line.biz/media/messaging-api/rich-menu/switching-richmenu-ja.png)

たとえばリッチメニューAとリッチメニューBを切り替えたい場合、以下の手順に従って設定します。

1. [リッチメニューの画像を準備する](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/#richmenu-switch-01)
1. [リッチメニューAを作成する](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/#richmenu-switch-02)
1. [リッチメニューAに画像をアップロードする](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/#richmenu-switch-03)
1. [リッチメニューBを作成する](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/#richmenu-switch-04)
1. [リッチメニューBに画像をアップロードする](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/#richmenu-switch-05)
1. [リッチメニューAをデフォルトにする](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/#richmenu-switch-06)
1. [リッチメニューエイリアスAを作成する](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/#richmenu-switch-07)
1. [リッチメニューエイリアスBを作成する](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/#richmenu-switch-08)
1. [リッチメニューの表示を終了する](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/#richmenu-switch-09)

## 1. リッチメニューの画像を準備する 

事前にリッチメニューAの画像（`richmenu-a.png`）と、リッチメニューBの画像（`richmenu-b.png`）を準備しておきます。使用できる画像について詳しくは、『Messaging APIリファレンス』の「[リッチメニューの画像の要件](https://developers.line.biz/ja/reference/messaging-api/#upload-rich-menu-image-requirements)」を参照してください。

| リッチメニューAの画像 | リッチメニューBの画像 |
| :-: | :-: |
| ![リッチメニューAの画像](https://developers.line.biz/media/messaging-api/rich-menu/richmenu-a.png) | ![リッチメニューBの画像](https://developers.line.biz/media/messaging-api/rich-menu/richmenu-b.png) |

## 2. リッチメニューAを作成する 

Messaging APIで[リッチメニューを作成](https://developers.line.biz/ja/reference/messaging-api/#create-rich-menu)します。この例では、タップ[領域オブジェクト](https://developers.line.biz/ja/reference/messaging-api/#area-object)のアクションに、以下を指定しています。

- **リッチメニューAの左側のタップ領域**
  - アクション：[URIアクション](https://developers.line.biz/ja/reference/messaging-api/#uri-action)
  - URI：[LINE Developersサイト](https://developers.line.biz/)
- **リッチメニューAの右側のタップ領域**
  - アクション：[リッチメニュー切替アクション](https://developers.line.biz/ja/reference/messaging-api/#richmenu-switch-action)（type：`richmenuswitch`）
  - 切替先：リッチメニューB（richMenuAliasId：`richmenu-alias-b`）

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
    "selected": false,
    "name": "richmenu-a",
    "chatBarText": "Tap to open",
    "areas": [
        {
            "bounds": {
                "x": 0,
                "y": 0,
                "width": 1250,
                "height": 1686
            },
            "action": {
                "type": "uri",
                "uri": "https://developers.line.biz/"
            }
        },
        {
            "bounds": {
                "x": 1251,
                "y": 0,
                "width": 1250,
                "height": 1686
            },
            "action": {
                "type": "richmenuswitch",
                "richMenuAliasId": "richmenu-alias-b",
                "data": "richmenu-changed-to-b"
            }
        }
    ]
}'
```

リッチメニューAが作成されると、レスポンスとしてリッチメニューのIDが返ります。

```json
{
  "richMenuId": "richmenu-19682466851b21e2d7c0ed482ee0930f"
}
```

## 3. リッチメニューAに画像をアップロードする 

リッチメニューを作成したら、Messaging APIでリッチメニューA用の「[画像をアップロード](https://developers.line.biz/ja/reference/messaging-api/#upload-rich-menu-image)」します。[手順2](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/#richmenu-switch-02)で取得したリッチメニューAのリッチメニューIDを、パスパラメータで指定します。

```sh
curl -v -X POST https://api-data.line.me/v2/bot/richmenu/richmenu-19682466851b21e2d7c0ed482ee0930f/content \
-H 'Authorization: Bearer {channel access token}' \
-H "Content-Type: image/png" \
-T richmenu-a.png
```

## 4. リッチメニューBを作成する 

リッチメニューAと同様の手順で、リッチメニューB（`richmenu-b`）を作成します。タップ[領域オブジェクト](https://developers.line.biz/ja/reference/messaging-api/#area-object)のアクションに、以下を指定します。

- **リッチメニューBの左側のタップ領域**
  - アクション：[リッチメニュー切替アクション](https://developers.line.biz/ja/reference/messaging-api/#richmenu-switch-action)（type：`richmenuswitch`）
  - 切替先：リッチメニューA（richMenuAliasId：`richmenu-alias-a`）
- **リッチメニューBの右側のタップ領域**
  - アクション：[URIアクション](https://developers.line.biz/ja/reference/messaging-api/#uri-action)
  - URI：[LINEヤフー Tech Blog](https://techblog.lycorp.co.jp/)

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
    "selected": false,
    "name": "richmenu-b",
    "chatBarText": "Tap to open",
    "areas": [
        {
            "bounds": {
                "x": 0,
                "y": 0,
                "width": 1250,
                "height": 1686
            },
            "action": {
                "type": "richmenuswitch",
                "richMenuAliasId": "richmenu-alias-a",
                "data": "richmenu-changed-to-a"
            }
        },
        {
            "bounds": {
                "x": 1251,
                "y": 0,
                "width": 1250,
                "height": 1686
            },
            "action": {
                "type": "uri",
                "uri": "https://techblog.lycorp.co.jp/"
            }
        }
    ]
}'
```

リッチメニューBが作成されると、レスポンスとしてリッチメニューのIDが返ります。

```json
{
  "richMenuId": "richmenu-4ecc8d672d9da4ba375fb82fa938fe5e"
}
```

## 5. リッチメニューBに画像をアップロードする 

リッチメニューBを作成したら、Messaging APIでリッチメニューB用の「[画像をアップロード](https://developers.line.biz/ja/reference/messaging-api/#upload-rich-menu-image)」します。[手順4](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/#richmenu-switch-04)で取得したリッチメニューIDを、パスパラメータで指定します。

```sh
curl -v -X POST https://api-data.line.me/v2/bot/richmenu/richmenu-4ecc8d672d9da4ba375fb82fa938fe5e/content \
-H 'Authorization: Bearer {channel access token}' \
-H "Content-Type: image/png" \
-T richmenu-b.png
```

## 6. リッチメニューAをデフォルトにする 

「[デフォルトのリッチメニューを設定する](https://developers.line.biz/ja/reference/messaging-api/#set-default-rich-menu)」エンドポイントを使って、リッチメニューAをデフォルトのリッチメニューにします。

```sh
curl -v -X POST https://api.line.me/v2/bot/user/all/richmenu/richmenu-19682466851b21e2d7c0ed482ee0930f \
-H 'Authorization: Bearer {channel access token}'
```

これによりリッチメニューAが表示されるようになります。しかし、リッチメニューエイリアスBが未作成のため、右側をタップしてもまだリッチメニューBには切り替わりません。

![デフォルトのリッチメニューが表示された](https://developers.line.biz/media/messaging-api/rich-menu/set-default-rich-menu.png)

<!-- note start -->

**リッチメニューAが表示されない場合**

デフォルトのリッチメニューよりも表示優先順位の高い、ユーザー単位のリッチメニューが既に設定されていた場合、リッチメニューAは表示されません。その場合は、表示されている[リッチメニューを削除する](https://developers.line.biz/ja/reference/messaging-api/#delete-rich-menu)か、[リッチメニューとユーザーのリンクを解除する](https://developers.line.biz/ja/reference/messaging-api/#unlink-rich-menu-from-user)ことで、リッチメニューAが表示されるようになります。詳しくは、「[リッチメニューの表示優先度](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/#rich-menu-display)」を参照してください。

<!-- note end -->

## 7. リッチメニューエイリアスAを作成する 

リッチメニューAの[リッチメニューエイリアスを作成](https://developers.line.biz/ja/reference/messaging-api/#create-rich-menu-alias)します。以下の例では、[手順2](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/#richmenu-switch-02)で作成しておいたリッチメニューAに、リッチメニューエイリアス`richmenu-alias-a`を設定します。

```sh
curl -v -X POST https://api.line.me/v2/bot/richmenu/alias \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d \
'{
    "richMenuAliasId": "richmenu-alias-a",
    "richMenuId": "richmenu-19682466851b21e2d7c0ed482ee0930f"
}'
```

## 8. リッチメニューエイリアスBを作成する 

同様にリッチメニューBの[リッチメニューエイリアスを作成](https://developers.line.biz/ja/reference/messaging-api/#create-rich-menu-alias)します。以下の例では、[手順4](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/#richmenu-switch-04)で作成しておいたリッチメニューBに、リッチメニューエイリアス`richmenu-alias-b`を設定します。

```sh
curl -v -X POST https://api.line.me/v2/bot/richmenu/alias \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d \
'{
    "richMenuAliasId": "richmenu-alias-b",
    "richMenuId": "richmenu-4ecc8d672d9da4ba375fb82fa938fe5e"
}'
```

これで、リッチメニューAで右側の領域をタップするとリッチメニューBに切り替わるようになりました。リッチメニューBで左側の領域をタップすると、リッチメニューAに戻ります。

| リッチメニューA | リッチメニューB |
| :-: | :-: |
| ![リッチメニューA](https://developers.line.biz/media/messaging-api/rich-menu/set-default-rich-menu.png) | ![リッチメニューB](https://developers.line.biz/media/messaging-api/rich-menu/switch-rich-menu.png) |

リッチメニューエイリアスと紐づくリッチメニューは、「[リッチメニューエイリアスを更新する](https://developers.line.biz/ja/reference/messaging-api/#update-rich-menu-alias)」エンドポイントを使って、いつでも変更できます。

## 9. リッチメニューの表示を終了する 

リッチメニューの表示を終了したい場合は、Messaging APIで以下の手順で実施します。

1. [デフォルトのリッチメニューを解除する](https://developers.line.biz/ja/reference/messaging-api/#clear-default-rich-menu)
1. [リッチメニューエイリアスを削除する](https://developers.line.biz/ja/reference/messaging-api/#delete-rich-menu-alias)
1. [リッチメニューを削除する](https://developers.line.biz/ja/reference/messaging-api/#delete-rich-menu)

なお、[ユーザーとのリンクを解除](https://developers.line.biz/ja/reference/messaging-api/#unlink-rich-menu-from-user)せずにリッチメニューを削除できます。しかしこの場合、リッチメニューは即時には削除されず、ユーザーがトーク画面に再入室したときに削除が反映されます。

LINE公式アカウントと友だちになっているユーザーの、ユーザーIDが分かっている場合は、リッチメニューを削除する代わりに、リッチメニューのリンクを解除できます。リッチメニューを保持した状態でリッチメニューとユーザーのリンクを解除するには、以下の手順に従って設定します。

- [リッチメニューとユーザーのリンクを解除する](https://developers.line.biz/ja/reference/messaging-api/#unlink-rich-menu-from-user)
- [複数のユーザーのリッチメニューのリンクを解除する](https://developers.line.biz/ja/reference/messaging-api/#unlink-rich-menu-from-users)

リッチメニューとユーザーのリンクを解除した場合、リッチメニューは即時に表示されなくなります。

## 意図したリッチメニューが表示されないときは 

意図したリッチメニューが表示されない場合は、以下の点を確認してください。

- [デフォルトのリッチメニューを解除してもリッチメニューが表示され続けてしまう](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/#youll-still-see-the-rich-menu-after-you-clear-the-default)
- [新しいデフォルトのリッチメニューを設定したのに他のリッチメニューが表示されてしまう](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/#you-see-a-different-rich-menu)

### デフォルトのリッチメニューを解除してもリッチメニューが表示され続けてしまう 

リッチメニュー切替アクションでリッチメニューAからリッチメニューBに、またはリッチメニューBからリッチメニューAに切り替わった場合、表示されるリッチメニューは、表示優先順位が最も高いユーザー単位のリッチメニューです。そのため、[手順6](https://developers.line.biz/ja/docs/messaging-api/switch-rich-menus/#richmenu-switch-06)で設定したデフォルトのリッチメニューを解除しただけでは、リッチメニューAもしくはリッチメニューBは引き続き表示されたままとなります。

その場合は、[リッチメニューを削除する](https://developers.line.biz/ja/reference/messaging-api/#delete-rich-menu)か、[リッチメニューとユーザーのリンクを解除する](https://developers.line.biz/ja/reference/messaging-api/#unlink-rich-menu-from-user)ことで、リッチメニューの表示を終了できます。リッチメニューの表示優先順位について詳しくは、「[リッチメニューの表示優先度](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/#rich-menu-display)」を参照してください。

### 新しいデフォルトのリッチメニューを設定したのに他のリッチメニューが表示されてしまう 

新しいデフォルトのリッチメニューを設定したのに他のリッチメニューが表示されてしまう場合は、デフォルトのリッチメニューよりも表示優先順位の高い、ユーザー単位のリッチメニューが設定されている可能性があります。

その場合は、意図せず表示されている[リッチメニューを削除する](https://developers.line.biz/ja/reference/messaging-api/#delete-rich-menu)か、[リッチメニューとユーザーのリンクを解除する](https://developers.line.biz/ja/reference/messaging-api/#unlink-rich-menu-from-user)ことで、新しいリッチメニューが表示されるようになります。詳しくは、「[リッチメニューの表示優先度](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/#rich-menu-display)」を参照してください。
