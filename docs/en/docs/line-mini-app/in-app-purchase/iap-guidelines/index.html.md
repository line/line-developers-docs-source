# In-app purchase development guidelines

This page explains the specification constraints, design considerations, and recommended implementation methods for using the in-app purchase feature in LINE MINI Apps.

When using the in-app purchase feature, follow the development guidelines below. Also, be sure to refer to the [LINE MINI App development guidelines](https://developers.line.biz/en/docs/line-mini-app/development-guidelines/).

**Prohibited matters**

- [Don't restrict access by IP address](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/iap-guidelines/#prohibit-ip-address-restriction)

**Required matters**

- [Verify access token validity](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/iap-guidelines/#verify-access-token)

**Recommended matters**

- [Verify the webhook signature](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/iap-guidelines/#verify-webhook-signature)
- [Eliminate duplicates](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/iap-guidelines/#eliminate-duplicates)
- [Implement proper error handling](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/iap-guidelines/#error-handling)
- [Don't send duplicate payment notifications](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/iap-guidelines/#payment-notifications)

## Prohibited matters 

### Don't restrict access by IP address 

On servers that receive webhooks, don't restrict access based on the IP address of the LINE Platform sending webhook requests. The IP address of the LINE Platform isn't disclosed and may change without notice. Instead of access control by IP address, use [signature verification](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/iap-guidelines/#verify-webhook-signature) to deny requests from unauthorized sources.

## Required matters 

### Verify access token validity 

When making a purchase reservation, use the [Verify access token validity](https://developers.line.biz/en/reference/line-login/#verify-access-token) endpoint to verify the access token validity, channel ID, and access token validity period on the server side of your LINE MINI App.

## Recommended matters 

### Implement with non-breaking changes in mind 

In LINE MINI App in-app purchase, non-breaking feature additions may be made. These changes are intended to expand the API without breaking existing features. Therefore, the following types of changes may be made without advance notice:

- Addition of new endpoints
- Addition of optional parameters, fields, and headers in API requests
- Addition of fields and headers in API responses
- Addition of enum values
- Addition of properties to webhook event objects
- Changes to the order of properties in API responses and webhook event objects
- Presence or absence of whitespace or line breaks between data elements

Implement your server so that it will work correctly even with these non-breaking feature additions.

### Verify the webhook signature 

To prevent forged requests, verify the signature using the `x-line-signature` request header.

- Calculate a digest of the request body using the HMAC-SHA256 algorithm with the channel secret as the secret key.
- Base64-encode the digest and check whether it matches the signature included in the `x-line-signature` request header.

Example of signature verification in Java

```java
class WebhookProcessor {
    void verify(String httpRequestBody) { // Request body string
        String channelSecret = '...'; // Channel secret string
        SecretKeySpec key = new SecretKeySpec(channelSecret.getBytes(), "HmacSHA256");
        Mac mac = Mac.getInstance("HmacSHA256");
        mac.init(key);

        byte[] source = httpRequestBody.getBytes("UTF-8");
        String signature = Base64.encodeBase64String(mac.doFinal(source));
        // Compare x-line-signature request header string and the signature
    }
}
```

For more information on webhook signature verification, see [Verify the Webhook signature](https://developers.line.biz/en/docs/messaging-api/verify-webhook-signature/) in the Messaging API documentation.

### Eliminate duplicates 

Due to network conditions, the same webhook event may be delivered multiple times. Use the order ID (`orderId`) to ensure that items are not granted multiple times for a single purchase. Also, ensure that cancel processing is not performed multiple times if the user cancels the payment in the app store.

### Implement proper error handling 

A purchase reservation doesn't guarantee that the payment will be completed. If a network error or other issues occur, take appropriate action, such as retrying the request or prompting the user to try again.

### Don't send duplicate payment notifications 

When a purchase is completed, a message is automatically sent to the user from the LINE Official Account "LINE In-App Purchase Notifications (LINEアプリ内課金お知らせ in Japanese)". Likewise, if the user cancels the payment in the app store, a message is automatically sent to the user.

If payment notifications are sent from another LINE Official Account in addition to this, the user will receive the same type of notification multiple times. To avoid degrading the user experience, don't send duplicate notifications.
