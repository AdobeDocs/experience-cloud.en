---
title: Sorting
description: Learn more how to perform sorting operations
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="LIMITED AVAILABILITY" type="Informative" url="../campaign-standard-migration-home.md" tooltip="Restricted to Campaign Standard migrated users"
---
# Sorting

Sorting is available by default in ascending order. To sort in descending order, append **%20desc** to the **_order** parameter's value.

To know if a field can be sorted, check the "sortable" parameter into the resource metadata. For more on this, refer to [this section](metadata-mechanism.md).

<br/>

***Sample requests***

* Sample GET request to retrieve emails in the database alphabetically ordered.

    ```

    -X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile/email?_order=email \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer <ACCESS_TOKEN>' \
    -H 'Cache-Control: no-cache' \
    -H 'X-Api-Key: <API_KEY>'

    ```

    Response to the request.

    ```

    {
    "content": [
        "adam@email.com",
        "allison.durance@example.com",
        "amy.dakota@mail.com",
        "andrea.johnson@mail.com",
        ...
    ]
    ...
    }

    ```

* Sample GET request to retrieve the email in the database in a descending alpha order.

    ```

    -X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile/email?_order=email%20desc \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer <ACCESS_TOKEN>' \
    -H 'Cache-Control: no-cache' \
    -H 'X-Api-Key: <API_KEY>'

    ```

    Response to the request.

    ```

    {
    "content": [
        "tombinder@example.com",
        "tombinder@example.com",
        "timross@example.com",
        "john.smith@example.com",
        ...
    ]
    }

    ```
