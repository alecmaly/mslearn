# https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-resource-roles-assign-roles

Source: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-resource-roles-assign-roles

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
 

 

 

 

 
 
# Assign Azure resource roles in Privileged Identity Management

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 
## Overview

With Microsoft Entra Privileged Identity Management (PIM), you can manage the built-in Azure resource roles, and custom roles, including (but not limited to):

- Owner

- User Access Administrator

- Contributor

- Security Admin

- Security Manager

Note

Users or members of a group assigned to the Owner or User Access Administrator subscription roles, and Microsoft Entra Global Administrators that enable subscription management in Microsoft Entra ID have Resource administrator permissions by default. These administrators can assign roles, configure role settings, and review access using Privileged Identity Management for Azure resources. A user can't manage Privileged Identity Management for Resources without Resource administrator permissions. View the list of Azure built-in roles.

Privileged Identity Management supports both built-in and custom Azure roles. For more information on Azure custom roles, see Azure custom roles.

Note

Agents and agent identities can receive and activate eligible Azure resource role assignments in preview. Each agent or agent identity requires an E7 license.

## Role assignment conditions

Use Azure attribute-based access control (Azure ABAC) conditions to limit permissions in eligible Azure resource role assignments. Assignees must activate eligible assignments before they can use the permissions. PIM combines fine-grained resource conditions with time-bound assignments, approval workflows, and an audit trail.

Note

When a role is assigned, the assignment:

- Can't be assigned for a duration of less than five minutes

- Can't be removed within five minutes of it being assigned

Currently, the following built-in roles can have conditions added:

- Storage Blob Data Contributor

- Storage Blob Data Owner

- Storage Blob Data Reader

For more information, see What is Azure attribute-based access control (Azure ABAC).

## Assign a role

Follow these steps to assign an Azure resource role to a user, group, agent, or agent identity.

- Sign in to the Microsoft Entra admin center as at least a User Access Administrator.

- Browse to ID Governance > Privileged Identity Management > Azure resources.

- Select the resource type you want to manage. Start at either the Management group dropdown or the Subscriptions dropdown, and then further select Resource groups or Resources as needed. Select Select for the resource you want to manage to open its overview page.

- Under Manage, select Roles to see the list of roles for Azure resources.

- Select Add assignments to open the Add assignments pane.

- Select a Role you want to assign.

- Select the No member selected link to open the Select a member or group pane.

- Select the user, group, agent, or agent identity you want to assign to the role and then choose Select.

- On the Settings tab, in the Assignment type list, select Eligible or Active.

Microsoft Entra PIM for Azure resources provides two distinct assignment types:

- Eligible assignments require the member to activate the role before using it. Depending on the role settings, activation might require multifactor authentication (MFA), a business justification, or approval from designated approvers.

- Active assignments don't require the member to activate the role before usage. Members assigned as active have the privileges assigned ready to use. This type of assignment is also available to customers who don't use Microsoft Entra PIM.

- To specify a specific assignment duration, change the start and end dates and times.

- If the role has been defined with actions that permit assignments to that role with conditions, then you can select Add condition to add a condition based on the principal user and resource attributes that are part of the assignment.

Conditions can be entered in the expression builder.

- When finished, select Assign.

- After the new role assignment is created, a status notification is displayed.

## Convert active role assignments to eligible role assignments (Preview)

Use the 'Assignments (Preview)' blade to change selected active Azure resource role assignments to eligible role assignments.

Enhanced Azure role assignment conversion is in preview. You can convert permanent active and time-bound active Azure resource role assignments to eligible role assignments.

Existing PIM licensing for Azure resources applies unchanged to users and groups. Eligible assignments for agents and agent identities require an E7 license. See PIM licensing requirements.

The existing permissions for managing role assignments apply: you need the Owner or User Access Administrator role at the scope you want to manage.

When the role assignment conversion takes effect, the eligible role assignment replaces the active role assignment. The user must activate the eligible role assignment. The eligible role assignment's Start time and End time define when the user can request activation, not the duration of each role activation. Role activation duration follows the role's activation settings.

- Sign in to the Azure portal.

- Open Privileged Identity Management, select Azure resources, and select the Azure scope you want to manage.

- Select Assignments (Preview), and then select Active Assignments.

- Select the role assignments you want to change, and then select Manage Assignments.

- In Update Assignments, under Target Assignment Type, select Eligible (Recommended).

- Under Assignment duration, select Time-bound, and specify Start time and End time.

- Select Save.

- Review Eligible Assignments to check the role assignment type and duration.

After setup, users can activate their eligible Azure resource role assignments in My Access.

## Assign a role using Azure Resource Manager API

Privileged Identity Management supports Azure Resource Manager (ARM) API commands to manage Azure resource roles, as documented in the PIM Azure Resource Manager API reference. For the permissions required to use the PIM API, see Understand the Privileged Identity Management APIs.

The following example is a sample HTTP request to create an eligible assignment for an Azure role.

### Request

`PUT https://management.azure.com/providers/Microsoft.Subscription/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/providers/Microsoft.Authorization/roleEligibilityScheduleRequests/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e?api-version=2020-10-01-preview
`

### Request body

`{
 "properties": {
 "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
 "roleDefinitionId": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/providers/Microsoft.Authorization/roleDefinitions/c8d4ff99-41c3-41a8-9f60-21dfdad59608",
 "requestType": "AdminAssign",
 "scheduleInfo": {
 "startDateTime": "2022-07-05T21:00:00.91Z",
 "expiration": {
 "type": "AfterDuration",
 "endDateTime": null,
 "duration": "P365D"
 }
 },
 "condition": "@Resource[Microsoft.Storage/storageAccounts/blobServices/containers:ContainerName] StringEqualsIgnoreCase 'foo_storage_container'",
 "conditionVersion": "1.0"
 }
}
`

Note

The `duration` field (value `P365D` in this example) sets the eligible assignment to expire after 365 days. To create permanent eligibility, configure the role management policy at the target scope to allow it.

### Response

Status code: 201

`{
 "properties": {
 "targetRoleEligibilityScheduleId": "b1477448-2cc6-4ceb-93b4-54a202a89413",
 "targetRoleEligibilityScheduleInstanceId": null,
 "scope": "/providers/Microsoft.Subscription/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e",
 "roleDefinitionId": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/providers/Microsoft.Authorization/roleDefinitions/c8d4ff99-41c3-41a8-9f60-21dfdad59608",
 "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
 "principalType": "User",
 "requestType": "AdminAssign",
 "status": "Provisioned",
 "approvalId": null,
 "scheduleInfo": {
 "startDateTime": "2022-07-05T21:00:00.91Z",
 "expiration": {
 "type": "AfterDuration",
 "endDateTime": null,
 "duration": "P365D"
 }
 },
 "ticketInfo": {
 "ticketNumber": null,
 "ticketSystem": null
 },
 "justification": null,
 "requestorId": "a3bb8764-cb92-4276-9d2a-ca1e895e55ea",
 "createdOn": "2022-07-05T21:00:45.91Z",
 "condition": "@Resource[Microsoft.Storage/storageAccounts/blobServices/containers:ContainerName] StringEqualsIgnoreCase 'foo_storage_container'",
 "conditionVersion": "1.0",
 "expandedProperties": {
 "scope": {
 "id": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e",
 "displayName": "Pay-As-You-Go",
 "type": "subscription"
 },
 "roleDefinition": {
 "id": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/providers/Microsoft.Authorization/roleDefinitions/c8d4ff99-41c3-41a8-9f60-21dfdad59608",
 "displayName": "Contributor",
 "type": "BuiltInRole"
 },
 "principal": {
 "id": "a3bb8764-cb92-4276-9d2a-ca1e895e55ea",
 "displayName": "User Account",
 "email": "user@my-tenant.com",
 "type": "User"
 }
 }
 },
 "name": "64caffb6-55c0-4deb-a585-68e948ea1ad6",
 "id": "/providers/Microsoft.Subscription/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/providers/Microsoft.Authorization/RoleEligibilityScheduleRequests64caffb6-55c0-4deb-a585-68e948ea1ad6",
 "type": "Microsoft.Authorization/RoleEligibilityScheduleRequests"
}
`

## Update or remove an existing role assignment

Follow these steps to update or remove an existing role assignment.

- Open Microsoft Entra Privileged Identity Management.

- Select Azure resources.

- Select the resource type you want to manage. Start at either the Management group dropdown or the Subscriptions dropdown, and then further select Resource groups or Resources as needed. Select Select for the resource you want to manage to open its overview page.

- Under Manage, select Roles to list the roles for Azure resources. The following screenshot lists the roles of an Azure Storage account. Select the role that you want to update or remove.

- Find the role assignment on the Eligible roles or Active roles tabs.

- To add or update a condition to refine Azure resource access, select Add or View/Edit in the Condition column for the role assignment.

- Select Add expression or Delete to update the expression. You can also select Add condition to add a new condition to your role.

For information about extending a role assignment, see Extend or renew Azure resource roles in Privileged Identity Management.

## Next steps

- Configure Azure resource role settings in Privileged Identity Management

- Assign Microsoft Entra roles in Privileged Identity Management

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-17
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
