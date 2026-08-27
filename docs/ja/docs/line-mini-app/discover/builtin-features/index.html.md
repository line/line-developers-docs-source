# ビルトイン機能

LINEミニアプリには、以下のビルトイン機能が組み込まれています。

<!-- table of contents -->

## アクションボタン 

LINEミニアプリのすべてのページに表示される[ヘッダー](https://developers.line.biz/ja/docs/line-mini-app/discover/ui-components/#header)には、デフォルトでアクションボタンが表示されます。

![](https://developers.line.biz/media/line-mini-app/discover/mini-header-action-button-ja.png)

アクションボタンを押すと、以下に示すLINEアプリのバージョンに応じた機能が表示されます。なお、アクションボタンのアイコンはLINEバージョンによって異なります。

| LINEアプリのバージョン | 表示される機能         |
| ---------------------- | ---------------------- |
| 26.7.0以降             | ドロップダウンメニュー |
| 15.12.0以降26.7.0未満  | マルチタブビュー       |
| 15.12.0未満            | オプション             |

<!-- tip start -->

**ヒント**

- [カスタムアクションボタン](https://developers.line.biz/ja/docs/line-mini-app/discover/custom-features/#custom-action-button)を実装すれば、LINEミニアプリの好きな場所に、好きな形式のシェア機能を実装できます。
- LINEミニアプリを閉じずに複数のトークルームを行き来するための機能など、新しい機能を追加する予定です。
- LINEミニアプリでは、アクションボタンを非表示にすることはできません。LINEミニアプリチャネルに追加されているLIFFアプリでは、［**モジュールモード**］は設定できません。

<!-- tip end -->

### ドロップダウンメニュー 

LINEバージョン26.7.0以降では、アクションボタンをタップすると、以下のドロップダウンメニューが表示されます。

![](https://developers.line.biz/media/line-mini-app/discover/mini-header-action-button-tap-ja.png)

| 項目 | 説明 |
| --- | --- |
| **すべてのタブ** | [マルチタブビュー](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#multi-tab-view)を表示します。 |
| **更新** | 現在開いているページを再読み込みします。 |
| **ページを最小化** | LIFFブラウザを最小化します。認証済ミニアプリでのみ利用できます。詳しくは『LIFFドキュメント』の「[LIFFブラウザを最小化する](https://developers.line.biz/ja/docs/liff/minimizing-liff-browser/)」を参照してください。 |
| **シェア** | 現在開いているページのLIFF URLまたはパーマネントリンクをLINEメッセージでシェアします。現在開いているページがLINEミニアプリのエンドポイントURLから始まらない場合、代わりにLINEミニアプリのLIFF URLをシェアします。メッセージには、以下の要素が含まれます。<ul><li>URL：現在開いているページのパーマネントリンク</li><li>タイトル：[LINE Developersコンソール](https://developers.line.biz/console/)の［**ウェブアプリ設定**］タブの［**LIFFアプリ名**］に入力した名前</li><li>詳細：自動的に設定されたテキスト</li><li>画像：[LINE Developersコンソール](https://developers.line.biz/console/)の［**チャネル基本設定**］タブの［**チャネルアイコン**］に設定した画像</li></ul> |
| **ホーム画面に追加** | 現在開いているページへのショートカット追加画面を表示します。現在開いているページがLINEミニアプリのエンドポイントURLから始まらない場合、エラーになります。LINEバージョン14.3.0以降の認証済ミニアプリでのみ利用できます。詳しくは、「[ユーザー端末のホーム画面にLINEミニアプリへのショートカットを追加する](https://developers.line.biz/ja/docs/line-mini-app/develop/add-to-home-screen/)」を参照してください。 |
| **お気に入り** | <p>現在開いているLINEミニアプリをお気に入りに追加します。次の条件をすべて満たす場合のみ利用できます。</p><p><ul><li>LINEミニアプリが[認証済ミニアプリ](https://developers.line.biz/ja/docs/line-mini-app/discover/introduction/#verified-mini-app)である。</li><li>ユーザーが日本のユーザーである。</li><li>ユーザーのLINEバージョンが15.18.0以降である。</li></ul></p><p>お気に入りに追加されたLINEミニアプリは、LINEアプリのMINIタブで確認できます。</p> |
| **権限設定** | <p>権限設定画面を開きます。権限設定画面では、現在開いているLINEミニアプリのカメラやマイクへのアクセス権を確認、変更できます。LINEバージョン14.6.0以降で利用できます。</p><p>ユーザーが権限を変更しても、LINEミニアプリ側でページを再読み込みしない限り、変更の内容が反映されない場合があるため注意してください。</p> |
| **サービス提供元の詳細** | [プロバイダーページ](https://developers.line.biz/ja/docs/partner-docs/provider-page/)を表示します。認証済ミニアプリでのみ利用できます。 |
| **通報** | <p>LINEアプリのお問い合わせフォームを外部ブラウザで開きます。次の条件をすべて満たす場合のみ利用できます。</p><ul><li>LINEミニアプリチャネルの［**チャネル基本設定**］タブの［**サービスを提供する地域**］が「日本」である。</li><li>ユーザーのLINEバージョンが15.6.0以降である。</li></ul> |

<!-- note start -->

**注意**

現在開いているページをシェアするには、LINEミニアプリに対応するLINEバージョンでアクションボタンをタップする必要があります。ユーザーが使用しているLINEのバージョンが、LINEミニアプリの[対応バージョン](https://developers.line.biz/ja/docs/line-mini-app/discover/specifications/#supported-platforms-and-versions)未満の場合は、アクションボタンをタップしたページに関わらず、LINEミニアプリのトップページがシェアされます。

<!-- note end -->

### マルチタブビュー 

マルチタブビューには、最近使用したサービスが表示されます。最近使用したサービスには、ユーザーが開いたLINEミニアプリとLIFFアプリが、利用履歴の新しい順に最大50件まで表示されます。ユーザーは利用履歴を使って、LINEミニアプリやLIFFアプリを再度開くことができます。

詳しくは、『LIFFドキュメント』の「[マルチタブビュー](https://developers.line.biz/ja/docs/liff/overview/#multi-tab-view)」を参照してください。

![](https://developers.line.biz/media/line-mini-app/discover/mini-multi-tab-view-ja.webp)

## チャネル同意の簡略化 

LIFFアプリがユーザーの情報を取得したり、ユーザーにメッセージを送信したりするには、ユーザーがLIFFアプリに初めてアクセスする際に、「チャネル同意画面」において、対応する権限に同意する必要があります。

LINEミニアプリでは、「チャネル同意の簡略化」機能によって、ユーザーがLINEミニアプリに初めてアクセスする際に、「チャネル同意画面」をスキップし、すぐにLINEミニアプリの利用を開始できるようになります。

詳しくは、「[LINEミニアプリの認可フロー](https://developers.line.biz/ja/docs/line-mini-app/develop/channel-consent-simplification/)」を参照してください。
