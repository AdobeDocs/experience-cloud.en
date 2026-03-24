---
title: Use enterprise org data in audience rules
description: Learn how to use enterprise organization IDs as audience criteria in Adobe Experience Rollouts to target specific customer organizations.
---

# Use enterprise org data in audience rules {#enterprise-org-data}

Experience Rollouts supports targeting users based on their enterprise organization (org) ID. This allows you to roll out features to specific customer organizations before making them broadly available.

## Adding an org in an audience rule {#adding-org-rule}

Enterprise org targeting is available in the **Audience** tab under **Audience Rules > Profile > Enterprise**.

Two org types are supported:

### DME orgs {#dme-orgs}

DME orgs are identified by their org ID. When creating the rule, enter only the org ID — do not include an auth source.

### DMA orgs {#dma-orgs}

DMA orgs use org IDs in the format `XXXXXXXXXXXXXXXXXXXXXXXX@ADOBEORG`. When entering a DMA org ID:

* Use the full org ID including the `@ADOBEORG` suffix.
* Enter `ADOBEORG` in all caps.

**Example:** `57F22B5D5A5F83AE0A495E6E@ADOBEORG`

## Important notes {#important-notes}

* Org-based targeting is evaluated against the organization associated with the user's authenticated session. Ensure the user is signed in to the correct organization when testing.
* If an org you expect to find is not appearing in the audience criteria, or if features are not being returned as expected for a specific org, contact Experience Rollouts support.
* Stage and Production environments may differ in which orgs are available. Test your audience rules in Stage before promoting to Production.

## See also {#see-also}

* [Audience in feature flags and feature groups](audience-in-feature-flags-and-feature-groups.md)
* [Update release audience rules](../feature-flags/update-release-audience-rules.md)
* [Complex audience rules](complex-rules.md)
