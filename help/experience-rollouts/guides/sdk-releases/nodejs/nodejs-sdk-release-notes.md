---
title: Node.js SDK release notes
description: Release notes for the Experience Rollouts Node.js SDK, including a changelog of new features, improvements, and bug fixes across all published versions.
---

# Node.js SDK release notes {#nodejs-sdk-release-notes}

This page lists the release history of the Experience Rollouts Node.js SDK. For integration setup, see [Node.js SDK integration guide](nodejs-sdk-integration-guide.md).

## Version 1.0.10 {#v1-0-10}

**Bug fixes and socket improvements**

* Fixed `ESOCKETTIMEDOUT` exception thrown during scheduled cache refreshes. Removed the `maxSockets` parameter from `featureRequestHttpParams` and `ingestAnalyticsHttpParams` in `createInstance()`.
* Fixed a bug where cacheable clients were incorrectly marked non-cacheable after HTTP 304 (Not Modified) responses.
* Removed `isReleaseBitEnabled()` — this method is no longer supported.
* Improved logging output for better diagnostics.
* Test and coverage folders are no longer included in the published npm package.

## Version 1.0.5 {#v1-0-5}

**Stability improvements**

General fixes to cache refresh handling and SDK initialization edge cases.

## Version 1.0.3 {#v1-0-3}

**Initial stable release**

First production release of the Node.js SDK supporting authenticated, anonymous, and default full-rollout feature flag retrieval.

## See also {#see-also}

* [Node.js SDK integration guide](nodejs-sdk-integration-guide.md)
* [Java SDK release notes](../../sdk-releases/java/java-sdk-release-notes.md)
* [SDKs](../../integrate/sdks.md)
