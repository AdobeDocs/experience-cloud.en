---
title: Endpoints
description: Learn more about the APIs endpoints.
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
exl-id: 9f6d3da6-374d-47f5-bc8f-b31b19cbb5ca
---
# Endpoints {#endpoints}

The available endpoints for Adobe Campaign REST API:

* **/profileAndServices**: interact with out of the box fields. Extended fields are not accessible with this endpoint.
* **/profileAndServicesExt**: interact with custom fields added during Profile or Services custom resource extension. For more on custom resources, refer to [this section](custom-resources.md).
* **/&lt;transactionalAPI&gt;**: interact with the transactional messages API (the name of the transactional messages API endpoint depends on your instance configuration). For more on this, refer to [this section](managing-transactional-messages.md).
* **/workflow/execution**: interact with workflows. For more on this, refer to [this section](controlling-a-workflow.md).

By default, the main resources available for the **profileAndServices** and **profileAndServicesExt** APIs are:

* **/profile**: interact with profiles from Campaign database. To add profiles to a service, use the **/service** endpoint. For more on profiles in Campaign, refer to the [Campaign documentation](https://helpx.adobe.com/campaign/standard/audiences/using/about-profiles.html).
* **/service**: manage subscription services. For more on services in Campaign, refer to the [Campaign documentation](https://helpx.adobe.com/campaign/standard/audiences/using/creating-a-service.html).

>[!NOTE]
>
>All other resources that have been extended or created are available via the **ProfileAndServicesExt** API only. They must be linked to the **Profile** resource in order to be accessible.
