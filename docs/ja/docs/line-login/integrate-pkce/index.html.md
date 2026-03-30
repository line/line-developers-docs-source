# LINEログインをPKCE対応する

## PKCEとは何か？ 

PKCE（Proof Key for Code Exchange）とは、認可コード横取り攻撃への対策を目的とし、[RFC7636](https://datatracker.ietf.org/doc/html/rfc7636)で定義されているOAuth2.0拡張仕様です。

PKCEの機構を持たないOAuth2.0の認可フローでは、悪意のあるアプリが何らかの方法で認可コードを含むカスタムURIを取得した場合、ユーザー固有のアクセストークンを横取りされる恐れがあります。LINEログインを組み込んだウェブアプリにPKCEの認可フローを導入することで、LINEログイン v2.1のセキュリティをさらに向上させ、「認可コード横取り攻撃」を防ぐことができます。

## LINEログインにPKCEを実装するメリット 

LINEログインを組み込んだウェブアプリに、PKCEを実装した場合と実装していない場合では、以下のように「認可コード横取り攻撃」に対する動作が異なります。ウェブアプリをよりセキュアにするために、PKCEの実装をおすすめします。

<table>
  <thead>
    <tr>
      <th>PKCE未実装の場合</th>
      <th>PKCE実装済みの場合</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>悪意のあるアプリが何らかの方法で認可コードを含むコールバックURLを取得した場合、アクセストークンを奪えてしまいます。<br><img style="padding-top:1em" alt="PKCE未実装の場合の認可コード横取り攻撃" src="/media/line-login/new-user-login-without-pkce-ja.svg" class="bg-border mt-3"></img></td>
      <td>悪意のあるアプリにリダイレクト時に渡される情報を横取りされても、一意の<code>code_challenge</code>を照合することでアクセストークンの横取りを防ぎます。<br><img style="padding:1em" alt="PKCE実装済みの場合の認可コード横取り攻撃" src="/media/line-login/new-user-login-with-pkce-ja.svg" class="bg-border mt-3"></img></td>
    </tr>
  </tbody>
</table>

<!-- tip start -->

**PKCEを導入するもう1つのメリット**

PKCE実装済みのLINEログインを組み込んだウェブアプリに、[**Yahoo! JAPANアプリ**](https://promo-mobile.yahoo.co.jp/yjapp/)からアクセスすると、メールアドレスとパスワードによるログインの工程をスキップできる[自動ログイン](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#line-auto-login)機能が有効になります。

![Yahoo! JAPANアプリからの自動ログイン](https://developers.line.biz/media/line-login/yja-to-line-login-ja.png)

<!-- tip end -->

## LINEログインにPKCEを実装する 

LINEログインにPKCEを実装するには、[通常のLINEログインの組み込み](https://developers.line.biz/ja/docs/line-login/integrate-line-login/)の手順に加えて以下の4つの手順を行います。

![PKCEの実装方法](https://developers.line.biz/media/line-login/new-user-login-pkce-workflow-ja.svg)

1. [`code_verifier`を生成する。](https://developers.line.biz/ja/docs/line-login/integrate-pkce/#generate-code-verifier)
2. [手順1で生成した`code_verifier`を元に`code_challenge`を生成する。](https://developers.line.biz/ja/docs/line-login/integrate-pkce/#generate-code-challenge)
3. [手順2で生成した`code_challenge`と`code_challenge_method`をクエリパラメータに付与した認可URLにユーザーをリダイレクトさせる。](https://developers.line.biz/ja/docs/line-login/integrate-pkce/#add-to-authentication-url)
4. [「アクセストークンを発行する」エンドポイントのリクエストボディに手順1で生成した`code_verifier`を加えて実行する。](https://developers.line.biz/ja/docs/line-login/integrate-pkce/#execute-issuing-access-token)

<!-- tip start -->

**PKCE対応のための新パラメータについて**

PKCE対応のために、LINEログインの「認可URL」および「アクセストークンを発行する」エンドポイントに、以下のパラメータが追加されました。

- `code_verifier`
- `code_challenge`
- `code_challenge_method`

各パラメータについて詳しくは、以下の各手順の説明を参照してください。

<!-- tip end -->

### 1. `code_verifier`の生成 

ウェブアプリ側で、ユーザーがLINEログインを実行したタイミングで、一意の`code_verifier`を生成します。`code_verifier`の仕様は[RFC7636](https://datatracker.ietf.org/doc/html/rfc7636)に準拠しています。

**パラメータ**

| パラメータ | 仕様 | 例 |
| --- | --- | --- |
| <code style="word-break: normal">code_verifier</code> | **使用可能文字種**：半角英数字（`a`〜`z`、`A`～`Z`、`0`～`9`）および記号（`-._~`）からなるランダムな文字列<br>**文字数**：43文字〜128文字 | wJKN8qz5t8SSI9lMFhBB6qwNkQBkuPZoCxzRhwLRUo1 |

**サンプルコード**

以下は、Node.jsを使った`code_verifier`の生成のサンプルコードです。

``` js
// randomAlphaNumericString()は、使用可能文字（半角英数字および記号）で構成された
// ランダムな文字列を引数に指定した整数分（43〜128）生成して返す関数を想定
const code_verifier = randomAlphaNumericString(43);
```

### 2. `code_challenge`の生成 

生成した`code_verifier`をSHA256でハッシュ化したうえで、Base64URL形式にエンコードすることで`code_challenge`を生成できます。

**パラメータ**

| パラメータ | 仕様 | 例 |
| --- | --- | --- |
| <code style="word-break: normal">code_challenge</code> | `code_verifier`をSHA256でハッシュ化したうえで、Base64URL形式にエンコードした値 | BSCQwo_m8Wf0fpjmwkIKmPAJ1A7tiuRSNDnXzODS7QI |

<!-- note start -->

**URLクエリパラメータ用に整形する**

`code_challenge`の値は、URLクエリパラメータとして利用できるように、通常のBase64形式の文字列から以下の削除・置換を行う必要があります。詳しくは、『RFC 4648』の「[5. Base 64 Encoding with URL and Filename Safe Alphabet](https://datatracker.ietf.org/doc/html/rfc4648#section-5)」を参照してください。

- パディング（文字詰めの`=`）の削除
- `+`を`-`に置換
- `/`を`_`に置換

| Base64形式の例 | `code_challenge`用に削除・置換を行った例 |
| --- | --- |
| BSCQwo_m8Wf0fpjmwk<b style="color:red">+</b>KmPAJ1A<b style="color:red">/</b>tiuRSNDnXzODS7<b style="color:red">==</b> | BSCQwo_m8Wf0fpjmwk<b style="color:red">-</b>KmPAJ1A<b style="color:red">_</b>tiuRSNDnXzODS7 |

<!-- note end -->

**サンプルコード**

以下は、Node.jsを使った`code_challenge`生成のサンプルコードです。

``` js
// このサンプルコードでは、Node.jsの"crypto"モジュールを使用しています。
// 参照：https://nodejs.org/api/crypto.html#crypto_crypto
const crypto = require("crypto");

// BASE64形式をBASE64URL形式にエンコードします。
function base64UrlEncode(str) {
    return str
        .replace(/\+/g, '-')
        .replace(/\//g, '_')
        .replace(/=/g, '');
}

// code_verifierをSHA256でハッシュ化し、BASE64URL形式にエンコードすることでcode_challengeを生成します。
const code_challenge = base64UrlEncode(crypto
    .createHash('sha256')
    .update(code_verifier)
    .digest('base64'));
```

### 3. 認可URLのクエリパラメータに`code_challenge`と`code_challenge_method`を含める 

通常のLINEログインの認可URLのクエリパラメータに`code_challenge`と`code_challenge_method`を含めます。

**パラメータ**

| パラメータ | タイプ | 必須  | 説明 |
| --- | --- | --- | --- |
| `code_challenge` | String | 任意  | [手順2](https://developers.line.biz/ja/docs/line-login/integrate-pkce/#generate-code-challenge)で生成した`code_challenge`。デフォルト値は`null`です（値を指定しない場合、リクエストはPKCE対応されません）。 |
| <code style="word-break: normal">code_challenge_method</code> | String | 任意  | `S256`（ハッシュ関数`SHA256`を表します。）<br><br>注：[RFC7636の「4.2.  Client Creates the Code Challenge」](https://datatracker.ietf.org/doc/html/rfc7636#section-4.2)では、`code_challenge`の生成方法として、`S256`以外に`plain`（変換なし）が定義されていますが、LINEログインではセキュリティ上の観点から`S256`のみをサポートしています。 |

**認可URLの例**

```sh
https://access.line.me/oauth2/v2.1/authorize?response_type=code&client_id=1234567890&redirect_uri=https%3A%2F%2Fexample.com%2Fauth%3Fkey%3Dvalue&state=12345abcde&scope=profile%20openid&nonce=09876xyz
&code_challenge={手順2で算出したcode_challengeの値}&code_challenge_method=S256
```

認可URLのその他のクエリパラメータについて詳しくは、「[ユーザーに認証と認可を要求する](https://developers.line.biz/ja/docs/line-login/integrate-line-login/#making-an-authorization-request)」を参照してください。

### 4. リクエストボディに`code_verifier`を指定してアクセストークンを発行する 

「[アクセストークンを発行する](https://developers.line.biz/ja/reference/line-login/#issue-access-token)」エンドポイントのリクエストボディに、`code_verifier`を指定して実行します。

**リクエストボディ**

<!-- parameter start (props: optional) -->
code_verifier
String

[手順1](https://developers.line.biz/ja/docs/line-login/integrate-pkce/#generate-code-verifier)で生成した`code_verifier`<br>（例：`wJKN8qz5t8SSI9lMFhBB6qwNkQBkuPZoCxzRhwLRUo1`）

<!-- parameter end -->

**リクエストの例**

```sh
curl -v -X POST https://api.line.me/oauth2/v2.1/token \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=authorization_code' \
-d 'code=1234567890abcde' \
--data-urlencode 'redirect_uri=https://example.com/auth?key=value' \
-d 'client_id=1234567890' \
-d 'client_secret=1234567890abcdefghij1234567890ab' \
-d 'code_verifier={手順1で生成したcode_verifier}'
```

「アクセストークンを発行する」エンドポイントについて詳しくは、『LINEログイン v2.1 APIリファレンス』の「[アクセストークンを発行する](https://developers.line.biz/ja/reference/line-login/#issue-access-token)」を参照してください。
