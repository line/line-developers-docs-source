# Control chat initiative (Chat Control)

<!-- warning start -->

**Warning**

The module channel currently offered automatically acquires chat initiative when it is attached to a LINE Official Account [(Default Active)](https://developers.line.biz/en/docs/partner-docs/module-technical-chat-control/#default-active), so there is no need to control chat initiative.

<!-- warning end -->

<!-- note start -->

**Procedures are required to use optional functions**

The functions described in this document are available only to corporate customers who have made the prescribed applications. If you would like to publish the extension function using the module, contact the sales representative or contact us from [LINE Marketplace Inquiry](https://line-marketplace.com/jp/inquiry) (only available in Japanese).

<!-- note end -->

## What is chat control (Chat Control)? 

To prevent multiple module channels from replying to or processing end user actions at the same time, we've introduced the concept of initiative (Chat Control) for module channels.

![Chat control](https://developers.line.biz/media/partner-docs/module-technical/chat-control-en.png)

| Initiative (Chat Control) | Description |
| --- | --- |
| Active Channel | A channel with initiative (Chat Control). By default, Primary CH (the standard Messaging API channel associated with the LINE Official Account) is the "Active Channel".<br>You can send reply messages, push messages, etc. from this channel.<br>Only one "Active Channel" can be attached for each LINE Official Account. |
| Standby Channel | A channel that doesn't have Chat Control.<br>Refrain from sending messages from this channel.<br>All channels other than Active Channel are "Standby Channel." |

<!-- note start -->

**Initiative (Chat Control) isn't set collectively for each module channel**

Initiative (Chat Control) is managed on a per-user, per-chat room, or per-group basis.

<!-- note end -->

<!-- note start -->

**Module channel with &quot;Default Active&quot; function**

A module channel with the "Default Active" function is a module channel that automatically becomes an Active Channel when you attach it to a LINE Official Account.

For more information, see [Default Active](https://developers.line.biz/en/docs/partner-docs/module-technical-chat-control/#default-active).

<!-- note end -->

## API reference 

- [Acquire Control API](https://developers.line.biz/en/reference/partner-docs/#acquire-control-api)
- [Release Control API](https://developers.line.biz/en/reference/partner-docs/#release-control-api)

## Default active 

The module channels offered on the LINE Marketplace are given the "Default Active" feature.

<!-- note start -->

**This feature is exclusive to the LINE Marketplace**

The "Default Active" feature is only available for module channels published on the [LINE Marketplace](https://line-marketplace.com/jp/inquiry).

<!-- note end -->

The features of the module channel with the "Default Active" feature are as follows.

### Auto active 

The normal module channel becomes a Standby Channel when attached to a LINE Official Account. After that, the module channel acquires initiative (Chat Control) using the Acquire Control API as needed (triggered by user operation, etc.) and becomes an Active Channel.

Module channels that have been given the "Default Active" feature will automatically become Active Channels when attached to a LINE Official Account. So, there is no need to call the Acquire Control API.

### Exclusive control 

Only one module channel with the "Default Active" feature can be attached to a LINE Official Account.

If a module channel with the "Default Active" feature has already been attached to a LINE Official Account, you won't be able to attach any other module channels with the "Default Active" feature to that account.

You can attach multiple module channels that don't have the "Default Active" feature, but the current doesn't provide them.
