---
title: Team management FAQ
description: Find answers to common questions about managing teams, members, and roles in Adobe Experience Rollouts.
exl-id: 8234f682-526c-47ca-b35b-2a615a95eced
---
# Team management FAQ {#team-management-faq}

## I am trying to add a user, but the search does not return any results {#user-not-found}

This can occur in the Stage environment if the user has never signed in to Stage before. To resolve this, ask the user to sign in to the Stage console at least once to create their account in the Stage identity system. After they have signed in, try searching for them again.

## I am an Admin but I cannot create or edit feature flags {#admin-cannot-edit-flags}

Roles in Experience Rollouts are mutually exclusive. The **Admin** role grants team management permissions but does not include the permissions of a **Product Release Owner**. To create and edit feature flags, a member needs the **Product Release Owner** role in addition to the **Admin** role.

Contact your team admin to have additional roles assigned. See [User roles](user-roles.md) for a full breakdown of what each role can do.

## Do admins have a hierarchy? Can one admin override another? {#admin-hierarchy}

No. Teams in Experience Rollouts have a flat structure. All members with the **Admin** role have equal permissions and can manage each other's configurations. There is no hierarchical approval workflow between admins.

## How do I remove a member from my team? {#remove-member}

Members are removed through the access management system. As an Admin, search for the member's access record for your team and revoke their role. If you are unsure how to do this, contact your organization's access management team.

## Can a member have more than one role? {#multiple-roles}

Yes. Assign multiple roles to a member when their responsibilities span more than one function. For example, a team member who both manages the team and creates feature flags should have both the **Admin** and **Product Release Owner** roles.

## See also {#see-also}

* [User roles](user-roles.md)
* [Add members to your team](add-team-members.md)
* [Manage teams](manage-teams.md)
