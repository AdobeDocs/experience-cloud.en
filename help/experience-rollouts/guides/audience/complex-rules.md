---
title: Complex audience rules
description: Learn how to work with large or complex audience rule sets in Adobe Experience Rollouts, including bulk value limits and how to split rules across multiple conditions.
exl-id: 37e037b6-45eb-4261-b580-30d94d8e55da
---
# Complex audience rules {#complex-rules}

## Bulk value limits {#bulk-value-limits}

When adding a large number of values to a single audience rule — for example, a long list of email addresses — you may encounter an error indicating that the rule has exceeded the maximum allowed size.

Each audience rule has a size limit per attribute. For email addresses, the limit depends on the total character length of the entries rather than a fixed count. As a general guideline, use approximately **100–115 email addresses per rule**.

If you need to target more entries than this limit allows, split the list into smaller chunks and apply them as separate OR-connected conditions using nested logic.

## Using nested logic for complex rules {#nested-logic}

Nested logic lets you combine multiple audience conditions with precise AND/OR control. To enable it:

1. Add the audience conditions you need.
2. Enable **Nested Logic** in the audience rules section.
3. Each condition is assigned a number. Enter a logical expression that references these numbers, for example:
   * `1 and (2 or 3)`
   * `(1 and 2) or 3`
   * `(1 and 2) or (3 and 4)`

This is the same mechanism used for percentage rules in combination with other criteria. See [Add percentage rules in audience criteria](adding-percentage-rules.md) for worked examples.

## See also {#see-also}

* [Audience in feature flags and feature groups](audience-in-feature-flags-and-feature-groups.md)
* [Add percentage rules in audience criteria](adding-percentage-rules.md)
