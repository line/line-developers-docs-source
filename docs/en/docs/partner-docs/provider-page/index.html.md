# Provider page

<!-- note start -->

**Use of optional functions requires an application**

Only corporate users who have submitted the required applications can use the functions described in this document. To use these functions with your LINE Official Account, contact your sales representative or contact [our Sales partners](https://www.lycbiz.com/jp/partner/sales/).

<!-- note end -->

## Overview 

A provider page is a list of the various services offered by the [Provider](https://developers.line.biz/en/glossary/#provider) on the LINE Platform. Providers can display the services they offer, such as LINE Official Account (Messaging API), LINE MINI App and LINE Login , on the provider page.

![provider page sample](https://developers.line.biz/media/partner-docs/provider-page-en.png)

## Provider page settings 

Only certified providers can configure and publish provider pages. For more information on certified providers, see [Certified provider](https://developers.line.biz/en/docs/line-developers-console/overview/#certified-provider).

You can configure your provider page from the **Provider page** tab on the [LINE Developers console](https://developers.line.biz/console/). The **Provider page** tab is displayed only if you are authorized to use the provider page function.

On the **Provider Page** tab, register your privacy policy URL and add the services you want to display on your provider page. You can add up to 100 services to a provider page. If the privacy policy URL is not yet registered, the registered services will not be displayed on Provider page.

<!-- tip start -->

**About LINE Official Account that can be added to your provider page**

The only LINE Official Account that can be added to your provider page are verified or [premium accounts](https://developers.line.biz/en/glossary/#premium-account). For more information about account types, see the [Account Types of LINE Official Account](https://www.linebiz.com/jp-en/service/line-official-account/account-type/) page on LINE for Business.

<!-- tip end -->

![provider page settings screen](https://developers.line.biz/media/partner-docs/provider-page-settings-en.png)

### Set the order in which services are displayed on the provider page 

From the **Provider page** tab on the [LINE Developers Console](https://developers.line.biz/console/), drag and drop each service up and down to reflect the order in which they are displayed on the provider page.

You cannot change the order of the service categories: LINE Official Account, LINE MINI App, and LINE Login. You can only change the order in which the services under each category are displayed.

### Provider page URL 

You can find the URL of your provider page (`https://provider.line.me/{ProviderID}`) under the **Provider page** tab on the [LINE Developers Console](https://developers.line.biz/console/).

## Sharing the your provider page URL with users 

When you share the URL of your provider page with users, the list of provider services offered is displayed to users.

- **LINE Official Account**: Share the link to the provider page in the rich menu or in the first message you send after being added as a friend.
- **LINE MINI App**: When users tap the [action button](https://developers.line.biz/en/docs/line-mini-app/discover/builtin-features/#action-button) in the LINE MINI App, an item labeled **About the service** will be displayed, allowing them to view the provider page.
- **LINE Login**: Share the link to the provider page on pages where you have set up a LINE Login button.

## Cautions on the common use of user IDs 

In principle, [LINE user data policy](https://terms2.line.me/LINE_Developers_user_data_policy?lang=ja) prohibits providers that offer multiple services on the LINE Platform from linking and sharing LINE user data obtained from each individual service. However, after publishing the provider page, if the following [Terms and conditions of use](https://developers.line.biz/en/docs/partner-docs/provider-page/#terms-and-conditions-of-use) are met, providers are allowed to link the LINE user data and use it in common.

Be aware that the provider, as the acquirer of the LINE user data, uses the information at the provider's own risk, in accordance with the relevant laws and regulations, and in a manner that doesn't negatively impact users.

### Terms and conditions of use 

As a provider, you must provide users with a link to the provider page and inform users that each service is provided by the same provider for each service that uses LINE user data in common.

In the case of Messaging API channels, observe the following.

- The contracted company and provider of the LINE Official Account must be the same, and the relationship between the two companies is not misleading to users.

Note that if you don't comply with the above rule, or if you are found to be operating your LINE account inappropriately, LY Corporation may recommend that you take corrective action or ban the use of LINE user data.
