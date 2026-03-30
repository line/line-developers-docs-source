# ユーザーを管理する（LINEログイン v2.0）

<!-- warning start -->

**LINEログイン v2.0は非推奨です**

このページは旧バージョンのLINEログイン v2.0に関するドキュメントです。LINEログイン v2.0は[非推奨](https://developers.line.biz/ja/glossary/#deprecated)であり、時期は未定ですが[廃止](https://developers.line.biz/ja/glossary/#end-of-life)を予定しているため、現行バージョン（LINEログイン v2.1）の利用を推奨します。なお廃止時期の告知から、実際の廃止までは一定の猶予期間を置く予定です。詳しくは、「[LINEログインのバージョンについて](https://developers.line.biz/ja/docs/line-login/overview/#versions)」を参照してください。

<!-- warning end -->

ここでは、[LINEログイン v2.0](https://developers.line.biz/ja/docs/line-login/overview/#versions)のエンドポイントを使って、LINEログインしたユーザーを管理する方法を説明します。

## ユーザープロフィールを取得する 

[アクセストークン](https://developers.line.biz/ja/docs/line-login/managing-access-tokens/)で特定されるユーザーのプロフィール情報を取得できます。プロフィール情報には、ユーザーID、表示名、プロフィール画像、およびステータスメッセージが含まれます。

ユーザープロフィールの取得方法は、LINEログイン v2.0とLINEログイン v2.1で共通です。詳しくは、「[ユーザープロフィールを取得する](https://developers.line.biz/ja/docs/line-login/managing-users/#get-profile)」を参照してください。

## ユーザーをログアウトする 

<!-- note start -->

**注意**

ここでは、LINEログイン v2.0のエンドポイントを使ってユーザーをログアウトする方法について説明します。最新のLINEログイン v2.1を使う方法については、「[ユーザーをログアウトする](https://developers.line.biz/ja/docs/line-login/managing-users/#logout)」を参照してください。

<!-- note end -->

より良いユーザー体験のために、ユーザーがアプリからログアウトする操作を提供することをお勧めします。

ユーザーがアプリからログアウトする操作を行ったときに、ユーザーの[アクセストークン](https://developers.line.biz/ja/docs/line-login/managing-access-tokens/)を取り消し、アプリ内のすべてのユーザーデータを削除してください。

アクセストークンを取り消すリクエストの例：

```sh
curl -v -X POST https://api.line.me/v2/oauth/revoke \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'refresh_token={refresh token}'
```

詳しくは、『LINEログイン v2.0 APIリファレンス』の「[アクセストークンを取り消す](https://developers.line.biz/ja/reference/line-login-v2/#revoke-access-token)」を参照してください。
