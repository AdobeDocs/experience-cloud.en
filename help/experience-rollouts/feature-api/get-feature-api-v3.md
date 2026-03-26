---
title: GET Feature API V3
description: API reference for the Experience Rollouts Feature API V3, used to retrieve feature flags for web and mobile applications.
exl-id: a2c1b0be-2305-41d9-8e4f-bcf36694fb9b
---
# GET Feature API V3 {#get-feature-api-v3}

The Feature API V3 is the primary endpoint for retrieving feature flags in web and mobile applications. It returns the features and releases a user is eligible for, based on their identity and the audience rules configured in the console.

**Endpoint:** `GET {HOST}/fg/api/v3/feature`

Use `https://p13-stage.adobe.io` for Stage and `https://p13n.adobe.io` for Production.

## Request {#request}

### Request headers {#request-headers}

| Header | Type | Description | Required |
|---|---|---|---|
| `x-api-key` | String | Your application's API key from the Adobe Developer Console. Must be provisioned separately for Stage and Production. | Yes |
| `Authorization` | String | **Not required** for unauthenticated scenarios. Use `Bearer <AccessToken>` for authenticated users. Use `Bearer <ServiceToken>` for server-side SDK caching scenarios. | No |
| `x-adobe-uuid` | String | A unique visitor or device ID. Used to support percentage rollout for unauthenticated users and to maintain stickiness across sessions and unauthenticated-to-authenticated transitions. | No |

### Query parameters {#query-parameters}

| Parameter | Type | Description | Required |
|---|---|---|---|
| `clientId` | String | The client ID of your application, as onboarded in the Experience Rollouts console. | Yes |
| `ignore_rf` | Boolean | If `true`, release flags are ignored and all releases for the client are returned. Default: `false`. | No |
| `rf` | String | Release flag. Used only when `ignore_rf` is `false`. | No |
| `meta` | Boolean | If `true`, metadata for each feature is included in the response, returned as a key-value pair where the value is Base64-encoded. Default: `false`. | No |
| `userId` | String | Requires a service token. The GUID of the user for whom you want to retrieve feature flags. | No |
| *Context parameters* | N/A | Any query parameter not listed above is treated as a context variable and used to evaluate audience rules. Pass multiple values as `?key1=val1&key2=val2`. Example: `?clientLanguage=ja_JP&contractCurrency=JPY`. | No |

## Response {#response}

### Response status codes {#response-status}

| Status code | Description |
|---|---|
| `200 OK` | Feature flag data returned in the response body. |
| `304 Not Modified` | The ETag passed by the client matches the latest server state. Treat this as a no-op — no changes to apply. |
| `400 Bad Request` | The `clientId` is not onboarded or the request is malformed. |
| `403 Forbidden` | Invalid API key or the application is not subscribed to the Experience Rollouts API in the Adobe Developer Console. |

### Response headers {#response-headers}

| Header | Description |
|---|---|
| `x-request-id` | A unique request identifier for debugging. Include this in any support request. |
| `ETag` | A token representing the current server state for this user's features. Pass this value as `If-None-Match` in subsequent requests. If the state has not changed, the API returns `304`. |
| `x-adobe-fg-poll-interval` | The TTL (in seconds) for the client's local cache. Re-call the API only after this interval has elapsed. |

### Response body {#response-body}

The response is a JSON object with the following top-level fields:

| Field | Type | Description |
|---|---|---|
| `api_version` | String | API version. Internal field — no processing required. |
| `json_version` | String | JSON schema version. Internal field — no processing required. |
| `ttl` | Integer | Cache TTL in seconds. Same value as the `x-adobe-fg-poll-interval` response header. Default: 300. |
| `caching_enabled` | Boolean | If `true`, feature evaluation happens locally on the client. If `false`, evaluation happens server-side on each request. |
| `client_analytics_params` | Object | Analytics configuration for the application. See [client_analytics_params fields](#client-analytics-params) below. |
| `releases` | Array | List of releases and feature flags the user is eligible for. See [releases fields](#releases-fields) below. |

#### client_analytics_params fields {#client-analytics-params}

| Field | Description |
|---|---|
| `app_id` | The numeric ID of the application. |
| `safe_event_required` | `true` if retargeting events are enabled for this client. |
| `analytics_required` | Always `false` in V3 responses. |

#### releases fields {#releases-fields}

| Field | Description |
|---|---|
| `release_name` | The name of the release or feature group the user is eligible for. |
| `bit_index` | The release bit index. Negative values indicate a Full Rollout state. |
| `features` | Array of feature flag keys the user is eligible for. A feature key is returned only if the user is eligible and the flag is in an enabled state. This is the primary field your application logic should be built around. |
| `meta` | Optional Base64-encoded metadata associated with the feature. Decode before using. |
| `release_analytics_params` | Array of analytics metadata objects for each eligible feature. See [release_analytics_params fields](#release-analytics-params) below. In Control Group scenarios, `features` is empty. |

#### release_analytics_params fields {#release-analytics-params}

| Field | Type | Description |
|---|---|---|
| `app_id` | Integer | Application ID. |
| `release_id` | Integer | Release ID. |
| `bit_index` | Integer | Release bit index. Deprecated. |
| `variant_id` | Integer | `0` if the user is in the Control Group; non-zero otherwise. |
| `feature_id` | Integer | Internal feature ID. |
| `f_key` | String | Feature flag key. |

## Sample request and response {#sample}

### Sample request {#sample-request}

```http
GET /fg/api/v3/feature?clientId=MyWebApp&meta=true HTTP/1.1
Host: p13n.adobe.io
Authorization: Bearer <ACCESS_TOKEN>
x-api-key: <YOUR_API_KEY>
If-None-Match: <ETAG>
```

### Sample response — user in test group {#sample-response-test}

```json
{
  "api_version": "0.1",
  "json_version": "0.1",
  "clients": {
    "MyWebApp": {
      "analyticsVersion": "2.0",
      "client_analytics_params": {
        "app_id": 1378,
        "safe_event_required": false,
        "analytics_required": false
      },
      "releases": [
        {
          "bit_index": -160,
          "release_name": "||features||",
          "features": ["ff1", "ff2", "ff3"],
          "release_analytics_params": [
            {
              "app_id": 1378,
              "release_id": -1,
              "bit_index": -160,
              "variant_id": 10040476,
              "feature_id": 26059,
              "f_key": "ff1",
              "analytics_required": true
            }
          ]
        }
      ]
    }
  },
  "ttl": 60
}
```

### Sample response — user in control group {#sample-response-control}

When a user is in the Control Group, the `features` array is empty and `variant_id` is `0`:

```json
{
  "api_version": "0.1",
  "json_version": "0.1",
  "clients": {
    "MyWebApp": {
      "releases": [
        {
          "bit_index": -160,
          "release_name": "||features||",
          "features": [],
          "release_analytics_params": [
            {
              "app_id": 1378,
              "release_id": -1,
              "bit_index": -160,
              "variant_id": 0,
              "feature_id": 26059,
              "f_key": "ff1"
            }
          ]
        }
      ]
    }
  },
  "ttl": 60
}
```

## See also {#see-also}

* [GET Feature API V2](get-feature-api-v2.md)
* [Web applications](../guides/integrate/web-applications.md)
* [Mobile applications](../guides/integrate/mobile-applications.md)
* [Integration steps](../guides/integrate/integration-steps.md)
