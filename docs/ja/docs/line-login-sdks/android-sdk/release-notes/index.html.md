# リリースノート

<!-- note start -->

**バージョン5.0.0以降のリリースノートはGitHubリポジトリで公開しています**

バージョン5.0.0以降のLINE SDK for Androidのリリースノートは、GitHubリポジトリで公開しています。詳しくは、[Releases](https://github.com/line/line-sdk-android/releases)を参照してください。

<!-- note end -->

2018/12/13

## LINE SDK 5.0.0 for Androidの日本語版リファレンスがリリースされました

LINE SDK 5.0.0 for Androidの日本語版リファレンスがリリースされました。

- [LINE SDK for Androidリファレンス（英語）](https://developers.line.biz/en/reference/android-sdk/)

2018/11/30

## LINE SDK for Android 4.0.10がリリースされました

LINE SDK 4.0.10 for Androidがリリースされました。LINE SDKのダウンロードについて詳しくは、以下のリンクを参照してください。

- [LINE SDKをダウンロード](https://developers.line.biz/ja/docs/downloads/)

変更点：

- LINEを無効化した後でLINEログインで認証すると、アクティビティが見つからないという問題が解決されました。

さらに簡単にアプリ開発を進めていただけるよう、引き続きSDKの品質向上に努めていきます。

2018/11/29

## LINE SDK 5.0.0 for Androidの日本語版ガイドがリリースされました

LINE SDK 5.0.0 for Androidの日本語版ガイドがリリースされました。

- [LINE SDK for Androidガイド](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/)

リファレンスも近日中に日本語化される予定です。

- [LINE SDK for Androidリファレンス（英語）](https://developers.line.biz/en/reference/android-sdk/)

2018/11/20

## LINE SDK 5.0.0 for Androidがリリースされました

LINE SDK 5.0.0 for Androidがリリースされました。インストール方法と使い方については、『[LINE SDK for Androidガイド](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/)』を参照してください。このガイドは、近日中に日本語化されます。

#### 変更点

##### LINEログイン v2.1およびSocial API v2.1に対応

ユーザーがLINEログインを使ってアプリにログインするときに、アプリに許可する権限をスコープとして設定できます。これにより、アクセストークンの取得時に、ログインリクエストに設定したスコープに応じたユーザー情報を含むIDトークンを取得できます。

ログインするユーザーに対して、ボットを友だち追加するオプションを表示できます。ユーザーとボットの間の友だち関係は、ログインレスポンスやSocial APIを使って確認できます。

##### オープンソース化

バージョン5.0.0から、LINE SDK for Androidはオープンソース化されました。[リポジトリ](https://github.com/line/line-sdk-android)にアクセスして、提供されているコードやサンプルを確認できます。

##### 詳しいリファレンス

ソースコードに基づいた、より詳しいリファレンスを利用できます。詳しくは、『[LINE SDK for Androidリファレンス（英語）](https://developers.line.biz/en/reference/android-sdk/)』を参照してください。このリファレンスは、近日中に日本語化されます。

2018/03/12

## LINE SDK 4.0.8 for Androidがリリースされました

LINE SDK 4.0.8 for Androidがリリースされました。LINE SDKのダウンロードについて詳しくは、以下のリンクを参照してください。

- [LINE SDKをダウンロード](https://developers.line.biz/ja/docs/downloads/)

変更点：

- LINEを一度も使用していない場合、SDKを組み込んだアプリにログインしようとすると、処理が実行中であることを示すインジケーターが表示されたままになるという問題が解決されました。

さらに簡単にアプリ開発を進めていただけるよう、引き続きSDKの品質向上に努めていきます。

2018/02/06

## LINE SDK 4.0.7 for Androidがリリースされました

LINE SDK 4.0.7 for Androidがリリースされました。LINE SDKのダウンロードについて詳しくは、以下のリンクを参照してください。

- [LINE SDKをダウンロード](https://developers.line.biz/ja/docs/downloads/)

変更点：

- ユーザーがホームボタンを使ってLINEを終了した後で、SDKを組み込んだアプリを開いたときLINEで認証処理が完了していないと、クラッシュが発生するという問題が解決されました。

さらに簡単にアプリ開発を進めていただけるよう、引き続きSDKの品質向上に努めていきます。

2017/09/29

## LINE SDK 4.0.6 for Androidがリリースされました

LINE SDK 4.0.6 for Androidがリリースされました。LINE SDKのダウンロードについて詳しくは、以下のリンクを参照してください。

- [LINE SDKをダウンロード](https://developers.line.biz/ja/docs/downloads/)

変更点：

- LINEのパスコード入力画面で戻るボタンをタップすると、処理が実行中であることを示すインジケーターが表示されたままになるという問題が解決されました。

さらに簡単にアプリ開発を進めていただけるよう、引き続きSDKの品質向上に努めていきます。

2017/06/02

## LINE SDK 4.0.5 for Android released

The LINE SDK 4.0.5 for Android has been released. For more information on downloading the LINE SDK, see below.

- [Download LINE SDK](https://developers.line.biz/ja/docs/downloads/)

Changes:

- Fixed an issue where a runtime error occurs upon calling `startActivityForActivity` with a login intent when using `appcompat` version 25.0.0 or higher.

2017/04/26

## LINE SDK 4.0.4 for Android released

The LINE SDK 4.0.4 for Android has been released. For more information on download the LINE SDK, see below.

- [Download LINE SDK](https://developers.line.biz/ja/docs/downloads/)

Changes:

- Made a minor change to the SDK’s authentication logic to fix a problem where `onActivityResult` does not get executed during app-to-app login.
- Fixed a known issue in 4.0.2 where `onActivityResult` returns a result of “CANCEL” on the first time that a user logs into an application using app-to-app login.

2017/04/10

## LINE SDK 4.0.2 for Android released

The LINE SDK 4.0.2 for Android has been released. You can download the SDK from the following page.

- [Download LINE SDK](https://developers.line.biz/ja/docs/downloads/)

Changes:

- Fixed an issue where browser login fails with an INTERNAL_ERROR on Android 4.x devices.

Known issues:

- On Android 4.x devices, onActivityResult returns a result of “CANCEL” the first time that a user logs into an application using the app-to-app login. However, the user will be able to successfully log in from their second attempt. This issue is caused by a problem in LINE and will be resolved in a future update.

2016/10/14

## LINE SDK 3.1.21 for Android released

The LINE SDK for Android has been updated to version 3.1.21. You can download it from the LINE SDK archives on the following page:

- [Download LINE SDK](https://developers.line.biz/ja/docs/downloads/)

Changes:

- Updated to prevent build warnings.

2016/10/11

## LINE SDK 3.1.20 for Android released

The LINE SDK for Android has been updated to version 3.1.20. You can download it from the LINE SDK archives on the following page:

- [Download LINE SDK](https://developers.line.biz/ja/docs/downloads/)

Changes:

- Updated build with Java 1.7 for compatibility.

2016/03/15

## LINE SDK 3.1.19 for Android version released

The LINE SDK for Android has been updated to version 3.1.19. You can download it from the LINE SDK archives on the following page:

- [Download LINE SDK](https://developers.line.biz/ja/docs/downloads/)

Changes:

- Fixed login error issue when user attempts to login again

2016/03/09

## LINE SDK 3.1.18 for Android released

The LINE SDK for Android has been updated to version 3.1.18. You can download it from the LINE SDK archives on the following page:

- [Download LINE SDK](https://developers.line.biz/ja/docs/downloads/)

Changes:

- Added support for 64-bit architecture
- Added the locale property to the login method
- Fixed some bugs
