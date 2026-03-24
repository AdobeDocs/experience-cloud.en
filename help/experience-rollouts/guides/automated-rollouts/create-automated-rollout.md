---
title: Create an automated rollout
description: Learn how to configure an automated rollout plan in Adobe Experience Rollouts with phase blocks and wait blocks so your audience expands automatically over time.
---

# Create an automated rollout {#create-automated-rollout}

An automated rollout lets you define all rollout phases and their schedules in one session. Experience Rollouts advances from one phase to the next automatically, without requiring you to return to the console for each step. See [Automated rollout concept](automated-rollout-concept.md) for an overview.

Automated rollouts are supported for feature flags, feature groups, and cross-team feature groups.

## Step 1: Enable automated rollout {#enable-automated-rollout}

When creating a new feature flag, feature group, or cross-team feature group, open the **Basic Details** tab and locate the **Select type of rollout** option. It defaults to **Manual**. To enable an automated rollout plan, select **Automated Rollout**.

>[!NOTE]
>
>When you select Automated Rollout, the percentage rollout field in Basic Details is automatically set to 100% and becomes non-editable. You will control the percentage for each phase individually in the Audience tab.

## Step 2: Build the rollout plan {#build-rollout-plan}

Open the **Audience** tab and enable the **Phases** toggle. This activates the **Add Phase Block** and **Add Wait Block** controls.

To build your rollout plan, add phase and wait blocks in the order you want them to execute:

### Add a phase block {#add-phase-block}

A phase block defines the audience criteria for one phase of the rollout. The first phase block is configured using the audience criteria already on the page. For each subsequent phase block, the previous phase's audience is pre-populated as a starting point.

Configure the audience for each phase block:

* **Percentage** — Set what percentage of the defined audience receives the feature in this phase.
* **Audience rules** — Add profile, context, or segment-based rules to target specific users.

>[!IMPORTANT]
>
>Each subsequent phase should expand on, not replace, the previous phase's audience. Do not remove audience rules from earlier phases when you configure later ones, as this can inadvertently exclude users who were already receiving the feature.

### Add a wait block {#add-wait-block}

A wait block defines the pause between two phase blocks. After adding a wait block, select one of the following options:

| Option | Description |
|---|---|
| **Wait** | A relative duration — for example, wait 2 days, wait 4 hours. Experience Rollouts advances to the next phase block after this duration elapses. |
| **Wait for** | A fixed date and time. Experience Rollouts advances to the next phase block at the specified moment. |

### Add subsequent phase blocks {#add-subsequent-phases}

Repeat the process to add additional phase blocks and wait blocks until your full rollout plan is configured.

## Step 3: Schedule or publish the rollout {#schedule-or-publish}

Once the rollout plan is complete, choose how to activate it:

* **Schedule** — Set a future date and time for the rollout to start automatically. See [Schedule](../feature-flags/schedule.md) for details.
* **Publish manually** — Turn the feature flag on or move the feature group to **Publish** state to start immediately.

The plan begins executing from the first phase block. You can monitor and edit the active plan at any time. See [Monitor and edit a rollout plan](monitor-edit-rollout-plan.md).

## See also {#see-also}

* [Automated rollout concept](automated-rollout-concept.md)
* [Monitor and edit a rollout plan](monitor-edit-rollout-plan.md)
* [Set a feature to gradually roll out](../feature-flags/set-feature-gradual-rollout.md)
* [Audience criteria](../audience/audience-in-feature-flags-and-feature-groups.md)
