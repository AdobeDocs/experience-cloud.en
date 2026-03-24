---
title: Release management APIs
description: API reference for the Experience Rollouts release management APIs, including endpoints to get, create, and edit releases and cross-team feature groups.
---

# Release management APIs {#release-management-apis}

The release management APIs let you retrieve, create, and edit releases and cross-team feature groups (CTFG) programmatically. These APIs use the v2 management endpoint.

**Base path:** `/m/api/v2/mgmt/release`

All requests require the headers described in the [common requirements](feature-management-apis-overview.md#common-requirements), plus the additional header listed below.

### Additional required header {#additional-header}

| Header | Description | Required |
|---|---|---|
| `x-user-context-org` | The numeric Team ID for your organization. You can find this value in the Experience Rollouts console under your team settings. | Yes |

## Get release by ID {#get-release}

Retrieves a single release or cross-team feature group by its numeric ID.

| | |
|---|---|
| **Endpoint** | `GET /m/api/v2/mgmt/release/{id}` |
| **Method** | GET |

### Query parameters {#get-query-params}

| Parameter | Type | Description | Default |
|---|---|---|---|
| `includePermissions` | Boolean | Include permissions for updating or deleting this release. | `true` |
| `includeOrg` | Boolean | Include organization information for this release. | `true` |
| `includeAnalyzeInfo` | Boolean | Include analytics information. | `false` |

### Response {#get-response}

| Status | Description |
|---|---|
| `200` | Success. Response body is a release object — see [Release object reference](#release-object). |
| `400` | Invalid release ID or malformed request. |

## Create release {#create-release}

Creates a new release or cross-team feature group.

| | |
|---|---|
| **Endpoint** | `POST /m/api/v2/mgmt/release` |
| **Method** | POST |

### Request body {#create-request-body}

The request body uses the [Release object](#release-object). For creation, `status` must be set to `"SAVED"` for cross-team feature groups (`CROSS_TEAM_FEATURE_GROUP` type) or `"DRAFT"` for standard releases (`RELEASE` type).

**Sample — create cross-team feature group:**

```json
{
  "params": {
    "rolloutType": "manual",
    "cohortingType": "guid",
    "tags": [],
    "canContextOverridePUP": false,
    "label": "my-cross-team-group"
  },
  "status": "SAVED",
  "type": "CROSS_TEAM_FEATURE_GROUP",
  "name": "my-cross-team-group",
  "description": null,
  "meta": "",
  "variations": [{ "variantPercentage": 100, "variantName": "Variant 1", "features": [] }],
  "audience": [{}],
  "clients": [],
  "pollInterval": 300,
  "org": { "id": "95" },
  "comment": ""
}
```

### Response {#create-response}

| Status | Description |
|---|---|
| `200` | Success. Response body is the created release object. |
| `400` | Invalid payload. |

## Edit release {#edit-release}

Updates an existing release or cross-team feature group. Pass the full release object including the `id` field.

| | |
|---|---|
| **Endpoint** | `PUT /m/api/v2/mgmt/release/{id}` |
| **Method** | PUT |

### Response {#edit-response}

| Status | Description |
|---|---|
| `200` | Success. Response body is the updated release object. |
| `417` | Concurrent update conflict. The release was modified between your GET and PUT calls. Fetch the current release and retry. |

## Release object reference {#release-object}

| Field | Type | Description | Required |
|---|---|---|---|
| `id` | Integer | Release ID. Required only for update calls. | Conditional |
| `name` | String | Release name. Max 50 chars. Pattern: `^[a-zA-Z0-9_ ,.:()-]*$`. Must be unique. | Yes |
| `description` | String | Optional description. Max 255 chars. | No |
| `type` | String | `"RELEASE"` for standard releases; `"CROSS_TEAM_FEATURE_GROUP"` for cross-team feature groups. | Yes |
| `status` | String | Release state. For IMS: `"DRAFT"` on create; `"DRAFT"`, `"SAVED"`, `"PUBLISHED"` on update. For CTFG: `"SAVED"` on create; `"SAVED"`, `"PUBLISHED"` on update. | Yes |
| `clients` | Array | Applications associated with this release. Each entry requires `id` (numeric) and `imsClientId` (string). | No |
| `audience` | Array | List of audience rules. See [Condition object](feature-flags-management-api.md#condition-object). | No |
| `variations` | Array | List of variations. Only 1 variation is supported during submission. | Required for submission |
| `params` | Object | Release parameters. See [Supported params fields](#supported-params). | Required for submission |
| `org` | Object | Organization object. Must include `id`. | No |

### Supported params fields {#supported-params}

| Field | Type | Description | Required |
|---|---|---|---|
| `label` | String | Display name. Max 50 chars. | Yes |
| `tags` | Array\<String\> | Optional tags. Max 50 chars each. | No |
| `canContextOverridePUP` | Boolean | If `true`, context rules override profile rules. Default: `false`. | Yes |
| `isBetaRelease` | Boolean | If `true`, marks this as a beta release. Default: `false`. | No |

### Variation object {#variation-object}

| Field | Type | Description | Required |
|---|---|---|---|
| `id` | Integer | Variation ID. Required only for update calls. | Conditional |
| `variantName` | String | Variant name. Max 50 chars. | Yes |
| `variantPercentage` | Double | Percentage of the audience receiving this variant. Range: [0, 100]. | Yes |
| `features` | Array | Features included in this variation. Each entry must include `id`, `name`, `clientId`, and `state`. | No |

## See also {#see-also}

* [Feature management APIs overview](feature-management-apis-overview.md)
* [Feature flags management API](feature-flags-management-api.md)
* [Feature group management API](feature-group-management-api.md)
* [Create a cross-team feature group](../guides/feature-flags/create-cross-team-feature-group.md)
