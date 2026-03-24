---
title: SDK benchmarking
description: Review Java SDK benchmarking results for Adobe Experience Rollouts, including response time measurements across varying numbers of feature flags under typical load conditions.
---

# SDK benchmarking {#sdk-benchmarking}

The Experience Rollouts Java SDK is benchmarked to give integrating teams a reliable estimate of the resources and response times to expect when the SDK runs inside their infrastructure.

## Test environment {#test-environment}

Benchmarking was performed on a Spring Boot application with the following fixed configuration:

* **CPU cores:** 8
* **JVM memory:** 4096 MB

## Test assumptions {#test-assumptions}

The following conditions were held constant across all benchmark runs:

* Feature flags tested: 8 to 128
* Context variables per feature flag: 2 (type `STRING`, length 36 characters)
* Average load: 15,000 requests per minute (RPM)
* Active threads: 100

## Results {#results}

The table below shows the 99.99th percentile response time for `getFeatures()` calls as the number of feature flags increases:

| Number of feature flags | Context variables per flag | Response time (ms, p99.99) |
|---|---|---|
| 8 | 2 | < 0.5 |
| 16 | 2 | < 0.5 |
| 32 | 2 | < 0.5 |
| 64 | 2 | < 1 |
| 128 | 2 | < 1 |

## Interpreting the results {#interpretation}

The benchmarks above represent performance under the specific test conditions described. Because the SDK runs inside your application's infrastructure, actual response times will vary based on factors specific to your environment:

* Available CPU and number of cores
* JVM heap size and garbage collection behavior
* Thread availability and context switching
* Current system load at time of request

Use these figures as a planning baseline rather than as guaranteed performance targets for your production environment.

## See also {#see-also}

* [Java SDK integration guide](java/java-sdk-integration-guide.md)
* [Java SDK release notes](java/java-sdk-release-notes.md)
* [SDKs](../integrate/sdks.md)
