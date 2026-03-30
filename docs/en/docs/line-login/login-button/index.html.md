# LINE Login button design guidelines

Add a LINE Login button to let your users log in to your application using [LINE Login](https://developers.line.biz/en/docs/line-login/overview/).

![LINE Login button image](https://developers.line.biz/media/line-login/login-button/login-button-en.png)

The LINE Login button is made up of the following components: the LINE icon, the LINE icon speech bubble, and the LINE Login button text.

Before using the LINE Login button, make sure you read and agree to the [Usage Guidelines for the LINE Login Button](https://terms2.line.me/LINE_Developers_Guidelines_for_Login_Button). By downloading the following LINE Login button template, you are deemed to have agreed to the guidelines.

[Download the LINE Login button template](https://vos.line-scdn.net/line-developers/docs/media/line-login/login-button/LINE_Login_Button_Image.zip)

<br>The file includes multiple sets of images in many resolutions that can be used with web, iOS, or Android applications. Use the PSD file to add customized login text in different languages.

## Design guidelines 

Use these design guidelines when adding the LINE Login button to your app.

### Size 

You can increase or decrease the size of the LINE Login button according to the device it will be displayed on as long as the image complies with the following conditions.

- The aspect ratio of the LINE icon does not change.
- The LINE icon remains clearly visible.

### Color 

Only the following colors can be used for the LINE Login button.

| Item | Color |
| :--- | :--- |
| Base color | ![base color](https://developers.line.biz/media/line-login/login-button/06c755.png)#06C755 |
| Hover | ![base color](https://developers.line.biz/media/line-login/login-button/06c755.png)#06C755 + ![hover color](https://developers.line.biz/media/line-login/login-button/000000-10-per.png)#000000 (opacity: 10%) |
| Press | ![base color](https://developers.line.biz/media/line-login/login-button/06c755.png)#06C755 + ![press color](https://developers.line.biz/media/line-login/login-button/000000-30-per.png)#000000 (opacity: 30%) |
| Disabled | ![white color](https://developers.line.biz/media/line-login/login-button/ffffff.png)#FFFFFF |
| Font/logo color (other than disabled) | ![logo white color](https://developers.line.biz/media/line-login/login-button/ffffff.png)#FFFFFF |
| Font/logo color (only disabled) | ![logo grey color](https://developers.line.biz/media/line-login/login-button/1e1e1e-20-per.png)#1E1E1E (opacity: 20%) |
| Vertical line color (other than disabled) | ![line color for other than disabled](https://developers.line.biz/media/line-login/login-button/000000-8-per.png)#000000 (opacity: 8%) |
| Vertical line color (only disabled) | ![line color for only disabled](https://developers.line.biz/media/line-login/login-button/e5e5e5-60-per.png)#E5E5E5 (opacity: 60%) |
| Border color (only disabled) | ![border color](https://developers.line.biz/media/line-login/login-button/e5e5e5-60-per.png)#E5E5E5 (opacity: 60%) |

<!-- note start -->

**Note the opacity color layers**

For opacity colors, be aware of the layers you place them on. For example, in the case of a vertical line on the hover button, place the hover (`#000000 (opacity: 30%)`) on top of the basic color layer (`#06C755`), and then place the vertical line (`#000000 (opacity: 8%)`) and text/logo (`#FFFFFF`) on the layer above it.

![Layers of LINE login buttons](https://developers.line.biz/media/line-login/login-button/login-button-color-layer-order-en.png)

For more information on the placement for each layer, see the below figure.

<!-- note end -->

![LINE Login button color](https://developers.line.biz/media/line-login/login-button/login-button-color-en.png)

### Text 

The recommended LINE login button text is "Log in with LINE". A list of recommended phrases for various languages can be found in the table below.

If you decide to use your own customized button text, make sure to follow these guidelines:

- No line breaks
- Text clearly indicates to the user that the button is for logging into the app with LINE

You can also use the LINE icon on its own without any button text as the LINE Login button.

|Language|Login button text (long)|Login button text (short)|
|--- |--- |--- |
|en|Log in with LINE|Log in|
|ja|LINEでログイン|ログイン|
|ko|LINE으로 로그인|로그인|
|de|Mit LINE anmelden|Anmelden|
|es|Iniciar sesión con LINE|Iniciar sesión|
|fr|Connexion avec LINE|Se connecter|
|id|Masuk dengan LINE|Masuk|
|it|Login con LINE|Login|
|ms|Log masuk dengan LINE|Log Masuk|
|pt-BR|Login com o LINE|Login|
|pt-PT|Iniciar sessão com o LINE|Iniciar sessão|
|ru|Войти в LINE|Войти|
|th|ล็อกอินด้วย LINE|ล็อกอิน|
|tr|LINE ile oturum açın|Oturum Aç|
|ar|تسجيل دخول باستخدام LINE|تسجيل دخول|
|vi|Đăng nhập với LINE|Đăng nhập|
|zh-CN|用LINE帐号登录|登录|
|zh-TW|與LINE連動|連動|

### Font 

The font of the button text must be readable. Recommended font sizes for each image size are included in the PSD files.

### Padding 

The width of the right and left padding for the login button text must be equal to or greater than the width of the LINE icon speech bubble. This width is defined as X in the image below.

The recommended height of the top and bottom padding for the login button text is X/2. Make sure you use a font size that allows for this padding to be maintained.

![LINE Login button padding](https://developers.line.biz/media/line-login/login-button/login-button-padding-en.png)

### Isolation zone 

The isolation zone is the space surrounding the LINE Login button which cannot contain any elements. The width of the isolation zone must be equal to or greater than the left padding of the LINE icon speech bubble. The width is defined as "A" in the image below. In addition to maintaining the isolation zone, avoid placing text or graphics near the isolation zone as that could compromise the effectiveness of the LINE Login button.

![LINE Login button isolation zone](https://developers.line.biz/media/line-login/login-button/login-button-isolation-zone.png)

### Common mistakes to avoid 

- Using a non-designated color
- Using an outdated LINE icon
- Using a different or modified icon instead of using the LINE icon
