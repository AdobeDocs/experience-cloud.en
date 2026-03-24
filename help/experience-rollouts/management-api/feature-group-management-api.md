---
title: Feature group management API
description: API reference for the Experience Rollouts feature group management API, including endpoints to get, create, update, delete, and control rollout plans for feature groups.
---

# Feature group management API {#feature-group-management-api}

The feature group management API allows you to programmatically create, read, update, and delete feature groups in Experience Rollouts, including automated and A/B testing rollout plans.

**Base path:** `/m/api/v1/mgmt/group`

All requests require the headers described in the [common requirements](feature-management-apis-overview.md#common-requirements).

## Get all feature groups {#get-all-groups}

Retrieves all feature groups for your organization.

| | |
|---|---|
| **Endpoint** | `GET /m/api/v1/mgmt/group` |
| **Method** | GET |

### Query parameters {#get-all-query-params}

| Parameter | Type | Description | Required |
|---|---|---|---|
| `myOrg` | Boolean | Set to `true` to include organization information. | Yes |
| `includeClientInfo` | Boolean | Set to `true` to include application information for each group. | Yes |

### Response {#get-all-response}

| Status | Description |
|---|---|
| `200` | Success. Response body is an array of feature group objects. |

## Get feature group by ID {#get-group-by-id}

Retrieves a single feature group by its numeric ID.

| | |
|---|---|
| **Endpoint** | `GET /m/api/v1/mgmt/group/{groupId}` |
| **Method** | GET |
| **Query parameter** | `includeAnalyzeInfo=true` (optional — adds analytics data to the response) |

### Response {#get-by-id-response}

| Status | Description |
|---|---|
| `200` | Success. Response body is a feature group object. |
| `400` | Invalid feature group ID. |

## Create feature group {#create-group}

Creates a new feature group with a manual, automated, or A/B testing rollout type.

| | |
|---|---|
| **Endpoint** | `POST /m/api/v1/mgmt/group` |
| **Method** | POST |

### Request body {#create-request-body}

The request body uses the [feature group object](#feature-group-object). The `rolloutType` inside `params` is mandatory and determines the structure of the payload.

**Sample — manual rollout:**

```json
{
  "params": {
    "rolloutType": "manual",
    "label": "my-feature-group",
    "tags": [],
    "canContextOverridePUP": false
  },
  "status": "SAVED",
  "type": "group",
  "name": "my.feature.group",
  "description": "A manual feature group",
  "variations": [{ "variantPercentage": 100, "variantName": "Variant 1", "features": [] }],
  "audience": [{ "criteria": { "and": [{ "operator": "EQ", "attr": "COUNTRY", "val": "US", "ruleId": 1, "category": "default" }] } }],
  "clients": [],
  "org": { "id": 95 }
}
```

**Sample — automated rollout:**

```json
{
  "params": { "rolloutType": "automated", "label": "my-automated-group", "tags": [] },
  "status": "SAVED",
  "type": "group",
  "name": "my.automated.group",
  "variations": [{ "variantPercentage": 100, "variantName": "Variant 1", "features": [] }],
  "phaseRollOutPlan": {
    "phaseRollOutBlocks": [
      { "isPhaseBlock": true, "phaseRule": { "audience": [] }, "waitRule": null, "blockId": 1, "blockName": "", "isBlockActivated": false },
      { "isPhaseBlock": false, "phaseRule": null, "waitRule": { "waitDuration": { "val": "2", "unit": "HOURS" } }, "blockId": 2, "blockName": "", "isBlockActivated": false },
      { "isPhaseBlock": true, "phaseRule": { "audience": [] }, "waitRule": null, "blockId": 3, "blockName": "", "isBlockActivated": false }
    ],
    "rollOutPlanState": "DRAFT"
  },
  "clients": [],
  "org": { "id": 95 }
}
```

### Response {#create-response}

| Status | Description |
|---|---|
| `200` | Success. Response body is the created feature group object. |
| `400` | Invalid payload — see [error messages](#error-messages) for details. |
| `403` | Insufficient permissions. |

## Update feature group {#update-group}

Updates an existing feature group. Pass the same structure as the create request body, including the `id` field.

| | |
|---|---|
| **Endpoint** | `PUT /m/api/v1/mgmt/group` |
| **Method** | PUT |

### Response {#update-response}

| Status | Description |
|---|---|
| `200` | Success. Response body is the updated feature group object. |
| `400` | Invalid payload. |
| `403` | Insufficient permissions. |

## Pause, resume, or abort a rollout plan {#pause-resume-abort}

Controls the execution of an in-progress automated or A/B testing rollout plan.

| Action | Endpoint |
|---|---|
| **Resume** | `POST /m/api/v1/mgmt/phaserollout/resume` |
| **Pause** | `POST /m/api/v1/mgmt/phaserollout/pause` |
| **Abort** | `POST /m/api/v1/mgmt/phaserollout/abort` |

### Request body {#control-request-body}

```json
{
  "entityId": 10282,
  "fgEntityType": "GROUP"
}
```

### Response {#control-response}

Returns `true` on success.

## Delete feature group {#delete-group}

Deletes a feature group by its numeric ID.

| | |
|---|---|
| **Endpoint** | `DELETE /m/api/v1/mgmt/group/{groupId}` |
| **Method** | DELETE |

### Response {#delete-response}

| Status | Description |
|---|---|
| `204` | Success. No response body. |
| `403` | Insufficient permissions. |

## Feature group object reference {#feature-group-object}

| Field | Type | Description | Required |
|---|---|---|---|
| `id` | Integer | Feature group ID. Required only for update calls. | Conditional |
| `name` | String | Feature group key. Max 50 chars. Pattern: `^[a-zA-Z0-9_.-]*$` | Yes (create) |
| `clients` | Array | Applications associated with the group. Each entry must include `id` and `imsClientId`. | Yes |
| `status` | String | `"SAVED"` or `"PUBLISHED"` | Yes |
| `type` | String | Always `"group"` for feature groups. | Yes |
| `org` | Object | Organization details. Must include `id`. | Yes |
| `params` | Object | Group parameters. `rolloutType` is mandatory (`"manual"`, `"automated"`, or `"ab-testing"`). Also supports `label` and `tags`. | Yes |
| `audience` | Array | Audience rules for manual rollout types. | No |
| `variations` | Array | List of variants. See [FeatureGroupVariation object](#featuregroupvariation-object). | No |
| `phaseRollOutPlan` | Object | Phase rollout plan. Required for automated and A/B testing types. See [PhaseRollOutPlan object](#phaserolloutplan-object). | Conditional |
| `description` | String | Optional display description. Max 225 chars. | No |

### FeatureGroupVariation object {#featuregroupvariation-object}

| Field | Type | Description | Required |
|---|---|---|---|
| `id` | Integer | Variation ID. Required only for update calls. | Conditional |
| `variantName` | String | Variant name. Hardcoded to `"Variant 1"`. | Yes |
| `variantPercentage` | Decimal | Percentage of the audience receiving this variant. Range: (0, 100]. | Yes |

### PhaseRollOutPlan object {#phaserolloutplan-object}

| Field | Type | Description | Required |
|---|---|---|---|
| `phaseRollOutBlocks` | Array | Ordered list of phase blocks and wait blocks. The last block must be a phase block. | Yes |
| `rollOutPlanState` | String | `"DRAFT"`, `"RUNNING"`, `"PAUSED"`, or `"ABORTED"` | Yes |

Each block in `phaseRollOutBlocks` is either a **phase block** (`isPhaseBlock: true`) containing a `phaseRule` with audience criteria, or a **wait block** (`isPhaseBlock: false`) containing a `waitRule` with either a `waitDuration` (relative) or `executionDate` (fixed timestamp).

## Error messages {#error-messages}

| Condition | Status | Error message |
|---|---|---|
| Invalid or empty name | 400 | `Error: Invalid value for release name.` |
| Empty audience criteria | 400 | `Error: Release is not valid` |
| Multiple variations for automated type | 400 | `Error: Feature variation is not valid. Variation name should be unique across variations` |
| Published group with no clients | 400 | `Error: At least one client must be associated with enabled feature group.` |
| Last block in plan is not a phase block | 400 | `Error: The last block in the Phase Rollout plan should be phase block` |
| Wait block timings out of order | 400 | `Error: Wait block timings are not in order in the phase rollout plan` |
| Inconsistent wait block types | 400 | `Error: Wait block should be of same type.` |
| Editing an activated phase block | 400 | `Error: Activated phase block should not be changed` |
| Empty rollout type | 400 | `Error: Rollout type cannot be empty while feature group creation` |
| Phase plan passed with manual type | 400 | `Error: PhaseRollOutPlan can't be added with manual rollout type while feature group creation` |
| Schedule passed with PUBLISHED status | 400 | `Error: Schedule can't be added in published state while release/group creation` |

## See also {#see-also}

* [Feature management APIs overview](feature-management-apis-overview.md)
* [Feature flags management API](feature-flags-management-api.md)
* [Management patch API](management-patch-api.md)
* [Create an automated rollout](../guides/automated-rollouts/create-automated-rollout.md)
