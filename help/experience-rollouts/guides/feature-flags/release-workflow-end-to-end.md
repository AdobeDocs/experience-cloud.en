---
title: Release workflow end-to-end
description: Learn the end-to-end workflow for managing a coordinated release in Adobe Experience Rollouts, from defining feature flags to going live.
---

# Release workflow end-to-end {#release-workflow}

This page describes the full sequence of activities involved in a coordinated release managed by a Release Manager.

## 1. Define feature flags per application {#define-flags}

Each product team assigns a **Product Release Owner** who logs in to the Experience Rollouts console and creates feature flags for the applications they own. The product team then implements the conditional logic in their code, placing features behind these flags.

## 2. Create the release {#create-release}

Creating a new release requires a support request — it is not fully self-serve. Contact Experience Rollouts support to have the release created. Provide the release name, owning team, target environment, objective, participating applications, and expected duration.

Once the release is confirmed, the Release Manager opens the console and completes the release configuration.

## 3. Add feature flags to the release {#add-flags}

For each application added to the release, the application's Product Release Owner logs in and adds the relevant feature flags to the release. These flags represent the features that will go live with the release.

## 4. Configure the audience {#configure-audience}

The Release Manager selects the audience for the release — for example, 1% of users in a specific country, all users with a specific email domain, or a list of specific user IDs. Once configured, the Release Manager saves and publishes the release, which pushes it live for the specified audience.

## 5. Expand and manage the rollout {#expand}

After the release goes live, the Release Manager can adjust the audience rules to expand the rollout gradually, monitor for issues, and use the release state controls to manage the lifecycle. See [Release states](release-states.md) for details.

## Key points {#key-points}

* All participating applications deploy their code to production independently behind feature flags — no coordinated deployment timing is needed.
* The release is the single point of control that activates all flags across teams simultaneously.
* Audience targeting for releases is based on authentication token attributes (country, email, user ID, percentage).

## See also {#see-also}

* [Request a release](request-a-release.md)
* [Update release audience rules](update-release-audience-rules.md)
* [Release states](release-states.md)
