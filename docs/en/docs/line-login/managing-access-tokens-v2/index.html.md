# Managing access tokens (LINE Login v2.0)

<!-- warning start -->

**LINE Login v2.0 is deprecated**

This page contains documentation for the previous version of LINE Login, v2.0. LINE Login v2.0 has been [deprecated](https://developers.line.biz/en/glossary/#deprecated), with the [end-of-life](https://developers.line.biz/en/glossary/#end-of-life) date to be determined, so we recommend that you use the current version (LINE Login v2.1). There will be a certain grace period between the end-of-life announcement and the actual end-of-life. For more information, see [LINE Login versions](https://developers.line.biz/en/docs/line-login/overview/#versions).

<!-- warning end -->

The access tokens managed through the LINE Login API verifies that an app has been granted permission to access user data (such as user IDs, display names, profile images, and status messages) saved on the LINE Platform.

This topic explains how to manage access tokens using [LINE Login v2.0](https://developers.line.biz/en/docs/line-login/overview/#versions) endpoints.

## Get the user's access token 

An access token is returned by the LINE Platform once user authentication is complete.

At this point, you can assume the app has permission to access user data.

To learn more, see:

**LINE Login:**

- [Integrating LINE Login (v2.0) with your web app](https://developers.line.biz/en/docs/line-login/integrate-line-login-v2/)

<!-- note start -->

**Access token validity period**

An access token is valid for 30 days after being issued. Any response with an access token also includes the number of seconds until the token expires in the `expires_in` property.

<!-- note end -->

### Refresh tokens 

A refresh token is returned along with an access token once user authentication is complete.

When an access token expires, you can use a refresh token to get a new one. To learn more, see [Refresh access token](https://developers.line.biz/en/reference/line-login-v2/#refresh-access-token) in the LINE Login v2.0 API reference.

<!-- note start -->

**Refresh token validity period**

A refresh token is valid for up to 90 days after its corresponding access token was issued.

If the refresh token expires, you must prompt the user to log in again to generate a new access token.

<!-- note end -->

## Verify access tokens 

Verify any access token that you receive from an app or external server before using it on your own servers.

To learn more, see [Verify access token validity](https://developers.line.biz/en/reference/line-login-v2/#verify-access-token) in the LINE Login v2.0 API reference.

<!-- note start -->

**Additional criteria that you need to check after verifying an access token**

When the LINE Login API successfully verifies an access token, its response contains a `client_id` property (the channel ID) and an `expires_in` property (the amount of time until the token expires). Make sure that these properties satisfy the following criteria before you use the access token.

| Property     | Criteria                                                |
| ------------ | ------------------------------------------------------- |
| `client_id`  | Channel ID of the LINE Login channel linked to your app |
| `expires_in` | A positive value                                        |

<!-- note end -->
