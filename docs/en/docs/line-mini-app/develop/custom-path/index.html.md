# Configuring Custom Path

<!-- tip start -->

**This feature can only be used for verified MINI Apps**

This feature is only available for verified MINI Apps.

<!-- tip end -->

Custom Path is a unique string that is set in the LIFF URL of published channel. The Custom Path feature allows you to set your own string in the LIFF URL as follows:

| Example URL with LIFF ID | Example of setting Custom Path |
| --- | --- |
| `https://miniapp.line.me/123456-abcdefg` | `https://miniapp.line.me/cony_coffee` |

For example, by setting a unique name as a Custom Path, users will be able to identify which brand or shop's LINE MINI App from the URL. Even when Custom Path is set, the URL by LIFF ID can still be accessed as before.

## How to apply 

If you use the Custom Path feature in your LINE MINI App, an application is required. The application differs depending on the area where the service is provided.

- [If your service area is Japan](https://developers.line.biz/en/docs/line-mini-app/develop/custom-path/#area-is-japan)
- [If your service area is Taiwan or Thailand](https://developers.line.biz/en/docs/line-mini-app/develop/custom-path/#area-is-taiwan-or-thailand)

### If your service area is Japan 

If your service area is Japan, to use the Custom Path feature, apply using the form below. Instructions on how to apply a Custom Path for multiple LINE MINI Apps at once can also be found in the form below (only available in Japanese).

[Application form](https://form-business.yahoo.co.jp/claris/enqueteForm?inquiry_type=lmini-custompath)

You will be notified of the confirmation of your application and the result of the review by email. It'll take 1-2 weeks from the time of application until the URL by Custom Path becomes available.

### If your service area is Taiwan or Thailand 

If you provide services in Taiwan or Thailand and would like to use the Custom Path feature, please contact your sales representative.

## Notes on applying for Custom Path 

Even if a Custom Path is set, the LIFF URL with the Custom Path set won't be displayed on the [LINE Developers Console](https://developers.line.biz/console/).

You can apply for a Custom Path before your LINE MINI App is reviewed. However, the Custom Path will only be set after the LINE MINI App have passed the review.

In principle, once a Custom Path has been set, it can't be changed.

### String that can be used as a Custom Path 

The following restrictions apply to the string you enter when applying for a Custom Path. Take these restrictions into account when filling in the string.

- Must be a minimum of 4 characters and a maximum of 29 characters.
- Only single-byte alphanumeric characters (`a-z`, `0-9`) and underscore (`_`) are allowed.
- Underscore (`_`) can't be used as the last character.
- Can't be numeric characters only.
- Spaces are not allowed.
- Include a proper noun that identify the brand or service.
- Can't use the same strings as services provided by LY Corporation.
- Can't use strings that are already in use, including by others.
- Strings that we deem inappropriate may not be used.
