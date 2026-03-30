# Introducing infrastructure as low code for LINE-based service development case study on improving development efficiency with CNAP

<!-- tip start -->

**About this page**

This page contains articles migrated from the LINE API Use Case site (closed on March 31, 2026) to the LINE Developers site. The page presents case studies of companies that have adopted the LINE Platform. Note that the content of the articles reflects the information available at the time of publication.

<!-- tip end -->

![SoftBank Corp.](https://developers.line.biz/media/messaging-api/technicalcase/softbank/en/softbank-logo.webp)

**SoftBank Corp.**

SoftBank Corp. operates a wide range of businesses, including telecommunications, cloud security, AI, and robotics. SoftBank Corp. aims to become “the company needed most by people around the world” by contributing to happiness for everyone through the Information Revolution, and will aim to realize an ideal society where everyone can live conveniently, comfortably, and safely by building on the business foundation we have established and leveraging the power of digital technologies.

## What is CNAP and how does it shorten application development period? 

Conventional application development has faced the following challenges.

- Development and infrastructure operations were handled by separate teams, so change requests had to be submitted for each release, which caused the release process to take longer.
- Development and execution environments, design practices, and policies lacked consistency, making it difficult to ensure proper governance.
- Operational tasks relied heavily on individuals and were not standardized, posing a risk of operational errors.

These challenges can be addressed by following DevOps principles, such as automating build and operation processes and standardizing system configurations. However, it is extremely challenging to prepare such an environment in-house, as it involves a high learning cost, requires significant time to build technical expertise, and demands ongoing maintenance to keep up with frequent version updates. The Cloud Native Application Platform (CNAP) is a service that provides a standardized and automated platform, which consolidates the DevOps know-how practiced by SoftBank. CNAP offers low-code configuration packages in which designs are standardized and build processes are automated. By maintaining and managing these packages, clients can overcome conventional challenges and focus on their core development. In this article, we introduce a case study on the use of CNAP in developing an inquiry management system using the LINE Messaging API.

### Image 

![roadmap](https://developers.line.biz/media/messaging-api/technicalcase/softbank/en/softbank-overview-1.webp)

![cnap-benefits](https://developers.line.biz/media/messaging-api/technicalcase/softbank/en/softbank-overview-2.webp)

![about-cnap](https://developers.line.biz/media/messaging-api/technicalcase/softbank/en/softbank-overview-3.webp)

![service-image](https://developers.line.biz/media/messaging-api/technicalcase/softbank/en/softbank-overview-4.webp)

## System overview 

![System architecture diagram](https://developers.line.biz/media/messaging-api/technicalcase/softbank/en/softbank-system-diagram.webp)

### Automated deployment to Azure environments using CNAP 

All infrastructure, from the front end to the back end, is built on Azure. We provide managed service provider (MSP) services that support public cloud platforms, including Microsoft Azure, Google Cloud, and Amazon Web Services (AWS). By developing these services in-house, we have built broad expertise in public cloud platforms. Among these, Azure is our most experienced public cloud platform as we began providing MSP services early, starting in October 2019. Thus, we chose Azure for this project. CNAP allows users to deploy and manage not only Kubernetes environments but also related resources in a unified manner by simply pushing YAML files that define system configurations in an abstracted form to a Git repository. Google Cloud and AWS are also supported.

### Performance and cost optimization using Azure Kubernetes Service 

As the application runs on a Kubernetes cluster, Azure Kubernetes Service (AKS) accounts for the largest portion of the overall costs. Also, since multiple pods can be placed on each node in the cluster, it is possible to host multiple services together as long as node resources are available. In addition, Kubernetes enables dynamic scaling based on workload. As a result, the system allows performance optimization for each service based on its workload, while minimizing costs.

### Components of CNAP, including AKS 

CNAP is a platform that supports automation of infrastructure operations through tightly integrated OSS components built around managed services such as AKS. We adopt Helm as the application packaging platform and use Flux CD as the continuous delivery (CD) platform to implement GitOps. In addition, we use Prometheus and Grafana for monitoring application metrics, logs, and errors. Based on the know-how accumulated through our own application development and operations, CNAP offers OSS components with a proven track record that come with recommended configurations, allowing clients to manage, operate, and monitor their systems on a self-service basis.

### Future goals 

By abstracting away the application infrastructure layer and providing managed platforms, CNAP offers an environment that allows clients to focus on application development. Through CNAP, we believe we can support a wide range of application development projects, including applications using LINE APIs. We will continue to expand our services and strive to better meet our clients' needs.

### A message for those developing new services 

As mentioned earlier, LINE has an exceptionally large active user base. As a result, services offered on the LINE Platform can reach a much broader range of end users. LINE also offers a rich set of APIs, allowing developers to create a wide variety of applications through different combinations and creative ideas. Please consider CNAP as an option when developing applications.

---

## Related links 

- [Cloud-Native Application Platform（CNAP）](https://www.softbank.jp/biz/services/platform/msp-service/cnap/)
- [MSP Service](https://www.softbank.jp/biz/services/platform/msp-service/)
- [SoftBank Corp.](https://global.tm.softbank.jp/en/)
