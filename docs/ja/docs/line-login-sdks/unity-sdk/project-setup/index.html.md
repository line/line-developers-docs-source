# プロジェクトを設定する

LINE SDK for Unityは、iOSまたはAndroidプラットフォームでLINE SDKを使用するためのインターフェイスを提供します。UnityエディターでLINE SDKを使用して各プラットフォームにエクスポートするには、開発環境にいくつかの要件があります。

## Unityの要件 

- Unity 2020.3.15以降。iOSおよびAndroidモジュールがインストール済みであること
- Unity Personal、Unity Plus、またはUnity Proの有効なサブスクリプションがあること

## iOSへのインストール 

LINE SDK for UnityをiOSに組み込むには、以下が必要です。

- デプロイメントターゲットとしてiOS 13.0以降
- Xcode 14.1以降

iOSでは、LINE SDK for Unityは、LINE SDK for iOS Swiftのラッパーとして機能します。Xcodeプロジェクトを書き出す時、必要なライブラリーを自動で追加します。

## Androidへのインストール 

UnityがプロジェクトをAndroidプラットフォーム向けにビルドするために、Android SDKが必要です。すでに『Unity User Manual』の「[Android環境の設定](https://docs.unity3d.com/ja/current/Manual/android-sdksetup.html)」を行ったことがある場合は、Android SDKはインストールされています。
