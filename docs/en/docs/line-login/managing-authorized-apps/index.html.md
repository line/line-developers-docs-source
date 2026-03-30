# Managing authorized apps

Users must consent to their information, such as [User ID](https://developers.line.biz/en/glossary/#user-id), being obtained when they use a LINE Login channel. After consenting, users can review the terms of consent or revoke consent at any time.

1. From your LINE app, tap **Settings** > **Account** > **Authorized apps**. <br> The settings screen for "Authorized apps" will be displayed.
2. Tap the app you wish to unauthorize.<br> The authorized app screen will be displayed.<br> ![Authorized app](https://developers.line.biz/media/line-login/managing-authorized-apps/authorized-app-en.png)<br> To review the terms of consent, tap "View permissions". <br> To revoke consent, tap "Unlink".

## When user revokes consent 

Access tokens and refresh tokens are deactivated as soon as the user revokes consent, impacting users and providers in these ways:

| Target | Description |
| --- | --- |
| User | <ul><li>When you try to use LINE Login on an app for which you revoked consent, the consent screen will be displayed again.</li><li>LINE Login will be prohibited until consent is obtained.</li></ul> |
| Provider | <ul><li>You won't be able to obtain user ID or profile information even with an access token that you've already acquired.</li><li>Access token can't be updated because refresh token isn't available.</li><li>You won't be able to obtain user ID or profile information until the user consents again and uses LINE Login.</li></ul> |

<!-- note start -->

**Respect the user's decision to revoke consent**

Each LINE user has a different user ID per provider. Even if the user consents again after revoking consent, their user ID doesn't change. This means that information associated with a given user ID can continue being used, even after the user revokes consent.

However, respect the user's decision to revoke consent and reacquire the user's information upon verifying the access token.

Take these actions if the access token has become invalid:

- If the access token expires and becomes invalid, use the refresh token to update the access token.
- However, if the user revokes consent, neither the access token nor the refresh token will be available.

You must handle user's information correctly according to the [LINE User Data Policy](https://terms2.line.me/LINE_Developers_user_data_policy?lang=en). Failure to adhere to the LINE User Data Policy will result in service discontinuation.

<!-- note end -->
