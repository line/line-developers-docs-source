# User account linking

You as a service provider can let your service users **securely** link their LINE account to the account for your service. To link accounts, the users must have your LINE Official Account as a friend. Leading users to link their LINE account to your service account enables you to utilize the user data from your service on LINE. With the user data, you can enrich the user experience on your LINE Official Account.

If a user links their LINE account to your service account, you can utilize your LINE Official Account to the user's benefit. For instance, if your service is a shopping site, you can:

- Send a LINE message to the user from your LINE Official Account when the user makes a purchase on your shopping site.
- Let users make an order from a chat with your LINE Official Account.

You can link accounts through LINE Login, but then you need to have a LINE Login channel. With the Messaging API, you can link accounts without a LINE Login channel.

## Account linking sequence 

The sequence to link a user's LINE account to your service account is as follows:

![](https://developers.line.biz/media/messaging-api/linking-accounts/sequence.png)

1. Your bot server calls the API that issues a link token with the user's LINE user ID.
1. The LINE Platform issues and returns a link token to your bot server.
1. Your bot server calls the Messaging API to send a linking URL to the user.
1. The LINE Platform sends the user the linking URL.
1. The user accesses the linking URL.
1. Your web server sends out your service's login page.
1. The user enters their credentials for your service.
1. Your web server gets the user ID for your service and uses the ID to generate a nonce (a number used once).
1. Your web server redirects the user to the account-linking endpoint.
1. The user accesses the account-linking endpoint.
1. The LINE Platform sends a webhook event that contains the LINE user ID and nonce to your bot server.
1. Your bot server uses the nonce to get the user ID of your service.

You can implement on your own to link accounts without the help of the Messaging API. However, your users may be exposed to security issues with account linking, so be aware if you implement this on your own. For instance, an attacker may send a URL to a user to link the attacker's LINE account to the user's service account. The Messaging API protects the user from such attacks. The Messaging API checks if the user who initiated to issue the linking URL is the real owner of the LINE account to link.

## Linking accounts 

To link your service's user account with LINE's user account, do as instructed below:

### 1. Issue a link token 

You need a link token to link a user's LINE and your service accounts. To [issue a link token](https://developers.line.biz/en/reference/messaging-api/#issue-link-token), send an HTTP POST request to the `/bot/user/{userId}/linkToken` endpoint.

```sh
curl -X POST https://api.line.me/v2/bot/user/{userId}/linkToken \
-H 'Authorization: Bearer {channel access token}'
```

If the request succeeds, the endpoint returns a status code `200` with a link token. The token is for one-time use only and valid for 10 minutes.

```sh
{
  "linkToken": "NMZTNuVrPTqlr2IF8Bnymkb7rXfYv5EY"
}
```

### 2. Send the linking URL to the user 

Your bot server sends a URL for the user to link accounts. For example, the linking URL can be specified in the [URI action](https://developers.line.biz/en/docs/messaging-api/actions/#uri-action) object of a [template message](https://developers.line.biz/en/docs/messaging-api/message-types/#template-messages). In the linking URL, add a query parameter with the linking token from step 1.

Here is an example request to send a message with a linking URL to the user.

```sh
curl -v -X POST https://api.line.me/v2/bot/message/push \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {channel access token}' \
-d '{
    "to": "{user id}",
    "messages": [{
        "type": "template",
        "altText": "Account Link",
        "template": {
            "type": "buttons",
            "text": "Account Link",
            "actions": [{
                "type": "uri",
                "label": "Account Link",
                "uri": "http://example.com/link?linkToken=xxx"
            }]
        }
    }]
}'
```

### 3. Get the user's ID of your service 

When the user accesses the URL, show the user the login page for your service. You can get the user's ID for your service when the user logs into your service.

### 4. Generate a nonce and redirect the user to the LINE Platform 

Generate a nonce with the user ID from step 3. The nonce must be:

- A string for a single-use and difficult to predict. For security, don't use predictable values, such as user IDs used in your services.
- Between 10 and 255 characters long.

When generating a random value for the nonce, consider these recommendations:

- Use a secure random number generator to generate the nonce.
- Make the nonce be at least 128 bits (16 bytes) long.
- Encode the nonce in Base64.

After you generate a nonce, link the nonce with the user ID of your service, and save the information. Then redirect the user to the URL below.

```sh
https://access.line.me/dialog/bot/accountLink?linkToken={link token}&nonce={nonce}
```

When the user accesses this endpoint, the LINE Platform checks if the user is the user the linking token was issued for. By the result of the verification, the LINE Platform acts differently as listed below.

- User verification succeeds: The LINE Platform sends an [account link event](https://developers.line.biz/en/reference/messaging-api/#account-link-event) to your bot server. The `result` property value of the event is `ok`.
- User verification fails: The LINE Platform sends an [account link event](https://developers.line.biz/en/reference/messaging-api/#account-link-event) to your bot server. The `result` property value of the event is `failed`.
- The linking token is invalid: If the linking token is expired or was used before, the LINE Platform sends no webhook event and shows an error to the user.

### 5. Linking accounts 

If the user verification succeeds from step 4, link the user's accounts. The account link event object contains the user's LINE user ID and the nonce. Use this nonce to get the user's ID for your service that you linked and saved earlier. Account linking is complete when you link the user's ID for your service to the user's LINE user ID.

## Unlinking accounts 

You must allow users to unlink accounts if they linked their LINE account to your service account:

- You must let users to unlink accounts at all times.
- You must inform users at the time of linking accounts that they can unlink the accounts.

For example, the Messaging API lets you customize [rich menus](https://developers.line.biz/en/docs/messaging-api/rich-menus-overview/) by user. You can display a menu to link accounts to those who are yet to link accounts. Likewise, you can display a menu to unlink accounts to those who linked their accounts.

## Learn more 

- [Messaging API reference](https://developers.line.biz/en/reference/messaging-api/)
