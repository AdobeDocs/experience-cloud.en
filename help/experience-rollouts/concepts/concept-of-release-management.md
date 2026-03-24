---
title: Concept of release management
description: Learn how release management in Experience Rollouts helps coordinate large, cross-team feature rollouts through feature flagging.
exl-id: f304fc12-e49c-40be-805b-5587fb87478a
---
# Concept of release management {#concept-of-release-management}

Large releases share a few common challenges: multiple teams are involved, schedules conflict, and dependencies are difficult to coordinate. Release management addresses these challenges by providing a structured way to roll out changes smoothly.

## What release management means {#what-it-means}

Release management covers the coordination of a release end to end — from the moment teams begin developing behind feature flags to the moment the feature is fully available to all users.

It allows teams to:

* Deploy independently to production, at their own pace, without revealing features to end users
* Go live only when all participating teams are ready
* Roll out the release gradually to a subset of users before full availability

## How it works in Experience Rollouts {#how-it-works}

Release management in Experience Rollouts builds on the concept of [feature flagging](what-is-a-feature-flag.md). Each team deploys their code to production behind a feature flag. A release is then a **collection of feature flags defined across multiple applications and teams**.

When all teams are ready, the release can be activated in a single operation — or gradually rolled out — without any individual team needing to redeploy or coordinate deployment timing.

This approach provides:

* **Independent deployment** — Teams deploy on their own schedule without affecting other teams or end users.
* **Coordinated activation** — All flags in a release are activated together when the release goes live.
* **Gradual rollout** — The release can be opened progressively to increasing percentages of users.

For details on configuring releases in Experience Rollouts, see [Release management](release-management.md).
