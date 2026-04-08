---
title: Feature groups to control multiple features
description: Learn how feature groups in Experience Rollouts let you bundle and manage related feature flags across applications as a single unit.
exl-id: dfeb7eff-34f1-4cb5-9c3e-a40d1eda3016
---
# Feature groups to control multiple features {#feature-groups}

A [feature flag](what-is-a-feature-flag.md) controls a single feature. When you need to manage multiple related feature flags together — and ensure they reach the same audience — you use a **feature group**.

## What a feature group does {#what-it-does}

A feature group bundles multiple feature flags and lets you apply a single audience rule to all of them at once. This is useful when a single user-facing capability spans multiple applications or services.

For example, consider a collaboration feature that involves changes across a desktop application, a mobile app, and a backend service. By creating a feature group with flags from all three applications, you can open the feature to 1% of users — and ensure those users see a consistent experience across all three surfaces simultaneously.

## Cross-application grouping {#cross-application}

Feature groups support cross-application feature management. Related flags across multiple applications can be grouped together.

