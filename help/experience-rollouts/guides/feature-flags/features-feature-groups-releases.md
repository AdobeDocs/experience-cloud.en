---
title: Features and feature groups
description: Learn about the differences between feature flags and feature groups in Adobe Experience Rollouts and when to use each.
---

# Features and feature groups {#features-feature-groups}

Experience Rollouts provides two artifacts for managing feature rollouts. Choosing the right one depends on the scope of your rollout and the number of features involved.

## The two artifacts {#artifacts}

**Feature flag**
The most atomic unit. Controls a single feature for a single application. Can be enabled or disabled for a defined audience.

**Feature group**
A collection of feature flags belonging to the same team. Allows managing multiple flags across multiple applications as a single unit.

## Comparison {#comparison}

| | Feature flag | Feature group |
|---|---|---|
| **Role required to manage audience** | Product Release Owner | Product Release Owner |
| **Applications** | Single | Multiple (same team) |
| **Rich audience criteria** | ✓ | ✓ |
| **Percentage rollout** | Combined with any audience criteria | Combined with any audience criteria |
| **A/B testing** | ✓ | ✓ |
| **Self-serve** | ✓ | ✓ |
| **Audit trail** | ✓ | ✓ |

## When to use each {#when-to-use}

| Scenario | Use |
|---|---|
| Testing or rolling out a single feature for one application | **Feature flag** |
| Coordinating multiple features in the same team, going live at the same time | **Feature group** |

## See also {#see-also}

* [Create your first feature flag](create-your-first-feature-flag.md)
* [Create a feature group](create-a-feature-group.md)
