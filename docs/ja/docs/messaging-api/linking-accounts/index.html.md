# ユーザーアカウントの連携

サービス提供者は、ユーザーのLINEアカウントと自社サービスのアカウントを**セキュアに**連携させることができます。アカウントを連携するには、ユーザーがLINE公式アカウントを友だち追加している必要があります。LINEアカウントと自社サービスのアカウントを連携させることで、自社サービスのユーザー情報をLINE上で活用できます。これにより、LINE公式アカウントでのユーザー体験を向上させることができます。

自社サービスのアカウントとLINEアカウントを連携させることで、ユーザーの利便性を高めることができます。たとえば、ショッピングサイトであれば、以下のようなことが可能です。

- ユーザーがショッピングサイトで商品を購入したときに、LINE公式アカウントからメッセージを送る。
- ユーザーがLINE公式アカウントとのトーク画面から注文する。

LINEログインを使ってもアカウントを連携できますが、その場合はLINEログインのチャネルが必要です。Messaging APIを使うと、LINEログインチャネルがなくてもアカウントを連携できます。

## アカウント連携のシーケンス 

ユーザーのLINEアカウントと自社サービスのアカウントを連携するシーケンスは以下のとおりです。

![](https://developers.line.biz/media/messaging-api/linking-accounts/sequence.png)

1. ボットサーバーが、LINEのユーザーIDから連携トークンを発行するAPIを呼び出す。
1. LINEプラットフォームが連携トークンを発行し、ボットサーバーに返す。
1. ボットサーバーがユーザーに連携URLを送信するために、Messaging APIを呼び出す。
1. LINEプラットフォームが、ユーザーに連携URLを送信する。
1. ユーザーが連携URLにアクセスする。
1. ウェブサーバーがログイン画面を表示する。
1. ユーザーが、自社サービスの認証情報を入力する。
1. ウェブサーバーが自社サービスのユーザーIDを取得し、それを使ってnonce（number used once）を生成する。
1. ウェブサーバーが、ユーザーをアカウント連携するエンドポイントにリダイレクトする。
1. ユーザーが、アカウントを連携するエンドポイントにアクセスする。
1. LINEプラットフォームがボットサーバーに、LINEのユーザーIDとnonceを含むイベントをWebhookで送信する。
1. ボットサーバーが、nonceを使って自社サービスのユーザーIDを取得する。

Messaging APIを使わなくても、独自に実装してアカウントを連携させることもできます。ただし、アカウント連携では、ユーザーがセキュリティ上の問題にさらされる可能性があるため、独自で実装する場合には、より注意が必要です。たとえば、攻撃者がユーザーにURLを送り、攻撃者のLINEアカウントとユーザーの自社サービスのアカウントを連携させることが考えられます。Messaging APIを使うと、このような攻撃からユーザーを守ることができます。Messaging APIでは、連携URLを発行したユーザーが、連携しようとしているLINEアカウントの正当な所有者であるかどうかを検証します。

## アカウントを連携する 

自社サービスのユーザーアカウントとLINEのユーザーアカウントを連携するには、以下の手順に従います。

### 1. 連携トークンを発行する 

ユーザーのLINEアカウントと自社サービスのアカウントを連携するには、連携トークンが必要です。[連携トークンを発行](https://developers.line.biz/ja/reference/messaging-api/#issue-link-token)するには、`/bot/user/{userId}/linkToken`エンドポイントにHTTP POSTリクエストを送信します。

```sh
curl -X POST https://api.line.me/v2/bot/user/{userId}/linkToken \
-H 'Authorization: Bearer {channel access token}'
```

リクエストが成功すると、ステータスコード`200`と連携トークンが返されます。連携トークンは10分間有効で、1回のみ使用できます。

```sh
{
  "linkToken": "NMZTNuVrPTqlr2IF8Bnymkb7rXfYv5EY"
}
```

### 2. ユーザーに連携URLを送信する 

ボットサーバーからユーザーに、連携URLを開くメッセージを送信します。たとえば、[URIアクション](https://developers.line.biz/ja/docs/messaging-api/actions/#uri-action)を設定した[テンプレートメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#template-messages)に連携URLを指定します。このとき、連携URLにはステップ1の連携トークンをクエリパラメータとして追加します。

以下は、連携URLを指定したメッセージをユーザーに送信するリクエストの例です。

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

### 3. 自社サービスのユーザーIDを取得する 

ユーザーが連携URLにアクセスしたら、自社サービスへのログイン画面を表示します。ユーザーがサービスにログインすると、自社サービスのユーザーIDを取得できます。

### 4. nonceを生成してユーザーをLINEプラットフォームにリダイレクトする 

ステップ3で取得したユーザーIDからnonce（number used once）を生成します。nonceの要件は以下のとおりです。

- 予測が難しく一度しか使用できない文字列であること。セキュリティ上問題があるため、自社サービスのユーザーIDなどの予測可能な値は使わないでください。
- 長さは10文字以上255文字以下であること。

nonceとしてランダムな値を生成する際の推奨事項は以下のとおりです。

- セキュアなランダム生成関数を使う。
- 少なくとも128ビット（16バイト）以上にする。
- Base64エンコードする。

nonceを生成したら、そのnonceとサービスのユーザーIDを紐づけて保存します。次に、ユーザーを以下のエンドポイントにリダイレクトします。

```sh
https://access.line.me/dialog/bot/accountLink?linkToken={link token}&nonce={nonce}
```

ユーザーがこのエンドポイントにアクセスすると、LINEプラットフォームにより、ユーザーが連携トークンを発行したユーザーかどうかを確認します。その確認結果に応じて、LINEプラットフォームは以下のような処理を行います。

- ユーザーの確認ができた場合：LINEプラットフォームからボットサーバーに`result`プロパティの値が`ok`の[アカウント連携イベント](https://developers.line.biz/ja/reference/messaging-api/#account-link-event)が送信されます。
- ユーザーの確認ができなかった場合：LINEプラットフォームからボットサーバーに`result`プロパティの値が`failed`の[アカウント連携イベント](https://developers.line.biz/ja/reference/messaging-api/#account-link-event)が送信されます。
- 連携トークンが無効の場合：連携トークンが有効期限切れや、使用済みの場合、LINEプラットフォームはWebhookイベントを送信せず、ユーザーにエラーを表示します。

### 5. アカウントを連携する 

ステップ4で、連携トークンを発行したユーザーであることが確認できた場合、ユーザーのアカウントを連携します。アカウント連携イベントには、LINEのユーザーIDとnonceが含まれています。このnonceを使って、nonceと紐づけて保存しておいた自社サービスのユーザーIDを取得します。LINEのユーザーIDと自社サービスのユーザーIDを連携すれば、アカウントの連携が完了します。

## アカウントの連携を解除する 

ユーザーがLINEアカウントと自社サービスのアカウントを連携している場合、連携を解除できるようにする必要があります。

- ユーザーがいつでもアカウントの連携を解除できるようにしておくこと。
- ユーザーがアカウントを連携するときに、連携を解除できることを通知すること。

たとえば、Messaging APIを使えば、ユーザーごとに[リッチメニュー](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/)をカスタマイズできます。アカウントを連携していないユーザーにはアカウントを連携するメニューを表示したり、アカウントを連携済みのユーザーには連携を解除するメニューを表示したりできます。

## 関連ページ 

- [Messaging APIリファレンス](https://developers.line.biz/ja/reference/messaging-api/)
