---
title: Branding
description: Discover all the tools available to manage your branding identities
audience: administration
context-tags: branding,overview;branding,main
role: Admin
level: Experienced
badge: label="LIMITED AVAILABILITY" type="Informative" url="../campaign-standard-migration-home.md" tooltip="Restricted to Campaign Standard migrated users"
exl-id: f6438303-5ae8-47c6-8c34-8e586f4b6fe7
---
# Get started with branding {#branding-gs}

>[!IMPORTANT]
>
>Brands cannot be created or modified by end-users: these operations have to be performed by Adobe Campaign technical administrator. For any request, contact Adobe Customer care.

Every company has brand guidelines that define both visual elements and technical details. Adobe Campaign helps you manage these guidelines centrally, so you can present a consistent brand image to your customers in everything you do, from logos in emails to the URLs and domains used in your campaigns.

Technical administrators can create and manage multiple brands within Adobe Campaign. This allows you to define all the elements that make up your brand identity, including logos and even email tracking settings. Once created, these brands can be easily linked to your deliveries.

You can add new entities of your organization in Campaign, or create a new type of email which you must send under a different subdomain. To perform this, follow the steps below:

1. **Configure a new subdomain** - For any new subdomain to be used by Adobe, the first step will be to configure it. You can perform this through [Campaign Control Panel](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/subdomains-branding.html) or reach out to your Adobe technical contact. Learn more about subdomain configuration [in this page](https://experienceleague.adobe.com/en/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/campaign/ac-domain-name-setup).

   >[!NOTE]
   >
   >Control Panel is accessible to all Admin users. The steps to grant Admin access to a user are detailed in [this page](https://experienceleague.adobe.com/docs/control-panel/using/discover-control-panel/managing-permissions.html#discover-control-panel).

1. **Create a delivery template** - Once the new brand is available, best practice is to create at least one new blank delivery template which reference this new brand. [Learn more](branding-assign.md).

1. **Check deliverability guidelines** - Before starting using the new domain, the strategy should be discussed with Adobe Deliverability team. They will help to define the best practices, if a new affinity should be created to split the IPs between domains for example, and/or if a ramp up plan should be defined.
