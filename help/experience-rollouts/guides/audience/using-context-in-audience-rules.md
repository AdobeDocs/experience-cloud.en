---
title: Use context in audience rules
description: Learn how to use context variables in audience rules for feature flags and feature groups in Adobe Experience Rollouts.
exl-id: 0367f475-9209-4d53-86b4-a739a73a23a7
---
# Use context in audience rules {#context-in-audience-rules}

Context variables are values provided by the client application at runtime. They allow you to target users based on dynamic, session-level information such as the user's active language, device type, or application state — criteria that are not part of the user's persistent profile.

Context variables are relevant for web, desktop, and mobile clients.

## How context variables work {#how-context-works}

Your application passes context variables to Experience Rollouts when evaluating a feature flag. You define rules in the console that check these values, and the platform uses them at the time of evaluation to determine whether the user qualifies.

If you define conditions in both the **Profile** and **Context** sections of the audience rules, all profile conditions are combined with all context conditions using AND logic.

## Context variable types {#variable-types}

### Pre-defined (list) type {#predefined-type}

A context variable with a fixed set of allowed values, such as a list of languages or countries.

Available operators: **Is**, **Is not equal to**, **Exists**, **In**

### Integer type {#integer-type}

A context variable that holds a numeric value.

Available operators: **Greater than**, **Greater than or equal to**, **Is**, **Less than**, **Less than or equal to**

### String type {#string-type}

A context variable that holds a free-form text value.

Available operators: **Is**, **Is not equal to**

## Adding a context variable {#adding-context-variable}

To add a context variable to an audience rule:

1. Open the feature flag or feature group in the console.
2. Go to the **Audience** tab.
3. Under **Context**, add a new condition.
4. Select the context variable, operator, and value.

If the context variable you need does not appear in the list, you can create a new one in a self-serve manner from the console's context variable management section.

>[!NOTE]
>
>When context variables are included in audience criteria, the **Audience Calculator** does not return an estimated count, because context values are determined at runtime and cannot be predicted in advance.

## See also {#see-also}

* [Audience in feature flags and feature groups](audience-in-feature-flags-and-feature-groups.md)
* [Add percentage rules in audience criteria](adding-percentage-rules.md)
* [Audience rule with client IP context variable](clientip-rule.md)
