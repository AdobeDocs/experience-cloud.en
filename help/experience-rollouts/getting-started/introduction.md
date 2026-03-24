---
title: Introduction to Experience Rollouts
description: Learn how Adobe Experience Rollouts provides a controlled release system for deploying features progressively to targeted audiences.
exl-id: a1b2c3d4-1111-4a5b-8c9d-0e1f2a3b4c5d
---

# Introduction to Experience Rollouts {#introduction}

Adobe Experience Rollouts is a controlled release system that lets teams deploy features all the way to production while keeping precise control over who sees them and when. A feature can be in production and invisible to end users — then switched on progressively for a targeted audience — without any redeployment.

## From development to production {#dev-to-prod}

Experience Rollouts supports the full journey of a feature from its earliest development stage through to general availability:

1. **Developer testing** — A developer creates a feature flag, deploys their code to any environment, and tests against only their own session. No other users are affected and no branching is required.

2. **Targeted preview** — A product owner links an audience to the feature flag, making the feature available to a defined subset of users (for example, beta participants or a specific region) for validation and feedback.

3. **Gradual rollout** — The feature is progressively opened to a wider audience — 1%, 10%, 50%, 100% — with the ability to pause, adjust, or turn off the feature at any step.

4. **General availability** — Once validation is complete, the feature is made available to all users.

## Core capabilities {#capabilities}

Experience Rollouts is a feature management platform that provides:

* **Feature flags** — Turn any feature on or off at runtime for a targeted audience, without redeploying code.

* **Audience targeting** — Control who sees a feature using user profile data, percentage-based rules, email address, email domain, IP address, or contextual attributes.

* **Feature groups** — Bundle multiple related feature flags across applications and manage them as a single unit, ensuring the same audience sees a consistent experience.

* **Releases** — Coordinate large, cross-team rollouts by grouping feature flags from multiple teams and applications into a single release event.

* **Gradual rollouts** — Phase feature delivery incrementally to reduce risk, gather feedback, and manage backend load.

* **Kill switch** — Turn off any feature immediately if a problem is detected, without a code change or redeployment.
