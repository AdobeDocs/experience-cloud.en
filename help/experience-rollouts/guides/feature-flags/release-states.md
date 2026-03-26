---
title: Release states
description: Learn about the lifecycle states of a release in Adobe Experience Rollouts, including what each state means and which transitions are allowed.
exl-id: c1311353-9c36-43c5-8e75-3b3ee225da41
---
# Release states {#release-states}

A Release Manager can update a release's state directly from the console navigation bar. The state controls whether the release is live, limited to testing, fully rolled out, or closed.

## Available states {#states}

| # | State | Description | Changes allowed |
|---|---|---|---|
| 1 | **Draft** | The release is saved in the system but not yet active. No audience rules are applied. | All changes allowed (release, features, audience). |
| 2 | **Saved** | The release is registered and a slot is allocated to it. The release is not yet visible to users. | All changes allowed. |
| 3 | **Published** | The release is live for the specified audience. Users who meet the audience criteria receive the features. | All changes allowed. |
| 4 | **Full rollout** | The release is available to all users regardless of audience rules. All audience rules are removed. | Feature changes allowed. Audience cannot be changed. |
| 5 | **Baselined** | All users now have the features from this release as default behavior. The conditional code can be removed. The release slot is freed up. | No changes allowed. |
| 6 | **Aborted** | The release has been stopped. No users receive features from this release. The release slot is freed up. | No changes allowed. |

## Allowed transitions {#transitions}

Not all state transitions are permitted. Understanding the allowed paths helps you plan your rollout and avoid errors when managing state changes:

* A release can move forward through the states: Draft → Saved → Published → Full rollout → Baselined
* A release can be Aborted from Draft, Saved, Published, or Full rollout
* Once Baselined or Aborted, no further changes are allowed

## Release capacity {#capacity}

The number of active (Saved or Published) releases at any time is limited. To free up capacity:

* Move completed releases to **Baselined** once all participating applications have removed their conditional code.
* **Abort** releases that were unsuccessful and will not be continued.

Plan to baseline or abort your releases within three months.

## See also {#see-also}

* [Request a release](request-a-release.md)
* [Release workflow end-to-end](release-workflow-end-to-end.md)
* [Update release audience rules](update-release-audience-rules.md)
