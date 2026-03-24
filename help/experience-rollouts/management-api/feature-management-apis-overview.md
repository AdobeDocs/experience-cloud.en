---
title: Feature management APIs overview
description: Overview of the Experience Rollouts management APIs, which allow you to create, read, update, and delete feature flags, feature groups, and releases programmatically.
---

# Feature management APIs overview {#feature-management-apis-overview}

The Experience Rollouts management APIs let you manage feature flags, feature groups, and releases programmatically. Teams that need to automate workflows or integrate Experience Rollouts into existing deployment pipelines can use these APIs instead of the console.

>[!NOTE]
>
>Access to the management APIs using a service token is granted on request. Contact Experience Rollouts support and provide a business justification to request access.

## Available management APIs {#available-apis}

The following management APIs are available:

* [Feature flags management API](feature-flags-management-api.md) — Create, read, update, and delete feature flags for an application.
* [Feature group management API](feature-group-management-api.md) — Create, read, update, and delete feature groups.
* [Release management APIs](release-management-apis.md) — Create and edit cross-team feature groups and releases.

## Common requirements {#common-requirements}

All management API calls require the following:

* An **API key** from the Adobe Developer Console — see [Subscribe to the API application](../guides/integrate/subscribe-to-api-application.md).
* An **IMS user access token** or **service token**, passed as `Bearer <token>` in the `Authorization` header.
* A `Content-Type: application/json` header.

API keys and tokens must be provisioned separately for Stage and Production environments.

## Helper guides {#helper-guides}

The following guides assist with building correct API payloads:

* [Get client ID for an application](get-client-id.md) — Look up the numeric client ID required by the feature flags and feature group management APIs.
* [Get desired audience criteria](get-audience-criteria.md) — Use the console and the GET API to generate the correct audience criteria JSON structure.
* [Management patch API](management-patch-api.md) — Update individual fields of a feature flag, feature group, or cross-team feature group without passing the full object.

## See also {#see-also}

* **GET Feature API V3** and **GET Feature API V2** — see the Feature API section of this guide for the full references.
* [Subscribe to the API application](../guides/integrate/subscribe-to-api-application.md)
