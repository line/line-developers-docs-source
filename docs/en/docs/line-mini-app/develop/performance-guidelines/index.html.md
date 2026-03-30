# Performance guidelines

To provide the best possible LINE MINI App experience to your users, take the performance of LINE MINI App into consideration.

A good reference regarding the importance of HTML5 performance, [Why does speed matter?](https://web.dev/learn/performance/why-speed-matters), can be found on web.dev.

For measuring performance, we recommend using performance measurement tools such as [Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/) and [PageSpeed Insights](https://pagespeed.web.dev/), provided by Google.

LY Corporation recommends the following score.

Performance measurement tool | Score
-|-
[Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/) | Performance: 50 and above

<!-- note start -->

**Note**

- Measure without executing LINE Login. When LINE Login is executed simultaneously, the performance of the LINE Login page is measured, preventing LINE MINI App's performance from being measured.
- Be sure to measure in the production environment (real environment). Note that the network environment can affect the performance score.

<!-- note end -->
