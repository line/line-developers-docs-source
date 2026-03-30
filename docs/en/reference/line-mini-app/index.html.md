# LINE MINI App API reference

## Service Messages 

<!-- tip start -->

**This feature can only be used for verified MINI Apps**

This feature is only available for verified MINI Apps. For unverified MINI Apps, you can test the feature on the internal channel for Developing, but you can't use the feature on the internal channel for Published.

<!-- tip end -->

The Service Message API enables you to send service messages from your service to your LINE MINI App users.

Sending service messages requires a service notification token and a [template](https://developers.line.biz/en/docs/line-mini-app/develop/service-messages/#service-message-templates).

- [Issue a service notification token](https://developers.line.biz/en/reference/line-mini-app/#issue-notification-token)
- [Send a service message](https://developers.line.biz/en/reference/line-mini-app/#send-service-message)

### Issuing a service notification token 

Issues a service notification token. Service notification tokens are used to send a service message to the associated user.

Service notification tokens have the following features:

- A service notification token expires 1 year (31,536,000 seconds) after being issued. While it is still valid, up to 5 service messages can be sent.
- Every time you use the service notification token, the token value is renewed unless it expired or no longer has remaining message counts. If you are planning to send successive service messages to a user, keep the renewed service notification token.

<!-- warning start -->

**Don't issue more than one service notification token with a single access token**

Issuing multiple service notification tokens reusing an access token obtained by [`liff.getAccessToken()`](https://developers.line.biz/en/reference/liff/#get-access-token) (LIFF access token) is not allowed.

Only one service notification token can be issued per LIFF access token.

<!-- warning end -->

<!-- note start -->

**Note**

Each service notification token is associated with one user. You can't use a service notification token associated with one user to send a service message to other users.

<!-- note end -->

_Example request_

<!-- tab start `shell` -->

```sh
curl -X POST https://api.line.me/message/v3/notifier/token \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer W1TeHCgfH2Liwa...' \
-d '{
    "liffAccessToken": "eyJhbGciOiJIUzI1NiJ9..."
}'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/message/v3/notifier/token`

#### Request headers 

<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`\
For more information, see [Channel access token](https://developers.line.biz/en/docs/basics/channel-access-token/) in the LINE Platform basics.

<!-- parameter end -->

<!-- note start -->

**Use of stateless channel access tokens is recommended**

[Long-lived channel access tokens](https://developers.line.biz/en/docs/basics/channel-access-token/#long-lived-channel-access-token) and [channel access token with a user-specified expiration (Channel Access Token v2.1)](https://developers.line.biz/en/docs/basics/channel-access-token/#user-specified-expiration) can't be used for LINE MINI App channels.

When developing LINE MINI Apps, either [stateless channel access tokens](https://developers.line.biz/en/docs/basics/channel-access-token/#stateless-channel-access-token) or [short-lived channel access tokens](https://developers.line.biz/en/docs/basics/channel-access-token/#short-lived-channel-access-token) can be used. Stateless channel access tokens are recommended among those two. Stateless channel access tokens have an unlimited number of issuances, so there is no need for the application to manage the token lifecycle.

<!-- note end -->

#### Request body 

<!-- parameter start (props: required) -->

liffAccessToken

String

User access token obtained by [`liff.getAccessToken()`](https://developers.line.biz/en/reference/liff/#get-access-token) (LIFF access token).

<!-- parameter end -->

#### Response 

Returns status code `200` and a JSON object with the following information.

<!-- parameter start -->

notificationToken

String

Service notification token

<!-- parameter end -->
<!-- parameter start -->

expiresIn

Number

The amount of time remaining in seconds before the service notification token expires. A service notification token expires 1 year (31,536,000 seconds) after being issued.

<!-- parameter end -->
<!-- parameter start -->

remainingCount

Number

The number of times you can send a service message with the issued service notification token

<!-- parameter end -->
<!-- parameter start -->

sessionId

String

The session ID. For more information, see [Sending service messages](https://developers.line.biz/en/docs/line-mini-app/develop/service-messages/).

<!-- parameter end -->

_Example response_

<!-- tab start `json` -->

```json
{
  "notificationToken": "34c11a03-b726-49e3-8ce0-949387a9..",
  "expiresIn": 31536000,
  "remainingCount": 5,
  "sessionId": "xD06...."
}
```

<!-- tab end -->

#### Error response 

Returns one of the following status codes and error messages.

| Status code | Description |
| --- | --- |
| 400 Bad request | This status code means one of the following: <ul><li>There is a problem with the request body.</li><li>The LIFF access token specified in the `liffAccessToken` property was used multiple times in a short span of time to request the issuing of service notification tokens.</li></ul> |
| 401 Unauthorized | This status code means one or both of the following: <ul><li>A valid channel access token hasn't been specified.</li><li>A valid LIFF access token hasn't been specified.</li><ul><li>When [the user closes the LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#behavior-when-closing-liff-app), the LIFF access token will be revoked even if it hasn't expired.</li></ul></ul> |
| 403 Forbidden | This channel isn't authorized to issue service messages. |
| 500 Internal Server Error | Error on the internal server |

_Example error response_

<!-- tab start `json` -->

```json
{
  "message": "[liffAccessToken] must not be blank"
}
```

<!-- tab end -->

### Sending service messages 

Sends a service message to a user specified in the service notification token.

Once a service message is sent, the token's value is renewed unless the token expired or no longer has remaining message counts. If you are planning to send successive service messages to a user, keep the renewed service notification token.

_Example request_

<!-- tab start `shell` -->

```sh
curl -X POST https://api.line.me/message/v3/notifier/send?target=service \
-H 'Authorization: Bearer W1TeHCgfH2Liwa...' \
-H 'Content-Type: application/json' \
-d '{
    "templateName": "thankyou_msg_en",
    "params": {
        "date": "2020-04-23",
        "username": "Brown & Cony"
    },
    "notificationToken": "34c11a03-b726-49e3-8ce0-949387a9.."
}'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/message/v3/notifier/send`

#### Request headers 

<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`\
For more information, see [Channel access token](https://developers.line.biz/en/docs/basics/channel-access-token/) in the LINE Platform basics.

<!-- parameter end -->

<!-- note start -->

**Use of stateless channel access tokens is recommended**

[Long-lived channel access tokens](https://developers.line.biz/en/docs/basics/channel-access-token/#long-lived-channel-access-token) and [channel access token with a user-specified expiration (Channel Access Token v2.1)](https://developers.line.biz/en/docs/basics/channel-access-token/#user-specified-expiration) cannot be used for LINE MINI App channels.

When developing LINE MINI Apps, either [stateless channel access tokens](https://developers.line.biz/en/docs/basics/channel-access-token/#stateless-channel-access-token) or [short-lived channel access tokens](https://developers.line.biz/en/docs/basics/channel-access-token/#short-lived-channel-access-token) can be used. Stateless channel access tokens are recommended among those two. Stateless channel access tokens have an unlimited number of issuances, so there is no need for the application to manage the token lifecycle.

<!-- note end -->

#### Query parameters 

<!-- parameter start (props: required) -->

target

`service`

<!-- parameter end -->

#### Request body 

<!-- parameter start (props: required) -->

templateName

String

The name of the template that was added and will be used for the service message. You can check the template name in the LINE Developers Console. For more information, see [Types of service messages that can be sent](https://developers.line.biz/en/docs/line-mini-app/develop/service-messages/#types-of-service-messages-that-can-be-sent).\
Use with a BCP 47 language tag suffix.\
Format: `{template name}_{BCP 47 language tag}`\
Max character limit: 30

<!-- note start -->

**Note**

The languages and language tags supported by the service message are as follows.

- Japanese: `ja`
- English: `en`
- Chinese (Traditional): `zh-TW`
- Thai: `th`
- Indonesian: `id`
- Korean: `ko`

<!-- note end -->

<!-- parameter end -->
<!-- parameter start (props: required) -->

params

object

JSON Object to specify each template variable-value pair. \
If the template has no template variable, specify an empty JSON object (`{ }`). \
The template variables are defined for each template. If a template variable is part of the required elements, be sure to specify a template variable-value pair. \
For more information, see [Adding service message templates to the channel](https://developers.line.biz/en/docs/line-mini-app/develop/service-messages/#service-message-templates).

<!-- parameter end -->
<!-- parameter start (props: required) -->

notificationToken

String

Service notification token

<!-- parameter end -->

#### Response 

Returns status code `200` and a JSON object with the following information.

<!-- parameter start -->

notificationToken

String

A renewed service notification token. Use this service notification token to send successive service messages.

<!-- parameter end -->
<!-- parameter start -->

expiresIn

Number

The remaining amount of time in seconds until renewed service notification token expires

<!-- parameter end -->
<!-- parameter start -->

remainingCount

Number

The number of times you can send successive service messages with the renewed service notification token.

<!-- parameter end -->
<!-- parameter start -->

sessionId

String

The session ID. For more information, see [Sending service messages](https://developers.line.biz/en/docs/line-mini-app/develop/service-messages/).

<!-- parameter end -->

<!-- note start -->

**Note**

If the values of `expiresIn` and `remainingCount` are `0`, it means that the service message was sent, but the service notification token couldn't be renewed.

<!-- note end -->

_Example response_

<!-- tab start `json` -->

```json
// Request was successful,
// renewed service notification
// token issued
{
  "notificationToken": "c9884874-bf6a-4241-8999-2767241c...",
  "expiresIn": 31535906,
  "remainingCount": 3,
  "sessionId": "xD06...."
}

// Request was successful,
// the service message
// was sent, but the LINE Platform
// cannot renew the token
{
  "expiresIn": 0,
  "remainingCount": 0
}
```

<!-- tab end -->

#### Error response 

Returns one of the following status codes and error messages.

| Status code | Description |
| --- | --- |
| 400 Bad request | This status code means one of the following: <ul><li>There is a problem with the request body. </li><li>The target recipient of the service message doesn't exist. </li></ul> |
| 401 Unauthorized | This status code means one or both of the following: <ul><li>A valid channel access token hasn't been specified.</li><li>A valid service notification token hasn't been specified. </li></ul> |
| 403 Forbidden | This status code means one of the following: <ul><li>This channel is not authorized to send service messages. </li><li>The specified template cannot be found.</li></ul> |

_Example error response_

<!-- tab start `json` -->

```json
{
  "message": "Invalid notifier token"
}
```

<!-- tab end -->

## Common Profile Quick-fill 

<!-- tip start -->

**Available only in verified MINI Apps**

To use Common Profile Quick-fill, your LINE MINI App must be verified and you must apply to use Quick-fill. For more information, see [Steps for using Quick-fill](https://developers.line.biz/en/docs/line-mini-app/quick-fill/overview/#process).

<!-- tip end -->

Quick-fill is a feature that automatically fills in the necessary profile information by tapping the **Auto-fill** button on the LINE MINI App. You can easily use the Common Profile information that a user has set in the Account Center in the LINE MINI App. For more information, see [Overview of Common Profile Quick-fill](https://developers.line.biz/en/docs/line-mini-app/quick-fill/overview/).

### liff.$commonProfile.get() 

Gets the information in the Common Profile that the user has set in the Account Center.

When you execute the `liff.$commonProfile.get()` method, a modal will appear to confirm the user's profile. After confirming the profile in the displayed modal, the user can tap **Auto-fill** and the profile information will be entered automatically.

Example of a modal display:

![](https://developers.line.biz/media/line-mini-app/quick-fill/quick-fill-modal-screen.png)

_Example_

<!-- tab start `javascript` -->

```javascript
const { data, error } = await liff.$commonProfile.get(
  ["family-name", "given-name", "email", "tel", "postal-code"],
  {
    formatOptions: {
      givenName: {
        excludeEmojis: false,
      },
      tel: {
        excludeNonJp: false,
      },
      postalCode: {
        digitsOnly: false,
      },
    },
  },
);
console.log(data);
console.log(error);
```

<!-- tab end -->

#### Syntax 

```javascript
liff.$commonProfile.get(scopes, options);
```

#### Arguments 

<!-- parameter start (props: required) -->

scopes

Array of strings

Specify the scope of the Common Profile you want to obtain.

For information on the values that can be specified for `scopes`, see [The `scopes` parameters that can be specified and its return value](https://developers.line.biz/en/docs/line-mini-app/quick-fill/overview/#common-profile-scope).

<!-- parameter end -->
<!-- parameter start (props: optional) -->

options

Object

Options for getting Common Profile information

<!-- parameter end -->
<!-- parameter start (props: optional) -->

options.formatOptions

Object

Options related to the format of information. Specify a [`formatOptions` object](https://developers.line.biz/en/reference/line-mini-app/#get-common-profile-format-options) for each scope specified in the `scopes` property.

Specify the scope for which you want to set the option in camel case format as the key. For example, when the scope is `given-name`, the key is `givenName`.

<!-- parameter end -->

#### `formatOptions` object 

<!-- parameter start (props: optional) -->

excludeEmojis

Boolean

Whether to remove emojis from the string. The default is `true`. This can only be specified in the following scopes:

- givenName
- familyName

<!-- parameter end -->
<!-- parameter start (props: optional) -->

excludeNonJp

Boolean

Whether to exclude phone numbers with 12 or more digits. The default is `true`. If `true`, an empty string and error information are returned when the phone number has 12 or more digits. This can only be specified in the following scope:

- tel

<!-- parameter end -->
<!-- parameter start (props: optional) -->

digitsOnly

Boolean

Whether to exclude postal codes that contain non-numeric characters. The default is `true`. If `true`, an empty string and error information are returned when the postal code contains characters other than numbers. This can only be specified in the following scope:

- postalCode

<!-- parameter end -->

_Example_

<!-- tab start `javascript` -->

```javascript
{
  givenName: {
    excludeEmojis: false,
  },
  tel: {
    excludeNonJp: false,
  },
  postalCode: {
    digitsOnly: false,
  },
}
```

<!-- tab end -->

#### Return value 

Returns `Promise` object of type `{ data: Partial<CommonProfile>, error: Partial<CommonProfileError>}`.

When `Promise` is resolved, an object of type `Partial<CommonProfile>` containing the user's Common Profile information is passed to the `data` property, and an object of type `Partial<CommonProfileError>` containing error information is passed to the `error` property.

In the following cases, the property of `data` will be `undefined` or `null`:

- Cases where the property value becomes `undefined`
  - If the target item isn't specified in the `scopes` parameter
  - If the target item is specified in the `scopes` parameter, but the user doesn't authorized permission for that item
- Cases where the property value becomes `null`
  - If the user hasn't set a value for the target item in the Common Profile
  - If an error occurs when retrieving the target item in the Common Profile

For information on the values of the properties that can be obtained according to the specified `scopes`, see [The `scopes` parameters that can be specified and its return value](https://developers.line.biz/en/docs/line-mini-app/quick-fill/overview/#common-profile-scope).

_Example of an object of type `Partial<CommonProfile>`_

<!-- tab start `json` -->

```javascript
{
  "family-name": "Yamada",
  "given-name": "Taro",
  "email": "sample@example.com",
  "tel": "09001234567",
  "postal-code": "1020094"
}
```

<!-- tab end -->

_Example of an object of type `Partial<CommonProfileError>`_

<!-- tab start `json` -->

```javascript
{
  "tel": ["Phone number has 12 or more digits"],
  "postal-code": ["Postal code contains non-numeric characters"]
}
```

<!-- tab end -->

#### Error response 

When the `Promise` is rejected, [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-errors) is passed.

_Example of calling the API without installing the plugin correctly_

<!-- tab start `javascript` -->

```javascript
new Error(
  "LiffCommonProfilePlugin isn't installed properly. Did you call liff.use(new LiffCommonProfilePlugin()) before using it?"
);
```

<!-- tab end -->

_Example of API being called in a browser other than LIFF browser_

<!-- tab start `javascript` -->

```javascript
new Error("liff.$commonProfile API is available only in LIFF browser.");
```

<!-- tab end -->

### liff.$commonProfile.getDummy() 

Gets the dummy data for the Common Profile. There are 10 types of dummy data available, and you can specify the dummy data to get using the `caseId`.

When you execute the `liff.$commonProfile.getDummy()` method, a modal will appear to confirm the dummy profile. You can get dummy data for the Common Profile by tapping **Auto-fill**.

Example of a modal display:

![](https://developers.line.biz/media/line-mini-app/quick-fill/quick-fill-dummy-modal-screen.png)

_Example_

<!-- tab start `javascript` -->

```javascript
const { data, error } = await liff.$commonProfile.getDummy(
  ["family-name", "given-name", "email", "tel", "postal-code"],
  {
    formatOptions: {
      givenName: {
        excludeEmojis: false,
      },
      tel: {
        excludeNonJp: false,
      },
      postalCode: {
        digitsOnly: false,
      },
    },
  },
  1,
);
console.log(data);
console.log(error);
```

<!-- tab end -->

#### Syntax 

```javascript
liff.$commonProfile.getDummy(scopes, options, caseId);
```

#### Arguments 

<!-- parameter start (props: required) -->

scopes

Array of strings

Specify the scope of the Common Profile you want to obtain.

For information on the values that can be specified for `scopes`, see [The `scopes` parameters that can be specified and its return value](https://developers.line.biz/en/docs/line-mini-app/quick-fill/overview/#common-profile-scope).

<!-- parameter end -->
<!-- parameter start (props: optional) -->

options

Object

Options for getting Common Profile information

<!-- parameter end -->
<!-- parameter start (props: optional) -->

options.formatOptions

Object

Options related to the format of information. Specify a [`formatOptions` object](https://developers.line.biz/en/reference/line-mini-app/#get-common-profile-format-options) for each scope specified in the `scopes` property.

Specify the scope for which you want to set the option in camel case format as the key. For example, when the scope is `given-name`, the key is `givenName`.

<!-- parameter end -->
<!-- parameter start (props: required) -->

caseId

number

Specify the ID of the dummy data you want to get. Dummy data with IDs from `1` to `10` is available.

For information about dummy data for each `caseId`, see [Dummy data for Common Profile that can be obtained](https://developers.line.biz/en/docs/line-mini-app/quick-fill/overview/#get-dummy-common-profile).

<!-- parameter end -->

#### Return value 

Returns `Promise` object of type `{ data: Partial<CommonProfile>, error: Partial<CommonProfileError>}`.

When `Promise` is resolved, an object of type `Partial<CommonProfile>` containing the dummy data of the Common Profile is passed to the `data` property, and an object of type `Partial<CommonProfileError>` containing error information is passed to the `error` property.

In the following cases, the property of `data` will be `undefined` or `null`:

- Cases where the property value becomes `undefined`
  - If the target item isn't specified in the `scopes` parameter
- Cases where the property value becomes `null`
  - If the dummy data doesn't have a value for the target item

For information on the dummy data you can get for the specified ID, see [Dummy data for Common Profile that can be obtained](https://developers.line.biz/en/docs/line-mini-app/quick-fill/overview/#get-dummy-common-profile).

_Example of an object of type `Partial<CommonProfile>`_

<!-- tab start `json` -->

```javascript
{
  "family-name": "見本田",
  "given-name": "見本夫",
  "family-name-kana": "ダミータ",
  "given-name-kana": "ダミーオ",
  "sex-enum": 0,
  "bday-day": 12,
  "bday-month": 3,
  "bday-year": 1998,
  "tel": "09001234567",
  "email": "dummy_39@yahoo.co.jp",
  "postal-code": "1020094",
  "address-level1": "東京都",
  "address-level2": "千代田区",
  "address-level3": "紀尾井町1-2",
  "address-level4": "東京ガーデンテラス紀尾井町"
}
```

<!-- tab end -->

_Example of an object of type `Partial<CommonProfileError>`_

<!-- tab start `json` -->

```javascript
{
  "tel": ["Phone number has 12 or more digits"],
  "postal-code": ["Postal code contains non-numeric characters"]
}
```

<!-- tab end -->

##### Error response 

When the `Promise` is rejected, [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-errors) is passed.

_Example of calling the API without installing the plugin correctly_

<!-- tab start `javascript` -->

```javascript
new Error(
  "LiffCommonProfilePlugin isn't installed properly. Did you call liff.use(new LiffCommonProfilePlugin()) before using it?"
);
```

<!-- tab end -->

_Example of API being called in a browser other than LIFF browser_

<!-- tab start `javascript` -->

```javascript
new Error("liff.$commonProfile API is available only in LIFF browser.");
```

<!-- tab end -->

### liff.$commonProfile.fill() 

Automatically fills the form with the Common Profile information you have obtained. The `data-liff-autocomplete` attribute is used to link each profile information to the form.

<!-- tip start -->

**Automatically filling that doesn't match the scope**

Automatic input using `liff.$commonProfile.fill()` is performed using the `data-liff-autocomplete` attribute of the form. At this time, the value specified in the `data-liff-autocomplete` attribute of the form must match the scope of the profile information obtained (`family-name`, `tel`, `bday-year`, etc.)

For example, if you want to automatically fill in a form after retrieving the year of birth (`bday-year`), month of birth (`bday-month`), and day of birth (`bday-day`) information and then process it into a format like `20110623`, you can use `document.getElementById().value` or `document.querySelector().value` instead of `liff.$commonProfile.fill()`.

<!-- tip end -->

_Example of automatically filling the family name, phone number, and gender as they were obtained_

<!-- tab start `javascript` -->

```javascript
// HTML
<input type="text" data-liff-autocomplete="family-name" />
<input type="tel" data-liff-autocomplete="tel" />
<select data-liff-autocomplete="sex-enum">
  <option value="0">男性</option>
  <option value="1">女性</option>
  <option value="2">回答なし</option>
  <option value="3">その他</option>
</select>

// JavaScript
const { data, error } = await liff.$commonProfile.get([
  "family-name",
  "tel",
  "sex-enum",
]);

liff.$commonProfile.fill(data);
```

<!-- tab end -->

_Example of automatically filling some of the common profile information that has been obtained in a slightly different format_

<!-- tab start `javascript` -->

```javascript
// HTML
<input type="text" data-liff-autocomplete="bday-year" />
<input type="text" data-liff-autocomplete="bday-month" />
<input type="text" data-liff-autocomplete="bday-day" />

// JavaScript
const { data, error } = await liff.$commonProfile.get([
  "bday-year",
  "bday-month",
  "bday-day",
]);

const year = data["bday-year"];
const month = data["bday-month"];
const day = data["bday-day"];

// If the month or day is one digit, pad with 0s to
const formattedMonth = month.toString().padStart(2, '0');
const formattedDay = day.toString().padStart(2, '0');

// Automatically fills the value after processing
liff.$commonProfile.fill({
  "bday-year": year,
  "bday-month": formattedMonth,
  "bday-day": formattedDay,
});
```

<!-- tab end -->

#### Syntax 

```javascript
liff.$commonProfile.fill(profile);
```

#### Arguments 

<!-- parameter start (props: required) -->

profile

Partial\<CommonProfile\>

Specify the profile information that is automatically fill into the form as a `Partial<CommonProfile>` type.

For information on the `scopes`, that can be specified, see [The `scopes` parameters that can be specified and its return value](https://developers.line.biz/en/docs/line-mini-app/quick-fill/overview/#common-profile-scope).

<!-- parameter end -->

#### Return value 

None

## In-app purchase (Client) 

<!-- tip start -->

**Application required to use the in-app purchase feature**

To use the in-app purchase feature, you must apply for use. For more information, see [In-app purchase overview](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/overview/) in the LINE MINI App documentation.

<!-- tip end -->

### liff.iap.getPlatformProducts() 

Gets a list of items available for purchase via in-app purchase.

_Example_

<!-- tab start `javascript` -->

```javascript
const productIds = ["iap_ln_002", "iap_ln_003"];
liff.iap
  .getPlatformProducts({ productIds })
  .then((products) => {
    console.log(products);
  })
  .catch((err) => {
    console.error(err);
  });
```

<!-- tab end -->

#### Syntax 

```javascript
liff.iap.getPlatformProducts({ productIds });
```

#### Arguments 

<!-- parameter start (props: required) -->

productIds

Array of strings

Array of [product IDs](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/iap-product-id/) for items you want to retrieve

<!-- parameter end -->

#### Return value 

A `Promise` object is returned. When the `Promise` object is resolved, an object with the product ID as a key and the following properties is passed:

<!-- parameter start -->

currency

String

Currency code in ISO 4217 format. Returned in the currency localized to the region of the app store the user is using.

<!-- parameter end -->
<!-- parameter start -->

price

Number

Price of the item. Returned in the currency localized to the region of the app store the user is using.

<!-- parameter end -->
<!-- parameter start -->

productName

String

Name of the item. Returned in the representation localized to the region of the app store the user is using.

<!-- parameter end -->

_Example return value_

<!-- tab start `json` -->

```json
{
  "iap_ln_002": {
    "currency": "JPY",
    "price": 100,
    "productName": "LINE Purchase 100"
  }
}
```

<!-- tab end -->

#### Error response 

When the `Promise` is rejected, a [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-error-object) is passed.

Possible errors include the following:

| Error message | Description |
| --- | --- |
| Need access_token for api call, Please login first | The user is not logged in. |
| In-App Purchase is not allowed in external browser | The method was executed in an external browser. |
| In-App Purchase is not allowed in this LIFF app | The LINE MINI App being run by the user does not support in-app purchase. |

### liff.iap.requestConsentAgreement() 

Requests user consent for the [Terms of Use: LINE In-App Purchase System](https://terms.line.me/line_iap_tou_1?lang=en).

If the user has not yet agreed to the "Terms of Use: LINE In-App Purchase System" or if new consent is required, a consent screen will be displayed.

<!-- tip start -->

**Always check the latest consent status**

If the [Terms of Use: LINE In-App Purchase System](https://terms.line.me/line_iap_tou_1?lang=en) are updated, re-consent will be required. Before starting in-app purchase, be sure to call this method to check the latest consent status.

<!-- tip end -->

#### Syntax 

```javascript
await liff.iap.requestConsentAgreement();
```

#### Arguments 

None

#### Return value 

A `Promise` object is returned.

- Resolves if the user agrees.
- Rejects with an error object if the user doesn't agree, or if the operation fails due to a network issue, a problem on the user's device, or an internal error on the LINE Platform.

#### Error response 

When the `Promise` is rejected, a [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-error-object) is passed.

Possible errors include the following:

| Error message | Description |
| --- | --- |
| The user did not agree to the terms. | The user did not agree to the [Terms of Use: LINE In-App Purchase System](https://terms.line.me/line_iap_tou_1?lang=en) . |
| Need access_token for api call, Please login first | The user is not logged in. |
| In-App Purchase is not allowed in external browser | The method was executed in an external browser. |
| In-App Purchase is not allowed in this LIFF app | The LINE MINI App being run by the user does not support in-app purchase. |

_Error response example_

<!-- tab start `json` -->

```json
{
  "code": "TERMS_AGREEMENT_ERROR",
  "message": "The user did not agree to the terms."
}
```

<!-- tab end -->

### liff.iap.createPayment() 

Launches the app store payment confirmation screen (App Store, Google Play) and starts the purchase transaction.

#### Syntax 

```javascript
liff.iap.createPayment({ productId, orderId });
```

#### Arguments 

<!-- parameter start (props: required) -->

productId

String

Pre-defined [product ID](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/iap-product-id/)

<!-- parameter end -->

<!-- parameter start (props: required) -->

orderId

String

Order ID obtained from the "[Reserve purchase](https://developers.line.biz/en/reference/line-mini-app/#reserve-purchase)" endpoint

<!-- parameter end -->

#### Return value 

Returns a `Promise<void>` object.

- Resolves if the purchase completes successfully.
- Rejects with an error object if the purchase is canceled, or if the operation fails due to a network issue, a problem on the user's device, or an internal error on the LINE Platform.

#### Error response 

When the `Promise` is rejected, a [`LiffError`](https://developers.line.biz/en/reference/liff/#liff-error-object) is passed.

Possible errors include the following:

| Error message | Description |
| --- | --- |
| Need access_token for api call, Please login first | The user is not logged in. |
| In-App Purchase is not allowed in external browser | The method was executed in an external browser. |
| In-App Purchase is not allowed in this LIFF app | The LINE MINI App being run by the user does not support in-app purchase. |

## In-app purchase (Server) 

<!-- tip start -->

**Application required to use the in-app purchase feature**

To use the in-app purchase feature, you must apply for use. For more information, see [In-app purchase overview](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/overview/) in the LINE MINI App documentation.

<!-- tip end -->

### Response headers 

In-app purchase responses include the following HTTP header. Save it to logs so you can reference them in future inquiries to LY Corporation.

| Response header   | Description                                        |
| ----------------- | -------------------------------------------------- |
| x-line-request-id | Request ID. An ID that is issued for each request. |

### Error response 

When the HTTP status code is in the 4xx or 5xx, a response body containing the following JSON data is returned:

<!-- parameter start (props: required) -->

errorCode

String

Error code

<!-- parameter end -->
<!-- parameter start (props: required) -->

message

String

Error message

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

details

array

Error details

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

details\[].message

String

Detailed message

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

details\[].property

String

Location where error occurred

<!-- parameter end -->

_Error response example_

When the HTTP status code is in the 4xx

<!-- tab start `json` -->

```json
{
  "errorCode": "VALIDATION_ERROR",
  "message": "Request validation failed.",
  "details": [
    {
      "message": "'clientOs' must be 'android' or 'ios'. Actually received: 'INVALID'",
      "property": "clientOs"
    }
  ]
}
```

<!-- tab end -->

When the HTTP status code is in the 5xx

<!-- tab start `json` -->

```json
{
  "errorCode": "INTERNAL_SERVER_ERROR",
  "message": "An internal server error occurred."
}
```

<!-- tab end -->

### Reserve purchase 

Reserve the purchase before starting the app store payment.

The order ID (`orderId`) included in the [response](https://developers.line.biz/en/reference/line-mini-app/#reserve-purchase-response) is also included in the [purchase complete event](https://developers.line.biz/en/reference/line-mini-app/#purchase-complete-event). The order ID is required for inquiries and investigations to LY Corporation, so be sure to save it.

Also, a successful reservation does not guarantee purchase completion, so grant items based on the purchase complete event.

_Request example_

<!-- tab start `shell` -->

```sh
curl -X POST https://api.line.me/iap/v1/product/reserve \
-H "Authorization: Bearer {UserAccessToken}" \
-H "Content-Type: application/json" \
-d '{
"clientIp": "192.168.1.1",
"clientOs": "android",
"productId": "iap_ln_002",
"shopProductName": "Premium Package"
}'

```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/iap/v1/product/reserve`

#### Request headers 

<!-- parameter start (props: required) -->

Authorization

Bearer `{user access token}`

The current user's access token. Can be obtained with the [`liff.getAccessToken()`](https://developers.line.biz/en/reference/liff/#get-access-token) method.

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->

#### Request body 

<!-- parameter start (props: required) -->

clientIp

String

The IP address of the user's device obtained from the server. Specify in IPv4 or IPv6 format.

<!-- parameter end -->
<!-- parameter start (props: required) -->

clientOs

String

The value obtained from the [`liff.getOS()`](https://developers.line.biz/en/reference/liff/#get-os) method. Either `ios` or `android`.

<!-- parameter end -->
<!-- parameter start (props: required) -->

productId

String

The [product ID](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/iap-product-id/) of the item to be purchased.

<!-- parameter end -->
<!-- parameter start (props: required) -->

shopProductName

String

The item name displayed in the purchase history.

Emojis and symbols can't be used. Set an appropriate value so that users can recognize the item they purchased.

Maximum characters: 20 (UTF-16)

<!-- parameter end -->

#### Response 

Returns a JSON object containing the status code `200` and the following information:

<!-- parameter start -->

orderId

String

Order ID.

<!-- parameter end -->

_Response example_

<!-- tab start `json` -->

```json
{ "orderId": "T2025020710000002126002" }
```

<!-- tab end -->

#### Error response 

For more information on error response format, see [Error response](https://developers.line.biz/en/reference/line-mini-app/#iap-error-responses).

Errors that may occur in addition to general ones include the following:

| Error code | Description |
| --- | --- |
| VALIDATION_ERROR | Request constraints are not met. For example, a value other than `ios` or `android` is passed to `clientOs`. |
| WEBHOOK_URL_IS_NOT_SET | The webhook URL to receive payment completion notifications is not set. |
| PRODUCT_ID_NOT_FOUND | The requested [product ID](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/iap-product-id/) does not exist. |
| BLOCKED_USER | This user has been determined to be a fraudulent user by the LINE Platform. Requests related to this user can't be processed. |
| INTERNAL_SERVER_ERROR | A temporary issue has occurred on the LINE Platform. For endpoints where retries are possible, retry using exponential backoff or similar methods. |
| TERMS_AGREEMENT_ERROR | Occurs when the latest terms and conditions have not been agreed to by this user in "[Obtain user consent for in-app purchase](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#get-user-consent)". |

_Error response example_

<!-- tab start `json` -->

```json
{
  "errorCode": "VALIDATION_ERROR",
  "message": "Request validation failed.",
  "details": [
    {
      "message": "'clientOs' must be 'android' or 'ios'. Actually received: 'INVALID'",
      "property": "clientOs"
    }
  ]
}
```

<!-- tab end -->

### Get webhook event history 

Gets the history of webhook events sent by the LINE Platform. You can retrieve up to 100 events at a time using cursor-based pagination.

The sort order is in ascending order of the date and time when the LINE Platform started sending webhook events.

You can only retrieve webhook events sent in the past 7 days. Currently, only [purchase complete events](https://developers.line.biz/en/reference/line-mini-app/#purchase-complete-event) are available, and [refund events](https://developers.line.biz/en/reference/line-mini-app/#refund-event) will be supported in the future.

_Example request_

<!-- tab start `shell` -->

```sh
curl "https://api.line.me/iap/v1/webhook/events?startEpochSeconds=1747330438&endEpochSeconds=1747708454&pageSize=10" \
  -H "Authorization: Bearer {ChannelAccessToken}"

```

<!-- tab end -->

#### HTTP request 

`GET https://api.line.me/iap/v1/webhook/events`

#### Request headers 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`\
For more information, see [Channel access token](https://developers.line.biz/en/docs/basics/channel-access-token/) in the LINE Platform Basics.

<!-- parameter end -->

#### Query parameters 

<!-- parameter start (props: required) -->

startEpochSeconds

Number

Specifies the start date and time of the period for which you want to retrieve webhook event history. The specified date and time are included in the retrieval target. Specify a UNIX time (in seconds) within the past 7 days.

<!-- parameter end -->
<!-- parameter start (props: required) -->

endEpochSeconds

Number

Specifies the end date and time of the period for which you want to retrieve webhook event history. The specified date and time are included in the retrieval target. Specify a UNIX time (in seconds) within the past 7 days.

<!-- parameter end -->
<!-- parameter start -->

cursor

String

Cursor for the webhook event page.\
Do not specify this in the first request. For the second and subsequent requests, you can retrieve the subsequent webhook events by specifying the `nextCursor` value included in the response from the previous request.

<!-- parameter end -->
<!-- parameter start (props: required) -->

pageSize

Number

Number of webhook events per page.<br> <ul><li>Minimum value: 1</li><li>Maximum value: 100</li></ul>

<!-- parameter end -->
<!-- parameter start -->

status

String

Status of the webhook events you want to retrieve. Specify one of the following:

- `SUCCESS`: Retrieves the history of webhook events received successfully.
- `FAILED`: Retrieves the history of webhook events that failed to be received.

If not specified, the history of all webhook events is retrieved regardless of whether the receipt was successful or failed.

<!-- parameter end -->

<!-- note start -->

**Do not change parameters other than cursor during pagination**

During pagination, make requests without changing parameters other than `cursor`. If you want to change parameters, start from the first page again.

<!-- note end -->

#### Response 

When successful, returns a JSON object with status code `200` and the information below.

<!-- parameter start -->

events

Array

List of webhook events.

<!-- parameter end -->
<!-- parameter start -->

events\[].transactionType

String

Always returns `PRODUCT`.

<!-- parameter end -->
<!-- parameter start -->

events[].event

Object

[Webhook event object](https://developers.line.biz/en/reference/line-mini-app/#purchase-complete-payload).

<!-- parameter end -->
<!-- parameter start (props: annotation="Not always included") -->

nextCursor

String

Cursor for the next page.\
If the next page does not exist, the value is `null`.

<!-- parameter end -->

_Example response_

<!-- tab start `json` -->

```json
{
  "events": [
    {
      "transactionType": "PRODUCT",
      "event": {
        "type": "purchaseComplete",
        "orderId": "T2025020710000002126002",
        "productId": "iap_ln_002",
        "userId": "U91FC5A...",
        "purchaseTimestamp": 1738672496,
        "channelId": "12345..."
      }
    }
  ],
  "nextCursor": "MTY3NjU0"
}
```

<!-- tab end -->

#### Error responses 

For more information on error response format, see [Error response](https://developers.line.biz/en/reference/line-mini-app/#iap-error-responses).

Errors that may occur in addition to general ones include the following:

| Error code | Description |
| --- | --- |
| VALIDATION_ERROR | Request constraints are not met. For example, a value other than `SUCCESS` or `FAILED` is passed to `status`. |
| INTERNAL_SERVER_ERROR | A temporary issue has occurred on the LINE Platform. For endpoints that allow retries, retry using exponential backoff or similar methods. |

## In-app purchase webhook event object 

<!-- tip start -->

**Application required to use the in-app purchase feature**

To use the in-app purchase feature, you must apply for use. For more information, see [In-app purchase overview](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/overview/) in the LINE MINI App documentation.

<!-- tip end -->

### Verify signature 

When your LINE MINI App server receives a webhook request, verify the signature included in the request header before processing the webhook event. This verification step is important to confirm that the webhook came from the LINE Platform and wasn't tampered with during transmission.

For more information, see [Verify webhook signature](https://developers.line.biz/en/docs/messaging-api/verify-webhook-signature/) in the Messaging API documentation.

### Purchase complete event 

This event occurs when a user purchases a reserved item at an app store (App Store, Google Play) and the payment is settled by LY Corporation. The webhook payload contains information about the purchased item.

#### Webhook payload 

<!-- parameter start -->

type

String

The type of webhook event. \
`purchaseComplete` is specified.

<!-- parameter end -->
<!-- parameter start -->

orderId

String

The ID of the order purchased by the user. Included in the response of the "[Reserve purchase](https://developers.line.biz/en/reference/line-mini-app/#reserve-purchase)" endpoint.

<!-- parameter end -->
<!-- parameter start -->

productId

String

The product ID ([`productId`](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/iap-product-id/)) of the item purchased by the user.

<!-- parameter end -->
<!-- parameter start -->

userId

String

The user ID of the user who made the purchase.

<!-- parameter end -->
<!-- parameter start -->

purchaseTimestamp

number

The time when the payment was completed on the LINE Platform. The unit is UNIX time (in seconds).

This time is not the time when the user actually completed the payment.

<!-- parameter end -->
<!-- parameter start -->

channelId

String

The channel ID of the LINE MINI App channel.

<!-- parameter end -->

_Example_

<!-- tab start `json` -->

```json
{
  "type": "purchaseComplete",
  "orderId": "T2025020710000002126002",
  "productId": "iap_ln_002",
  "userId": "U91FC5A...",
  "purchaseTimestamp": 1738672496,
  "channelId": "12345..."
}
```

<!-- tab end -->

### Refund event 

This event occurs when a refund was issued for an item purchased by a user at an app store (App Store, Google Play). The event contains information about the item refunded.

#### Webhook payload 

<!-- parameter start -->

type

String

The type of webhook event. \
`refundComplete` is specified.

<!-- parameter end -->
<!-- parameter start -->

orderId

String

The ID of the order that was refunded by the user. Included in the response of the [Reserve purchase](https://developers.line.biz/en/reference/line-mini-app/#reserve-purchase) endpoint.

<!-- parameter end -->
<!-- parameter start -->

productId

String

The product ID ([`productId`](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/iap-product-id/)) of the item that was refunded by the user.

<!-- parameter end -->
<!-- parameter start -->

userId

String

The user ID of the user who requested the refund.

<!-- parameter end -->
<!-- parameter start -->

purchaseTimestamp

number

The time when the refunded item was purchased. The unit is UNIX time (in seconds).

Matches the `purchaseTimestamp` of the [purchase complete event](https://developers.line.biz/en/reference/line-mini-app/#purchase-complete-event). This time is not when the user actually completed the refund.

<!-- parameter end -->
<!-- parameter start -->

channelId

String

The channel ID of the LINE MINI App channel.

<!-- parameter end -->

_Example_

<!-- tab start `json` -->

```json
{
  "type": "refundComplete",
  "orderId": "T2025020710000002126002",
  "productId": "iap_ln_002",
  "userId": "U91FC5A...",
  "purchaseTimestamp": 1738672496,
  "channelId": "12345..."
}
```

<!-- tab end -->
