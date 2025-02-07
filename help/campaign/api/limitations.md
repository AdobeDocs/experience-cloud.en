---
title: Recommendations & limitations
description: Recommendations & limitations when migrating to Campaign v8 REST APIs.
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
mini-toc-levels: 1
badge: label="LIMITED AVAILABILITY" type="Informative" url="../campaign-standard-migration-home.md" tooltip="Restricted to Campaign Standard migrated users"
exl-id: 45acebb1-9325-4e26-8fe9-cc73f745d801
---
# Recommendations & limitations {#limitations}

## Permissions & security {#permissions} 

### Product profiles mapping

In Campaign Standard, you were granted elevated admin role access to APIs regardless of your assigned product profile. Campaign v8 introduces a different set of product profiles, requiring mapping from Campaign Standard to Campaign v8 product profiles.

With the migration, two product profiles are added to your existing or pre-created technical accounts: Administrator and Message center (for accessing transactional APIs). Review the product profile mapping and assign the needed product profile if you do not want the Admin product profile mapped with your technical account.

### Tenant ID

After migration, for any future integrations, it is recommended to use your **Campaign v8 tenant ID** in REST URLs, replacing your previous Campaign Standard tenant ID.

### Key usage

Management of PKey values differs between Campaign Standard and Campaign v8. If you were storing PKeys with Campaign Standard, ensure your implementation dynamically forms subsequent API calls using PKeys or hrefs obtained from previous API calls.

## Available APIs {#deprecated}

For now, the REST APIs listed below are available for use:

* **Profiles**
* **Services & subscriptions**
* **Custom resources**
* **Workflows**
* **Transactional messages**

>[!AVAILABILITY]
>
>For now, the **Transactional messages** REST API is not available.
>
>The REST APIs listed below are deprecated and not available for use:
>* Marketing history
>* Organizational units
>* Privacy management

## Filtering

* To use your filters in REST API payloads, you need to edit them in Campaign v8 and provide a name to use in your payloads. To do so access the filter's additional parameters from the **[!UICONTROL Parameters]** tab, and provide the desired name in the **[!UICONTROL Filter name in REST API]** field.

    ![](assets/api-filtering.png)


* The "by" prefix required to use custom filters is no longer needed. The filter name should be used as-is in your requests.

    Example:
    
    `GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServicesExt/<resourceName>/<customFilterName>?<customFilterparam>=<customFilterValue>`

## Dropped database fields

Some fields from the database are being dropped during migration. When using a dropped field, REST APIs will return blank values. In the future, all dropped fields will be deprecated and removed.

## POST with linked resources

When using the following request body format, with "vehicleOwner" representing the link to "nms:recipient":

```
{
    "vehicleNumber": "20009",
    "vehicleName": "Model E",
    "vehicleOwner":{
        "firstName":"tester 11",
        "lastName":"Smith 11"
    }
}
```

The link information is ignored. Consequently, a new record is generated under "cusVehicle" containing only "vehicleNumber" and "vehicleName" values. However, the link remains null, resulting in "vehicleOwner" being set to null.

In Campaign v8, when the same request body structure is used and the "vehicle" is linked to a profile, an error occurs. This error occurs because the "firstName" property is not recognized as valid for "cusVehicle.". However, a request body comprising only the attributes without the link functions without any issues.

## PATCH operations

* Campaign v8 does not support PATCH with an empty request body: it returns a 204 No Content status.
* While Campaign Standard supports PATCH on elements/attributes within a schema, note that PATCH operations on location are not supported in Campaign v8. Attempting a PATCH on location will result in a 500 Internal Server Error with an error message indicating that the 'zipCode' property is not valid for the 'profile' resource.

## REST responses

The section below lists minor differencies between Campaign Standard and v8 REST responses.

* For single GET records, the response includes the href in the response.
* When queried with the attribute, Campaign v8 provides Count and Pagination in the reponse.
* After POST operations, values from linked resources are returned in the response.

## Error codes and messages

The section below lists the differences between Campaign Standard and Campaign v8 error codes and messages.

|Scenario|Campaign Standard|Campaign v8|
|  ---  |  ---  |  ---  |
|Use an Invalid PKey in request Body|500 - 'O5iRp40EGA' attribute unknown (see definition of 'Profiles (nms:recipient)' schema). XTK-170036 Unable to parse expression '@id = @O5iRp40EGA'.|404 - Unable to decrypt PKey. (PKey=@jksad)|
|Use an Invalid PKey in URI|500 - 'O5iRp40EGA' attribute unknown (see definition of 'Profiles (nms:recipient)' schema). XTK-170036 Unable to parse expression '@id = @O5iRp40EGA'.|404 - Unable to decrypt PKey. (PKey=@jksad) Unsupported endpoint. (endpoint=rest/profileAndServices/profile/@jksad)|
|Using two different raw Pkeys in the URI and request body|500 - RST-360011 An error has occurred - please contact your administrator. RST-360012 Inconsistent operation on resource 'service' – Cannot update key 'SVC3' to 'SVC4'.|500 - An error has occurred - please contact your administrator.|
|Using PKey in the URI and a different raw PKey in the request body|500 - A 'Service' with the same key 'SVC4' already exists. PGS-220000 PostgreSQL error: ERROR:  duplicate key value violates unique constraint "nmsservice_name" DETAIL:  Key (sname)=(SVC4) already exists.|500 - An error has occurred - please contact your administrator.|
|Using non-existing raw-id in URI|404 - RST-360011 An error has occurred - please contact your administrator. Unable to find document with path 'Service' from key 'adobe_nl:0' (document with schema 'service' and name 'adobe_nl')|404 - Unable to find document with path 'Service' from key 'adobe_nl' (document with schema 'service' and name 'adobe_nl')|
|Using non-existing raw-id in request body|404 - RST-360011 An error has occurred - please contact your administrator. Unable to find document with path 'Service' from key 'adobe_nl' (document with schema 'service' and name 'adobe_nl')|404 - Unable to find document with path 'Service' from key 'adobe_nl' (document with schema 'service' and name 'adobe_nl')|
|-|500 - RST-360011 An error has occurred - please contact your administrator.|500 - An error has occurred - please contact your administrator.|
|Insert a profile/service with invalid gender (or anything) enum value|500 - RST-360011 An error has occurred - please contact your administrator. The value 'invalid' is not valid for the 'nms:recipient:gender' enumeration of the '@gender' field|500 -An error has occurred - please contact your administrator.|

## Profile - Timezone

With Campaign Standard, timezone is displayed as part of the JSON response of **profileAndServices/profile** REST API calls.

With Campaign v8, timezone is only shown to user as part of **profileAndServicesExt/profile** REST API calls. It is not part of **profileAndServices/profile** REST API calls since it is being added in an extended schema.

## Workflows - External Signal triggering

Campaign Standard Workflow GET API returns parameter names such as the workflow instance variables and their data types (boolean, string, etc.). This is used to create appropriately formatted JSON request body when triggering the signal via a POST API call.

Campaign v8 does not support advertising workflow instance variables, but expects developers to know what those are. As such, post-migration, parameters information in POST request body will need to be constructed without the availability of parameters information in GET API response. 

<!--## Transactional messages

* With Campaign Standard, a POST request returns empty fields for elements and attributes in the request body. With Campaign v8, the response returns values that match the ones in the request body instead.

* When publishing an event configuration, the API preview panel displays the REST URL alongside the request body syntax.

    Since Campaign v8 does not support event configuration fields definition (event creation is just adding a value to eventType enumeration), there is no API preview panel when adding an event type. The REST URL is displayed  in the transactional message user interface once an event transactional message is published.-->
