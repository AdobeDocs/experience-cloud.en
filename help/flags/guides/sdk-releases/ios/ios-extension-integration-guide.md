---
title: Experience Rollout extension for iOS integration guide
description: Learn how to integrate the Experience Rollout extension with the Adobe Experience Platform Mobile SDK on iOS.
hide: true
---
# Experience Rollout extension for iOS {#ios-extension-integration-guide}

This guide describes how to integrate the Experience Rollout extension with the Adobe Experience Platform Mobile SDK on iOS.

## Prerequisites {#prerequisites}

Before implementing the Experience Rollout extension, ensure you have:

* A mobile property configured in [Adobe Experience Platform Data Collection](https://experience.adobe.com/#/data-collection)
* The Experience Rollout extension installed and configured in your mobile property
* An Adobe Experience Cloud Organization ID
* Minimum deployment target: iOS 12.0
* Xcode 14.1 or later

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

#### Using Swift Package Manager (Recommended) {#swift-package-manager}

1. In Xcode, navigate to **File** > **Add Package Dependencies**.
1. Enter the Adobe Experience Platform Mobile SDK repository URL:

   ```
   https://github.com/adobe/aepsdk-core-ios
   ```

1. Add the following packages:

   | Package | Repository |
   |---|---|
   | AEPCore, AEPLifecycle | `https://github.com/adobe/aepsdk-core-ios` |
   | AEPEdge | `https://github.com/adobe/aepsdk-edge-ios` |
   | AEPEdgeIdentity | `https://github.com/adobe/aepsdk-edgeidentity-ios` |
   | AEPRollout | `https://github.com/adobe/aepsdk-rollout-ios` |

#### Using CocoaPods {#cocoapods}

Add the following pods to your `Podfile`:

```ruby
pod 'AEPCore'
pod 'AEPLifecycle'
pod 'AEPEdge'
pod 'AEPEdgeIdentity'
pod 'AEPRollout'
```

Then run:

```bash
pod install
```

>[!IMPORTANT]
>
>For production applications, Adobe recommends pinning to explicit version numbers instead of using `~>` or open ranges. See the [CocoaPods versioning guide](https://guides.cocoapods.org/using/the-podfile.html) for more information.

### Initialize the SDK {#initialize-sdk}

Initialize the Mobile SDK in your `AppDelegate` (or `SceneDelegate`) before calling any Experience Rollout extension APIs. Use the Environment File ID from your mobile property so the app picks up the rollout settings you published in Data Collection.

**Swift**

```swift
import AEPCore
import AEPLifecycle
import AEPEdge
import AEPEdgeIdentity
import AEPRollout

@main
class AppDelegate: UIResponder, UIApplicationDelegate {

    func application(
        _ application: UIApplication,
        didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
    ) -> Bool {

        MobileCore.setLogLevel(.error)

        MobileCore.registerExtensions(
            [Lifecycle.self, Edge.self, Identity.self, Rollout.self]
        ) {
            // Initialize with your Environment File ID from Data Collection
            MobileCore.configureWith(appId: "YOUR_ENVIRONMENT_FILE_ID")
        }

        return true
    }
}
```

**Objective-C**

```objc
@import AEPCore;
@import AEPLifecycle;
@import AEPEdge;
@import AEPEdgeIdentity;
@import AEPRollout;

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application
    didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    [AEPMobileCore setLogLevel:AEPLogLevelError];

    NSArray *extensions = @[
        AEPMobileLifecycle.class,
        AEPMobileEdge.class,
        AEPMobileEdgeIdentity.class,
        AEPMobileRollout.class
    ];

    [AEPMobileCore registerExtensions:extensions completion:^{
        // Initialize with your Environment File ID from Data Collection
        [AEPMobileCore configureWithAppId:@"YOUR_ENVIRONMENT_FILE_ID"];
    }];

    return YES;
}

@end
```

>[!IMPORTANT]
>
>For production apps, use `LogLevel.error` only. Do not use `.debug` or `.verbose` in release builds.

## Evaluation context {#evaluation-context}

`FeatureEvaluationContext` includes targeting attributes (used for rollout rule matching) and optional identity (used for analytics).

| Method | Required | Description |
|---|---|---|
| `withIdentity(namespace:id:)` | No | First argument: identity namespace (see [Adobe Identity namespaces](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/namespaces)). Second argument: identity value. Include this when you want that namespace and ID represented in analytics for this evaluation. If not provided, analytics uses ECID by default. This is not used to drive feature enablement decisions. |
| `withAttributes(_:)` | No | `[String: [String]]`. Key is the context attribute name used by your rollout rules (for example `locale`, `platform`, `appVersion`, `deviceType`). Value is the list of candidate attribute values for that key for the current user/session (for example `["en_US"]` or `["phone"]`). |

**Swift**

```swift
import AEPRollout

let attrs: [String: [String]] = [
    "locale": ["en_US"],
    "platform": ["IOS"],
    "appVersion": ["3.0.0"]
]

let ctx = FeatureEvaluationContext.builder()
    .withIdentity(namespace: "Email", id: "customer@example.com")
    .withAttributes(attrs)
    .build()
```

**Objective-C**

```objc
@import AEPRollout;

NSDictionary<NSString *, NSArray<NSString *> *> *attrs = @{
    @"locale": @[@"en_US"],
    @"platform": @[@"IOS"],
    @"appVersion": @[@"3.0.0"]
};

AEPFeatureEvaluationContext *ctx = [[[AEPFeatureEvaluationContextBuilder builder]
    withIdentityNamespace:@"Email" id:@"customer@example.com"]
    withAttributes:attrs]
    .build;
```

### Sample targeting attributes {#sample-attributes}

| Attribute | Description | Example values |
|---|---|---|
| `locale` | User's locale/language | `["en_US"]`, `["fr_FR"]` |
| `platform` | Platform identifier | `["IOS"]` |
| `appVersion` | Application version | `["3.0.0"]` |
| `deviceType` | Device type | `["phone"]`, `["tablet"]` |

## API reference {#api-reference}

### isFeatureEnabled {#is-feature-enabled}

`isFeatureEnabled` returns whether an Experience Rollout feature is on or off for the given context. Pass `featureKey`, a `FeatureEvaluationContext` (optional targeting attributes and optional identity for analytics), and a completion handler. See [Evaluation context](#evaluation-context).

**Signature**

*Swift*

```swift
Rollout.isFeatureEnabled(
    featureKey: String,
    evaluationContext: FeatureEvaluationContext,
    completion: @escaping (Bool) -> Void
)
```

*Objective-C*

```objc
[AEPMobileRollout isFeatureEnabled:(NSString *)featureKey
               evaluationContext:(AEPFeatureEvaluationContext *)evaluationContext
                      completion:(void (^)(BOOL))completion];
```

**Parameters**

| Parameter | Type | Description |
|---|---|---|
| `featureKey` | String | Feature key to evaluate in Experience Rollout |
| `evaluationContext` | FeatureEvaluationContext | Include targeting attributes and optional identity for analytics as needed; use `FeatureEvaluationContext.builder().build()` for an empty context. See [Evaluation context](#evaluation-context). |
| `completion` | `(Bool) -> Void` | Called with `true` if the feature is enabled, `false` otherwise. |

**Examples**

*Swift*

```swift
import AEPRollout

Rollout.isFeatureEnabled(
    featureKey: "new-checkout-experience",
    evaluationContext: ctx
) { isEnabled in
    if isEnabled {
        showNewCheckout()
    } else {
        showDefaultCheckout()
    }
}
```

*Objective-C*

```objc
@import AEPRollout;

[AEPMobileRollout isFeatureEnabled:@"new-checkout-experience"
               evaluationContext:ctx
                      completion:^(BOOL isEnabled) {
    if (isEnabled) {
        [self showNewCheckout];
    } else {
        [self showDefaultCheckout];
    }
}];
```

### getFeature {#get-feature}

`getFeature` returns the evaluated feature payload for the provided context. Use this API when you need more than enabled/disabled and want feature metadata or values.

**Signature**

*Swift*

```swift
Rollout.getFeature(
    featureKey: String,
    evaluationContext: FeatureEvaluationContext,
    completion: @escaping (FeatureEvaluationResult?) -> Void
)
```

*Objective-C*

```objc
[AEPMobileRollout getFeature:(NSString *)featureKey
         evaluationContext:(AEPFeatureEvaluationContext *)evaluationContext
                completion:(void (^)(AEPFeatureEvaluationResult * _Nullable))completion];
```

**Parameters**

| Parameter | Type | Description |
|---|---|---|
| `featureKey` | String | Feature key to evaluate in Experience Rollout |
| `evaluationContext` | FeatureEvaluationContext | Include targeting attributes and optional identity for analytics as needed; use `FeatureEvaluationContext.builder().build()` for an empty context. See [Evaluation context](#evaluation-context). |
| `completion` | `(FeatureEvaluationResult?) -> Void` | Called with the evaluated feature payload; may be `nil` when the feature is not found. |

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

*Swift*

```swift
import AEPRollout

Rollout.getFeature(
    featureKey: "new-checkout-experience",
    evaluationContext: ctx
) { feature in
    if let meta = feature?.meta, !meta.isEmpty {
        applyMetaDrivenExperience(meta)
    } else {
        showFallbackExperience()
    }
}
```

*Objective-C*

```objc
@import AEPRollout;

[AEPMobileRollout getFeature:@"new-checkout-experience"
         evaluationContext:ctx
                completion:^(AEPFeatureEvaluationResult * _Nullable feature) {
    NSString *meta = feature.meta;
    if (meta != nil && meta.length > 0) {
        [self applyMetaDrivenExperience:meta];
    } else {
        [self showFallbackExperience];
    }
}];
```

### refreshCache {#refresh-cache}

By default, the Experience Rollout extension regularly syncs the latest rollout rules and features from the server on a schedule you can configure. If you need an update sooner than the next scheduled sync, call `refreshCache` to force a refresh. Typical cases include after sign-in or when app state changes in a way that should affect targeting.

**Syntax**

*Swift*

```swift
Rollout.refreshCache()
```

*Objective-C*

```objc
[AEPMobileRollout refreshCache];
```

### extensionVersion {#extension-version}

Returns the version string of the Experience Rollout extension.

**Syntax**

```swift
Rollout.extensionVersion(): String
```

**Example**

*Swift*

```swift
let version = Rollout.extensionVersion()
```

*Objective-C*

```objc
NSString *version = [AEPMobileRollout extensionVersion];
```

## API summary {#api-summary}

| API | Returns |
|---|---|
| `isFeatureEnabled(featureKey:evaluationContext:completion:)`. `FeatureEvaluationContext` carries targeting attributes for rules and optional identity for analytics. See [isFeatureEnabled](#is-feature-enabled). | Bool via completion handler |
| `getFeature(featureKey:evaluationContext:completion:)`. Returns the evaluated feature payload for the given context. See [getFeature](#get-feature). | FeatureEvaluationResult? via completion handler |
| `refreshCache()` | Void |
| `extensionVersion()` | String |

## See also {#see-also}

* [Mobile applications](../../integrate/mobile-applications.md)
* [Integration steps](../../integrate/integration-steps.md)
* [SDKs](../../integrate/sdks.md)
* [Android extension integration guide](../android/android-extension-integration-guide.md)

<!-- -->
