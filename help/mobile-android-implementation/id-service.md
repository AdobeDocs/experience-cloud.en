---
title: Implement the Experience Cloud ID Service with Launch
description: Learn how to add the Experience Cloud ID Service extension and use the Set Customer IDs action to collect customer ids. This lesson is part of the Implementing the Experience Cloud in Mobile Android Applications tutorial.
seo-description:
seo-title: Implement the Experience Cloud ID Service with Launch
solution: Experience Cloud
---

# Add the Experience Cloud ID Service

The [Experience Cloud ID Service](https://marketing.adobe.com/resources/help/en_US/mcvid/) sets a common visitor id across all Adobe solutions in order to power Experience Cloud capabilities such as audience-sharing between solutions.  You can also send your own customer ids to the Service to enable cross-device targeting and integrations with your Customer Relationship Management (CRM) system.

The ID Service is part of the Mobile Core extension, so you have already implemented it! At present time, this tutorial does not include instructions for setting Customer Ids. Please see the documentation for details on [how to set Customer Ids](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference).

## Validation Steps

To validate the calls to the ID Service, run the sample app in Android Studio, open the Debug Console and look for the request and the response:

1. **Request to the ID Service** (filter Logcat to `IdentityExtension`) In this example, the ID (`d_mid`)has already been set and is just being reported up again)

    ```java
    03-14 17:01:18.526 7743-7803/com.adobe.busbooking D/ADBMobile: IdentityExtension - Sending request (https://dpm.demdex.net/id?d_mid=59651426340521082405908216148091920022&d_ver=2&d_orgid=7ABB3E6A5A7491460A495D61%40AdobeOrg)
    ```

1. **Response from the ID Service** (filter Logcat to `IdentityExtension`). Note how the `mid` value matches the `d_mid` value in the request above:

    ```java
    03-14 17:01:19.033 7743-7803/com.adobe.busbooking D/ADBMobile: IdentityExtension - Received ID response (mid: 59651426340521082405908216148091920022, blob: j8Odv6LonN4r3an7LhD3WZrU1bUpAkFkkiY1ncBR96t2PTI, hint: 9, ttl: 604800
    ```

[Next "Add Adobe Target VEC Support" >](target-vec.md)
