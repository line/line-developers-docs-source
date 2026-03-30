# LINEミニアプリの構造

LINEミニアプリのページは、（A）ヘッダーおよび（B）ボディで構成されています。

![](https://developers.line.biz/media/line-mini-app/mini_concept.png)

## ヘッダー 

LINEミニアプリのヘッダーは、プラットフォームネイティブのコンポーネントが使用されており、LINEが自動生成します。

ヘッダーは、以下のコンポーネントで構成されています。

![](https://developers.line.biz/media/line-mini-app/discover/mini_uicomp_header.png)

| 番号 | コンポーネント | 説明 |
| --- | --- | --- |
| 1 | サービス名 | LINEミニアプリのページで指定した`<title>`要素が表示されます。フォントは設定できません。 |
| - | サブテキスト | 未認証ミニアプリの場合、「サービス名」の下にコンテンツの元のドメインが表示されます。認証済ミニアプリの場合、「サービス名」の下にLINEミニアプリ名と認証バッジが表示されます。 |
| 2 | [アクションボタン](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#action-button) | アクションボタンを押すと、[マルチタブビュー](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#multi-tab-view)または[オプション](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#multi-tab-view-option)のどちらかがLINEアプリのバージョンに応じて表示されます。LINEバージョン15.12.0以降ではマルチタブビューが表示され、LINEバージョン15.12.0未満ではオプションが表示されます。 |
| 3 | 閉じるボタン／最小化ボタン | 閉じるボタンと最小化ボタンのどちらが表示されるかは、LINEのバージョンとLINEミニアプリの種類によって異なります。<table><thead><tr><th>LINEのバージョン</th><th>未認証ミニアプリ</th><th>認証済ミニアプリ</th></tr></thead><tbody><tr><td><ul><li>iOS版LINEバージョン14.15.1未満</li><li>Android版LINEバージョン15.0.0未満</li></ul></td><td>閉じるボタン</td><td>閉じるボタン</td></tr><tr><td><ul><li>iOS版LINEバージョン14.15.1以降</li><li>Android版LINEバージョン15.0.0以降</li></ul></td><td>閉じるボタン</td><td>最小化ボタン</td></tr></tbody></table>閉じるボタンをタップすると、LINEミニアプリを閉じます。最小化ボタンをタップすると、LINEミニアプリを最小化します。最小化について詳しくは、『LIFFドキュメント』の「[LIFFブラウザを最小化する](https://developers.line.biz/ja/docs/liff/minimizing-liff-browser/)」を参照してください。 |
| 4 | 戻るボタン | 前のページを表示します。 |
| 5 | ローディングバー | 現在のページの読み込み状況を表示します。 |

## ボディ 

ボディはWebViewが使用されています。HTML5およびLIFFを活用して、サービスごとに開発してください。

LINEミニアプリの開発に関する仕様については、「[LINEミニアプリの仕様](https://developers.line.biz/ja/docs/line-mini-app/discover/specifications/)」を参照してください。
