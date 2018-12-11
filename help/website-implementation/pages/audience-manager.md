---
title: Implement Adobe Audience Manager with Launch
description:
seo-description:
seo-title: Implement Adobe Audience Manager with Launch
solution: Experience Cloud
---

# Adobe Audience Manager (AAM)

This lesson will guide you through the steps to enable [Adobe Audience Manager](https://marketing.adobe.com/resources/help/en_US/aam/) using Server-Side Forwarding.

Audience Manager provides industry-leading services for online audience data management, giving digital advertisers and publishers the tools they need to control and leverage their data assets to help drive sales success.

There are two ways to implement Audience Manager in a website:

* **Server-Side Forwarding (SSF)** -- For customers with Adobe Analytics, this is the easiest and recommended way to implement. Adobe Analytics forwards data to AAM on Adobe's backend, allowing for one less request on the page. This enables key integration features and conforms with our best practices for Audience Manager code implementation and deployment.

* **Client-Side DIL** -- This approach is for customers who do not have Adobe Analytics. DIL code (Data Integration Library Code) sends data directly from the web page into Audience Manager. This approach will not be covered in this lesson.

## Learning Objectives

At the end of this lesson, you will be able to:

1. Add Audience Manager using Server-Side Forwarding of the Analytics Beacon
1. Describe the two main ways to implement Audience Manager in a website
1. Validate the Audience Manager implementation

## Prerequisites

You should know your “Audience Manager Subdomain” (also known as the “Partner Name” “Partner ID,” or “Partner Subdomain”) before you begin.

## Server-Side Forwarding (SSF)

### Enable Server-Side Forwarding in the Analytics Admin Console

In order for the Analytics servers to start forwarding beacon data to Audience Manager, a configuration needs to made in the Adobe Analytics Admin Console. Since it can take up to four hours to start forwarding the data, you should do this first.

As stated on [this page of the Help documentation](https://marketing.adobe.com/resources/help/en_US/reference/ssf.html), after logging into Analytics go to **[!UICONTROL Admin \> Report Suites \> (select report suites) \> Edit Settings \> General \> Server-Side Forwarding]**. Enable SSF for the report suite.

>[!NOTE] Since SSF is enabled at the report suite, don't forget to repeat this step for your real report suites when you are deploying Launch on your actual site.

### Enable Server-side Forwarding in Launch

Server-side Forwarding is enabled in Launch by adding the Audience Manager module to the Adobe Analytics extension.

**To enable SSF in Launch**

1. Go to [!UICONTROL Extensions > Installed] and click to configure the Analytics extension.

1. Expand the `Adobe Audience Manager` section

1. Check the box to **[!UICONTROL Automatically share Analytics Data with Audience Manager]** to add the Audience Manager Module to the AppMeasurement.js implementation.

1. Add your “Audience Manager Subdomain” (also known as the “Partner Name” “Partner ID,” or “Partner Subdomain”)

1. Save these changes to the Analytics extension

Server Side forwarding code is now implemented!

>[!NOTE] In Launch, you will not need to configure the AAM extension to enable Server-Side Forwarding, as it is only used for client-side DIL implementations.
>[!NOTE] If you have just enabled SSF in the interface, as described
above, it will take up to four hours to start working.

#### Validation Steps

### Additional information

For a complete description and requirements list for Server-Side forwarding, please review the [documentation](https://marketing.adobe.com/resources/help/en_US/reference/ssf.html) as well, so that you are familiar with how it works, what is required, and how to validate.