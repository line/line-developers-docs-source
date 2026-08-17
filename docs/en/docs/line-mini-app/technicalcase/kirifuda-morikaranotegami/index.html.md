# Nature conservation through play: A technical case study of Letters from the Forest launched on the LINE MINI App

<!-- tip start -->

**About this page**

This page contains articles migrated from the LINE API Use Case site (closed on March 31, 2026) to the LINE Developers site. The page presents case studies of companies that have adopted the LINE Platform. Note that the content of the articles reflects the information available at the time of publication.

<!-- tip end -->

![KIRIFUDA Inc.](https://developers.line.biz/media/line-mini-app/technicalcase/kirifuda-morikaranotegami/en/kirifuda-morikaranotegami-logo.png)

**KIRIFUDA Inc.**

We are KIRIFUDA Inc. (hereinafter referred to as "KIRIFUDA"), a solution provider and system developer supporting the real-world adoption of blockchain, with a mission to "create a society where creativity and value circulate through Web3". We provide one-stop services, from business strategy consulting to system development, for companies in Japan and abroad, helping them build business foundations for the Web3 era.

## Service overview: "Letters from the Forest", a LINE MINI App for logging environmental actions 

"Letters from the Forest" is a LINE MINI App for logging environmental actions, jointly introduced by Tokyu Land Corporation and KIRIFUDA to the Resort Town Tateshina in Nagano Prefecture. Visitors engage in environmentally conscious actions—such as bringing their own personal toiletries to reduce consumption, skipping linen changes, or participating in forest conservation programs to deepen their knowledge. These actions are represented as NFTs issued on the blockchain. When the user scans the wood-carved QR codes installed on-site, the LINE Official Account is automatically added as a friend and the LINE MINI App launches. Tapping the "Receive NFT" button activates an animation that places a digital stamp in the user account. Through the rich menu of the LINE Official Account, users can access their My Page at any time to view collected stamps and redeem them for coupons usable within the facility once they reach the required number. This design gamifies environmental contributions by adopting elements of Japan’s "poi-katsu" (reward point-collecting) culture.

Tokyu Land Corporation has made company-wide efforts to invest in decarbonization and engage in forest conservation initiatives. Notably, the forests of Resort Town Tateshina are regional resources that must be sustained by proper forest thinning and conservation management. However, simply asking visitors to "act in an environmentally friendly way" did little to motivate proactive participation. Therefore, digital content that combines "learning and fun" was needed. Furthermore, these actions may eventually be aggregated into carbon credits. In doing so, it is essential to maintain authentic records of each visitor’s environmental contributions. To address this need for verifiable proof, KIRIFUDA proposed NFTs as a tamper-resistant method to record individual action logs. With NFTs, visual content such as digital stamps can be integrated alongside activity data, creating an engaging experience where visitors enjoy collecting stamps while gaining a tangible sense of their own environmental contribution. From a corporate standpoint, this system ensures that data is securely stored and reliably tracked for this project.

### Image 

![service-image](https://developers.line.biz/media/line-mini-app/technicalcase/kirifuda-morikaranotegami/en/kirifuda-morikaranotegami-ui-img.gif)

## System overview 

![System configuration diagram](https://developers.line.biz/media/line-mini-app/technicalcase/kirifuda-morikaranotegami/en/kirifuda-morikaranotegami-system.png)

### Technical configuration of "Letters from the Forest": Seamless integration of LIFF and blockchain 

For the client-side, we used LIFF as the base, while on the server-side, we implemented user authentication linked with the LINE Login infrastructure, as well as messaging functions via the Messaging API.  
We used Web3Auth for wallet generation, and Alchemy for minting and querying NFTs. Minting processes are handled via asynchronous queues using Google Cloud Tasks. To ensure a seamless UX unaffected by blockchain-specific latency, all intensive backend processes are sent to the queue, allowing users to proceed without interruption. By leveraging LINE Login sessions, the system is designed to securely track each user’s environmental activity history and NFT holdings.

To run blockchain operations within the LINE MINI App environment, it was essential to strictly adhere to the specific initialization flow of LIFF. Since a LINE MINI App loads within an embedded view inside LINE, it involves a multi-stage initialization process. This requires a design that triggers blockchain operations—such as wallet generation and NFT minting, which require their own initialization separate from LIFF—precisely when all necessary conditions are met. Even a slight timing error could lead to initialization failure or result in a blank screen for users, severely compromising the user experience. Therefore, the implementation demanded meticulous precision.

Furthermore, unlike a standalone native app, the true value of a LINE MINI App lies in its seamless integration with existing features such as chat screens and rich menus. For instance, we had to meticulously design interaction scenarios focused on the LINE user flow—such as sending a confirmation via the Messaging API immediately after an NFT is minted, or guiding users from a button in the chat room to launch the MINI App and mint an NFT. Our greatest challenge was not merely integrating technologies, but crafting an experience that feels natural to the user. This required continuous ingenuity across both front-end engineering and product planning.

### Initial feedback and operational reality 

Located in a forested area, Resort Town Tateshina has some locations with limited mobile carrier coverage, but this did not significantly hinder the user experience. Regarding operations, KIRIFUDA managed the LINE Official Account entirely, asking local staff only to set up the wood-carved QR codes and provide basic guidance to visitors. Since the process was very similar to existing resort reward programs, both users and staff were able to enjoy the experience without any confusion.

Regarding areas for improvement identified after the launch, some users found the process of redeeming their NFT stamps for coupons confusing. We are currently optimizing the UI and refining the instructions on the reward exchange screen to make the redemption process more intuitive and seamless. On the other hand, we have received a great deal of positive feedback, with users noting that they could "receive items without even being aware they were NFTs", that "the stamp designs are so cute that they make me want to collect them", and that "it’s fun to learn about the environment while playing". The project was also featured on a TV Tokyo program, and Tokyu Land Corporation has highly praised the way visitors gained a genuine sense of "contributing to the environment without even realizing it".

### Future outlook: Building a cross-sector environmental contribution program 

We aim to expand the environmental contribution coupons beyond Tateshina’s "Letters from the Forest" to other urban facilities owned by Tokyu Land Corporation. By building a system where the proof of forest contribution can be redeemed at various locations—such as SHIBUYA FUKURAS, hotels in Daikanyama, or other commercial facilities—we can create a two-way flow of customer engagement between resorts and urban locations. For instance, an eco-friendly action in a Tokyo cafe, such as using a reusable bag, could earn small benefits redeemable in Tateshina. This group-wide incentive design aims to continuously encourage eco-friendly behavior and enhances sustainability-focused user experience across the entire Tokyu Group ecosystem.

This service, which integrates the LINE MINI App with NFT technology, has applications beyond environmental contributions and can be adapted for any loyalty program. In recent years, there has been growing momentum in fan-driven industries—such as music and sports—to record and visualize fan participation and social sharing through NFTs. By combining the personalized, one-on-one communication feature of LINE Official Accounts with NFTs that can be sold and collected as digital merchandise, we can achieve deeper fan engagement than conventional e-commerce or social media platforms. Moving forward, KIRIFUDA aims to expand technical validation and partnerships in this area, establishing a new standard for Web3 initiatives that seamlessly bridge the digital and physical worlds on the LINE Platform.

### A message for those considering using LINE API 

Finally, for developers and planners, the greatest advantage of leveraging the LINE APIs is the ability to seamlessly reach over 97 million LINE users in Japan as potential users through a single platform. Beyond the standard LINE Official Accounts and LINE MINI Apps, the platform is rapidly evolving with features that bridge online and offline experiences, such as eKYC integration and push notifications via LINE Beacon. As this project demonstrates, integrating blockchain and NFTs with LINE can significantly lower the barrier to entry for Web3—provided the experience is designed to be intuitive for users to start. At KIRIFUDA, we have designed services that merge LINE’s diverse APIs with blockchain technology. If you have any ideas about what you want to achieve with LINE, or a vision for realizing a new type of user experience using Web3, please feel free to reach out to us. Let’s work together to create the next generation of user experiences on the LINE Platform.

---

## Related links 

- [KIRIFUDA Inc.](https://kirifuda.io/)
