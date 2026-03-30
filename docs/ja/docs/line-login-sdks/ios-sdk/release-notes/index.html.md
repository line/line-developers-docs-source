# リリースノート

<!-- note start -->

**バージョン5.0.0以降のリリースノートはGitHubリポジトリで公開しています**

バージョン5.0.0以降のLINE SDK for iOSのリリースノートは、GitHubリポジトリで公開しています。詳しくは、[Releases](https://github.com/line/line-sdk-ios-swift/releases)を参照してください。

<!-- note end -->

2018/12/13

## LINE SDK 5.0.0 for iOSの日本語版リファレンスがリリースされました

LINE SDK 5.0.0 for iOSの日本語版リファレンスがリリースされました。

- [LINE SDK for iOS Swiftリファレンス（英語）](https://developers.line.biz/en/reference/ios-sdk-swift/)
- [LINE SDK for iOS Objective-Cリファレンス（英語）](https://developers.line.biz/en/reference/ios-sdk-objc/)

2018/11/29

## LINE SDK 5.0.0 for iOSの日本語版ガイドがリリースされました

LINE SDK 5.0.0 for iOSの日本語版ガイドがリリースされました。

- [LINE SDK for iOSガイド](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/)

リファレンスも近日中に日本語化される予定です。

- [LINE SDK for iOS Swiftリファレンス（英語）](https://developers.line.biz/en/reference/ios-sdk-swift/)
- [LINE SDK for iOS Objective-Cリファレンス（英語）](https://developers.line.biz/en/reference/ios-sdk-objc/)

2018/11/20

## LINE SDK 5.0.0 for iOSがリリースされました

LINE SDK 5.0.0 for iOSがリリースされました。インストール方法と使い方については、『[LINE SDK for iOSガイド](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/)』を参照してください。このガイドは、近日中に日本語化されます。

#### 変更点

##### LINEログイン v2.1およびSocial API v2.1に対応

ユーザーがLINEログインを使ってアプリにログインするときに、アプリに許可する権限をスコープとして設定できます。これにより、アクセストークンの取得時に、ログインリクエストに設定したスコープに応じたユーザー情報を含むIDトークンを取得できます。

ログインするユーザーに対して、ボットを友だち追加するオプションを表示できます。ユーザーとボットの間の友だち関係は、ログインレスポンスやSocial APIを使って確認できます。

##### Swiftで書かれた新しいSDK

Swiftで開発されたLINE SDK for iOS Swiftを使うと、最新の方法でLINEのAPIを実装できます。LINE SDK 5.0.0 for iOS Objective-Cは、Objective-C向けとしては最後のSDKです。

##### オープンソース化

LINE SDK for iOS Swiftはオープンソース化されています。[リポジトリ](https://github.com/line/line-sdk-ios-swift)にアクセスして、提供されているコードやサンプルを確認できます。

##### 詳しいリファレンス

ソースコードに基づいた、より詳しいリファレンスを利用できます。詳しくは、以下を参照してください。これらのリファレンスは、近日中に日本語化されます。

- [LINE SDK for iOS Swiftリファレンス（英語）](https://developers.line.biz/en/reference/ios-sdk-swift/)
- [LINE SDK for iOS Objective-Cリファレンス（英語）](https://developers.line.biz/en/reference/ios-sdk-objc/)

2018/04/13

## LINE SDK 4.1.1 for iOSがリリースされました

LINE SDK 4.1.1 for iOSがリリースされました。LINE SDKのダウンロードについて詳しくは、以下のリンクを参照してください。

- [LINE SDKをダウンロード](https://developers.line.biz/ja/docs/downloads/)

変更点：

- ログアウト後も`LineSDKLogin`オブジェクトにアクセストークンがキャッシュされたままになるという問題が解決されました。

2018/01/29

## LINE SDK 4.1.0 for iOSがリリースされました

LINE SDK 4.1.0 for iOSがリリースされました。LINE SDKのダウンロードについて詳しくは、以下のリンクを参照してください。

- [LINE SDKをダウンロード](https://developers.line.biz/ja/docs/downloads/)

変更点：

- ウェブログインの実行時に、外部ブラウザではなくSafari View Controllerが使用されるようになりました。

2017/03/22

##  LINE SDK for iOS CocoaPod released

We have released the LINE SDK for iOS on CocoaPods. You can now download the LINE SDK for iOS using CocoaPods for your Objective-C and Swift projects.

For information on how to download the SDK with CocoaPods, see the link below.

- Download with [CocoaPods](https://cocoapods.org/)

2017/01/27

## LINE SDK 4.0.1 for iOS released

The LINE SDK 4.0.1 for iOS has been released. You can download the SDK from the following page.

- [Download LINE SDK](https://developers.line.biz/ja/docs/downloads/)

Changes:

- Fixed an issue which causes an authentication error when using Web Login.

2016/12/13

## Change to requirement on whitelisting LINE domains

Whitelisting LINE domains is no longer a requirement for using the LINE SDK for iOS. As such, the documentation on whitelisting LINE domains found in the Settings for iOS 9 or later section has been removed.

2016/10/07

## The LINE SDK 3.2.1 for iOS released

The LINE SDK for iOS has been updated to version 3.2.1. You can download it from the LINE SDK archives on the following page:

- [Download LINE SDK](https://developers.line.biz/ja/docs/downloads/)

Changes:

- `LineAdapter+Login.framework` and `LineAdapterUI.framework` merged to `LineAdapter.framework`.
- Definition changed for swift.

In addition, the LINE SDK starter application has been revised to be compatibility with this version of the SDK. You can clone or download it from the GitHub repository below.

- [https://github.com/line/line-sdk-starter-ios](https://github.com/line/line-sdk-starter-ios)
