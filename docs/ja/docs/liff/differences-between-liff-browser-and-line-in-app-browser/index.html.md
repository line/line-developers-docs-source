# LIFFブラウザとLINE内ブラウザの違い

LINEアプリ上でLIFFアプリを開くと、[LIFFブラウザ](https://developers.line.biz/ja/glossary/#liff-browser)または[LINE内ブラウザ](https://developers.line.biz/ja/glossary/#line-iab)上で開かれます。LIFFブラウザとLINE内ブラウザは異なるブラウザであり、LIFFアプリの一部機能はLIFFブラウザでのみ利用できます。

このページでは、LIFFブラウザとLINE内ブラウザを判別する方法や、利用できる機能の違いなどを紹介します。

<!-- table of contents -->

## LIFFブラウザ 

LIFFアプリ専用のブラウザです。次の方法でLIFFアプリを開くと、LIFFブラウザで開かれます。

- LINEアプリのトークルーム上で[LIFF URL](https://developers.line.biz/ja/glossary/#liff-url)をタップする。
- 外部ブラウザでLIFF URLをタップする。

## LINE内ブラウザ 

LINEのアプリ内専用のブラウザです。次の方法でLIFFアプリを開くと、LINE内ブラウザで開かれます。

- LINEアプリのトークルーム上でLIFFアプリのエンドポイントURLをタップする。

なお、LIFFではLINE内ブラウザは外部ブラウザの一種として扱われます。たとえば、LINE内ブラウザで[`liff.getContext()`](https://developers.line.biz/ja/reference/liff/#get-context)メソッドを実行すると、戻り値の`type`プロパティの値は`external`（外部ブラウザ）になります。

## LIFFブラウザかLINE内ブラウザかを判別する 

LIFFアプリが開かれたブラウザがLIFFブラウザかLINE内ブラウザかを判別するには、次の2つの方法があります。

- [ユーザーインターフェースで判別する](https://developers.line.biz/ja/docs/liff/differences-between-liff-browser-and-line-in-app-browser/#identify-from-ui)
- [`liff.isInClient()`メソッドで判別する](https://developers.line.biz/ja/docs/liff/differences-between-liff-browser-and-line-in-app-browser/#identify-using-liff-is-in-client)

### ユーザーインターフェースで判別する 

LIFFブラウザとLINE内ブラウザでは、ヘッダーやフッターのユーザーインターフェースが異なります。そのため、LIFFアプリを開いているブラウザのユーザインターフェースを確認することで、LIFFブラウザかLINE内ブラウザかを判別できます。

| LIFFブラウザ | LINE内ブラウザ |
| --- | --- |
| ![](https://developers.line.biz/media/liff/differences-between-liff-browser-and-line-in-app-browser/liff-browser.png)<ul><li>ヘッダー<ul><li>最小化ボタンが<b>ない</b></li><li>アクションボタンが<b>ある</b>（※）</li></ul></li><li>フッターが<b>ない</b></li></ul> | ![](https://developers.line.biz/media/liff/differences-between-liff-browser-and-line-in-app-browser/line-in-app-browser.png)<ul><li>ヘッダー<ul><li>最小化ボタンが<b>ある</b></li><li>アクションボタンが<b>ない</b></li></ul></li><li>フッターが<b>ある</b></li></ul> |

※ モジュールモードでは非表示になります。詳しくは、「[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/#registering-liff-app)」を参照してください。

### `liff.isInClient()`メソッドで判別する 

`liff.isInClient()`メソッドを使うと、LIFFブラウザかどうかを判別できます。詳しくは、『LIFF APIリファレンス』の「[liff.isInClient()](https://developers.line.biz/ja/reference/liff/#is-in-client)」を参照してください。

## LIFFブラウザとLINE内ブラウザで利用できる機能の違い 

LIFFブラウザとLINE内ブラウザで利用できる機能の違いは次のとおりです。

| 機能 | LIFFブラウザ | LINE内ブラウザ |
| --- | --- | --- |
| [画面サイズ](https://developers.line.biz/ja/docs/liff/overview/#screen-size)の指定 | ✅ | ❌ |
| [アクションボタン](https://developers.line.biz/ja/docs/liff/overview/#action-button) | ✅ | ❌ |
| [マルチタブビュー](https://developers.line.biz/ja/docs/liff/overview/#multi-tab-view) | ✅ | ❌ |
| [二次元コードリーダー](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#opening-two-dimensional-code-reader) | ✅ | ❌ |
| [トークルームへのメッセージ送信](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#sending-messages) | ✅ | ❌ |
| [シェアターゲットピッカー](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#share-target-picker) | ✅ | ❌ |
| [LIFFアプリではない外部のサイトへの遷移時のポップアップ表示](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#transition-to-external-site) | ✅ | ❌ |
| [LIFF間遷移](https://developers.line.biz/ja/docs/liff/opening-liff-app/#move-liff-to-liff) | ✅ | ❌ |

✅：利用できる<br>❌：利用できない
