# https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/deployment-stacks

Source: https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/deployment-stacks

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
 

 

 

 

 
 
# Create and deploy Azure deployment stacks in Bicep

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 An Azure deployment stack is a resource that enables you to manage a group of Azure resources as a single, cohesive unit. When you submit a Bicep file or an Azure Resource Manager JSON template (ARM JSON template) to a deployment stack, you define the resources that the stack manages. If you remove a resource from the template, it can be detached or deleted based on the specified actionOnUnmanage behavior of the deployment stack. You can restrict access to the deployment stack using Azure role-based access control (Azure RBAC), similar to other Azure resources.

To create and update a deployment stack, use the Azure CLI, Azure PowerShell, or the Azure portal with Bicep files. The stack transpiles these Bicep files into ARM JSON templates and deploys them as a deployment object. The deployment stack offers additional capabilities beyond the familiar deployment resources and is a superset of those capabilities.

`Microsoft.Resources/deploymentStacks` is the resource type for deployment stacks. It consists of a main template that can perform one-to-many updates across scopes to the resources it describes and block any unwanted changes to those resources.

When planning your deployment and determining which resource groups should be part of the same stack, consider the management lifecycle of those resources, which includes creation, updating, and deletion. For example, you might need to provision some test virtual machines for various application teams across different resource group scopes. You can use a deployment stack to create these test environments and update the test virtual machine configurations through subsequent updates to the deployment stack. After completing the project, you might need to remove or delete any resources that you created, such as the test virtual machines. Use a deployment stack and specify the appropriate delete flag to remove managed resources. This streamlined approach saves time during environment cleanup, as it involves a single update to the stack resource rather than individually modifying or removing each test virtual machine across various resource group scopes.

Deployment stacks require Azure PowerShell version 12.0.0 or later or Azure CLI version 2.61.0 or later.

To create your first deployment stack, work through Quickstart: create deployment stack.

## Why use deployment stacks?

Deployment stacks provide the following benefits:

- Streamlined provisioning and management of resources across different scopes as a unified entity.

- Prevention of undesired modifications to managed resources via deny settings.

- Efficient environment cleanup using delete flags during deployment stack updates.

- Use of standard templates such as Bicep, ARM templates, or template specs for your deployment stacks.

### Known issues and limitations

For known limitations, known issues, and recommended workarounds, see Known issues for deployment stacks.

## Built-in roles

Warning

Enforcement of the RBAC permission Microsoft.Resources/deploymentStacks/manageDenySetting/action is rolling out across regions, including Government Clouds.

There are two built-in roles for deployment stack:

- Azure Deployment Stack Contributor: Users can manage deployment stacks, but can't create or delete deny-assignments within the deployment stacks.

- Azure Deployment Stack Owner: Users can manage deployment stacks, including those users with deny-assignments.

## Create deployment stacks

You can create a deployment stack resource at resource group, subscription, or management group scope. The template you provide with a deployment stack defines the resources to create or update at the target scope.

- A stack at resource group scope can deploy the template to the same resource group where the deployment stack exists.

- A stack at subscription scope can deploy the template to a resource group or to the same subscription where the deployment stack exists.

- A stack at management group scope can deploy the template to the subscription.

It's important to note that where a deployment stack exists, so is the deny-assignment created with the deny settings capability. For example, by creating a deployment stack at subscription scope that deploys the template to resource group scope and with deny settings mode `DenyDelete`, you can easily provision managed resources to the specified resource group and block delete attempts to those resources. This approach helps you enhance the security of the deployment stack by separating it at the subscription level instead of at the resource-group level. This separation ensures that the developer teams working with the provisioned resources only have visibility and write access to the resource groups. The deployment stack remains isolated at a higher level. This configuration minimizes the number of users that can edit a deployment stack and make changes to its deny-assignment. For more information, see Protect managed resource against deletion.

You can also use the create-stack commands to update deployment stacks.

To create a deployment stack at the resource group scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`New-AzResourceGroupDeploymentStack `
 -Name "<deployment-stack-name>" `
 -ResourceGroupName "<resource-group-name>" `
 -TemplateFile "<bicep-file-name>" `
 -ActionOnUnmanage "detachAll" `
 -DenySettingsMode "none"
`

`az stack group create \
 --name '<deployment-stack-name>' \
 --resource-group '<resource-group-name>' \
 --template-file '<bicep-file-name>' \
 --action-on-unmanage 'detachAll' \
 --deny-settings-mode 'none'
`

This feature isn't implemented at this time.

To create a deployment stack at the subscription scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`New-AzSubscriptionDeploymentStack `
 -Name "<deployment-stack-name>" `
 -Location "<location>" `
 -TemplateFile "<bicep-file-name>" `
 -DeploymentResourceGroupName "<resource-group-name>" `
 -ActionOnUnmanage "detachAll" `
 -DenySettingsMode "none"
`

The `DeploymentResourceGroupName` parameter specifies the resource group used to store the managed resources. If you don't specify the parameter, the managed resources are stored in the subscription scope.

`az stack sub create \
 --name '<deployment-stack-name>' \
 --location '<location>' \
 --template-file '<bicep-file-name>' \
 --deployment-resource-group' <resource-group-name>' \
 --action-on-unmanage 'detachAll' \
 --deny-settings-mode 'none'
`

The `deployment-resource-group` parameter specifies the resource group used to store the managed resources. If you don't specify the parameter, the managed resources are stored in the subscription scope.

This feature isn't implemented at this time.

To create a deployment stack at the management group scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Portal

`New-AzManagementGroupDeploymentStack `
 -Name "<deployment-stack-name>" `
 -Location "<location>" `
 -TemplateFile "<bicep-file-name>" `
 -DeploymentSubscriptionId "<subscription-id>" `
 -ActionOnUnmanage "detachAll" `
 -DenySettingsMode "none"
`

The `deploymentSubscriptionId` parameter specifies the subscription used to store the managed resources. If you don't specify the parameter, the managed resources are stored in the management group scope.

`az stack mg create \
 --name '<deployment-stack-name>' \
 --location '<location>' \
 --template-file '<bicep-file-name>' \
 --deployment-subscription '<subscription-id>' \
 --action-on-unmanage 'detachAll' \
 --deny-settings-mode 'none'
`

The `deployment-subscription` parameter specifies the subscription used to store the managed resources. If you don't specify the parameter, the managed resources are stored in the management group scope.

This feature isn't implemented at this time.

## List deployment stacks

To list deployment stack resources at the resource group scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`Get-AzResourceGroupDeploymentStack `
 -ResourceGroupName "<resource-group-name>"
`

`az stack group list \
 --resource-group '<resource-group-name>'
`

- From the Azure portal, open the resource group that contains the deployment stacks.

- From the left menu, select `Deployment stacks` to list the deployment stacks deployed to the resource group.

To list deployment stack resources at the subscription scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`Get-AzSubscriptionDeploymentStack
`

`az stack sub list
`

- From the Azure portal, open the subscription that contains the deployment stacks.

- From the left menu, select `Deployment stacks` to list the deployment stacks deployed to the subscription.

To list deployment stack resources at the management group scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`Get-AzManagementGroupDeploymentStack `
 -ManagementGroupId "<management-group-id>"
`

`az stack mg list \
 --management-group-id '<management-group-id>'
`

This feature isn't implemented at this time.

## Update deployment stacks

To update a deployment stack, which might involve adding or deleting a managed resource, you need to make changes to the underlying Bicep files. Once you make the modifications, you can update the deployment stack by either running the update command or rerunning the create command.

The infrastructure-as-code design pattern gives you full control over the list of managed resources.

### Use the Set command

To update a deployment stack at the resource group scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`Set-AzResourceGroupDeploymentStack `
 -Name "<deployment-stack-name>" `
 -ResourceGroupName "<resource-group-name>" `
 -TemplateFile "<bicep-file-name>" `
 -ActionOnUnmanage "detachAll" `
 -DenySettingsMode "none"
`

`az stack group create \
 --name '<deployment-stack-name>' \
 --resource-group '<resource-group-name>' \
 --template-file '<bicep-file-name>' \
 --action-on-unmanage 'detachAll' \
 --deny-settings-mode 'none'
`

Note

The Azure CLI doesn't have a deployment stack set command. Use the New command instead.

This feature isn't implemented at this time.

To update a deployment stack at the subscription scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`Set-AzSubscriptionDeploymentStack `
 -Name "<deployment-stack-name>" `
 -Location "<location>" `
 -TemplateFile "<bicep-file-name>" `
 -DeploymentResourceGroupName "<resource-group-name>" `
 -ActionOnUnmanage "detachAll" `
 -DenySettingsMode "none"
`

The `DeploymentResourceGroupName` parameter specifies the resource group used to store the deployment stack resources. If you don't specify a resource group name, the deployment stack service creates a new resource group for you.

`az stack sub create \
 --name '<deployment-stack-name>' \
 --location '<location>' \
 --template-file '<bicep-file-name>' \
 --deployment-resource-group '<resource-group-name>' \
 --action-on-unmanage 'detachAll' \
 --deny-settings-mode 'none'
`

This feature isn't implemented at this time.

To update a deployment stack at the management group scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`Set-AzManagementGroupDeploymentStack `
 -Name "<deployment-stack-name>" `
 -Location "<location>" `
 -TemplateFile "<bicep-file-name>" `
 -DeploymentSubscriptionId "<subscription-id>" `
 -ActionOnUnmanage "detachAll" `
 -DenySettingsMode "none"
`

`az stack mg create \
 --name '<deployment-stack-name>' \
 --location '<location>' \
 --template-file '<bicep-file-name>' \
 --deployment-subscription '<subscription-id>' \
 --action-on-unmanage 'detachAll' \
 --deny-settings-mode 'none'
`

This feature isn't implemented at this time.

### Use the New command

You get a warning similar to the following one:

`The deployment stack 'myStack' you're trying to create already exists in the current subscription/management group/resource group. Do you want to overwrite it? Detaching: resources, resourceGroups (Y/N)
`

For more information, see Create deployment stacks.

### Control detachment and deletion

A detached resource (or unmanaged resource) refers to a resource that the deployment stack doesn't track or manage but still exists within Azure.

To instruct Azure to delete unmanaged resources, update the stack with the create stack command and include the `ActionOnUnmanage` switch. For more information, see Create deployment stack.

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

Use the `ActionOnUnmanage` switch to define what happens to resources that are no longer managed after a stack is updated or deleted. Allowed values are:

- `deleteAll`: Use delete rather than detach for managed resources and resource groups.

- `deleteResources`: Use delete rather than detach for managed resources only.

- `detachAll`: Detach the managed resources and resource groups.

For example:

`New-AzSubscriptionDeploymentStack `
 -Name "<deployment-stack-name" `
 -TemplateFile "<bicep-file-name>" `
 -DenySettingsMode "none" `
 -ActionOnUnmanage "deleteAll" 
`

Use the `action-on-unmanage` switch to define what happens to resources that are no longer managed after a stack is updated or deleted. Allowed values are:

- `deleteAll`: Use delete rather than detach for managed resources and resource groups.

- `deleteResources`: Use delete rather than detach for managed resources only.

- `detachAll`: Detach the managed resources and resource groups.

For example:

`az stack sub create `
 --name '<deployment-stack-name>' `
 --location '<location>' `
 --template-file '<bicep-file-name>' `
 --action-on-unmanage 'deleteAll' `
 --deny-settings-mode 'none' 
`

This feature isn't implemented.

Warning

When deleting resource groups with the `action-on-unmanage` switch set to `deleteAll`, you delete the managed resource groups and all the resources contained within them.

### Handle the stack-out-of-sync error

When updating or deleting a deployment stack, you might encounter the following stack-out-of-sync error, indicating the stack resource list isn't correctly synchronized.

`The deployment stack '{0}' might not have an accurate list of managed resources. To prevent resources from being accidentally deleted, check that the managed resource list doesn't have any additional values. If there is any uncertainty, it's recommended to redeploy the stack with the same template and parameters as the current iteration. To bypass this warning, specify the 'BypassStackOutOfSyncError' flag.
`

You can obtain a list of the resources from the Azure portal or redeploy the currently deployed Bicep file with the same parameters. The output shows the managed resources.

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`...
Resources: /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/demoRg/providers/Microsoft.Network/virtualNetworks/vnetthmimleef5fwk
 /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/demoRg/providers/Microsoft.Storage/storageAccounts/storethmimleef5fwk
`

`"resources": [
 {
 "denyStatus": "none",
 "id": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/demoRg/providers/Microsoft.Network/virtualNetworks/vnetthmimleef5fwk",
 "resourceGroup": "demoRg",
 "status": "managed"
 },
 {
 "denyStatus": "none",
 "id": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/demoRg/providers/Microsoft.Storage/storageAccounts/storethmimleef5fwk",
 "resourceGroup": "demoRg",
 "status": "managed"
 }
]
`

- Open the Azure portal.

- Open the resource group that contains the stack.

- From the left menu, expand Settings, and then select Deployment stacks.

- Select the stack name to open the stack.

After you review and verify the list of resources in the stack, rerun the command with the `BypassStackOutOfSyncError` switch in Azure PowerShell (or `bypass-stack-out-of-sync-error` in Azure CLI). Use this switch only after thoroughly reviewing the list of resources in the stack. Don't use this switch by default.

## Delete deployment stacks

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

The `ActionOnUnmanage` switch defines the action to the resources that are no longer managed. The switch has the following values:

- `DeleteAll`: Delete both the resources and the resource groups.

- `DeleteResources`: Delete only the resources.

- `DetachAll`: Detach the resources.

The `action-on-unmanage` switch defines the action to the resources that are no longer managed. The switch has the following values:

- `delete-all`: Delete both the resources and the resource groups.

- `delete-resources`: Delete only the resources.

- `detach-all`: Detach the resources.

Select one of the delete flags when you delete a deployment stack.

Even if you specify the delete-all switch, unmanaged resources within the resource group where the deployment stack is located prevent both the unmanaged resources and the resource group itself from being deleted.

To delete deployment stack resources at the resource group scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`Remove-AzResourceGroupDeploymentStack `
 -name "<deployment-stack-name>" `
 -ResourceGroupName "<resource-group-name>" `
 -ActionOnUnmanage "<deleteAll/deleteResources/detachAll>"
`

`az stack group delete \
 --name '<deployment-stack-name>' \
 --resource-group '<resource-group-name>' \
 --action-on-unmanage '<deleteAll/deleteResources/detachAll>'
`

- From the Azure portal, open the resource group that contains the deployment stacks.

- From the left menu, select `Deployment stacks`, select the deployment stack to delete, and then select `Delete stack`.

- Select an `Update behavior`, and then select `Next`.

To delete deployment stack resources at the subscription scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`Remove-AzSubscriptionDeploymentStack `
 -Name "<deployment-stack-name>" `
 -ActionOnUnmanage "<deleteAll/deleteResources/detachAll>"
`

`az stack sub delete \
 --name '<deployment-stack-name>' \
 --action-on-unmanage '<deleteAll/deleteResources/detachAll>'
`

- From the Azure portal, open the subscription that contains the deployment stacks.

- From the left menu, select `Deployment stacks`, select the deployment stack to delete, and then select `Delete stack`.

- Select an `Update behavior` (delete flag), and then select `Next`.

To delete deployment stack resources at the management group scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`Remove-AzManagementGroupDeploymentStack `
 -Name "<deployment-stack-name>" `
 -ManagementGroupId "<management-group-id>" `
 -ActionOnUnmanage "<deleteAll/deleteResources/detachAll>"
`

`az stack mg delete \
 --name '<deployment-stack-name>' \
 --management-group-id '<management-group-id>' \
 --action-on-unmanage '<deleteAll/deleteResources/detachAll>'
`

This feature isn't implemented at this time.

## View managed resources in deployment stack

The deployment stack service doesn't yet have an Azure portal graphical user interface (GUI). To view the managed resources inside a deployment stack, use the following Azure PowerShell/Azure CLI commands:

To view managed resources at the resource group scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`(Get-AzResourceGroupDeploymentStack -Name "<deployment-stack-name>" -ResourceGroupName "<resource-group-name>").Resources
`

`az stack group list \
 --name '<deployment-stack-name>' \
 --resource-group '<resource-group-name>' \
 --output 'json'
`

- From the Azure portal, open the resource group that contains the deployment stacks.

- From the left menu, select `Deployment stacks`.

- Select one of the deployment stacks to view the managed resources of the deployment stack.

To view managed resources at the subscription scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`(Get-AzSubscriptionDeploymentStack -Name "<deployment-stack-name>").Resources
`

`az stack sub show \
 --name '<deployment-stack-name>' \
 --output 'json'
`

- From the Azure portal, open the subscription that contains the deployment stacks.

- From the left menu, select `Deployment stacks` to list the deployment stacks deployed to the subscription.

- Select the deployment stack to list the managed resources.

To view managed resources at the management group scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`(Get-AzManagementGroupDeploymentStack -Name "<deployment-stack-name>" -ManagementGroupId "<management-group-id>").Resources
`

`az stack mg show \
 --name '<deployment-stack-name>' \
 --management-group-id '<management-group-id>' \
 --output 'json'
`

This feature isn't implemented at this time.

## Add resources to deployment stack

To add a managed resource, add the resource definition to the underlying Bicep files, and then run the update command or rerun the create command. For more information, see Update deployment stacks.

## Delete managed resources from deployment stack

To delete a managed resource, remove the resource definition from the underlying Bicep files, and then run the update command or rerun the create command. For more information, see Update deployment stacks.

## Protect managed resources

You can assign specific permissions to the managed resources of a deployment stack to prevent unauthorized security principals from deleting or updating them. These permissions are referred to as deny settings. Store stacks at parent scope. For example, to protect resources in a subscription, place the stack at the parent scope, which is the immediate parent management group.

The deny setting only applies to the control plane operations and not the data plane operations. For example, you create storage accounts and key vaults through the control plane, which means the deployment stack manages them. However, you create child resources like secrets or blob containers through the data plane, which means deployment stack can't manage them.

The deny setting only applies to explicitly created resources, not implicitly created ones. For example, a managed AKS cluster creates multiple other services to support it, such as a virtual machine. In this case, since the virtual machine isn't defined in the Bicep file and is an implicitly created resource, it isn't subject to the deployment stack deny settings.

Note

The latest release requires specific permissions at the stack scope to:

- Create or update a deployment stack, and configure deny setting to a value other than `None`.

- Update or delete a deployment stack with an existing deny setting of a value other than `None`.

Use the deployment stack built-in roles to grant permissions.

- 
PowerShell

- 
CLI

- 
Portal

The Azure PowerShell includes these parameters to customize the deny-assignment:

- `DenySettingsMode`: Defines the operations that are prohibited on the managed resources to safeguard against unauthorized security principals attempting to delete or update them. This restriction applies to everyone unless you explicitly grant access. The values include: `None`, `DenyDelete`, and `DenyWriteAndDelete`.

- `DenySettingsApplyToChildScopes`: When specified, the deny setting mode configuration also applies to the child scope of the managed resources, which includes child resources that the stack doesn't manage. Without this switch, the deny settings don't apply to those child resources. For example, a Bicep file defines a Microsoft.Sql/servers resource (parent) and a Microsoft.Sql/servers/databases resource (child). If you create a deployment stack by using the Bicep file with the `DenySettingsApplyToChildScopes` setting enabled and the `DenySettingsMode` set to `DenyWriteAndDelete`, you can't add any extra child resources to either the Microsoft.Sql/servers resource or the Microsoft.Sql/servers/databases resource.

- `DenySettingsExcludedAction`: List of role-based management operations that are excluded from the deny settings. Up to 200 actions are permitted.

- `DenySettingsExcludedPrincipal`: List of Microsoft Entra principal IDs excluded from the lock. Up to five principals are permitted.

The Azure CLI includes these parameters to customize the deny-assignment:

- `deny-settings-mode`: Defines the operations that are prohibited on the managed resources to safeguard against unauthorized security principals attempting to delete or update them. This restriction applies to everyone unless they're explicitly granted access. The values include: `none`, `denyDelete`, and `denyWriteAndDelete`.

- `deny-settings-apply-to-child-scopes`: When specified, the deny setting mode configuration also applies to the child scope of the managed resources, which includes child resources that the stack doesn't manage. Without this parameter, the deny settings don't apply to those child resources. For example, a Bicep file defines a Microsoft.Sql/servers resource (parent) and a Microsoft.Sql/servers/databases resource (child). If you create a deployment stack by using the Bicep file with the `deny-settings-apply-to-child-scopes` setting enabled and the `deny-settings-mode` set to `denyWriteAndDelete`, you can't add any extra child resources to either the Microsoft.Sql/servers resource or the Microsoft.Sql/servers/databases resource.

- `deny-settings-excluded-actions`: List of RBAC management operations excluded from the deny settings. Up to 200 actions are allowed.

- `deny-settings-excluded-principals`: List of Microsoft Entra principal IDs excluded from the lock. Up to five principals are allowed.

This feature isn't implemented at this time.

### Exclude principals from deny settings

Use the excluded principals setting (`DenySettingsExcludedPrincipal` in Azure PowerShell, `deny-settings-excluded-principals` in Azure CLI) to exempt specific identities from the deny setting. The setting accepts the Microsoft Entra object ID of any principal type, including:

- Users

- Microsoft Entra groups (for example, security groups)

- Service principals

- Managed identities

When you exclude a group, the deny setting doesn't apply to the principals in that group. Managing exclusions through group membership is the recommended approach, because you can change who's excluded by updating the group rather than updating the deployment stack. Identities that are commonly excluded include CI/CD service connections and workload identities, platform team or break-glass administrator groups, and policy remediation identities.

Important

You can exclude a maximum of five principals. Specifying more than five principals doesn't return an error, so confirm that the list contains no more than five entries. To exclude more identities than the limit allows, consolidate them into one or more Microsoft Entra groups and exclude the groups instead of the individual principals.

When you exclude a group, the deny setting is evaluated against that group's membership. If you use nested groups, test the configuration to confirm that the principals you intend to exclude are exempted before you rely on the deny setting.

To apply deny settings at the resource group scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`New-AzResourceGroupDeploymentStack `
 -Name "<deployment-stack-name>" `
 -ResourceGroupName "<resource-group-name>" `
 -TemplateFile "<bicep-file-name>" `
 -ActionOnUnmanage "detachAll" `
 -DenySettingsMode "denyDelete" `
 -DenySettingsExcludedAction "Microsoft.Compute/virtualMachines/write Microsoft.StorageAccounts/delete" `
 -DenySettingsExcludedPrincipal "<object-id>,<object-id>"
`

`az stack group create \
 --name '<deployment-stack-name>' \
 --resource-group '<resource-group-name>' \
 --template-file '<bicep-file-name>' \
 --action-on-unmanage 'detachAll' \
 --deny-settings-mode 'denyDelete' \
 --deny-settings-excluded-actions 'Microsoft.Compute/virtualMachines/write Microsoft.StorageAccounts/delete' \
 --deny-settings-excluded-principals '<object-id> <object-id>'
`

This feature isn't implemented at this time.

To apply deny settings at the subscription scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`New-AzSubscriptionDeploymentStack `
 -Name "<deployment-stack-name>" `
 -Location "<location>" `
 -TemplateFile "<bicep-file-name>" `
 -ActionOnUnmanage "detachAll" `
 -DenySettingsMode "denyDelete" `
 -DenySettingsExcludedAction "Microsoft.Compute/virtualMachines/write Microsoft.StorageAccounts/delete" `
 -DenySettingsExcludedPrincipal "<object-id>,<object-id>"
`

Use the `DeploymentResourceGroupName` parameter to specify the resource group name at which the deployment stack is created. If a scope isn't specified, it uses the scope of the deployment stack.

`az stack sub create \
 --name '<deployment-stack-name>' \
 --location '<location>' \
 --template-file '<bicep-file-name>' \
 --action-on-unmanage 'detachAll' \
 --deny-settings-mode 'denyDelete' \
 --deny-settings-excluded-actions 'Microsoft.Compute/virtualMachines/write Microsoft.StorageAccounts/delete' \
 --deny-settings-excluded-principals '<object-id> <object-id>'
`

Use the `deployment-resource-group` parameter to specify the resource group at which the deployment stack is created. If a scope isn't specified, it uses the scope of the deployment stack.

This feature isn't implemented.

To apply deny settings at the management group scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`New-AzManagementGroupDeploymentStack `
 -Name "<deployment-stack-name>" `
 -Location "<location>" `
 -TemplateFile "<bicep-file-name>" `
 -ActionOnUnmanage "detachAll" `
 -DenySettingsMode "denyDelete" `
 -DenySettingsExcludedActions "Microsoft.Compute/virtualMachines/write Microsoft.StorageAccounts/delete" `
 -DenySettingsExcludedPrincipal "<object-id>,<object-id>"
`

Use the `DeploymentSubscriptionId ` parameter to specify the subscription ID at which the deployment stack is created. If a scope isn't specified, it uses the scope of the deployment stack.

`az stack mg create \
 --name '<deployment-stack-name>' \
 --location '<location>' \
 --template-file '<bicep-file-name>' \
 --action-on-unmanage 'detachAll' \
 --deny-settings-mode 'denyDelete' \
 --deny-settings-excluded-actions 'Microsoft.Compute/virtualMachines/write Microsoft.StorageAccounts/delete' \
 --deny-settings-excluded-principals '<object-id> <object-id>'
`

Use the `deployment-subscription ` parameter to specify the subscription ID at which the deployment stack is created. If a scope isn't specified, it uses the scope of the deployment stack.

This feature isn't implemented.

## Detach managed resources from deployment stack

By default, deployment stacks detach and don't delete unmanaged resources when they're no longer contained within the stack's management scope. For more information, see Update deployment stacks.

## Export templates from deployment stacks

You can export the resources from a deployment stack to a JSON output. You can pipe the output to a file.

To export a deployment stack at the resource group scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Portal

`Save-AzResourceGroupDeploymentStack `
 -Name "<deployment-stack-name>" `
 -ResourceGroupName "<resource-group-name>" `
`

`az stack group export \
 --name '<deployment-stack-name>' \
 --resource-group '<resource-group-name>'
`

This feature isn't implemented at this time.

To export a deployment stack at the subscription scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`Save-AzSubscriptionDeploymentStack `
 -name "<deployment-stack-name>"
`

`az stack sub export \
 --name '<deployment-stack-name>'
`

This feature isn't implemented at this time.

To export a deployment stack at the management group scope:

- 
Azure PowerShell

- 
Azure CLI

- 
Azure portal

`Save-AzManagementGroupDeploymentStack `
 -Name "<deployment-stack-name>" `
 -ManagementGroupId "<management-group-id>"
`

`az stack mg export \
 --name '<deployment-stack-name>' \
 --management-group-id '<management-group-id>'
`

This feature isn't implemented at this time.

## Next steps

To go through a Bicep deployment quickstart, see Quickstart: Create and deploy a deployment stack with Bicep.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-09
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
