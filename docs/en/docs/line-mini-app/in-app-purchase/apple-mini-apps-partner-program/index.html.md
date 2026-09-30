# Reduced App Store fees through the Mini Apps Partner Program

This page explains how the Mini Apps Partner Program offered by Apple Inc. applies to LINE MINI App in-app purchases, including how fee reductions work, how to apply, application requirements, and the effects of participating in the program.

<!-- table of contents -->

## What is the Mini Apps Partner Program 

The [Mini Apps Partner Program](https://developer.apple.com/programs/mini-apps-partner/) is a fee reduction program for in-app purchases. You can optionally apply for this program for any LINE MINI App that has been approved to use the in-app purchase feature.

When the Mini Apps Partner Program applies to a LINE MINI App, the fees payable to Apple Inc. in connection with the payment of sales proceeds from App Store transactions on iOS shall be reduced. If the fees are reduced under the Mini Apps Partner Program, the amount equivalent to the fees payable by LY Corporation to the App Store shall also be reduced. Accordingly, the amount to be deducted from the gross sales amount pursuant to the [LINE In-App Purchase Terms of Use (for LINE MINI App Provider)](https://terms2.line.me/LINE_MINI_App_IAP?lang=en) shall also be reduced.

## Requirements for applying to the Mini Apps Partner Program 

You can apply for the Mini Apps Partner Program only for LINE MINI Apps for which your [in-app purchase](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/overview/) application has been approved.

If you haven't applied to use in-app purchase, follow the steps in [Apply to use in-app purchase](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/request-iap-review/).

## Apply for the Mini Apps Partner Program 

You can apply for the Mini Apps Partner Program when submitting your LINE MINI App for a verification review in the LINE Developers Console. Apply separately for each LINE MINI App.

For more information, see [Apply for the Mini Apps Partner Program](https://developers.line.biz/en/docs/line-mini-app/submit/submission-guide/#apply-for-program).

## How fee reductions apply 

The Mini Apps Partner Program applies to each LINE MINI App, while each payment is evaluated separately against the requirements for the fee reduction.

The fee reduction doesn't apply to App Store payments that don't meet the program requirements, Google Play payments, or test payments.

### Age range verification 

When a user launches a LINE MINI App to which the Mini Apps Partner Program applies, the user's age range may be verified. The [Declared Age Range API](https://developer.apple.com/documentation/declaredagerange) offered by Apple Inc. may be used to verify the user's age range. Service providers don't need to implement age range verification in their LINE MINI Apps.

If the user declines to share their age range, the user's age range can't otherwise be verified, or the user's device environment doesn't support age range verification, the following restrictions may apply:

- The fee for payments made by the user may not be reduced.
- The user may be restricted from using the LINE MINI App, and the app may close before it launches.

<!-- note start -->

**Age range verification information isn't provided to service providers**

Age-related information used or obtained during age range verification under the Mini Apps Partner Program, such as the user's age, date of birth, or age range, isn't provided to the LINE MINI App service provider.

<!-- note end -->

## Implement payments with reduced fees 

The LINE Platform determines whether a fee reduction applies to a payment. Therefore, you don't need to implement separate in-app purchase flows based on whether the Mini Apps Partner Program applies. If you've already implemented the in-app purchase feature, no code changes are required when the program takes effect.

For more information about the purchase flow, see [Integrate the in-app purchase feature](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/implement-in-app-purchase/).

## Webhook events for payments with reduced fees 

In [purchase complete events](https://developers.line.biz/en/reference/line-mini-app/#purchase-complete-event) and [refund events](https://developers.line.biz/en/reference/line-mini-app/#refund-event), `APPLE_MINI_APPS_PARTNER_PROGRAM` is returned as the value of the `paymentBenefitProgram` property if the Mini Apps Partner Program fee reduction applied to the payment. If the fee reduction didn't apply, this property isn't included.

The `paymentBenefitProgram` property provides additional information for identifying payments that received a fee reduction. It doesn't affect the purchase result or the item granted to the user.

The following is an example of a purchase complete event for a payment that received a fee reduction:

```json
{
  "type": "purchaseComplete",
  "orderId": "T2025020710000002126002",
  "productId": "iap_ln_002",
  "userId": "U91FC5A...",
  "purchaseTimestamp": 1738672496,
  "channelId": "12345...",
  "paymentBenefitProgram": "APPLE_MINI_APPS_PARTNER_PROGRAM"
}
```

## Considerations when transitioning between LINE MINI Apps 

When transitioning from another LINE MINI App to a LINE MINI App to which the Mini Apps Partner Program applies, use the destination [LIFF URL](https://developers.line.biz/en/glossary/#liff-url) or [permanent link](https://developers.line.biz/en/docs/line-mini-app/develop/permanent-links/) instead of the web app's endpoint URL so that age range verification occurs at the appropriate time.
