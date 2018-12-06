---
title: Implement Adobe Audience Manager with Launch
description:
seo-description:
seo-title: Implement Adobe Audience Manager with Launch
solution: Experience Cloud
---

# Adobe Audience Manager (AAM)

There are two ways to implement Audience Manager:

* **Server-Side Forwarding (SSF)** -- For customers with Adobe Analytics, this is the easiest and recommended way to implement. Adobe Analytics forwards data to AAM on Adobe's backend, allowing for one less request on the page. This enables key integration features and conforms with our best practices for Audience Manager code implementation and deployment.

* **Client-Side DIL** -- This approach is for customers who do not have Adobe Analytics. DIL code (Data Integration Library Code) sends data directly from the web page into Audience Manager.

## Prerequisites

You should know your “Audience Manager Subdomain” (also known as the “Partner Name” “Partner ID,” or “Partner Subdomain”) before you begin.

## Server-Side Forwarding (SSF)

This tutorial provides basic information on how to set up a Server-Side forwarding implementation. For a complete description and requirements list for Server-Side forwarding, please review the [documentation](https://marketing.adobe.com/resources/help/en_US/reference/ssf.html) as well, so that you are familiar with how it works, what is required, and how to validate.

### Enable Server-Side Forwarding in the Analytics Admin Console

Launch will contain the code associated with SSF and the response from AAM back to the page, *but SSF also needs to be enabled in the Adobe Analytics Admin Console*.

As stated on [this page of the Help documentation](https://marketing.adobe.com/resources/help/en_US/reference/ssf.html), after logging into Analytics go to **[!UICONTROL Admin \> Report Suites \> (select report suites) \> Edit Settings \> General \> Server-Side Forwarding]**. Enable SSF for the report suite.

### Enable Server-side Forwarding in Launch

1. Go to **[!UICONTROL Extensions > Installed]** and click to configure the Analytics extension.

1. Expand the `Adobe Audience Manager` section

1. Check the box to **[!UICONTROL Automatically share Analytics Data with Audience Manager]** to add the Audience Manager Module to the AppMeasurement.js implementation.

1. Add your “Audience Manager Subdomain” (also known as the “Partner Name” “Partner ID,” or “Partner Subdomain”)

1. Save these changes to the Analytics extension Server

Side forwarding code is now implemented!

>[!NOTE] In Launch, you will not need to configure the AAM extension to enable Server-Side Forwarding, as it is only used for client-side DIL implementations.
>[!NOTE] If you have just enabled SSF in the interface, as described
above, it will take up to four hours to start working.

#### Validation Steps
