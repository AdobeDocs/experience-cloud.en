---
title: Branding
description: Discover how to configure your brand
audience: administration
context-tags: branding,overview;branding,main
role: Admin
level: Experienced
badge: label="LIMITED AVAILABILITY" type="Informative" url="../campaign-standard-migration-home.md tooltip="Restricted to Campaign Standard migrated users"
---
# Configure brands {#branding-configure}

>[!IMPORTANT]
>
>Brands cannot be created or modified by end-users: these operations have to be performed by Adobe Campaign technical administrator. For any request, contact Adobe Customer care.

In Adobe Campaign V8, Brands can be found in the **[!UICONTROL Administration > Platform > Branding]** menu.

A **[!UICONTROL Brand]** is defined by the following characteristics:

* An **[!UICONTROL Identity]**, which defines and personalizes your brand. This section contains the following fields:

    * **[!UICONTROL Label]** visible in the interface
    * **[!UICONTROL ID]**
    * **[!UICONTROL Brand name]**
    * **[!UICONTROL Website URL]** and **[!UICONTROL Website label]** of the brand
    * **[!UICONTROL Brand logo]**

* **[!UICONTROL Header parameters of sent emails]** which personalizes what the recipients of your campaigns will see. This section contains the following fields:

    * **[!UICONTROL Sender (email address)]** with the brand's email address.
    * **[!UICONTROL Sender (name)]** with the brand's name.
    * **[!UICONTROL Reply to (email address)]** with the email address the customer can reply to.
    * **[!UICONTROL Reply to (name)]** with the brand's name.
    * **[!UICONTROL Error (email address)]** with the email address to use in case of an error.

  >[!IMPORTANT]
  >
  >After having updated the header parameters of the emails, if the name and email address of the sender have not changed in the email created from the template, check the template's advanced settings.

* **[!UICONTROL Brand configs]** defines the servers used for tracking also for landing page access.. This section contains the following fields:

    * **[!UICONTROL Brand subdomain]** used for hosting and accessing the different landing pages you create.
    * **[!UICONTROL Tracking URL]** of the tracking server used as the tracked URL during the deliveries.
    * **[!UICONTROL Mirror URL]** of the mirror page server used as the default mirror page in your deliveries.
    * **[!UICONTROL Application URL]** of the application server used for hosting and accessing the different landing pages you create.

  Note that configuration for tracking, mirror, and application servers is stored in separate external accounts associated with routing. These settings are applied during provisioning and should not be modified. To display URLs, access the **[!UICONTROL Branding prefixes]** tab from your external account.

<!--![](assets/branding_05.png)-->

<!--
* **[!UICONTROL Tracking URL configs]**, which defines the configuration of the URLs tracking for your brand.

  The additional parameters that allow the links to be tracked on external systems such as Web Analytics tools like Adobe Analytics or Google Analytics are defined here.
-->
