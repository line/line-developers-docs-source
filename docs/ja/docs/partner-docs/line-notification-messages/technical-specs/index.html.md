# LINE通知メッセージAPIの技術仕様

<!-- note start -->

**オプション機能を利用するには手続きが必要です**

本ドキュメントに記載の機能は、所定の申請等を行った法人ユーザーのみがご利用いただけます。自社のLINE公式アカウントでご利用になりたいお客様は、担当営業までご連絡いただくか、[弊社パートナー](https://www.lycbiz.com/jp/partner/sales/)にお問い合わせください。

<!-- note end -->

## ユーザーにLINE通知メッセージを送る 

電話番号を指定してLINE通知メッセージのAPIにメッセージの送信をリクエストすると、その電話番号が登録されているLINEアカウントに対してLINE通知メッセージが送信されます。LINEヤフー株式会社は受領した情報をメッセージ送信の宛先照合のためにのみ利用し、照合後は速やかに破棄します。なお、個人情報等を含む通知内容の確認や手続きの継続には、SMSによる本人確認が必要な場合があります。

LINE通知メッセージには、LINE通知メッセージ（テンプレート）とLINE通知メッセージ（フレキシブル）の2種類があり、それぞれ使用するAPIが異なります。

- LINE通知メッセージ（テンプレート）
  - [LINE通知メッセージ（テンプレート）を送る](https://developers.line.biz/ja/reference/line-notification-messages/#send-line-notification-message-template)
  - [送信済みのLINE通知メッセージ（テンプレート）の数を取得する](https://developers.line.biz/ja/reference/line-notification-messages/#get-number-of-sent-line-notification-messages-template)
- LINE通知メッセージ（フレキシブル）
  - [LINE通知メッセージ（フレキシブル）を送る](https://developers.line.biz/ja/reference/line-notification-messages/#send-line-notification-message-flexible)
  - [送信済みのLINE通知メッセージ（フレキシブル）の数を取得する](https://developers.line.biz/ja/reference/line-notification-messages/#get-number-of-sent-line-notification-messages-flexible)

詳しくは、「[LINE通知メッセージAPIリファレンス](https://developers.line.biz/ja/reference/line-notification-messages/)」を参照してください。

### LINE通知メッセージで送信可能なメッセージタイプ 

LINE通知メッセージ（テンプレート）では、用意されたテンプレートやアイテム、ボタンを組み合わせて簡単にメッセージを作成できます。メッセージを作成する際は、「[LINE通知メッセージ（テンプレート）UXガイドライン](https://www.lycbiz.com/sites/default/files/media/jp/download/LINE_Official_Notification_Template_UXGuideline.pdf)」に準拠してください。

![LINE通知メッセージ（テンプレート）のサンプル](https://developers.line.biz/media/line-notification-message/notification-messages-template.png)

LINE通知メッセージ（フレキシブル）では、[Flex Message](https://developers.line.biz/ja/docs/messaging-api/message-types/#flex-messages)などを用いて、より柔軟にメッセージが作成できます。ただしメッセージ内に画像、動画、音声を含めることは許可されていません。またLINE通知メッセージ（フレキシブル）では事前のUX審査があり、審査に通過したメッセージのみ送信できます。メッセージを作成する際は、「[LINE通知メッセージ（フレキシブル）UXガイドライン](https://www.lycbiz.com/sites/default/files/media/jp/download/LINE%E9%80%9A%E7%9F%A5%E3%83%A1%E3%83%83%E3%82%BB%E3%83%BC%E3%82%B8UX%E3%82%AC%E3%82%A4%E3%83%89%E3%83%A9%E3%82%A4%E3%83%B3.pdf)」に準拠してください。

### 電話番号のハッシュ化 

LINE通知メッセージAPIで宛先`to`を指定する際には、[E.164](https://developers.line.biz/ja/glossary/#e164)形式に正規化された電話番号、例：`+818000001234`をSHA256でハッシュ化した文字列を指定します。ハイフンは含まないでください。以下はPython3を用いた電話番号のハッシュ化の例です。

```python
import hashlib

phone_number = "+818000001234"
hashed_phone_number = hashlib.sha256(phone_number.encode()).hexdigest()
print(hashed_phone_number)

# d41e0ad70dddfeb68f149ad6fc61574b9c5780ab7bcb2fba5517771ffbb2409c
```

### メッセージの送信通知を受信する 

LINE通知メッセージAPIをリクエストし、ユーザーに対してLINE通知メッセージの送信が完了した際に、専用のWebhookイベント（[配信完了イベント](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#receive-delivery-event)）がLINEプラットフォームから送信されます。

リクエスト時にリクエストヘッダーの`X-Line-Delivery-Tag`で任意の文字列を指定すると、Webhookの[配信完了イベント](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/#receive-delivery-event)の`delivery.data`プロパティでその文字列が返されます。`X-Line-Delivery-Tag`は、Webhook受信時にどのメッセージが配信完了したのかを判別する、などの用途で使用できます。

詳しくは[Webhookの配信完了イベント](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/)を参照してください。

### 送信済みLINE通知メッセージの数を取得する 

以下のAPIで送信済みのLINE通知メッセージの数を取得できます。

- [送信済みのLINE通知メッセージ（テンプレート）の数を取得する](https://developers.line.biz/ja/reference/line-notification-messages/#get-number-of-sent-line-notification-messages-template)
- [送信済みのLINE通知メッセージ（フレキシブル）の数を取得する](https://developers.line.biz/ja/reference/line-notification-messages/#get-number-of-sent-line-notification-messages-flexible)

<!-- note start -->

**注意**

送信通数には、実際にユーザーに送信されたLINE通知メッセージの通数のみが集計されます。送信条件について詳しくは、「[LINE通知メッセージが送信される条件](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#conditions-for-sending-line-notification-messages)」を参照してください。

<!-- note end -->

## LINE通知メッセージが送信される条件 

以下の条件をすべて満たす場合に、ユーザーに対してメッセージが送信されます。

- LINE通知メッセージの送信対象として指定した電話番号が、ユーザーがLINEに登録している電話番号と一致していること
- ユーザーがLINEに登録している電話番号が有効であること（SMSによる電話番号認証を、一定期間内に一度実施している）
- ユーザーがLINE通知メッセージの受信に同意していること
- ユーザーがLINE通知メッセージ送信元であるLINE公式アカウントをブロックしていないこと
- LINE通知メッセージの送信対象として指定した電話番号が、日本、タイ、台湾で発行された電話番号かつ、[LINEアプリにおいて電話番号による認証を行うことができる電話番号](https://help.line.me/line/smartphone/pc?lang=ja&contentId=20000104)であること
- ユーザーがLINEのプライバシーポリシー（2022年3月改定以降のもの）に同意していること

LINEアプリでのLINE通知メッセージの設定について詳しくは、『LINEみんなの使い方ガイド』の「[LINE通知メッセージを受信する方法](https://guide.line.me/ja/services/notification-message.html)」を参照してください。

## LINE通知メッセージとAPIに関する補足事項 

- [「LINE通知メッセージが届きました」メッセージについて](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#about-recive-the-new-line-notification-message)
- [LINE通知メッセージの受信設定](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#how-to-consent-for-line-notification-messages)
- [LINE通知メッセージの受信への同意を行っていない際に送信されたメッセージについて](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#user-has-not-given-consent-when-receive-line-notification-messages)
- [LINE公式アカウントをブロックしているユーザーに対するLINE通知メッセージAPIのリクエストについて](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#about-pnp-api-block-response)
- [LINE通知メッセージAPIのリクエストが成功したが、メッセージが送信されない場合について](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#why-i-cant-receive-line-notification-messages)
- [LINE公式アカウントと友だちではないユーザーにLINE通知メッセージを送信した際の友だち追加やブロックについて](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#when-user-add-or-block-oa)
- [LINE公式アカウントと友だちではないユーザーにLINE通知メッセージを送信した際のリッチメニューの表示について](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#about-richmenu-displayed)
- [LINE通知メッセージの利用料金の請求対象について](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#about-delivered-pnp-messages)

### 「LINE通知メッセージが届きました」メッセージについて 

LINE通知メッセージの送信時に「LINE」という名前のLINE公式アカウント（システムアカウント）から以下のメッセージが送信されます。このメッセージは、LINE通知メッセージ送信するたびに、必ず送信されるメッセージです。LINE通知メッセージの送信者は、このメッセージが送信されないようにしたり、送信される回数を減らしたりする制御を行うことはできません。

![LINE通知メッセージが届きました](https://developers.line.biz/media/line-notification-message/type1-pnpflow-3-ja.png)

<!-- note start -->

**ブロック時の動作**

LINE通知メッセージAPIで送信対象として指定したユーザーが、LINE通知メッセージの送信元であるLINE公式アカウントをブロックしていた場合は、LINE通知メッセージは送信されず、「LINE」システムアカウントからの「LINE通知メッセージが届きました」メッセージについても送信されません。

また、送信元であるLINE公式アカウントをブロックしていた間に送信されたLINE通知メッセージは、ユーザーがブロックを解除しても後から届くことはありません。

<!-- note end -->

### LINE通知メッセージの受信設定 

LINE通知メッセージが送られてきた際に、ユーザーはLINE通知メッセージの受信に同意（もしくは拒否）できます。また、LINE通知メッセージが送られたとき以外にも、任意のタイミングでLINEアプリの［**設定**］>［**プライバシー管理**］>［**情報の提供**］>［**LINE通知メッセージ**］からLINE通知メッセージの受信に同意（もしくは拒否）できます。

![LINE通知メッセージの受信同意](https://developers.line.biz/media/line-notification-message/consent-line-notification-message-ja.png)

#### 受信設定の状態 

LINE通知メッセージの受信設定には、以下の3つの状態があります。

| 状態 | 説明 |
| --- | --- |
| 同意（オン） | 受信に同意しています。LINE通知メッセージは送信されます。 |
| 拒否（オフ） | 受信を拒否しています。LINE通知メッセージは送信されません。 |
| 未設定 | まだ同意も拒否もしていない状態です。LINE通知メッセージ受信時に、LINE通知メッセージの受信への同意を求めるメッセージが送信されます。<ul><li>バージョン8.0.0以前のLINEアプリにおいてLINEアカウントを新規作成した場合などに、LINE通知メッセージの受信設定の状態は「未設定」となります。</li><li>1度でも「未設定」以外の状態に変更した場合、「未設定」状態に戻すことはできません。</li></ul> |

### LINE通知メッセージの受信への同意を行っていない際に送信されたメッセージについて 

| 状態 | 説明 |
| --- | --- |
| 拒否（オフ） | リクエストされたLINE通知メッセージは送信されず、削除されます。 |
| 未設定 | [LINE通知メッセージの受信設定](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-1)の受信後、24時間以内にLINE通知メッセージの受信に同意した場合は、メッセージは送信されます。24時間以内にLINE通知メッセージ受信同意を行わない場合、リクエストされたメッセージは送信されず削除されます。 |

### LINE公式アカウントをブロックしているユーザーに対するLINE通知メッセージAPIのリクエストについて 

LINE公式アカウントをブロックしているユーザーに対して、LINE通知メッセージAPIでLINE通知メッセージの送信をリクエストした場合、HTTPステータスコード`200`または`202`のレスポンスが返ります。ただしこの場合、実際にはLINE通知メッセージの送信は行われず、[Webhookの配信完了イベント](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/)も送られません。

### LINE通知メッセージAPIのリクエストが成功したが、メッセージが送信されない場合について 

LINE公式アカウントをブロックしていないユーザーに対して、LINE通知メッセージAPIをリクエストし成功した（HTTPステータスコード`200`または`202`のレスポンスを受信した）が、実際にユーザーに対してLINE通知メッセージが送信されない場合、下記のような原因が考えられます。

- LINE通知メッセージAPIリクエスト時に指定した電話番号に紐づくユーザーは、LINE通知メッセージの受信設定が未設定であり、[LINE通知メッセージの受信設定](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-1)を受信した際に、「拒否」に変更した。
- LINE通知メッセージAPIリクエスト時に指定した電話番号に紐づくユーザーは、LINE通知メッセージの受信設定が未設定であり、[LINE通知メッセージの受信設定](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-1)を受信した際に、設定を行わずに放置した。
- LINE通知メッセージAPIリクエスト時に指定した電話番号に紐づくユーザーは、SMS認証が必要な状態であったが、[電話番号の認証](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/flow-when-receiving-message/#user-consent-flow-for-receiving-line-notification-messages-3)メッセージを受信した際にSMS認証を行わずに放置した。

### LINE公式アカウントと友だちではないユーザーにLINE通知メッセージを送信した際の友だち追加やブロックについて 

LINE通知メッセージ送信元のLINE公式アカウントと友だちではないユーザーが、LINE通知メッセージを受信した際には、そのLINE公式アカウントを友だち追加するかどうか選択できます。友だち追加を行った場合、[フォローイベント](https://developers.line.biz/ja/reference/messaging-api/#follow-event)が送信されます。ブロックを行った場合、[フォロー解除イベント](https://developers.line.biz/ja/reference/messaging-api/#unfollow-event)が送信されます。LINE通知メッセージを利用する場合、フォローイベントを受信したことがないユーザーからフォロー解除イベントが送信される場合があります。

### LINE公式アカウントと友だちではないユーザーにLINE通知メッセージを送信した際のリッチメニューの表示について 

LINE通知メッセージを受信したユーザーは、LINE公式アカウントと友だちにならなくても1対1のトーク画面を開いて、リッチメニューを利用できます。このとき、[LINE Official Account Manager](https://developers.line.biz/ja/docs/messaging-api/rich-menus-overview/#creating-a-rich-menu-with-the-line-manager)または[Messaging API](https://developers.line.biz/ja/docs/messaging-api/using-rich-menus/#set-the-default-rich-menu)で設定したデフォルトのリッチメニューは表示されますが、[Messaging APIで設定するユーザー単位のリッチメニュー](https://developers.line.biz/ja/reference/messaging-api/#link-rich-menu-to-user)は表示されません。

![友だちにならなくてもリッチメニューは利用できる](https://developers.line.biz/media/line-notification-message/about-richmenu-displayed.png)

また、LINE通知メッセージを受信したユーザーはLINE公式アカウントと友だちにならなくても、LINE公式アカウントにメッセージを送ることができます。そのため、Webhookで友だちでないユーザーの[ポストバックイベント](https://developers.line.biz/ja/reference/messaging-api/#postback-event)や[メッセージイベント](https://developers.line.biz/ja/reference/messaging-api/#message-event)が届くことがあります。

### LINE通知メッセージの利用料金の請求対象について 

LINE通知メッセージでは、**実際にユーザーに送信が行われたメッセージのみ**が利用料金の請求対象となります。

実際にユーザーに送信が行われたメッセージの数は、APIで取得できます。詳しくは、「[送信済みLINE通知メッセージの数を取得する](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/technical-specs/#get-number-of-sent-line-notification-messages)」を参照してください。
