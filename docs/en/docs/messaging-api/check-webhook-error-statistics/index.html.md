# Check webhook error causes and statistics

The Messaging API provides a feature to check error causes and statistics when sending webhooks. This is useful for understanding the status of sending webhooks when a webhook wasn't received due to a problem on the bot server, etc.

![Display of error statistics when an error is returned from the bot server](https://developers.line.biz/media/messaging-api/receiving-messages/webhook-error-en.jpg)

## Enable error statistics 

The display of error statistics is disabled by default. To display error statistics, perform the following steps from the [LINE Developers Console](https://developers.line.biz/console/):

1. Open the settings screen of the channel for which you want to display error statistics.
1. Click the **Messaging API** tab.
1. Turn on **Use webhook**.
1. Turn on **Error statistics aggregation**.

After turning on **Error statistics aggregation**, click the **Webhook errors** tab to view the statistics. The errors are aggregated only while **Error statistics aggregation** is turned on. Data from periods when it was turned off won't be displayed retroactively. The time zone used for the date and time of the displayed errors is UTC+9. You can also download past error information in TSV format by clicking **Download TSV file**.

![Error statistics aggregation](https://developers.line.biz/media/messaging-api/receiving-messages/error-statistics-en.png)

<!-- tip start -->

**Error Statistics don't include requests made to verify a webhook URL**

Error statistics only show webhooks that were actually attempted to be sent. Error statistics don't include requests made to [verify a webhook URL](https://developers.line.biz/en/docs/messaging-api/verify-webhook-url/), regardless of whether they succeeded or failed.

<!-- tip end -->

## Check the reason for errors 

Error statistics provide the reasons and details for errors. There are four types of reasons.

| Reason for error | Summary |
| --- | --- |
| `could_not_connect` | The LINE Platform tried to send a webhook to the bot server, but couldn't successfully connect to the bot server. For more information, see [The reason is could_not_connect](https://developers.line.biz/en/docs/messaging-api/check-webhook-error-statistics/#reason-could-not-connect) section. |
| `request_timeout` | The LINE Platform sent a webhook to the bot server, but the bot server didn't return a response within 2 seconds. For more information, see [The reason is request_timeout](https://developers.line.biz/en/docs/messaging-api/check-webhook-error-statistics/#reason-request-timeout) section. |
| `error_status_code` | The LINE Platform sent a webhook to the bot server, but the bot server returned a response other than the HTTP status code in the `20x`. For more information, see [The reason is error_status_code](https://developers.line.biz/en/docs/messaging-api/check-webhook-error-statistics/#reason-status-code) section. |
| `unclassified` | An unknown error occurred that can't be categorized above. For more information, see [The reason is unclassified](https://developers.line.biz/en/docs/messaging-api/check-webhook-error-statistics/#reason-unclassified) section. |

## Check the detail for errors 

The details for each reason are as follows:

- [The reason is could_not_connect](https://developers.line.biz/en/docs/messaging-api/check-webhook-error-statistics/#reason-could-not-connect)
- [The reason is request_timeout](https://developers.line.biz/en/docs/messaging-api/check-webhook-error-statistics/#reason-request-timeout)
- [The reason is error_status_code](https://developers.line.biz/en/docs/messaging-api/check-webhook-error-statistics/#reason-status-code)
- [The reason is unclassified](https://developers.line.biz/en/docs/messaging-api/check-webhook-error-statistics/#reason-unclassified)

### The reason is `could_not_connect` 

If the LINE Platform tried to send a webhook to the bot server, but couldn't successfully connect to the bot server, the reason will be `could_not_connect`. The details in this case are as follows.

| Detail for error | Summary |
| --- | --- |
| `Connection failed` | Failed to connect to bot server. |
| `Connection failed (received GOAWAY)` | Connection refused when connecting to bot server. |
| `Connection failed (session closed)` | Connection to the bot server was unexpectedly terminated. |
| `Connection timeout` | Connection to the bot server didn't complete within a certain period of time. |
| `DNS Query timeout` | Webhook URL name resolution was performed, but name resolution couldn't be completed within a certain period of time. |
| `Invalid URL syntax` | An invalid webhook URL is specified (e.g., RFC violation). |
| `Session protocol negotiation failure` | Connected to bot server, but protocol negotiation failed. |
| `No SSL/TLS record` | The bot server response isn't SSL/TLS encrypted. |
| `TLS handshake failure` | Connected to bot server, but TLS handshake failed. Check if the bot server supports [SSL/TLS specification of the webhook source](https://developers.line.biz/en/docs/messaging-api/ssl-tls-spec-of-the-webhook-source/). |
| `Unknown host` | The host specified in the Webhook URL couldn't be found. |

### The reason is `request_timeout` 

If a webhook is sent from the LINE Platform to the bot server, but the response isn't received by the LINE Platform or the sending fails midway, the reason will be `request_timeout`. The details in this case are as follows. Note that the webhook may have been successfully received by the bot server.

| Detail for error | Summary |
| --- | --- |
| `Request timeout` | Webhook was sent to the bot server, but no response was returned within a certain period of time. |

### The reason is `error_status_code` 

If the reason is `error_status_code`, the details will contain the HTTP status code.

### The reason is `unclassified` 

If an unclassified error occurs, the reason is `unclassified`. The details in this case are as follows.

| Detail for error | Summary |
| --- | --- |
| `Session closed unexpectedly` | A webhook was sent to the bot server, but the connection was unexpectedly closed. |
| `Stream closed unexpectedly` | A webhook was sent to the bot server, but the stream was unexpectedly closed. |
| `Unclassified webhook dispatch error` | An unclassifiable and unexpected error occurred. |

## Enable webhook redelivery to prepare for errors 

By enabling webhook redelivery in advance, if your bot server fails to receive a webhook and an error occurs, the webhook will be resent to your bot server. For more information, see [Redeliver a webhook that failed to be received](https://developers.line.biz/en/docs/messaging-api/receiving-messages/#webhook-redelivery).
