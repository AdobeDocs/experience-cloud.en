---
title: Schedule
description: Learn how to schedule a feature flag, feature group, or cross-team feature group to activate automatically at a future date and time in Adobe Experience Rollouts.
---

# Schedule {#schedule}

Scheduling is an optional feature that lets you set a future date and time for a feature flag, feature group, or cross-team feature group to activate automatically. Manual on/off toggling remains available and is not required to be replaced with a schedule.

Scheduling is supported for:

* Feature flags
* Feature groups
* Cross-team feature groups (schedules the transition to the **Publish** state)

## Step 1: Set the schedule {#set-schedule}

1. Open the feature flag, feature group, or cross-team feature group in the console.
2. Select the **Schedule** button on the right side of the screen.
3. In the pop-up, set the **start date and time** and select the **timezone**.

## Step 2: Save {#save}

Select **Set Schedule**, then save the settings. The schedule does not take effect until you save.

## After a schedule is set {#after-schedule-set}

Once saved, the scheduled date and time appear in the feature flag or feature group view.

If you attempt to toggle the on/off state manually while a schedule is active, a warning appears asking whether you want to override the schedule or cancel the action.

## On the scheduled date and time {#on-schedule}

At the scheduled time, the feature flag or feature group automatically activates (moves to the ON state). For cross-team feature groups, the state transitions to **Published**.

After the schedule fires, the **Schedule** button is disabled. Schedules can only be set when the feature flag or feature group is in the off (or Saved, for cross-team feature groups) state.

## See also {#see-also}

* [Create your first feature flag](create-your-first-feature-flag.md)
* [Create a feature group](create-a-feature-group.md)
* [Create a cross-team feature group](create-cross-team-feature-group.md)
