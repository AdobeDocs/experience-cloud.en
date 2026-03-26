---
title: A/B testing with feature flags
description: Learn how to run A/B tests using feature groups in Adobe Experience Rollouts by configuring multiple variants for a set of feature flags.
exl-id: bb849049-229c-40ff-bbfe-7996f868bcc3
---
# A/B testing with feature flags {#a-b-testing}

A/B tests in Experience Rollouts are performed using **feature groups**. By configuring more than one variant in a feature group, you can serve different versions of a feature to different subsets of your audience and compare results.

## Prerequisites {#prerequisites}

* You have access to the console — see [Log in to the console](../console/log-in-to-the-console.md)
* You belong to a team and your application is onboarded
* You have the **Developer** or **Product Release Owner** role
* You have created the feature flags to test — see [Create your first feature flag](create-your-first-feature-flag.md)

## Step 1: Create a feature group with multiple variants {#create}

1. Navigate to **Feature Testing > Feature Groups** and select **New Feature Group**.
2. In **Basic Details**, provide a title, key, and description.
3. Set a **percentage rollout** to define how much of your audience participates in the test.
4. Set **Variants** to a value greater than one (for example, two variants for a classic A/B test).
5. See [Set a feature group to gradually roll out](set-feature-group-gradual-rollout.md) to understand how the exposure percentage is distributed across variants.

## Step 2: Set the audience {#audience}

On the **Audience** tab, add audience criteria and select the applications to include. Feature groups can span multiple applications within the same team.

>[!NOTE]
>
>To target external users in an A/B test, you must have the **Product Release Owner** role. The Developer role is sandboxed and limited to private testing.

## Step 3: Add features per variant {#features}

Under the **Features** tab, each variant has its own tab. Add the appropriate feature flags to each variant to define the different experiences you want to compare.

>[!IMPORTANT]
>
>A feature flag can only be served through one method at a time — feature flag, feature group, or release. Adding a flag to a feature group removes any audience or percentage rollout set directly on the flag.

## Step 4: Save and activate {#save}

Save the feature group settings. When you are ready to start the test, set the feature group to the active state.

## See also {#see-also}

* [Create a feature group](create-a-feature-group.md)
* [Set a feature group to gradually roll out](set-feature-group-gradual-rollout.md)
* [Analytics](analytics.md)
