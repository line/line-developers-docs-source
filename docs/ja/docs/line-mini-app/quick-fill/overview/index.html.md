# 共通プロフィールのクイック入力の概要

<!-- tip start -->

**認証済ミニアプリでのみ利用できます**

共通プロフィールのクイック入力を利用するには、LINEミニアプリが認証済みであり、かつクイック入力の利用申請を行う必要があります。詳しくは、「[クイック入力の利用手順](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#process)」を参照してください。

<!-- tip end -->

## 共通プロフィールのクイック入力とは 

クイック入力とは、LINEミニアプリ上で［**自動入力**］をタップすることで、必要なプロフィール情報が自動で入力される機能です。ユーザーがアカウントセンターで設定した共通プロフィールの情報が、LINEミニアプリで簡単に利用できます。

![](https://developers.line.biz/media/line-mini-app/quick-fill/quick-fill-3-steps.png)

LINEミニアプリにクイック入力を導入すると、住所や電話番号の登録が必要な場面で、ボタンをタップするだけで必要な情報が自動で入力されます。これにより、たとえばお店の予約やオンラインストアでの注文時に、ユーザーは面倒な手入力の手間を省くことができます。

このページでは、LINEミニアプリでクイック入力を組み込む方法を紹介します。

ユーザーがLINEミニアプリ上でクイック入力を利用する方法については、『LINEみんなの使い方ガイド』の「[共通プロフィールを設定してクイック入力を利用する](https://guide.line.me/ja/services/quick-fill.html)」を参照してください。

### クイック入力を利用できる言語 

クイック入力の機能は、現時点では日本語のみをサポートしています。そのためLINEアプリの言語設定に関わらず、クイック入力の画面は日本語で表示されます。

## クイック入力の利用手順 

クイック入力を利用するには、LINEミニアプリが認証済みであり、かつクイック入力の利用申請を行う必要があります。これは、以下の手順に従います。

- [Step 1. 認証済ミニアプリを準備する](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#process-step-1)
- [Step 2. クイック入力の利用申請と開発を行う](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#process-step-2)

### Step 1. 認証済ミニアプリを準備する 

クイック入力は、認証済ミニアプリでのみ利用できます。このため、まずクイック入力を組み込むための認証済ミニアプリを準備します。詳しくは、「[LINEミニアプリ開発から公開までの流れ](https://developers.line.biz/ja/docs/line-mini-app/quickstart/#overall-process)」を参照してください。

### Step 2. クイック入力の利用申請と開発を行う 

認証済ミニアプリを準備したら、次はクイック入力の利用申請と開発を行います。これは、以下の手順に従います。

- [Step 2-1. クイック入力の利用申請を行い、承認を得る](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#process-step-2-1)
- [Step 2-2. LINE Developersコンソールでクイック入力のスコープを指定する](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#process-step-2-2)
- [Step 2-3. クイック入力を組み込む](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#process-step-2-3)
- [Step 2-4. LINEミニアプリの審査を依頼する](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#process-step-2-4)

#### Step 2-1. クイック入力の利用申請を行い、承認を得る 

クイック入力を利用するには、まず利用申請書に記入の上、申請フォームより申請してください。同一のサービス事業主が複数のLINEミニアプリを一括で申請する場合は、複数申請用の利用申請書を使用できます。

- [【単一申請用】利用申請書（Excelファイル）](https://workers-hub.ent.box.com/s/06w8vzqxfwx2e031oq2q9ztj7ca8p7h8)
- [【複数申請用】利用申請書（Excelファイル）](https://workers-hub.ent.box.com/s/xrwjm892d1uxsiblptfgoj07r0v5zwbp)

利用申請書に記入したら、以下のフォームより申請してください。申請の受領確認や、審査結果はメールでご連絡します。

[申請フォーム](https://form-business.yahoo.co.jp/claris/enqueteForm?inquiry_type=miniapp-quick-fill)

#### Step 2-2. LINE Developersコンソールでクイック入力のスコープを指定する 

クイック入力の利用申請を行い、承認された後は、利用したい情報のスコープを指定します。[LINE Developersコンソール](https://developers.line.biz/console/)で対象のLINEミニアプリチャネルを選択し、［**ウェブアプリ設定**］タブの［**Scope**］セクションで使用したいスコープにチェックを入れます。

なお、認証済ミニアプリのスコープを指定するには、［**審査申請**］タブにある［**検索可能にする**］ボタンを押して、LINEミニアプリを検索できるようにしておく必要があります。

![](https://developers.line.biz/media/line-mini-app/quick-fill/quick-fill-scope-ja.png)

クイック入力で利用できるスコープの種類について詳しくは、「[LINE Developersコンソールで選択できるスコープの種類](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#scope)」を参照してください。

<!-- tip start -->

**クイック入力とチャネル同意の簡略化を同時に有効にした場合の挙動について**

クイック入力と[チャネル同意の簡略化](https://developers.line.biz/ja/docs/line-mini-app/develop/channel-consent-simplification/)を同時に有効にした場合、「アクセス許可要求画面」においてユーザーが共通プロフィールのトグルボタンをオフにすることができなくなります。この挙動については、今後修正が予定されています。「アクセス許可要求画面」について詳しくは、「[「アクセス許可要求画面」で`openid`スコープ以外の権限を要求する](https://developers.line.biz/ja/docs/line-mini-app/develop/channel-consent-simplification/#request-permissions-other-than-openid)」を参照してください。

<!-- tip end -->

#### Step 2-3. クイック入力を組み込む 

スコープを指定したら、LINEミニアプリにクイック入力を組み込みます。開発方法について詳しくは、「[LIFFプラグインでクイック入力を組み込む](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#use-liff-plugin)」を参照してください。

なお、クイック入力を組み込んだLINEミニアプリを開発する際は、以下に従ってください。

- [共通プロフィールのクイック入力のデザインレギュレーション](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/design-regulations/)
- [LINEミニアプリ開発ガイドライン](https://developers.line.biz/ja/docs/line-mini-app/development-guidelines/)
- [LIFFアプリ開発ガイドライン](https://developers.line.biz/ja/docs/liff/development-guidelines/)
- [LINEログイン開発ガイドライン](https://developers.line.biz/ja/docs/line-login/development-guidelines/)

#### Step 2-4. LINEミニアプリの審査を依頼する 

クイック入力を組み込んだら、LINEミニアプリチャネルの［**審査申請**］タブからLINEミニアプリの審査を依頼してください。LINEミニアプリの審査を通過すると、変更内容を公開済みのLINEミニアプリに反映できるようになります。

## LIFFプラグインでクイック入力を組み込む 

クイック入力の開発にはLIFF SDKおよび[LIFFプラグイン](https://developers.line.biz/ja/docs/liff/liff-plugin/)を使用します。LIFFプラグインが動作するLIFF SDKのバージョンについては、「[LIFF SDKのバージョン](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#liff-sdk-version)」を参照してください。

LINEミニアプリには、以下の2種類の方法でLIFF SDKを組み込めます。

- [CDNパスを指定してクイック入力を組み込む](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#specify-cdn-path)
- [npmパッケージを利用してクイック入力を組み込む](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#use-npm-package)

LIFFアプリにLIFF SDKを組み込んだら、以下のように[`liff.use()`](https://developers.line.biz/ja/reference/liff/#use)メソッドにクイック入力のLIFFプラグインを渡すことで、LIFFプラグインが有効化されます。

```javascript
liff.use(new LiffCommonProfilePlugin());
await liff.init({ liffId: "xxx" });

const { data, error } = await liff.$commonProfile.get();
liff.$commonProfile.fill(data);
```

これにより`liff`オブジェクトへ`$commonProfile`というプロパティが追加され、以下のようなクイック入力のクライアントAPIが使えるようになります。

- [`liff.$commonProfile.get()`](https://developers.line.biz/ja/reference/line-mini-app/#get-common-profile)
- [`liff.$commonProfile.getDummy()`](https://developers.line.biz/ja/reference/line-mini-app/#get-dummy-common-profile)
- [`liff.$commonProfile.fill()`](https://developers.line.biz/ja/reference/line-mini-app/#fill-common-profile)

### CDNパスを指定してクイック入力を組み込む 

CDNパスを指定する場合、`script`タグを使用してパッケージを読み込むと、windowオブジェクトへ`liffCommonProfile`というプロパティが追加されます。`liffCommonProfile`の内部に存在する`LiffCommonProfilePlugin`というクラスのインスタンスを`liff.use()`の引数に渡します。

```html
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <script src="https://static.line-scdn.net/liff/edge/2/sdk.js"></script>
    <script src="https://static.line-scdn.net/5/liff-common-profile/edge/production/1.0.0/index.umd.cjs"></script>
    <title>LIFF App</title>
  </head>
  <body>

    <script type="module" src="/index.js"></script>
  </body>
</html>
```

```js
liff.use(new liffCommonProfile.LiffCommonProfilePlugin());

const { data, error } = await liff.$commonProfile.get();
liff.$commonProfile.fill(data);
```

詳しくは、『LIFFドキュメント』の「[CDNパスを指定する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#specify-cdn-path)」を参照してください。

### npmパッケージを利用してクイック入力を組み込む 

npmパッケージを利用する場合、パッケージから`LiffCommonProfilePlugin`クラスをインポートして、そのインスタンスを`liff.use()`の引数に渡します。

```sh
$ npm install @line/liff-common-profile-plugin
```

```js
import liff from "@line/liff";
import { LiffCommonProfilePlugin } from "@line/liff-common-profile-plugin";
liff.use(new LiffCommonProfilePlugin());

const { data, error } = await liff.$commonProfile.get();
liff.$commonProfile.fill(data);
```

詳しくは、『LIFFドキュメント』の「[npmパッケージを利用する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#use-npm-package)」を参照してください。

## クイック入力の動作環境 

クイック入力は、ユーザーがiOS版LINEまたはAndroid版LINEを使用している場合のみ動作します。

システム側におけるクイック入力の動作環境は、以下のとおりです。

- [LIFF SDKのバージョン](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#liff-sdk-version)
- [Node.jsのバージョン](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#nodejs-version)

なおLINEミニアプリは、[LINE Front-end Framework（LIFF）](https://developers.line.biz/ja/docs/liff/overview/)の仕組みを利用しています。クイック入力の推奨環境については、『LIFFドキュメント』の「[推奨環境](https://developers.line.biz/ja/docs/liff/overview/#operating-environment)」も併せて参照してください。

<!-- note start -->

**LIFFアプリの動作が保証されるエンドポイントURLの遷移先**

LIFFアプリは、エンドポイントURL（例：`https://example.com/path`）と完全に一致、もしくはエンドポイントURLよりも下の階層（例：`https://example.com/path/to/lower?key1=value1#URL-fragment`）においてのみ動作します。それ以外へ遷移した場合の動作は保証されません。

<!-- note end -->

### LIFF SDKのバージョン 

クイック入力の開発にはLIFFプラグインを使用するため、LIFF SDKはv2.19.0以上を使用してください。LIFFプラグインについて詳しくは、『LIFFドキュメント』の「[LIFFプラグイン](https://developers.line.biz/ja/docs/liff/liff-plugin/)」を参照してください。

### Node.jsのバージョン 

npmを利用してLIFF SDKをインストールする場合、Node.jsのバージョンは18.15.0以上を使用してください。なおCDNパスを指定してLIFF SDKを使用する場合は、Node.jsは不要です。

LIFFアプリにLIFF SDKを組み込む方法について詳しくは、『LIFFドキュメント』の「[LIFFアプリにLIFF SDKを組み込む](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#integrating-sdk)」を参照してください。

## LINE Developersコンソールで選択できるスコープの種類 

LINE Developersコンソールで選択できる、クイック入力のスコープの種類は以下のとおりです。

| スコープ | 説明 |
| --- | --- |
| `commonprofile.name` | ユーザーが登録した「氏名」を取得する権限 |
| `commonprofile.email` | ユーザーが登録した「メールアドレス」を取得する権限 |
| `commonprofile.address` | ユーザーが登録した「住所」を取得する権限 |
| `commonprofile.gender` | ユーザーが登録した「性別」を取得する権限 |
| `commonprofile.birthday` | ユーザーが登録した「誕生日」を取得する権限 |
| `commonprofile.phone` | ユーザーが登録した「電話番号」を取得する権限 |

上記のスコープがLINE Developersコンソールに表示されない場合は、「[Step 2-1. クイック入力の利用申請を行い、承認を得る](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#process-step-2-1)」を参照してください。

なおユーザーが「[チャネル同意画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#consent-screen-settings)」で同意する際は、一部のスコープだけを選択して許可することはできません。「アカウントセンターでの管理情報（共通プロフィール）」として対象のスコープを一括で許可するか、あるいは許可しない形になります。

## 取得できる共通プロフィールのスコープと戻り値 

[`liff.$commonProfile.get()`](https://developers.line.biz/ja/reference/line-mini-app/#get-common-profile)および[`liff.$commonProfile.getDummy()`](https://developers.line.biz/ja/reference/line-mini-app/#get-dummy-common-profile)で取得できる共通プロフィールのスコープと、それぞれの戻り値は以下のとおりです。

| 番号 | `scopes` | 説明 | データ型 | 戻り値の最大文字数<br/>（半角英数字の場合） | 戻り値の最大文字数<br/>（ひらがな漢字の場合） | 戻り値の説明 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | `family-name` | 氏名（姓） | string | 100 | 50 |  |
| 2 | `given-name` | 氏名（名） | string | 100 | 50 |  |
| 3 | `family-name-kana` | フリガナ氏名（姓） | string | 100 | 50 |  |
| 4 | `given-name-kana` | フリガナ氏名（名） | string | 100 | 50 |  |
| 5 | `sex-enum` | 性別 | number | 1（固定長） | N/A | <ul><li>`0`：男性</li><li>`1`：女性</li><li>`2`：その他</li><li>`3`：無回答</li></ul> |
| 6 | `bday-day` | 誕生日 | number | 2 | N/A |  |
| 7 | `bday-month` | 誕生月 | number | 2 | N/A |  |
| 8 | `bday-year` | 誕生年 | number | 4 | N/A |  |
| 9 | `tel` | 電話番号 | string | 200 | N/A |  |
| 10 | `email` | メールアドレス | string | 200 | N/A |  |
| 11 | `postal-code` | 郵便番号 | string | 47 | N/A |  |
| 12 | `address-level1` | 住所第一 | string | 53 | 53 |  |
| 13 | `address-level2` | 住所第二 | string | 53 | 53 |  |
| 14 | `address-level3` | 住所第三 | string | 100 | 69 |  |
| 15 | `address-level4` | 住所第四 | string | 100 | 69 |  |

なおアカウントセンターの共通プロフィールは、LINEやYahoo! JAPANで登録されているプロフィールを組み合わせて設定されます。ユーザーがアカウントセンターを利用していない場合は、LINEのプロフィール情報が共通プロフィールとして自動入力されます。

## 取得できる共通プロフィールのダミーデータ 

[`liff.$commonProfile.getDummy()`](https://developers.line.biz/ja/reference/line-mini-app/#get-dummy-common-profile)を使うと、共通プロフィールのダミーデータを取得できます。用意されている10種類の中から、`caseId`で取得するダミーデータを指定できます。

| `caseId` | `family-name`  | `given-name`  | `family-name-kana`  | `given-name-kana`  | `sex-enum` | `bday-day` | `bday-month` | `bday-year` | `tel`  | `email`  | `postal-code`  | `address-level1`  | `address-level2`  | `address-level3`  | `address-level4` |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 見本田 | 見本夫 | ダミータ | ダミーオ | 0 | 12 | 3 | 1998 | 09001234567 | dummy_39@yahoo.co.jp | 1020094 | 東京都 | 千代田区 | 紀尾井町1-2 | 東京ガーデンテラス紀尾井町 |
| 2 |  |  |  |  | 1 | 12 | 3 | 1998 | 09001234567 | dummy_39@yahoo.co.jp | N5X 1N7 | 東京都 |  | 紀尾井町1-2 | 東京ガーデンテラス紀尾井町 |
| 3 | 見本田 |  | ダミータ |  | 2 |  |  |  | 09001234567 | dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dummy_39dumm@yahoo.co.jp | 102-0094 | 東京都 | 千代田区 |  | 東京ガーデンテラス紀尾井町 |
| 4 |  | 見本夫 |  | ダミーオ | 3 | 12 | 3 | 1998 | 0901234567 | dummy_39@yahoo.co.jp | 1077 AA2 15000N5X 1N7107715000X 1077 AA2 15000N5X 1N71 | 東京都 | 千代田区 | 紀尾井町1-2 |  |
| 5 | Daimta | Damio | ダミータ | ダミーオ | 0 | 12 | 3 | 1998 | 09001234567 |  | 1020094 | Tokyo | Chiyoda-ku | Kioi-cho,1-2 | Tokyo Garden terrace Kioi-cho, |
| 6 | 1234 | 4321 | ダミータ | ダミーオ | 1 |  |  | 1998 | 090-1234-5678 | dummy_39@yahoo.co.jp |  | ﾄｳｷｮｳﾄ | ﾁﾖﾀﾞｸ | ｷｵｲﾁｮｳ1-2 | ﾄｳｷｮｳｶﾞｰﾃﾞﾝﾃﾗｽｷｵｲﾁｮｳ |
| 7 | ﾀﾞﾐｰﾀ | ﾀﾞﾐｵ | ダミータ | ダミーオ | 2 |  | 3 |  | 09001234567090012345670900123456709001234567090012345670900123456709001234567090012345670900123456709001234567090012345670900123456709001234567090012345670900123456709001234567090012345670900123456709 | dummy_39@yahoo.co.jp | 1020094 |  |  |  |  |
| 8 | ダミ！？ | ダミ夫@ | ダミータ | ダミーオ | 3 | 12 |  | 1998 | 09001234567 | dummy_39@yahoo.co.jp | 1020094 | 🍀 | 🍀🍀 | 🍀🍀🍀 | 🍀🍀🍀🍀 |
| 9 | 🐶🐶🐶 | ダミ💚 | ダミータ | ダミーオ | 0 | 12 | 3 | 1998 |  | dummy_39@yahoo.co.jp | 102-0094 | 東京都東京都東京都東京都東京都東京都東京都東京都東京都東京都東京都東京都東京都東京都東京都東京都東京都東京都東京都東京都東京都東京都東京都東京都東京都東京都 | 千代田区千代田区千代田区千代田区千代田区千代田区千代田区千代田区千代田区千代田区千代田区千代田区千代田区千 | 紀尾井町1-2紀尾井町1-2紀尾井町1-2紀尾井町1-2紀尾井町1-2紀尾井町1-2紀尾井町1-2紀尾井町1-2紀尾井町1-2紀尾井町1-2紀尾井町1-2紀尾井町1-2紀尾井町1-2紀尾井町1-2紀尾井町1-2紀尾井町1-2紀尾井町1-2紀尾井町1-2紀尾井町1-2紀尾井町1-2 | 東京ガーデンテラス紀尾井町東京ガーデンテラス紀尾井町東京ガーデンテラス紀尾井町東京ガーデンテラス紀尾井町東京ガーデンテラス紀尾井町東京ガーデンテラス紀尾井町東京ガーデンテラス紀尾井町 |
| 10 | ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田ダミー田 | ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫ダミー夫 | ダミータダミータダミータダミータダミータダミータダミータダミータダミータダミータダミータダミータダミータダミータダミータダミータダミータダミータダミータダミータダミータダミータダミータダミータダミータ | ダミーオダミーオダミーオダミーオダミーオダミーオダミーオダミーオダミーオダミーオダミーオダミーオダミーオダミーオダミーオダミーオダミーオダミーオダミーオダミーオダミーオダミーオダミーオ | 1 | 12 | 3 | 1998 | 09001234567 | dummy_39@yahoo.co.jp | N5X 1N7 |  | 千代田区 | 紀尾井町1-2 | 東京ガーデンテラス紀尾井町 |

## 共通プロフィールの情報を取得するときのオプション 

[`liff.$commonProfile.get()`](https://developers.line.biz/ja/reference/line-mini-app/#get-common-profile)で共通プロフィールの情報を取得するとき、各スコープに対して以下のオプションを指定できます。これらのオプションはデフォルトではすべて`true`になっているため、オプションを無効にしたい場合は`false`を指定してください。

| プロパティ | デフォルト値 | 内容 | 指定可能なスコープ |
| --- | --- | --- | --- |
| `excludeEmojis` | true | 文字列内の絵文字を削除するかどうか。 | <ul><li>`given-name`</li><li>`family-name`</li></ul> |
| `excludeNonJp` | true | 12桁以上の電話番号を排除するかどうか。`true`の場合、電話番号が12桁以上のときは、空文字とエラー情報を返します。 | <ul><li>`tel`</li></ul> |
| `digitsOnly` | true | 数字以外の郵便番号を排除するかどうか。`true`の場合、郵便番号に数字以外が含まれているときは、空文字とエラー情報を返します。 | <ul><li>`postal-code`</li></ul> |

## APIリファレンス 

クイック入力で使用するクライアントAPIについて詳しくは、『LINEミニアプリAPIリファレンス』の「[共通プロフィールのクイック入力](https://developers.line.biz/ja/reference/line-mini-app/#quick-fill)」を参照してください。
