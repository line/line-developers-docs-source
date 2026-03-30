# 共通プロフィールのクイック入力のデザインレギュレーション

<!-- tip start -->

**認証済ミニアプリでのみ利用できます**

共通プロフィールのクイック入力を利用するには、LINEミニアプリが認証済みであり、かつクイック入力の利用申請を行う必要があります。詳しくは、「[クイック入力の利用手順](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/#process)」を参照してください。

<!-- tip end -->

## クイック入力のユーザー体験 

LINEミニアプリのクイック入力では、エンドユーザーが[自動入力ボタン](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/design-regulations/#what-is-auto-fill-button)をタップすると、プロフィールを確認するモーダルが表示されます。表示されたモーダルでプロフィールを確認後、ユーザーが［**自動で入力する**］をタップすることで、プロフィール情報が自動で入力されます。

なお、モーダルは[`liff.$commonProfile.get()`](https://developers.line.biz/ja/reference/line-mini-app/#get-common-profile)メソッドを呼び出すことで表示できます。このため、モーダルを自社で開発する必要はありません。

モーダルを表示するタイミングは、LINEミニアプリの構成に応じて自由に設定できますが、以下のパターンを推奨および禁止しています。

- [推奨する画面遷移](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/design-regulations/#recommended-screen-transition)
- [禁止する画面遷移](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/design-regulations/#prohibited-screen-transition)

### 推奨する画面遷移 

LINEミニアプリにクイック入力を組み込む際は、以下の画面遷移を推奨します。

- [会員登録画面に遷移したらすぐにモーダルを表示する](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/design-regulations/#show-modal-immediately-after-transition)
- [入力フォームを選択したらモーダルを表示する](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/design-regulations/#show-modal-when-selecting-input-form)
- [自動入力ボタンをタップしたらモーダルを表示する](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/design-regulations/#show-modal-when-tapping-auto-fill-button)
- [チャネル同意画面で同意したら遷移先でモーダルを表示する](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/design-regulations/#show-modal-after-consent-screen)

#### 会員登録画面に遷移したらすぐにモーダルを表示する 

会員登録画面に遷移したら、すぐに[`liff.$commonProfile.get()`](https://developers.line.biz/ja/reference/line-mini-app/#get-common-profile)メソッドを呼び出してモーダルを表示します。このとき、ユーザーがモーダルを一度閉じても再び表示できるよう、会員登録画面に自動入力ボタンを設置します。

![](https://developers.line.biz/media/line-mini-app/quick-fill/recommended-screen-transition-02.png)

#### 入力フォームを選択したらモーダルを表示する 

会員登録画面でユーザーが入力フォームを選択したら、[`liff.$commonProfile.get()`](https://developers.line.biz/ja/reference/line-mini-app/#get-common-profile)メソッドを呼び出してモーダルを表示します。

![](https://developers.line.biz/media/line-mini-app/quick-fill/recommended-screen-transition-04.png)

#### 自動入力ボタンをタップしたらモーダルを表示する 

会員登録画面でユーザーが自動入力ボタンをタップしたら、[`liff.$commonProfile.get()`](https://developers.line.biz/ja/reference/line-mini-app/#get-common-profile)メソッドを呼び出してモーダルを表示します。

![](https://developers.line.biz/media/line-mini-app/quick-fill/recommended-screen-transition-01.png)

#### チャネル同意画面で同意したら遷移先でモーダルを表示する 

LINEミニアプリの[チャネル同意画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#consent-screen-settings)でユーザーが［**許可する**］をタップしたら、そのまま会員登録画面へ遷移させます。会員登録画面へ遷移したら[`liff.$commonProfile.get()`](https://developers.line.biz/ja/reference/line-mini-app/#get-common-profile)メソッドを呼び出してモーダルを表示します。このとき、ユーザーがモーダルを一度閉じても再び表示できるよう、会員登録画面に自動入力ボタンを設置します。

![](https://developers.line.biz/media/line-mini-app/quick-fill/recommended-screen-transition-03.png)

### 禁止する画面遷移 

LINEミニアプリにクイック入力を組み込む際は、以下のような画面遷移は禁止します。このような画面遷移を発見した場合、あらかじめクイック入力の利用申請時に同意いただいた規約に基づき、権限を剥奪することがあります。

- [自動入力するフォーム以外の画面でモーダルを表示する](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/design-regulations/#show-modal-on-non-auto-fill-form)
- [入力フォームに存在しない項目を取得する](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/design-regulations/#get-non-existent-item)
- [フォームへの自動入力を飛ばして確認画面へ遷移する](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/design-regulations/#skip-input-form)

#### 自動入力するフォーム以外の画面でモーダルを表示する 

自動入力するフォーム以外の画面でモーダルを表示することは禁止されています。

![](https://developers.line.biz/media/line-mini-app/quick-fill/prohibited-screen-transition-01.png)

#### 入力フォームに存在しない項目を取得する 

入力フォームに存在しない項目を取得することは禁止されています。たとえば会員登録フォームにフリガナの項目がないにも関わらず、フリガナの情報を取得することは禁止です。

![](https://developers.line.biz/media/line-mini-app/quick-fill/prohibited-screen-transition-02.png)

#### フォームへの自動入力を飛ばして確認画面へ遷移する 

ユーザーがモーダルで［**自動で入力する**］ボタンをタップした後、フォームへの自動入力を飛ばして登録確認画面へ遷移したり、取得したプロフィール情報をそのまま登録して登録完了画面へ遷移したりすることは禁止です。

![](https://developers.line.biz/media/line-mini-app/quick-fill/prohibited-screen-transition-03.png)

## 自動入力ボタンガイドライン 

LINEミニアプリにクイック入力を組み込む際は、以下を遵守してください。

### 自動入力ボタンとは 

4タイプ、計13種類の自動入力ボタンを用意しています。LINEミニアプリにあわせて、任意のボタンを使用してください。ボタンの一覧は「[自動入力ボタンの種類](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/design-regulations/#auto-fill-button)」で確認できます。

![](https://developers.line.biz/media/line-mini-app/quick-fill/auto-fill-button-guideline-01.png)

### 自動入力ボタンの使用例 

ボタンは変形や加工、アニメーション、効果（拡大、回転、装飾）などを加えず、そのまま使用してください。禁止事項について詳しくは、「[自動入力ボタンの禁止事項](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/design-regulations/#auto-fill-button-prohibition)」を参照してください。

![](https://developers.line.biz/media/line-mini-app/quick-fill/auto-fill-button-guideline-02.png)

### 自動入力ボタンの配置 

ユーザーの視認性を高めるため、自動入力ボタンはフォームの入力フィールドと左揃えにして配置するか、中央揃えで配置してください。

#### 左揃えの例 

![](https://developers.line.biz/media/line-mini-app/quick-fill/auto-fill-button-guideline-03.png)

#### 中央揃えの例 

![](https://developers.line.biz/media/line-mini-app/quick-fill/auto-fill-button-guideline-04.png)

#### 配置する際の注意事項 

自動入力ボタンは、ボタンを押したことによって入力されるフォームが認識できる適切な位置に配置してください。

![](https://developers.line.biz/media/line-mini-app/quick-fill/auto-fill-button-guideline-05.png)

#### ボタンの周囲にはクリアスペースを確保してください 

ボタンは、視認性と独立性を確保するために、上下左右に10pxのクリアスペースを確保してください。

![](https://developers.line.biz/media/line-mini-app/quick-fill/auto-fill-button-guideline-06.png)

### 自動入力ボタンの禁止事項 

自動入力ボタンでは、以下のような加工は禁止されています。

| ❌ 拡大縮小 | ❌ 変形（長体、平体、斜体、回転） |
| --- | --- |
| ![](https://developers.line.biz/media/line-mini-app/quick-fill/auto-fill-button-guideline-07.png) | ![](https://developers.line.biz/media/line-mini-app/quick-fill/auto-fill-button-guideline-08.png) |

| ❌ 装飾（影、縁取り、立体表示） | ❌ 要素と重ねての表示 |
| --- | --- |
| ![](https://developers.line.biz/media/line-mini-app/quick-fill/auto-fill-button-guideline-09.png) | ![](https://developers.line.biz/media/line-mini-app/quick-fill/auto-fill-button-guideline-10.png) |

また自動入力ボタンの、以下のような表示や使用方法も禁止されています。

| ❌ 独自のボタンを使う | ❌ 自動入力ボタンの下にテキストを追加する |
| --- | --- |
| ![](https://developers.line.biz/media/line-mini-app/quick-fill/auto-fill-button-prohibition-01.png) | ![](https://developers.line.biz/media/line-mini-app/quick-fill/auto-fill-button-prohibition-02.png) |

| ❌ 自動入力ボタンを拡大、縮小する | ❌ 自動入力ボタンを非表示にする |
| --- | --- |
| ![](https://developers.line.biz/media/line-mini-app/quick-fill/auto-fill-button-prohibition-03.png) | ![](https://developers.line.biz/media/line-mini-app/quick-fill/auto-fill-button-prohibition-04.png) |

## 自動入力ボタンの種類 

4タイプで計13種類の自動入力ボタンを用意しています。LINEミニアプリにあわせて、任意のボタンを使用してください。

- [タイプA](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/design-regulations/#type-a)
- [タイプB](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/design-regulations/#type-b)
- [タイプC](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/design-regulations/#type-c)
- [タイプD](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/design-regulations/#type-d)

<!-- tip start -->

**自動入力ボタンは指定されたサイズで表示してください**

自動入力ボタンはタイプごとに指定されたサイズで表示してください。自動入力ボタンの画像は、指定のサイズに対して2倍の大きさになっているため、実寸で表示しないよう注意してください。

<!-- tip end -->

<!-- note start -->

**自動入力ボタンの画像はURLを指定して使用してください**

自動入力ボタンの画像は、予告なく変更される可能性があります。画像はダウンロードして使用するのではなく、必ず記載のURLを直接指定して使用してください。またあらかじめ告知を行った上で、特定の画像を削除したり、URLを変更したりする可能性もあります。あらかじめご了承ください。

<!-- note end -->

### タイプA 

タイプAは1が基本形で、2から4はカラーバリエーションです。サイズは横が264px、縦が73pxです。ALT属性は、`ユーザー情報を自動入力。LINEやYahoo! JAPANに登録した情報を利用できます`を指定してください。

|  | 自動入力ボタン | URL |
| --- | --- | --- |
| 1 | ![](https://account-center-fe.line-scdn.net/images/quick_fill_button_AC_black.png) | `https://account-center-fe.line-scdn.net/images/quick_fill_button_AC_black.png` |
| 2 | ![](https://account-center-fe.line-scdn.net/images/quick_fill_button_AC_white.png) | `https://account-center-fe.line-scdn.net/images/quick_fill_button_AC_white.png` |
| 3 | ![](https://account-center-fe.line-scdn.net/images/quick_fill_button_AC_gray.png) | `https://account-center-fe.line-scdn.net/images/quick_fill_button_AC_gray.png` |
| 4 | ![](https://account-center-fe.line-scdn.net/images/quick_fill_button_AC_blue.png) | `https://account-center-fe.line-scdn.net/images/quick_fill_button_AC_blue.png` |

### タイプB 

タイプBは1が基本形で、2から4はカラーバリエーションです。サイズは横が264px、縦が73pxです。ALT属性は、`ユーザー情報を自動入力。LINEやYahoo! JAPANに登録した情報を利用できます`を指定してください。

|  | 自動入力ボタン | URL |
| --- | --- | --- |
| 1 | ![](https://account-center-fe.line-scdn.net/images/quick_fill_button_simple_black.png) | `https://account-center-fe.line-scdn.net/images/quick_fill_button_simple_black.png` |
| 2 | ![](https://account-center-fe.line-scdn.net/images/quick_fill_button_simple_white.png) | `https://account-center-fe.line-scdn.net/images/quick_fill_button_simple_white.png` |
| 3 | ![](https://account-center-fe.line-scdn.net/images/quick_fill_button_simple_gray.png) | `https://account-center-fe.line-scdn.net/images/quick_fill_button_simple_gray.png` |
| 4 | ![](https://account-center-fe.line-scdn.net/images/quick_fill_button_simple_blue.png) | `https://account-center-fe.line-scdn.net/images/quick_fill_button_simple_blue.png` |

### タイプC 

タイプCは1の基本形のみです。サイズは横が264px、縦が73pxです。ALT属性は、`ユーザー情報を自動入力。LINEやYahoo! JAPANに登録した情報を利用できます`を指定してください。

|  | 自動入力ボタン | URL |
| --- | --- | --- |
| 1 | ![](https://account-center-fe.line-scdn.net/images/quick_fill_button_LY_white.png) | `https://account-center-fe.line-scdn.net/images/quick_fill_button_LY_white.png` |

### タイプD 

タイプDは1が基本形で、2から4はカラーバリエーションです。サイズは横が288px、縦が66pxです。ALT属性は、`LINEで自動入力しますか？氏名、電話番号、メールアドレス、住所など。自動入力`を指定してください。

|  | 自動入力ボタン | URL |
| --- | --- | --- |
| 1 | ![](https://account-center-fe.line-scdn.net/images/quick_fill_button_LINE_white.png) | `https://account-center-fe.line-scdn.net/images/quick_fill_button_LINE_white.png` |
| 2 | ![](https://account-center-fe.line-scdn.net/images/quick_fill_button_LINE_black.png) | `https://account-center-fe.line-scdn.net/images/quick_fill_button_LINE_black.png` |
| 3 | ![](https://account-center-fe.line-scdn.net/images/quick_fill_button_LINE_gray.png) | `https://account-center-fe.line-scdn.net/images/quick_fill_button_LINE_gray.png` |
| 4 | ![](https://account-center-fe.line-scdn.net/images/quick_fill_button_LINE_blue.png) | `https://account-center-fe.line-scdn.net/images/quick_fill_button_LINE_blue.png` |
