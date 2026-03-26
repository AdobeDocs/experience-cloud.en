---
title: Release management FAQs
description: Find answers to common questions about release management in Adobe Experience Rollouts.
exl-id: 802b99bd-85ee-4f4d-afca-88d1297f8782
---
# Release management FAQs {#release-management-faqs}

## How do I request a release? {#request-release}

Contact Experience Rollouts support to request a release. Provide your team name, application details, target audience, and desired rollout timeline.

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

You can combine multiple rules using AND/OR logic, including nested conditions.

## How do I add an application to a release? {#onboard-application}

After the release is created, open it in the console and add your application to the release configuration. The Product Release Owner for each application can then add the relevant feature flags.

## A feature is not being returned for a user who should qualify. How do I troubleshoot? {#troubleshoot}

Follow these steps to debug:

1. **Check the release state.** The release must be in **Published** or **Full rollout** state to serve features.
2. **Check the application and feature flag.** Verify that the feature flag is created for the correct application and that the application is associated with the correct release.
3. **Check that the feature flag is enabled.** A disabled flag will not be served even if the release is active.
4. **Review the audience criteria.** Confirm that the user meets all the conditions defined in the audience rules. Double-check the criteria for the specific release the feature is associated with.

## See also {#see-also}

* [Contact support](../support/contact-support.md)
