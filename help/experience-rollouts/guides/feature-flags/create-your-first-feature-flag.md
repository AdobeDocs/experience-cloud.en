---
title: Create your first feature flag
description: Learn how to create a feature flag in Adobe Experience Rollouts, set an audience, and test it before rolling out to users.
exl-id: ae115120-8da9-465e-a556-c17591ea7054
---
# Create your first feature flag {#create-feature-flag}

## Prerequisites {#prerequisites}

Before creating a feature flag, complete the following:

* You have access to the Experience Rollouts console — see [Log in to the console](../console/log-in-to-the-console.md)
* Your application is onboarded — see [Onboard your application](../applications/onboard-your-application.md)
* You have the **Developer** or **Product Release Owner** role

## Step 1: Create the feature flag {#create}

To create a new feature flag, follow these steps in the console:

1. Log in to the Experience Rollouts console and navigate to **Features & Releases > Feature Flags**.
2. Select your application from the **Application** drop-down.
3. Select **New Feature**.
4. Provide a title, key, description, and optionally a tag.
5. Optionally add an audience criteria (see Step 2).
6. Save your feature flag settings.

## Step 2: Add an audience criteria {#audience}

Audience criteria control which users see the feature. You can add criteria based on:

* Profile attributes (such as country, email domain, user ID)
* Context variables
* Predefined audience segments

To add audience criteria, go to the **Audience** tab when creating or editing a feature flag.

>[!NOTE]
>
>The **Developer** role is sandboxed. Developers can only expose a feature to themselves by adding their own User ID under **Audience > Profile > User ID**. To expose a feature to external users, you need the **Product Release Owner** role.

## Step 3: Calculate audience size {#audience-size}

After adding audience criteria, select **Calculate** in the bottom bar to get an estimated count of users who qualify for the feature. This helps validate your targeting before going live.

## Step 4: Schedule (optional) {#schedule}

You can schedule a feature flag to activate at a future date and time. See [Schedule](schedule.md) for details.

## FAQ: I cannot add a feature flag as a Developer {#faq}

The **Developer** role is sandboxed. Developers can test features privately by adding their User ID to the audience. They cannot expose features to external users. Use the **Product Release Owner** role to release features to external users. Contact your team admin to update your role.

## See also {#see-also}

* [Set a feature to gradually roll out](set-feature-gradual-rollout.md)
* [Create a feature group](create-a-feature-group.md)
