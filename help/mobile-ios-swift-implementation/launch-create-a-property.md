---
title: Create a Launch Property for Mobile Apps
description: Learn how to log into the Launch interface and create a mobile Launch property. This lesson is part of the Implementing the Experience Cloud in Mobile iOS Swift Applications tutorial.
seo-description:
seo-title: Create a Launch Property for Mobile Apps
solution: Experience Cloud
---

# Create a Launch Property

Adobe Experience Platform Launch is the next generation of mobile SDK and website tag management capabilities. Launch gives customers a simple way to deploy and manage all of the analytics, marketing, and advertising solutions necessary to power relevant customer experiences. There is no additional charge for Launch. It is available to any Adobe Experience Cloud customer.

In this lesson, you will create a Launch property for mobile apps.

## Prerequisites

In order to complete the next few lessons, you must have permission to Develop, Approve, Publish, Manage Extensions, and Manage Environments in Launch. If you are unable to complete any of these steps because the user interface options are not available to you, reach out to your Experience Cloud Administrator to request access. For more information on Launch permissions, see [the documentation](https://docs.adobelaunch.com/launch-reference/administration/user-permissions).

## Learning Objectives

At the end of this lesson, you will be able to:

* Log into the Launch user interface
* Create a new Launch mobile property
* Configure a Launch mobile property

## Go to Launch

**To get to Launch**

1. Log into the [Adobe Experience Cloud](https://experiencecloud.adobe.com)

1. Click the ![Solution Switcher Icon](images/mobile-launch-solutionSwitcher.png) icon to open the solution switcher

1. Select **[!UICONTROL Launch]** from the menu

    ![Open the solution switcher using the icon and click Activation](images/mobile-launch-solutionSwitcherActivation.png)

1. Under **[!UICONTROL Adobe Experience Cloud Launch]**, click the **[!UICONTROL Go to Launch]** button

   ![Click the Launch button](images/mobile-launch-goToLaunch.png)

You should now see the `Properties` screen (if no properties have ever been created in the account, this screen might be empty):

![Properties Screen](images/mobile-launch-propertiesScreen.png)

If you use Launch frequently, you can also bookmark the following URL and log in directly [https://launch.adobe.com](https://launch.adobe.com)

## Create a Property

A property is basically a container that you fill with extensions, rules, data elements, and libraries as you deploy tags to your app. A single mobile property can be used across multiple app platforms (e.g. iOS and Android) provided the apps contain similar functionality and require the same solutions to be implemented.  For more information on creating properties, see ["Set up a mobile property"](https://aep-sdks.gitbook.io/docs/getting-started/create-a-mobile-property) in the product documentation.

**To Create a Property**

1. Click the **[!UICONTROL New Property]** button:

    ![Click New Property](images/mobile-launch-addNewProperty.png)

1. Name your property (e.g. `Mobile Tutorial`)
1. As the platform, click **[!UICONTROL Mobile]**
1. Click the **[!UICONTROL Save]** button

   ![Create a new Property](images/mobile-launch-newProperty.png)

Your new property should display on Properties page. Note that if you check the box next to the property name, options to **[!UICONTROL Configure]** or **[!UICONTROL Delete]** the property appear above the property list. Click on the name of your property (e.g. `Mobile Tutorial`) to open the `Overview` screen.
![Click the name of the property to open it](images/mobile-launch-openProperty.png)

[Next "Add Extensions" >](launch-add-extensions.md)
