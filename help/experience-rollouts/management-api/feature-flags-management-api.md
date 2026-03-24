---
title: Feature flags management API
description: API reference for the Experience Rollouts feature flags management API, including endpoints to get, create, update, and delete feature flags for an application.
exl-id: 027e9cfc-01ee-4270-8635-5d6086a67723
---
# Feature flags management API {#feature-flags-management-api}

The feature flags management API allows you to programmatically create, read, update, and delete feature flags for your applications in Experience Rollouts.

**Base path:** `/m/api/v1/mgmt/feature`

All requests require the headers described in the [common requirements](feature-management-apis-overview.md#common-requirements).

## Get all feature flags {#get-all-features}

Retrieves all feature flags for a specified application.

| | |
|---|---|
| **Endpoint** | `GET /m/api/v1/mgmt/feature` |
| **Method** | GET |

### Query parameters {#get-all-query-params}

| Parameter | Type | Description | Required |
|---|---|---|---|
| `clientId` | Integer | Numeric ID of the application. See [Get client ID](get-client-id.md). Required if `imsClientId` is not provided. | Conditional |
| `imsClientId` | String | String-format client ID of the application. Required if `clientId` is not provided. | Conditional |
| `nonReleaseFeature` | Boolean | Set to `true` to include independent feature flags not associated with any group or release. Required for API-based workflows. | Yes |

### Response {#get-all-response}

| Status | Description |
|---|---|
| `200` | Success. Response body contains a list of feature flag objects. |

The response body contains a `features` array. Each element is a feature flag object with the fields described in the [FeatureDTO object reference](#featuredto-object).

**Sample response:**

```json
{
  "features": [
    {
      "id": 22079,
      "name": "new.FF.1",
      "clientId": 1191,
      "state": "enabled",
      "description": "first feature flag",
      "release": { "id": 2631, "name": "FF.group", "status": "SAVED" },
      "audience": null,
      "params": { "label": "new FF 1", "rolloutType": "manual" }
    },
    {
      "id": 22080,
      "name": "new.FF.2",
      "clientId": 1191,
      "state": "enabled",
      "description": "second feature flag",
      "audience": [
        {
          "id": 10034665,
          "criteria": { "and": [{ "operator": "EQ", "attr": "LOCALE", "val": "EN" }] }
        }
      ]
    }
  ]
}
```

## Get feature flag by ID {#get-feature-by-id}

Retrieves a single feature flag by its numeric ID.

| | |
|---|---|
| **Endpoint** | `GET /m/api/v1/mgmt/feature/{featureId}` |
| **Method** | GET |

### Response {#get-by-id-response}

| Status | Description |
|---|---|
| `200` | Success. Response body is a single [FeatureDTO object](#featuredto-object). |
| `400` | Invalid feature ID. |

## Create feature flag {#create-feature}

Creates a new feature flag.

| | |
|---|---|
| **Endpoint** | `POST /m/api/v1/mgmt/feature` |
| **Method** | POST |

### Request body {#create-request-body}

The request body is a [FeatureDTO object](#featuredto-object). The following fields are required for creation:

| Field | Required | Notes |
|---|---|---|
| `name` | Yes | Feature flag key. Max 50 characters. Pattern: `^[a-zA-Z0-9_.-]*$` |
| `clientId` | Yes | Numeric application ID. See [Get client ID](get-client-id.md). |
| `state` | Yes | `"enabled"` or `"disabled"` |

### Response {#create-response}

| Status | Description |
|---|---|
| `200` | Success. Response body contains `{ "generatedFeatureId": <id> }`. |
| `400` | Invalid payload. |
| `403` | Insufficient permissions for this client or audience rule. |
| `417` | Users with the Developer role cannot save a feature with a public rule — at least one audience rule is required. |

**Sample request:**

```json
{
  "name": "my-new-feature",
  "clientId": 1191,
  "state": "disabled",
  "description": "A new feature flag",
  "meta": "VGVzdA==",
  "audience": [
    {
      "criteria": {
        "and": [{ "operator": "EQ", "attr": "COUNTRY", "category": "default", "ruleId": 1, "val": "US" }]
      }
    }
  ],
  "variations": [{ "variantPercentage": 100, "variantName": "Variation 1" }],
  "params": { "label": "My New Feature", "tags": [] }
}
```

## Update feature flag {#update-feature}

Updates an existing feature flag. Pass the complete [FeatureDTO object](#featuredto-object) including the `id` field.

| | |
|---|---|
| **Endpoint** | `PUT /m/api/v1/mgmt/feature` |
| **Method** | PUT |

### Response {#update-response}

| Status | Description |
|---|---|
| `200` | Success. Response body is the updated FeatureDTO object. |
| `400` | Invalid payload. |
| `403` | Insufficient permissions. |
| `417` | Concurrent update conflict. Fetch the current feature first and retry with the latest `version` value from `params`. |

## Delete feature flag {#delete-feature}

Deletes a feature flag by its numeric ID.

| | |
|---|---|
| **Endpoint** | `DELETE /m/api/v1/mgmt/feature/{featureId}` |
| **Method** | DELETE |

### Response {#delete-response}

| Status | Description |
|---|---|
| `204` | Success. No response body. |
| `403` | Insufficient permissions. |

## FeatureDTO object reference {#featuredto-object}

| Field | Type | Description | Required |
|---|---|---|---|
| `id` | Integer | Feature flag ID. Required only for update calls. | Conditional |
| `name` | String | Feature flag key (returned in API responses). Max 50 chars. Pattern: `^[a-zA-Z0-9_.-]*$` | Yes (create) |
| `clientId` | Integer | Numeric application ID. | Yes |
| `state` | String | `"enabled"` or `"disabled"` | Yes |
| `meta` | String | Base64-encoded metadata returned with the feature in API responses. Max 1024 chars. | No |
| `description` | String | Display description. Max 225 chars. | No |
| `audience` | Array | List of audience rules. See [FeatureRule object](#featurerule-object). Use [Get desired audience criteria](get-audience-criteria.md) to generate this. | No |
| `variations` | Array | List of variants. Max 3. See [FeatureVariation object](#featurevariation-object). | No |
| `params` | Object | Additional metadata. Supported keys: `label` (display name in UI), `tags` (string array). | No |
| `release` | Object | Release/group association. `null` if the flag is not in a group. Read-only. | No |

### FeatureVariation object {#featurevariation-object}

| Field | Type | Description | Required |
|---|---|---|---|
| `id` | Integer | Variation ID. Required only for update calls. | Conditional |
| `variantName` | String | Variant name. Fixed values: `"Variation 1"`, `"Variation 2"`, `"Variation 3"`. | Yes |
| `variantPercentage` | Decimal | Percentage of the audience receiving this variant. Must be greater than 0 and no more than 100, with up to 2 decimal places. | Yes |

### FeatureRule object {#featurerule-object}

| Field | Type | Description | Required |
|---|---|---|---|
| `id` | Integer | Rule ID. Required only for update calls. Set to `null` when adding a new rule. | Conditional |
| `criteria` | Object | Condition object defining the audience rule. See [Condition object](#condition-object). | Yes |

### Condition object {#condition-object}

| Field | Type | Description |
|---|---|---|
| `and` | Array\<Condition\> | All conditions must be true. |
| `or` | Array\<Condition\> | At least one condition must be true. |
| `not` | Condition | This condition must be false. |
| `attr` | String | The user attribute to evaluate (for example, `COUNTRY`, `LOCALE`). |
| `operator` | String | Comparison operator (for example, `EQ`, `IN`, `LT`). |
| `val` | String | The value to compare against. |
| `meta` | Object | Optional condition metadata. `desc` field sets the display label in the UI. |

Either one of `and`, `or`, or `not`, or a combination of `attr`, `operator`, and `val` must be provided in each Condition.

## See also {#see-also}

* [Feature management APIs overview](feature-management-apis-overview.md)
* [Management patch API](management-patch-api.md)
* [Get client ID for an application](get-client-id.md)
* [Get desired audience criteria](get-audience-criteria.md)
