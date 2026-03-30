# Verify webhook URL

If you're using Messaging API webhooks, we recommend that you use one of these methods to verify that the LINE Platform can communicate with the webhook URL (bot server).

- [Verification method 1: Verify with the endpoint for webhook URL validation](https://developers.line.biz/en/docs/messaging-api/verify-webhook-url/#verify-method-01)
- [Verification method 2: Use the webhook URL's "Verify" button in the LINE Developers Console](https://developers.line.biz/en/docs/messaging-api/verify-webhook-url/#verify-method-02)

<!-- tip start -->

**Return status code 200 for the communication request**

The LINE Platform sends an HTTP POST request that doesn't include a webhook event to the webhook URL (bot server) to confirm communication. Design your bot server to return status code `200`.

Example HTTP POST request without a webhook event:

```json
{
  "destination": "xxxxxxxxxx",
  "events": []
}
```

<!-- tip end -->

If the bot server didn't receive the webhook after verifying the webhook URL, [investigate the cause of webhook reception failure](https://developers.line.biz/en/docs/messaging-api/verify-webhook-url/#investigate-webhook-reception-failure).

## Verification method 1: Verify with the endpoint for webhook URL validation 

Verify the communication by using the endpoint for webhook URL test.

- [Test webhook endpoint](https://developers.line.biz/en/reference/messaging-api/#test-webhook-endpoint)

## Verification method 2: Use the webhook URL's "Verify" button in the LINE Developers Console 

In the [LINE Developers Console](https://developers.line.biz/console/), click the webhook URL's **Verify** button to perform the verification.

![send target](https://developers.line.biz/media/news/webhook-url-verify-button.png)

## Investigate the cause of webhook reception failure 

If the bot server didn't receive the webhook after verifying the webhook URL, use the following methods to investigate the cause of webhook reception failure:

- Check the [response](https://developers.line.biz/en/reference/messaging-api/#test-webhook-endpoint-response) or [error response](https://developers.line.biz/en/reference/messaging-api/#test-webhook-endpoint-error-response) returned from the endpoint to test webhook URL
- [Check webhook error causes and statistics](https://developers.line.biz/en/docs/messaging-api/check-webhook-error-statistics/)
- Check [SSL/TLS specification of the webhook source](https://developers.line.biz/en/docs/messaging-api/ssl-tls-spec-of-the-webhook-source/)
