---
title: Implement Adobe Analytics with Launch
description:
seo-description:
seo-title: Implement Adobe Analytics with Launch
solution: Experience Cloud
---

# Adobe Analytics

Adobe Analytics is an industry-leading solution that empowers you to understand your customers as people and steer your business with customer intelligence.

In this lesson, you will implement the Adobe Analytics extension and create rules to send data to Adobe Analytics.

## Learning Objectives

At the end of this lesson, you will be able to:

1. Set variables at a global level in the Analytics extension
1. Add the page view beacon (s.t()) globally to the site
1. Add additional variables under specific conditions in the page view beacon using rules
1. Track clicks and other events (s.tl())
1. Add Analytics plugins

There are many things that could be implemented for Analytics in Launch. This lesson is not exhaustive, but should give you a solid overview of the main techniques you will need for implementing in your own site.

## Prerequisites

You should have already completed the lessons in [Configure Launch](launch.md) and [Add the ID Service](id-service.md).

In addition, you will need at least one report suite ID. If you don't have a test/dev report suite that you can use for this tutorial, please create one. If you are unsure how to do that, see [the documentation](https://marketing.adobe.com/resources/help/en_US/reference/new_report_suite.html). Please also have your tracking server readily available. You can retrieve this from your current implementation, or talk to your Adobe Consultant or Customer Care representative to help you select one.

## Add the Analytics Extension

The Analytics extension consists of two main parts:

1. The extension configuration, which manages the core AppMeasurement.js library settings and can set global variables
1. Rule actions to do the following:
    1. Set Variables
    1. Clear Variables
    1. Send the Analytics Beacon

**To add the Analytics extension**

1. Go to **[!UICONTROL Extensions > Catalog]**
1. Locate the Adobe Analytics extension
1. Click **[!UICONTROL Install]**

   ![Install the Analytics extension](../assets/images/analytics-catalog-install.png)

1. Under `Library Management > Report Suites`, enter the report suite ids you would like to use with each Launch environment (It's OK to use one report suite for all environments in this tutorial, but in real life you would want to use separate report suites, as shown in the image below)

   ![Enter the report suite ids](../assets/images/analytics-config-reportSuite.png)

   >[!TIP] We recommend using the `Manage the library for me option` as the `Library Management` setting as it makes it much easier to keep the core `AppMeasurement.js` code up-to-date.

1. Under `General > Tracking Server`, enter your tracking server, e.g. "`tmd.sc.omtrdc.net`." Enter your SSL Tracking Server if your site supports `https://`

   ![Enter the tracking servers](../assets/images/analytics-config-trackingServer.png)

1. In the Global Variables section, set the `Page Name` variable using your `Page Name` data element (click the ![data element icon](../assets/images/icon-dataElement.png) icon and choose the page Page Name element)

   ![Set the page name variable](../assets/images/analytics-extension-pageName.png)

1. In the Link Tracking section, enter `enablementadobe.com` in the `Never Track` section and click the **[!UICONTROL Save]** button

1. Check the box to `Keep URL Parameters`

1. Click **[!UICONTROL Save to Library and Build]**

   ![Configure the Link Tracking section](../assets/images/analytics-config-linkTracking.png)

>[!NOTE] Global variables can be set in the extension configuration or in rule actions. Be aware that when setting variables with the extension configuration, the data layer must be defined before the Launch embed codes.

## Send the Page View Beacon

Now you will create a rule to fire the Analytics beacon, which will send the `Page Name` variable set in the extension configuration.

>[!NOTE] You have already created an "All Pages - Library Loaded" rule in the Target section of this tutorial, which is triggered on every page when the Launch library loads. You *could* use this rule for Analytics as well, however this requires all data layer attributes that you would like to pass to Analytics to be defined before the Launch embed codes. To allow more flexibility with the data collection, you will create a new "all pages" rule triggered on DOM Ready to fire the Analytics beacon.

1. Go to the **[!UICONTROL Rules]** section in the top navigation and then and then click **[!UICONTROL Add Rule]**

   ![Add Rule](../assets/images/target-addRule.png)

1. Name the rule `All Pages - DOM Ready`
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

### Validate the Page View Beacon

Now that we have created a rule to send an Analytics beacon, we should be able to see the request in the Experience Cloud Debugger.

1. Open the [We.Retail site](https://aem.enablementadobe.com/content/we-retail/us/en.html) in your Chrome browser
1. Click the Debugger icon ![Open the Experience Cloud Debugger](../assets/images/analytics-debuggerIcon.png) to open the **[!UICONTROL Adobe Experience Cloud Debugger]**
1. Click to the Analytics tab
1. Expand your Report Suite name to show all of the requests made to it
1. Confirm the Page Name variable and value

![Validate the page hit](../assets/images/analytics-validatePageHit.png)

>[!NOTE] If the Page Name is not showing up for you, go back through the steps in this page to make sure that you haven't missed anything.

## Add Variables with Rules

When you configured the Analytics Extension, you populated the `pageName` variable in the extension configuration. This is a fine location to populate other Analytics variables such as eVars and props, provided the value you are passing is available on the page before the Launch embed codes.

A more flexible location to set variables&mdash;as well as events&mdash;is in rules using the `Set Variables` action. Using rules allows you to set different Analytics variables and events under different conditions. For example, you could set the `prodView` only on product detail pages and the `purchase` event only on order confirmation pages. This section will teach you how to set variables using rules.

Product Detail Pages (PDP) are important points for data collection on retail sites. Typically, you want your analytics system to register that a product view occurred and which product was viewed. This is helpful in understanding which products are popular with your customers. On a media site, article or video pages could use similar tracking techniques to the ones you will use in this section.  When we load a Product Detail Page, we would like to put that value into a "Page Type" `eVar`, as well as set an event. This will allow us to see the following in our analysis:

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

### Validate the Product Detail Page Data

We have just created a rule that sets some variables (before the hit goes out). We should now be able to see the new data going out in the hit in the Experience Cloud Debugger.

1. Open the [We.Retail site](https://aem.enablementadobe.com/content/we-retail/us/en.html) in your Chrome browser and navigate to any product detail page
1. Click the Debugger icon ![Open the Experience Cloud Debugger](../assets/images/analytics-debuggerIcon.png) to open your **[!UICONTROL Adobe Experience Cloud Debugger]**
1. Click to the Analytics tab
1. Expand your Report Suite's hit
1. Notice the Product Detail Variables that are now in the debugger, namely that `eVar2` has been set to product detail page, and that the `Events` variable has been set to event2 (and that your Page Name is still set by the Analytics extension)

![Validate the page hit](../assets/images/analytics-validatePDPvars.png)

## Add a Plug-in

A Plug-in is a piece of JavaScript code that you can add to your implementation to perform a specific function that is not built into the product. Plug-ins can be built by you, by other Adobe Customers/Partners, or by Adobe Consulting. Even if they are created by Adobe Consulting, they are always implemented on your site as-is, and you are responsible to do all of the testing on your site to make sure that they work correctly.

To implement plug-ins, there are basically three steps:

1. Include the doPlugins function, where the plug-in will be referenced
1. Add the main function code for the plug-in
1. Include the code that calls the function and sets variables, etc.

### Make the Analytics Object Globally Accessible

If you are going to add the doPlugins function (below) and use plug-ins, you need to check a box to make the Analytics "s" object available globally in the Analytics implementation.

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

The purpose of this plug-in is to keep values from getting falsely duplicated in the code when a visitor refreshes a page or uses the browser's back button to go back to a page where a value was set. In this lesson, you will use it to keep the `clickthrough` event from being duplicated.

The code for this plug-in is available in the [Analytics Documentation](https://marketing.adobe.com/resources/help/en_US/sc/implement/getValOnce.html), but we will include it here for your ease of copy/paste.

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

1. Paste it into the code window in the Analytics extension (if you don't still have it open, re-open it as per the previous step), **completely below** the doPlugins function (not inside of it).

![Add Plug-in Code](../assets/images/analytics-doPluginsAndGeValOnceCode.png)

You can now call this plug-in from within doPlugins.

### Calling Plug-ins from Within doPlugins

Now that the code is there and can be referenced, we can make the calls to plug-ins within the doPlugins function.

First you will call a plug-in which has been incorporated into the AppMeasurement library, and so is known as a "utility." It is referred to as `s.Util.getQueryParam`, because it is part of the s object, is a built-in utility, and will grab values (based on a parameter) from the query string in the URL.

1. Copy the following code:

   `s.campaign = s.Util.getQueryParam("cid");`

1. Paste it into the doPlugins function. This will look for a parameter called `cid` in the current page URL and place it into the s.campaign variable.
1. Now call the getValOnce function by copying the following code and pasting it in right below the call to getQueryParam:

   `s.campaign=s.getValOnce(s.campaign,'s_cmp',30);`
This code will make sure that the same value is not sent in more than once in a row for 30 days (see the documentation for ways to customize this code to your needs).

      ![Call Plug-ins in doPlugins](../assets/images/analytics-doPluginsWithPlugins.png)

1. Save the code window
1. Click **[!UICONTROL Save to Library and Build]**

### Validate the Plug-ins

Now let's make sure that the plug-ins are working the way that we expect.

1. Open the [We.Retail site](https://aem.enablementadobe.com/content/we-retail/us/en.html) in your Chrome browser
1. Click the Debugger icon ![Open the Experience Cloud Debugger](../assets/images/analytics-debuggerIcon.png) to open the **[!UICONTROL Adobe Experience Cloud Debugger]**
1. Click to the Analytics tab
1. Expand your Report Suite
1. Notice the Analytics hit does not have a Campaign variable
1. Leaving the Debugger open, go back to the We.Retail site and add  `?cid=1234` to the URL and hit Enter to refresh the page with that query string included

   ![Add a Query String](../assets/images/analytics-cidAdded.png)

1. Check the Debugger and confirm that there is a second Analytics request with a Campaign variable set to `1234`

      ![getQueryParam step 1](../assets/images/analytics-getQueryParam1.png)

1. Go back and refresh the We.Retail page again, with the query string still in the URL
1. Check the next hit in the Debugger, and the Campaign variable should not be present, because the getValOnce plug-in has made sure that it doesn't get duplicated and look like another person came in from the campaign tracking code.

   ![getQueryParam step 1](../assets/images/analytics-getQueryParam2.png)

   >[!NOTE] There are actually a few different ways to grab a parameter out of the query string of the URL, including in the Analytics extension configuration. However, in these other non-plug-in options, they don't provide the ability to stop unnecessary duplication, as we have done here with the getValOnce plug-in. This is the author's favorite method, but you should determine which method works best for you and your needs.

## Send a Track Link Beacon

When a page loads, your typically fire a page load beacon triggered by the `s.t()` function. This automatically increments a `page view` metric for the page listed in the `pageName` variable.

However, sometimes you don't want to increment page views on your site, because the action that is taking place is "smaller" (or maybe just different) than a page view. In this case, we will use the `s.tl()` function, which is commonly referred to as a "track link" request or "hit". Even though it is referred to as a track link call, it doesn't have to be triggered on a link click. It can be triggered by *any* of the events that are available to you via in the Launch rule builder, including your own custom JavaScript.

In this tutorial, we will trigger an `s.tl()` call using one of the coolest JavaScript events, an `Enters Viewport` event.

### The Use Case

For this use case, we want to know if people are scrolling down on our We.Retail home page far enough to see the *New Arrivals* section of our page. There is some internal discord at our company about whether people are even seeing that section or not, so we want to use Analytics to determine the truth.

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

### Validate the Track Link Beacon

Now we will want to make sure that this hit goes in when we scroll down to the New Arrivals section of the Home Page of our site. When we first bring up our site, the values shouldn't be there, but as we scroll down and the section comes into view, the hit should fire with our new values.

1. Open the [We.Retail site](https://aem.enablementadobe.com/content/we-retail/us/en.html) in your Chrome browser and make sure you are at the top of the home page.
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
