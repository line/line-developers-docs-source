# 外部ブラウザでLINEミニアプリを開く

<!-- tip start -->

**2025年10月1日より外部ブラウザでLINEミニアプリを利用できるようになりました**

詳しくは、2025年9月26日のニュース、「[LINEミニアプリにおいて、2025年10月1日よりすべてのユーザーがウェブブラウザでサービスを利用できるようになります](https://developers.line.biz/ja/news/2025/09/26/mini-app-browser/)」を参照してください。

<!-- tip end -->

LINEミニアプリを開発する際は、ユーザーが[外部ブラウザ](https://developers.line.biz/ja/glossary/#external-browser)でエンドポイントURLにアクセスした場合にも、LINEミニアプリのサービスを利用できるようにしてください。

LINEミニアプリを外部ブラウザで利用する際には、以下の点に注意してください。

<!-- table of contents -->

## LINEログインが必要なサービスの場合は明示的にログイン処理を行う 

外部ブラウザでLINEミニアプリを開く場合、LIFFブラウザとは異なり[`liff.init()`](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)メソッドを実行するだけではLINEログインが実行されません。

そのため、サービスを利用するためにLINEログインが必要な場合は、以下のいずれかの方法でLINEログインを明示的に実行する必要があります。

### 1. 初期化時に自動的にLINEログインを実行する 

[`liff.init()`](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)メソッドの`config`オブジェクトの`withLoginOnExternalBrowser`プロパティに`true`を指定することで、外部ブラウザでのLIFFアプリ初期化時に、[`liff.login()`](https://developers.line.biz/ja/reference/liff/#login)メソッドを自動で実行できます。

例：

```js
liff
  .init({
    liffId: "1234567890-AbcdEfgh", // LIFF IDを指定する
    withLoginOnExternalBrowser: true, // 自動ログインを有効にする
  })
  .then(() => {
    // LIFF APIの利用を始める
  });
```

### 2. 未ログインの場合にLINEログインを実行する 

ユーザーのLINEログインが必要になったタイミングで、未ログインの場合にLINEログインを実行します。

[`liff.isLoggedIn()`](https://developers.line.biz/ja/reference/liff/#is-logged-in)メソッドでユーザーのログイン状態を確認し、未ログインの場合は[`liff.login()`](https://developers.line.biz/ja/reference/liff/#login)メソッドを実行します。

例：

```js
if (!liff.isLoggedIn()) {
  liff.login();
}
```

詳しくは、『LIFFドキュメント』の「[外部ブラウザでLINEログインを利用する場合](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#to-use-line-login-in-external-browser)」を参照してください。

## 外部ブラウザで利用できない機能を使う場合はユーザーをLINEアプリに誘導する 

LINEミニアプリが外部ブラウザで利用できない機能を使う必要がある場合、ユーザーがLINEアプリ上でLINEミニアプリを開く必要があります。

外部ブラウザで利用できない機能、および動作が保証されていない機能は以下のとおりです。

- [liff.sendMessages()](https://developers.line.biz/ja/reference/liff/#send-messages)
- [liff.openWindow()](https://developers.line.biz/ja/reference/liff/#open-window)
- [liff.closeWindow()](https://developers.line.biz/ja/reference/liff/#close-window)
- [liff.scanCode()](https://developers.line.biz/ja/reference/liff/#scan-code)（非推奨）
- [liff.iap.*（アプリ内課金）](https://developers.line.biz/ja/reference/line-mini-app/#in-app-purchase)

該当する機能を利用しているLINEミニアプリが外部ブラウザで開かれた場合、画面上に「この機能を利用するにはLINEアプリでLINEミニアプリを開く必要があります。」といった文言とLINEミニアプリへのリンクを設置することを推奨しています。

なお、[`liff.getContext()`](https://developers.line.biz/ja/reference/liff/#get-context)メソッドや、[`liff.isInClient()`](https://developers.line.biz/ja/reference/liff/#is-in-client)メソッドを使うことでLINEミニアプリの動作環境を取得できます。LINEミニアプリの動作環境に応じて表示を変更する場合は、これらのメソッドの利用を推奨します。

## LINE未使用のユーザーがLINEミニアプリを開くことを想定する 

LINE未使用のユーザーでもLINEミニアプリを利用できるようにする場合は、外部ブラウザでLINEミニアプリを開いた後、LINEログインを実行せずにサービスが動作するようにしてください。

外部ブラウザでLINEログインしなくても使用可能なLIFF APIのプロパティとメソッドは以下のとおりです。

- [liff.id](https://developers.line.biz/ja/reference/liff/#id)
- [liff.ready](https://developers.line.biz/ja/reference/liff/#ready)
- [liff.init()](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)
- [liff.getOS()](https://developers.line.biz/ja/reference/liff/#get-os)
- [liff.getAppLanguage()](https://developers.line.biz/ja/reference/liff/#get-app-language)
- [liff.getLanguage()](https://developers.line.biz/ja/reference/liff/#get-language)（非推奨）
- [liff.getVersion()](https://developers.line.biz/ja/reference/liff/#get-version)
- [liff.getLineVersion()](https://developers.line.biz/ja/reference/liff/#get-line-version)
- [liff.isInClient()](https://developers.line.biz/ja/reference/liff/#is-in-client)
- [liff.isLoggedIn()](https://developers.line.biz/ja/reference/liff/#is-logged-in)
- [liff.permanentLink.createUrlBy()](https://developers.line.biz/ja/reference/liff/#permanent-link-create-url-by)
- [liff.use()](https://developers.line.biz/ja/reference/liff/#use)
