---
title: Java SDK integration guide
description: Learn how to integrate the Experience Rollouts Java SDK into your backend service to retrieve and evaluate feature flags.
---

# Java SDK integration guide {#java-sdk-integration-guide}

The Experience Rollouts Java SDK is a server-side library that caches feature flag data locally and evaluates flags without a synchronous API call on every request. This guide covers the current SDK (4.x).

## Prerequisites {#prerequisites}

Before integrating the Java SDK, ensure you have:

* JDK 11 or later (required from SDK version 3.0.0 onward; earlier versions support JDK 8+)
* A Maven-based build system
* An **API key** and **service token** client ID from your Adobe Developer Console project — see [Subscribe to the API application](../../integrate/subscribe-to-api-application.md)
* Your **application client IDs** registered in the Experience Rollouts console — see [Onboard your application](../../applications/onboard-your-application.md)

## Add the Maven dependency {#maven-dependency}

Add the Experience Rollouts Java SDK to your project's `pom.xml`:

```xml
<dependency>
  <groupId>com.adobe.cloudtech</groupId>
  <artifactId>fg-client-sdk</artifactId>
  <version>4.0.6</version>
</dependency>
```

## Initialize the SDK {#initialize}

The SDK is initialized once at application startup using `FloodgateClient.createInstance()`. The method takes a `FloodgateConfiguration` object that you build with the configuration builder.

### Implement the service token callback {#service-token-callback}

The SDK uses a callback interface to retrieve a fresh service token at runtime:

```java
private class FgConfigCallBack implements FGConfigBaseCallBack {

  @Override
  public String getIMSServiceToken() {
    // Fetch and return a valid service token
  }

  @Override
  public boolean isAnalyticsEnabled() {
    return false; // Set to true to enable analytics
  }
}
```

### Create the configuration object {#configuration}

Use the configuration builder to set up the SDK:

```java
FloodgateConfiguration configuration = FloodgateConfiguration.FloodgateConfigurationBuilder
    .aFloodgateConfiguration(
        FgEnv.PRD,                   // Use FgEnv.STG for Stage
        "<YOUR_API_KEY>",
        Set.of("<CLIENT_ID_1>", "<CLIENT_ID_2>"),
        new FgConfigCallBack(),
        CallType.ASYNC
    )
    .withRetryPolicy(retryPolicy)    // Optional: defaults to 5 retries, 10s interval
    .build();
```

Use `FgEnv.STG` for the Stage environment and `FgEnv.PRD` for Production.

### Create the client instance {#client-instance}

```java
FloodgateClient fgClient = FloodgateClient.createInstance(configuration);
```

## Retrieve feature flags {#retrieve-features}

### Authenticated user {#authenticated-user}

Use an IMS access token to retrieve feature flags for the current user:

```java
GetFeatureRequest request = GetFeatureRequestBuilder
    .aGetFeatureRequest("<CLIENT_ID>")
    .withAccessToken("<USER_ACCESS_TOKEN>")
    .withContext(context)
    .build();

FeaturesResponse[] features = fgClient.getFeatures(request);
```

### Anonymous user {#anonymous-user}

For unauthenticated users, pass a visitor ID and your service token:

```java
GetFeatureRequest request = GetFeatureRequestBuilder
    .aGetFeatureRequest("<CLIENT_ID>")
    .withServiceToken("<SERVICE_TOKEN>")
    .withVisitorId("<VISITOR_ID>")
    .withContext(context)
    .build();

FeaturesResponse[] features = fgClient.getFeatures(request);
```

### Retrieve a specific feature flag or release {#specific-feature}

To retrieve a single feature flag by key:

```java
GetFeatureRequest request = GetFeatureRequestBuilder
    .aGetFeatureRequest("<CLIENT_ID>")
    .withAccessToken("<ACCESS_TOKEN>")
    .withFeatureKey("<FEATURE_KEY>")
    .build();
```

To retrieve by release key, replace `.withFeatureKey()` with `.withReleaseKey()`.

## Check if a feature is enabled {#check-feature}

```java
boolean isEnabled = FloodgateClient.isFeatureEnabled(features, "MY_FEATURE_FLAG");

if (isEnabled) {
  // Serve the new experience
} else {
  // Serve the default experience
}
```

For release-based checks:

```java
boolean isEnabled = FloodgateClient.isFeatureEnabled(features, "MY_RELEASE", "MY_FEATURE_FLAG");
```

## Cache management {#cache-management}

The SDK caches feature flag data and refreshes it on a polling interval set per application in the console. To trigger an on-demand cache refresh:

```java
fgClient.refreshClientCache("<CLIENT_ID>");
```

### Non-cacheable clients {#non-cacheable}

For non-cacheable clients, `getFeature()` makes a live API call each time. The SDK continues background polling and switches to cache-based serving when the client becomes cacheable. Supported from SDK version 0.8 onward.

## Configuration options {#configuration-options}

The following optional configuration methods are available on the builder:

| Option | Method | Description |
|---|---|---|
| Always use cache | `.alwaysCache()` | Bypasses caching response from the API; use for flags with no audience rules |
| Disable caching | `.neverCache()` | Disables default caching; useful for custom cache refresh logic |
| Custom HTTP client | `.withHttpClient(client)` | Use your own HTTP client |
| Custom executor | `.withScheduledExecutorService(executor)` | Use your own scheduled executor for background polling |
| Include control group | `.includeControlGroup()` | Returns control group data in the feature response |

## Handle errors {#error-handling}

Wrap `getFeatures()` calls to catch SDK exceptions:

```java
try {
  features = fgClient.getFeatures(request);
} catch (FgClientException e) {
  int statusCode = e.getStatusCode();
  // Handle error and serve default experience
} catch (FgInitException e) {
  e.printStackTrace();
}
```

## See also {#see-also}

* [Java SDK release notes](java-sdk-release-notes.md)
* [SDKs](../../integrate/sdks.md)
* [Subscribe to the API application](../../integrate/subscribe-to-api-application.md)
* [Integration steps](../../integrate/integration-steps.md)
