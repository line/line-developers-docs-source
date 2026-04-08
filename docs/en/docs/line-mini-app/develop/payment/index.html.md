# Handling payments

You can provide users with a payment feature by integrating a payment system into your LINE MINI App.

## Available payment system 

The payment systems available on LINE MINI Apps vary by country or region.

| Payment methods | Japan | Taiwan | Thailand |
| --- | :-: | :-: | :-: |
| [LINE Pay](https://developers.line.biz/en/docs/line-mini-app/develop/payment/#line-pay) | ❌ | ✅ | ✅ |
| [In-app purchase for the LINE MINI App](https://developers.line.biz/en/docs/line-mini-app/develop/payment/#in-app-purchase) | ✅ | ❌ | ❌ |
| [Other methods](https://developers.line.biz/en/docs/line-mini-app/develop/payment/#other-payment-methods) | ✅ | ✅ | ✅ |

<!-- note start -->

**The LINE Pay service in Japan has been terminated**

The LINE Pay service in Japan has been terminated as of April 30, 2025. The LINE Pay services in Taiwan and Thailand continue to be available.

<!-- note end -->

## LINE Pay 

### Preparing LINE Pay Merchant Account 

To use LINE Pay on LINE MINI App, you need a LINE Pay Merchant Account. If you don't have one yet, apply on the [LINE Pay's official website](https://pay.line.me/portal/global/main).

### Developing a service that uses LINE Pay 

Once you acquire a LINE Pay Merchant account, integrate LINE Pay to your LINE MINI App. For more information on LINE Pay, see the [Online payment documentation](https://developers-pay.line.me/online) in LINE Pay Developers.

When using LINE Pay, the payment will be processed as follows:

1. When a user initiates a transaction on your LINE MINI App, the payment process on LINE Pay is launched.

   The screen displayed by LINE MINI App:<br>![](https://developers.line.biz/media/line-mini-app/mini_linepay_flow01.png)

2. The user confirms the payment details with LINE Pay and enters the LINE Pay authentication information.

   The screen displayed by LINE Pay:<br>![](https://developers.line.biz/media/line-mini-app/mini_linepay_flow02.png)

3. The order confirmation page is displayed.

   The screen displayed by LINE MINI App:<br>![](https://developers.line.biz/media/line-mini-app/mini_linepay_flow03.png)

### Testing LINE Pay 

To test your payment process implementation, you can use the [sandbox](https://developers-pay.line.me/sandbox) provided by LINE Pay.

## In-app purchase for the LINE MINI App 

[In-app purchase](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/overview/) is a system that allows users to buy digital content provided within a LINE MINI App. Users launch the LINE MINI App within the LINE app to begin purchasing digital content, and the payment is processed using the App Store or Google Play payment system.

Currently, in-app purchase is available only in Japan. For more information on eligibility and other requirements, see [In-app purchase overview](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/overview/).

## Other payment methods 

To offer other payment methods other than those mentioned above in your LINE MINI App, implement them as you would on ordinary web pages. However, you must design the process so that users are redirected to your LINE MINI App page after completing a transaction on an external domain or app.
