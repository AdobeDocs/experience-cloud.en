---
title: Switch Launch Environments with the Adobe Experience Cloud Debugger
description: Learn how to use the Experience Cloud Debugger to load different Launch embed codes. This lesson is part of the Implementing the Experience Cloud in Websites with Launch tutorial.
seo-description:
seo-title: Switch Launch Environments with the Adobe Experience Cloud Debugger
solution: Experience Cloud
---

# Switch Launch Environments with the Experience Cloud Debugger

In this lesson you will use the [Adobe Experience Cloud Debugger extension](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) to replace the Launch property hardcoded on the [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html) with your own property.

This technique is called environment switching and will be helpful later, when you work with Launch on your own website. You will be able to load your production website in your browser, but with your *development* Launch environment. This enables you to confidently make and validate Launch changes independently from your regular code releases.  After all, this separation of marketing tag releases from your regular code releases is one of the main reasons customers use Launch in the first place!

## Learning Objectives

At the end of this lesson, you will be able to:

* Use the Debugger to load an alternate Launch environment
* Use the Debugger to validate that you have loaded an alternate Launch environment
  
## Get the URL of your Development Environment

1. In your Launch property, open the `Environments` page

1. In the **[!UICONTROL Development]** row, click the Install icon ![Install icon](images/launch-installIcon.png) to open the modal

1. Click the Copy icon ![Copy icon](images/launch-copyIcon.png) to copy the embed code to your clipboard

1. Click **[!UICONTROL Close]** to close the modal

   ![Install icon](images/launch-copyInstallCode.png)

## Replace the Launch URL on the Luma Demo Site

1. Open the [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html) in your Chrome browser

1. Open the [Experience Cloud Debugger extension](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) by clicking the ![Debugger Icon](images/icon-debugger.png) icon

   ![Click the Debugger icon](images/switchEnvironments-openDebugger.png)

1. Note that the currently implemented Launch property is shown on the Summary tab

   ![Launch environment shown in Debugger](images/switchEnvironments-debuggerOnWeRetail-prod.png)

1. Go to the Tools tab

1. Scroll to the section **[!UICONTROL Replace Launch Embed Code]**

1. Make sure the Chrome tab with the Luma site is in focus behind the Debugger (not the tab with this tutorial or the tab with the Launch interface).  Paste the embed code that is in your clipboard into the input field

1. Toggle on the "Apply across luma.enablementadobe.com" feature so that all pages on the Luma site will map to your Launch property

1. Click the **[!UICONTROL Save]** button

   ![Launch environment shown in Debugger](images/switchEnvironments-debugger-save.png)

1. Reload the Luma site and check the Summary tab of the Debugger. Under the Launch section, you should now see your Development Property is being used. Confirm that both the Name of the property matches yours and that the Environment says "development."

   ![Launch environment shown in Debugger](images/switchEnvironments-debuggerOnWeRetail.png)

>[!NOTE] The Debugger will save this configuration and replace the Launch embed codes whenever you come back to the Luma site. It will not impact other sites you visit in other open tabs. To stop the Debugger from replacing the embed code, click the **[!UICONTROL Remove]** button next to the embed code in the Tools tab of the Debugger.

As you continue the tutorial, you will use this technique of mapping the Luma site to your own Launch property to validate your Launch implementation. When you start using Launch on your production website, you can use this same technique to validate changes.

[Next "Add the Adobe Experience Platform Identity Service" >](id-service.md)