# モジュールチャネルを連携（アタッチ）する

<!-- note start -->

**オプション機能を利用するには手続きが必要です**

本ドキュメントに記載の機能は、所定の申請等を行った法人ユーザーのみがご利用いただけます。モジュールを利用した拡張機能の公開を希望するお客様は、担当営業までご連絡いただくか、[LINEマーケットプレイス お問い合わせ](https://line-marketplace.com/jp/inquiry)よりお問い合わせください。

<!-- note end -->

モジュールチャネルの機能を利用するには、以下の手順に従って、LINE公式アカウントの管理者からの認可と、モジュールチャネルの連携（アタッチ）が必要です。

## OAuth 2.0の認可の仕組みを利用してモジュールチャネルをアタッチする 

OAuth 2.0の認可の仕組みのフローに従って、LINE公式アカウントの管理者から認可を得ることで、モジュールチャネルをアタッチできます。

## モジュールをアタッチするためのフロー 

1つ目の画面と5つ目の画面は、モジュールチャネルの開発担当企業が準備してください。

![OAuth 2.0の認可の仕組みを使ったモジュールチャネルのアタッチするフロー](https://developers.line.biz/media/partner-docs/module-technical/flow-ja.png)

<!-- note start -->

**LINE公式アカウントに複数のモジュールチャネルをアタッチする際の制限**

「Default Active」の機能が付与されたモジュールチャネルは、1つのLINE公式アカウントに複数アタッチすることはできません。

<!-- note end -->

1. [LINE公式アカウントの管理者に認可を要求する](https://developers.line.biz/ja/docs/partner-docs/module-technical-attach-channel/#request-auth-from-line-oa-admin)
1. [連携画面について](https://developers.line.biz/ja/docs/partner-docs/module-technical-attach-channel/#about-linkage-screen)
1. [認可コードまたはエラーコードを受け取る](https://developers.line.biz/ja/docs/partner-docs/module-technical-attach-channel/#get-auth-code)
1. [モジュールチャネルの提供者の操作で連携（アタッチ）する](https://developers.line.biz/ja/docs/partner-docs/module-technical-attach-channel/#link-attach-by-operation-of-module-channel-provider)

### 1. LINE公式アカウントの管理者に認可を要求する 

LINE公式アカウントの管理者に、認証と認可のためのURL（認可URL`https://manager.line.biz/module/auth/v1/authorize`にクエリパラメータを付けたもの）にアクセスしてもらうことで、LINE公式アカウントへモジュールチャネルをアタッチするプロセスが開始されます。

**認証と認可のためのURLの例**

```
https://manager.line.biz/module/auth/v1/authorize?response_type=code&client_id=1234567890&redirect_uri=https%3A%2F%2Fexample.com%2Fcallback&scope=message%3Asend%20message%3Areceive&state={CSRF token}&region=JP&basic_search_id={LINE Official Account basic ID}&brand_type=premium
```

一般的には、モジュールチャネルの連携を開始するためのページに、このURLにアクセスするリンクを設置し、LINE公式アカウントの管理者にリンクをクリックしてもらいます。上記の例で提示されているフローでは、「【貴社サービス内】連携開始ページ」で、［**Attach Module**］ボタンをクリックしたときに、このURLにアクセスするように設定しています。

#### クエリパラメータ 

<!-- parameter start (props: required) -->

response_type

String

`code`

<!-- parameter end -->
<!-- parameter start (props: required) -->

redirect_uri

String

リダイレクトURL。モジュールチャネルの開発担当企業が、認可コードを受け取るためのURLです。認証と認可（連携画面での操作）の後に、LINE公式アカウントの管理者がこのURLにリダイレクトされます。

このURLは、モジュールチャネルの開発担当企業が用意してください。なお、このURLはあらかじめ[LINE Developersコンソール](https://developers.line.biz/console/)でモジュールチャネルに登録したリダイレクトURLと一致させてください。

<!-- note start -->

**redirect_uriにはURLエンコードした値を指定してください**

クエリパラメータのURLエンコードを忘れると、2つ目以降のクエリパラメータが認証URLに対するクエリパラメータとして認識され、リダイレクト先に渡されません。

例えば、`redirect_uri`に`https://example.com/auth?param1=value1&param2=value2`を指定する場合、認証と認可のためのURLは`https://manager.line.biz/module/auth/v1/authorize?response_type=code&client_id=1234567890&redirect_uri=https%3A%2F%2Fexample.com%2Fauth%3Fparam1%3Dvalue1%26param2%3Dvalue2&scope=message%3Asend%20message%3Areceive&state={CSRF token}&region=JP&basic_search_id={LINE Official Account basic id}&brand_type=premium`とします。

<!-- note end -->

<!-- parameter end -->
<!-- parameter start (props: required) -->

client_id

String

モジュールチャネルのチャネルID。LINEプラットフォームが発行した、チャネル固有の識別子です。

<!-- parameter end -->
<!-- parameter start (props: required) -->

scope

String

LINE公式アカウントの管理者に許可を求める権限（スコープ）を指定します。複数のスコープを指定する場合は、URLエンコードされた空白文字（%20）で区切って指定してください。詳しくは、「[スコープ](https://developers.line.biz/ja/docs/partner-docs/module-technical-attach-channel/#scopes)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

state

String

[クロスサイトリクエストフォージェリ（CSRF）](https://datatracker.ietf.org/doc/html/rfc6749#section-10.12)防止用の固有な英数字の文字列。モジュールチャネルの開発担当企業のシステムでランダムにユニークな値を生成する必要があります。URLエンコードされた文字列は使用できません。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

region

String

モジュールチャネルをアタッチするLINE公式アカウントの地域。`JP`や`TW`を指定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

basic_search_id

String

LINE公式アカウントの[ベーシックID](https://help.linebiz.com/lineadshelp/s/article/L000001191?language=ja)。特定のLINE公式アカウントにのみモジュールチャネルへのアタッチを許可する場合に指定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

brand_type

String

アタッチ可能な[LINE公式アカウントのアカウント種別](https://www.lycbiz.com/jp/service/line-official-account/account-type/)を制限する場合に指定します。

- プレミアムアカウント: `premium`
- 認証済アカウント: `verified`
- 未認証アカウント: `unverified`

複数のアカウント種別を指定する場合には、URLエンコードされた空白文字（%20）で連結します。例えば、プレミアムアカウントおよび認証済アカウントのみアタッチ可能なように制限する場合は`brand_type=premium%20verified`とします。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

code_challenge

String

認可コード横取り攻撃への対策としてOAuth 2.0の拡張仕様で定義されるPKCE（Proof Key for Code Exchange）を利用する場合に指定します。[RFC 7636](https://datatracker.ietf.org/doc/html/rfc7636)に準拠しています。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

code_challenge_method

String

`S256`

認可コード横取り攻撃への対策としてOAuth 2.0の拡張仕様で定義されるPKCE（Proof Key for Code Exchange）を利用する場合に指定します。[RFC 7636](https://datatracker.ietf.org/doc/html/rfc7636)に準拠しています。

<!-- parameter end -->

#### スコープ 

`scope`パラメータに指定できるスコープは以下のとおりです。複数のスコープを指定するには、URLエンコードされた空白文字（%20）で区切って指定します。

| スコープ | モジュールチャネルで利用できるAPI |
| --- | --- |
| 指定不要（デフォルト） | スコープ不要で利用できます。<ul><li>[連携トークンを発行する（/v2/bot/user/{userId}/linkToken）](https://developers.line.biz/ja/reference/messaging-api/#issue-link-token)</li></ul> |
| `message%3Asend`<br />(message:send) | <ul><li>[応答メッセージを送る（/v2/bot/message/reply）](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)</li><li>[プッシュメッセージを送る（/v2/bot/message/push）](https://developers.line.biz/ja/reference/messaging-api/#send-push-message)</li><li>[マルチキャストメッセージを送る（/v2/bot/message/multicast）](https://developers.line.biz/ja/reference/messaging-api/#send-multicast-message)</li><li>[ブロードキャストメッセージを送る（/v2/bot/message/broadcast）](https://developers.line.biz/ja/reference/messaging-api/#send-broadcast-message)</li><li>[ナローキャストメッセージを送る（/v2/bot/message/narrowcast）](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message) および関連API</li><li>[オーディエンス管理（/v2/bot/audienceGroup/\*\*\*）](https://developers.line.biz/ja/reference/messaging-api/#manage-audience-group)</li><li>[当月に送信できるメッセージ数の上限目安を取得する（/v2/bot/message/quota）](https://developers.line.biz/ja/reference/messaging-api/#get-quota)</li><li>[当月のメッセージ利用状況を取得する（/v2/bot/message/quota/consumption）](https://developers.line.biz/ja/reference/messaging-api/#get-consumption)</li><li>[ローディングのアニメーションを表示する（/v2/bot/chat/loading/start）](https://developers.line.biz/ja/reference/messaging-api/#display-a-loading-indicator)</li></ul> |
| `message%3Areceive`<br />(message:receive) | <ul><li>Messaging APIおよびModule Channel APIのWebhookイベントの受信</li><ul><li>[Webhook](https://developers.line.biz/ja/reference/messaging-api/#webhooks)</li><li>[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#webhook-event-objects)</li></ul><li>[チャットの主導権（Chat Control）](https://developers.line.biz/ja/docs/partner-docs/module-technical-chat-control/#what-is-chat-control)</li></ul> |
| `account%3Amanage`<br />(account:manage) | <ul><li>[デフォルトのリッチメニューを設定する（/v2/bot/user/all/richmenu/{richMenuId}）](https://developers.line.biz/ja/reference/messaging-api/#set-default-rich-menu)</li><li>[メッセージの送信数を取得する（/v2/bot/insight/message/delivery?date={date}）](https://developers.line.biz/ja/reference/messaging-api/#get-number-of-delivery-messages)</li><li>[友だち数を取得する（/v2/bot/insight/followers?date={date}）](https://developers.line.biz/ja/reference/messaging-api/#get-number-of-followers)</li><li>[友だちの属性情報に基づく統計情報を取得する（/v2/bot/insight/demographic）](https://developers.line.biz/ja/reference/messaging-api/#get-demographic)</li><li>[ユーザーの操作に基づく統計情報を取得する（/v2/bot/insight/message/event?requestId={requestId}）](https://developers.line.biz/ja/reference/messaging-api/#get-message-event)</li><li>[ユニットごとの統計情報を取得する（/v2/bot/insight/message/event/aggregation?customAggregationUnit={customAggregationUnit}&from={from}&to={to}）](https://developers.line.biz/ja/reference/messaging-api/#get-statistics-per-unit)</li></ul> |
| `message%3Amark_as_read`<br />(message:mark_as_read) | <ul><li>[ユーザーからのメッセージに既読を付ける（/v2/bot/message/markAsRead）](https://developers.line.biz/ja/reference/partner-docs/#mark-messages-from-users-as-read)</li></ul> |
| `message%3Atemplated_pnp`<br />(message:templated_pnp) | <ul><li>[LINE通知メッセージ（テンプレート）を送る（/v2/bot/message/pnp/templated/push）](https://developers.line.biz/ja/reference/line-notification-messages/#send-line-notification-message-template)</li><li>[送信済みのLINE通知メッセージ（テンプレート）の数を取得する（/v2/bot/message/delivery/pnp/templated）](https://developers.line.biz/ja/reference/line-notification-messages/#get-number-of-sent-line-notification-messages-template)</li><li>LINE通知メッセージの配信が完了した際に送信されるWebhookイベントの受信（[Webhookの配信完了イベント](https://developers.line.biz/ja/docs/partner-docs/line-notification-messages/message-sending-complete-webhook-event/)）</li></ul> |
| `profile%3Aread`<br />(profile:read) | <ul><li>[プロフィール情報を取得する（/v2/bot/profile/{userId}）](https://developers.line.biz/ja/reference/messaging-api/#get-profile)</li><li>[グループトークの概要を取得する（/v2/bot/group/{groupId}/summary）](https://developers.line.biz/ja/reference/messaging-api/#get-group-summary)</li><li>[グループトークのメンバーのプロフィール情報を取得する（/v2/bot/group/{groupId}/member/{userId}）](https://developers.line.biz/ja/reference/messaging-api/#get-group-member-profile)</li><li>[複数人トークのメンバーのプロフィールを取得する（/v2/bot/room/{roomId}/member/{userId}）](https://developers.line.biz/ja/reference/messaging-api/#get-room-member-profile)</li><li>[グループトークに参加しているユーザーの人数を取得する（/v2/bot/group/{groupId}/members/count）](https://developers.line.biz/ja/reference/messaging-api/#get-members-group-count)</li><li>[複数人トークに参加しているユーザーの人数を取得する（/v2/bot/room/{roomId}/members/count）](https://developers.line.biz/ja/reference/messaging-api/#get-members-room-count)</li></ul> |
| `coupon%3Amanage`<br />(coupon:manage) | <ul><li>[クーポンを作成する（/v2/bot/coupon）](https://developers.line.biz/ja/reference/messaging-api/#create-coupon)</li><li>[クーポンを終了する（/v2/bot/coupon/{couponId}/close）](https://developers.line.biz/ja/reference/messaging-api/#discontinue-coupon)</li><li>[クーポンの一覧を取得する（/v2/bot/coupon）](https://developers.line.biz/ja/reference/messaging-api/#get-coupons-list)</li><li>[クーポンの詳細を取得する（/v2/bot/coupon/{couponId}）](https://developers.line.biz/ja/reference/messaging-api/#get-coupon)</li><li>メッセージタイプに[クーポンメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#coupon-messages)を指定してメッセージを送る</li></ul> |
| `crm%3Amanage`<br />(crm:manage) | このスコープはChat Plugin機能（※）を利用するモジュールチャネルでのみ指定が可能です。それ以外の場合は指定しないでください。<br />Chat Plugin機能を利用する場合は必須となります。Chat Plugin機能を利用するモジュールチャネルにおいて、このスコープを指定していなかった場合、今後Chat Pluginで提供される機能を利用することができない場合があります。 |

（※）Chat Plugin機能は、現在一部の法人ユーザーにのみ公開しています。

### 2. 連携画面について 

LINE公式アカウントの管理者が、認証と認可のためのURLにアクセスすると、LINE Official Account Managerの連携画面が表示されます。連携画面には、モジュールチャネル作成時に申請した内容が表示されます。設定内容は、[LINE Developersコンソール](https://developers.line.biz/console/)で確認できます。

![連携画面](https://developers.line.biz/media/partner-docs/attach-disp-ja.png)

### 3. 認可コードまたはエラーコードを受け取る 

LINE公式アカウントの管理者が認証と認可を終了すると、認証と認可のためのURLで指定したリダイレクトURL（`redirect_uri`）に、以下のクエリパラメータを通じて認可コードやエラーコードが渡されます。上記の例で提示されている[フロー](https://developers.line.biz/ja/docs/partner-docs/module-technical-attach-channel/#attach-flow)では、「【OAM】確認および連携」で［**連携**］ボタンをクリックしたときに認可コードやエラーコードが渡されます。

#### 認可コードを受け取る 

LINE公式アカウントの管理者による認証と認可が完了すると、以下のクエリパラメータが付与されたリダイレクトURL（`redirect_uri`）にリダイレクトされます。

##### クエリパラメータ 

<!-- parameter start -->

code

String

LINE公式アカウントに連携（アタッチ）するときに必要な認可コードです。認可コードには有効期間があります。また、認可コードは1回のみ使用できます。

<!-- parameter end -->
<!-- parameter start -->

state

String

CSRF対策用の文字列です。認証と認可のためのURLの`state`クエリパラメータで指定した文字列と同じものであることを確認してください。

<!-- parameter end -->

#### エラーコードを受け取る 

LINE公式アカウントの管理者が認可を拒否した場合、以下のクエリパラメータが付与されたリダイレクトURL（`redirect_uri`）にリダイレクトされます。

##### クエリパラメータ 

<!-- parameter start -->

error

String

エラーコードです。

<!-- parameter end -->
<!-- parameter start -->

error_description

String

エラーの詳細です。

<!-- parameter end -->
<!-- parameter start -->

state

String

CSRF対策用の文字列です。認証と認可のためのURLの`state`クエリパラメータで指定した文字列と同じものであることを確認してください。

<!-- parameter end -->

### 4. モジュールチャネルの提供者の操作で連携（アタッチ）する 

認可コードを取得し、`state`クエリパラメータで渡された文字列に問題がないことが確認できたら、モジュールチャネルをLINE公式アカウントにアタッチします。

詳しくは、『法人ユーザー向けオプションAPIリファレンス』の「[モジュールチャネルの提供者の操作で連携（アタッチ）する](https://developers.line.biz/ja/reference/partner-docs/#link-attach-by-operation-module-channel-provider)」を参照してください。
