# Module

<!-- note start -->

**Procedures are required to use optional functions**

The functions described in this document are available only to corporate customers who have made the prescribed applications. If you would like to publish the extension function using the module, contact the sales representative or contact us from [LINE Marketplace Inquiry](https://line-marketplace.com/jp/inquiry) (only available in Japanese).

<!-- note end -->

## Overview 

The module is a mechanism that allows you to add functions using the Messaging API to your LINE Official Account by linking (attaching) it to your LINE Official Account. Modules are provided as a type of channel [module channel](https://developers.line.biz/en/docs/line-developers-console/overview/#channel). Even if your LINE Official Account hasn't created a Messaging API channel, you can still call the Messaging API from a module channel to send messages to users and set rich menus.

![module channel](https://developers.line.biz/media/partner-docs/module/module-channel-en.png)

### Relationship between module channel and LINE Official Account 

Normally, you can only create (open) one Messaging API channel for one LINE Official Account. Module channels, on the other hand, can be linked to multiple LINE Official Accounts.

![Attach same service](https://developers.line.biz/media/partner-docs/module-technical/attach-same-service-en.png)

- OA "X"、OA "Y"、OA "Z": LINE Official Account
- Module CH: Module channel
- System: Module CH webhook destination and bot server

<!-- tip start -->

**About the server used for module channels**

In the module channel, the server that communicates with the LINE Platform system is prepared by the company in charge of developing the module channel. The server set as the webhook destination and the server that calls the Messaging API, etc., doesn't have to be the same.

<!-- tip end -->

### Module usage example 

For example, let's say you have a LINE Official Account that uses the chat function of the LINE Official Account Manager to communicate with users. If a "module channel with in-store reservation function" is linked to this LINE Official Account, you can chat with users on the LINE Official Account Manager and automate the in-store reservation process through the module.

<!-- tip start -->

**Webhooks are enabled for module channels**

If the [webhook use is disabled](https://developers.line.biz/en/reference/messaging-api/#get-webhook-endpoint-information) in the response settings of your LINE Official Account, webhook events won't be sent to the Messaging API channel. Webhook events are still sent to the module channel under these settings.

Depending on the content of the webhook event you get, the module channel can be implemented to send a message to the user.

<!-- tip end -->

![Sample](https://developers.line.biz/media/partner-docs/module/module-sample.png)

| Number | Description |
| --- | --- |
| 1 | The user sends a message |
| 2 | The operator sends a message to the user using the chat function of LINE Official Account Manager |
| 3 | The user presses the rich menu to execute the module with the function to make a reservation |
| 4 | The bot for the reservation function responds and the reservation process begins |

## Reference 

For more information on technical specs such as the REST API provided by the module, see [Module](https://developers.line.biz/en/reference/partner-docs/#module) in the options for corporate customers API reference.

## Prepare the necessary systems and mechanisms 

<!-- note start -->

**Note**

Currently, the module is only available for release as a paid extension on the [LINE Marketplace](https://line-marketplace.com/) (only available in Japanese).

<!-- note end -->

The functions provided by LY Corporation in the module are as follows.

| Function name | Description |
| --- | --- |
| Mechanism for linking module channels to LINE Official Accounts | It provides a mechanism for OAuth 2.0 authorization and a mechanism for linking module channels to LINE Official Accounts using the REST API. For more information, see [Attach module channels using the OAuth 2.0 authorization mechanism](https://developers.line.biz/en/docs/partner-docs/module-technical-attach-channel/#attach-module-channels-using-oauth-2-0-auth-mechanism). |
| API to unlink the LINE Official Account from the module channel | A REST API is provided to unlink the LINE Official Account from the module channel. For more information, see [Unlink (detach) the module channel by the operation of the module channel administrator](https://developers.line.biz/en/reference/partner-docs/#unlink-detach-module-channel-by-operation-mc-admin) in the options for corporate customers API reference. |
| API to control chat initiative | Module channels have a concept called chat initiative (Chat Control). You can send a [reply message](https://developers.line.biz/en/reference/messaging-api/#send-reply-message) to a user, group, or chat room from the channel with the initiative. <br>Normally, the module channels offered on the LINE Marketplace don't require initiative control, but we provide a REST API to control chat initiative to handle cases where chat initiative is changed due to unexpected events.<br>For more information, see [Control chat initiative (Chat Control)](https://developers.line.biz/en/docs/partner-docs/module-technical-chat-control/). |
| Mechanism to use the Messaging API from a module channel | When calling the Messaging API from a module channel, you need to specify a special request header specifically for the module. For more information, see [Using the Messaging API from a module channel](https://developers.line.biz/en/docs/partner-docs/module-technical-using-messaging-api/). |
| Webhook events dedicated to the module channel | The module channel provides dedicated webhook events. For more information, see [Receive module channel-specific webhook events](https://developers.line.biz/en/docs/partner-docs/module-technical-using-messaging-api/#get-module-channel-specific-webhook-events). |
| API to get information of a LINE Official Account linked to a module channel | Provides a REST API to get information about a LINE Official Account linked to a module channel. For more information, see [Get the LINE Official Account information from the module channel](https://developers.line.biz/en/docs/partner-docs/module-technical-using-messaging-api/#get-line-oa-info-from-module-channel). |

Other than the above, all other systems (servers, etc.) and mechanisms required to publish extensions on the LINE Marketplace must be provided (developed) by the customer. For example:

- [Mechanisms for using the functions provided by the module](https://developers.line.biz/en/docs/partner-docs/module/#develop-your-system)
- [Mechanism for using the Messaging API from a module channel](https://developers.line.biz/en/docs/partner-docs/module/#develop-messaging-api-and-backend)
- [Mechanism of management screen and operation console required for users to use extended functions](https://developers.line.biz/en/docs/partner-docs/module/#develop-cms)
- [Mechanism for payment and management of module usage fees](https://developers.line.biz/en/docs/partner-docs/module/#manage-payment-system)
- [Support mechanism for users](https://developers.line.biz/en/docs/partner-docs/module/#user-support)

### Mechanisms for using the functions provided by the module 

The module channel is used in conjunction with the LINE Official Account based on the [OAuth 2.0 authorization code granting flow](https://datatracker.ietf.org/doc/html/rfc6749). Customers are required to prepare various mechanisms to use the functions described in [Prepare the necessary systems and mechanisms](https://developers.line.biz/en/docs/partner-docs/module/#module-functions), including the system required to grant OAuth 2.0 authorization codes (authorization requests).

### Mechanism for using the Messaging API from a module channel 

To use the Messaging API from a module channel linked to your LINE Official Account, you need to request the Messaging API with a special request header specifically for the module channel. Customers are required to prepare the mechanism for requesting the Messaging API and the mechanism for extended functions (chatbots, etc.) provided by the module.

<!-- tip start -->

**Additional costs may be required for message delivery**

When calling the Messaging API from a module channel to send messages to users, the operator of the LINE Official Account linked to the module channel may be required to pay the [Messaging API fee](https://developers.line.biz/en/docs/messaging-api/pricing/). This is the same as when a message is sent from a Messaging API channel using the Messaging API.

<!-- tip end -->

### Mechanism of management screen and operation console required for users to use extended functions 

Customers are required to provide their own management screens, operation consoles, and other mechanisms necessary for users to use the extended functions implemented in the module.

### Mechanism for payment and management of module usage fees 

The module will be available as a paid extension on the [LINE Marketplace](https://line-marketplace.com/) (only available in Japanese). Customers are required to provide their own mechanisms for managing users who use the extensions and for settling usage fees.

### Support mechanism for users 

Customers are required to prepare a support mechanism for users who use the module extensions. LY Corporation doesn't provide support to users of extensions published on the [LINE Marketplace](https://line-marketplace.com/jp/inquiry) (only available in Japanese).

## Note 

You must comply with these items when using the module channel function in the LINE Marketplace:

- [Messaging API calls from Messaging API channel (combined)](https://developers.line.biz/en/docs/partner-docs/module/#restrict-messaging-api-request)
- [Max number of module channels that can be linked](https://developers.line.biz/en/docs/partner-docs/module/#attach-limit)
- [Types of Messaging APIs available for module channel](https://developers.line.biz/en/docs/partner-docs/module/#module-scopes)
- [Get webhook event](https://developers.line.biz/en/docs/partner-docs/module/#bot-module-channel-receive-webhook)

### Messaging API calls from Messaging API channel (combined) 

We don't recommend using the Messaging API from the Messaging API channel for LINE Official Accounts that are linked to the module channel. This is because, depending on the system implementation, unexpected behavior may occur in the extended functions provided by the module.

For example, these problems may occur:

- The rich menu provided by the module wasn't displayed because of [linking rich menu to the user via Messaging API](https://developers.line.biz/en/reference/messaging-api/#link-rich-menu-to-user).
- A user sends a message or performs an action on a message sent from the Messaging API channel, and a [webhook event was sent](https://developers.line.biz/en/docs/partner-docs/module/#bot-module-channel-receive-webhook). This webhook event wasn't expected in the module's system, so it couldn't be handled correctly.

### Max number of module channels that can be linked 

In the LINE Marketplace, only one module channel (extension) can be linked to one LINE Official Account at the same time.

### Types of Messaging APIs available for module channel 

The type of Messaging API available for the module channel depends on the permissions (scope) granted when the module channel is linked. For more information, see [Scopes](https://developers.line.biz/en/docs/partner-docs/module-technical-attach-channel/#scopes) in the Attach Module Channel document.

### Get webhook event 

In the module channel, you can set one endpoint URL to get webhook events.

When a module channel is linked to a LINE Official Account, webhook events corresponding to the content sent to the LINE Official Account's chat room are also sent to the endpoints set up in the module channel. For more information on webhook events in module channels, see [Receiving a webhook](https://developers.line.biz/en/docs/partner-docs/module-technical-using-messaging-api/#get-webhook).

<!-- tip start -->

**Webhook events dedicated to module channels**

There are webhook events that are sent only to the module channel. For more information, see [Receive module channel-specific webhook events](https://developers.line.biz/en/docs/partner-docs/module-technical-using-messaging-api/#get-module-channel-specific-webhook-events).

<!-- tip end -->

<!-- note start -->

**About webhook events in Messaging API channels**

If the LINE Official Account linked to the module channel is [using the Messaging API channel](https://developers.line.biz/en/docs/messaging-api/getting-started/) and [webhook use is enabled](https://developers.line.biz/en/docs/messaging-api/building-bot/#set-up-bot-on-line-developers-console), webhook events will be sent to both the module channel and the endpoint URL set for the Messaging API channel. In this case, the webhook event sent to the Messaging API channel endpoint URL will have the [`mode` property set to `standby`](https://developers.line.biz/en/reference/messaging-api/#common-properties) and the webhook event won't contain a reply token to [send reply message](https://developers.line.biz/en/reference/messaging-api/#send-reply-message).

<!-- note end -->
