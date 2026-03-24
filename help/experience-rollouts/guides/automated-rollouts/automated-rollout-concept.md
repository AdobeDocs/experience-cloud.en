---
title: Automated rollout concept
description: Understand how automated rollouts work in Adobe Experience Rollouts, including phase blocks, wait blocks, and how the rollout plan progresses automatically.
---

# Automated rollout concept {#automated-rollout-concept}

An automated rollout lets you define your entire phased rollout plan in one go. Instead of manually returning to the console to expand your audience for each phase, you configure all phases and their schedules upfront and Experience Rollouts advances through them automatically.

Automated rollouts are supported for feature flags, feature groups, and cross-team feature groups.

## How it works {#how-it-works}

A rollout plan is made up of **phase blocks** and **wait blocks** that are executed in sequence:

* **Phase block** — Defines the audience criteria for one phase of the rollout. When the plan reaches a phase block, that audience becomes the active audience for the feature.
* **Wait block** — Defines the pause between two phase blocks. A wait block can be either a relative duration (for example, "wait 3 days") or a fixed date and time.

The plan starts when you publish the feature or schedule it for a future date. Experience Rollouts moves from one block to the next automatically according to the schedule you configured.

## Phase block behavior {#phase-block-behavior}

Each subsequent phase block is pre-populated with the audience from the previous phase. This makes it easier to build incrementally expanding rollouts where each new phase includes all prior audience groups in addition to new ones.

>[!IMPORTANT]
>
>Audience rules in each phase block are editable, so you must make sure not to delete audience criteria from previous phases when you add new ones. Reducing audience scope mid-rollout can result in users unexpectedly losing access to a feature.

## Rollout plan states {#rollout-plan-states}

Once a rollout plan is live, it can be in one of three states:

| State | Description |
|---|---|
| **In progress** | The plan is executing. A progress indicator in the console shows which phase block is currently active. All completed blocks are locked and cannot be edited. |
| **Paused** | The plan is on hold. The audience from the last completed phase block remains active. Future phase and wait blocks can still be edited while paused. |
| **Aborted** | The plan has been stopped permanently. The audience from the last completed phase block remains active. No further edits to the plan are allowed. Aborting the plan does not turn off the feature — you must separately change the feature state if you want to stop serving it. |

## See also {#see-also}

* [Create an automated rollout](create-automated-rollout.md)
* [Monitor and edit a rollout plan](monitor-edit-rollout-plan.md)
* [Set a feature to gradually roll out](../feature-flags/set-feature-gradual-rollout.md)
