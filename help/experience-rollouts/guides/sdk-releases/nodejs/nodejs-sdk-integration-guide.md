---
title: Node.js SDK integration guide
description: Learn how to integrate the Experience Rollouts Node.js SDK into your backend service to retrieve and evaluate feature flags.
---

# Node.js SDK integration guide {#nodejs-sdk-integration-guide}

The Experience Rollouts Node.js SDK is a server-side library intended for Node.js services. It caches feature flag data locally and evaluates flags without a synchronous API call on every request.

>[!NOTE]
>
>The Node.js SDK is designed for server-side use only. For client-side web applications, call the Feature API V3 REST endpoint directly.

## Prerequisites {#prerequisites}

Before integrating the Node.js SDK, ensure you have:

* A Node.js server-side application
* An **API key** and **service token** obtained through Adobe Developer Console — see [Subscribe to the API application](../../integrate/subscribe-to-api-application.md)
* Your **application client IDs** registered in the Experience Rollouts console — see [Onboard your application](../../applications/onboard-your-application.md)

## Install the SDK {#install}

Add the SDK to your project's `package.json`:

```json
"@floodgate/fg-client-sdk": "~1.0.10"
```

Then require it in your code:

```javascript
const { floodgateClient } = require('@floodgate/fg-client-sdk');
```

## Initialize the SDK {#initialize}

Call `createInstance()` once at application startup:

```javascript
floodgateClient.createInstance(
  {
    adobeIoApiKey: "<YOUR_API_KEY>",
    clientIds: ["<CLIENT_ID_1>", "<CLIENT_ID_2>"],
    env: "PRD",    // Use "STG" for Stage
    featureRequestHttpParams: {
      timeout: 60 * 1000  // Optional: request timeout in ms
    },
    ingestAnalyticsHttpParams: {
      timeout: 5 * 1000   // Optional: analytics timeout in ms
    }
  },
  function(cb) {
    // Fetch a fresh service token from IMS and pass it in the callback
    cb(null, SERVICE_TOKEN);
  },
  function() {
    return true;  // Return false to disable analytics
  },
  function(response) {
    // Called when the SDK initializes successfully
    console.log("SDK initialized");
  },
  function(err) {
    // Called if initialization fails
    console.error("SDK init error:", err);
  }
);
```

## Retrieve feature flags {#retrieve-features}

Feature flags are returned asynchronously in a callback. Choose the appropriate method based on your user context.

### Authenticated user {#authenticated-user}

```javascript
floodgateClient.getFeatures(
  {
    userAccessToken: "<USER_ACCESS_TOKEN>",
    visitorId: "<VISITOR_ID>",
    clientId1: "<CLIENT_ID>",
    meta: true
  },
  function(err, features) {
    if (err) {
      // Handle error and serve default experience
      return;
    }
    const isEnabled = floodgateClient.isFeatureEnabled(features, "MY_FEATURE_FLAG");
    // Serve experience based on isEnabled
  }
);
```

### Anonymous user {#anonymous-user}

When no user access token is available, use a release flag or omit the token to receive full-rollout releases:

```javascript
floodgateClient.getFeatures(
  {
    releaseFlag: "<RELEASE_FLAG>",
    visitorId: "<VISITOR_ID>",
    clientId1: "<CLIENT_ID>",
    meta: false
  },
  callback
);
```

### Default full-rollout releases {#default-releases}

When neither an access token nor a release flag is provided, the SDK returns features in **Full Rollout** or **Baseline** state:

```javascript
floodgateClient.getFeatures(
  {
    clientId1: "<CLIENT_ID>",
    visitorId: "<VISITOR_ID>",
    meta: false
  },
  callback
);
```

## Check if a feature is enabled {#check-feature}

```javascript
const isEnabled = floodgateClient.isFeatureEnabled(features, "MY_FEATURE_FLAG");

if (isEnabled) {
  // Serve the new experience
} else {
  // Serve the default experience
}
```

## Enable debug logging {#debug-logging}

To enable verbose SDK logs, pass a debug-level logger instance when calling `createInstance()`:

```javascript
const bunyan = require('bunyan');
const logger = bunyan.createLogger({ name: "fg", sourceType: "SDK", level: "debug" });

floodgateClient.createInstance(
  { ..., log: logger },
  ...
);
```

## See also {#see-also}

* [Node.js SDK release notes](nodejs-sdk-release-notes.md)
* [SDKs](../../integrate/sdks.md)
* [Subscribe to the API application](../../integrate/subscribe-to-api-application.md)
* [Integration steps](../../integrate/integration-steps.md)
