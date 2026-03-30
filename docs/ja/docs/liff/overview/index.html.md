# LINE Front-end Framework (LIFF)

LINE Front-end Framework（LIFF）は、LINEヤフー株式会社が提供するウェブアプリのプラットフォームです。このプラットフォームで動作するウェブアプリを、LIFFアプリと呼びます。

LIFFアプリを使うと、LINEのユーザーIDなどをLINEプラットフォームから取得できます。LIFFアプリではこれらを利用して、ユーザー情報を活用した機能を提供したり、ユーザーの代わりにメッセージを送信したりできます。

LIFF v2で追加された機能については、「[リリースノート](https://developers.line.biz/ja/docs/liff/release-notes/)」を参照してください。

<!-- tip start -->

**LIFFの機能をウェブ上で試せます**

LINEヤフー株式会社では開発者向けに[LIFFプレイグラウンド](https://liff-playground.netlify.app/)というウェブアプリ（LIFFアプリ）を提供しています。LIFFプレイグラウンドではLIFFの基本的な機能が試せます。LIFFを用いるとどのようなことができるのかを確認したいときに参照してください。なお、[LIFFプレイグラウンドのソースコード](https://github.com/line/liff-playground)をGitHubで公開しています。

<!-- tip end -->

<!-- note start -->

**OpenChatでのLIFFアプリの利用はサポートされていません**

現在のところ、OpenChatではLIFFアプリの利用は正式にサポートされていません。たとえば、LIFFアプリからプロフィール情報を取得できない場合があります。

<!-- note end -->

## デモ用のLIFFアプリを体験する 

[LINE API Use Case](https://lineapiusecase.com/)では、デモ用のLIFFアプリと、そのソースコードを公開しています。お手持ちのスマートフォンでデモ用のLIFFアプリを開いて、店舗予約やテーブルオーダーを体験してみましょう。

- [デモ用のLIFFアプリでヘアサロンやレストランの店舗予約を体験する](https://lineapiusecase.com/ja/usecase/reservation.html)
- [デモ用のLIFFアプリでデジタル会員証を体験する](https://lineapiusecase.com/ja/usecase/membership.html)
- [デモ用のLIFFアプリでテーブルオーダーを体験する](https://lineapiusecase.com/ja/usecase/tableorder.html)
- [デモ用のLIFFアプリでスマホレジを体験する](https://lineapiusecase.com/ja/usecase/smartretail.html)

## 推奨環境 

LIFFの推奨環境は以下のとおりです。

なお、LIFFアプリを[LIFFブラウザ](https://developers.line.biz/ja/docs/liff/overview/#liff-browser)で開いた場合と、[外部ブラウザ](https://developers.line.biz/ja/glossary/#external-browser)で開いた場合では、使用できる機能が異なります。たとえば、`liff.scanCode()`は、外部ブラウザでは利用できません。詳しくは、「[LIFF v2 APIリファレンス](https://developers.line.biz/ja/reference/liff/)」を参照してください。

### LIFFアプリをLIFFブラウザで開く場合 

| 項目 | 推奨環境 | 最低動作環境 |
| --- | --- | --- |
| iOS | 最新バージョン。[WKWebView](https://developer.apple.com/documentation/webkit/wkwebview)が使用されます。 | LINEの推奨環境に準ずる。 \* |
| Android | 最新バージョン。[Android WebView](https://developer.android.com/reference/android/webkit/WebView)が使用されます。 | LINEの推奨環境に準ずる。 \* |
| LINE | 最新バージョン | LINEの推奨環境に準ずる。 \* |

<!-- note start -->

**LIFFアプリは、OS、LINEともに最新バージョンの環境での利用を推奨します**

LIFFアプリは、OS、LINEともに最新バージョンの環境での利用を推奨します。上記の「最低動作環境」以降のバージョンでも、機能や設定によっては動作しない場合や画面が正常に表示されない場合があります。

<!-- note end -->

\* LINEの推奨環境については、ヘルプセンターの「[LINEの推奨環境を教えてください](https://help.line.me/line/ios/pc?lang=ja&contentId=10002433)」を参照してください。

### LIFFアプリを外部ブラウザで開く場合 

以下のブラウザの最新バージョンで動作します。

Microsoft Edge、Google Chrome、Firefox、Safari

## LIFFブラウザ 

LIFFブラウザはLIFFアプリ専用のブラウザです。ユーザーがLINEでLIFFのURLを開くと、LIFFブラウザでLIFFアプリが開きます。

![LIFF browser](https://developers.line.biz/media/liff/overview/liffBrowser.png)

LIFFブラウザはLINE内で動作するため、LIFFアプリはユーザーにログインを促さなくてもユーザーデータにアクセスすることができます。また、LIFFブラウザはLIFFアプリを共有したり、LIFFアプリから友だちにメッセージを送るなど、LINE特有の機能を提供しています。

## LIFFブラウザの仕様 

LIFFブラウザは、iOSでは[WKWebView](https://developer.apple.com/documentation/webkit/wkwebview)、Androidでは[Android WebView](https://developer.android.com/reference/android/webkit/WebView)を利用しています。そのため、LIFFブラウザの仕様および動作についてもこれらの仕組みに準拠します。

なお、LIFFブラウザは、外部ブラウザがサポートしているウェブ技術の一部をサポートしていません。詳しくは、「[LIFFブラウザと外部ブラウザの違い](https://developers.line.biz/ja/docs/liff/differences-between-liff-browser-and-external-browser/)」を参照してください。

## LIFFブラウザのキャッシュ 

LIFFブラウザが利用している[WKWebView](https://developer.apple.com/documentation/webkit/wkwebview)や[Android WebView](https://developer.android.com/reference/android/webkit/WebView) は、表示したコンテンツの内容を、[Cache-Control](https://developer.mozilla.org/ja/docs/Web/HTTP/Reference/Headers/Cache-Control) などのHTTPヘッダーの指示に従って、キャッシュとして保存して利用する場合があります。

LIFFブラウザにおけるキャッシュの制御については、[Cache-Control](https://developer.mozilla.org/ja/docs/Web/HTTP/Reference/Headers/Cache-Control) などのHTTPヘッダーを用いて行ってください。

<!-- note start -->

**キャッシュの削除について**

LIFFブラウザに保存されたキャッシュを明示的に削除することはできません。

<!-- note end -->

## LIFFブラウザの画面サイズ 

LIFFブラウザは、以下の3つの画面サイズで表示できます。

![画面サイズ](https://developers.line.biz/media/liff/overview/viewTypes.png)

画面サイズは、LIFFアプリをLINEログインチャネルに追加するときに指定します。詳しくは、「[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/#registering-liff-app)」を参照してください。

## アクションボタン 

LIFFアプリの画面サイズを`Full`に指定している場合、ヘッダーには、デフォルトでアクションボタンが表示されます。

![](https://developers.line.biz/media/news/2025/liff-action-button-after.png)

<!-- tip start -->

**アクションボタンを非表示にする**

LINE DevelopersコンソールでLIFFアプリの［**モジュールモード**］をオンにすると、アクションボタンを非表示にできます。詳しくは、「[LIFFアプリをチャネルに追加する](https://developers.line.biz/ja/docs/liff/registering-liff-apps/)」を参照してください。

<!-- tip end -->

アクションボタンを押すと、[マルチタブビュー](https://developers.line.biz/ja/docs/liff/overview/#multi-tab-view)または[オプション](https://developers.line.biz/ja/docs/liff/overview/#multi-tab-view-option)のどちらかがLINEアプリのバージョンに応じて表示されます。LINEバージョン15.12.0以降ではマルチタブビューが表示され、LINEバージョン15.12.0未満ではオプションが表示されます。

## マルチタブビュー 

マルチタブビューには、使用中のLIFFアプリのオプションと最近使用したサービスが表示されます。

1. [オプション](https://developers.line.biz/ja/docs/liff/overview/#multi-tab-view-option)
1. [最近使用したサービス](https://developers.line.biz/ja/docs/liff/overview/#multi-tab-view-recent-service)

![](https://developers.line.biz/media/liff/overview/liff-multi-tab-view-ja.png)

### オプション 

以下のオプションが、ユーザーのLINEアプリの設定言語で表示されます。

| 項目 | 説明 |
| --- | --- |
| **更新** | 現在開いているページを再読み込みします。 |
| **シェア** | 現在開いているページの[パーマネントリンク](https://developers.line.biz/ja/glossary/#permanent-link-liff)を、LINEメッセージでシェアします。 |
| **ページを最小化** | LIFFブラウザを最小化します。詳しくは、「[LIFFブラウザを最小化する](https://developers.line.biz/ja/docs/liff/minimizing-liff-browser/)」を参照してください。 |
| **権限設定** | 権限設定画面を開きます。権限設定画面では、現在開いているLIFFアプリのカメラやマイクへのアクセス権を確認できます。変更はできません。LINEバージョン14.6.0以降で利用可能です。 |

<!-- note start -->

**パーマネントリンクのシェアに失敗する場合があります**

現在のページのURLがLINE Developersコンソールの［**エンドポイントURL**］に指定したURLで始まらない場合、パーマネントリンクを取得できずシェアに失敗します。

<!-- note end -->

### 最近使用したサービス 

最近使用したサービスには、ユーザーが開いたLIFFアプリが、利用履歴の新しい順に最大50件まで表示されます。

LIFFアプリを閉じたり、別のLIFFアプリを新たに開いたりするとその時点のスクリーンショットが利用履歴として表示されます。ユーザーは利用履歴を使って、LIFFアプリを再度開くことができます。

LIFFアプリが利用履歴から再度開かれた際、LIFFアプリは再開または再読み込みされます。再開、再読み込みの仕様は、以下のとおりです。

| 再度開かれた際の挙動 | 条件 | 仕様 |
| --- | --- | --- |
| LIFFアプリが再開される | <p>以下の条件を両方満たすLIFFアプリ</p><ul><li>12時間以内に使用したLIFFアプリ</li><li>利用履歴の最新10件に含まれるLIFFアプリ</li></ul> | ユーザーが使用を中断した画面からLIFFアプリが再開します。アクセストークン、ブラウザの閲覧履歴、画面のスクロール位置は保持されています。 |
| LIFFアプリが再読み込みされる | 再開される条件を満たさない場合 | ユーザーが使用を中断したURLでLIFFアプリが初期化されます。アクセストークン、ブラウザの閲覧履歴、画面のスクロール位置は破棄されます。 |

#### 最近使用したサービスに表示される条件 

最近使用したサービスにLIFFアプリが表示されるには、以下の条件をすべて満たす必要があります。

- LINEアプリのバージョンが15.12.0以降
- LIFFアプリの[画面サイズ](https://developers.line.biz/ja/docs/liff/overview/#screen-size)に`Full`を指定
- LIFFアプリのモジュールモードがオフ

#### 最近使用したサービスに表示される単位 

最近使用したサービスでは、LIFFアプリがLIFF ID単位で表示されます。同じLIFFアプリを「最近使用したサービス」以外から再度開いた場合は、新たにLIFFアプリが開かれ、古いLIFFアプリは終了します。

なお、LIFF間遷移で他のLIFFアプリを開いた場合は、異なるLIFF IDであっても1つのLIFFアプリとしてまとめて表示されます。

#### LIFFアプリが再読み込みされた場合`liff.sendMessages()`メソッドは使用できません 

最近使用したサービスから再読み込みされたLIFFアプリで、[`liff.sendMessages()`](https://developers.line.biz/ja/reference/liff/#send-messages)メソッドを使用するとエラーが発生します。このため、LIFFアプリが再読み込みされた場合`liff.sendMessages()`メソッドは使用できません。

LIFFアプリが再読み込みされた後に`liff.sendMessages()`メソッドを使いたい場合は、トークルーム上のLIFF URLをタップするなどしてLIFFアプリを開き直す必要があります。

## 開発上のガイドライン 

LIFFアプリを開発する際は、「[LIFFアプリ開発ガイドライン](https://developers.line.biz/ja/docs/liff/development-guidelines/)」に従ってください。

## LIFFアプリの開発をサポートするツール 

LINEヤフー株式会社では、開発者の方々がLIFFアプリの開発をより円滑に行えるよう、以下のツールを提供しています。

| ツール名 | このツールでできること |
| --- | --- |
| [LIFFスターターアプリ](https://developers.line.biz/ja/docs/liff/trying-liff-app/) | LIFFについて初めて学ぶ人向けのスターターアプリです。LIFFアプリの開発の始め方を理解しやすいよう、LIFFアプリの初期化のデモのみを行っています。まずは動くものを作って、LIFFの概要を大まかに理解したい方にお勧めです。 |
| [Create LIFF App](https://developers.line.biz/ja/docs/liff/cli-tool-create-liff-app/) | LIFFアプリの開発環境がコマンド1つで構築できるCLIツールです。Reactの[Create React App](https://github.com/facebook/create-react-app)や、Next.jsの[Create Next App](https://nextjs.org/docs/pages/api-reference/cli/create-next-app)のように、Create LIFF Appからの質問に答えていくことで、用途に合わせたLIFFアプリのひな形を含む開発環境が生成され、すぐに開発を始めることができます。 |
| [LIFF CLI](https://developers.line.biz/ja/docs/liff/liff-cli/) | <p>LIFFアプリの開発を円滑にするCLIツールです。LIFF CLIでできることは次のとおりです。</p><ul><li>LIFFアプリを作成、更新、参照、削除する</li><li>LIFFアプリの開発環境を作成する</li><li>LIFFアプリを[LIFF Inspector](https://developers.line.biz/ja/docs/liff/liff-plugin/#liff-inspector)でデバッグする</li><li>ローカル開発サーバーをHTTPSで起動する</li></ul>今後のアップデートで[LIFF Mock](https://developers.line.biz/ja/docs/liff/liff-plugin/#liff-mock)の機能も追加される予定です。 |
| [LIFFプレイグラウンド](https://liff-playground.netlify.app/) | LIFFの機能をオンライン上で試すことができます。[LIFFプレイグラウンドのソースコード](https://github.com/line/liff-playground)はGitHubで公開していますので、開発者は任意のLIFF IDを設定して、独自のLIFFプレイグラウンドをサーバー上にデプロイすることも可能です。 |

## 作業の流れ 

LIFFアプリをエンドユーザーが利用できるようにするには、以下の手順を行います。

1. LIFFアプリを追加する[チャネルを作成する](https://developers.line.biz/ja/docs/liff/getting-started/)
1. [LIFFスターターアプリを試してみる](https://developers.line.biz/ja/docs/liff/trying-liff-app/)、または[LIFFアプリを開発する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/)
