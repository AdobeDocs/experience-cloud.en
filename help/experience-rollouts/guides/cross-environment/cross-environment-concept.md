---
title: Cross-environment concept
description: Learn how cross-environment capabilities in Adobe Experience Rollouts let you link applications across environments and manage feature flags consistently from development to production.
exl-id: a53b1c62-1d53-404b-9a94-4265cdcabac2
---
# Cross-environment concept {#cross-environment-concept}

Cross-environment capabilities let you link your application instances across different deployment environments — such as QA, Stage, and Production — and manage feature flags consistently across all of them from within Experience Rollouts.

## The problem cross-environment solves {#problem}

Without cross-environment linking, each application instance in Experience Rollouts is completely independent from its counterparts in other environments. This creates several friction points:

* An application named `my-app` in Stage has no relationship to `my-app` in Production — they are treated as separate, unrelated applications.
* You cannot view the status of a feature flag in Stage while working in Production. You have to switch environments manually to compare flag states.
* Importing a feature flag configuration from a lower environment to a higher one requires manual recreation.

## What cross-environment enables {#what-it-enables}

By linking application instances across environments, your team can:

* Define which of your application's deployment environments map to which Experience Rollouts environments
* Use custom environment labels (for example, `Dev`, `Staging`, `Prod`) that match your team's naming conventions
* View the status of a feature flag across all linked environments from a single view
* Import feature flags from a lower environment into a higher one with a few clicks — without recreating them manually

## How environments are structured {#environment-structure}

Experience Rollouts has two platform environments: **Stage** and **Production**. Your application, however, may have more environments — for example, QA, Staging, and Production. Cross-environment linking lets you decide where each of your application's environments lives:

* QA and Staging environments can be hosted in either the Experience Rollouts Stage or Production environment.
* Production environments must be hosted in the Experience Rollouts Production environment.

This flexibility means you are not forced into a one-size-fits-all mapping.

## Next steps {#next-steps}

* [Associate environments to an application](associate-environments.md) — set up the links between your application instances
* [View feature flags across environments](view-feature-flags-across-environments.md) — monitor flag status across all linked environments
* [Import feature flags](import-feature-flags.md) — promote feature flags from lower to higher environments
