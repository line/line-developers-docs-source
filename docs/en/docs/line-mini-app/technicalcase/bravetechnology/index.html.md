# 'How queue management solutions are scaling with the LINE MINI App: The development use case of "matoca" and "yoboca"'

<!-- tip start -->

**About this page**

This page contains articles migrated from the LINE API Use Case site (closed on March 31, 2026) to the LINE Developers site. The page presents case studies of companies that have adopted the LINE Platform. Note that the content of the articles reflects the information available at the time of publication.

<!-- tip end -->

![BraveTechnology inc.](https://developers.line.biz/media/line-mini-app/technicalcase/bravetechnology/en/bravetechnology_logo.webp)

**BraveTechnology inc.**

Waiting in line is something everyone experiences. At BraveTechnology, our mission is to reduce the stress that comes with it by providing waitlist and notification services through LINE MINI Apps.

## The service provider’s thoughts on developing the system 

We deliver services to realize our mission of reducing the stress of waiting for everyone.

Most people dislike waiting—whether it's unexpected long waits or delays even with a reservation. On the other hand, businesses also face the stress of keeping customers waiting and of potentially disrupting nearby areas. During the COVID-19 pandemic, this stress has only intensified as people tried to avoid the "Three Cs" (closed spaces, crowded places, and close-contact settings).

To address these issues, we provide two services: "matoca" for waitlist management and "yoboca" for pickup notifications. With matoca, users can secure a place in line without physically standing in a queue and are notified via LINE when it is their turn. In situations where there is a wait between purchase and pickup, yoboca sends LINE notifications when an order is ready for pickup. With these services, users are free to relax at a cafe or run errands until they are called, helping to reduce the stress of waiting.

There are countless moments of waiting in everyday life, and each brings its own stress. We will continue working to reduce this waiting stress using LINE.

### Image 

![service image](https://developers.line.biz/media/line-mini-app/technicalcase/bravetechnology/en/bravetechnology_screenshot.webp)

## System overview 

![System architecture diagram](https://developers.line.biz/media/line-mini-app/technicalcase/bravetechnology/en/bravetechnology_system_diagram.webp)

### Adopting AWS with future scalability in mind 

We have been using AWS since the days of "LINE de Junbanmachi", adopting cloud services so that both development and operations can be handled by a small team. Released last September, yoboca adopts a serverless architecture. It is built on pay-as-you-go, fully managed services such as AWS Lambda and Amazon SQS, combined with automation through CI/CD. This architecture helps reduce both operational and financial costs while providing a scalable foundation for future growth.

### Aiming to deliver services that enhance marketing and customer loyalty through integration with other services 

Recently, we released APIs that enable matoca and yoboca to integrate with POS systems, ticketing machines, and e-commerce sites. Previously, these services operated independently, but by integrating with in-store equipment such as POS systems, no additional devices are required, and operational steps for staff at partner businesses can be reduced. In addition to integrating with other devices and services, we plan to further leverage user behavior data to develop services that enhance marketing initiatives and customer loyalty for partner businesses.

### A message for those developing new services 

As mentioned earlier, LINE is a platform with an exceptionally large number of active users and a wide range of available APIs. Like any platform, it has certain constraints, while developers may naturally aspire to build more flexible and sophisticated systems. However, such complexity is not always what users are looking for. We encourage developers to focus on creating services that genuinely meet user needs and to select technologies and platforms accordingly. If ease of use is a top priority, leveraging the LINE Platform can be an effective choice. In such cases, we recommend considering LINE as one of your options.

---

## Related links 

- [BraveTechnology inc.](https://bravetechnology.co.jp/)
- [matoca](https://junbanmachi.jp/)
- [yoboca](https://yoboca.jp/)
