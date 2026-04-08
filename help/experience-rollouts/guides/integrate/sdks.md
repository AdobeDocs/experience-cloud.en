---
title: SDKs
description: Learn about the SDK architecture in Adobe Experience Rollouts and the available mobile SDK extension for Android.
exl-id: 110a440d-b52a-4e1e-a94f-86f9741a223a
---
# SDKs {#sdks}

Experience Rollouts provides SDKs for integrating feature flags into your applications. This page describes the SDK architecture and available options.

## SDK architecture {#architecture}

All Experience Rollouts SDKs share the same core architecture:

* **Initialization** — The SDK is configured at startup and registers with the Experience Rollouts service.
* **Feature retrieval** — The SDK retrieves feature flag data and evaluates flags locally.
* **Caching** — The SDK caches feature flag data and refreshes it on a configurable polling interval (TTL).
* **Error handling** — If the service is unavailable, the SDK continues serving feature flag evaluations from the local cache.

## Available SDKs {#available-sdks}

### Android extension {#android-extension}

The Experience Rollout extension for Android integrates with the Adobe Experience Platform Mobile SDK.

See the [Android extension integration guide](../sdk-releases/android/android-extension-integration-guide.md) for setup instructions.

>[!NOTE]
>
>Additional SDK options for web and other mobile platforms are being prepared and will be available soon. Contact your Adobe representative for early access guidance.

## See also {#see-also}

* [Android extension integration guide](../sdk-releases/android/android-extension-integration-guide.md)
* [Web services](web-services.md)
* [Integration steps](integration-steps.md)
