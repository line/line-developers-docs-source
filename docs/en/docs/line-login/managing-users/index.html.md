# Managing users

This topic explains how to manage users who have logged in through the LINE Login API.

## Getting user profiles 

You can get profile information for users who have been identified by an [access token](https://developers.line.biz/en/docs/line-login/managing-access-tokens/). Profile information includes a user's ID, display name, profile image, and status message.

<!-- note start -->

**Check your access token's scope**

You need an access token with the `profile` scope to get a user's profile information. To learn more, see [Authenticating users and making authorization requests](https://developers.line.biz/en/docs/line-login/integrate-line-login/#making-an-authorization-request) and [Scopes](https://developers.line.biz/en/docs/line-login/integrate-line-login/#scopes).

<!-- note end -->

Example request:

```sh
curl -v -X GET https://api.line.me/v2/profile \
-H 'Authorization: Bearer {access token}'
```

Example response:

```json
{
  "userId":"U4af4980629...",
  "displayName":"Brown",
  "pictureUrl":"https://profile.line-scdn.net/abcdefghijklmn",
  "statusMessage":"Hello, LINE!"
}
```

To learn more, see [Get user profile](https://developers.line.biz/en/reference/line-login/#get-user-profile) in the LINE Login v2.1 API reference.

<!-- tip start -->

**Identifying users for a service**

Identify users by their [user IDs](https://developers.line.biz/en/glossary/#user-id). User IDs can't be changed.

Users can set a new display name, profile image, and status message at any time.

You can't identify users with this information.

<!-- tip end -->

<!-- tip start -->

**Identifying users with ID tokens**

You can get a user's profile information and email address using the ID token that you obtain along with their access token.

To learn more, see [Verify ID token](https://developers.line.biz/en/reference/line-login/#verify-id-token) in the LINE Login v2.1 API reference.

<!-- tip end -->

## Logging out users 

To create a better user experience, we recommend providing a way for users to log out of your app.

When a user has logged out of your app, revoke their [access token](https://developers.line.biz/en/docs/line-login/managing-access-tokens/) and delete all the user data in your app.

Example request to revoke an access token:

```sh
curl -v -X POST 'https://api.line.me/oauth2/v2.1/revoke' \
-H "Content-Type:application/x-www-form-urlencoded" \
-d "client_id={channel id}&client_secret={channel secret}&access_token={access token}"
```

To learn more, see [Revoke access tokens](https://developers.line.biz/en/reference/line-login/#revoke-access-token) in the LINE Login v2.1 API reference.
