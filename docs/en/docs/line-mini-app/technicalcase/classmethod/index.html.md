# A case study of mobile order system CX ORDER

<!-- tip start -->

**About this page**

This page contains articles migrated from the LINE API Use Case site (closed on March 31, 2026) to the LINE Developers site. The page presents case studies of companies that have adopted the LINE Platform. Note that the content of the articles reflects the information available at the time of publication.

<!-- tip end -->

![Classmethod](https://developers.line.biz/media/line-mini-app/technicalcase/classmethod/classmethod_logo.webp)

**Classmethod, Inc.**

With its mission to "empower creativity for everyone", Classmethod provides technical support across various fields, including cloud, data analytics, mobile, IoT, AI, and machine learning. The company also helps businesses leverage LINE by offering LINE MINI App development services, as well as "CX ORDER", a service that enables businesses to create mobile ordering LINE MINI Apps.

## The service provider’s thoughts on developing the system 

Although we are an IT company, we also operate a fully cashless café in Akihabara called "[DevelopersIO CAFE](https://cafe.classmethod.jp/)."\*

Drawing on our experience developing and operating various online sales channels—such as LINE, websites, and native apps—we released [CX ORDER](https://cxorder.jp/lp/), a cloud service that provides mobile ordering functionality through LINE MINI Apps.

In the short term, our goal is to help businesses (mainly restaurants) supplement the revenue lost due to reduced operating hours or temporary closures by expanding their takeout channels. Over the medium to long term, we aim to improve operational efficiency, reduce labor needs, and support ongoing user engagement via LINE.

While mobile ordering is attracting attention, it is still an innovative new service, so it is essential to lower the barriers to adoption as much as possible. We believe that by leveraging LINE, we can deliver a frictionless customer experience.

\* "DevelopersIO CAFE" was closed on December 20, 2022.

### Image 

| Product List | Product Details | Order Confirmation | Order Complete |
| --- | --- | --- | --- |
| ![Product List](https://developers.line.biz/media/line-mini-app/technicalcase/classmethod/classmethod_screenshot_1.webp) | ![Product Details](https://developers.line.biz/media/line-mini-app/technicalcase/classmethod/classmethod_screenshot_2.webp) | ![Order Confirmation](https://developers.line.biz/media/line-mini-app/technicalcase/classmethod/classmethod_screenshot_3.webp) | ![Order Complete](https://developers.line.biz/media/line-mini-app/technicalcase/classmethod/classmethod_screenshot_4.webp) |

## System overview 

![System architecture diagram](https://developers.line.biz/media/line-mini-app/technicalcase/classmethod/classmethod_system_diagram.webp)

### Built primarily on AWS, with the adoption of Google Cloud also underway 

We primarily use AWS, our area of greatest expertise. Users access each app and API through Amazon CloudFront. For core functions, we use Amazon ECS and Amazon Aurora, with auto-scaling configured to handle increased traffic.

Additionally, we utilize Amazon DynamoDB for frequently accessed data, as well as AWS Lambda and Amazon SQS. While AWS is our main platform, we have also started utilizing Google Cloud for certain functions.

### Ongoing cloud infrastructure and operational costs 

Since core functions are built on Amazon ECS and Amazon Aurora, some additional costs are incurred compared to a fully serverless environment. Considering implementation costs and medium- to long-term operational costs, we believe the current configuration is appropriate. However, we plan to explore options such as migrating specific functions to serverless environments or adjusting the overall configuration as the situation evolves.

### Operational tools supporting the infrastructure 

We use AWS CDK (TypeScript) for infrastructure configuration management. Since CX ORDER is built with TypeScript across both the app and API, engineers can handle everything seamlessly, from the infrastructure layer to the frontend. We have also introduced Sentry to monitor app errors and send notifications to Slack. When multiple events occur at the same tenant in a short period, we work with the Customer Success Team to understand the customer's situation and help resolve errors. We use Google Analytics to track user behavior, and leverage the data to improve the apps and create user segments for message delivery.

### Aiming to boost sales, improve operational efficiency, and reduce labor needs at client stores 

Our top priority is to boost sales, improve operational efficiency, and reduce staffing needs for the stores that implement our system. We will continue to add and refine features by gathering feedback from more customers. In addition, we are exploring ways to contribute to customer communication using LINE, by introducing new features and through customer success efforts, drawing on insights from our internal experiments.

### Requests for the LINE API 

The LINE API is easy to implement and offers a well-focused set of core features, which keeps it simple. Maintaining this simplicity and ensuring stable operation are essential as more services become integrated with LINE in the future. In terms of customer understanding, combining attribute information held by LINE with information held by services will enable more detailed strategies.

### A message for those developing new services 

Using LINE APIs and SDKs can help reduce development workload. Moreover, by adopting LINE as your ID infrastructure, you can lower the hurdle for users to start using your service. Once users start using the service, you can turn them into loyal customers by continuing communication through your LINE Official Account. This is another important benefit. While different channels have their own characteristics, building your service around LINE can offer significant benefits.

---

## Related Links 

- [Classmethod, Inc. | LINE for Business](https://www.lycbiz.com/jp/partner/technology/line/classmethod/)
- [Classmethod, Inc.](https://classmethod.jp/english/)
- [CX ORDER](https://cxorder.jp/lp/)
