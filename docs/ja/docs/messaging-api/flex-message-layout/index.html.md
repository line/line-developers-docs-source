# Flex Messageのレイアウト

Flex Messageでは、[CSS Flexible Box（CSS Flexbox）](https://www.w3.org/TR/css-flexbox-1/)の仕様に基づき、複雑なレイアウトのメッセージを構築できます。CSS FlexboxのFlexコンテナがFlex Messageの[ボックス](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/#box)に相当し、CSS FlexboxのFlexアイテムがFlex Messageのコンポーネントに相当します。

ここでは、Flex Messageのレイアウトを作成する方法を学びます。JSONスキーマについて詳しくは、『Messaging APIリファレンス』の「[Flex Message](https://developers.line.biz/ja/reference/messaging-api/#flex-message)」を参照してください。

## ボックスコンポーネントの向き 

[ボックスコンポーネント](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/#box)には、横向きと縦向きの2種類があります。横向きのボックスは水平ボックス、縦向きのボックスは垂直ボックスと呼ばれます。向きによって、ボックスの主軸と交差軸が決まります。主軸は向きに平行で、水平ボックスの主軸は水平、垂直ボックスの主軸は垂直です。交差軸は主軸に対し垂直です。主軸によって、ボックスの子コンポーネントの配置が決まります。詳しくは、「[余白を使った子コンポーネントの配置](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#justify-property)」を参照してください。

ボックスコンポーネントの向きを指定するには、`layout`プロパティを指定します。水平ボックスと垂直ボックスに加え、ベースラインボックスも利用できます。

| ボックス | `layout`プロパティ | 主軸 | 交差軸 | 子要素の配置 |
| --- | --- | --- | --- | --- |
| 水平ボックス | `horizontal` | 水平 | 垂直 | 水平 |
| 垂直ボックス | `vertical` | 垂直 | 水平 | 垂直 |
| ベースラインボックス | `baseline` | 水平 | 垂直 | 水平<br />詳しくは、「[ベースラインボックスの子コンポーネント](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#baseline-box)」を参照してください。 |

### ベースラインボックスの子コンポーネント 

ベースラインボックスは水平ボックスと同様に動作します。ただし、水平ボックスとは、以下の点で動作が異なります。

#### 垂直方向の揃え位置 

ベースラインボックス内のコンポーネントは、同じベースラインによって垂直方向に整列されます。つまり、フォントサイズに関係なく、すべての子コンポーネントのベースラインが同じになります。[アイコンコンポーネント](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/#icon)のベースラインはアイコン画像の底辺です。

![](https://developers.line.biz/media/messaging-api/flex-message-layout/baseline.png)

#### 使用できないプロパティ 

ベースラインボックスの子コンポーネントでは、`gravity`プロパティと`offsetBottom`プロパティは利用できません。

## 使用できる子コンポーネント 

ボックスの`layout`プロパティによって、子コンポーネントとして使用できるコンポーネントが異なります。

| &nbsp; | ベースラインボックス | 水平ボックス<br >垂直ボックス |
| --- | :-: | :-: |
| [ボックス](https://developers.line.biz/ja/reference/messaging-api/#box) | ❌ | ✅ |
| [ボタン](https://developers.line.biz/ja/reference/messaging-api/#button) | ❌ | ✅ |
| [画像](https://developers.line.biz/ja/reference/messaging-api/#f-image) | ❌ | ✅ |
| [アイコン](https://developers.line.biz/ja/reference/messaging-api/#icon) | ✅ | ❌ |
| [テキスト](https://developers.line.biz/ja/reference/messaging-api/#f-text) | ✅ | ✅ |
| [スパン](https://developers.line.biz/ja/reference/messaging-api/#span)<br />（テキストの子要素として使用できます） | ❌ | ❌ |
| [セパレータ](https://developers.line.biz/ja/reference/messaging-api/#separator) | ❌ | ✅ |
| [フィラー](https://developers.line.biz/ja/reference/messaging-api/#filler) (deprecated) | ✅ | ✅ |

✅：ボックス内で使用できる ❌：ボックス内で使用できない

## コンポーネントのサイズ 

コンポーネントの`position`プロパティが`relative`に設定されている場合、コンポーネントの幅と高さはコンポーネントの`flex`プロパティで決まります。

- [水平ボックス内の幅の分配](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#horizontal-box)
- [垂直ボックス内の高さの分配](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#vertical-box)
- [ボックスの幅](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#box-width)
- [ボックスの最大幅](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#box-max-width)
- [ボックスの高さ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#box-height)
- [ボックスの最大高](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#box-max-height)
- [画像のサイズ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#image-size)
- [アイコン、テキスト、スパンのサイズ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#other-component-size)
- [その他のコンポーネントのサイズ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#other-component)
- [フォントサイズの自動縮小](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#adjusts-fontsize-to-fit)
- [フォントサイズ設定に応じたサイズへの拡大縮小](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#size-scaling)

### 水平ボックス内の幅の分配 

水平ボックスでは、子コンポーネントの`flex`プロパティが`1`以上に設定されている場合、親ボックスの幅を兄弟コンポーネントと共有します。`flex`プロパティのデフォルト値は`1`です。それぞれの子コンポーネントが取得する幅の割合は、`flex`プロパティの値の合計に対する、子コンポーネントの`flex`プロパティの値で決まります。

たとえば、水平ボックスに2つのコンポーネントがあり、1つは`flex`プロパティが`2`に設定され、もう1つは`3`に設定されているとします。すると、利用可能な幅（水平ボックスの幅）は2:3の比率で分割され、各コンポーネントに割り当てられます。

![](https://developers.line.biz/media/messaging-api/flex-message-layout/flexSample1.png)

上のFlex Messageを表現するには以下のようなJSONデータを指定します。

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "horizontal",
    "contents": [
      {
        "type": "text",
        "text": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
        "wrap": true,
        "color": "#ff0000",
        "flex": 2
      },
      {
        "type": "text",
        "text": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
        "wrap": true,
        "color": "#0000ff",
        "flex": 3
      }
    ]
  }
}
```

コンポーネントの`flex`プロパティが`0`の場合、コンポーネントはボックスの幅のうち、コンポーネントの内容をすべて表示するのに必要な幅を取ります。ただし、ボックスの幅からはみ出した部分は表示されません。

たとえば、水平ボックスに3つの子コンポーネントがあり、それぞれの`flex`プロパティが`0`、`2`、`3`に設定されているとします。最初のコンポーネントは`flex`プロパティが`0`に設定されているため、テキスト「Hello」に合わせて幅を取ります。そして、利用可能な残りの幅は、下図のように、2:3の割合で残りの2つのコンポーネントに割り当てられます。

![](https://developers.line.biz/media/messaging-api/flex-message-layout/flexSample2.png)

上のFlex Messageを表現するには以下のようなJSONデータを指定します。

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "horizontal",
    "contents": [
      {
        "type": "text",
        "text": "Hello",
        "color": "#00ff00",
        "flex": 0
      },
      {
        "type": "text",
        "text": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
        "wrap": true,
        "color": "#ff0000",
        "flex": 2
      },
      {
        "type": "text",
        "text": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
        "wrap": true,
        "color": "#0000ff",
        "flex": 3
      }
    ]
  }
}
```

<!-- tip start -->

**flexプロパティとCSS Flexbox**

水平ボックス内の子コンポーネントの`flex`プロパティは、CSS Flexboxの`flex`プロパティと次のように対応しています。

| Flex Messageの子コンポーネントの`flex`プロパティの値 | 対応するCSS Flexboxのスタイル |
| :-: | --- |
| `0` | `flex: 0 0 auto;` |
| `0`以上 | `flex: X 0 0;`（Xは子コンポーネントの`flex`プロパティの値） |

<!-- tip end -->

### 垂直ボックス内の高さの分配 

垂直ボックスでは、子コンポーネントの`flex`プロパティが`1`以上に設定されている場合、親ボックスの高さを兄弟コンポーネントと共有します。`flex`プロパティのデフォルト値は`0`です。それぞれの子コンポーネントが取得する高さの割合は、`flex`プロパティの値の合計に対する、子コンポーネントの`flex`プロパティの値で決まります。

下の例では、水平ボックスに2つの垂直ボックスがあります。最初の垂直ボックスには5行を占めるテキストがあり、2番目の垂直ボックスには2つのテキストと3つのセパレータがあります。

![](https://developers.line.biz/media/messaging-api/flex-message-layout/flexSample5.png)

このとき、各コンポーネントは次のルールで配置されています。

1. 左側の垂直ボックスが5行分の高さがあるため、右側の垂直ボックスも同じ高さになります。
1. 右側の垂直ボックスの子コンポーネントは、高さ全体を占める必要がないため、余白ができます。
1. 2つのテキストの`flex`プロパティの値（`2`と`3`）をもとに、余白が2：3に分割され、各コンポーネントに割り当てられます。

上のFlex Messageを表現するには以下のようなJSONデータを指定します。

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "horizontal",
    "contents": [
      {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "text",
            "wrap": true,
            "text": "TEXT\nTEXT\nTEXT\nTEXT\nTEXT"
          }
        ],
        "backgroundColor": "#c0c0c0"
      },
      {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "separator",
            "color": "#ff0000"
          },
          {
            "type": "text",
            "text": "flex=2",
            "flex": 2
          },
          {
            "type": "separator",
            "color": "#ff0000"
          },
          {
            "type": "text",
            "text": "flex=3",
            "flex": 3
          },
          {
            "type": "separator",
            "color": "#ff0000"
          }
        ]
      }
    ]
  }
}
```

<!-- tip start -->

**CSS flexプロパティとCSS Flexbox**

垂直ボックス内の子コンポーネントの`flex`プロパティは、CSS Flexboxの`flex`プロパティと次のように対応しています。

| Flex Messageの子コンポーネントの`flex`プロパティの値 | 対応するCSS Flexboxのスタイル |
| :-: | --- |
| `0` | `flex: 0 0 auto;` |
| `0` or greater | `flex: X 0 auto;`（Xは子コンポーネントの`flex`プロパティの値） |

<!-- tip end -->

### ボックスの幅 

ボックスの幅は、`width`プロパティを使って、ピクセル単位、または親コンポーネントの幅に対するパーセンテージで指定できます。水平ボックス内の子ボックスの幅を指定した場合、子ボックスの`flex`プロパティは`0`に設定されます。

<!-- note start -->

**widthプロパティをピクセルで指定する場合**

バブルの幅は、デバイスの画面サイズに依存します。バブルの全体的なレイアウトを調整するために`width`プロパティをピクセルで指定すると、最終的に予期せぬレイアウトになることがあります。デバイスの画面サイズの影響を受けにくくするために、`flex`プロパティを使うことをお勧めします。

<!-- note end -->

### ボックスの最大幅 

ボックスの最大幅は、`maxWidth`プロパティを使って、ピクセル単位、または親コンポーネントの幅に対するパーセンテージで指定できます。`maxWidth`プロパティは`width`プロパティよりも優先されます。`width`プロパティから算出されるボックスの幅が、`maxWidth`プロパティから算出されるボックスの幅よりも大きい場合、ボックスの幅は`maxWidth`プロパティの値に設定されます。

### ボックスの高さ 

ボックスの高さは、`height`プロパティを使って、ピクセル単位、または親コンポーネントの高さに対するパーセンテージで指定できます。水平ボックスの子ボックスの高さを指定した場合、子ボックスの`flex`プロパティは`0`に設定されます。

### ボックスの最大高 

ボックスの最大高は、`maxHeight`プロパティを使って、ピクセル単位、または親コンポーネントの高さに対するパーセンテージで指定できます。`maxHeight`プロパティは`height`プロパティよりも優先されます。`height`プロパティから算出されるボックスの高さが、`maxHeight`プロパティから算出されるボックスの高さよりも大きい場合、ボックスの高さは`maxHeight`プロパティの値に設定されます。

### 画像のサイズ 

[画像コンポーネント](https://developers.line.biz/ja/reference/messaging-api/#f-image)の幅は、`size`プロパティを使って、ピクセル単位、パーセンテージ単位、またはキーワードで設定できます。高さはアスペクト比（`aspectRatio`プロパティで指定）を維持するように自動調整されます。

| 単位 | 許容される値 | 例 |
| --- | --- | --- |
| パーセンテージ | 元画像の幅に対する割合。正の整数または小数を`%`で指定します。 | `50%` `23.5%` |
| ピクセル | 正の整数または小数を`px`で指定します。 | `50px` `23.5px` |
| キーワード | `xxs`、`xs`、`sm`、`md`、`lg`、`xl`、`xxl`、`3xl`、`4xl`、`5xl`、`full`のいずれかの値を指定できます。列挙した順にサイズが大きくなります。 | `md`（デフォルト値） |

### アイコン、テキスト、スパンのサイズ 

[アイコン](https://developers.line.biz/ja/reference/messaging-api/#icon)、[テキスト](https://developers.line.biz/ja/reference/messaging-api/#f-text)、[スパン](https://developers.line.biz/ja/reference/messaging-api/#span)のコンポーネントのサイズは、`size`プロパティを使って、ピクセル単位、またはキーワードで指定できます。パーセンテージは指定できません。

| 単位 | 許容される値 | 例 |
| --- | --- | --- |
| ピクセル | 正の整数または小数を`px`で指定します。 | `50px` `23.5px` |
| キーワード | `xxs`、`xs`、`sm`、`md`、`lg`、`xl`、`xxl`、`3xl`、`4xl`、`5xl`のいずれかの値を指定できます。列挙した順にサイズが大きくなります。 | `md`（デフォルト値） |

### その他のコンポーネントのサイズ 

ボタンなどのコンポーネントでは、`flex`プロパティとは異なるプロパティでサイズを指定できます。JSONスキーマについて詳しくは、『Messaging APIリファレンス』の「[Flex Message](https://developers.line.biz/ja/reference/messaging-api/#flex-message)」を参照してください。

### フォントサイズの自動縮小 

[ボタン](https://developers.line.biz/ja/reference/messaging-api/#button)、[テキスト](https://developers.line.biz/ja/reference/messaging-api/#f-text)のコンポーネントでは、`adjustMode`プロパティで`shrink-to-fit`を指定すると、テキストのフォントサイズが自動縮小されます。`adjustMode`プロパティはベストエフォートで機能するため、プラットフォームによって動作が異なる、あるいは動作しない場合があります。

![](https://developers.line.biz/media/messaging-api/flex-message-layout/adjusts-fontsize-to-fit.png)

### フォントサイズ設定に応じたサイズへの拡大縮小 

Flex Messageの[ボタン](https://developers.line.biz/ja/reference/messaging-api/#button)、[テキスト](https://developers.line.biz/ja/reference/messaging-api/#f-text)、および[アイコン](https://developers.line.biz/ja/reference/messaging-api/#icon)の`scaling`プロパティに`true`を指定すると、LINEアプリのフォントサイズ設定に応じて、フォントサイズやアイコンのサイズが自動的に拡大縮小されます。`scaling`プロパティを`true`にすることで、アクセシビリティに配慮したメッセージを送ることができます。

| フォントサイズが［**小**］の場合 | フォントサイズが［**特大**］の場合 |
| --- | --- |
| ![](https://developers.line.biz/media/messaging-api/flex-message-layout/scaling-sample-small-ja.jpg) | ![](https://developers.line.biz/media/messaging-api/flex-message-layout/scaling-sample-extra-large-ja.jpg) |

上のFlex Messageを表現するには以下のようなJSONデータを指定します。

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "text",
        "text": "hello, world",
        "size": "30px"
      },
      {
        "type": "text",
        "text": "hello, world",
        "margin": "10px",
        "size": "30px",
        "scaling": true
      }
    ]
  }
}
```

<!-- tip start -->

**フォントサイズの自動縮小との併用**

ボタンおよびテキストでは、`scaling`プロパティに`true`を指定し、かつ`adjustMode`プロパティに`shrink-to-fit`を指定することができます。その場合、フォントサイズが自動的に拡大縮小された結果、テキストの幅がコンポーネントの幅を超えたとき、フォントサイズはコンポーネントの幅に合わせて縮小されます。

以下は、LINEアプリのフォントサイズが［**特大**］の場合の例です。

| | |
| --- | --- |
| ![](https://developers.line.biz/media/messaging-api/flex-message-layout/scaling-sample-small-tip.png) | <ol><li>デフォルトの場合</li><li>`scaling`プロパティに`true`を指定した場合</li><li>`scaling`プロパティに`true`を指定し、`adjustMode`プロパティに`shrink-to-fit`を指定した場合</li></ol> |

<!-- tip end -->

## コンポーネントの位置 

子コンポーネントがあるボックスに余白がある場合、各コンポーネントを[水平](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#align-property)または[垂直](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#gravity-property)に整列できます。

子コンポーネントを配置するには、親コンポーネントの[パディング](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#padding-property)または子コンポーネントの[`margin`プロパティ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#margin-property)を使用します。子コンポーネントを[主軸](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#justify-content)上に配置することも、[交差軸](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#align-items)上に配置することもできます。[オフセット](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#component-offset)は、子コンポーネントを配置するために使用できるもう1つの選択肢です。

### テキストや画像を水平方向に整列させる 

[テキスト](https://developers.line.biz/ja/reference/messaging-api/#f-text)や[画像](https://developers.line.biz/ja/reference/messaging-api/#f-image)のコンポーネントを水平方向に整列させるには、`align`プロパティを使用します。`align`プロパティは親コンポーネントの向きの影響を受けません。利用可能な整列オプションは以下のとおりです。

- 左揃え：`start`
- 右揃え：`end`
- 中央揃え：`center`（デフォルト値）

![](https://developers.line.biz/media/messaging-api/flex-message-layout/alignSample.png)

上のFlex Messageを表現するには以下のようなJSONデータを指定します。

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "text",
        "text": "align=start",
        "align": "start"
      },
      {
        "type": "separator",
        "color": "#ff0000"
      },
      {
        "type": "text",
        "text": "align=center",
        "align": "center"
      },
      {
        "type": "separator",
        "color": "#ff0000"
      },
      {
        "type": "text",
        "text": "align=end",
        "align": "end"
      }
    ]
  }
}
```

### テキスト、画像、ボタンを垂直方向に整列させる 

[テキスト](https://developers.line.biz/ja/reference/messaging-api/#f-text)、[画像](https://developers.line.biz/ja/reference/messaging-api/#f-image)、または[ボタン](https://developers.line.biz/ja/reference/messaging-api/#button)のコンポーネントを垂直方向に整列させるには、`gravity`プロパティを使用します。`gravity`プロパティは親コンポーネントの向きの影響を受けません。利用可能な整列オプションは以下のとおりです。

- 上揃え：`top`（デフォルト値）
- 下揃え：`bottom`
- 中央揃え：`center`

<!-- note start -->

**注意**

[ベースラインボックス](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#baseline-box)の子要素ではこの設定は無視されます。

<!-- note end -->

![](https://developers.line.biz/media/messaging-api/flex-message-layout/gravitySample.png)

上のFlex Messageを表現するには以下のようなJSONデータを指定します。

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "horizontal",
    "contents": [
      {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "text",
            "wrap": true,
            "text": "TEXT\nTEXT\nTEXT\nTEXT\nTEXT"
          }
        ],
        "backgroundColor": "#c0c0c0"
      },
      {
        "type": "text",
        "text": "top",
        "gravity": "top"
      },
      {
        "type": "separator",
        "color": "#ff0000"
      },
      {
        "type": "text",
        "text": "center",
        "gravity": "center"
      },
      {
        "type": "separator",
        "color": "#ff0000"
      },
      {
        "type": "text",
        "text": "bottom",
        "gravity": "bottom"
      },
      {
        "type": "separator",
        "color": "#ff0000"
      }
    ]
  }
}
```

### ボックスのパディングで子コンポーネントを配置する 

子コンポーネントをボックスコンポーネントの中に配置するには、ボックスコンポーネントのパディングを使用します。パディングは、親コンポーネントのボーダーと子コンポーネントの間にスペースを割り当てます。利用可能なパディングのプロパティは`paddingAll`、`paddingTop`、`paddingStart`、`paddingEnd`です。パディングはピクセル単位、パーセンテージ単位（親ボックスの幅に対する）、またはキーワードで指定できます。

| 単位 | 許容可能な値 | 例 |
| --- | --- | --- |
| パーセンテージ | 親ボックスの幅に対する割合。正の整数または小数を`%`で指定します。 | `50%` `23.5%` |
| ピクセル | 正の整数または小数を`px`で指定します。 | `50px` `23.5px` |
| キーワード | `none`（パディングなし）, `xs`, `sm`, `md`, `lg`, `xl`, `xxl`のいずれかの値を指定できます。列挙した順にサイズが大きくなります。 | `md`（デフォルト値） |

`paddingTop`、`paddingBottom`、`paddingStart`、`paddingEnd`の各プロパティは、`paddingAll`プロパティよりも優先されます。`paddingTop`、`paddingBottom`、`paddingStart`、`paddingEnd`が指定されている場合、`paddingAll`プロパティは無視されます。

![](https://developers.line.biz/media/messaging-api/flex-message-layout/paddingSample.png)

上のFlex Messageを表現するには以下のようなJSONデータを指定します。

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "horizontal",
    "contents": [
      {
        "type": "box",
        "layout": "horizontal",
        "contents": [
          {
            "type": "text",
            "text": "hello, world"
          }
        ],
        "backgroundColor": "#ffffff"
      }
    ],
    "backgroundColor": "#ffd2d2",
    "paddingTop": "20px",
    "paddingAll": "80px",
    "paddingStart": "40px"
  }
}
```

なお、上のFlex Messageのテキストを長くすると、以下のようにレイアウトされます。

![](https://developers.line.biz/media/messaging-api/flex-message-layout/paddingSample2.png)

### 余白を使った子コンポーネントの配置 

[ボックス](https://developers.line.biz/ja/reference/messaging-api/#box)の余白を使って、子コンポーネントを軸に沿って配置できます。ここでは[主軸](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#justify-content)と[交差軸](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#align-items)に沿ってコンポーネントを配置する方法を学びます。

<!-- tip start -->

**親ボックスコンポーネントによって主軸と交差軸が変わります**

`justifyContent`プロパティと`alignItems`プロパティは、それぞれ主軸と交差軸に沿った子コンポーネントの配置を設定します。親ボックスコンポーネントによって、主軸と交差軸の向きは変わります。

![](https://developers.line.biz/media/messaging-api/flex-message-layout/horizontal_vertical_axis.png)

書字方向（`LTR`または`RTL`）は、親ボックスコンポーネントの向きに関係なく、常に水平方向に適用されます。

<!-- tip end -->

#### 主軸に沿って子コンポーネントを配置する 

ボックスの子コンポーネントを主軸に沿って配置するには、`justifyContent`プロパティを使用します。主軸の向きは水平ボックスでは水平、垂直ボックスでは垂直です。このプロパティを有効にするには、すべての子コンポーネントの`flex`プロパティが`0`である必要があります。なぜなら、子コンポーネントのうち、1つでも`flex`プロパティが`1`以上であれば、子コンポーネントは親ボックスいっぱいに広がり、子コンポーネントを配置するスペースがなくなるためです。デフォルトでは、水平ボックスの子コンポーネントは`flex`プロパティが`1`になるため注意してください。

`justifyContent`プロパティの値によって、書字方向がLTRの水平ボックスの子コンポーネントがどのように配置されるか見てみましょう。

![](https://developers.line.biz/media/messaging-api/flex-message-layout/justify-content-01.svg)
![](https://developers.line.biz/media/messaging-api/flex-message-layout/justify-content-02.svg)
![](https://developers.line.biz/media/messaging-api/flex-message-layout/justify-content-03.svg)
![](https://developers.line.biz/media/messaging-api/flex-message-layout/justify-content-04.svg)
![](https://developers.line.biz/media/messaging-api/flex-message-layout/justify-content-05.svg)
![](https://developers.line.biz/media/messaging-api/flex-message-layout/justify-content-06.svg)

| プロパティの値 | 子コンポーネントの配置 |
| --- | --- |
| `flex-start` | 水平ボックス：親コンポーネントの書字方向の始まる側に寄せます。<br />垂直ボックス：親コンポーネントの上側に寄せます。 |
| `center` | 親コンポーネントの中心にまとめて配置します。 |
| `flex-end` | 水平ボックス：親コンポーネントの書字方向の終わり側に寄せます。<br />垂直ボックス：親コンポーネントの下側に寄せます。 |
| `space-between` | 親コンポーネントに均等に配置します。最初と最後の子コンポーネントは親コンポーネントの両端に配置します。子コンポーネント間の余白は均等です。 |
| `space-around` | 親コンポーネントに均等に配置します。親コンポーネントの余白は2×子コンポーネントの数で分割されます。それぞれの子コンポーネントの左右に分割された余白が配置されます。 |
| `space-evenly` | 親コンポーネントに均等に配置します。親コンポーネントの余白はそれぞれの子コンポーネントの左右に均等に配置されます。 |

たとえば上記の`flex-start`のFlex Messageを表現するには、以下のようなJSONデータを指定します。

```json
{
  "type": "bubble",
  "direction": "ltr",
  "body": {
    "type": "box",
    "layout": "horizontal",
    "contents": [
      {
        "type": "box",
        "layout": "vertical",
        "contents": [],
        "width": "40px",
        "height": "30px",
        "backgroundColor": "#00aaff",
        "flex": 0
      },
      {
        "type": "box",
        "layout": "vertical",
        "contents": [],
        "width": "20px",
        "height": "30px",
        "backgroundColor": "#00aaff",
        "flex": 0
      },
      {
        "type": "box",
        "layout": "vertical",
        "contents": [],
        "height": "30px",
        "width": "50px",
        "backgroundColor": "#00aaff",
        "flex": 0
      }
    ],
    "justifyContent": "flex-start",
    "spacing": "5px"
  }
}
```

#### 交差軸に沿って子コンポーネントを配置する 

ボックスの子コンポーネントを交差軸に沿って配置するには、`alignItems`プロパティを使用します。交差軸の向きは水平ボックスでは垂直、垂直ボックスでは水平です。

`alignItems`プロパティの値によって、書字方向がLTRの水平ボックスの子コンポーネントがどのように配置されるか見てみましょう。

![](https://developers.line.biz/media/messaging-api/flex-message-layout/alignItems-01.svg)
![](https://developers.line.biz/media/messaging-api/flex-message-layout/alignItems-02.svg)
![](https://developers.line.biz/media/messaging-api/flex-message-layout/alignItems-03.svg)

| プロパティの値 | 子コンポーネントの配置 |
| --- | --- |
| `flex-start` | 水平ボックス：親コンポーネントの上側に寄せます。<br />垂直ボックス：親コンポーネントの書字方向の始まる側に寄せます。 |
| `center` | 親コンポーネントの中心にまとめて配置します。 |
| `flex-end` | 水平ボックス：親コンポーネントの下側に寄せます。<br />垂直ボックス：親コンポーネントの書字方向の終わり側に寄せます。 |

たとえば上記の`flex-start`のFlex Messageを表現するには、以下のようなJSONデータを指定します。

```json
{
  "type": "bubble",
  "direction": "ltr",
  "body": {
    "type": "box",
    "layout": "horizontal",
    "contents": [
      {
        "type": "box",
        "layout": "vertical",
        "contents": [],
        "height": "100px",
        "backgroundColor": "#00aaff",
        "flex": 0,
        "width": "85px"
      },
      {
        "type": "box",
        "layout": "vertical",
        "contents": [],
        "height": "30px",
        "backgroundColor": "#00aaff",
        "flex": 0,
        "width": "85px"
      },
      {
        "type": "box",
        "layout": "vertical",
        "contents": [],
        "height": "60px",
        "backgroundColor": "#00aaff",
        "flex": 0,
        "width": "85px"
      }
    ],
    "spacing": "5px",
    "alignItems": "flex-start",
    "height": "200px"
  }
}
```

### ボックスの`spacing`プロパティ 

コンポーネント間の最小スペースは、親ボックスコンポーネントの`spacing`プロパティを使って、ピクセル単位、またはキーワードで指定できます。パーセンテージは指定できません。

| 単位 | 許容される値 | 例 |
| --- | --- | --- |
| ピクセル | 正の整数または小数を`px`で指定します。 | `50px` `23.5px` |
| キーワード | `none`（スペースなし）、 `xs`、 `sm`、 `md`、 `lg`、 `xl`、 `xxl`のいずれかの値を指定できます。列挙した順にサイズが大きくなります。 | `md` |

以下のFlex Messageには、水平ボックスに3つの垂直ボックスが等間隔（`md`）で配置されています。

![](https://developers.line.biz/media/messaging-api/flex-message-layout/spacingSample.png)

上のFlex Messageを表現するには以下のようなJSONデータを指定します。

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "horizontal",
    "spacing": "md",
    "contents": [
      {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "text",
            "text": "TEXT1"
          }
        ],
        "backgroundColor": "#80ffff"
      },
      {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "text",
            "text": "TEXT2"
          }
        ],
        "backgroundColor": "#80ffff"
      },
      {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "text",
            "text": "TEXT3"
          }
        ],
        "backgroundColor": "#80ffff"
      }
    ]
  }
}
```

特定のコンポーネントについてこの設定を上書きするには、そのコンポーネントで`margin`プロパティを設定します。

### コンポーネントの`margin`プロパティ 

ある子コンポーネントの前に挿入する最小スペースは、子コンポーネントの`margin`プロパティを使って、ピクセル単位、またはキーワードで指定できます。パーセンテージは指定できません。

| 単位 | 許容される値 | 例 |
| --- | --- | --- |
| ピクセル | 正の整数または小数を`px`で指定します。 | `50px` `23.5px` |
| キーワード | `none`（スペースなし）、 `xs`、 `sm`、 `md`、 `lg`、 `xl`、 `xxl`のいずれかの値を指定できます。列挙した順にサイズが大きくなります。 | `md` |

`margin`プロパティは、親ボックスの[`spacing`プロパティ](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#spacing-property)よりも優先されます。また、ボックスの最初の子コンポーネントに`margin`プロパティが指定されている場合、コンポーネントの前にスペースが入ります。

以下のFlex Messageの例では、子コンポーネントとして、3つの垂直ボックスが水平ボックスに配置されています。親である水平ボックスには`spacing`プロパティが`md`に設定され、3番目の垂直ボックスには`margin`プロパティが`xxl`に設定されています。

![](https://developers.line.biz/media/messaging-api/flex-message-layout/marginSample.png)

上のFlex Messageを表現するには以下のようなJSONデータを指定します。

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "horizontal",
    "spacing": "md",
    "contents": [
      {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "text",
            "text": "TEXT1"
          }
        ],
        "backgroundColor": "#80ffff"
      },
      {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "text",
            "text": "TEXT2"
          }
        ],
        "backgroundColor": "#80ffff"
      },
      {
        "type": "box",
        "layout": "vertical",
        "contents": [
          {
            "type": "text",
            "text": "TEXT3"
          }
        ],
        "backgroundColor": "#80ffff",
        "margin": "xxl"
      }
    ]
  }
}
```

### オフセット 

コンポーネントを配置する別の選択肢として、オフセットを使用する方法があります。オフセットのプロパティは、親コンポーネントの`position`プロパティの値、`relative`と`absolute`によって動作が異なります。ただし、[ブロック](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/#block)の最初の子コンポーネントは`absolute`にすることはできません。

使用できるオフセットのプロパティは`offsetTop`、`offsetBottom`、`offsetStart`、`offsetEnd`です。プロパティの値はピクセル、またはキーワード（`one`、`xs`、`sm`、`md`、`lg`、`xl`、`xxl`）で指定できます。また、`offsetStart`と`offsetEnd`にはボックスの幅に対するパーセンテージを、`offsetTop`と`offsetBottom`にはボックスの高さに対するパーセンテージを指定することもできます。

以下の「TARGET」と表示されているボックスの位置が、オフセットによってどのように変わるかを見ていきましょう。

![](https://developers.line.biz/media/messaging-api/flex-message-layout/offsetSample1.png)

上のFlex Messageを表現するには以下のようなJSONデータを指定します。

```json
{
  "type": "bubble",
  "direction": "ltr",
  "body": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "box",
        "layout": "horizontal",
        "contents": [
          {
            "type": "text",
            "text": "REFERENCE BOX\n1\n2\n3",
            "align": "center",
            "wrap": true
          }
        ],
        "backgroundColor": "#80ffff"
      },
      {
        "type": "box",
        "layout": "horizontal",
        "contents": [
          {
            "type": "text",
            "text": "TARGET"
          }
        ],
        "backgroundColor": "#ff8080"
      }
    ]
  }
}
```

#### 相対位置の場合のオフセット 

コンポーネントを通常の位置を基準に配置するには、`position`プロパティを`relative`に設定します。詳しくは、CSS Positioned Layout Module Level 3の「[Relative positioning](https://www.w3.org/TR/css-position-3/#relpos-insets)」を参照してください。

| プロパティ | 説明 |
| --- | --- |
| `offsetTop` | コンポーネントを通常の位置の上端から下に動かします。 |
| `offsetBottom` | コンポーネントを通常の位置の下端から上に動かします。 |
| `offsetStart` | コンポーネントをテキストの始まる側から動かします。[バブル](https://developers.line.biz/ja/reference/messaging-api/#bubble)の書字方向がLTRの場合、右に動かします。RTLの場合、左に動かします。 |
| `offsetEnd` | コンポーネントをテキストの終わる側から動かします。[バブル](https://developers.line.biz/ja/reference/messaging-api/#bubble)の書字方向がLTRの場合、左に動かします。RTLの場合、右に動かします。 |

「TARGET」と表示されているコンポーネントの通常の位置が1枚目の画像です。`position`プロパティとオフセットプロパティを使って位置を動かしたのが2枚目の画像です。

![](https://developers.line.biz/media/messaging-api/flex-message-layout/offsetSample1.png)
![](https://developers.line.biz/media/messaging-api/flex-message-layout/offsetSample2.png)

コンポーネントを例のように動かすには、プロパティを以下のように設定します。

| プロパティ     | 値         |
| -------------- | ---------- |
| `position`     | `relative` |
| `offsetTop`    | `10px`     |
| `offsetBottom` | -          |
| `offsetStart`  | `40px`     |
| `offsetEnd`    | -          |

例のFlex Messageを表現するには以下のようなJSONデータを指定します。

```json
{
  "type": "bubble",
  "direction": "ltr",
  "body": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "box",
        "layout": "horizontal",
        "contents": [
          {
            "type": "text",
            "text": "REFERENCE BOX\n1\n2\n3",
            "align": "center",
            "wrap": true
          }
        ],
        "backgroundColor": "#80ffff"
      },
      {
        "type": "box",
        "layout": "horizontal",
        "contents": [
          {
            "type": "text",
            "text": "TARGET"
          }
        ],
        "backgroundColor": "#ff8080",
        "offsetTop": "10px",
        "offsetStart": "40px",
        "position": "relative"
      }
    ]
  }
}
```

#### 絶対位置の場合のオフセット 

親コンポーネントの外枠を基準に配置するには、`position`プロパティを`absolute`に設定します。詳しくは、CSS Positioned Layout Module Level 3の「[Absolute positioning](https://www.w3.org/TR/css-position-3/#abs-pos)」を参照してください。

<table>
  <thead>
    <tr>
      <th>プロパティ</th>
      <th colspan="2">説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>offsetTop</code></td>
      <td colspan="2">親要素の上端からコンポーネントの上端までの相対位置を指定します。</td>
    </tr>
    <tr>
      <td><code>offsetBottom</code></td>
      <td colspan="2">親要素の下端からコンポーネントの下端までの相対位置を指定します。</td>
    </tr>
    <tr>
      <td rowspan="2"><code>offsetStart</code></td>
      <td><a href="https://developers.line.biz/ja/reference/messaging-api/#bubble">バブル</a>の書字方向がLTRの場合</td>
      <td>親要素の左端からコンポーネントの左端までの相対位置を指定します。</td>
    </tr>
    <tr>
      <td><a href="https://developers.line.biz/ja/reference/messaging-api/#bubble">バブル</a>の書字方向がRTLの場合</td>
      <td>親要素の右端からコンポーネントの右端までの相対位置を指定します。</td>
    </tr>
    <tr>
      <td rowspan="2"><code>offsetEnd</code></td>
      <td><a href="https://developers.line.biz/ja/reference/messaging-api/#bubble">バブル</a>の書字方向がLTRの場合</td>
      <td>親要素の右端からコンポーネントの右端までの相対位置を指定します。</td>
    </tr>
    <tr>
      <td><a href="https://developers.line.biz/ja/reference/messaging-api/#bubble">バブル</a>の書字方向がRTLの場合</td>
      <td>親要素の左端からコンポーネントの左端までの相対位置を指定します。</td>
    </tr>
  </tbody>
</table>

<!-- note start -->

**注意**

オフセットプロパティを指定しない場合のコンポーネントの位置は、端末によって異なる可能性があります。そのため、縦方向（`offsetTop`または`offsetBottom`）および横方向（`offsetStart`または`offsetEnd`）のオフセットプロパティを明示的に指定することを推奨します。

<!-- note end -->

「TARGET」と表示されているコンポーネントの通常の位置が1枚目の画像です。`position`プロパティとオフセットプロパティを使って位置を動かしたのが2枚目の画像です。

![](https://developers.line.biz/media/messaging-api/flex-message-layout/offsetSample1.png)
![](https://developers.line.biz/media/messaging-api/flex-message-layout/offsetSample3.png)

コンポーネントを例のように動かすには、プロパティを以下のように設定します。

| プロパティ     | 値         |
| -------------- | ---------- |
| `position`     | `absolute` |
| `offsetTop`    | `10px`     |
| `offsetBottom` | `20px`     |
| `offsetStart`  | `40px`     |
| `offsetEnd`    | `80px`     |

例のFlex Messageを表現するには以下のようなJSONデータを指定します。

```json
{
  "type": "bubble",
  "direction": "ltr",
  "body": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "box",
        "layout": "horizontal",
        "contents": [
          {
            "type": "text",
            "text": "REFERENCE BOX\n1\n2\n3",
            "align": "center",
            "wrap": true
          }
        ],
        "backgroundColor": "#80ffff"
      },
      {
        "type": "box",
        "layout": "horizontal",
        "contents": [
          {
            "type": "text",
            "text": "TARGET"
          }
        ],
        "backgroundColor": "#ff8080",
        "position": "absolute",
        "offsetStart": "40px",
        "offsetEnd": "80px",
        "offsetTop": "10px",
        "offsetBottom": "20px"
      }
    ]
  }
}
```

##### 絶対位置の子コンポーネントと親コンポーネントのサイズ 

`position`プロパティが`absolute`に設定された子ボックスコンポーネントは、親コンポーネントの大きさに影響をを与えなくなり、さらに親コンポーネントの影響を受けなくなります。コンポーネントが親コンポーネントよりも大きい場合、親コンポーネントの外側にはみ出た部分は表示されません。

絶対位置と相対位置の効果を比べてみましょう。最初の画像にある水平ボックス「REFERENCE BOX」コンポーネントは、相対位置に設定されています。同じコンポーネントを絶対位置に設定したものが2番目の画像です。

![](https://developers.line.biz/media/messaging-api/flex-message-layout/offsetSample1.png)
![](https://developers.line.biz/media/messaging-api/flex-message-layout/offsetSample4.png)

2番目の画像の例でわかるように、「REFERENCE BOX」の大きさは、親コンポーネント（垂直ボックス）の大きさに影響を与えなくなり、さらに親コンポーネントの影響を受けなくなります。そのため、親コンポーネントよりも大きい部分（「2」と「3」の行）は表示されていません。また、親コンポーネント（余白）の影響で大きくなっていた左右の余白部分は、元の大きさ（テキスト「REFERENCE BOX」の幅）に戻ります。

## 線形グラデーション背景 

[ボックスコンポーネント](https://developers.line.biz/ja/reference/messaging-api/#box)では、`background.type`プロパティに`linearGradient`を指定することで、背景に線形グラデーションを設定できます。ここでは、グラデーションの[角度](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#linear-gradient-bg-angle)と[中間色](https://developers.line.biz/ja/docs/messaging-api/flex-message-layout/#linear-gradient-bg-center-color)の設定方法を学びます。

<!-- note start -->

**グラデーションの方向は親の書字方向に影響されません**

グラデーションの方向は、親要素の書字方向（`LTR`または`RTL`）の影響を受けません。

<!-- note end -->

### 線形グラデーションの角度 

線形グラデーションの角度は、0度から360度未満の整数または少数で指定できます。角度を90度にするには`90deg`、23.5度にするには`23.5deg`を指定します。角度によって、グラデーションの方向が変わります。

- 0度：下から上
- 45度：左下から右上
- 90度：左から右
- 180度：上から下

角度が大きくなるにつれて、方向は時計回りに回転します。

**0度の線形グラデーション（下から上）**

![](https://developers.line.biz/media/messaging-api/flex-message-layout/linear-gradient-bg-deg-0.png)

上のFlex Messageを表現するには以下のようなJSONデータを指定します。

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "vertical",
    "contents": [],
    "background": {
      "type": "linearGradient",
      "angle": "0deg",
      "startColor": "#ff0000",
      "endColor": "#0000ff"
    },
    "height": "200px"
  }
}
```

**45度の線形グラデーション（左下から右上）**

![](https://developers.line.biz/media/messaging-api/flex-message-layout/linear-gradient-bg-deg-45.png)

**90度の線形グラデーション（左から右）**

![](https://developers.line.biz/media/messaging-api/flex-message-layout/linear-gradient-bg-deg-90.png)

**180度の線形グラデーション（上から下）**

![](https://developers.line.biz/media/messaging-api/flex-message-layout/linear-gradient-bg-deg-180.png)

詳しくは、『Messaging APIリファレンス』の「[ボックス](https://developers.line.biz/ja/reference/messaging-api/#box)」を参照してください。

### グラデーションの中間色 

グラデーションに中間色を追加する、つまり、グラデーションを3色にするには、`centerColor`プロパティを指定します。`centerPosition`プロパティで中間色の位置を指定できます。

**開始点から10%の位置に中間色を置いた場合**

![開始点から10%の位置に中間色を置いた3色のグラデーション](https://developers.line.biz/media/messaging-api/flex-message-layout/linear-gradient-bg-percent-10.png)

上のFlex Messageを表現するには以下のようなJSONデータを指定します。

```json
{
  "type": "bubble",
  "body": {
    "type": "box",
    "layout": "vertical",
    "contents": [],
    "background": {
      "type": "linearGradient",
      "angle": "0deg",
      "startColor": "#ff0000",
      "centerColor": "#0000ff",
      "endColor": "#00ff00",
      "centerPosition": "10%"
    },
    "height": "200px"
  }
}
```

**開始点から50%の位置に中間色を置いた場合**

![開始点から50%の位置に中間色を置いた3色のグラデーション](https://developers.line.biz/media/messaging-api/flex-message-layout/linear-gradient-bg-percent-50.png)

**開始点から90%の位置に中間色を置いた場合**

![開始点から90%の位置に中間色を置いた3色のグラデーション](https://developers.line.biz/media/messaging-api/flex-message-layout/linear-gradient-bg-percent-90.png)

## 描画順序 

コンポーネントは、JSONで指定された順序で描画されます。JSON定義の最初のコンポーネントが最初に描画されます。そして、次のコンポーネントが最初のコンポーネントの上に描画されます。つまり、最後のコンポーネントはバブルの最前面に描画されます。

描画順序を変更するには、JSON定義のコンポーネントの順序を変更してください。

## 関連ページ 

- [Flex Messageを送信する](https://developers.line.biz/ja/docs/messaging-api/using-flex-messages/)
- [Flex Messageの要素](https://developers.line.biz/ja/docs/messaging-api/flex-message-elements/)
- [Flex Message](https://developers.line.biz/ja/reference/messaging-api/#flex-message)（Messaging APIリファレンス）
