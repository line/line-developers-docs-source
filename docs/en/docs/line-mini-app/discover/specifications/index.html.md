# Specifications

This page explains the specs for developing a LINE MINI App.

<!-- table of contents -->

## HTML5 Support 

When developing a LINE MINI App, you can use almost any [HTML5](https://html.spec.whatwg.org/) specification. For example, you can use [Geolocation API](https://www.w3.org/TR/geolocation/) to acquire information regarding the user's location, and provide users with information on nearby shops. Most Map APIs that are compatible with HTML5 can be used, including the Google Maps API.

![](https://developers.line.biz/media/line-mini-app/mini_map_api.png)

### Support Media Formats 

Media formats supported by HTML5 are also supported by LINE MINI App. See these HTML5 Specifications:

- [img element](https://html.spec.whatwg.org/multipage/embedded-content.html#the-img-element)
- [Media element](https://html.spec.whatwg.org/multipage/media.html)

### HTML5 Support in the browser 

This site is helpful in finding out how HTML5 is supported on an external browser:

- [https://caniuse.com](https://caniuse.com/)

## Supported Platforms and Versions 

LINE MINI Apps are developed using [LIFF](https://developers.line.biz/en/docs/liff/overview/). Therefore, the supported OS versions and LINE versions of LINE MINI App are based on the [Recommended operating environment](https://developers.line.biz/en/docs/liff/overview/#operating-environment) of LIFF.

<!-- note start -->

**Note**

Supported versions are subject to change without notice.

<!-- note end -->

### Opening LINE MINI App in an external browser 

<!-- tip start -->

**As of October 2025, LINE MINI Apps can be used in an external browser**

The screen that is displayed when users open LINE MINI Apps in an external browser has been changed. For more information, see the news from September 26, 2025, [On October 1, 2025, all LINE MINI App users will be able to use the service in a web browser](https://developers.line.biz/en/news/2025/09/26/mini-app-browser/).

<!-- tip end -->

When a user who doesn't use LINE, or a LINE user in a situation where [deep links](https://en.wikipedia.org/wiki/Mobile_deep_linking) don't work opens a LINE MINI App in an [external browser](https://developers.line.biz/en/glossary/#external-browser), a page like the one shown below will be displayed, and the user will be guided to open the LINE MINI App using LINE's smartphone app ([LIFF browser](https://developers.line.biz/en/glossary/#liff-browser)). Tapping [**Open in web browser**] on the page displays the LIFF endpoint URL page in the web browser.

![](https://developers.line.biz/media/line-mini-app/landing-page-en.png)

## Supported LIFF Versions 

LINE MINI Apps are developed using [LIFF](https://developers.line.biz/en/docs/liff/overview/). The minimum version of the LIFF SDK available for use on LINE MINI App is v2.1.

LINE MINI App allows the use of all LIFF APIs provided by LIFF v2.1.x.
