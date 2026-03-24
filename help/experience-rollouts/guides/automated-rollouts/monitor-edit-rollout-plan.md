---
title: Monitor and edit a rollout plan
description: Learn how to track the progress of an automated rollout plan in Adobe Experience Rollouts and how to pause, resume, or abort a plan that is in progress.
---

# Monitor and edit a rollout plan {#monitor-edit-rollout-plan}

Once an automated rollout is live, you can track its progress and intervene if needed. This page describes how to read the progress indicator, pause and resume a plan, and abort it if necessary.

This page assumes you have already created and published a rollout plan. See [Create an automated rollout](create-automated-rollout.md) if you have not yet set one up.

## View rollout progress {#view-progress}

After the rollout plan starts executing, open the **Audience** tab of the feature to see the current state of the plan. The plan displays a progress indicator that marks which phase block is currently active.

Use the progress indicator to understand the following:

* **Completed blocks** — All phase and wait blocks above the indicator have been executed. These blocks are locked and cannot be edited.
* **Current block** — The block currently highlighted is the active phase or wait period.
* **Upcoming blocks** — All phase and wait blocks below the indicator have not yet executed. These can still be edited.

## Pause a rollout plan {#pause}

To pause the rollout at any point while it is in progress, select **Pause Rollout** in the console.

When the plan is paused:

* The audience from the last completed phase block remains active. Users in that audience continue to receive the feature.
* The feature flag, feature group, or cross-team feature group stays in its current on or published state. It continues serving the feature to the current active audience.
* Upcoming phase and wait blocks remain editable.

To resume a paused plan, select **Resume Rollout**. The plan continues from where it left off.

## Abort a rollout plan {#abort}

To permanently stop the rollout plan, select **Abort Rollout** in the console.

When the plan is aborted:

* The audience from the last completed phase block remains active, and the feature continues to be served to that audience.
* The feature itself is not turned off — if you want to stop serving the feature entirely, you must separately abort the release or turn off the feature flag or group.
* Upcoming phase and wait blocks can no longer be edited.
* An aborted plan cannot be resumed.

>[!IMPORTANT]
>
>Aborting a rollout plan does not automatically turn off the feature. Take a separate action on the feature state if you want to stop serving it to users.

## Edit upcoming phase blocks {#edit-upcoming}

While the plan is in progress (or paused), you can still edit any phase or wait block that has not yet been executed:

* Adjust the audience rules or percentage for an upcoming phase block.
* Change the duration or fixed date of an upcoming wait block.

Completed blocks are locked and cannot be changed.

## See also {#see-also}

* [Create an automated rollout](create-automated-rollout.md)
* [Automated rollout concept](automated-rollout-concept.md)
* [Release states](../feature-flags/release-states.md)
