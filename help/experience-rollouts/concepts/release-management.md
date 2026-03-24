---
title: Release management in Experience Rollouts
description: Learn how release management in Experience Rollouts coordinates multi-team feature delivery through dark deployments, production testing, and gradual rollouts.
exl-id: b8c9d0e1-8888-4b2c-5d6e-7f8a9b0c1d2e
---

# Release management in Experience Rollouts {#release-management}

A typical major release involves multiple teams and multiple applications, each with their own deployment timelines and dependencies. Experience Rollouts provides a release management model that lets teams work independently while still delivering a coordinated, controlled release to end users.

## Key capabilities {#capabilities}

### Dark deployments {#dark-deployments}

Teams no longer need to time their code deployment with a specific go-live date. Code can be deployed to production behind feature flags at any time. End users do not see any change until the release is activated. Teams can deploy at their own pace, confident that nothing is exposed prematurely.

### Testing in production {#testing-in-production}

Once code is deployed to production — dark deployed — Experience Rollouts can open the features to internal testers and QA teams. This allows full testing against the production environment and real production data, without any risk of exposing changes to end users.

### Gradual rollout {#gradual-rollout}

When a release is ready to go live, it does not have to be all-or-nothing. Experience Rollouts allows controlling the rollout progressively — starting with a small percentage of users, monitoring feedback and performance, and expanding the audience over time. This reduces strain on backend systems and gives teams time to respond to any issues before full exposure.

### Coordinated activation {#coordinated-activation}

Multiple teams develop features independently, each behind their own feature flags. Once all teams are ready, Experience Rollouts provides a single control point to activate all flags across teams and applications simultaneously — or gradually — so the release goes live as one cohesive experience.

## See also {#see-also}

* [Concept of release management](concept-of-release-management.md)
* [Feature groups to control multiple features](feature-groups-to-control-multiple-features.md)
* [Gradual rollout](gradual-rollout.md)
