# LINEミニアプリチャネルをビジネスマネージャーの組織と接続する

LINEミニアプリチャネルを[ビジネスマネージャー](https://www.lycbiz.com/jp/service/business-manager/)の組織と接続できます。接続すると、同じ組織に接続している他のサービスのアカウントと連携できるようになります。

現時点で利用できる機能は、LINE公式アカウントとの接続のみです。今後は、接続したLINE公式アカウントの[ビジネスプロフィール](https://www.lycbiz.com/jp/manual/OfficialAccountManager/profile/)にLINEミニアプリの情報を表示できるようにするなど、機能の拡張を予定しています。

ビジネスマネージャーについて詳しくは、『LINEヤフー for Business』の「[ビジネスマネージャー](https://www.lycbiz.com/jp/service/business-manager/)」を参照してください。

<!-- table of contents -->

## ビジネスマネージャーの組織との接続条件 

LINEミニアプリチャネルをビジネスマネージャーの組織と接続するには、次の条件をすべて満たす必要があります。

- [認証済ミニアプリ](https://developers.line.biz/ja/glossary/#verified-mini-app)である。
- LINEミニアプリチャネルの［**サービスを提供する地域**］が「日本」である。
- 本番用のLINEミニアプリのプロバイダーとサービス事業主が一致している（※）。
- ビジネスマネージャーの組織の［**地域**］が「日本」である。
- LINEミニアプリチャネルとビジネスマネージャーの組織の［**会社・事業者の所在国・地域**］が一致している。

※ LINEミニアプリチャネルの公開済みデータの［**事業情報**］タブにおいて、以下のいずれかを満たす必要があります。

- 「開発担当企業情報」セクションの［**サービス事業主と同じ**］がオンである
- 「開発担当企業情報」セクションの［**サービス事業主と同じ**］がオフで、かつ「プロバイダー情報」セクションの［**プロバイダー**］が「サービス事業主」である

## ビジネスマネージャーの組織との接続方法 

<!-- note start -->

**ビジネスマネージャーの組織との接続は解除できません**

LINEミニアプリチャネルをビジネスマネージャーの組織と一度接続すると、接続を解除できません。ただし、ビジネスマネージャー上で他の組織に移動することは可能です。詳しくは、『LINE for Business』の「[接続したアカウント・チャネルを他の組織に移動することはできますか？](https://help.linebiz.com/lineadshelp/s/article/L000001731?language=ja)」を参照してください。

<!-- note end -->

LINEミニアプリチャネルをビジネスマネージャーの組織と接続する流れは次のとおりです。

1. [開発者が接続をリクエストする](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#send-link-request)
1. [開発者が接続リクエスト用URLをビジネスマネージャーの組織の管理者に送信する](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#send-link-request-url)
1. [ビジネスマネージャーの組織の管理者がリクエストを承認する](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#approve-request)

以降の説明では、LINE Developersコンソールとビジネスマネージャーを操作します。LINE DevelopersコンソールをLINEミニアプリチャネルのAdmin権限を持つ[開発者](https://developers.line.biz/ja/docs/line-developers-console/overview/#developer)が操作し、ビジネスマネージャーを組織の管理者が操作してください。

### 1. 開発者が接続をリクエストする 

LINEミニアプリチャネルの［**ビジネスマネージャー接続**］タブを開きます。

![](https://developers.line.biz/media/line-mini-app/service/business-manager-tab-ja.png)

［**組織ID**］に接続先の組織の組織ID（BM + 11桁の半角数字）を入力し、［**接続をリクエストする**］をクリックします。

<!-- tip start -->

**組織IDを確認する**

ビジネスマネージャーの組織の組織ID（BM + 11桁の半角数字）は、組織の管理者に問い合わせてください。開発者自身が組織の権限を持っている場合は、ビジネスマネージャーのヘッダーで確認できます。

![](https://developers.line.biz/media/line-mini-app/service/business-manager-header-ja.png)

<!-- tip end -->

### 2. 開発者が接続リクエスト用URLをビジネスマネージャーの組織の管理者に送信する 

[開発者が接続をリクエストする](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#send-link-request)と、［**ビジネスマネージャー接続**］タブに接続リクエスト用URLが表示されます。

![](https://developers.line.biz/media/line-mini-app/service/send-link-request-ja.png)

接続リクエスト用URLは、ビジネスマネージャー側のURLです。ビジネスマネージャーの組織の管理者がこのURLを開き、リクエストを承認することで、LINEミニアプリチャネルとビジネスマネージャーの組織が接続されます。

接続リクエスト用URLをビジネスマネージャーの組織の管理者に送信し、承認を依頼してください。なお、開発者がビジネスマネージャーの組織の管理者でもある場合は、接続リクエスト用URLの表示はスキップされ、リクエストが自動で承認されます。

<!-- tip start -->

**接続リクエスト用URLの有効期間**

接続リクエスト用URLの有効期間は発行から7日間（168時間）です。有効期限が切れた場合は、［**接続をリクエストする**］から、再度接続をリクエストしてください。

<!-- tip end -->

### 3. ビジネスマネージャーの組織の管理者がリクエストを承認する 

ビジネスマネージャーの組織の管理者が接続リクエスト用URLを開くと、リクエストの承認画面が表示されます。

![](https://developers.line.biz/media/line-mini-app/service/approve-send-link-request-ja.png)

LINEミニアプリチャネルと組織に誤りがないこと、および注意事項を確認し、［**承認する**］をクリックします。

## 接続審査 

LINEミニアプリチャネルをビジネスマネージャーの組織と接続すると、接続審査が行われます。これは、チャネルと組織の所有者が一致するかを確認する目的で行われます。

接続審査が完了し、[ステータス](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#account-linking-review-status)が認証済みになると、同じ組織に接続している他のサービスのアカウントと連携できるようになります。

### 接続審査の開始条件 

接続審査が開始されるには、次の条件をすべて満たす必要があります。

- LINEミニアプリチャネルとビジネスマネージャーの組織が接続済みである。
- ビジネスマネージャーの組織が認証済みである。

ビジネスマネージャーの組織の認証審査について詳しくは、『LINEヤフー for Business』の「[03. 組織の認証審査](https://www.lycbiz.com/jp/manual/BusinessManager/BMshare004/?list=21791)」および『LINE for Business』の「[ビジネスマネージャーの審査が始まるタイミング、審査内容、審査日数を教えてください](https://help.linebiz.com/lineadshelp/s/article/L000001858?language=ja)」を参照してください。

なお、LINEミニアプリチャネルをビジネスマネージャーの組織に接続した際に、組織の認証審査の開始条件を満たした場合は、組織の認証審査と接続審査が同時に行われます。

#### 接続審査の開始条件の例外 

LINEミニアプリチャネルを接続したビジネスマネージャーの組織が未認証であり、かつ組織の認証審査の開始条件を満たしていない場合であっても、次の条件に該当する場合は、接続審査が行われ、否認されることがあります。

- LINEミニアプリチャネルの事業情報とビジネスマネージャーの組織のビジネス情報が一致していない。

詳しくは、「[接続審査が否認された場合](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#account-linking-review-status-rejected)」を参照してください。

### 接続審査のステータス 

接続審査のステータスは次のとおりです。

| ステータス | 説明 |
| --- | --- |
| 未認証 | [接続審査の開始条件](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#account-linking-review-requirements)を満たしていません。組織の認証審査が完了し、認証済みになると、接続審査が開始されます。 |
| 認証済み | 接続審査が完了しました。 |
| 否認 | 接続審査が否認されました。詳しくは、「[接続審査が否認された場合](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#account-linking-review-status-rejected)」を参照してください。 |

#### 接続審査のステータスの確認方法 

接続審査のステータスはLINE Developersコンソールかビジネスマネージャーで確認できます。

LINE Developersコンソールでは、LINEミニアプリチャネルの［**ビジネスマネージャー接続**］タブの「ビジネスマネージャー接続」で確認できます。

![](https://developers.line.biz/media/line-mini-app/service/account-linking-review-status-in-console-ja.png)

ビジネスマネージャーでは、「アカウント・チャネル」画面の「接続審査ステータス」で確認できます。

![](https://developers.line.biz/media/line-mini-app/service/account-linking-review-status-in-bm-ja.png)

### 接続審査が否認された場合 

接続審査が否認された場合、次のような理由が考えられます。

- LINEミニアプリチャネルの事業情報とビジネスマネージャーの組織のビジネス情報が一致していない。

LINEミニアプリチャネルの事業情報とビジネスマネージャーの組織のビジネス情報を確認し、状況に応じて対応してください。

- [LINEミニアプリチャネルの事業情報に誤りがある場合](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#account-linking-review-status-rejected-line-mini-app)
- [ビジネスマネージャーの組織のビジネス情報に誤りがある場合](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#account-linking-review-status-rejected-business-manager)
- [LINEミニアプリチャネルを誤ったビジネスマネージャーの組織に接続した場合](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#account-linking-review-status-rejected-wrong-organization)

#### LINEミニアプリチャネルの事業情報に誤りがある場合 

LINEミニアプリチャネルの事業情報を正しい情報に更新してください。事業情報の更新にはLINEミニアプリの再審査が必要です。詳しくは、「[認証済ミニアプリ更新後の再審査](https://developers.line.biz/ja/docs/line-mini-app/service/update-service/)」を参照してください。

LINEミニアプリの再審査後、更新内容を本番用のLINEミニアプリチャネルに反映したら、[接続審査の再審査](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#account-linking-review-resubmission)をリクエストしてください。

#### ビジネスマネージャーの組織のビジネス情報に誤りがある場合 

- [ビジネスマネージャーの組織が未認証の場合](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#account-linking-review-status-rejected-business-manager-unverified)
- [ビジネスマネージャーの組織が認証済みの場合](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#account-linking-review-status-rejected-business-manager-verified)

##### ビジネスマネージャーの組織が未認証の場合 

ビジネスマネージャーの組織が未認証の場合、組織のビジネス情報を正しい情報に更新し、組織の認証審査を完了してください。ビジネスマネージャーの組織の認証審査について詳しくは、『LINEヤフー for Business』の「[03. 組織の認証審査](https://www.lycbiz.com/jp/manual/BusinessManager/BMshare004/?list=21791)」および『LINE for Business』の「[ビジネスマネージャーの審査が始まるタイミング、審査内容、審査日数を教えてください](https://help.linebiz.com/lineadshelp/s/article/L000001858?language=ja)」を参照してください。

組織の認証審査が完了したら、[接続審査の再審査](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#account-linking-review-resubmission)をリクエストしてください。

##### ビジネスマネージャーの組織が認証済みの場合 

ビジネスマネージャーの組織が認証済みの場合、ビジネス情報は変更できません。新しい組織を作成し、LINEミニアプリチャネルを移動してください。詳しくは、『LINE for Business』の「[接続したアカウント・チャネルを他の組織に移動することはできますか？](https://help.linebiz.com/lineadshelp/s/article/L000001731?language=ja)」を参照してください。

組織の移動後、移動先の組織が[接続審査の開始条件](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#account-linking-review-requirements)を満たしている場合、接続審査が開始されます。

#### LINEミニアプリチャネルを誤ったビジネスマネージャーの組織に接続した場合 

LINEミニアプリチャネルを正しいビジネスマネージャーの組織に移動してください。詳しくは、『LINE for Business』の「[接続したアカウント・チャネルを他の組織に移動することはできますか？](https://help.linebiz.com/lineadshelp/s/article/L000001731?language=ja)」を参照してください。

組織の移動後、移動先の組織が[接続審査の開始条件](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#account-linking-review-requirements)を満たしている場合、接続審査が開始されます。

### 接続審査の再審査 

#### 接続審査の再審査の開始条件 

接続審査の再審査が開始されるには、LINEミニアプリチャネルを接続したビジネスマネージャーの組織が、認証済みである必要があります。[接続審査の開始条件の例外](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#account-linking-review-requirements-exceptions)に該当した結果、接続審査が否認された場合は、接続審査の再審査をリクエストする前に、組織の認証審査を完了してください。

#### 接続審査の再審査のリクエスト方法 

接続審査の再審査は、ビジネスマネージャーの組織の管理者がリクエストする必要があります。再審査をリクエストする流れは次のとおりです。

1. ビジネスマネージャーのメニューの［**アカウント・チャネル**］をクリックし、「アカウント・チャネル」画面を開きます。

   ![](https://developers.line.biz/media/line-mini-app/service/account-channel-ja.png)

1. 接続審査の再審査をリクエストするLINEミニアプリチャネルの［**詳細**］をクリックします。

   ![](https://developers.line.biz/media/line-mini-app/service/rejected-details-ja.png)

1. ［**認証を再度リクエスト**］をクリックします。

   ![](https://developers.line.biz/media/line-mini-app/service/link-review-results-ja.png)

再審査をリクエストすると、接続審査の再審査が開始されます。

## LINEミニアプリチャネルをLINE公式アカウントと接続する 

LINEミニアプリチャネルを同じビジネスマネージャーの組織に接続しているLINE公式アカウントと接続できます。

現時点で利用できる機能は、LINE公式アカウントとの接続のみです。今後は、接続したLINE公式アカウントの[ビジネスプロフィール](https://www.lycbiz.com/jp/manual/OfficialAccountManager/profile/)にLINEミニアプリの情報を表示できるようにするなど、機能の拡張を予定しています。

### LINE公式アカウントとの接続条件 

LINEミニアプリチャネルをLINE公式アカウントと接続するには、次の条件をすべて満たす必要があります。

- LINEミニアプリチャネルとビジネスマネージャーの組織が接続済みで、[接続審査のステータス](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#account-linking-review-status)が認証済みである。
- LINE公式アカウントとビジネスマネージャーの組織が接続済みで、[接続審査のステータス](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#account-linking-review-status)が認証済みである（※）。
- LINEミニアプリチャネルとLINE公式アカウントが同じビジネスマネージャーの組織に接続している。

※ LINE公式アカウントをビジネスマネージャーの組織と接続する方法について詳しくは、『LINEヤフー for Business』の「[02. 組織にアカウントを接続する](https://www.lycbiz.com/jp/manual/BusinessManager/BMshare003/)」を参照してください。

### LINE公式アカウントとの接続方法 

<!-- note start -->

**LINE公式アカウントとの接続は解除できません**

LINEミニアプリチャネルをLINE公式アカウントと一度接続すると、接続を解除できません。

<!-- note end -->

LINEミニアプリチャネルをLINE公式アカウントと接続する流れは次のとおりです。

1. [接続するLINE公式アカウントを選択する](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#select-line-official-account)
1. [接続するLINEミニアプリチャネルを選択する](https://developers.line.biz/ja/docs/line-mini-app/service/business-manager-link/#select-line-mini-app-channel)

以降の説明では、ビジネスマネージャーを操作します。ビジネスマネージャーの組織の管理者が操作してください。

#### 1. 接続するLINE公式アカウントを選択する 

まず、接続するLINE公式アカウントを選択します。ビジネスマネージャーのメニューの［**LINE公式アカウント接続**］をクリックし、「LINE公式アカウントと接続」画面を開きます。

![](https://developers.line.biz/media/line-mini-app/service/line-official-account-linking-menu-ja.png)

<!-- tip start -->

**開発者がビジネスマネージャーの組織の管理者でもある場合**

開発者がビジネスマネージャーの組織の管理者でもある場合は、LINEミニアプリチャネルの［**ビジネスマネージャー接続**］タブの「LINE公式アカウント接続」セクションから、ビジネスマネージャーの「LINE公式アカウントと接続」画面を開くことができます。

![](https://developers.line.biz/media/line-mini-app/service/line-official-account-linking-from-line-mini-app-channel-ja.png)

<!-- tip end -->

接続するLINE公式アカウントの名前をクリックします。

![](https://developers.line.biz/media/line-mini-app/service/line-official-account-linking-oa-name-ja.png)

#### 2. 接続するLINEミニアプリチャネルを選択する 

次に、選択したLINE公式アカウントに接続するLINEミニアプリチャネルを選択します。［**接続先を選択**］をクリックします。

![](https://developers.line.biz/media/line-mini-app/service/select-target-for-linking-ja.png)

選択したLINE公式アカウントと同じ組織に接続しているアカウント・チャネルの一覧が表示されます。接続するLINEミニアプリチャネルの［**選択**］をクリックします。

![](https://developers.line.biz/media/line-mini-app/service/select-ja.png)

確認画面が表示されるため、LINE公式アカウントとLINEミニアプリチャネルに誤りがないこと、および注意事項を確認し、［**接続**］をクリックします。

![](https://developers.line.biz/media/line-mini-app/service/link-channel-ja.png)

## 関連ページ 

- [ビジネスマネージャー](https://www.lycbiz.com/jp/service/business-manager/)
- [02. 組織にアカウントを接続する](https://www.lycbiz.com/jp/manual/BusinessManager/BMshare003/)
- [03. 組織の認証審査](https://www.lycbiz.com/jp/manual/BusinessManager/BMshare004/?list=21791)
- [LINE公式アカウントに他のサービスのアカウントを接続する](https://www.lycbiz.com/jp/manual/BusinessManager/yahoo-display-linkage/)
- [ビジネスマネージャーの審査が始まるタイミング、審査内容、審査日数を教えてください](https://help.linebiz.com/lineadshelp/s/article/L000001858?language=ja)
- [接続したアカウント・チャネルを他の組織に移動することはできますか？](https://help.linebiz.com/lineadshelp/s/article/L000001731?language=ja)
