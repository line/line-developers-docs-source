# LINEミニアプリ APIリファレンス

## サービスメッセージ 

<!-- tip start -->

**認証済ミニアプリでのみ利用できます**

この機能は、認証済ミニアプリでのみ利用できます。未認証ミニアプリの場合、開発用の内部チャネルではテストできますが、公開用の内部チャネルでは利用できません。

<!-- tip end -->

サービスメッセージAPIを使用すると、サービスからLINEミニアプリのユーザーに、サービスメッセージを送信できます。

サービスメッセージを送信するには、サービス通知トークンと[テンプレート](https://developers.line.biz/ja/docs/line-mini-app/develop/service-messages/#service-message-templates)が必要です。

- [サービス通知トークンを発行する](https://developers.line.biz/ja/reference/line-mini-app/#issue-notification-token)
- [サービスメッセージを送信する](https://developers.line.biz/ja/reference/line-mini-app/#send-service-message)

### サービス通知トークンを発行する 

サービス通知トークンを発行します。サービス通知トークンを使用すると、紐づけられたユーザーに対してサービスメッセージを送信できます。

サービス通知トークンの特徴は以下のとおりです。

- サービス通知トークンは、発行から1年間（31,536,000秒間）有効です。有効期限が切れるまでに、最大5回サービスメッセージを送信できます。
- サービス通知トークンを使用すると、有効期限が切れておらず、残りの送信可能回数が0でない場合は、サービス通知トークンの値が更新されます。ユーザーに対して、後続のサービスメッセージを送信する場合は、更新後のサービス通知トークンを保存してください。

<!-- warning start -->

**1つのアクセストークンで複数のサービス通知トークンを発行しないでください**

[`liff.getAccessToken()`](https://developers.line.biz/ja/reference/liff/#get-access-token)で取得したアクセストークン（LIFFのアクセストークン）を再利用して、複数のサービス通知トークンを発行することは許可されていません。

LIFFのアクセストークン1つにつき、発行できるサービス通知トークンは1つだけです。

<!-- warning end -->

<!-- note start -->

**注意**

サービス通知トークンは、一人のユーザーに紐づいています。あるユーザーに紐づいたサービス通知トークンを利用して、ほかのユーザーにサービスメッセージを送信することはできません。

<!-- note end -->

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -X POST https://api.line.me/message/v3/notifier/token \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer W1TeHCgfH2Liwa...' \
-d '{
    "liffAccessToken": "eyJhbGciOiJIUzI1NiJ9..."
}'
```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://api.line.me/message/v3/notifier/token`

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`\
詳しくは、「[チャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/)」を参照してください。

<!-- parameter end -->

<!-- note start -->

**ステートレスチャネルアクセストークンの使用を推奨します**

LINEミニアプリチャネルでは、[長期のチャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/#long-lived-channel-access-token)および、[任意の有効期間を指定できるチャネルアクセストークン（チャネルアクセストークンv2.1）](https://developers.line.biz/ja/docs/basics/channel-access-token/#user-specified-expiration)は使用できません。

LINEミニアプリの開発では、[ステートレスチャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/#stateless-channel-access-token)または[短期のチャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/#short-lived-channel-access-token)を使用できます。このうち、ステートレスチャネルアクセストークンの使用を推奨します。ステートレスチャネルアクセストークンは、発行数に制限がないため、アプリケーション側でトークンのライフサイクルを管理する必要がありません。

<!-- note end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

liffAccessToken

String

[`liff.getAccessToken()`](https://developers.line.biz/ja/reference/liff/#get-access-token)で取得したアクセストークン（LIFFのアクセストークン）

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

notificationToken

String

サービス通知トークン

<!-- parameter end -->
<!-- parameter start -->

expiresIn

Number

サービス通知トークンの有効期限が切れるまでの秒数。サービス通知トークンは、発行から1年間（31,536,000秒間）有効です。

<!-- parameter end -->
<!-- parameter start -->

remainingCount

Number

発行されたサービス通知トークンで、サービスメッセージを送信できる回数

<!-- parameter end -->
<!-- parameter start -->

sessionId

String

セッションID。詳しくは、「[サービスメッセージを送信する](https://developers.line.biz/ja/docs/line-mini-app/develop/service-messages/)」を参照してください。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "notificationToken": "34c11a03-b726-49e3-8ce0-949387a9..",
  "expiresIn": 31536000,
  "remainingCount": 5,
  "sessionId": "xD06...."
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のいずれかのステータスコードとエラーメッセージを返します。

| ステータスコード | 説明 |
| --- | --- |
| 400 Bad request | 以下のいずれかです。<ul><li>リクエストボディに問題があります。</li><li>`liffAccessToken`プロパティに指定したLIFFのアクセストークンを使用して、サービス通知トークンの発行が短時間に連続してリクエストされました。</li></ul> |
| 401 Unauthorized | 以下のいずれか、または両方です。<ul><li>有効なチャネルアクセストークンが指定されていません。</li><li>有効なLIFFのアクセストークンが指定されていません。</li><ul><li>ユーザーが[LIFFアプリを閉じる](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#behavior-when-closing-liff-app)と、有効期限が切れていなくてもアクセストークンは無効化されます。</li></ul></ul> |
| 403 Forbidden | このチャネルには、サービス通知トークンを発行する許可が与えられていません。 |
| 500 Internal Server Error | 内部サーバーのエラーです。 |

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
{
  "message": "[liffAccessToken] must not be blank"
}
```

<!-- tab end -->

### サービスメッセージを送る 

サービス通知トークンで指定されたユーザーに、サービスメッセージを送信します。

サービスメッセージを送信すると、有効期限が切れておらず、残りの送信可能回数が0でない場合は、サービス通知トークンの値が更新されます。ユーザーに対して、後続のサービスメッセージを送信する予定がある場合は、更新後のサービス通知トークンを保存してください。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -X POST https://api.line.me/message/v3/notifier/send?target=service \
-H 'Authorization: Bearer W1TeHCgfH2Liwa...' \
-H 'Content-Type: application/json' \
-d '{
    "templateName": "thankyou_msg_en",
    "params": {
        "date": "2020-04-23",
        "username": "Brown & Cony"
    },
    "notificationToken": "34c11a03-b726-49e3-8ce0-949387a9.."
}'
```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://api.line.me/message/v3/notifier/send`

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->
<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`\
詳しくは、『LINEプラットフォームの基礎知識』の「[チャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/)」を参照してください。

<!-- parameter end -->

<!-- note start -->

**ステートレスチャネルアクセストークンの使用を推奨します**

LINEミニアプリチャネルでは、[長期のチャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/#long-lived-channel-access-token)および、[任意の有効期間を指定できるチャネルアクセストークン（チャネルアクセストークンv2.1）](https://developers.line.biz/ja/docs/basics/channel-access-token/#user-specified-expiration)は使用できません。

LINEミニアプリの開発では、[ステートレスチャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/#stateless-channel-access-token)または[短期のチャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/#short-lived-channel-access-token)を使用できます。このうち、ステートレスチャネルアクセストークンの使用を推奨します。ステートレスチャネルアクセストークンは、発行数に制限がないため、アプリケーション側でトークンのライフサイクルを管理する必要がありません。

<!-- note end -->

#### クエリパラメータ 

<!-- parameter start (props: required) -->

target

`service`

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

templateName

String

サービスメッセージとして利用する、追加済みテンプレートの名前。テンプレートの名前はLINE Developersコンソールで確認できます。詳しくは、「[送信できるサービスメッセージの種類](https://developers.line.biz/ja/docs/line-mini-app/develop/service-messages/#types-of-service-messages-that-can-be-sent)」を参照してください。\
BCP 47言語タグを末尾に追加してください。\
フォーマット：`{template name}_{BCP 47 language tag}`\
最大文字数：30

<!-- note start -->

**注意**

サービスメッセージでサポートしている言語と言語タグは、以下のとおりです。

- 日本語：`ja`
- 英語：`en`
- 中国語（繁体字）：`zh-TW`
- タイ語：`th`
- インドネシア語：`id`
- 韓国語：`ko`

<!-- note end -->

<!-- parameter end -->
<!-- parameter start (props: required) -->

params

object

テンプレート変数と値のペアを指定するJSONオブジェクト。\
テンプレートにテンプレート変数がない場合は、空のJSONオブジェクト（`{ }`）を指定します。\
テンプレート変数は、テンプレートごとに定義されています。必須の要素にテンプレート変数が含まれる場合は、必ずテンプレート変数と値のペアを指定してください。\
詳しくは、「[サービスメッセージのテンプレートをチャネルに追加する](https://developers.line.biz/ja/docs/line-mini-app/develop/service-messages/#service-message-templates)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

notificationToken

String

サービス通知トークン

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

notificationToken

String

更新後のサービス通知トークン。このサービス通知トークンを使用して、後続のサービスメッセージを送信します。

<!-- parameter end -->
<!-- parameter start -->

expiresIn

Number

更新後のサービス通知トークンの有効期限が切れるまでの秒数

<!-- parameter end -->
<!-- parameter start -->

remainingCount

Number

更新後のサービス通知トークンで、後続のサービスメッセージを送信できる回数

<!-- parameter end -->
<!-- parameter start -->

sessionId

String

セッションID。詳しくは、「[サービスメッセージを送信する](https://developers.line.biz/ja/docs/line-mini-app/develop/service-messages/)」を参照してください。

<!-- parameter end -->

<!-- note start -->

**注意**

`expiresIn`および`remainingCount`の値が`0`の場合は、サービスメッセージは送信されたが、サービス通知トークンが更新できなかったことを示します。

<!-- note end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
// リクエストは成功し、
// 新しいサービス通知トークンが
// 発行されました。
{
  "notificationToken": "c9884874-bf6a-4241-8999-2767241c...",
  "expiresIn": 31535906,
  "remainingCount": 3,
  "sessionId": "xD06...."
}

// リクエストは成功し、
// サービスメッセージは送信されたが、
// LINEプラットフォームがサービス
// 通知トークンを更新できない場合
{
  "expiresIn": 0,
  "remainingCount": 0
}
```

<!-- tab end -->

#### エラーレスポンス 

以下のいずれかのステータスコードとエラーメッセージを返します。

| ステータスコード | 説明 |
| --- | --- |
| 400 Bad request | 以下のいずれかです。<ul><li>リクエストボディに問題があります。</li><li>サービスメッセージ送信対象のユーザーが存在しません。</li></ul> |
| 401 Unauthorized | 以下のいずれか、または両方です。<ul><li>有効なチャネルアクセストークンが指定されていません。</li><li>有効なサービス通知トークンが指定されていません。</li></ul> |
| 403 Forbidden | 以下のいずれかです。<ul><li>このチャネルには、サービスメッセージを送信する許可が与えられていません。</li><li>指定されたテンプレートが見つかりません。</li></ul> |
| 500 Internal Server Error | 内部サーバーのエラーです。 |

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
{
  "message": "Invalid notifier token"
}
```

<!-- tab end -->

## 共通プロフィールのクイック入力 

<!-- tip start -->

**認証済ミニアプリでのみ利用できます**

共通プロフィールのクイック入力を利用するには、LINEミニアプリが認証済みであり、かつクイック入力の利用申請を行う必要があります。詳しくは、「[クイック入力の利用手順](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#process)」を参照してください。

<!-- tip end -->

クイック入力とは、LINEミニアプリ上で［**自動入力**］をタップすることで、必要なプロフィール情報が自動で入力される機能です。ユーザーがアカウントセンターで設定した共通プロフィールの情報が、LINEミニアプリで簡単に利用できます。詳しくは、「[共通プロフィールのクイック入力の概要](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/)」を参照してください。

### liff.$commonProfile.get() 

ユーザーがアカウントセンターで設定している共通プロフィールの情報を取得します。

`liff.$commonProfile.get()`メソッドを実行すると、ユーザーがプロフィールの情報を確認するためのモーダルが表示されます。表示されたモーダルでプロフィールを確認後、ユーザーが［**自動で入力する**］をタップすると、共通プロフィールの情報を取得できます。

モーダルの表示例：

![](https://developers.line.biz/media/line-mini-app/quick-fill/quick-fill-modal-screen.png)

_例_

<!-- tab start `javascript` -->

```javascript
const { data, error } = await liff.$commonProfile.get(
  ["family-name", "given-name", "email", "tel", "postal-code"],
  {
    formatOptions: {
      givenName: {
        excludeEmojis: false,
      },
      tel: {
        excludeNonJp: false,
      },
      postalCode: {
        digitsOnly: false,
      },
    },
  },
);
console.log(data);
console.log(error);
```

<!-- tab end -->

#### 構文 

```javascript
liff.$commonProfile.get(scopes, options);
```

#### 引数 

<!-- parameter start (props: required) -->

scopes

Array of strings

取得したい共通プロフィールのスコープを指定します。

`scopes`に指定できる値については、「[取得できる共通プロフィールのスコープと戻り値](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#common-profile-scope)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

options

Object

共通プロフィールの情報を取得するときのオプション

<!-- parameter end -->
<!-- parameter start (props: optional) -->

options.formatOptions

Object

情報の形式に関するオプション。`scopes`プロパティで指定した各スコープに対して、[`formatOptions`オブジェクト](https://developers.line.biz/ja/reference/line-mini-app/#get-common-profile-format-options)を指定します。

キーには、オプションを設定したいスコープをキャメルケース形式で指定します。たとえば、スコープが`given-name`のとき、キーは`givenName`になります。

<!-- parameter end -->

#### `formatOptions`オブジェクト 

<!-- parameter start (props: optional) -->

excludeEmojis

Boolean

文字列内の絵文字を削除するかどうか。デフォルトは`true`です。以下のスコープにのみ指定できます。

- givenName
- familyName

<!-- parameter end -->
<!-- parameter start (props: optional) -->

excludeNonJp

Boolean

12桁以上の電話番号を排除するかどうか。デフォルトは`true`です。`true`の場合、電話番号が12桁以上のときは、空文字とエラー情報を返します。以下のスコープにのみ指定できます。

- tel

<!-- parameter end -->
<!-- parameter start (props: optional) -->

digitsOnly

Boolean

数字以外の郵便番号を排除するかどうか。デフォルトは`true`です。`true`の場合、郵便番号に数字以外が含まれているときは、空文字とエラー情報を返します。以下のスコープにのみ指定できます。

- postalCode

<!-- parameter end -->

_例_

<!-- tab start `javascript` -->

```javascript
{
  givenName: {
    excludeEmojis: false,
  },
  tel: {
    excludeNonJp: false,
  },
  postalCode: {
    digitsOnly: false,
  },
}
```

<!-- tab end -->

#### 戻り値 

`{ data: Partial<CommonProfile>, error: Partial<CommonProfileError>}`型の`Promise`オブジェクトが返されます。

`Promise`がresolveされると、`data`プロパティにユーザーの共通プロフィール情報を含む`Partial<CommonProfile>`型、`error`プロパティにエラー情報を含む`Partial<CommonProfileError>`型のオブジェクトが渡されます。

次のような場合、`data`が持つプロパティは`undefined`もしくは`null`になります。

- `undefined`になるケース
  - 引数の`scopes`で対象の項目を指定していない場合
  - 引数の`scopes`で対象の項目を指定したが、ユーザーがその項目の権限を許可していない場合
- `null`になるケース
  - ユーザーが共通プロフィールで対象の項目に値を設定していない場合
  - 共通プロフィールで対象の項目を取得する時にエラーが発生した場合

指定したスコープに応じて取得できるプロパティの値については、「[取得できる共通プロフィールのスコープと戻り値](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#common-profile-scope)」を参照してください。

_`Partial<CommonProfile>`型のオブジェクトの例_

<!-- tab start `json` -->

```javascript
{
  "family-name": "山田",
  "given-name": "太郎",
  "email": "sample@example.com",
  "tel": "09001234567",
  "postal-code": "1020094"
}
```

<!-- tab end -->

_`Partial<CommonProfileError>`型のオブジェクトの例_

<!-- tab start `json` -->

```javascript
{
  "tel": ["Phone number has 12 or more digits"],
  "postal-code": ["Postal code contains non-numeric characters"]
}
```

<!-- tab end -->

#### エラーレスポンス 

`Promise`がrejectされたときは、[`LiffError`](https://developers.line.biz/ja/reference/liff/#liff-errors)が渡されます。

_プラグインを正しくインストールせずにAPIを呼んだ場合の例_

<!-- tab start `javascript` -->

```javascript
new Error(
  "LiffCommonProfilePlugin isn't installed properly. Did you call liff.use(new LiffCommonProfilePlugin()) before using it?"
);
```

<!-- tab end -->

_LIFFブラウザ以外でAPIが呼ばれた場合の例_

<!-- tab start `javascript` -->

```javascript
new Error("liff.$commonProfile API is available only in LIFF browser.");
```

<!-- tab end -->

### liff.$commonProfile.getDummy() 

共通プロフィールのダミーデータを取得します。10種類のダミーデータが用意されており、`caseId`によって取得するダミーデータを指定できます。

`liff.$commonProfile.getDummy()`メソッドを実行すると、プロフィールの情報を確認するためのモーダルが表示されます。［**自動で入力する**］をタップすると、共通プロフィールのダミーデータを取得できます。

モーダルの表示例：

![](https://developers.line.biz/media/line-mini-app/quick-fill/quick-fill-dummy-modal-screen.png)

_例_

<!-- tab start `javascript` -->

```javascript
const { data, error } = await liff.$commonProfile.getDummy(
  ["family-name", "given-name", "email", "tel", "postal-code"],
  {
    formatOptions: {
      givenName: {
        excludeEmojis: false,
      },
      tel: {
        excludeNonJp: false,
      },
      postalCode: {
        digitsOnly: false,
      },
    },
  },
  1,
);
console.log(data);
console.log(error);
```

<!-- tab end -->

#### 構文 

```javascript
liff.$commonProfile.getDummy(scopes, options, caseId);
```

#### 引数 

<!-- parameter start (props: required) -->

scopes

Array of strings

取得したい共通プロフィールのスコープを指定します。

`scopes`に指定できる値については、「[取得できる共通プロフィールのスコープと戻り値](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#common-profile-scope)」を参照してください。

<!-- parameter end -->
<!-- parameter start (props: optional) -->

options

Object

共通プロフィールの情報を取得するときのオプション

<!-- parameter end -->
<!-- parameter start (props: optional) -->

options.formatOptions

Object

情報の形式に関するオプション。`scopes`プロパティで指定した各スコープに対して、[`formatOptions`オブジェクト](https://developers.line.biz/ja/reference/line-mini-app/#get-common-profile-format-options)を指定します。

キーには、オプションを設定したいスコープをキャメルケース形式で指定します。たとえば、スコープが`given-name`のとき、キーは`givenName`になります。

<!-- parameter end -->
<!-- parameter start (props: required) -->

caseId

number

取得したいダミーデータのIDを指定します。IDが`1`から`10`までのダミーデータが用意されています。

`caseId`ごとのダミーデータについては、「[取得できる共通プロフィールのダミーデータ](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#get-dummy-common-profile)」を参照してください。

<!-- parameter end -->

#### 戻り値 

`{ data: Partial<CommonProfile>, error: Partial<CommonProfileError>}`型の`Promise`オブジェクトが返されます。

`Promise`がresolveされると、`data`プロパティにダミーデータを含む`Partial<CommonProfile>`型、`error`プロパティにエラー情報を含む`Partial<CommonProfileError>`型のオブジェクトが渡されます。

次のような場合、`data`が持つプロパティは`undefined`もしくは`null`になります。

- `undefined`になるケース
  - 引数の`scopes`で対象の項目を指定していない場合
- `null`になるケース
  - ダミーデータで対象の項目に値が設定されていない場合

指定したIDに応じて取得できるダミーデータについては、「[取得できる共通プロフィールのダミーデータ](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#get-dummy-common-profile)」を参照してください。

_`Partial<CommonProfile>`型のオブジェクトの例_

<!-- tab start `json` -->

```javascript
{
  "family-name": "見本田",
  "given-name": "見本夫",
  "family-name-kana": "ダミータ",
  "given-name-kana": "ダミーオ",
  "sex-enum": 0,
  "bday-day": 12,
  "bday-month": 3,
  "bday-year": 1998,
  "tel": "09001234567",
  "email": "dummy_39@yahoo.co.jp",
  "postal-code": "1020094",
  "address-level1": "東京都",
  "address-level2": "千代田区",
  "address-level3": "紀尾井町1-2",
  "address-level4": "東京ガーデンテラス紀尾井町"
}
```

<!-- tab end -->

_`Partial<CommonProfileError>`型のオブジェクトの例_

<!-- tab start `json` -->

```javascript
{
  "tel": ["Phone number has 12 or more digits"],
  "postal-code": ["Postal code contains non-numeric characters"]
}
```

<!-- tab end -->

##### エラーレスポンス 

`Promise`がrejectされたときは、[`LiffError`](https://developers.line.biz/ja/reference/liff/#liff-errors)が渡されます。

_プラグインを正しくインストールせずにAPIを呼んだ場合の例_

<!-- tab start `javascript` -->

```javascript
new Error(
  "LiffCommonProfilePlugin isn't installed properly. Did you call liff.use(new LiffCommonProfilePlugin()) before using it?"
);
```

<!-- tab end -->

_LIFFブラウザ以外でAPIが呼ばれた場合の例_

<!-- tab start `javascript` -->

```javascript
new Error("liff.$commonProfile API is available only in LIFF browser.");
```

<!-- tab end -->

### liff.$commonProfile.fill() 

取得した共通プロフィールの情報をフォームに自動入力します。それぞれのプロフィール情報とフォームの紐づけには、`data-liff-autocomplete`属性を用います。

<!-- tip start -->

**スコープと一致しないフォームへの自動入力**

`liff.$commonProfile.fill()`による自動入力は、フォームの`data-liff-autocomplete`属性を用いて行います。このとき、フォームの`data-liff-autocomplete`属性に指定する値は、取得したプロフィール情報のスコープ（`family-name`、`tel`、`bday-year`など）と一致している必要があります。

たとえば、誕生年（`bday-year`）、誕生月（`bday-month`）、誕生日（`bday-day`）の情報をそれぞれ取得した後、`20110623`のような形式に加工した上でフォームに自動入力させたい場合は、`liff.$commonProfile.fill()`の代わりに、`document.getElementById().value`や`document.querySelector().value`を用いることができます。

<!-- tip end -->

_取得した姓、電話番号、性別をそのまま自動入力する例_

<!-- tab start `javascript` -->

```javascript
// HTML
<input type="text" data-liff-autocomplete="family-name" />
<input type="tel" data-liff-autocomplete="tel" />
<select data-liff-autocomplete="sex-enum">
  <option value="0">男性</option>
  <option value="1">女性</option>
  <option value="2">その他</option>
  <option value="3">無回答</option>
</select>

// JavaScript
const { data, error } = await liff.$commonProfile.get([
  "family-name",
  "tel",
  "sex-enum",
]);

liff.$commonProfile.fill(data);
```

<!-- tab end -->

_取得した共通プロフィール情報の形式を一部変更して自動入力する場合_

<!-- tab start `javascript` -->

```javascript
// HTML
<input type="text" data-liff-autocomplete="bday-year" />
<input type="text" data-liff-autocomplete="bday-month" />
<input type="text" data-liff-autocomplete="bday-day" />

// JavaScript
const { data, error } = await liff.$commonProfile.get([
  "bday-year",
  "bday-month",
  "bday-day",
]);

const year = data["bday-year"];
const month = data["bday-month"];
const day = data["bday-day"];

// 月と日が1桁の場合、2桁になるように0埋めする
const formattedMonth = month.toString().padStart(2, '0');
const formattedDay = day.toString().padStart(2, '0');

// 加工後の値を自動入力
liff.$commonProfile.fill({
  "bday-year": year,
  "bday-month": formattedMonth,
  "bday-day": formattedDay,
});
```

<!-- tab end -->

#### 構文 

```javascript
liff.$commonProfile.fill(profile);
```

#### 引数 

<!-- parameter start (props: required) -->

profile

Partial&lt;CommonProfile&gt;

フォームに自動入力させるプロフィール情報を、`Partial<CommonProfile>`型で指定します。

指定できるスコープについては、「[取得できる共通プロフィールのスコープと戻り値](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#common-profile-scope)」を参照してください。

<!-- parameter end -->

#### 戻り値 

なし

## アプリ内課金（クライアント） 

<!-- tip start -->

**アプリ内課金機能を利用するには申請が必要です**

アプリ内課金機能を利用するには、利用申請を行う必要があります。詳しくは、『LINEミニアプリドキュメント』の「[アプリ内課金の概要](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/overview/)」を参照してください。

<!-- tip end -->

### liff.iap.getPlatformProducts() 

アプリ内課金で購入可能なアイテムの一覧を取得します。

_例_

<!-- tab start `javascript` -->

```javascript
const productIds = ["iap_ln_002", "iap_ln_003"];
liff.iap
  .getPlatformProducts({ productIds })
  .then((products) => {
    console.log(products);
  })
  .catch((err) => {
    console.error(err);
  });
```

<!-- tab end -->

#### 構文 

```javascript
liff.iap.getPlatformProducts({ productIds });
```

#### 引数 

<!-- parameter start (props: required) -->

productIds

Array of strings

取得したいアイテムの[プロダクトID](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-product-id/)の配列

<!-- parameter end -->

#### 戻り値 

`Promise`オブジェクトが返されます。`Promise`オブジェクトがresolveされると、プロダクトIDをキーとし、以下のプロパティを持つオブジェクトが渡されます。

<!-- parameter start -->

currency

String

ISO 4217形式の通貨コード。ユーザーが使用しているアプリストアのリージョンにローカライズされた通貨で返されます。

<!-- parameter end -->
<!-- parameter start -->

price

Number

アイテムの価格。ユーザーが使用しているアプリストアのリージョンにローカライズされた通貨で返されます。

<!-- parameter end -->
<!-- parameter start -->

productName

String

アイテムの名前。ユーザーが使用しているアプリストアのリージョンにローカライズされた表記で返されます。

<!-- parameter end -->

_戻り値の例_

<!-- tab start `json` -->

```json
{
  "iap_ln_002": {
    "currency": "JPY",
    "price": 100,
    "productName": "LINE Purchase 100"
  }
}
```

<!-- tab end -->

#### エラーレスポンス 

`Promise`が`reject`されたときは、[`LiffError`](https://developers.line.biz/ja/reference/liff/#liff-error-object)が渡されます。

発生する可能性があるエラーには、次のようなものがあります。

| エラーメッセージ | 説明 |
| --- | --- |
| Need access_token for api call, Please login first | ユーザーがログインしていません。 |
| In-App Purchase is not allowed in external browser | メソッドが外部ブラウザで実行されました。 |
| In-App Purchase is not allowed in this LIFF app | ユーザーが実行したLINEミニアプリがアプリ内課金をサポートしていません。 |

### liff.iap.requestConsentAgreement() 

ユーザーに対して、[LINEアプリ内課金利用規約](https://terms.line.me/line_iap_tou_1)への同意を求めます。

ユーザーがLINEアプリ内課金利用規約に対し未同意の場合や、新たな同意が必要な場合は同意画面が表示されます。

<!-- tip start -->

**常に最新の同意状況を確認してください**

[LINEアプリ内課金利用規約](https://terms.line.me/line_iap_tou_1)が更新された場合、再度の同意が必要になります。アプリ内課金を開始する前には、必ずこのメソッドを呼び出して最新の同意状況を確認してください。

<!-- tip end -->

#### 構文 

```javascript
await liff.iap.requestConsentAgreement();
```

#### 引数 

なし

#### 戻り値 

`Promise`オブジェクトが返されます。

- ユーザーが同意するとresolveされます。
- ユーザーが同意しない場合や、ネットワーク上の問題、ユーザー端末やLINEプラットフォーム側のサーバー内部で問題が発生して失敗した場合は、エラーオブジェクトを伴ってrejectされます。

#### エラーレスポンス 

`Promise`が`reject`されたときは、[`LiffError`](https://developers.line.biz/ja/reference/liff/#liff-error-object)が渡されます。

発生する可能性があるエラーには、次のようなものがあります。

| エラーメッセージ | 説明 |
| --- | --- |
| The user did not agree to the terms. | ユーザーが[LINEアプリ内課金利用規約](https://terms.line.me/line_iap_tou_1)に同意しませんでした。 |
| Need access_token for api call, Please login first | ユーザーがログインしていません。 |
| In-App Purchase is not allowed in external browser | メソッドが外部ブラウザで実行されました。 |
| In-App Purchase is not allowed in this LIFF app | ユーザーが実行したLINEミニアプリがアプリ内課金をサポートしていません。 |

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
{
  "code": "TERMS_AGREEMENT_ERROR",
  "message": "The user did not agree to the terms."
}
```

<!-- tab end -->

```

### liff.iap.createPayment() 

アプリストア（App Store、Google Play）の決済確認画面を起動し、購入処理を開始します。

#### 構文 

```javascript
liff.iap.createPayment({ productId, orderId });
```

#### 引数 

<!-- parameter start (props: required) -->

productId

string

事前に定義済みの[プロダクトID](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-product-id/)

<!-- parameter end -->

<!-- parameter start (props: required) -->

orderId

String

「[購入処理を予約する](https://developers.line.biz/ja/reference/line-mini-app/#reserve-purchase)」エンドポイントで取得した注文ID

<!-- parameter end -->

#### 戻り値 

`Promise<void>`オブジェクトが返されます。

- 購入が正常に完了するとresolveされます。
- キャンセルされた場合や、ネットワーク上の問題、ユーザー端末やLINEプラットフォーム側のサーバー内部で問題が発生して失敗した場合は、エラーオブジェクトを伴ってrejectされます。

#### エラーレスポンス 

`Promise`が`reject`されたときは、[`LiffError`](https://developers.line.biz/ja/reference/liff/#liff-error-object)が渡されます。

発生する可能性があるエラーには、次のようなものがあります。

| エラーメッセージ | 説明 |
| --- | --- |
| Need access_token for api call, Please login first | ユーザーがログインしていません。 |
| In-App Purchase is not allowed in external browser | メソッドが外部ブラウザで実行されました。 |
| In-App Purchase is not allowed in this LIFF app | ユーザーが実行したLINEミニアプリがアプリ内課金をサポートしていません。 |

## アプリ内課金（サーバー） 

<!-- tip start -->

**アプリ内課金機能を利用するには申請が必要です**

アプリ内課金機能を利用するには、利用申請を行う必要があります。詳しくは、『LINEミニアプリドキュメント』の「[アプリ内課金の概要](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/overview/)」を参照してください。

<!-- tip end -->

### レスポンスヘッダー 

アプリ内課金のレスポンスには、以下のHTTPヘッダーが含まれます。将来の弊社への問い合わせの際に参照できるよう、ログに保存してください。

| レスポンスヘッダー | 説明                                               |
| ------------------ | -------------------------------------------------- |
| x-line-request-id  | リクエストID。各リクエストごとに発行されるIDです。 |

### エラーレスポンス 

HTTPステータスコードが400番台または500番台の場合、以下のJSONデータを含むレスポンスボディが返されます。

<!-- parameter start (props: required) -->

errorCode

String

エラーコード

<!-- parameter end -->
<!-- parameter start (props: required) -->

message

String

エラーメッセージ

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

details

array

エラーの詳細

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

details\[].message

String

詳細メッセージ

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

details\[].property

String

エラーの発生箇所

<!-- parameter end -->

_エラーレスポンスの例_

HTTPステータスコードが400番台の場合

<!-- tab start `json` -->

```json
{
  "errorCode": "VALIDATION_ERROR",
  "message": "Request validation failed.",
  "details": [
    {
      "message": "'clientOs' must be 'android' or 'ios'. Actually received: 'INVALID'",
      "property": "clientOs"
    }
  ]
}
```

<!-- tab end -->

HTTPステータスコードが500番台の場合

<!-- tab start `json` -->

```json
{
  "errorCode": "INTERNAL_SERVER_ERROR",
  "message": "An internal server error occurred."
}
```

<!-- tab end -->

### 購入処理を予約する 

アプリストア決済を開始する前に、購入処理を予約します。

[レスポンス](https://developers.line.biz/ja/reference/line-mini-app/#reserve-purchase-response)に含まれる注文ID（`orderId`）は[購入完了イベント](https://developers.line.biz/ja/reference/line-mini-app/#purchase-complete-event)にも含まれます。注文IDは弊社への問い合わせや調査で必要になるため、必ず保存してください。

また、予約成功は購入完了を保証しないため、アイテム付与は購入完了イベントを起点に行ってください。

_リクエストの例_

<!-- tab start `shell` -->

```sh
curl -X POST https://api.line.me/iap/v1/product/reserve \
-H "Authorization: Bearer {UserAccessToken}" \
-H "Content-Type: application/json" \
-d '{
"clientIp": "192.168.1.1",
"clientOs": "android",
"productId": "iap_ln_002",
"shopProductName": "Premium Package"
}'

```

<!-- tab end -->

#### HTTPリクエスト 

`POST https://api.line.me/iap/v1/product/reserve`

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{user access token}`

現在のユーザーのアクセストークン。[`liff.getAccessToken()`](https://developers.line.biz/ja/reference/liff/#get-access-token)メソッドで取得できます。

<!-- parameter end -->
<!-- parameter start (props: required) -->

Content-Type

application/json

<!-- parameter end -->

#### リクエストボディ 

<!-- parameter start (props: required) -->

clientIp

String

サーバーで取得したユーザー端末のIPアドレス。IPv4またはIPv6形式で指定してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

clientOs

String

[`liff.getOS()`](https://developers.line.biz/ja/reference/liff/#get-os)メソッドで取得した値。`ios`または`android`。

<!-- parameter end -->
<!-- parameter start (props: required) -->

productId

String

購入対象の[プロダクトID](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-product-id/)。

<!-- parameter end -->
<!-- parameter start (props: required) -->

shopProductName

String

購入履歴に表示されるアイテム名。

絵文字や記号は使用できません。ユーザーが購入したアイテムを認識できるように適切な値を設定してください。

最大文字数：20（UTF-16）

<!-- parameter end -->

#### レスポンス 

ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

orderId

String

注文ID。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{ "orderId": "T2025020710000002126002" }
```

<!-- tab end -->

#### エラーレスポンス 

エラーレスポンスの形式については、[エラーレスポンス](https://developers.line.biz/ja/reference/line-mini-app/#iap-error-responses)を参照してください。

一般的なもの以外で発生する可能性があるエラーには、次のようなものがあります。

| エラーコード | 説明 |
| --- | --- |
| VALIDATION_ERROR | リクエスト制約が守られていません。例として、`clientOs`に`ios`または`android`以外の値が渡されています。 |
| WEBHOOK_URL_IS_NOT_SET | 支払い完了通知を受け取るWebhook URLが設定されていません。 |
| PRODUCT_ID_NOT_FOUND | リクエストされた[プロダクトID](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-product-id/)が存在しません。 |
| BLOCKED_USER | LINEプラットフォームにより、このユーザーが不正利用者と判断されました。このユーザーに関連するリクエストは処理できません。 |
| INTERNAL_SERVER_ERROR | LINEプラットフォームに一時的な問題が発生しています。再試行が可能なエンドポイントについては、指数バックオフや類似の方法で再試行してください。 |
| TERMS_AGREEMENT_ERROR | 「[ユーザーからアプリ内課金利用の同意を取得する](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/#get-user-consent)」において、このユーザーから最新の規約に対して同意を得ることができていない場合に発生します。 |

_エラーレスポンスの例_

<!-- tab start `json` -->

```json
{
  "errorCode": "VALIDATION_ERROR",
  "message": "Request validation failed.",
  "details": [
    {
      "message": "'clientOs' must be 'android' or 'ios'. Actually received: 'INVALID'",
      "property": "clientOs"
    }
  ]
}
```

<!-- tab end -->

### Webhookイベントの履歴を取得する 

LINEプラットフォームが送信したWebhookイベントの履歴を取得します。カーソルベースのページネーションで、1回に最大100件取得できます。

ソート順は、LINEプラットフォームでWebhookイベントの送信を開始した日時の昇順となります。

取得できるWebhookイベントは過去7日間に送信されたものに限られます。現時点では[購入完了イベント](https://developers.line.biz/ja/reference/line-mini-app/#purchase-complete-event)のみ取得可能で、[返金イベント](https://developers.line.biz/ja/reference/line-mini-app/#refund-event)は今後対応予定です。

_リクエストの例_

<!-- tab start `shell` -->

```sh

curl "https://api.line.me/iap/v1/webhook/events?startEpochSeconds=1747330438&endEpochSeconds=1747708454&pageSize=10" \
  -H "Authorization: Bearer {ChannelAccessToken}"

```

<!-- tab end -->

#### HTTPリクエスト 

`GET https://api.line.me/iap/v1/webhook/events`

#### リクエストヘッダー 

<!-- parameter start (props: required) -->

Authorization

Bearer `{channel access token}`\
詳しくは、『LINEプラットフォームの基礎知識』の「[チャネルアクセストークン](https://developers.line.biz/ja/docs/basics/channel-access-token/)」を参照してください。

<!-- parameter end -->

#### クエリパラメータ 

<!-- parameter start (props: required) -->

startEpochSeconds

Number

Webhookイベントの履歴を取得する期間の開始日時を指定します。指定した日時も取得対象に含まれます。過去7日以内のUNIX時間（秒）で指定してください。

<!-- parameter end -->
<!-- parameter start (props: required) -->

endEpochSeconds

Number

Webhookイベントの履歴を取得する期間の終了日時を指定します。指定した日時も取得対象に含まれます。過去7日以内のUNIX時間（秒）で指定してください。

<!-- parameter end -->
<!-- parameter start -->

cursor

String

Webhookイベントのページのカーソル。\
初回のリクエストでは指定しないでください。2回目以降のリクエストでは、前回のリクエスト時のレスポンスに含まれていた`nextCursor`の値を指定することで、続きのWebhookイベントを取得できます。

<!-- parameter end -->
<!-- parameter start (props: required) -->

pageSize

Number

1ページあたりのWebhookイベントの件数。<br> <ul><li>最小値：1</li><li>最大値：100</li></ul>

<!-- parameter end -->
<!-- parameter start -->

status

String

取得したいWebhookイベントのステータス。次のいずれかを指定します。

- `SUCCESS`：受け取りに成功したWebhookイベントの履歴を取得します。
- `FAILED`：受け取りに失敗したWebhookイベントの履歴を取得します。

未指定の場合、受け取りの成否に関わらず、すべてのWebhookイベントの履歴を取得します。

<!-- parameter end -->

<!-- note start -->

**ページネーション中はcursor以外のパラメータを変更しないでください**

ページネーション中は、`cursor`以外のパラメータを変更せずにリクエストしてください。パラメータを変更したい場合、最初のページからリクエストし直してください。

<!-- note end -->

#### レスポンス 

成功した場合、ステータスコード`200`と以下の情報を含むJSONオブジェクトを返します。

<!-- parameter start -->

events

Array

Webhookイベントのリスト。

<!-- parameter end -->
<!-- parameter start -->

events\[].transactionType

String

常に`PRODUCT`が返されます。

<!-- parameter end -->
<!-- parameter start -->

events[].event

Object

[Webhookイベントオブジェクト](https://developers.line.biz/ja/reference/line-mini-app/#purchase-complete-payload)。

<!-- parameter end -->
<!-- parameter start (props: annotation="含まれないことがあります") -->

nextCursor

String

次のページのカーソル。\
次のページが存在しない場合、`null`となります。

<!-- parameter end -->

_レスポンスの例_

<!-- tab start `json` -->

```json
{
  "events": [
    {
      "transactionType": "PRODUCT",
      "event": {
        "type": "purchaseComplete",
        "orderId": "T2025020710000002126002",
        "productId": "iap_ln_002",
        "userId": "U91FC5A...",
        "purchaseTimestamp": 1738672496,
        "channelId": "12345..."
      }
    }
  ],
  "nextCursor": "MTY3NjU0"
}
```

<!-- tab end -->

#### エラーレスポンス 

エラーレスポンスの形式については、[エラーレスポンス](https://developers.line.biz/ja/reference/line-mini-app/#iap-error-responses)を参照してください。

一般的なもの以外で発生する可能性があるエラーには、次のようなものがあります。

| エラーコード | 説明 |
| --- | --- |
| VALIDATION_ERROR | リクエスト制約が守られていません。例として、`status`に`SUCCESS`または`FAILED`以外の値が渡されています。 |
| INTERNAL_SERVER_ERROR | LINEプラットフォームに一時的な問題が発生しています。再試行が可能なエンドポイントについては、指数バックオフや類似の方法で再試行してください。 |

## アプリ内課金 Webhookイベントオブジェクト 

<!-- tip start -->

**アプリ内課金機能を利用するには申請が必要です**

アプリ内課金機能を利用するには、利用申請を行う必要があります。詳しくは、『LINEミニアプリドキュメント』の「[アプリ内課金の概要](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/overview/)」を参照してください。

<!-- tip end -->

### 署名を検証する 

LINEミニアプリのサーバーにWebhookのリクエストが届いたら、Webhookイベントを処理する前に、リクエストヘッダーに含まれる署名を検証してください。署名の検証は、LINEミニアプリのサーバーに届いたリクエストが「LINEプラットフォームから送信されたWebhookか」および「通信経路で改ざんされていないか」などを確認するための重要な手順です。

詳しくは、『Messaging APIドキュメント』の「[Webhookの署名を検証する](https://developers.line.biz/ja/docs/messaging-api/verify-webhook-signature/)」を参照してください。

### 購入完了イベント 

このイベントは、ユーザーがアプリストア（App Store、Google Play）で予約アイテムを購入し、弊社が精算したときに発生します。Webhookのペイロードには購入されたアイテムの情報が含まれます。

#### Webhookペイロード 

<!-- parameter start -->

type

String

Webhookイベントのタイプ。\
`purchaseComplete`が指定されます。

<!-- parameter end -->
<!-- parameter start -->

orderId

String

ユーザーが購入した注文のID。「[購入処理を予約する](https://developers.line.biz/ja/reference/line-mini-app/#reserve-purchase)」エンドポイントのレスポンスに含まれます。

<!-- parameter end -->
<!-- parameter start -->

productId

String

ユーザーが購入したアイテムのプロダクトID（[`productId`](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-product-id/)）。

<!-- parameter end -->
<!-- parameter start -->

userId

String

購入を行ったユーザーのユーザーID。

<!-- parameter end -->
<!-- parameter start -->

purchaseTimestamp

number

LINEプラットフォームで決済を完了した時間。単位はUNIX時間（秒）です。

この時間は購入を行ったユーザーが実際に支払いを完了した時間ではありません。

<!-- parameter end -->
<!-- parameter start -->

channelId

String

LINEミニアプリチャネルのチャネルID。

<!-- parameter end -->

_例_

<!-- tab start `json` -->

```json
{
  "type": "purchaseComplete",
  "orderId": "T2025020710000002126002",
  "productId": "iap_ln_002",
  "userId": "U91FC5A...",
  "purchaseTimestamp": 1738672496,
  "channelId": "12345..."
}
```

<!-- tab end -->

### 返金イベント 

このイベントは、ユーザーがアプリストア（App Store、Google Play）で購入したアイテムに対して返金が行われた場合に発生します。イベントには返金対象となったアイテムの情報が含まれます。

#### Webhookペイロード 

<!-- parameter start -->

type

String

Webhookイベントのタイプ。\
`refundComplete`が指定されます。

<!-- parameter end -->
<!-- parameter start -->

orderId

String

ユーザーが購入後にキャンセルした注文のID。「[購入処理を予約する](https://developers.line.biz/ja/reference/line-mini-app/#reserve-purchase)」エンドポイントのレスポンスに含まれます。

<!-- parameter end -->
<!-- parameter start -->

productId

String

ユーザーが購入後にキャンセルしたアイテムのプロダクトID（[`productId`](https://developers.line.biz/ja/docs/line-mini-app/in-app-purchase/iap-product-id/)）。

<!-- parameter end -->
<!-- parameter start -->

userId

String

購入後にキャンセルを行ったユーザーのユーザーID。

<!-- parameter end -->
<!-- parameter start -->

purchaseTimestamp

number

キャンセルされたアイテムが購入された際の時間。単位はUNIX時間（秒）です。

[購入完了イベント](https://developers.line.biz/ja/reference/line-mini-app/#purchase-complete-event)の`purchaseTimestamp`と一致します。この時間はユーザーが実際に返金を完了した時間ではありません。

<!-- parameter end -->
<!-- parameter start -->

channelId

String

LINEミニアプリチャネルのチャネルID。

<!-- parameter end -->

_例_

<!-- tab start `json` -->

```json
{
  "type": "refundComplete",
  "orderId": "T2025020710000002126002",
  "productId": "iap_ln_002",
  "userId": "U91FC5A...",
  "purchaseTimestamp": 1738672496,
  "channelId": "12345..."
}
```

<!-- tab end -->
