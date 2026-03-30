# A case study of developing a LINE bot to handle inquiries related to relocation and settlement

<!-- tip start -->

**About this page**

This page contains articles migrated from the LINE API Use Case site (closed on March 31, 2026) to the LINE Developers site. The page presents case studies of companies that have adopted the LINE Platform. Note that the content of the articles reflects the information available at the time of publication.

<!-- tip end -->

![heptagon inc.](https://developers.line.biz/media/messaging-api/technicalcase/heptagon/en/heptagon-logo.webp)

**heptagon inc.**

As an AWS Advanced Consulting Partner, we provide support for cloud adoption, primarily to companies based in the Tohoku region of Japan. We are also actively engaged in advancing digital transformation (DX) among companies in Tohoku. By collaborating with companies that seek growth through the adoption of advanced technologies and new mindsets, heptagon inc. contributes to productivity enhancement, operational improvement, and the introduction of new working styles.

## The service provider’s thoughts on developing the system 

During the COVID-19 pandemic, Misawa City approached us with a request to build an online system that would allow people to consult about relocation and settlement, as it was no longer possible to hold in-person events. Because the project began partway through the fiscal year, the budget was limited, making it necessary to develop a system that could be used by as many people as possible while minimizing the operational burden on city staff.

To meet these requirements, we quickly agreed on the following development approach:

- Use LINE, a platform already widely used by the public, as the interface
- Provide automated responses using AI for anticipated inquiries
- Adopt a serverless architecture that allows for a small start in order to keep operating costs low
- Reduce development person-hours by leveraging cloud-native technologies such as APIs and SaaS provided by cloud vendors, rather than building everything from scratch
- Enable post-launch operations to be handled primarily by city staff without relying on external vendors

We saw this project as an ideal opportunity to apply our technical strengths to support a local municipality, and we therefore decided to move forward with the project.

### Image 

![service-image](https://developers.line.biz/media/messaging-api/technicalcase/heptagon/en/heptagon-screenshot.webp)

## System overview 

![System architecture diagram](https://developers.line.biz/media/messaging-api/technicalcase/heptagon/en/heptagon-system-diagram.webp)

### Achieving minimal development hours and operating costs with AWS 

We positioned AWS, our core area of expertise, at the center of the API backend. As management interfaces, we adopted Azure QnA Maker, which makes it easy to build an AI chatbot, and Google Sheets, which municipal staff were already familiar with. To ensure the project remained within the approved budget, development hours were kept to a minimum, and services were combined to prevent usage fees and operating costs from increasing after the service launch.

### Ongoing cloud infrastructure and operational costs 

The backend computing environment employs a serverless architecture centered on AWS Lambda. Email delivery, databases, and storage are all provided through fully managed, pay-as-you-go services. This approach eliminates fixed infrastructure costs and keeps ongoing operating costs low. At the current scale, many of these services are operating within their respective free tiers.

### Operational tools supporting the infrastructure 

Serverless Framework (deployment and configuration management) / CloudWatch (monitoring) / Zabbix (monitoring)

### Solving local challenges with the LINE API 

Although LINE Official Accounts are already widely used in regional areas, leveraging the LINE API greatly expands the scope of services that can be provided. We aim to address challenges faced by regional communities through services that utilize LINE.

### A message for those developing new services 

By leveraging the LINE ecosystem, developers can provide users with an easy-to-use and familiar interface while significantly reducing development hours. Furthermore, integrating LINE with a company’s core competencies creates greater opportunities to deliver services that are easily accessible to a wide audience. We believe that including LINE as one of the development options can be a strong strategic advantage.

---

## Related links 

- [heptagon inc.](https://heptagon.co.jp/)
