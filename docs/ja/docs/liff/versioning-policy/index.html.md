# バージョニングポリシー

LIFFアプリに適切なLIFF SDKを組み込むために、LIFFのバージョニングポリシーを正しく理解してください。

- [メジャーバージョンのステータス](https://developers.line.biz/ja/docs/liff/versioning-policy/#version-support-status)
- [LIFFのバージョニングポリシー](https://developers.line.biz/ja/docs/liff/versioning-policy/#versioning-policy)
- [LIFF SDK（sdk.js）のアップデートポリシー](https://developers.line.biz/ja/docs/liff/versioning-policy/#update-policy)
- [LIFF SDKのライフサイクル](https://developers.line.biz/ja/docs/liff/versioning-policy/#life-cycle)

<!-- note start -->

**注意**

LIFF SDKのアップデートに伴い、LIFFアプリに組み込んだLIFF SDKが廃止されることがあります。廃止されたLIFF SDKを組み込んでいるLIFFアプリは、開けません。

長期的にLIFFアプリを利用する場合は、定期的にこのページを確認し、適切なLIFF SDKを組み込んでください。

<!-- note end -->

## メジャーバージョンのステータス 

[LIFF SDKのライフサイクル](https://developers.line.biz/ja/docs/liff/versioning-policy/#life-cycle)は、メジャーバージョンごとに規定されています。現在サポートされているLIFF SDKのメジャーバージョンと、各バージョンのステータスは以下のとおりです。

| LIFFバージョン<br>（リリース日） | ステータス<br>（現ステータスの最終日） | 利用可否および説明 |
| --- | --- | --- |
| LIFF v1<br>（2018年6月6日） | 廃止<br>（2021年10月1日） | ❌ 予告なくCDNエッジパスおよびCDN固定パスがすべて無効になり、LIFFアプリが開けなくなります。 |
| LIFF v2<br>（2019年10月16日） | アクティブ<br>（～LIFF v3のリリース日） | ✅ 現行バージョンです。新規機能の追加や既存機能の改善が頻繁に行われます。 |
| LIFF v3<br>（未定） |  |

## LIFFのバージョニングポリシー 

LIFF v2.2.0以降、LIFFのバージョンナンバーは、[セマンティック バージョニング](https://semver.org/lang/ja/)（SemVer）で定められたルールに従います。

SemVerでは、以下のバージョン形式を定義しています。

`メジャー.マイナー.パッチ`

たとえば、`v1.2.3`の場合、`1`はメジャーバージョン、`2`はマイナーバージョン、`3`はパッチバージョンを表します。

各バージョンの定義は以下のとおりです。

| バージョン | 説明 |
| --- | --- |
| メジャー | 公開されているAPIに対して、後方互換性を持たない変更があった場合に更新されます。<br>バージョンアップの例：v1.1.12 → **v2.0.0** |
| マイナー | 公開されているAPIの後方互換性を維持したまま、機能を追加した場合に更新されます。<br>バージョンアップの例：v1.1.12 → **v1.2.0** |
| パッチ | 後方互換性を維持したままバグ修正を行う場合に更新されます。バグ修正とは、間違った振る舞いを修正する内部の変更を指します。<br>バージョンアップの例：v1.1.12 → **v1.1.13** |

## LIFF SDK（sdk.js）のアップデートポリシー 

LIFFでは、LIFF v2.1.13リリース以降、以下の2種類のCDNパスを用意しています。[LIFFアプリにLIFF SDKを組み込む](https://developers.line.biz/ja/docs/liff/developing-liff-apps/#integrating-sdk)ときに、目的に合ったCDNパスを指定してください。

| CDNパス | 説明 |
| --- | --- |
| CDNエッジパス | メジャーバージョンのみを含むCDNパスです。常に最新の機能を使用する場合は、このCDNパスを使用します。メジャーバージョンがアップデートされたときのみURLを更新する必要があります。<br>例：https://static.line-scdn.net/liff/edge/**2**/sdk.js |
| CDN固定パス | パッチバージョンまで含むCDNパスです。特定のバージョンの機能を使用する場合は、このCDNパスを使用します。LIFFアプリを更新しない限り、指定したパッチバージョンを使い続けることができます。LIFFの新機能や、セキュリティ改善、バグ修正を反映したいときのみURLを更新してください。自動的に更新されないため、LIFF SDKのアップデートの影響を受けません。<br>例：https://static.line-scdn.net/liff/edge/**versions/2.22.3**/sdk.js |

<!-- note start -->

**どのバージョンを使うべきか**

CDN固定パスを使用している開発者は、LIFFアプリを更新するタイミングを決める必要があります。アップデートの内容を正しく理解し、自分のLIFFアプリに適しているか判断するために、『LIFFドキュメント』の「[リリースノート](https://developers.line.biz/ja/docs/liff/release-notes/)」をこまめに確認してください。

<!-- note end -->

CDN固定パスを指定する例：

```html
<script charset="utf-8" src="https://static.line-scdn.net/liff/edge/versions/2.22.3/sdk.js"></script>
```

<!-- tip start -->

**後方互換性を維持するためのCDNパスについて**

作成済みのLIFFアプリの動作を保証するために、以下のCDNパスでLIFF SDKの提供を継続します。このCDNパスで利用できるLIFF SDKは、CDNエッジパスで利用できるLIFF SDKと同じバージョンです。

後方互換性を維持するためのCDNパス：<br> https://static.line-scdn.net/liff/edge/**2.1**/sdk.js

<!-- tip end -->

<!-- note start -->

**後方互換性を維持するためのCDNパスの廃止について**

後方互換性を維持するためのCDNパスは、[LIFF SDKのライフサイクルスケジュール](https://developers.line.biz/ja/docs/liff/versioning-policy/#life-cycle-schedule)に関わらず廃止される可能性があります。LIFFアプリで指定するCDNパスを、CDNエッジパスに変更することをおすすめします。

方針が決まり次第改めてお知らせします。

<!-- note end -->

## LIFF SDKのライフサイクル 

LIFF SDKのライフサイクルは、メジャーバージョンごとに以下のように規定されています。

新しいメジャーバージョンがリリースされたときのステータスは「アクティブ」です。次のメジャーバージョンがリリースされるときに、現在のメジャーバージョンのステータスが「アクティブ」から「メンテナンス」に変更され、一定期間経過後に「非推奨」、「廃止」の順に変更されます。

| ステータス | 利用可否および説明 | サポート期間 |
| --- | --- | --- |
| アクティブ | ✅ 現行バージョンです。新規機能の追加や既存機能の改善が頻繁に行われます。 | リリース日から、次のメジャーバージョンがリリースされた日まで |
| メンテナンス | ✅ 既存機能を維持するために必要な、バグ修正やセキュリティ改善が行われます。 | アクティブ期間最終日から12か月間 |
| 非推奨 | ✅ アップデートされません。 | メンテナンス期間最終日から6か月間 |
| 廃止 | ❌ 廃止日以降、予告なくCDNエッジパスおよびCDN固定パスがすべて無効になり、LIFFアプリが開けなくなります。 | - |

### LIFF SDKのライフサイクルスケジュール 

LIFF SDKのメジャーバージョンのライフサイクルをよく理解し、適切な準備を行ってください。

| LIFFバージョン<br>（リリース日） | アクティブ期間 | メンテナンス期間 | 非推奨期間 | 廃止日 |
| --- | --- | --- | --- | --- |
| LIFF v1<br>（2018年6月6日） | ～ 2019年10月15日<br>`✅ LIFF v1` | ～ 2021年4月1日<br>`✅ LIFF v1` | ～ 2021年9月30日<br>`✅ LIFF v1` | 2021年10月1日<br>`❌ LIFF v1` |
| LIFF v2<br>（2019年10月16日） | ～ LIFF v3のリリース日<br>`✅ LIFF v2` | ～未定<br>`✅ LIFF v2` | ～未定<br>`✅ LIFF v2` | 未定<br>`❌ LIFF v2` |
| LIFF v3<br>（未定） |  |  |  |

`✅ LIFF v1`/`❌ LIFF v1`：https://**d.line-scdn.net/liff/1.0**/sdk.js の利用可否

`✅ LIFF v2`/`❌ LIFF v2`：https://static.line-scdn.net/liff/edge/**2**/sdk.js 、 https://static.line-scdn.net/liff/edge/**versions/2.x.x**/sdk.js 、および https://static.line-scdn.net/liff/edge/**2.1**/sdk.js の利用可否
