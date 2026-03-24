---
title: Features, feature groups, and releases
description: Learn about the differences between feature flags, feature groups, cross-team feature groups, and releases in Adobe Experience Rollouts and when to use each.
exl-id: 241054a6-69f3-4349-b456-720b5ec55e1a
---
# Features, feature groups, and releases {#features-feature-groups-releases}

Experience Rollouts provides four artifacts for managing feature rollouts. Choosing the right one depends on the scope of your rollout, the number of teams involved, and the audience targeting capabilities you need.

## The four artifacts {#artifacts}

**Feature flag**
The most atomic unit. Controls a single feature for a single application, owned by one team. Can be enabled or disabled for a defined audience.

**Feature group**
A collection of feature flags belonging to the same team. Allows managing multiple flags across multiple applications in one team as a single unit.

**Cross-team feature group**
Extends feature group capabilities across multiple teams and applications. Self-serve and supports rich audience criteria, but does not support caching.

**Release**
Designed for large, coordinated rollouts across multiple teams and applications. Uses authentication token-based audience targeting. Supports caching on the server SDK.

## Comparison {#comparison}

| | Feature flag | Feature group | Cross-team feature group | Release |
|---|---|---|---|---|
| **Role required to manage audience** | Product Release Owner | Product Release Owner | Feature Admin | Release Manager |
| **Applications** | Single | Multiple (same team) | Multiple (cross-team) | Multiple (cross-team) |
| **Teams** | Single | Single | Cross-team | Cross-team |
| **Rich audience criteria** | ✓ | ✓ | ✓ | Limited |
| **Percentage rollout** | Combined with any audience criteria | Combined with any audience criteria | Combined with any audience criteria | Combined with fixed audience criteria |
| **A/B testing** | ✓ | ✓ | ✗ | ✗ |
| **Caching in server SDK** | Default on/off flags only | No caching | No caching | All releases cached locally |
| **Self-serve** | ✓ | ✓ | ✓ | Requires support request |
| **Audit trail** | ✓ | ✓ | ✓ | ✓ |

## When to use each {#when-to-use}

| Scenario | Use |
|---|---|
| Testing or rolling out a single feature for one application | **Feature flag** |
| Coordinating multiple features in the same team, going live at the same time | **Feature group** |
| Coordinating features across applications in different teams, with rich targeting | **Cross-team feature group** |
| Large coordinated release across multiple teams, with SDK-level caching | **Release** |

## See also {#see-also}

* [Create your first feature flag](create-your-first-feature-flag.md)
* [Create a feature group](create-a-feature-group.md)
* [Create a cross-team feature group](create-cross-team-feature-group.md)
* [Releases and cross-team feature groups](releases-and-cross-team-feature-groups.md)
