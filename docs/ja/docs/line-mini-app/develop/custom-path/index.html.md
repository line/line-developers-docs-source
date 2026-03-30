# Custom Pathを設定する

<!-- tip start -->

**認証済ミニアプリでのみ利用できます**

この機能は、認証済ミニアプリでのみ利用できます。

<!-- tip end -->

Custom Pathとは、本番用のLIFF URLに設定する独自の文字列のことをいいます。Custom Path機能を用いると、以下のように、LIFF URLに独自の文字列を設定できます。

| LIFF IDによるURLの例 | Custom Pathを設定した例 |
| --- | --- |
| `https://miniapp.line.me/123456-abcdefg` | `https://miniapp.line.me/cony_coffee` |

たとえば、ユニークな名前をCustom Pathとして設定することにより、ユーザーはURLからどのブランドや店舗のLINEミニアプリなのかがわかるようになります。なお、Custom Pathを設定した場合でも、LIFF IDによるURLも従来どおりアクセスできます。

## 申請方法 

LINEミニアプリでCustom Path機能を利用するには申請が必要です。申請方法は、サービスを提供する地域ごとに異なります。

- [サービスを提供する地域が日本の場合](https://developers.line.biz/ja/docs/line-mini-app/develop/custom-path/#area-is-japan)
- [サービスを提供する地域が台湾またはタイの場合](https://developers.line.biz/ja/docs/line-mini-app/develop/custom-path/#area-is-taiwan-or-thailand)

### サービスを提供する地域が日本の場合 

サービスを提供する地域が日本の場合、Custom Path機能を利用するには、以下のフォームより申請してください。複数のLINEミニアプリにおけるCustom Pathを一括で申請する方法も、以下のフォームに記載されています。

[申請フォーム](https://form-business.yahoo.co.jp/claris/enqueteForm?inquiry_type=lmini-custompath)

申請の受領確認や、審査結果はメールでご連絡します。なお、申請からCustom PathによるURLが利用できるようになるまで、1〜2週間ほどかかります。あらかじめご了承ください。

### サービスを提供する地域が台湾またはタイの場合 

サービスを提供する地域が台湾またはタイのお客様で、Custom Path機能をご利用になりたい場合は、担当営業までご連絡ください。

## Custom Pathを申請する際の注意事項 

Custom Pathが設定されても、[LINE Developersコンソール](https://developers.line.biz/console/)上では、Custom Pathが設定されたLIFF URLは表示されませんので注意してください。

Custom Pathは、LINEミニアプリの審査前にも申請できます。しかし、設定されるのはLINEミニアプリが審査に通過した後になります。

一度設定されたCustom Pathは、原則として変更できません。

### Custom Pathとして使用できる文字列 

Custom Pathを申請する際に記入する文字列には、以下の制約があります。これらの制約をふまえた上で文字列を記入してください。

- 4文字以上、29文字以内にしてください。
- 半角英数字（`a-z`、`0-9`）、アンダースコア（`_`）のみ使用できます。
- 最後の文字にアンダースコア（`_`）は使用できません。
- 数字のみにはできません。
- 空白は使用できません。
- ブランドやサービスを特定できる固有名詞を含めてください。
- LINEヤフー株式会社が提供するサービスと同じ文字列は使用できません。
- 他者によるものも含め、すでに利用されている文字列は使用できません。
- その他、当社が不適当であると判断した文字列は使用できません。
