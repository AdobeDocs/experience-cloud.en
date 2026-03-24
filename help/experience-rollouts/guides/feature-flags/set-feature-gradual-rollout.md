---
title: Set a feature to gradually roll out
description: Learn how to configure a percentage-based gradual rollout for a feature flag in Adobe Experience Rollouts.
---

# Set a feature to gradually roll out {#gradual-rollout-feature}

The percentage rollout for a feature flag is configured in the **Basic Details** tab. You can adjust this value up or down at any time as the rollout progresses.

## How it works {#how-it-works}

When you set a percentage rollout — for example, 25% — that percentage of your defined audience is exposed to the feature. The remaining percentage is placed in the **control group**, which receives the default experience.

You can increase or decrease the percentage over time to expand or contract the rollout. Reducing the percentage to 0% effectively turns off the feature for everyone in the audience without deleting the flag.

## See also {#see-also}

* [Gradual rollout](../../../concepts/gradual-rollout.md)
* [Set a feature group to gradually roll out](set-feature-group-gradual-rollout.md)
* [Create your first feature flag](create-your-first-feature-flag.md)
