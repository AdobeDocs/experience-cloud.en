----
title: Implement Adobe Analytics with Launch
description: Learn how to implement Adobe Analytics using the Adobe Analytics Launch extension, send a screen view beacon, add variables, track events, and add plugins. This lesson is part of the Implementing the Experience Cloud in Mobile iOS Swift Applications tutorial.
seo-description:
seo-title: Implement Adobe Analytics with Launch
solution: Experience Cloud
---

# Add Adobe Analytics

In this lesson, you will enable Adobe Analytics tracking in your app. This will include "Lifecycle" metrics (environment-based information), as well as tracking screen loads and user actions.

[Adobe Analytics](https://marketing.adobe.com/resources/help/en_US/reference/) is an industry-leading solution that empowers you to understand your customers as people and steer your business with customer intelligence.

In the lesson [Add Extensions](launch-add-extensions.md), you added the analytics extension to your Launch property. In the lesson [Install the Mobile SDK](launch-install-the-mobile-sdk.md) you imported the extension into the sample application. These steps have prepared you to track your app in Adobe Analytics. Now all you have to do is identify the screens and actions in your app that you want to send to Analytics, and you are ready to go.

## Learning Objectives

At the end of this lesson, you will be able to:

* Verify that Lifecycle metrics are being sent to Adobe Analytics, after the basic SDK implementation
* Add code to track states/screens that load on your app, as well as sending additional data along with the state/screen load hit
* Add code to track actions in your app, as well as sending additional data along with the hit

There are many things that could be implemented for Analytics in Launch. This lesson is not exhaustive, but should give you a solid overview of the main techniques you will need for implementing in your own app.

## Prerequisites

You should have already completed the lessons in the [Configure Launch](launch-create-a-property.md) section. In that section, and in Adobe Launch, you will have already set up your configuration, including the tracking server and report suite ID(s).

## Lifecycle Metrics and Adobe Analytics

Lifecycle metrics are environment-based metrics and dimensions that can be easily enabled in an app using the Experience Platform SDK. A quick line of code nets you a host of information, as shown in the [documentation](https://marketing.adobe.com/resources/help/en_US/mobile/ios/metrics.html) (this link going to iOS docs - of course the Android equivalent is available as well).

In the [Configure Launch](launch-create-a-property.md) section of this tutorial, you copied code from your Adobe Launch mobile property and pasted it into your sample project. This enabled Lifecycle metrics. These metrics and dimensions, including environment- and app-specific metrics like app version, number of engaged users, OS version, time parting, days since last use, etc. can be very helpful in the analysis of your app, especially as you build Analytics segments from them to apply to all of your reports.

### Viewing the Analytics LifeCycle Hit

Although you can see the Lifecycle hits in any debugging program/packet sniffer, we will simply show them in the Xcode debugging console.

1. Having added your Lifecycle code in the previous section of the tutorial, build and run your project in Xcode so that it launches the simulator
1. In the Xcode debugging console, type `lifecycle` into the filter at the bottom to limit what shows up, and then scroll to the bottom of the entries
1. Notice that the `Analytics request was sent with body`
1. See values in the hit, including things like AppID, CarrierName, DayOfWeek, DaysSinceFirstUse, and other metrics/dimensions listed in the documentation

![Lifecycle Hit Debugging](images/mobile-analytics-lifecycleHitDebugging.png)

## Import ACPCore Library

In the next sections, we will use APIs to track screen loads ("trackState") or actions ("trackAction") in your app. Therefore, we need to import the library for the files that reference these APIs. In this sample app tutorial, we will only need to do this for one file, namely "BookingViewController.swift". However, in your app, you will likely need to do this for multiple files.

The reason that we are talking about the Core library here (as opposed to the Analytics library) is because the main things that you will use for Analytics, namely the trackState and trackAction APIs, have been moved from the Analytics code libraries to the Core code library, so that you can send data to other solutions besides Analytics. The documentation has it listed for both Android and iOS, including Objective-C and Swift. In this section of the tutorial, we will continue to focus on iOS and Swift.

1. Open BookingViewController.swift in Xcode
1. At the top of the file (typically alongside other import statements) add `import ACPCore` to the file
1. Save
1. You are now ready to use trackState or trackAction APIs in this file

![Import ACPCore to File](images/mobile-analytics-importACPCoreToFile.png)

## Track Screen Views in Your App

In your app, you may have many different screens of content that you are providing for your users. This is the equivalent of pages on the Web. Adobe Analytics provides a method for you to send in these "page view hits" and view them in the same reports that you are used to for your Web properties. This method is called "trackState."
In this tutorial we will place the code for a trackState call into only one screen (page) in your app. In real life, you will replicate this on all of the other screens/states in your app.
In this exercise, we will also explore a few different ways of sending data (key/value pairs) in with the hit.

Following is syntax and a code example from the documentation that you can use as you do the exercises or code your own app.

**Syntax:**
`+ (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) data;`

**Example**
`ACPCore.trackState("state name", data: ["key": "value"])`

### Send a Basic Screen View Hit

>[!NOTE] If you have followed the steps in this tutorial to implement Target, you will have some additional code in the viewDidLoad() function which is not shown in the screenshots of this section. This is expected, and is meant to provide focus on the task at hand.

1. With the sample app open in Xcode, go to BookingViewController.swift, and in the viewDidLoad() function, add a trackState method call
1. Set the `state name` to "Home Screen"
1. Instead of adding any extra data, add `nil` as a placeholder in the method call
1. Or copy and paste in the following:

`ACPCore.trackState("Home Screen", data: nil)`

![Basic trackState Call](images/mobile-analytics-basicTrackState2.png)

**See the Results**

1. Save, build and run the project
1. When the simulator runs and opens the main home screen of the app, view the Xcode console
1. Filter the console to entries with "home" and look at the bottom entry which shows that the `Analytics request was sent with body`
1. Note that pageName variable is set to Home Screen, and there are no other custom data pairs. Even though you are setting the "state name" in trackState and technically not a "page name," the code uses the pageName variable to track state name, in order to provide consistency with the same kind of construct in a Web site implementation.

![Basic trackState Result](images/mobile-analytics-basicTrackStateResult1.png)

### Send a Screen View Hit With Data

1. Go back into BookingViewController.swift, and in the "super.viewDidLoad()" function, comment out (or delete) the basic (no data added) trackState call from the last exercise
1. Add a new trackState method call, this time with data, using `key1` as the key and `value1` as the value
1. Leave the `state name` as "Home Screen"
1. Or copy and paste in:

`ACPCore.trackState("Home Screen", data: ["key1": "value1"])`

![Basic trackState Call](images/mobile-analytics-trackStateWithData2.png)

**See the Results**

1. Save, build and run the project again
1. When the simulator runs and opens the main home screen of the app, view the Xcode console
1. Leave the filter as "home" and look at the bottom entry which shows that the `Analytics request was sent with body`
1. Now see that in addition to the pageName being set, you also have the key/value pair that was sent in on the hit

![Basic trackState Result](images/mobile-analytics-trackStateWithDataResult1.png)

>[!NOTE] In case you are familiar with "props and eVars" in Analytics, you will notice that these variable names are not in the SDK. All key/value data coming from the SDK will be sent as [contextData variables](https://marketing.adobe.com/resources/help/en_US/sc/implement/context_data_variables.html), and as such will need to be mapped to props or eVars (or other variables) by using [Processing Rules](https://marketing.adobe.com/resources/help/en_US/reference/processing_rules.html) in the Analytics UI.

### Additional Data-Sending Options

In the previous two sections you have sent 1) no data, and then 2) one key/value pair. However, what if you want to send multiple data points to Analytics with a screen or state load? Following are two options.

#### Option 1: Multiple Key/Value Pairs

In the trackState call, you have the option of sending multiple key/value pairs, simply by comma separating them in the data set. For example:
`ACPCore.trackState("Home Screen", data: ["key1": "value1", "key2": "value2"])`

#### Option 2: Dictionary Object

You can also define a dictionary in your code and then send that in with the trackState as well. Of course, if you have already defined some dictionary objects in your code, and want to send them into Analytics, this can be the perfect option for you. For example:
`let screenInfo = ["key1":"value1", "key2":"value2", "key3":"value3"]`
 `ACPCore.trackState("Home Screen", data: screenInfo)`

**Extra Credit**
Go ahead and try these two options out in your code, viewing the results in the Xcode debugging console. You can use the same filter as before, and check the results to make sure that you have the variables and values coming through

## Track Actions in Your App

Similar to tracking non-page-load actions on a Web site, we often want to track an action that a user takes in our app, E.g. clicks on things that don't load another screen. This is handled very similarly to the trackState we used above, except that this method is called `trackAction`.

Following is syntax and a code example from the documentation that you can use as you do the exercises or code your own app.

**Syntax:**
`+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) data;`

**Example**
`ACPCore.trackAction("action name", data: ["key": "value"])`

### Track Interaction with 'NonStop' Checkbox

In this sample bus booking app, there is a checkbox that let's users decide if they want to limit their search results to  options. We have decided that we want to track the interaction with that checkbox in Adobe Analytics.

![NonStop Checkbox](images/mobile-analytics-nonstopCheckbox.png)

This checkbox is controlled in the BookingViewController.swift file in the sample project. In this exercise, you will send a trackAction hit when people check the box, and another one if they uncheck the box, setting "on" or "off" to a variable, respectively.

#### Setting the trackAction Code

1. With the sample project open in Xcode, go to BookingViewController.swift, and locate the "nonStopButtonToggled" function
1. In the `if` statement, the first sections deselects the box if it is already selected. Therefore, we want to send in a hit that sets a value to "off", using the following code:

    `ACPCore.trackAction("NonStop Button Interaction", data: ["NonStop": "off"])`

1. In the next section (the "else" section), it checks the box if it isn't already checked. Therefore, we want to send in a hit that sets a value to "on", since they are checking the box:

    `ACPCore.trackAction("NonStop Button Interaction", data: ["NonStop": "on"])`

Notice the other customizations in the code:

* We are setting the `action name` to "NonStop Button Interaction." This is the value that will be in the "action" parameter, as well as the name of the custom link, going into the custom link report/dimension in Adobe Analytics
* The name of the `key` we are using is "NonStop." This is the key name that we can look for in Processing Rules in the Analytics Admin Console, so that we can map these values to a prop or eVar.

The function now looks like this:

![NonStop Checkbox](images/mobile-analytics-nonStopButtonCode2.png)

#### See the Code in Action

1. After adding the code, save the project, run and build
1. Click the garbage icon to clear the debugger console
1. Check the box in the simulator, noticing that instantly there are 2 hits in the debugger coming up. The last one is the sending of the data to Adobe Analytics from the code we just placed
1. Notice that both the action and pev2 parameters are set to "NonStop Button Interaction" (with encoded spaces)
1. Notice that the "NonStop=on" key/value pair are present, and can then be assigned to a prop/eVar in Processing Rules
1. Notice the "pe=lnk_o" key/value, showing that this is a "custom link" hit, triggered by trackAction

![trackAction Result in Debugger](images/mobile-analytics-trackActionResult1.png)

Nice work! You have completed the Analytics section. Of course, there are many other things that you can do to enhance our Analytics implementation, but hopefully this has given you some of the core skills you will need to tackle the rest of your needs.

### Additional Benefits of trackState and trackAction

In these last exercises, you were able to send data from the app into Adobe Analytics by using the trackState and trackAction APIs. Because the Experience Platform SDK is rooted in Launch, By Adobe, there are many more things that you can do in Launch, even adding functionality after your app has shipped.
In Launch you are able to watch for the trackState and trackAction APIs, and have them trigger additional actions, like executing URLs to Adobe solutions or to external partners, or run other code.

[Next "Add Adobe Audience Manager" >](audience-manager.md)
