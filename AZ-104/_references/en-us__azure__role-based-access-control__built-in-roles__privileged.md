# https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles/privileged

Source: https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles/privileged

---

id="main"
 role="main"
 class="layout-body-main "
 data-bi-name="content"
 lang="en-us"
 dir="ltr"
 >
 
 
 
 
 
 Table of contents 
 
 
 
 Exit editor mode
 
 

 
 
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 

 

 
 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 
 
 
 
 
 
 
 
 Reading mode
 
 
 
 
 Table of contents
 
 
 
 
 
 
 Read in English
 
 
 
 
 
 
 
 Add
 
 
 
 
 
 
 Add to Plans
 
 
 
 
 
 
 
 Edit
 
 
 
 
 
 
 
 
 
 
 Copy Markdown
 
 
 
 
 
 
 Print
 
 
 
 

 
 

 
 

 

 
 
 
 
 
 
 
 
 Note
 

 
 Access to this page requires authorization. You can try signing in or changing directories.
 

 
 Access to this page requires authorization. You can try changing directories.
 

 

 

 

 
 
# Azure built-in roles for Privileged

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This article lists the Azure built-in roles in the Privileged category.

## Contributor

Grants full access to manage all resources, but does not allow you to assign roles in Azure RBAC, manage assignments in Azure Blueprints, or share image galleries.

Learn more

Actions
Description

*
Create and manage resources of all types

NotActions

Microsoft.Authorization/*/Delete
Delete roles, policy assignments, policy definitions and policy set definitions

Microsoft.Authorization/*/Write
Create roles, role assignments, policy assignments, policy definitions and policy set definitions

Microsoft.Authorization/elevateAccess/Action
Grants the caller User Access Administrator access at the tenant scope

Microsoft.Blueprint/blueprintAssignments/write
Create or update any blueprint assignments

Microsoft.Blueprint/blueprintAssignments/delete
Delete any blueprint assignments

Microsoft.Compute/galleries/share/action
Shares a Gallery to different scopes

Microsoft.Purview/consents/write
Create or Update a Consent Resource.

Microsoft.Purview/consents/delete
Delete the Consent Resource.

Microsoft.Resources/deploymentStacks/manageDenySetting/action
Manage the denySettings property of a deployment stack.

Microsoft.Subscription/cancel/action
Cancels the Subscription

Microsoft.Subscription/enable/action
Reactivates the Subscription

DataActions

none

NotDataActions

none

`{
 "assignableScopes": [
 "/"
 ],
 "description": "Grants full access to manage all resources, but does not allow you to assign roles in Azure RBAC, manage assignments in Azure Blueprints, or share image galleries.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
 "name": "b24988ac-6180-42a0-ab88-20f7382dd24c",
 "permissions": [
 {
 "actions": [
 "*"
 ],
 "notActions": [
 "Microsoft.Authorization/*/Delete",
 "Microsoft.Authorization/*/Write",
 "Microsoft.Authorization/elevateAccess/Action",
 "Microsoft.Blueprint/blueprintAssignments/write",
 "Microsoft.Blueprint/blueprintAssignments/delete",
 "Microsoft.Compute/galleries/share/action",
 "Microsoft.Purview/consents/write",
 "Microsoft.Purview/consents/delete",
 "Microsoft.Resources/deploymentStacks/manageDenySetting/action",
 "Microsoft.Subscription/cancel/action",
 "Microsoft.Subscription/enable/action"
 ],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Contributor",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Owner

Grants full access to manage all resources, including the ability to assign roles in Azure RBAC.

Learn more

Actions
Description

*
Create and manage resources of all types

NotActions

none

DataActions

none

NotDataActions

none

`{
 "assignableScopes": [
 "/"
 ],
 "description": "Grants full access to manage all resources, including the ability to assign roles in Azure RBAC.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
 "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
 "permissions": [
 {
 "actions": [
 "*"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Owner",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Reservations Administrator

Lets one read and manage all the reservations in a tenant

Learn more

Actions
Description

Microsoft.Capacity/*/read

Microsoft.Capacity/*/action

Microsoft.Capacity/*/write

Microsoft.Authorization/roleAssignments/read
Get information about a role assignment.

Microsoft.Authorization/roleDefinitions/read
Get information about a role definition.

Microsoft.Authorization/roleAssignments/write
Create a role assignment at the specified scope.

Microsoft.Authorization/roleAssignments/delete
Delete a role assignment at the specified scope.

NotActions

none

DataActions

none

NotDataActions

none

`{
 "assignableScopes": [
 "/providers/Microsoft.Capacity"
 ],
 "description": "Lets one read and manage all the reservations in a tenant",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/a8889054-8d42-49c9-bc1c-52486c10e7cd",
 "name": "a8889054-8d42-49c9-bc1c-52486c10e7cd",
 "permissions": [
 {
 "actions": [
 "Microsoft.Capacity/*/read",
 "Microsoft.Capacity/*/action",
 "Microsoft.Capacity/*/write",
 "Microsoft.Authorization/roleAssignments/read",
 "Microsoft.Authorization/roleDefinitions/read",
 "Microsoft.Authorization/roleAssignments/write",
 "Microsoft.Authorization/roleAssignments/delete"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Reservations Administrator",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Role Based Access Control Administrator

Manage access to Azure resources by assigning roles using Azure RBAC. This role does not allow you to manage access using other ways, such as Azure Policy.

Note

This role includes the `*/read` action for the control plane. Users that are assigned this role can read control plane information for all Azure resources.

Actions
Description

Microsoft.Authorization/roleAssignments/write
Create a role assignment at the specified scope.

Microsoft.Authorization/roleAssignments/delete
Delete a role assignment at the specified scope.

*/read
Read control plane information for all Azure resources.

Microsoft.Support/*
Create and update a support ticket

NotActions

none

DataActions

none

NotDataActions

none

`{
 "assignableScopes": [
 "/"
 ],
 "description": "Manage access to Azure resources by assigning roles using Azure RBAC. This role does not allow you to manage access using other ways, such as Azure Policy.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/f58310d9-a9f6-439a-9e8d-f62e7b41a168",
 "name": "f58310d9-a9f6-439a-9e8d-f62e7b41a168",
 "permissions": [
 {
 "actions": [
 "Microsoft.Authorization/roleAssignments/write",
 "Microsoft.Authorization/roleAssignments/delete",
 "*/read",
 "Microsoft.Support/*"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Role Based Access Control Administrator",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## User Access Administrator

Lets you manage user access to Azure resources.

Note

This role includes the `*/read` action for the control plane. Users that are assigned this role can read control plane information for all Azure resources.

Learn more

Actions
Description

*/read
Read control plane information for all Azure resources.

Microsoft.Authorization/*
Manage authorization

Microsoft.Support/*
Create and update a support ticket

NotActions

none

DataActions

none

NotDataActions

none

`{
 "assignableScopes": [
 "/"
 ],
 "description": "Lets you manage user access to Azure resources.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
 "name": "18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
 "permissions": [
 {
 "actions": [
 "*/read",
 "Microsoft.Authorization/*",
 "Microsoft.Support/*"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "User Access Administrator",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Next steps

- Assign Azure roles using the Azure portal

 
 

 
 

 

 
 
 
 
 
 
## Feedback

 
 
 Was this page helpful?
 

 
 
 
 
 
 Yes
 
 
 
 
 
 No
 
 
 
 
 
 
 No
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix? 
 
 

 
 

 
 

 

 

 
 
 

 
 
 
 
## 
 Additional resources
 

 
 

 
 

 
 

 
 

 
 
 
 
 
- 
 
 Last updated on 
 2026-07-01
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
