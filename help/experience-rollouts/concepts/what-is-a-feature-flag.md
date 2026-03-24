---
title: What is a feature flag
description: Learn what feature flags are and how they let you turn application features on or off at runtime without redeployment.
exl-id: d4e5f6a7-4444-4d8e-1f2a-3b4c5d6e7f8a
---

# What is a feature flag {#what-is-a-feature-flag}

A feature flag is a mechanism that lets you turn features of your application on or off at runtime — without redeploying code.

Feature flags decouple **code deployment** from **feature availability**. You can ship new code to production with the feature hidden behind a flag, then switch it on whenever you are ready — for all users, or for a targeted subset.

This separation significantly reduces risk. Developers can build and ship continuously with minimal disruption, while product teams retain full control over when and to whom a feature becomes visible.

>[!NOTE]
>
>In Experience Rollouts, a feature flag is the most atomic unit of feature control. It can be used on its own to target a single feature, or combined with other flags in a [feature group](feature-groups-to-control-multiple-features.md) or [release](release-management.md).
