# LIFFアプリを開発する

LIFFアプリは、HTMLやJavaScriptで構成されるウェブアプリです。ここでは、LIFFアプリを開発する手順とLIFFアプリ特有の処理について説明します。

<!-- table of contents -->

## LIFFアプリのタイトルを設定する 

LIFFアプリのタイトルは、LIFFアプリのヘッダーに表示されます。LIFFアプリのHTMLソースの`<title>`要素に、LIFFアプリのタイトルを指定します。

```html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>タイトル</title>
```

## LIFFアプリにLIFF SDKを組み込む 

LIFFアプリには、以下の2種類の方法でLIFF SDKを組み込めます。

- [CDNパスを指定する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#specify-cdn-path)
- [npmパッケージを利用する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#use-npm-package)

### CDNパスを指定する 

LIFF SDKで提供する機能を利用するには、LIFFアプリのHTMLソースの`<script>`要素の`src`属性に、LIFF SDKのCDNパスを指定します。LIFFでは、以下の2種類のCDNパスを用意しています。目的に合ったCDNパスを指定してください。

| CDNパス | 説明 |
| --- | --- |
| CDNエッジパス | メジャーバージョンのみを含むCDNパスです。常に最新の機能を使用する場合は、このCDNパスを使用します。メジャーバージョンがアップデートされたときのみURLを更新する必要があります。<br>例：https://static.line-scdn.net/liff/edge/**2**/sdk.js |
| CDN固定パス | パッチバージョンまで含むCDNパスです。特定のバージョンの機能を使用する場合は、このCDNパスを使用します。LIFFアプリを更新しない限り、指定したパッチバージョンを使い続けることができます。LIFFの新機能や、セキュリティ改善、バグ修正を反映したいときのみURLを更新してください。自動的に更新されないため、LIFF SDKのアップデートの影響を受けません。<br>例：https://static.line-scdn.net/liff/edge/**versions/2.22.3**/sdk.js |

<!-- note start -->

**どのバージョンを使うべきか**

CDN固定パスを使用している開発者は、LIFFアプリを更新するタイミングを決める必要があります。アップデートの内容を正しく理解し、自分のLIFFアプリに適しているか判断するために、『LIFFドキュメント』の「[リリースノート](https://developers.line.biz/ja/docs/liff/release-notes/)」をこまめに確認してください。

<!-- note end -->

CDN固定パスを指定する例：

```html
<script charset="utf-8" src="https://static.line-scdn.net/liff/edge/versions/2.22.3/sdk.js"></script>
```

<!-- note start -->

**LIFF SDKはUTF-8で書かれています**

LIFF SDKはUTF-8で書かれているため、HTMLソースをUTF-8以外の文字コードで作成する場合は、`charset="utf-8"`をあわせて指定してください。

<!-- note end -->

### npmパッケージを利用する 

LIFFでは、npmパッケージも公開しています。npmを利用して、LIFF SDKをインストールすることもできます。

<!-- note start -->

**SDKバージョンを管理してください**

適切なSDKバージョンを使用することは開発者の責任です。SDKバージョンを最新の状態に保つために、[LIFFリリースノート](https://developers.line.biz/ja/docs/liff/release-notes/)を定期的に確認し、ローカルのSDKを頻繁に更新してください。LIFFのバージョニングポリシーの詳細は『[LIFF SDK（sdk.js）のアップデートポリシー](https://developers.line.biz/ja/docs/liff/versioning-policy/#update-policy)』を参照してください。

<!-- note end -->

<!-- note start -->

**webpack v5を使ったプロジェクトでLIFF v2.16.0以前のnpm版を使用すると、ビルド時にエラーが発生します**

[webpack v5から、Node.jsのポリフィルが削除されました。](https://webpack.js.org/blog/2020-10-10-webpack-5-release/#automatic-nodejs-polyfills-removed)その影響により、webpack v5を使ったプロジェクトでLIFF v2.16.0以前のnpm版を使用すると、ビルド時にエラーが発生します。詳しくは、2021年10月26日のニュース、「[LIFF v2.16.1をリリースしました](https://developers.line.biz/ja/news/2021/10/26/release-liff-2-16-1/)」を参照してください。

<!-- note end -->

LIFF SDKをnpmでインストールし、アプリに組み込むための手順は、以下のとおりです。

1. 以下のコマンドをターミナルで実行し、npmでLIFF SDKをインストールしてください。

   ```bash
   $ npm install --save @line/liff
   ```

   あるいは、以下のコマンドをターミナルで実行し、YarnでLIFF SDKをインストールすることもできます。

   ```bash
   $ yarn add @line/liff
   ```

1. SDKをアプリに組み込む

   JavaScriptまたはTypeScriptファイルに以下のコードを組み込んでください。

   ```js
   import liff from "@line/liff";

   liff.init({
     liffId: "1234567890-AbcdEfgh", // Use own liffId
   });
   ```

   TypeScriptの型の定義は`@line/liff`パッケージに含まれています。

   <!-- note start -->

   **window.liff を宣言および編集しないでください**

   下位互換性を維持するため、グローバルLIFFインスタンスの`window.liff`を宣言および編集しないでください。LINEが正常に動作しなくなる可能性があります。

   <!-- note end -->

関連ページ：[https://www.npmjs.com/package/@line/liff](https://www.npmjs.com/package/@line/liff)

<!-- tip start -->

**LIFF SDKのファイルサイズを削減する**

プラガブルSDKを使うと、LIFF SDKのファイルサイズを削減できます。詳しくは、「[プラガブルSDK](https://developers.line.biz/ja/docs/liff/pluggable-sdk/)」を参照してください。

<!-- tip end -->

## LIFFアプリを初期化する 

[`liff.init()`](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)メソッドを実行すると、LIFFアプリが初期化され、LIFFアプリからLIFF SDKの他のメソッドを実行できるようになります。

LIFFアプリは、ページを開くたびに必ず初期化する必要があります。同じLIFFアプリ内での遷移であっても、新たにページを開く場合には`liff.init()`メソッドを実行してください。

LIFFアプリが正しく初期化されていない状態でLIFFの機能を使用した場合、それらの動作は保証対象外です。

ユーザーがLINEアプリ上で[LIFF URL](https://developers.line.biz/ja/glossary/#liff-url)にアクセスしてから、LIFFアプリが初期化されるまでの流れは以下のとおりです。

![Interactive SVG](https://developers.line.biz/media/liff/initializing-liff-app-flow-liff-browser-ja.svg)

詳しくは、「[LIFF URLにアクセスしてからLIFFアプリが開くまでの動作について](https://developers.line.biz/ja/docs/liff/opening-liff-app/#redirect-flow)」を参照してください。

<!-- note start -->

**LIFFアプリのクエリパラメータについて**

LIFF URLへのアクセス時やLIFF間遷移時などに、URLに `liff.*` のようなクエリパラメータが付与されることがあります。

例：

- `liff.state`（LIFF URLに指定した追加情報を示す）
- `liff.referrer`（LIFF間遷移前のURLを示す。詳しくは、「[LIFF間遷移前のURLを取得する](https://developers.line.biz/ja/docs/liff/opening-liff-app/#using-liff-referrer)」を参照してください）

上記は、LIFFアプリを正常に動作させるために、SDK側から付与されるクエリパラメータです。LIFFアプリのURLに独自の処理を行う場合は、LIFFアプリの起動やLIFF間遷移などLIFFアプリの正常な動作を保証するため、`liff.init`がresolveされるまで`liff.*`のクエリパラメータを変更しないように設計してください。

<!-- note end -->

<!-- tip start -->

**LIFFアプリを初期化する前でも実行できるメソッド**

以下のプロパティおよびメソッドは、`liff.init()`メソッドを実行する前でも利用できます。たとえば、LIFFアプリを初期化する前にLIFFアプリを動作させている環境を取得できます。

- [liff.ready](https://developers.line.biz/ja/reference/liff/#ready)
- [liff.getOS()](https://developers.line.biz/ja/reference/liff/#get-os)
- [liff.getAppLanguage()](https://developers.line.biz/ja/reference/liff/#get-app-language)
- [liff.getLanguage()](https://developers.line.biz/ja/reference/liff/#get-language)（非推奨）
- [liff.getVersion()](https://developers.line.biz/ja/reference/liff/#get-version)
- [liff.getLineVersion()](https://developers.line.biz/ja/reference/liff/#get-line-version)
- [liff.isInClient()](https://developers.line.biz/ja/reference/liff/#is-in-client)
- [liff.closeWindow()](https://developers.line.biz/ja/reference/liff/#close-window)
- [liff.use()](https://developers.line.biz/ja/reference/liff/#use)
- [liff.i18n.setLang()](https://developers.line.biz/ja/reference/liff/#i18n-set-lang)

`liff.closeWindow()`メソッドは、LIFF SDKバージョンが2.4.0以上の場合のみ、`liff.init()`によるLIFFアプリの初期化が終了する前でも実行できます。

<!-- tip end -->

<!-- tip start -->

**外部ブラウザでのLIFFアプリ初期化時にliff.login()メソッドを自動で実行するには**

`liff.init()`メソッドの`config`オブジェクトの`withLoginOnExternalBrowser`プロパティに`true`を指定することで、外部ブラウザでのLIFFアプリ初期化時に、`liff.login()`メソッドを自動で実行できます。

```js
liff
  .init({
    liffId: "1234567890-AbcdEfgh", // Use own liffId
    withLoginOnExternalBrowser: true, // Enable automatic login process
  })
  .then(() => {
    // Start to use liff's api
  });
```

<!-- tip end -->

`liffId`に指定するLIFFアプリIDは、LIFFアプリをチャネルに追加すると取得できます。詳しくは、「[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)」を参照してください。

```javascript
liff
  .init({
    liffId: "1234567890-AbcdEfgh", // Use own liffId
  })
  .then(() => {
    // start to use LIFF's api
  })
  .catch((err) => {
    console.log(err);
  });
```

なお、`liff.ready`で、LIFFアプリ起動後、`liff.init()`の実行が初めて終了したときにresolveする`Promise`オブジェクトを取得できます。

詳しくは、『LIFF v2 APIリファレンス』の「[liff.init()](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)」および「[liff.ready](https://developers.line.biz/ja/reference/liff/#ready)」を参照してください。

### LIFFアプリ初期化時の注意事項 

LIFFアプリを初期化する際の注意事項は以下のとおりです。注意事項を確認し、理解した上でLIFFアプリの開発を行ってください。

- [`liff.init()`をエンドポイントURL以下の階層で実行する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#initializing-liff-app-notes-1)
- [`liff.init()`を1次リダイレクト先URLと2次リダイレクト先URLで1回ずつ実行する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#initializing-liff-app-notes-2)
- [URLを操作する処理は`liff.init()`が完了してから実行する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#initializing-liff-app-notes-3)
- [1次リダイレクト先URLの取り扱いに注意する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#initializing-liff-app-notes-4)

#### `liff.init()`をエンドポイントURL以下の階層で実行する 

`liff.init()`メソッドはエンドポイントURLと完全に一致、もしくはエンドポイントURLよりも下の階層においてのみ動作します。これら以外のURLに遷移して実行した場合、`liff.init()`メソッドの動作は保証されません。

以下の例では、エンドポイントURLが`https://example.com/path1/`の場合に、`liff.init()`メソッドを実行するURLで動作が保証されるかどうかを示しています。なお、動作が保証されないURLでは、[マルチタブビュー](https://developers.line.biz/ja/docs/liff/overview/#multi-tab-view)などのLIFFアプリの一部機能が正しく動作しない可能性があります。

| `liff.init()`を実行するURL            | 動作の保証 |
| ------------------------------------- | ---------- |
| `https://example.com/`                | ❌         |
| `https://example.com/path1/`          | ✅         |
| `https://example.com/path1/language/` | ✅         |
| `https://example.com/path2/`          | ❌         |

<!-- note start -->

**liff.init()メソッドの実行時に、コンソールに「liff.init() was called with a current URL that is not related to the endpoint URL.」という警告メッセージが表示される**

LIFF v2.27.2以降では、動作が保証されないURLで`liff.init()`メソッドを実行すると、コンソールに警告メッセージが表示されます。

たとえば、LIFFアプリのエンドポイントURLが`https://example.com/path1/path2/`で、`liff.init()`メソッドを実行するURLが`https://example.com/path1/`の場合、表示される警告メッセージは次のとおりです。

```
liff.init() was called with a current URL that is not related to the endpoint URL.
https://example.com/path1/ is not under https://example.com/path1/path2/
```

上記の警告メッセージが表示された場合、エンドポイントURLを`https://example.com/`や`https://example.com/path1/`に変更できないか検討してください。これらのURLに変更することで、`liff.init()`メソッドの動作が保証されます。

<!-- note end -->

#### `liff.init()`を1次リダイレクト先URLと2次リダイレクト先URLで1回ずつ実行する 

`liff.init()`メソッドは、1次リダイレクト先URLに付与される`liff.state`や`access_token=xxx`などの情報を元に初期化処理を行います。エンドポイントURLにクエリパラメータやパスが含まれている場合、正しくLIFFアプリを初期化するために、1次リダイレクト先URLと2次リダイレクト先URLで、1回ずつ`liff.init()`メソッドを実行してください。リダイレクトについて詳しくは、「[LIFF URLにアクセスしてからLIFFアプリが開くまでの動作について](https://developers.line.biz/ja/docs/liff/opening-liff-app/#redirect-flow)」を参照してください。

#### URLを操作する処理は`liff.init()`が完了してから実行する 

URLを操作する処理は、`liff.init()`メソッドが返す`Promise`オブジェクトがresolveしてから実行してください。

```javascript
// Example using window.location.replace()
liff
  .init({
    liffId: "1234567890-AbcdEfgh", // Use own liffId
  })
  .then(() => {
    // Redirect to another page after the returned Promise object has been resolved
    window.location.replace(location.href + "/entry/");
  });
```

`Promise`オブジェクトがresolveする前に、次のようなURLを操作する処理を実行すると、LIFFアプリを正常に開けない場合があります。

- [`Document.location`](https://developer.mozilla.org/ja/docs/Web/API/Document/location)プロパティや[`Window.location`](https://developer.mozilla.org/ja/docs/Web/API/Window/location)プロパティを使ってURLを変更する
- [History API](https://developer.mozilla.org/ja/docs/Web/API/History_API)の[`history.pushState()`](https://developer.mozilla.org/ja/docs/Web/API/History/pushState)メソッドや[`history.replaceState()`](https://developer.mozilla.org/ja/docs/Web/API/History/replaceState)メソッドを使ってURLを変更する
- サーバー側でステータスコード`301`や`302`を返し、別のURLにリダイレクトする

#### 1次リダイレクト先URLの取り扱いに注意する 

1次リダイレクト先URLに自動的に付与される`access_token=xxx`はユーザーのアクセストークン（機密情報）です。Google Analyticsなど外部のロギングツールに、1次リダイレクト先URLを送らないように注意してください。

なお、LIFF v2.11.0以降のバージョンでは、`liff.init()`メソッドがresolveされたタイミングでURLから機密情報が除外されます。そのため、以下のように`then()`メソッド内でページビューを送信することで、機密情報の漏洩を防ぐことができます。ロギングツールを利用する場合は、LIFFアプリをv2.11.0以降にバージョンアップすることをお勧めします。LIFF v2.11.0の更新内容について詳しくは、「[リリースノート](https://developers.line.biz/ja/docs/liff/release-notes/#liff-v2-11-0)」を参照してください。

```javascript
liff
  .init({
    liffId: "1234567890-AbcdEfgh", // Use own liffId
  })
  .then(() => {
    ga("send", "pageview");
  });
```

### 外部ブラウザでLINEログインを利用する場合 

外部ブラウザでLINEログインを利用する場合は、以下のとおり`liff.init()`メソッドを2回実行します。

1. LIFF SDKロード後に、`liff.init()`メソッドを実行します。
1. `liff.login()`メソッドを実行し、認証ページおよび認可画面の処理が終了すると、LIFFアプリ（`redirectUri`）にリダイレクトされます。そこで、改めて`liff.init()`メソッドを実行します。

   `liff.init()`メソッドの処理中にエラーが発生した場合、またはログイン時にユーザーが認可をキャンセルした場合は、`errorCallback`が実行されます。

![フロー図](https://developers.line.biz/media/liff/initializing-liff-app-flow.png)

<!-- note start -->

**LIFFブラウザ内での認可リクエストについて**

LIFFブラウザ内でLINEログインによる認可リクエストを行った際の動作は保証されません。また、LIFFアプリを外部ブラウザやLINE内ブラウザで開く場合には、必ず[`liff.login()`](https://developers.line.biz/ja/reference/liff/#login)メソッドでログイン処理を行い、[LINEログインによる認可リクエスト](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#making-an-authorization-request)は行わないでください。

<!-- note end -->

## LIFF APIを呼び出す 

LIFF SDKの組み込みとLIFFの初期化を行うことで、LIFFアプリの機能を使用できます。

- [LIFFアプリが動作している環境を取得する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#getting-environment)
- [ログイン処理を行う](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#login-with-line-login)
- [URLを開く](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#opening-url)
- [二次元コードリーダーを表示する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#opening-two-dimensional-code-reader)
- [LIFFアプリが起動された画面を取得する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#getting-context)
- [ユーザーのプロフィールを取得する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#getting-user-profile)
- [ユーザーとLINE公式アカウントの友だち関係を取得する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#get-friendship-status)
- [現在のページのパーマネントリンクを取得する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#get-permanent-link)
- [現在のトークルームにメッセージを送信する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#sending-messages)
- [ユーザーの友だちにメッセージを送信する（シェアターゲットピッカー）](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#share-target-picker)
- [LIFFアプリを閉じる](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#closing-liff-app)

### LIFFアプリが動作している環境を取得する 

`liff.isInClient()`メソッドや`liff.getOS()`メソッドなどを実行して、LIFFアプリが動作している環境を取得します。

```javascript
// print the environment in which the LIFF app is running
console.log(liff.getAppLanguage());
console.log(liff.getVersion());
console.log(liff.isInClient());
console.log(liff.isLoggedIn());
console.log(liff.getOS());
console.log(liff.getLineVersion());
```

詳しくは、『LIFF APIリファレンス』の各メソッドを参照してください。

- [liff.getAppLanguage()](https://developers.line.biz/ja/reference/liff/#get-app-language)
- [liff.getVersion()](https://developers.line.biz/ja/reference/liff/#get-version)
- [liff.isInClient()](https://developers.line.biz/ja/reference/liff/#is-in-client)
- [liff.isLoggedIn()](https://developers.line.biz/ja/reference/liff/#is-logged-in)
- [liff.getOS()](https://developers.line.biz/ja/reference/liff/#get-os)
- [liff.getLineVersion()](https://developers.line.biz/ja/reference/liff/#get-line-version)

### ログイン処理を行う 

[外部ブラウザ](https://developers.line.biz/ja/glossary/#external-browser)および[LINE内ブラウザ](https://developers.line.biz/ja/glossary/#line-iab)の場合、`liff.login()`メソッドを実行して、ログイン処理を行います。

<!-- note start -->

**注意**

LIFFブラウザの場合、`liff.init()`実行時に自動でログイン処理が実行されるため、`liff.login()`は利用できません。

<!-- note end -->

<!-- tip start -->

**liff.init()メソッド実行時にwithLoginOnExternalBrowserプロパティをtrueにした場合**

`liff.init()`メソッドの`withLoginOnExternalBrowser`プロパティを`true`に指定した場合、外部ブラウザでもLIFFアプリ初期化時に`liff.login()`メソッドを自動で実行することができます。詳しくは、『LIFF APIリファレンス』の「[liff.init()](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)」を参照してください。

<!-- tip end -->

```javascript
// login call, only when external browser or LINE's in-app browser is used
if (!liff.isLoggedIn()) {
  liff.login();
}
```

また、`liff.logout()`メソッドを実行して、ログアウトすることもできます。

```javascript
// logout call only when external browse or LINE's in-app browser is used
if (liff.isLoggedIn()) {
  liff.logout();
  window.location.reload();
}
```

詳しくは、『LIFF v2 APIリファレンス』の「[liff.login()](https://developers.line.biz/ja/reference/liff/#login)」および「[liff.logout()](https://developers.line.biz/ja/reference/liff/#logout)」を参照してください。

### URLを開く 

`liff.openWindow()`メソッドを実行して、指定したURLをLINE内ブラウザまたは外部ブラウザで開きます。

以下のコードは`https://line.me`を外部ブラウザで開きます。

```javascript
// openWindow call
liff.openWindow({
  url: "https://line.me",
  external: true,
});
```

詳しくは、『LIFF v2 APIリファレンス』の「[liff.openWindow()](https://developers.line.biz/ja/reference/liff/#open-window)」を参照してください。

### 二次元コードリーダーを表示する 

`liff.scanCodeV2()`メソッドを実行して、二次元コードリーダーを起動し、ユーザーが読み取った文字列を取得します。

```javascript
// scanCodeV2 call
liff
  .scanCodeV2()
  .then((result) => {
    // e.g. result = { value: 'Hello LIFF app!' }
  })
  .catch((err) => {
    console.log(err);
  });
```

詳しくは、『LIFF APIリファレンス』の「[liff.scanCodeV2()](https://developers.line.biz/ja/reference/liff/#scan-code-v2)」を参照してください。

<!-- note start -->

**liff.scanCode()メソッドは非推奨です**

従来の`liff.scanCode()`メソッドは[非推奨](https://developers.line.biz/ja/glossary/#deprecated)になります。二次元コードリーダーを実装する場合は、`liff.scanCodeV2()`メソッドを使用することをお勧めします。

<!-- note end -->

<!-- note start -->

**liff.scanCode2()メソッドの動作環境**

`liff.scanCodeV2()`メソッドは以下の環境で動作します。

- iOS：iOS14.3以降
- Android：すべてのバージョン
- 外部ブラウザ：[WebRTC API](https://developer.mozilla.org/ja/docs/Web/API/WebRTC_API) をサポートするウェブブラウザ

<table>
  <thead>
    <tr>
      <th>OS</th>
      <th>バージョン</th>
      <th>LIFFブラウザ</th>
      <th>外部ブラウザ</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">iOS</td>
      <td>11〜14.2</td>
      <td>❌</td>
            <td>✅ ※1</td>
    </tr>
    <tr>
      <td>14.3以降</td>
      <td>✅ ※2</td>
      <td>✅ ※1</td>
    </tr>
    <tr>
      <td>Android</td>
      <td>すべてのバージョン</td>
      <td>✅ ※2</td>
      <td>✅ ※1</td>
    </tr>
    <tr>
      <td>PC</td>
      <td>すべてのバージョン</td>
      <td>❌</td>
      <td>✅ ※1</td>
    </tr>
  </tbody>
</table>

※1 [WebRTC API](https://developer.mozilla.org/ja/docs/Web/API/WebRTC_API)をサポートするウェブブラウザのみ利用できます。

※2 LIFFブラウザの画面サイズが`Full`の場合のみ利用できます。詳しくは、『LIFFドキュメント』の「[LIFFブラウザの画面サイズ](https://developers.line.biz/ja/docs/liff/overview/#screen-size)」を参照してください。

<!-- note end -->

<!-- note start -->

**二次元コードリーダーを起動するには［Scan QR］をオンにしてください**

[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)ときに、［**Scan QR**］をオンにしてください。［**Scan QR**］の設定は、LIFFアプリ追加後も[LINE Developersコンソール](https://developers.line.biz/console/)のLIFFタブで変更できます。

<!-- note end -->

### LIFFアプリが起動された画面を取得する 

`liff.getContext()`メソッドを実行して、LIFFアプリが起動された画面（1対1のトーク、グループトーク、複数人トーク、または外部ブラウザ）に関する情報を取得します。

```javascript
const context = liff.getContext();
console.log(context);
// {"type": "utou", "userId": "U70e153189a29f1188b045366285346bc", "viewType": "full", "accessTokenHash": "ArIXhlwQMAZyW7SDHm7L2g", "availability": {"shareTargetPicker": {"permission": true, "minVer": "10.3.0"}, "multipleLiffTransition": {"permission": true, "minVer": "10.18.0"}}}
```

詳しくは、『LIFF v2 APIリファレンス』の「[liff.getContext()](https://developers.line.biz/ja/reference/liff/#get-context)」を参照してください。

### ユーザーのプロフィールを取得する 

LIFFアプリでIDトークンを取得して、ユーザーのプロフィールを取得する方法は2つあります。目的に合わせて正しく使い分けてください。

- [サーバーに送信するために取得する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#getting-tokens)
- [LIFFアプリで使用するために取得する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#getting-decoded-id-token)

<!-- note start -->

**スコープを選択してください**

[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)ときに、`openid`スコープを選択してください。スコープを選択しなかった場合やユーザーが認可しなかった場合は、IDトークンを取得できません。スコープの選択は、LIFFアプリ追加後も[LINE Developersコンソール](https://developers.line.biz/console/)のLIFFタブで変更できます。

<!-- note end -->

<!-- tip start -->

**メールアドレスを取得できます**

[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)ときに、`email`スコープを選択し、ユーザーが認可すると、メールアドレスも取得できます。スコープの選択は、LIFFアプリ追加後も[LINE Developersコンソール](https://developers.line.biz/console/)のLIFFタブで変更できます。

<!-- tip end -->

#### サーバーに送信するために取得する 

LIFFアプリからサーバーにユーザー情報を送信する場合は、以下の方法で取得したアクセストークンまたはIDトークンを送信します。サーバーでユーザー情報を使用する方法について詳しくは、「[LIFFアプリおよびサーバーでユーザー情報を使用する](https://developers.line.biz/ja/docs/liff/using-user-profile/)」を参照してください。

- `liff.getAccessToken()`メソッドを実行して、現在のユーザーのアクセストークンを取得します。詳しくは、『LIFF v2 APIリファレンス』の「[liff.getAccessToken()](https://developers.line.biz/ja/reference/liff/#get-access-token)」を参照してください。

  ```javascript
  // get access token
  if (!liff.isLoggedIn() && !liff.isInClient()) {
    window.alert(
      'To get an access token, you need to be logged in. Tap the "login" button below and try again.',
    );
  } else {
    const accessToken = liff.getAccessToken();
    console.log(accessToken);
  }
  ```

- `liff.getIDToken()`メソッドを実行して、「現在のユーザーの生のIDトークン」を取得します。詳しくは、『LIFF v2 APIリファレンス』の「[liff.getIDToken()](https://developers.line.biz/ja/reference/liff/#get-id-token)」を参照してください。

  ```javascript
  liff.init(() => {
    const idToken = liff.getIDToken();
    console.log(idToken); // print raw idToken object
  });
  ```

#### LIFFアプリで使用するために取得する 

`liff.getDecodedIDToken()`メソッドを実行して、現在のユーザーのプロフィール情報およびメールアドレスを取得します。

LIFFアプリでユーザーの表示名などを利用する場合に、このAPIを利用してください。

<!-- warning start -->

**ユーザー情報をサーバーに送信しないでください**

`liff.getDecodedIDToken()`で取得したユーザー情報をサーバーに送信しないでください。代わりに、[`liff.getIDToken()`](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#getting-tokens)で取得したIDトークンを送信します。

<!-- warning end -->

```javascript
liff.init(() => {
  const idToken = liff.getDecodedIDToken();
  console.log(idToken); // print decoded idToken object
});
```

詳しくは、『LIFF v2 APIリファレンス』の「[liff.getDecodedIDToken()](https://developers.line.biz/ja/reference/liff/#get-decoded-id-token)」を参照してください。

### ユーザーとLINE公式アカウントの友だち関係を取得する 

ユーザーと、LIFFアプリが追加されているLINEログインのチャネルにリンクされているLINE公式アカウントの友だち関係を取得します。

LINEログインのチャネルにLINE公式アカウントをリンクする方法については、『LINEログインドキュメント』の「[LINEログインしたときにLINE公式アカウントを友だち追加する（友だち追加オプション）](https://developers.line.biz/ja/docs/line-login/link-a-bot/)」を参照してください。

```javascript
liff.getFriendship().then((data) => {
  if (data.friendFlag) {
    // something you want to do
  }
});
```

詳しくは、『LIFF v2 APIリファレンス』の「[liff.getFriendship()](https://developers.line.biz/ja/reference/liff/#get-friendship)」を参照してください。

<!-- note start -->

**スコープを選択してください**

[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)ときに、`profile`スコープを選択してください。スコープを選択しなかった場合やユーザーが認可しなかった場合は、友だち関係を取得できません。スコープの選択は、LIFFアプリ追加後も[LINE Developersコンソール](https://developers.line.biz/console/)のLIFFタブで変更できます。

<!-- note end -->

### ユーザーにLINE公式アカウントの友だち追加またはブロック解除を促す 

LINE公式アカウントの友だち追加、またはブロック解除を促すサブウィンドウを表示します。

- LINE公式アカウントと友だちになっていない場合は、友だち追加を促すサブウィンドウが表示されます。
- LINE公式アカウントをブロックしている場合は、ブロック解除を促すサブウィンドウが表示されます。
- LINE公式アカウントと既に友だちになっている場合は、サブウィンドウが表示された後、自動で閉じられます。

```javascript
try {
  await liff.requestFriendship();
} catch (error) {
  console.log(error);
}
```

詳しくは、『LIFF v2 APIリファレンス』の「[liff.requestFriendship()](https://developers.line.biz/ja/reference/liff/#request-friendship)」を参照してください。

### LIFFアプリの任意のページのパーマネントリンクを取得する 

`liff.permanentLink.createUrlBy()`メソッドを実行して、LIFFアプリの任意のページのパーマネントリンクを取得できます。

```javascript
// For example, if the endpoint URL of the LIFF app is https://example.com/path1?q1=v1 and its LIFF ID is 1234567890-AbcdEfgh
liff.permanentLink
  .createUrlBy("https://example.com/path1?q1=v1")
  .then((permanentLink) => {
    // https://liff.line.me/1234567890-AbcdEfgh
    console.log(permanentLink);
  });

liff.permanentLink
  .createUrlBy("https://example.com/path1/path2?q1=v1&q2=v2")
  .then((permanentLink) => {
    // https://liff.line.me/1234567890-AbcdEfgh/path2?q=2=v2
    console.log(permanentLink);
  });
```

詳しくは、『LIFF v2 APIリファレンス』の「[liff.permanentLink.createUrlBy()](https://developers.line.biz/ja/reference/liff/#permanent-link-create-url-by)」を参照してください。

### 現在のトークルームにメッセージを送信する 

`liff.sendMessages()`メソッドを実行して、ユーザーの代わりに、LIFFアプリが開かれているトークルームにメッセージを送信します。1回のリクエストでメッセージオブジェクトを最大5つまで送信できます。

以下のコードは、LIFFアプリが表示されているトークルームに、ユーザーのメッセージとして「Hello, World!」を送信します。

```javascript
liff
  .sendMessages([
    {
      type: "text",
      text: "Hello, World!",
    },
  ])
  .then(() => {
    console.log("message sent");
  })
  .catch((err) => {
    console.log("error", err);
  });
```

詳しくは、『LIFF APIリファレンス』の「[liff.sendMessages()](https://developers.line.biz/ja/reference/liff/#send-messages)」を参照してください。

### ユーザーの友だちにメッセージを送信する（シェアターゲットピッカー） 

`liff.shareTargetPicker()`メソッドを実行して、ターゲットピッカー（グループまたは友だちを選択する画面）を表示し、ターゲットピッカーで選択した相手に、開発者が作成したメッセージを送信します。このメッセージは、ユーザーが送信したかのように、グループまたは友だちに表示されます。

ターゲットピッカーで選択できる対象は、ユーザーの友だち（LINE公式アカウントを含む）と、ユーザーが参加しているグループのみです。オープンチャットは含まれません。

![target picker](https://developers.line.biz/media/liff/share-target-picker_tobe_ja.png)

#### シェアターゲットピッカーを利用するには 

シェアターゲットピッカーを利用するには、以下の手順に従って「情報利用に関する同意について」に同意する必要があります。この同意は、チャネルごとに必要です。

1. [LINE Developersコンソール](https://developers.line.biz/console/)で、LIFFアプリを追加するLINEログインのチャネルを選択します。
1. ［**LIFF**］タブの［**シェアターゲットピッカー**］をクリックすると、「情報利用に関する同意について」が表示されます。
1. 表示された内容をよく読み、［**上記の事項に同意する**］をチェックし、［**有効化**］をクリックします。

#### シェアターゲットピッカーのサンプルコード 

以下のコードは、ターゲットピッカーを表示し、選択したグループまたは友だちに、ユーザーのメッセージとして「Hello, World!」を送信します。あらかじめ、`liff.isApiAvailable()`メソッドを実行すると、LIFFアプリを起動した環境でターゲットピッカーが使用可能であることを確認できます。

```javascript
if (liff.isApiAvailable("shareTargetPicker")) {
  liff.shareTargetPicker([
    {
      type: "text",
      text: "Hello, World!",
    },
  ]);
}
```

詳しくは、『LIFF v2 APIリファレンス』の「[liff.isApiAvailable()](https://developers.line.biz/ja/reference/liff/#is-api-available)」および「[liff.shareTargetPicker()](https://developers.line.biz/ja/reference/liff/#share-target-picker)」を参照してください。

### LIFFアプリを閉じる 

`liff.closeWindow()`メソッドを実行して、開いているLIFFアプリを閉じます。

```javascript
// closeWindow call
if (!liff.isInClient()) {
  window.alert(
    "This button is unavailable as LIFF is currently being opened in an external browser.",
  );
} else {
  liff.closeWindow();
}
```

詳しくは、『LIFF v2 APIリファレンス』の「[liff.closeWindow()](https://developers.line.biz/ja/reference/liff/#close-window)」を参照してください。

<!-- note start -->

**注意**

`liff.closeWindow()`の外部ブラウザでの動作は、保証対象外です。

<!-- note end -->

## OGPタグを設定する 

LIFFアプリの各ページにOGPタグを設定すると、たとえばLINEのトークルームでLIFFアプリのURL（`https://liff.line.me/{liffId}`）をシェアしたときに、任意のタイトルや説明文、サムネイル画像を表示できます。

LIFFで対応しているOGPタグは以下のとおりです。OGPタグについて詳しくは、「[The Open Graph protocol](https://ogp.me/)」を参照してください。

```html
<html lang="ja" prefix="og: http://ogp.me/ns#">
<meta property="og:title" content="タイトル">
<meta property="og:type" content="`website`、`blog`、または`article`">
<meta property="og:description" content="ページの簡単な説明">
<meta property="og:url" content="ページのURL">
<meta property="og:site_name" content="サイト全体を表す名前">
<meta property="og:image" content="サムネイル画像のURL">
```

<!-- note start -->

**注意**

LIFFアプリのURLを、`line://app/{liffId}`（非推奨）の形式でシェアしたときは、OGPタグは無視されます。

<!-- note end -->

## LIFFアプリではない外部のサイトに遷移した場合 

LIFFブラウザでは、LIFFアプリからLIFFアプリでない外部サイトを開いた場合、「外部サイトに遷移した」ということを示すポップアップが表示されます。

![外部サイトに遷移した時のポップアップ](https://developers.line.biz/media/news/2022/liff-opening-external-site-ja.jpg)

ポップアップは、同じウィンドウで外部サイトを開いた場合にのみ表示されます。別のウィンドウで外部サイトを開いた場合は、ポップアップは表示されません。

<!-- note start -->

**LIFFアプリのエンドポイントURLより上の階層への遷移**

LIFFアプリで、エンドポイントURL（例：`https://example.com/path`）より上の階層（例：`https://example.com/`）へ遷移した際の動作は保証されません。

<!-- note end -->

## LIFFアプリを閉じたときの挙動 

LIFFブラウザで開かれているLIFFアプリを、ユーザーの操作や[`liff.closeWindow()`](https://developers.line.biz/ja/reference/liff/#close-window)で閉じたときの挙動は、LINEアプリのバージョンやLIFFアプリの設定によって異なります。

### LINEアプリのバージョンが15.12.0以降の場合 

LINEアプリのバージョンが15.12.0以降の場合、LIFFアプリがマルチタブビューの[「最近使用したサービス」に表示される条件](https://developers.line.biz/ja/docs/liff/overview/#multi-tab-view-condition)を満たしているかどうかでLIFFアプリを閉じたときの挙動が変わります。

| | |
| --- | --- |
| 条件を満たしている場合 | LIFFアプリを閉じた場合も、12時間以内であればLIFFアプリが再開できます。アクセストークンやブラウザの閲覧履歴、画面のスクロール位置は保持されます。 |
| 条件を満たしていない場合 | LIFFアプリを閉じると同時にLIFFアプリが終了します。このため、LIFFアプリを閉じるとアクセストークンは無効化されます。 |

詳しくは、「[最近使用したサービス](https://developers.line.biz/ja/docs/liff/overview/#multi-tab-view-recent-service)」を参照してください。

### LINEアプリのバージョンが15.12.0より前の場合 

LINEアプリのバージョンが15.12.0より前の場合、LIFFアプリを閉じると同時にLIFFアプリが終了します。このため、LIFFアプリを閉じるとアクセストークンは無効化されます。

## 次のステップ 

LIFFアプリを開発したら、任意のサーバーにデプロイしてください。デプロイ後は、以下の操作を行います。

1. [LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)
1. [LIFFアプリを開く](https://developers.line.biz/ja/docs/liff/opening-liff-app/)
