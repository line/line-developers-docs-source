# チャネルアクセストークンv2.1を発行する

LINEプラットフォームでは、[4種類のチャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/#channel-access-token-types)が利用可能です。このうち、チャネルアクセストークンv2.1とステートレスチャネルアクセストークンは、JSON Web Token（JWT）を用いて生成することができます。

このページでは、アサーション署名キーの仕様と、署名キーからJWTを生成する方法、また生成したJWTを用いてチャネルアクセストークンを発行する方法について、チャネルアクセストークンv2.1を対象に説明します。

## チャネルアクセストークンv2.1の発行手順 

チャネルアクセストークンv2.1の発行手順は下図のとおりです。この図は、次の3つの手順を表しています。

- [アサーション署名キーを発行する](https://developers.line.biz/ja/docs/messaging-api/generate-json-web-token/#create-an-assertion-signing-key) （図の手順1）
- [JWTを生成する](https://developers.line.biz/ja/docs/messaging-api/generate-json-web-token/#generate-jwt) （図の手順6）
- [チャネルアクセストークンv2.1を発行する](https://developers.line.biz/ja/docs/messaging-api/generate-json-web-token/#issue_a_channel_access_token_v2_1) （図の手順7）

![](https://developers.line.biz/media/messaging-api/channel-access-token/channel-access-token-issue-flow.svg)

<!-- tip start -->

**チャネルアクセストークンv2.1の仕様**

チャネルアクセストークンv2.1の発行における認証方式は[「Using JWTs as Authorization Grants」（RFC 7523）](https://datatracker.ietf.org/doc/html/rfc7523#section-2.1)に準拠しています。これは[OAuth Assertion Framework（RFC 7521）](https://datatracker.ietf.org/doc/html/rfc7521#section-4.1)のAssertion Frameworkにおいて[JSON Web Token（RFC 7519）](https://datatracker.ietf.org/doc/html/rfc7519)を利用したものです。

<!-- tip end -->

## アサーション署名キーを発行する 

アサーション署名キーの発行は、次の2つの手順で行います。

- [1. アサーション署名キーのキーペアを生成する](https://developers.line.biz/ja/docs/messaging-api/generate-json-web-token/#generate-a-key-pair-for-the-assertion-signing-key)
- [2. 公開鍵を登録し、`kid`を取得する](https://developers.line.biz/ja/docs/messaging-api/generate-json-web-token/#register-public-key-and-get-kid)

### 1. アサーション署名キーのキーペアを生成する 

JWTを生成するには、アサーション署名キーのキーペア（秘密鍵・公開鍵）をあらかじめ生成する必要があります。

#### アサーション署名キーの仕様 

以下の基準を満たす[JSON Web Key（RFC7517）](https://datatracker.ietf.org/doc/html/rfc7517)をJWTのアサーション署名キーとして利用できます。

1. RSA公開鍵である（`kty`プロパティに`RSA`が設定されている）こと。
2. RSA鍵長が2048bitであること。
3. 署名アルゴリズムにRS256（RSASSA-PKCS1-v1_5 with SHA256）が使われている（`alg`プロパティに`RS256`が設定されている）こと。
4. 公開鍵を署名に利用することが明示されている（`use`や`key_ops`が下表のように設定されている）こと。

したがって、アサーション署名キーの公開鍵には、以下のフィールドが含まれている必要があります。

| プロパティ | 説明 |
| --- | --- |
| `kty` | 鍵で使用される暗号アルゴリズムファミリー。`RSA`を指定してください。 |
| `alg` | 鍵で使用されるアルゴリズム。`RS256`を指定してください。 |
| `use`<sup>\*1</sup> | 鍵の用途。`sig`を指定してください。 |
| `key_ops`<sup>\*1</sup> | 鍵の利用が想定されているオペレーション。`["verify"]`のみを指定してください。 |
| `e` | 公開鍵を復元するための絶対値 |
| `n` | 公開鍵を復元するための暗号指数 |

\*1 `use`か`key_ops`のいずれかを指定してください。

<!-- note start -->

**公開鍵を登録する前に確認すること**

登録する公開鍵に`kid`プロパティがないことを確認してください。アサーション署名キーの公開鍵に`kid`プロパティが含まれているとエラーになります。これは`kid`がLINE Developersコンソールで公開鍵を登録したときにのみ発行されるためです。

<!-- note end -->

アサーション署名キーのキーペアは、公開仕様をもとに開発者が自らプログラムを作成して生成することもできますが、仕様を満たすライブラリ等を利用するとより簡単に生成できます。

以下、アサーション署名キーを生成する手順の例を紹介します。

- [jwx（Go言語のライブラリ）でキーペアを生成する](https://developers.line.biz/ja/docs/messaging-api/generate-json-web-token/#use-go-lang)
- [JWCrypto（Pythonのライブラリ）でキーペアを生成する](https://developers.line.biz/ja/docs/messaging-api/generate-json-web-token/#use-python)
- [ブラウザでキーペアを生成する](https://developers.line.biz/ja/docs/messaging-api/generate-json-web-token/#use-browser)

#### jwx（Go言語のライブラリ）でキーペアを生成する 

[jwxコマンドラインツール](https://github.com/lestrrat-go/jwx/tree/develop/v2/cmd/jwx)でキーペアを生成できます。このコマンドラインツールは、オープンソースのGo言語ライブラリである[jwx](https://github.com/lestrrat-go/jwx)の一部で、JWTの実装に使用されます。Go言語の開発環境が整っていない場合は、[Go言語の公式サイト](https://go.dev/doc/install)からGoをダウンロードしてください。

以下の手順でアサーション署名キーを発行してください。

##### 1. jwxコマンドラインツールをインストールする 

以下のコマンドを実行し、jwxコマンドラインツールをインストールします。

```sh
$ git clone https://github.com/lestrrat-go/jwx.git
$ cd jwx
$ make jwx
```

インストール完了後、jwxコマンドラインツールがインストールされたパスが表示されます。

```
// インストールされたパスの表示例
Installed jwx in {インストールされたパス}
```

以降の手順でコマンドが実行できるよう、パスの設定を行ってください。

##### 2. 秘密鍵と公開鍵を生成する 

以下のコマンドを実行し秘密鍵を生成します。

```sh
$ jwx jwk generate --type RSA --keysize 2048 --template '{"alg":"RS256","use":"sig"}' > private.key
```

秘密鍵をもとに公開鍵を生成します。

```sh
$ jwx jwk format --public-key private.key > public.key
```

成功すると以下のような秘密鍵と公開鍵が生成されます。

**秘密鍵の例：**

```json
{
  "alg": "RS256",
  "d": "JeSJWnvZ......",
  "dp": "gBDRXGg7......",
  "dq": "MjFJ4xM9......",
  "e": "AQ......",
  "kty": "RSA",
  "n": "pTS2jGso......",
  "p": "xQibzkW6......",
  "q": "1qWtyQ9s......",
  "qi": "sdVGblc......",
  "use": "sig"
}
```

**公開鍵の例：**

```json
{
  "alg": "RS256",
  "e": "AQ......",
  "kty": "RSA",
  "n": "pTS2jGso......",
  "use": "sig"
}
```

#### JWCrypto（Pythonのライブラリ）でキーペアを生成する 

JWTを実装するためのオープンソースのPythonライブラリである[JWCrypto](https://github.com/latchset/jwcrypto)でキーペアを生成できます。JWCryptoを使用するには、Python3とpipがインストールされている必要があります。Python3がインストールされていない場合は、[Pythonの公式サイト](https://www.python.org/downloads/)からお使いのOSに対応したインストーラーをダウンロードし、インストールを進めてください。Python3がインストールされると、pipもインストールされます。Python3はインストールされているがpipがインストールされていない場合は、『[pip documentation](https://pip.pypa.io/en/stable/installation/)』を参照し、インストールしてください。

以下の手順でアサーション署名キーを発行してください。

##### 1. JWCryptoをインストールする 

以下のコマンドを実行しJWCryptoをインストールします。

```python
$ pip install jwcrypto
```

##### 2. 秘密鍵と公開鍵を生成するコードを書く 

以下のように、`kty`を`RSA`、`alg`を`RS256`、`use`を`sig`、`size`を`2048`として引数に指定して、秘密鍵と公開鍵を生成するpythonファイルを作成します。

```python
from jwcrypto import jwk
import json
key = jwk.JWK.generate(kty='RSA', alg='RS256', use='sig', size=2048)

private_key = key.export_private()
public_key = key.export_public()

print("=== private key ===\n"+json.dumps(json.loads(private_key),indent=2))
print("=== public key ===\n"+json.dumps(json.loads(public_key),indent=2))
```

pythonファイルは任意のファイル名で保存してください。ここでは、`app.py`とします。

保存したpythonファイルと同じディレクトリで、以下のコマンドを実行し、秘密鍵をもとに公開鍵を生成します。

```sh
$ python app.py
```

成功すると以下のような秘密鍵と公開鍵が標準出力されます。

**秘密鍵の例：**

```json
{
  "alg": "RS256",
  "d": "zKh7iwIIPXXFKYQS...",
  "dp": "u1qKg_43UeuGpZFI...",
  "dq": "69AzYgpcg0ckypUrv...",
  "e": "AQ..",
  "kty": "RSA",
  "n": "_RzHf7cgG_i6Pdo_...",
  "p": "_20iRavoSrMIwWuRPxo...",
  "q": "_a5QodMBbEriAgztXvHi...",
  "qi": "JozdjTtK57IFLeVAB...",
  "use": "sig"
}
```

**公開鍵の例：**

```json
{
  "alg": "RS256",
  "e": "AQAB",
  "kty": "RSA",
  "n": "_RzHf7cgG_i6Pdo...",
  "use": "sig"
}
```

#### ブラウザでキーペアを生成する 

[Web Crypto API](https://developer.mozilla.org/ja/docs/Web/API/Web_Crypto_API)に対応しているウェブブラウザを使用している場合、[`SubtleCrypto.generateKey()`](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/generateKey)メソッドを使って秘密鍵と公開鍵を生成できます。たとえば、Google Chromeを使用している場合は、Chromeのデベロッパーツールのコンソールから以下のコードを入力して実行します。

```javascript
(async () => {
  const pair = await crypto.subtle.generateKey(
    {
      name: "RSASSA-PKCS1-v1_5",
      modulusLength: 2048,
      publicExponent: new Uint8Array([1, 0, 1]),
      hash: "SHA-256",
    },
    true,
    ["sign", "verify"],
  );

  console.log("=== private key ===");
  console.log(
    JSON.stringify(
      await crypto.subtle.exportKey("jwk", pair.privateKey),
      null,
      "  ",
    ),
  );

  console.log("=== public key ===");
  console.log(
    JSON.stringify(
      await crypto.subtle.exportKey("jwk", pair.publicKey),
      null,
      "  ",
    ),
  );
})();
```

成功すると以下のような秘密鍵と公開鍵が生成されます。

**秘密鍵の例：**

```json
{
  "alg": "RS256",
  "d": "GaDzOmc4......",
  "dp": "WAByrYmh......",
  "dq": "WLwjYun0......",
  "e": "AQ......",
  "ext": true,
  "key_ops": [
    "sign"
  ],
  "kty": "RSA",
  "n": "vsbOUoFA......",
  "p": "5QJitCu9......",
  "q": "1ULfGui5......",
  "qi": "2cK4apee......"
}
```

**公開鍵の例：**

```json
{
  "alg": "RS256",
  "e": "AQ......",
  "ext": true,
  "key_ops": [
    "verify"
  ],
  "kty": "RSA",
  "n": "vsbOUoFA......"
}
```

### 2. 公開鍵を登録し、`kid`を取得する 

キーペアを生成したら、[LINE Developersコンソール](https://developers.line.biz/console/)に公開鍵を登録し、`kid`を取得します。公開鍵を登録するには、コンソールにアクセスし、自分のチャネルのチャネル設定を開きます。［**チャネル基本設定**］タブをクリックし、次に、アサーション署名キーの横にある［**公開鍵を登録する**］ボタンをクリックします。公開鍵を入力し、［**登録**］ボタンで登録を確定します。

公開鍵の登録に成功すると、`kid`を取得できます。

## JWTを生成する 

JWTは、ヘッダー、ペイロード、署名からなる文字列です。すべての項目が必須フィールドです。JWTを生成するには、任意の[JWTライブラリ](https://www.jwt.io/ja/libraries)を使用することもできますし、アサーション署名キーを使って独自のコードをスクラッチで書くこともできます。

### ヘッダー 

ヘッダーには以下のプロパティを含める必要があります。

| プロパティ | 型 | 説明 |
| --- | --- | --- |
| `alg` | String | JWT生成のアルゴリズム。`RS256`を指定します。 |
| `typ` | String | トークンのタイプ。`JWT`を指定します。 |
| `kid` | String | キーID。「[2. 公開鍵を登録し、kidを取得する](https://developers.line.biz/ja/docs/messaging-api/generate-json-web-token/#register-public-key-and-get-kid)」で取得した`kid`の値を指定します。 |

以下は、ヘッダーの値をデコードした例です。

```json
{
  "alg": "RS256",
  "typ": "JWT",
  "kid": "536e453c-aa93-4449-8e90-add2608783c6"
}
```

### ペイロード 

ペイロードには以下のプロパティを含める必要があります。

| プロパティ | タイプ | 説明 |
| --- | --- | --- |
| `iss` | String | チャネルID。[LINE Developersコンソール](https://developers.line.biz/console/)で取得できます。このプロパティの値は`sub`と同じにする必要があります。 |
| `sub` | String | チャネルID。[LINE Developersコンソール](https://developers.line.biz/console/)で取得できます。このプロパティの値は`iss`と同じにする必要があります。 |
| `aud` | String | `https://api.line.me/`を指定します。 |
| `exp` | Number | JWTの有効期限をUNIX時間（秒）で指定します。JWTアサーションの最大有効期間は30分です。 |
| `token_exp` | Number | チャネルアクセストークンの有効期間を秒単位で指定します。チャネルアクセストークンの最大有効期間は30日です。 |

以下は、デコードされたペイロードの例です。

```json
{
  "iss": "1234567890",
  "sub": "1234567890",
  "aud": "https://api.line.me/",
  "exp": 1559702522,
  "token_exp": 86400
}
```

### 署名 

JWTを生成するには、ヘッダーとペイロードに署名する必要があります。[node-jose](https://developers.line.biz/ja/docs/messaging-api/generate-json-web-token/#jwt-use-nodejs)（Node.jsのライブラリ）または[PyJWT](https://developers.line.biz/ja/docs/messaging-api/generate-json-web-token/#jwt-use-python)（Pythonのライブラリ）を利用して、署名を作成し、それを使ってJWTを生成する方法を説明します。

#### node-jose（Node.jsのライブラリ）でJWTを生成する 

Node.jsのライブラリであるnode-joseを使って署名を作成し、JWTを生成するには、[Node.js](https://nodejs.org/en)と[node-jose](https://github.com/cisco/node-jose#installing)がインストールされていることを確認してください。

以下は、node-joseを使って**秘密鍵**で署名してJWTを生成するコードの例です。このコードを使って自分のJWTを生成する場合は、`privateKey`を自分のアサーション署名キーの**秘密鍵**の値に変更し、`header`と`payload`の値をそれぞれ変更してから実行します。内容が改ざんされていないことを証明するために、必ず**秘密鍵**で署名します。node-joseの使い方について詳しくは、[node-jose](https://github.com/cisco/node-jose#installing)を参照してください。

```javascript
let jose = require("node-jose");

let privateKey = `
{
    "p": "4h8yEw4q9VkzhXMgXZsIZVkEuZ49EmtWYk9zs0hPTa24ejjRMA6KTYh_va0GlaChO9t0MVQVuduznt-OFZyRAinr4svU4MKD2A3gTHJJCxs0xICva8rkHXqxfPwXngpb5L_xFURbXcSTzMcKckWuOpyPznAgY4XsZxw0t7ewj9E",
    "kty": "RSA",
    "q": "pVhBdRN5K3MEiZzU4__TsrtSBJDD_stu60m73iIvsHIrvK3Dmfl-J1zhsyOvi3NH9mVXpUimBwP8nTe-BlVM71G7_EotFHeKH1zTmBlx6AOngmrc40W2Hd__OZW0NfC_xOTvI_Ea2BNGoGtcrIGVFLTivJ4y9wAVOKA058zJ0ls",
    "d": "ObzE_-TROJazDm-ry-8TKRBMGzwcwTK6lMFSk7n-Xp6h7cDauSdRRYnZivC1lh5plVG3I9aUmPTRbVk7nrPqOlp4WWKQ27lyLd5IogbArpXgnBSkp9Zy0lWzvOsI3gHNnYuehyksHB53FIK93t838JfDQoXUUzalNoNwAGfkTNZxT4GIXGMGzNck2Z_urOATMf8-wdad-u4a5IB2KfHugwH2kw-Zig7fbdcN4_DeKWpuigdesa48Yj_hRJRws-mVFp-xHlGJehumnM_v8FLD85ap8L1hwvBqdJQeurcLXYzZbtdp9a5GpJI7gzOTMoEdxIKlEIIbaOKv4rkkztdhoQ",
    "e": "AQAB",
    "use": "sig",
    "kid": "536e453c-aa93-4449-8e90-add2608783c6",
    "qi": "XQ2puK9LT5yimyJXlXb4nHEBzPGe3sYbaZW_gMK4iHuM8cseImwLNP8ZIeGaNx5X_hZ6ZOzkjtYJjY85fvaWa2UDGdGlEw3ZO-Nk0Qu_exBrqZgZAsua75TjpJRw01Yd1TNBx5MYuvhltJLsjW-uSjcE-rZoO74FEe9pYYeQjI4",
    "dp": "Qq_wlK4Y_ULRbwoFAZY3Y6xdOGDyofwF_fhwpu8sdDxHq8QV7ZZcM4GOKuJcjsRQyNZv7hxeS_H_h1tnC_igy4KRjtGOdrrnJ1DwVZte72eWqF1LXv73R7pnnfS7AmELuOriruL6Dy1qaXpKGmlyeNazkq5-3tsgXUh0Q7po2AE",
    "alg": "RS256",
    "dq": "Wj1ovDT8lLIZb-Ggby9YotuJT-SSk6UDzHZZikquLGajaD6N2qNILsOKivKXBEzOobN9uj-EHaAXZtbdZyd27cZ2CqORJvJ299b5xLFecXpNGeio1YFee7-c1BjYWfgjMZqgycT1GairizINSjkO3FY8ySSuPBBXhKgrN7eVDrE",
    "n": "kgwP0NPaoAwhSh9iLlRaT7FSRbNsl6T5-j-bB3xAT1UbsxOJ9v06S3_54bpYlEAkjlrO-i1vmSzfSVnqFXnjWThWRvPmBDth3Ka7hQm9UXjiAvTzYxXGFjyhALqa_-DQCtdrqIhi8E4hAuSu--kGgnFKg3G-21KJuqnVzsXrClGkxbmVufx0MJjJxr1YGfkTMG8i0dovS9tnkioDAkt1knupiYk5ir_WiNy4T-70T5s3ktC5_4Uz10hS-rWeUxiihzG8G7ceg84-Kt5jKP_AgUnel-ksRyfgSJCYC9nHyz913a3ALj3Dzt7TBaxwAjlxESrdNz5RE9DNDZfPmNWRSw"
  }
`;

let header = {
  alg: "RS256",
  typ: "JWT",
  kid: "536e453c-aa93-4449-8e90-add2608783c6",
};

let payload = {
  iss: "1234567890",
  sub: "1234567890",
  aud: "https://api.line.me/",
  exp: Math.floor(new Date().getTime() / 1000) + 60 * 30,
  token_exp: 60 * 60 * 24 * 30,
};

jose.JWS.createSign(
  { format: "compact", fields: header },
  JSON.parse(privateKey),
)
  .update(JSON.stringify(payload))
  .final()
  .then((result) => {
    console.log(result);
  });
```

Base64形式でエンコードされたヘッダーとクレーム・セット、および秘密鍵（rsa_private.pemファイルなど）を、ヘッダーで定義したアルゴリズムを使用して署名します。署名後、Base64形式でエンコードされた結果がJWTです。以下はJWTの例です。

```sh
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IjJjNjU4NWYzLThkZGQtNDZjNC05YmUyLWI1NGE3MGFhOTRlYSJ9.eyJpc3MiOiIxNjUzOTQ3MTcyIiwic3ViIjoiMTY1Mzk0NzE3MiIsImF1ZCI6Imh0dHBzOi8vYXBpLmxpbmUubWUvIiwiZXhwIjoiMTU4NTIwMDA2MiIsInRva2VuX2V4cCI6IjI1OTIwMDAifQ.UVG6PAEub-OPbZ3nJuVxRRPjY6Sz_eIHJV9DTTAHCR79YsG4yWvoa9AeIctibb6IJQKgTEV7mF7LsUDmXldEDqYwyEmKs38zj_995Ntc9SYBFphHpr09NqfMoqMphwKqms2NOnqgcHreFs27d9Q0Qv8Rtv2t7SB2cVO__KrsjzYNs3miTvDdkqYLXFo5fXwuzNtHOCAJomd6bhMR8Yd1-vJmtMCBPK4hmA98w8fG_NhcyLbw-B9AuxQ6z92zXiRhNyPlK_3ce2T7HtgUluJ4xJl4xdLJ_C6hvTAqtQxmSiJKzbjUiANF6hVBTomU8vkaIjEKjnlT1uPMihfrsA3pzQ
```

#### PyJWT（Pythonのライブラリ）でJWTを生成する 

PyJWTを使って署名し、JWTを生成するには、[Python](https://www.python.org/downloads/)と[PyJWT](https://github.com/jpadilla/pyjwt)がインストールされている必要があります。

以下は、PyJWTを使って**秘密鍵**で署名してJWTを生成するコードの例です。このコードを使って自分のJWTを作成する場合は、`privateKey`を自分のアサーション署名キーの**秘密鍵**の値に変更し、`headers`の`kid`と`payload`の値をそれぞれ変更してから実行します。コンテンツが改ざんされていないことを証明するために、必ず**秘密鍵**で署名します。PyJWTの使い方について詳しくは、[PyJWT](https://github.com/jpadilla/pyjwt#installing)を参照してください。

```python
import jwt
from jwt.algorithms import RSAAlgorithm
import time

privateKey = {
  "alg": "RS256",
  "d": "dcA-LXLBRecBQbW7a8LKAriFJhnpXzwu2uNoVF_8-QmGVzI5682FWh_CWhl_B6J0fpmA-d7_EP0WCB3AGhxlyTP6ROoYJo7nygb_KMLREM7n64LFGbvNtw4jk7dmISXl_JuEX6CG09BBx4GLh9AGHSaK4v9B-dDvrNZlAo2mIjISHNcAPENbOl_XIOmZpJd56znjjc1gGKaYGbIm8unxHnPhL66IVYGRu8gxKfG6JUP7o370-VDfFOeaAR0HshTycP6M41jcDSjL6z9-J-Sh0zSZXqGS4u82TNtmwtRTzVwd0w30KQ0TTROTiNsz5apVHjpMvmAxRlbvcW41xIq8sQ",
  "dp": "PAWBMzwnwgc-yixarV30gemH6Wk15HfSUYpR4wJZUHemGx_LE5GXdnKoyy8G9DAl6XMpm7YVH8cPXgXYNh-JlAggvzUeH5A7KAV4ZPTNak4CI844GSbYIu_dPBcVAg0O6sxQWugYpPbPnMDpE7qf4KilSSVG3JKqEMxkYySjZZE",
  "dq": "LBA_q2YYnglCL41-1b3BmzCm-hs7Q-N__otDWO01I03VYnzU-vEQmxy6Fzrh2Y4Fgwp6D8iScu42AOyhE-T-qDNbAsCB0iZeFqm84g6VQAfDbknjIUZtcGvQgzy-zlrl253_QdyJvl2b44KT1hfoF0tDNA1rhOy7WlBM__rH0Pc",
  "e": "AQAB",
  "kty": "RSA",
  "n": "x2glWJ7baQV4vdElnAXA5yu8yFk4LpszkHW3Ey-BKGT3kGVLy3Jk3OvkwjBFOglXWeyTWe_rJkMYkBKuon5syZVjrjb24CmViAXGr6d6IvrYWj8IGZ6ElVABfnjGgZMVywmBb7hIh2p8QR0L8UJEuWjBU5nlwkMBpvnY2HXAVhvir8CN7WRj_GBMxxgg7wSuW1tV-7Qf44grMqJ0Je7zjflS4-TpI8Ox3nhamn0d7NIdQ3jNdTP7IZF61IvETgb_6NdFnfsN-aifJC-Ea3ZwhVcEGJ5z3MMoKSoChJmkJMiV9CldqGRnEDWwBugZHeEtn71eGVE3DAXAzrf525YHYQ",
  "p": "7eH8LAzNkITH6t7CWU5tPAmQlGQPkby66Yfq52tSZ43pQRz0CdtDYCQnGoBXvHzAHhzH4MjmNLOSGVimZK_dIRg5lJaPvVe6hgQ3pYud5WzPWsnQTsC7agQ2rfQglyFUtjwd1gWBIY4gwHj4BYG6Up3g0TlX1sf_juZxcLhkOsc",
  "q": "1pf-Pj2ZPL1nGqVcMVH_hfziIOBtjxc5vMGyHwTaLAA9y2xKfe_SRU8kUK2q5ZykJ8wMckR9Pduuyn-vp4q2FANVSN69G01pUKM2ppkgXuil2S3REmzniGdajZjkpWKaZ6z1tJ_xSv9ghx06Dbro8n___KnpBq6afb022anRxJc",
  "qi": "6L6SgH_pkyqq1Tb6QXPAGmtqVZT58Ljf3QTw6Tx5OdZ9NNvDReHHb64MgbUMLhLzGMeXGqDI5j0WLhtXv4ddCKWkF7OeKLUNuRP7yLpyYMazn8TEOjKHsgLAklenxcSgYaoO_wULh1mze1_ZO2PJNgvkIx_Xzr0XDUAqUp4W0jk",
  "use": "sig"
}

headers = {
    "alg": "RS256",
    "typ": "JWT",
    "kid": "9869e446-3489-4516-a83f-ec9214ad94d0"
}

payload = {
  "iss": "1234567890",
  "sub": "1234567890",
  "aud": "https://api.line.me/",
  "exp":int(time.time())+(60 * 30),
  "token_exp": 60 * 60 * 24 * 30
}

key = RSAAlgorithm.from_jwk(privateKey)

JWT = jwt.encode(payload, key, algorithm="RS256", headers=headers, json_encoder=None)
print(JWT)
```

Base64形式でエンコードされたヘッダーとクレーム・セット、および秘密鍵を、ヘッダーで定義したアルゴリズムを使用して署名します。署名後、Base64形式でエンコードされた結果がJWTです。以下はJWTの例です。

```sh
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ijk4NjllNDQ2LTM0ODktNDUxNi1hODNmLWVjOTIxNGFkOTRkMCJ9.eyJpc3MiOiIxMjM0NTY3ODkwIiwic3ViIjoiMTIzNDU2Nzg5MCIsImF1ZCI6Imh0dHBzOi8vYXBpLmxpbmUubWUvIiwiZXhwIjoxNjIzOTk1NTk5LCJ0b2tlbl9leHAiOjI1OTIwMDB9.Zf32xTqgUHSYw2C2Mlmunqz_AtkaqvGh0msx9XJMX6QYLPT4m4QYF3PsER-zfbhbByNT4rH09JEMRP7bzcNMQ8l4n_WXwTyLkNciZYzF-sTiVHiZu4ucJm4_l8ni5NaqOVEntsCp1wQi8-VLjaMpQlQ7crCdouEMFFeyVwgERfH8ui6UZaJeIlJKRZTnO6iYvKYuLyUsqzowfwZo0hcnnZIXKnjZ81ukjH3_78EHXOD5ivovAT7CtmBoglm3Bvsi0N6PlEONLhHqpCleaYTXRmCykxDLP600JRvi5TYApaN-8n2Bo3FskXJLuxquWLP-LTfMDlkakmfEfcQCiz7daQ
```

## チャネルアクセストークンv2.1を発行する 

[生成した](https://developers.line.biz/ja/docs/messaging-api/generate-json-web-token/#generate-jwt)JWTアサーションを指定して、[チャネルアクセストークンv2.1を発行](https://developers.line.biz/ja/reference/messaging-api/#issue-channel-access-token-v2-1)できます。

<!-- note start -->

**キーIDを使ってチャネルアクセストークンv2.1を管理する**

- チャネルアクセストークンv2.1をリクエストすると、チャネルアクセストークンと一意のキーID（`key_id`）のペアがレスポンスとして返されます。チャネルアクセストークンを適切に管理するため、チャネルアクセストークンとキーIDのペアを安全に保管するようにしてください。
- キーIDは、2020年6月22日にMessaging APIに追加された識別子です。キーIDを持たないチャネルアクセストークンv2.1を使用している場合は、チャネルアクセストークンv2.1を再発行し、トークンとキーIDのペアを保管することをお勧めします。チャネルアクセストークンを再発行した場合は、新しいトークンを使用するようにボットを更新してください。

<!-- note end -->

チャネルアクセストークンv2.1を取得する手順は以下のとおりです。

![](https://developers.line.biz/media/messaging-api/channel-access-token/using_keyID_procedure_01.png)

1. 生成したJWTを指定して、[チャネルアクセストークンv2.1を発行する](https://developers.line.biz/ja/reference/messaging-api/#issue-channel-access-token-v2-1)エンドポイントを実行し、チャネルアクセストークンを発行します。
2. チャネルアクセストークンとキーIDがLINEプラットフォームから返ります。
3. チャネルアクセストークンとキーIDをペアにしてデータベースなどに保管します。

### チャネルアクセストークンv2.1を取り消す 

[チャネルアクセストークンv2.1を取り消す](https://developers.line.biz/ja/reference/messaging-api/#revoke-channel-access-token-v2-1)エンドポイントを実行することで、有効なチャネルアクセストークンを取り消すことができます。

<!-- note start -->

**有効なチャネルアクセストークンの識別**

無効なチャネルアクセストークンを指定して、[チャネルアクセストークンv2.1を取り消す](https://developers.line.biz/ja/reference/messaging-api/#revoke-channel-access-token-v2-1)エンドポイントを実行した場合も、エラーレスポンスは発生しません。[すべての有効なチャネルアクセストークンv2.1のキーIDを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-all-valid-channel-access-token-key-ids-v2-1)エンドポイントを使って、現在有効なチャネルアクセストークンとペアになるキーIDを取得できます。取得したキーIDを、データベースなどに保管したチャネルアクセストークンとキーIDのペアと照合することで、有効なチャネルアクセストークンを識別できます。

<!-- note end -->

チャネルアクセストークンv2.1を取り消す手順は以下のとおりです。

![](https://developers.line.biz/media/messaging-api/channel-access-token/using_keyID_procedure_02.png)

1. 保存したアサーション署名キーからJWTを再生成します。
2. JWTを使って[すべての有効なチャネルアクセストークンv2.1のキーIDを取得する](https://developers.line.biz/ja/reference/messaging-api/#get-all-valid-channel-access-token-key-ids-v2-1)エンドポイントを実行します。
3. 有効なチャネルアクセストークンのキーIDがLINEプラットフォームから返ります。
4. 取得したキーIDをデータベースと照合します。
5. 取得したキーIDと一致する、チャネルアクセストークンとキーIDのペアがあるかどうかを確認します。
6. 有効なチャネルアクセストークンを取得します。
7. 有効なチャネルアクセストークンを指定して、[チャネルアクセストークンv2.1を取り消す](https://developers.line.biz/ja/reference/messaging-api/#revoke-channel-access-token-v2-1)エンドポイントを実行します。
8. LINEプラットフォームによってチャネルアクセストークンが取り消されます。
