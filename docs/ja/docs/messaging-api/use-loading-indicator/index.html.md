# ローディングのアニメーションを表示する

LINE公式アカウントがユーザーからのメッセージを受信したあと、メッセージの準備や予約の処理などで返答に少し時間がかかることがあります。そのような場合に、ユーザーにそのまま待機しておいて欲しいことをローディングのアニメーションで視覚的に伝えることができます。

![](https://developers.line.biz/media/messaging-api/loading-indicator/loading-indicator.png)

## ローディングのアニメーションを表示する 

[ローディングのアニメーションを表示する](https://developers.line.biz/ja/reference/messaging-api/#display-a-loading-indicator)エンドポイントを使用すると、トークの画面にローディングのアニメーションを表示できます。アニメーションは指定した秒数（5秒〜60秒）が経過するか、表示中にLINE公式アカウントからメッセージが届くと自動的に消えます。

![](https://developers.line.biz/media/messaging-api/loading-indicator/loading-animation.gif)

表示先としてユーザーIDを指定することで、ユーザーとLINE公式アカウントの1対1のトークにアニメーションを表示できます。グループトークまたは複数人トークは指定できません。

ローディングのアニメーションは、ユーザーが対象のLINE公式アカウントとのトーク画面を表示しているときのみ表示されます。ユーザーがトーク画面を表示していないときに、ローディングのアニメーションを表示するリクエストを行っても、通知は行われません。また、その後にユーザーがトーク画面を開いてもアニメーションは表示されません。

ローディングのアニメーションが表示されている間に再び表示のリクエストを行うと、アニメーションはそのまま表示され続け、表示が消えるまでの時間は2回目のリクエストで指定した秒数に上書きされます。

### リクエストの例 

以下は、ローディングのアニメーションを5秒間表示するリクエストの例です。

```sh
curl -v -X POST https://api.line.me/v2/bot/chat/loading/start \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {channel access token}' \
-d '{
    "chatId": "U4af4980629...",
    "loadingSeconds": 5
}'
```

詳しくは、『Messaging APIリファレンス』の「[ローディングのアニメーションを表示する](https://developers.line.biz/ja/reference/messaging-api/#display-a-loading-indicator)」を参照してください。
