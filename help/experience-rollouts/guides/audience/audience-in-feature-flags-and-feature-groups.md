---
title: Audience in feature flags and feature groups
description: Learn how to define audience criteria for feature flags and feature groups in Adobe Experience Rollouts using profile attributes, segments, and the audience calculator.
exl-id: 4a8f7c3f-1ae5-4e65-a070-9fc33133eec0
---
# Audience in feature flags and feature groups {#audience-overview}

Experience Rollouts provides rich audience targeting for feature flags and feature groups. You can combine profile attributes, context variables, and audience segments to precisely control which users receive a feature.

## Profile rules {#profile-rules}

Profile rules let you target users based on attributes such as country, email domain, account type, user ID, and more. You can combine multiple attributes using AND/OR operators and build nested logic for complex targeting scenarios.

To add profile rules, go to the **Audience** tab of a feature flag or feature group and add conditions under **Profile**.

You can save a set of audience rules as a reusable **Audience** for use across multiple flags and groups.

For context-based targeting (for example, targeting by the user's active language or client type), see [Use context in audience rules](using-context-in-audience-rules.md).

## Segments {#segments}

Feature flags and feature groups support audience segments. Segments allow you to:

* Use a single pre-defined audience definition across multiple feature flags and groups
* Include **event-based criteria** in your audience targeting — something not possible with profile rules alone

To use a segment, go to the **Audience** tab and select one or more segments from the list. You can combine multiple segments using AND/OR operators, and add additional profile or context filters alongside them.

>[!NOTE]
>
>You need the **Test Manager** role or higher to create audience segments.

## Audience calculator {#audience-calculator}

After defining your audience criteria, select **Calculate** in the bottom bar to get an estimated count of users who qualify. This helps you validate the reach of your targeting before activating the feature.

>[!NOTE]
>
>The audience calculator does not return a value when context variables are included in the criteria, because context values are determined at runtime and cannot be predicted in advance.

## See also {#see-also}

* [Use context in audience rules](using-context-in-audience-rules.md)
* [Add percentage rules in audience criteria](adding-percentage-rules.md)
* [Complex audience rules](complex-rules.md)
* [Create your first feature flag](../feature-flags/create-your-first-feature-flag.md)
