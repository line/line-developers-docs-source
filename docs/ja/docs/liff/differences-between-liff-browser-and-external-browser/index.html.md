# LIFFブラウザと外部ブラウザの違い

<!-- tip start -->

**LIFFブラウザの仕様**

詳しくは、「[LIFFブラウザの仕様](https://developers.line.biz/ja/docs/liff/overview/#liff-browser-spec)」を参照してください。

<!-- tip end -->

[LIFFブラウザ](https://developers.line.biz/ja/glossary/#liff-browser)は、[外部ブラウザ](https://developers.line.biz/ja/glossary/#external-browser)がサポートしているウェブ技術の一部をサポートしていません。LIFFブラウザでサポートしていないウェブ技術として、以下のものがあります。

| ウェブ技術 | 説明 |
| --- | --- |
| [theme-color Meta Tag](https://caniuse.com/meta-theme-color) | ユーザーインターフェースの色を指定する機能 |
| [Download attribute](https://caniuse.com/download) | ハイパーリンクを、リソースへの遷移ではなく、リソースのダウンロードに使用する機能 |
| [Add to home screen (A2HS)](https://caniuse.com/sr_web-app-manifest) | <p>ユーザーがウェブアプリケーションを端末のホーム画面に追加できるようにする機能。</p><p>なお、LINEミニアプリでは、[マルチタブビュー](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#multi-tab-view)の［**ホーム画面に追加**］や[`liff.createShortcutOnHomeScreen()`](https://developers.line.biz/ja/reference/liff/#create-shortcut-on-home-screen)メソッドを使うことで、ユーザー端末のホーム画面にLINEミニアプリへのショートカットを追加できます。詳しくは、『LINEミニアプリドキュメント』の「[ユーザー端末のホーム画面にLINEミニアプリへのショートカットを追加する](https://developers.line.biz/ja/docs/line-mini-app/develop/add-to-home-screen/)」を参照してください。</p> |
| [Service Workers](https://caniuse.com/serviceworkers) | ウェブアプリケーションでオフライン対応、バックグラウンド同期、プッシュ通知などをできるようにする機能 |

なお、上記のウェブ技術については、今後、LIFFブラウザがサポートする可能性があります。

上記以外のウェブ技術について、LIFFブラウザがサポートしているかどうかは、[WKWebView](https://developer.apple.com/documentation/webkit/wkwebview)や[Android WebView](https://developer.android.com/reference/android/webkit/WebView)の仕様に従います。詳しくは、『[Can I use...](https://caniuse.com/)』を参照してください。
