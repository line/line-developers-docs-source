# Managing users (LINE Login v2.0)

<!-- warning start -->

**LINE Login v2.0 is deprecated**

This page contains documentation for the previous version of LINE Login, v2.0. LINE Login v2.0 has been [deprecated](https://developers.line.biz/en/glossary/#deprecated), with the [end-of-life](https://developers.line.biz/en/glossary/#end-of-life) date to be determined, so we recommend that you use the current version (LINE Login v2.1). There will be a certain grace period between the end-of-life announcement and the actual end-of-life. For more information, see [LINE Login versions](https://developers.line.biz/en/docs/line-login/overview/#versions).

<!-- warning end -->

This topic explains how to use [LINE Login v2.0](https://developers.line.biz/en/docs/line-login/overview/#versions) endpoints to manage users who have logged in through the LINE Login API.

## Get user profiles 

You can get profile information for users who have been identified by an [access token](https://developers.line.biz/en/docs/line-login/managing-access-tokens/). Profile information includes a user's ID, display name, profile image, and status message.

Both LINE Login v2.0 and v2.1 share the same method for fetching user profiles. To learn more, see [Getting user profiles](https://developers.line.biz/en/docs/line-login/managing-users/#get-profile).

## Log out users 

<!-- note start -->

**Note**

This is the documentation for LINE Login v2.0, an older version of LINE Login.

To learn how to do this using the latest version, LINE Login v2.1, see [Logging out users](https://developers.line.biz/en/docs/line-login/managing-users/#logout).

<!-- note end -->

To create a better user experience, we recommend providing a way for users to log out of your app.

When a user has logged out of your app, revoke their [access token](https://developers.line.biz/en/docs/line-login/managing-access-tokens-v2/) and delete all the user data in your app.

Example request to revoke an access token:

```sh
curl -v -X POST https://api.line.me/v2/oauth/revoke \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'refresh_token={refresh token}'
```

To learn more, see [Revoke access token](https://developers.line.biz/en/reference/line-login-v2/#revoke-access-token) in the LINE Login v2.0 API reference.
