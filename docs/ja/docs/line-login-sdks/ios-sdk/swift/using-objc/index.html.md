# Objective-CのコードでSDKを使用する

## 概要 

LINE SDK for iOS SwiftはすべてSwiftで書かれていますが、Objective-Cのプロジェクトで使用できます。方法は2つあります。

## オプション1：言語混在プロジェクトを作成する 

SwiftとSwift/Objective-Cの相互運用の経験がある場合は、LINE SDK for iOS SwiftをObjective-Cのプロジェクトに直接組み込み、Swift言語でLINE SDKのAPIを呼び出すことをお勧めします。

Objective-Cの既存のプロジェクトは、Objective-CとSwiftの言語混在プロジェクトに変換できます。言語混在プロジェクトに、LINE SDK for iOS Swiftと処理を受け渡しするSwiftのファイルを追加できます。

Swiftのファイル内で必要な宣言をObjective-Cから利用するには、宣言に`@objc`属性または`@objcMembers`属性を付与してください。これらの属性について詳しくは、Swift.orgの「[Attributes](https://docs.swift.org/swift-book/ReferenceManual/Attributes.html#ID592)」を参照してください。

Swiftのファイルをプロジェクトにインポートすると、Xcodeにより自動的にブリッジングヘッダーファイルが生成されます。これにより、それらのファイルをObjective-Cのコードでも利用できるようになります。ブリッジングヘッダーについて詳しくは、Appleの「[Importing Swift into Objective-C](https://developer.apple.com/documentation/swift/importing-swift-into-objective-c)」を参照してください。

SwiftのクラスをObjective-Cのプロジェクトで使えるようにするうえで、以下の記事も役に立ちます。

- [Jen Sipila](https://jen-sip.medium.com/)の「[Setting up Swift and Objective-C Interoperability](https://medium.com/ios-os-x-development/swift-and-objective-c-interoperability-2add8e6d6887)」。特に、「Make a Swift Class available to Objective-C Files」セクションが参考になります。
- Appleの「[Migrating Your Objective-C Code to Swift](https://developer.apple.com/documentation/swift/migrating-your-objective-c-code-to-swift)」。プロセス全体を理解するのに役立ちます。

## オプション2：Objective-Cラッパーを使う 

Objective-CのコードでLINE SDK for iOS Swiftと処理を受け渡しするには、LINE SDK for iOS Swiftに含まれるObjective-Cラッパーを使います。オプション1とは異なり、Objective-Cラッパーフレームワークをプロジェクトに追加する必要があります。ここでは、Objective-Cラッパーの基本概念、インストール、および一般的な使い方について説明します。

LINE SDK for iOS SwiftはSwiftのコードにのみ対応しています。SDKをObjective-Cのコードに対応させるため、Objective-CラッパーはコアSDK上に実装されています。LINE SDK for iOS Swiftの中核的な機能のほとんどを、ラッパーを介して利用できます。Swiftと完全な互換性がないObjective-Cの仕様の制限により、一部の機能はObjective-Cラッパーで利用できません。

本来のSDKと名前衝突を起こさないように、タイプとほとんどのSDKコンポーネントの名前に「LineSDK」というプリフィックスが付きます。ラッパーの設定には追加的な手順も伴います。

ラッパーはLINE SDK for iOS Swiftを使うための一時的な手段であることに留意してください。LINE SDK for iOS Swiftの機能をフル活用するには、プロジェクトをSwiftに移行する事を推奨します。

### インストール 

#### 前提条件 

LINE SDK for iOSをビルドしてObjective-Cラッパーを介して使用するには、以下が必要です。

- デプロイメントターゲットとしてiOS 11.0以降
- Xcode 10以降

#### CocoaPods 

CocoaPodsについて詳しくない場合は、『[CocoaPods Getting Started Guide](https://guides.cocoapods.org/using/getting-started.html)』を参照してください。CocoaPodsを使ってLINE SDK for iOS Swiftをアプリに組み込む前に、作業環境にCocoaPodsのgemをインストールする必要があります。

1. Podfileを準備したら、ターゲットに以下のpodコマンドを追加します。

    ```ruby
    platform :ios, '11.0'
    use_frameworks!

    target '<Your App Target Name>' do
        pod 'LineSDKSwift/ObjC', '~> 5.0'
    end
    ```

1. 以下のコマンドを実行します。

    ```bash
    $ pod install
    ```

1. LINE SDK for iOS Swiftがダウンロードされ、Xcodeのワークスペースに組み込まれます。

##### SDKをインポートする 

LINE SDK for iOS SwiftをObjective-Cラッパーと共にObjective-Cのプロジェクトにインポートするには、以下のように`@import LineSDK;`を追加します。

```objective-c
#import "ViewController.h"
@import LineSDK;

@implementation ViewController
// ...
@end
```

#### Carthage 

[Carthage](https://github.com/Carthage/Carthage)は分散型の依存性マネージャーで、ライブラリをビルドしてバイナリのフレームワークとして利用できます。

1. Carthageツールをインストールするには、[Homebrew](https://brew.sh/)を使います。

    ```bash
    $ brew update
    $ brew install carthage
    ```

1. Carthageを使ってLINE SDK for iOS SwiftをXcodeプロジェクトに組み込むには、CartfileにSDKのGitHubリポジトリを以下のように指定します。

    ```
    github "line/line-sdk-ios-swift" ~> 5.0
    ```

1. 以下のコマンドを実行してLINE SDK for iOS Swiftをビルドします。

    ```
    $ carthage update line-sdk-ios-swift
    ```

以下のセクションに記載された手順に従って、ビルドされた`LineSDK.framework`ファイルと`LineSDKObjC.framework`ファイルをXcodeプロジェクトに追加できます。

##### フレームワークファイルをXcodeプロジェクトにリンクする 

`Carthage/Build/iOS`フォルダーから`LineSDK.framework`ファイルと`LineSDKObjC.framework`ファイルをドラッグして、アプリのターゲットの［Build Phases］設定タブの［Link Binary With Libraries］セクションにドロップします。

##### ビルドフェーズでフレームワークファイルをコピーする 

1. アプリのターゲットの［Build Phases］設定タブで ［**+**］アイコンをクリックして、［**New Run Script Phase**］を選択します。以下の内容で実行スクリプトを作成します。

    ```
    /usr/local/bin/carthage copy-frameworks
    ```

1. フレームワークファイルのパスを［Input Files］セクションに追加します。

    ```
    $(SRCROOT)/Carthage/Build/iOS/LineSDK.framework
    $(SRCROOT)/Carthage/Build/iOS/LineSDKObjC.framework
    ```

1. フレームワークファイルのパスを［Output Files］セクションに追加します。

    ```
    $(BUILT_PRODUCTS_DIR)/$(FRAMEWORKS_FOLDER_PATH)/LineSDK.framework
    $(BUILT_PRODUCTS_DIR)/$(FRAMEWORKS_FOLDER_PATH)/LineSDKObjC.framework
    ```

［Build Phases］設定タブは以下のようになるはずです。

![iOS SDK Swift ObjCのリンクの[Build Phase] タブに[Link Binary with Library]、[Copy Bundle Resources]、および [Run Script] サブタブが表示されます。](https://developers.line.biz/media/ios-sdk-swift/install-carthage-objc.png)

##### ［Always Embed Swift Standard Libraries］オプションを有効にする 

［Build Settings］設定タブで［Always Embed Swift Standard Libraries］（`ALWAYS_EMBED_SWIFT_STANDARD_LIBRARIES`）オプションを［YES］に設定して、Swiftの標準ライブラリを最終的なアプリバンドルに含めます。

##### SDKをインポートする 

LINE SDK for iOS SwiftをObjective-Cラッパーと共にObjective-Cのプロジェクトにインポートするには、以下のように`@import LineSDKObjC;`を追加します。

```objective-c
#import "ViewController.h"
@import LineSDKObjC;

@implementation ViewController
// ...
@end
```

### 命名規則 

Objective-Cラッパーを使う場合、タイプとほとんどのSDKコンポーネントの名前に「LineSDK」というプリフィックスが付きます。以下のコードサンプルは、よく実行されるタスクのObjective-Cでの制御方法を示しています。

#### 複数の権限を指定してユーザーをログインさせる 

```objective-c
NSSet *permissions = [NSSet setWithObjects:
                          [LineSDKLoginPermission profile],
                          [LineSDKLoginPermission openID],
                          nil];
[[LineSDKLoginManager sharedManager]
    loginWithPermissions:permissions
        inViewController:self
              parameters:nil
       completionHandler:^(LineSDKLoginResult *result, NSError *error) {
           if (result) {
               NSLog(@"User Name: %@", result.userProfile.displayName);
           } else {
               NSLog(@"Error: %@", error);
           }
       }
 ];
```

#### ユーザープロフィールを取得する 

```objective-c
[LineSDKAPI getProfileWithCompletionHandler:
    ^(LineSDKUserProfile * _Nullable profile, NSError * _Nullable error)
{
    if (profile) {
        NSLog(@"User Name: %@", profile.displayName);
    } else {
        NSLog(@"Error: %@", error);
    }
}];
```

### Objective-Cラッパーでエラーを制御する 

Objective-Cの規則に対応するため、Objective-Cラッパーは`NSError`オブジェクトをスローします。以下のコードでは、エラーがLINE SDKに関係するのかどうかを確認しています。

```objective-c
NSError *error = // ... An error from LINE SDK ObjC Wrapper
if ([error.domain isEqualToString:[LineSDKErrorConstant errorDomain]]) {
    // SDK Error
}
```

ラッパーからスローされるすべてのエラーは、本来のLINE SDK for iOS Swiftからスローされるのと同じ`code`プロパティと`userInfo`プロパティを持ちます。それらを使ってエラーの原因を確認できます。

```objective-c
if (error.code == 2004) {
    // invalidHTTPStatusAPIError
    NSNumber *statusCode = error.userInfo[[LineSDKErrorConstant userInfoKeyStatusCode]];
    if ([statusCode integerValue] == 403) {
        // Permission granting issue. Ask for authorization with enough permission again.
    }
}
```

エラーを特定して制御する方法については、「[エラーを制御する](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/swift/error-handling/)」を参照してください。
