---
title: Recommendations & limitations
description: Recommendations & limitations when migrating to Campaign v8 REST APIs.
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="LIMITED AVAILABILITY" type="Informative" url="../campaign-standard-migration-home.md" tooltip="Restricted to Campaign Standard migrated users"
---
# Recommendations & limitations {#limitations}

## Filtering

To use your filters in REST API payloads, you need to edit them in Campaign v8 and provide a name to use in your payloads. To do so access the filter's additional parameters from the **[!UICONTROL Parameters]** tab, and provide the desired name in the **[!UICONTROL Filter name in REST API]** field.

![](assets/api-filtering.png)

## Product profiles mapping

In Campaign Standard, you were granted elevated admin role Campaign v8ess to APIs regardless of your assigned product profile. Campaign v8 introduces a different set of product profiles, requiring mapping from Campaign Standard to Campaign v8 product profiles.

With the migration, two product profiles are added to your existing or pre-created technical accounts: Administrator and Message center (for accessing transactional APIs). Review the product profile mapping and assign the needed product profile if you do not want the Admin product profile mapped with your technical account.

## Tenant ID

After migration, for any future integrations, it is recommended to use your **Campaign v8 tenant ID** in REST URLs, replacing your previous Campaign Standard tenant ID.

## Key usage

Management of PKey values differs between Campaign Standard and Campaign v8. If you were storing PKeys with Campaign Standard, ensure your implementation dynamically forms subsequent API calls using PKeys or hrefs obtained from previous API calls.

## Dropped database fields

Some fields from the database are being dropped during migration. When using a dropped field, REST APIs will return blank values. In the future, all dropped fields will be deprecated and removed.

<!--= https://wiki.corp.adobe.com/display/MSE/REST+API+Migration+%3A%3A+Profile#RESTAPIMigration::Profile-ProfilefieldspresentinCampaign StandardbutmissinginCampaign v8
on doit les lister ? lesquels sont dropped ou pas ?-->

## PATCH operations

* Campaign v8 does not support PATCH with an empty request body: it returns a 204 No Content status.
* While Campaign Standard supports PATCH on elements/attributes within a schema, note that PATCH operations on location are not supported in Campaign v8. Attempting a PATCH on location will result in a 500 Internal Server Error with an error message indicating that the 'zipCode' property is not valid for the 'profile' resource.
