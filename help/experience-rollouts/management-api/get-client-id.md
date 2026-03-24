---
title: Get client ID for an application
description: Learn how to find the numeric client ID for an application in the Experience Rollouts console, which is required when calling the management APIs.
exl-id: cb7c3e30-eb1d-4028-8a4e-b72baa7c3712
---
# Get client ID for an application {#get-client-id}

The feature flags and feature group management APIs require a numeric `clientId` to identify which application the feature belongs to. This is different from the string-based IMS client ID used for API authentication.

Follow these steps to find the numeric client ID for an application.

## Steps {#steps}

To find the numeric client ID for an application, follow these steps:

1. Log in to the Experience Rollouts console.
2. Navigate to **Features & Releases**.
3. Select the **Feature Flags** tab.
4. Open the **Application** dropdown and select the application whose client ID you need.
5. Look at the URL in your browser's address bar. After `feature-flags/`, the number shown is the numeric client ID for that application.

For example, if the URL ends with `.../feature-flags/1191/...`, the client ID is `1191`.

## Use the client ID in API calls {#use-in-api}

Pass this value as the `clientId` parameter in management API requests. For example, when creating a feature flag:

```json
{
  "name": "my-feature-flag",
  "clientId": 1191,
  "state": "disabled"
}
```

## See also {#see-also}

* [Feature flags management API](feature-flags-management-api.md)
* [Feature group management API](feature-group-management-api.md)
* [Get desired audience criteria](get-audience-criteria.md)
