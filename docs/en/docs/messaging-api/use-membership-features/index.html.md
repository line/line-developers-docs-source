# Use membership features

[Membership](https://www.lycbiz.com/jp/service/line-official-account/Membership/) (only available in Japanese) is a monthly membership subscription feature available for the LINE Official Account. Users can subscribe to the membership plan on your LINE Official Account to receive exclusive member perks.

## Endpoint for getting membership information 

With the Messaging API, you can get membership information with the following endpoints:

- [Get a user's membership subscription status](https://developers.line.biz/en/docs/messaging-api/use-membership-features/#get-a-users-membership-subscription-status)
- [Get a list of users who have joined the membership](https://developers.line.biz/en/docs/messaging-api/use-membership-features/#get-membership-user-ids)
- [Get membership plans being offered](https://developers.line.biz/en/docs/messaging-api/use-membership-features/#get-membership-plans)

<!-- tip start -->

**How to start a membership**

You can set up and publish your membership on the [LINE Official Account Manager](https://manager.line.biz/). For more information, see [You can easily create subscription services on LINE! What is the "Membership" feature of the LINE Official Account?](https://www.lycbiz.com/jp/column/line-official-account/service-information/membership/) (only available in Japanese) in LINE for Business.

Currently, the membership feature is only available for LINE Official Accounts in Japan.

<!-- tip end -->

### Get a user's membership subscription status 

This endpoint allows you to get information about the memberships to which the user specified by the user ID is subscribed. For more information, see [Get a user's membership subscription status](https://developers.line.biz/en/reference/messaging-api/#get-a-users-membership-subscription-status) in the Messaging API reference.

### Get a list of users who have joined the membership 

This endpoint allows you to get a list of user IDs for users who have joined the membership of your LINE Official Account. For more information, see [Get a list of users who have joined the membership](https://developers.line.biz/en/reference/messaging-api/#get-membership-user-ids) in the Messaging API reference.

### Get membership plans being offered 

This endpoint allows you to get the membership plans that are currently being offered through your LINE Official Account membership. For more information, see [Get membership plans being offered](https://developers.line.biz/en/reference/messaging-api/#get-membership-plans) in the Messaging API reference.

## Webhook membership event 

When a user joins, renews, or leaves a membership of your LINE Official Account, a webhook membership event is sent. For more information, see [Membership event](https://developers.line.biz/en/reference/messaging-api/#membership-event) in the Messaging API reference.
