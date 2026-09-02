# LINEミニアプリ上でLINE公式アカウントを友だち追加する（友だち追加オプション）

友だち追加オプションを使うと、LINEミニアプリ上でLINE公式アカウントの友だち追加を促すことができます。

## 友だち追加オプションとは 

LINEミニアプリの[アクセス許可要求画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#verification-screen)や[チャネル同意画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#consent-screen-settings)に、LINE公式アカウントを友だち追加するオプションを表示できます。これを、友だち追加オプションと呼びます。

![](https://developers.line.biz/media/line-mini-app/channel-consent-simplification/add-friend-option-verification-screen-ja.png) ![](https://developers.line.biz/media/line-mini-app/channel-consent-simplification/add-friend-option-channel-consent-screen-ja.png)

<!-- tip start -->

**認証プロバイダーの場合、認可画面上の友だち追加オプションはデフォルトでオンになります**

LINEミニアプリチャネルが[認証プロバイダー](https://developers.line.biz/ja/docs/line-developers-console/overview/#certified-provider)に属している場合、アクセス許可要求画面やチャネル同意画面上の友だち追加オプションは、デフォルトでオンになります。

ユーザーがオプションを手動でオフにしない限り、アクセス許可要求画面やチャネル同意画面で認可したときに、友だち追加オプションで指定したLINE公式アカウントが友だちとして追加されます。

<!-- tip end -->

## 友だち追加オプションの利用条件 

友だち追加オプションでLINEミニアプリとLINE公式アカウントをリンクするには、次の条件をすべて満たす必要があります。

- LINE公式アカウントがMessaging APIを利用している（※1）。
- LINE公式アカウントに紐づいているMessaging APIチャネルとLINEミニアプリチャネルが同じプロバイダーに属している。
- 操作するアカウントが、LINEミニアプリチャネルのAdmin権限（※2）とLINE公式アカウントの管理者権限（※3）の両方を持っている。

※1 LINE公式アカウントでMessaging APIを利用する方法について詳しくは、『Messaging APIドキュメント』の「[LINE公式アカウントでMessaging APIを有効にする](https://developers.line.biz/ja/docs/messaging-api/getting-started/#using-oa-manager)」を参照してください。\
※2 LINEミニアプリチャネルのAdmin権限は、[LINE Developersコンソール](https://developers.line.biz/console/)で確認できます。\
※3 LINE公式アカウントの管理者権限は、[LINE Official Account Manager](https://manager.line.biz)で確認できます。

## 友だち追加オプションの設定方法 

1. [LINE Developersコンソール](https://developers.line.biz/console/)でLINEミニアプリチャネルの［**ウェブアプリ設定**］タブを開きます。
1. ［**友だち追加オプション**］を「On (normal)」に設定します。
1. ［**チャネル基本設定**］タブを開きます。
1. 「デフォルトのLINE公式アカウント」セクションの［**編集**］をクリックします（※）。
1. LINEミニアプリチャネルとリンクさせるLINE公式アカウントを選択し、［**更新**］をクリックします。

※ タイおよび台湾のLINEミニアプリチャネルでは、「リンクされたLINE公式アカウント」セクションの［**編集**］をクリックします。

## 任意のタイミングでLINE公式アカウントの友だち追加、またはブロック解除を促す 

[`liff.requestFriendship()`](https://developers.line.biz/ja/reference/liff/#request-friendship)メソッドを使うと、LINE公式アカウントの友だち追加、またはブロック解除を促すサブウィンドウを任意のタイミングで表示できます。

詳しくは、『LIFF APIリファレンス』の「[`liff.requestFriendship()`](https://developers.line.biz/ja/reference/liff/#request-friendship)」を参照してください。

## 友だち追加オプションで複数のLINE公式アカウントを使用する 

友だち追加オプションでは、複数のLINE公式アカウントを使用することもできます。この機能を使うと、あらかじめ許可リスト（※）に登録したLINE公式アカウントの中から、ユーザーの状況に応じた適切なLINE公式アカウントを友だち追加の対象として表示できます。

利用条件と使用方法について詳しくは、次のセクションを参照してください。

- [複数のLINE公式アカウントを使用する機能の利用条件](https://developers.line.biz/ja/docs/line-mini-app/service/add-friend-option/#use-multiple-accounts-requirements)
- [複数のLINE公式アカウントを使用する方法](https://developers.line.biz/ja/docs/line-mini-app/service/add-friend-option/#how-to-use-multiple-accounts)

※ アクセス許可要求画面やチャネル同意画面などに表示できる、LINE公式アカウントのリスト。

### 複数のLINE公式アカウントを使用する機能の利用条件 

友だち追加オプションで複数のLINE公式アカウントを使用するには、「[友だち追加オプションの利用条件](https://developers.line.biz/ja/docs/line-mini-app/service/add-friend-option/#requirements)」に加えて、LINEミニアプリチャネルの［**サービスを提供する地域**］が「日本」である必要があります。

### 複数のLINE公式アカウントを使用する方法 

友だち追加オプションで複数のLINE公式アカウントを使用するには、次の手順で設定と実装を行います。

1. [LINE Developersコンソールで複数のLINE公式アカウントを使用する機能を設定する](https://developers.line.biz/ja/docs/line-mini-app/service/add-friend-option/#configure-use-multiple-accounts)
1. [LINEミニアプリ上で友だち追加を促すLINE公式アカウントを切り替える](https://developers.line.biz/ja/docs/line-mini-app/service/add-friend-option/#switch-line-official-account)

#### 1. LINE Developersコンソールで複数のLINE公式アカウントを使用する機能を設定する 

1. [LINE Developersコンソール](https://developers.line.biz/console/)でLINEミニアプリチャネルの［**ウェブアプリ設定**］タブを開きます。
1. ［**友だち追加オプション**］を「On (normal)」に設定します。
1. ［**チャネル基本設定**］タブを開きます。
1. 「友だち追加オプション」セクションの［**複数アカウントを使用**］をクリックします。

   ![](https://developers.line.biz/media/line-mini-app/service/add-friend-option/use-multiple-accounts-ja.png)

1. 許可リストに関する注意事項が表示されます。注意事項を確認し、［**同意して有効にする**］をクリックします。

   ![](https://developers.line.biz/media/line-mini-app/service/add-friend-option/agree-and-enable-ja.png)

1. 許可リストの編集画面が表示されます。許可リストには、［**デフォルトのLINE公式アカウント**］に設定したアカウントを含め、最大1,000件のLINE公式アカウントを登録できます。許可リストに登録するアカウントを選択し、［**確認**］をクリックします。

   ![](https://developers.line.biz/media/line-mini-app/service/add-friend-option/confirm-ja.png)

1. 確認画面が表示されます。誤りがないことを確認し、［**実行**］をクリックします。

   ![](https://developers.line.biz/media/line-mini-app/service/add-friend-option/apply-ja.png)

<!-- note start -->

**許可リストに関する注意事項**

- LINEミニアプリと同じサービスのLINE公式アカウントを許可リストに登録してください。
- 異なるサービスのLINE公式アカウントを登録することは、[LINEミニアプリポリシー](https://terms2.line.me/LINE_MINI_App?lang=ja)に違反します。
- ポリシー違反が確認された場合は、チャネルの利用を停止することがあります。
- 許可リストへの変更は、審査なしで即時反映されます。
- ［**デフォルトのLINE公式アカウント**］に設定したアカウントを除き、許可リストにLINE公式アカウントが1件も登録されていない場合、［**複数アカウントを使用**］が自動でオフになります。

<!-- note end -->

<!-- tip start -->

**［デフォルトのLINE公式アカウント］の設定は任意です**

友だち追加オプションで複数のLINE公式アカウントを使用する場合、［**デフォルトのLINE公式アカウント**］の設定は任意です。

［**デフォルトのLINE公式アカウント**］を設定すると、アクセス許可要求画面やチャネル同意画面などに表示するLINE公式アカウントを取得できなかった場合に、フォールバックとして表示できます。

<!-- tip end -->

#### 2. LINEミニアプリ上で友だち追加を促すLINE公式アカウントを切り替える 

- [アクセス許可要求画面に表示するLINE公式アカウントを切り替える](https://developers.line.biz/ja/docs/line-mini-app/service/add-friend-option/#verification-screen)
- [チャネル同意画面に表示するLINE公式アカウントを切り替える](https://developers.line.biz/ja/docs/line-mini-app/service/add-friend-option/#channel-consent-screen)
- [LINE公式アカウントの友だち追加、またはブロック解除を促すサブウィンドウに表示するLINE公式アカウントを切り替える](https://developers.line.biz/ja/docs/line-mini-app/service/add-friend-option/#subwindow)

##### アクセス許可要求画面に表示するLINE公式アカウントを切り替える 

アクセス許可要求画面に表示するLINE公式アカウントを切り替えるには、[`liff.permission.requestAll()`](https://developers.line.biz/ja/reference/liff/#permission-request-all)メソッドに`officialAccount`プロパティを指定します。`officialAccount`プロパティを指定するには、LIFF SDKがv2.30.0以上である必要があります。

```javascript
try {
  const permissionStatus = await liff.permission.query("profile");

  if (permissionStatus.state === "prompt") {
    await liff.permission.requestAll({
      officialAccount: {
        id: "@819...",
        fallback: true,
      },
    });
  }
} catch (error) {
  console.error(error);
}
```

詳しくは、『LIFF APIリファレンス』の「[`liff.permission.requestAll()`](https://developers.line.biz/ja/reference/liff/#permission-request-all)」を参照してください。

なお、アクセス許可要求画面は、[`openid`スコープ以外の権限を必要とするメソッド](https://developers.line.biz/ja/docs/line-mini-app/develop/channel-consent-simplification/#request-permissions-other-than-openid)を実行した際にも表示されることがあります。この場合、［**デフォルトのLINE公式アカウント**］に設定したLINE公式アカウントが表示されます。任意のLINE公式アカウントに切り替えることはできません。

##### チャネル同意画面に表示するLINE公式アカウントを切り替える 

チャネル同意画面に表示するLINE公式アカウントを切り替えるには、[LIFF URL](https://developers.line.biz/ja/glossary/#liff-url)または[パーマネントリンク](https://developers.line.biz/ja/glossary/#permanent-link-liff)に`prompt_bot_id`クエリパラメータを付与します。`prompt_bot_id`クエリパラメータには、友だち追加を促すLINE公式アカウントのIDを、ベーシックIDまたは[プレミアムID](https://developers.line.biz/ja/glossary/#premium-id)で指定します。

```
https://miniapp.line.me/123456-abcedfg?prompt_bot_id=@819...
```

##### LINE公式アカウントの友だち追加、またはブロック解除を促すサブウィンドウに表示するLINE公式アカウントを切り替える 

[`liff.requestFriendship()`](https://developers.line.biz/ja/reference/liff/#request-friendship)メソッドを使うと、LINE公式アカウントの友だち追加、またはブロック解除を促すサブウィンドウを任意のタイミングで表示できます。

サブウィンドウに表示するLINE公式アカウントを切り替えるには、`liff.requestFriendship()`メソッドに`officialAccount`プロパティを指定します。`officialAccount`プロパティを指定するには、LIFF SDKがv2.30.0以上である必要があります。

```javascript
try {
  await liff.requestFriendship({
    officialAccount: {
      id: "@819...",
      fallback: true,
    },
    template: { id: "coupon" },
  });
} catch (error) {
  console.log(error);
}
```

詳しくは、『LIFF APIリファレンス』の「[`liff.requestFriendship()`](https://developers.line.biz/ja/reference/liff/#request-friendship)」を参照してください。

## 「チャネル同意の簡略化」機能を併用する場合の注意点 

友だち追加オプションと「[チャネル同意の簡略化](https://developers.line.biz/ja/docs/line-mini-app/develop/channel-consent-simplification/#what-is-channel-consent-simplification)」機能を併用する場合、アクセス許可要求画面およびチャネル同意画面が表示されないことがあります。

詳しくは、「[「チャネル同意の簡略化」機能と友だち追加オプションを併用する際の注意点](https://developers.line.biz/ja/docs/line-mini-app/develop/channel-consent-simplification/#add-friend-option)」を参照してください。
