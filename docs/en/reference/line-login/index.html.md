# LINE Login v2.1 API reference

## Common specifications 

### Rate limits 

If you send a large number of requests to the LINE Login API within a short period of time, and it is determined that it will affect the operation of the LINE Platform, we may temporarily restrict your requests. Refrain from sending large numbers of requests for any purpose, including load testing.

<!-- tip start -->

**On rate limit thresholds**

Rate limit thresholds for the LINE Login API are not disclosed.

<!-- tip end -->

### Status codes 

These HTTP status codes are returned after an API call. We follow the [HTTP status code specification](https://datatracker.ietf.org/doc/html/rfc7231#section-6) unless otherwise stated.

| Status code | Description |
| --- | --- |
| 200 OK | The request succeeded. |
| 400 Bad Request | There was a problem with the request. Check the request parameters and JSON format. |
| 401 Unauthorized | Check that the authorization header is correct. |
| 403 Forbidden | You are not authorized to use the API. Confirm that your account or plan is authorized to use the API. |
| 413 Payload Too Large | Request exceeds the max size of 2MB. Make the request smaller than 2MB and try again. |
| 429 Too Many Requests | Temporarily restricting requests because [rate-limit](https://developers.line.biz/en/reference/line-login/#rate-limits) has been exceeded by a large number of requests. |
| 500 Internal Server Error | There was a temporary error on the API server. |

### Response headers 

The following HTTP headers are included in LINE Login API responses:

| Response header | Description |
| --- | --- |
| x-line-request-id | Request ID. An ID is issued for each request. |

## OAuth 

### Issue access token 

Endpoint: `POST` `https://api.line.me/oauth2/v2.1/token`

Issues access tokens.

The access tokens managed through the LINE Login API attest that an app has been granted permission to access user data (such as user IDs, display names, profile images, and status messages) saved on the LINE Platform.

LINE Login API calls require you to provide an access token or refresh token that was sent in an earlier response.

<!-- note start -->

**Note**

- This is the reference for the LINE Login v2.1 endpoint. For information on the v2.0 endpoint, see [Issue access token](https://developers.line.biz/en/reference/line-login-v2/#issue-access-token) in the v2.0 API reference.
- As new LINE Login features are added and existing features are modified, the structure of the JSON objects in responses and ID tokens may change. These changes may cause properties to be added or ordered differently; whitespace and line breaks to be added or removed between elements; and the size of the data to vary. Design your backend to be tolerant of future payloads that are structured differently.

<!-- note end -->

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/oauth2/v2.1/token \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=authorization_code' \
-d 'code=1234567890abcde' \
--data-urlencode 'redirect_uri=https://example.com/auth?key=value' \
-d 'client_id=1234567890' \
-d 'client_secret=1234567890abcdefghij1234567890ab' \
-d 'code_verifier=wJKN8qz5t8SSI9lMFhBB6qwNkQBkuPZoCxzRhwLRUo1'
```

<!-- tab end -->

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

[Authorization code](https://developers.line.biz/en/docs/line-login/integrate-line-login/#receiving-the-authorization-code) received from the LINE Platform

<!-- parameter end -->
<!-- parameter start (props: required) -->

redirect_uri

String

Same value as `redirect_uri` specified in the [authorization request](https://developers.line.biz/en/docs/line-login/integrate-line-login/#making-an-authorization-request).

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
<!-- parameter start (props: optional) -->

code_verifier

String

A random 43-128 character string consisting of single-byte alphanumeric characters and symbols (e.g. `wJKN8qz5t8SSI9lMFhBB6qwNkQBkuPZoCxzRhwLRUo1`).<br><br>If your LINE Login implements PKCE, you can add this parameter to verify the validity of the `code_verifier` on the LINE Platform side before returning the access token.<br><br>For more information on how to implement PKCE, see [Implement PKCE for LINE Login](https://developers.line.biz/en/docs/line-login/integrate-pkce/#how-to-integrate-pkce) in the LINE Login documentation.

<!-- parameter end -->

#### Response 

Returns status code `200` and a JSON object with the following information.

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

id_token

String

[JSON Web Token (JWT)](https://datatracker.ietf.org/doc/html/rfc7519) with information about the user. This property is returned only if you requested the `openid` scope. For more information about ID tokens, see [Get profile information from ID tokens](https://developers.line.biz/en/docs/line-login/verify-id-token/).

<!-- parameter end -->
<!-- parameter start -->

refresh_token

String

Token used to get a new access token (refresh token). Valid for 90 days after the access token is issued.

For more information, see [Refresh access token](https://developers.line.biz/en/reference/line-login/#refresh-access-token).

<!-- parameter end -->
<!-- parameter start -->

scope

String

Permissions granted to the access token. For more information on scopes, see [Scopes](https://developers.line.biz/en/docs/line-login/integrate-line-login/#scopes).

Note that the `email` scope isn't returned as a value of the `scope` property even if access to it has been granted.

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
  "access_token": "bNl4YEFPI/hjFWhTqexp4MuEw5YPs...",
  "expires_in": 2592000,
  "id_token": "eyJhbGciOiJIUzI1NiJ9...",
  "refresh_token": "Aa1FdeggRhTnPNNpxr8p",
  "scope": "profile",
  "token_type": "Bearer"
}
```

<!-- tab end -->

### Verify access token validity 

Verifies if an access token is valid.

For general recommendations on how to securely handle user registration and login with access tokens, see [Creating a secure login process between your app and server](https://developers.line.biz/en/docs/line-login/secure-login-process/) in the LINE Login documentation.

<!-- note start -->

**Note**

This is the reference for the LINE Login v2.1 endpoint. For information on the v2.0 endpoint, see [Verify access token validity](https://developers.line.biz/en/reference/line-login-v2/#verify-access-token) in the LINE Login v2.0 API reference.

<!-- note end -->

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X GET \
'https://api.line.me/oauth2/v2.1/verify?access_token=eyJhbGciOiJIUzI1NiJ9.UnQ_o-GP0VtnwDjbK0C8E_NvK...'
```

<!-- tab end -->

#### HTTP request 

`GET https://api.line.me/oauth2/v2.1/verify`

#### Query parameters 

<!-- parameter start (props: required) -->

access_token

Access token

<!-- parameter end -->

#### Response 

If the access token is valid, a `200 OK` status code is returned with a JSON object that has the following information.

<!-- parameter start -->

scope

String

Permissions granted to the access token. To learn more about scopes, see [Scopes](https://developers.line.biz/en/docs/line-login/integrate-line-login/#scopes).

<!-- parameter end -->
<!-- parameter start -->

client_id

String

Channel ID for which the access token is issued

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
  "scope": "profile",
  "client_id": "1440057261",
  "expires_in": 2591659
}
```

<!-- tab end -->

#### Error response 

If the access token has expired, a `400 Bad Request` HTTP status code and a JSON response are returned.

_Example error response_

<!-- tab start `json` -->

```json
{
  "error": "invalid_request",
  "error_description": "access token expired"
}
```

<!-- tab end -->

### Refresh access token 

Gets a new access token using a refresh token.

A refresh token is returned along with an access token once user authentication is complete.

<!-- note start -->

**Note**

- This is the reference for the LINE Login v2.1 endpoint. For information on the v2.0 endpoint, see [Refresh access token](https://developers.line.biz/en/reference/line-login-v2/#refresh-access-token) in the LINE Login v2.0 API reference.
- You can't use this to refresh a channel access token for the Messaging API.

<!-- note end -->

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/oauth2/v2.1/token \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=refresh_token&refresh_token={your_refresh_token}&client_id={your_channel_id}&client_secret={your_channel_secret}'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/oauth2/v2.1/token`

#### Request headers 

<!-- parameter start (props: required) -->

Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### Request body 

<!-- parameter start (props: required) -->

grant_type

String

`refresh_token`

<!-- parameter end -->
<!-- parameter start (props: required) -->

refresh_token

String

The refresh token corresponding to the access token to be reissued. Valid for up to 90 days after the access token was issued. If the refresh token expires, you must prompt the user to log in again to generate a new access token.

<!-- parameter end -->
<!-- parameter start (props: required) -->

client_id

String

Channel ID. Found in the [LINE Developers Console](https://developers.line.biz/console/).

<!-- parameter end -->
<!-- parameter start (props: annotation="See description") -->

client_secret

String

Channel secret. Found in the [LINE Developers Console](https://developers.line.biz/console/).

- Required for channels whose **App types** is only **Web app**.
- Ignored for channels whose **App types** is **Mobile app** and **Web app**.
- Ignored for channels whose **App types** is only **Mobile app**.

<!-- parameter end -->

#### Response 

If the access token is successfully refreshed, a new access token and refresh token are returned.

<!-- parameter start -->

access_token

String

Access token. Valid for 30 days.

<!-- parameter end -->
<!-- parameter start -->

token_type

String

`Bearer`

<!-- parameter end -->
<!-- parameter start -->

refresh_token

String

Refresh token you specified for the `refresh_token` property when requesting to reissue an access token. Getting a new access token won't extend the validity period of the refresh token.

<!-- parameter end -->
<!-- parameter start -->

expires_in

Number

Validity period of the access token. Expressed in the remaining number of seconds to expiry from when the API was called.

<!-- parameter end -->
<!-- parameter start -->

scope

String

Permissions obtained through the access token. For more information on scopes, see [Scopes](https://developers.line.biz/en/docs/line-login/integrate-line-login/#scopes).

<!-- parameter end -->

_Example response_

<!-- tab start `json` -->

```json
{
  "token_type": "Bearer",
  "scope": "profile",
  "access_token": "bNl4YEFPI/hjFWhTqexp4MuEw...",
  "expires_in": 2591977,
  "refresh_token": "8iFFRdyxNVNLWYeteMMJ"
}
```

<!-- tab end -->

#### Error response 

If the refresh token has expired, a `400 Bad Request` HTTP status code and a JSON response are returned.

_Example error response_

<!-- tab start `json` -->

```json
{
  "error": "invalid_grant",
  "error_description": "invalid refresh token"
}
```

<!-- tab end -->

### Revoke access token 

Invalidates a user's access token.

<!-- note start -->

**Note**

- This is the reference for the LINE Login v2.1 endpoint. For information on the v2.0 endpoint, see [Revoke access token](https://developers.line.biz/en/reference/line-login-v2/#revoke-access-token) in the LINE Login v2.0 API reference.
- You can't use this to invalidate a channel access token for the Messaging API.

<!-- note end -->

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/oauth2/v2.1/revoke \
-H "Content-Type: application/x-www-form-urlencoded" \
-d "client_id={channel id}&client_secret={channel secret}&access_token={access token}"
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/oauth2/v2.1/revoke`

#### Request headers 

<!-- parameter start (props: required) -->

Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### Request body 

<!-- parameter start (props: required) -->

access_token

String

Access token

<!-- parameter end -->
<!-- parameter start (props: required) -->

client_id

String

Channel ID. Found in the [LINE Developers Console](https://developers.line.biz/console/).

<!-- parameter end -->
<!-- parameter start (props: annotation="See description") -->

client_secret

String

Channel secret. Found in the [LINE Developers Console](https://developers.line.biz/console/).

- Required for channels whose **App types** is only **Web app**.
- Ignored for channels whose **App types** is **Mobile app** and **Web app**.
- Ignored for channels whose **App types** is only **Mobile app**.

<!-- parameter end -->

#### Response 

Returns status code `200` and an empty response body.

### Deauthorize your app to which the user has granted permissions 

Deauthorize your app on behalf of the user, revoking the permissions previously granted by the user. For more information, see the required matter "[Deauthorize your app when a user unregisters from your app](https://developers.line.biz/en/docs/line-login/development-guidelines/#deauthorize)" in the [LINE Login development guidelines](https://developers.line.biz/en/docs/line-login/development-guidelines/).

You can also revoke permissions for LIFF apps and LINE MINI Apps with this endpoint.

For more information about how a user can deauthorize apps to which the user has granted permissions, see [Managing authorized apps](https://developers.line.biz/en/docs/line-login/managing-authorized-apps/) in the LINE Login documentation.

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X POST https://api.line.me/user/v1/deauthorize \
-H 'Authorization: Bearer {channel access token}' \
-H 'Content-Type: application/json' \
-d '{
    "userAccessToken": "{user access token}"
}'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/user/v1/deauthorize`

#### Request headers 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`

The following types of channel access tokens are available:

- [Channel access token with a user-specified expiration (Channel access token v2.1)](https://developers.line.biz/en/docs/basics/channel-access-token/#user-specified-expiration)
- [Stateless channel access token](https://developers.line.biz/en/docs/basics/channel-access-token/#stateless-channel-access-token)

For more information about how to issue channel access tokens, see [Channel access token](https://developers.line.biz/en/docs/basics/channel-access-token/) in the LINE Platform basics.

<!-- parameter end -->

#### Request body 

<!-- parameter start (props: required) -->

userAccessToken

String

Access token of the target user

<!-- parameter end -->

#### Response 

Returns status code `204` and an empty response body.

#### Error response 

Returns the following HTTP status code and an error response:

| Code | Description |
| --- | --- |
| `400` | Invalid access token for the target user. Consider these reasons:<ul><li>The user has already deauthorized your app.</li><li>You have already deauthorized your app on behalf of the user via the API.</li></ul> |

_Error response example_

<!-- tab start `json` -->

```json
// If the access token for the target user is invalid (400 Bad Request)
{
  "message": "invalid token"
}
```

<!-- tab end -->

### Verify ID token 

ID tokens are JSON web tokens (JWT) with information about the user. It's possible for an attacker to spoof an [ID token](https://developers.line.biz/en/docs/line-login/verify-id-token/#id-tokens). Use this call to verify that a received ID token is authentic, meaning you can use it to obtain the user's profile information and email.

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X POST 'https://api.line.me/oauth2/v2.1/verify' \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'id_token=eyJraWQiOiIxNmUwNGQ0ZTU2NzgzYTc5MmRjYjQ2ODRkOD...' \
--data-urlencode 'client_id=1234567890'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/oauth2/v2.1/verify`

#### Request headers 

<!-- parameter start (props: required) -->

Content-Type

application/x-www-form-urlencoded

<!-- parameter end -->

#### Request body 

<!-- parameter start (props: required) -->

id_token

String

ID token

<!-- parameter end -->
<!-- parameter start (props: required) -->

client_id

String

Expected channel ID. Unique identifier for your channel issued by the LINE Platform. Found in the [LINE Developers Console](https://developers.line.biz/console/).

<!-- parameter end -->
<!-- parameter start (props: optional) -->

nonce

String

Expected `nonce` value. Use the `nonce` value provided in the authorization request. Omit if the `nonce` value was not specified in the authorization request.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

user_id

String

Expected user ID. Learn how to get the user ID from [Get user profile](https://developers.line.biz/en/reference/line-login/#get-user-profile).

<!-- parameter end -->

#### Response 

The ID token payload is returned when the specified ID token is successfully verified.

<!-- parameter start -->

iss

String

URL used to generate the ID token.

<!-- parameter end -->
<!-- parameter start -->

sub

String

User ID for which the ID token was generated.

<!-- parameter end -->
<!-- parameter start -->

aud

String

Channel ID

<!-- parameter end -->
<!-- parameter start -->

exp

Number

The expiration time of the ID token in UNIX time (in seconds).

<!-- parameter end -->
<!-- parameter start -->

iat

Number

Time when the ID token was generated in UNIX time (in seconds).

<!-- parameter end -->
<!-- parameter start -->

auth_time

Number

Time the user was authenticated in UNIX time (in seconds). Not included if the `max_age` value wasn't specified in the authorization request.

<!-- parameter end -->
<!-- parameter start -->

nonce

String

The `nonce` value specified in the authorization URL. Not included if the `nonce` value wasn't specified in the authorization request.

<!-- parameter end -->
<!-- parameter start -->

amr

Array of strings

A list of authentication methods used by the user. Not included in the payload under certain conditions.

One or more of:

- `pwd`: Log in with email and password
- `lineautologin`: LINE automatic login (including through LINE SDK)
- `lineqr`: Log in with QR code
- `linesso`: Log in with single sign-on
- `mfa`: Log in with two-factor authentication

<!-- parameter end -->
<!-- parameter start -->

name

String

User's display name. Not included if the `profile` scope wasn't specified in the authorization request.

<!-- parameter end -->
<!-- parameter start -->

picture

String

User's profile image URL. Not included if the `profile` scope wasn't specified in the authorization request.

<!-- parameter end -->
<!-- parameter start -->

email

String

User's email address. Not included if the `email` scope wasn't specified in the authorization request.

<!-- parameter end -->

_Example response_

<!-- tab start `json` -->

```json
{
  "iss": "https://access.line.me",
  "sub": "U1234567890abcdef1234567890abcdef",
  "aud": "1234567890",
  "exp": 1504169092,
  "iat": 1504263657,
  "nonce": "0987654asdf",
  "amr": ["pwd"],
  "name": "Taro Line",
  "picture": "https://sample_line.me/aBcdefg123456",
  "email": "taro.line@example.com"
}
```

<!-- tab end -->

#### Error response 

A JSON object is returned when the specified ID token fails to be verified.

| error_description | Description |
| --- | --- |
| Invalid IdToken. | The ID token is malformed or the signature is invalid. |
| Invalid IdToken Issuer. | The ID token was generated on a site other than "https://access.line.me". |
| IdToken expired. | The ID token has expired. |
| Invalid IdToken Audience. | The ID token's Audience value is different from the `client_id` specified in the request. |
| Invalid IdToken Nonce. | The ID token's Nonce value is different from the `nonce` specified in the request. |
| Invalid IdToken Subject Identifier. | The ID token's SubjectIdentifier value is different from the `user_id` specified in the request. |

_Example error response_

<!-- tab start `json` -->

```json
{
  "error": "invalid_request",
  "error_description": "Invalid IdToken."
}
```

<!-- tab end -->

### Get user information 

Gets a user's ID, display name, and profile image. The scope required for the access token is different for the [Get user profile](https://developers.line.biz/en/reference/line-login/#get-user-profile) endpoint.

You can only get the main profile information. You can't get the user's [subprofile](https://developers.line.biz/en/glossary/#subprofile).

<!-- note start -->

**Note**

Requires an access token with the `openid` scope. For more information, see [Authenticating users and making authorization requests](https://developers.line.biz/en/docs/line-login/integrate-line-login/#making-an-authorization-request) and [Scopes](https://developers.line.biz/en/docs/line-login/integrate-line-login/#scopes) in the LINE Login documentation.

<!-- note end -->

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/oauth2/v2.1/userinfo \
-H 'Authorization: Bearer {access token}'
```

<!-- tab end -->

#### HTTP request 

`GET https://api.line.me/oauth2/v2.1/userinfo`

`POST https://api.line.me/oauth2/v2.1/userinfo`

#### Request headers 

<!-- parameter start (props: required) -->

Authorization

Bearer `{access token}`

<!-- parameter end -->

#### Response 

<!-- parameter start -->

sub

String

User ID

<!-- parameter end -->
<!-- parameter start -->

name

String

User's display name. Not included if the `profile` scope wasn't specified in the authorization request.

<!-- parameter end -->
<!-- parameter start -->

picture

String

User's profile image URL. Not included if the `profile` scope wasn't specified in the authorization request.

<!-- parameter end -->

_Example response_

<!-- tab start `json` -->

```json
{
  "sub": "U1234567890abcdef1234567890abcdef",
  "name": "Taro Line",
  "picture": "https://profile.line-scdn.net/0h8pWWElvzZ19qLk3ywQYYCFZraTIdAGEXEhx9ak56MDxDHiUIVEEsPBspMG1EGSEPAk4uP01t0m5G"
}
```

<!-- tab end -->

## Profile 

### Get user profile 

Gets a user's ID, display name, profile image, and status message. The scope required for the access token is different for the [Get user information](https://developers.line.biz/en/reference/line-login/#userinfo) endpoint.

You can only get the main profile information. You can't get the user's [subprofile](https://developers.line.biz/en/glossary/#subprofile).

<!-- note start -->

**Note**

Requires an access token with the `profile` scope. For more information, see [Authenticating users and making authorization requests](https://developers.line.biz/en/docs/line-login/integrate-line-login/#making-an-authorization-request) and [Scopes](https://developers.line.biz/en/docs/line-login/integrate-line-login/#scopes) in the LINE Login documentation.

<!-- note end -->

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

Profile image URL. This is an HTTPS URL. It's only included in the response if the user has set a profile image.

Profile image thumbnails:

You can get a thumbnail version of a user's profile image by appending any of the following suffixes to their profile image URL.

| Suffix   | Thumbnail size |
| -------- | -------------- |
| `/large` | 200 x 200      |
| `/small` | 51 x 51        |

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
  "userId": "U4af4980629...",
  "displayName": "Brown",
  "pictureUrl": "https://profile.line-scdn.net/abcdefghijklmn",
  "statusMessage": "Hello, LINE!"
}
```

<!-- tab end -->

## Friendship status 

### Get friendship status 

Gets the friendship status between a user and the LINE Official Account linked to your LINE Login channel.

For more information on how to use the add friend option, see [Add a LINE Official Account as a friend when logged in (add friend option)](https://developers.line.biz/en/docs/line-login/link-a-bot/) in the LINE Login documentation.

_Example request_

<!-- tab start `shell` -->

```sh
curl -v -X GET https://api.line.me/friendship/v1/status \
-H 'Authorization: Bearer {access token}'
```

<!-- tab end -->

#### HTTP request 

`GET https://api.line.me/friendship/v1/status`

#### Request headers 

<!-- parameter start (props: required) -->

Authorization

Bearer `{access token}`

<!-- parameter end -->

<!-- note start -->

**Note**

Requires an access token with the `profile` scope. For more information, see [Authenticating users and making authorization requests](https://developers.line.biz/en/docs/line-login/integrate-line-login/#making-an-authorization-request) and [Scopes](https://developers.line.biz/en/docs/line-login/integrate-line-login/#scopes) in the LINE Login documentation.

<!-- note end -->

#### Response 

<!-- parameter start -->

friendFlag

Boolean

- `true`: The user has added the LINE Official Account as a friend and has not blocked it.
- Otherwise, `false`.

<!-- parameter end -->

_Example response_

<!-- tab start `json` -->

```json
{
  "friendFlag": true
}
```

<!-- tab end -->
