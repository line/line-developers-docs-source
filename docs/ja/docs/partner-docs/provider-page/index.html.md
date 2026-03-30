# プロバイダーページ

<!-- note start -->

**オプション機能を利用するには手続きが必要です**

本ドキュメントに記載の機能は、所定の申請等を行った法人ユーザーのみがご利用いただけます。自社のLINE公式アカウントでご利用になりたいお客様は、担当営業までご連絡いただくか、[弊社パートナー](https://www.lycbiz.com/jp/partner/sales/)にお問い合わせください。

<!-- note end -->

## 概要 

プロバイダーページとは、[プロバイダー](https://developers.line.biz/ja/glossary/#provider)がLINEプラットフォーム上で提供している各種サービスの一覧ページです。プロバイダーが提供しているLINE公式アカウント（Messaging API）、LINEミニアプリ、LINEログインのサービスをプロバイダーページに表示できます。

![プロバイダーページの例](https://developers.line.biz/media/partner-docs/provider-page-ja.png)

## プロバイダーページを設定する 

プロバイダーページは認証プロバイダーのみ設定、公開できます。認証プロバイダーについて詳しくは、「[認証プロバイダーについて](https://developers.line.biz/ja/docs/line-developers-console/overview/#certified-provider)」を参照してください。

プロバイダーページの設定は、[LINE Developersコンソール](https://developers.line.biz/console/)の［**プロバイダーページ**］タブで行います。［**プロバイダーページ**］タブは、プロバイダーページが利用できる場合のみ表示されます。

［**プロバイダーページ**］タブでプライバシーポリシーURLを登録して、プロバイダーページで表示したいサービスを追加してください。サービスはプロバイダーページに最大100個追加することができます。プライバシーポリシーURLが登録されていない場合、サービスを追加してもプロバイダーページには表示されません。

<!-- tip start -->

**プロバイダーページに追加できるLINE公式アカウントについて**

プロバイダーページに追加できるLINE公式アカウントは、認証済アカウントと[プレミアムアカウント](https://developers.line.biz/ja/glossary/#premium-account)のみです。未認証アカウントはプロバイダーページには追加できません。アカウント種別について詳しくは、『LINEヤフー for Business』の「[LINE公式アカウント アカウント種別](https://www.lycbiz.com/jp/service/line-official-account/account-type/)」を参照してください。

<!-- tip end -->

![プロバイダーページの設定画面](https://developers.line.biz/media/partner-docs/provider-page-settings-ja.png)

### プロバイダーページでのサービスの表示順を設定する 

[LINE Developersコンソール](https://developers.line.biz/console/)の［**プロバイダーページ**］タブで、各サービスの上下の順序をドラッグアンドドロップで変更すると、その順序がプロバイダーページでの表示順に反映されます。

なおプロバイダーページ内のカテゴリ（LINE公式アカウント、LINEミニアプリ、LINEログイン）の順序は変更できません。各カテゴリ内のサービスの表示順のみ変更できます。

### プロバイダーページのURL 

プロバイダーページのURL（`https://provider.line.me/{プロバイダーID}`）は[LINE Developersコンソール](https://developers.line.biz/console/)の［**プロバイダーページ**］タブで確認できます。

## プロバイダーページのURLをユーザーに共有する 

プロバイダーぺージのURLをユーザーに共有することにより、プロバイダーが提供しているサービスの一覧をユーザーに表示することができます。

- **LINE公式アカウント**：リッチメニューや、友だち追加されたときの初回配信メッセージなどで、リンクの形でご利用ください。
- **LINEミニアプリ**：LINEミニアプリの[アクションボタン](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#action-button)を押すと、［**サービス提供元の詳細**］というプロバイダーページを表示するための項目が表示されます。
- **LINEログイン**：LINEログインボタンを設置しているページなどで、リンクの形でご利用ください。

## ユーザーID共通利用に関する注意事項 

プロバイダーが提供する複数のサービスでLINEプラットフォームを利用している場合、プロバイダーがそれぞれのサービスで取得したLINEユーザー情報を紐づけし、共通で利用することを[LINEユーザーデータポリシー](https://terms2.line.me/LINE_Developers_user_data_policy?lang=ja)では原則禁止しています。ただし、プロバイダーページを公開した上で、以下の[利用条件](https://developers.line.biz/ja/docs/partner-docs/provider-page/#terms-and-conditions-of-use)を満たす場合には、プロバイダーがLINEユーザー情報を紐づけし、共通で利用することを許可します。

なおLINEユーザー情報の利用にあたっては、プロバイダーがLINEユーザー情報の取得者であることを認識し、プロバイダーの責任の元、各種関連法規則に則り、ユーザーにとって不利益の無いように利用してください。

### 利用条件 

LINEユーザー情報を共通利用するそれぞれのサービス上で、ユーザーに対してプロバイダーページへの導線を設け、ユーザーに各サービスが同一のプロバイダーで提供されることを周知してください。

Messaging APIチャネルが対象になる場合は、下記も順守してください。

- LINE公式アカウントの契約企業とプロバイダーが同一であること。または両社の関係がユーザーにとって、誤認を招くようなものになってないこと。

なお、上記ルールが守られていない場合や、不適切に運営されていると思われる場合においては、LINEヤフー株式会社より是正の勧告やLINEユーザー情報の利用禁止の勧告を行うことがある旨、ご了承ください。
