---
title: Add Extensions to a Mobile Launch property
description: Learn how to add extensions to a mobile Launch property. This lesson is part of the Implementing the Experience Cloud in Mobile iOS Swift Applications tutorial.
seo-description:
seo-title: Add Extensions to a Mobile Launch property
solution: Experience Cloud
---

# Add Extensions

In this lesson, you will add extensions to your Launch property.

Launch is a platform that allows Adobe and third-party vendors to create extensions to make it easy to deploy their solutions through Launch. An extension is a package of code that extends the Launch interface and client functionality. Extensions give you the ability to choose only the parts of the Adobe Experience Platform SDK that you need for your specific app.  You can think of Launch as an operating system, and extensions are the apps you use to achieve your tasks.

Since you will be implementing the Adobe solutions (e.g. Target, Analytics, and Audience Manager), you will add the necessary extensions required to support them.

>[!WARNING] Adding and removing Extensions in mobile Launch properties requires you to update your app. This is different from web Launch properties, in which you can add or remove extensions at any time, without having to update your website.

## Prerequisites

Your Launch user account needs permission to "Manage Extensions" in order to complete this lesson. If you are unable to complete any of these steps because the user interface options are not available to you, reach out to your Experience Cloud Administrator for access. For more information on Launch permissions, see [the documentation](https://docs.adobelaunch.com/launch-reference/administration/user-permissions).

You will need the following solution details:

* One Analytics report suite ID. If you don't have a test/dev report suite that you can use for this tutorial, please create one. If you are unsure how to do that, see [the documentation](https://marketing.adobe.com/resources/help/en_US/reference/new_report_suite.html).

* Your Analytics tracking server. You can retrieve your tracking server from your current implementation, Adobe Consultant or Customer Care representative.

## Learning Objectives

At the end of this lesson, you will be able to:

* Add Extensions to a mobile Launch property
* Configure the Analytics extension
* Configure the Target and Target VEC extensions

>[!NOTE] Adobe Audience Manager can be implemented via a configuration in the Analytics extension and thus you will not need to add the Audience Manager extension in this tutorial

## Review the Pre-installed extensions

1. Click the **[!UICONTROL Extensions]** tab to go to the extensions page
1. Note that the Mobile Core and `Profile` extensions are pre-installed in your new mobile property
1. Click the **[!UICONTROL Configure]** button on the Core extension to examine its settings

   ![Go to the extensions tab](images/mobile-extensions-installed-default.png)

1. The Mobile Core extension represents the core Adobe Experience Platform SDK required for any app implementation. The core contains common set of functionality and frameworks such as a Experience Cloud Identity services, data event hub, rules engine, reusable networking, disk access routines, etc., which is required by all Adobe and third-party extensions.  For more information on the Mobile Core extension, see [the documentation](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core).

   1. Note that your Experience Cloud Org ID is detected automatically and pre-populated
   1. The Experience Cloud Server field allows you to specify a custom endpoint for Visitor ID Service requests. Use the default setting (leave it blank) for this tutorial.
   1. The Session Timeout field allows you to specify when an app Lifecycle session should timeout. By default, it will timeout if the app is in the background for 300 seconds. Use the default setting for this tutorial.

1. Since you haven't changed any of the settings, click **[!UICONTROL Cancel]** to leave the extension configuration

    ![Click Cancel to leave the configuration](images/mobile-extensions-core-cancel.png)

1. The Profile extension allows the SDK to store data in a client-side profile. It has no configurations, so there is nothing to look at. For more information on the Profile extension, see [the documentation](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile).

## Add the Solution Extensions

Now it's time to get to the fun part and start adding the extensions for the solutions you will be implementing in this tutorial. When using Launch with mobile applications, the app must be updated every time an extension is added or removed. In order to save time later, we will add all of the extensions in this lesson. Just skip any solutions which your company has not licensed.

### Add the Adobe Analytics extension

>[!NOTE] If you do not have a license for Adobe Analytics, you can skip this section. At this time, the Analytics extension for mobile properties is used solely to manage SDK settings and does not add interface options to Launch, such as Rule actions.

**To add the extension**

1. Click on the Catalog tab to see the _uninstalled_ extensions

1. Find the **[!UICONTROL Adobe Analytics]** extension and click **[!UICONTROL Install]**
  
    ![Go to the Extensions catalog and click Install to add the Analytics extension](images/mobile-extensions-catalog-installAnalytics.png)

1. Enter your **[!UICONTROL Report Suite ID]**. This is the Report Suite to which the app will send data. At the moment, only one report suite can be specified per property.
1. Enter your **[!UICONTROL Analytics Tracking Server]**. This is the domain to which the beacons will be sent, typically in the format `yoursite.sc.omtrdc.net`.
1. Check the box for **[!UICONTROL Offline Enabled]**. When the Offline Enabled check box is selected, Analytics hits are queued when your device is offline and are sent later when your device is back online. To use offline tracking, **ensure** that your report suite is timestamp enabled. For more information, see the [documentation](https://marketing.adobe.com/resources/help/en_US/sc/implement/offline_tracking.html).
1. Check the box for **[!UICONTROL Audience Manager Forwarding]**. This will forward Analytics data to Audience Manager, so you won't have to make an additional call from the app to Audience Manager. This setting is used by both Audience Manager and the People Core Service, so check the box even if you haven't licensed Audience Manager.
1. Check the box to **[!UICONTROL Backdate Previous Session Info]**
1. Click the **[!UICONTROL Save]** button
  
    ![Go to the Extensions catalog and click Install to add the Analytics extension](images/mobile-extensions-analytics-settings.png)

### Add the Target extension

Adobe Target has two official extensions, the Adobe Target extension and the Adobe Target VEC extension. The Adobe Target supports all of the API familiar to users of our earlier mobile SDKs. The Adobe Target VEC extension adds support for Target's Visual Experience Composer (currently in Beta), which allows marketers to build simple activities that change image and text elements on the page in a What-You-See-Is-What-You-Get (WYSIWYG) interface. In this tutorial, you will use both.

>[!NOTE] If you do not have a license for Adobe Target, you can skip this section. At this time, the Target extension for mobile properties is used solely to manage SDK settings and does not add interface options to Launch, such as Rule actions.

**To add the extension**

1. Click on the Catalog tab to see the _uninstalled_ extensions

1. Find the **[!UICONTROL Adobe Target]** extension and click **[!UICONTROL Install]**
  
   ![Go to the Extensions catalog and click Install to add the Target extension](images/mobile-extensions-catalog-installTarget.png)

1. Your **[!UICONTROL Client Code]** will pre-populate.
1. Enter `busbookingapp` as the **[!UICONTROL Environment Id]** (this will create a new [host](https://docs.adobe.com/help/en/target/using/administer/hosts.html) in Target for the app)
1. Leave the **[!UICONTROL Timeout]** set to 5 seconds. This setting controls how long the app should wait for the Target response before displaying default content.
1. Click the **[!UICONTROL Save]** button
  
    ![Configure the Target settings](images/mobile-extensions-target-settings.png)

### Add the Target VEC extension

Now that the Target extension has been added, you can add the Target VEC extension. At this time, the Target VEC extension for mobile properties is used solely to manage SDK settings and does not add interface options to Launch, such as Rule actions.

>[!NOTE] If you do not have a license for Adobe Target, you can skip this section

**To add the extension**

1. Click on the Catalog tab to see the _uninstalled_ extensions

1. Find the **[!UICONTROL Adobe Target VEC]** extension and click **[!UICONTROL Install]**
  
   ![Go to the Extensions catalog and click Install to add the Target extension](images/mobile-extensions-catalog-installTargetVEC.png)

1. Turn **[!UICONTROL Auto-Fetch Target Campaigns]**&nbsp;&nbsp;`ON` . This will pre-fetch all of the Target activities when the app first loads, reducing the number of requests that need to be made.
1. Leave **[!UICONTROL Fetch In Background]**&nbsp;&nbsp;`OFF`. This setting only appears when `Auto-Fetch Target Campaigns` is used.  Leaving this setting `OFF` will allow you to run VEC activities on the home screen of the app, but will also add a delay to the app start up to ensure that the Target request has completed or timed out before the home screen displays. We recommend that you leave this setting `OFF` when you are running activities on the home screen and toggle it `ON` when you are not.  This setting can be changed at any time in the Launch interface without updating your app.
1. Leave the **[!UICONTROL Target Workspace Property]** blank. This setting is used in conjunction with the Target Premium [Enterprise User Permissions](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/property-channel.html) feature.
1. Click the **[!UICONTROL Save]** button
  
    ![Configure the Target VEC settings](images/mobile-extensions-targetVEC-settings.png)

That's it! Now that you have added the extensions to your property, you can add them to a library:

[Next "Create a Library" >](launch-create-a-library.md)