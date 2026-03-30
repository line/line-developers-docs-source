# Technical case study of Smart Public Lab: LINE utilization strategy supporting administrative digital transformation

<!-- tip start -->

**About this page**

This page contains articles migrated from the LINE API Use Case site (closed on March 31, 2026) to the LINE Developers site. The page presents case studies of companies that have adopted the LINE Platform. Note that the content of the articles reflects the information available at the time of publication.

<!-- tip end -->

![Playnext Lab Inc.](https://developers.line.biz/media/messaging-api/technicalcase/playnext-lab/en/playnext-lab-logo.png)

**Playnext Lab Inc.**

Founded in 2016, we operate under the vision of “Building the future through technology and diversity,” and provide a wide range of services including smartphone games, HR tech services, and chatbot system development. In recent years, we have also focused on providing GovTech services that connect governments and citizens. Leveraging the development capabilities of a global engineer team with members from 17 countries, we strive to grow our own services and aim to support digital transformation for both society and our clients through cutting-edge technologies.

## Service overview and the challenges we want to solve 

Smart Public Lab is a service that supports the operational efficiency of municipal staff while enhancing resident satisfaction. Built around “Smart Public Lab with LINE SMART CITY GovTech Program,” which enables next-generation digital transformation of administrative services through LINE accounts in a simple and accessible manner, and online application services, Smart Public Lab serves as a comprehensive digital contact point for municipalities. It eliminates the need for in-person visits, waiting at service counters, and paper-based procedures, and is currently used through the official LINE accounts of approximately 100 local governments across Japan.

Smart Public Lab GovTech Program provides an extensive set of functions, including document and form creation, segmented information delivery with granular condition settings, advanced scenario-based chatbot messaging, calendar-based reservations for public facilities and events, a disaster mode optimized for emergency response, location-based spot search, and payment functions. These capabilities extend beyond those available through standard LINE Official Account features. The online application service of Smart Public Lab supports applications that require identity verification using My Number Cards, as well as online payments convenient for paying issuance fees and administrative charges. It also supports access to LGWAN (Local Government Wide Area Network), allowing use of existing government-issued computers and minimizing the burden of implementation. The Tourist Guide service of Smart Public Lab enables local governments to develop a tourism guide service that customizes spot search functions and utilizes content from tourism websites to deliver relevant information to non-resident users via tourism-specific LINE Official Accounts. Chatbots guide users from the LINE chat screen and enable spot recommendations tailored to different usage scenarios.

Based on the users’ current location or selected area, the service can display relevant facilities by category, such as history, food, or accommodation. Since it is linked with Google Maps, another appealing feature is that users can quickly check routes and detailed information for selected spots.

### Image 

![service-image](https://developers.line.biz/media/messaging-api/technicalcase/playnext-lab/en/playnext-lab-ui-img.png)

## System Overview 

![System architecture diagram](https://developers.line.biz/media/messaging-api/technicalcase/playnext-lab/en/playnext-lab-system-diagram.png)

### Improving administrative services using acquired data 

Through the administrative DX system, resident surveys can be shifted from paper to LINE, improving operational efficiency through data digitization. In addition, notifications for cancer screenings can be sent based on residents’ dates of birth, and appointments for cancer screenings can be made through LINE.\* By having residents register the types of information they wish to receive on LINE, information can be delivered to specific segments. As a result, LINE is widely used as a channel for communicating administrative information to residents across a broad range of age groups.

\*Behavioral data linked to LINE accounts is collected and used only after obtaining user consent.

### Background to selecting AWS for system construction 

We adopted Amazon Web Services (hereinafter “AWS”) for building the administrative DX systems. Because administrative services are directly linked to citizens’ daily lives, systems must operate reliably at all times and provide scalability to handle sudden spikes in access. AWS delivers high performance that meets these requirements. In addition, security is one of the most critical considerations when handling administrative data. AWS offers robust security measures and abundant compliance certifications, providing a reliable environment for the secure management of confidential information.

Ease of operation and maintenance was also one of the factors in the selection. AWS provides a broad set of tools and services that streamline management and maintenance, reducing operational burden and enabling prompt service improvements. We have extensive experience using AWS and have accumulated the expertise needed to make full use of the platform. We adopted AWS for these reasons. We regularly review the infrastructure's running costs using AWS Billing and Cost Management, and analyze trends such as each user's usage frequency. We use GitHub for source code management during development because it is easy to manage.

### Future outlook for municipal digital service counters 

As part of administrative DX initiatives, Smart Public Lab aims to expand the range of functions that address challenges faced by residents and municipal staff, thereby broadening the scope of support offered by municipal digital service counters.

In January 2023, we launched an online application service that enables My Number Card authentication on LINE Official Accounts. In Okawa City, Fukuoka Prefecture, 96% of applications for childbirth and childcare support benefits were received through its LINE official account (survey by PlayNext Lab Inc.), providing residents with a highly user-friendly system. While highly functional systems often become more difficult to operate, Smart Public Lab is designed specifically for local governments. We remain committed to providing services with a strong focus on UI and UX, ensuring that both residents and staff can continue to use the system in an intuitive and simple way.

### Requests for LINE API development 

We felt that the availability of APIs that allow the retrieval of users’ location information and “Read” status would further expand the range of services that can be offered on LINE.

### A message for those developing new services 

One of the greatest advantages of LINE is its overwhelming user base and high active user rate, which allows us to reach users across all age groups. By utilizing LINE authentication, the reservation feature of Smart Public Lab eliminates the need for user registration.

In fact, 54% of consultation reservations (survey by PlayNext Lab Inc.) have been made via LINE. Leveraging the LINE API has helped us expand our user reach and reduce user drop-offs, enabling the development of a system that contributes to lower costs associated with marketing and growth hacking.

---

## Related links 

- [Smart Public Lab](https://www.playnext-lab.co.jp/govtech/)
