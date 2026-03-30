# LINE Login API v2.0 reference

<!-- warning start -->

**LINE Login v2.0 is deprecated**

This page contains documentation for the previous version of LINE Login, v2.0. LINE Login v2.0 has been [deprecated](https://developers.line.biz/en/glossary/#deprecated), with the [end-of-life](https://developers.line.biz/en/glossary/#end-of-life) date to be determined, so we recommend that you use the current version (LINE Login v2.1). There will be a certain grace period between the end-of-life announcement and the actual end-of-life. For more information, see [LINE Login versions](https://developers.line.biz/en/docs/line-login/overview/#versions).

<!-- warning end -->

## Common specifications

### Rate limits 

If you send a large number of requests to the LINE Login API within a short period of time, and it is determined that it will affect the operation of the LINE Platform, we may temporarily restrict your requests. Refrain from sending large numbers of requests for any purpose, including load testing.

<!-- tip start -->

**On rate limit thresholds**

Rate limit thresholds for the LINE Login API are not disclosed.

<!-- tip end -->

### Status codes 

These HTTP status codes are returned after an API call. We follow the [HTTP status code specification](https://datatracker.ietf.org/doc/html/rfc7231#section-6) unless otherwise stated.

Status code | Description
---- | ----
200 OK | Request successful
400 Bad Request | Problem with the request. Check the request parameters and JSON format.
401 Unauthorized | Check that the authorization header is correct.
403 Forbidden | Not authorized to use the API. Confirm that your account or plan is authorized to use the API.
413 Payload Too Large | Request exceeds the max size of 2MB. Make the request smaller than 2MB and try again.
429 Too Many Requests | Temporarily restricting requests because [rate-limit](https://developers.line.biz/en/reference/line-login-v2/#rate-limits) has been exceeded by a large number of requests.
500 Internal Server Error | Temporary error on the API server.

## OAuth

### Issue access token 

Issues access token.

The access tokens managed through the LINE Login API indicate that an app has been granted permission to access user data (such as user IDs, display names, profile images, and status messages) saved on the LINE Platform.

LINE Login API calls require you to provide an access token or refresh token that was sent in an earlier response.

<!-- note start -->

**Note**

This is a description of the LINE Login v2.0 endpoint. For information on the v2.1 endpoint, see [Issue access token](https://developers.line.biz/en/reference/line-login/#issue-access-token) in the v2.1 API reference.

<!-- note end -->

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/oauth/accessToken \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=authorization_code' \
-d 'code=b5fd32eacc791df' \
-d 'redirect_uri=https%3A%2F%2Fexample.com%2Fauth' \
-d 'client_id=12345' \
-d 'client_secret=d6524edacc8742aeedf98f'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/v2/oauth/accessToken`

#### Request headers 

<!-- parameter start (props: required) -->
Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### Request body 

<!-- parameter start (props: required) -->
grant_type
String

`authorization_code`

<!-- parameter end -->
<!-- parameter start (props: required) -->
code
String

[Authorization code](https://developers.line.biz/en/docs/line-login/integrate-line-login-v2/#receiving-the-authorization-code) received from the LINE Platform

<!-- parameter end -->
<!-- parameter start (props: required) -->
redirect_uri
String

Callback URL

<!-- parameter end -->
<!-- parameter start (props: required) -->
client_id
String

Channel ID. Found in the [LINE Developers Console](https://developers.line.biz/console/).

<!-- parameter end -->
<!-- parameter start (props: required) -->
client_secret
String

Channel secret. Found in the [LINE Developers Console](https://developers.line.biz/console/).

<!-- parameter end -->

#### Response 

This returns a `200` status code and a JSON object with the following information.

<!-- parameter start -->
access_token
String

Access token. Valid for 30 days.

<!-- parameter end -->
<!-- parameter start -->
expires_in
Number

Number of seconds until the access token expires.

<!-- parameter end -->
<!-- parameter start -->
refresh_token
String

Token used to get a new access token (refresh token). Valid for up to 10 days after the access token expires.

To learn more, see [Refresh access token](https://developers.line.biz/en/reference/line-login-v2/#refresh-access-token).

<!-- parameter end -->
<!-- parameter start -->
scope
String

Permissions granted to the access token.

- `P`: You have permission to access the user's profile information.

<!-- parameter end -->
<!-- parameter start -->
token_type
String

`Bearer`

<!-- parameter end -->

_Example response_

<!-- tab start `json` -->

```json
{
    "access_token": "bNl4YEFPI/hjFWhTqexp4MuEw5YPs7qhr6dJDXKwNPuLka...",
    "expires_in": 2591977,
    "refresh_token": "8iFFRdyxNVNLWYeteMMJ",
    "scope": "P",
    "token_type": "Bearer"
}
```

<!-- tab end -->

### Verify access token validity 

Verifies that an access token is valid.

For general recommendations on how to securely handle user registration and login with access tokens, see [Verify access tokens](https://developers.line.biz/en/docs/line-login/managing-access-tokens-v2/#verify-access-token) in the LINE Login documentation.

<!-- note start -->

**Note**

This is the reference for the LINE Login v2.0 endpoint. For information on the v2.1 endpoint, see [Verify access token validity](https://developers.line.biz/en/reference/line-login/#verify-access-token) in the LINE Login v2.1 API reference.

<!-- note end -->

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/oauth/verify \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'access_token=bNl4YEFPI/hjFWhTqexp4MuEw5YPs7qhr6dJDXKwNPuLka...'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/v2/oauth/verify`

#### Request headers 

<!-- parameter start (props: required) -->
Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### Request body 

<!-- parameter start -->
access_token
String

Access token

<!-- parameter end -->

#### Response 

If the access token is valid, a `200 OK` status code is returned with a JSON object that has the following information.

<!-- parameter start -->
scope
String

Permissions granted to the access token.

- `P`: You have permission to access the user's profile information.

<!-- parameter end -->
<!-- parameter start -->
client_id
String

The channel ID for which the access token was issued.

<!-- parameter end -->
<!-- parameter start -->
expires_in
Number

Number of seconds until the access token expires.

<!-- parameter end -->

_Example response_

<!-- tab start `json` -->

```json
{
   "scope":"P",
   "client_id":"1350031035",
   "expires_in":2591965
}
```

<!-- tab end -->

#### Error response 

If the access token has expired, a `400 Bad Request` status code is returned with a JSON object.

_Example error response_

<!-- tab start `json` -->

```json
{
    "error": "invalid_request",
    "error_description": "access_token invalid"
}
```

<!-- tab end -->

### Refresh access token 

Gets a new access token using a refresh token. Refresh tokens are returned with the access token when the user authorizes your app.

<!-- note start -->

**Note**

- This is the reference for the LINE Login v2.0 endpoint. For information on the v2.1 endpoint, see [Refresh access token](https://developers.line.biz/en/reference/line-login/#refresh-access-token) in the LINE Login v2.1 API reference.
- You can't use this to refresh a channel access token for the Messaging API.

<!-- note end -->

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/oauth/accessToken \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=refresh_token' \
--data-urlencode 'client_id={channel ID}' \
--data-urlencode 'client_secret={channel secret}' \
--data-urlencode 'refresh_token={refresh token}'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/v2/oauth/accessToken`

#### Request headers 

<!-- parameter start (props: required) -->
Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### Request body 

<!-- parameter start -->
grant_type
String

`refresh_token`

<!-- parameter end -->
<!-- parameter start -->
refresh_token
String

The refresh token corresponding to the access token to be reissued. Valid for up to 10 days after the access token expires. If the refresh token expires, you must prompt the user to log in again to generate a new access token.

<!-- parameter end -->
<!-- parameter start -->
client_id
String

Channel ID. Found in the [LINE Developers Console](https://developers.line.biz/console/).

<!-- parameter end -->
<!-- parameter start -->
client_secret
String

Channel secret. Found in the [LINE Developers Console](https://developers.line.biz/console/).

<!-- parameter end -->

#### Response 

If the access token is successfully refreshed, a new access token and refresh token are returned.

<!-- parameter start -->
token_type
String

`Bearer`

<!-- parameter end -->
<!-- parameter start -->
scope
String

Permissions granted to the access token.

- `P`: You have permission to access the user's profile information.

<!-- parameter end -->
<!-- parameter start -->
access_token
String

Access token

<!-- parameter end -->
<!-- parameter start -->
expires_in
Number

Number of seconds until the access token expires.

<!-- parameter end -->
<!-- parameter start -->
refresh_token
String

Token used to get a new access token (refresh token). Valid for up to 10 days after the access token expires.

<!-- parameter end -->

_Example response_

<!-- tab start `json` -->

```json
{
   "token_type":"Bearer",
   "scope":"P",
   "access_token":"bNl4YEFPI/hjFWhTqexp4MuEw...",
   "expires_in":2591977,
   "refresh_token":"8iFFRdyxNVNLWYeteMMJ"
}
```

<!-- tab end -->

#### Error response 

If the refresh token has expired, a `400 Bad Request` status code is returned with a JSON object.

_Example error response_

<!-- tab start `json` -->

```json
{
    "error": "invalid_grant",
    "error_description": "invalid refresh_token"
}
```

<!-- tab end -->

### Revoke access token 

Invalidates a user's access token.

<!-- note start -->

**Note**

- This is the reference for the LINE Login v2.0 endpoint. For information on the v2.1 endpoint, see [Revoke access token](https://developers.line.biz/en/reference/line-login/#revoke-access-token) in the LINE Login v2.1 API reference.
- You can't use this to invalidate a channel access token for the Messaging API.

<!-- note end -->

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/v2/oauth/revoke \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'refresh_token={refresh token}'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/v2/oauth/revoke`

#### Request headers 

<!-- parameter start (props: required) -->
Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### Request body 

<!-- parameter start -->
refresh_token
String

The refresh token corresponding to the access token to be invalidated.

<!-- parameter end -->

#### Response 

Returns status code `200` and an empty response body.

## Profile

### Get user profile 

Gets a user's ID, display name, profile image, and status message.

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/v2/profile \
-H 'Authorization: Bearer {access token}'
```

<!-- tab end -->

#### HTTP request 

`GET https://api.line.me/v2/profile`

#### Request headers 

<!-- parameter start (props: required) -->
Authorization

Bearer `{access token}`

<!-- parameter end -->

#### Response 

<!-- parameter start -->
userId
String

User ID

<!-- parameter end -->
<!-- parameter start -->
displayName
String

User's display name

<!-- parameter end -->
<!-- parameter start -->
pictureUrl
String

Profile image URL. This is an HTTPS URL. Not included in the response if the user doesn't have a profile image.

Profile image thumbnails:

You can get a thumbnail version of a user's profile image by appending any of these suffixes to their profile image URL.

Suffix | Thumbnail size
-------- | ------
`/large` | 200 x 200
`/small` | 51 x 51

e.g. `https://profile.line-scdn.net/abcdefghijklmn/large`

<!-- parameter end -->
<!-- parameter start -->
statusMessage
String

User's status message. Not included in the response if the user doesn't have a status message.

<!-- parameter end -->

_Example response_

<!-- tab start `json` -->

```json
{
  "userId":"U4af4980629...",
  "displayName":"Brown",
  "pictureUrl":"https://profile.line-scdn.net/abcdefghijklmn",
  "statusMessage":"Hello, LINE!"
}
```

<!-- tab end -->
