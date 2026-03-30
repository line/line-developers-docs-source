# LINE Profile+

<!-- note start -->

**Use of optional functions requires an application**

Only corporate users in Japan who have submitted the required applications can use the functions described in this document. To use the information registered with LINE Profile+ via LINE Login, LIFF App, or LINE MINI App, contact your sales representative or [our Sales partners](https://www.lycbiz.com/jp/partner/sales/). For LINE MINI Apps, this feature is only available for verified MINI Apps.

<!-- note end -->

LINE Profile+ is a service for managing the profile information of LINE users. The information that users register with LINE Profile+ is different from usual [profile information](https://developers.line.biz/en/glossary/#profile-information) and can only be obtained by corporate users who have undergone the application process.

<!-- table of contents -->

## Differences between profile information and LINE Profile+ 

For more information on the differences between LINE profile information and LINE Profile+, see [Get user profile information](https://developers.line.biz/en/docs/basics/user-profile/) in the LINE Platform basics.

- [What is user profile information](https://developers.line.biz/en/docs/basics/user-profile/#what-is-profile)
- [LINE Profile+](https://developers.line.biz/en/docs/basics/user-profile/#what-is-line-profile-plus)

## Get user data registered with LINE Profile+ 

You can get information registered with LINE Profile+ by using either the LIFF app or LINE MINI App, or by integrating LINE Login into your own web app.

Use the following steps to specify the scopes of information you want to obtain, and to get the payload of the ID token containing LINE Profile+ information.

| Step | [Via LIFF App or LINE MINI App](https://developers.line.biz/en/docs/partner-docs/line-profile-plus/#liff-mini) | [Via LINE Login](https://developers.line.biz/en/docs/partner-docs/line-profile-plus/#line-login) |
| --- | --- | --- |
| 1. Specify scopes | [Specify scopes on LINE Developers Console](https://developers.line.biz/en/docs/partner-docs/line-profile-plus/#liff-specify-scope) | [Specify scopes for authorization URL](https://developers.line.biz/en/docs/partner-docs/line-profile-plus/#line-login-specify-scope) |
| 2. Get ID token payload | [Get ID token payload via liff.getDecodedIDToken()](https://developers.line.biz/en/docs/partner-docs/line-profile-plus/#liff-get-id-token) | [Validate ID token obtained when issuing access token to get ID token payload](https://developers.line.biz/en/docs/partner-docs/line-profile-plus/#line-login-get-id-token) |
| 3. Get LINE Profile+ Information | [Get LINE Profile+ information from ID token payload](https://developers.line.biz/en/docs/partner-docs/line-profile-plus/#liff-get-profile-plus) | [Get LINE Profile+ information from ID token payload](https://developers.line.biz/en/docs/partner-docs/line-profile-plus/#line-login-get-profile-plus) |

### Via LIFF App or LINE MINI App 

To get information registered with LINE Profile+ via LIFF App or LINE MINI App, set the [scopes](https://developers.line.biz/en/docs/partner-docs/line-profile-plus/#scope) of information you want to obtain on the [LINE Developers Console](https://developers.line.biz/console/), then get ID token payload, and you will be able to obtain the LINE Profile+ information of currently logged-in users.

#### 1. Specify scopes on LINE Developers Console 

Specify the scopes of information you want to obtain in advance. Select the target channel on the [LINE Developers Console](https://developers.line.biz/console/), and from the **Scope** section under the **Web app settings** tab of the LINE MINI App chanel or the **LIFF** tab of the LINE Login channel, check the scope(s) you would like to use.

For more information on the scopes you can get via LINE Profile+, see [LINE Profile+ scopes](https://developers.line.biz/en/docs/partner-docs/line-profile-plus/#scope).

![profile plus scope](https://developers.line.biz/media/partner-docs/profile_plus_scopes_en.png)

<!-- note start -->

**Specify openid at the same time**

To get information registered with LINE Profile+, an ID token is required. Specify `openid` for requesting permission to get the ID token at the same time.

<!-- note end -->

#### 2. Get ID token payload via liff.getDecodedIDToken() 

When you execute the [`liff.getDecodedIDToken()`](https://developers.line.biz/en/reference/liff/#get-decoded-id-token) method of the LIFF SDK, you can get a payload of decoded ID token that contains LINE Profile+ information of currently logged-in users of the LIFF App or the LINE MINI App.

Example code for getting ID token payload:

```javascript
liff.init(() => {
  const idToken = liff.getDecodedIDToken();
  console.log(idToken); // print decoded idToken object
});
```

#### 3. Get LINE Profile+ information from ID token payload 

Verify the LINE Profile+ information in the ID token payload obtained from step 2.

Example of LINE Profile+ information:

```json
"given_name": "LINE",
"middle_name": "L",
"family_name": "Taro",
"gender": "male",
"birthdate": "1990-01-01",
"phone_number": "+81901111....",
"address": {
    "postal_code": "1028282",
    "region": "Tokyo",
    "locality": "Kioicho, Chiyoda-ku",
    "street_address": "1-3",
    "country": "JP"
}
```

For more information on LINE Profile+ information included in ID token, see [LINE Profile+ information included in ID token](https://developers.line.biz/en/docs/partner-docs/line-profile-plus/#id-token).

### Via LINE Login 

You can obtain information registered with LINE Profile+ by integrating LINE Login v2.1 into your web app and using an [ID token](https://developers.line.biz/en/docs/line-login/verify-id-token/#id-tokens).

This page only contains additional information on using LINE Profile+. For more details about how to integrate LINE Login v2.1, see [Integrating LINE Login with your web app](https://developers.line.biz/en/docs/line-login/integrate-line-login/).

<!-- note start -->

**Note**

LINE Profile+ is not compatible with LINE Login v2.0 or earlier.

<!-- note end -->

#### 1. Specify scopes for authorization URL 

Specify dedicated scopes for the authorization URL `scope` parameter.

For more information on the scopes you can get via LINE Profile+, see [LINE Profile+ scopes](https://developers.line.biz/en/docs/partner-docs/line-profile-plus/#scope).

The following is an example of an authorization URL with query parameters:

```sh
https://access.line.me/oauth2/v2.1/authorize?response_type=code&client_id=1234567890&redirect_uri=https%3A%2F%2Fexample.com%2Fauth%3Fkey%3Dvalue&state=123abc&scope=openid%20profile%20real_name%20gender%20birthdate%20phone%20address&bot_prompt=normal&nonce=0987654asd
```

<!-- note start -->

**Specify openid at the same time**

To get information registered with LINE Profile+, an ID token is required. Specify `openid` for requesting permission to get the ID token at the same time.

<!-- note end -->

For more information about the operation after the user accesses the authorization URL, see [Authentication process](https://developers.line.biz/en/docs/line-login/integrate-line-login/#authentication-process).

#### 2. Validate ID token obtained when issuing access token to get ID token payload 

Information registered with LINE Profile+ is included in the [ID token](https://developers.line.biz/en/docs/line-login/verify-id-token/#id-tokens). The ID token is included in the response when [issuing the access token](https://developers.line.biz/en/docs/line-login/integrate-line-login/#get-access-token).

Request example:

```sh
curl -v -X POST https://api.line.me/oauth2/v2.1/token \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=authorization_code' \
-d 'code=b5fd32eacc791df' \
--data-urlencode 'redirect_uri=https://example.com/auth?key=value' \
-d 'client_id=12345' \
-d 'client_secret=d6524edacc8742aeedf98f'
```

ID tokens obtained via [Issue access token](https://developers.line.biz/en/reference/line-login/#issue-access-token) are encoded in Base64 format (e.g. `eyJhbGciOiJIUzI1NiJ9...`). You can get ID token payload decoded in JSON format by executing [Verify ID token](https://developers.line.biz/en/reference/line-login/#verify-id-token).

Request example:

```sh
curl -v -X POST 'https://api.line.me/oauth2/v2.1/verify' \
 -d 'id_token=eyJraWQiOiIxNmUwNGQ0ZTU2NzgzYTc5MmRjYjQ2ODRkOD...' \
 -d 'client_id=1234567890'
```

#### 3. Get LINE Profile+ information from ID token payload 

Verify the LINE Profile+ information in the ID token payload obtained from step 2.

Example of LINE Profile+ information:

```json
"given_name": "LINE",
"middle_name": "L",
"family_name": "Taro",
"gender": "male",
"birthdate": "1990-01-01",
"phone_number": "+81901111....",
"address": {
    "postal_code": "1028282",
    "region": "Tokyo",
    "locality": "Kioicho, Chiyoda-ku",
    "street_address": "1-3",
    "country": "JP"
}
```

For more information on LINE Profile+ information included in ID token, see [LINE Profile+ information included in ID token](https://developers.line.biz/en/docs/partner-docs/line-profile-plus/#id-token).

## LINE Profile+ scopes 

These are the scopes of information you can obtain via LINE Profile+:

- `real_name`: Authority to obtain the "name" registered by the user
- `gender`: Authority to obtain the "gender" registered by the user
- `birthdate`: Authority to obtain the "birthdate" registered by the user
- `phone`: Authority to obtain the "phone number" registered by the user
- `address`: Authority to obtain the "address" registered by the user

<!-- note start -->

**Note**

It is necessary to apply for the scope to be used in advance.

<!-- note end -->

## LINE Profile+ information included in ID token 

The payload of the ID token you acquired through either the LIFF App or LINE MINI App, or through LINE Login, contains information from the specified scope of LINE Profile+.

#### Payload 

When using LINE Profile+, the following properties are added to the ID token.

| Properties | Type | Description | Scope that requires authorization |
| --- | --- | --- | --- |
| `given_name` | String | First name | `real_name` |
| `given_name_pronunciation` | String | Kana of first name | `real_name` |
| `middle_name` | String | Middle name | `real_name` |
| `family_name` | String | Last name | `real_name` |
| `family_name_pronunciation` | String | Kana of last name. It is katakana. | `real_name` |
| `gender` | String | "male", "female", or a value entered by users | `gender` |
| `birthdate` | String | Birthdate. The format follows the [RFC3339 protocol](https://www.ietf.org/rfc/rfc3339.txt). | `birthdate` |
| `phone_number` | String | Phone number. The format follows the [E.164](https://developers.line.biz/en/glossary/#e164). | `phone` |
| `address` | Object | [Address object](https://developers.line.biz/en/docs/partner-docs/line-profile-plus/#address-object) | `address` |

##### Address object 

You can register up to 10 addresses to LINE Profile+. For ID tokens, you can get only one recently updated or used address.

| Field | Type | Description |
| --- | --- | --- |
| `postal_code` | String | Postal code. Single byte numbers with no hyphens. This is optional so may be left blank in some cases. |
| `region` | String | State or province |
| `locality` | String | City |
| `street_address` | String | The value entered in "Street" and "Other". "Street" and "Other" are separated by a line break code (`/n`). This is optional so may be left blank in some cases. |
| `country` | String | Country name. Notation in line with ISO 3166-1 alpha-2. |

#### Payload example 

```json
{
  "iss": "https://access.line.me",
  "sub": "U272cada9c6f4c0c933b0713bc2f90f68",
  "aud": "1234567890",
  "exp": 1513142487,
  "iat": 1513138887,
  "name": "LINE taro",
  "picture": "https://profile.line-scdn.net/0h8pWWElvzZ19qLk3ywQYYCFZraTIdAGEXEhx9ak56MDxDHiUIVEEsPBspMG1EGSEPAk4uP01t0m5G",
  "given_name": "LINE",
  "middle_name": "L",
  "family_name": "Taro",
  "gender": "male",
  "birthdate": "1990-01-01",
  "phone_number": "+81901111....",
  "address": {
    "postal_code": "1028282",
    "region": "Tokyo",
    "locality": "Kioicho, Chiyoda-ku",
    "street_address": "1-3",
    "country": "JP"
  }
}
```
