---
title: Log in to the Experience Rollouts console
description: Learn how to get started with Adobe Experience Rollouts by finding your team, requesting access, and logging in to the console.
---

# Log in to the Experience Rollouts console {#log-in}

Getting started with Experience Rollouts involves three steps: finding or creating your team, requesting access, and logging in to the console.

## Before you begin {#before-you-begin}

Experience Rollouts is organized around **teams**. Each team owns one or more applications and manages feature flags for those applications. Before you can log in, you need to belong to a team.

Check with your product or engineering lead to find out whether a team already exists for your project. If it does, ask the team admin to add you with the correct [user role](../teams/user-roles.md). If no team exists yet, follow the steps in [Create a new team](create-a-new-team.md).

## Request access {#request-access}

Once you know which team to join, request access through your organization's access management system. See [Request access](request-access.md) for step-by-step instructions.

After your request is approved, you will receive the permissions associated with the role granted by your team admin.

## Log in to the console {#log-in-steps}

After access is granted:

1. Go to [https://experience.adobe.com/](https://experience.adobe.com/) and sign in with your organization credentials.
2. Select **Experience Rollouts** from the application switcher.
3. Select the appropriate environment — **Stage** for testing, **Production** for live rollouts. See [Environments overview](environments-overview.md) for details.

## First steps after logging in {#first-steps}

After logging in, verify that your application is listed in the console. Applications are managed by team admins. If your application is not listed, contact your team admin to have it added. See [Manage applications](../applications/manage-applications.md) for more information.

## Key terminology {#terminology}

| Term | Definition |
|---|---|
| **Team** | A self-managed group that owns applications and manages feature flags. Teams have a flat structure with different user roles and permission levels. |
| **Application** | The application you want to control with feature flags. Each application is owned by a team. |
| **Feature flag / Feature group / Release** | The artifacts created in Experience Rollouts for feature testing and release management. |
