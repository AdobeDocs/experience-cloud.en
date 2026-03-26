---
title: Java SDK release notes
description: Release notes for the Experience Rollouts Java SDK, including a changelog of new features, improvements, and bug fixes across all published versions.
exl-id: c6f6b1d1-54bc-4cfd-8574-506aa833b1a6
---
# Java SDK release notes {#java-sdk-release-notes}

This page lists the release history of the Experience Rollouts Java SDK. For integration setup, see [Java SDK integration guide](java-sdk-integration-guide.md).

## Version 4.0.6 {#v4-0-6}

**Control group data in responses**

You can now retrieve variant and control group data in the SDK response, matching the behavior of the REST Feature APIs. To enable this, add `.includeControlGroup()` to your `FloodgateConfiguration` builder.

## Version 4.0.5 {#v4-0-5}

**Stability and performance improvements**

Minor internal improvements to cache refresh reliability and connection handling.

## Version 4.0.4 {#v4-0-4}

**Retry policy improvements**

Improved default retry behavior on transient service errors.

## Version 4.0.3 {#v4-0-3}

**Bug fixes**

General stability fixes for edge cases in async initialization.

## Version 4.0.1 (Beta) {#v4-0-1-beta}

**Beta release of the 4.x SDK**

Introduced DX client support, DX region configuration, and AEP (sandbox) support.

## Version 3.1.0 {#v3-1-0}

**Streaming support for DX clients**

Added SSE-based streaming capability to notify SDK clients of flag updates in near real time.

## Version 3.0.x {#v3-0-x}

**Java 11 requirement introduced**

Starting with version 3.0.0, the SDK requires JDK 11 or later. Earlier major versions support JDK 8+.

Introduced audience-by-reference support for DX clients, allowing reusable audience definitions to be referenced by ID in feature entities.

## Version 2.x {#v2-x}

**Non-cacheable client support (from 0.8)**

Non-cacheable clients can call `getFeature()` live instead of reading from the SDK cache. The SDK continues polling in the background and switches to cache-based serving when the client becomes cacheable.

Additional 2.x improvements included new builder options (`alwaysCache()`, `neverCache()`, custom HTTP client and executor support), feature and release key filtering, and impersonated user retrieval.

## Version 1.x {#v1-x}

Initial release series. Supported JDK 8+, Maven dependency integration, and basic authenticated and anonymous feature flag retrieval.

## See also {#see-also}

* [Java SDK integration guide](java-sdk-integration-guide.md)
* [Node.js SDK release notes](../../sdk-releases/nodejs/nodejs-sdk-release-notes.md)
* [SDKs](../../integrate/sdks.md)
