# Switch between tabs on rich menus

You can provide users with a rich menu with tab switching using per-user rich menus. To switch between rich menus with ease, like switching between tabs, use [rich menu aliases](https://developers.line.biz/en/glossary/#rich-menu-alias) and [rich menu switch action](https://developers.line.biz/en/reference/messaging-api/#richmenu-switch-action).

![](https://developers.line.biz/media/messaging-api/rich-menu/switching-richmenu-ja.png)

Here are the steps to set up two rich menus, rich menu A and rich menu B and enable switching between the two:

1. [Prepare rich menu images](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/#richmenu-switch-01)
1. [Create rich menu A](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/#richmenu-switch-02)
1. [Upload rich menu A image](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/#richmenu-switch-03)
1. [Create rich menu B](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/#richmenu-switch-04)
1. [Upload rich menu B image](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/#richmenu-switch-05)
1. [Set rich menu A as default](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/#richmenu-switch-06)
1. [Create rich menu alias A](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/#richmenu-switch-07)
1. [Create rich menu alias B](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/#richmenu-switch-08)
1. [Stop displaying rich menu](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/#richmenu-switch-09)

## 1. Prepare rich menu images 

Prepare an image for rich menu A (`richmenu-a.png`) and an image for rich menu B (`richmenu-b.png`). For more information on supported image specification, see [Requirements for rich menu image](https://developers.line.biz/en/reference/messaging-api/#upload-rich-menu-image-requirements) in the Messaging API reference.

| Image for rich menu A | Image for rich menu B |
| :-: | :-: |
| ![Rich menu A image](https://developers.line.biz/media/messaging-api/rich-menu/richmenu-a.png) | ![Rich menu B image](https://developers.line.biz/media/messaging-api/rich-menu/richmenu-b.png) |

## 2. Create rich menu A 

[Create a rich menu](https://developers.line.biz/en/reference/messaging-api/#create-rich-menu) with the Messaging API. For this example, specify actions for tappable areas in the [area object](https://developers.line.biz/en/reference/messaging-api/#area-object) as follows:

- **Rich menu A's tappable area on the left**
  - Action: [URI action](https://developers.line.biz/en/reference/messaging-api/#uri-action)
  - URI: [LINE Developers site](https://developers.line.biz/)
- **Rich menu A's tappable area on the right**
  - Action: [Rich menu switch action](https://developers.line.biz/en/reference/messaging-api/#richmenu-switch-action) (type: `richmenuswitch`)
  - Switching target: Rich menu B (richMenuAliasId: `richmenu-alias-b`).

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

When the rich menu A is created, the ID of the rich menu is returned as a response.

```json
{
  "richMenuId": "richmenu-19682466851b21e2d7c0ed482ee0930f"
}
```

## 3. Upload rich menu A image 

Now that we created rich menu A, [upload an image](https://developers.line.biz/en/reference/messaging-api/#upload-rich-menu-image) for rich menu A with the Messaging API. Specify the target menu as the path parameter with the rich menu ID we received from [step 2](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/#richmenu-switch-02).

```sh
curl -v -X POST https://api-data.line.me/v2/bot/richmenu/richmenu-19682466851b21e2d7c0ed482ee0930f/content \
-H 'Authorization: Bearer {channel access token}' \
-H "Content-Type: image/png" \
-T richmenu-a.png
```

## 4. Create rich menu B 

Create rich menu B (`richmenu-b`) in the same way as rich menu A. Specify actions for tappable areas in the [area object](https://developers.line.biz/en/reference/messaging-api/#area-object) as follows.

- **Rich menu B's tappable area on the left**
  - Action: [Rich menu switch action](https://developers.line.biz/en/reference/messaging-api/#richmenu-switch-action) (type: `richmenuswitch`)
  - Switching target: Rich menu A (richMenuAliasId: `richmenu-alias-a`)
- **Rich menu B's tappable area on the right**
  - Action: [URI action](https://developers.line.biz/en/reference/messaging-api/#uri-action)
  - URI: [LINE API Use Case](https://lineapiusecase.com/en/top.html)

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
                "uri": "https://lineapiusecase.com/en/top.html"
            }
        }
    ]
}'
```

When the rich menu B is created, the ID of the rich menu is returned as a response.

```json
{
  "richMenuId": "richmenu-4ecc8d672d9da4ba375fb82fa938fe5e"
}
```

## 5. Upload rich menu B image 

Now that we created rich menu B, [upload an image](https://developers.line.biz/en/reference/messaging-api/#upload-rich-menu-image) for rich menu B with the Messaging API. Specify the target menu as the path parameter with the rich menu ID we received in [step 4](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/#richmenu-switch-04).

```sh
curl -v -X POST https://api-data.line.me/v2/bot/richmenu/richmenu-4ecc8d672d9da4ba375fb82fa938fe5e/content \
-H 'Authorization: Bearer {channel access token}' \
-H "Content-Type: image/png" \
-T richmenu-b.png
```

## 6. Set rich menu A as default 

[Set the default rich menu](https://developers.line.biz/en/reference/messaging-api/#set-default-rich-menu) to the rich menu A.

```sh
curl -v -X POST https://api.line.me/v2/bot/user/all/richmenu/richmenu-19682466851b21e2d7c0ed482ee0930f \
-H 'Authorization: Bearer {channel access token}'
```

This makes the rich menu A displayed as the default. If you tap the right half of the rich menu A, the menu doesn't switch to the rich menu B. This is because we haven't created an alias for the rich menu B yet.

![Default rich menu displayed](https://developers.line.biz/media/messaging-api/rich-menu/set-default-rich-menu.png)

<!-- note start -->

**If rich menu A is not displayed**

If the user has a per-user rich menu set with a display priority higher than the default rich menu, the rich menu A isn't displayed. To make the rich menu A displayed, [delete](https://developers.line.biz/en/reference/messaging-api/#delete-rich-menu) the per-user rich menu or [unlink](https://developers.line.biz/en/reference/messaging-api/#unlink-rich-menu-from-user) the rich menu from the user. For more information, see [Display priority of rich menus](https://developers.line.biz/en/docs/messaging-api/rich-menus-overview/#rich-menu-display).

<!-- note end -->

## 7. Create rich menu alias A 

[Create an alias](https://developers.line.biz/en/reference/messaging-api/#create-rich-menu-alias) for the rich menu A. Here is an example request to set an alias `richmenu-alias-a` to the rich menu A that we created in [step 2](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/#richmenu-switch-02).

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

## 8. Create rich menu alias B 

[Create an alias](https://developers.line.biz/en/reference/messaging-api/#create-rich-menu-alias) for the rich menu B. Here is an example request to set the alias `richmenu-alias-b` to the rich menu B that we created in [step 4](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/#richmenu-switch-04).

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

Now, when you tap the right tappable area of the rich menu A, you can switch to the rich menu B. When you tap the left tappable area of the rich menu B, you can switch back to the rich menu A.

| Rich menu A | Rich menu B |
| :-: | :-: |
| ![Rich menu A](https://developers.line.biz/media/messaging-api/rich-menu/set-default-rich-menu.png) | ![Rich menu B](https://developers.line.biz/media/messaging-api/rich-menu/switch-rich-menu.png) |

You can [change the aliases](https://developers.line.biz/en/reference/messaging-api/#update-rich-menu-alias) at all times.

## 9. Stop displaying rich menu 

Suppose we want to stop displaying the rich menu. With the Messaging API, withdraw the rich menu in this order:

1. [Clear the default menu setting of the rich menu](https://developers.line.biz/en/reference/messaging-api/#clear-default-rich-menu).
1. [Delete the rich menu aliases](https://developers.line.biz/en/reference/messaging-api/#delete-rich-menu-alias).
1. [Delete the rich menu](https://developers.line.biz/en/reference/messaging-api/#delete-rich-menu).

You can delete a rich menu without [unlinking the rich menu from the user](https://developers.line.biz/en/reference/messaging-api/#unlink-rich-menu-from-user). But this removes the rich menu not immediately but the next time the user opens the chat.

You can unlink a rich menu from a user who is a friend of your LINE Official Account, if you know the user ID. To unlink a rich menu from a user but keep the rich menu:

- [Unlink rich menu from user](https://developers.line.biz/en/reference/messaging-api/#unlink-rich-menu-from-user)
- [Unlink rich menus from multiple users](https://developers.line.biz/en/reference/messaging-api/#unlink-rich-menu-from-users)

The moment you unlink a rich menu from a user, the rich menu disappears from the chat room right away.

## When the intended rich menu isn't displayed 

If the intended rich menu isn't displayed, check the following points:

- [You'll still see the rich menu after you clear the default](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/#youll-still-see-the-rich-menu-after-you-clear-the-default)
- [You set a new default rich menu but you see a different rich menu](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/#you-see-a-different-rich-menu)

### You'll still see the rich menu after you clear the default 

When you switch from rich menu A to B or from B to A, you'll see the per-user menu with the highest display priority. Therefore, clearing the default rich menu set in [step 6](https://developers.line.biz/en/docs/messaging-api/switch-rich-menus/#richmenu-switch-06) has no effect on what you see. You'll still see the rich menu A or B.

Now if you [delete a rich menu](https://developers.line.biz/en/reference/messaging-api/#delete-rich-menu) or [unlink a rich menu from a user](https://developers.line.biz/en/reference/messaging-api/#unlink-rich-menu-from-user), the rich menu is no longer displayed. For more information about the display priority of rich menus, see [Display priority of rich menus](https://developers.line.biz/en/docs/messaging-api/rich-menus-overview/#rich-menu-display).

### You set a new default rich menu but you see a different rich menu 

If you don't see the rich menu you set as a new default, the problem lies in the display priority. There is a possibility that a per-user rich menu with a higher display priority exists.

To make the new default visible, you can [delete](https://developers.line.biz/en/reference/messaging-api/#delete-rich-menu) the rich menu you see or [unlink rich menu from user](https://developers.line.biz/en/reference/messaging-api/#unlink-rich-menu-from-user). For more information, see [Display priority of rich menus](https://developers.line.biz/en/docs/messaging-api/rich-menus-overview/#rich-menu-display).
