---
title: Switch Launch Environments with the Adobe Experience Cloud Debugger
description:
seo-description:
seo-title: Switch Launch Environments with the Adobe Experience Cloud Debugger
solution: Experience Cloud
---

# Switch Launch Environments with the Experience Cloud Debugger

In this lesson you will use the [Adobe Experience Cloud Debugger extension](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) to replace the Launch property hardcoded on the [We.Retail demo site](https://aem.enablementadobe.com/content/we-retail/us/en.html) with your own property.

Environment switching will be helpful outside of this tutorial, when you work with Launch own website. You will be able to load your production website in your browser, but with your *Development* Launch environment. This enables you to confidently make and validate Launch changes independently from your regular code releases.  After all, this separation of marketing tag releases from your main codebase releases is probably one of the main reasons you are using Launch in the first place!

## Learning Objectives

At the end of this lesson, you will be able to:

* Use the Debugger to load an alternate Launch environment
* Use the Debugger to validate that you have loaded an alternate Launch environment
  
## Get the URL of your Development Environment

1. In your Launch property, open the `Environments` page

1. In the **[!UICONTROL Development]** row, click the Install icon

   ![Install icon](../assets/images/launch-installIcon.png) to open the modal

1. Click the Copy icon ![Copy icon](../assets/images/launch-copyIcon.png) to copy the embed code to your clipboard

1. Click **[!UICONTROL Close]** to close the modal

   ![Install icon](../assets/images/launch-copyInstallCode.png)

## Replace the Launch URL on the We.Retail Demo Site

1. Open the [We.Retail demo site](https://aem.enablementadobe.com/content/we-retail/us/en.html) in your Chrome browser

1. Open the [Experience Cloud Debugger extension](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) by clicking the ![Debugger Icon](../assets/images/icon-debugger.png) icon

   ![Click the Debugger icon](../assets/images/switchEnvironments-openDebugger.png)

1. Note that the currently implemented Launch property is shown on the Summary tab

   ![Launch environment shown in Debugger](../assets/images/switchEnvironments-debuggerOnWeRetail.png)

1. Go to the Tools Tab

1. Click **[!UICONTROL Adobe Launch > Dynamically Insert Launch > Embed Code]** button to open the text input field:

   ![Click the Adobe Launch > Dynamically Insert Launch > Embed Code button](../assets/images/switchEnvironments-debugger-editEmbedCode.png)

1. Paste the embed code that is in your clipboard

1. Click the disk icon to save

   ![Launch environment shown in Debugger](../assets/images/switchEnvironments-debugger-save.png)

1. Reload and check the Summary tab of the Debugger. Under the Launch section, you should now see your Development Property is implemented, showing your property name (I.e. "Launch Tutorial" or whatever you named your property)!

   ![Launch environment shown in Debugger](../assets/images/switchEnvironments-debuggerOnWeRetail.png)

>[!NOTE] The Debugger will save this configuration and replace the Launch embed codes whenever you come back to the We.Retail site. It will not impact other sites you visit in other open tabs. To stop the Debugger from replacing the embed code, click the "X" next to the embed code in the Debugger. 

As you continue the tutorial, you will use this technique of mapping the We.Retail site to your own Launch property to validate your Launch implementation. When you start using Launch on your production website, you can use this same technique to validate changes you make to your Development and Staging Environments before you publish them to Production.

[Next "Add the Experience Cloud ID Service" >](id-service.md)