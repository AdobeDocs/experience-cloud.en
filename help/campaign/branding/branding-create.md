---
title: Branding
description: Discover how to create a new brand
audience: administration
context-tags: branding,overview;branding,main
feature: Instance Settings
role: Admin
level: Experienced
---
# Create a new brand {#brand-create}

You can add new entities of your organization in Campaign, or create a new type of email which you must send under a different subdomain. To perform this, follow the steps below:

1. **Configure a new subdomain** - For any new subdomain to be used by Adobe, the first step will be to configure it. You can perform this through [Campaign Control Panel](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/subdomains-branding.html) or reach out to your Adobe technical contact. Learn more about subdomain configuration [in this article](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/campaign/ac-domain-name-setup.html).

   >[!NOTE]
   >
   >Control Panel is accessible to all Admin users. The steps to grant Admin access to a user are detailed in [this page](https://experienceleague.adobe.com/docs/control-panel/using/discover-control-panel/managing-permissions.html#discover-control-panel).

1. **Create a ticket** - Once the subdomain is configured, Adobe will set it up in the your production environment. To request this, [create a ticket to Client Care](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) with the following information:

   * Subject: ACS New brand set up
   
   * Content: A new domain has been configured and we would like to get it set up in our Campaign platform
   
   * Domain: XXX
   
   * Production URL: XXX.campaign.adobe.com

1. **Create a delivery template** - Once the new brand is available, best practice is to create at least one new blank delivery template which reference this new brand. [Learn more](#linking-a-brand-to-a-template).

1. **Check deliverability guidelines** - Before starting using the new domain, the strategy should be discussed with Adobe Deliverability team. They will help to define the best practices, if a new affinity should be created to split the IPs between domains for example, and/or if a ramp up plan should be defined. Learn more about Deliverability best practices [in this section](../../sending/using/about-deliverability.md).
