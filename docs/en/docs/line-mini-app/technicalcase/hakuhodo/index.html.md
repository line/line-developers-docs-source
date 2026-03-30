# A development case study of “PoHUNT,” a digital revitalization initiative for mobility and health promotion in Asahi Town, Toyama Prefecture

<!-- tip start -->

**About this page**

This page contains articles migrated from the LINE API Use Case site (closed on March 31, 2026) to the LINE Developers site. The page presents case studies of companies that have adopted the LINE Platform. Note that the content of the articles reflects the information available at the time of publication.

<!-- tip end -->

![HAKUHODO Inc.](https://developers.line.biz/media/line-mini-app/technicalcase/hakuhodo/en/hakuhodo_logo.webp)

**HAKUHODO Inc.**

Founded in 1895, Hakuhodo Inc. continues to pursue innovations every day based on our philosophies of “Sei-katsu-sha Insight” and ”Commitment to Partnership,” which remain unchanged to this day. Teams of highly creative professionals work collaboratively to support clients in solving challenges across a broad range of fields—not only in advertising, but also in management, business development, and social issues. In recent years, we have also focused on regional revitalization and the promotion of digital transformation, launching projects dedicated to addressing social issues.

## The service provider’s thoughts on developing the system 

Many local governments in Japan are facing the issue of transportation operators withdrawing due to aging populations and depopulation. As residents’ transportation options decrease, outings become less frequent, leading to various problems such as the decline of the town's economic activity, fewer opportunities for communication, and worsening health among the elderly. To address these issues, Asahi Town in Toyama Prefecture developed “PoHUNT,” a community revitalization initiative designed to encourage mobility. On the LINE MINI App, users can earn points by scanning QR codes installed at commercial facilities and viewing health-related information. These points can then be used to enter lucky draws or participate in regional competitions, creating a system that gamifies mobility and health-related activities. By integrating with "Nokkaru Asahimachi," a ride-sharing public transportation service launched in 2020, the initiative simultaneously provides transportation options and generates transportation demand, with the aim of revitalizing the town.

### Image 

![](https://developers.line.biz/media/line-mini-app/technicalcase/hakuhodo/en/hakuhodo_screenshot.webp)

## System overview 

![System architecture diagram](https://developers.line.biz/media/line-mini-app/technicalcase/hakuhodo/en/hakuhodo_system_diagram.webp)

### Using AWS for its comprehensive functionality and ease of maintenance 

We adopted anybot, a service provided by Evolany Co., Ltd., to implement PoHUNT. The service infrastructure primarily uses AWS (Amazon Web Services) EC2 for the following two reasons.

**Comprehensive functionality**

- AWS enables smooth integration when adding core features to the service, such as databases, notification functions (email and SMS), and storage.

**Ease of infrastructure maintenance**

- By utilizing cloud infrastructure, maintenance processes can be easily automated and managed.

### Ongoing cloud infrastructure and operational costs 

With traditional on-premises infrastructure management, various costs arise, including equipment expenses and physical space. In contrast, cloud infrastructure (AWS) uses a pay-as-you-go model, where costs are incurred only for what is used, significantly reducing running costs. Additionally, the infrastructure can be scaled up or adjusted easily and quickly in line with service size and scale, allowing for running costs to be controlled at a reasonable level.

### Operational tools supporting the infrastructure 

CloudWatch (Monitoring) / Zabbix (Monitoring)

### Linking with the municipality's LINE Official Account to revitalize the entire town 

We also distributed resident surveys via PoHUNT as part of the town’s development efforts, and the high response rate validated its effectiveness as a town development platform. Based on these results, we plan to promote municipal digital transformation initiatives centered on the point features of PoHUNT. By linking with the municipality's LINE Official Account and rolling out initiatives on a regular basis, we aim to apply the solution not only to commercial and health-related areas but also across a wide range of fields, ultimately revitalizing the entire town. Additionally, based on the insights gained from this case, we are also considering applying them to marketing initiatives for other municipalities and companies.

### A message for those developing new services 

We see advantages in not having to develop separately for each OS or version, which keeps initial development and operational workloads low. Moreover, since Hakuhodo's primary role is service development rather than system development, we design our services with a strong focus on how to make them truly usable for users, as well as how to sustain them within a limited budget. For companies and organizations that value such perspectives, the fact that LINE is used by a wide range of age groups and that there is no cost to operate the account is highly attractive.

---

## Related links 

- [Toward a “Community Revitalization DX” That Everyone Can Participate In — A New Platform for Regional Co-Creation, “PoHUNT” (Part 1)](https://seikatsusha-ddm.com/article/12588/)
- [Toward a “Community Revitalization DX” That Everyone Can Participate In — A New Platform for Regional Co-Creation, “PoHUNT” (Part 2)](https://seikatsusha-ddm.com/article/12596/)
- [Nokkaru](https://www.hakuhodo.co.jp/news/info/94130/)
- [HAKUHODO Inc.](https://www.hakuhodo-global.com/)
