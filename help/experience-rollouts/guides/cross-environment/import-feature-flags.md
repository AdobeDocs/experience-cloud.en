---
title: Import feature flags
description: Learn how to import feature flags from a lower environment into a higher environment in Adobe Experience Rollouts to avoid recreating flag configurations manually.
exl-id: 37c84d75-a565-4202-8c99-f630e05b6bb6
---
# Import feature flags {#import-feature-flags}

Experience Rollouts lets you import feature flags from a lower environment (for example, Stage) into a higher environment (for example, Production). This avoids having to recreate flag configurations manually and reduces the risk of configuration drift between environments.

## Prerequisites {#prerequisites}

To use the import workflow, your application instances must be linked across environments. See [Associate environments to an application](associate-environments.md).

## Step 1: Go to the destination environment and application {#step-1}

Log in to the console for the **destination** environment — the environment you want to import flags *into*. Select the application you want to import flags into from the application drop-down on the Feature Flags page.

>[!IMPORTANT]
>
>Your current environment and selected application must be the **destination** — not the source. For example, to import a flag from Stage into Production, log in to the Production console and select your Production application.

## Step 2: Open the import dialog {#step-2}

Select **Import Feature Flags**. A dialog opens showing the source environment and application, pre-populated based on the linked environments configured for your application. If needed, you can change the source environment and application from the drop-downs in the dialog.

## Step 3: Select the feature flags to import {#step-3}

From the list of feature flags in the source environment, select the flags you want to import. You can select one, multiple, or all flags at once.

## Step 4: Handle existing flags (if required) {#step-4}

If a feature flag with the same key already exists in the destination environment, Experience Rollouts will ask you to confirm whether to overwrite it. Review the existing flag configuration before confirming, as overwriting will replace the destination flag's settings with those from the source.

## Important notes {#important-notes}

Keep the following in mind when importing feature flags:

* Imported flags are always set to the **OFF** state in the destination environment, regardless of their state in the source environment. You must manually enable them after import.
* If a flag was scheduled to activate at a future date and time in the source environment, that schedule is **not** carried over. You must set a new schedule in the destination environment if needed.

## See also {#see-also}

* [Associate environments to an application](associate-environments.md)
* [View feature flags across environments](view-feature-flags-across-environments.md)
* [Cross-environment concept](cross-environment-concept.md)
