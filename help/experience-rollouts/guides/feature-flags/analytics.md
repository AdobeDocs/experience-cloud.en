---
title: Analytics
description: Learn how to enable and use the built-in analytics dashboard in Adobe Experience Rollouts to track feature flag performance and measure rollout impact.
exl-id: edddca99-f263-461b-a16f-b46ee7c15f6c
---
# Analytics {#analytics}

Experience Rollouts provides built-in analytics for feature flags, feature groups, cross-team feature groups, and releases. Use the analytics dashboard to understand how many users are participating in your rollout and how the variant and control groups compare.

## Enable analytics {#enable}

Analytics must be enabled at two levels:

1. **Application level** — Contact Experience Rollouts support to enable analytics for your application.
2. **Feature flag level** — Once analytics is enabled for your application, check the **Enable analytics** checkbox on the **Basic Details** tab of each feature flag you want to track.

>[!NOTE]
>
>Analytics can be enabled for up to 20 feature flags per application by default. Contact support if you need to increase this limit.

## View the analytics dashboard {#dashboard}

Once analytics is enabled, all feature flags, feature groups, and releases for your application will start tracking data. Access the dashboard by selecting **Results** on the feature flag, feature group, or release you want to analyze.

The dashboard displays:

* **Participants** — Total number of users who qualified for the feature (variant + control group combined)
* **Control group** — Number of users assigned to the control group (users who received the default experience)
* **Day-level graph** — Daily line charts showing enrollment in the variant and control group over time; markers indicate when the feature flag configuration was updated
* **Variant-level analytics** — Cumulative count of users enrolled in the control group and each variant

For feature groups and releases, select the **Results** drop-down to pick an application and view analytics for that application. Analytics is only available for applications that have it enabled.

## See also {#see-also}

* [Create your first feature flag](create-your-first-feature-flag.md)
* [A/B testing with feature flags](a-b-testing.md)
* [Create a feature group](create-a-feature-group.md)
