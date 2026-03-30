# LIFF CLI

<!-- table of contents -->

## LIFF CLIとは 

LIFF CLIとは、LIFFアプリの開発を円滑にするCLIツールです。

- [GitHub](https://github.com/line/liff-cli)
- [npm](https://www.npmjs.com/package/@line/liff-cli)

LIFF CLIでできることは次のとおりです。

- LIFFアプリを作成、更新、参照、削除する
- LIFFアプリの開発環境を作成する
- LIFFアプリを[LIFF Inspector](https://developers.line.biz/ja/docs/liff/liff-plugin/#liff-inspector)でデバッグする
- ローカル開発サーバーをHTTPSで起動する

今後のアップデートで[LIFF Mock](https://developers.line.biz/ja/docs/liff/liff-plugin/#liff-mock)の機能も追加される予定です。

## LIFF CLIの動作環境 

LIFF CLIはNode.jsで動作します。パッケージ管理にはnpmまたはYarnが使用可能ですが、このページではnpmを使います。このページの内容は次の各バージョンで動作を確認しています。

| 名前                                                     | バージョン |
| -------------------------------------------------------- | ---------- |
| [LIFF CLI](https://www.npmjs.com/package/@line/liff-cli) | 0.4.1      |
| [LIFF SDK](https://www.npmjs.com/package/@line/liff)     | 2.24.0     |
| [Node.js](https://nodejs.org/en)                         | 22.2.0     |
| [npm](https://www.npmjs.com/)                            | 10.7.0     |

## LIFF CLIをインストールする 

ターミナルまたはコマンドラインツール（以下「ターミナル」と言います）を開き、次のコマンドを実行します。

```bash
$ npm install -g @line/liff-cli
```

コマンドを実行すると、LIFF CLIがインストールされ、`liff-cli`コマンドを実行できるようになります。

## チャネルを管理する 

`channel`コマンドを使うと、LIFF CLIで管理するチャネルを追加したり、デフォルトのチャネルを設定したりできます。なお、チャネルはあらかじめ[LINE Developersコンソール](https://developers.line.biz/console/)で作成する必要があります。

### チャネルを追加する 

`add`サブコマンドを使うと、LIFF CLIで管理するチャネルを追加できます。追加したいチャネルのチャネルIDを`add`サブコマンドに渡すと、チャネルシークレットを入力するプロンプトが表示されます。チャネルシークレットを入力すると、チャネルが追加されます。

```bash
$ liff-cli channel add 1234567890
? Channel Secret?: ********************************
Channel 1234567890 is now added.
```

LIFF CLIの各コマンドにチャネルIDを渡す際は、上記のように、あらかじめ`add`サブコマンドでそのチャネルIDを持つチャネルを追加しておく必要があります。

### デフォルトのチャネルを設定する 

`use`サブコマンドを使うと、LIFF CLIのデフォルトのチャネルを設定できます。設定したいチャネルのチャネルIDを`use`サブコマンドに渡します。

```bash
$ liff-cli channel use 1234567890
Channel 1234567890 is now selected.
```

デフォルトのチャネルは、LIFF CLIの各コマンドでチャネルIDを省略した場合に使われます。

## LIFFアプリを管理する 

`app`コマンドを使うと、LIFFアプリの作成、更新、参照、削除ができます。

### LIFFアプリを作成する 

`create`サブコマンドを使うと、LIFFアプリを作成できます。LIFFアプリの作成に成功すると、LIFF IDがターミナルに表示されます。

```bash
$ liff-cli app create \
   --channel-id 1234567890 \
   --name "Brown Coffee" \
   --endpoint-url https://example.com \
   --view-type full
Successfully created LIFF app: 1234567890-AbcdEfgh
```

#### オプション 

`create`サブコマンドでは、以下のオプションを利用できます。

| オプション | 必須  | 説明 |
| --- | --- | --- |
| `-c`、`--channel-id` |  | LIFFアプリを作成したいチャネルのチャネルIDを指定します。省略すると、[デフォルトのチャネル](https://developers.line.biz/ja/docs/liff/liff-cli/#manage-channels-use)のチャネルIDが指定されます。 |
| `-n`、`--name` | ✅ | LIFFアプリ名を指定します。LIFFアプリ名には、「LINE」またはそれに類する文字列、不適切な文字列は含めることができません。 |
| `-e`、`--endpoint-url` | ✅ | <p>LIFFアプリのエンドポイントURLを指定します。LIFFアプリを実装したウェブアプリのURLです（例：`https://example.com`）。LIFF URLを利用してLIFFアプリを起動した際に、このURLが利用されます。</p><p>URLスキームは**https**である必要があります。なお、URLフラグメント（#URL-fragment）は指定できません。</p> |
| `-v`、`--view-type` | ✅ | <p>LIFFアプリの画面サイズ。以下のいずれかの値を指定します。</p><ul><li>`full`</li><li>`tall`</li><li>`compact`</li></ul>詳しくは、「[LIFFブラウザの画面サイズ](https://developers.line.biz/ja/docs/liff/overview/#screen-size)」を参照してください。 |

### LIFFアプリを更新する 

`update`サブコマンドを使うと、LIFFアプリの設定を更新できます。

```bash
$ liff-cli app update \
   --liff-id 1234567890-AbcdEfgh \
   --channel-id 1234567890 \
   --name "Brown Cafe"
Successfully updated LIFF app: 1234567890-AbcdEfgh
```

#### オプション 

`update`サブコマンドでは、以下のオプションを利用できます。

| オプション | 必須  | 説明 |
| --- | --- | --- |
| `--liff-id` | ✅ | 更新したいLIFFアプリのLIFF IDを指定します。 |
| `--channel-id` |  | LIFFアプリが属するチャネルのチャネルIDを指定します。省略すると、[デフォルトのチャネル](https://developers.line.biz/ja/docs/liff/liff-cli/#manage-channels-use)のチャネルIDが指定されます。 |
| `--name` |  | LIFFアプリ名を指定します。LIFFアプリ名には、「LINE」またはそれに類する文字列、不適切な文字列は含めることができません。 |
| `--endpoint-url` |  | <p>LIFFアプリのエンドポイントURLを指定します。LIFFアプリを実装したウェブアプリのURLです（例：`https://example.com`）。LIFF URLを利用してLIFFアプリを起動した際に、このURLが利用されます。</p><p>URLスキームは**https**である必要があります。なお、URLフラグメント（#URL-fragment）は指定できません。</p> |
| `--view-type` |  | <p>LIFFアプリの画面サイズ。以下のいずれかの値を指定します。</p><ul><li>`full`</li><li>`tall`</li><li>`compact`</li></ul>詳しくは、「[LIFFブラウザの画面サイズ](https://developers.line.biz/ja/docs/liff/overview/#screen-size)」を参照してください。 |

### LIFFアプリを参照する 

`list`サブコマンドを使うと、LIFFアプリを参照できます。LIFF IDとLIFFアプリ名が一覧で表示されます。

```bash
$ liff-cli app list --channel-id 1234567890
LIFF apps:
1234567890-AbcdEfgh: Brown Coffee
1234567890-IjklMnop: Brown Cafe
```

#### オプション 

`list`サブコマンドでは、以下のオプションを利用できます。

| オプション | 必須  | 説明 |
| --- | --- | --- |
| `--channel-id` |  | LIFFアプリを参照したいチャネルのチャネルIDを指定します。省略すると、[デフォルトのチャネル](https://developers.line.biz/ja/docs/liff/liff-cli/#manage-channels-use)のチャネルIDが指定されます。 |

### LIFFアプリを削除する 

`delete`サブコマンドを使うと、LIFFアプリを削除できます。

```bash
$ liff-cli app delete \
   --liff-id 1234567890-AbcdEfgh \
   --channel-id 1234567890
Deleting LIFF app...
Successfully deleted LIFF app: 1234567890-AbcdEfgh
```

#### オプション 

`delete`サブコマンドでは、以下のオプションを利用できます。

| オプション | 必須  | 説明 |
| --- | --- | --- |
| `--liff-id` | ✅ | 削除したいLIFFアプリのLIFF IDを指定します。 |
| `--channel-id` |  | LIFFアプリの属するチャネルのチャネルIDを指定します。省略すると、[デフォルトのチャネル](https://developers.line.biz/ja/docs/liff/liff-cli/#manage-channels-use)のチャネルIDが指定されます。 |

## LIFFアプリのひな形を作成する 

`scaffold`コマンドを使うと、[Create LIFF App](https://developers.line.biz/ja/docs/liff/cli-tool-create-liff-app/)を通じてLIFFアプリのひな形を作成できます。LIFFアプリのプロジェクト名を`scaffold`コマンドに渡すと、そのプロジェクト名を使ってCreate LIFF Appを実行します。

```bash
$ liff-cli scaffold my-app --liff-id 1234567890-AbcdEfgh
```

Create LIFF Appについて詳しくは、「[Create LIFF AppでLIFFアプリの開発環境を構築する](https://developers.line.biz/ja/docs/liff/cli-tool-create-liff-app/)」を参照してください。

### オプション 

`scaffold`コマンドでは、以下のオプションを利用できます。

| オプション        | 必須  | 説明                              |
| ----------------- | ---- | --------------------------------- |
| `-l`、`--liff-id` |      | LIFFアプリのLIFF IDを指定します。 |

## LIFFアプリの開発環境を作成する 

`init`コマンドを使うと、LIFFアプリの開発環境を作成できます。`init`コマンドでは、以下の3つの処理を順に行います。

1. [チャネルの追加](https://developers.line.biz/ja/docs/liff/liff-cli/#manage-channels-add)
1. [LIFFアプリの作成](https://developers.line.biz/ja/docs/liff/liff-cli/#manage-liff-apps-create)
1. [LIFFアプリのひな形を作成する](https://developers.line.biz/ja/docs/liff/liff-cli/#scaffold)

```bash
$ liff-cli init \
   --channel-id 1234567890 \
   --name "Brown Coffee" \
   --view-type full \
   --endpoint-url https://example.com
```

たとえば、上記のコマンドを実行すると、チャネルIDが「1234567890」のチャネルを追加します。次に、そのチャネルに、LIFFアプリ名が「Brown Coffee」、エンドポイントURLが「https://example.com」、画面サイズが「Full」のLIFFアプリを作成します。最後に、作成したLIFFアプリのLIFF IDを設定したひな形を作成します。

```bash
liff-cli init \
   --channel-id 1234567890 \
   --name "Brown Coffee" \
   --view-type full \
   --endpoint-url https://example.com

? Channel Secret?: ********************************
Channel 1234567890 is now added.
Welcome to the Create LIFF App
? Which template do you want to use? vanilla
? JavaScript or TypeScript? JavaScript
? Which package manager do you want to use? npm

Installing dependencies:
- @line/liff

removed 10 packages in 944ms

22 packages are looking for funding
  run `npm fund` for details

Installing devDependencies:
- vite

added 10 packages in 7s

25 packages are looking for funding
  run `npm fund` for details

Done! Now run:

  cd Brown Coffee
  npm run dev

App 1234567890-AbcdEfgh successfully created.

Now do the following:
  1. go to app directory: `cd Brown Coffee`
  2. create certificate key files (e.g. `mkcert localhost`, see: https://developers.line.biz/en/docs/liff/liff-cli/#serve-operating-conditions )
  3. run LIFF app template using command above (e.g. `npm run dev` or `yarn dev`)
  4. open new terminal window, navigate to `Brown Coffee` directory
  5. run `liff-cli serve -l 1234567890-AbcdEfgh -u http://localhost:${PORT FROM STEP 3.}/`
  6. open browser and navigate to http://localhost:${PORT FROM STEP 3.}/
```

### オプション 

`init`コマンドでは、以下のオプションを利用できます。なお、オプションを省略すると、`init`コマンドを実行した際に、そのオプションを入力するプロンプトが表示されます。

```bash
$ liff-cli init
? Channel ID? 1234567890
? App name? Brown Coffee
? View type? full
? Endpoint URL? (leave empty for default 'https://localhost:9000') https://example.com
```

| オプション | 必須  | 説明 |
| --- | --- | --- |
| `-c`、`--channel-id` | ✅ ※1 | LIFFアプリを作成したいチャネルのチャネルIDを指定します。 |
| `-n`、`--name` | ✅ ※2 | LIFFアプリ名を指定します。LIFFアプリ名には、「LINE」またはそれに類する文字列、不適切な文字列は含めることができません。 |
| `-v`、`--view-type` | ✅ ※2 | <p>LIFFアプリの画面サイズ。以下のいずれかの値を指定します。</p><ul><li>`full`</li><li>`tall`</li><li>`compact`</li></ul>詳しくは、「[LIFFブラウザの画面サイズ](https://developers.line.biz/ja/docs/liff/overview/#screen-size)」を参照してください。 |
| `-e`、`--endpoint-url` |  | <p>LIFFアプリのエンドポイントURLを指定します。LIFFアプリのデプロイ先のURLです（例：`https://example.com`）。LIFF URLを利用してLIFFアプリを起動した際に、このURLが利用されます。</p><p>URLスキームは**https**である必要があります。なお、URLフラグメント（#URL-fragment）は指定できません。</p> |

※1 [デフォルトのチャネル](https://developers.line.biz/ja/docs/liff/liff-cli/#manage-channels-use)を設定していない場合、オプションかプロンプトのいずれかで指定する必要があります。<br>※2 オプションかプロンプトのいずれかで指定する必要があります。

## ローカル開発サーバーをHTTPSで起動する 

`serve`コマンドを使うと、ローカル開発サーバーをHTTPSで起動できます。

`serve`コマンドにLIFFアプリが動いているローカル開発サーバーを指定すると、ローカル開発サーバーを対象とするローカルプロキシサーバーをHTTPSで起動し、LIFFアプリのエンドポイントURLをローカルプロキシサーバーのURLで書き換えます。これにより、開発者はより簡単にローカル開発サーバーをHTTPSで起動できます。

<!-- note start -->

**公開済みのLIFFアプリではserveコマンドを実行しないでください**

`serve`コマンドを実行すると、LIFFアプリのエンドポイントURLがローカルプロキシサーバーのURLで書き換えられるため、ユーザーがLIFFアプリにアクセスできなくなります。そのため、公開済みのLIFFアプリでは`serve`コマンドを実行しないでください。

![](https://developers.line.biz/media/liff/liff-cli/endpoint-url-ja.png)

<!-- note end -->

```bash
# ローカル開発サーバーをURLで指定する場合
$ liff-cli serve \
   --liff-id 1234567890-AbcdEfgh \
   --url http://localhost:3000/

Successfully updated endpoint url for LIFF ID: 1234567890-AbcdEfgh.

→  LIFF URL:     https://liff.line.me/1234567890-AbcdEfgh
→  Proxy server: https://localhost:9000/
```

```bash
# ローカル開発サーバーをホストとポート番号で指定する場合
$ liff-cli serve \
   --liff-id 1234567890-AbcdEfgh \
   --host localhost \
   --port 3000

Successfully updated endpoint url for LIFF ID: 1234567890-AbcdEfgh.

→  LIFF URL:     https://liff.line.me/1234567890-AbcdEfgh
→  Proxy server: https://localhost:9000/
```

### LIFFアプリをLIFF Inspectorでデバッグする 

`serve`コマンドに`--inspect`オプションを指定すると、LIFFアプリを[LIFF Inspector](https://developers.line.biz/ja/docs/liff/liff-plugin/#liff-inspector)でデバッグできます。

`--inspect`オプションは、LIFF InspectorのLIFF Inspector ServerをHTTPSで起動するため、開発者はLIFFアプリにLIFF Inspector PluginをインストールするだけでLIFFアプリをデバッグできます。詳しくは、LIFF Inspectorの[README](https://github.com/line/liff-inspector/blob/main/README_ja.md)を参照してください。

```bash
$ liff-cli serve \
   --liff-id 1234567890-AbcdEfgh \
   --url http://localhost:3000/ \
   --inspect

Successfully updated endpoint url for LIFF ID: 1234567890-AbcdEfgh.

→  LIFF URL:     https://liff.line.me/1234567890-AbcdEfgh
→  Proxy server: https://localhost:9000/?li.origin=wss%3A%2F%2Flocalhost%3A9222
Debugger listening on wss://192.168.1.6:9222

You need to serve this server over SSL/TLS
For help, see: https://github.com/line/liff-inspector#important-liff-inspector-server-need-to-be-served-over-ssltls
```

LIFF URLにアクセスすると、`serve`コマンドを実行したターミナルに`devtools://devtools/`から始まるURLが表示されます。このURLをGoogle Chromeで開くと、LIFFアプリをGoogle Chrome上でデバッグできます。

```bash
connection from client, id: 1234567890-AbcdEfgh
DevTools URL: devtools://devtools/bundled/inspector.html?wss=localhost:9222/?hi_id=1234567890-AbcdEfgh
```

### ローカル開発サーバーを外部に公開する 

LIFF CLIでは、プロキシとして[ngrok](https://ngrok.com/)をサポートしています。ngrokを使用するには、`serve`コマンドの`--proxy-type`オプションに以下のいずれかの値を指定します。

- [ngrok](https://developers.line.biz/ja/docs/liff/liff-cli/#serve-proxy-type-ngrok)
- [ngrok-v1](https://developers.line.biz/ja/docs/liff/liff-cli/#serve-proxy-type-ngrok-v1)（非推奨）

#### プロキシの種類：`ngrok` 

`--proxy-type`オプションに`ngrok`を指定すると、ローカルプロキシサーバーの代わりに[ngrok](https://github.com/ngrok/ngrok-javascript)を使うことができます。これにより、ローカルの開発サーバーを外部に公開できます。ngrokを使用する際は、環境変数として`NGROK_AUTHTOKEN`にngrokの認証トークンを設定してください。

```bash
$ NGROK_AUTHTOKEN={認証トークン} liff-cli serve \
  --liff-id 1234567890-AbcdEfgh \
  --url http://localhost:3000/ \
  --proxy-type ngrok

Successfully updated endpoint url for LIFF ID: 1234567890-AbcdEfgh.

→  LIFF URL:     https://liff.line.me/1234567890-AbcdEfgh
→  Proxy server: https://1234abcd.ngrok.example.com/
```

#### プロキシの種類：`ngrok-v1`（非推奨） 

<!-- note start -->

**ngrok-v1は非推奨です**

ngrok v1はすでに開発やメンテナンスを終了しているため、`ngrok-v1`は非推奨です。ngrokを使用する際は、プロキシの種類に[`ngrok`](https://developers.line.biz/ja/docs/liff/liff-cli/#serve-proxy-type-ngrok)を指定してください。

<!-- note end -->

`--proxy-type`オプションに`ngrok-v1`を指定すると、ローカルプロキシサーバーの代わりに[ngrok v1](https://github.com/inconshreveable/ngrok)を使うことができます。これにより、ローカル開発サーバーを外部に公開できます。なお、この機能を使うには、[ngrok v1](https://github.com/inconshreveable/ngrok)と[node-pty](https://www.npmjs.com/package/node-pty)を別途インストールする必要があります。

```bash
$ liff-cli serve \
  --liff-id 1234567890-AbcdEfgh \
  --url http://127.0.0.1:3000/ \
  --proxy-type ngrok-v1

ngrok-v1 is experimental feature.
Successfully updated endpoint url for LIFF ID: 1234567890-AbcdEfgh.

→  LIFF URL:     https://liff.line.me/1234567890-AbcdEfgh
→  Proxy server: https://1234abcd.ngrok.example.com/
```

### `serve`コマンドの動作条件 

`serve`コマンドが動作するには、次の条件をすべて満たす必要があります。

- localhostに対して有効な証明書（`localhost.pem`）と秘密鍵（`localhost-key.pem`）を作成する。
- `localhost.pem`と`localhost-key.pem`を作成した場所（例：LIFFアプリのプロジェクトのルートディレクトリ）で`serve`コマンドを実行する。

次の手順に従って、localhostに対して有効な証明書（`localhost.pem`）と秘密鍵（`localhost-key.pem`）を作成してください。ここでは[mkcert](https://github.com/FiloSottile/mkcert)を使います。mkcertについて詳しくは、mkcertの[README](https://github.com/FiloSottile/mkcert/blob/master/README.md)を参照してください。

1. 次のコマンドを実行し、`mkcert`をインストールします。

```bash
# macOSの場合（Homebrewを使用）
$ brew install mkcert

# Windowsの場合（Chocolateyを使用）
$ choco install mkcert
```

2. `mkcert -install`を実行し、ローカル認証局を作成します。

```bash
$ mkcert -install
```

3. `mkcert localhost`を実行し、localhostに対して有効な証明書（`localhost.pem`）と秘密鍵（`localhost-key.pem`）を作成します。

```bash
$ mkcert localhost
Note: the local CA is not installed in the Firefox trust store.
Run "mkcert -install" for certificates to be trusted automatically ⚠️

Created a new certificate valid for the following names 📜
 - "localhost"

The certificate is at "./localhost.pem" and the key at "./localhost-key.pem" ✅
```

### オプション 

`serve`コマンドでは、以下のオプションを利用できます。

| オプション | 必須  | 説明 |
| --- | --- | --- |
| `-l`、 `--liff-id` | ✅ | ローカル開発サーバーのLIFFアプリのLIFF IDを指定します。[デフォルトのチャネル](https://developers.line.biz/ja/docs/liff/liff-cli/#manage-channels-use)のLIFFアプリのLIFF IDのみを指定できます。 |
| `-u`、 `--url` | ✅ ※1 | ローカル開発サーバーのURLを指定します。 |
| `--host` | ✅ ※2 | ローカル開発サーバーのホストを指定します。 |
| `--port` | ✅ ※2 | ローカル開発サーバーのポート番号を指定します。 |
| `-i`、 `--inspect` |  | 指定すると、LIFF Inspectorを起動します。 |
| `--proxy-type` |  | <p>使用するプロキシの種類。以下のいずれかの値を指定します。</p><ul><li>`local-proxy`：ローカルプロキシ</li><li>`ngrok`：[ngrok](https://github.com/ngrok/ngrok-javascript)</li><li>`ngrok-v1`：[ngrok v1](https://github.com/inconshreveable/ngrok)（非推奨）</li></ul>デフォルト値は`local-proxy`です。 |
| `--ngrok-command` |  | ngrok v1を実行するコマンドを指定します。デフォルト値は`ngrok`です。 |
| `--local-proxy-port` |  | ローカル開発サーバーを対象とするローカルプロキシサーバーが待ち受けるポート番号を指定します。デフォルト値は`9000`です。 |
| `--local-proxy-inspector-port` |  | LIFF Inspector Serverを対象とするローカルプロキシサーバーが待ち受けるポート番号を指定します。デフォルト値は`9223`です。 |

※1 ローカル開発サーバーをURLで指定する場合は必須です。<br>※2 ローカル開発サーバーをホストとポート番号で指定する場合は必須です。
