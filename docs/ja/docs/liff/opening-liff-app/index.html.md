# LIFFアプリを開く

LIFFアプリは、[LIFFブラウザ](https://developers.line.biz/ja/glossary/#liff-browser)または[外部ブラウザ](https://developers.line.biz/ja/glossary/#external-browser)で開くことができます。

このページでは、ユーザーがLIFFアプリを開く際の操作方法や、LIFFアプリが開くまでの動作について説明します。

<!-- table of contents -->

## ユーザーがLIFFアプリを開く際の操作 

ここでは、ユーザーがLIFFアプリを開く際の操作を説明します。

1. ユーザーが[LIFF URL](https://developers.line.biz/ja/glossary/#liff-url)にアクセスします。

   LIFF URLは、[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)と、発行されます。\
   たとえば、LINEアプリのトークにLIFF URLを送信し、吹き出しに表示されたLIFF URLをタップします。

   ![](https://developers.line.biz/media/liff/open-liff-app.png)

1. ユーザーからの認可が必要な場合、チャネル同意画面が表示されます。同意画面では、ユーザーがLIFFアプリに必要な権限を与えることを許可します。

   ![同意画面](https://developers.line.biz/media/line-login/integrate-login-web/consent-screen-ja.png)

1. LIFFアプリが開きます。

   ![LIFF browser](https://developers.line.biz/media/liff/overview/liffBrowser.png)

### LIFF URLにアクセスした際にLIFFアプリが開かれる環境について 

ユーザーがLIFF URLにアクセスすると、[外部ブラウザ](https://developers.line.biz/ja/glossary/#external-browser)またはLINEアプリ上で[LIFFブラウザ](https://developers.line.biz/ja/glossary/#liff-browser)が開きます。

LIFF URLは、iOSの[ユニバーサルリンク](https://developer.apple.com/documentation/xcode/allowing-apps-and-websites-to-link-to-your-content/)やAndroidの[アプリリンク](https://developer.android.com/training/app-links)に対応しているため、LINEアプリ外からLIFF URLを開いた場合もLINEアプリ上でLIFFブラウザが開かれます。

ただしユーザーが利用するOSの仕様によって、Safari、Chromeなどの外部ブラウザ上でも、ユニバーサルリンクやアプリリンクが動作せずにLINEアプリ上でLIFFブラウザが開かないことがあります。また、LINEアプリ以外のネイティブアプリ上でLIFF URLにアクセスした場合、外部ブラウザとLIFFブラウザのどちらでLIFFアプリが開かれるかは、そのネイティブアプリのWebView仕様に準拠します。

これらの理由から、LIFF URLにアクセスした場合にLIFFアプリがどの環境で開かれるかは保証していません。LIFF URLにアクセスしたとしてもLINEアプリ上でLIFFブラウザが開かない場合もあることに注意してください。

## LIFF URLにアクセスしてからLIFFアプリが開くまでの動作について 

ここでは、ユーザーがLIFF URLにアクセスしたときに、LIFFアプリが正しく開くように実装するために、2つのリダイレクト先の設定方法、および`liff.init()`メソッドを実行するタイミングを説明します。

| リダイレクト先 | 説明 |
| --- | --- |
| 1次リダイレクト先URL | ユーザーがLIFF URLにアクセスしたときに、LIFFサーバーから初めてリダイレクトされる先のURLです。ここにリダイレクトされたときに、`liff.init()`メソッドを実行します。 |
| 2次リダイレクト先URL | `liff.init()`メソッドが実行されたときに、ユーザーがリダイレクトされる先のURLです。ここにリダイレクトされたら、LIFFアプリのページを表示します。 |

![リダイレクトの流れ](https://developers.line.biz/media/liff/redirect-flow.png)

### LIFF URLを作成する 

LIFF URLは、LINEヤフー株式会社が提供するLIFFサーバーを指すURLです。[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)と、発行されます。

LIFF URLの例：`https://liff.line.me/1234567890-AbcdEfgh`

#### サポートされているLIFF URL 

サポートされているLIFF URLは、以下のとおりです。

- `https://liff.line.me/{liffId}`&nbsp;
- `https://miniapp.line.me/{liffId}` (LINEミニアプリのみ)

<!-- note start -->

**「https://line.me/R/app/{liffId}」および「line://app/{liffId}」は非推奨です**

[LIFF v1](https://developers.line.biz/ja/docs/liff/versioning-policy/#life-cycle-schedule)向けに提供されていた以下の形式のLIFF URLは、[非推奨](https://developers.line.biz/ja/glossary/#deprecated)です。

- `https://line.me/R/app/{liffId}`&nbsp;
- `line://app/{liffId}`&nbsp;

<!-- note end -->

### 1次リダイレクト先URLを作成する 

1次リダイレクト先URLは、常にLINE Developersコンソールの［**エンドポイントURL**］に指定したURLです。

<!-- note start -->

**LIFF URLに指定した追加情報の扱い**

1次リダイレクト先URLではLIFF URLに指定した追加情報（例：`path_A/?key1=value1#URL-fragment`）はすべて`liff.state`クエリパラメータに含まれています。

例：`https://example.com/2020campaign/?key=value&liff.state=urlencoded(path_A/?key1=value1#URL-fragment)`

なお、LIFF URLに追加情報を指定しない場合は、`liff.state`クエリパラメータは省略されます。

<!-- note end -->

### 2次リダイレクト先URLを作成する 

2次リダイレクト先URLは、ユーザーがアクセスするURLによって異なります。

LINE Developersコンソールの［**エンドポイントURL**］に指定したパスやクエリパラメータ（`/2020campaign/?key=value`）が、2次リダイレクト先に含まれます。

| ユーザーがアクセスするURL | 2次リダイレクト先URL |
| --- | --- |
| LIFF URL（1）<br>例：`https://liff.line.me/{liffId}` | LINE Developersコンソールの［**エンドポイントURL**］に指定したURLです。<br>例：`https://example.com/2020campaign/?key=value` |
| LIFF URLに追加情報を指定したURL（2）<br>例：`https://liff.line.me/{liffId}/path_A/?key1=value1#URL-fragment` | 図の(2)のように3種類の情報を組み合わせたURLです。<ul><li>［**エンドポイントURL**］に指定したドメイン名（`https://example.com`）</li><li>［**エンドポイントURL**］に指定したパスやクエリパラメータ（`/2020campaign/?key=value`）</li><li>LIFF URLに指定した追加情報（`/path_A/?key1=value1#URL-fragment`）</li></ul>例：`https://example.com/2020campaign/path_A/?key=value&key1=value1#URL-fragment` |

![エンドポイントURL](https://developers.line.biz/media/liff/endpoint-url.png)

## LIFFアプリから別のLIFFアプリを開いた場合の動作について（LIFF間遷移） 

LIFFブラウザでLIFFアプリを開いているときに、別のLIFFアプリへのリンクをクリックすると、LIFFブラウザを開いたまま別のアプリを表示することができます。これを「LIFF間遷移」と呼びます。LIFF間遷移ではLIFFブラウザが閉じないため、LIFFブラウザの戻るボタンで遷移元のLIFFアプリに戻ることができます。

- [LIFF間遷移が可能な条件](https://developers.line.biz/ja/docs/liff/opening-liff-app/#conditions-liff-to-liff)
- [LIFFアプリの画面サイズによる動作](https://developers.line.biz/ja/docs/liff/opening-liff-app/#behavior-by-screen-size)
- [LIFF間遷移後の「chat_message.write」スコープについて](https://developers.line.biz/ja/docs/liff/opening-liff-app/#about-chat-message-write-scope)
- [LIFF間遷移前のURLを取得する](https://developers.line.biz/ja/docs/liff/opening-liff-app/#using-liff-referrer)
- [別のLIFFアプリを開いた場合に表示されるメッセージ](https://developers.line.biz/ja/docs/liff/opening-liff-app/#messages-liff-to-liff)

![LIFF-apps-transition](https://developers.line.biz/media/liff/liff_transition.png)

<!-- note start -->

**意図しない動作**

古いバージョンのLIFF SDKを使っている場合、以下のような意図しない動作になることがあります。

- パス（`/path`）が指定されたLIFF URLから別のLIFFアプリへ遷移したにもかかわらず、LINE Developersコンソールの［**エンドポイントURL**］に指定したURLへ遷移してしまう
- ユーザーに権限の認可を求める[同意画面](https://developers.line.biz/ja/docs/line-login/link-a-bot/)で［**キャンセル**］をクリックした場合、一度LIFFブラウザを閉じなくてはならない
- 遷移先がLINEミニアプリの場合、LIFFブラウザヘッダのデザインが自動で変化しない

複数のLIFFアプリ間を遷移するように設計する際は、最新版のLIFF SDKを使うことをお勧めします。

<!-- note end -->

### LIFF間遷移が可能な条件 

以下の条件をすべて満たす場合に、LIFF間遷移が可能となります。

- LIFF SDKバージョンが2.4.1以上
- 遷移元のLIFFアプリの画面サイズが`Full`表示に設定されている
- 遷移先のLIFFアプリが`liff.init()`で正しく初期化されている

### LIFFアプリの画面サイズによる動作 

- 遷移元のLIFFアプリの画面サイズが`Tall`もしくは`Compact`の場合は、遷移先の画面サイズにかかわらず一度ブラウザが閉じてから、遷移先のLIFFアプリが表示されます。
- 遷移元のLIFFアプリの画面サイズが`Full`の場合、遷移後のLIFFアプリは画面サイズの指定にかかわらず`Full`で表示されます。
- 遷移元のLIFFアプリの画面サイズが`Full`で、遷移先のLIFFアプリの画面サイズの指定が`Tall`もしくは`Compact`だった場合、遷移後のLIFFアプリでは、[アクションボタン](https://developers.line.biz/ja/docs/liff/overview/#action-button)は表示されません。

### LIFF間遷移後の「chat_message.write」スコープについて 

LIFF間遷移後の`chat_message.write`スコープは、遷移先のURLによって有効かどうかが異なります。

| 遷移先のURL | URLの例 | 遷移後の`chat_message.write`スコープ |
| --- | --- | --- |
| LIFF URL | `https://liff.line.me/{liffId}` | **有効** |
| LIFF URLに追加情報を指定したURL | `https://liff.line.me/{liffId}/path_A/?key1=value1#URL-fragment` | **有効** |
| エンドポイントURL | `https://example.com` | **無効** |

`chat_message.write`スコープが有効であれば、遷移後のLIFFアプリでも[`liff.sendMessages()`](https://developers.line.biz/ja/reference/liff/#send-messages)メソッドを利用できます。

### LIFF間遷移前のURLを取得する 

LIFF間遷移でLIFFアプリを開いた場合、遷移後のLIFFアプリのURLには`liff.referrer`というクエリパラメータが付与されます。`liff.referrer`の値には、LIFF間遷移時にLIFFサーバーが受信した`Referer`リクエストヘッダーのアドレスを、[パーセントエンコード](https://ja.wikipedia.org/wiki/%E3%83%91%E3%83%BC%E3%82%BB%E3%83%B3%E3%83%88%E3%82%A8%E3%83%B3%E3%82%B3%E3%83%BC%E3%83%87%E3%82%A3%E3%83%B3%E3%82%B0)したURLが設定されます。`liff.referrer`の値を確認することで、遷移前のURLを取得できます。

<!-- note start -->

**LINEバージョン12.13.0〜13.19.xでは、LIFF間遷移後のLIFFアプリのURLにliff.referrerが付与されません**

詳しくは、2023年11月30日のニュース、「[LINEバージョン12.13.0以降でLIFF間遷移後にliff.referrerが付与されない不具合を修正しました](https://developers.line.biz/ja/news/2023/11/30/liff-update-line-13-20-0/)」を参照してください。

<!-- note end -->

以下は、LIFF間遷移時に`liff.referrer`が付与される例です。

|  | 遷移前のLIFFアプリのURL | リンク先のURL | 遷移後のLIFFアプリのURL（`liff.init()`メソッド実行後） |
| --- | --- | --- | --- |
| **付与される場合** | `https://first.example.com/` | `https://liff.line.me/{LIFF ID}`<br>（LIFF URL） | `✅ https://second.example.com/?liff.referrer=https%3A%2F%2Ffirst.example.com%2F` ※1 |
| **付与されない場合** | `https://first.example.com/` | `https://second.example.com/`<br>（エンドポイントURL） | `❌ https://second.example.com/` ※2 |

※1 遷移後のLIFFアプリのURLには`liff.referrer`以外にも`liff.*`のクエリパラメータが付与されていることがあります。<br>※2 LIFFアプリのエンドポイントURLを直接開いた場合、`liff.referrer`は付与されません。

### 別のLIFFアプリを開いた場合に表示されるメッセージ 

LIFFアプリから別のURLにアクセスしたときに、「○○（LIFFアプリの名称）へ移動しました。」というメッセージが表示される場合があります。

このメッセージは、先に開いているLIFFアプリ（遷移元のLIFFアプリ）と異なるLIFF IDのLIFFアプリを開いたときに表示されます。このメッセージの表示の有無は、LIFF間遷移の成功とは関係ありません。

![](https://developers.line.biz/media/liff/switched-to-another-app-ja.png)
