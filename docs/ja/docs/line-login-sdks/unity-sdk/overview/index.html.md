# LINE SDK for Unityの概要

LINE SDK for Unityを使うと、最新の方法でLINEプラットフォームのAPIを実装できます。このSDKに含まれる機能は、個人に合わせたユーザーエクスペリエンスを提供する魅力的なUnityゲームの開発に役立ちます。

## 機能 

LINE SDK for Unityは[LINE SDK for iOS Swift](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/)および[LINE SDK for Android](https://developers.line.biz/ja/docs/line-login-sdks/android-sdk/)向けのラッパーです。 iOSまたはAndroidで実行されるUnityゲームに、以下の機能を提供します。

### ユーザー認証 

ユーザーは自分のLINEアカウントを使って、開発者が作成したUnityゲームにログインできます。LINE SDK for Unityを組み込めば、LINEログインを簡単にアプリに組み込むことができます。ユーザーがAndroidデバイス上のLINEにログイン済みの場合、LINEの認証情報を入力せずに自動的にアプリにログインできます。そのため、ユーザーはアカウント登録作業を行わずにアプリを使い始められます。

### OpenIDによるユーザーデータの利用 

ユーザーがログインすると、そのユーザーのLINEプロフィールを取得できます。開発者は特別なシステムを構築せずに、LINEに登録されているユーザー情報を使用できます。

LINE SDKでは[OpenID Connect](https://openid.net/developers/how-connect-works/) 1.0仕様がサポートされます。アクセストークンを取得すると、ユーザーのLINEプロフィールを含むIDトークンを取得できます。

### APIコール 

LINE SDKに含まれるメソッドを使用して、ユーザーのプロフィールを取得したり、ユーザーをログアウトさせたり、アクセストークンを管理したりできます。

## オープンソースSDK 

LINE SDK for Unityはオープンソースのプロジェクトです。[リポジトリ](https://github.com/line/line-sdk-unity)にアクセスして、提供されているコードやサンプルを確認できます。

## SDKを使用する 

UnityゲームでLINE SDKを使用するには、以下の手順を行います。

1. チャネルを作成します。詳しくは、『LINEログインドキュメント』の「[LINEログインを始めよう](https://developers.line.biz/ja/docs/line-login/getting-started/)」を参照してください。
2. SDKを使用して、UnityゲームにLINEログインを組み込みます。詳しくは、「[UnityゲームにLINEログインを組み込む](https://developers.line.biz/ja/docs/line-login-sdks/unity-sdk/integrate-line-login/)」を参照してください。
3. SDKを使用してアプリから、またはLINEログインAPIを通じてサーバー側から、APIコールを実行します。詳しくは、『[LINE SDK for Unity APIリファレンス（英語）](https://developers.line.biz/en/reference/unity-sdk/)』および『[LINEログイン v2.1 APIリファレンス](https://developers.line.biz/ja/reference/line-login/)』を参照してください。

### スターターアプリを試してみる 

スターターアプリを使って、LINEログインの動作を確認できます。詳しくは、「[スターターアプリを試してみる](https://developers.line.biz/ja/docs/line-login-sdks/unity-sdk/try-line-login/)」を参照してください。

## このガイドの内容 

このガイドでは、LINE SDKをUnityゲームに組み込む方法と、SDKで利用できるAPI機能をアプリから使う方法について説明します。各トピックについては以下の表を参照してください。

タイトル | 内容
-|-
[LINE SDK for Unityの概要](https://developers.line.biz/ja/docs/line-login-sdks/unity-sdk/overview/) | SDKの機能と、利用方法の概要
[プロジェクトを設定する](https://developers.line.biz/ja/docs/line-login-sdks/unity-sdk/project-setup/) | LINE SDK for Unityを組み込むために必要な前提条件と環境
[スターターアプリを試してみる](https://developers.line.biz/ja/docs/line-login-sdks/unity-sdk/try-line-login/) | スターターアプリを実行する方法
[UnityゲームにLINEログインを組み込む](https://developers.line.biz/ja/docs/line-login-sdks/unity-sdk/integrate-line-login/) | LINE SDKをプロジェクトに組み込み、LINEログインを活用してアプリのユーザーエクスペリエンスを向上させる方法
[SDKを使用する](https://developers.line.biz/ja/docs/line-login-sdks/unity-sdk/using-sdk/) | LINE SDK for Unityの使用方法とその他の詳細
[LINE SDK for Unity APIリファレンス（英語）](https://developers.line.biz/en/reference/unity-sdk/) | LINE SDK for Unityのインターフェースおよびクラスの詳細

## その他のリソース 

『LINE SDK for Unityドキュメント』の [トップページ](https://developers.line.biz/ja/docs/line-login-sdks/unity-sdk/)から、以下の情報を参照できます。

タイトル | 内容
-|-
[リリースノート](https://developers.line.biz/ja/docs/line-login-sdks/unity-sdk/release-notes/) | SDKの変更履歴
