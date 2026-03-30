# パーマネントリンクを作成する

ユーザーがLINEミニアプリにアクセスするために、LIFF URLだけでなく、パーマネントリンクも使用できます。ただし、LINEミニアプリのページをシェアするときは、LIFF URLではなく、パーマネントリンクを使用してください。

[ヘッダー](https://developers.line.biz/ja/docs/line-mini-app/discover/ui-components/#header)に表示されるアクションボタンから、LINEミニアプリのページをシェアした場合は、自動的にそのページのパーマネントリンクが作成されます。

それ以外の状況では、以下の計算式に従ってパーマネントリンクを作成してください。

`LIFF URL + (LINEミニアプリページのURL - エンドポイントURL) = パーマネントリンク`

例：

| 項目                      | 設定                                           |
| ------------------------- | ---------------------------------------------- |
| LIFF URL（※）             | `https://miniapp.line.me/123456-abcedfg`       |
| LINEミニアプリページのURL | `https://example.com/shop?search=shoes#item10` |
| エンドポイントURL（※）    | `https://example.com`                          |

※[LINE Developersコンソール](https://developers.line.biz/console/)の［**ウェブアプリ設定**］タブで確認できます。

この場合、LINEミニアプリページのURLに対応するパーマネントリンクは、以下のとおりです。

```
https://miniapp.line.me/123456-abcedfg/shop?search=shoes#item10
```

<!-- tip start -->

**ヒント**

LINEミニアプリページのURLには、ページパス、クエリパラメータおよびフラグメントを使用できます。

<!-- tip end -->

<!-- note start -->

**LINEミニアプリのLIFF URLが変更されました**

[2023年12月13日](https://developers.line.biz/ja/news/2023/12/13/change-of-liff-url-for-line-mini-app/)より、LINEミニアプリのLIFF URLが`https://miniapp.line.me/{liffId}`に変更されました。

従来の`https://liff.line.me/{liffId}`にアクセスした場合も、引き続き当該のLINEミニアプリが開きます。そのため、発行済みのQRコードも引き続き利用可能です。

<!-- note end -->

## LINEアプリのバージョンによるドメイン名の違い 

ヘッダーに表示される[アクションボタン](https://developers.line.biz/ja/docs/line-mini-app/discover/builtin-features/#action-button)からLINEミニアプリをシェアする場合、LINEアプリのバージョンによって作成されるパーマネントリンクのドメイン名が異なります。

| LINEアプリのバージョン | 作成されるURLの例                  |
| ---------------------- | ---------------------------------- |
| 13.20以降              | `https://miniapp.line.me/{liffId}` |
| 13.20未満              | `https://liff.line.me/{liffId}`    |

## LINEをインストールしていない場合の動作 

ユーザーがLINEをインストールしている場合は、ユーザーがパーマネントリンクをクリックすると、LINEが自動的に起動してLINEミニアプリのページが表示されます。ユーザーがLINEをインストールしていない場合は、ウェブブラウザが開き、LINEでLINEミニアプリを開くように案内されます。この案内からは、ウェブブラウザ上でLIFFのエンドポイントURLのページを開くこともできます。
