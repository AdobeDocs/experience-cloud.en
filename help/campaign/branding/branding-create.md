---
title: Branding
description: Discover how to create a new brand
audience: administration
context-tags: branding,overview;branding,main
role: Admin
level: Experienced
badge: label="LIMITED AVAILABILITY" type="Informative" url="https://experienceleague-review.corp.adobe.com/docs/experience-cloud/campaign/campaign-standard-migration-home.html" tooltip="Restricted to Campaign Standard migrated users"
---
# Create a new brand {#brand-create}

>[!IMPORTANT]
>
>Brands cannot be created or modified by end-users: these operations have to be performed by Adobe Campaign technical administrator. For any request, contact Adobe Customer care.

You can add new entities of your organization in Campaign, or create a new type of email which you must send under a different subdomain. To perform this, follow the steps below:

1. **Configure a new subdomain** - For any new subdomain to be used by Adobe, the first step will be to configure it. You can perform this through [Campaign Control Panel](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/subdomains-branding.html) or reach out to your Adobe technical contact. Learn more about subdomain configuration [in this article](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/campaign/ac-domain-name-setup.html).

   >[!NOTE]
   >
   >Control Panel is accessible to all Admin users. The steps to grant Admin access to a user are detailed in [this page](https://experienceleague.adobe.com/docs/control-panel/using/discover-control-panel/managing-permissions.html#discover-control-panel).


1. **Create a delivery template** - Once the new brand is available, best practice is to create at least one new blank delivery template which reference this new brand. [Learn more](branding-assign.md).

1. **Check deliverability guidelines** - Before starting using the new domain, the strategy should be discussed with Adobe Deliverability team. They will help to define the best practices, if a new affinity should be created to split the IPs between domains for example, and/or if a ramp up plan should be defined.
