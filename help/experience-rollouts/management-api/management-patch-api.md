---
title: Management patch API
description: Use the Experience Rollouts PATCH API to update individual fields of a feature flag, feature group, or cross-team feature group without passing the full object.
---

# Management patch API {#management-patch-api}

The PATCH API lets you update specific fields of a feature flag, feature group, or cross-team feature group without sending the full object in the request body. This is useful for targeted updates such as changing an audience rule, toggling state, or adjusting a variation percentage.

## Feature flag PATCH {#feature-flag-patch}

Updates one or more fields of a feature flag.

| | |
|---|---|
| **Endpoint** | `PATCH /m/api/v1/mgmt/feature/{featureFlagId}` |
| **Method** | PATCH |

### Request headers {#ff-request-headers}

All requests require the headers described in the [common requirements](feature-management-apis-overview.md#common-requirements).

### Path parameter {#ff-path-param}

| Parameter | Type | Description | Required |
|---|---|---|---|
| `featureFlagId` | Integer | The numeric ID of the feature flag to update. | Yes |

### Request body {#ff-request-body}

Pass only the fields you want to update. The response always returns the complete updated feature flag object.

**Example — update description only:**

```json
{
  "description": "Updated description"
}
```

**Example — remove existing audience:**

```json
{
  "audience": null
}
```

**Example — add a new audience when none existed:**

```json
{
  "audience": [
    {
      "criteria": {
        "and": [
          { "operator": "EQ", "attr": "sandboxType", "val": "DEVELOPMENT", "ruleId": 1, "category": "contextual" }
        ]
      }
    }
  ]
}
```

**Example — update an existing audience rule:**

```json
{
  "audience": [
    {
      "id": 10020035,
      "criteria": {
        "and": [
          { "operator": "EQ", "attr": "sandboxType", "val": "PRODUCTION", "ruleId": 1, "category": "contextual" }
        ]
      }
    }
  ]
}
```

**Example — change state and variation percentage:**

```json
{
  "state": "disabled",
  "variations": [
    {
      "id": 10017188,
      "variantName": "Variation 1",
      "variantPercentage": 80.0
    }
  ]
}
```

>[!NOTE]
>
>When updating an existing audience rule, include the rule's `id` (available from the GET feature response) to update it in place. When updating variations, include the variation's `id` to avoid creating a duplicate.

### Response {#ff-response}

| Status | Description |
|---|---|
| `200` | Success. Response body is the complete updated feature flag object. |
| `400` | Invalid payload. |
| `403` | Insufficient permissions. |
| `417` | Concurrent update conflict. Fetch the current feature and retry. |

## Feature group PATCH {#feature-group-patch}

Updates one or more fields of a feature group. The request and response structure is the same as the feature flag PATCH — only the endpoint differs.

| | |
|---|---|
| **Endpoint** | `PATCH /m/api/v1/mgmt/group/{featureGroupId}` |
| **Method** | PATCH |

## Cross-team feature group PATCH {#ctfg-patch}

Updates one or more fields of a cross-team feature group. Uses the v2 release endpoint.

| | |
|---|---|
| **Endpoint** | `PATCH /m/api/v2/mgmt/release/{CTFGId}` |
| **Method** | PATCH |

## See also {#see-also}

* [Feature flags management API](feature-flags-management-api.md)
* [Feature group management API](feature-group-management-api.md)
* [Release management APIs](release-management-apis.md)
* [Feature management APIs overview](feature-management-apis-overview.md)
