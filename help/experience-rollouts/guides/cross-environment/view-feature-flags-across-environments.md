---
title: View feature flags across environments
description: Learn how to view the status of feature flags across all linked environments for an application in Adobe Experience Rollouts.
---

# View feature flags across environments {#view-flags-across-environments}

Once you have linked your application instances across environments, Experience Rollouts displays the status of each feature flag across all linked environments directly in the feature flags listing page. This gives you a single view to compare flag states — for example, whether a flag is ON in Stage and OFF in Production — without switching environments.

## Prerequisites {#prerequisites}

Your application instances must be linked across environments before cross-environment status is visible. See [Associate environments to an application](associate-environments.md) for setup instructions.

## How it works {#how-it-works}

When you navigate to **Features & Releases > Feature Flags** and select an application that has linked instances, the listing page shows additional columns for each linked environment. Each column displays the current state of the feature flag in that environment.

Feature flags are matched across environments by their **key** — not by their name. This means:

* A flag can have a different display name in each environment, as long as the key is the same.
* The name shown in each environment column is the name used in that environment.

## Use case {#use-case}

A typical workflow is to develop and test a feature flag in a lower environment (for example, Stage), then verify its status before promoting the configuration to Production. Cross-environment visibility lets you confirm the flag is correctly configured in Stage before importing it to Production — all from within the Production console.

## See also {#see-also}

* [Associate environments to an application](associate-environments.md)
* [Import feature flags](import-feature-flags.md)
* [Cross-environment concept](cross-environment-concept.md)
