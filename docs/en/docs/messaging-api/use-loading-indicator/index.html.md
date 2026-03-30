# Display a loading animation

After your LINE Official Account receives a message from a user, the response may takes some time due to message preparation or reservation processing. In such cases, you can visually tell the user that you want them to wait by displaying a loading animation.

![](https://developers.line.biz/media/messaging-api/loading-indicator/loading-indicator.png)

## Display a loading animation 

By using the [Display a loading animation](https://developers.line.biz/en/reference/messaging-api/#display-a-loading-indicator) endpoint, you can display a loading animation in one-on-one chats between users and LINE Official Accounts. The loading animation will automatically disappear after the specified number of seconds (5 to 60 seconds) has elapsed or when a new message arrives from your LINE Official Account.

![](https://developers.line.biz/media/messaging-api/loading-indicator/loading-animation.gif)

You can display the loading animation in a one-on-one chat between a user and your LINE Official Account by specifying the user ID as the display destination. You can't specify group chats or multi-person chats.

The loading animation is only displayed when the user is viewing the chat screen with your LINE Official Account. If you request to display the loading animation when the user isn't viewing the chat screen, no notification will be displayed. Even if the user opens the chat screen later, the animation won't be displayed.

If you request to display the loading animation again while it is still visible, the animation will continue to be displayed and the time until it disappears will be overridden by the number of seconds specified in the second request.

### Example request 

Here is an example request to display a loading animation for 5 seconds:

```sh
curl -v -X POST https://api.line.me/v2/bot/chat/loading/start \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {channel access token}' \
-d '{
    "chatId": "U4af4980629...",
    "loadingSeconds": 5
}'
```

For more information, see [Display a loading animation](https://developers.line.biz/en/reference/messaging-api/#display-a-loading-indicator) in the Messaging API reference.
