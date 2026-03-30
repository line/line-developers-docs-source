# Log in to the LINE Developers Console

To log in to the [LINE Developers Console](https://developers.line.biz/console/), you need your [Business ID](https://help2.line.me/business_id/web/?lang=en&contentId=20011264) and developer account.

This page explains how to log in to the LINE Developers Console, create a developer account, and link your Business ID with your LINE account.

## Log in to the LINE Developers Console 

To log in to the LINE Developers Console, click the **[Log in to Console](https://developers.line.biz/console/)** button in the top-right corner of the [LINE Developers site](https://developers.line.biz/).

![Click Log in to Console](https://developers.line.biz/media/line-developers-console/login-account-02-en.png)

The Business ID login screen will appear. Choose your login method and log in. You can log in to Business ID with any of the following accounts:

- [LINE account](https://developers.line.biz/en/docs/line-developers-console/login-account/#line-account)
- [Business account](https://developers.line.biz/en/docs/line-developers-console/login-account/#business-account)
- [Yahoo! JAPAN ID](https://developers.line.biz/en/docs/line-developers-console/login-account/#yahoo-japan-id) (Only available in Japan)

For more information about the difference between login methods, see [Business ID login methods](https://help2.line.me/business_id/web/?lang=en&contentId=20011265) in the Help Center.

![](https://developers.line.biz/media/line-developers-console/login-account-01-en.png)

### Log in with LINE account 

When logging in to your Business ID with your LINE account, use the following methods to log in:

- **Auto login**: Log in without operation on your smartphone with LINE installed.
- **Email address log in**: Log in using the email address and password registered for your LINE account.
- **QR code log in**: Log in using the QR code reader of your smartphone's LINE app to scan the QR code displayed.
- **Single Sign On (SSO) login**: Log in by clicking the login button on the confirmation screen showing "Continue as".

<!-- tip start -->

**Two-factor authentication is enabled when logging in with LINE account**

Two-factor authentication is enabled when you log in using your LINE account. When you log in from a browser on your computer using an email address, you must enter the email address and password of your LINE account, and then enter the authentication code displayed on your smartphone's LINE App.

![Two-factor authentication flow](https://developers.line.biz/media/news/login-flow-with-2fa-en.png)

Once two-factor authentication is executed, the browser used to log in won't require two-factor authentication again for one year. Also, if you've already logged in to [LINE Official Account Manager](https://manager.line.biz/) using two-factor authentication, you won't be required to log in to the LINE Developers Console with the same account.

<!-- tip end -->

### Log in with business account 

When logging in to your Business ID with your business account, use the email address and password registered with your Business ID.

### Log in with Yahoo! JAPAN ID 

When logging in to your Business ID with your Yahoo! JAPAN ID, you must link your Yahoo! JAPAN ID to [Yahoo! JAPAN Business ID](https://support.yahoo-net.jp/PccBizmanager/s/article/H000011271) (only available in Japanese).

Note that logging in to your Business ID using your Yahoo! JAPAN ID is only available in Japan.

For more information about how to log in with your Yahoo! JAPAN ID, see [What are the available login methods?](https://id.yahoo.co.jp/login/login_methods.html) (only available in Japanese) in the Yahoo! JAPAN ID Guide.

## Create a developer account (only on first login) 

When you first log in to the [LINE Developers Console](https://developers.line.biz/console/) with your LINE account or business account, create a developer account. Enter **Developer name** and **Your email**. Read carefully and agree to the [LINE Developers Agreement](https://terms2.line.me/LINE_Developers_Agreement?lang=en). Click **Create my account**. This step is only required on first login.

![Developer account creation screen](https://developers.line.biz/media/line-developers-console/developer-registration-01-en.png)

Once the developer account has been created, a screen showing that the developer account has been created will be displayed.

![Developer account creation completion screen](https://developers.line.biz/media/line-developers-console/developer-registration-02-en.png)

## Account relationships 

You need a developer account to use the LINE Developers Console. In addition, a developer account is always linked to a Business ID on a one-to-one basis. When you first log in to the LINE Developers Console and [create a developer account](https://developers.line.biz/en/docs/line-developers-console/login-account/#register-as-developer), your Business ID and developer account will be automatically linked.

<!-- note start -->

**Note on linking your developer account to your Business ID**

- If you delete the Business ID linked with your developer account, you will no longer be able to log in to your developer account
- A Business ID linked with a developer account can't be changed later

<!-- note end -->

A developer account and a LINE account are linked through a Business ID. When you link your LINE account to your Business ID that is linked to your developer account, you can link your LINE account to your developer account. For more information on how to link accounts, see [Link your Business ID with your LINE account](https://developers.line.biz/en/docs/line-developers-console/login-account/#link-business-account-with-line-account).

The relationship between developer accounts, Business IDs, and LINE accounts is as follows:

|  | Developer account | Business ID | LINE account |
| --- | --- | --- | --- |
| Developer account | — | One-to-one link (\*) | Linked via Business ID (one-to-one) |
| Business ID | One-to-one link (\*) | — | Can be linked one-to-one |
| LINE account | Linked via Business ID (one-to-one) | Can be linked one-to-one | — |

\* When you [create a developer account](https://developers.line.biz/en/docs/line-developers-console/login-account/#register-as-developer), your Business ID will automatically be linked to your developer account.

<!-- tip start -->

**About the email address for each account**

The name and email address registered for your developer account, Business ID, and LINE account are managed separately. Therefore, the email addresses registered to each account may be different.

<!-- tip end -->

### Account relationships when creating a new Business ID 

When you first log in to the LINE Developers Console and create a new Business ID, the linking behavior of your LINE account will vary depending on whether you use your LINE account or a business account (email address and password) to create the Business ID. The relationship between the account type used and the linkage between the developer account and your LINE account is as follows:

| Account type | LINE account linked to developer account |
| --- | --- |
| LINE account | LINE account used to create your Business ID |
| Business account<br>(email address and password) | None (\*) |

\* You can link a LINE account to your Business ID created with a business account at any time. For more information, see [Link your Business ID with your LINE account](https://developers.line.biz/en/docs/line-developers-console/login-account/#link-business-account-with-line-account).

## Link your Business ID with your LINE account 

You can only link one Business ID per each LINE account. You can't link multiple Business IDs to a single LINE account.

Follow these steps to link your Business ID with your LINE account:

1. Log in to the [LINE Developers Console](https://developers.line.biz/console/)
1. Click the icon in the top-right corner of the screen

   ![Click the icon in the top-right corner of the screen](https://developers.line.biz/media/line-developers-console/linking-line-account-click-user-icon-en.png)

1. Click the account information, and then open the profile screen

   ![Click account information](https://developers.line.biz/media/line-developers-console/linking-line-account-click-account-en.png)

1. Click the **Go to Business ID Profile** button to go to your Business ID profile

   ![Click the Go to Business ID profile](https://developers.line.biz/media/line-developers-console/linking-line-account-click-business-id-en.png)

1. Click the link icon next to "Unlinked" on the LINE account section

   ![Link to LINE account](https://developers.line.biz/media/line-developers-console/linking-line-account-click-link-icon-en.png)

1. Log in to the LINE account you want to link your Business ID with
1. Once login to your LINE account is complete, the LINE account will be linked to the Business ID

<!-- note start -->

**When the message &quot;This LINE account is already in use.&quot; is displayed when linking your LINE account**

The LINE account that you want to link to your Business ID must not be linked to any other Business ID. If you try to link your Business ID to a LINE account that you've previously linked to any other Business ID, you will see a message that says, "This LINE account is already in use," and you won't be able to link the accounts.

![Link to LINE account](https://developers.line.biz/media/line-developers-console/login-account-04-en.png)

<!-- note end -->

<!-- tip start -->

**Linking a developer account with a LINE account**

A developer account and a LINE account are linked through a Business ID. When you link your LINE account to your Business ID that is linked to your developer account, you can link your LINE account to your developer account.

<!-- tip end -->

## Unlink your LINE account from your Business ID 

In order to unlink your LINE account from your Business ID, you must register the email address and password (business account) with your Business ID. When you unlink your LINE account from your Business ID, the link between your developer account and your LINE account will also be invalidated.

Follow these steps to unlink LINE account from your Business ID:

1. Log in to the [LINE Developers Console](https://developers.line.biz/console/) with the Business ID you want to unlink your LINE account from
1. Click the icon in the top-right corner of the screen

   ![Click the icon in the top-right corner of the screen](https://developers.line.biz/media/line-developers-console/linking-line-account-click-user-icon-en.png)

1. Click the account information, and then open the profile screen

   ![Click account information](https://developers.line.biz/media/line-developers-console/linking-line-account-click-account-en.png)

1. Click the **Go to Business ID Profile** button to go to your Business ID profile

   ![Click the Go to Business ID Profile](https://developers.line.biz/media/line-developers-console/linking-line-account-click-business-id-en.png)

1. Click the delete icon on the LINE account section
   - If you haven't registered your email address and password (business account) with your Business ID, the delete icon won't be displayed. Click the edit icon on the email address section and register your email address and password.

   ![Unlink LINE account](https://developers.line.biz/media/line-developers-console/unlink-business-account-with-line-account-en.png)

1. Click **Delete** on the confirmation screen

   ![Click Delete on the confirmation screen](https://developers.line.biz/media/line-developers-console/unlink-business-account-click-delete-en.png)

1. The Business ID and the LINE account are unlinked

## Available features 

The type of channel you can create depends on whether a developer account logged into the LINE Developers Console is linked to a LINE account.

Depending on the roles assigned to the developer account you're using, there are restrictions on the features you can use. For more information, see [Managing roles](https://developers.line.biz/en/docs/line-developers-console/managing-roles/).

The following channel types are available for developer accounts depending on their link status with a LINE account:

| Link status | LINE Login | Blockchain Service | LINE MINI App |
| --- | --- | --- | --- |
| Developer account linked to a LINE account | ✅ | ✅ | ✅ |
| Developer account not linked to a LINE account | ✅ | ❌ | ✅ |

Messaging API channels can be created by creating LINE Official Accounts. For more information, see [Get started with the Messaging API](https://developers.line.biz/en/docs/messaging-api/getting-started/) in the Messaging API documentation.
