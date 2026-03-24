---
title: Update release audience rules
description: Learn how to configure and update audience criteria for a release in Adobe Experience Rollouts, including supported rule types and how to combine them.
---

# Update release audience rules {#update-release-audience-rules}

## Access the audience settings {#access}

To start configuring who receives your release, navigate to the audience settings in the console:

1. Open your release in the Experience Rollouts console.
2. Go to the **Audience** tab.
3. Enable the toggle next to **Audience Rules**.
4. Select whether to add **inclusion rules** (who should receive the release) or **exclusion rules** (who should not).

## Supported audience criteria {#criteria}

### ID type {#id-type}
Target users based on their account type (for example, personal or enterprise accounts).

### Country {#country}
Target users based on their registered country.

### User ID {#user-id}
Target specific users by their unique user identifier (GUID).

### Email address {#email}
Target users by their exact email address. To add multiple email addresses at once, select **in** from the operator drop-down (instead of **is**), then:
* Enter a comma-separated list of addresses in the text box, or
* Upload a `.txt` file with one address per line, or
* Upload a `.csv` file with the list of addresses

If your list is very large, split it into smaller batches.

### Email domain {#email-domain}
Target all users whose email address belongs to a specific domain (for example, `yourcompany.com`).

### Client IP {#client-ip}
Target users based on their client IP address.

### Percentage {#percentage}
Target a random percentage of all users, including unauthenticated users.

### Percentage (authenticated only) {#percentage-auth}
Target a random percentage of authenticated users only. Unauthenticated users are excluded.

## Combining multiple rules {#combining-rules}

You can combine multiple audience criteria using AND/OR logic.

**Examples:**

* To target only enterprise accounts from a specific domain, combine the **ID type** rule with the **Email domain** rule using AND.
* To target 10% of users from a specific country, combine the **Country** rule with the **Percentage** rule.

Use the **+/-** icons to add or remove conditions. To duplicate a condition, select the duplicate icon next to an existing rule. For complex nested logic, enable **Nested Logic** and enter a valid expression in the text box.

## See also {#see-also}

* [Request a release](request-a-release.md)
* [Release workflow end-to-end](release-workflow-end-to-end.md)
* [Release states](release-states.md)
