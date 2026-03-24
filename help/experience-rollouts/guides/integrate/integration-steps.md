---
title: Integration steps
description: Follow the integration steps for your application type to connect Adobe Experience Rollouts to your web service, web or mobile app, or desktop application.
---

# Integration steps {#integration-steps}

Choose the integration path that matches your application type.

## Web services {#web-services}

Backend services integrate using a server-side SDK. Choose the SDK for your technology stack.

**Java**

Follow the [Java SDK integration guide](../../sdk-releases/java/java-sdk-integration-guide.md) for setup, dependency configuration, and initialization.

**Node.js**

Follow the [Node.js SDK integration guide](../../sdk-releases/nodejs/nodejs-sdk-integration-guide.md) for setup and initialization.

**Other languages**

If your stack is not listed above, integrate directly with the [Feature API V3](../../feature-api/get-feature-api-v3.md). Contact Experience Rollouts support if you need guidance.

## Web and mobile applications {#web-mobile}

Web and mobile applications call the **Feature API V3** to retrieve feature flags for the current user and apply conditional logic in the application.

See [GET Feature API V3](../../feature-api/get-feature-api-v3.md) for the full API reference.

## Desktop applications {#desktop}

Desktop applications call the **Feature API V2** to retrieve feature flags.

See [GET Feature API V2](../../feature-api/get-feature-api-v2.md) for the full API reference.

>[!IMPORTANT]
>
>Desktop clients must honor the TTL value in the API response and implement graceful error handling for API unavailability. See [Desktop applications](desktop-applications.md) for requirements.

## See also {#see-also}

* [Startup guide](startup-guide.md)
* [SDKs](sdks.md)
* [Web services](web-services.md)
* [Desktop applications](desktop-applications.md)
