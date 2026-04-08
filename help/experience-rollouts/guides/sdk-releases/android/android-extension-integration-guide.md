---
title: Experience Rollout extension for Android integration guide
description: Learn how to integrate the Experience Rollout extension with the Adobe Experience Platform Mobile SDK on Android.
exl-id: 683ef4d4-e637-4b7b-b694-689c7e65a99e
---
# Experience Rollout extension for Android {#android-extension-integration-guide}

This guide describes how to integrate the Experience Rollout extension with the Adobe Experience Platform Mobile SDK on Android.

## Prerequisites {#prerequisites}

Before implementing the Experience Rollout extension, ensure you have:

* A mobile property configured in [Adobe Experience Platform Data Collection](https://experience.adobe.com/#/data-collection)
* The Experience Rollout extension installed and configured in your mobile property
* An Adobe Experience Cloud Organization ID
* Minimum SDK: API 21 (Android 5.0 Lollipop)

## Extension dependencies {#extension-dependencies}

The Experience Rollout extension requires the following Adobe Experience Platform extensions:

| Extension | Description | Required |
|---|---|---|
| Mobile Core | Provides core functionality including configuration and event processing | Yes |
| Lifecycle | Collects application lifecycle and session data for the Mobile SDK | Yes |
| Edge Network | Enables communication with Adobe Experience Platform Edge Network | Yes |
| Edge Identity | Manages user identity for Edge Network | Yes |

Ensure these extensions are installed in your Data Collection mobile property and included in your app dependencies.

## Configure Experience Rollout extension in Data Collection {#configure}

### Install the extension {#install-extension}

1. Log in to [Adobe Experience Platform Data Collection](https://experience.adobe.com/#/data-collection).
1. Select the **Tags** tab and choose your mobile property.
1. Navigate to **Extensions** > **Catalog**.
1. Search for **Experience Rollout extension** and select **Install**.
1. Configure the extension settings:

   | Setting | Description |
   |---|---|
   | Sandbox | The Adobe Experience Platform sandbox containing your Experience Rollout configuration |
   | Application ID | A unique identifier for your application in Experience Rollout |
   | Dataset ID | The Adobe Experience Platform dataset ID for the analytics event data |

1. Select **Save**.
1. Follow the [publishing process](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/overview) to update your configuration.

### Get the Environment File ID {#environment-file-id}

1. In your mobile property, navigate to **Environments**.
1. Select the box icon under the **Install** column for your environment.
1. In the **Mobile Install Instructions** dialog, copy the **Environment File ID**.

## Add Experience Rollout extension to your app {#add-to-app}

### Add dependencies {#add-dependencies}

Add the Mobile SDK dependencies to your project. The Experience Rollout extension requires Mobile Core and the Edge-related extensions listed below.

#### Using Gradle with BOM (Recommended) {#gradle-bom}

Add the following dependencies to your app's `build.gradle.kts` file:

```kotlin
dependencies {
    // Adobe Experience Platform Mobile SDK BOM
    implementation(platform("com.adobe.marketing.mobile:sdk-bom:3.+"))

    // Required extensions
    implementation("com.adobe.marketing.mobile:core")
    implementation("com.adobe.marketing.mobile:lifecycle")
    implementation("com.adobe.marketing.mobile:edge")
    implementation("com.adobe.marketing.mobile:edgeidentity")

    // Experience Rollout extension
    implementation("com.adobe.marketing.mobile:rollout")
}
```

#### Using Gradle (Groovy) {#gradle-groovy}

```groovy
dependencies {
    // Adobe Experience Platform Mobile SDK BOM
    implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')

    // Required extensions
    implementation 'com.adobe.marketing.mobile:core'
    implementation 'com.adobe.marketing.mobile:lifecycle'
    implementation 'com.adobe.marketing.mobile:edge'
    implementation 'com.adobe.marketing.mobile:edgeidentity'

    // Experience Rollout extension
    implementation 'com.adobe.marketing.mobile:rollout'
}
```

>[!IMPORTANT]
>
>For production applications, Adobe recommends using explicit version numbers instead of dynamic versions. See [Managing Gradle dependencies](https://docs.gradle.org/current/userguide/dependency_management.html) for more information.

### Add permissions {#add-permissions}

Add the following permissions to your `AndroidManifest.xml` file:

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

### Initialize the SDK {#initialize-sdk}

Initialize the Mobile SDK in your `Application` class before calling any Experience Rollout extension APIs. Use the Environment File ID from your mobile property with `MobileCore.initialize` so the app picks up the rollout settings you published in Data Collection.

#### Using MobileCore.initialize {#mobile-core-initialize}

Available starting from Android BOM version 3.8.0, this API automatically registers extensions and enables lifecycle tracking.

>[!IMPORTANT]
>
>For production apps, use `LoggingMode.ERROR` only. Do not use `DEBUG` or `VERBOSE` in release builds.

**Kotlin**

```kotlin
import android.app.Application
import com.adobe.marketing.mobile.LoggingMode
import com.adobe.marketing.mobile.MobileCore

class MainApplication : Application() {

    override fun onCreate() {
        super.onCreate()

        MobileCore.setLogLevel(LoggingMode.ERROR)

        // Initialize with your Environment File ID from Data Collection
        MobileCore.initialize(this, "YOUR_ENVIRONMENT_FILE_ID")
    }
}
```

**Java**

```java
import android.app.Application;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;

public class MainApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();

        MobileCore.setLogLevel(LoggingMode.ERROR);

        // Initialize with your Environment File ID from Data Collection
        MobileCore.initialize(this, "YOUR_ENVIRONMENT_FILE_ID", null);
    }
}
```

### Register the Application class {#register-application}

Register your `Application` class in `AndroidManifest.xml`:

```xml
<application
    android:name=".MainApplication"
    ... >
</application>
```

## Evaluation context {#evaluation-context}

`FeatureEvaluationContext` includes targeting attributes (used for rollout rule matching) and optional identity (used for analytics).

| Method | Required | Description |
|---|---|---|
| `withIdentity(namespace, id)` | No | First argument: identity namespace (see [Adobe Identity namespaces](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/namespaces)). Second argument: identity value. Include this when you want that namespace and ID represented in analytics for this evaluation. If not provided, analytics uses ECID by default. This is not used to drive feature enablement decisions. |
| `withAttributes(map)` | No | `Map<String, List<String>>`. Key is the context attribute name used by your rollout rules (for example `locale`, `platform`, `appVersion`, `deviceType`). Value is the list of candidate attribute values for that key for the current user/session (for example `["en_US"]` or `["phone"]`). |

**Kotlin**

```kotlin
import com.adobe.marketing.mobile.rollout.FeatureEvaluationContext

val attrs = mapOf(
    "locale" to listOf("en_US"),
    "platform" to listOf("ANDROID"),
    "appVersion" to listOf("3.0.0")
)

val ctx = FeatureEvaluationContext.builder()
    .withIdentity("Email", "customer@example.com")
    .withAttributes(attrs)
    .build()
```

**Java**

```java
import com.adobe.marketing.mobile.rollout.FeatureEvaluationContext;
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

Map<String, List<String>> attrs = new HashMap<>();
attrs.put("locale", Arrays.asList("en_US"));
attrs.put("platform", Arrays.asList("ANDROID"));
attrs.put("appVersion", Arrays.asList("3.0.0"));

FeatureEvaluationContext ctx = FeatureEvaluationContext.builder()
        .withIdentity("Email", "customer@example.com")
        .withAttributes(attrs)
        .build();
```

### Sample targeting attributes {#sample-attributes}

| Attribute | Description | Example values |
|---|---|---|
| `locale` | User's locale/language | `["en_US"]`, `["fr_FR"]` |
| `platform` | Platform identifier | `["ANDROID"]` |
| `appVersion` | Application version | `["3.0.0"]` |
| `deviceType` | Device type | `["phone"]`, `["tablet"]` |

## API reference {#api-reference}

### isFeatureEnabled {#is-feature-enabled}

`isFeatureEnabled` returns whether an Experience Rollout feature is on or off for the given context. Pass `featureKey`, a `FeatureEvaluationContext` (optional targeting attributes and optional identity for analytics), and a callback. See [Evaluation context](#evaluation-context).

**Signature**

*Kotlin*

```kotlin
Rollout.isFeatureEnabled(
    featureKey: String,
    evaluationContext: FeatureEvaluationContext,
    callback: AdobeCallback<Boolean>
)
```

*Java*

```java
Rollout.isFeatureEnabled(
    String featureKey,
    FeatureEvaluationContext evaluationContext,
    AdobeCallback<Boolean> callback);
```

**Parameters**

| Parameter | Type | Description |
|---|---|---|
| `featureKey` | String | Feature key to evaluate in Experience Rollout |
| `evaluationContext` | FeatureEvaluationContext | Include targeting attributes and optional identity for analytics as needed; use `FeatureEvaluationContext.builder().build()` for an empty context. See [Evaluation context](#evaluation-context). |
| `callback` | AdobeCallback&lt;Boolean&gt; | Invoked with `true` if the feature is enabled, `false` otherwise. You can also pass `AdobeCallbackWithError<Boolean>` to handle `fail(...)`. |

**Examples**

*Kotlin*

```kotlin
import com.adobe.marketing.mobile.AdobeCallback
import com.adobe.marketing.mobile.rollout.Rollout

Rollout.isFeatureEnabled(
    "new-checkout-experience",
    ctx,
    object : AdobeCallback<Boolean> {
        override fun call(isEnabled: Boolean?) {
            if (isEnabled == true) {
                showNewCheckout()
            } else {
                showDefaultCheckout()
            }
        }
    }
)
```

*Java*

```java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.rollout.Rollout;

Rollout.isFeatureEnabled(
    "new-checkout-experience",
    ctx,
    new AdobeCallback<Boolean>() {
        @Override
        public void call(Boolean isEnabled) {
            if (Boolean.TRUE.equals(isEnabled)) {
                showNewCheckout();
            } else {
                showDefaultCheckout();
            }
        }
    }
);
```

### getFeature {#get-feature}

`getFeature` returns the evaluated feature payload for the provided context. Use this API when you need more than enabled/disabled and want feature metadata or values.

**Signature**

*Kotlin*

```kotlin
Rollout.getFeature(
    featureKey: String,
    evaluationContext: FeatureEvaluationContext,
    callback: AdobeCallback<FeatureEvaluationResult>
)
```

*Java*

```java
Rollout.getFeature(
    String featureKey,
    FeatureEvaluationContext evaluationContext,
    AdobeCallback<FeatureEvaluationResult> callback);
```

**Parameters**

| Parameter | Type | Description |
|---|---|---|
| `featureKey` | String | Feature key to evaluate in Experience Rollout |
| `evaluationContext` | FeatureEvaluationContext | Include targeting attributes and optional identity for analytics as needed; use `FeatureEvaluationContext.builder().build()` for an empty context. See [Evaluation context](#evaluation-context). |
| `callback` | AdobeCallback&lt;FeatureEvaluationResult&gt; | Invoked with the evaluated feature payload; may be `null` when the feature is not found. You can also pass `AdobeCallbackWithError<FeatureEvaluationResult>` to handle `fail(...)`. |

**Response**

*FeatureEvaluationResult*

| Field | Type | Description |
|---|---|---|
| `id` | Int | Numeric feature identifier |
| `key` | String | Feature key |
| `releaseKey` | String? | Release key for this feature when available |
| `meta` | String? | Feature metadata as a JSON string when available |
| `analyticsParam` | AnalyticsParam? | Analytics details for the evaluated feature |

*AnalyticsParam*

| Field | Type | Description |
|---|---|---|
| `releaseId` | Int | Numeric release identifier |
| `featureId` | Int | Numeric feature identifier |
| `variantId` | String? | Variant identifier |

**Examples**

*Kotlin*

```kotlin
import com.adobe.marketing.mobile.AdobeCallback
import com.adobe.marketing.mobile.rollout.FeatureEvaluationResult
import com.adobe.marketing.mobile.rollout.Rollout

Rollout.getFeature(
    "new-checkout-experience",
    ctx,
    object : AdobeCallback<FeatureEvaluationResult> {
        override fun call(feature: FeatureEvaluationResult?) {
            val meta = feature?.meta
            if (!meta.isNullOrEmpty()) {
                applyMetaDrivenExperience(meta)
            } else {
                showFallbackExperience()
            }
        }
    }
)
```

*Java*

```java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.rollout.FeatureEvaluationResult;
import com.adobe.marketing.mobile.rollout.Rollout;

Rollout.getFeature(
    "new-checkout-experience",
    ctx,
    new AdobeCallback<FeatureEvaluationResult>() {
        @Override
        public void call(FeatureEvaluationResult feature) {
            String meta = feature != null ? feature.getMeta() : null;
            if (meta != null && !meta.isEmpty()) {
                applyMetaDrivenExperience(meta);
            } else {
                showFallbackExperience();
            }
        }
    }
);
```

### refreshCache {#refresh-cache}

By default, the Experience Rollout extension regularly syncs the latest rollout rules and features from the server on a schedule you can configure. If you need an update sooner than the next scheduled sync, call `refreshCache` to force a refresh. Typical cases include after sign-in or when app state changes in a way that should affect targeting.

**Syntax**

*Kotlin*

```kotlin
Rollout.refreshCache()
```

*Java*

```java
Rollout.refreshCache();
```

### extensionVersion {#extension-version}

Returns the version string of the Experience Rollout extension.

**Syntax**

```kotlin
Rollout.extensionVersion(): String
```

**Example**

*Kotlin*

```kotlin
val version = Rollout.extensionVersion()
```

*Java*

```java
String version = Rollout.extensionVersion();
```

## API summary {#api-summary}

| API | Returns |
|---|---|
| `isFeatureEnabled(featureKey, evaluationContext, callback)`. `FeatureEvaluationContext` carries targeting attributes for rules and optional identity for analytics. See [Feature evaluation](#is-feature-enabled). | Boolean via callback |
| `getFeature(featureKey, evaluationContext, callback)`. Returns the evaluated feature payload for the given context. See [getFeature](#get-feature). | FeatureEvaluationResult via callback |
| `refreshCache()` | void |
| `extensionVersion()` | String |

## See also {#see-also}

* [Mobile applications](../../integrate/mobile-applications.md)
* [Integration steps](../../integrate/integration-steps.md)
* [SDKs](../../integrate/sdks.md)
