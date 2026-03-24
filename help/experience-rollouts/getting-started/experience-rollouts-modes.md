---
title: Experience Rollouts modes
description: Learn about the two feature targeting modes in Adobe Experience Rollouts — user-level targeting and org-level targeting — and when to use each.
exl-id: 0fdfa429-d9bd-4990-8f96-cd9deb273aa0
---
# Experience Rollouts modes {#modes}

Experience Rollouts provides two distinct feature targeting modes. Each serves a different release control purpose and is designed for a specific type of application or use case.

>[!TIP]
>
>Choose the mode based on what you are controlling: individual user sessions or organization and environment scope.

## User-level targeting {#user-level}

### Overview {#user-level-overview}

User-level targeting enables feature rollout at the individual user level. It supports precise targeting of specific users, internal testers, canary users, and percentage-based gradual rollouts.

This mode is best suited for applications that need to vary the experience based on who is logged in.

### When to use {#user-level-when}

Use user-level targeting when you want to:

* Enable a feature for specific users
* Run A/B experiments
* Perform canary testing with a small group before a wider rollout
* Gradually roll out a feature by percentage of users
* Fine-tune the experience based on individual user attributes (such as email domain or profile data)

### Limitations {#user-level-limitations}

User-level targeting is not designed for the following scenarios:

* Does not control features at the organization, environment, or region level
* Not intended for tenant-wide feature enablement or entitlement gating

## Org and environment-level targeting {#org-level}

### Overview {#org-level-overview}

Org-level targeting enables feature rollout at the organization, environment, and region scope. It controls feature availability across entire organizations or specific deployment environments, rather than for individual users.

This mode is designed for enterprise-level feature gating and environment-specific rollouts.

### When to use {#org-level-when}

Use org-level targeting when you want to:

* Enable a feature for an entire organization
* Control feature availability by environment (for example, stage versus production)
* Perform a regional rollout
* Gate features based on entitlement or subscription tier

### Limitations {#org-level-limitations}

Org and environment-level targeting is not designed for the following scenarios:

* Does not support rich user profile-based targeting
* Does not support percentage-based rollout at the individual user level
* Not intended for experimentation or A/B testing

## Comparison {#comparison}

| Dimension | User-level targeting | Org and environment-level targeting |
|---|---|---|
| Control scope | Individual user | Organization, environment, region |
| Targeting basis | User profile and attributes | Org and environment context |
| Percentage rollout | Yes | No |
| A/B testing | Yes | No |
| Enterprise gating | No | Yes |

## Choosing the right mode {#choosing}

* If your question is *"Which users should see this feature?"* → Use **user-level targeting**
* If your question is *"Which organizations or environments should have this feature?"* → Use **org and environment-level targeting**
