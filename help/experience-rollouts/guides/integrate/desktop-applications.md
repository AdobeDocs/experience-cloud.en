---
title: Desktop applications
description: Learn how to integrate Adobe Experience Rollouts into a desktop application using the Feature API V2.
---

# Desktop applications {#desktop-applications}

Desktop applications integrate with Experience Rollouts by making direct REST API calls. Use the **Feature API V2** for desktop clients.

See **GET Feature API V2** in the Feature API section of this guide for the full API reference.

## Integration requirements {#requirements}

Desktop clients must:

* **Honor the TTL value** returned in the API response. The TTL defines how long the client should cache feature flag data before calling the API again. Implement a test case that validates this behavior to ensure older application versions enter hibernation correctly when no feature flags are being served.
* **Handle HTTP error scenarios gracefully**. Build in a fallback feature set so the application remains functional if the API is temporarily unavailable.
* **Maintain a detailed integration test plan** that covers both the TTL and error handling requirements above.

## Application ID {#app-id}

Desktop clients can use a **product code and product version** as the application identifier when calling the API, in place of a standard client ID.

## See also {#see-also}

* [Integration steps](integration-steps.md)
* [Startup guide](startup-guide.md)
