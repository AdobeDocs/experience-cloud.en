---
title: Troubleshooting
description: Use the Experience Rollouts workbench to diagnose feature flag evaluation issues for specific users, including checking which features are enabled, disabled, or unmatched for a given user identity.
---

# Troubleshooting {#troubleshooting}

Experience Rollouts includes a built-in diagnostic tool called the **Features Workbench** that helps you understand exactly which feature flags a specific user receives and why. Use it to investigate reports of unexpected feature behavior without needing to reproduce issues in code.

## Access the Features Workbench {#access-workbench}

To open the Features Workbench, follow these steps:

1. Log in to the Experience Rollouts console.
2. Navigate to **Workbench > End-Users** from the top menu.
3. Select the **Features** tab.

## Input a user identity {#input-identity}

To look up feature flag evaluations for a specific user, enter the following information in the workbench form:

* **ID type** — Select the type of identifier you are using. Supported types include email, GUID, and visitor ID. You can also enter a **release flag** directly to look up which releases were enabled for a user based on their flag value.
* **ID value** — Enter the user's identifier. If you select email as the ID type, note that multiple GUIDs can be associated with the same email address. A GUID dropdown is provided so you can switch between associated GUIDs.
* **Auth source type** — Select if applicable to your integration.
* **Context variables** — Optionally provide context key-value pairs that affect audience rule evaluation (for example, country, device type).
* **Team and application** — Select the team and application for which you want to fetch feature flags. Your current team and one of its applications are pre-selected by default.

After filling in the form, select **Fetch Features**.

## Interpret the results {#interpret-results}

The results depend on the ID type you entered.

### Email or GUID lookup {#email-guid-lookup}

When you look up a user by email or GUID, two sections appear in the results:

**Release flags**

This section shows three lists for the selected team and application:

* **Enabled** — Releases currently active for this user.
* **Disabled** — Releases that exist but are not enabled for this user.
* **Unused** — Release bits that have no release attached to them.

Releases associated with the currently selected team and application appear at the top of each list.

**Feature flags and groups**

This section lists all feature flags from the selected team and application that are currently enabled for the user. Each entry shows:

* Feature flag key and name
* Feature group (if the flag belongs to one)
* Variant (if A/B testing is configured)
* Whether the flag is audience-linked

You can also select **Show Request/Response** to inspect the exact API request and response that produced the results.

### Non-self email or non-GUID ID {#non-self-lookup}

When the email entered is not your own, or when a non-GUID ID type is used, only the **Feature flags and groups** section is shown.

### Release flag lookup {#release-flag-lookup}

When you enter a **release flag** as the ID type, only the **Release flags** section is shown, listing which releases were enabled and disabled for the user associated with that flag.

## Common issues {#common-issues}

The following table describes common problems and how to investigate them using the workbench.

| Symptom | What to check |
|---|---|
| User does not receive a feature flag they should | Verify the team and application selection. Check that the user's ID matches the audience rule type (email, GUID, etc.). Confirm the feature is in **Publish** or **Full Rollout** state. |
| Feature is enabled for all users unexpectedly | Confirm the feature has no audience rules applied, or that the percentage is set to 100%. Check if the feature is in **Full Rollout** state. |
| Audience rule is not matching | Use the workbench with context variables to confirm that the values passed at runtime match what is configured in the audience rule. |
| Feature flag state is correct but user still sees old behavior | Check the TTL configured for the application. The SDK caches feature data and refreshes only at the configured polling interval. |

## See also {#see-also}

* [Get support](get-support.md)
* [Contact support](contact-support.md)
* [Update release audience rules](../feature-flags/update-release-audience-rules.md)
* [Release states](../feature-flags/release-states.md)
