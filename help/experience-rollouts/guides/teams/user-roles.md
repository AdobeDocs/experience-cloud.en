---
title: User roles
description: Learn about the five user roles available in Adobe Experience Rollouts and how to choose the right role for each team member.
---

# User roles {#user-roles}

Experience Rollouts provides five roles. Each role is designed for a specific set of responsibilities. Roles are mutually exclusive by default — a member with the Admin role does not automatically have Product Release Owner permissions. Assign multiple roles to a member when broader access is needed.

## Available roles {#roles}

| Role | Responsibilities |
|---|---|
| **Admin** | Onboards applications to the console, manages team members, and approves or rejects access requests. Required before the team can start using feature flags. |
| **Product Release Owner** | Creates and updates feature flags and feature groups for their application. Can link audiences to feature flags to make features available to external users. |
| **Developer** | Works in a sandboxed context to test features behind feature flags without affecting other users. Can expose a feature flag to a private audience (such as a specific user ID or email address) in Stage or Production. |
| **Feature Admin** | Creates and manages cross-team feature groups. Use this role when coordinating flags across applications owned by different teams. |
| **Release Manager** | Manages multi-team, multi-application releases and updates the audience rules that define who receives a release. |

## Choosing the right role {#choosing}

Use the following guidance to assign roles:

* **Adding or updating feature flags for your application** → **Product Release Owner**
* **Testing features privately without affecting others** → **Developer**
* **Managing cross-team feature groups** → **Feature Admin**
* **Managing releases across multiple teams and applications** → **Release Manager**
* **Onboarding applications and managing team membership** → **Admin**

>[!NOTE]
>
>A member can hold more than one role. For example, an engineer who both tests features and manages the team's applications should have both the **Developer** and **Admin** roles.

## Permissions error {#permissions-error}

If a member encounters a "not enough permissions" error when trying to update a feature or group, they need the **Product Release Owner** role. Contact your team admin to have this role added.

## See also {#see-also}

* [Add members to your team](add-team-members.md)
* [Manage teams](manage-teams.md)
