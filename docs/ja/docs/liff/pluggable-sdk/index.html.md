# プラガブルSDK

<!-- table of contents -->

## プラガブルSDKとは 

プラガブルSDKとは、LIFF SDKに含めるLIFF APIを選択できる機能です。

LIFFアプリで利用するLIFF APIのみをLIFF SDKに含めることで、LIFF SDKのファイルサイズを最大約34%削減できます。その結果、LIFFアプリの表示速度を向上させることができます。

## プラガブルSDKの使用条件 

LIFF v2.22.0以降のnpmパッケージ版でのみ利用できます。CDN版では利用できません。npmパッケージの利用方法について詳しくは、「[npmパッケージを利用する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#use-npm-package)」を参照してください。

## プラガブルSDKの使用方法 

プラガブルSDKの使用方法は、以下のとおりです。

- [liffオブジェクトをインポートする](https://developers.line.biz/ja/docs/liff/pluggable-sdk/#import-liff-object)
- [LIFF APIを有効化する](https://developers.line.biz/ja/docs/liff/pluggable-sdk/#activate-liff-api)

### liffオブジェクトをインポートする 

まず、`liff`オブジェクトを`@line/liff/core`からインポートします。

```js
import liff from "@line/liff/core";
```

この`liff`オブジェクトには、以下のプロパティとメソッドのみが含まれています。

- [`liff.id`](https://developers.line.biz/ja/reference/liff/#id)プロパティ
- [`liff.ready`](https://developers.line.biz/ja/reference/liff/#ready)プロパティ
- [`liff.init()`](https://developers.line.biz/ja/reference/liff/#initialize-liff-app)メソッド
- [`liff.getVersion()`](https://developers.line.biz/ja/reference/liff/#get-version)メソッド
- [`liff.use()`](https://developers.line.biz/ja/reference/liff/#use)メソッド

上記以外のLIFF APIを利用するには、対応するモジュールをインポートします。以下の例では、[`liff.getOS()`](https://developers.line.biz/ja/reference/liff/#get-os)メソッドと[`liff.getAppLanguage()`](https://developers.line.biz/ja/reference/liff/#get-app-language)メソッドに対応するモジュールをインポートしています。

```js
import liff from "@line/liff/core";
import GetOS from "@line/liff/get-os";
import GetAppLanguage from "@line/liff/get-app-language";
```

各LIFF APIに対応するモジュールについては、「[LIFF APIと対応するモジュール一覧](https://developers.line.biz/ja/docs/liff/pluggable-sdk/#liff-api-and-module-list)」を参照してください。

### LIFF APIを有効化する 

次に、インポートしたLIFF APIのモジュールを`liff.use()`メソッドに渡し、LIFF APIを有効化します。LIFF APIのモジュールはクラスで定義されているため、`liff.use()`メソッドにインスタンスを渡す必要があります。

```js
import liff from "@line/liff/core";
import GetOS from "@line/liff/get-os";
import GetAppLanguage from "@line/liff/get-app-language";

liff.use(new GetOS());
liff.use(new GetAppLanguage());
```

LIFF APIを有効化すると、LIFF APIを利用できるようになります。

以下の例では、有効化した`liff.getOS()`メソッドと`liff.getAppLanguage()`メソッドは利用できますが、有効化していない`liff.login()`メソッドは利用できません。

```js
import liff from "@line/liff/core";
import GetOS from "@line/liff/get-os";
import GetAppLanguage from "@line/liff/get-app-language";

liff.use(new GetOS());
liff.use(new GetAppLanguage());

liff.init({
  liffId: "123456-abcedfg",
});

liff.getOS(); // 利用できる
liff.getAppLanguage(); // 利用できる
liff.login(); // 利用できない
```

## プラガブルSDKの注意事項 

技術的な制約から、`liff.use()`メソッドは`liff.init()`メソッドより前に実行してください。`liff.init()`メソッドを実行した後に`liff.use()`メソッドを実行した場合の動作は保証されません。

### liff.use()メソッドの正しい実行例 

```js
import liff from "@line/liff/core";
import GetOS from "@line/liff/get-os";

// liff.use()メソッドをliff.init()メソッドより前に実行している
liff.use(new GetOS());

liff.init({
  liffId: "123456-abcedfg",
});
```

### liff.use()メソッドの間違った実行例 

```js
import liff from "@line/liff/core";
import GetOS from "@line/liff/get-os";

liff.init({
  liffId: "123456-abcedfg",
});

// liff.use()メソッドをliff.init()メソッドより後に実行している
liff.use(new GetOS());
```

## LIFF APIと対応するモジュール一覧 

| LIFF API | モジュール |
| --- | --- |
| [`liff.getOS()`](https://developers.line.biz/ja/reference/liff/#get-os) | `@line/liff/get-os` |
| [`liff.getAppLanguage()`](https://developers.line.biz/ja/reference/liff/#get-app-language) | `@line/liff/get-app-language` |
| [`liff.getLanguage()`](https://developers.line.biz/ja/reference/liff/#get-language)（非推奨） | `@line/liff/get-language` |
| [`liff.getLineVersion()`](https://developers.line.biz/ja/reference/liff/#get-line-version) | `@line/liff/get-line-version` |
| [`liff.getContext()`](https://developers.line.biz/ja/reference/liff/#get-context) | `@line/liff/get-context` |
| [`liff.isInClient()`](https://developers.line.biz/ja/reference/liff/#is-in-client) | `@line/liff/is-in-client` |
| [`liff.isLoggedIn()`](https://developers.line.biz/ja/reference/liff/#is-logged-in) | `@line/liff/is-logged-in` |
| [`liff.isApiAvailable()`](https://developers.line.biz/ja/reference/liff/#is-api-available) | `@line/liff/is-api-available` |
| [`liff.login()`](https://developers.line.biz/ja/reference/liff/#login) | `@line/liff/login` |
| [`liff.logout()`](https://developers.line.biz/ja/reference/liff/#logout) | `@line/liff/logout` |
| [`liff.getAccessToken()`](https://developers.line.biz/ja/reference/liff/#get-access-token) | `@line/liff/get-access-token` |
| [`liff.getIDToken()`](https://developers.line.biz/ja/reference/liff/#get-id-token) | `@line/liff/get-id-token` |
| [`liff.getDecodedIDToken()`](https://developers.line.biz/ja/reference/liff/#get-decoded-id-token) | `@line/liff/get-decoded-id-token` |
| [`liff.permission.getGrantedAll()`](https://developers.line.biz/ja/reference/liff/#permission-get-granted-all)<br><br>[`liff.permission.query()`](https://developers.line.biz/ja/reference/liff/#permission-query)<br><br>[`liff.permission.requestAll()`](https://developers.line.biz/ja/reference/liff/#permission-request-all) | `@line/liff/permission` |
| [`liff.getProfile()`](https://developers.line.biz/ja/reference/liff/#get-profile) | `@line/liff/get-profile` |
| [`liff.getFriendship()`](https://developers.line.biz/ja/reference/liff/#get-friendship) | `@line/liff/get-friendship` |
| [`liff.openWindow()`](https://developers.line.biz/ja/reference/liff/#open-window) | `@line/liff/open-window` |
| [`liff.closeWindow()`](https://developers.line.biz/ja/reference/liff/#close-window) | `@line/liff/close-window` |
| [`liff.sendMessages()`](https://developers.line.biz/ja/reference/liff/#send-messages) | `@line/liff/send-messages` |
| [`liff.shareTargetPicker()`](https://developers.line.biz/ja/reference/liff/#share-target-picker) | `@line/liff/share-target-picker` |
| [`liff.scanCodeV2()`](https://developers.line.biz/ja/reference/liff/#scan-code-v2) | `@line/liff/scan-code-v2` |
| [`liff.scanCode()`](https://developers.line.biz/ja/reference/liff/#scan-code)（非推奨） | `@line/liff/scan-code` |
| [`liff.permanentLink.createUrlBy()`](https://developers.line.biz/ja/reference/liff/#permanent-link-create-url-by)<br><br>[`liff.permanentLink.createUrl()`](https://developers.line.biz/ja/reference/liff/#permanent-link-create-url)<br><br>[`liff.permanentLink.setExtraQueryParam()`](https://developers.line.biz/ja/reference/liff/#permanent-linke-set-extra-query-param) | `@line/liff/permanent-link` |
| [`liff.i18n.setLang()`](https://developers.line.biz/ja/reference/liff/#i18n-set-lang) | `@line/liff/i18n` |
| [`liff.createShortcutOnHomeScreen()`](https://developers.line.biz/ja/reference/liff/#create-shortcut-on-home-screen) | `@line/liff/create-shortcut-on-home-screen` |
