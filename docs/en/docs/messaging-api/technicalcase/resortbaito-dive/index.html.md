# A case study on the development of \"Resort Baito Dive\" to enhance temporary staff satisfaction

<!-- tip start -->

**About this page**

This page contains articles migrated from the LINE API Use Case site (closed on March 31, 2026) to the LINE Developers site. The page presents case studies of companies that have adopted the LINE Platform. Note that the content of the articles reflects the information available at the time of publication.

<!-- tip end -->

![Dive Inc.](https://developers.line.biz/media/messaging-api/technicalcase/resortbaito-dive/en/resortbaito-dive-logo.png)

**Dive Inc.**

Dive Inc. is a startup whose core business is providing staffing services for tourist facilities, mainly through "resort baito" (short-term resort jobs). We contribute to addressing the critical labor shortage faced by the tourism industry. Our service website has more than 40,000 registered users annually, and the number of LINE friends has surpassed 150,000. By creating employment opportunities that connect workers with local communities, we are committed to regional revitalization and the growth of the tourism industry.

## Service overview and issues to address 

At Dive Inc., our resort part-time resort staffing service, “Resort Baito Dive”, uses a LINE Official Account. Through the LINE Official Account, temporary staff communicate daily with sales representatives and customer support. These interactions cover a wide range of topics, from day-to-day concerns during assignments to consultations about job searches. During peak months, the number of messages sent reaches approximately 63,000 per month. We strive to handle each interaction with care, and as a result, we have received highly positive feedback from temporary staff.

### Image 

![service-image](https://developers.line.biz/media/messaging-api/technicalcase/resortbaito-dive/en/resortbaito-dive-ui-img.png)

![service-cms-image](https://developers.line.biz/media/messaging-api/technicalcase/resortbaito-dive/en/resortbaito-dive-ui-img-2.png)

## System Overview 

![System architecture diagram](https://developers.line.biz/media/messaging-api/technicalcase/resortbaito-dive/en/resortbaito-dive-system.png)

### Technologies that support Resort Baito Dive and their impacts 

Our infrastructure is built on AWS. The front-end is delivered using CloudFront and S3, while the back-end API is built using ALB (Application Load Balancer) and ECS on Fargate.

The Webhook that receives chat messages from users is designed using a combination of API Gateway and SQS (Simple Queue Service), with subsequent processing handled by Lambda. This architecture ensures reliable reception of user messages. We have adopted Aurora Serverless v2 for the database, enhancing operational efficiency through automated provisioning. Furthermore, these infrastructure configurations are managed as code using AWS CDK, and deployments are automated with GitHub Actions. As our development language, TypeScript is used consistently across the front-end, back end, and infrastructure to reduce engineers’ cognitive load. This unified approach enables efficient and high-quality system operations.

Following the release, responses to chat messages received between the end of the previous business day and the start of the next were completed by the morning, whereas previously this work extended into the afternoon. Additionally, enhancements to search functionality reduced the time required for routine checks for missed chat responses conducted several times a day—from approximately one hour per check to around 30 minutes—resulting in substantial improvements in operational efficiency.

### Future outlook for Resort Baito Dive 

With chat data now accumulated within the company, we plan to utilize this data for analytical purposes to further improve user satisfaction.

### Requests for the LINE API 

Because the API for retrieving user IDs of members in group chats and multi-person chats can only be executed by verified accounts, we encountered difficulties testing with development accounts. We would appreciate it if, through a special application process for testing purposes, this API could also be made available to unverified accounts.

- [Get group chat member user IDs](https://developers.line.biz/en/reference/messaging-api/#get-group-member-user-ids)

- [Get multi-person chat member user IDs](https://developers.line.biz/en/reference/messaging-api/#get-room-member-user-ids)

### A message for those developing new services 

When you need to receive user messages such as chats without fail, an effective approach is to place messages received via a Webhook into a queue. Separating message reception from processing in this way creates a scalable architecture.

---

## Related Links 

- [Dive Inc.](https://resortbaito-dive.com/)
- [Development Company: Classmethod, Inc.](https://classmethod.jp/)
