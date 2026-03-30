# LINE Developersコンソールへのログイン

[LINE Developersコンソール](https://developers.line.biz/console/)へのログインには、[ビジネスID](https://help2.line.me/business_id/web/?lang=ja&contentId=20011264)と開発者アカウントが必要です。

このページでは、LINE Developersコンソールへのログイン方法や、開発者アカウントの作成方法、ビジネスIDとLINEアカウントとの連携方法について説明します。

## LINE Developersコンソールにログインする 

LINE Developersコンソールにログインするには、[LINE Developersサイト](https://developers.line.biz/)の右上にある［**[コンソールにログイン](https://developers.line.biz/console/)**］をクリックします。

![コンソールにログインをクリック](https://developers.line.biz/media/line-developers-console/login-account-02-ja.png)

ビジネスIDのログイン画面が表示されるので、ログイン方法を選んでログインしてください。ビジネスIDには、以下のいずれかのアカウントでログインします。

- [LINEアカウント](https://developers.line.biz/ja/docs/line-developers-console/login-account/#line-account)
- [ビジネスアカウント](https://developers.line.biz/ja/docs/line-developers-console/login-account/#business-account)
- [Yahoo! JAPAN ID](https://developers.line.biz/ja/docs/line-developers-console/login-account/#yahoo-japan-id) （日本でのみ利用できます）

ログイン方法の違いについて詳しくは、ヘルプセンターの「[ログイン方法の違い](https://help2.line.me/business_id/web/?lang=ja&contentId=20011265)」を参照してください。

![](https://developers.line.biz/media/line-developers-console/login-account-01-ja.png)

### LINEアカウントでログインする 

LINEアカウントでビジネスIDにログインする場合、以下のいずれかの認証方法でログインできます。

- **自動ログイン**：LINEがインストールされているスマートフォンから、操作なしでログイン
- **メールアドレスログイン**：LINEアカウントのメールアドレスとパスワードを入力してログイン
- **QRコードログイン**：表示されたQRコードを、スマートフォン版LINEのQRコードリーダーでスキャンしてログイン
- **シングルサインオン（SSO）によるログイン**：「次のアカウントでログイン」と表示された確認画面でログインボタンをクリックしてログイン

<!-- tip start -->

**LINEアカウントでのログインでは二要素認証が有効です**

LINEアカウントでのログインは、二要素認証が有効になっています。パソコンのブラウザからメールアドレスログインをする場合、LINEアカウントのメールアドレスとパスワードを入力した後、画面に表示された認証番号をスマートフォン版LINEで入力してください。

![二要素認証の流れ](https://developers.line.biz/media/news/login-flow-with-2fa-ja.png)

二要素認証を一度実施すると、ログインに使用したブラウザでは1年間、二要素認証が不要になります。また、すでに[LINE Official Account Manager](https://manager.line.biz/)へ二要素認証を用いてログイン済みの場合は、同じアカウントでLINE Developersコンソールへログインする際に二要素認証は求められません。

<!-- tip end -->

### ビジネスアカウントでログインする 

ビジネスアカウントでビジネスIDにログインする場合、ビジネスIDに登録しているメールアドレスとパスワードを入力することでログインできます。

### Yahoo! JAPAN IDでログインする 

Yahoo! JAPAN IDでビジネスIDにログインする場合、Yahoo! JAPAN IDを[Yahoo! JAPANビジネスID](https://support.yahoo-net.jp/PccBizmanager/s/article/H000011271)と連携している必要があります。

なお、Yahoo! JAPAN IDを使ったビジネスIDへのログインは日本でのみ利用できます。

Yahoo! JAPAN IDのログイン方法について詳しくは、『Yahoo! JAPAN IDガイド』の「[どんなログイン方法があるの？](https://id.yahoo.co.jp/login/login_methods.html)」を参照してください。

## 開発者アカウントを作成する（初回ログイン時のみ） 

LINEアカウントまたはビジネスアカウントで[LINE Developersコンソール](https://developers.line.biz/console/)に初めてログインしたら、開発者アカウントを作成します。［**開発者名**］と［**メールアドレス**］を入力します。[LINE開発者契約](https://terms2.line.me/LINE_Developers_Agreement?lang=ja)をよく読み、同意できる場合はチェックボックスにチェックを入れて、［**アカウントの作成**］をクリックします。この作業は、初回ログイン時のみ必要です。

![開発者アカウント作成画面](https://developers.line.biz/media/line-developers-console/developer-registration-01-ja.png)

開発者アカウントが作成できたら、開発者アカウント作成完了画面が表示されます。

![開発者アカウント作成完了画面](https://developers.line.biz/media/line-developers-console/developer-registration-02-ja.png)

## アカウントの関係 

LINE Developersコンソールの利用には開発者アカウントが必要となります。また、開発者アカウントには必ず1対1でビジネスIDが紐づけられます。LINE Developersコンソールへの初回ログイン時に[開発者アカウントを作成](https://developers.line.biz/ja/docs/line-developers-console/login-account/#register-as-developer)することで、ビジネスIDと開発者アカウントが自動的に紐づきます。

<!-- note start -->

**開発者アカウントとビジネスIDの紐づけに関する注意**

- 開発者アカウントに紐づけられたビジネスIDを削除すると、開発者アカウントへのログインができなくなります
- 開発者アカウントに紐づけたビジネスIDは、後から変更できません

<!-- note end -->

開発者アカウントとLINEアカウントは、ビジネスIDを介して紐づけられます。開発者アカウントと紐づくビジネスIDにLINEアカウントを連携することで、開発者アカウントにLINEアカウントを紐づけることができます。連携方法について詳しくは、「[ビジネスIDにLINEアカウントを連携させる](https://developers.line.biz/ja/docs/line-developers-console/login-account/#link-business-account-with-line-account)」を参照してください。

開発者アカウントとビジネスID、LINEアカウントとの関係は以下のとおりです。

|  | 開発者アカウント | ビジネスID | LINEアカウント |
| --- | --- | --- | --- |
| 開発者アカウント | — | 1対1で紐づく（※） | ビジネスID経由で紐づけ（1対1） |
| ビジネスID | 1対1で紐づく（※） | — | 1対1で連携可能 |
| LINEアカウント | ビジネスID経由で紐づけ（1対1） | 1対1で連携可能 | — |

※ [開発者アカウントを作成](https://developers.line.biz/ja/docs/line-developers-console/login-account/#register-as-developer)した際に、ビジネスIDと開発者アカウントが自動的に紐づきます。

<!-- tip start -->

**各アカウントのメールアドレスについて**

開発者アカウント、ビジネスID、LINEアカウントに登録した名前やメールアドレスは、それぞれ別々に管理されています。そのため、それぞれのアカウントに登録されているメールアドレスは異なる場合があります。

<!-- tip end -->

### ビジネスIDを新規作成する際のアカウントの関係 

LINE Developersサイトへの初回ログイン時にビジネスIDを新規に作成する場合、LINEアカウントとビジネスアカウント（メールアドレス、パスワード）どちらの方法でビジネスIDを作成するかによって、LINEアカウントの連携状態が異なります。ビジネスIDを作成したアカウントの種類と、開発者アカウントとLINEアカウントとの紐づけの関係は以下のようになります。

| アカウントの種類 | 開発者アカウントと紐づくLINEアカウント |
| --- | --- |
| LINEアカウント | ビジネスIDの作成に使用したLINEアカウント |
| ビジネスアカウント<br>（メールアドレス、パスワード） | なし（※） |

※ ビジネスアカウントで作成したビジネスIDには、後から任意でLINEアカウントを連携できます。詳しくは、「[ビジネスIDにLINEアカウントを連携させる](https://developers.line.biz/ja/docs/line-developers-console/login-account/#link-business-account-with-line-account)」を参照してください。

## ビジネスIDにLINEアカウントを連携させる 

ビジネスIDには、LINEアカウントを1対1で連携できます。1つのLINEアカウントを、複数のビジネスIDに連携させることはできません。

ビジネスIDとLINEアカウントの連携は、以下の手順で設定します。

1. LINEアカウントを連携させたいビジネスIDで[LINE Developersコンソール](https://developers.line.biz/console/)にログイン
1. 画面右上のアイコンをクリック

   ![画面右上のアイコンをクリック](https://developers.line.biz/media/line-developers-console/linking-line-account-click-user-icon-ja.png)

1. アカウント情報をクリックし、プロフィール画面を開く

   ![アカウント情報をクリック](https://developers.line.biz/media/line-developers-console/linking-line-account-click-account-ja.png)

1. ［**ビジネスIDプロフィールに移動**］ボタンをクリックし、ビジネスIDプロフィールに移動

   ![ビジネスIDプロフィールに移動ボタンをクリック](https://developers.line.biz/media/line-developers-console/linking-line-account-click-business-id-ja.png)

1. 「LINEアカウント」の「未連携」の横に表示されている連携アイコンをクリック

   ![LINEアカウントと連携する](https://developers.line.biz/media/line-developers-console/linking-line-account-click-link-icon-ja.png)

1. ビジネスIDと連携させたいLINEアカウントでログイン
1. LINEアカウントのログインが完了すると、ビジネスIDとLINEアカウントが連携されます

<!-- note start -->

**LINEアカウント連携時に「すでに登録されているLINEアカウントです」と表示された場合**

ビジネスIDと連携させるLINEアカウントは、他のビジネスIDと未連携である必要があります。すでにビジネスIDと連携されているLINEアカウントと連携しようとした場合、「すでに登録されているLINEアカウントです」というメッセージが表示され、連携はできません。

![LINEアカウントが連携済みの場合](https://developers.line.biz/media/line-developers-console/login-account-04-ja.png)

<!-- note end -->

<!-- tip start -->

**開発者アカウントとLINEアカウントの紐づけ**

開発者アカウントとLINEアカウントは、ビジネスIDを介して紐づけられます。開発者アカウントと紐づくビジネスIDにLINEアカウントを連携することで、開発者アカウントにLINEアカウントを紐づけることができます。

<!-- tip end -->

## ビジネスIDとLINEアカウントの連携を解除する 

ビジネスIDとLINEアカウントの連携を解除するには、ビジネスIDにメールアドレスとパスワード（ビジネスアカウント）の登録が必要です。ビジネスIDとLINEアカウントの連携を解除すると、開発者アカウントとLINEアカウントの紐づけも解除されます。

ビジネスIDとLINEアカウントの連携の解除は、以下の手順で設定します。

1. LINEアカウントとの連携を解除したいビジネスIDで[LINE Developersコンソール](https://developers.line.biz/console/)にログイン
1. 画面右上のアイコンをクリック

   ![画面右上のアイコンをクリック](https://developers.line.biz/media/line-developers-console/linking-line-account-click-user-icon-ja.png)

1. アカウント情報をクリックし、プロフィール画面を開く

   ![アカウント情報をクリック](https://developers.line.biz/media/line-developers-console/linking-line-account-click-account-ja.png)

1. ［**ビジネスIDプロフィールに移動**］ボタンをクリックし、ビジネスIDプロフィールに移動

   ![ビジネスIDプロフィールに移動ボタンをクリック](https://developers.line.biz/media/line-developers-console/linking-line-account-click-business-id-ja.png)

1. 「LINEアカウント」に表示されている削除アイコンをクリック
   - ビジネスIDにメールアドレスとパスワード（ビジネスアカウント）を登録していない場合は削除アイコンが表示されません。「メールアドレス」の編集アイコンをクリックし、メールアドレスとパスワードを登録してください。

   ![LINEアカウントとの連携を解除する](https://developers.line.biz/media/line-developers-console/unlink-business-account-with-line-account-ja.png)

1. 確認画面で［**削除**］をクリック

   ![確認画面で削除をクリック](https://developers.line.biz/media/line-developers-console/unlink-business-account-click-delete-ja.png)

1. ビジネスIDとLINEアカウントの連携が解除される

## 利用できる機能 

LINE Developersコンソールのログインした開発者アカウントがLINEアカウントと連携しているかどうかで、作成可能なチャネルタイプが異なります。

また、利用中の開発者アカウントに付与されたチャネルの権限によって、利用できる機能に制限があります。詳しくは、「[権限を管理する](https://developers.line.biz/ja/docs/line-developers-console/managing-roles/)」を参照してください。

開発者アカウントとLINEアカウントの連携状態に応じて、以下のチャネルタイプが作成できます。

| 連携状態 | LINEログイン | ブロックチェーンサービス | LINEミニアプリ |
| --- | --- | --- | --- |
| LINEアカウントと連携済み | ✅ | ✅ | ✅ |
| LINEアカウントと未連携 | ✅ | ❌ | ✅ |

Messaging APIチャネルは、LINE公式アカウントを開設することで作成できます。詳しくは、『Messaging APIドキュメント』の「[Messaging APIを始めよう](https://developers.line.biz/ja/docs/messaging-api/getting-started/)」を参照してください。
