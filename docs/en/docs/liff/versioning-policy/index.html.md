# Versioning policy

To integrate the appropriate LIFF SDK into your LIFF app, make sure to understand the LIFF Versioning policy.

- [The LIFF MAJOR version status](https://developers.line.biz/en/docs/liff/versioning-policy/#version-support-status)
- [The LIFF Versioning policy](https://developers.line.biz/en/docs/liff/versioning-policy/#versioning-policy)
- [The LIFF SDK (sdk.js) update policy](https://developers.line.biz/en/docs/liff/versioning-policy/#update-policy)
- [The LIFF SDK life cycle](https://developers.line.biz/en/docs/liff/versioning-policy/#life-cycle)

<!-- note start -->

**Note**

By updating of LIFF SDK, the LIFF SDK integrated in your LIFF app may be discontinued. A LIFF app that uses the discontinued LIFF SDK cannot be opened.

If using the LIFF app for a long period of time, check this page regularly and integrate the appropriate LIFF SDK.

<!-- note end -->

## The LIFF MAJOR version status 

[The LIFF SDK life cycle](https://developers.line.biz/en/docs/liff/versioning-policy/#life-cycle) is specified for each MAJOR version. The MAJOR versions of LIFF SDK currently supported and the status of each version are as follows:

| LIFF Version<br>(Release date) | Status<br>(Period of current status) | Availability and description |
| --- | --- | --- |
| LIFF v1<br>(June 6, 2018) | End-of-life<br>(October 1, 2021) | ❌ Without prior notice, all CDN edge paths and CDN fixed paths will be disabled, and you won't be able to open the LIFF apps. |
| LIFF v2<br>(October 16, 2019) | Active<br>(~ Release date of the LIFF v3) | ✅ The LIFF SDK is the current version. Frequently new features are added and existing features are improved. |
| LIFF v3<br>(TBD) |  |

## The LIFF Versioning policy 

Beginning with LIFF v2.2.0, the version number of LIFF will follow the rules set by [Semantic Versioning](https://semver.org/) (SemVer).

SemVer defines this version format:

`MAJOR.MINOR.PATCH`

For example, in `v1.2.3`, `1` is the MAJOR version, `2` is the MINOR version, and `3` is the PATCH version.

Here's what each version means:

| Version | Description |
| --- | --- |
| MAJOR | It will be incremented if any backwards incompatible changes are introduced to the public API.<br>e.g. v1.1.12 -> **v2.0.0** |
| MINOR | It will be incremented if new, backwards compatible functionality is introduced to the public API.<br>e.g. v1.1.12 -> **v1.2.0** |
| PATCH | It will be incremented if only backwards compatible bug fixes are introduced. A bug fix is defined as an internal change that fixes incorrect behavior.<br>e.g. v1.1.12 -> **v1.1.13** |

## LIFF SDK (sdk.js) update policy 

Since the LIFF v2.1.13 release, we prepare these two types of CDN paths. When [Integrating the LIFF SDK into LIFF app](https://developers.line.biz/en/docs/liff/developing-liff-apps/#integrating-sdk), specify the CDN path that suits your purpose.

| CDN path | Description |
| --- | --- |
| CDN edge path | This is a CDN path that contains only the MAJOR version. Use this CDN path if you want to always be up-to-date with the latest LIFF features. You only need to update your URL when a new MAJOR version is released.<br>e.g.: https://static.line-scdn.net/liff/edge/**2**/sdk.js |
| CDN fixed path | This is a CDN path that contains up to the PATCH version. Use this CDN path if you want to use the LIFF features of a specific version. You can continue to use the specified PATCH version as long as you don't update the LIFF app. Update your URL only when you want to implement our new features, security updates, and bug fixes. It's not updated automatically and isn't affected by the LIFF SDK update.<br>e.g.: https://static.line-scdn.net/liff/edge/**versions/2.22.3**/sdk.js |

<!-- note start -->

**Which version should you use?**

Developers using the CDN fixed path will need to decide when to update their LIFF app. You can evaluate each update we provide by frequently checking the [Release notes](https://developers.line.biz/en/docs/liff/release-notes/) in the LIFF documentation and decide if the update is right for you.

<!-- note end -->

Example of specifying a CDN fixed path:

```html
<script charset="utf-8" src="https://static.line-scdn.net/liff/edge/versions/2.22.3/sdk.js"></script>
```

<!-- tip start -->

**The CDN path to maintain backwards compatibility**

To guarantee the behavior of the created LIFF app, we will continue to provide the LIFF SDK with the following CDN path.

The LIFF SDK available with this CDN path is the same version as the LIFF SDK available with the CDN edge path.

CDN path for backwards compatibility: <br> https://static.line-scdn.net/liff/edge/**2.1**/sdk.js

<!-- tip end -->

<!-- note start -->

**Backwards compatible CDN path discontinuation**

The CDN path to maintain backwards compatibility may be discontinued regardless of [Life Cycle Schedule of the LIFF SDK](https://developers.line.biz/en/docs/liff/versioning-policy/#life-cycle-schedule).

We recommend changing the CDN path specified in your LIFF app to the CDN edge path.

We will inform you as soon as the policy is decided.

<!-- note end -->

## The LIFF SDK life cycle 

The LIFF SDK life cycle is defined as follows for each MAJOR version.

The status is "Active" when a new MAJOR version is released. When the next MAJOR version is released, the status of the current MAJOR version will change from "active" to "maintenance" and after a period of time, it will change to "deprecated", then "obsolete".

| Status | Availability and description | Support period |
| --- | --- | --- |
| Active | ✅ The LIFF SDK is the current version. Frequently new features are added and existing features are improved. | From the release date of this MAJOR version to the release date of the next MAJOR version |
| Maintaining | ✅ Bug fixes and security improvements needed to maintain existing features | 12 months after "Active" period |
| Deprecated | ✅ The LIFF SDK is no longer updated. | 6 months after "Maintaining" period |
| End-of-life | ❌ After the discontinuation date, all CDN edge paths and CDN fixed paths will become invalid without notice, and the LIFF app will no longer be usable. | - |

### The LIFF SDK life cycle schedule 

Familiarize yourself with the life cycle of MAJOR versions of the LIFF SDK and make the appropriate preparations.

| LIFF Version<br>(Release date) | Active period | Maintenance period | Deprecation period | End-of-life date |
| --- | --- | --- | --- | --- |
| LIFF v1<br>(June 6, 2018) | ~ October 15, 2019<br>`✅ LIFF v1` | ~ April 1, 2021<br>` ✅ LIFF v1` | ~ September 30, 2021<br>`✅ LIFF v1` | October 1, 2021<br>`❌ LIFF v1` |
| LIFF v2<br>(October 16, 2019) | ~ Release date of the LIFF v3<br>`✅ LIFF v2` | ~ TBD<br>`✅ LIFF v2` | ~ TBD<br>`✅ LIFF v2` | TBD<br>`❌ LIFF v2` |
| LIFF v3<br>(TBD) |  |  |  |

`✅ LIFF v1`/`❌ LIFF v1`: Availability of https://**d.line-scdn.net/liff/1.0**/sdk.js

`✅ LIFF v2`/`❌ LIFF v2`: Availability of https://static.line-scdn.net/liff/edge/**2**/sdk.js, https://static.line-scdn.net/liff/edge/**versions/2.x.x**/sdk.js, and https://static.line-scdn.net/liff/edge/**2.1**/sdk.js
