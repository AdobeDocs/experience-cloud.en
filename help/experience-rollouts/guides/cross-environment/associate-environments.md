---
title: Associate environments to an application
description: Learn how to link your application instances across environments in Adobe Experience Rollouts so you can manage feature flags consistently from development to production.
exl-id: 53080db1-f257-4369-82ab-57c84395a40a
---
# Associate environments to an application {#associate-environments}

Linking your application instances across environments enables cross-environment visibility and import workflows. You must have the **Admin** role to configure this. See [User roles](../teams/user-roles.md) if you need to verify your role.

For background on why this is useful, see [Cross-environment concept](cross-environment-concept.md).

## Step 1: Open the application settings {#step-1}

1. Log in to the Experience Rollouts console.
2. Navigate to **Admin > Applications**.
3. Select **New Application** to onboard a new app, or select an existing application to edit it.

## Step 2: Configure the Associated Environments section {#step-2}

In the application form, scroll to the **Associated Environments** section. Each row in this section defines one of your application's deployment environments. For each environment, configure the following fields:

| Field | Description |
|---|---|
| **Environment** | Select a standard environment identifier from the list: QA1, QA2, STG1, STG2, PROD1, or PROD2. This tells Experience Rollouts whether the environment is production or non-production, and determines the color coding used in the console. |
| **Environment label** | A custom name for this environment as your team refers to it — for example, `Dev`, `Staging`, or `Production`. This is free-form and does not need to match the standard identifier. |
| **Experience Rollouts environment** | The platform environment (Stage or Production) where this application instance is hosted. Pre-populated based on which console you are currently in. |
| **Application ID** | The client ID of the application instance in this environment. Auto-populated when you select an application from the drop-down. |

## Step 3: Link application instances across environments {#step-3}

To link instances across environments, follow these steps for each additional environment:

1. Create the application instance in its target environment (for example, create the QA app in the Stage console).
2. Return to the application you are configuring and add a new row in **Associated Environments**.
3. From the **Application ID** drop-down, select the application instance you just created. The environment tag and label populate automatically.
4. Select **Update** to save.

Repeat this process for each environment you want to link — for example, linking QA, Stage, and Production instances of the same application.

## Important notes {#important-notes}

* QA and Stage environments can be hosted in either the Experience Rollouts Stage or Production platform environment.
* Production environments (PROD1, PROD2) can only be hosted in the Experience Rollouts Production environment.
* You can only link to a lower environment from a higher one. For example, from Production you can link to a Stage or QA instance, but the reverse is read-only.

## See also {#see-also}

* [Cross-environment concept](cross-environment-concept.md)
* [View feature flags across environments](view-feature-flags-across-environments.md)
* [Import feature flags](import-feature-flags.md)
