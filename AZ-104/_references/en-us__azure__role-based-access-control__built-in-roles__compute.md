# https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles/compute

Source: https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles/compute

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
 

 

 

 

 
 
# Azure built-in roles for Compute

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This article lists the Azure built-in roles in the Compute category.

## Azure Arc VMware VM Contributor

Arc VMware VM Contributor has permissions to perform all VM actions.

Learn more

Actions
Description

Microsoft.ConnectedVMwarevSphere/virtualmachines/*

Microsoft.ConnectedVMwarevSphere/virtualmachineinstances/*

Microsoft.Insights/AlertRules/Write
Create or update a classic metric alert

Microsoft.Insights/AlertRules/Delete
Delete a classic metric alert

Microsoft.Insights/AlertRules/Read
Read a classic metric alert

Microsoft.Insights/AlertRules/Activated/Action
Classic metric alert activated

Microsoft.Insights/AlertRules/Resolved/Action
Classic metric alert resolved

Microsoft.Insights/AlertRules/Throttled/Action
Classic metric alert rule throttled

Microsoft.Insights/AlertRules/Incidents/Read
Read a classic metric alert incident

Microsoft.Resources/deployments/read
Gets or lists deployments.

Microsoft.Resources/deployments/write
Creates or updates an deployment.

Microsoft.Resources/deployments/delete
Deletes a deployment.

Microsoft.Resources/deployments/cancel/action
Cancels a deployment.

Microsoft.Resources/deployments/validate/action
Validates a deployment.

Microsoft.Resources/deployments/whatIf/action
Predicts template deployment changes.

Microsoft.Resources/deployments/exportTemplate/action
Export template for a deployment

Microsoft.Resources/deployments/operations/read
Gets or lists deployment operations.

Microsoft.Resources/deployments/operationstatuses/read
Gets or lists deployment operation statuses.

Microsoft.Resources/subscriptions/resourcegroups/deployments/read
Gets or lists deployments.

Microsoft.Resources/subscriptions/resourcegroups/deployments/write
Creates or updates an deployment.

Microsoft.Resources/subscriptions/resourcegroups/deployments/operations/read
Gets or lists deployment operations.

Microsoft.Resources/subscriptions/resourcegroups/deployments/operationstatuses/read
Gets or lists deployment operation statuses.

Microsoft.ResourceHealth/availabilityStatuses/read
Gets the availability statuses for all resources in the specified scope

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Resources/subscriptions/read
Gets the list of subscriptions.

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.Resources/subscriptions/operationresults/read
Get the subscription operation results.

Microsoft.HybridCompute/machines/read
Read any Azure Arc machines

Microsoft.HybridCompute/machines/write
Writes an Azure Arc machines

Microsoft.HybridCompute/machines/delete
Deletes an Azure Arc machines

Microsoft.HybridCompute/machines/UpgradeExtensions/action
Upgrades Extensions on Azure Arc machines

Microsoft.HybridCompute/machines/assessPatches/action
Assesses any Azure Arc machines to get missing software patches

Microsoft.HybridCompute/machines/installPatches/action
Installs patches on any Azure Arc machines

Microsoft.HybridCompute/machines/extensions/read
Reads any Azure Arc extensions

Microsoft.HybridCompute/machines/extensions/write
Installs or Updates an Azure Arc extensions

Microsoft.HybridCompute/machines/extensions/delete
Deletes an Azure Arc extensions

Microsoft.HybridCompute/operations/read
Read all Operations for Azure Arc for Servers

Microsoft.HybridCompute/locations/operationresults/read
Reads the status of an operation on Microsoft.HybridCompute Resource Provider

Microsoft.HybridCompute/locations/operationstatus/read
Reads the status of an operation on Microsoft.HybridCompute Resource Provider

Microsoft.HybridCompute/machines/patchAssessmentResults/read
Reads any Azure Arc patchAssessmentResults

Microsoft.HybridCompute/machines/patchAssessmentResults/softwarePatches/read
Reads any Azure Arc patchAssessmentResults/softwarePatches

Microsoft.HybridCompute/machines/patchInstallationResults/read
Reads any Azure Arc patchInstallationResults

Microsoft.HybridCompute/machines/patchInstallationResults/softwarePatches/read
Reads any Azure Arc patchInstallationResults/softwarePatches

Microsoft.HybridCompute/locations/updateCenterOperationResults/read
Reads the status of an update center operation on machines

Microsoft.HybridCompute/machines/hybridIdentityMetadata/read
Read any Azure Arc machines's Hybrid Identity Metadata

Microsoft.HybridCompute/osType/agentVersions/read
Read all Azure Connected Machine Agent versions available

Microsoft.HybridCompute/osType/agentVersions/latest/read
Read the latest Azure Connected Machine Agent version

Microsoft.HybridCompute/machines/runcommands/read
Reads any Azure Arc runcommands

Microsoft.HybridCompute/machines/runcommands/write
Installs or Updates an Azure Arc runcommands

Microsoft.HybridCompute/machines/runcommands/delete
Deletes an Azure Arc runcommands

Microsoft.HybridCompute/machines/licenseProfiles/read
Reads any Azure Arc licenseProfiles

Microsoft.HybridCompute/machines/licenseProfiles/write
Installs or Updates an Azure Arc licenseProfiles

Microsoft.HybridCompute/machines/licenseProfiles/delete
Deletes an Azure Arc licenseProfiles

Microsoft.HybridCompute/licenses/read
Reads any Azure Arc licenses

Microsoft.HybridCompute/licenses/write
Installs or Updates an Azure Arc licenses

Microsoft.HybridCompute/licenses/delete
Deletes an Azure Arc licenses

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
 "description": "Arc VMware VM Contributor has permissions to perform all VM actions.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/b748a06d-6150-4f8a-aaa9-ce3940cd96cb",
 "name": "b748a06d-6150-4f8a-aaa9-ce3940cd96cb",
 "permissions": [
 {
 "actions": [
 "Microsoft.ConnectedVMwarevSphere/virtualmachines/*",
 "Microsoft.ConnectedVMwarevSphere/virtualmachineinstances/*",
 "Microsoft.Insights/AlertRules/Write",
 "Microsoft.Insights/AlertRules/Delete",
 "Microsoft.Insights/AlertRules/Read",
 "Microsoft.Insights/AlertRules/Activated/Action",
 "Microsoft.Insights/AlertRules/Resolved/Action",
 "Microsoft.Insights/AlertRules/Throttled/Action",
 "Microsoft.Insights/AlertRules/Incidents/Read",
 "Microsoft.Resources/deployments/read",
 "Microsoft.Resources/deployments/write",
 "Microsoft.Resources/deployments/delete",
 "Microsoft.Resources/deployments/cancel/action",
 "Microsoft.Resources/deployments/validate/action",
 "Microsoft.Resources/deployments/whatIf/action",
 "Microsoft.Resources/deployments/exportTemplate/action",
 "Microsoft.Resources/deployments/operations/read",
 "Microsoft.Resources/deployments/operationstatuses/read",
 "Microsoft.Resources/subscriptions/resourcegroups/deployments/read",
 "Microsoft.Resources/subscriptions/resourcegroups/deployments/write",
 "Microsoft.Resources/subscriptions/resourcegroups/deployments/operations/read",
 "Microsoft.Resources/subscriptions/resourcegroups/deployments/operationstatuses/read",
 "Microsoft.ResourceHealth/availabilityStatuses/read",
 "Microsoft.Authorization/*/read",
 "Microsoft.Resources/subscriptions/read",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.Resources/subscriptions/operationresults/read",
 "Microsoft.HybridCompute/machines/read",
 "Microsoft.HybridCompute/machines/write",
 "Microsoft.HybridCompute/machines/delete",
 "Microsoft.HybridCompute/machines/UpgradeExtensions/action",
 "Microsoft.HybridCompute/machines/assessPatches/action",
 "Microsoft.HybridCompute/machines/installPatches/action",
 "Microsoft.HybridCompute/machines/extensions/read",
 "Microsoft.HybridCompute/machines/extensions/write",
 "Microsoft.HybridCompute/machines/extensions/delete",
 "Microsoft.HybridCompute/operations/read",
 "Microsoft.HybridCompute/locations/operationresults/read",
 "Microsoft.HybridCompute/locations/operationstatus/read",
 "Microsoft.HybridCompute/machines/patchAssessmentResults/read",
 "Microsoft.HybridCompute/machines/patchAssessmentResults/softwarePatches/read",
 "Microsoft.HybridCompute/machines/patchInstallationResults/read",
 "Microsoft.HybridCompute/machines/patchInstallationResults/softwarePatches/read",
 "Microsoft.HybridCompute/locations/updateCenterOperationResults/read",
 "Microsoft.HybridCompute/machines/hybridIdentityMetadata/read",
 "Microsoft.HybridCompute/osType/agentVersions/read",
 "Microsoft.HybridCompute/osType/agentVersions/latest/read",
 "Microsoft.HybridCompute/machines/runcommands/read",
 "Microsoft.HybridCompute/machines/runcommands/write",
 "Microsoft.HybridCompute/machines/runcommands/delete",
 "Microsoft.HybridCompute/machines/licenseProfiles/read",
 "Microsoft.HybridCompute/machines/licenseProfiles/write",
 "Microsoft.HybridCompute/machines/licenseProfiles/delete",
 "Microsoft.HybridCompute/licenses/read",
 "Microsoft.HybridCompute/licenses/write",
 "Microsoft.HybridCompute/licenses/delete"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Azure Arc VMware VM Contributor",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Azure Batch Account Contributor

Grants full access to manage all Batch resources, including Batch accounts, pools and jobs.

Learn more

Actions
Description

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Batch/*
Manage all Batch resources.

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

NotActions

none

DataActions

Microsoft.Batch/*
Manage all Batch resources.

NotDataActions

none

`{
 "assignableScopes": [
 "/"
 ],
 "description": "Grants full access to manage all Batch resources, including Batch accounts, pools and jobs.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/29fe4964-1e60-436b-bd3a-77fd4c178b3c",
 "name": "29fe4964-1e60-436b-bd3a-77fd4c178b3c",
 "permissions": [
 {
 "actions": [
 "Microsoft.Authorization/*/read",
 "Microsoft.Batch/*",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read"
 ],
 "notActions": [],
 "dataActions": [
 "Microsoft.Batch/*"
 ],
 "notDataActions": []
 }
 ],
 "roleName": "Azure Batch Account Contributor",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Azure Batch Account Reader

Lets you view all resources including pools and jobs in the Batch account.

Learn more

Actions
Description

Microsoft.Batch/*/read
View all resources in Batch account.

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

NotActions

none

DataActions

Microsoft.Batch/*/read
View all resources in Batch account.

NotDataActions

none

`{
 "assignableScopes": [
 "/"
 ],
 "description": "Lets you view all resources including pools and jobs in the Batch account.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/11076f67-66f6-4be0-8f6b-f0609fd05cc9",
 "name": "11076f67-66f6-4be0-8f6b-f0609fd05cc9",
 "permissions": [
 {
 "actions": [
 "Microsoft.Batch/*/read",
 "Microsoft.Resources/subscriptions/resourceGroups/read"
 ],
 "notActions": [],
 "dataActions": [
 "Microsoft.Batch/*/read"
 ],
 "notDataActions": []
 }
 ],
 "roleName": "Azure Batch Account Reader",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Azure Batch Data Contributor

Grants permissions to manage Batch pools and jobs but not to modify accounts.

Learn more

Actions
Description

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Batch/batchAccounts/read
Lists Batch accounts or gets the properties of a Batch account

Microsoft.Batch/batchAccounts/applications/*
Create and manage applications and application packages on a Batch account.

Microsoft.Batch/batchAccounts/certificates/*
Create and manage certificates on a Batch account. (Warning: Certificate feature was retired)

Microsoft.Batch/batchAccounts/certificateOperationResults/*
Gets the results of a long running certificate operation on a Batch account. (Warning: Certificate feature was retired)

Microsoft.Batch/batchAccounts/pools/*
Create and manage pools on a Batch account.

Microsoft.Batch/batchAccounts/poolOperationResults/*
Gets the results of a long running pool operation on a Batch account.

Microsoft.Batch/locations/*/read
Get Batch account operation result/Batch quota/supported VM size at the given location.

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

NotActions

none

DataActions

Microsoft.Batch/batchAccounts/jobSchedules/*
Create and manage job schedules on a Batch account.

Microsoft.Batch/batchAccounts/jobs/*
Create and manage jobs on a Batch account.

NotDataActions

none

`{
 "assignableScopes": [
 "/"
 ],
 "description": "Grants permissions to manage Batch pools and jobs but not to modify accounts.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/6aaa78f1-f7de-44ca-8722-c64a23943cae",
 "name": "6aaa78f1-f7de-44ca-8722-c64a23943cae",
 "permissions": [
 {
 "actions": [
 "Microsoft.Authorization/*/read",
 "Microsoft.Batch/batchAccounts/read",
 "Microsoft.Batch/batchAccounts/applications/*",
 "Microsoft.Batch/batchAccounts/certificates/*",
 "Microsoft.Batch/batchAccounts/certificateOperationResults/*",
 "Microsoft.Batch/batchAccounts/pools/*",
 "Microsoft.Batch/batchAccounts/poolOperationResults/*",
 "Microsoft.Batch/locations/*/read",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read"
 ],
 "notActions": [],
 "dataActions": [
 "Microsoft.Batch/batchAccounts/jobSchedules/*",
 "Microsoft.Batch/batchAccounts/jobs/*"
 ],
 "notDataActions": []
 }
 ],
 "roleName": "Azure Batch Data Contributor",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Azure Batch Job Submitter

Lets you submit and manage jobs in the Batch account.

Learn more

Actions
Description

Microsoft.Batch/batchAccounts/applications/read
Lists applications or gets the properties of an application

Microsoft.Batch/batchAccounts/applications/versions/read
Gets the properties of an application package

Microsoft.Batch/batchAccounts/pools/read
Lists pools on a Batch account or gets the properties of a pool

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

NotActions

none

DataActions

Microsoft.Batch/batchAccounts/jobSchedules/*
Create and manage job schedules on a Batch account.

Microsoft.Batch/batchAccounts/jobs/*
Create and manage jobs on a Batch account.

NotDataActions

none

`{
 "assignableScopes": [
 "/"
 ],
 "description": "Lets you submit and manage jobs in the Batch account.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/48e5e92e-a480-4e71-aa9c-2778f4c13781",
 "name": "48e5e92e-a480-4e71-aa9c-2778f4c13781",
 "permissions": [
 {
 "actions": [
 "Microsoft.Batch/batchAccounts/applications/read",
 "Microsoft.Batch/batchAccounts/applications/versions/read",
 "Microsoft.Batch/batchAccounts/pools/read",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read"
 ],
 "notActions": [],
 "dataActions": [
 "Microsoft.Batch/batchAccounts/jobSchedules/*",
 "Microsoft.Batch/batchAccounts/jobs/*"
 ],
 "notDataActions": []
 }
 ],
 "roleName": "Azure Batch Job Submitter",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Classic Virtual Machine Contributor

Lets you manage classic virtual machines, but not access to them, and not the virtual network or storage account they're connected to.

Actions
Description

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.ClassicCompute/domainNames/*
Create and manage classic compute domain names

Microsoft.ClassicCompute/virtualMachines/*
Create and manage virtual machines

Microsoft.ClassicNetwork/networkSecurityGroups/join/action

Microsoft.ClassicNetwork/reservedIps/link/action

Microsoft.ClassicNetwork/reservedIps/read

Microsoft.ClassicNetwork/virtualNetworks/join/action

Microsoft.ClassicNetwork/virtualNetworks/read

Microsoft.ClassicStorage/storageAccounts/disks/read

Microsoft.ClassicStorage/storageAccounts/images/read

Microsoft.ClassicStorage/storageAccounts/listKeys/action

Microsoft.ClassicStorage/storageAccounts/read

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

Microsoft.ResourceHealth/availabilityStatuses/read
Gets the availability statuses for all resources in the specified scope

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

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
 "description": "Lets you manage classic virtual machines, but not access to them, and not the virtual network or storage account they're connected to.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/d73bb868-a0df-4d4d-bd69-98a00b01fccb",
 "name": "d73bb868-a0df-4d4d-bd69-98a00b01fccb",
 "permissions": [
 {
 "actions": [
 "Microsoft.Authorization/*/read",
 "Microsoft.ClassicCompute/domainNames/*",
 "Microsoft.ClassicCompute/virtualMachines/*",
 "Microsoft.ClassicNetwork/networkSecurityGroups/join/action",
 "Microsoft.ClassicNetwork/reservedIps/link/action",
 "Microsoft.ClassicNetwork/reservedIps/read",
 "Microsoft.ClassicNetwork/virtualNetworks/join/action",
 "Microsoft.ClassicNetwork/virtualNetworks/read",
 "Microsoft.ClassicStorage/storageAccounts/disks/read",
 "Microsoft.ClassicStorage/storageAccounts/images/read",
 "Microsoft.ClassicStorage/storageAccounts/listKeys/action",
 "Microsoft.ClassicStorage/storageAccounts/read",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.ResourceHealth/availabilityStatuses/read",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.Support/*"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Classic Virtual Machine Contributor",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Compute Fleet Contributor

Allows users to manage Compute Fleet resources.

Actions
Description

Microsoft.AzureFleet/fleets/*
Create and manage compute fleets

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

Microsoft.ResourceHealth/availabilityStatuses/read
Gets the availability statuses for all resources in the specified scope

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

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
 "description": "Allows users to manage Compute Fleet resources.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/2bed379c-9fba-455b-99e4-6b911073bcf2",
 "name": "2bed379c-9fba-455b-99e4-6b911073bcf2",
 "permissions": [
 {
 "actions": [
 "Microsoft.AzureFleet/fleets/*",
 "Microsoft.Authorization/*/read",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.ResourceHealth/availabilityStatuses/read",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Compute Fleet Contributor",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Compute Gallery Artifacts Publisher

This is the role for publishing gallery artifacts.

Actions
Description

Microsoft.Compute/galleries/*

Microsoft.Compute/locations/capsOperations/read
Gets the status of an asynchronous Caps operation

Microsoft.Compute/locations/communityGalleries/*

Microsoft.Compute/locations/sharedGalleries/*

Microsoft.Compute/images/*

Microsoft.Compute/virtualMachines/write
Creates a new virtual machine or updates an existing virtual machine

Microsoft.Compute/disks/write
Creates a new Disk or updates an existing one

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

NotActions

Microsoft.Compute/galleries/share/action
Shares a Gallery to different scopes

DataActions

none

NotDataActions

none

`{
 "assignableScopes": [
 "/"
 ],
 "description": "This is the role for publishing gallery artifacts.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/85a2d0d9-2eba-4c9c-b355-11c2cc0788ab",
 "name": "85a2d0d9-2eba-4c9c-b355-11c2cc0788ab",
 "permissions": [
 {
 "actions": [
 "Microsoft.Compute/galleries/*",
 "Microsoft.Compute/locations/capsOperations/read",
 "Microsoft.Compute/locations/communityGalleries/*",
 "Microsoft.Compute/locations/sharedGalleries/*",
 "Microsoft.Compute/images/*",
 "Microsoft.Compute/virtualMachines/write",
 "Microsoft.Compute/disks/write",
 "Microsoft.Authorization/*/read",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read"
 ],
 "notActions": [
 "Microsoft.Compute/galleries/share/action"
 ],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Compute Gallery Artifacts Publisher",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Compute Gallery Image Reader

This is the role for reading gallery images.

Learn more

Actions
Description

Microsoft.Compute/galleries/images/read
Gets the properties of Gallery Image

Microsoft.Compute/galleries/images/versions/read
Gets the properties of Gallery Image Version

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
 "description": "This is the role for reading gallery images.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/cf7c76d2-98a3-4358-a134-615aa78bf44d",
 "name": "cf7c76d2-98a3-4358-a134-615aa78bf44d",
 "permissions": [
 {
 "actions": [
 "Microsoft.Compute/galleries/images/read",
 "Microsoft.Compute/galleries/images/versions/read"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Compute Gallery Image Reader",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Compute Gallery Sharing Admin

This role allows user to share gallery to another subscription/tenant or share it to the public.

Learn more

Actions
Description

Microsoft.Compute/galleries/share/action
Shares a Gallery to different scopes

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
 "description": "This role allows user to share gallery to another subscription/tenant or share it to the public.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/1ef6a3be-d0ac-425d-8c01-acb62866290b",
 "name": "1ef6a3be-d0ac-425d-8c01-acb62866290b",
 "permissions": [
 {
 "actions": [
 "Microsoft.Compute/galleries/share/action"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Compute Gallery Sharing Admin",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Compute Limit Operator

Read and manage compute limits using compute limit operations.

Actions
Description

Microsoft.ComputeLimit/locations/guestSubscriptions/read
Reads guest subscriptions for a given host subscription within a location.

Microsoft.ComputeLimit/locations/guestSubscriptions/write
Adds a subscription as a guest to consume a host subscription's shared compute limits.

Microsoft.ComputeLimit/locations/guestSubscriptions/delete
Removes a subscription as a guest preventing it from consuming the host subscription's shared compute limits.

Microsoft.ComputeLimit/locations/sharedLimits/read
Lists all compute shared limits a host subscription shares with its guest subscriptions.

Microsoft.ComputeLimit/locations/sharedLimits/write
Enables sharing of a compute limit by a host subscription with its guest subscriptions.

Microsoft.ComputeLimit/locations/sharedLimits/delete
Disables sharing of a compute limit by a host subscription with its guest subscriptions.

Microsoft.ComputeLimit/register/action
Registers the subscription for the Compute Limit resource provider and enables the management of compute limit resources.

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

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
 "description": "Read and manage compute limits using compute limit operations.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/980cf6f7-edec-4fd1-8e9e-28f70b1d5258",
 "name": "980cf6f7-edec-4fd1-8e9e-28f70b1d5258",
 "permissions": [
 {
 "actions": [
 "Microsoft.ComputeLimit/locations/guestSubscriptions/read",
 "Microsoft.ComputeLimit/locations/guestSubscriptions/write",
 "Microsoft.ComputeLimit/locations/guestSubscriptions/delete",
 "Microsoft.ComputeLimit/locations/sharedLimits/read",
 "Microsoft.ComputeLimit/locations/sharedLimits/write",
 "Microsoft.ComputeLimit/locations/sharedLimits/delete",
 "Microsoft.ComputeLimit/register/action",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Compute Limit Operator",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Data Operator for Managed Disks

Provides permissions to upload data to empty managed disks, read, or export data of managed disks (not attached to running VMs) and snapshots using SAS URIs and Azure AD authentication.

Actions
Description

none

NotActions

none

DataActions

Microsoft.Compute/disks/download/action
Perform read data operations on Disk SAS Uri

Microsoft.Compute/disks/upload/action
Perform write data operations on Disk SAS Uri

Microsoft.Compute/snapshots/download/action
Perform read data operations on Snapshot SAS Uri

Microsoft.Compute/snapshots/upload/action
Perform write data operations on Snapshot SAS Uri

NotDataActions

none

`{
 "assignableScopes": [
 "/"
 ],
 "description": "Provides permissions to upload data to empty managed disks, read, or export data of managed disks (not attached to running VMs) and snapshots using SAS URIs and Azure AD authentication.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/959f8984-c045-4866-89c7-12bf9737be2e",
 "name": "959f8984-c045-4866-89c7-12bf9737be2e",
 "permissions": [
 {
 "actions": [],
 "notActions": [],
 "dataActions": [
 "Microsoft.Compute/disks/download/action",
 "Microsoft.Compute/disks/upload/action",
 "Microsoft.Compute/snapshots/download/action",
 "Microsoft.Compute/snapshots/upload/action"
 ],
 "notDataActions": []
 }
 ],
 "roleName": "Data Operator for Managed Disks",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Desktop Virtualization Application Group Contributor

Contributor of the Desktop Virtualization Application Group.

Learn more

Actions
Description

Microsoft.DesktopVirtualization/applicationgroups/*

Microsoft.DesktopVirtualization/hostpools/read
Read hostpools

Microsoft.DesktopVirtualization/hostpools/sessionhosts/read
Read hostpools/sessionhosts

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

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
 "description": "Contributor of the Desktop Virtualization Application Group.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/86240b0e-9422-4c43-887b-b61143f32ba8",
 "name": "86240b0e-9422-4c43-887b-b61143f32ba8",
 "permissions": [
 {
 "actions": [
 "Microsoft.DesktopVirtualization/applicationgroups/*",
 "Microsoft.DesktopVirtualization/hostpools/read",
 "Microsoft.DesktopVirtualization/hostpools/sessionhosts/read",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Authorization/*/read",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Support/*"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Desktop Virtualization Application Group Contributor",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Desktop Virtualization Application Group Reader

Reader of the Desktop Virtualization Application Group.

Learn more

Actions
Description

Microsoft.DesktopVirtualization/applicationgroups/*/read

Microsoft.DesktopVirtualization/applicationgroups/read
Read applicationgroups

Microsoft.DesktopVirtualization/hostpools/read
Read hostpools

Microsoft.DesktopVirtualization/hostpools/sessionhosts/read
Read hostpools/sessionhosts

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.Resources/deployments/read
Gets or lists deployments.

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Insights/alertRules/read
Read a classic metric alert

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
 "description": "Reader of the Desktop Virtualization Application Group.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/aebf23d0-b568-4e86-b8f9-fe83a2c6ab55",
 "name": "aebf23d0-b568-4e86-b8f9-fe83a2c6ab55",
 "permissions": [
 {
 "actions": [
 "Microsoft.DesktopVirtualization/applicationgroups/*/read",
 "Microsoft.DesktopVirtualization/applicationgroups/read",
 "Microsoft.DesktopVirtualization/hostpools/read",
 "Microsoft.DesktopVirtualization/hostpools/sessionhosts/read",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.Resources/deployments/read",
 "Microsoft.Authorization/*/read",
 "Microsoft.Insights/alertRules/read",
 "Microsoft.Support/*"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Desktop Virtualization Application Group Reader",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Desktop Virtualization Contributor

Contributor of Desktop Virtualization.

Learn more

Actions
Description

Microsoft.DesktopVirtualization/*

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

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
 "description": "Contributor of Desktop Virtualization.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/082f0a83-3be5-4ba1-904c-961cca79b387",
 "name": "082f0a83-3be5-4ba1-904c-961cca79b387",
 "permissions": [
 {
 "actions": [
 "Microsoft.DesktopVirtualization/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Authorization/*/read",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Support/*"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Desktop Virtualization Contributor",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Desktop Virtualization Host Pool Contributor

Contributor of the Desktop Virtualization Host Pool.

Learn more

Actions
Description

Microsoft.DesktopVirtualization/hostpools/*

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

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
 "description": "Contributor of the Desktop Virtualization Host Pool.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/e307426c-f9b6-4e81-87de-d99efb3c32bc",
 "name": "e307426c-f9b6-4e81-87de-d99efb3c32bc",
 "permissions": [
 {
 "actions": [
 "Microsoft.DesktopVirtualization/hostpools/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Authorization/*/read",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Support/*"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Desktop Virtualization Host Pool Contributor",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Desktop Virtualization Host Pool Reader

Reader of the Desktop Virtualization Host Pool.

Learn more

Actions
Description

Microsoft.DesktopVirtualization/hostpools/*/read

Microsoft.DesktopVirtualization/hostpools/read
Read hostpools

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.Resources/deployments/read
Gets or lists deployments.

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Insights/alertRules/read
Read a classic metric alert

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
 "description": "Reader of the Desktop Virtualization Host Pool.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/ceadfde2-b300-400a-ab7b-6143895aa822",
 "name": "ceadfde2-b300-400a-ab7b-6143895aa822",
 "permissions": [
 {
 "actions": [
 "Microsoft.DesktopVirtualization/hostpools/*/read",
 "Microsoft.DesktopVirtualization/hostpools/read",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.Resources/deployments/read",
 "Microsoft.Authorization/*/read",
 "Microsoft.Insights/alertRules/read",
 "Microsoft.Support/*"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Desktop Virtualization Host Pool Reader",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Desktop Virtualization Power On Contributor

Provide permission to the Azure Virtual Desktop Resource Provider to start virtual machines.

Learn more

Actions
Description

Microsoft.Compute/virtualMachines/start/action
Starts the virtual machine

Microsoft.Compute/virtualMachines/read
Get the properties of a virtual machine

Microsoft.Compute/virtualMachines/instanceView/read
Gets the detailed runtime status of the virtual machine and its resources

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.HybridCompute/machines/read
Read any Azure Arc machines

Microsoft.HybridCompute/operations/read
Read all Operations for Azure Arc for Servers

Microsoft.HybridCompute/locations/operationresults/read
Reads the status of an operation on Microsoft.HybridCompute Resource Provider

Microsoft.HybridCompute/locations/operationstatus/read
Reads the status of an operation on Microsoft.HybridCompute Resource Provider

Microsoft.AzureStackHCI/virtualMachineInstances/read
Gets/Lists virtual machine instance resource

Microsoft.AzureStackHCI/virtualMachineInstances/start/action
Starts virtual machine instance resource

Microsoft.AzureStackHCI/operations/read
Gets operations

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
 "description": "Provide permission to the Azure Virtual Desktop Resource Provider to start virtual machines.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/489581de-a3bd-480d-9518-53dea7416b33",
 "name": "489581de-a3bd-480d-9518-53dea7416b33",
 "permissions": [
 {
 "actions": [
 "Microsoft.Compute/virtualMachines/start/action",
 "Microsoft.Compute/virtualMachines/read",
 "Microsoft.Compute/virtualMachines/instanceView/read",
 "Microsoft.Authorization/*/read",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.HybridCompute/machines/read",
 "Microsoft.HybridCompute/operations/read",
 "Microsoft.HybridCompute/locations/operationresults/read",
 "Microsoft.HybridCompute/locations/operationstatus/read",
 "Microsoft.AzureStackHCI/virtualMachineInstances/read",
 "Microsoft.AzureStackHCI/virtualMachineInstances/start/action",
 "Microsoft.AzureStackHCI/operations/read"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Desktop Virtualization Power On Contributor",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Desktop Virtualization Power On Off Contributor

Provide permission to the Azure Virtual Desktop Resource Provider to start and stop virtual machines.

Learn more

Actions
Description

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.AzureStackHCI/operations/read
Gets operations

Microsoft.AzureStackHCI/virtualMachineInstances/read
Gets/Lists virtual machine instance resource

Microsoft.AzureStackHCI/virtualMachineInstances/restart/action
Restarts virtual machine instance resource

Microsoft.AzureStackHCI/virtualMachineInstances/start/action
Starts virtual machine instance resource

Microsoft.AzureStackHCI/virtualMachineInstances/stop/action
Stops virtual machine instance resource

Microsoft.Compute/virtualMachines/deallocate/action
Powers off the virtual machine and releases the compute resources

Microsoft.Compute/virtualMachines/instanceView/read
Gets the detailed runtime status of the virtual machine and its resources

Microsoft.Compute/virtualMachines/powerOff/action
Powers off the virtual machine. Note that the virtual machine will continue to be billed.

Microsoft.Compute/virtualMachines/read
Get the properties of a virtual machine

Microsoft.Compute/virtualMachines/restart/action
Restarts the virtual machine

Microsoft.Compute/virtualMachines/start/action
Starts the virtual machine

Microsoft.ComputeSchedule/locations/virtualMachinesCancelOperations/action
virtualMachinesCancelOperations: cancelOperations for a virtual machine

Microsoft.ComputeSchedule/locations/virtualMachinesExecuteDeallocate/action
VirtualMachinesExecuteDeallocate: Execute deallocate operation for a batch of virtual machines, this operation is triggered as soon as Computeschedule receives it.

Microsoft.ComputeSchedule/locations/virtualMachinesExecuteHibernate/action
VirtualMachinesExecuteHibernate: Execute hibernate operation for a batch of virtual machines, this operation is triggered as soon as Computeschedule receives it.

Microsoft.ComputeSchedule/locations/virtualMachinesExecuteStart/action
VirtualMachinesExecuteStart: Execute start operation for a batch of virtual machines, this operation is triggered as soon as Computeschedule receives it.

Microsoft.ComputeSchedule/locations/virtualMachinesGetOperationErrors/action
VirtualMachinesGetOperationErrors: Get error details on operation errors (like transient errors encountered, additional logs) if they exist.

Microsoft.ComputeSchedule/locations/virtualMachinesGetOperationStatus/action
VirtualMachinesGetOperationStatus: Polling endpoint to read status of operations performed on virtual machines

Microsoft.ComputeSchedule/locations/virtualMachinesSubmitDeallocate/action
VirtualMachinesSubmitDeallocate: Schedule deallocate operation for a batch of virtual machines at datetime in future.

Microsoft.ComputeSchedule/locations/virtualMachinesSubmitHibernate/action
VirtualMachinesSubmitHibernate: Schedule hibernate operation for a batch of virtual machines at datetime in future.

Microsoft.ComputeSchedule/locations/virtualMachinesSubmitStart/action
VirtualMachinesSubmitStart: Schedule start operation for a batch of virtual machines at datetime in future.

Microsoft.ComputeSchedule/register/action
Register the subscription for Microsoft.ComputeSchedule

Microsoft.DesktopVirtualization/hostpools/read
Read hostpools

Microsoft.DesktopVirtualization/hostpools/sessionhosts/read
Read hostpools/sessionhosts

Microsoft.DesktopVirtualization/hostpools/sessionhosts/usersessions/delete
Delete hostpools/sessionhosts/usersessions

Microsoft.DesktopVirtualization/hostpools/sessionhosts/usersessions/read
Read hostpools/sessionhosts/usersessions

Microsoft.DesktopVirtualization/hostpools/sessionhosts/usersessions/sendMessage/action
Send message to user session

Microsoft.DesktopVirtualization/hostpools/sessionhosts/write
Write hostpools/sessionhosts

Microsoft.DesktopVirtualization/hostpools/write
Write hostpools

Microsoft.HybridCompute/locations/operationresults/read
Reads the status of an operation on Microsoft.HybridCompute Resource Provider

Microsoft.HybridCompute/locations/operationstatus/read
Reads the status of an operation on Microsoft.HybridCompute Resource Provider

Microsoft.HybridCompute/machines/read
Read any Azure Arc machines

Microsoft.HybridCompute/operations/read
Read all Operations for Azure Arc for Servers

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

Microsoft.Insights/eventtypes/values/read
Read Activity Log events

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

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
 "description": "Provide permission to the Azure Virtual Desktop Resource Provider to start and stop virtual machines.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/40c5ff49-9181-41f8-ae61-143b0e78555e",
 "name": "40c5ff49-9181-41f8-ae61-143b0e78555e",
 "permissions": [
 {
 "actions": [
 "Microsoft.Authorization/*/read",
 "Microsoft.AzureStackHCI/operations/read",
 "Microsoft.AzureStackHCI/virtualMachineInstances/read",
 "Microsoft.AzureStackHCI/virtualMachineInstances/restart/action",
 "Microsoft.AzureStackHCI/virtualMachineInstances/start/action",
 "Microsoft.AzureStackHCI/virtualMachineInstances/stop/action",
 "Microsoft.Compute/virtualMachines/deallocate/action",
 "Microsoft.Compute/virtualMachines/instanceView/read",
 "Microsoft.Compute/virtualMachines/powerOff/action",
 "Microsoft.Compute/virtualMachines/read",
 "Microsoft.Compute/virtualMachines/restart/action",
 "Microsoft.Compute/virtualMachines/start/action",
 "Microsoft.ComputeSchedule/locations/virtualMachinesCancelOperations/action",
 "Microsoft.ComputeSchedule/locations/virtualMachinesExecuteDeallocate/action",
 "Microsoft.ComputeSchedule/locations/virtualMachinesExecuteHibernate/action",
 "Microsoft.ComputeSchedule/locations/virtualMachinesExecuteStart/action",
 "Microsoft.ComputeSchedule/locations/virtualMachinesGetOperationErrors/action",
 "Microsoft.ComputeSchedule/locations/virtualMachinesGetOperationStatus/action",
 "Microsoft.ComputeSchedule/locations/virtualMachinesSubmitDeallocate/action",
 "Microsoft.ComputeSchedule/locations/virtualMachinesSubmitHibernate/action",
 "Microsoft.ComputeSchedule/locations/virtualMachinesSubmitStart/action",
 "Microsoft.ComputeSchedule/register/action",
 "Microsoft.DesktopVirtualization/hostpools/read",
 "Microsoft.DesktopVirtualization/hostpools/sessionhosts/read",
 "Microsoft.DesktopVirtualization/hostpools/sessionhosts/usersessions/delete",
 "Microsoft.DesktopVirtualization/hostpools/sessionhosts/usersessions/read",
 "Microsoft.DesktopVirtualization/hostpools/sessionhosts/usersessions/sendMessage/action",
 "Microsoft.DesktopVirtualization/hostpools/sessionhosts/write",
 "Microsoft.DesktopVirtualization/hostpools/write",
 "Microsoft.HybridCompute/locations/operationresults/read",
 "Microsoft.HybridCompute/locations/operationstatus/read",
 "Microsoft.HybridCompute/machines/read",
 "Microsoft.HybridCompute/operations/read",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Insights/eventtypes/values/read",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Desktop Virtualization Power On Off Contributor",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Desktop Virtualization Reader

Reader of Desktop Virtualization.

Learn more

Actions
Description

Microsoft.DesktopVirtualization/*/read

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.Resources/deployments/read
Gets or lists deployments.

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Insights/alertRules/read
Read a classic metric alert

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
 "description": "Reader of Desktop Virtualization.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/49a72310-ab8d-41df-bbb0-79b649203868",
 "name": "49a72310-ab8d-41df-bbb0-79b649203868",
 "permissions": [
 {
 "actions": [
 "Microsoft.DesktopVirtualization/*/read",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.Resources/deployments/read",
 "Microsoft.Authorization/*/read",
 "Microsoft.Insights/alertRules/read",
 "Microsoft.Support/*"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Desktop Virtualization Reader",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Desktop Virtualization Session Host Operator

Operator of the Desktop Virtualization Session Host.

Learn more

Actions
Description

Microsoft.DesktopVirtualization/hostpools/read
Read hostpools

Microsoft.DesktopVirtualization/hostpools/sessionhosts/*

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

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
 "description": "Operator of the Desktop Virtualization Session Host.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/2ad6aaab-ead9-4eaa-8ac5-da422f562408",
 "name": "2ad6aaab-ead9-4eaa-8ac5-da422f562408",
 "permissions": [
 {
 "actions": [
 "Microsoft.DesktopVirtualization/hostpools/read",
 "Microsoft.DesktopVirtualization/hostpools/sessionhosts/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Authorization/*/read",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Support/*"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Desktop Virtualization Session Host Operator",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Desktop Virtualization User

Allows user to use the applications in an application group.

Learn more

Actions
Description

none

NotActions

none

DataActions

Microsoft.DesktopVirtualization/applicationGroups/useApplications/action
Use ApplicationGroup

Microsoft.DesktopVirtualization/appAttachPackages/useApplications/action
Allow user permissioning on app attach packages in an application group

NotDataActions

none

`{
 "assignableScopes": [
 "/"
 ],
 "description": "Allows user to use the applications in an application group.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/1d18fff3-a72a-46b5-b4a9-0b38a3cd7e63",
 "name": "1d18fff3-a72a-46b5-b4a9-0b38a3cd7e63",
 "permissions": [
 {
 "actions": [],
 "notActions": [],
 "dataActions": [
 "Microsoft.DesktopVirtualization/applicationGroups/useApplications/action",
 "Microsoft.DesktopVirtualization/appAttachPackages/useApplications/action"
 ],
 "notDataActions": []
 }
 ],
 "roleName": "Desktop Virtualization User",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Desktop Virtualization User Session Operator

Operator of the Desktop Virtualization User Session.

Learn more

Actions
Description

Microsoft.DesktopVirtualization/hostpools/read
Read hostpools

Microsoft.DesktopVirtualization/hostpools/sessionhosts/read
Read hostpools/sessionhosts

Microsoft.DesktopVirtualization/hostpools/sessionhosts/usersessions/*

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

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
 "description": "Operator of the Desktop Virtualization User Session.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/ea4bfff8-7fb4-485a-aadd-d4129a0ffaa6",
 "name": "ea4bfff8-7fb4-485a-aadd-d4129a0ffaa6",
 "permissions": [
 {
 "actions": [
 "Microsoft.DesktopVirtualization/hostpools/read",
 "Microsoft.DesktopVirtualization/hostpools/sessionhosts/read",
 "Microsoft.DesktopVirtualization/hostpools/sessionhosts/usersessions/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Authorization/*/read",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Support/*"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Desktop Virtualization User Session Operator",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Desktop Virtualization Virtual Machine Contributor

This role is in preview and subject to change. Provide permission to the Azure Virtual Desktop Resource Provider to create, delete, update, start, and stop virtual machines.

Learn more

Actions
Description

Microsoft.DesktopVirtualization/hostpools/read
Read hostpools

Microsoft.DesktopVirtualization/hostpools/write
Write hostpools

Microsoft.DesktopVirtualization/hostpools/retrieveRegistrationToken/action
Retrieve registration token for host pool

Microsoft.DesktopVirtualization/hostpools/sessionhosts/read
Read hostpools/sessionhosts

Microsoft.DesktopVirtualization/hostpools/sessionhosts/write
Write hostpools/sessionhosts

Microsoft.DesktopVirtualization/hostpools/sessionhosts/delete
Delete hostpools/sessionhosts

Microsoft.DesktopVirtualization/hostpools/sessionhosts/usersessions/read
Read hostpools/sessionhosts/usersessions

Microsoft.DesktopVirtualization/hostpools/sessionhosts/usersessions/disconnect/action
Disconnects the user session form session host

Microsoft.DesktopVirtualization/hostpools/sessionhosts/usersessions/sendMessage/action
Send message to user session

Microsoft.DesktopVirtualization/hostpools/sessionHostConfigurations/read
Read hostpools/sessionhostconfigurations

Microsoft.DesktopVirtualization/hostpools/doNotUseInternalAPI/action
Internal operation that is not meant to be called by customers. This will be removed in a future version. Do not use it.

Microsoft.DesktopVirtualization/hostpools/sessionhosts/retryprovisioning/action
Action on retryprovisioning.

Microsoft.Compute/availabilitySets/read
Get the properties of an availability set

Microsoft.Compute/availabilitySets/write
Creates a new availability set or updates an existing one

Microsoft.Compute/availabilitySets/vmSizes/read
List available sizes for creating or updating a virtual machine in the availability set

Microsoft.Compute/disks/read
Get the properties of a Disk

Microsoft.Compute/disks/write
Creates a new Disk or updates an existing one

Microsoft.Compute/disks/delete
Deletes the Disk

Microsoft.Compute/galleries/read
Gets the properties of Gallery

Microsoft.Compute/galleries/images/read
Gets the properties of Gallery Image

Microsoft.Compute/galleries/images/versions/read
Gets the properties of Gallery Image Version

Microsoft.Compute/images/read
Get the properties of the Image

Microsoft.Compute/locations/usages/read
Gets service limits and current usage quantities for the subscription's compute resources in a location

Microsoft.Compute/locations/vmSizes/read
Lists available virtual machine sizes in a location

Microsoft.Compute/operations/read
Lists operations available on Microsoft.Compute resource provider

Microsoft.Compute/skus/read
Gets the list of Microsoft.Compute SKUs available for your Subscription

Microsoft.Compute/virtualMachines/read
Get the properties of a virtual machine

Microsoft.Compute/virtualMachines/write
Creates a new virtual machine or updates an existing virtual machine

Microsoft.Compute/virtualMachines/delete
Deletes the virtual machine

Microsoft.Compute/virtualMachines/start/action
Starts the virtual machine

Microsoft.Compute/virtualMachines/powerOff/action
Powers off the virtual machine. Note that the virtual machine will continue to be billed.

Microsoft.Compute/virtualMachines/restart/action
Restarts the virtual machine

Microsoft.Compute/virtualMachines/deallocate/action
Powers off the virtual machine and releases the compute resources

Microsoft.Compute/virtualMachines/runCommand/action
Executes a predefined script on the virtual machine

Microsoft.Compute/virtualMachines/extensions/read
Get the properties of a virtual machine extension

Microsoft.Compute/virtualMachines/extensions/write
Creates a new virtual machine extension or updates an existing one

Microsoft.Compute/virtualMachines/extensions/delete
Deletes the virtual machine extension

Microsoft.Compute/virtualMachines/runCommands/read
Get the properties of a virtual machine run command

Microsoft.Compute/virtualMachines/runCommands/write
Creates a new virtual machine run command or updates an existing one

Microsoft.Compute/virtualMachines/vmSizes/read
Lists available sizes the virtual machine can be updated to

Microsoft.Network/networkSecurityGroups/read
Gets a network security group definition

Microsoft.Network/networkInterfaces/write
Creates a network interface or updates an existing network interface.

Microsoft.Network/networkInterfaces/read
Gets a network interface definition.

Microsoft.Network/networkInterfaces/join/action
Joins a Virtual Machine to a network interface. Not Alertable.

Microsoft.Network/networkInterfaces/delete
Deletes a network interface

Microsoft.Network/virtualNetworks/subnets/read
Gets a virtual network subnet definition

Microsoft.Network/virtualNetworks/subnets/join/action
Joins a virtual network. Not Alertable.

Microsoft.Network/virtualNetworks/usages/read
Get the IP usages for each subnet of the virtual network

Microsoft.Network/virtualNetworks/read
Get the virtual network definition

Microsoft.Network/networkSecurityGroups/read
Gets a network security group definition

Microsoft.Marketplace/offerTypes/publishers/offers/plans/agreements/read
Returns an Agreement.

Microsoft.KeyVault/vaults/deploy/action
Enables access to secrets in a key vault when deploying Azure resources

Microsoft.Storage/storageAccounts/read
Returns the list of storage accounts or gets the properties for the specified storage account.

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.DesktopVirtualization/scalingPlans/read
Read scalingplans

Microsoft.DesktopVirtualization/scalingPlans/write
Write scalingplans

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
 "description": "This role is in preview and subject to change. Provide permission to the Azure Virtual Desktop Resource Provider to create, delete, update, start, and stop virtual machines.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/a959dbd1-f747-45e3-8ba6-dd80f235f97c",
 "name": "a959dbd1-f747-45e3-8ba6-dd80f235f97c",
 "permissions": [
 {
 "actions": [
 "Microsoft.DesktopVirtualization/hostpools/read",
 "Microsoft.DesktopVirtualization/hostpools/write",
 "Microsoft.DesktopVirtualization/hostpools/retrieveRegistrationToken/action",
 "Microsoft.DesktopVirtualization/hostpools/sessionhosts/read",
 "Microsoft.DesktopVirtualization/hostpools/sessionhosts/write",
 "Microsoft.DesktopVirtualization/hostpools/sessionhosts/delete",
 "Microsoft.DesktopVirtualization/hostpools/sessionhosts/usersessions/read",
 "Microsoft.DesktopVirtualization/hostpools/sessionhosts/usersessions/disconnect/action",
 "Microsoft.DesktopVirtualization/hostpools/sessionhosts/usersessions/sendMessage/action",
 "Microsoft.DesktopVirtualization/hostpools/sessionHostConfigurations/read",
 "Microsoft.DesktopVirtualization/hostpools/doNotUseInternalAPI/action",
 "Microsoft.DesktopVirtualization/hostpools/sessionhosts/retryprovisioning/action",
 "Microsoft.Compute/availabilitySets/read",
 "Microsoft.Compute/availabilitySets/write",
 "Microsoft.Compute/availabilitySets/vmSizes/read",
 "Microsoft.Compute/disks/read",
 "Microsoft.Compute/disks/write",
 "Microsoft.Compute/disks/delete",
 "Microsoft.Compute/galleries/read",
 "Microsoft.Compute/galleries/images/read",
 "Microsoft.Compute/galleries/images/versions/read",
 "Microsoft.Compute/images/read",
 "Microsoft.Compute/locations/usages/read",
 "Microsoft.Compute/locations/vmSizes/read",
 "Microsoft.Compute/operations/read",
 "Microsoft.Compute/skus/read",
 "Microsoft.Compute/virtualMachines/read",
 "Microsoft.Compute/virtualMachines/write",
 "Microsoft.Compute/virtualMachines/delete",
 "Microsoft.Compute/virtualMachines/start/action",
 "Microsoft.Compute/virtualMachines/powerOff/action",
 "Microsoft.Compute/virtualMachines/restart/action",
 "Microsoft.Compute/virtualMachines/deallocate/action",
 "Microsoft.Compute/virtualMachines/runCommand/action",
 "Microsoft.Compute/virtualMachines/extensions/read",
 "Microsoft.Compute/virtualMachines/extensions/write",
 "Microsoft.Compute/virtualMachines/extensions/delete",
 "Microsoft.Compute/virtualMachines/runCommands/read",
 "Microsoft.Compute/virtualMachines/runCommands/write",
 "Microsoft.Compute/virtualMachines/vmSizes/read",
 "Microsoft.Network/networkSecurityGroups/read",
 "Microsoft.Network/networkInterfaces/write",
 "Microsoft.Network/networkInterfaces/read",
 "Microsoft.Network/networkInterfaces/join/action",
 "Microsoft.Network/networkInterfaces/delete",
 "Microsoft.Network/virtualNetworks/subnets/read",
 "Microsoft.Network/virtualNetworks/subnets/join/action",
 "Microsoft.Network/virtualNetworks/usages/read",
 "Microsoft.Network/virtualNetworks/read",
 "Microsoft.Network/networkSecurityGroups/read",
 "Microsoft.Marketplace/offerTypes/publishers/offers/plans/agreements/read",
 "Microsoft.KeyVault/vaults/deploy/action",
 "Microsoft.Storage/storageAccounts/read",
 "Microsoft.Authorization/*/read",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.DesktopVirtualization/scalingPlans/read",
 "Microsoft.DesktopVirtualization/scalingPlans/write"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Desktop Virtualization Virtual Machine Contributor",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Desktop Virtualization Workspace Contributor

Contributor of the Desktop Virtualization Workspace.

Learn more

Actions
Description

Microsoft.DesktopVirtualization/workspaces/*

Microsoft.DesktopVirtualization/applicationgroups/read
Read applicationgroups

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

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
 "description": "Contributor of the Desktop Virtualization Workspace.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/21efdde3-836f-432b-bf3d-3e8e734d4b2b",
 "name": "21efdde3-836f-432b-bf3d-3e8e734d4b2b",
 "permissions": [
 {
 "actions": [
 "Microsoft.DesktopVirtualization/workspaces/*",
 "Microsoft.DesktopVirtualization/applicationgroups/read",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Authorization/*/read",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Support/*"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Desktop Virtualization Workspace Contributor",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Desktop Virtualization Workspace Reader

Reader of the Desktop Virtualization Workspace.

Learn more

Actions
Description

Microsoft.DesktopVirtualization/workspaces/read
Read workspaces

Microsoft.DesktopVirtualization/applicationgroups/read
Read applicationgroups

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.Resources/deployments/read
Gets or lists deployments.

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Insights/alertRules/read
Read a classic metric alert

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
 "description": "Reader of the Desktop Virtualization Workspace.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/0fa44ee9-7a7d-466b-9bb2-2bf446b1204d",
 "name": "0fa44ee9-7a7d-466b-9bb2-2bf446b1204d",
 "permissions": [
 {
 "actions": [
 "Microsoft.DesktopVirtualization/workspaces/read",
 "Microsoft.DesktopVirtualization/applicationgroups/read",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.Resources/deployments/read",
 "Microsoft.Authorization/*/read",
 "Microsoft.Insights/alertRules/read",
 "Microsoft.Support/*"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Desktop Virtualization Workspace Reader",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Disk Backup Reader

Provides permission to backup vault to perform disk backup.

Learn more

Actions
Description

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Compute/disks/read
Get the properties of a Disk

Microsoft.Compute/disks/beginGetAccess/action
Get the SAS URI of the Disk for blob access

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
 "description": "Provides permission to backup vault to perform disk backup.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/3e5e47e6-65f7-47ef-90b5-e5dd4d455f24",
 "name": "3e5e47e6-65f7-47ef-90b5-e5dd4d455f24",
 "permissions": [
 {
 "actions": [
 "Microsoft.Authorization/*/read",
 "Microsoft.Compute/disks/read",
 "Microsoft.Compute/disks/beginGetAccess/action"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Disk Backup Reader",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Disk Pool Operator

Provide permission to StoragePool Resource Provider to manage disks added to a disk pool.

Actions
Description

Microsoft.Compute/disks/write
Creates a new Disk or updates an existing one

Microsoft.Compute/disks/read
Get the properties of a Disk

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

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
 "description": "Used by the StoragePool Resource Provider to manage Disks added to a Disk Pool.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/60fc6e62-5479-42d4-8bf4-67625fcc2840",
 "name": "60fc6e62-5479-42d4-8bf4-67625fcc2840",
 "permissions": [
 {
 "actions": [
 "Microsoft.Compute/disks/write",
 "Microsoft.Compute/disks/read",
 "Microsoft.Authorization/*/read",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Disk Pool Operator",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Disk Restore Operator

Provides permission to backup vault to perform disk restore.

Learn more

Actions
Description

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.Compute/disks/write
Creates a new Disk or updates an existing one

Microsoft.Compute/disks/read
Get the properties of a Disk

Microsoft.Compute/disks/beginGetAccess/action
Get the SAS URI of the Disk for blob access

Microsoft.Compute/disks/endGetAccess/action
Revoke the SAS URI of the Disk

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
 "description": "Provides permission to backup vault to perform disk restore.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/b50d9833-a0cb-478e-945f-707fcc997c13",
 "name": "b50d9833-a0cb-478e-945f-707fcc997c13",
 "permissions": [
 {
 "actions": [
 "Microsoft.Authorization/*/read",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.Compute/disks/write",
 "Microsoft.Compute/disks/read",
 "Microsoft.Compute/disks/beginGetAccess/action",
 "Microsoft.Compute/disks/endGetAccess/action"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Disk Restore Operator",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Disk Snapshot Contributor

Provides permission to backup vault to manage disk snapshots.

Learn more

Actions
Description

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.Compute/snapshots/delete
Delete a Snapshot

Microsoft.Compute/snapshots/write
Create a new Snapshot or update an existing one

Microsoft.Compute/snapshots/read
Get the properties of a Snapshot

Microsoft.Compute/snapshots/beginGetAccess/action
Get the SAS URI of the Snapshot for blob access

Microsoft.Compute/snapshots/endGetAccess/action
Revoke the SAS URI of the Snapshot

Microsoft.Compute/disks/beginGetAccess/action
Get the SAS URI of the Disk for blob access

Microsoft.Storage/storageAccounts/listkeys/action
Returns the access keys for the specified storage account.

Microsoft.Storage/storageAccounts/write
Creates a storage account with the specified parameters or update the properties or tags or adds custom domain for the specified storage account.

Microsoft.Storage/storageAccounts/read
Returns the list of storage accounts or gets the properties for the specified storage account.

Microsoft.Storage/storageAccounts/delete
Deletes an existing storage account.

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
 "description": "Provides permission to backup vault to manage disk snapshots.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/7efff54f-a5b4-42b5-a1c5-5411624893ce",
 "name": "7efff54f-a5b4-42b5-a1c5-5411624893ce",
 "permissions": [
 {
 "actions": [
 "Microsoft.Authorization/*/read",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.Compute/snapshots/delete",
 "Microsoft.Compute/snapshots/write",
 "Microsoft.Compute/snapshots/read",
 "Microsoft.Compute/snapshots/beginGetAccess/action",
 "Microsoft.Compute/snapshots/endGetAccess/action",
 "Microsoft.Compute/disks/beginGetAccess/action",
 "Microsoft.Storage/storageAccounts/listkeys/action",
 "Microsoft.Storage/storageAccounts/write",
 "Microsoft.Storage/storageAccounts/read",
 "Microsoft.Storage/storageAccounts/delete"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Disk Snapshot Contributor",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Quantum Workspace Data Contributor

Create, read, and modify jobs and other Workspace data. This role is in preview and subject to change.

Learn more

Actions
Description

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.Quantum/Workspaces/read
Read Workspace

Microsoft.Quantum/locations/offerings/read
Read providers supported

NotActions

none

DataActions

Microsoft.Quantum/Workspaces/jobs/read
Read jobs and other data

Microsoft.Quantum/Workspaces/jobs/write
Write jobs and other data

NotDataActions

none

`{
 "assignableScopes": [
 "/"
 ],
 "description": "Create, read, and modify jobs and other Workspace data. This role is in preview and subject to change.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/c1410b24-3e69-4857-8f86-4d0a2e603250",
 "name": "c1410b24-3e69-4857-8f86-4d0a2e603250",
 "permissions": [
 {
 "actions": [
 "Microsoft.Authorization/*/read",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.Quantum/Workspaces/read",
 "Microsoft.Quantum/locations/offerings/read"
 ],
 "notActions": [],
 "dataActions": [
 "Microsoft.Quantum/Workspaces/jobs/read",
 "Microsoft.Quantum/Workspaces/jobs/write"
 ],
 "notDataActions": []
 }
 ],
 "roleName": "Quantum Workspace Data Contributor",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Virtual Machine Administrator Login

View Virtual Machines in the portal and login as administrator

Learn more

Actions
Description

Microsoft.Network/publicIPAddresses/read
Gets a public IP address definition.

Microsoft.Network/virtualNetworks/read
Get the virtual network definition

Microsoft.Network/loadBalancers/read
Gets a load balancer definition

Microsoft.Network/networkInterfaces/read
Gets a network interface definition.

Microsoft.Compute/virtualMachines/*/read

Microsoft.HybridCompute/machines/*/read

Microsoft.HybridConnectivity/endpoints/listCredentials/action
Gets the endpoint access credentials to the resource.

NotActions

none

DataActions

Microsoft.Compute/virtualMachines/login/action
Log in to a virtual machine as a regular user

Microsoft.Compute/virtualMachines/loginAsAdmin/action
Log in to a virtual machine with Windows administrator or Linux root user privileges

Microsoft.HybridCompute/machines/login/action
Log in to an Azure Arc machine as a regular user

Microsoft.HybridCompute/machines/loginAsAdmin/action
Log in to an Azure Arc machine with Windows administrator or Linux root user privilege

NotDataActions

none

`{
 "assignableScopes": [
 "/"
 ],
 "description": "View Virtual Machines in the portal and login as administrator",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/1c0163c0-47e6-4577-8991-ea5c82e286e4",
 "name": "1c0163c0-47e6-4577-8991-ea5c82e286e4",
 "permissions": [
 {
 "actions": [
 "Microsoft.Network/publicIPAddresses/read",
 "Microsoft.Network/virtualNetworks/read",
 "Microsoft.Network/loadBalancers/read",
 "Microsoft.Network/networkInterfaces/read",
 "Microsoft.Compute/virtualMachines/*/read",
 "Microsoft.HybridCompute/machines/*/read",
 "Microsoft.HybridConnectivity/endpoints/listCredentials/action"
 ],
 "notActions": [],
 "dataActions": [
 "Microsoft.Compute/virtualMachines/login/action",
 "Microsoft.Compute/virtualMachines/loginAsAdmin/action",
 "Microsoft.HybridCompute/machines/login/action",
 "Microsoft.HybridCompute/machines/loginAsAdmin/action"
 ],
 "notDataActions": []
 }
 ],
 "roleName": "Virtual Machine Administrator Login",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Virtual Machine Contributor

Create and manage virtual machines, manage disks, install and run software, reset password of the root user of the virtual machine using VM extensions, and manage local user accounts using VM extensions. This role does not grant you management access to the virtual network or storage account the virtual machines are connected to. This role does not allow you to assign roles in Azure RBAC.

Learn more

Actions
Description

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Compute/availabilitySets/*
Create and manage compute availability sets

Microsoft.Compute/locations/*
Create and manage compute locations

Microsoft.Compute/virtualMachines/*
Perform all virtual machine actions including create, update, delete, start, restart, and power off virtual machines. Execute scripts on virtual machines.

Microsoft.Compute/virtualMachineScaleSets/*
Create and manage virtual machine scale sets

Microsoft.Compute/cloudServices/*

Microsoft.Compute/disks/write
Creates a new Disk or updates an existing one

Microsoft.Compute/disks/read
Get the properties of a Disk

Microsoft.Compute/disks/delete
Deletes the Disk

Microsoft.Compute/hostgroups/write
Creates a new host group or updates an existing host group

Microsoft.Compute/hostgroups/hosts/write
Creates a new host or updates an existing host

Microsoft.DevTestLab/schedules/*

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

Microsoft.Network/applicationGateways/backendAddressPools/join/action
Joins an application gateway backend address pool. Not Alertable.

Microsoft.Network/loadBalancers/backendAddressPools/join/action
Joins a load balancer backend address pool. Not Alertable.

Microsoft.Network/loadBalancers/inboundNatPools/join/action
Joins a load balancer inbound NAT pool. Not alertable.

Microsoft.Network/loadBalancers/inboundNatRules/join/action
Joins a load balancer inbound nat rule. Not Alertable.

Microsoft.Network/loadBalancers/probes/join/action
Allows using probes of a load balancer. For example, with this permission healthProbe property of VM scale set can reference the probe. Not alertable.

Microsoft.Network/loadBalancers/read
Gets a load balancer definition

Microsoft.Network/locations/*
Create and manage network locations

Microsoft.Network/networkInterfaces/*
Create and manage network interfaces

Microsoft.Network/networkSecurityGroups/join/action
Joins a network security group. Not Alertable.

Microsoft.Network/networkSecurityGroups/read
Gets a network security group definition

Microsoft.Network/publicIPAddresses/join/action
Joins a public IP address. Not Alertable.

Microsoft.Network/publicIPAddresses/read
Gets a public IP address definition.

Microsoft.Network/virtualNetworks/read
Get the virtual network definition

Microsoft.Network/virtualNetworks/subnets/join/action
Joins a virtual network. Not Alertable.

Microsoft.RecoveryServices/locations/*

Microsoft.RecoveryServices/Vaults/backupFabrics/backupProtectionIntent/write
Create a backup Protection Intent

Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/*/read

Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/read
Returns object details of the Protected Item

Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/write
Create a backup Protected Item

Microsoft.RecoveryServices/Vaults/backupPolicies/read
Returns all Protection Policies

Microsoft.RecoveryServices/Vaults/backupPolicies/write
Creates or Updates Protection Policy

Microsoft.RecoveryServices/Vaults/read
The Get Vault operation gets an object representing the Azure resource of type 'vault'

Microsoft.RecoveryServices/Vaults/usages/read
Returns usage details for a Recovery Services Vault.

Microsoft.RecoveryServices/Vaults/write
Create Vault operation creates an Azure resource of type 'vault'

Microsoft.ResourceHealth/availabilityStatuses/read
Gets the availability statuses for all resources in the specified scope

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.SerialConsole/serialPorts/connect/action
Connect to a serial port

Microsoft.SqlVirtualMachine/*

Microsoft.Storage/storageAccounts/listKeys/action
Returns the access keys for the specified storage account.

Microsoft.Storage/storageAccounts/read
Returns the list of storage accounts or gets the properties for the specified storage account.

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
 "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they're connected to.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
 "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
 "permissions": [
 {
 "actions": [
 "Microsoft.Authorization/*/read",
 "Microsoft.Compute/availabilitySets/*",
 "Microsoft.Compute/locations/*",
 "Microsoft.Compute/virtualMachines/*",
 "Microsoft.Compute/virtualMachineScaleSets/*",
 "Microsoft.Compute/cloudServices/*",
 "Microsoft.Compute/disks/write",
 "Microsoft.Compute/disks/read",
 "Microsoft.Compute/disks/delete",
 "Microsoft.Compute/hostgroups/write",
 "Microsoft.Compute/hostgroups/hosts/write",
 "Microsoft.DevTestLab/schedules/*",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
 "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
 "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
 "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
 "Microsoft.Network/loadBalancers/probes/join/action",
 "Microsoft.Network/loadBalancers/read",
 "Microsoft.Network/locations/*",
 "Microsoft.Network/networkInterfaces/*",
 "Microsoft.Network/networkSecurityGroups/join/action",
 "Microsoft.Network/networkSecurityGroups/read",
 "Microsoft.Network/publicIPAddresses/join/action",
 "Microsoft.Network/publicIPAddresses/read",
 "Microsoft.Network/virtualNetworks/read",
 "Microsoft.Network/virtualNetworks/subnets/join/action",
 "Microsoft.RecoveryServices/locations/*",
 "Microsoft.RecoveryServices/Vaults/backupFabrics/backupProtectionIntent/write",
 "Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/*/read",
 "Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/read",
 "Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/write",
 "Microsoft.RecoveryServices/Vaults/backupPolicies/read",
 "Microsoft.RecoveryServices/Vaults/backupPolicies/write",
 "Microsoft.RecoveryServices/Vaults/read",
 "Microsoft.RecoveryServices/Vaults/usages/read",
 "Microsoft.RecoveryServices/Vaults/write",
 "Microsoft.ResourceHealth/availabilityStatuses/read",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.SerialConsole/serialPorts/connect/action",
 "Microsoft.SqlVirtualMachine/*",
 "Microsoft.Storage/storageAccounts/listKeys/action",
 "Microsoft.Storage/storageAccounts/read",
 "Microsoft.Support/*"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Virtual Machine Contributor",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Virtual Machine Data Access Administrator (preview)

Manage access to Virtual Machines by adding or removing role assignments for the Virtual Machine Administrator Login and Virtual Machine User Login roles. Includes an ABAC condition to constrain role assignments.

Actions
Description

Microsoft.Authorization/roleAssignments/write
Create a role assignment at the specified scope.

Microsoft.Authorization/roleAssignments/delete
Delete a role assignment at the specified scope.

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.Resources/subscriptions/read
Gets the list of subscriptions.

Microsoft.Management/managementGroups/read
List management groups for the authenticated user.

Microsoft.Network/publicIPAddresses/read
Gets a public IP address definition.

Microsoft.Network/virtualNetworks/read
Get the virtual network definition

Microsoft.Network/loadBalancers/read
Gets a load balancer definition

Microsoft.Network/networkInterfaces/read
Gets a network interface definition.

Microsoft.Compute/virtualMachines/*/read

Microsoft.HybridCompute/machines/*/read

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Support/*
Create and update a support ticket

NotActions

none

DataActions

none

NotDataActions

none

Condition

((!(ActionMatches{'Microsoft.Authorization/roleAssignments/write'})) OR (@Request[Microsoft.Authorization/roleAssignments:RoleDefinitionId] ForAnyOfAnyValues:GuidEquals{1c0163c0-47e6-4577-8991-ea5c82e286e4, fb879df8-f326-4884-b1cf-06f3ad86be52})) AND ((!(ActionMatches{'Microsoft.Authorization/roleAssignments/delete'})) OR (@Resource[Microsoft.Authorization/roleAssignments:RoleDefinitionId] ForAnyOfAnyValues:GuidEquals{1c0163c0-47e6-4577-8991-ea5c82e286e4, fb879df8-f326-4884-b1cf-06f3ad86be52}))
Add or remove role assignments for the following roles:
Virtual Machine Administrator Login
Virtual Machine User Login

`{
 "assignableScopes": [
 "/"
 ],
 "description": "Manage access to Virtual Machines by adding or removing role assignments for the Virtual Machine Administrator Login and Virtual Machine User Login roles. Includes an ABAC condition to constrain role assignments.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/66f75aeb-eabe-4b70-9f1e-c350c4c9ad04",
 "name": "66f75aeb-eabe-4b70-9f1e-c350c4c9ad04",
 "permissions": [
 {
 "actions": [
 "Microsoft.Authorization/roleAssignments/write",
 "Microsoft.Authorization/roleAssignments/delete",
 "Microsoft.Authorization/*/read",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.Resources/subscriptions/read",
 "Microsoft.Management/managementGroups/read",
 "Microsoft.Network/publicIPAddresses/read",
 "Microsoft.Network/virtualNetworks/read",
 "Microsoft.Network/loadBalancers/read",
 "Microsoft.Network/networkInterfaces/read",
 "Microsoft.Compute/virtualMachines/*/read",
 "Microsoft.HybridCompute/machines/*/read",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Support/*"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": [],
 "conditionVersion": "2.0",
 "condition": "((!(ActionMatches{'Microsoft.Authorization/roleAssignments/write'})) OR (@Request[Microsoft.Authorization/roleAssignments:RoleDefinitionId] ForAnyOfAnyValues:GuidEquals{1c0163c0-47e6-4577-8991-ea5c82e286e4, fb879df8-f326-4884-b1cf-06f3ad86be52})) AND ((!(ActionMatches{'Microsoft.Authorization/roleAssignments/delete'})) OR (@Resource[Microsoft.Authorization/roleAssignments:RoleDefinitionId] ForAnyOfAnyValues:GuidEquals{1c0163c0-47e6-4577-8991-ea5c82e286e4, fb879df8-f326-4884-b1cf-06f3ad86be52}))"
 }
 ],
 "roleName": "Virtual Machine Data Access Administrator (preview)",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Virtual Machine Local User Login

View Virtual Machines in the portal and login as a local user configured on the Arc server.

Learn more

Actions
Description

Microsoft.HybridCompute/machines/*/read

Microsoft.HybridConnectivity/endpoints/listCredentials/action
Gets the endpoint access credentials to the resource.

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
 "description": "View Virtual Machines in the portal and login as a local user configured on the arc server",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/602da2ba-a5c2-41da-b01d-5360126ab525",
 "name": "602da2ba-a5c2-41da-b01d-5360126ab525",
 "permissions": [
 {
 "actions": [
 "Microsoft.HybridCompute/machines/*/read",
 "Microsoft.HybridConnectivity/endpoints/listCredentials/action"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Virtual Machine Local User Login",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Virtual Machine User Login

View Virtual Machines in the portal and login as a regular user.

Learn more

Actions
Description

Microsoft.Network/publicIPAddresses/read
Gets a public IP address definition.

Microsoft.Network/virtualNetworks/read
Get the virtual network definition

Microsoft.Network/loadBalancers/read
Gets a load balancer definition

Microsoft.Network/networkInterfaces/read
Gets a network interface definition.

Microsoft.Compute/virtualMachines/*/read

Microsoft.HybridCompute/machines/*/read

Microsoft.HybridConnectivity/endpoints/listCredentials/action
Gets the endpoint access credentials to the resource.

NotActions

none

DataActions

Microsoft.Compute/virtualMachines/login/action
Log in to a virtual machine as a regular user

Microsoft.HybridCompute/machines/login/action
Log in to an Azure Arc machine as a regular user

NotDataActions

none

`{
 "assignableScopes": [
 "/"
 ],
 "description": "View Virtual Machines in the portal and login as a regular user.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/fb879df8-f326-4884-b1cf-06f3ad86be52",
 "name": "fb879df8-f326-4884-b1cf-06f3ad86be52",
 "permissions": [
 {
 "actions": [
 "Microsoft.Network/publicIPAddresses/read",
 "Microsoft.Network/virtualNetworks/read",
 "Microsoft.Network/loadBalancers/read",
 "Microsoft.Network/networkInterfaces/read",
 "Microsoft.Compute/virtualMachines/*/read",
 "Microsoft.HybridCompute/machines/*/read",
 "Microsoft.HybridConnectivity/endpoints/listCredentials/action"
 ],
 "notActions": [],
 "dataActions": [
 "Microsoft.Compute/virtualMachines/login/action",
 "Microsoft.HybridCompute/machines/login/action"
 ],
 "notDataActions": []
 }
 ],
 "roleName": "Virtual Machine User Login",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## VM Restore Operator

Create and Delete resources during VM Restore. This role is in preview and subject to change.

Learn more

Actions
Description

Microsoft.Authorization/*/read
Read roles and role assignments

Microsoft.Compute/disks/read
Get the properties of a Disk

Microsoft.Compute/disks/write
Creates a new Disk or updates an existing one

Microsoft.Compute/disks/delete
Deletes the Disk

Microsoft.Compute/disks/beginGetAccess/action
Get the SAS URI of the Disk for blob access

Microsoft.Compute/disks/endGetAccess/action
Revoke the SAS URI of the Disk

Microsoft.Compute/locations/diskOperations/read
Gets the status of an asynchronous Disk operation

Microsoft.Compute/virtualMachines/read
Get the properties of a virtual machine

Microsoft.Compute/virtualMachines/write
Creates a new virtual machine or updates an existing virtual machine

Microsoft.Compute/virtualMachines/delete
Deletes the virtual machine

Microsoft.Compute/virtualMachines/instanceView/read
Gets the detailed runtime status of the virtual machine and its resources

Microsoft.Compute/virtualMachines/extensions/read
Get the properties of a virtual machine extension

Microsoft.Compute/virtualMachines/extensions/write
Creates a new virtual machine extension or updates an existing one

Microsoft.Compute/virtualMachines/extensions/delete
Deletes the virtual machine extension

Microsoft.Insights/alertRules/*
Create and manage a classic metric alert

Microsoft.Network/locations/operationResults/read
Gets operation result of an async POST or DELETE operation

Microsoft.Network/locations/operations/read
Gets operation resource that represents status of an asynchronous operation

Microsoft.Network/locations/usages/read
Gets the resources usage metrics

Microsoft.Network/networkInterfaces/delete
Deletes a network interface

Microsoft.Network/networkInterfaces/ipconfigurations/read
Gets a network interface ip configuration definition.

Microsoft.Network/networkInterfaces/join/action
Joins a Virtual Machine to a network interface. Not Alertable.

Microsoft.Network/networkInterfaces/read
Gets a network interface definition.

Microsoft.Network/networkInterfaces/write
Creates a network interface or updates an existing network interface.

Microsoft.Network/networkSecurityGroups/read
Gets a network security group definition

Microsoft.Network/networkSecurityGroups/securityRules/read
Gets a security rule definition

Microsoft.Network/publicIPAddresses/delete
Deletes a public IP address.

Microsoft.Network/publicIPAddresses/join/action
Joins a public IP address. Not Alertable.

Microsoft.Network/publicIPAddresses/read
Gets a public IP address definition.

Microsoft.Network/publicIPAddresses/write
Creates a public IP address or updates an existing public IP address.

Microsoft.Network/virtualNetworks/read
Get the virtual network definition

Microsoft.Network/virtualNetworks/subnets/join/action
Joins a virtual network. Not Alertable.

Microsoft.Network/virtualNetworks/subnets/read
Gets a virtual network subnet definition

Microsoft.Resources/deployments/*
Create and manage a deployment

Microsoft.Resources/subscriptions/resourceGroups/read
Gets or lists resource groups.

Microsoft.Storage/checkNameAvailability/read
Checks that account name is valid and is not in use.

Microsoft.Storage/storageAccounts/blobServices/containers/delete
Returns the result of deleting a container

Microsoft.Storage/storageAccounts/blobServices/containers/read
Returns list of containers

Microsoft.Storage/storageAccounts/blobServices/containers/write
Returns the result of put blob container

Microsoft.Storage/storageAccounts/listKeys/action
Returns the access keys for the specified storage account.

Microsoft.Storage/storageAccounts/read
Returns the list of storage accounts or gets the properties for the specified storage account.

Microsoft.Storage/storageAccounts/write
Creates a storage account with the specified parameters or update the properties or tags or adds custom domain for the specified storage account.

NotActions

none

DataActions

Microsoft.Storage/storageAccounts/blobServices/containers/blobs/delete
Returns the result of deleting a blob

Microsoft.Storage/storageAccounts/blobServices/containers/blobs/read
Returns a blob or a list of blobs

Microsoft.Storage/storageAccounts/blobServices/containers/blobs/write
Returns the result of writing a blob

Microsoft.Storage/storageAccounts/blobServices/containers/blobs/add/action
Returns the result of adding blob content

NotDataActions

none

`{
 "assignableScopes": [
 "/"
 ],
 "description": "Create and Delete resources during VM Restore. This role is in preview and subject to change.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/dfce8971-25e3-42e3-ba33-6055438e3080",
 "name": "dfce8971-25e3-42e3-ba33-6055438e3080",
 "permissions": [
 {
 "actions": [
 "Microsoft.Authorization/*/read",
 "Microsoft.Compute/disks/read",
 "Microsoft.Compute/disks/write",
 "Microsoft.Compute/disks/delete",
 "Microsoft.Compute/disks/beginGetAccess/action",
 "Microsoft.Compute/disks/endGetAccess/action",
 "Microsoft.Compute/locations/diskOperations/read",
 "Microsoft.Compute/virtualMachines/read",
 "Microsoft.Compute/virtualMachines/write",
 "Microsoft.Compute/virtualMachines/delete",
 "Microsoft.Compute/virtualMachines/instanceView/read",
 "Microsoft.Compute/virtualMachines/extensions/read",
 "Microsoft.Compute/virtualMachines/extensions/write",
 "Microsoft.Compute/virtualMachines/extensions/delete",
 "Microsoft.Insights/alertRules/*",
 "Microsoft.Network/locations/operationResults/read",
 "Microsoft.Network/locations/operations/read",
 "Microsoft.Network/locations/usages/read",
 "Microsoft.Network/networkInterfaces/delete",
 "Microsoft.Network/networkInterfaces/ipconfigurations/read",
 "Microsoft.Network/networkInterfaces/join/action",
 "Microsoft.Network/networkInterfaces/read",
 "Microsoft.Network/networkInterfaces/write",
 "Microsoft.Network/networkSecurityGroups/read",
 "Microsoft.Network/networkSecurityGroups/securityRules/read",
 "Microsoft.Network/publicIPAddresses/delete",
 "Microsoft.Network/publicIPAddresses/join/action",
 "Microsoft.Network/publicIPAddresses/read",
 "Microsoft.Network/publicIPAddresses/write",
 "Microsoft.Network/virtualNetworks/read",
 "Microsoft.Network/virtualNetworks/subnets/join/action",
 "Microsoft.Network/virtualNetworks/subnets/read",
 "Microsoft.Resources/deployments/*",
 "Microsoft.Resources/subscriptions/resourceGroups/read",
 "Microsoft.Storage/checkNameAvailability/read",
 "Microsoft.Storage/storageAccounts/blobServices/containers/delete",
 "Microsoft.Storage/storageAccounts/blobServices/containers/read",
 "Microsoft.Storage/storageAccounts/blobServices/containers/write",
 "Microsoft.Storage/storageAccounts/listKeys/action",
 "Microsoft.Storage/storageAccounts/read",
 "Microsoft.Storage/storageAccounts/write"
 ],
 "notActions": [],
 "dataActions": [
 "Microsoft.Storage/storageAccounts/blobServices/containers/blobs/delete",
 "Microsoft.Storage/storageAccounts/blobServices/containers/blobs/read",
 "Microsoft.Storage/storageAccounts/blobServices/containers/blobs/write",
 "Microsoft.Storage/storageAccounts/blobServices/containers/blobs/add/action"
 ],
 "notDataActions": []
 }
 ],
 "roleName": "VM Restore Operator",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Windows 365 Network Interface Contributor

This role is used by Windows 365 to provision required network resources and join Microsoft-hosted VMs to network interfaces.

Learn more

Actions
Description

Microsoft.Resources/subscriptions/resourcegroups/read
Gets or lists resource groups.

Microsoft.Resources/deployments/read
Gets or lists deployments.

Microsoft.Resources/deployments/write
Creates or updates an deployment.

Microsoft.Resources/deployments/delete
Deletes a deployment.

Microsoft.Resources/deployments/operations/read
Gets or lists deployment operations.

Microsoft.Resources/deployments/operationstatuses/read
Gets or lists deployment operation statuses.

Microsoft.Network/locations/operations/read
Gets operation resource that represents status of an asynchronous operation

Microsoft.Network/locations/operationResults/read
Gets operation result of an async POST or DELETE operation

Microsoft.Network/locations/usages/read
Gets the resources usage metrics

Microsoft.Network/networkInterfaces/write
Creates a network interface or updates an existing network interface.

Microsoft.Network/networkInterfaces/read
Gets a network interface definition.

Microsoft.Network/networkInterfaces/delete
Deletes a network interface

Microsoft.Network/networkInterfaces/join/action
Joins a Virtual Machine to a network interface. Not Alertable.

Microsoft.Network/networkInterfaces/effectiveNetworkSecurityGroups/action
Get Network Security Groups configured On Network Interface Of The Vm

Microsoft.Network/networkInterfaces/effectiveRouteTable/action
Get Route Table configured On Network Interface Of The Vm

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
 "description": "This role is used by Windows 365 to provision required network resources and join Microsoft-hosted VMs to network interfaces.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/1f135831-5bbe-4924-9016-264044c00788",
 "name": "1f135831-5bbe-4924-9016-264044c00788",
 "permissions": [
 {
 "actions": [
 "Microsoft.Resources/subscriptions/resourcegroups/read",
 "Microsoft.Resources/deployments/read",
 "Microsoft.Resources/deployments/write",
 "Microsoft.Resources/deployments/delete",
 "Microsoft.Resources/deployments/operations/read",
 "Microsoft.Resources/deployments/operationstatuses/read",
 "Microsoft.Network/locations/operations/read",
 "Microsoft.Network/locations/operationResults/read",
 "Microsoft.Network/locations/usages/read",
 "Microsoft.Network/networkInterfaces/write",
 "Microsoft.Network/networkInterfaces/read",
 "Microsoft.Network/networkInterfaces/delete",
 "Microsoft.Network/networkInterfaces/join/action",
 "Microsoft.Network/networkInterfaces/effectiveNetworkSecurityGroups/action",
 "Microsoft.Network/networkInterfaces/effectiveRouteTable/action"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Windows 365 Network Interface Contributor",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Windows 365 Network User

This role is used by Windows 365 to read virtual networks and join the designated virtual networks.

Learn more

Actions
Description

Microsoft.Network/virtualNetworks/read
Get the virtual network definition

Microsoft.Network/virtualNetworks/subnets/read
Gets a virtual network subnet definition

Microsoft.Network/virtualNetworks/usages/read
Get the IP usages for each subnet of the virtual network

Microsoft.Network/virtualNetworks/subnets/join/action
Joins a virtual network. Not Alertable.

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
 "description": "This role is used by Windows 365 to read virtual networks and join the designated virtual networks.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/7eabc9a4-85f7-4f71-b8ab-75daaccc1033",
 "name": "7eabc9a4-85f7-4f71-b8ab-75daaccc1033",
 "permissions": [
 {
 "actions": [
 "Microsoft.Network/virtualNetworks/read",
 "Microsoft.Network/virtualNetworks/subnets/read",
 "Microsoft.Network/virtualNetworks/usages/read",
 "Microsoft.Network/virtualNetworks/subnets/join/action"
 ],
 "notActions": [],
 "dataActions": [],
 "notDataActions": []
 }
 ],
 "roleName": "Windows 365 Network User",
 "roleType": "BuiltInRole",
 "type": "Microsoft.Authorization/roleDefinitions"
}
`

## Windows Admin Center Administrator Login

Let's you manage the OS of your resource via Windows Admin Center as an administrator.

Learn more

Actions
Description

Microsoft.HybridCompute/machines/*/read

Microsoft.HybridCompute/machines/extensions/*

Microsoft.HybridCompute/machines/upgradeExtensions/action
Upgrades Extensions on Azure Arc machines

Microsoft.HybridCompute/operations/read
Read all Operations for Azure Arc for Servers

Microsoft.Network/networkInterfaces/read
Gets a network interface definition.

Microsoft.Network/loadBalancers/read
Gets a load balancer definition

Microsoft.Network/publicIPAddresses/read
Gets a public IP address definition.

Microsoft.Network/virtualNetworks/read
Get the virtual network definition

Microsoft.Network/networkSecurityGroups/read
Gets a network security group definition

Microsoft.Network/networkSecurityGroups/defaultSecurityRules/read
Gets a default security rule definition

Microsoft.Network/networkWatchers/securityGroupView/action
View the configured and effective network security group rules applied on a VM.

Microsoft.Network/networkSecurityGroups/securityRules/read
Gets a security rule definition

Microsoft.Network/networkSecurityGroups/securityRules/write
Creates a security rule or updates an existing security rule

Microsoft.HybridConnectivity/endpoints/write
Update the endpoint to the target resource.

Microsoft.HybridConnectivity/endpoints/read
Gets the endpoint to the resource.

Microsoft.HybridConnectivity/endpoints/serviceConfigurations/write
Update the service details in the service configurations of the target resource.

Microsoft.HybridConnectivity/endpoints/serviceConfigurations/read
Gets the details about the service to the resource.

Microsoft.HybridConnectivity/endpoints/listManagedProxyDetails/action
Fetches the managed proxy details

Microsoft.Compute/virtualMachines/read
Get the properties of a virtual machine

Microsoft.Compute/virtualMachines/patchAssessmentResults/latest/read
Retrieves the summary of the latest patch assessment operation

Microsoft.Compute/virtualMachines/patchAssessmentResults/latest/softwarePatches/read
Retrieves list of patches assessed during the last patch assessment operation

Microsoft.Compute/virtualMachines/patchInstallationResults/read
Retrieves the summary of the latest patch installation operation

Microsoft.Compute/virtualMachines/patchInstallationResults/softwarePatches/read
Retrieves list of patches attempted to be installed during the last patch installation operation

Microsoft.Compute/virtualMachines/extensions/read
Get the properties of a virtual machine extension

Microsoft.Compute/virtualMachines/instanceView/read
Gets the detailed runtime status of the virtual machine and its resources

Microsoft.Compute/virtualMachines/runCommands/read
Get the properties of a virtual machine run command

Microsoft.Compute/virtualMachines/vmSizes/read
Lists available sizes the virtual machine can be updated to

Microsoft.Compute/locations/publishers/artifacttypes/types/read
Get the properties of a VMExtension Type

Microsoft.Compute/locations/publishers/artifacttypes/types/versions/read
Get the properties of a VMExtension Version

Microsoft.Compute/diskAccesses/read
Get the properties of DiskAccess resource

Microsoft.Compute/galleries/images/read
Gets the properties of Gallery Image

Microsoft.Compute/images/read
Get the properties of the Image

Microsoft.AzureStackHCI/Clusters/Read
Gets clusters

Microsoft.AzureStackHCI/Clusters/ArcSettings/Read
Gets Arc resource of Azure Local cluster

Microsoft.AzureStackHCI/Clusters/ArcSettings/Extensions/Read
Gets extension resource of HCI cluster

Microsoft.AzureStackHCI/Clusters/ArcSettings/Extensions/Write
Create or update extension resource of HCI cluster

Microsoft.AzureStackHCI/Clusters/ArcSettings/Extensions/Delete
Delete extension resources of Azure Local cluster

Microsoft.AzureStackHCI/Operations/Read
Gets operations

Microsoft.ConnectedVMwarevSphere/VirtualMachines/Read
Read virtualmachines

Microsoft.ConnectedVMwarevSphere/VirtualMachines/Extensions/Write
Write extension resource

Microsoft.ConnectedVMwarevSphere/VirtualMachines/Extensions/Read
Gets extension resource

NotActions

none

DataActions

Microsoft.HybridCompute/machines/WACLoginAsAdmin/action
Lets you manage the OS of your resource via Windows Admin Center as an administrator.

Microsoft.Compute/virtualMachines/WACloginAsAdmin/action
Lets you manage the OS of your resource via Windows Admin Center as an administrator

Microsoft.AzureStackHCI/Clusters/WACloginAsAdmin/Action
Manage OS of Azure Local resource via Windows Admin Center as an administrator

Microsoft.ConnectedVMwarevSphere/virtualmachines/WACloginAsAdmin/action
Lets you manage the OS of your resource via Windows Admin Center as an administrator.

NotDataActions

none

`{
 "assignableScopes": [
 "/"
 ],
 "description": "Let's you manage the OS of your resource via Windows Admin Center as an administrator.",
 "id": "/providers/Microsoft.Authorization/roleDefinitions/a6333a3e-0164-44c3-b281-7a577aff287f",
 "name": "a6333a3e-0164-44c3-b281-7a577aff287f",
 "permissions": [
 {
 "actions": [
 "Microsoft.HybridCompute/machines/*/read",
 "Microsoft.HybridCompute/machines/extensions/*",
 "Microsoft.HybridCompute/machines/upgradeExtensions/action",
 "Microsoft.HybridCompute/operations/read",
 "Microsoft.Network/networkInterfaces/read",
 "Microsoft.Network/loadBalancers/read",
 "Microsoft.Network/publicIPAddresses/read",
 "Microsoft.Network/virtualNetworks/read",
 "Microsoft.Network/networkSecurityGroups/read",
 "Microsoft.Network/networkSecurityGroups/defaultSecurityRules/read",
 "Microsoft.Network/networkWatchers/securityGroupView/action",
 "Microsoft.Network/networkSecurityGroups/securityRules/read",
 "Microsoft.Network/networkSecurityGroups/securityRules/write",
 "Microsoft.HybridConnectivity/endpoints/write",
 "Microsoft.HybridConnectivity/endpoints/read",
 "Microsoft.HybridConnectivity/endpoints/serviceConfigurations/write",
 "Microsoft.HybridConnectivity/endpoints/serviceConfigurations/read",
 "Microsoft.HybridConnectivity/endpoints/listManagedProxyDetails/action",
 "Microsoft.Compute/virtualMachines/read",
 "Microsoft.Compute/virtualMachines/patchAssessmentResults/latest/read",
 "Microsoft.Compute/virtualMachines/patchAssessmentResults/latest/softwarePatches/read",
 "Microsoft.Compute/virtualMachines/patchInstallationResults/read",
 "Microsoft.Compute/virtualMachines/patchInstallationResults/softwarePatches/read",
 "Microsoft.Compute/virtualMachines/extensions/read",
 "Microsoft.Compute/virtualMachines/instanceView/read",
 "Microsoft.Compute/virtualMachines/runCommands/read",
 "Microsoft.Compute/virtualMachines/vmSizes/read",
 "Microsoft.Compute/locations/publishers/artifacttypes/types/read",
 "Microsoft.Compute/locations/publishers/artifacttypes/types/versions/read",
 "Microsoft.Compute/diskAccesses/read",
 "Microsoft.Compute/galleries/images/read",
 "Microsoft.Compute/images/read",
 "Microsoft.AzureStackHCI/Clusters/Read",
 "Microsoft.AzureStackHCI/Clusters/ArcSettings/Read",
 "Microsoft.AzureStackHCI/Clusters/ArcSettings/Extensions/Read",
 "Microsoft.AzureStackHCI/Clusters/ArcSettings/Extensions/Write",
 "Microsoft.AzureStackHCI/Clusters/ArcSettings/Extensions/Delete",
 "Microsoft.AzureStackHCI/Operations/Read",
 "Microsoft.ConnectedVMwarevSphere/VirtualMachines/Read",
 "Microsoft.ConnectedVMwarevSphere/VirtualMachines/Extensions/Write",
 "Microsoft.ConnectedVMwarevSphere/VirtualMachines/Extensions/Read"
 ],
 "notActions": [],
 "dataActions": [
 "Microsoft.HybridCompute/machines/WACLoginAsAdmin/action",
 "Microsoft.Compute/virtualMachines/WACloginAsAdmin/action",
 "Microsoft.AzureStackHCI/Clusters/WACloginAsAdmin/Action",
 "Microsoft.ConnectedVMwarevSphere/virtualmachines/WACloginAsAdmin/action"
 ],
 "notDataActions": []
 }
 ],
 "roleName": "Windows Admin Center Administrator Login",
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
