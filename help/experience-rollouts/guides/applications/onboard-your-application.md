---
title: Onboard your application
description: Learn how to onboard a new application to Adobe Experience Rollouts so you can start creating and managing feature flags.
exl-id: d88c27a5-f490-4504-9764-5e4ce98fdf20
---
# Onboard your application {#onboard-your-application}

You must have the **Admin** role to add a new application. Contact your admin if you need to verify or update your role.

## Add a new application {#add-application}

1. Log in to the Experience Rollouts console and navigate to **Experience Rollout > Applications**.

   >[!NOTE]
   >
   >If the **New Application** button is not visible, verify that you have the **Floodgate Admin** role.

2. Select **New Application**.

3. Select the **platform** that matches your application type (web or mobile).

4. Provide the following information:

   | Field | Description |
   |---|---|
   | **Application ID** | A unique identifier used when calling Experience Rollouts from your code. Use your application's client ID. |
   | **TTL** | The polling interval (in seconds) for refreshing the per-application cache. Applies to server-side SDKs only. |

5. Select **Add**. Your application is now registered and ready for feature flag configuration.

## What comes next {#next-steps}

Once your application is onboarded, you can start creating feature flags:

* [Create your first feature flag](../feature-flags/create-your-first-feature-flag.md)
* [Integrate Experience Rollouts in your app](../integrate/integrating-in-your-app.md)

## See also {#see-also}

* [Manage applications](manage-applications.md)
* [Log in to the console](../console/log-in-to-the-console.md)
