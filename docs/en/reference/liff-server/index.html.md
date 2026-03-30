# Server API

<!-- tip start -->

**Version number differs from LIFF SDK**

The version number of the server API is different from that of LIFF SDK. The currently released version of LIFF SDK is `v2`, but the version of the server API is `v1`.

<!-- tip end -->

## Server API 

### Preparing a channel access token 

The LIFF server API is used to operate the LIFF apps on the LINE Login channel. Therefore, in order to use the server API, a channel access token for the LINE Login channel is required. The types of channel access tokens available are [short-lived channel access tokens](https://developers.line.biz/en/reference/messaging-api/#issue-shortlived-channel-access-token) or [stateless channel access tokens](https://developers.line.biz/en/reference/messaging-api/#issue-stateless-channel-access-token).

### Adding the LIFF app to a channel 

Adds the LIFF app to a channel. You can add up to 30 LIFF apps on one channel.

<!-- tip start -->

**We recommend creating a LIFF app as a LINE MINI App**

In the future, LIFF and the LINE MINI App will be integrated into a single brand. As a result of this integration, LIFF will be integrated into the LINE MINI App. For this reason, we recommend that you create a new LIFF app as a LINE MINI App. For more information, see the news from [February 12, 2025](https://developers.line.biz/en/news/2025/02/12/line-mini-app/).

<!-- tip end -->

_Example_

<!-- tab start `shell` -->

```sh
curl -X POST https://api.line.me/liff/v1/apps \
-H "Authorization: Bearer {channel access token}" \
-H "Content-Type: application/json" \
-d '{
    "view": {
        "type": "full",
        "url": "https://example.com/myservice"
    },
    "description": "Service Example",
    "features": {
        "qrCode": true
    },
    "permanentLinkPattern": "concat",
    "scope": ["profile", "chat_message.write"],
    "botPrompt": "none"
}'
```

<!-- tab end -->

#### HTTP request 

`POST https://api.line.me/liff/v1/apps`

#### Request headers 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`\
For more information, see [Preparing a channel access token](https://developers.line.biz/en/reference/liff-server/#preparing-channel-access-token).

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->

#### Request body 

<!-- parameter start (props: required) -->

view.type

String

Size of the LIFF app view. Specify one of these values:

- `compact`
- `tall`
- `full`

For more information, see [Size of the LIFF app view](https://developers.line.biz/en/docs/liff/overview/#screen-size).

<!-- parameter end -->
<!-- parameter start (props: required) -->

view.url

String

Endpoint URL. This is the URL of the web app that implements the LIFF app (e.g. `https://example.com`). Used when the LIFF app is launched using the LIFF URL.

The URL scheme must be **https**. URL fragments (#URL-fragment) can't be specified.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

view.moduleMode

Boolean

`true` to use the LIFF app in modular mode. When in modular mode, the action button in the header is not displayed.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

description

String

Name of the LIFF app.

The LIFF app name can't include "LINE" or similar strings, or inappropriate strings.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

features.qrCode

Boolean

`true` to use the 2D code reader in the LIFF app. `false` otherwise. The default value is `false`.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

permanentLinkPattern

String

How additional information in LIFF URLs is handled. Specify `concat`.

For more information, see [Opening a LIFF app](https://developers.line.biz/en/docs/liff/opening-liff-app/) in the LIFF documentation.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

scope

Array of strings

Array of scopes required for some LIFF SDK methods to function.

- `openid`
- `email`
- `profile`
- `chat_message.write`

The default value is `["profile", "chat_message.write"]`. For more information on each scope, see [Adding the LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/#registering-liff-app) in the LIFF documentation.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

botPrompt

String

Specify the setting for [add friend option](https://developers.line.biz/en/docs/line-login/link-a-bot/) with one of the following values:

- `normal`: Display the option to add the LINE Official Account as a friend in the channel consent screen.
- `aggressive`: Display a screen with the option to add the LINE Official Account as a friend after the channel consent screen.
- `none`: Don't display the option to add the LINE Official Account as a friend.

The default value is `none`.

<!-- parameter end -->

#### Response 

Returns status code `200` and a JSON object with the following properties.

<!-- parameter start -->

liffId

String

LIFF app ID

<!-- parameter end -->

_Example_

<!-- tab start `json` -->

```json
{
  "liffId": "{liffId}"
}
```

<!-- tab end -->

#### Error response 

One of the following status codes is returned.

| Status code | Description |
| --- | --- |
| 400 | This status code means one of the following:<ul><li>The request contains an invalid value.</li><li>The maximum number of LIFF apps that can be added to the channel has been reached.</li></ul> |
| 401 | Authentication failed. |

### Update LIFF app settings 

Partially updates LIFF app settings.

_Example_

<!-- tab start `shell` -->

```sh
curl -X PUT https://api.line.me/liff/v1/apps/{liffId} \
-H "Authorization: Bearer {channel access token}" \
-H "Content-Type: application/json" \
-d '{
    "view": {
        "url": "https://new.example.com"
    }
}'
```

<!-- tab end -->

#### HTTP request 

`PUT https://api.line.me/liff/v1/apps/{liffId}`

#### Request headers 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`\
For more information, see [Preparing a channel access token](https://developers.line.biz/en/reference/liff-server/#preparing-channel-access-token).

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->

#### Path parameters 

<!-- parameter start (props: required) -->

liffId

ID of the LIFF app to be updated

<!-- parameter end -->

#### Request body 

<!-- parameter start (props: optional) -->

view.type

String

Size of the LIFF app view. Specify one of these values:

- `compact`
- `tall`
- `full`

For more information, see [Size of the LIFF app view](https://developers.line.biz/en/docs/liff/overview/#screen-size).

<!-- parameter end -->
<!-- parameter start (props: optional) -->

view.url

String

Endpoint URL. This is the URL of the web app that implements the LIFF app (e.g. `https://example.com`). Used when the LIFF app is launched using the LIFF URL.

The URL scheme must be **https**. URL fragments (#URL-fragment) can't be specified.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

view.moduleMode

Boolean

`true` to use the LIFF app in modular mode. When in modular mode, the action button in the header is not displayed.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

description

String

Name of the LIFF app.

The LIFF app name can't include "LINE" or similar strings, or inappropriate strings.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

features.qrCode

Boolean

`true` to use the 2D code reader in the LIFF app. `false` otherwise.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

permanentLinkPattern

String

How additional information in LIFF URLs is handled. Specify `concat`.

For more information, see [Opening a LIFF app](https://developers.line.biz/en/docs/liff/opening-liff-app/) in the LIFF documentation.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

scope

Array of strings

Array of scopes required for some LIFF SDK methods to function.

- `openid`
- `email`
- `profile`
- `chat_message.write`

For more information on each scope, see [Adding the LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/#registering-liff-app) in the LIFF documentation.

<!-- parameter end -->
<!-- parameter start (props: optional) -->

botPrompt

String

Specify the setting for [add friend option](https://developers.line.biz/en/docs/line-login/link-a-bot/) with one of the following values:

- `normal`: Display the option to add the LINE Official Account as a friend in the channel consent screen.
- `aggressive`: Display a screen with the option to add the LINE Official Account as a friend after the channel consent screen.
- `none`: Don't display the option to add the LINE Official Account as a friend.

<!-- parameter end -->

<!-- note start -->

**Note**

Only the properties specified in the request body are updated.

<!-- note end -->

#### Response 

Status code `200` is returned.

#### Error response 

One of the following status codes is returned.

| Status code | Description |
| --- | --- |
| 400 | The request contains an invalid value. |
| 401 | Authentication failed. |
| 404 | This status code means one of the following:<ul><li>The specified LIFF app does not exist.</li><li>The specified LIFF app has been added to another channel.</li></ul> |

### Get all LIFF apps 

Gets information on all the LIFF apps added to the channel.

_Example_

<!-- tab start `shell` -->

```sh
curl -X GET https://api.line.me/liff/v1/apps \
-H "Authorization: Bearer {channel access token}"
```

<!-- tab end -->

#### HTTP request 

`GET https://api.line.me/liff/v1/apps`

#### Request headers 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`\
For more information, see [Preparing a channel access token](https://developers.line.biz/en/reference/liff-server/#preparing-channel-access-token).

<!-- parameter end -->

#### Response 

Returns status code `200` and a JSON object with these properties.

<!-- parameter start -->

apps

Array of objects

Array of LIFF app objects

<!-- parameter end -->
<!-- parameter start -->

apps\[].liffId

String

LIFF app ID

<!-- parameter end -->
<!-- parameter start -->

apps[].view.type

String

Size of the LIFF app view. One of these values:

- `compact`
- `tall`
- `full`

For more information, see [Size of the LIFF app view](https://developers.line.biz/en/docs/liff/overview/#screen-size).

<!-- parameter end -->
<!-- parameter start -->

apps[].view.url

String

Endpoint URL. This is the URL of the web app that implements the LIFF app (e.g. `https://example.com`). Used when the LIFF app is launched using the LIFF URL.

<!-- parameter end -->
<!-- parameter start -->

apps[].view.moduleMode

Boolean

`true` to use the LIFF app in modular mode. When in modular mode, the action button in the header is not displayed.

<!-- parameter end -->
<!-- parameter start -->

apps\[].description

String

Name of the LIFF app

<!-- parameter end -->
<!-- parameter start -->

apps[].features.ble

Boolean

`true` if the LIFF app supports Bluetooth® Low Energy for LINE Things. `false` otherwise.

<!-- parameter end -->
<!-- parameter start -->

apps[].features.qrCode

Boolean

`true` if the 2D code reader can be launched in the LIFF app. `false` otherwise.

<!-- parameter end -->
<!-- parameter start -->

apps\[].permanentLinkPattern

String

How additional information in LIFF URLs is handled. `concat` is returned.

For more information, see [Opening a LIFF app](https://developers.line.biz/en/docs/liff/opening-liff-app/) in the LIFF documentation.

<!-- parameter end -->
<!-- parameter start -->

apps\[].scope

Array of strings

Scopes of the LIFF app.

- `openid`
- `email`
- `profile`
- `chat_message.write`

For more information on each scope, see [Adding the LIFF app to your channel](https://developers.line.biz/en/docs/liff/registering-liff-apps/#registering-liff-app) in the LIFF documentation.

<!-- parameter end -->
<!-- parameter start -->

apps\[].botPrompt

String

The setting for [add friend option](https://developers.line.biz/en/docs/line-login/link-a-bot/).

- `normal`: Display the option to add the LINE Official Account as a friend in the channel consent screen.
- `aggressive`: Display a screen with the option to add the LINE Official Account as a friend after the channel consent screen.
- `none`: Don't display the option to add the LINE Official Account as a friend.

<!-- parameter end -->

_Example_

<!-- tab start `json` -->

```json
{
  "apps": [
    {
      "liffId": "{liffId}",
      "view": {
        "type": "full",
        "url": "https://example.com/myservice"
      },
      "description": "Happy New York",
      "permanentLinkPattern": "concat"
    },
    {
      "liffId": "{liffId}",
      "view": {
        "type": "tall",
        "url": "https://example.com/myservice2"
      },
      "features": {
        "ble": true,
        "qrCode": true
      },
      "permanentLinkPattern": "concat",
      "scope": ["profile", "chat_message.write"],
      "botPrompt": "none"
    }
  ]
}
```

<!-- tab end -->

#### Error response 

One of the following status codes is returned.

| Status code | Description                          |
| ----------- | ------------------------------------ |
| 401         | Authentication failed.               |
| 404         | There is no LIFF app on the channel. |

### Delete LIFF app from a channel 

Deletes a LIFF app from a channel.

_Example_

<!-- tab start `shell` -->

```sh
curl -X DELETE https://api.line.me/liff/v1/apps/{liffId} \
-H "Authorization: Bearer {channel access token}"
```

<!-- tab end -->

#### HTTP request 

`DELETE https://api.line.me/liff/v1/apps/{liffId}`

#### Request headers 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`\
For more information, see [Preparing a channel access token](https://developers.line.biz/en/reference/liff-server/#preparing-channel-access-token).

<!-- parameter end -->

#### Path parameters 

<!-- parameter start (props: required) -->

liffId

ID of the LIFF app to be deleted

<!-- parameter end -->

#### Response 

Status code `200` is returned.

#### Error response 

One of the following status codes is returned.

| Status code | Description |
| --- | --- |
| 401 | Authentication failed. |
| 404 | This status code means one of the following:<ul><li>The specified LIFF app does not exist.</li><li>The specified LIFF app has been added to another channel.</li></ul> |
