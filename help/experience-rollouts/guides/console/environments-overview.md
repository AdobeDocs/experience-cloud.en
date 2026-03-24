---
title: Environments overview
description: Learn about the Stage and Production environments in Adobe Experience Rollouts and when to use each.
---

# Environments overview {#environments}

Experience Rollouts provides separate environments so you can validate your feature flags before promoting changes to your live users.

## Available environments {#available-environments}

| Environment | Purpose |
|---|---|
| **Stage** | Testing and validation. Use this environment to configure and test feature flags before enabling them in Production. |
| **Production** | Live rollouts. Feature flags configured here are evaluated against your real user base. |

>[!IMPORTANT]
>
>Changes made in Stage do not automatically carry over to Production. Feature flags and audience rules must be configured separately in each environment.

## Selecting an environment {#selecting}

After logging in to the Experience Rollouts console, select the environment from the environment switcher at the top of the interface. Make sure you are working in the correct environment before creating or modifying feature flags.

## Best practices {#best-practices}

Follow these recommendations to avoid configuration errors and protect your production audience:

* Always create and test feature flags in **Stage** first.
* Validate audience rules, percentage rollouts, and targeting logic in Stage before replicating in Production.
* Use the [cross-environment workflow](../cross-environment/cross-environment-concept.md) to view and manage flag status across environments.

## See also {#see-also}

* [Log in to the console](log-in-to-the-console.md)
* [Associate environments to an application](../cross-environment/associate-environments.md)
* [View feature flags across environments](../cross-environment/view-feature-flags-across-environments.md)
