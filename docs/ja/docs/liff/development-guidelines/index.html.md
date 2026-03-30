# LIFFアプリ開発ガイドライン

LIFFを使ったウェブアプリを開発する際は、以下の開発ガイドラインに従ってください。

- [ユーザー情報は必ず安全に取り扱う](https://developers.line.biz/ja/docs/liff/development-guidelines/#liff-development-rules1)
- [LIFFアプリを初期化する際の注意点](https://developers.line.biz/ja/docs/liff/development-guidelines/#liff-development-rules2)
- [LIFFアプリを開発する際に必ず守るべきこと](https://developers.line.biz/ja/docs/liff/development-guidelines/#liff-development-rules3)
- [LINEプラットフォームへの大量リクエストの禁止](https://developers.line.biz/ja/docs/liff/development-guidelines/#prohibiting-mass-requests-to-line-platform)
- [ユーザー退会時の連動アプリに対する権限取消](https://developers.line.biz/ja/docs/liff/development-guidelines/#deauthorize)

LIFFはLINEログインの仕組みを利用しています。そのため、『LINEログインドキュメント』の「[LINEログイン開発ガイドライン](https://developers.line.biz/ja/docs/line-login/development-guidelines/)」の内容にも従ってください。

<!-- note start -->

**注意**

LIFF開発における基本ルールは、[規約とポリシー](https://developers.line.biz/ja/terms-and-policies/)に記載される内容に基づきます。

<!-- note end -->

## ユーザー情報は必ず安全に取り扱う 

- LIFFアプリおよびサーバーでユーザー情報を使用する場合、LIFFアプリでユーザー情報を正しく処理しないと、なりすましやその他の種類の攻撃に対して脆弱になります。LIFFアプリおよびサーバーで、LIFFアプリで取得したユーザー情報を、安全に使用する方法について詳しくは、「[LIFFアプリおよびサーバーでユーザー情報を使用する](https://developers.line.biz/ja/docs/liff/using-user-profile/)」を参照してください。
- LIFFのエンドポイントURLやLIFF URLのURLフラグメントには、アクセストークンやユーザーIDなどの機密情報が含まれます。外部にURLが漏洩しないように注意してください。

## LIFFアプリを初期化する際の注意点 

「[LIFFアプリ初期化時の注意事項](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#initializing-liff-app-notes)」を参照してください。

## LIFFアプリを開発する際に必ず守るべきこと 

- LIFFアプリをSPA（Single Page Application）で構築する場合、LIFFはフラグメントを用いたルーティングとは相性が悪いため、[History API](https://html.spec.whatwg.org/multipage/nav-history-apis.html#the-history-interface)を利用して実装してください。
- 以下のようなデバイスまたはOSの機能を利用するAPIは、必ずユーザー操作をきっかけにして実行されるように実装してください。
  - 位置情報の取得
  - カメラへのアクセス
  - マイクへのアクセス
- ユーザーの同意なく、cookie、localStorage、またはsessionStorageを使ってユーザーをトラックしたり、LINEのユーザー情報と外部セッション情報を結びつけたりしないでください。
- テスト段階のLIFFアプリに対するアクセス権限は、LIFFアプリ側で制限してください。
- LIFFアプリとLIFFアプリ内で開くコンテンツのURLスキームは、**https**である必要があります。コンテンツのURLスキームがhttpの場合は、[LINE内ブラウザ](https://developers.line.biz/ja/glossary/#line-iab)で表示されます。この場合、LIFFアプリとしてチャネルに追加されていても、LIFFアプリとして動作しません。

<!-- note start -->

**LIFFアプリにおけるcookie、localStorage、またはsessionStorageの利用**

LIFFアプリではcookie、localStorage、またはsessionStorageを利用できます。ただし、OSの仕様変更によって将来的に利用が制限される可能性があります。

<!-- note end -->

## LINEプラットフォームへの大量リクエストの禁止 

負荷テストを目的に、[LIFF URLスキーム](https://developers.line.biz/ja/docs/line-login/using-line-url-scheme/#opening-a-liff-app) （`https://liff.line.me/{liffId}`）を経由してLIFFアプリへ大量のアクセスを行ったり、[LIFF API](https://developers.line.biz/ja/reference/liff/)に大量のリクエストを送信したりしないでください。LIFFアプリの負荷テストを行う場合は、LINEプラットフォームへの大量のリクエストが発生しないテスト環境を用意してください。

<!-- note start -->

**注意**

レート制限を超えて送信を行った場合、`429 Too Many Requests`が返却され、エラーとなります。

<!-- note end -->

## ユーザー退会時の連動アプリに対する権限取消 

LIFFアプリからユーザーが退会する場合、あるいはユーザーが連動アプリとLINEアプリの連携を解除した場合は、以下を必ず行ってください。

1. ユーザーがその連動アプリに対して認可していた権限を、[連動アプリに認可した権限を取り消す](https://developers.line.biz/ja/reference/line-login/#deauthorize)エンドポイントを用いて、ユーザーの代わりに取り消してください。
1. 退会や連携解除を行ったことで何が起きるのかを、その機能のそば、もしくは会員登録時や連携時にユーザーが同意する規約などに記載してください。
   - 例：本サービスを退会すると、退会したことがLINEヤフー株式会社に通知され、本サービスとLINEの連携は解除されます。
   - 例：この操作により、LINEヤフー株式会社に通知が行われ、本サービスとLINEの連携が解除されます。

次のようなユースケースにおいて、権限の取消が必要となります。

![アカウントを連携してから解除するまでの流れ](https://developers.line.biz/media/line-login/development-guidelines/deauthorize-your-app-ja.png)

ユーザーがLINEログインを組み込んだアプリにLINEアカウントでログインし、チャネル同意画面で[認可を行う](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#authorization-process)と、LINEアプリの［**設定**］ > ［**アカウント**］ > ［**連動アプリ**］に対象アプリが表示されるようになります。ユーザーが連動アプリを退会した後も、認可した権限がそのままにならないよう、権限の取消を行ってください。

なお連動アプリに対して認可した権限をユーザー自身が取り消す方法については、『LINEログインドキュメント』の「[ユーザーによる連動アプリの管理について](https://developers.line.biz/ja/docs/line-login/managing-authorized-apps/)」を参照してください。
