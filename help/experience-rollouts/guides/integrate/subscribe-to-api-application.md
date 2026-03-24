---
title: Subscribe to the API application in Adobe Developer Console
description: Learn how to subscribe your application to the Experience Rollouts API through Adobe Developer Console so you can call the feature flag endpoints.
exl-id: 23ce5c40-0def-49f8-b34a-2350bb421969
---
# Subscribe to the API application in Adobe Developer Console {#subscribe-to-api}

To call the Experience Rollouts API from your application, you need to subscribe to it through the [Adobe Developer Console](https://developer.adobe.com/console). This gives your application a client ID that Experience Rollouts uses to identify the caller.

## Prerequisites {#prerequisites}

Before subscribing, confirm the following:

* Your application is onboarded in the Experience Rollouts console — see [Onboard your application](../applications/onboard-your-application.md)
* You have access to the Adobe Developer Console for your organization

## Subscribe to the Experience Rollouts API {#subscribe}

To subscribe your application to the Experience Rollouts API, follow these steps:

1. Go to [Adobe Developer Console](https://developer.adobe.com/console) and sign in with your organization credentials.
2. Select your project, or create a new one.
3. Select **Add API**.
4. Search for and select **Experience Rollouts API**.
5. Follow the prompts to configure the API and generate credentials.
6. Note the **Client ID** generated for your project. This is the identifier you use when calling the Experience Rollouts API and when onboarding your application in the Experience Rollouts console.

## Server-side SDK integrations {#server-sdk}

If you are integrating using the Java SDK or Node.js SDK, you need a **service token** client ID in addition to an API key. The service token allows the SDK to call Experience Rollouts APIs in the background.

>[!NOTE]
>
>Server-side SDK client IDs must be allowlisted by Experience Rollouts support before they can make API calls. Contact support after completing the Developer Console setup.

## See also {#see-also}

* [Startup guide](startup-guide.md)
* [SDKs](sdks.md)
* [Onboard your application](../applications/onboard-your-application.md)
* [Integration steps](integration-steps.md)
