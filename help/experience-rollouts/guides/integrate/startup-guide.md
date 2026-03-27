---
title: Startup guide
description: Follow these steps to get your application integrated with Adobe Experience Rollouts, from requesting access to creating your first feature flag.
exl-id: 7aa09535-45fa-4ddf-9e3f-a23f8a8ee666
---
# Startup guide {#startup-guide}

Follow these steps to integrate Experience Rollouts into your application.

## Step 1: Request access {#step-1-access}

Request access to the Experience Rollouts console and join your team. See [Request access](../console/request-access.md) for step-by-step instructions.

## Step 2: Onboard your application {#step-2-onboard}

After gaining access, log in to the Experience Rollouts console and verify that your application is listed under your team. If it is not, ask your team admin to add it. See [Onboard your application](../applications/onboard-your-application.md).

Before onboarding, prepare the following:

| Requirement | Details |
|---|---|
| **Application ID** | A unique client identifier used when calling the Experience Rollouts APIs. Use your application's existing client ID where available. |
| **Server-side clients** | If integrating with a server-side SDK, you need an admin client ID with appropriate permissions. |
| **Desktop clients** | A product code and product version can be used in place of a client ID. |

## Step 3: Get your credentials {#step-3-credentials}

If you are integrating via a server-side SDK, you need a service token client ID. Contact Experience Rollouts support to have your client ID allowlisted before you can make API calls from the SDK.

## Step 4: Integrate using an SDK {#step-4-integrate}

Follow the [integration steps](integration-steps.md) for your application type. Choose the path that fits your stack:

* **Web services** → Java SDK or Node.js SDK
* **Web and mobile apps** → Web SDK or mobile SDK (coming soon)
* **Desktop apps** → SDK (coming soon)

## Step 5: Create and test your first feature flag {#step-5-feature-flag}

Once integration is complete, create your first feature flag in the console and test it:

* [Create your first feature flag](../feature-flags/create-your-first-feature-flag.md)

## See also {#see-also}

* [Integrate Experience Rollouts in your app](integrating-in-your-app.md)
* [Integration steps](integration-steps.md)
* [SDKs](sdks.md)
