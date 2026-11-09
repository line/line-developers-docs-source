# Stop displaying rich menus

There are times when you may want to stop displaying the current rich menu to users, such as when a campaign ends or when you stop offering seasonal products. Depending on the type of rich menu, the target of the unlink, the method of unlinking, the scope and timing of the change vary. As a result, the rich menu may unexpectedly remain visible even after you take steps to stop displaying it.

This page explains how to stop displaying rich menus and what to be aware of when doing so.

<!-- table of contents -->

## Stop displaying a default rich menu 

To stop displaying a default rich menu that is displayed to all users, unlink it according to the method used to set the rich menu.

- [If you set it up with the Messaging API](https://developers.line.biz/en/docs/messaging-api/stop-displaying-rich-menu/#stop-displaying-default-rich-menu-messaging-api)
- [If you set it up with the LINE Official Account Manager](https://developers.line.biz/en/docs/messaging-api/stop-displaying-rich-menu/#stop-displaying-default-rich-menu-oa)

However, even if you unlink a default rich menu, the per-user rich menu will continue to be displayed for users who are linked to a per-user rich menu.

### If you set it up with the Messaging API 

If you set up a rich menu with the Messaging API, use the [Clear default rich menu](https://developers.line.biz/en/reference/messaging-api/#clear-default-rich-menu) endpoint.

Even if you clear a rich menu, the change won't be reflected in a user's rich menu until the user re-enters the chat screen. Also, it may take about a minute for the change to be applied.

### If you set it up with the LINE Official Account Manager 

If you set up a rich menu with the [LINE Official Account Manager](https://manager.line.biz/), change or delete the setting from the LINE Official Account Manager. You can't stop displaying a rich menu set up with the LINE Official Account Manager from the Messaging API.

## Stop displaying a per-user rich menu 

To stop displaying a per-user rich menu, unlink the rich menu from the user. Use one of the following endpoints according to the range of target users.

| Target | Endpoint to use | Timing of unlinking |
| --- | --- | --- |
| A single user | [Unlink rich menu from user](https://developers.line.biz/en/reference/messaging-api/#unlink-rich-menu-from-user) | Immediate |
| Multiple users | [Unlink rich menus from multiple users](https://developers.line.biz/en/reference/messaging-api/#unlink-rich-menu-from-users), etc. | Asynchronous |
| All users linked to a specific rich menu | [Replace or unlink the linked rich menus in batches](https://developers.line.biz/en/reference/messaging-api/#batch-control-rich-menus-of-users) | Asynchronous |

However, even if you unlink a per-user rich menu, the default rich menu will continue to be displayed for users who are linked to a default rich menu.

## If you are using tab switching (rich menu aliases) 

If you are switching tabs using rich menu aliases, a user may tap a tab and switch to another rich menu while you are unlinking the rich menu from the user. In this case, the link to the target rich menu may remain without being unlinked.

![](https://developers.line.biz/media/messaging-api/rich-menu/stop-displaying-rich-menu-tab-switching.webp)

To completely stop displaying the rich menu, we recommend stopping the display using the following steps:

1. Use the [Delete rich menu alias](https://developers.line.biz/en/reference/messaging-api/#delete-rich-menu-alias) endpoint so that users can't switch to another tab.
1. Use an endpoint such as [Replace or unlink the linked rich menus in batches](https://developers.line.biz/en/reference/messaging-api/#batch-control-rich-menus-of-users) to unlink the target rich menu from users.
1. To unlink the links that remained without being unlinked due to tab switching, wait for a while and re-execute the unlinking process.

For rich menus using the rich menu alias deleted in step 1, tab switching won't be possible until the unlinking is complete, which may temporarily degrade the user experience.

## Delete unneeded rich menus 

Once you have confirmed that the rich menu is completely no longer displayed to users and is no longer displayed on the user's chat screen, we recommend deleting the unneeded rich menu with the [Delete rich menu](https://developers.line.biz/en/reference/messaging-api/#delete-rich-menu) endpoint.

There is a limit to the number of rich menus you can create with the Messaging API (1,000 per LINE Official Account). By deleting unneeded rich menus, you can operate without reaching the limit.

Even if you delete only the rich menu without [unlinking it from users](https://developers.line.biz/en/docs/messaging-api/stop-displaying-rich-menu/#stop-displaying-per-user-rich-menu), it won't disappear immediately from the user's chat screen. The deleted rich menu will continue to be displayed until the user re-enters the chat screen. If you want to stop it immediately even while the user is on the chat screen, don't delete the rich menu, but unlink it first.

Also, you can [get rich menu insight even after deleting a rich menu](https://developers.line.biz/en/docs/messaging-api/rich-menus-overview/#rich-menu-insight-after-deletion), but you will no longer be able to [get rich menu list](https://developers.line.biz/en/reference/messaging-api/#get-rich-menu-list) via the Messaging API. If you plan to get statistical information even after deleting a rich menu, be sure to save the rich menu ID before deleting it.
