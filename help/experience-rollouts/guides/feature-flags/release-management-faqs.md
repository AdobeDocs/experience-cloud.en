---
title: Release management FAQs
description: Find answers to common questions about release management in Adobe Experience Rollouts.
exl-id: 802b99bd-85ee-4f4d-afca-88d1297f8782
---
# Release management FAQs {#release-management-faqs}

## How do I request a release? {#request-release}

See [Request a release](request-a-release.md) for the full process and the information you need to provide.

## What audience criteria are supported for releases? {#audience-criteria}

Releases support the following audience rules:

* ID type (account type)
* Country
* User ID (GUID)
* Email address (individual or bulk list)
* Email domain
* Client IP
* Percentage (all users)
* Percentage (authenticated users only)

You can combine multiple rules using AND/OR logic, including nested conditions. See [Update release audience rules](update-release-audience-rules.md) for step-by-step configuration instructions.

## How do I add an application to a release? {#onboard-application}

After the release is created, open it in the console and add your application to the release configuration. The Product Release Owner for each application can then add the relevant feature flags. See [Release workflow end-to-end](release-workflow-end-to-end.md) for the full sequence.

## A feature is not being returned for a user who should qualify. How do I troubleshoot? {#troubleshoot}

Follow these steps to debug:

1. **Check the release state.** The release must be in **Published** or **Full rollout** state to serve features. See [Release states](release-states.md).
2. **Check the application and feature flag.** Verify that the feature flag is created for the correct application and that the application is associated with the correct release.
3. **Check that the feature flag is enabled.** A disabled flag will not be served even if the release is active.
4. **Review the audience criteria.** Confirm that the user meets all the conditions defined in the audience rules. Double-check the criteria for the specific release the feature is associated with.

## See also {#see-also}

* [Request a release](request-a-release.md)
* [Update release audience rules](update-release-audience-rules.md)
* [Release states](release-states.md)
* [Release workflow end-to-end](release-workflow-end-to-end.md)
