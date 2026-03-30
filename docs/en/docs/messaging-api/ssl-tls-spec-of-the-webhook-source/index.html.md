# SSL/TLS specification of the webhook source

When a bot server gets webhook events sent from the LINE Platform, it must use HTTPS communication. Use an SSL/TLS certificate issued by a public certification authority for HTTPS communication. You can purchase an SSL certificate, or you can use a free certificate, such as [Let's Encrypt](https://letsencrypt.org/).

Bot servers that receive webhooks must support HTTPS communication based on the following specifications:

<!-- table of contents -->

## Supported cipher suites 

Cipher suites with [Deprecated](https://developers.line.biz/en/glossary/#deprecated) status are maintained for compatibility, but may be discontinued without notice in the near future. Also, supported SSL/TLS protocol versions and HTTP versions vary by cipher suite.

<!-- tip start -->

**The table can be scrolled left or right**

Scroll the table to the right to see the status of each cipher suite, the supported SSL/TLS protocol version, and the supported HTTP version.

<!-- tip end -->

| IANA | OpenSSL | Hex code | Status | Supported SSL/TLS protocol versions | Supported HTTP versions |
| --- | --- | --- | --- | --- | --- |
| TLS_AES_256_GCM_SHA384 | TLS_AES_256_GCM_SHA384 | 0x13, 0x02 |  | TLS 1.3 | <ul><li>HTTP/1.0</li><li>HTTP/1.1</li><li>HTTP/2</li></ul> |
| TLS_CHACHA20_POLY1305_SHA256 | TLS_CHACHA20_POLY1305_SHA256 | 0x13, 0x03 |  | TLS 1.3 | <ul><li>HTTP/1.0</li><li>HTTP/1.1</li><li>HTTP/2</li></ul> |
| TLS_AES_128_GCM_SHA256 | TLS_AES_128_GCM_SHA256 | 0x13, 0x01 |  | TLS 1.3 | <ul><li>HTTP/1.0</li><li>HTTP/1.1</li><li>HTTP/2</li></ul> |
| TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 | ECDHE-ECDSA-AES128-GCM-SHA256 | 0xc0, 0x2b |  | TLS 1.2 | <ul><li>HTTP/1.0</li><li>HTTP/1.1</li><li>HTTP/2</li></ul> |
| TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 | ECDHE-RSA-AES128-GCM-SHA256 | 0xc0,0x2f |  | TLS 1.2 | <ul><li>HTTP/1.0</li><li>HTTP/1.1</li><li>HTTP/2</li></ul> |
| TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 | ECDHE-ECDSA-AES256-GCM-SHA384 | 0xc0, 0x2c |  | TLS 1.2 | <ul><li>HTTP/1.0</li><li>HTTP/1.1</li><li>HTTP/2</li></ul> |
| TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 | ECDHE-RSA-AES256-GCM-SHA384 | 0xc0, 0x30 |  | TLS 1.2 | <ul><li>HTTP/1.0</li><li>HTTP/1.1</li><li>HTTP/2</li></ul> |
| TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256 | ECDHE-ECDSA-CHACHA20-POLY1305 | 0xcc, 0xa9 |  | TLS 1.2 | <ul><li>HTTP/1.0</li><li>HTTP/1.1</li><li>HTTP/2</li></ul> |
| TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256 | ECDHE-RSA-CHACHA20-POLY1305 | 0xcc, 0xa8 |  | TLS 1.2 | <ul><li>HTTP/1.0</li><li>HTTP/1.1</li><li>HTTP/2</li></ul> |
| TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA | ECDHE-RSA-AES128-SHA | 0xc0, 0x13 | Deprecated | TLS 1.2 | <ul><li>HTTP/1.0</li><li>HTTP/1.1</li></ul> |
| TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA | ECDHE-RSA-AES256-SHA | 0xc0, 0x14 | Deprecated | TLS 1.2 | <ul><li>HTTP/1.0</li><li>HTTP/1.1</li></ul> |
| TLS_RSA_WITH_AES_128_GCM_SHA256 | AES128-GCM-SHA256 | 0x00, 0x9c | Deprecated | TLS 1.2 | <ul><li>HTTP/1.0</li><li>HTTP/1.1</li></ul> |
| TLS_RSA_WITH_AES_128_CBC_SHA | AES128-SHA | 0x00, 0x2f | Deprecated | TLS 1.2 | <ul><li>HTTP/1.0</li><li>HTTP/1.1</li></ul> |
| TLS_RSA_WITH_AES_256_CBC_SHA | AES256-SHA | 0x00, 0x35 | Deprecated | TLS 1.2 | <ul><li>HTTP/1.0</li><li>HTTP/1.1</li></ul> |

## Supported SSL/TLS protocol versions 

Supported protocol versions vary by cipher suite. For more information, see the "Supported SSL/TLS protocol versions" column under [Supported cipher suites](https://developers.line.biz/en/docs/messaging-api/ssl-tls-spec-of-the-webhook-source/#cipher-suites).

| Protocol version | Supported |
| ---------------- | --------- |
| TLS 1.3          | ✅        |
| TLS 1.2          | ✅        |
| TLS 1.1 or lower | ❌        |

## Supported HTTP versions 

Supported HTTP versions vary by cipher suite. For more information, see the "Supported HTTP versions" column under [Supported cipher suites](https://developers.line.biz/en/docs/messaging-api/ssl-tls-spec-of-the-webhook-source/#cipher-suites).

| HTTP version | Supported |
| ------------ | --------- |
| HTTP/2       | ✅        |
| HTTP/1.1     | ✅        |
| HTTP/1.0     | ✅        |
