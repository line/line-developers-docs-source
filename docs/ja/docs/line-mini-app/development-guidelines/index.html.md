# LINEミニアプリ開発ガイドライン

LINEミニアプリを使ったウェブアプリを開発する際は、以下の開発ガイドラインに従ってください。

- [LINEプラットフォームへの大量リクエストの禁止](https://developers.line.biz/ja/docs/line-mini-app/development-guidelines/#prohibiting-mass-requests-to-line-platform)
- [ログ保存の推奨](https://developers.line.biz/ja/docs/line-mini-app/development-guidelines/#save-logs)
- [ユーザー退会時の連動アプリに対する権限取消](https://developers.line.biz/ja/docs/line-mini-app/development-guidelines/#deauthorize)

LINEミニアプリはLIFFで提供される仕組みを利用しています。そのため、『LIFFドキュメント』の「[LIFFアプリ開発ガイドライン](https://developers.line.biz/ja/docs/liff/development-guidelines/)」の内容にも従ってください。

<!-- note start -->

**注意**

LINEミニアプリ開発における基本ルールは、[規約とポリシー](https://developers.line.biz/ja/terms-and-policies/)に記載される内容に基づきます。

<!-- note end -->

## LINEプラットフォームへの大量リクエストの禁止 

負荷テストを目的に、[LIFF URLスキーム](https://developers.line.biz/ja/docs/line-login/using-line-url-scheme/#opening-a-liff-app) （`https://miniapp.line.me/{liffId}`）を経由してLINEミニアプリへ大量のアクセスを行ったり、[LIFF API](https://developers.line.biz/ja/reference/liff/)や[サービスメッセージAPI](https://developers.line.biz/ja/reference/line-mini-app/)に大量のリクエストを送信したりしないでください。LINEミニアプリの負荷テストを行う場合は、LINEプラットフォームへの大量のリクエストが発生しないテスト環境を用意してください。

<!-- note start -->

**注意**

レート制限を超えて送信を行った場合、`429 Too Many Requests`が返却され、エラーとなります。

<!-- note end -->

## ログ保存の推奨 

問題が発生した際に、開発者自身が原因や影響範囲の調査を円滑に行えるよう、[サービスメッセージAPI](https://developers.line.biz/ja/reference/line-mini-app/)のリクエストのログを一定期間保存することを推奨します。

### サービスメッセージAPIリクエスト時のログ 

[サービスメッセージAPI](https://developers.line.biz/ja/reference/line-mini-app/)のリクエストを行った際は、レスポンスに含まれる、[サービス通知トークン](https://developers.line.biz/ja/reference/line-mini-app/#issue-notification-token-response)`notificationToken`に加え、以下の情報をログとして保存することを推奨します。

- APIリクエストを行った時間
- リクエストメソッド
- APIエンドポイント
- LINEプラットフォームからレスポンスされた[ステータスコード](https://developers.line.biz/ja/reference/line-mini-app/)

具体的には、以下のような形式でログファイルなどに保存します。

| APIリクエストを行った時間 | リクエストメソッド | APIエンドポイント | ステータスコード |
| --- | --- | --- | --- |
| Mon, 16 Jul 2021 10:20:23 GMT | POST | `https://api.line.me/message/v3/notifier/send?target=service` | 200 |

<!-- tip start -->

**追加でログに保存しておくと有用な情報**

運用するLINEミニアプリの要件等によっては、上記に加えて、たとえば以下のような情報を保存しておくことで、問題が発生した際の調査をより円滑に行うことができます。

- サービスメッセージAPIに対するリクエストのボディ
- APIリクエスト後にLINEプラットフォームから返却されたサービス通知トークン`notificationToken`以外のレスポンスのボディ

<!-- tip end -->

<!-- note start -->

**ログの提供は行っておりません**

サービスメッセージAPIのリクエストのログ等は、お問い合わせいただいても提供は行っておりません。ログの保存は、LINEミニアプリを開発する開発者自身で行ってください。

<!-- note end -->

## ユーザー退会時の連動アプリに対する権限取消 

LINEミニアプリからユーザーが退会する場合、あるいはユーザーが連動アプリとLINEアプリの連携を解除した場合は、以下を必ず行ってください。

1. ユーザーがその連動アプリに対して認可していた権限を、[連動アプリに認可した権限を取り消す](https://developers.line.biz/ja/reference/line-login/#deauthorize)エンドポイントを用いて、ユーザーの代わりに取り消してください。
1. 退会や連携解除を行ったことで何が起きるのかを、その機能のそば、もしくは会員登録時や連携時にユーザーが同意する規約などに記載してください。
   - 例：本サービスを退会すると、退会したことがLINEヤフー株式会社に通知され、本サービスとLINEの連携は解除されます。
   - 例：この操作により、LINEヤフー株式会社に通知が行われ、本サービスとLINEの連携が解除されます。

次のようなユースケースにおいて、権限の取消が必要となります。

![アカウントを連携してから解除するまでの流れ](https://developers.line.biz/media/line-login/development-guidelines/deauthorize-your-app-ja.png)

ユーザーがLINEログインを組み込んだアプリにLINEアカウントでログインし、チャネル同意画面で[認可を行う](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#authorization-process)と、LINEアプリの［**設定**］ > ［**アカウント**］ > ［**連動アプリ**］に対象アプリが表示されるようになります。ユーザーが連動アプリを退会した後も、認可した権限がそのままにならないよう、権限の取消を行ってください。

なお連動アプリに対して認可した権限をユーザー自身が取り消す方法については、『LINEログインドキュメント』の「[ユーザーによる連動アプリの管理について](https://developers.line.biz/ja/docs/line-login/managing-authorized-apps/)」を参照してください。
