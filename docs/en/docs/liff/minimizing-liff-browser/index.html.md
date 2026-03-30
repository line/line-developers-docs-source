# Minimizing LIFF browser

This page explains LIFF browser minimization.

<!-- table of contents -->

## What is LIFF browser minimization 

[LIFF browser](https://developers.line.biz/en/glossary/#liff-browser) minimization is a feature that allows you to suspend viewing a LIFF browser to perform another action.

When viewing a LIFF browser in a chat room, the user may want to perform another action, such as sending a message to the chat room. In this case, minimizing the LIFF browser will suspend viewing the LIFF browser and allow the user to perform the action. After performing the action, the user can resume viewing the LIFF browser by maximizing the LIFF browser.

The LIFF browser will be displayed as an icon when minimized.

![LIFF browser minimization](https://developers.line.biz/media/liff/minimizing-liff-app/liff-minimize-en.png)

<!-- tip start -->

**Minimizing LINE's in-app browser**

Like LIFF browser, [LINE's in-app browser](https://developers.line.biz/en/glossary/#line-iab) also supports minimization. For more information, see [Minimizing the browsing web page](https://guide.line.me/ja/chats-calls-notifications/chats/minimizebrowser.html) (only available in Japanese) in the LINE user's guide.

<!-- tip end -->

## Conditions of use for LIFF browser minimization 

To minimize a LIFF browser, the following conditions must be met:

- LINE for iOS version 12.18.0 or later or LINE for Android version 15.0.0 or later
- **Settings** > **Apps** > **LINE** > **Display over other apps** is on for the user's device (only required in LINE for Android)
- `Full` is specified as the [screen size](https://developers.line.biz/en/docs/liff/overview/#screen-size) for your LIFF app
- [`chat_message.write` scope](https://developers.line.biz/en/docs/liff/registering-liff-apps/#registering-liff-app) is off for your LIFF app
- The LIFF browser isn't overlapping on another modal

<!-- note start -->

**The LIFF app after LIFF-to-LIFF transition must meet the conditions of use**

To minimize the LIFF browser after [LIFF-to-LIFF transition](https://developers.line.biz/en/docs/liff/opening-liff-app/#move-liff-to-liff), the LIFF app after transition must meet the conditions of use.

For example, as described in [Behavior based on screen size of the LIFF app](https://developers.line.biz/en/docs/liff/opening-liff-app/#behavior-by-screen-size) in the LIFF documentation, the LIFF app after transition will be displayed in `Full`, regardless of the screen size specified. However, if `Tall` or `Compact` is specified as the screen size for the LIFF app after transition, the LIFF app after transition won't satisfy the conditions of use for LIFF browser minimization.

<!-- note end -->

LIFF browser minimization will be available on LINE for iPadOS, but the date is yet to be determined.

## Minimizing a LIFF browser 

There are three ways to minimize a LIFF browser:

- [Tapping an option from the action button](https://developers.line.biz/en/docs/liff/minimizing-liff-browser/#tap-action-button-option)
- [Tapping an in-app alert](https://developers.line.biz/en/docs/liff/minimizing-liff-browser/#tap-in-app-alert)
- [Swiping a LIFF browser](https://developers.line.biz/en/docs/liff/minimizing-liff-browser/#swipe-liff-browser)

### Tapping an option from the action button 

Tap the **Minimize browser** option after opening the [multi-tab view](https://developers.line.biz/en/docs/liff/overview/#multi-tab-view) from the [action button](https://developers.line.biz/en/docs/liff/overview/#action-button).

![LIFF browser minimization (tapping an action button option)](https://developers.line.biz/media/liff/minimizing-liff-app/tap-action-button-option-en.png)

### Tapping an in-app alert 

Tap an in-app alert.

![LIFF browser minimization (tapping an in-app alert)](https://developers.line.biz/media/liff/minimizing-liff-app/tap-in-app-alert.png)

### Swiping a LIFF browser 

Swipe a LIFF browser down.

![LIFF browser minimization (swiping a LIFF browser)](https://developers.line.biz/media/liff/minimizing-liff-app/swipe-liff-browser-en.png)

## Maximizing a LIFF browser 

To maximize a LIFF browser, tap the minimized LIFF browser.

![LIFF browser maximization](https://developers.line.biz/media/liff/minimizing-liff-app/maximize-liff-browser-en.png)

## Moving a minimized LIFF browser 

To move a minimized LIFF browser, drag the LIFF browser.

![Moving a minimized LIFF browser](https://developers.line.biz/media/liff/minimizing-liff-app/move-minimized-liff-browser-en.png)

## Closing a minimized LIFF browser (LINE version earlier than 15.20.0) 

In LINE version earlier than 15.20.0, there are two ways to close a minimized LIFF browser:

- [Swiping a LIFF browser off the screen (only available in LINE for iOS)](https://developers.line.biz/en/docs/liff/minimizing-liff-browser/#close-minimized-liff-browser-1)
- [Drag a minimized LIFF browser to the close icon](https://developers.line.biz/en/docs/liff/minimizing-liff-browser/#close-minimized-liff-browser-2)

### Swiping a LIFF browser off the screen (only available in LINE for iOS) 

Swipe the minimized LIFF browser off the screen.

![Closing a minimized LIFF browser](https://developers.line.biz/media/liff/minimizing-liff-app/close-minimized-liff-browser-en.png)

### Drag a minimized LIFF browser to the close icon 

Dragging a minimized LIFF browser shows the close icon at the bottom of the screen. Drag the minimized LIFF browser to the close icon and release your finger.

![Closing a minimized LIFF browser](https://developers.line.biz/media/liff/minimizing-liff-app/close-minimized-liff-browser-ios-12-12-0-or-later-en.png)

## Closing a minimized LIFF browser (LINE version 15.20.0 or later) 

In LINE version 15.20.0 or later, you can close the minimized LIFF browser by tapping the close button displayed at the top-right corner of the minimized LIFF browser.

![Close minimized liff browser](https://developers.line.biz/media/liff/minimizing-liff-app/close-minimized-liff-browser-line-15-20-0-or-later-en.png)

## Priority of LIFF browser icon display 

A LIFF browser will be displayed as an icon when minimized. The priority of LIFF browser icon display is as follows:

1. Channel icon: The channel icon of a LINE Login channel
1. Favicon: The favicon of a LIFF app
1. Common icon: A link icon
