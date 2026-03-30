# カスタム機能

さらにユーザー体験を充実させるために、以下の機能をLINEミニアプリに追加できます。使用できる機能は、LINEミニアプリが未認証ミニアプリか認証済ミニアプリかによって異なります。

| 機能 | 未認証ミニアプリ | 認証済ミニアプリ |
| --- | --- | --- |
| [サービスメッセージ](https://developers.line.biz/ja/docs/line-mini-app/discover/custom-features/#service-messages) | ❌ | ✅ |
| [Custom Path](https://developers.line.biz/ja/docs/line-mini-app/discover/custom-features/#custom-path) | ❌ | ✅ |
| [ユーザー端末のホーム画面にLINEミニアプリへのショートカットを追加する](https://developers.line.biz/ja/docs/line-mini-app/discover/custom-features/#create-shortcut-on-home-screen) | ❌ | ✅ |
| [ユーザーをLINE公式アカウントの友だち追加へ誘導する](https://developers.line.biz/ja/docs/line-mini-app/discover/custom-features/#OA-friend) | ✅ | ✅ |
| [決済システムの利用](https://developers.line.biz/ja/docs/line-mini-app/discover/custom-features/#using-payment-systems) | ✅ | ✅ |
| [カスタムアクションボタン](https://developers.line.biz/ja/docs/line-mini-app/discover/custom-features/#custom-action-button) | ✅ | ✅ |
| [共通プロフィールのクイック入力](https://developers.line.biz/ja/docs/line-mini-app/discover/custom-features/#quick-fill) | ❌ | ✅ |

## サービスメッセージ 

レストランや宿泊施設の予約の確認通知をユーザーに送信する場合は、「サービスメッセージ」を利用できます。

サービスメッセージは、ユーザーからのリクエストに対する確認や応答としてユーザーが知るべき情報を、LINEミニアプリから通知する機能です。

LINEミニアプリから送られたサービスメッセージは、LINEミニアプリの種類にかかわらず、LINEミニアプリを提供する地域ごとに決められたトークルームに表示されます。

| 日本 | タイ | 台湾 |
| :-: | :-: | :-: |
| LINEミニアプリ お知らせ | LINE MINI App Notice | LINE MINI App 通知 |
| ![LINEミニアプリ お知らせ](https://developers.line.biz/media/line-mini-app/mini_service_notifier_jp.png) | ![LINE MINI App Notice](https://developers.line.biz/media/line-mini-app/mini_service_notifier_th.png) | ![LINE MINI App 通知](https://developers.line.biz/media/line-mini-app/mini_service_notifier_tw.png) |

サービスメッセージを送信するには、サービスメッセージAPIを使用します。詳しくは、「[サービスメッセージを送信する](https://developers.line.biz/ja/docs/line-mini-app/develop/service-messages/)」を参照してください。

<!-- note start -->

**サービスメッセージの送信条件**

サービスメッセージは、LINEミニアプリ上でのユーザーの操作（アクション）に対する確認や応答としてのみ送信できます。値下げ、ショッピング特典、新商品、割引クーポン、プロモーションなどの情報を含む広告やイベントの通知は禁止されています。サービスメッセージの条件について詳しくは、「[サービスメッセージの条件](https://developers.line.biz/ja/docs/line-mini-app/service/service-operation/#conditions-for-service-messages)」を参照してください。

<!-- note end -->

## Custom Path 

Custom Pathとは、本番用のLIFF URLに設定する独自の文字列のことをいいます。Custom Path機能を用いると、以下のように、LIFF URLに独自の文字列を設定できます。

| LIFF IDによるURLの例 | Custom Pathを設定した例 |
| --- | --- |
| `https://miniapp.line.me/123456-abcdefg` | `https://miniapp.line.me/cony_coffee` |

たとえば、ユニークな名前をCustom Pathとして設定することにより、ユーザーはURLからどのブランドや店舗のLINEミニアプリなのかがわかるようになります。Custom Pathについて詳しくは、「[Custom Pathを設定する](https://developers.line.biz/ja/docs/line-mini-app/develop/custom-path/)」を参照してください。

## ユーザー端末のホーム画面にLINEミニアプリへのショートカットを追加する 

ユーザー端末のホーム画面にLINEミニアプリへのショートカットを追加できます。この機能を使うと、ユーザーは端末のホーム画面からLINEミニアプリに直接アクセスできるようになります。

![](https://developers.line.biz/media/line-mini-app/develop/add-to-home-screen/add-shortcut-screen-ios-ja.png)
![](https://developers.line.biz/media/line-mini-app/develop/add-to-home-screen/shortcut-ios-ja.png)

会員証やモバイルオーダーなど、ユーザーの利用頻度の高いサービスでこの機能を活用することで、ユーザー体験を向上させることができます。

詳しくは、「[ユーザー端末のホーム画面にLINEミニアプリへのショートカットを追加する](https://developers.line.biz/ja/docs/line-mini-app/develop/add-to-home-screen/)」を参照してください。

## ユーザーをLINE公式アカウントの友だち追加へ誘導する 

LINEミニアプリでは、友だち追加オプションを使って、[アクセス許可要求画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#verification-screen)、もしくは[チャネル同意画面](https://developers.line.biz/ja/docs/line-mini-app/develop/configure-console/#consent-screen-settings)からLINE公式アカウントの友だち追加への誘導ができます。

詳しくは、 「[LINEミニアプリ上でLINE公式アカウントを友だち追加する（友だち追加オプション）](https://developers.line.biz/ja/docs/line-mini-app/service/line-mini-app-oa/#link-a-line-official-account-with-your-channel)」を参照してください。

![bot link feature 1](https://developers.line.biz/media/line-mini-app/miniguide-incremental-01-ja.png)
![bot link feature 2](https://developers.line.biz/media/line-mini-app/miniguide-incremental-02-ja.png)

また、[`liff.requestFriendship()`](https://developers.line.biz/ja/reference/liff/#request-friendship)メソッドを用いて、任意のタイミングでLINE公式アカウントの友だち追加、またはブロック解除を促すサブウィンドウを表示することも可能です。

## 決済システムの利用 

LINE Payだけでなく、クレジットカードなどの支払い方法をLINEミニアプリに統合できます。また日本のみ、[LINEミニアプリのアプリ内課金](https://developers.line.biz/ja/docs/line-mini-app/discover/custom-features/#in-app-purchase)機能を利用できます。詳しくは、「[決済システムを利用する](https://developers.line.biz/ja/docs/line-mini-app/develop/payment/)」を参照してください。

![mini intro linepay](https://developers.line.biz/media/line-mini-app/mini_intro_linepay.png)

## カスタムアクションボタン 

友だち同士で、LINEミニアプリを簡単にシェアするために[ビルトインのアクションボタン](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#action-button)が用意されていますが、[カスタムアクションボタンを実装](https://developers.line.biz/ja/docs/line-mini-app/develop/share-messages/)することもできます。

![](https://developers.line.biz/media/line-mini-app/mini_share_custom.png)

## 共通プロフィールのクイック入力 

クイック入力とは、LINEミニアプリ上で［**自動入力**］をタップすることで、必要なプロフィール情報が自動で入力される機能です。ユーザーがアカウントセンターで設定した共通プロフィールの情報が、LINEミニアプリで簡単に利用できます。詳しくは、[共通プロフィールのクイック入力の概要](https://developers.line.biz/ja/docs/line-mini-app/quick-fill/overview/)を参照してください。

![](https://developers.line.biz/media/line-mini-app/quick-fill/quick-fill-3-steps.png)

LINEミニアプリにクイック入力を導入すると、住所や電話番号の登録が必要な場面で、ボタンをタップするだけで必要な情報が自動で入力されます。これにより、たとえば店舗の予約やオンラインストアでの注文時に、ユーザーは面倒な手入力の手間を省くことができます。
