---
title: Create a cross-team feature group
description: Learn how to create a cross-team feature group in Adobe Experience Rollouts to coordinate feature flags across applications owned by different teams.
exl-id: 9627d511-fa60-4650-9d06-1a1eca6b2a36
---
# Create a cross-team feature group {#create-cross-team-feature-group}

## Prerequisites {#prerequisites}

Before creating a cross-team feature group, confirm the following:

* You have access to the console — see [Log in to the console](../console/log-in-to-the-console.md)
* You belong to a team and your application is onboarded
* You have the **Feature Admin** role — see [User roles](../teams/user-roles.md)
* You have created the feature flags to include — see [Create your first feature flag](create-your-first-feature-flag.md)

A cross-team feature group allows bundling feature flags from applications across multiple teams with rich audience targeting. Unlike releases, it is fully self-serve and has no limit on the number you can create. See [Releases and cross-team feature groups](releases-and-cross-team-feature-groups.md) for a comparison.

## Step 1: Create the cross-team feature group {#create}

Start the creation process from the Releases section of the console:

1. Navigate to **Features & Releases > Releases** in the console.
2. Select **New Feature Group (Cross-Team)**.

## Step 2: Basic details {#basic-details}

Provide a title, key, description, and optionally a tag. Configure the following options:

* **Percentage rollout** — Set how much of the audience receives the feature.
* **Rollout type** — Set to Manual. The percentage is managed step-by-step as your rollout progresses.

>[!NOTE]
>
>A/B testing is not supported for cross-team feature groups. To run A/B tests, use a standard [feature group](create-a-feature-group.md) (applications must be in the same team).

## Step 3: Audience {#audience}

On the **Audience** tab, enable **Audience Rules** and configure:

* **Segments** — Select a predefined audience segment.
* **Additional filters** — Add profile-based or context-based criteria directly.
* **Applications** — Select one or more applications from your team or other teams.

>[!IMPORTANT]
>
>Adding an application from another team grants the Feature Admins of that team the right to add feature flags for their application to this cross-team feature group. You cannot add their feature flags yourself.

## Step 4: Features {#features}

Under the **Features** tab, you see a box for each application included:

* For applications in your own team, you can add feature flags directly.
* For applications from other teams, those boxes are grayed out — the respective team's Feature Admins must add their flags.

>[!IMPORTANT]
>
>A feature flag can only be served through one method at a time. Adding a flag to a cross-team feature group removes any audience or percentage rollout set on the flag directly. Flags already in another release or feature group will not appear.

## Step 5: Schedule (optional) {#schedule}

You can schedule the cross-team feature group to activate at a future date and time. See [Schedule](schedule.md) for details.

## Managing states {#states}

The team that creates the cross-team feature group owns it and can manage its state. Feature Admin members of the owning team can transition between states using the state dropdown:

| State | Description |
|---|---|
| **Save** | Saved and not live. All changes are allowed. |
| **Publish** | Live for the configured audience. Feature admins can continue updating audience criteria and percentage rollout. |
| **Full rollout** | Available to all users. Cannot restrict the audience further after this point. |
| **Baseline** | Features are now the default. The cross-team feature group is closed. |
| **Abort** | The rollout is stopped. No users receive features from this group. |

## FAQs {#faqs}

**Is there a limit on the number of cross-team feature groups?**
No. Unlike releases, there is no limit. However, archive or disable groups when no longer needed.

**What is the difference between a release and a cross-team feature group?**
See [Releases and cross-team feature groups](releases-and-cross-team-feature-groups.md) for a detailed comparison.

## See also {#see-also}

* [Releases and cross-team feature groups](releases-and-cross-team-feature-groups.md)
* [Create a feature group](create-a-feature-group.md)
