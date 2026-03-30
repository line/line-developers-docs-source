# LINEミニアプリの仕様

LINEミニアプリの開発に関する仕様を説明します。

<!-- table of contents -->

## HTML5サポート 

LINEミニアプリを開発する場合は、[HTML5](https://html.spec.whatwg.org/)のほとんどの仕様を使用できます。たとえば、[Geolocation API](https://www.w3.org/TR/geolocation/)を使用して、ユーザーの位置情報を取得し、近くの店舗の情報をユーザーに提供できます。Google Maps APIなど、HTML5と互換性のあるほとんどのMap APIも使用できます。

![](https://developers.line.biz/media/line-mini-app/mini_map_api.png)

### 対応メディア形式 

HTML5でサポートされているメディア形式は、LINEミニアプリでサポートされています。以下のHTML5の仕様を参照してください。

- [img 要素](https://html.spec.whatwg.org/multipage/embedded-content.html#the-img-element)
- [Media 要素](https://html.spec.whatwg.org/multipage/media.html)

### ブラウザにおけるHTML5のサポート状況 

外部ブラウザにおけるHTML5のサポート状況を調べるには、以下のサイトが便利です。

- [https://caniuse.com](https://caniuse.com/)

## 対応プラットフォームとバージョン 

LINEミニアプリは、[LIFF](https://developers.line.biz/ja/docs/liff/overview/)を使用して開発します。そのため、LINEミニアプリの対応するOSバージョンとLINEバージョンは、LIFFの[推奨環境](https://developers.line.biz/ja/docs/liff/overview/#operating-environment)に準拠しています。

<!-- note start -->

**注意**

サポートされているバージョンは、予告なしに変更される場合があります。

<!-- note end -->

### 外部ブラウザでLINEミニアプリを開く場合 

<!-- tip start -->

**2025年10月1日より外部ブラウザでLINEミニアプリを利用できるようになりました**

外部ブラウザでLINEミニアプリを開いた場合に、表示される画面が変更されました。詳しくは、2025年9月26日のニュース、「[LINEミニアプリにおいて、2025年10月1日よりすべてのユーザーがウェブブラウザでサービスを利用できるようになります](https://developers.line.biz/ja/news/2025/09/26/mini-app-browser/)」を参照してください。

<!-- tip end -->

LINE未使用ユーザー、もしくは[ディープリンク](https://en.wikipedia.org/wiki/Mobile_deep_linking)が動作しない状況にあるLINEユーザーが、[外部ブラウザ](https://developers.line.biz/ja/glossary/#external-browser)でLINEミニアプリを開くと、以下の図のようなページが表示され、LINEミニアプリをスマートフォン版LINE（[LIFFブラウザ](https://developers.line.biz/ja/glossary/#liff-browser)）で開くように案内されます。ページ内の［**ウェブブラウザで開く**］をタップすると、LIFFのエンドポイントURLのページがウェブブラウザで表示されます。

![](https://developers.line.biz/media/line-mini-app/landing-page-ja.png)

## LIFFの対応バージョン 

LINEミニアプリは、[LIFF](https://developers.line.biz/ja/docs/liff/overview/)を使用して開発します。 LINEミニアプリで使用できるLIFF SDKの最小バージョンはv2.1です。

LINEミニアプリでは、LIFF v2.1.xが提供するすべてのLIFF APIを使用できます。
