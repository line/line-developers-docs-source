# Configure module channel settings

<!-- note start -->

**Procedures are required to use optional functions**

The functions described in this document are available only to corporate customers who have made the prescribed applications. If you would like to publish the extension function using the module, contact the sales representative or contact us from [LINE Marketplace Inquiry](https://line-marketplace.com/jp/inquiry) (only available in Japanese).

<!-- note end -->

In the module channel, a dedicated **module** tab appears in the [LINE Developers Console](https://developers.line.biz/console/).

In the **module** tab, you can set the module channel's webhook URL, whether to receive webhook, and the `redirect_uri` specified when [requesting authorization from the LINE Official Account admin](https://developers.line.biz/en/docs/partner-docs/module-technical-attach-channel/#request-auth-from-line-oa-admin).

![Module tab in LINE Developers Console](https://developers.line.biz/media/partner-docs/module-technical/module-tab-in-console-en.png)

## 1. module tab 

The **module** tab is a setting item dedicated only to the module channel.

## 2. Webhook settings 

### Webhook URL 

You can set one webhook URL for the module channel. See also [Receiving a webhook](https://developers.line.biz/en/docs/partner-docs/module-technical-using-messaging-api/#get-webhook).

### Using webhook 

You can set whether the module channel receives webhook events.

### Resend webhook 

You can set whether or not to resend the webhook event from the LINE Platform when getting the webhook event fails in the webhook URL of the module channel.

### Error stats 

You can set whether or not to display stats about webhook event reception failures on the **Webhook errors** tab.

## 3. Redirect settings 

### Redirect URL 

For the redirect URL, specify the value of the `redirect_uri` parameter used to [request authorization from the LINE Official Account admin](https://developers.line.biz/en/docs/partner-docs/module-technical-attach-channel/#request-auth-from-line-oa-admin). The redirect URL scheme must be `https`.

You can specify multiple redirect URLs for a single channel.
