# パフォーマンスガイドライン

LINEミニアプリのユーザーがサービスを快適に利用できるように、LINEミニアプリのパフォーマンスも十分に考慮してください。

HTML5のパフォーマンスの重要性については、web.devの「[速度が重要な理由](https://web.dev/learn/performance/why-speed-matters?hl=ja)」が参考になります。

なお、パフォーマンスを計測する場合は、Googleが提供する[Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/)や[PageSpeed Insights](https://pagespeed.web.dev/)などのパフォーマンス計測ツールを利用することをお勧めします。

LINEヤフー株式会社では、以下のスコアを満たすことを推奨しています。

パフォーマンス計測ツール | スコア
-|-
[Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/) | Performance: 50以上

<!-- note start -->

**注意**

- LINEログインが実行されない状態で計測してください。LINEログインが実行されると、LINEログインのページのパフォーマンスが計測され、LINEミニアプリのパフォーマンスは計測されません。
- プロダクション環境（本番環境）で計測してください。スコアは、ネットワーク環境などの影響を受ける場合があります。

<!-- note end -->
