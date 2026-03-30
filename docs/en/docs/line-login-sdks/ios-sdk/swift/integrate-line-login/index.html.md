# Integrating LINE Login with your iOS app

Once you [install the SDK](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/setting-up-project/) and configure your project, you can start leveraging LINE Login to improve your app's user experience.

## Setting up the LineSDK framework and your channel ID 

To process the results generated through login actions, set up the LINE SDK for iOS Swift in the `AppDelegate.swift` file.

### 1. Import the LineSDK framework 

At the top of the `AppDelegate.swift` file, import the `LineSDK` framework as below:

```swift
// AppDelegate.swift
import LineSDK
```

To use the SDK in other files within your app, also import the SDK into those files.

### 2. Call the `LoginManager.setup` method 

Call the `LoginManager.setup` method just after your app is launched as below:

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    // Add this to your "didFinishLaunching" delegate method.
    LoginManager.shared.setup(channelID: "YOUR_CHANNEL_ID", universalLinkURL: nil)

    return true
}
```

<!-- note start -->

**Note**

Make sure you call the `setup` method **before** you access other properties or call other methods of the LINE SDK for iOS Swift.

<!-- note end -->

#### Using a universal link 

If you set up a universal link in the LINE Developers Console, call the `setup` method with the `universalLinkURL` parameter. This secures the login process by letting LINE open your app with the universal link.

For more information on how to handle the login process using a universal link, see [Using universal links](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/universal-links-support/).

### 3. Handle app opening 

To handle the authentication result returned from the LINE Platform, pass the received URL to the `application(_:open:options:)` method of `LoginManager`. This means modifying either your app delegate class or your scene delegate classes, depending on whether your project supports multiple windows (a feature [introduced in iOS 13](https://developer.apple.com/documentation/uikit/scenes)).

#### Modify app delegate 

iOS 12 and earlier will open URLs by calling your `UIApplicationDelegate` object. Therefore, add the following lines to the `application(_:open:options:)` delegate method of your app delegate class:

```swift
// AppDelegate.swift
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {
    return LoginManager.shared.application(app, open: url)
}
```

#### Modify scene delegates 

By default, iOS 13 and later will try to open URLs by calling a `UISceneDelegate` object.

If you created your project with Xcode 11 or later, then by default it will contain a `SceneDelegate.swift` file and your `Info.plist` file will contain a `UIApplicationSceneManifest` entry. Add the following lines to any scene delegate class you want to use:

If your app supports multiple windows, add the following lines to any scene delegate class you want to use:

```swift
// SceneDelegate.swift
func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
    _ = LoginManager.shared.application(.shared, open: URLContexts.first?.url)
}
```

<!-- note start -->

**If you're not supporting multiple windows**

If your app doesn't support multiple windows, iOS will call your `UIApplicationDelegate` object to open URLs. Modify your app delegate class instead.

<!-- note end -->

## Performing a login process 

To let the user log in to your iOS app, you can create a LINE-branded login button to take the user through the authentication and authorization process.

There are 2 ways to add a login button:

- [Use the LINE SDK's built-in login button](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/integrate-line-login/#use-button)
- [Use your own code](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/integrate-line-login/#use-code)

### Use the LINE SDK's built-in login button 

The LINE SDK for iOS Swift provides a predefined login button. The `LoginButton` class in the SDK is a subclass of the `UIButton` class and follows the style recommended in the [LINE Login button design guidelines](https://developers.line.biz/en/docs/line-login/login-button/). You can add a login button to the user interface of your app to provide your users with a quick way to log in as below:

```swift
// In your view controller
override func viewDidLoad() {
    super.viewDidLoad()

    // Create Login Button.
    let loginButton = LoginButton()
    loginButton.delegate = self

    // Configuration for permissions and presenting.
    loginButton.permissions = [.profile]
    loginButton.presentingViewController = self

    // Add button to view and layout it.
    view.addSubview(loginButton)
    loginButton.translatesAutoresizingMaskIntoConstraints = false
    loginButton.centerXAnchor.constraint(equalTo: view.centerXAnchor).isActive = true
    loginButton.centerYAnchor.constraint(equalTo: view.centerYAnchor).isActive = true
}
```

When your user taps the login button, the user will be authenticated with proper login flow: if the user has LINE installed on the device, your app retrieves the user’s LINE credentials from LINE to perform authentication. Otherwise, the user is redirected to the LINE Login dialog on their browser and prompted for their LINE credentials.

To receive the login state, implement the related delegate methods of the `LoginButtonDelegate` protocol as below:

```swift
extension LoginViewController: LoginButtonDelegate {
    func loginButton(_ button: LoginButton, didSucceedLogin loginResult: LoginResult) {
        hideIndicator()
        print("Login Succeeded.")
    }

    func loginButton(_ button: LoginButton, didFailLogin error: LineSDKError) {
        hideIndicator()
        print("Error: \(error)")
    }

    func loginButtonDidStartLogin(_ button: LoginButton) {
        showIndicator()
        print("Login Started.")
    }
}
```

When the login process finishes, either of the delegate methods is invoked with the login result.

### Use your own code 

Instead of using the default login button, you can also customize your user interface and login process with your own code.

To perform a login process, call the `LoginManager.login` method with appropriate parameters. Typically, a login process takes place in a view controller as below:

```swift
// LoginViewController.swift

import LineSDK

class LoginViewController: UIViewController {
    override func viewDidLoad() {
        //...
    }

    func login() {
        LoginManager.shared.login(permissions: [.profile], in: self) {
            result in
            switch result {
            case .success(let loginResult):
                print(loginResult.accessToken.value)
                // Do other things you need with the login result
            case .failure(let error):
                print(error)
            }
        }
    }
}
```

The completion handler is called with the `result` argument after the user completes a login process. Switch on the login result to access login details.

If the login is successful, the LINE Platform returns a `LoginResult` object that contains common login information. Use the `LoginManager.shared.isAuthorized` method to access the login state.

If an error occurs during the login process, the LINE SDK returns the `result` argument of `.failure` and an associated `LineSDKError` enumeration member. See [Handling errors](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/error-handling/) for how to get the error details from the SDK and how to handle them appropriately.

For how to design your login interface, see [LINE Login button design guidelines](https://developers.line.biz/en/docs/line-login/login-button/) where you can also download the LINE Login button images.

## Handling the login result 

### Token permissions 

While you can specify any permissions you want the users to grant to your app when you call the `LoginManager.login` method, your channel may not have the corresponding permissions. In this case, the `permissions` property of the `LoginResult` object is different from what you specified in the authorization request.

To check the authorized permissions associated with the access token, get the `permissions` property. For example, check whether a `.profile` permission is contained in the token by using the code below:

```swift
case .success(let loginResult):
    let profileEnabled = loginResult.permissions.contains(.profile)
```

API calls without appropriate permissions fail. For more information, see [Handling errors](https://developers.line.biz/en/docs/line-login-sdks/ios-sdk/swift/error-handling/).

### User profile 

If you specify the profile permission in the authorization request, the login result will contain a `UserProfile` object. You can construct your own user system by accessing the user profile information as below:

```swift
LoginManager.shared.login(permissions: [.profile], in: self) {
    result in
    switch result {
    case .success(let loginResult):
        if let profile = loginResult.userProfile {
            print("User ID: \(profile.userID)")
            print("User Display Name: \(profile.displayName)")
            print("User Icon: \(String(describing: profile.pictureURL))")
        }
    case .failure(let error):
        print(error)
    }
}
```

The user ID is unique only to an individual provider. The same LINE user will have a different user ID for different providers. Avoid using the user ID to identify users across different providers.

### Using user data on your server 

<!-- warning start -->

**User impersonation**

Do not trust user IDs, or other information available in the `UserProfile` object, when sent by a client to your backend server. A malicious client can send an arbitrary user ID or malformed information to your server to impersonate a user.

Instead, the client should send the server an access token, and the server should use the token to retrieve user data.

<!-- warning end -->

Typically, a back-end server verifies a user's identity based on a user ID, display name, or some other LINE account property. Instead of sending this information from app to backend as plain text, send the access token that is stored in the app. Then, use the access token to securely send and receive data. Your back-end server can validate the access token against the LINE Platform and then retrieve a user's details.

Access tokens can be retrieved from the `LoginResult` object. Here's an example:

```swift
LoginManager.shared.login(permissions: [.profile], in: self) {
    result in
    switch result {
    case .success(let loginResult):
        let token = loginResult.accessToken.value
        // Send `token` to your server.
    case .failure(let error):
        print(error)
```

Learn more about what APIs to call from your backend on these pages:

- [Verify access token validity](https://developers.line.biz/en/reference/line-login/#verify-access-token)
- [Get user profile](https://developers.line.biz/en/reference/line-login/#get-user-profile)
