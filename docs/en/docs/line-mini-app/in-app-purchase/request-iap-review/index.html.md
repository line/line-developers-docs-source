# Apply to use in-app purchase

This page explains how to apply for in-app purchase.

## Things to check prior to applying 

Before applying to use in-app purchase, be sure to check the "[In-app purchase overview](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/overview/)" and "[In-app purchase development guidelines](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/iap-guidelines/)". Also, note the following points.

### Relationship between the in-app purchase review and the verification review 

- Even if the in-app purchase review is completed, users can't utilize in-app purchase unless the [verification review (review for publishing as a verified MINI App)](https://developers.line.biz/en/docs/line-mini-app/submit/submission-guide/) is approved.
- During the verification review, you can't apply for in-app purchase.
- During the in-app purchase review, you can't apply for the verification review.

### In-app purchase review period 

- It takes approximately two weeks for LY Corporation to complete its in-app purchase review. You can't specify the completion date of the review in advance. Thank you for your understanding.
- If your application is rejected after the review, it will take a few more days for the re-application and re-review process.
- After your in-app purchase application is approved, you must apply for the [verification review](https://developers.line.biz/en/docs/line-mini-app/submit/submission-guide/). This also has a separate review period.

## Application flow 

To apply to use in-app purchase, follow the steps below.

### 1. Enter the required information 

Enter the required information on the **In-app purchase** tab in the [LINE Developers Console](https://developers.line.biz/console/).

When applying, enter all information accurately, including the company name:

- Register Business information / LINE MINI App information
- Register Information security information
- Upload the LY Corporation business partner information application form

#### In-app purchase contract entity 

When using in-app purchase, the following information must all match the information set in the "Service company information" section on the **Business information** tab of the relevant LINE MINI App channel:

- "Business information / LINE MINI App information" section
  - **Company name**
- "Information security" section
  - **Name of the organization performing the operations**
- LY Corporation business partner information application form in the "LY Corporation business partner information" section
  - Your company information - Company name
  - Payment account information - Account holder name

### 2. Apply to use in-app purchase 

Once you have finished entering the required information, click the **Apply to use in-app purchase** button.

LY Corporation will review your application and determine whether to approve or reject it. When approved, the status display in the "Workflow in progress" section will change to "Approved".

<!-- tip start -->

**You can cancel your application until review begins**

When you apply to use in-app purchase, the workflow status will be "Applied for review" until the review actually begins. While in "Applied for review" status, you can cancel the application.

<!-- tip end -->

### 3. Configure after approval 

Once your application to use in-app purchase is approved and the status changes to "Approved", the **Apply to use in-app purchase** tab and **In-app purchase settings** tab will be displayed.

![](https://developers.line.biz/media/line-mini-app/in-app-purchase/tabs-in-iap-tab-en.png)

For more information on what to configure in the **In-app purchase settings** tab, see [Set up in-app purchase](https://developers.line.biz/en/docs/line-mini-app/in-app-purchase/iap-settings/).

## Change application information 

To modify your application information, select the **Apply to use in-app purchase** tab and edit the relevant items.

- If you have applied for in-app purchase review and the status in "Workflow in progress" is "Applied for review" or "Reviewing", you can't edit the information.
  - If the status is "Applied for review": Click **Cancel the application** to cancel the application, then edit it.
  - If the status is "Reviewing": You can't cancel while your application is under review. Update the information after the review is complete.
- If you change the information within the **Apply to use in-app purchase** tab, you need to re-apply for in-app purchase.
- The information within the **In-app purchase settings** tab (webhook URL and tester information) doesn't require re-review.
- If there are changes to the information related to the company, first complete the re-application for [verification review](https://developers.line.biz/en/docs/line-mini-app/submit/submission-guide/), then re-apply for in-app purchase review.
