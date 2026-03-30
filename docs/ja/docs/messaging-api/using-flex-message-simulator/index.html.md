# チュートリアル - Flex Message Simulatorでデジタル名刺を作成する

Flex Messageは、[CSS Flexible box (CSS Flexbox)](https://www.w3.org/TR/css-flexbox-1/)を基盤に自由にカスタマイズできるメッセージです。必要に応じて、メッセージのサイズを調整したり、特定の場所にテキスト、画像、アイコンを割り当てたり、インタラクティブなボタンを追加したりできます。

このチュートリアルでは、[Flex Message Simulator](https://developers.line.biz/flex-simulator/)を使ったデジタル名刺の作り方を紹介します。Flex Message Simulatorはコードを記述せずにFlex Messageのブレインストーミング、設計、プロトタイプ作成ができるツールです。Flex Messageを初めて使う場合は、まず「[Flex Messageを送信する](https://developers.line.biz/ja/docs/messaging-api/using-flex-messages/)」を参照してください。

## 目標 

このチュートリアルを最後まで進めると、次の画像のようなデジタル名刺が完成します。また、この[ダウンロードリンク](https://developers.line.biz/media/code-samples/flex-message-simulator-example-ja.json)から、JSONで定義された結果を取得できます。しかし、このチュートリアルを通してFlex Message Simulatorに慣れることをお勧めします。このツールは、Flex Messageのさまざまなユースケースに対処するのにとても便利だからです。

![アウトプット](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/ja-final-output.png)

## はじめる前に 

チュートリアルをスムーズに進めるために、「[Messaging APIの概要](https://developers.line.biz/ja/docs/messaging-api/overview/)」および「[Flex Messageを送信する](https://developers.line.biz/ja/docs/messaging-api/using-flex-messages/)」を読んでおくことをお勧めします。また、初めてFlex Message Simulatorを使う場合は、このセクションから読み進めてFlex Message Simulatorについて学んでいきましょう。もし、すでにFlex Message Simulatorに慣れているなら、[チュートリアル本編](https://developers.line.biz/ja/docs/messaging-api/using-flex-message-simulator/#select-flex-message)から始めてください。

### Flex Message Simulatorについて知ろう 

Flex Message Simulatorは、Flex Messageを作成し、プレビューできるツールです。開発環境を用意したりコードを書いたりすることなく、Flex Messageを作成し、Flex Messageを送信してプレビューできます。

まず、[Flex Message Simulator](https://developers.line.biz/flex-simulator/)を開いてください。[LINE Developersコンソール](https://developers.line.biz/console/)にログインしていない場合は、ログインを求められます。LINE Developersコンソールの開発者アカウントを持っている場合、ログインしてください。アカウントを持っていない場合、［**アカウントを作成**］をクリックし、手順に従ってアカウントを作成してください。

Flex Message Simulatorの画面は3つの部分で構成されています。

- **プレビューエリア**：ツリービューエリアとプロパティエリアで入力したデータを元にしたFlex Messageが表示される部分。
- **ツリービューエリア**：Flex Messageのデータ構造を編集したり表示したりする部分。
- **プロパティエリア**：ツリービューエリアで選択した項目のプロパティを設定する部分。この領域で入力したデータを基に、Flex Message SimulatorはFlex Messageを生成します。

![Flex Message エリア](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/ja-areas.png)

ツリービューエリアの項目の上にマウスを置くと、該当する部分がプレビューエリアでハイライトされます。この動作は次の動画で確認できます。

<video width="883" height="381" controls>
  <source src="https://vos.line-scdn.net/line-developers/docs/media/video/flex-message-simulator.mp4" type="video/mp4">
  お使いのブラウザはビデオタグに対応していません。
</video>

#### 定義済みのFlex Messageレイアウトを使用できます 

Flex Message Simulatorでは、定義済みのFlex Messageレイアウトが提供されています。

定義済みのレイアウトを使用するには、ページの右上にある［**Showcase**］をクリックします。使いたいレイアウトをクリックし、画面右下の［**作成**］をクリックします。

<!-- note start -->

**レイアウトについて**

このチュートリアルでは、定義済みのレイアウトを使用せずに、Flex Messageを最初から作成します。

<!-- note end -->

![Flex Message Simulator Showcase](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/showcase.png)

#### 作成したFlex MessageのJSONをコピーできます 

生成されたJSONデータをコピーするには、ページの右上にある［**</>View as JSON**］をクリックし、［**コピー**］をクリックします。

![View as JSON](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/view-as-json.png)

## チュートリアルをショートカットする 

手順を読まずに飛ばして結果だけを見たい場合は、Flex MessageオブジェクトのJSONデータを[ダウンロード](https://developers.line.biz/media/code-samples/flex-message-simulator-example-ja.json)できます。Flex Message Simulatorでは、次の手順で結果をプレビューできます。

1. ［ **</>View as JSON**］をクリックします。JSONデータのモーダルが表示されます。
1. モーダル内のコードを削除します。
1. ダウンロードしたJSONファイルの中身をコピーし、モーダルにペーストします。
1. ［**適用**］をクリックして変更を保存します。ペーストしたFlex Messageがプレビューエリアに表示されます。

![サンプルのJSONデータから作成したFlex Messageをプレビューする](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/ja-confirm-example-code-output.png)

## 1. コンテナタイプを選ぶ 

それでは、Flex Message Simulatorを学ぶために、デジタル名刺の作成を始めましょう。名刺を作るのに必要なのはバブル1つだけですから、Flex Messageコンテナのタイプは[バブル](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/#bubble)になります。

バブルタイプのFlex Messageコンテナを作成するには、右上の［**New**］をクリックし、ドロップダウンメニューから［**bubble**］を選択します。

![Bubbleタイプのコンテナを選択する](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/select-bubble-type.png)

<!-- tip start -->

**ヒント**

ドロップダウンメニューから［**bubble**］を選択すると、プレビューエリアの下に「OK」メッセージがポップアップ表示されます。これは、編集内容がプレビューエリアに正常に反映されたことを意味します。

![Messageタイプを選択する](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/type.png)

<!-- tip end -->

コンテナのタイプの詳細については、「[コンテナ](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/#container)」を参照してください。

## 2. ヘッダーを追加する 

作成したコンテナに、会社名を表示するヘッダーを追加しましょう。ヘッダーは「[ブロック](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/#block)」のタイプの一つで、ほかにヒーロー、ボディおよびフッターがあります。ヘッダーは主にメッセージの件名やコンテンツの見出しの表示に使用されます。

![Blockスタイル例](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/elements.png)

1. ヘッダーを追加するために、ツリービューエリアで［**header**］を選択します。上部の［**+**］をクリックし、［**box**］を選択します。
1. ヘッダーの背景色を設定します。プロパティエリアの［**backgroundColor**］フィールドに、16進数カラーコードの背景色（このチュートリアルでは`#00B900`）を入力し、Enterキーを押します。これで、ヘッダーがボディブロックと視覚的に区別できるようになりました。

   <!-- tip start -->

   **入力内容を反映するにはEnterキーを押します**

   プロパティエリアで項目を編集または選択し、キーボードのEnterキーを押すと、プレビューエリアに反映されます。これ以降の説明では、Enterキーの操作は省略します。

   <!-- tip end -->

   ![ヘッダーの背景色を設定する](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/set-header-color.png)

1. ヘッダーにテキストを追加します。
   1. ツリービューで、［**header**］の下の［**box [vertical]**］をクリックします。

      <!-- tip start -->

      **ヒント**

      Vertical box（垂直ボックス）は、Flex Messageのレイアウト方式の一つです。子要素を配置する向きを決定します。詳しくは、[ボックスコンポーネントの向き](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#box-component-orientation)を参照してください。

      <!-- tip end -->

   1. ツリービューの［**+**］をクリックし、ドロップダウンメニューから［**text**］を選択します。［**text**］が［**box [vertical]**］の下に作成されます。
   1. ツリービューで、作成したtext要素をクリックします。
   1. プロパティエリアの［**text**］フィールドで、値を「hello, world」から「Flex Message Corp」に書き換えます。

背景色を変更したのでヘッダーが目立つようになりましたが、テキストが少し読みづらくなりました。それでは、テキストの色とフォントの太さを変更して見やすくしましょう。ツリービューエリアで［**text**］をクリックし、プロパティエリアの［**color**］フィールドを`#FFFFFF`に、［**weight**］フィールドの値を`bold`に設定します。

これで、次のような表示になったか確認しましょう。テキストがはっきり見える、目立つヘッダーになりました。

![ヘッダーアウトプット](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/add-header-final.png)

## 3. 画像を追加する 

デジタル名刺の見栄えをよくする方法の一つに、画像の追加があります。Flex Message Simulatorを使うと、画像の追加やスタイル設定が簡単にできます。画像を追加するには、主に画像コンテンツの表示に使用する[ヒーローブロック](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/#block)を使います。

1. ツリービューエリアの［**hero**］をクリックします。
1. 左上の［**+**］をクリックし、ドロップダウンメニューから［**image**］を選択します。デフォルト画像がプレビューエリアに表示されます。
1. 画像を変更するために、ツリービューエリアで［**image**］をクリックします。プロパティエリアの［**url**］フィールドに、名刺のポートレート画像のURLを入力します。このチュートリアルでは、[こちら](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/mary.png)の画像を使用します。

   <!-- note start -->

   **画像に関する要件**

   Flex Message Simulatorに画像ファイルはアップロードできません。すでにウェブ上にアップロードされている画像のURLを指定してください。画像とそのURLは、以下の条件を満たす必要があります。
   - プロトコル：HTTPS（TLS 1.2以降）
   - 画像フォーマット：JPEGまたはPNG
   - 最大画像サイズ：1024 x 1024ピクセル
   - 最大ファイルサイズ：10MB

   <!-- note end -->

   <!-- tip start -->

   **推奨ファイルサイズ**

   表示の遅延を防ぐために、個々の画像ファイルサイズを1MB以下にすることを推奨しています。

   <!-- tip end -->

画像はうまく反映されましたが、背景と比較すると少し小さいようです。サイズを調整しましょう。

![画像を追加する](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/add-image.png)

画像サイズを変更するには、ツリービューで［**image**］をクリックし、［**size**］プロパティで画像の幅を指定します。このチュートリアルではフィールドの右隣のボタンをクリックして、ドロップダウンメニューから`xl`を選択します。あるいは、値を入力してピクセルまたは`%`で指定することも可能です。詳しくは、Messaging API リファレンスの『[画像](https://developers.line.biz/ja/reference/messaging-api/#f-image)』の「size」欄を参照してください。

これで名刺の画像が大きくなりました。

![画像が追加されたメッセージ](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/add-image-final.png)

## 4. 名前を追加する 

名刺に名前は必須です。名前などの重要な情報は、目立ちやすいスタイルで提示するのが効果的です。画像の下に名前を入れる手順は次のとおりです。

1. ツリービューエリアで、［**body**］の下の［**box [vertical]**］をクリックします。
1. ［**+**］をクリックし、ドロップダウンメニューから［**text**］を選択します。テキストの要素がボックスの下に作成されます。
1. ツリービューエリアで、［**text**］をクリックします。
1. プロパティエリアで、［**text**］フィールドのテキストの内容を「hello, world」から名前に変更します。

[ヘッダーテキスト](https://developers.line.biz/ja/docs/messaging-api/using-flex-message-simulator/#add-header)と同じように、名前にもスタイルを追加しましょう。フォントサイズを大きくして太字にし、テキストを中央揃えにします。

- **サイズ**：［**size**］フィールドで`xl`を選択（デフォルトのサイズは`md`です）
- **太字**：［**weight**］フィールドで`bold`を選択
- **中央揃え**：［**align**］フィールドで`center`を選択

次のように、名刺に名前が入りました。

![名前が追加されたメッセージ](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/ja-add-name-final.png)

## 5. 役職を追加する 

名刺に記載される内容で名前と同じくらい重要な情報は、役職です。名前の下に役職を追加しましょう。

1. ツリービューエリアで、［**body**］の下にある1つ目の［**box [vertical]**］をクリックします。
1. ［**+**］をクリックし、ドロップダウンメニューから［**text**］を選択します。これで新しいテキスト欄ができました。
1. ツリービューエリアで、作成した［**text**］要素をクリックします。
1. プロパティエリアに、textフィールドが表示されます。テキストの内容を「hello, world」から役職に変更します。

先ほど名前を中央揃えにしたので、役職も同様に中央揃えにしましょう。プロパティエリアで、［**align**］フィールドを`center`に設定します。

これで、名刺に役職が追加されました。

![役職が追加されたメッセージ](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/ja-add-job-title-final.png)

## 6. セパレータを追加する 

この後、名刺をインタラクティブにするためのボタンを追加する予定です。その前に、[セパレータ](https://developers.line.biz/ja/reference/messaging-api/#separator)を追加して、情報セクションとインタラクティブセクションを視覚的に分離しましょう。

1. ツリービューエリアで、［**body**］の下にある1つ目の［**box [vertical]**］をクリックします。
1. ［**+**］をクリックし、ドロップダウンメニューから［**separator**］を選択します。役職のすぐ下にセパレータが追加されます。

![セパレータを追加する](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/ja-add-separator.png)

セパレータとその上の役職の間隔が狭く見えます。セパレータにマージンを設定して、両者の間に空間を作りましょう。マージンついて詳しくは、『Messaging APIリファレンス』の「[セパレータ](https://developers.line.biz/ja/reference/messaging-api/#separator)」を参照してください。

1. ツリービューエリアで、［**separator**］をクリックします。
1. プロパティエリアで、［**margin**］フィールドを`md`に設定します。

これで、余裕を持ったセパレータが追加されました。

![セパレータが追加されたメッセージ](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/ja-add-separator-final.png)

## 7. ボタンを追加する 

手順6で述べたように、名刺をインタラクティブにするために、ボタンを追加しましょう。セパレータの下に2つのボタンを追加したいと思います。まず、ボタンをグループ化するためのコンポーネントが必要です。

1. ［**body**］の下の最初の［**box [vertical]**］をクリックします。
1. ［**+**］をクリックし、ドロップダウンメニューから［**box**］を選択します。これにより、ボタンを追加できる新しい垂直ボックスが作成できました。

それでは、押すとアクションが実行されるボタンを作っていきます。ボタンに使用できるアクションのタイプは、[URIアクション](https://developers.line.biz/ja/reference/messaging-api/#uri-action)や[ポストバックアクション](https://developers.line.biz/ja/reference/messaging-api/#postback-action)などです。このチュートリアルでは次の2つのボタンを追加します。

1. [会社のウェブサイトに移動する](https://developers.line.biz/ja/docs/messaging-api/using-flex-message-simulator/#add-action-1)
1. [LINE Front-end Framework（LIFF）で作成された登録フォームを開く](https://developers.line.biz/ja/docs/messaging-api/using-flex-message-simulator/#add-action-2)

### 7-1. 会社のウェブサイトに移動する 

次の手順で、会社のウェブサイトに移動するようにボタンを設定します。

1. ツリービューエリアで、先ほど作成したボタンを追加するための［**box [vertical]**］をクリックします。
1. ［**+**］をクリックし、ドロップダウンメニューから［**button**］を選択します。
1. ［**button [action]**］をクリックします。
1. プロパティエリアを一番下までスクロールすると［**Action**］セクションがあります。［**type**］プロパティのデフォルトは`uri`です。今回設定するのはウェブサイトのURLなので、値はこのままにしておきます。
1. 同じ［**Action**］セクションで、［**label**］プロパティに「Flex Message Corp 公式サイト」と入力します。これがボタンのラベルになります。
1. ウェブサイトを開くために、［**uri**］プロパティにウェブサイトのURIを入力します。

<!-- note start -->

**uriフィールドのドメイン名、パス、クエリパラメータ、フラグメントはパーセントエンコードしてください**

［**uri**］フィールドのドメイン名、パス、クエリパラメータ、フラグメントはUTF-8を用いて[パーセントエンコード](https://ja.wikipedia.org/wiki/%E3%83%91%E3%83%BC%E3%82%BB%E3%83%B3%E3%83%88%E3%82%A8%E3%83%B3%E3%82%B3%E3%83%BC%E3%83%87%E3%82%A3%E3%83%B3%E3%82%B0)してください。たとえば、以下の構成要素を持つURIを指定する場合は、`https://example.com/path?q=%E3%81%8A%E3%81%AF%E3%82%88%E3%81%86#%E3%81%93%E3%82%93%E3%81%AB%E3%81%A1%E3%81%AF`とします。

| スキーム | ドメイン名  | パス  | クエリパラメータ | フラグメント |
| -------- | ----------- | ----- | ---------------- | ------------ |
| https    | example.com | /path | q=おはよう       | こんにちは   |

<!-- note end -->

これで、タップすると会社のウェブサイトに移動するボタンが名刺に追加されました。

![URIアクションボタンを追加する](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/ja-add-uri-button.png)

ヘッダーテキストや名前、役職で実施したように、ボタンにもスタイルを追加しましょう。ボタンに色を追加することで、タップ可能な領域がわかりやすくなります。次の3種類の定義済みのボタンスタイルから選んで色をつけることができます。

- **primary**：濃色のボタン向けのスタイル
- **secondary**：淡色のボタン向けのスタイル
- **link**：HTMLのテキストリンクのスタイル

このチュートリアルのように、コンポーネント内で複数のボタンを縦に重ねて配置する場合、`link`スタイルの使用を推奨します。背景に色を付ける代わりに、linkスタイルを適用しましょう。

1. ツリービューエリアで、［**button**］をクリックします。
1. プロパティーエリアで、［**style**］プロパティを`link`に設定します。

ボタンが次のように表示されます。

![ボタンの色を変更する](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/ja-change-button-color.png)

### 7-2. LINE Front-end Framework（LIFF）で作成された登録フォームを開く 

それでは、残りのボタンを追加していきましょう。2つ目のボタンには、ビジネスの登録フォームに[LINE Front-end Framework（LIFF）](https://developers.line.biz/ja/docs/liff/overview/)URLを追加します。LIFFで登録フォームを作成すると、そのフォームで取得した情報を元に、後でユーザーに新しいメッセージを送信できます。LIFFについて詳しくは、「[LIFFアプリを開発する](https://developers.line.biz/ja/docs/liff/developing-liff-apps/)」および「[LIFFスターターアプリを試してみる](https://developers.line.biz/ja/docs/liff/trying-liff-app/)」を参照してください。

次の手順で2つ目のボタンを追加します。

1. ツリービューエリアで、1つ目のボタンを作成した［**box [vertical]**］をクリックします。
1. ［**+**］をクリックし、ドロップダウンメニューから［**button**］を選択します。これでボタンが作成されます。
1. プロパティエリアで以下を設定します。
   - **style**プロパティを`link`に設定
   - **label**プロパティを「利用者登録する」に変更
   - **type**プロパティを`uri`のままにする
   - **uri**プロパティにLIFFアプリのURLを入力

これで、LIFFアプリを設定した2つ目のボタンができました。

![LIFFボタンを追加する](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/ja-add-liff-button.png)

### 7-3. ボタンの配置を調整する 

2つのボタンは、距離が近過ぎます。見た目はそうでもないのですが、ボタンのスタイルを`primary`や`secondary`に変更すると、よく分かります。間に余裕を持たせてボタンを配置する場合は、親要素であるボックスコンポーネントに[マージン](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#margin-property)または[パディング](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#padding-property)が使えます。このチュートリアルではパディングを追加します。

1. ツリービューで、作成した2つのボタンが含まれる［**box [vertical]**］を選択します。
1. プロパティエリアで、［**Padding**］の中の［**paddingTop**］を`10px`に設定します。

これでボタンの間のスペースが広がりました。

![ボタンにスタイルを追加する](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/ja-style-buttons.png)

以上で、デジタル名刺を作成するチュートリアルは完了です！

## 次のステップ 

Flex Messageを構築したら、「[作成したFlex MessageのJSONをコピーできます](https://developers.line.biz/ja/docs/messaging-api/using-flex-message-simulator/#copy-json)」の説明に従って、構築したFlex MessageのJSONデータをエクスポートできます。このJSONデータを利用することで、Messaging APIでFlex Messageをメッセージとして送信できます。詳しくは、「[Messaging APIで送信する](https://developers.line.biz/ja/docs/messaging-api/using-flex-messages/#sending-messages-with-the-messaging-api)」を参照してください。

## 最後に 

Flex Message Simulatorは、コードを記述せずに、Flex Messageのブレインストーミング、設計、プロトタイプ作成ができるツールです。このチュートリアルで示したように、Flex Messageの使用例は無限にあります。Flex Message Simulatorを使うと、技術的な障壁をなくして、気軽にアイディアを具体化したり、プロトタイプをテストしたりしてFlex Messageを素早く作れます。ぜひみなさん独自のFlex Messageを作ってみてください。

## 関連ページ 

- [Flex Messageを送信する](https://developers.line.biz/ja/docs/messaging-api/using-flex-messages/)
- [Flex Messageの要素](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/)
- [Flex Messageのレイアウト](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/)
- [Flex Message](https://developers.line.biz/ja/reference/messaging-api/#flex-message)（Messaging APIリファレンス）
