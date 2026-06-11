# LINE MINI App UI components

LINE MINI App page consists of (A) Header and (B) Body

![](https://developers.line.biz/media/line-mini-app/mini_concept.png)

## Header 

The header of a verified MINI App displays the title, LINE MINI App name, and verified badge. For unverified MINI Apps, the title and the domain name of the endpoint URL are displayed.

![](https://developers.line.biz/media/line-mini-app/line-mini-app-header-en.png)

The header is composed of the following components. You can't set the header or specific components of the header to be hidden.

![](https://developers.line.biz/media/line-mini-app/discover/mini_uicomp_header.png)

| Number | Component | Description |
| --- | --- | --- |
| 1 | Title | The `<title>` element of the LINE MINI App page is displayed. You cannot set the font. |
| - | Subtext | For verified MINI Apps, the LINE MINI App name and verified badge are displayed under the title. For unverified MINI Apps, the domain name of the endpoint URL is displayed. |
| 2 | Action button | When you tap the action button, features available for your LINE app version will be displayed. For more information, see [Action button](https://developers.line.biz/en/docs/line-mini-app/discover/builtin-features/#action-button). |
| 3 | Minimize Button / Close Button | Which button appears, the minimize button or the close button, depends on the type of the LINE MINI App and the LINE version.<table><thead><tr><th>Type of LINE MINI App</th><th>LINE version</th><th>Button displayed</th></tr></thead><tbody><tr><td rowspan="2">Verified MINI App</td><td><ul><li>LINE for iOS version 14.15.1 - 26.6.x</li><li>LINE for Android version 15.0.0 - 26.6.x</li></ul></td><td>Minimize button</td></tr><tr><td>Versions other than the above</td><td>Close button</td></tr><tr><td>Unverified MINI App</td><td>All versions</td><td>Close button</td></tr></tbody></table>Tapping the close button closes the LINE MINI App. Tapping the minimize button minimizes the LINE MINI App. For more information about minimizing, see [Minimizing LIFF browser](https://developers.line.biz/en/docs/liff/minimizing-liff-browser/) in the LIFF documentation. |
| 4 | Return Button | Displays the previous page. |
| 5 | Loading Bar | Displays load status of the current page. |

## Body 

WebView is used for the body. Utilize HTML5 and LIFF for when developing each of your services.

For more information on LINE MINI App development specifications, see [LINE MINI App specifications](https://developers.line.biz/en/docs/line-mini-app/discover/specifications/).
