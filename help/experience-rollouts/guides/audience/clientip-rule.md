---
title: Audience rule with client IP context variable
description: Learn how to use the client IP context variable in audience rules in Adobe Experience Rollouts, including support for IP addresses, CIDR blocks, and network ranges.
exl-id: 0c313d5a-e68a-4479-83f3-866adfc237e0
---
# Audience rule with client IP context variable {#clientip-rule}

The `clientip` context variable lets you target users based on their client IP address. This is useful for restricting or enabling features based on the network from which users are accessing your application — for example, limiting early access to users on a corporate network.

## Supported input types {#input-types}

The `clientip` context variable supports three types of input values:

| Input type | Description | Supported operators |
|---|---|---|
| **IP address** | A single IPv4 or IPv6 address | Is, Is not equal to, In |
| **CIDR block** | A range of IP addresses in CIDR notation (for example, `192.168.1.0/24`) | Is, In, Is not equal to |
| **Network range** | A pre-defined named network range maintained by the platform | Is part of |

## Adding a client IP rule {#adding-rule}

1. Open the feature flag, feature group, or cross-team feature group in the console.
2. Go to the **Audience** tab.
3. Under **Context**, add a condition using the **clientip** variable.
4. Select the operator and enter the value (IP address, CIDR block, or select a pre-defined network range).

## See also {#see-also}

* [Use context in audience rules](using-context-in-audience-rules.md)
* [Audience in feature flags and feature groups](audience-in-feature-flags-and-feature-groups.md)
* [Complex audience rules](complex-rules.md)
