---
title: SDKs
description: Learn about the SDK architecture in Flags and the available AEP Web SDK and AEP Mobile SDK extensions.
hide: true
exl-id: 110a440d-b52a-4e1e-a94f-86f9741a223a
---
# SDKs {#sdks}

Flags provides SDKs for integrating feature flags into your applications. Flags is deployed via the AEP Web SDK and AEP Mobile SDK.

## SDK architecture {#architecture}

All Flags SDKs share the same core architecture:

* **Initialization** — The SDK is configured at startup and registers with the Flags service.
* **Feature retrieval** — The SDK retrieves feature flag data and evaluates flags locally.
* **Caching** — The SDK caches feature flag data and refreshes it on a configurable polling interval (TTL).
* **Error handling** — If the service is unavailable, the SDK continues serving feature flag evaluations from the local cache.

## Available SDKs {#available-sdks}

### AEP Web SDK {#web-sdk}

The Flags extension for web integrates with the Adobe Experience Platform Web SDK, enabling flag evaluation in web applications.

### Android extension {#android-extension}

The Flags extension for Android integrates with the Adobe Experience Platform Mobile SDK.

See the [Android extension integration guide](../sdk-releases/android/android-extension-integration-guide.md) for setup instructions.

### iOS extension {#ios-extension}

The Flags extension for iOS integrates with the Adobe Experience Platform Mobile SDK.

See the [iOS extension integration guide](../sdk-releases/ios/ios-extension-integration-guide.md) for setup instructions.

## See also {#see-also}

* [Android extension integration guide](../sdk-releases/android/android-extension-integration-guide.md)
* [Web services](web-services.md)
* [Integration steps](integration-steps.md)

<!-- -->
