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

Feature groups support cross-application feature management as long as the flags belong to the **same team** in Experience Rollouts. One team can own multiple applications, so related flags across those applications can be grouped together.

## Feature groups versus releases {#vs-releases}

| | Feature group | Release |
|---|---|---|
| Scope | Within a single team | Across multiple teams |
| Use case | Coordinating flags within your team | Large, multi-team launch coordination |
| Privileges required | Team-level | Higher (release manager) |

If the feature flags you want to group belong to applications owned by different teams, use a [release](release-management.md) instead of a feature group.
