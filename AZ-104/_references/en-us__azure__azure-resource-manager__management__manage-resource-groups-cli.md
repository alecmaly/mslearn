# https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-cli

Source: https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-cli

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
 

 

 

 

 
 
# Manage Azure resource groups by using Azure CLI

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Learn how to use Azure CLI with Azure Resource Manager to manage your Azure resource groups.

## Prerequisites

- Azure CLI. For more information, see How to install the Azure CLI.

- An authenticated account. After installing Azure CLI, sign in for the first time. For more information, see How to sign in to the Azure CLI.

## What is a resource group

A resource group is a container that holds related resources for an Azure solution. The resource group can include all the resources for the solution, or only those resources that you want to manage as a group. You decide how to add resources to resource groups based on what makes the most sense for your organization. Generally, add resources that share the same lifecycle to the same resource group so you can easily deploy, update, and delete them as a group.

The resource group stores metadata about the resources. When you specify a location for the resource group, you're specifying where that metadata is stored. For compliance reasons, you might need to ensure that your data is stored in a particular region.

## Create resource groups

To create a resource group, use az group create.

`az group create --name demoResourceGroup --location westus
`

## List resource groups

To list the resource groups in your subscription, use az group list.

`az group list
`

To get one resource group, use az group show.

`az group show --name exampleGroup
`

## Delete resource groups

To delete a resource group, use az group delete.

`az group delete --name exampleGroup
`

For more information about how Azure Resource Manager orders the deletion of resources, see Azure Resource Manager resource group deletion.

## Deploy resources

You can deploy Azure resources by using Azure CLI, or by deploying an Azure Resource Manager (ARM) template or Bicep file.

### Deploy resources by using storage operations

The following example creates a storage account. The name you provide for the storage account must be unique across Azure.

`az storage account create --resource-group exampleGroup --name examplestore --location westus --sku Standard_LRS --kind StorageV2
`

### Deploy resources by using an ARM template or Bicep file

To deploy an ARM template or Bicep file, use az deployment group create.

`az deployment group create --resource-group exampleGroup --template-file storage.bicep
`

The following example shows the Bicep file named `storage.bicep` that you're deploying:

`@minLength(3)
@maxLength(11)
param storagePrefix string

var uniqueStorageName = concat(storagePrefix, uniqueString(resourceGroup().id))

resource uniqueStorage 'Microsoft.Storage/storageAccounts@2022-09-01' = {
 name: uniqueStorageName
 location: 'eastus'
 sku: {
 name: 'Standard_LRS'
 }
 kind: 'StorageV2'
 properties: {
 supportsHttpsTrafficOnly: true
 }
}
`

For more information about deploying an ARM template, see Deploy resources with Resource Manager templates and Azure CLI.

For more information about deploying a Bicep file, see Deploy resources with Bicep and Azure CLI.

## Lock resource groups

Locking prevents other users in your organization from accidentally deleting or modifying critical resources.

To prevent a resource group and its resources from being deleted, use az lock create.

`az lock create --name LockGroup --lock-type CanNotDelete --resource-group exampleGroup
`

To get the locks for a resource group, use az lock list.

`az lock list --resource-group exampleGroup
`

To delete a lock, use az lock delete.

`az lock delete --name exampleLock --resource-group exampleGroup
`

For more information, see Lock resources with Azure Resource Manager.

## Tag resource groups

You can apply tags to resource groups and resources to logically organize your assets. For information, see Using tags to organize your Azure resources.

## Export resource groups to templates

To assist with creating ARM templates, you can export a template from existing resources. For more information, see Use Azure CLI to export a template.

## Manage access to resource groups

To manage access to a resource group, use Azure role-based access control (Azure RBAC). For more information, see Add or remove Azure role assignments using Azure CLI.

## Next steps

- To manage Azure resources, see Manage Azure resources by using Azure CLI.

- To learn Azure Resource Manager, see Azure Resource Manager overview.

- To learn the Resource Manager template syntax, see Understand the structure and syntax of Azure Resource Manager templates.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-02-27
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
