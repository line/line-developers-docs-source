# Use audiences

Audiences help you to apply advanced targeting. For example, you can target a group of users who read your message or clicked a URL in a message.

<!-- note} start -->

**To use Identifiers for Advertisers (IFA)**

You can use IFAs to specify recipients, but this is only available to corporate users who submit an application form. To use IFA with your LINE Official Account, contact your sales representative or contact [our Sales partners](https://www.lycbiz.com/jp/partner/sales/).

<!-- note} end -->

## Create an audience 

You can use the Messaging API to create audiences. Supported audience types are:

| Audience | Description |
| --- | --- |
| [Audience for uploading user IDs](https://developers.line.biz/en/reference/messaging-api/#create-upload-audience-group) | A set of users specified with [user IDs](https://developers.line.biz/en/glossary/#user-id) or IFA (Identifier For Advertisers) |
| [Message click audience](https://developers.line.biz/en/reference/messaging-api/#create-click-audience-group) | A set of users who clicked a URL in a message sent |
| [Message impression audience](https://developers.line.biz/en/reference/messaging-api/#create-imp-audience-group)  | A set of users who read a message sent |

You can't create the following types of audiences with the Messaging API:

- Chat tag audience
- Friend path audience
- Reservation audience
- Rich menu impression audience
- Rich menu click audience
- Web traffic audience (LINE Tag)
- Web traffic audience (Tracking Tag)
- App event audience
- Video view audience
- Image click audience
- LINE Beacon Network ad impression audience

<!-- note start -->

**Limit on concurrent operations**

For user ID based audiences, the number of concurrent endpoint operations is limited per audience ID (`audienceGroupId`). This limitation is applied on creating an audience for uploading user IDs and adding user IDs to an audience. For more information, see [Limit on the number of concurrent operations](https://developers.line.biz/en/reference/messaging-api/#limit-on-the-number-of-concurrent-operations).

<!-- note end -->

## Use audiences 

You can use audiences to send narrowcast messages. For more information, see [Send narrowcast messages](https://developers.line.biz/en/docs/messaging-api/sending-messages/#send-narrowcast-message).

## Share audiences 

The Messaging API and the [LINE Official Account Manager](https://manager.line.biz/) can use the audiences created for the same LINE Official Account with each other. There are no initial settings required to use audiences with each other.

If you want to use audiences between the Messaging API and tools other than the LINE Official Account Manager (such as the [LINE Ads Manager](https://admanager.line.biz/)), you will need to set up audience sharing. For more information about how to share audiences, see [Share your audience in Business Manager](https://developers.line.biz/en/docs/messaging-api/using-audience/#audience-sharing-business-manager).

| Tool that creates audience | Tool that uses audience | Availability of audience |
| --- | --- | --- |
| Messaging API | LINE Official Account Manager | ✅ |
| LINE Official Account Manager | Messaging API | ✅ |
| Messaging API | Tools other than LINE Official Account Manager | ✅ \*1 |
| Tools other than LINE Official Account Manager | Messaging API | ✅ \*1 |

\*1 Available if you share the audience in the Business Manager.

### Share your audience in Business Manager 

The [Business Manager](https://data.linebiz.com/solutions/business-manager) allows you to share specific audiences across multiple services (such as the LINE Ads Manager) and use the audiences with each other.

You can share audiences between Messaging API channels under the same provider by using the audience sharing function in the Business Manager. However, only verified accounts and [premium accounts](https://developers.line.biz/en/glossary/#premium-account) can set audience sharing in the Business Manager.

You can get data of the shared audience in Business Manager by using the following endpoints:

- [Get a list of shared audiences in Business Manager](https://developers.line.biz/en/reference/messaging-api/#get-shared-audience-list)
- [Get shared audience data in Business Manager ](https://developers.line.biz/en/reference/messaging-api/#get-shared-audience)

For more information on how to share audiences, see [Sharing Resources](https://data.linebiz.com/business-manager/manual/bmmaniyuarushare003) (only available in Japanese) in the Business Manager manual.

## Audience specification 

The audience specification is as follows.

| Property | Specification |
| --- | --- |
| Number of audiences per channel | 1,000 at maximum |
| Retention period | 180 days (15,552,000 seconds) at maximum |
| Number of user IDs or IFAs uploadable per request to make an audience | <ul><li>JSON: 10,000 at maximum</li><li>File: 1,500,000 at maximum</li></ul> |
| Number of users per audience | <ul><li>Audience for uploading user IDs: No limit</li><li>Message click audience: Minimum 50</li><li>Message impression audience: Minimum 50</li></ul> |
| Time limit to create a retargeting audience[^retargeting-audiences]<br />after you send a message | 60 days (5,184,000 seconds) at maximum |

[^retargeting-audiences]: This applies only on message click audience and message impression audience

For more information on narrowcast message restrictions, see [Restrictions on sending messages using attributes and audiences](https://developers.line.biz/en/reference/messaging-api/#send-narrowcast-message-restrictions) in the Messaging API reference.
