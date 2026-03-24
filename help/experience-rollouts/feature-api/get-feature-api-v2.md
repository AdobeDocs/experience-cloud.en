---
title: GET Feature API V2
description: API reference for the Experience Rollouts Feature API V2, used to retrieve feature flags for desktop applications.
exl-id: c1e63d57-2a5f-48f6-8b2c-8d83a5c39b4b
---
# GET Feature API V2 {#get-feature-api-v2}

The Feature API V2 is designed for desktop application integration. It retrieves feature flags and release data for the authenticated user, supporting product code and product version as the application identifier in addition to a standard client ID.

**Endpoint:** `GET {HOST}/fg/api/v2/feature`

Use `https://p13-stage.adobe.io` for Stage and `https://p13n.adobe.io` for Production.

## Request {#request}

### Request headers {#request-headers}

| Header | Type | Description | Required |
|---|---|---|---|
| `x-api-key` | String | Your application's API key from the Adobe Developer Console. Must be provisioned separately for Stage and Production. | Yes |
| `Authorization` | String | `Bearer <AccessToken>` or `Bearer <ServiceToken>`. | Yes |
| `x-adobe-uuid` | String | A unique visitor or device ID. Used for percentage rollout in unauthenticated scenarios and to maintain session stickiness. | No |

### Query parameters {#query-parameters}

| Parameter | Type | Description | Required |
|---|---|---|---|
| `clientId` | String | The client ID of the application, as onboarded in the Experience Rollouts console. Multiple values can be passed: `clientId=C1&clientId=C2`. | No |
| `p` | String | Product, version, platform, locale string (PVPL format). Example: `PHSP:17.0:WIN:en_US`. Multiple values can be passed: `p=PHSP:17.0:WIN:en_US&p=PPRO:8:WIN:en_US`. Only product code and product version are used in evaluation. | No |
| `meta` | Boolean | If `true`, Base64-encoded metadata is returned for each feature. Default: `false`. | No |
| *Context parameters* | N/A | Any additional key-value pair is treated as a context variable for audience rule evaluation. Example: `clientLanguage=ja_JP&contractCurrency=JPY`. | No |

>[!NOTE]
>
>At least one of `clientId` or `p` is required to identify the application.

## Response {#response}

### Response status codes {#response-status}

| Status code | Description |
|---|---|
| `200 OK` | Feature flag data returned in the response body. |
| `304 Not Modified` | The ETag matches the current server state. Treat as a no-op — no changes to apply. |
| `401 Unauthorized` | The authorization token is invalid. |

### Response headers {#response-headers}

| Header | Description |
|---|---|
| `x-request-id` | A unique request identifier for debugging. Include this in any support request. |
| `ETag` | Token representing the current feature state for the user. Pass as `If-None-Match` in subsequent requests. Returns `304` if unchanged. |
| `x-adobe-fg-poll-interval` | TTL in seconds for the client's local cache. Re-call the API only after this interval elapses. |

### Response body {#response-body}

The response is a JSON object with the following top-level fields:

| Field | Type | Description |
|---|---|---|
| `api_version` | String | API version. Internal field — no processing required. |
| `json_version` | String | JSON schema version. Internal field — no processing required. |
| `ttl` | Integer | Cache TTL in seconds. Default: 300. |
| `clients` | Object | Map of client IDs (or PVPL strings) to their release data. Each key contains the fields described below. |

#### Per-client response fields {#per-client-fields}

| Field | Description |
|---|---|
| `releases` | Array of releases the user is eligible for. See [releases fields](#releases-fields) below. |
| `client_analytics_params` | Analytics configuration object. See [client_analytics_params fields](#analytics-fields) below. |

#### releases fields {#releases-fields}

| Field | Description |
|---|---|
| `release_name` | Name of the release or feature group. |
| `bit_index` | Release bit index. Deprecated. May be `null` or negative depending on release state. |
| `features` | Array of feature flag keys the user is eligible for. A feature key appears only if the user is eligible and the flag is enabled. |
| `meta` | Optional Base64-encoded metadata. Decode before using. |
| `release_analytics_params` | Analytics metadata for eligible features. In Control Group scenarios, `features` is empty. |

#### release_analytics_params fields {#release-analytics-params}

| Field | Type | Description |
|---|---|---|
| `app_id` | Integer | Application ID. |
| `release_id` | Integer | Release ID. |
| `bit_index` | Integer | Deprecated. |
| `variant_id` | Integer | `0` if Control Group; non-zero otherwise. |
| `feature_id` | Integer | Internal feature ID. |
| `f_key` | String | Feature flag key. |

#### client_analytics_params fields {#analytics-fields}

| Field | Type | Description |
|---|---|---|
| `app_id` | Integer | Application ID. |
| `safe_event_required` | Boolean | `true` if retargeting events are enabled. |
| `analytics_required` | Boolean | `false` if analytics is disabled or on default flow; `true` if Kinesis flow is enabled. |

## Sample request and response {#sample}

### Sample request {#sample-request}

```http
GET /fg/api/v2/feature?clientId=MyDesktopApp&p=PHSP:17.0:WIN:en_US&meta=true HTTP/1.1
Host: p13n.adobe.io
Authorization: Bearer <ACCESS_TOKEN>
x-api-key: <YOUR_API_KEY>
If-None-Match: <ETAG>
```

### Sample response {#sample-response}

```json
{
  "api_version": "0.1",
  "json_version": "0.1",
  "clients": {
    "PHSP:17.0:WIN:en_US": {
      "analyticsVersion": "1.0",
      "releases": []
    },
    "MyDesktopApp": {
      "analyticsVersion": "1.0",
      "client_analytics_params": {
        "app_id": 388,
        "safe_event_required": false,
        "analytics_required": false
      },
      "releases": [
        {
          "bit_index": 160,
          "release_name": "||features||",
          "features": ["feature_a", "feature_b"],
          "release_analytics_params": [
            {
              "app_id": 388,
              "release_id": -1,
              "bit_index": 160,
              "variant_id": 10031741,
              "feature_id": 2918,
              "f_key": "feature_a"
            }
          ],
          "meta": []
        }
      ]
    }
  },
  "ttl": 300
}
```

## See also {#see-also}

* [GET Feature API V3](get-feature-api-v3.md)
* [Desktop applications](../guides/integrate/desktop-applications.md)
* [Integration steps](../guides/integrate/integration-steps.md)
