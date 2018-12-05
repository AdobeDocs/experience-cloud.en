---
title: Implement Adobe Analytics with Launch
description:
seo-description:
seo-title: Implement Adobe Analytics with Launch
solution: Experience Cloud
---

# Adobe Analytics

In this lesson, we will implement the Adobe Analytics extension, and create rules that will send data data from the page into Adobe Analytics.

The Adobe Analytics extension supports client-side Analytics implementations using AppMeasurement.js.

There are many things that could be implemented for Analytics in Launch, but we will limit this demo to the implementation of the following items:

1. Tracking `pageName` at a global level in the Analytics extension
1. When Product Detail Pages are viewed, set an `eVar` and an `event`
1. Tracking a click on navigation links, populating an `eVar`, `prop`, and `event`
1. Implementing a plug-in to help track campaigns, and keep them from falsely duplicating `click-throughs`

## Prerequisites

As noted in the Adobe Target section, to complete the lessons in this section, you should have already completed the lessons in [Configure Launch](launch.md) and [Add the ID Service](id-service.md). Implementing Analytics does not depend on having Target implemented, but for the purposes of this tutorial, we will assume that you did follow along and implement Target.

In addition, you will need at least one report suite ID and also your tracking servers to complete this tutorial. If you don't have a test/dev report suite that you can use for this tutorial, please create one. If you are unsure how to do that, see [the documentation](https://marketing.adobe.com/resources/help/en_US/reference/new_report_suite.html). Please also have your tracking code readily available. You can retrieve this from your current implementation, or talk to your Adobe Consultant or Customer Care representative to help you decide on one.

## Add the Analytics Extension

1. Go to **[!UICONTROL Extensions > Catalog]**
1. Locate the Adobe Analytics extension
1. Click **[!UICONTROL Install]**

   ![Install the Analytics extension](../assets/images/analytics-catalog-install.png)


1. Under `Library Management > Report Suites`, enter the report suite ids you would like to use with each Launch environment (It's OK to use one report suite for all environments in this tutorial, but in real life you would want to use separate report suites, as shown in the image below)

   ![Enter the report suite ids](../assets/images/analytics-config-reportSuite.png)

   >![TIP]
   >
   >We recommend using the `Manage the library for me option` as the `Library Management` setting as it makes it much easier to keep the core `AppMeasurement.js` code up-to-date.

1. Under `General > Tracking Server`, enter your tracking server, e.g. "`tmd.sc.omtrdc.net`." Enter your SSL Tracking Server if your site supports `https://`

   ![Enter the tracking servers](../assets/images/analytics-config-trackingServer.png)

1. In the Global Variables section, set the `Page Name` variable using your `Page Name` data element (click the ![data element icon](../assets/images/icon-dataElement.png) icon and choose the page Page Name element)

   ![Set the page name variable](../assets/images/analytics-extension-pageName.png)

1. In the Link Tracking section, enter `enablementadobe.com` in the `Never Track` section and click the **[!UICONTROL Save]** button

1. Check the box to `Keep URL Parameters`

1. Click **[!UICONTROL Save to Library and Build]**

   ![Configure the Link Tracking section](../assets/images/analytics-config-linkTracking.png)

>[!NOTE]
>
>Global variables can be set in the extension configuration or in rule actions. Be aware that when setting variables with the extension configuration, the data layer must be defined before the Launch embed codes.

### What is different from DTM

* Support for Server Side Forwarding to Audience Manager is built-in
* Report Suites don't auto-populate---you have to know the specific report suite ids and manually enter them
* The managed library option ships with a specific version of AppMeasurement.js

* Multiple Analytics instances, like having two Analytics "Tools" in DTM, is not supported

* General: New options for *Custom* Character Set and Currency Code
* General: Data Center option has been removed
* Global Variables: New options for Server, State, Zip

* Global Variables: data elements must be defined before the Launch header embed code for variables set in the extension configuration (variables set in Rules can come from data elements set before the event)

* Custom Code: Option to load before or after the UI settings has been removed
* Some options have been rearranged to more intuitive locations

## Fire the Analytics Beacon in a Rule

Now you will create a rule to fire the Analytics beacon, which will also set the `Page Name` variable.
>[!NOTE] We have already created an "All Pages - Library Loaded" rule in the Target section of this tutorial, which fires on every page. We *could* use this rule for Analytics as well, but this rule fires at the top of the page, and best practice for Analytics is to fire closer to the bottom of the page, so that we can use data that has been developed on the page as it loads, etc. Therefore, we will be creating a new "all pages" rule to use for Analytics.

1. Go to the **[!UICONTROL Rules]** section in the top navigation and then and then click **[!UICONTROL Add Rule]**

   ![Add Rule](../assets/images/target-addRule.png)

1. Name the rule `All Pages - DOM Ready - Analytics`
1. Click **[!UICONTROL Events > Add]** to open the `Event Configuration` screen

   ![Name the rule and add the event](../assets/images/analytics-domReady-nameAddAnalyticsEvent.png)

1. Select **[!UICONTROL Event Type > DOM Ready]**
1. Click **[!UICONTROL Keep Changes]**
   ![Configure the Event](../assets/images/analytics-configureEventDomReady.png)

1. Under Actions, click the ![Click the Plus icon](../assets/images/icon-plus.png) to add a new action

   ![Click the Plus icon to add a new action](../assets/images/analytics-ruleAddAction.png)

1. Select **[!UICONTROL Extension > Adobe Analytics]**

1. Select **[!UICONTROL Action Type > Send Beacon]**

1. Leave Tracking set to `s.t()`. Note that if you wanted to make an `s.tl()` call in a click-event rule you could do that using the Send Beacon action, as well. However, in this case, we have set the action in this rule to "DOM Ready" so it won't require a click.

1. Click the **[!UICONTROL Keep Changes]** button

   ![Click the Plus icon to add a new action](../assets/images/analytics-sendBeacon.png)

1. Click **[!UICONTROL Save to Library and Build]**

  ![Click Save to Library and Build](../assets/images/analytics-saveToLibraryAndBuild.png)

## Validate the Page Load Hit and Page Name Variable

Now that we have created a rule to send an Analytics beacon, we should be able to see the hit in the Experience Cloud Debugger.

1. Open (or refresh) your we.retail page in a browser (you should have set a bookmark to it in an early exercise)
1. Click the debugger icon ![Open the Experience Cloud Debugger](../assets/images/analytics-debuggerIcon.png) to open your **[!UICONTROL Adobe Experience Cloud Debugger]**
1. Click to the Analytics tab
1. Expand your Report Suite's hit
1. Notice the Page Name variable/value

![Validate the page hit](../assets/images/analytics-validatePageHit.png)

>[!NOTE] If the Page Name is not showing up for you, go back through the steps in this page to make sure that you haven't missed anything.

## Setting "Product Details Page" into an `eVar` (and set an `Event`) on Product Details Pages

In our deployment, we are going to focus on Product Detail Pages (PDP), also sometimes called "Product View Pages." When we load a Product Detail Page, we would like to put that value into a "Page Type" `eVar`, as well as set an event. This will allow us to see the following in our analysis:

1. How many times product detail pages are loaded
1. How other factors (campaigns, search, etc) affect how many PDP's people load.

### Create Data Element for Page Type

1. Click **[!UICONTROL Data Elements]** in the top navigation
1. Click **[!UICONTROL Add Data Element]**
1. Name the data element `Page Type`
1. Check the `Clean text` and `Force Lower Case` options
1. Select **[!UICONTROL Data Element Type > JavaScript Variable]**
1. Use `digitalData.page.category.type` as the `Path to Variable`
1. Click **[!UICONTROL Save to Library and Build]**

### Create the Rule for Product Detail Pages

For this functionality, we will create another page load rule, triggered by DOM Ready again. However, this time, since we only want this to fire on PDP's and not on other page types, we will put a condition on the rule instead of having it fire every time any page loads.

1. Go to the **[!UICONTROL Rules]** section in the top navigation and then and then click **[!UICONTROL Add Rule]**

   ![Add Rule](../assets/images/target-addRule.png)

1. Name the rule `PDP Pages - DOM Ready - Analytics`
1. Click **[!UICONTROL Events > Add]** to open the `Event Configuration` screen

   ![Name the rule and add the event](../assets/images/analytics-domReadyAddEvent.png)

1. Select **[!UICONTROL Event Type > DOM Ready]**
1. Set the **[!UICONTROL Order]** to 40, so that it will happen BEFORE the main Analytics rule runs. In this rule, we will set some variables, and then in the main Analytics rule the beacon sends them in (along with the normal every-page stuff).
1. Click **[!UICONTROL Keep Changes]**
   ![Configure the Event](../assets/images/analytics-configDOMReadyEvent.png)

1. Under **[!UICONTROL Conditions]**, click the ![Click the Plus icon](../assets/images/icon-plus.png) to open the `Condition Configuration` screen
   ![Click the Plus icon to add a new condition](../assets/images/analytics-PDPRuleAddCondition.png)

   1. Select **[!UICONTROL Condition Type > Value Comparison]**
   1. Use the data element picker, choose `Page Type` in the first field
   1. Select  **[!UICONTROL Contains]** from the comparison operator dropdown
   1. In the next field type `product-page` (this is the unique part of the page type value pulled from the data layer on PDP's)
   1. Click **[!UICONTROL Keep Changes]**

      ![Define the condition](../assets/images/analytics-PDP-condition.png)

1. Under Actions, click the ![Click the Plus icon](../assets/images/icon-plus.png) to add a new action

   ![Click the Plus icon to add a new action](../assets/images/analytics-PDPAddAction.png)

1. Select **[!UICONTROL Extension > Adobe Analytics]**
1. Select **[!UICONTROL Action Type > Set Variables]**
1. Set **[!UICONTROL eVar2 Set as]** `product detail page`
1. Set **[!UICONTROL event2]**, leaving the optional values blank
1. Click **[!UICONTROL Keep Changes]**

      ![Set Analytics Variables in PDP Rule](../assets/images/analytics-PDPsetVariables.png)

1. Click **[!UICONTROL Save to Library and Build]**

## Validate the Product Detail Page Data

We have just created a rule that sets some variables (before the hit goes out). We should now be able to see the new data going out in the hit in the Experience Cloud Debugger.

1. Open your we.retail site in a browser and navigate to any product detail page
1. Click the debugger icon ![Open the Experience Cloud Debugger](../assets/images/analytics-debuggerIcon.png) to open your **[!UICONTROL Adobe Experience Cloud Debugger]**
1. Click to the Analytics tab
1. Expand your Report Suite's hit
1. Notice the Product Detail Variables that are now in the debugger, namely that `eVar2` has been set to product detail page, and that the `Events` variable has been set to event2 (and that your Page Name is still set by the Analytics extension)

![Validate the page hit](../assets/images/analytics-validatePDPvars.png)

## Add a Plug-in to Track Campaigns

A Plug-in is a piece of JavaScript code that we can add to our implementation to perform a specific function that is not built into the product. Plug-ins can be built by you, by other Adobe Customers/Partners, or by Adobe Consulting. Even if they are created by Adobe Consulting, they are always implemented on your site as-is, and you are responsible to do all of the testing on your site to make sure that they work correctly.

To implement plug-ins, there are basically three steps:

1. Include the doPlugins function, where the plug-in will be referenced
1. Add the main function code for the plug-in
1. Include the code that calls the function and sets variables, etc.

### Make the Code Globally Accessible

If you are going to add the doPlugins function (below) and use plug-ins, you need to check a box to make the code available globally in the Analytics implementation.

1. Go to **[!UICONTROL Extensions > Installed]**

1. In the Adobe Analytics extension, Click **[!UICONTROL Configure]**

![Configure Analytics](../assets/images/analytics-configureExtension.png)

1. Under **[!UICONTROL Library Management]**, select the box labeled `Make tracker globally accessible`. As you can see in the help bubble, this will make the tracker be scoped globally under window.s, which will be important as we refer to it in our customer JavaScript.

### Including the doPlugins Function

To add plug-ins, we need to add a function called doPlugins. This function is not added by default, but once added, is handled by the AppMeasurement library, and is called last when a hit is being sent into Adobe Analytics. Therefore, you can use this function to run some JavaScript to set variables that are easier set this way.

1. While still in the Analytics extension, scroll down and expand the section titled `Configure Tracking Using Custom Code.`
1. Select **[!UICONTROL Open Editor]**
1. Paste the following code into the code editor:

   ```javascript

   /* Plugin Config */
   s.usePlugins=true
   s.doPlugins=function(s) {
   /* Add calls to plugins here */
   }
   ```

1. Keep this window open for the next step

### Add Function Code for the Plug-in

We are actually going to call two plug-ins in this code, but one of them is built into the AppMeasurement library, so for that one we do not need to add the function to call. However, for the second one, we do need to add the function code as well. This function is called getValOnce().

### The getValOnce() Plug-in

The purpose of this plug-in is to keep values from getting falsely duplicated in the code when a visitor refreshes a page or uses the browser's back button to go back to a page where a value was set. In this tutorial, we will use it to keep the `clickthrough` event from being duplicated.

This code for this plug-in is available in the [Analytics Documentation](https://marketing.adobe.com/resources/help/en_US/sc/implement/getValOnce.html), but we will include it here for your ease of copy/paste.

1. Copy the following code

   ```javascript

   /*
   * Plugin: getValOnce_v1.11
   */
   s.getValOnce=new Function("v","c","e","t",""
   +"var s=this,a=new Date,v=v?v:'',c=c?c:'s_gvo',e=e?e:0,i=t=='m'?6000"
   +"0:86400000,k=s.c_r(c);if(v){a.setTime(a.getTime()+e*i);s.c_w(c,v,e"
   +"==0?0:a);}return v==k?'':v");

   ```

1. Paste it into the code window in the Analytics extension (that you hopefully still have open - else re-open from the previous step), **completely below** the doPlugins function (not inside of it).

![Add Plug-in Code](../assets/images/analytics-doPluginsAndGeValOnceCode.png)

You can now call this plug-in from within doPlugins.

### Calling Plug-ins from Within doPlugins

Now that the code is there and can be referenced, we can make the calls to plug-ins within the doPlugins function.
First we will call a plug-in which has been incorporated into the AppMeasurement library, and so is known as a "utility." It is referred to as `s.Util.getQueryParam`, because it is part of the s object, is a built-in utility, and will grab values (based on a parameter) from the query string in the URL.

1. copy the following code:

   `s.campaign = s.Util.getQueryParam("cid");`

1. Paste it into the doPlugins function. This will look for a parameter called `cid` in the current page URL and place it into the s.campaign variable.
1. Now call the getValOnce function by copying the following code and pasting it in right below the call to getQueryParam:

   `s.campaign=s.getValOnce(s.campaign,'s_cmp',30);`
This code will make sure that the same value is not sent in more than once in a row for 30 days (see the documentation for ways to customize this code to your needs).

![Call Plug-ins in doPlugins](../assets/images/analytics-doPluginsWithPlugins.png)

1. Save the code window
1. Click **[!UICONTROL Save to Library and Build]**

## Validate the Plug-ins

Now let's make sure that the plug-ins are working the way that we expect.

1. Open your browser to we.retail
1. Click the debugger icon ![Open the Experience Cloud Debugger](../assets/images/analytics-debuggerIcon.png) to open your **[!UICONTROL Adobe Experience Cloud Debugger]**
1. Click to the Analytics tab
1. Expand your Report Suite's hit
1. Notice the Analytics hit does not have a Campaign variable
1. Leaving your debugger open, go back to the site and add  `?cid=1234` to the URL and hit Enter to refresh the page with that query string included

   ![Add a Query String](../assets/images/analytics-cidAdded.png)

1. Check the debugger and now see that there is a Campaign variable with the value 1234 in this second hit

![getQueryParam step 1](../assets/images/analytics-getQueryParam1.png)

1. Go back and refresh the page, with the query string still in the URL
1. Check the next hit in the debugger, and the Campaign variable value will be gone, because the getValOnce plug-in has made sure that it doesn't get duplicated and look like another person came in from the campaign tracking code.

   ![getQueryParam step 1](../assets/images/analytics-getQueryParam2.png)

   >[!NOTE] There are actually a few different ways to grab a parameter out of the query string of the URL, including in the Analytics extension configuration. However, in these other non-plug-in options, they don't provide the ability to stop unnecessary duplication, as we have done here with the getValOnce plug-in. This is the author's favorite method, but you should determine which method works best for you and your needs.

## Sending an `s.tl()` into Analytics

When a page loads, we typically have Launch trigger an `s.t()` call, which is referred to as a page load call. This sets the variables you send in, and automatically records a `page view` metric for the page listed in the `pageName` variable.

However, sometimes you don't want to increase page views on your site, because the action that is taking place is "smaller" (or maybe just different) than a page view. In this case, we will use the `s.tl` function, which is commonly referred to as a custom link call (or "hit"). Even though it is referred to as a custom link call, it doesn't have to be triggered on a link click. It can be triggered by *any* of the events that are available to you in the Launch rules.

In this tutorial, we will trigger an `s.tl()` call using one of the coolest JavaScript events, an `Enters Viewport` event.

### The Use Case

For this use case, we want to know if people are scrolling down on our we.retail home page far enough to see the *New Arrivals* section on our page. There is some internal discord at our company about whether people are even seeing that section or not, so we want to use Analytics to determine the truth.

### Create the Rule in Launch

1. Go to the **[!UICONTROL Rules]** section in the top navigation and then and then click **[!UICONTROL Add Rule]**
   ![Add Rule](../assets/images/target-addRule.png)
1. Name the rule `View New Arrivals Section`
1. Click **[!UICONTROL Events > Add]** to open the `Event Configuration` screen

   ![Add New Arrivals Rule](../assets/images/analytics-newArrivalsRuleAdd.png)

1. Select **[!UICONTROL Event Type > Enters Viewport]**. This will bring up a field where you need to enter the CSS selector that will identify the item on your page that should trigger the rule when it enters view in the browser.
1. Go back to the home page of we.retail and scroll down to the New Arrivals section.
1. Right-click on the space between the "NEW ARRIVALS" title and the items in this section, and select `Inspect` from the right-click menu. This will get you close to what we want. :)
1. Right around there, possibly right under the selected section, you are looking for a div with `class="we-productgrid aem-GridColumn aem-GridColumn--default--12"`. Locate this element.
1. Right-click on this element and select **[!UICONTROL Copy > Copy Selector]**

![Configure the Enters Viewport Event](../assets/images/analytics-copyElementSelector.png)

1. Go back to Launch, and paste this value from the clipboard into the field labeled `Elements matching the CSS selector`.
   1. On a side note, it is up to you to decide how to identify CSS selectors. This method is a bit fragile, as certain changes on the page may break this selector. Please consider this when using any CSS selectors in Launch.
1. Click **[!UICONTROL Keep Changes]**
   ![Configure the Enters Viewport Event](../assets/images/analytics-configEntersViewportEvent.png)

1. Under Actions, click the ![Click the Plus icon](../assets/images/icon-plus.png) to add a new action

1. Select **[!UICONTROL Extension > Adobe Analytics]**
1. Select **[!UICONTROL Action Type > Set Variables]**
1. Set `eVar3` to `Home Page - New Arrivals`
1. Set `prop3` to `Home Page - New Arrivals`
1. Set the `Events` variable to `event3`
1. Click **[!UICONTROL Keep Changes]**

![Configure the Enters Viewport Event](../assets/images/analytics-configViewportAction.png)

1. Under Actions, click the ![Click the Plus icon](../assets/images/icon-plus.png) to add another new action

![Add Send Beacon Action](../assets/images/analytics-newArrivalsSendBeacon1.png)

1. Select **[!UICONTROL Extension > Adobe Analytics]**
1. Select **[!UICONTROL Action Type > Send Beacon]**
1. Choose the **[!UICONTROL s.tl()]** tracking option
1. In the **[!UICONTROL Link Name]** field, enter `Scrolled down to New Arrivals'. This value will be placed into the Custom Links report in Analytics.
1. Click **[!UICONTROL Keep Changes]**

![Config New Arrivals Beacon](../assets/images/analytics-configEntersViewportBeacon.png)

1. Click **[!UICONTROL Save to Library and Build]**

## Validate the Enters Viewport s.tl()

Now we will want to make sure that this hit goes in when we scroll down to the New Arrivals section of the Home Page of our site. When we first bring up our site, the values shouldn't be there, but as we scroll down and the section comes into view, the hit should fire with our new values.

1. Open the we.retail site in the browser and make sure you are at the top of the home page.
1. Click the **[!UICONTROL debugger icon]** ![Open the Experience Cloud Debugger](../assets/images/analytics-debuggerIcon.png) to open your [!UICONTROL Adobe Experience Cloud Debugger]
1. Click to the Analytics tab
1. Expand your Report Suite's hit
1. Notice the normal page view hit for the home page with the page name, etc. (but nothing in eVar3 or prop3).

![Debugger with a Page View](../assets/images/analytics-debuggerPageView.png)

1. Leaving the debugger open, scroll down on your site until you can see the New Arrivals section
1. View the debugger again, and another Analytics hit should have appeared. This hit should have the params associated with the s.tl() hit that we set up, namely:
   1. `LinkType = "link_o"` (this means that the hit is a custom link hit, not a page view hit)
   1. `LinkName = "Scrolled down to New Items"`
   1. `prop3 = "Home Page - New Arrivals"`
   1. `eVar3 = "Home Page - New Arrivals"`
   1. `Events = "event3"`

![Debugger with a Page View](../assets/images/analytics-debuggerEntersViewport.png)

Nice work! You have completed the Analytics section. Of course, there are many other things that we can do to enhance our Analytics implementation, but hopefully this has given you some of the core skills you will need to tackle the rest of your needs.

[Next "Add Adobe Audience Manager"](audience-manager.md)
