# LIFF v2 APIリファレンス

## 共通仕様 

### 動作環境 

LIFF v2の動作環境については、『LIFFドキュメント』の「[概要](https://developers.line.biz/ja/docs/liff/overview/)」を参照してください。

なお、LIFFアプリをLIFFブラウザで開いた場合と、外部ブラウザで開いた場合では、使用できる機能が異なります。たとえば、`liff.scanCode()`は、外部ブラウザでは利用できません。詳しくは、各クライアントAPIの説明をご覧ください。

<!-- note start -->

**OpenChatでのLIFFアプリの利用はサポートされていません**

現在のところ、OpenChatではLIFFアプリの利用は正式にサポートされていません。たとえば、LIFFアプリからプロフィール情報を取得できない場合があります。

<!-- note end -->

### LIFF SDKのエラー 

LIFF SDKのエラーはLiffErrorオブジェクトで返されます。

<!-- note start -->

**エラーを識別する際は、エラーコードとエラーメッセージの両方を参照してください**

エラーメッセージは予告なく変更されることがあるため、エラーをエラーメッセージの完全一致で識別すると、LIFFアプリが正常に動作しなくなる可能性があります。エラーを識別する際は、エラーメッセージが変更されてもLIFFアプリが正常に動作するよう、エラーコードとエラーメッセージの両方を参照してください。

なお、エラーコードによってエラーを一意に識別できるよう、将来的に改善する予定です。

<!-- note end -->

_例_

<!-- tab start `json` -->

```json
{
  "code": "INIT_FAILED",
  "message": "Failed to init LIFF SDK"
}
```

<!-- tab end -->

#### LiffErrorオブジェクト 

<!-- parameter start -->

code

String

エラーコード

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

message

String

エラーメッセージ

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

cause

Unknown

エラーの原因

<!-- parameter end -->

#### エラー内容 

| エラーコード | 説明 |
| --- | --- |
| 400 | リクエストに問題があります。リクエストパラメータとJSONの形式を確認してください。 |
| 401 | Authorizationヘッダーを正しく送信していることを確認してください。 |
| 403 | APIを使用する権限がありません。ご契約中のプランやアカウントに付与されている権限を確認してください。 |
| 429 | リクエスト頻度をレート制限内に抑えてください。 |
| 500 | APIサーバーの一時的なエラーです。 |
| INIT_FAILED | LIFF SDKの初期化時にエラーが発生しました。 |
| INVALID_ARGUMENT | 無効な引数が指定されました。 |
| UNAUTHORIZED | <ul><li>ユーザーが認可しませんでした。</li><li>アクセストークンを指定せずにAPIが呼ばれました。</li><li>ログイン処理を行う前に、シェアターゲットピッカーを呼び出しました。</li></ul> |
| FORBIDDEN | <ul><li>必要な権限がありません。</li><li>サポートされていない環境で機能を利用しようとしました。</li></ul> |
| INVALID_CONFIG | 無効な設定です。<ul><li>[`liff.init()`](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)を使ってLIFFアプリを初期化するには、liffIdを指定する必要があります。</li><li>[`liff.permanentLink.createUrl()`](https://developers.line.biz/ja/reference/liff/#permanent-link-create-url)を実行したページのURLが、［**エンドポイントURL**］に指定したURLで始まりません。</li></ul> |
| INVALID_ID_TOKEN | IDトークンが正規のものであることを確認できませんでした。 |
| EXCEPTION_IN_SUBWINDOW | サブウィンドウで問題が発生しました。<ul><li>ターゲットピッカー（グループまたは友だちを選択する画面）を表示後、10分以上操作しなかった場合など</li></ul> |
| UNKNOWN | 不明なエラーです。 |

## LIFF SDKのプロパティ 

### liff.id 

[`liff.init()`](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)に渡したLIFFアプリID（`String`型）を保持するプロパティです。

`liff.init()`を実行するまでは、`null`です。

_例_

<!-- tab start `javascript` -->

```javascript
const liffId = "my-liff-id";
liff.init({ liffId });

// liff.id equals to liffId
```

<!-- tab end -->

### liff.ready 

LIFFアプリ起動後、[`liff.init()`](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)の実行が初めて終了したときにresolveする`Promise`オブジェクトを保持するプロパティです。

`liff.ready`を利用すると、`liff.init()`の終了を待って、任意の処理を実行できます。

<!-- tip start -->

**LIFFアプリ初期化前でも実行できます**

`liff.ready`は、`liff.init()`によるLIFFアプリの初期化が終了する前でも実行できます。

<!-- tip end -->

_例_

<!-- tab start `javascript` -->

```javascript
liff.ready.then(() => {
  // do something you want when liff.init finishes
});
```

<!-- tab end -->

<!-- note start -->

**注意**

`liff.init()`実行中に何か問題が起きても、`liff.ready`はrejectしません。また、[`LiffError`オブジェクト](https://developers.line.biz/ja/reference/liff/#liff-errors)を返すこともありません。

<!-- note end -->

## 初期化 

### liff.init() 

LIFFアプリを初期化します。

このメソッドを実行すると、LIFF SDKの他のメソッドを実行できるようになります。LIFFアプリは、ページを開くたびに必ず初期化する必要があります。同じLIFFアプリ内での遷移であっても、新たにページを開く場合には`liff.init()`メソッドを実行してください。

LIFFアプリが正しく初期化されていない状態でLIFFの機能を使用した場合、それらの動作は保証対象外です。

`liff.init()`メソッドを実行するとき、LIFF SDKは現在のユーザーのアクセストークンやIDトークンをLINEプラットフォームから取得します。

- LIFF SDKが取得したアクセストークンを利用するには、「[liff.getAccessToken()](https://developers.line.biz/ja/reference/liff/#get-access-token)」を呼び出します。
- LIFF SDKが取得したIDトークンのペイロードを利用するには、「[liff.getDecodedIDToken()](https://developers.line.biz/ja/reference/liff/#get-decoded-id-token)」を呼び出します。

#### LIFFアプリ初期化時の注意事項 

LIFFアプリを初期化する際の注意事項は以下のとおりです。注意事項を確認し、理解した上でLIFFアプリの開発を行ってください。

- [`liff.init()`をエンドポイントURL以下の階層で実行する](https://developers.line.biz/ja/reference/liff/#initializing-liff-app-notes-1)
- [`liff.init()`を1次リダイレクト先URLと2次リダイレクト先URLで1回ずつ実行する](https://developers.line.biz/ja/reference/liff/#initializing-liff-app-notes-2)
- [URLを操作する処理は`liff.init()`が完了してから実行する](https://developers.line.biz/ja/reference/liff/#initializing-liff-app-notes-3)
- [1次リダイレクト先URLの取り扱いに注意する](https://developers.line.biz/ja/reference/liff/#initializing-liff-app-notes-4)

##### `liff.init()`をエンドポイントURL以下の階層で実行する 

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

##### `liff.init()`を1次リダイレクト先URLと2次リダイレクト先URLで1回ずつ実行する 

`liff.init()`メソッドは、1次リダイレクト先URLに付与される`liff.state`や`access_token=xxx`などの情報を元に初期化処理を行います。エンドポイントURLにクエリパラメータやパスが含まれている場合、正しくLIFFアプリを初期化するために、1次リダイレクト先URLと2次リダイレクト先URLで、1回ずつ`liff.init()`メソッドを実行してください。リダイレクトについて詳しくは、『LIFFドキュメント』の「[LIFF URLにアクセスしてからLIFFアプリが開くまでの動作について](https://developers.line.biz/ja/docs/liff/opening-liff-app/#redirect-flow)」を参照してください。

##### URLを操作する処理は`liff.init()`が完了してから実行する 

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

##### 1次リダイレクト先URLの取り扱いに注意する 

1次リダイレクト先URLに自動的に付与される`access_token=xxx`はユーザーのアクセストークン（機密情報）です。Google Analyticsなど外部のロギングツールに、1次リダイレクト先URLを送らないように注意してください。

なお、LIFF v2.11.0以降のバージョンでは、`liff.init()`メソッドがresolveされたタイミングでURLから機密情報が除外されます。そのため、以下のように`then()`メソッド内でページビューを送信することで、機密情報の漏洩を防ぐことができます。ロギングツールを利用する場合は、LIFFアプリをv2.11.0以降にバージョンアップすることをお勧めします。LIFF v2.11.0の更新内容について詳しくは、『LIFFドキュメント』の「[リリースノート](https://developers.line.biz/ja/docs/liff/release-notes/#liff-v2-11-0)」を参照してください。

```javascript
liff
  .init({
    liffId: "1234567890-AbcdEfgh", // Use own liffId
  })
  .then(() => {
    ga("send", "pageview");
  });
```

<!-- note start -->

**LIFFアプリのクエリパラメータについて**

LIFF URLへのアクセス時やLIFF間遷移時などに、URLに `liff.*` のようなクエリパラメータが付与されることがあります。

例：

- `liff.state`（LIFF URLに指定した追加情報を示す）
- `liff.referrer`（LIFF間遷移前のURLを示す。詳しくは、「[LIFF間遷移前のURLを取得する](https://developers.line.biz/ja/docs/liff/opening-liff-app/#using-liff-referrer)」を参照してください。）

上記は、LIFFアプリを正常に動作させるために、SDK側から付与されるクエリパラメータです。 LIFFアプリのURLに独自の処理を行う場合は、LIFFアプリの起動やLIFF間遷移などLIFFアプリの正常な動作を保証するため、`liff.init`がresolveされるまで`liff.*`のクエリパラメータを変更しないように設計してください。

<!-- note end -->

<!-- tip start -->

**LIFFアプリを初期化する前でも実行できるメソッド**

以下のプロパティおよびメソッドは、`liff.init()`メソッドを実行する前でも利用できます。
LIFFアプリを初期化する前にLIFFアプリを動作させている環境を取得したり、LIFFアプリ初期化に失敗した際にLIFFアプリを閉じたりできます。

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

_例_

<!-- tab start `javascript` -->

```javascript
// Promiseオブジェクトを使用する方法
liff
  .init({
    liffId: "123456-abcedfg", // Use own liffId
  })
  .then(() => {
    // Start to use liff's api
  })
  .catch((err) => {
    // Error happens during initialization
    console.log(err.code, err.message);
  });

// コールバックを使用する方法
liff.init({ liffId: "123456-abcedfg" }, successCallback, errorCallback);
```

<!-- tab end -->

#### 構文 

```javascript
liff.init(config, successCallback, errorCallback);
```

#### 引数 

<!-- parameter start (props: required) -->

config

Object

LIFFアプリの設定

<!-- parameter end -->
<!-- parameter start (props: required) -->

config.liffId

String

LIFFアプリID。LIFFアプリをチャネルに追加すると取得できます。詳しくは、「[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)」を参照してください。\
ここで指定したLIFFアプリIDは、[`liff.id`](https://developers.line.biz/ja/reference/liff/#id)で取得できます。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

config.withLoginOnExternalBrowser

Boolean

外部ブラウザでのLIFFアプリ初期化時に`liff.login()`メソッドを自動で実行するかどうかを、以下のどちらかの値で指定します。デフォルト値は`false`です。

- `true`：外部ブラウザで`liff.login()`メソッドを自動で実行します。
- `false`：外部ブラウザで`liff.login()`メソッドを自動で実行しません。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

successCallback

Function

LIFFアプリの初期化に成功したときにデータオブジェクトを返すコールバック

<!-- note start -->

**注意**

successCallbackは、戻り値の`Promise`オブジェクトのresolveと同じタイミングで処理されます。ただし、処理の順番は保証されません。

<!-- note end -->

<!-- parameter end -->
<!-- parameter start (props: optional) -->

errorCallback

Function

LIFFアプリの初期化に失敗したときにエラーオブジェクトを返すコールバック

<!-- note start -->

**注意**

errorCallbackは、戻り値の`Promise`オブジェクトのrejectと同じタイミングで処理されます。ただし、処理の順番は保証されません。

<!-- note end -->

<!-- parameter end -->

#### 戻り値 

`Promise`オブジェクトが返されます。

##### エラーレスポンス 

`Promise`がrejectされたときは、[`LiffError`](https://developers.line.biz/ja/reference/liff/#liff-errors)が渡されます。

## 動作環境の取得 

### liff.getOS() 

ユーザーがLIFFアプリを動作させている環境を取得します。

<!-- tip start -->

**LIFFアプリ初期化前でも実行できます**

このメソッドは、`liff.init()`によるLIFFアプリの初期化が終了する前でも実行できます。

<!-- tip end -->

#### 構文 

```javascript
liff.getOS();
```

#### 引数 

なし

#### 戻り値 

ユーザーがLIFFアプリを動作させている環境が、文字列で返されます。戻り値はユーザーエージェント文字列中のOS名に基づくため、返却される値はブラウザの種類（[LIFFブラウザ](https://developers.line.biz/ja/glossary/#liff-browser)、[LINE内ブラウザ](https://developers.line.biz/ja/glossary/#line-iab)、[外部ブラウザ](https://developers.line.biz/ja/glossary/#external-browser)）を問いません。

たとえば、ユーザーがiOSを使用している場合、使用しているブラウザがLIFFブラウザかSafariかは問わず、`ios` が返却されます。

| 戻り値  | 説明              |
| ------- | ----------------- |
| ios     | iOSもしくはiPadOS |
| android | Android           |
| web     | 上記以外          |

LIFFアプリをサポートするOSやブラウザについては、[動作環境](https://developers.line.biz/ja/docs/liff/overview/#operating-environment)を参照してください。

### liff.getAppLanguage() 

LIFFアプリが動作しているLINEアプリの言語設定を取得します。

<!-- tip start -->

**LIFFアプリ初期化前でも実行できます**

このメソッドは、`liff.init()`によるLIFFアプリの初期化が終了する前でも実行できます。

<!-- tip end -->

#### 使用条件 

LIFF SDKのバージョンが2.24.0以上

#### 動作条件 

`liff.getAppLanguage()`メソッドが正しく動作するには、以下の条件をすべて満たす必要があります。

- LIFFアプリが[LIFFブラウザ](https://developers.line.biz/ja/glossary/#liff-browser)上で動作している。
- LINEアプリのバージョンが14.11.0以上である。

なお、上記の条件を満たさない場合、`liff.getAppLanguage()`メソッドは[`liff.getLanguage()`](https://developers.line.biz/ja/reference/liff/#get-language)メソッドと同じ挙動になります。

#### 構文 

```javascript
liff.getAppLanguage();
```

#### 引数 

なし

#### 戻り値 

LIFFアプリが動作しているLINEアプリの言語設定が[RFC 5646](https://datatracker.ietf.org/doc/html/rfc5646)に準拠した文字列で返されます。

### liff.getLanguage() 

<!-- note start -->

**liff.getLanguage()メソッドは非推奨です**

`liff.getLanguage()`メソッドは非推奨になりました。LIFFアプリを動作させている環境の言語設定を取得するには、[`liff.getAppLanguage()`](https://developers.line.biz/ja/reference/liff/#get-app-language)メソッドを使用してください。詳しくは、[2024年7月23日のニュース](https://developers.line.biz/ja/news/2024/07/23/release-liff-2-24-0/)を参照してください。

<!-- note end -->

LIFFアプリを動作させている環境の言語設定を取得します。

<!-- tip start -->

**LIFFアプリ初期化前でも実行できます**

このメソッドは、`liff.init()`によるLIFFアプリの初期化が終了する前でも実行できます。

<!-- tip end -->

#### 構文 

```javascript
liff.getLanguage();
```

#### 引数 

なし

#### 戻り値 

LIFFアプリを動作させている環境の`navigator.language`で取得できる言語設定が、文字列で返されます。

### liff.getVersion() 

LIFF SDKのバージョンを取得します。

<!-- tip start -->

**LIFFアプリ初期化前でも実行できます**

このメソッドは、`liff.init()`によるLIFFアプリの初期化が終了する前でも実行できます。

<!-- tip end -->

#### 構文 

```javascript
liff.getVersion();
```

#### 引数 

なし

#### 戻り値 

LIFF SDKのバージョンが、文字列で返されます。

### liff.getLineVersion() 

ユーザーのLINEバージョンを取得します。

<!-- tip start -->

**LIFFアプリ初期化前でも実行できます**

このメソッドは、`liff.init()`によるLIFFアプリの初期化が終了する前でも実行できます。

<!-- tip end -->

#### 構文 

```javascript
liff.getLineVersion();
```

#### 引数 

なし

#### 戻り値 

ユーザーがLIFFブラウザでLIFFアプリを開くと、ユーザーのLINEバージョンが文字列で返されます。ユーザーが外部ブラウザでLIFFアプリを開くと、 `null`が返されます。

### liff.getContext() 

LIFFアプリが起動された画面（1対1のトーク、グループトーク、複数人トーク、または外部ブラウザ）に関する情報を取得します。

<!-- warning start -->

**トークルームの内部識別子の提供は廃止されました**

LIFFアプリに対するトークルームの内部識別子（1対1トークID、グループID、トークルームID）の提供は廃止されました。詳しくは、2023年2月6日のニュース、「[2023年2月6日をもってLIFFアプリに対するトークルームの内部識別子の提供を廃止しました](https://developers.line.biz/ja/news/2023/02/06/liff-spec-change/)」を参照してください。

<!-- warning end -->

_例_

<!-- tab start `javascript` -->

```javascript
const context = liff.getContext();
console.log(context);
```

<!-- tab end -->

#### 構文 

```javascript
liff.getContext();
```

#### 引数 

なし

#### 戻り値 

各種APIを呼び出すために必要な情報を含むデータオブジェクトが返されます。

<!-- parameter start -->

type

String

LIFFアプリが起動された画面の種類。以下のいずれかの値が含まれます。

- `utou`：1対1のトーク。
- `group`：グループトーク。
- `room`：複数人トーク。
- `external`：外部ブラウザ。
- `none`：LINEの1対1のトーク、グループ、複数人トーク、外部ブラウザ以外から起動した場合。例：ウォレットタブ

LIFF間遷移後のLIFFアプリでも、このプロパティが返ります。

<!-- parameter end -->
<!-- parameter start -->

userId

String

ユーザーID。`type`プロパティが、`utou`、`room`、`group`、`none`または`external`の場合に含まれます。ただし、`type`プロパティが`external`の場合は、nullが返されることがあります。

<!-- parameter end -->
<!-- parameter start -->

liffId

String

LIFF ID。

<!-- parameter end -->
<!-- parameter start -->

viewType

String

LIFFアプリの画面サイズ。`type`プロパティが`external`以外の場合に、以下のいずれかの値が含まれます。

- `compact`
- `tall`
- `full`

詳しくは、「[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

endpointUrl

String

LIFFアプリのエンドポイントURL。

<!-- parameter end -->
<!-- parameter start -->

accessTokenHash

String

SHA256でハッシュ化したアクセストークンの前半部分。アクセストークンの検証に使用されます。

<!-- parameter end -->
<!-- parameter start -->

availability

Object

LIFFアプリを起動した環境で、LIFFの機能が使用可能かどうかを[`availability`オブジェクト](https://developers.line.biz/ja/reference/liff/#get-context-return-value-availability)として返します。

<!-- parameter end -->
<!-- parameter start -->

scope

Array of strings

LIFF SDKの一部のメソッドを利用するために必要なスコープの中で、どのスコープを持っているかを返します。

- `openid`：[`liff.getIDToken()`](https://developers.line.biz/ja/reference/liff/#get-id-token)および[`liff.getDecodedIDToken()`](https://developers.line.biz/ja/reference/liff/#get-decoded-id-token)を使用するためのスコープ
- `email`：[`liff.getIDToken()`](https://developers.line.biz/ja/reference/liff/#get-id-token)および[`liff.getDecodedIDToken()`](https://developers.line.biz/ja/reference/liff/#get-decoded-id-token)で、メールアドレスを取得するためのスコープ
- `profile`：[`liff.getProfile()`](https://developers.line.biz/ja/reference/liff/#get-profile)および[`liff.getFriendship()`](https://developers.line.biz/ja/reference/liff/#get-friendship)を使用するためのスコープ
- `chat_message.write`：[`liff.sendMessages()`](https://developers.line.biz/ja/reference/liff/#send-messages)を使用するためのスコープ

スコープについて詳しくは、『LIFFドキュメント』の「[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/#registering-liff-app)」を参照してください。

<!-- tip start -->

**liff.getContext()メソッドとliff.permission.getGrantedAll()メソッドの違い**

`liff.getContext()`メソッドでは、LIFFアプリのスコープ（※）の一覧を取得します。

一方、[`liff.permission.getGrantedAll()`](https://developers.line.biz/ja/reference/liff/#permission-get-granted-all)メソッドでは、LIFFアプリのスコープのうち、ユーザーが権限の付与に同意したスコープの一覧を取得します。

※ LINEログインチャネルの［**LIFF**］タブにある「Scope」セクションで指定したスコープ

<!-- tip end -->

<!-- parameter end -->
<!-- parameter start -->

menuColorSetting

Object

LIFFブラウザのヘッダー部分のカラー設定を[`menuColorSetting`オブジェクト](https://developers.line.biz/ja/reference/liff/#get-context-return-value-menucolorsetting)として返します。

なお、ヘッダー部分のカラー設定の変更は、現在提供していません。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

miniAppId

String

LINEミニアプリのCustom Path機能で設定されている文字列が返されます。Custom Path機能について詳しくは、『LINEミニアプリドキュメント』の「[Custom Pathを設定する](https://developers.line.biz/ja/docs/line-mini-app/develop/custom-path/)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

miniDomainAllowed

Boolean

LINEミニアプリを`miniapp.line.me`ドメインで利用できるかどうかを返します。

<!-- parameter end -->
<!-- parameter start -->

permanentLinkPattern

String

LIFF URLの追加情報の処理方法。`concat`が返されます。

詳しくは、『LIFFドキュメント』の「[LIFFアプリを開く](https://developers.line.biz/ja/docs/liff/opening-liff-app/)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="廃止") -->

utouId

String

このプロパティは廃止されました。詳しくは、2023年2月6日のニュース、「[2023年2月6日をもってLIFFアプリに対するトークルームの内部識別子の提供を廃止しました](https://developers.line.biz/ja/news/2023/02/06/liff-spec-change/)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="廃止") -->

groupId

String

このプロパティは廃止されました。詳しくは、2023年2月6日のニュース、「[2023年2月6日をもってLIFFアプリに対するトークルームの内部識別子の提供を廃止しました](https://developers.line.biz/ja/news/2023/02/06/liff-spec-change/)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: annotation="廃止") -->

roomId

String

このプロパティは廃止されました。詳しくは、2023年2月6日のニュース、「[2023年2月6日をもってLIFFアプリに対するトークルームの内部識別子の提供を廃止しました](https://developers.line.biz/ja/news/2023/02/06/liff-spec-change/)」を参照してください。

<!-- parameter end -->

_例（LIFFブラウザの場合）_

<!-- tab start `json` -->

```json
{
  "type": "utou",
  "utouId": "e2bff570-...",
  "userId": "U850014438e...",
  "liffId": "123456-abcedfg",
  "viewType": "full",
  "endpointUrl": "https://example.com/",
  "accessTokenHash": "EVWYWo1yYA...",
  "availability": {
    "shareTargetPicker": {
      "permission": true,
      "minVer": "10.3.0"
    },
    "multipleLiffTransition": {
      "permission": true,
      "minVer": "10.18.0"
    },
    "subwindowOpen": {
      "permission": true,
      "minVer": "11.7.0"
    },
    "scanCode": {
      "permission": false,
      "minVer": "9.4.0",
      "unsupportedFromVer": "9.19.0"
    },
    "scanCodeV2": {
      "permission": true,
      "minVer": "11.7.0",
      "minOsVer": "14.3.0"
    },
    "getAdvertisingId": {
      "permission": false,
      "minVer": "7.14.0"
    },
    "addToHomeScreen": {
      "permission": false,
      "minVer": "9.16.0"
    },
    "bluetoothLeFunction": {
      "permission": false,
      "minVer": "9.14.0",
      "unsupportedFromVer": "9.19.0"
    },
    "skipChannelVerificationScreen": {
      "permission": false,
      "minVer": "11.14.0"
    },
    "addToHomeV2": {
      "permission": false,
      "minVer": "13.20.0"
    },
    "addToHomeHideDomain": {
      "permission": false,
      "minVer": "13.20.0"
    },
    "addToHomeLineScheme": {
      "permission": false,
      "minVer": "13.20.0"
    }
  },
  "scope": [
    "chat_message.write",
    "openid",
    "profile"
  ],
  "menuColorSetting": {
    "adaptableColorSchemes": [
      "light"
    ],
    "lightModeColor": {
      "iconColor": "#111111",
      "statusBarColor": "black",
      "titleTextColor": "#111111",
      "titleSubtextColor": "#B7B7B7",
      "titleButtonColor": "#111111",
      "titleBackgroundColor": "#FFFFFF",
      "progressBarColor": "#06C755",
      "progressBackgroundColor": "#FFFFFF"
    },
    "darkModeColor": {
      "iconColor": "#FFFFFF",
      "statusBarColor": "white",
      "titleTextColor": "#FFFFFF",
      "titleSubtextColor": "#949494",
      "titleButtonColor": "#FFFFFF",
      "titleBackgroundColor": "#111111",
      "progressBarColor": "#06C755",
      "progressBackgroundColor": "#111111"
    }
  },
  "miniDomainAllowed": false,
  "permanentLinkPattern": "concat"
}
```

<!-- tab end -->

_例（外部ブラウザの場合）_

<!-- tab start `json` -->

```json
{
  "type": "external",
  "liffId": "123456-abcedfg",
  "endpointUrl": "https://example.com/",
  "accessTokenHash": "EVWYWo1yYA...",
  "availability": {
    "shareTargetPicker": {
      "permission": true,
      "minVer": "10.3.0"
    },
    "multipleLiffTransition": {
      "permission": true,
      "minVer": "10.18.0"
    },
    "subwindowOpen": {
      "permission": true,
      "minVer": "11.7.0"
    },
    "scanCode": {
      "permission": true,
      "minVer": "9.4.0",
      "unsupportedFromVer": "9.19.0"
    },
    "scanCodeV2": {
      "permission": true,
      "minVer": "11.7.0",
      "minOsVer": "14.3.0"
    },
    "getAdvertisingId": {
      "permission": false,
      "minVer": "7.14.0"
    },
    "addToHomeScreen": {
      "permission": false,
      "minVer": "9.16.0"
    },
    "bluetoothLeFunction": {
      "permission": false,
      "minVer": "9.14.0",
      "unsupportedFromVer": "9.19.0"
    },
    "skipChannelVerificationScreen": {
      "permission": false,
      "minVer": "11.14.0"
    },
    "addToHomeV2": {
      "permission": false,
      "minVer": "13.20.0"
    },
    "addToHomeHideDomain": {
      "permission": false,
      "minVer": "13.20.0"
    },
    "addToHomeLineScheme": {
      "permission": false,
      "minVer": "13.20.0"
    }
  },
  "scope": [
    "chat_message.write",
    "openid",
    "profile"
  ],
  "menuColorSetting": {
    "adaptableColorSchemes": [
      "light"
    ],
    "lightModeColor": {
      "iconColor": "#111111",
      "statusBarColor": "black",
      "titleTextColor": "#111111",
      "titleSubtextColor": "#B7B7B7",
      "titleButtonColor": "#111111",
      "titleBackgroundColor": "#FFFFFF",
      "progressBarColor": "#06C755",
      "progressBackgroundColor": "#FFFFFF"
    },
    "darkModeColor": {
      "iconColor": "#FFFFFF",
      "statusBarColor": "white",
      "titleTextColor": "#FFFFFF",
      "titleSubtextColor": "#949494",
      "titleButtonColor": "#FFFFFF",
      "titleBackgroundColor": "#111111",
      "progressBarColor": "#06C755",
      "progressBackgroundColor": "#111111"
    }
  },
  "miniDomainAllowed": false,
  "permanentLinkPattern": "concat"
}
```

<!-- tab end -->

#### `availability`オブジェクト 

`availability`オブジェクトには、以下のプロパティが含まれます。

<!-- parameter start -->

shareTargetPicker

Object

LIFFアプリを起動した環境で、[`liff.shareTargetPicker()`](https://developers.line.biz/ja/reference/liff/#share-target-picker)が使用可能かどうかを[オブジェクト](https://developers.line.biz/ja/reference/liff/#get-context-return-value-availability-common)で表します。

※`liff.shareTargetPicker()`の使用可否は、このプロパティではなく、[liff.isApiAvailable('shareTargetPicker')](https://developers.line.biz/ja/reference/liff/#is-api-available)で確認することをお勧めします。

<!-- parameter end -->
<!-- parameter start -->

multipleLiffTransition

Object

LIFFアプリを起動した環境で、LIFFアプリを閉じずに[`liff.openWindow()`](https://developers.line.biz/ja/reference/liff/#open-window)で[別のLIFFアプリへ遷移する](https://developers.line.biz/ja/docs/liff/opening-liff-app/#move-liff-to-liff)ことが可能かどうかを[オブジェクト](https://developers.line.biz/ja/reference/liff/#get-context-return-value-availability-common)で表します。

※LIFF間遷移可否の情報は、このプロパティではなく、[liff.isApiAvailable('multipleLiffTransition')](https://developers.line.biz/ja/reference/liff/#is-api-available)で確認することをお勧めします。

<!-- parameter end -->
<!-- parameter start -->

subwindowOpen

Object

LIFFアプリを起動した環境で、サブウィンドウが使用可能かどうかを[オブジェクト](https://developers.line.biz/ja/reference/liff/#get-context-return-value-availability-common)で表します。

<!-- parameter end -->
<!-- parameter start -->

scanCode

Object

LIFFアプリを起動した環境で、[`liff.scanCode()`](https://developers.line.biz/ja/reference/liff/#scan-code)が使用可能かどうかを[オブジェクト](https://developers.line.biz/ja/reference/liff/#get-context-return-value-availability-common)で表します。

<!-- parameter end -->
<!-- parameter start -->

scanCodeV2

Object

LIFFアプリを起動した環境で、[`liff.scanCodeV2()`](https://developers.line.biz/ja/reference/liff/#scan-code-v2)が使用可能かどうかを[オブジェクト](https://developers.line.biz/ja/reference/liff/#get-context-return-value-availability-common)で表します。

<!-- parameter end -->
<!-- parameter start -->

getAdvertisingId

Object

LIFFアプリを起動した環境で、`liff.getAid()`が使用可能かどうかを[オブジェクト](https://developers.line.biz/ja/reference/liff/#get-context-return-value-availability-common)で表します。

なお、`liff.getAid()`は現在提供していません。

<!-- parameter end -->
<!-- parameter start -->

addToHomeScreen

String

LIFFアプリを起動した環境で、`liff.addToHomeScreen()`が使用可能かどうかを[オブジェクト](https://developers.line.biz/ja/reference/liff/#get-context-return-value-availability-common)で表します。

なお、`liff.addToHomeScreen()`は現在提供していません。

<!-- parameter end -->
<!-- parameter start -->

bluetoothLeFunction

Object

LIFFアプリを起動した環境で、LINE ThingsのためのBluetooth® Low Energyが使用可能かどうかを[オブジェクト](https://developers.line.biz/ja/reference/liff/#get-context-return-value-availability-common)で表します。

なお、この機能は現在提供していません。

<!-- parameter end -->
<!-- parameter start -->

skipChannelVerificationScreen

Object

LIFFアプリを起動した環境で、「チャネル同意の簡略化」機能を利用できるかどうかを[オブジェクト](https://developers.line.biz/ja/reference/liff/#get-context-return-value-availability-common)で表します。詳しくは、『LINEミニアプリドキュメント』の「[同意画面のプロセスをスキップする](https://developers.line.biz/ja/docs/line-mini-app/develop/channel-consent-simplification/)」を参照してください。

<!-- parameter end -->
<!-- parameter start -->

addToHomeV2

Object

LIFFアプリを起動した環境で、[`liff.createShortcutOnHomeScreen()`](https://developers.line.biz/ja/reference/liff/#create-shortcut-on-home-screen)が使用可能かどうかを[オブジェクト](https://developers.line.biz/ja/reference/liff/#get-context-return-value-availability-common)で表します。

※`liff.createShortcutOnHomeScreen()`の使用可否は、このプロパティではなく、[liff.isApiAvailable('createShortcutOnHomeScreen')](https://developers.line.biz/ja/reference/liff/#is-api-available)で確認することをお勧めします。

<!-- parameter end -->
<!-- parameter start -->

addToHomeHideDomain

Object

ショートカットを、ユーザー端末のホーム画面に追加する画面を表示する際に、エンドポイントURLを非表示にできるかどうかを[オブジェクト](https://developers.line.biz/ja/reference/liff/#get-context-return-value-availability-common)で表します。

なお、この機能は現在提供していません。

<!-- parameter end -->
<!-- parameter start -->

addToHomeLineScheme

Object

[LINE URLスキーム](https://developers.line.biz/ja/docs/line-login/using-line-url-scheme/)を指定したショートカットが作成可能かどうかを[オブジェクト](https://developers.line.biz/ja/reference/liff/#get-context-return-value-availability-common)で表します。

なお、この機能は現在提供していません。

<!-- parameter end -->

_例_

<!-- tab start `json` -->

```json
{
  "shareTargetPicker": {
    "permission": true,
    "minVer": "10.3.0"
  }
}
```

<!-- tab end -->

#### `availability`オブジェクトの共通プロパティ 

<!-- parameter start -->

permission

Boolean

LIFFアプリを起動した環境で、`availability`オブジェクトのプロパティ名で指定された機能が、使用可能かどうかを表します。

- `true`：機能は使用可能。
- `false`：機能は使用不可。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

minVer

String

該当する機能がサポートされているLINEの最小バージョン

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

maxVer

String

該当する機能がサポートされているLINEの最大バージョン

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

unsupportedFromVer

String

該当する機能がサポート対象外となったLINEのバージョン

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

minOsVer

String

該当する機能がサポートされているOSの最小バージョン

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

maxOsVer

String

該当する機能がサポートされているOSの最大バージョン

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

unsupportedFromOsVer

String

該当する機能がサポート対象外となったOSのバージョン

<!-- parameter end -->

#### `menuColorSetting`オブジェクト 

`menuColorSetting`オブジェクトには、以下のプロパティが含まれます。

<!-- parameter start -->

adaptableColorSchemes

Array of strings

常に`light`を返します。

<!-- parameter end -->
<!-- parameter start -->

lightModeColor

Object

`adaptableColorSchemes`が`light`だった場合の、カラー設定を[オブジェクト](https://developers.line.biz/ja/reference/liff/#get-context-return-value-menucolorsetting-common)で表します。

<!-- parameter end -->
<!-- parameter start -->

darkModeColor

Object

`adaptableColorSchemes`が`dark`だった場合の、ヘッダーのカラー設定を[オブジェクト](https://developers.line.biz/ja/reference/liff/#get-context-return-value-menucolorsetting-common)で表します。

なお、このヘッダーのカラー設定は現在提供していません。

<!-- parameter end -->

_例_

<!-- tab start `json` -->

```json
{
  "adaptableColorSchemes": [
    "light"
  ],
  "lightModeColor": {
    "iconColor": "#111111",
    "statusBarColor": "black",
    "titleTextColor": "#111111",
    "titleSubtextColor": "#B7B7B7",
    "titleButtonColor": "#111111",
    "titleBackgroundColor": "#FFFFFF",
    "progressBarColor": "#06C755",
    "progressBackgroundColor": "#FFFFFF"
  },
  "darkModeColor": {
    "iconColor": "#FFFFFF",
    "statusBarColor": "white",
    "titleTextColor": "#FFFFFF",
    "titleSubtextColor": "#949494",
    "titleButtonColor": "#FFFFFF",
    "titleBackgroundColor": "#111111",
    "progressBarColor": "#06C755",
    "progressBackgroundColor": "#111111"
  }
}
```

<!-- tab end -->

#### `menuColorSetting`オブジェクトの共通プロパティ 

<!-- parameter start -->

iconColor

String

ヘッダーのアイコンの色を`#RRGGBB`のような16進数カラーコードで表します。

<!-- parameter end -->
<!-- parameter start -->

statusBarColor

String

常に`white`を返します。

<!-- parameter end -->
<!-- parameter start -->

titleTextColor

String

ヘッダーのタイトルテキストの色を`#RRGGBB`のような16進数カラーコードで表します。

<!-- parameter end -->
<!-- parameter start -->

titleSubtextColor

String

ヘッダーのサブタイトルテキストの色を`#RRGGBB`のような16進数カラーコードで表します。

<!-- parameter end -->
<!-- parameter start -->

titleButtonColor

String

ヘッダーのボタンの色を`#RRGGBB`のような16進数カラーコードで表します。

<!-- parameter end -->
<!-- parameter start -->

titleBackgroundColor

String

ヘッダーの背景色を`#RRGGBB`のような16進数カラーコードで表します。

<!-- parameter end -->
<!-- parameter start -->

progressBarColor

String

ヘッダーのプログレスバーの色を`#RRGGBB`のような16進数カラーコードで表します。

<!-- parameter end -->
<!-- parameter start -->

progressBackgroundColor

String

ヘッダーのプログレスバーの背景色を`#RRGGBB`のような16進数カラーコードで表します。

<!-- parameter end -->

### liff.isInClient() 

LIFFアプリをLIFFブラウザで動作させているかどうかを取得します。

<!-- tip start -->

**LIFFアプリ初期化前でも実行できます**

このメソッドは、`liff.init()`によるLIFFアプリの初期化が終了する前でも実行できます。

<!-- tip end -->

#### 構文 

```javascript
liff.isInClient();
```

#### 引数 

なし

#### 戻り値 

- `true`：[LIFFブラウザ](https://developers.line.biz/ja/glossary/#liff-browser)で動作させている
- `false`：[外部ブラウザ](https://developers.line.biz/ja/glossary/#external-browser)または[LINE内ブラウザ](https://developers.line.biz/ja/glossary/#line-iab)で動作させている

### liff.isLoggedIn() 

ユーザーがログインしているかどうかを取得します。

_例_

<!-- tab start `javascript` -->

```javascript
if (liff.isLoggedIn()) {
  // `liff.getProfile()`のような、アクセストークンが必要なAPIを使用できます。
}
```

<!-- tab end -->

#### 構文 

```javascript
liff.isLoggedIn();
```

#### 引数 

なし

#### 戻り値 

- `true`：ログインしている
- `false`：ログインしていない

### liff.isApiAvailable() 

指定したAPIや機能が、LIFFアプリを起動した環境で使用可能かどうかを確認します。たとえば、APIが対応しているLINEバージョンであることや、APIを呼び出すために特別な同意が必要な場合は同意していることを確認します。

_例_

<!-- tab start `javascript` -->

```javascript
// Check if shareTargetPicker is available
if (liff.isApiAvailable('shareTargetPicker')) {
  liff.shareTargetPicker([
    {
      type: "text",
      text: "Hello, World!"
    }
  ])
    .then(
      console.log("ShareTargetPicker was launched")
    ).catch(function(res) {
      console.log("Failed to launch ShareTargetPicker")
    })
}

// Check if the LIFF-to-LIFF transition is available
if (liff.isApiAvailable('multipleLiffTransition')) {
  window.location.href = "https://line.me/{liffId}", // URL for another LIFF app
}
```

<!-- tab end -->

#### 構文 

```javascript
liff.isApiAvailable(apiName);
```

#### 引数 

<!-- parameter start (props: required) -->

apiName

String

LIFFのクライアントAPIや機能の名前。次のいずれかを指定できます。

- `createShortcutOnHomeScreen`：[`liff.createShortcutOnHomeScreen()`](https://developers.line.biz/ja/reference/liff/#create-shortcut-on-home-screen)メソッドが利用可能かどうか
- `scanCodeV2`：[`liff.scanCodeV2()`](https://developers.line.biz/ja/reference/liff/#scan-code-v2)メソッドが利用可能かどうか
- `scanCode`：[`liff.scanCode()`](https://developers.line.biz/ja/reference/liff/#scan-code)メソッドが利用可能かどうか
- `shareTargetPicker`：[`liff.shareTargetPicker()`](https://developers.line.biz/ja/reference/liff/#share-target-picker)メソッドが利用可能かどうか
- `iap`：LINEミニアプリの[アプリ内課金](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/overview/)機能が利用可能かどうか
- `multipleLiffTransition`：[LIFF間遷移](https://developers.line.biz/ja/docs/liff/opening-liff-app/#move-liff-to-liff)が利用可能かどうか
- `skipChannelVerificationScreen`：LINEミニアプリの「[チャネル同意の簡略化](https://developers.line.biz/ja/docs/line-mini-app/develop/channel-consent-simplification/#what-is-channel-consent-simplification)」機能が利用可能かどうか

<!-- parameter end -->

#### 戻り値 

指定したAPIや機能が、現在の環境で使用可能かどうかが返されます。使用可能の場合は`true`が返されます。使用不可能の場合は`false`が返されます。`false`が返される例は以下のとおりです。

- APIが対応していないLINEバージョンでLIFFアプリを起動した場合
- 外部ブラウザで利用できないAPIにもかかわらず、外部ブラウザでLIFFアプリを起動した場合
- 使用するために特別な同意が必要なAPIにもかかわらず、同意していない場合
- 使用するためにログインが必要なAPIにもかかわらず、ログインしていない場合
- 使用するためにアクセストークンが必要なAPIにもかかわらず、アクセストークンの有効期限が切れている場合

## 認証 

### liff.login() 

[外部ブラウザ](https://developers.line.biz/ja/glossary/#external-browser)および[LINE内ブラウザ](https://developers.line.biz/ja/glossary/#line-iab)上で、ログイン処理を行います。

<!-- note start -->

**注意**

LIFFブラウザの場合、`liff.init()`実行時に自動でログイン処理が実行されるため、`liff.login()`は利用できません。

<!-- note end -->

<!-- note start -->

**LIFFブラウザ内での認可リクエストについて**

LIFFブラウザ内でLINEログインによる認可リクエストを行った際の動作は保証されません。また、LIFFアプリを外部ブラウザやLINE内ブラウザで開く場合には、必ず本メソッドでログイン処理を行い、[LINEログインによる認可リクエスト](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#making-an-authorization-request)は行わないでください。

<!-- note end -->

_例_

<!-- tab start `javascript` -->

```javascript
if (!liff.isLoggedIn()) {
  liff.login({ redirectUri: "https://example.com/path" });
}
```

<!-- tab end -->

#### 構文 

```javascript
liff.login(loginConfig);
```

#### 引数 

<!-- parameter start (props: optional) -->

loginConfig

Object

ログインの設定

<!-- parameter end -->
<!-- parameter start (props: optional) -->

loginConfig.redirectUri

String

ログイン後にLIFFアプリで表示するURL。デフォルト値は［**エンドポイントURL**］に設定したURLです。［**エンドポイントURL**］の設定方法について詳しくは、『LIFFドキュメント』の「[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/#registering-liff-app)」を参照してください。

`redirectUri`に指定したURLが［**エンドポイントURL**］に設定したURLで始まらない場合、ログイン処理に失敗し、エラー画面が表示されます。

![](https://developers.line.biz/media/liff/liff_login_error_screen.png)

たとえば、［**エンドポイントURL**］が`https://example.com/path1/path2?query1=value1`の場合、ログイン処理の成否は以下のとおりです。なお、クエリパラメータやURLフラグメントはログイン処理の成否に影響しません。

<table>
  <thead>
    <tr>
      <th>redirectUri</th>
      <th>ログイン処理</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <ul>
          <li>https://example.com/path1/path2?query1=value1</li>
          <li>https://example.com/path1/path2?query2=value2</li>
          <li>https://example.com/path1/path2#URL-fragment</li>
          <li>https://example.com/path1/path2</li>
          <li>https://example.com/path1/path2/</li>
          <li>https://example.com/path1/path2/path3</li>
        </ul>
      </td>
      <td>✅ 成功</td>
    </tr>
    <tr>
      <td>
        <ul>
          <li>https://example.com/path1</li>
          <li>https://example.com/</li>
          <li>https://example.com/path2/path1</li>
        </ul>
      </td>
      <td>❌ 失敗</td>
    </tr>
  </tbody>
</table>

<!-- parameter end -->

#### 戻り値 

なし

### liff.logout() 

ログアウトします。

_例_

<!-- tab start `javascript` -->

```javascript
if (liff.isLoggedIn()) {
  liff.logout();
}
```

<!-- tab end -->

#### 構文 

```javascript
liff.logout();
```

#### 引数 

なし

#### 戻り値 

なし

### liff.getAccessToken() 

LIFF SDKが取得した「現在のユーザーのアクセストークン」を取得します。

LIFFアプリからサーバーにユーザー情報を送信するときに、このAPIで取得したアクセストークンを利用できます。サーバーでユーザー情報を使用する方法について詳しくは、『LIFFドキュメント』の「[LIFFアプリおよびサーバーでユーザー情報を使用する](https://developers.line.biz/ja/docs/liff/using-user-profile/)」を参照してください。

<!-- note start -->

**アクセストークンの有効期間**

アクセストークンの有効期間は、発行後12時間です。なお、ユーザーがLIFFアプリを閉じると、有効期限が切れていなくてもアクセストークンが無効化される場合があります。詳しくは、『LIFFドキュメント』の「[LIFFアプリを閉じたときの挙動](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#behavior-when-closing-liff-app)」を参照してください。

<!-- note end -->

<!-- tip start -->

**LIFF SDKがアクセストークンを取得するタイミング**

- LIFFブラウザでLIFFアプリを起動した場合は、[`liff.init()`](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)を呼び出したときに、LIFF SDKがアクセストークンを取得します。
- 外部ブラウザでLIFFアプリを起動した場合は、以下の手順を行ったのちに、LIFF SDKがアクセストークンを取得します。
  1. LIFFアプリで、[`liff.login()`](https://developers.line.biz/ja/reference/liff/#login)を呼び出す。
  2. ユーザーがログインする。
  3. LIFFアプリで、再度[`liff.init()`](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)を呼び出す。

<!-- tip end -->

_例_

<!-- tab start `javascript` -->

```javascript
const accessToken = liff.getAccessToken();
if (accessToken) {
  fetch("https://api...", {
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${accessToken}`,
    },
    //...
  });
}
```

<!-- tab end -->

#### 構文 

```javascript
liff.getAccessToken();
```

#### 引数 

なし

#### 戻り値 

現在のユーザーのアクセストークンを文字列で返します。

### liff.getIDToken() 

LIFF SDKが取得した「現在のユーザーのIDトークン」を取得します。IDトークンは、ユーザー情報を含むJSONウェブトークン（JWT）です。

LIFFアプリからサーバーにユーザー情報を送信するときに、このAPIで取得したIDトークンを利用できます。サーバーでユーザー情報を使用する方法について詳しくは、『LIFFドキュメント』の「[LIFFアプリおよびサーバーでユーザー情報を使用する](https://developers.line.biz/ja/docs/liff/using-user-profile/)」を参照してください。

<!-- note start -->

**スコープを選択してください**

[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)ときに、`openid`スコープを選択してください。スコープを選択しなかった場合やユーザーが認可しなかった場合は、IDトークンを取得できません。スコープの選択は、LIFFアプリ追加後も[LINE Developersコンソール](https://developers.line.biz/console/)のLIFFタブで変更できます。

<!-- note end -->

<!-- tip start -->

**LIFF SDKがIDトークンを取得するタイミング**

- LIFFブラウザでLIFFアプリを起動した場合は、[`liff.init()`](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)を呼び出したときに、LIFF SDKがIDトークンを取得します。
- 外部ブラウザでLIFFアプリを起動した場合は、以下の手順を行ったのちに、LIFF SDKがIDトークンを取得します。

  1. LIFFアプリで、[`liff.login()`](https://developers.line.biz/ja/reference/liff/#login)を呼び出す。
  2. ユーザーがログインする。
  3. LIFFアプリで、再度[`liff.init()`](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)を呼び出す。

<!-- tip end -->

<!-- tip start -->

**メールアドレスを取得できます**

[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)ときに、`email`スコープを選択し、ユーザーが認可すると、メールアドレスも取得できます。スコープの選択は、LIFFアプリ追加後も[LINE Developersコンソール](https://developers.line.biz/console/)のLIFFタブで変更できます。

<!-- tip end -->

_例_

<!-- tab start `javascript` -->

```javascript
liff
  .init({
    liffId: "123456-abcedfg", // Use own liffId
  })
  .then(() => {
    const idToken = liff.getIDToken();
    console.log(idToken); // print idToken object
  });
```

<!-- tab end -->

#### 構文 

```javascript
liff.getIDToken();
```

#### 引数 

なし

#### 戻り値 

IDトークンが返されます。

### liff.getDecodedIDToken() 

LIFF SDKが取得したIDトークンの「ペイロード」を取得します。ペイロードには、ユーザーの表示名、プロフィール画像のURL、メールアドレスなどの情報が含まれます。

LIFFアプリでユーザーの表示名などを利用する場合に、このメソッドを利用してください。

なお取得できる情報はメインプロフィールのみです。ユーザーの[サブプロフィール](https://developers.line.biz/ja/glossary/#subprofile)は取得できません。

<!-- warning start -->

**ユーザー情報をサーバーに送信しないでください**

このメソッドで取得したユーザー情報をサーバーに送信しないでください。サーバーでユーザー情報を使用する方法について詳しくは、『LIFFドキュメント』の「[LIFFアプリおよびサーバーでユーザー情報を使用する](https://developers.line.biz/ja/docs/liff/using-user-profile/)」を参照してください。

<!-- warning end -->

<!-- note start -->

**スコープを選択してください**

[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)ときに、`openid`スコープを選択してください。スコープを選択しなかった場合やユーザーが認可しなかった場合は、IDトークンを取得できません。スコープの選択は、LIFFアプリ追加後も[LINE Developersコンソール](https://developers.line.biz/console/)のLIFFタブで変更できます。

<!-- note end -->

<!-- tip start -->

**LIFF SDKがIDトークンを取得するタイミング**

- LIFFブラウザでLIFFアプリを起動した場合は、[`liff.init()`](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)を呼び出したときに、LIFF SDKがIDトークンを取得します。
- 外部ブラウザでLIFFアプリを起動した場合は、以下の手順を行ったのちに、LIFF SDKがIDトークンを取得します。

  1. LIFFアプリで、[`liff.login()`](https://developers.line.biz/ja/reference/liff/#login)を呼び出す。
  2. ユーザーがログインする。
  3. LIFFアプリで、再度[`liff.init()`](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)を呼び出す。

<!-- tip end -->

<!-- tip start -->

**メールアドレスを取得できます**

[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)ときに、`email`スコープを選択し、ユーザーが認可すると、メールアドレスも取得できます。スコープの選択は、LIFFアプリ追加後も[LINE Developersコンソール](https://developers.line.biz/console/)のLIFFタブで変更できます。

<!-- tip end -->

_例_

<!-- tab start `javascript` -->

```javascript
liff
  .init({
    liffId: "123456-abcedfg", // Use own liffId
  })
  .then(() => {
    const idToken = liff.getDecodedIDToken();
    console.log(idToken); // print decoded idToken object
  });
```

<!-- tab end -->

#### 構文 

```javascript
liff.getDecodedIDToken();
```

#### 引数 

なし

#### 戻り値 

IDトークンのペイロードが返されます。

IDトークンのペイロードについて詳しくは、「[IDトークンからプロフィール情報を取得する](https://developers.line.biz/ja/docs/line-login/verify-id-token/)」の「ペイロード」を参照してください。

_例_

<!-- tab start `json` -->

```json
{
  "iss": "https://access.line.me",
  "sub": "U1234567890abcdef1234567890abcdef ",
  "aud": "1234567890",
  "exp": 1504169092,
  "iat": 1504263657,
  "amr": ["pwd"],
  "name": "Taro Line",
  "picture": "https://sample_line.me/aBcdefg123456"
}
```

<!-- tab end -->

### liff.permission.getGrantedAll() 

ユーザーが権限の付与に同意したスコープの一覧を取得します。

このメソッドで取得できるスコープは次のとおりです。

- [`profile`](https://developers.line.biz/ja/docs/liff/registering-liff-apps/#registering-liff-app)
- [`chat_message.write`](https://developers.line.biz/ja/docs/liff/registering-liff-apps/#registering-liff-app)
- [`openid`](https://developers.line.biz/ja/docs/liff/registering-liff-apps/#registering-liff-app)
- [`email`](https://developers.line.biz/ja/docs/liff/registering-liff-apps/#registering-liff-app)

<!-- tip start -->

**liff.getContext()メソッドとliff.permission.getGrantedAll()メソッドの違い**

[`liff.getContext()`](https://developers.line.biz/ja/reference/liff/#get-context)メソッドでは、LIFFアプリのスコープ（※）の一覧を取得します。

一方、`liff.permission.getGrantedAll()`メソッドでは、LIFFアプリのスコープのうち、ユーザーが権限の付与に同意したスコープの一覧を取得します。

※ LINEログインチャネルの［**LIFF**］タブにある「Scope」セクションで指定したスコープ

<!-- tip end -->

_例_

<!-- tab start `javascript` -->

```javascript
liff.permission.getGrantedAll().then((scopes) => {
  // ["profile", "chat_message.write", "openid", "email"]
  console.log(scopes);
});
```

<!-- tab end -->

#### 構文 

```javascript
liff.permission.getGrantedAll();
```

#### 引数 

なし

#### 戻り値 

`Promise`がresolveされると、ユーザーが権限の付与に同意したスコープの配列が渡されます。

##### エラーレスポンス 

`Promise`がrejectされたときは、[`LiffError`](https://developers.line.biz/ja/reference/liff/#liff-errors)が渡されます。

### liff.permission.query() 

ユーザーが指定した権限の付与に同意しているかどうかを確認します。

_例_

<!-- tab start `javascript` -->

```javascript
liff.permission.query("profile").then((permissionStatus) => {
  // permissionStatus = { state: 'granted' }
});
```

<!-- tab end -->

#### 構文 

```javascript
liff.permission.query(permission);
```

#### 引数 

<!-- parameter start (props: required) -->

permission

String

確認対象の権限。以下のいずれかのスコープを指定します。

- [`profile`](https://developers.line.biz/ja/docs/liff/registering-liff-apps/#registering-liff-app)
- [`chat_message.write`](https://developers.line.biz/ja/docs/liff/registering-liff-apps/#registering-liff-app)
- [`openid`](https://developers.line.biz/ja/docs/liff/registering-liff-apps/#registering-liff-app)
- [`email`](https://developers.line.biz/ja/docs/liff/registering-liff-apps/#registering-liff-app)

<!-- parameter end -->

#### 戻り値 

`Promise`オブジェクトが返されます。

`Promise`がresolveされると、以下のプロパティを持つオブジェクトが渡されます。

<!-- parameter start -->

state

String

以下のいずれかの値が含まれます。

- `granted`: 権限付与にユーザーが同意済み。
- `prompt`: 権限付与にユーザーが未同意。
- `unavailable`: 指定したスコープをチャネルが持たないため、利用不可。

<!-- parameter end -->

### liff.permission.requestAll() 

LINEミニアプリが要求する権限の「アクセス許可要求画面」を表示します。

![アクセス許可要求画面](https://developers.line.biz/media/line-mini-app/verification-screen-ja.png)

<!-- note start -->

**liff.permission.requestAll()の動作環境**

`liff.permission.requestAll()`は[LINEミニアプリ](https://developers.line.biz/ja/docs/line-mini-app/)でのみ動作します。

このメソッドを実行するには、あらかじめ[LINE Developersコンソール](https://developers.line.biz/console/)で、［**チャネル同意の簡略化**］をオンにする必要があります。チャネル同意の簡略化の設定方法について詳しくは、『LINEミニアプリドキュメント』の「[「チャネル同意の簡略化」の設定方法](https://developers.line.biz/ja/docs/line-mini-app/develop/channel-consent-simplification/#simplification-feature-setup)」を参照してください。

<!-- note end -->

<!-- note start -->

**ユーザーが未同意の権限があるかどうか確認してから実行してください**

権限付与にユーザーがすべて同意済みの場合、`liff.permission.requestAll()`を実行すると、`Promise`がrejectされ、[`LiffError`](https://developers.line.biz/ja/reference/liff/#liff-errors)が渡されます。そのため、[`liff.permission.query()`](https://developers.line.biz/ja/reference/liff/#permission-query)を使って、ユーザーが未同意の権限があるかどうかを確認してください。未同意の権限がある場合にのみ、`liff.permission.requestAll()`を実行するようにしてください。

<!-- note end -->

_例_

<!-- tab start `javascript` -->

```javascript
liff.permission.query("profile").then((permissionStatus) => {
  if (permissionStatus.state === "prompt") {
    liff.permission.requestAll();
  }
});
```

<!-- tab end -->

#### 構文 

```javascript
liff.permission.requestAll();
```

#### 引数 

なし

#### 戻り値 

`Promise`オブジェクトが返されます。

##### エラーレスポンス 

［**チャネル同意の簡略化**］がオンになっていない場合や、権限付与にユーザーがすべて同意済みの場合は、`Promise`がrejectされ、[`LiffError`](https://developers.line.biz/ja/reference/liff/#liff-errors)が渡されます。

## プロフィール 

### liff.getProfile() 

現在のユーザーの[プロフィール情報](https://developers.line.biz/ja/glossary/#profile-information)を取得します。

なお取得できる情報はメインプロフィールのみです。ユーザーの[サブプロフィール](https://developers.line.biz/ja/glossary/#subprofile)は取得できません。

<!-- warning start -->

**ユーザー情報をサーバーに送信しないでください**

このメソッドで取得したユーザー情報をサーバーに送信しないでください。サーバーでユーザー情報を使用する方法について詳しくは、『LIFFドキュメント』の「[LIFFアプリおよびサーバーでユーザー情報を使用する](https://developers.line.biz/ja/docs/liff/using-user-profile/)」を参照してください。

<!-- warning end -->

<!-- note start -->

**スコープを選択してください**

[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)ときに、`profile`スコープを選択してください。スコープを選択しなかった場合やユーザーが認可しなかった場合は、プロフィール情報を取得できません。スコープの選択は、LIFFアプリ追加後も[LINE Developersコンソール](https://developers.line.biz/console/)のLIFFタブで変更できます。

<!-- note end -->

_例_

<!-- tab start `javascript` -->

```javascript
liff
  .getProfile()
  .then((profile) => {
    const name = profile.displayName;
  })
  .catch((err) => {
    console.log("error", err);
  });
```

<!-- tab end -->

#### 構文 

```javascript
liff.getProfile();
```

#### 引数 

なし

#### 戻り値 

`Promise`オブジェクトが返されます。

`Promise`がresolveされると、ユーザーのプロフィール情報を含むオブジェクトが渡されます。

<!-- parameter start -->

userId

String

ユーザーID

<!-- parameter end -->
<!-- parameter start -->

displayName

String

表示名

<!-- parameter end -->
<!-- parameter start -->

pictureUrl

String

画像のURL。ユーザーが設定していない場合は返されません。

<!-- parameter end -->
<!-- parameter start -->

statusMessage

String

ステータスメッセージ。ユーザーが設定していない場合は返されません。

<!-- parameter end -->

##### エラーレスポンス 

`Promise`がrejectされたときは、[`LiffError`](https://developers.line.biz/ja/reference/liff/#liff-errors)が渡されます。

_例_

<!-- tab start `json` -->

```json
{
  "userId": "U4af4980629...",
  "displayName": "Brown",
  "pictureUrl": "https://profile.line-scdn.net/abcdefghijklmn",
  "statusMessage": "Hello, LINE!"
}
```

<!-- tab end -->

### liff.getFriendship() 

ユーザーとLINE公式アカウントの友だち関係を取得します。

ただし、LIFFアプリが追加されているLINEログインのチャネルに、LINE公式アカウントがリンクされている場合に、そのLINE公式アカウントとの友だち関係のみを取得できます。LINEログインのチャネルに、LINE公式アカウントをリンクする方法については、『LINEログインドキュメント』の「[LINEログインしたときにLINE公式アカウントを友だち追加する（友だち追加オプション）](https://developers.line.biz/ja/docs/line-login/link-a-bot/)」を参照してください。

<!-- note start -->

**スコープを選択してください**

[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)ときに、`profile`スコープを選択してください。スコープを選択しなかった場合やユーザーが認可しなかった場合は、友だち関係を取得できません。スコープの選択は、LIFFアプリ追加後も[LINE Developersコンソール](https://developers.line.biz/console/)のLIFFタブで変更できます。

<!-- note end -->

_例_

<!-- tab start `javascript` -->

```javascript
liff.getFriendship().then((data) => {
  if (data.friendFlag) {
    // something you want to do
  }
});
```

<!-- tab end -->

#### 構文 

```javascript
liff.getFriendship();
```

#### 引数 

なし

#### 戻り値 

`Promise`オブジェクトが返されます。

友だち関係を取得できると、`Promise`がresolveされ、友だち関係に関する情報が渡されます。

<!-- parameter start -->

friendFlag

Boolean

- `true`：ユーザーがLINE公式アカウントを友だち追加済みで、ブロックしていない。
- `false`：それ以外の場合。

<!-- parameter end -->

##### エラーレスポンス 

`Promise`がrejectされたときは、[`LiffError`](https://developers.line.biz/ja/reference/liff/#liff-errors)が渡されます。

_例_

<!-- tab start `json` -->

```json
{
  "friendFlag": true
}
```

<!-- tab end -->

### liff.requestFriendship() 

LINE公式アカウントの友だち追加、またはブロック解除を促すサブウィンドウを表示します。

![](https://developers.line.biz/media/liff/request-friendship/request-friendship-add-friend-ja.png)

- LINE公式アカウントと友だちになっていない場合は、友だち追加を促すサブウィンドウが表示されます。
- LINE公式アカウントをブロックしている場合は、ブロック解除を促すサブウィンドウが表示されます。
- LINE公式アカウントと既に友だちになっている場合は、サブウィンドウが表示された後、自動で閉じられます。

友だち追加、またはブロック解除を促すLINE公式アカウントは、[チャネルにLINE公式アカウントをリンクする](https://developers.line.biz/ja/docs/line-login/link-a-bot/#link-a-line-official-account)ことで指定できます。詳しくは、『LINEログインドキュメント』の「[LINEログインしたときにLINE公式アカウントを友だち追加する（友だち追加オプション）](https://developers.line.biz/ja/docs/line-login/link-a-bot/)」を参照してください。

LIFFブラウザの画面サイズが`Full`の場合のみ利用できます。詳しくは、『LIFFドキュメント』の「[LIFFブラウザの画面サイズ](https://developers.line.biz/ja/docs/liff/overview/#screen-size)」を参照してください。

_例_

<!-- tab start `javascript` -->

```javascript
try {
  await liff.requestFriendship();
} catch (error) {
  console.log(error);
}
```

<!-- tab end -->

#### 構文 

```javascript
liff.requestFriendship();
```

#### 引数 

なし

#### 戻り値 

`Promise`オブジェクトが返されます。

<!-- note start -->

**ユーザーの操作結果は戻り値では確認できません**

ユーザーによって友だち追加やブロック解除が行われたかは、戻り値では確認できません。`liff.requestFriendship()`メソッドを実行後の友だち関係については、[`liff.getFriendship()`](https://developers.line.biz/ja/reference/liff/#get-friendship)メソッドで確認してください。

<!-- note end -->

##### エラーレスポンス 

`Promise`がrejectされたときは、[`LiffError`](https://developers.line.biz/ja/reference/liff/#liff-errors)が渡されます。

友だち追加オプションの［**リンクされたLINE公式アカウント**］が未設定の場合や、LIFFアプリの画面サイズが`Full`でない場合、エラーコード`FORBIDDEN`が返ります。

## ウィンドウ 

### liff.openWindow() 

指定したURLをLINE内ブラウザまたは外部ブラウザで開きます。

<!-- note start -->

**liff.openWindow()の動作環境**

`liff.openWindow()`の外部ブラウザでの利用は、保証対象外です。

<!-- note end -->

_例_

<!-- tab start `javascript` -->

```javascript
liff.openWindow({
  url: "https://line.me",
  external: true,
});
```

<!-- tab end -->

#### LINEバージョンごとの挙動の違い 

`liff.openWindow()`メソッドで[ユニバーサルリンク](https://developer.apple.com/documentation/xcode/allowing-apps-and-websites-to-link-to-your-content/)や[アプリリンク](https://developer.android.com/training/app-links)が有効なURLを開いた場合、LINEバージョンと[`params.external`](https://developers.line.biz/ja/reference/liff/#open-window-arguments)パラメータの設定によって挙動が異なります。挙動の違いは以下のとおりです。

|  | `params.external`が`false`<br>（デフォルト値） | `params.external`が`true` |
| --- | --- | --- |
| LINE 14.20.0未満（※） | <ul><li>iOSの場合：LINE内ブラウザでURLを開く</li><li>Androidの場合：URLに対応するアプリに遷移 </li></ul> | <ul><li>iOSの場合：URLに対応するアプリに遷移</li><li>Androidの場合：デフォルトブラウザでURLを開く</li></ul> |
| LINE 14.20.0以上15.20.0未満 | URLに対応するアプリに遷移 | URLに対応するアプリに遷移 |
| LINE 15.20.0以上 | LINE内ブラウザでURLを開く| URLに対応するアプリに遷移 |

※ LINEバージョン14.20.0以降はOSによる挙動の違いはありません。

#### 構文 

```javascript
liff.openWindow(params);
```

#### 引数 

<!-- parameter start (props: required) -->

params

Object

パラメータオブジェクト

<!-- parameter end -->
<!-- parameter start (props: required) -->

params.url

String

URL。完全なURLで指定します。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

params.external

Boolean

指定したURLを外部ブラウザで開くかどうかを、以下のどちらかの値で指定します。デフォルト値は`false`です。

- `true`：外部ブラウザで開きます。
- `false`：LINE内ブラウザで開きます。

<!-- parameter end -->

#### 戻り値 

なし

### liff.closeWindow() 

LIFFアプリを閉じます。

LIFFアプリを閉じたときの挙動は、LINEアプリのバージョンやLIFFアプリの設定によって異なります。詳しくは、『LIFFドキュメント』の「[LIFFアプリを閉じたときの挙動](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#behavior-when-closing-liff-app)」を参照してください。

<!-- tip start -->

**LIFFアプリ初期化前でも実行できます**

このメソッドは、LIFF SDKバージョンが2.4.0以上の場合のみ、`liff.init()`によるLIFFアプリの初期化が終了する前でも実行できます。

<!-- tip end -->

<!-- note start -->

**注意**

`liff.closeWindow()`の外部ブラウザでの動作は、保証対象外です。

<!-- note end -->

_例_

<!-- tab start `javascript` -->

```javascript
liff.closeWindow();
```

<!-- tab end -->

#### 構文 

```javascript
liff.closeWindow();
```

#### 引数 

なし

#### 戻り値 

なし

## メッセージ 

### liff.sendMessages() 

ユーザーの代わりに、LIFFアプリが開かれているトークルームにメッセージを送信します。

この機能を利用するには、以下の条件を満たす必要があります。

- 1対1のトーク、[グループトーク](https://developers.line.biz/ja/glossary/#group)、または[複数人トーク](https://developers.line.biz/ja/glossary/#room)から起動したLIFFアプリの[LIFFブラウザ](https://developers.line.biz/ja/glossary/#liff-browser)内である
- [`chat_message.write`スコープ](https://developers.line.biz/ja/docs/liff/registering-liff-apps/#registering-liff-app)が有効である
- LIFFアプリが「[最近使用したサービス](https://developers.line.biz/ja/docs/liff/overview/#multi-tab-view-recent-service)」から再読み込みされていない

条件を満たしていない場合、`liff.sendMessages()`メソッドが利用できず、エラーコード`403`の`user doesn't grant required permissions yet`エラーが発生します。以下は、エラーが発生する場合の例です。

- [Keepメモ](https://help.line.me/line/smartphone/pc?lang=ja&contentId=20017696)の機能を利用してLIFFアプリにアクセスした場合。
- ウェブサイトのリダイレクト処理などにより[LIFFアプリを開く](https://developers.line.biz/ja/docs/line-login/using-line-url-scheme/#opening-a-liff-app)ためのURLスキームにアクセスした場合。
- LIFF間遷移後のLIFFアプリで`chat_message.write`スコープが無効になった場合。詳しくは、『LIFFドキュメント』の「[LIFF間遷移後の「chat_message.write」スコープについて](https://developers.line.biz/ja/docs/liff/opening-liff-app/#about-chat-message-write-scope)」を参照してください。
- ユーザーが`chat_message.write`スコープを認可しなかった場合。

なお、LIFFアプリが起動された画面に関する情報は、[`liff.getContext()`](https://developers.line.biz/ja/reference/liff/#get-context)メソッドで取得できます。

_例_

<!-- tab start `javascript` -->

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

<!-- tab end -->

#### 構文 

```javascript
liff.sendMessages(messages);
```

#### 引数 

<!-- parameter start (props: required) -->

messages

Array of objects

[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)\
最大件数：5\
Messaging APIの以下のタイプのメッセージを送信できます。

- [テキストメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#text-messages)。ただし、`emojis`プロパティおよび`quoteToken`プロパティは利用できません。
- [スタンプメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#sticker-messages)。ただし、`quoteToken`プロパティは利用できません。
- [画像メッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#image-messages)。
- [動画メッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#video-messages)。ただし、`trackingId`プロパティは利用できません。
- [音声メッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#audio-messages)。
- [位置情報メッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#location-messages)。
- [テンプレートメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#template-messages)。ただし、設定できるアクションは[URIアクション](https://developers.line.biz/ja/docs/messaging-api/actions/#uri-action)のみです。
- [Flex Message](https://developers.line.biz/ja/docs/messaging-api/message-types/#flex-messages)。ただし、設定できるアクションは[URIアクション](https://developers.line.biz/ja/docs/messaging-api/actions/#uri-action)のみです。

<!-- parameter end -->

`liff.sendMessages()`メソッドによってユーザーからテンプレートメッセージまたはFlex Messageが送信された場合、LINEプラットフォームからWebhookは送信されません。それ以外の[メッセージタイプ](https://developers.line.biz/ja/docs/messaging-api/message-types/)であれば、Webhookは送信されます。`liff.sendMessages()`メソッドで画像、動画、および音声のメッセージが送信されると、結果として送信されるWebhookイベントの`contentProvider.type`プロパティの値は`external`になります。詳しくは、『Messaging APIリファレンス』の「[メッセージイベント](https://developers.line.biz/ja/reference/messaging-api/#message-event)」を参照してください。

#### 戻り値 

`Promise`オブジェクトが返されます。

- メッセージの送信が成功すると、`Promise`がresolveされます。値は渡されません。
- メッセージの送信が失敗すると、`Promise`がrejectされ、[`LiffError`](https://developers.line.biz/ja/reference/liff/#liff-errors)が渡されます。

### liff.shareTargetPicker() 

ターゲットピッカー（グループまたは友だちを選択する画面）を表示し、ターゲットピッカーで選択した相手に、開発者が作成したメッセージを送信します。このメッセージは、ユーザーが送信したかのように、グループまたは友だちに表示されます。

ターゲットピッカーで選択できる対象は、ユーザーの友だち（LINE公式アカウントを含む）と、ユーザーが参加しているグループのみです。オープンチャットは含まれません。

#### liff.shareTargetPicker()メソッドの使用条件 

`liff.shareTargetPicker()`メソッドを使用するには、以下の条件をすべて満たす必要があります。

- ユーザーがログインしている。
- [LINE Developersコンソール](https://developers.line.biz/console/)でシェアターゲットピッカーがオンになっている。詳しくは、『LIFFドキュメント』の「[シェアターゲットピッカーを利用するには](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#using-share-target-picker)」を参照してください。

<!-- note start -->

**スマートフォンの外部ブラウザでliff.shareTargetPicker()メソッドを実行した際に、メールアドレスログインの画面が表示されることがあります**

[外部ブラウザ](https://developers.line.biz/ja/glossary/#external-browser)でターゲットピッカーを表示するには、[シングルサインオン（SSO）によるログイン](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#line-sso-login)セッションが必要です。

[自動ログイン](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#line-auto-login)によるログイン処理では、SSOによるログインセッションが発行されないため、`liff.shareTargetPicker()`メソッドの実行時にターゲットピッカーが表示されず、代わりに[メールアドレスログイン](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#mail-or-qrcode-login)の画面が表示されることがあります。

メールアドレスとパスワードを入力してログインすると、SSOによるログインセッションが発行され、ターゲットピッカーが表示されるようになります。

<!-- note end -->

<!-- note start -->

**ユーザーがシェアターゲットピッカーでメッセージを送信した人数は、取得できません**

ユーザーのプライバシーを保護するため、シェアターゲットピッカーで、何人にメッセージが送信されたかの情報は取得できません。また、提供も行なっておりません。

<!-- note end -->

_例_

<!-- tab start `javascript` -->

```javascript
liff
  .shareTargetPicker(
    [
      {
        type: "text",
        text: "Hello, World!",
      },
    ],
    {
      isMultiple: true,
    },
  )
  .then(function (res) {
    if (res) {
      // succeeded in sending a message through TargetPicker
      console.log(`[${res.status}] Message sent!`);
    } else {
      // sending message canceled
      console.log("TargetPicker was closed!");
    }
  })
  .catch(function (error) {
    // something went wrong before sending a message
    console.log("something wrong happen");
  });
```

<!-- tab end -->

#### 構文 

```javascript
liff.shareTargetPicker(messages, options);
```

#### 引数 

<!-- parameter start (props: required) -->

messages

Array of objects

[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)\
最大件数：5\
Messaging APIの以下のタイプのメッセージを送信できます。

- [テキストメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#text-messages)。ただし、`emojis`プロパティおよび`quoteToken`プロパティは利用できません。
- [画像メッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#image-messages)。
- [動画メッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#video-messages)。ただし、`trackingId`プロパティは利用できません。
- [音声メッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#audio-messages)。
- [位置情報メッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#location-messages)。
- [テンプレートメッセージ](https://developers.line.biz/ja/docs/messaging-api/message-types/#template-messages)。ただし、設定できるアクションは[URIアクション](https://developers.line.biz/ja/docs/messaging-api/actions/#uri-action)のみです。
- [Flex Message](https://developers.line.biz/ja/docs/messaging-api/message-types/#flex-messages)。ただし、設定できるアクションは[URIアクション](https://developers.line.biz/ja/docs/messaging-api/actions/#uri-action)のみです。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

options

Object

シェアターゲットピッカーのオプション

<!-- parameter end -->
<!-- parameter start (props: optional) -->

options.isMultiple

Boolean

ユーザーがターゲットピッカーで選択するメッセージ送信先として、複数の送信先を選択可能にするかどうかを、以下のどちらかの値で指定します。デフォルト値は`true`です。

- `true`：ユーザーはグループ、友だち、トークの中から、複数の送信先を選択できます。
- `false`：ユーザーは友だちの中から、1人のみを送信先として選択できます。

<!-- parameter end -->

<!-- note start -->

**isMultipleにfalseを設定しても、1人の友だちのみにメッセージが送信されることは保証できません**

`isMultiple`プロパティに`false`を設定しても、シェアターゲットピッカーを複数回呼び出すことや、シェア後のメッセージをユーザー側で再度シェアすることで、複数のユーザーへのメッセージ送信が可能です。厳密にユーザーから1人の友だちに対して、一度しかメッセージを送信できないようにする場合には、LIFFアプリ実装時に制限をかける必要があります。

URLを含むメッセージを送信し、URLへのアクセスを制限する場合の例を紹介します。

1. URLにユニークなトークンを付与し、メッセージを送信します。
2. メッセージ内のURLへアクセスされた際にサーバー側でトークンを検証し、複数のユーザーからのアクセスを制限します。

<!-- note end -->

#### 戻り値

`Promise`オブジェクトが返されます。

- 正しくメッセージが送信されると、`Promise`がresolveされ、以下のプロパティを持つオブジェクトが渡されます。

    <!-- parameter start -->

  status

  String

  常に`success`です。

    <!-- parameter end -->

- メッセージを送信する前に、ユーザーがキャンセルしてターゲットピッカーを閉じると、`Promise`がresolveされますが、オブジェクトは渡されません。

- ターゲットピッカーが表示される前に問題が発生した場合は、`Promise`がrejectされ、`LiffError`が渡されます。LiffErrorオブジェクトについては、「[LIFF SDKのエラー](https://developers.line.biz/ja/reference/liff/#liff-errors)」を参照してください。

<!-- note start -->

**注意**

`Promise`がresolveした場合とrejectした場合のコールバック関数内で、`alert()`を実行すると一部端末で正しく動作しません。

<!-- note end -->

## カメラ 

### liff.scanCodeV2() 

二次元コードリーダーを起動し、読み取った文字列を取得します。二次元コードリーダーを起動するには、あらかじめ[LINE Developersコンソール](https://developers.line.biz/console/)で、 [**Scan QR**] をオンにする必要があります。

<!-- note start -->

**liff.scanCodeV2()の動作環境**

`liff.scanCodeV2()`は以下の環境で動作します。

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

<!-- note start -->

**liff.scanCodeV2()の動作仕様**

`liff.scanCodeV2()`は、内部で[jsQR](https://github.com/cozmo/jsQR)という外部ライブラリを使用しています。そのため、`liff.scanCodeV2()`メソッド実行時に起動する二次元コードリーダーは、[jsQR](https://github.com/cozmo/jsQR)の動作仕様に依存します。なお、使用ライブラリは予告なく更新、変更される可能性があります。

<!-- note end -->

_例_

<!-- tab start `javascript` -->

```javascript
liff
  .scanCodeV2()
  .then((result) => {
    // result = { value: "" }
  })
  .catch((error) => {
    console.log("error", error);
  });
```

<!-- tab end -->

#### 構文 

```javascript
liff.scanCodeV2();
```

#### 引数 

なし

#### 戻り値 

`Promise`オブジェクトが返されます。

二次元コードリーダーで文字列が読み取れると、`Promise`がresolveされ、読み取った文字列を含むオブジェクトが渡されます。

<!-- parameter start -->

value

String

二次元コードリーダーで読み取った文字列

<!-- parameter end -->

##### エラーレスポンス 

`Promise`が`reject`されたときは、[`LiffError`](https://developers.line.biz/ja/reference/liff/#liff-errors)が渡されます。

### liff.scanCode() 

<!-- note start -->

**liff.scanCode()メソッドは非推奨です**

従来の`liff.scanCode()`メソッドは[非推奨](https://developers.line.biz/ja/glossary/#deprecated)になります。二次元コードリーダーを実装する場合は、[`liff.scanCodeV2()`](https://developers.line.biz/ja/reference/liff/#scan-code-v2)メソッドを使用することをお勧めします。

<!-- note end -->

<br>

LINEの二次元コードリーダーを起動し、読み取った文字列を取得します。二次元コードリーダーを起動するには、あらかじめ[LINE Developersコンソール](https://developers.line.biz/console/)で、 [**Scan QR**] をオンにする必要があります。

<!-- note start -->

**iOS版LINEでは使用できません**

`liff.scanCode()`は以下の環境で動作します。

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
      <td>iOS</td>
      <td>すべてのバージョン</td>
      <td>❌</td>
      <td>❌</td>
    </tr>
    <tr>
      <td>Android</td>
      <td>すべてのバージョン</td>
      <td>✅</td>
      <td>❌</td>
    </tr>
    <tr>
      <td>PC</td>
      <td>すべてのバージョン</td>
      <td>❌</td>
      <td>❌</td>
    </tr>
  </tbody>
</table>

技術的な問題があり、iOS版LINEでは、`liff.scanCode`は`undefined`になります。サンプルコードのように、関数の存在を確認してから、使用してください。iOS版LINEや外部ブラウザでも二次元コードリーダーをお使いになりたい場合は、「[`liff.scanCodeV2()`](https://developers.line.biz/ja/reference/liff/#scan-code-v2)」を参照してください。

<!-- note end -->

<!-- note start -->

**二次元コードリーダーを起動するには［Scan QR］をオンにしてください**

- [LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)ときに、［**Scan QR**］をオンにしてください。［**Scan QR**］の設定は、LIFFアプリ追加後も[LINE Developersコンソール](https://developers.line.biz/console/)のLIFFタブで変更できます。
- `liff.scanCode()`は、外部ブラウザでは利用できません。

<!-- note end -->

_例_

<!-- tab start `javascript` -->

```javascript
if (liff.scanCode) {
  liff.scanCode().then((result) => {
    // result = { value: "" }
  });
}
```

<!-- tab end -->

#### 構文 

```javascript
liff.scanCode();
```

#### 引数 

なし

#### 戻り値 

`Promise`オブジェクトが返されます。

LINEの二次元コードリーダーで文字列が読み取れると、`Promise`がresolveされ、読み取った文字列を含むオブジェクトが渡されます。

<!-- parameter start -->

value

String

二次元コードリーダーで読み取った文字列

<!-- parameter end -->

## パーマネントリンク 

### liff.permanentLink.createUrlBy() 

LIFFアプリの任意のページのパーマネントリンクを取得します。

パーマネントリンクの形式：

```
https://liff.line.me/{liffId}/{path}?{query}#{URL fragment}
```

_例_

<!-- tab start `javascript` -->

```javascript
// For example, if the endpoint URL of the LIFF app
// is https://example.com/path1?q1=v1
// and its LIFF ID is 1234567890-AbcdEfgh
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

liff.permanentLink
  .createUrlBy("https://example.com/")
  .catch((error) => {
  // Error: currentPageUrl must start with endpoint URL of LIFF App.
  console.log(error);
});
```

<!-- tab end -->

#### 構文 

```javascript
liff.permanentLink.createUrlBy(url);
```

#### 引数 

<!-- parameter start (props: required) -->

url

String

パーマネントリンクを取得するURL。任意のクエリパラメータやURLフラグメントを追加できます。

<!-- parameter end -->

#### 戻り値 

`Promise`オブジェクトが返されます。

`Promise`がresolveされると、パーマネントリンクの文字列が渡されます。

##### エラーレスポンス 

パーマネントリンクを取得するURLが、[LINE Developersコンソール](https://developers.line.biz/console/)の［**エンドポイントURL**］に指定したURLで始まらない場合、`Promise`がrejectされ、[`LiffError`](https://developers.line.biz/ja/reference/liff/#liff-errors)が渡されます。

たとえば、パーマネントリンクを取得するURL（例：`https://example.com/`）が、［**エンドポイントURL**］（例：`https://example.com/path1?q1=v1`）より上の階層の場合、`Promise`がrejectされます。

### liff.permanentLink.createUrl() 

<!-- note start -->

**liff.permanentLink.createUrl()は次回メジャーバージョン以降に非推奨になる可能性があります**

技術的な問題があり、`liff.permanentLink.createUrl()`は、次回メジャーバージョン以降に非推奨になる可能性があります。現在のページのパーマネントリンクを取得するには、[`liff.permanentLink.createUrlBy()`](https://developers.line.biz/ja/reference/liff/#permanent-link-create-url-by)を使用することをお勧めします。

<!-- note end -->

現在のページのパーマネントリンクを取得します。

パーマネントリンクの形式：

```
https://liff.line.me/{liffId}/{path}?{query}#{URL fragment}
```

_例_

<!-- tab start `javascript` -->

```javascript
// For example, if current location is
// /shopping?item_id=99#details
// (LIFF ID = 1234567890-AbcdEfgh)
const myLink = liff.permanentLink.createUrl();

// myLink equals "https://liff.line.me/1234567890-AbcdEfgh/shopping?item_id=99#details"
```

<!-- tab end -->

#### 構文 

```javascript
liff.permanentLink.createUrl();
```

#### 引数 

なし

#### 戻り値 

現在のページのパーマネントリンクが、文字列で返されます。

現在のページのURLがLINE Developersコンソールの［**エンドポイントURL**］に指定したURLで始まらない場合、`LiffError`例外が発生します。

### liff.permanentLink.setExtraQueryParam() 

<!-- note start -->

**liff.permanentLink.setExtraQueryParam()は次回メジャーバージョン以降に非推奨になる可能性があります**

技術的な問題があり、`liff.permanentLink.setExtraQueryParam()`は、次回メジャーバージョン以降に非推奨になる可能性があります。現在のページのパーマネントリンクに、任意のクエリパラメータを追加するには、[`liff.permanentLink.createUrlBy()`](https://developers.line.biz/ja/reference/liff/#permanent-link-create-url-by)を使用することをお勧めします。

<!-- note end -->

現在のページのパーマネントリンクに、任意のクエリパラメータを追加できます。

`liff.permanentLink.setExtraQueryParam()`を実行するたびに、前回追加したクエリパラメータは破棄されます。

<!-- tip start -->

**追加したクエリパラメータの削除について**

- 追加したクエリパラメータを削除するには、`liff.permanentLink.setExtraQueryParam("")`を実行します。
- 追加したクエリパラメータは、ユーザーが別のページに移動すると破棄されます。

<!-- tip end -->

_例_

<!-- tab start `javascript` -->

```javascript
// For example, if current location is
// /food?menu=pizza
// (LIFF ID = 1234567890-AbcdEfgh)
liff.permanentLink.setExtraQueryParam("user_tracking_id=8888");
const myLink = liff.permanentLink.createUrl();

// myLink equals "https://liff.line.me/1234567890-AbcdEfgh/food?menu=pizza&user_tracking_id=8888"
```

<!-- tab end -->

#### 構文 

```javascript
liff.permanentLink.setExtraQueryParam(extraString);
```

#### 引数 

<!-- parameter start (props: required) -->

extraString

String

追加するクエリパラメータ

<!-- parameter end -->

#### 戻り値 

なし

## LIFFプラグイン 

### liff.use() 

[プラガブルSDK](https://developers.line.biz/ja/docs/liff/pluggable-sdk/)のLIFF APIや、[LIFFプラグイン](https://developers.line.biz/ja/docs/liff/liff-plugin/)を有効化し、初期化処理を実行します。

_プラガブルSDKのLIFF APIの例_

<!-- tab start `javascript` -->

```javascript
import liff from "@line/liff/core";
import GetOS from "@line/liff/get-os";

liff.use(new GetOS());

liff.init({
  liffId: "123456-abcedfg", // Use own liffId
});
```

<!-- tab end -->

_LIFFプラグインの例_

<!-- tab start `javascript` -->

```javascript
class greetPlugin {
  constructor() {
    this.name = "greet";
  }

  install() {
    return {
      hello: this.hello,
    };
  }

  hello() {
    console.log("Hello, World!");
  }
}

liff.use(new greetPlugin());
```

<!-- tab end -->

#### 構文 

```javascript
liff.use(module, option);
```

#### 引数 

<!-- parameter start (props: required) -->

module

Object

プラガブルSDKのLIFF APIのモジュールやLIFFプラグイン。

LIFF APIのモジュールを渡す場合、インスタンス化する必要があります。詳しくは、『LIFFドキュメント』の「[プラガブルSDKの使用方法](https://developers.line.biz/ja/docs/liff/pluggable-sdk/#how-to-use)」を参照してください。

LIFFプラグインを渡す場合、LIFFプラグインがクラスのときは、インスタンス化する必要があります。詳しくは、『LIFFドキュメント』の「[LIFFプラグインを使用する](https://developers.line.biz/ja/docs/liff/liff-plugin/#use-liff-plugin)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

option

Any value

`module`プロパティで指定した、LIFFプラグインに渡す値。LIFFプラグインの[`install()`](https://developers.line.biz/ja/docs/liff/liff-plugin/#install)メソッドの第2引数として渡されます。詳しくは、『LIFFドキュメント』の「[option](https://developers.line.biz/ja/docs/liff/liff-plugin/#option)」を参照してください。

<!-- parameter end -->

#### 戻り値 

`liff`オブジェクトが返されます。

## 多言語化 

### liff.i18n.setLang() 

LIFF SDKが表示する文言の言語を指定します。

_例_

<!-- tab start `javascript` -->

```javascript
liff.i18n.setLang("en");
```

<!-- tab end -->

#### 構文 

```javascript
liff.i18n.setLang(language);
```

#### 引数 

<!-- parameter start (props: required) -->

language

String

[RFC 5646（BCP 47）](https://datatracker.ietf.org/doc/html/rfc5646)で定義されている言語タグ。指定した言語タグの翻訳がない場合は、`en`がフォールバックとして使用されます。

<!-- parameter end -->

#### 戻り値 

`Promise`オブジェクトが返されます。

##### エラーレスポンス 

`Promise`がrejectされたときは、[`LiffError`](https://developers.line.biz/ja/reference/liff/#liff-errors)が渡されます。

## その他 

### liff.createShortcutOnHomeScreen() 

<!-- tip start -->

**認証済ミニアプリでのみ利用できます**

この機能は、認証済ミニアプリでのみ利用できます。未認証ミニアプリの場合、開発用の内部チャネルではテストできますが、公開用の内部チャネルでは利用できません。

<!-- tip end -->

[LINEミニアプリ](https://developers.line.biz/ja/docs/line-mini-app/)へのショートカットを、ユーザー端末のホーム画面に追加する画面を表示します。

![](https://developers.line.biz/media/line-mini-app/develop/add-to-home-screen/add-shortcut-screen-ios-ja.png)

詳しくは、『LINEミニアプリドキュメント』の「[ユーザー端末のホーム画面にLINEミニアプリへのショートカットを追加する](https://developers.line.biz/ja/docs/line-mini-app/develop/add-to-home-screen/)」を参照してください。

<!-- note start -->

**liff.createShortcutOnHomeScreen()メソッドを実行するタイミング**

`liff.createShortcutOnHomeScreen()`メソッドは、ユーザー体験を損なわないよう、LINEミニアプリ上でのユーザー操作（例：タップ）に対する応答として実行してください。

<!-- note end -->

_例_

<!-- tab start `javascript` -->

```javascript
// LINEミニアプリのエンドポイントURLが
// https://example.com/path1/path2、
// LIFF IDが1234567890-AbcdEfghの場合

// LIFF URLを指定した例
liff
  .createShortcutOnHomeScreen({
    url: "https://miniapp.line.me/1234567890-AbcdEfgh",
  })
  .then(() => { /* ... */ });

liff
  .createShortcutOnHomeScreen({
    url: "https://liff.line.me/1234567890-AbcdEfgh",
  })
  .then(() => { /* ... */ });

// パーマネントリンクを指定した例
liff
  .createShortcutOnHomeScreen({
    url: "https://liff.line.me/1234567890-AbcdEfgh/path3",
  })
  .then(() => { /* ... */ });

// LINEミニアプリのエンドポイントURLを指定した例
liff
  .createShortcutOnHomeScreen({
    url: "https://example.com/path1/path2",
  })
  .then(() => { /* ... */ });

// LINEミニアプリのエンドポイントURLから始まるURLを指定した例
liff
  .createShortcutOnHomeScreen({
    url: "https://example.com/path1/path2/path3",
  })
  .then(() => { /* ... */ });

// エラーになるURLを指定した例
liff
  .createShortcutOnHomeScreen({
    url: "https://example.com/invalid-path",
  })
  .then(() => { /* ... */ })
  .catch((error) => {
    // invalid URL.
    console.log(error.message);
  });
```

<!-- tab end -->

#### 使用条件 

`liff.createShortcutOnHomeScreen()`メソッドを使用するには、以下の条件をすべて満たす必要があります。

- LINEミニアプリである。
- LINEミニアプリのLIFF SDKのバージョンがv2.23.0以上である。
- ユーザー端末のLINEアプリのバージョンが13.20.0以上である。

#### 動作条件 

ユーザー端末のOSがiOSの場合、`liff.createShortcutOnHomeScreen()`メソッドが動作する条件は以下のとおりです。動作しない環境においてこのメソッドを実行すると、エラーページが表示されます。

| デフォルトのブラウザ         | iOSのバージョン    | 動作するかどうか   |
| ---------------------------- | ------------------ | ------------------ |
| Safari                       | すべてのバージョン | 動作する           |
| Chrome                       | 16.4以降           | 動作する           |
| Safari、Chrome以外のブラウザ | 16.4以降           | 動作は保証されない |
| Safari以外のブラウザ         | 16.4未満           | 動作しない         |

たとえば、iOS 16.4未満において、Chromeで`liff.createShortcutOnHomeScreen()`メソッドを実行した場合は、以下のエラーページが表示されます。

![](https://developers.line.biz/media/line-mini-app/develop/add-to-home-screen/add-shortcut-screen-ios-error-ja.png)

#### 構文 

```javascript
liff.createShortcutOnHomeScreen(params);
```

#### 引数 

<!-- parameter start (props: required) -->

params

Object

パラメータオブジェクト

<!-- parameter end -->
<!-- parameter start (props: required) -->

params.url

String

URL。以下のURLを指定できます。

- [LIFF URL](https://developers.line.biz/ja/glossary/#liff-url)
- [パーマネントリンク](https://developers.line.biz/ja/glossary/#permanent-link-liff)
- LINEミニアプリのエンドポイントURL
- LINEミニアプリのエンドポイントURLから始まるURL

<!-- parameter end -->

#### 戻り値 

`Promise`オブジェクトが返されます。

ショートカット追加画面が表示されると、`Promise`がresolveされます。値は渡されません。

なお、ユーザーが端末のホーム画面にLINEミニアプリへのショートカットを実際に追加したかどうかは確認できません。

##### エラーレスポンス 

`Promise`が`reject`されたときは、[`LiffError`](https://developers.line.biz/ja/reference/liff/#liff-errors)が渡されます。
