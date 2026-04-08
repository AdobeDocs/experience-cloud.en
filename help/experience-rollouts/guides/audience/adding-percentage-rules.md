---
title: Add percentage rules in audience criteria
description: Learn how to add percentage-based rules within audience criteria in Adobe Experience Rollouts to target different rollout percentages for different audience segments.
exl-id: 15a3c26f-31fc-4e73-aa0e-035dcbe7d770
---
# Add percentage rules in audience criteria {#adding-percentage-rules}

## When to use percentage rules in the audience tab {#when-to-use}

The **percentage rollout** field on the Basic Details tab applies a single percentage to your entire audience. For example, 50% rollout means 50% of all users who match your audience criteria receive the feature.

However, some rollout scenarios require different percentages for different groups — for example:

* 100% of UK users and 50% of US users
* All users from an imported email list, plus 50% of users from a specific country

In these cases, use the **Percentage** rule in the **Audience** tab's context section, combined with nested logic.

>[!TIP]
>
>If you want to apply a single percentage across your entire audience — for example, 10% of users in (US and UK) — use the **percentage rollout** on the Basic Details tab instead.

## How to add a percentage rule {#how-to-add}

The **Percentage** option is available as a rule in the context section of the Audience tab.

1. Go to the **Audience** tab of your feature flag or feature group.
2. Under **Audience**, add a **Context Percentage** rule and set the desired value.
3. Add any other audience conditions you need (for example, a Country rule).

## Combining percentage rules with nested logic {#nested-logic}

To apply different percentages to different segments, use **nested logic** to combine the conditions:

1. Enable **Nested Logic** in the audience rules section.
2. Each condition is assigned a number automatically.
3. Enter a logical expression referencing those numbers.

Use one of the following expressions to describe the relationship between your conditions:

* `1 and (2 or 3)` — condition 1 AND (condition 2 OR condition 3)
* `(1 and 2) or 3` — (condition 1 AND condition 2) OR condition 3
* `(1 and 2) or (3 and 4)` — two independent groups

## Examples {#examples}

**Example 1: All users from an imported list and 10% of users from a specific country**

Add two rules: one for the imported user list and one Percentage rule (10%) combined with a Country rule. Use nested logic: `1 or (2 and 3)`.

**Example 2: 10% of US users and 20% of UK users**

Add four rules: Country = US, Percentage = 10%, Country = UK, Percentage = 20%. Use nested logic: `(1 and 2) or (3 and 4)`.

## See also {#see-also}

* [Audience in feature flags and feature groups](audience-in-feature-flags-and-feature-groups.md)
* [Complex audience rules](complex-rules.md)
* [Set a feature to gradually roll out](../feature-flags/set-feature-gradual-rollout.md)
