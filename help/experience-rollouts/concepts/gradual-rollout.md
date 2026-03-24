---
title: Gradual rollout
description: Learn how gradual rollouts in Experience Rollouts let you phase feature delivery into production safely, with real-time feedback and minimal risk.
exl-id: c9d0e1f2-9999-4c3d-6e7f-8a9b0c1d2e3f
---

# Gradual rollout {#gradual-rollout}

A gradual rollout phases a new feature into production incrementally, rather than enabling it for all users at once. This approach reduces risk, helps manage backend load, and creates a tight feedback loop before full release.

## Benefits {#benefits}

**Safety net**
By releasing to a small audience first, you can track feedback and monitor behavior in production before expanding. If issues appear, the impact is limited and the feature can be turned off immediately — without a code change or redeployment.

**Backend load management**
Opening a feature to all users simultaneously can cause sudden spikes in server load. A gradual rollout distributes the increase in traffic over time, allowing infrastructure to scale smoothly.

**Real-time feedback**
Each phase of the rollout surfaces feedback from real users. Teams can act on that feedback — refining the experience, fixing edge cases, or adjusting messaging — before the next phase.

## How it works {#how-it-works}

Experience Rollouts provides granular targeting rules to increase user exposure step by step. A typical gradual rollout might follow this pattern:

1. Enable the feature for **1%** of users
2. Monitor feedback and performance metrics
3. Expand to **10%**, then **25%**, then **50%**
4. Reach **100%** once confidence is established

At every step, a single action can pause the rollout or turn off the feature entirely if something goes wrong.

## See also {#see-also}

* [Feature flags to enable and disable features](feature-flags-to-enable-disable-features.md)
* [Release management](release-management.md)
