# LINE MINI App icon specifications and guidelines

The LINE MINI App icon is used in a variety of places, including the channel consent screen, the Home tab, LINE messages, and service messages. This page provides guidelines to follow when creating an icon, as well as instructions on how to upload an image for the icon.

- [The main locations for the LINE MINI App icon](https://developers.line.biz/en/docs/line-mini-app/design/line-mini-app-icon/#main-locations)
- [Guidelines](https://developers.line.biz/en/docs/line-mini-app/design/line-mini-app-icon/#guidelines)
- [How to upload an image for the icon](https://developers.line.biz/en/docs/line-mini-app/design/line-mini-app-icon/#how-to-upload)

## The main locations for the LINE MINI App icon 

The main locations for the LINE MINI App icon are as follows:

- [Channel consent screen](https://developers.line.biz/en/docs/line-mini-app/develop/configure-console/#consent-screen-settings)
- [Home tab](https://developers.line.biz/en/docs/line-mini-app/discover/introduction/#home-tab)
- [LINE messages](https://developers.line.biz/en/docs/line-mini-app/discover/introduction/#line-message)
- [Service messages](https://developers.line.biz/en/docs/line-mini-app/develop/service-messages/)

![](https://developers.line.biz/media/line-mini-app/line-mini-app-icon/channel-consent-screen-en.png)
![](https://developers.line.biz/media/line-mini-app/line-mini-app-icon/home-tab-en.png)
![](https://developers.line.biz/media/line-mini-app/line-mini-app-icon/line-message-en.png)
![](https://developers.line.biz/media/line-mini-app/line-mini-app-icon/service-messages-en.png)

## Guidelines 

The following are guidelines to follow when designing the icons for LINE MINI Apps. The icons may appear small, especially on mobile devices. Design your icons so that they are visible to users in any location.

- [Prohibited matters](https://developers.line.biz/en/docs/line-mini-app/design/line-mini-app-icon/#prohibited-matters)
- [Required matters](https://developers.line.biz/en/docs/line-mini-app/design/line-mini-app-icon/#required-matters)
- [Recommended matters](https://developers.line.biz/en/docs/line-mini-app/design/line-mini-app-icon/#recommended-matters)

### Prohibited matters 

#### Use of the LINE MINI App logo 

Don't include the LINE MINI App logo shown below in your logo:

| Japanese | English |
| --- | --- |
| ![](https://developers.line.biz/media/line-mini-app/line-mini-app-icon/mini-icon-guideline-mini-logo-ja.png) | ![](https://developers.line.biz/media/line-mini-app/line-mini-app-icon/mini-icon-guideline-mini-logo-en.png) |

### Required matters 

#### Icon size 

The background area (BG SIZE) of the icon should be 130x130px.

![](https://developers.line.biz/media/line-mini-app/mini_icon_background.png)

#### Logo size 

The minimum logo size (LOGO SIZE) must be 54x54px and the maximum must be 90x90px. The recommended size is between 54×54px and 76×76px.

![](https://developers.line.biz/media/line-mini-app/line-mini-app-icon/mini-icon-guideline-size-en.png)

### Recommended matters 

#### Logo design 

To maintain the visibility and quality of the logo at all times, it should be designed as a stand-alone icon or wordmark.

![](https://developers.line.biz/media/line-mini-app/line-mini-app-icon/mini-icon-guideline-design.png)

<!-- tip start -->

**Creating an icon from a template file in PSD format (optional)**

We provide a PSD template file that can be used to create an icon. Using the template file, the outline of the icon can be set. Setting the outline will make it easier to recognize the icon when it is placed in front of a background of the same color as the icon in the LINE app. Download the following template file (PSD format) before creating your icon.

[Download template file (PSD format)](https://vos.line-scdn.net/line-developers/docs/media/line-mini/icon_template_file.psd)

When creating an icon based on the template file, specify the outline color according to the background color. At this point, it is recommended to select a background color type in the template file. Also, hide unused layers in the template file before saving.

![](https://developers.line.biz/media/line-mini-app/mini_icon_guideline_color.png)

| Background color                  | Outline color   | Outline opacity |
| --------------------------------- | --------------- | --------------- |
| White (#FFFFFF)                   | Black (#000000) | 12%             |
| Black (#000000)<br>Dark (#181818) | White (#FFFFFF) | 8%              |
| Other color                       | Black (#000000) | 8%              |

<!-- tip end -->

## How to upload an image for the icon 

Upload an image for the icon from the **Channel icon** in the **Basic settings** tab of the [LINE Developers Console](https://developers.line.biz/console/). The only file formats that can be used for an icon are PNG and JPEG.

The uploaded image for the icon is automatically cropped and the icon background is transparent. Make sure that the logo fits into the green square in the preview image.

![](https://developers.line.biz/media/line-mini-app/line-mini-app-icon/mini-icon-form-en.png)
