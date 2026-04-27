# エラーを制御する

## 概要 

SDKにより、発生する可能性があるエラーが制御され、適切な情報が提供されます。その情報を使って、最終的なプロダクトでエラーを適切に処理できます。

LINE SDK for iOS Swiftのすべてのメソッドが、レスポンスとして`Result`列挙型を返します。レスポンスに`.failure`のケースが含まれる場合は、関連づけられたエラーを取得できます。

```swift
API.getProfile { result in
    switch result {
    case .success(let profile):
        print(profile.displayName)
    case .failure(let error):
        print(error)
        // Handle the error
    }
}
```

上のサンプルコードでは単にエラーを出力しています。ログに出力されるエラーには、人間が判読できる形式でエラーの原因が記述されています。この情報から、個々のエラーに対処する方法を判定できます。

## エラーのタイプと理由 

LINE SDK for iOS Swiftで報告されるエラーは、`Swift.Error`プロトコルに適合する列挙型である`LineSDKError`インスタンスとして返されます。この列挙型のメンバーは、エラーが発生した段階と原因を示すカテゴリを表しています。現在、エラーの理由として以下の4つのカテゴリが定義されています。

- `.requestFailed(reason: RequestErrorReason)`：APIリクエストの作成中にエラーが発生しました。パラメータが無効であるか、アクセストークンが存在しない可能性があります。
- `.responseFailed(reason: ResponseErrorReason)`：サーバーレスポンスの受信中にエラーが発生しました。レスポンスが正しくないか、ネットワークエラーが発生した可能性があります。
- `.authorizeFailed(reason: AuthorizeErrorReason)`：認可のプロセスでエラーが発生しました。たとえば、ユーザーがプロセスをキャンセルしたか、IDトークンの検証に失敗しました。
- `.generalError(reason: GeneralErrorReason)`：その他の一般エラーが発生しました。たとえば、データを文字列に変換できないか、パラメータが前提条件を満たしていません。

各エラーカテゴリは詳細な理由に関連づけられています。詳細な理由も列挙型です。これらの列挙型には、必要な情報またはSDKのエラーの基になるシステムで生成された`Error`インスタンスを含むメンバーが含まれます。

理由がどのようなものか理解するため、以下の`ResponseErrorReason`列挙型のスニペットを参照してください。

```swift
public enum ResponseErrorReason {
    // Error happens in the underlying `URLSession`. Code 2001.
    case URLSessionError(Error)
    // The response is not a valid `HTTPURLResponse`. Code 2002.
    case nonHTTPURLResponse
    // Cannot parse received data to an instance of target type. Code 2003.
    case dataParsingFailed(Any.Type, Data, Error)
    // Received response contains an invalid HTTP status code. Code 2004.
    case invalidHTTPStatusAPIError(detail: APIErrorDetail)
}
```

<!-- note start -->

**注意**

これは説明を目的としています。最終的なコードは上記とは異なる可能性があります。

<!-- note end -->

## エラーデータを取得する 

最上位の`LineSDKError`インスタンスからエラーの詳細を取得するには、Swiftのパターンマッチングを使ってエラーから関連データを抽出します。たとえば、エラーの原因がサーバーから返された無効なHTTPステータスコードにあるかどうかを確認するには、以下のコードを使います。

```swift
case .failure(let error):
    if case .responseFailed(
        reason: .invalidHTTPStatusAPIError(let detail)) = error
    {
        print("HTTP Status Code: \(detail.code)")
        print("API Error Detail: \(detail.error?.detail ?? "nil")")
        print("Raw Response: \(detail.raw)")
    }
```

エラーのタイプと原因に従って、エラーの制御方法を決定できます。たとえば、`.invalidHTTPStatusAPIError`が発生した場合は、`detail`パラメータの`code`プロパティを確認できます。エラーコード`500`はサーバーエラーを示すため、メッセージを表示する以外にできることはないかもしれません。その一方で、エラーコード`403`は対象のAPIエンドポイントにアクセスする権限が現在のトークンに不足していることを示します。この場合はユーザーに、アプリに再度ログインして対象のエンドポイントにアクセスするために必要な権限を付与するように促すことができます。

以下のコードは、上記のエラーを制御する方法を示しています。

```swift
case .failure(let error):
    if case .responseFailed(
        reason: .invalidHTTPStatusAPIError(let detail)) = error
    {
        if detail.code == 500 {
            print("LINE API Server Error: \(String(describing: detail.error)")
        } else if detail.code == 403 {
            print("Not enough permission. Login again with required permissions?")
            // Do Login
        }
    }
```

## 一般的なエラーを制御するショートカットを使う 

LINE SDK for iOS Swiftの使用中に発生する可能性がある一般的なエラーは数多く存在します。それらをすばやく識別するためのショートカットがいくつかあります。これらのショートカットを使って、返されるエラーのパターンッマッチングにかける作業を減らすことができます。

```swift
case .failure(let error):
    if error.isUserCancelled {
        // User cancelled the login process himself/herself.

    } else if error.isPermissionError {
        // Equivalent to checking .responseFailed.invalidHTTPStatusAPIError
        // with code 403. Should login again.

    } else if error.isURLSessionTimeOut {
        // Underlying request timeout in URL session. Should try again later.

    } else if error.isRefreshTokenError {
        // User is accessing a public API with expired token, LINE SDK tried to
        // refresh the access token automatically, but failed (due to refresh token)
        // also expired. Should login again.

    } else if /* error.isXYZ other condition */ {
        // You could also extend LineSDKError to make your own shortcuts.

    } else {
        // Any other errors.
        print("\(error)")
    }
```

一般的なエラーを制御するショートカットを使えば、エラー制御のコードを簡単に抽象化できます。シンプルなエラー制御の設計方法はアプリのアーキテクチャによって変わりますが、一般的で広く受容されている手法を使って、同じエラー制御コードの繰り返しを防ぐことができます。グッドプラクティスとして、すべてのエラー制御コードを1か所にまとめることをお勧めします。

## エラーコードとユーザー情報 

`LineSDKError`列挙型は`CustomNSError`プロトコルと`LocalizedError`プロトコルに適合しています。各エラーの理由には`errorCode`プロパティと`errorUserInfo`プロパティが定義されており、エラーのタイプと追加の詳細を識別するときに役立ちます。

## 最後に 

エラー制御は簡単な作業ではありませんが、時間をかける価値が確かにあります。エラーを徹底的に制御することにより、アプリのユーザーエクスペリエンスを大幅に向上させることができます。

発生する可能性のあるエラーのコードとその内容については、『LINE SDK for iOS Swiftリファレンス（英語）』の「[LineSDKError](https://developers.line.biz/en/reference/ios-sdk-swift/Enums/LineSDKError.html)」を参照してください。

LINE SDK for iOS Swiftのバージョンアップと共に、より多くのエラーが追加される可能性があります。SDKをアップグレードする前に「[iOS SDKリリースノート](https://developers.line.biz/ja/docs/line-login-sdks/ios-sdk/release-notes/)」で大幅な変更がないか確認し、アプリ側のエラー制御方法を更新する必要があるかどうかを判定してください。
