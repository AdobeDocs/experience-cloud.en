---
title: Get desired audience criteria
description: Learn how to generate the correct audience criteria JSON structure for use in the Experience Rollouts management APIs by using the console and the GET feature API.
---

# Get desired audience criteria {#get-audience-criteria}

The audience criteria field in the management APIs uses a structured JSON format that can be complex to write by hand. The recommended approach is to build the desired audience using the console and then retrieve its JSON representation via the API.

## Steps {#steps}

To get the JSON for a desired audience criteria, follow these steps:

1. In the Experience Rollouts console, create a temporary feature flag with the audience criteria you want to use in your API call.
2. After saving, note the feature flag ID from the browser URL. The ID appears in the URL after the client ID. For example, in `.../feature-flags/1191/22080`, the feature ID is `22080`.
3. Call the [Get Feature by ID](feature-flags-management-api.md#get-feature-by-id) endpoint with that feature ID.
4. In the response JSON, locate the `audience` field. This contains the exact audience criteria structure you need.
5. Copy the `audience` value, removing the `id` attribute from each rule object. Use this in your Create or Update feature API call.

## Example {#example}

After calling GET `/m/api/v1/mgmt/feature/22080`, the response includes:

```json
{
  "audience": [
    {
      "id": 10034665,
      "criteria": {
        "and": [
          {
            "operator": "EQ",
            "attr": "LOCALE",
            "val": "EN",
            "ruleId": 1,
            "category": "default"
          }
        ]
      }
    }
  ]
}
```

To use this in a Create feature call, remove the `id` field from the audience object:

```json
{
  "audience": [
    {
      "criteria": {
        "and": [
          {
            "operator": "EQ",
            "attr": "LOCALE",
            "val": "EN",
            "ruleId": 1,
            "category": "default"
          }
        ]
      }
    }
  ]
}
```

## See also {#see-also}

* [Feature flags management API](feature-flags-management-api.md)
* [Get client ID for an application](get-client-id.md)
* [Management patch API](management-patch-api.md)
