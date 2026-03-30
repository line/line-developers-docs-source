# LINEミニアプリのセーフエリア

ノッチがある端末でもLINEミニアプリのすべてを表示するために、CSSを使ってLINEミニアプリをセーフエリアに収めることを推奨します。
LINEミニアプリでは、ノーマルモードとランドスケープモードの両方をサポートします。ノーマルモードとランドスケープモードでは、必要なセーフエリアが異なります。

具体的には、LINEミニアプリのページのpaddingを、以下のように設定します。

<!-- table of contents -->

## ノーマルモードの場合 

- 下：34px

paddingの例：
```
{
  padding-bottom: 34px;
}
```

![](https://developers.line.biz/media/line-mini-app/mini_design_safearea_normal.png)

## ランドスケープモードの場合 

- 左右：44px
- 下：21px

paddingの例：
```
{
  padding-right: 44px;
  padding-bottom: 21px;
  padding-left: 44px;
}
```

![](https://developers.line.biz/media/line-mini-app/mini_design_safearea_landscape.png)
