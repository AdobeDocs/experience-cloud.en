---
title: Import feature flags
description: Learn how to import feature flags from one sandbox into another in Adobe Experience Rollouts to avoid recreating flag configurations manually.
exl-id: 37c84d75-a565-4202-8c99-f630e05b6bb6
---
# Import feature flags {#import-feature-flags}

Experience Rollouts lets you import feature flags from one sandbox (for example, sandbox 1) into another sandbox (for example, sandbox 2). This avoids having to recreate flag configurations manually and reduces the risk of configuration drift between sandboxes.

## Step 1: Go to the destination sandbox and application {#step-1}

Log in to the console for the **destination** sandbox — the sandbox you want to import flags *into*. Select the application you want to import flags into from the application drop-down on the Feature Flags page.

>[!IMPORTANT]
>
>Your current sandbox and selected application must be the **destination** — not the source. For example, to import a flag from sandbox 1 into sandbox 2, log in to the sandbox 2 console and select your sandbox 2 application.

## Step 2: Open the import dialog {#step-2}

Select **Import Feature Flags**. A dialog opens showing the source sandbox and application, pre-populated based on the available applications. If needed, you can change the source sandbox and application from the drop-downs in the dialog.

## Step 3: Select the feature flags to import {#step-3}

From the list of feature flags in the source sandbox, select the flags you want to import. You can select one, multiple, or all flags at once.

## Step 4: Select the state of feature flags to import {#step-4}

Use the dropdown to choose how the feature flags should be imported — either **Enabled**, **Disabled**, or in their **Current state**. By default, feature flags are imported in the **Disabled** state.

## Important notes {#important-notes}

Keep the following in mind when importing feature flags:

* If a feature flag with the same key already exists in the destination sandbox, it will not be imported.

## See also {#see-also}

* [Features and feature groups](../feature-flags/features-feature-groups-releases.md)
* [Create your first feature flag](../feature-flags/create-your-first-feature-flag.md)
