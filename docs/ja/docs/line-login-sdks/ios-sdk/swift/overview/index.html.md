# LINE SDK for iOS Swiftの概要

Swiftで開発されたLINE SDK for iOS Swiftを使うと、最新の方法でLINEプラットフォームのAPIを実装できます。このSDKに含まれる機能は、個人に合わせたユーザーエクスペリエンスを提供する魅力的なiOSアプリの開発に役立ちます。

## 機能 

LINE SDK for iOS Swiftは以下の機能を提供します。

### ユーザー認証 

この機能により、ユーザーは自分のLINEアカウントを使って開発者の作成したサービスやアプリにログインできます。LINE SDK for iOS Swiftを組み込めば、LINEログインを簡単にアプリに組み込むことができます。ユーザーがiOSデバイス上のLINEにログイン済みの場合、LINEの認証情報を入力せずに自動的にアプリにログインできます。そのため、ユーザーは面倒な登録作業なしでアプリを使い始められます。

### ユーザーデータの利用とOpenIDのサポート 

ユーザーがログインすると、ユーザーのLINEプロフィールを取得できます。開発者はユーザーシステムを構築せずに、LINEに登録されているユーザー情報を利用できます。

LINE SDKでは[OpenID Connect](https://openid.net/developers/how-connect-works/) 1.0仕様がサポートされます。アクセストークンの取得時に、ユーザーのLINEプロフィールを含むIDトークンを取得できます。

### APIコール 

LINE SDKに含まれるメソッドを使用してユーザーのプロフィール情報を取得したり、ユーザーをログアウトしたり、アクセストークンを管理したりすることができます。

## オープンソースSDK 

LINE SDK for iOS Swiftはオープンソースのプロジェクトです。[リポジトリ](https://github.com/line/line-sdk-ios-swift)にアクセスして、提供されているコードやサンプルを確認できます。

## LINE SDKを使用する 

iOSアプリでLINE SDKを使用するには、以下の手順に従います。

1. チャネルを作成する。

   詳しくは、『LINEログインドキュメント』の「[LINEログインを始めよう](https://developers.line.biz/ja/docs/line-login/getting-started/)」を参照してください。

2. LINE SDKを使用してiOSアプリにLINEログインを組み込む。

   詳しくは、「[プロジェクトを設定する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/setting-up-project/)」および「[iOSアプリにLINEログインを組み込む](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/integrate-line-login/)」を参照してください。

3. LINEログインを利用する。

   アプリでLINEログインを使用する場合は、「[ユーザーを管理する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/managing-users/)」および『[LINE SDK for iOS Swiftリファレンス（英語）](https://developers.line.biz/en/reference/ios-sdk-swift/)』を参照してください。

   サーバーでLINEログインAPIを使用する場合は、「[アクセストークンを管理する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/managing-access-tokens/)」および『[LINEログイン v2.1 APIリファレンス](https://developers.line.biz/ja/reference/line-login/)』を参照してください。

### スターターアプリを試してみる 

スターターアプリを使って、LINEログインの動作を確認できます。「[スターターアプリを試してみる](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/try-line-login/)」を参照してください。

## このガイドの内容 

このガイドでは、LINE SDKをアプリに組み込む方法と、SDKで利用できるAPI機能をアプリから使う方法について説明します。各トピックについては以下の表を参照してください。

| タイトル | 内容 |
| --- | --- |
| [LINE SDK for iOS Swiftの概要](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/overview/) | SDKの機能と、SDKの利用方法の概要 |
| [スターターアプリを試してみる](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/try-line-login/) | スターターアプリの実行方法 |
| [プロジェクトを設定する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/setting-up-project/) | LINE SDKをプロジェクトに組み込む方法 |
| [iOSアプリにLINEログインを組み込む](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/integrate-line-login/) | LINEログインを活用してアプリのユーザーエクスペリエンスを向上させる方法 |
| [SDKで友だち追加オプションを利用する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/link-a-bot/) | LINE公式アカウントを友だち追加するオプションを表示し、LINE公式アカウントとユーザーの間の友だち関係を取得する方法 |
| [ユーザーを管理する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/managing-users/) | ユーザープロフィールの取得、IDトークンを使ったユーザーデータの取得、およびユーザーのログアウト方法 |
| [アクセストークンの管理](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/managing-access-tokens/) | アクセストークンの更新、検証、および現在のアクセストークンの取得方法 |
| [エラーを処理する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/error-handling/) | SDKで返されるエラーの制御方法 |
| [Objective-CのコードでSDKを使用する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/using-objc/) | LINE SDK for iOS SwiftをObjective-Cのプロジェクトに組み込む方法 |
| [SDKをアップグレードする](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/migration-guide/) | LINE SDK v4.1 for iOSからLINE SDK v5 for iOS Swiftにアップグレードする方法 |
| [LINE SDK v5 for iOS Swiftリファレンス（英語）](https://developers.line.biz/en/reference/ios-sdk-swift/) | SDKで利用できるプロトコルとクラスの詳細情報 |

## その他のリソース 

| タイトル | 内容 |
| --- | --- |
| [iOS SDKリリースノート](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/release-notes/) | SDKの変更履歴 |
| [LINE APIのSDK](https://developers.line.biz/ja/docs/downloads/) | LINE SDKのダウンロードリンク |
