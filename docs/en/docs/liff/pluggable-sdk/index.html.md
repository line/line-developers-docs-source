# Pluggable SDK

<!-- table of contents -->

## What is the pluggable SDK 

The pluggable SDK is a feature that allows you to choose which LIFF APIs to include in the LIFF SDK.

By including only the LIFF APIs used by your LIFF app, you can reduce the LIFF SDK file size by up to about 34%. As a result, you can improve the display speed of your LIFF app.

## Use conditions of the pluggable SDK 

The pluggable SDK is only available in the npm version of LIFF v2.22.0 or later. It's not available in the CDN version. For more information about using the npm package, see [Use the npm package](https://developers.line.biz/en/docs/liff/developing-liff-apps/#use-npm-package).

## How to use the pluggable SDK 

The pluggable SDK can be used as follows:

- [Import the liff object](https://developers.line.biz/en/docs/liff/pluggable-sdk/#import-liff-object)
- [Activate the LIFF APIs](https://developers.line.biz/en/docs/liff/pluggable-sdk/#activate-liff-api)

### Import the liff object 

First, import the `liff` object from `@line/liff/core`.

```js
import liff from "@line/liff/core";
```

This `liff` object includes only the following properties and methods:

- [`liff.id`](https://developers.line.biz/en/reference/liff/#id) property
- [`liff.ready`](https://developers.line.biz/en/reference/liff/#ready) property
- [`liff.init()`](https://developers.line.biz/en/reference/liff/#initialize-liff-app) method
- [`liff.getVersion()`](https://developers.line.biz/en/reference/liff/#get-version) method
- [`liff.use()`](https://developers.line.biz/en/reference/liff/#use) method

To use LIFF APIs other than those listed above, import the corresponding modules. In the following example, the corresponding modules are imported for the [`liff.getOS()`](https://developers.line.biz/en/reference/liff/#get-os) method and the [`liff.getAppLanguage()`](https://developers.line.biz/en/reference/liff/#get-app-language) method:

```js
import liff from "@line/liff/core";
import GetOS from "@line/liff/get-os";
import GetAppLanguage from "@line/liff/get-app-language";
```

For more information on the modules corresponding to each LIFF API, see [LIFF API and the corresponding module list](https://developers.line.biz/en/docs/liff/pluggable-sdk/#liff-api-and-module-list).

### Activate the LIFF APIs 

Next, pass the imported LIFF API modules to the `liff.use()` method to activate the LIFF APIs. Since the LIFF API modules are defined as classes, you must pass the instances to the `liff.use()` method.

```js
import liff from "@line/liff/core";
import GetOS from "@line/liff/get-os";
import GetAppLanguage from "@line/liff/get-app-language";

liff.use(new GetOS());
liff.use(new GetAppLanguage());
```

Once the LIFF APIs are activated, you can use the LIFF APIs.

In the example below, the activated `liff.getOS()` method and the `liff.getAppLanguage()` method are available, but the unactivated `liff.login()` method isn't available:

```js
import liff from "@line/liff/core";
import GetOS from "@line/liff/get-os";
import GetAppLanguage from "@line/liff/get-app-language";

liff.use(new GetOS());
liff.use(new GetAppLanguage());

liff.init({
  liffId: "123456-abcedfg",
});

liff.getOS(); // Available
liff.getAppLanguage(); // Available
liff.login(); // Not available
```

## Important points about the pluggable SDK 

Due to technical limitations, the `liff.use()` method should be executed before the `liff.init()` method. The execution of the `liff.use()` method after the `liff.init()` method isn't guaranteed to work.

### Example of correct execution of the liff.use() method 

```js
import liff from "@line/liff/core";
import GetOS from "@line/liff/get-os";

// The liff.use() method is executed before the liff.init() method
liff.use(new GetOS());

liff.init({
  liffId: "123456-abcedfg",
});
```

### Example of wrong execution of the liff.use() method 

```js
import liff from "@line/liff/core";
import GetOS from "@line/liff/get-os";

liff.init({
  liffId: "123456-abcedfg",
});

// The liff.use() method is executed after the liff.init() method
liff.use(new GetOS());
```

## LIFF API and the corresponding module list 

| LIFF API | Module |
| --- | --- |
| [`liff.getOS()`](https://developers.line.biz/en/reference/liff/#get-os) | `@line/liff/get-os` |
| [`liff.getAppLanguage()`](https://developers.line.biz/en/reference/liff/#get-app-language) | `@line/liff/get-app-language` |
| [`liff.getLanguage()`](https://developers.line.biz/en/reference/liff/#get-language) (deprecated) | `@line/liff/get-language` |
| [`liff.getLineVersion()`](https://developers.line.biz/en/reference/liff/#get-line-version) | `@line/liff/get-line-version` |
| [`liff.getContext()`](https://developers.line.biz/en/reference/liff/#get-context) | `@line/liff/get-context` |
| [`liff.isInClient()`](https://developers.line.biz/en/reference/liff/#is-in-client) | `@line/liff/is-in-client` |
| [`liff.isLoggedIn()`](https://developers.line.biz/en/reference/liff/#is-logged-in) | `@line/liff/is-logged-in` |
| [`liff.isApiAvailable()`](https://developers.line.biz/en/reference/liff/#is-api-available) | `@line/liff/is-api-available` |
| [`liff.login()`](https://developers.line.biz/en/reference/liff/#login) | `@line/liff/login` |
| [`liff.logout()`](https://developers.line.biz/en/reference/liff/#logout) | `@line/liff/logout` |
| [`liff.getAccessToken()`](https://developers.line.biz/en/reference/liff/#get-access-token) | `@line/liff/get-access-token` |
| [`liff.getIDToken()`](https://developers.line.biz/en/reference/liff/#get-id-token) | `@line/liff/get-id-token` |
| [`liff.getDecodedIDToken()`](https://developers.line.biz/en/reference/liff/#get-decoded-id-token) | `@line/liff/get-decoded-id-token` |
| [`liff.permission.getGrantedAll()`](https://developers.line.biz/en/reference/liff/#permission-get-granted-all)<br><br>[`liff.permission.query()`](https://developers.line.biz/en/reference/liff/#permission-query)<br><br>[`liff.permission.requestAll()`](https://developers.line.biz/en/reference/liff/#permission-request-all) | `@line/liff/permission` |
| [`liff.getProfile()`](https://developers.line.biz/en/reference/liff/#get-profile) | `@line/liff/get-profile` |
| [`liff.getFriendship()`](https://developers.line.biz/en/reference/liff/#get-friendship) | `@line/liff/get-friendship` |
| [`liff.openWindow()`](https://developers.line.biz/en/reference/liff/#open-window) | `@line/liff/open-window` |
| [`liff.closeWindow()`](https://developers.line.biz/en/reference/liff/#close-window) | `@line/liff/close-window` |
| [`liff.sendMessages()`](https://developers.line.biz/en/reference/liff/#send-messages) | `@line/liff/send-messages` |
| [`liff.shareTargetPicker()`](https://developers.line.biz/en/reference/liff/#share-target-picker) | `@line/liff/share-target-picker` |
| [`liff.scanCodeV2()`](https://developers.line.biz/en/reference/liff/#scan-code-v2) | `@line/liff/scan-code-v2` |
| [`liff.scanCode()`](https://developers.line.biz/en/reference/liff/#scan-code) (deprecated) | `@line/liff/scan-code` |
| [`liff.permanentLink.createUrlBy()`](https://developers.line.biz/en/reference/liff/#permanent-link-create-url-by)<br><br>[`liff.permanentLink.createUrl()`](https://developers.line.biz/en/reference/liff/#permanent-link-create-url)<br><br>[`liff.permanentLink.setExtraQueryParam()`](https://developers.line.biz/en/reference/liff/#permanent-linke-set-extra-query-param) | `@line/liff/permanent-link` |
| [`liff.i18n.setLang()`](https://developers.line.biz/en/reference/liff/#i18n-set-lang) | `@line/liff/i18n` |
| [`liff.createShortcutOnHomeScreen()`](https://developers.line.biz/en/reference/liff/#create-shortcut-on-home-screen) | `@line/liff/create-shortcut-on-home-screen` |
