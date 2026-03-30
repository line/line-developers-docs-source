# ビルトイン機能

LINEミニアプリには、以下のビルトイン機能が組み込まれています。

<!-- table of contents -->

## アクションボタン 

LINEミニアプリのすべてのページに表示される[ヘッダー](https://developers.line.biz/ja/docs/line-mini-app/discover/ui-components/#header)には、デフォルトでアクションボタンが表示されます。

![](https://developers.line.biz/media/line-mini-app/discover/mini-header-action-butoon-ja.png)

アクションボタンを押すと、[マルチタブビュー](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#multi-tab-view)または[オプション](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#multi-tab-view-option)のどちらかがLINEアプリのバージョンに応じて表示されます。LINEバージョン15.12.0以降ではマルチタブビューが表示され、LINEバージョン15.12.0未満ではオプションが表示されます。

<!-- tip start -->

**ヒント**

- [カスタムアクションボタン](https://developers.line.biz/ja/docs/line-mini-app/discover/custom-features/#custom-action-button)を実装すれば、LINEミニアプリの好きな場所に、好きな形式のシェア機能を実装できます。
- LINEミニアプリを閉じずに複数のトークルームを行き来するための機能など、新しい機能を追加する予定です。
- LINEミニアプリでは、アクションボタンを非表示にすることはできません。LINEミニアプリチャネルに追加されているLIFFアプリでは、［**モジュールモード**］は設定できません。

<!-- tip end -->

## マルチタブビュー 

マルチタブビューには、使用中のLINEミニアプリのオプションと最近使用したサービスが表示されます。

1. [オプション](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#multi-tab-view-option)
1. [最近使用したサービス](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#multi-tab-view-recent-service)

![](https://developers.line.biz/media/line-mini-app/discover/mini-multi-tab-view-ja.png)

### オプション 

以下のオプションが、ユーザーのLINEアプリの設定言語で表示されます。

| 項目 | 説明 |
| --- | --- |
| **更新** | 現在開いているページを再読み込みします。 |
| **シェア** | 現在開いているページのLIFF URLまたはパーマネントリンクをLINEメッセージでシェアします。現在開いているページがLINEミニアプリのエンドポイントURLから始まらない場合、代わりにLINEミニアプリのLIFF URLをシェアします。メッセージには、以下の要素が含まれます。<ul><li>URL：現在開いているページのパーマネントリンク</li><li>タイトル：[LINE Developersコンソール](https://developers.line.biz/console/)の［**ウェブアプリ設定**］タブの［**LIFFアプリ名**］に入力した名前</li><li>詳細：自動的に設定されたテキスト</li><li>画像：[LINE Developersコンソール](https://developers.line.biz/console/)の［**チャネル基本設定**］タブの［**チャネルアイコン**］に設定した画像</li></ul> |
| **ホーム画面に追加** | 現在開いているページへのショートカット追加画面を表示します。現在開いているページがLINEミニアプリのエンドポイントURLから始まらない場合、エラーになります。LINEバージョン14.3.0以降の認証済ミニアプリでのみ利用できます。詳しくは、「[ユーザー端末のホーム画面にLINEミニアプリへのショートカットを追加する](https://developers.line.biz/ja/docs/line-mini-app/develop/add-to-home-screen/)」を参照してください。 |
| **お気に入り** | <p>現在開いているLINEミニアプリをお気に入りに追加します。次の条件をすべて満たす場合のみ利用できます。</p><p><ul><li>LINEミニアプリが[認証済ミニアプリ](https://developers.line.biz/ja/docs/line-mini-app/discover/introduction/#verified-mini-app)である。</li><li>ユーザーが日本のユーザーである。</li><li>ユーザーのLINEバージョンが15.18.0以降である。</li></ul></p><p>お気に入りに追加されたLINEミニアプリは、LINEアプリのウォレットタブで確認できます。</p> |
| **ページを最小化** | LIFFブラウザを最小化します。認証済ミニアプリでのみ利用できます。詳しくは『LIFFドキュメント』の「[LIFFブラウザを最小化する](https://developers.line.biz/ja/docs/liff/minimizing-liff-browser/)」を参照してください。 |
| **権限設定** | <p>権限設定画面を開きます。権限設定画面では、現在開いているLINEミニアプリのカメラやマイクへのアクセス権を確認、変更できます。LINEバージョン14.6.0以降で利用できます。</p><p>ユーザーが権限を変更しても、LINEミニアプリ側でページを再読み込みしない限り、変更の内容が反映されない場合があるため注意してください。</p> |
| **サービス提供元の詳細** | [プロバイダーページ](https://developers.line.biz/ja/docs/partner-docs/provider-page/)を表示します。認証済ミニアプリでのみ利用できます。 |
| **通報** | <p>LINEアプリのお問い合わせフォームを外部ブラウザで開きます。次の条件をすべて満たす場合のみ利用できます。</p><ul><li>LINEミニアプリチャネルの［**チャネル基本設定**］タブの［**サービスを提供する地域**］が「日本」である。</li><li>ユーザーのLINEバージョンが15.6.0以降である。</li></ul> |

<!-- note start -->

**注意**

現在開いているページをシェアするには、LINEミニアプリに対応するLINEバージョンでアクションボタンをタップする必要があります。ユーザーが使用しているLINEのバージョンが、LINEミニアプリの[対応バージョン](https://developers.line.biz/ja/docs/line-mini-app/discover/specifications/#supported-platforms-and-versions)未満の場合は、アクションボタンをタップしたページに関わらず、LINEミニアプリのトップページがシェアされます。

<!-- note end -->

### 最近使用したサービス 

最近使用したサービスにはユーザーが開いたLINEミニアプリとLIFFアプリが、利用履歴の新しい順に最大50件まで表示されます。ユーザーは利用履歴を使って、LINEミニアプリやLIFFアプリを再度開くことができます。

詳しくは、『LIFFドキュメント』の「[最近使用したサービス](https://developers.line.biz/ja/docs/liff/overview/#multi-tab-view-recent-service)」を参照してください。

## チャネル同意の簡略化 

LIFFアプリがユーザーの情報を取得したり、ユーザーにメッセージを送信したりするには、ユーザーがLIFFアプリに初めてアクセスする際に、「チャネル同意画面」において、対応する権限に同意する必要があります。

LINEミニアプリでは、「チャネル同意の簡略化」機能によって、ユーザーが簡略化に対する同意を初回のみ行うだけで、別のLINEミニアプリに初めてアクセスする際に「チャネル同意画面」をスキップし、すぐにLINEミニアプリの利用を開始できるようになります。

詳しくは、「[LINEミニアプリの認可フロー](https://developers.line.biz/ja/docs/line-mini-app/develop/channel-consent-simplification/)」を参照してください。
