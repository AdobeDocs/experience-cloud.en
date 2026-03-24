---
title: Releases and cross-team feature groups
description: Learn the difference between releases and cross-team feature groups in Adobe Experience Rollouts and when to use each for coordinated multi-team rollouts.
---

# Releases and cross-team feature groups {#releases-and-cross-team}

Both releases and cross-team feature groups support coordinated rollouts across multiple teams and applications. The right choice depends on your caching requirements, audience targeting needs, and how much control you want over the process.

## Cross-team feature groups {#cross-team-feature-groups}

A cross-team feature group allows you to bundle feature flags from applications owned by different teams and manage them with rich audience criteria.

Key characteristics:

* **Self-serve** — No support request required to create one
* **Rich audience targeting** — Supports the full set of audience criteria (profile attributes, context variables, percentage rollout)
* **No limit** on the number you can create
* **No caching** — Feature flag evaluations require an API call; SDK-level caching is not supported

For step-by-step creation instructions, see [Create a cross-team feature group](create-cross-team-feature-group.md).

## Releases {#releases}

A release is designed for large, coordinated launches where caching at the SDK level is required. Releases use authentication token-based audience targeting.

Key characteristics:

* **Requires a support request** — Releases are not fully self-serve; contact Experience Rollouts support to create one
* **SDK caching** — All release data is cached locally in the server SDK, reducing API calls
* **Limited audience criteria** — Audience rules are based on authentication tokens (country, email, user ID, percentage, etc.)
* **Limited active releases** — A finite number of active releases can exist at a time; plan to close or baseline releases within three months

## Comparison {#comparison}

| | Cross-team feature group | Release |
|---|---|---|
| Self-serve | ✓ | Requires support request |
| Rich audience criteria | ✓ | Limited |
| A/B testing | ✗ | ✗ |
| SDK caching | ✗ | ✓ |
| Active limit | No limit | Limited |

## Recommendation {#recommendation}

If your use case involves rich audience targeting and self-serve management, use a **cross-team feature group**. If your backend services require SDK-level caching and the simpler audience criteria of releases is sufficient, use a **release**.

## See also {#see-also}

* [Features, feature groups, and releases](features-feature-groups-releases.md)
* [Create a cross-team feature group](create-cross-team-feature-group.md)
* [Request a release](request-a-release.md)
