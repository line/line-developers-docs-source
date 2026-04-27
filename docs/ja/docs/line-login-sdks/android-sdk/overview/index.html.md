# LINE SDK for Androidの概要

LINE SDK for Androidを使うと、最新の方法でLINEプラットフォームのAPIを実装できます。このSDKに含まれる機能は、個人に合わせたユーザーエクスペリエンスを提供する魅力的なAndroidアプリの開発に役立ちます。

## 機能 

LINE SDK for Androidは以下の機能を提供します。

### ユーザー認証 

この機能により、ユーザーは自分のLINEアカウントを使って開発者の作成したサービスやアプリにログインできます。LINE SDK for Androidを組み込めば、LINEログインを簡単にアプリに組み込むことができます。ユーザーがAndroidデバイス上のLINEにログイン済みの場合、LINEの認証情報を入力せずに自動的にアプリにログインできます。そのため、ユーザーは面倒な登録作業なしでアプリを使い始められます。

### ユーザーデータの利用とOpenIDのサポート 

ユーザーがログインすると、ユーザーのLINEプロフィールを取得できます。開発者はユーザーシステムを構築せずに、LINEに登録されているユーザー情報を利用できます。

LINE SDKでは[OpenID Connect](https://openid.net/developers/how-connect-works/) 1.0仕様がサポートされます。アクセストークンの取得時に、ユーザーのLINEプロフィールを含むIDトークンを取得できます。

### APIコール 

LINE SDKに含まれるメソッドを使用してユーザーのプロフィール情報を取得したり、ユーザーをログアウトしたり、アクセストークンを管理したりすることができます。

## オープンソースSDK 

LINE SDK for Androidはオープンソースのプロジェクトです。[リポジトリ](https://github.com/line/line-sdk-android)にアクセスして、提供されているコードやサンプルを確認できます。

## LINE SDKを使用する 

AndroidアプリでLINE SDKを使用するには、以下の手順に従います。

1. チャネルを作成する。

   詳しくは、『LINEログインドキュメント』の「[LINEログインを始めよう](https://developers.line.biz/ja/docs/line-login/getting-started/)」を参照してください。

2. LINE SDKを使用してAndroidアプリにLINEログインを組み込む。

   詳しくは、「[AndroidアプリにLINEログインを組み込む](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/integrate-line-login/)」を参照してください。

   友だち追加オプションを利用する場合は、「[SDKで友だち追加オプションを利用する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/link-a-bot/)」を参照してください。

3. LINEログインを利用する。

   アプリでLINEログインを使用する場合は、「[ユーザーを管理する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/managing-users/)」および『[LINE SDK for Androidリファレンス（英語）](https://developers.line.biz/en/reference/android-sdk/)』を参照してください。

   サーバーでLINEログインAPIを使用する場合は、「[アクセストークンを管理する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/managing-access-tokens/)」および『[LINEログイン v2.1 APIリファレンス](https://developers.line.biz/ja/reference/line-login/)』を参照してください。

### サンプルアプリを試してみる 

サンプルアプリを使って、LINEログインの動作を確認できます。詳しくは、「[サンプルアプリを試してみる](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/try-line-login/)」を参照してください。

## このガイドの内容 

このガイドでは、LINE SDKをアプリに組み込む方法と、SDKで利用できるAPI機能をアプリから使う方法について説明します。各トピックについては以下の表を参照してください。

| タイトル | 内容 |
| --- | --- |
| [LINE SDK for Androidの概要](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/overview/) | SDKの機能と、SDKの利用方法の概要 |
| [サンプルアプリを試してみる](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/try-line-login/) | サンプルアプリの実行方法 |
| [AndroidアプリにLINEログインを組み込む](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/integrate-line-login/) | LINE SDKをプロジェクトに組み込み、LINEログインを活用してアプリのユーザーエクスペリエンスを向上させる方法 |
| [SDKで友だち追加オプションを利用する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/link-a-bot/) | LINE公式アカウントを友だち追加するオプションを表示し、LINE公式アカウントとユーザーの間の友だち関係を取得する方法 |
| [ユーザーを管理する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/managing-users/) | ユーザープロフィールの取得、IDトークンを使ったユーザーデータの取得、およびユーザーのログアウト方法 |
| [アクセストークンの管理](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/managing-access-tokens/) | アクセストークンの更新、検証、および現在のアクセストークンの取得方法 |
| [エラーを処理する](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/handling-errors/) | SDKで返されるエラー |
| [LINE SDK v5 for Androidリファレンス（英語）](https://developers.line.biz/en/reference/android-sdk/) | SDKで利用できるインターフェイスとクラスの詳細情報 |

## その他のリソース 

| タイトル | 内容 |
| --- | --- |
| [Android SDKリリースノート](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/release-notes/) | SDKの変更履歴 |
| [LINE APIのSDK](https://developers.line.biz/ja/docs/downloads/) | LINE SDKのダウンロードリンク |
