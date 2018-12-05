---
title: Implement Experience Cloud Integrations with Launch
description:
seo-description:
seo-title: Implement Experience Cloud Integrations with Launch
solution: Experience Cloud
---

# Experience Cloud Integrations

## Audience Sharing

Audience Sharing with the People Core Service requires that you implement the Experience Cloud ID Service and the Audience Manager Module for Analytics, which we have already done. The Experience Cloud ID Service extension for Launch will guarantee that the ID Service always loads in the correct order to set the appropriate MID parameter in the Analytics and Target calls to ensure proper visitor stitching on Adobe's backend. This will enable you to share audiences from Analytics, Audience Manager, and the Audience Library to Target and Analytics.

### Validate the Audience Sharing information

These validation steps require that you have the appropriate level of access to complete all of the tasks. If you are unable to complete the tasks, please work with other individuals in your organization who have the required access or contact your administrator.

## Analytics for Target (A4T)

In addition to implementing the Experience Cloud Id Service, A4T requires that Target loads before Analytics. The lessons in this tutorial You should always see matching supplemental data ids (SDIDs) in both calls&mdash;these ids stitch hits together in the Analytics processing for A4T.

### Validate the A4T Implementation

## Customer Attributes

In addition to implementing the Experience Cloud Id Service, Customer Attributes requires that you set Customer Ids via the Id Service. The Customer Ids need to be set *before* Target and Analytics load. When using a "Library Loaded" rule to fire the target-global-mbox, be sure to use the "Set Customer Id" action before all of the Target actions.

### Validate the Customer Attributes Implementation