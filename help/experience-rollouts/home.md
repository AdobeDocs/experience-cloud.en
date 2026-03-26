---
title: Adobe Experience Rollouts
description: Learn how to use Adobe Experience Rollouts to deliver features safely and gradually with controlled rollouts, feature flags, and targeted audience management.
exl-id: c400d75d-d928-4cf6-a094-1a2f443389f0
---
# Adobe Experience Rollouts {#experience-rollouts-home}

Adobe Experience Rollouts lets product teams ship new features gradually and safely — without redeployments or downtime. You define who sees what, when, and at what pace. If something goes wrong, you turn the feature off instantly. If it goes well, you expand the audience on your schedule.

## What you can do

**Control who sees new features.** Target releases to specific users, organizations, regions, or custom attributes. Start with a small group, validate the experience, then expand — all from the console, with no code changes.

**Run A/B experiments.** Serve different variants to different segments of your audience and measure which performs better. Use the results to make informed product decisions before a full release.

**Reduce release risk.** Break large changes into smaller, controlled rollouts. If a bug or performance issue appears, disable only the affected feature — the rest of your application stays stable.

**Coordinate across teams.** Cross-team feature groups let multiple teams participate in a single coordinated release, each managing their own feature flags while sharing a common rollout schedule and audience.

## Onboard your first feature

Getting value from Experience Rollouts starts with three steps:

1. **Set up your team and application** — [Request access](guides/console/request-access.md) to the console, then [onboard your application](guides/applications/onboard-your-application.md) so Experience Rollouts knows which clients to serve.

2. **Create and publish a feature flag** — Follow the [Create your first feature flag](guides/feature-flags/create-your-first-feature-flag.md) guide to define a flag, set your initial audience, and publish it to your environment.

3. **Integrate with your application** — Connect your app to the Experience Rollouts API or SDK so it can retrieve and apply feature flags at runtime. Start with the [integration steps](guides/integrate/integration-steps.md) for your application type.

Once your first flag is live, you can refine its audience, configure a gradual rollout, and promote it from saved to full rollout.

## Need help?

If something does not behave as expected, the [troubleshooting guide](guides/support/troubleshooting.md) covers the most common issues. For anything else, [contact support](guides/support/contact-support.md).
