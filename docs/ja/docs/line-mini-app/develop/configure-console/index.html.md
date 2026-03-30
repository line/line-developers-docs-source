# LINE DevelopersコンソールでLINEミニアプリの設定を管理する

[LINE Developersコンソール](https://developers.line.biz/console/)に登録した一部の情報は、LINEミニアプリのユーザーに表示されます。

## プロバイダー設定 

LINEミニアプリチャネルが属するプロバイダーの設定のうち、ユーザーに表示される情報は以下のとおりです。

### ［**プロバイダー設定**］タブ 

| 項目 | 画面 |
| --- | --- |
| **プロバイダー名** | <ul><li>[アクセス許可要求画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#verification-screen)</li><li>[チャネル同意画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#consent-screen-settings)</li></ul> |

## チャネル設定 

LINEミニアプリチャネルの設定のうち、ユーザーに表示される情報は以下のとおりです。

### ［**チャネル基本設定**］タブ 

| 項目 | 表示される画面 |
| --- | --- |
| **チャネルアイコン** | <ul><li>[アクションボタン](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#built-in-share-settings)</li><li>[マルチタブビュー](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#multi-tab-view-settings)</li><li>[アクセス許可要求画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#verification-screen)</li><li>[チャネル同意画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#consent-screen-settings)</li><li>[サービスメッセージのフッターセクション](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#footer-section-of-service-message)</li><li>[ショートカット追加画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#add-shortcut-screen)</li></ul>LINEミニアプリのアイコンとしてユーザーに認識される画像です。 |
| **チャネル名** | <ul><li>[アクションボタン](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#built-in-share-settings)</li><li>[マルチタブビュー](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#multi-tab-view-settings)</li><li>[アクセス許可要求画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#verification-screen)</li><li>[チャネル同意画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#consent-screen-settings)</li><li>[サービスメッセージのフッターセクション](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#footer-section-of-service-message)</li><li>[ショートカット追加画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#add-shortcut-screen)</li></ul><p>LINEミニアプリ名としてユーザーに認識されるテキストです。［**チャネル名**］は、［**ウェブアプリ設定**］タブ > ［**LIFFアプリ名**］にコピーされます。</p><p>英語で入力してください。日本語など、ほかの言語でチャネル名を入力するには、「[チャネル同意画面の多言語対応について](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#localization)」を参照してください。</p> |
| **チャネル説明** | <ul><li>[アクセス許可要求画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#verification-screen)</li><li>[チャネル同意画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#consent-screen-settings)</li></ul>英語で入力してください。日本語など、ほかの言語でチャネル説明を入力するには、「[チャネル同意画面の多言語対応について](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#localization)」を参照してください。 |
| **プライバシーポリシーURL** | [チャネル同意画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#consent-screen-settings) |
| **多言語対応** | [チャネル同意画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#consent-screen-settings) |

<!-- note start -->

**チャネル説明に含めなければいけない情報**

LINEミニアプリの開発を外部委託した場合など、LINEミニアプリのサービス事業主と開発担当企業が異なる場合は、［**チャネル説明**］には以下の内容を明記してください。

- サービス事業主名
- 開発担当企業名
- LINEミニアプリを通じて取得されたユーザーの個人情報をほかの企業に提供する場合、実際の企業名

<!-- note end -->

### ［**ウェブアプリ設定**］タブ 

| 項目                  | 表示される画面                                 |
| --------------------- | ---------------------------------------------- |
| **エンドポイントURL** | [ショートカット追加画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#add-shortcut-screen) |

## アクションボタン 

ユーザーが[アクションボタン](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#action-button)からLINEミニアプリのページをシェアしたときに、[LINE Developersコンソール](https://developers.line.biz/console/)に登録した以下の情報が、送信先のトークルームに表示されます。

![アクションボタン](https://developers.line.biz/media/line-mini-app/mini_share_builtin_share.png)

| 情報 | 設定 |
| --- | --- |
| LINEミニアプリ名 | ［**チャネル基本設定**］タブ > ［**チャネル名**］ |
| LINEミニアプリのアイコン | ［**チャネル基本設定**］タブ > ［**チャネルアイコン**］ |

## マルチタブビュー 

ユーザーが[アクションボタン](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#action-button)を押したときに、[LINE Developersコンソール](https://developers.line.biz/console/)に登録した以下の情報が、[マルチタブビュー](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#multi-tab-view)に表示されます。

![](https://developers.line.biz/media/line-mini-app/develop/mini-multi-tab-view-config-ja.png)

| 情報 | 設定 |
| --- | --- |
| LINEミニアプリ名 | ［**チャネル基本設定**］タブ > ［**チャネル名**］ |
| LINEミニアプリのアイコン | ［**チャネル基本設定**］タブ > ［**チャネルアイコン**］ |

## アクセス許可要求画面 

[LINE Developersコンソール](https://developers.line.biz/console/)に登録した以下の情報が、「[アクセス許可要求画面](https://developers.line.biz/ja/docs/line-mini-app/develop/channel-consent-simplification/#request-permissions-other-than-openid)」に表示されます。

![](https://developers.line.biz/media/line-mini-app/line-mini-app-playground-verification-screen-ja.png)

| 情報 | 設定 |
| --- | --- |
| LINEミニアプリのアイコン | ［**チャネル基本設定**］タブ > ［**チャネルアイコン**］ |
| LINEミニアプリ名 | ［**チャネル基本設定**］タブ > ［**チャネル名**］ |
| プロバイダー名 | LINEミニアプリチャネルが属するプロバイダーの［**プロバイダー設定**］タブ > ［**プロバイダー名**］ |
| 説明 | ［**チャネル基本設定**］タブ > ［**チャネル説明**］ |

## チャネル同意画面 

[LINE Developersコンソール](https://developers.line.biz/console/)に登録した以下の情報が、[チャネル同意画面](https://developers.line.biz/ja/docs/line-mini-app/develop/channel-consent-simplification/#authorization-flow-disabled)に表示されます。

![チャネル同意画面](https://developers.line.biz/media/line-mini-app/mini-permission-request-ja.png)

| 情報 | 設定 |
| --- | --- |
| LINEミニアプリのアイコン | ［**チャネル基本設定**］タブ > ［**チャネルアイコン**］ |
| LINEミニアプリ名 | ［**チャネル基本設定**］タブ > ［**チャネル名**］ |
| プロバイダー名 | LINEミニアプリチャネルが属するプロバイダーの［**プロバイダー設定**］タブ > ［**プロバイダー名**］ |
| 説明 | ［**チャネル基本設定**］タブ > ［**チャネル説明**］ |
| プライバシーポリシーページのURL | ［**チャネル基本設定**］タブ > ［**プライバシーポリシーURL**］ |

なお、LINEミニアプリが認証済ミニアプリの場合は、LINEミニアプリ名の横に認証バッジが表示されます。また、LINEミニアプリの提供者が認証プロバイダーでない場合は、「LINEヤフー株式会社は提供元を確認していません。」という注意書きが表示されます。

### チャネル同意画面の多言語対応について 

チャネル同意画面のLINEミニアプリ名と説明は、ユーザーがLINEで設定した言語で表示されます。たとえば、ユーザーがLINEの言語を日本語に設定していた場合は、［**日本語**］に設定したチャネル名とチャネル説明が表示されます。

| 情報 | 設定 |
| --- | --- |
| LINEミニアプリ名 | ［**チャネル基本設定**］タブ > ［**多言語対応**］ > ［**チャネル名**］ |
| 説明 | ［**チャネル基本設定**］タブ > ［**多言語対応**］ > ［**チャネル説明**］ |

<!-- note start -->

**注意**

- LINEミニアプリでサービスを提供している国で使用されている主な言語に対応してください。
- ユーザーがLINEで設定した言語に対応する情報が［**多言語対応**］で設定されていない場合は、［**チャネル名**］と［**チャネル説明**］に設定した英語の情報が表示されます。

<!-- note end -->

## サービスメッセージのフッターセクション 

[LINE Developersコンソール](https://developers.line.biz/console/)に登録した以下の情報が、サービスメッセージのフッターセクションに表示されます。サービスメッセージについて詳しくは、「[サービスメッセージを送信する](https://developers.line.biz/ja/docs/line-mini-app/develop/service-messages/)」を参照してください。

![サービスメッセージ](https://developers.line.biz/media/line-mini-app/mini_service_notifier.png)

| 情報             | 設定                                                    |
| ---------------- | ------------------------------------------------------- |
| LINEミニアプリ名 | ［**チャネル基本設定**］タブ > ［**チャネル名**］       |
| 画像             | ［**チャネル基本設定**］タブ > ［**チャネルアイコン**］ |

## ショートカット追加画面 

[LINE Developersコンソール](https://developers.line.biz/console/)に登録した以下の情報が、ショートカット追加画面に表示されます。ショートカット追加画面について詳しくは、「[ユーザー端末のホーム画面にLINEミニアプリへのショートカットを追加する](https://developers.line.biz/ja/docs/line-mini-app/develop/add-to-home-screen/)」を参照してください。

![](https://developers.line.biz/media/line-mini-app/develop/add-to-home-screen/add-shortcut-screen-ios-ja.png)

| 情報 | 設定 |
| --- | --- |
| LINEミニアプリ名 | ［**チャネル基本設定**］タブ > ［**チャネル名**］ |
| LINEミニアプリのアイコン | ［**チャネル基本設定**］タブ > ［**チャネルアイコン**］ |
| LINEミニアプリのエンドポイントURL | ［**ウェブアプリ設定**］タブ > ［**エンドポイントURL**］ |
