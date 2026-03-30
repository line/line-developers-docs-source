# Handling errors

## Overview 

The SDK handles potential errors and provide you with appropriate information so that you can process errors appropriately in your final product.

All of the methods in the LINE SDK for iOS Swift returns an `Result` enumeration as its response. You can get an associated error when the response contains the `.failure` case as below:

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

The sample code above simply prints out the error. The printed error in the log describes the cause of the error in a human-readable sentence. Using this information, you can determine how to handle individual error cases.

## Error types and error reasons 

Any error reported by the LINE SDK for iOS Swift is a `LineSDKError` instance, which is an enumeration conforming to the `Swift.Error` protocol. Its members represent a reason category to indicate in which phase and for what reason the error occurred. Currently, there are four defined categories of error reasons:

- `.requestFailed(reason: RequestErrorReason)`: Error occurred while creating an API request. This may be due to invalid parameters or lack of access token.
- `.responseFailed(reason: ResponseErrorReason)`: Error occurred after receiving the server response. This may be due to an incorrect response or networking errors.
- `.authorizeFailed(reason: AuthorizeErrorReason)`: Error occurred during the authorization process. For example, the user cancels the process or the ID token verification fails.
- `.generalError(reason: GeneralErrorReason)`: Other general error causes, such as data-string conversion failures or parameters that do not meet the preconditions.

Each error category is associated with a detailed reason which is an enumeration as well. These enumerations contain reason members with necessary information or an underlying `Error` instance from the system.

To understand what a reason looks like, see the below snippet of the `ResponseErrorReason` enumeration:

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

**Note**

This is for a demonstration purpose. Your final code may not be the same as above.

<!-- note end -->

## Getting error data 

To find out details about the error from the top level `LineSDKError` instance, you can use Swift pattern matching and extract associated data from the error. For example, you can check whether an error comes from an invalid HTTP status code from the server:

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

According to the error type and its cause, you can determine how to handle the error. For example, if an `.invalidHTTPStatusAPIError` occurs, you can check the `code` property of its `detail` parameter. If the error code is `500`, it indicates a server error and there may be little you can do other than displaying pop-up messages. However, if the error code is `403`, it indicates that your current token has insufficient permissions to access the target API endpoint. In this case, you can prompt the user to log in again and grant required permissions to your app for accessing the target endpoint.

The code below shows how to handle errors explained above:

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

## Using shortcuts to handle common errors 

There are a number of common errors that may occur while using the LINE SDK for iOS Swift. There are several shortcuts to identify them quickly. You can use these shortcuts to reduce work on pattern-matching the returned error:

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

By using shortcuts to handle common errors, it becomes easier for you to abstract your error handling code. While designing simple error handling depends on the architecture of your app, a common and widely accepted practice is to avoid repeating the same error handling code. As a good practice, put all error handling code in a single location.

## Error code and user data 

The `LineSDKError` enumeration conforms to the `CustomNSError` protocol and the `LocalizedError` protocol. Each error reason has its own `errorCode` and `errorUserInfo` properties to help you identify the error type and additional details.

## Conclusion 

Error handling is not an easy task, but it is definitely worth spending some time on. You can significantly improve your app's user experience by handling errors thoroughly.

For information about possible error codes and what they indicate, see [LineSDKError](https://developers.line.biz/en/reference/ios-sdk-swift/Enums/LineSDKError.html) in the LINE SDK for iOS Swift reference.

More errors may be added to the LINE SDK for iOS Swift as it evolves. Before you upgrade the SDK, make sure to check [Release notes](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/release-notes/) for any significant changes and determine whether you need to upgrade your error handling methods.
