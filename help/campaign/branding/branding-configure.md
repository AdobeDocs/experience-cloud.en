---
title: Branding
description: Discover how to configure your brand
audience: administration
context-tags: branding,overview;branding,main
feature: Instance Settings
role: Admin
level: Experienced
---
# Configure brands {#branding-configure}

>[!IMPORTANT]
>
>Brands cannot be created or modified by end-users: these operations have to be performed by Adobe Campaign technical administrator. For any request, contact Adobe Customer care.

Brands can be found in the **[!UICONTROL Administration > Instance settings > Brand configuration]** menu.

By default, a newly created brand is visible only to users assigned with the corresponding rights by the administrator.

A **Brand** is defined by the following characteristics:

* An **Identity**, which defines and personalizes your brand. This section contains the following fields:

  ![](assets/branding_01.png)

    * **Label** visible in the interface
    * **Brand name**
    * **Website URL** and **Website label** of the brand
    * **Brand logo**

* **[!UICONTROL Header parameters of sent emails]** which personalizes what the recipients of your campaigns will see. This section contains the following fields:

  ![](assets/branding_04_header.png)

    * **Sender (email address)** with the brand's email address.
    * **Sender (name)** with the brand's name.
    * **Reply to (email address)** with the email address the customer can reply to.
    * **Reply to (name)** with the brand's name.
    * **Error (email address)** with the email address to use in case of an error.

  >[!IMPORTANT]
  >
  >After having updated the header parameters of the emails, if the name and email address of the sender have not changed in the email created from the template, check the template's advanced settings.

* **Server(s) exposed on the internet** defines the servers used for tracking but also for landing page access. This section contains the following fields:

  ![](assets/configure_branding_04.png)

    * **External URL of the application server** used for hosting and accessing the different landing pages you create.
    * **External URL of the tracking server** used as the tracked URL during the deliveries.
    * **External URL of the mirror page server** used as the default mirror page in your deliveries.

    >[!NOTE]
    >
    >To display the landing page preview and the mirror page rendering in the Campaign user interface, the application server and mirror page server URLs must be secure. In that case, use https:// rather than http:// when setting up these URLs.

* **[!UICONTROL Tracking URL configuration (Web Analytics)]**, which defines the configuration of the URLs tracking for your brand.

  The additional parameters that allow the links to be tracked on external systems such as Web Analytics tools like Adobe Analytics or Google Analytics are defined here.

  ![](assets/branding_05.png)
