---
title: Create a feature group
description: Learn how to create a feature group in Adobe Experience Rollouts to manage multiple feature flags across applications in your team as a single unit.
exl-id: 58148df1-84ee-4a78-a4b4-71f74cd8ce0a
---
# Create a feature group {#create-feature-group}

## Prerequisites {#prerequisites}

Before creating a feature group, complete the following:

* You have access to the Experience Rollouts console — see [Log in to the console](../console/log-in-to-the-console.md)
* You belong to a team — see [Manage teams](../teams/manage-teams.md)
* Your application is onboarded — see [Onboard your application](../applications/onboard-your-application.md)
* You have the **Developer** or **Product Release Owner** role — see [User roles](../teams/user-roles.md)
* You have created the feature flags you want to add to the group — see [Create your first feature flag](create-your-first-feature-flag.md)

For an introduction to feature groups, see [Feature groups to control multiple features](../../concepts/feature-groups-to-control-multiple-features.md).

## Step 1: Create the feature group {#create}

Open the console and start a new feature group:

1. Log in to the Experience Rollouts console and navigate to **Feature Testing > Feature Groups**.
2. Select **New Feature Group**.

## Step 2: Basic details {#basic-details}

Configure the general settings for the feature group:

1. Provide a title, key, description, and optionally a tag.
2. Set a **percentage rollout** for the feature group.
3. If you want to run an A/B test, select more than one variant. Otherwise, leave it at one variant. See [A/B testing with feature flags](a-b-testing.md) for details.

## Step 3: Audience {#audience}

Define who will receive the features in this group:

1. On the **Audience** tab, add audience criteria to define which users receive the feature.
2. Under **Applications**, add one or more applications from your team. Feature groups can span multiple applications as long as they all belong to the same team.

>[!NOTE]
>
>The **Developer** role is sandboxed. Add your own User ID under **Audience > Profile > User ID** to test privately. To target external users, you need the **Product Release Owner** role.

## Step 4: Features {#features}

Assign the feature flags that will be controlled by this group:

1. Under the **Features** tab, you see a box for each application you selected.
2. Add feature flags for each application.
3. If you selected multiple variants (for A/B testing), you see tabs for each variant. Add the appropriate feature flags to each.

>[!IMPORTANT]
>
>A feature flag can only be served through one method — either directly as a feature flag, through a feature group, or through a release. When you add a feature flag to a feature group, any audience or percentage rollout set on the flag is removed. Feature flags already assigned to another release or feature group will not appear in the list.

## Step 5: Schedule (optional) {#schedule}

You can schedule the feature group to activate at a future date and time. See [Schedule](schedule.md) for details.

## See also {#see-also}

* [Set a feature group to gradually roll out](set-feature-group-gradual-rollout.md)
* [A/B testing with feature flags](a-b-testing.md)
* [Feature groups to control multiple features](../../concepts/feature-groups-to-control-multiple-features.md)
