# Channel access token

The channel access token is an opaque string that is used to verify that the application attempting to use the [channel](https://developers.line.biz/en/glossary/#channel) has permission to use the channel. With a channel access token, you can use many useful features offered by [LINE Platform](https://developers.line.biz/en/glossary/#line-platform), such as the Messaging API.

On this page, you'll learn the basics of channel access tokens, such as an overview and types. By reading this page, you'll be able to more easily develop using the features of the LINE Platform.

<!-- table of contents -->

## What is a channel 

First, a brief explanation of channels. Channels are the communication paths used to access the features provided by the LINE Platform. For example, there are the following channels:

- Messaging API channel
- LINE Login channel
- LINE MINI App channel

The channel access token is used, for example, when an application uses the Messaging API channel to verify that the user is authorized to use the channel.

![Channel](https://developers.line.biz/media/basics/channel.png)

## Why use channel access tokens 

Why use a channel access token at all? In some systems, the most common way to verify that a user is authorized is to use an ID and password, in which case the application enters the ID and password when using the channel.

In general, however, the channel will be used many times during the course of providing services. Since it's impractical for a channel user to enter their ID and password each time an application uses the channel, a channel access token is used instead. Channel access tokens allow channel users to use the channel without having to enter their ID and password.

![Channel access token](https://developers.line.biz/media/basics/channel-access-token.png)

<!-- note start -->

**Revoke any channel access tokens suspected of being compromised**

Channel access tokens are used to verify that an application is authorized to use a channel. This means that if the channel access token is compromised, the channel could be used by an unintended third party. Therefore, if you suspect that the channel access token has been compromised, revoke it. For more information, see [Revoke any channel access tokens suspected of being compromised](https://developers.line.biz/en/docs/basics/channel-access-token/#revoke-channel-access-token).

<!-- note end -->

## Types of channel access tokens 

There are four types of channel access tokens. These channel access tokens vary in validity period and the number of tokens that can be issued per channel.

| Type | Validity period | Number of issues per channel |
| --- | --- | --- |
| Channel access token with a user-specified expiration | Up to 30 days | 30 |
| Stateless channel access token | 15 minutes | Limitless |
| Short-lived channel access token | 30 days | 30 |
| Long-lived channel access token | Indefinite | 1 |

The number of channel access tokens issued is counted for each type of channel access token. Therefore, 30 short-lived channel access tokens can be issued even if 30 channel access tokens with a user-specified expiration are issued. An expired channel access token isn't counted as issued.

<!-- tip start -->

**Can be used repeatedly within the validity period**

The same channel access token can be used multiple times within the validity period of the channel access token. For more information, see [Can be used repeatedly within the validity period](https://developers.line.biz/en/docs/basics/channel-access-token/#use-repeatedly).

<!-- tip end -->

In addition, the types of channel access tokens that you can use vary by product and feature. For example, long-lived channel access tokens are only available for Messaging API channels. See the documentation of each product to find out which channel access tokens can be used with each product.

The following sections describe the individual channel access tokens:

- [Channel access token with a user-specified expiration (Channel access token v2.1)](https://developers.line.biz/en/docs/basics/channel-access-token/#user-specified-expiration)
- [Stateless channel access token](https://developers.line.biz/en/docs/basics/channel-access-token/#stateless-channel-access-token)
- [Short-lived channel access token](https://developers.line.biz/en/docs/basics/channel-access-token/#short-lived-channel-access-token)
- [Long-lived channel access token](https://developers.line.biz/en/docs/basics/channel-access-token/#long-lived-channel-access-token)

### Channel access token with a user-specified expiration (Channel access token v2.1) 

Channel access token v2.1 allows developers to set the validity period of up to 30 days. Security can also be enhanced by using JSON Web Token (JWT) for channel access token generation.

Up to 30 channel access tokens v2.1 can be issued per channel. Any attempt to issue more than the number that can be issued will result in the issuance request being denied. For more information about channel access tokens v2.1, see [Issue channel access tokens v2.1](https://developers.line.biz/en/docs/messaging-api/generate-json-web-token/) in the Messaging API documentation.

### Stateless channel access token 

Stateless channel tokens are channel access tokens that are only valid for 15 minutes. There is no limit to the number of stateless channel access tokens that can be issued. Once a stateless channel access token is issued, it can't be revoked.

For more information about issuing stateless access tokens, see [Issue stateless channel access token](https://developers.line.biz/en/reference/messaging-api/#issue-stateless-channel-access-token) in the Messaging API reference.

### Short-lived channel access token 

Short-lived channel access tokens are channel access tokens valid for 30 days. Up to 30 tokens can be issued per channel. If you issue more than you can issue, the oldest channel access token will be revoked.

For more information on issuing short-lived channel access tokens, see [Issue short-lived channel access token](https://developers.line.biz/en/reference/messaging-api/#issue-shortlived-channel-access-token) in the Messaging API reference.

### Long-lived channel access token 

Long-lived channel access tokens are channel access tokens that don't expire and can only be issued through the Messaging API channel. This can be issued at any time from the **Messaging API** tab in the Messaging API channel of the [LINE Developers Console](https://developers.line.biz/console/). You can revoke these tokens at any time.

Reissuing a long-lived channel access token will invalidate the currently active long-lived channel access token. You can also extend the validity of a currently active long-lived channel access token by up to 24 hours when reissuing it.

## Example of channel access token operation 

Channel access tokens are intended to be issued for each development team or group of users. For example, Development Team A and Development Team B will be issued different channel access tokens. This way, if Development Team A's channel access token is suspected to have been compromised, or if Development Team A needs to reissue a channel access token for its own reasons, Development Team B won't be affected.

In addition, as shown in the figure below, a maximum of two channel access tokens can be issued for each development team or user group to ensure continuous service.

![Example of channel access token operation](https://developers.line.biz/media/basics/operate-channel-access-token.png)

## Checklist 

In using channel access tokens, note the following:

- [Can be used repeatedly within the validity period](https://developers.line.biz/en/docs/basics/channel-access-token/#use-repeatedly)
- [Revoke any channel access tokens suspected of being compromised](https://developers.line.biz/en/docs/basics/channel-access-token/#revoke-channel-access-token)

### Can be used repeatedly within the validity period 

The same channel access token can be used multiple times within its validity period. With this in mind, for channel access tokens v2.1 and short-lived channel access tokens, don't reissue channel access tokens each time you use a channel. If a large number of channel access tokens are issued in a short period of time and it's determined that this will affect the operation of the LINE Platform, the issuance may be temporarily restricted. Note that stateless channel access tokens are designed to be issued each time a channel is used.

In addition, if you use a channel access token whose validity period has expired, you won't be able to use the channel because your channel authorization can't be verified. It is recommended that you set up a system to automatically issue new channel access tokens before they expire.

### Revoke any channel access tokens suspected of being compromised 

Channel access tokens are used to verify channel privileges. This means that if the channel access token is compromised, there is a possibility that the channel could be used by an unintended third party.

For example, in the case of the Messaging API, there is a feature called "Broadcast message" which sends the same message to all users who are friends with the LINE Official Account. If the channel access token is compromised, a third party can send broadcast message, resulting in malicious messages being sent to all friends.

For this reason, if you suspect that your revocable channel access token has been compromised, revoke it. For more information about revoking a channel access token, see the following references:

- [Revoke channel access token v2.1](https://developers.line.biz/en/reference/messaging-api/#revoke-channel-access-token-v2-1)
- [Revoke short-lived or long-lived channel access token](https://developers.line.biz/en/reference/messaging-api/#revoke-longlived-or-shortlived-channel-access-token)
