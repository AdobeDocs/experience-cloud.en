---
title: Feature flags to enable and disable features
description: Learn how feature flags in Experience Rollouts let you control feature availability, manage dependencies, and reduce deployment risk.
---

# Feature flags to enable and disable features {#feature-flags}

Feature flags let you turn application features on or off at runtime without redeploying code. They also separate code deployments from feature availability — new code can be deployed to production behind a flag and switched on only when you are ready.

This practice significantly reduces risk. Developers can build with agility and confidence, while product teams retain control over the timing and audience of every feature release.

## Manage dependencies during development {#manage-dependencies}

Feature flags help manage dependencies when testing in rapid development cycles. Developers spend less time resolving merge conflicts and refactoring, and more time delivering features.

Because feature availability is controlled outside of the code, multiple features can be developed in parallel — without complex branching. Individual features can be rolled forward or back independently, without affecting other features in progress.

## Dark deployments {#dark-deployments}

Because enable and disable decisions live outside the codebase, you can deploy code to production while keeping the feature invisible to end users. This is called a **dark deployment**.

Dark deployments let you push code safely to production, test it in the live environment against real conditions, and go live when you choose — not when the deployment schedule forces you to.

## Gradual rollout {#gradual-rollout}

When you are ready to release, you can use a feature flag to perform a **gradual rollout**: open the feature to 1% of users, measure feedback and performance, then increase progressively.

This rolling approach gives you tighter control over the experience you deliver and a faster feedback loop with real users, so your teams can respond quickly before a full release.

## Kill switch {#kill-switch}

If a release does not go as planned — unfavorable feedback, a bug, or a performance issue — you can turn the feature off immediately using the feature flag as a **kill switch**. No code change or redeployment is needed.

## Feature flag lifecycle {#lifecycle}

A feature flag in Experience Rollouts follows this typical lifecycle:

1. A developer creates a feature flag and tests it in isolation — without exposing it to other users.
2. A product owner links an audience to the flag, making the feature visible to a defined set of external users.
3. The flag is optionally added to a [feature group](feature-groups-to-control-multiple-features.md) to be managed alongside related flags.
4. The flag is optionally added to a [release](release-management.md) for cross-team coordination.
