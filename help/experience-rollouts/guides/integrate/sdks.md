---
title: SDKs
description: Learn about the SDK architecture in Adobe Experience Rollouts and the available SDKs for Java and Node.js.
---

# SDKs {#sdks}

Experience Rollouts provides server-side SDKs for backend service integration. This page describes the SDK architecture and available options.

## SDK architecture {#architecture}

All Experience Rollouts SDKs share the same core architecture:

* **Initialization** — The SDK is configured via a `createInstance()` call that returns a singleton object.
* **Feature retrieval** — The `getFeatures()` method retrieves feature flag data from the SDK.
* **Caching** — The SDK caches responses from the Experience Rollouts service. A Cache Manager refreshes the cache on a configurable polling interval (TTL).
* **Error handling** — If the service returns a 503, the Cache Manager retains the existing cached data and continues serving feature flag evaluations. If data has not changed since the last call (304), the cache is not updated.

## Prerequisites {#prerequisites}

Before integrating an SDK, ensure you have the following:

1. **Application ID** — The client ID for each application onboarded in the Experience Rollouts console.
2. **Service token** — Used by the SDK to call the Experience Rollouts APIs in the background.
3. **API key** — Used alongside the service token for API authentication.

## Available SDKs {#available-sdks}

### Java SDK {#java-sdk}

The Java SDK is distributed via Maven. Add the dependency to your project's `pom.xml` to integrate. For Spring-based applications, the Maven dependency automatically sets up the SDK cache before your application fully loads.

Key specifications for the Java SDK:

* **Supported JDK:** JDK 8 and later
* **Non-cacheable clients:** Supported from SDK version 0.8 onward. For non-cacheable clients, `getFeature()` makes a live API call instead of reading from cache. The SDK continues polling in the background and switches to cache-based serving if the client becomes cacheable.

See the [Java SDK integration guide](../../sdk-releases/java/java-sdk-integration-guide.md) for setup instructions.

### Node.js SDK {#nodejs-sdk}

The Node.js SDK is distributed via npm.

See the [Node.js SDK integration guide](../../sdk-releases/nodejs/nodejs-sdk-integration-guide.md) for setup instructions.

## Choosing between SDK and REST API {#sdk-vs-api}

| Scenario | Recommendation |
|---|---|
| Backend Java or Node.js service | Use the appropriate SDK for automatic caching and simplified integration |
| Other backend language | Use the [Feature API V3](../../feature-api/get-feature-api-v3.md) directly |
| Web or mobile application | Use the [Feature API V3](../../feature-api/get-feature-api-v3.md) directly |
| Desktop application | Use the [Feature API V2](../../feature-api/get-feature-api-v2.md) directly |

## See also {#see-also}

* [Web services](web-services.md)
* [Integration steps](integration-steps.md)
* [Java SDK integration guide](../../sdk-releases/java/java-sdk-integration-guide.md)
* [Node.js SDK integration guide](../../sdk-releases/nodejs/nodejs-sdk-integration-guide.md)
