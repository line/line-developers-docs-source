# LINEログインボタン デザインガイドライン

LINEログインボタンを追加することによって、ユーザーが[LINEログイン](https://developers.line.biz/ja/docs/line-login/overview/)を利用してアプリにログインできるようになります。

![LINEログインボタンの画像](https://developers.line.biz/media/line-login/login-button/login-button-ja.png)

LINEログインボタンは、LINEアイコン、LINEアイコンの吹き出し、LINEログインボタンテキストの、3つの要素で構成されています。

LINEログインボタンを利用するには、「[Usage Guidelines for the LINE Login Button](https://terms2.line.me/LINE_Developers_Guidelines_for_Login_Button)」を読み、内容に同意する必要があります。以下のLINEログインボタンのテンプレートをダウンロードすることにより、ガイドラインに同意したものとみなされます。

[LINEログインボタンのテンプレートをダウンロード](https://vos.line-scdn.net/line-developers/docs/media/line-login/login-button/LINE_Login_Button_Image.zip)

<br>ウェブ、iOS、またはAndroidアプリに利用できる画像セットがさまざまな画質で用意されています。ログインテキストを多言語にカスタマイズするには、PSDファイルを使います。

## デザインガイドライン 

アプリにLINEログインボタンを追加する際は、本デザインガイドラインに従ってください。

### サイズ 

以下の条件を満たしていれば、ログインボタンを表示させるデバイスに応じて、画像サイズを拡大または縮小してかまいません。

- LINEアイコンのアスペクト比が維持されている。
- LINEアイコンをはっきりと視認できる。

### 色 

LINEログインボタンは、必ず以下の色で表示してください。

| 項目 | 色指定 |
| :--- | :--- |
| 基本色 | ![base color](https://developers.line.biz/media/line-login/login-button/06c755.png)#06C755 |
| マウスオーバー | ![base color](https://developers.line.biz/media/line-login/login-button/06c755.png)#06C755 + ![hover color](https://developers.line.biz/media/line-login/login-button/000000-10-per.png)#000000（不透明度：10％） |
| タップ/クリック | ![base color](https://developers.line.biz/media/line-login/login-button/06c755.png)#06C755 + ![press color](https://developers.line.biz/media/line-login/login-button/000000-30-per.png)#000000（不透明度：30％） |
| 無効 | ![white color](https://developers.line.biz/media/line-login/login-button/ffffff.png)#FFFFFF |
| 文字色/ロゴ（無効以外） | ![logo white color](https://developers.line.biz/media/line-login/login-button/ffffff.png)#FFFFFF |
| 文字色/ロゴ（無効のみ） | ![logo grey color](https://developers.line.biz/media/line-login/login-button/1e1e1e-20-per.png)#1E1E1E（不透明度：20％） |
| 縦線（無効以外） | ![line color for other than disabled](https://developers.line.biz/media/line-login/login-button/000000-8-per.png)#000000（不透明度：8％） |
| 縦線（無効） | ![line color for only disabled](https://developers.line.biz/media/line-login/login-button/e5e5e5-60-per.png)#E5E5E5（不透明度：60％） |
| 枠線（無効のみ） | ![border color](https://developers.line.biz/media/line-login/login-button/e5e5e5-60-per.png)#E5E5E5（不透明度：60％） |

<!-- note start -->

**透明色のレイヤーにご注意ください**

透明色は、配置するレイヤーにご注意ください。たとえば、マウスオーバーの縦線の場合、基本色（`#06C755`）のレイヤーの上に、マウスオーバー（`#000000（不透明度：30％）`）を配置し、さらにその上のレイヤーに縦線（`#000000（不透明度：8％）`）とテキスト／ロゴ（`#FFFFFF`）を配置します。

![LINEログインボタンのレイヤー](https://developers.line.biz/media/line-login/login-button/login-button-color-layer-order-ja.png)

各レイヤーの配置について詳しくは、下図を参考にしてください。

<!-- note end -->

![LINEログインボタンの色](https://developers.line.biz/media/line-login/login-button/login-button-color-ja.png)

### テキスト 

LINEログインボタンのテキストは、「LINEでログイン」にすることを推奨しています。各言語での推奨文言については、以下の表を参照してください。

独自のボタンテキストを使用する場合は、以下のガイドラインに従ってください。

- 改行を入れないこと。
- LINEでアプリにログインすることがユーザーにはっきりと伝わること。

LINEアイコンをテキストなしでLINEログインボタンとして使用することも可能です。

|言語|ログインボタンテキスト（長文）|ログインボタンテキスト（短文）|
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

### フォント 

ボタンテキストのフォントは、判読可能なものでなければなりません。画像サイズ毎に推奨される文字の大きさについては、PSDファイルを参照してください。

### 余白 

LINEログインボタンテキストの左右の余白は、LINEアイコンの吹き出しの幅以上である必要があります（以下の図でＸと定義されている部分です）。

上下の余白は吹き出しの幅の1/2を推奨します。文字サイズを選ぶ際は、これらの余白を確保できるようにご注意ください。

![LINEログインボタンの余白](https://developers.line.biz/media/line-login/login-button/login-button-padding-ja.png)

### 保護エリア 

保護エリアとは、LINEログインボタンの周囲の、何も要素を含めない部分です。保護エリアの幅は、LINEアイコンの吹き出しの左の余白と同等以上にしてください（以下の図でAと定義されている部分です）。保護エリアを維持するだけでなく、LINEログインボタンの効果を損なわないよう、テキストやグラフィックを保護エリアの近くに配置しないでください。

![LINEログインボタンの保護エリア](https://developers.line.biz/media/line-login/login-button/login-button-isolation-zone.png)

### よくある間違い 

- 規定以外の色を使用する。
- 旧式のLINEアイコンを使用する。
- 別のアイコンまたは改変したLINEアイコンを使用する。
