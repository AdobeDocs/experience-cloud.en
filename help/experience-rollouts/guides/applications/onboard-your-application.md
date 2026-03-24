---
title: Onboard your application
description: Learn how to onboard a new application to Adobe Experience Rollouts so your team can start creating and managing feature flags.
---

# Onboard your application {#onboard-your-application}

You must have the **Admin** role to add a new application. See [User roles](../teams/user-roles.md) if you need to verify your role or request it from your team admin.

## Add a new application {#add-application}

1. Log in to the Experience Rollouts console and navigate to **Admin > Applications**.

   >[!NOTE]
   >
   >If the **New Application** button is not visible, verify that you are in the correct team and that you have the **Admin** role.

2. Select **New Application**.

3. Select the **channel** that matches your application type (web, mobile, desktop, or service).

4. Provide the following information:

   | Field | Description |
   |---|---|
   | **Application ID** | A unique identifier used when calling Experience Rollouts from your code. Use your application's client ID. |
   | **TTL** | The polling interval (in seconds) for refreshing the per-application cache. Applies to server-side SDKs only. |
   | **Team** | The team that will own and manage this application. Only members of this team can create and edit feature flags for it. |

5. Select **Add**. Your application is now registered and ready for feature flag configuration.

## What comes next {#next-steps}

Once your application is onboarded, your team can start creating feature flags:

* [Create your first feature flag](../../feature-flags/create-your-first-feature-flag.md)
* [Integrate Experience Rollouts in your app](../integrate/integrating-in-your-app.md)

## See also {#see-also}

* [Manage applications](manage-applications.md)
* [User roles](../teams/user-roles.md)
* [Log in to the console](../console/log-in-to-the-console.md)
