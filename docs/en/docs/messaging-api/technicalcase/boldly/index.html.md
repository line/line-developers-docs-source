# A LINE MINI App case study of an on-demand autonomous bus reservation system

<!-- tip start -->

**About this page**

This page contains articles migrated from the LINE API Use Case site (closed on March 31, 2026) to the LINE Developers site. The page presents case studies of companies that have adopted the LINE Platform. Note that the content of the articles reflects the information available at the time of publication.

<!-- tip end -->

![BOLDLY Inc.](https://developers.line.biz/media/messaging-api/technicalcase/boldly/en/boldly_logo.webp)

**BOLDLY Inc.**

BOLDLY is working toward a world where everyone can travel freely, affordably, and safely. By leveraging IoT and autonomous driving technologies, BOLDLY collaborates with local transportation providers and vehicle developers around the globe to implement sustainable public transportation solutions.

## The service provider’s thoughts on developing the system 

We design our autonomous buses to function as a “horizontal elevator” for the community.

This solution increases convenience for the residents by providing low-speed and frequent mobility services within a limited area.

In a town like Sakai-machi in Ibaraki Prefecture, where large areas lack access to public transportation, running buses on fixed schedules to cover the entire area is not practical from a cost and efficiency perspective.

So, we decided to create a service that works like a taxi—something you can easily call whenever you need it. While many on-demand ride dispatch applications already exist, we chose to develop this system on the LINE Platform, which has 92 million users (according to LINE Corporation research; LINE app monthly active users as of the end of June 2022). Our hope is that if elderly residents, who may not be familiar with smartphones, become comfortable using LINE, they will gain more than just a bus reservation tool; they will gain a way to stay in touch with family and friends. We believe that if people can call an autonomous bus from the LINE app they already use, instead of having to learn how to use a new app, it will give them the confidence to go out more freely. This is also why we named the LINE Official Account after the character "Sakai ARMA." We want people to be able to call the autonomous bus as if they are talking to a friend.

### Image 

![service image](https://developers.line.biz/media/messaging-api/technicalcase/boldly/en/boldly_screenshot.webp)

## System overview 

![System architecture diagram](https://developers.line.biz/media/messaging-api/technicalcase/boldly/en/boldly_system_diagram.webp)

### Optimizing operations by migrating to AWS 

Since our existing in-house systems were already running on AWS, we implemented the infrastructure for the LINE reservation system on the same platform.

While the initial prototype utilized tools like Google Apps Script, we migrated the entire infrastructure to AWS as we moved toward full-scale service development and operation, to align the new service’s architecture and data management with our existing systems.

By migrating our infrastructure, we have also been able to optimize operations, including integrating build pipelines with existing systems.

### Running costs of cloud infrastructure 

In addition to API-based integration, Dispatcher relies on multiple communication channels, including the transmission of video and audio from onboard devices and the real-time exchange of telemetry data via WebSocket.

For this reason, from the early stages of service development, we had a clear intention to use cloud infrastructure to reduce the costs associated with infrastructure management and maintenance. In addition, as the number of connected vehicles increases and communication volumes are expected to grow accordingly, we leverage cloud infrastructure that can be easily scaled in line with service growth, allowing us to manage resources efficiently.

### Exploring a boarding authentication system using facial recognition with data registered through LINE 

We are considering an update to the passenger authentication process at boarding.

Currently, passengers can board the bus by presenting an ID issued at the time of reservation to the driver. However, as autonomous buses move toward driverless operation, this approach has clear limitations.

To address this challenge, we are developing a passenger authentication system based on facial recognition. By using cameras at the time of boarding, the system verifies whether the passenger is the same person who made the reservation, based on facial data registered through LINE. From an operational efficiency perspective, we are also considering an update to the reservation system that would enable ride-sharing.

### A message for those developing new services 

In our service, users are required to complete everything themselves—from vehicle reservations to boarding authentication. For B2C services like this, developers often face challenges related to customer communication and customer list management. The LINE Platform offers a wide range of features to address these challenges, including communication through chat and customer management via friend registration. By leveraging these features in our reservation system, we were able to proceed with development without encountering major obstacles. If you are building a B2C service, we encourage you to consider using the LINE Platform.

---

## Related links 

- [BOLDLY Inc.](https://www.softbank.jp/drive/)
