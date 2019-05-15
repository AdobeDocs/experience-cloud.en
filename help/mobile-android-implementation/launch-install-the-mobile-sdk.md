---
title: Install the Adobe Mobile SDK in a Mobile Android app
description: Learn how to get your Launch property's embed codes and implement them in your website. This lesson is part of the Implementing the Experience Cloud in Mobile Android Applications tutorial.
seo-description:
seo-title: Install the Adobe Mobile SDK in a Mobile Android app
solution: Experience Cloud
---

# Install the Mobile SDK

In this lesson, you will implement the Mobile SDK with the extensions and settings corresponding to your Launch property's Development environment.

## Prerequisites

In this lesson we will start adding code to the Bus Booking app, so if you haven't already done so:

1. Download and Install [Android Studio](https://developer.android.com/studio)
1. Download the [Bus Booking app](https://github.com/Adobe-Marketing-Cloud/busbooking-mobileapps)

## Learning Objectives

At the end of this lesson, you will be able to:

* Obtain the installation instructions for your mobile Launch property
* Understand the difference between a Development, Staging, and Production environment
* Update your `build.gradle` file to add the Mobile SDK
* Import the Mobile SDK into your app
* Verify that the SDK has been implemented successfully
* Enable Lifecycle Metrics in the app

## Get the Installation Instructions

The Installation Instructions for mobile Launch properties are a collection of code snippets that you add to specific locations in your mobile app.

Click on the `Environments` tab in the top navigation to go to the environments page. Note that Development, Staging, and Production environments have been pre-created for you. These correspond to the typical environments in the code development and release process. Code is first written by a developer in a Development environment. When they have completed their work, they send it to a Staging environment for QA and other teams to review. Once the QA and other teams are satisfied, the code is then published to the Production environment, which is the public-facing environment  which your visitors experience when they download your app.  

Launch permits additional Development environments, which is useful in large organizations in which multiple developers are working on different projects at the same time.

Development, Staging, and Production are the only environments we need to complete the tutorial.  

![Click Environments in the top nav](images/mobile-launch-environments.png)

In the **[!UICONTROL Development]** row, click the Install icon ![Install icon](images/mobile-launch-installIcon.png) to open the embed code modal.  

   ![Click the icon to open the embed code modal](images/mobile-launch-openEmbedCode.png)

Let's go through the instructions step-by-step.

## Update the build.gradle file

If you have previously used Launch in websites, one of the first things you will notice is that there are a lot more installation instructions for mobile apps than for websites.

The Adobe Mobile SDK for Android uses Gradle to manage dependencies between its various components. One of the first things we will do is add the Adobe Mobile SDK dependencies to the Bus Booking app's build.gradle file.

**To update the build.gradle file**

1. Open Android Studio
1. Select "Open an existing Android Studio Project"

   ![Select "Open an existing Android Studio Project"](images/android/mobile-launch-install-openProject.png)

1. Open the build.gradle file at the root of the Bus Booking Android folder:

   ![Open the build.gradle file at the root of the Bus Booking Android folder](images/android/mobile-launch-install-openApp.png)

1. Open the dropdown and switch to the Project view

   ![Select "Project" from the dropdown](images/android/mobile-launch-install-openProjectView.png)

1. Open the **Android > bus > build.gradle** file

   ![Open Android > bus > build.gradle](images/android/mobile-launch-install-openGradle.png)

1. In the Launch interface, make sure the operating system is set to `Android`

1. Copy the dependencies to your clipboard, by clicking the ![Copy](images/mobile-launch-copyIcon.png) icon

   ![Copy dependencies to your clipboard in the Launch interface](images/android/mobile-launch-install-copyDependencies.png)

1. In Android Studio, paste the dependencies from your clipboard right after the existing dependencies (but before the closing `}`)
1. Click the "Sync Now" link to sync the project

   ![Copy dependencies to your clipboard in the Launch interface](images/android/mobile-launch-install-pasteDependencies.png)

## Update the Application

Now it's time to update the App to import the SDK

**To import the SDK**

1. Open the Main Application file in the Bus Booking app, which is located at **Android > bus > src > main > java > com.adobe.busbooking > DemoApplication**

   ![Open DemoApplication](images/android/mobile-launch-install-openDemoApplication.png)

1. In the Launch interface, scroll to the **[!UICONTROL Add Initialization Code]** section.
1. Copy the import statements, by clicking the first ![Copy](images/mobile-launch-copyIcon.png) icon in the **[!UICONTROL Add Initialization Code]** section:

   ![Copy the import statements to your clipboard](images/android/mobile-launch-install-copyImports.png)

1. In Android Studio, paste these import statements *before* the existing imports in the `DemoApplication` file. Note that the Core extension includes libraries to support callbacks, the identity service, lifecycle metrics, and console logging among other features.

    ![Paste the import statements into your DemoApplication file](images/android/mobile-launch-install-pasteImports.png)

1. In the Launch interface, copy the two lines related to the Core extension, by clicking the second ![Copy](images/mobile-launch-copyIcon.png) icon in the **[!UICONTROL Add Initialization Code]** section. The second line turns on console logging statements (available options are "DEBUG", "VERBOSE", "WARNING", and "ERROR").

   ![Copy the Core statements to your clipboard](images/android/mobile-launch-install-copyCore.png)

1. In Android Studio, paste these Core statements into the `DemoApplication` file right after `super.onCreate()`
1. Remove the `//` comments before the `try` and `catch` lines

   ![Paste the Core statements into your DemoApplication file](images/android/mobile-launch-install-pasteCore.png)

1. In the Launch interface, copy the extension statements, by clicking the third ![Copy](images/mobile-launch-copyIcon.png) icon in the [!UICONTROL Add Initialization Code] section.

   ![Copy the Extension statements to your clipboard](images/android/mobile-launch-install-copyExtensions.png)

1. In Android Studio, paste these extension statements into the `try` section. Note that `MobileCore.configureWithAppID` contains the identifier of the Launch development environment of your property. This is important, as you will need to update this value when we are ready to deploy the app to the production environment.

   ![Paste the Extension statements into your DemoApplication file](images/android/mobile-launch-install-pasteExtensions.png)

## Verify the implementation

1. Save your Android Studio project
1. Run the app and launch it in the Emulator. If you don't have any emulator devices configured, configure one now, being sure to configure a device running Android 4.1 (API 16) or later. 

   ![Run the app and launch it in the emulator](images/android/mobile-launch-install-buildAndLaunch.png)

1. Wait for the Emulator to launch and fully open the app to the booking screen (this may take a few minutes)

   ![Wait for the app to fully open](images/android/mobile-launch-install-simulator.png)

1. Confirm that calls are being made to the Adobe servers in the Android Studio Logcat

   ![Wait for the app to fully open](images/android/mobile-launch-install-console.png)

Here are examples of some specific calls you can look for:

1. **Calls to retrieve the Launch configuration** (filter Logcat to `adobedtm.com`). Note the extension configurations which you entered in the earlier lesson. While adding the extension requires an update to the app, these settings can be managed externally in Launch and changed at any time:

    ```java
    03-14 16:30:29.484 24869-24930/com.adobe.busbooking D/ADBMobile: ConfigurationExtension - Cached configuration loaded. 
     {"target.propertyToken":"","target.timeout":5,"global.privacy":"optedin","analytics.backdatePreviousSessionInfo":true,"analytics.offlineEnabled":true,"build.environment":"dev","rules.url":"https://assets.adobedtm.com/launch-EN360aefc739b04410816f751a95861744-development-rules.zip","experienceCloud.org":"7ABB3E6A5A7491460A495D61@AdobeOrg","target.clientCode":"techmarketingdemos","target.autoFetch":true,"target.fetchBackground":false,"lifecycle.sessionTimeout":300,"target.environmentId":"busbookingapp","analytics.server":"tmd.sc.omtrdc.net","analytics.rsids":"tmd-mobile-dev1","analytics.batchLimit":0,"property.id":"PRb4881271498b4f2cbaf67d38a8f3891a","global.ssl":true,"analytics.aamForwardingEnabled":true}
    ```

1. **Request to the ID Service** (filter Logcat to `IdentityExtension`) In this example, the ID (`d_mid`)has already been set and is just being reported up again)

    ```java
   03-14 17:01:18.526 7743-7803/com.adobe.busbooking D/ADBMobile: IdentityExtension - Sending request (https://dpm.demdex.net/id?d_mid=59651426340521082405908216148091920022&d_ver=2&d_orgid=7ABB3E6A5A7491460A495D61%40AdobeOrg)
    ```

1. **Analytics request** (filter Logcat to `AnalyticsExtension`)

    ```java
   03-14 17:01:18.509 7743-7777/com.adobe.busbooking D/ADBMobile: AnalyticsExtension - Sending Analytics ID call (https://tmd.sc.omtrdc.net/id?mcorgid=7ABB3E6A5A7491460A495D61%40AdobeOrg&mid=59651426340521082405908216148091920022)
    ```

Congratulations, you've added the SDK to a mobile app!

## Enable Lifecycle Metrics in the App

Lifecycle metrics are environment-based metrics and dimensions that can be easily enabled in an app using the Experience Platform SDK. Since they can be used by multiple Experience Cloud solutions, we will enable them here, before we move deeper into the individual solutions. This is as simple as adding a couple lines of code to our app in the right place.

### Import the Core Library into the BusBookingActivity File

In order to make API calls via the Adobe Experience Platform Mobile SDK, you need to import the libraries into the appropriate files. In this case, to utilize the Lifecycle API call, we need to import the Core library.

1. With your app open in Android Studio, open the BusBookingActivity file, which is in the same directory as the DemoApplication file that you've been working in.
1. At the top of the file, add the following MobileCore import statement so that you can use the associated API calls
    `import com.adobe.marketing.mobile.MobileCore;`

![Import the Mobile Core Library](images/android/mobile-launch-install-importMobileCore.png)

### Adding the Lifecycle Code

You will now add the Lifecycle code to the main onResume() function in the app, in order to trigger the Lifecycle functions.

1. Open the BusBookingActivity file
1. Scroll down near the bottom of the file and locate the onResume() function
1. Add the following two lines of code under the `super.onResume()` line:
    ```java
     MobileCore.setApplication(getApplication());
     MobileCore.lifecycleStart(null);
     ```

![Insert Lifecycle Code](images/android/mobile-launch-install-lifecycle.png)

### Validating the Lifecycle Hit

When you run your app, you should now get one or more Lifecycle messages in the debug section of Android Studio.

1. Run a build, and choose a simulator to run the app
1. After the simulator is up and running, click to the "Run" section of the debugger in Android Studio
1. Do a search for `internalaction=Lifecycle`
1. See that there are lines that include this key/value pair, as well as the other Lifecycle metrics.

Note that lines you'll see are actually Analytics calls with Lifecycle metrics.

![Validate Lifecycle](images/android/mobile-launch-install-validateLifecycle.png)

[Next "Add the Experience Cloud ID Service" >](id-service.md)