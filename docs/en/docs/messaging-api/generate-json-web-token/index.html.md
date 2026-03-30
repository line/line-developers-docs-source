# Issue channel access token v2.1

There are [four types of channel access tokens](https://developers.line.biz/en/docs/basics/channel-access-token/#channel-access-token-types) available on the LINE Platform. Of these, channel access tokens v2.1 and stateless channel access tokens can be generated using JSON Web Token (JWT).

This page explains how to specify an assertion signing key, how to generate a JWT from a signing key, and how to issue a channel access token using the generated JWT, targeting channel access tokens v2.1.

## Process of issuing a channel access token v2.1 

The process of issuing a channel access token v2.1 is illustrated in the diagram below. This diagram shows the following three steps:

- [Create an assertion signing key](https://developers.line.biz/en/docs/messaging-api/generate-json-web-token/#create-an-assertion-signing-key) (Step 1 in the diagram)
- [Generate a JWT](https://developers.line.biz/en/docs/messaging-api/generate-json-web-token/#generate-jwt) (Step 6 in the diagram)
- [Issue a channel access token v2.1](https://developers.line.biz/en/docs/messaging-api/generate-json-web-token/#issue_a_channel_access_token_v2_1) (Step 7 in the diagram)

![](https://developers.line.biz/media/messaging-api/channel-access-token/channel-access-token-issue-flow-en.svg)

<!-- tip start -->

**Channel access token v2.1 specification**

The authentication method for issuing a channel access token v2.1 is in accordance with [Using JWTs as Authorization Grants (RFC 7523)](https://datatracker.ietf.org/doc/html/rfc7523#section-2.1). This is the Assertion Framework of [OAuth Assertion Framework (RFC 7521)](https://datatracker.ietf.org/doc/html/rfc7521#section-4.1) using [JSON Web Token (RFC 7519)](https://datatracker.ietf.org/doc/html/rfc7519).

<!-- tip end -->

## Create an assertion signing key 

Issuing an assertion signing key is done in the these two steps:

- [1. Generate a key pair for the assertion signing key](https://developers.line.biz/en/docs/messaging-api/generate-json-web-token/#generate-a-key-pair-for-the-assertion-signing-key)
- [2. Register public key and get `kid`](https://developers.line.biz/en/docs/messaging-api/generate-json-web-token/#register-public-key-and-get-kid)

### 1. Generate a key pair for the assertion signing key 

To create a JWT, you must first create an assertion signing key pair (private key, public key).

#### Assertion signing key specification 

You can use a [JSON Web Key (RFC7517)](https://datatracker.ietf.org/doc/html/rfc7517) that meets these criteria as an assertion signing key for JWT.

- The key must be an RSA public key. (Set the `kty`property to `RSA`)
- The RSA key must be 2048 bits long.
- Use RS256 (RSASSA-PKCS1-v1_5 with SHA256) as the signing algorithm. (Set the `alg` property to `RS256`)
- State that the public key is for signing. (Set `use` or `key_ops` as instructed in the table below).

Therefore, the public key of the assertion signing key must contain these properties:

| Property | Description |
| --- | --- |
| `kty` | Cryptographic algorithm family used in key. Set to `RSA`. |
| `alg` | Algorithm used in the key. Set to `RS256`. |
| `use`<sup>\*1</sup> | Usage of the key. Set to `sig`. |
| `key_ops`<sup>\*1</sup> | Operation for the key to be used. Set to `["verify"]` only. |
| `e` | Absolute value for restoring public key |
| `n` | Cryptographic index for restoring public key |

\*1 Specify either one of `use` or `key_ops`.

<!-- note start -->

**Check before you register a public key**

Make sure the public key you register doesn't have the `kid` property. An error occurs if the public key of the assertion signing key has the `kid` property. This is because that `kid` is issued only when you register a public key in the LINE Developers Console.

<!-- note end -->

You can choose to write your own program to generate an assertion signing key pair based on the published specification, but you can use libraries that meet the specification to generate a key more easily.

Here is an example of the steps for generating an assertion signing key:

- [Create a key pair with jwx (Go language library)](https://developers.line.biz/en/docs/messaging-api/generate-json-web-token/#use-go-lang)
- [Create a key pair with JWCrypto (Python library)](https://developers.line.biz/en/docs/messaging-api/generate-json-web-token/#use-python)
- [Create a key pair with a browser](https://developers.line.biz/en/docs/messaging-api/generate-json-web-token/#use-browser)

#### Create a key pair with jwx (Go language library) 

You can generate a key pair with the [jwx command line tool](https://github.com/lestrrat-go/jwx/tree/develop/v2/cmd/jwx). The command line tool is part of [jwx](https://github.com/lestrrat-go/jwx), an open source Go language library, used for JWT implementation. If you don't have Go language development environment set up, download Go from the [Go language official site](https://go.dev/doc/install).

To issue an assertion signing key:

##### 1. Install the jwx command line tool 

Install the jwx command line tool with this command.

```sh
$ git clone https://github.com/lestrrat-go/jwx.git
$ cd jwx
$ make jwx
```

When the installation is complete, you'll see the path where the jwx command line tool has been installed.

```
// Example of installed path display
Installed jwx in {installed path}
```

You should configure the path so that the commands in subsequent steps can be executed.

##### 2. Generate private key and public key 

Create a private key with this command.

```sh
$ jwx jwk generate --type RSA --keysize 2048 --template '{"alg":"RS256","use":"sig"}' > private.key
```

Create a public key with the private key.

```sh
$ jwx jwk format --public-key private.key > public.key
```

If successful, a private key and public key are generated:

**Private key example**

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

**Public key example**

```json
{
  "alg": "RS256",
  "e": "AQ......",
  "kty": "RSA",
  "n": "pTS2jGso......",
  "use": "sig"
}
```

#### Create a key pair with JWCrypto (Python library) 

You can create a key pair with an open source Python library, [JWCrypto](https://github.com/latchset/jwcrypto) for JWT implementation. To use JWCrypto, you need Python 3 and pip installed on your computer. If you don't have Python 3, download an installer for your OS from the [Python official site](https://www.python.org/downloads/) and proceed with installation. Pip is installed when Python3 is installed. If you have Python 3 but no pip, see the [pip documentation](https://pip.pypa.io/en/stable/installation/) for installation.

To issue an assertion signing key:

##### 1. Install JWCrypto 

Install JWCrypto with this command.

```python
$ pip install jwcrypto
```

##### 2. Write code to create private and public keys 

Create a python file that generates private and public keys by specifying `kty` as `RSA`, `alg` as `RS256`, `use` as `sig`, and `size` as `2048`, like below.

```python
from jwcrypto import jwk
import json
key = jwk.JWK.generate(kty='RSA', alg='RS256', use='sig', size=2048)

private_key = key.export_private()
public_key = key.export_public()

print("=== private key ===\n"+json.dumps(json.loads(private_key),indent=2))
print("=== public key ===\n"+json.dumps(json.loads(public_key),indent=2))
```

Save the python file using any file name you want. In this case, the file name is `app.py`.

In the same directory where you saved the python file, generate a public key based on the private key with this command.

```sh
$ python app.py
```

If successful, a private key and public key are generated in the standard output:

**Private key example**

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

**Public key example**

```json
{
  "alg": "RS256",
  "e": "AQAB",
  "kty": "RSA",
  "n": "_RzHf7cgG_i6Pdo...",
  "use": "sig"
}
```

#### Generate a key pair with a browser 

If your browser supports [Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API), you can use the [`SubtleCrypto.generateKey()`](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/generateKey) method to generate a private key and public key. If you have Google Chrome, enter and run this code from the console of Chrome's developer tools.

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

If successful, a private key and public key are generated.

**Private key example**

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

**Public key example**

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

### 2. Register public key and get `kid` 

After you generate a key pair, register the public key in the [LINE Developers Console](https://developers.line.biz/console/) and in return, get `kid`. To register your public key, visit the console and open the channel settings for your channel. Click the **Basic settings** tab and then the **Register a public key** button next to assertion signing key. Enter the public key and finalize the registration with the **Register** button.

If the public key is successfully registered, you'll get `kid` in return.

## Generate a JWT 

JWT is a string and contains header, payload, and signature, all of which are required. To generate a JWT, you can use any [JWT library](https://www.jwt.io/libraries) or write your own code from scratch with your assertion signing key.

### Header 

The header must contain these properties:

| Property | Type | Description |
| --- | --- | --- |
| `alg` | String | The algorithm for JWT generation. Set the value to `"RS256"` |
| `typ` | String | The type of the token. Set the value to `"JWT"`. |
| `kid` | String | The key ID. Set the value to the `kid` property returned for [2. Register public key and get `kid`](https://developers.line.biz/en/docs/messaging-api/generate-json-web-token/#register-public-key-and-get-kid). |

This is an example of a decoded header:

```json
{
  "alg": "RS256",
  "typ": "JWT",
  "kid": "536e453c-aa93-4449-8e90-add2608783c6"
}
```

### Payload 

The payload must contain these properties:

| Property | Type | Description |
| --- | --- | --- |
| `iss` | String | Channel ID. You can retrieve your channel ID from the [LINE Developers Console](https://developers.line.biz/console/). The value of this property and `sub` must be the same. |
| `sub` | String | Channel ID. You can retrieve your channel ID from the [LINE Developers Console](https://developers.line.biz/console/). The value of this property and `iss` must be the same. |
| `aud` | String | Set the value to `https://api.line.me/`. |
| `exp` | Number | The expiration time of the JWT in UNIX time (in seconds). The maximum lifetime of a JWT assertion is 30 minutes. |
| `token_exp` | Number | The channel access token's validity period in seconds. The maximum lifetime of a channel access token is 30 days. |

This is an example of a decoded payload:

```json
{
  "iss": "1234567890",
  "sub": "1234567890",
  "aud": "https://api.line.me/",
  "exp": 1559702522,
  "token_exp": 86400
}
```

### Signature 

You need to sign the header and payload to generate a JWT. Learn how to create a signature and use the result to generate a JWT with [node-jose](https://developers.line.biz/en/docs/messaging-api/generate-json-web-token/#jwt-use-nodejs) (Node.js library) or [PyJWT](https://developers.line.biz/en/docs/messaging-api/generate-json-web-token/#jwt-use-python) (Python library).

#### Generate a JWT with node-jose (Node.js library) 

To create a signature and generate a JWT with node-jose, a Node.js library, make sure you have [Node.js](https://nodejs.org/en) and [node-jose](https://github.com/cisco/node-jose#installing) installed.

The example code below uses node-jose to sign with a **private key** to generate a JWT. To generate your own JWT using this code, first change the value of `privateKey` to the private key of your assertion signing key. Also change `header` and `payload` to your own values and run the code. Make sure to sign with your **private key** to prove that the content isn't tampered with. See [node-jose](https://github.com/cisco/node-jose#installing) for more information on the usage.

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

Sign the Base64url-encoded header, Base64url-encoded claim set, and a private key (such as an rsa_private.pem file), using the algorithm you specified in the header. The Base64url-encoded result is your JWT. Here is an example of JWT.

```sh
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IjJjNjU4NWYzLThkZGQtNDZjNC05YmUyLWI1NGE3MGFhOTRlYSJ9.eyJpc3MiOiIxNjUzOTQ3MTcyIiwic3ViIjoiMTY1Mzk0NzE3MiIsImF1ZCI6Imh0dHBzOi8vYXBpLmxpbmUubWUvIiwiZXhwIjoiMTU4NTIwMDA2MiIsInRva2VuX2V4cCI6IjI1OTIwMDAifQ.UVG6PAEub-OPbZ3nJuVxRRPjY6Sz_eIHJV9DTTAHCR79YsG4yWvoa9AeIctibb6IJQKgTEV7mF7LsUDmXldEDqYwyEmKs38zj_995Ntc9SYBFphHpr09NqfMoqMphwKqms2NOnqgcHreFs27d9Q0Qv8Rtv2t7SB2cVO__KrsjzYNs3miTvDdkqYLXFo5fXwuzNtHOCAJomd6bhMR8Yd1-vJmtMCBPK4hmA98w8fG_NhcyLbw-B9AuxQ6z92zXiRhNyPlK_3ce2T7HtgUluJ4xJl4xdLJ_C6hvTAqtQxmSiJKzbjUiANF6hVBTomU8vkaIjEKjnlT1uPMihfrsA3pzQ
```

#### Generate a JWT with PyJWT (Python library) 

To create a signature and generate a JWT with PyJWT, you need [Python](https://www.python.org/downloads/) and [PyJWT](https://github.com/jpadilla/pyjwt) installed.

The example code below uses PyJWT to sign with a **private key** to generate a JWT. To generate your own JWT using this code, first change the value of `privateKey` to the private key of your assertion signing key. Also, change `kid` in `headers` and `payload` to your own values and run the code. Make sure to sign with your **private key** to prove that the content isn't tampered with. See [PyJWT](https://github.com/jpadilla/pyjwt#installing) for more information on the usage.

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

Sign the Base64url-encoded header, Base64url-encoded claim set, and a private key using the algorithm you specified in the header. The Base64url-encoded result is your JWT. Here is an example of JWT.

```sh
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ijk4NjllNDQ2LTM0ODktNDUxNi1hODNmLWVjOTIxNGFkOTRkMCJ9.eyJpc3MiOiIxMjM0NTY3ODkwIiwic3ViIjoiMTIzNDU2Nzg5MCIsImF1ZCI6Imh0dHBzOi8vYXBpLmxpbmUubWUvIiwiZXhwIjoxNjIzOTk1NTk5LCJ0b2tlbl9leHAiOjI1OTIwMDB9.Zf32xTqgUHSYw2C2Mlmunqz_AtkaqvGh0msx9XJMX6QYLPT4m4QYF3PsER-zfbhbByNT4rH09JEMRP7bzcNMQ8l4n_WXwTyLkNciZYzF-sTiVHiZu4ucJm4_l8ni5NaqOVEntsCp1wQi8-VLjaMpQlQ7crCdouEMFFeyVwgERfH8ui6UZaJeIlJKRZTnO6iYvKYuLyUsqzowfwZo0hcnnZIXKnjZ81ukjH3_78EHXOD5ivovAT7CtmBoglm3Bvsi0N6PlEONLhHqpCleaYTXRmCykxDLP600JRvi5TYApaN-8n2Bo3FskXJLuxquWLP-LTfMDlkakmfEfcQCiz7daQ
```

## Issue a channel access token v2.1 

You can [issue a channel access token v2.1](https://developers.line.biz/en/reference/messaging-api/#issue-channel-access-token-v2-1) with the JWT assertion you [generated](https://developers.line.biz/en/docs/messaging-api/generate-json-web-token/#generate-jwt).

<!-- note start -->

**To manage channel access tokens v2.1 using key IDs**

- When you request for a channel access token v2.1, the response you get is a pair of the channel access token and a unique key ID (`key_id`). For proper management of channel access tokens, safely store the channel access token and key ID pair.
- The key ID is an identifier added to the Messaging API on June 22, 2020. If your app uses a channel access token v2.1 without a key ID, we recommend that you re-issue a channel access token v2.1 and safely store the token and key ID pair. If you re-issue a channel access token, make sure to update your bot to use the new token.

<!-- note end -->

The process for getting a channel access token v2.1 is as follows:

![](https://developers.line.biz/media/messaging-api/channel-access-token/using_keyID_procedure_01.png)

1. Execute the [Issue channel access token v2.1](https://developers.line.biz/en/reference/messaging-api/#issue-channel-access-token-v2-1) endpoint with the JWT you generated to issue a channel access token.
2. The LINE Platform sends you a channel access token and a key ID.
3. Store the channel access token and key ID pair in a database or somewhere else.

### Revoke channel access token v2.1 

You can [revoke a channel access token v2.1](https://developers.line.biz/en/reference/messaging-api/#revoke-channel-access-token-v2-1) if your channel access token is valid.

<!-- note start -->

**To verify the validity of channel access tokens**

You can use an invalid channel access token to execute the [Revoke channel access token v2.1](https://developers.line.biz/en/reference/messaging-api/#revoke-channel-access-token-v2-1) endpoint and get no error. You can get key IDs for valid channel access tokens using the [Get all valid channel access token key IDs v2.1](https://developers.line.biz/en/reference/messaging-api/#get-all-valid-channel-access-token-key-ids-v2-1) endpoint. You can identify valid access tokens by matching the obtained key IDs with pairs of a channel access token and a key ID stored in a database, etc.

<!-- note end -->

The process for revoking a channel access token v2.1 is as follows:

![](https://developers.line.biz/media/messaging-api/channel-access-token/using_keyID_procedure_02.png)

1. Re-generate a JWT from the assertion signing key you stored.
2. Execute the [Get all valid channel access token key IDs v2.1](https://developers.line.biz/en/reference/messaging-api/#get-all-valid-channel-access-token-key-ids-v2-1) endpoint with the JWT.
3. The LINE Platform returns key IDs for valid channel access tokens.
4. Check the key IDs against your database.
5. See if you have a channel access token and key ID pair that matches any of the key IDs returned.
6. Retrieve the channel access token validated.
7. Execute the [Revoke channel access token v2.1](https://developers.line.biz/en/reference/messaging-api/#revoke-channel-access-token-v2-1) endpoint with the channel access token.
8. The LINE Platform revokes the channel access token.
