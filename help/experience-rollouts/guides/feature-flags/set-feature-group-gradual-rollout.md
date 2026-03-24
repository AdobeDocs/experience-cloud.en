---
title: Set a feature group to gradually roll out
description: Learn how to configure a percentage-based gradual rollout for a feature group in Adobe Experience Rollouts.
---

# Set a feature group to gradually roll out {#gradual-rollout-feature-group}

The percentage rollout for a feature group is configured in the **Basic Details** tab. You can adjust this value up or down at any time as the rollout progresses.

## How it works {#how-it-works}

When you set a percentage rollout — for example, 60% — that percentage of your defined audience is exposed to the feature group. The remaining 40% is placed in the **control group**, which receives default behavior.

If you have configured multiple variants (for A/B testing), the exposure percentage is distributed equally across variants. For example, 60% exposure with three variants results in 20% per variant, with 40% in the control group.

You can increase or decrease the percentage at any time to expand, reduce, or pause the rollout.

## See also {#see-also}

* [Create a feature group](create-a-feature-group.md)
* [A/B testing with feature flags](a-b-testing.md)
* [Gradual rollout](../../../concepts/gradual-rollout.md)
