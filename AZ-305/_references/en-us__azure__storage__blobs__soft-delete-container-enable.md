# https://learn.microsoft.com/en-us/azure/storage/blobs/soft-delete-container-enable

Source: https://learn.microsoft.com/en-us/azure/storage/blobs/soft-delete-container-enable

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
 

 

 

 

 
 
# Enable and manage soft delete for containers

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Container soft delete protects your data from being accidentally or erroneously modified or deleted. When you enable container soft delete for a storage account, you can recover a deleted container and its contents within a retention period that you specify. For more details about container soft delete, see Soft delete for containers.

For end-to-end data protection, Microsoft recommends that you also enable soft delete for blobs and blob versioning. To learn how to enable soft delete for blobs, see Enable and manage soft delete for blobs. To learn how to enable blob versioning, see Blob versioning.

## Enable container soft delete

You can enable or disable container soft delete for the storage account at any time by using Azure built-in policy, Azure portal, PowerShell, Azure CLI, or an Azure Resource Manager template. Microsoft recommends setting the retention period for container soft delete to a minimum of seven days.

To enable blob and container soft delete at scale via Azure built-in policy, reference Configure soft delete for blobs and containers on storage accounts.

- 
Portal

- 
PowerShell

- 
Azure CLI

- 
Template

To enable container soft delete for your storage account by using Azure portal, follow these steps:

- In the Azure portal, navigate to your storage account.

- Locate the Data protection settings under Data management.

- Select Enable soft delete for containers.

- Specify a retention period between 1 and 365 days.

- Save your changes.

To enable container soft delete with PowerShell, first install the Az.Storage module, version 3.9.0 or later. Next, call the Enable-AzStorageContainerDeleteRetentionPolicy command and specify the number of days for the retention period. Replace the values in angle brackets with your own values:

`Enable-AzStorageContainerDeleteRetentionPolicy -ResourceGroupName <resource-group> `
 -StorageAccountName <storage-account> `
 -RetentionDays 7
`

To check the current settings for container soft delete, call the Get-AzStorageBlobServiceProperty command:

`$properties = Get-AzStorageBlobServiceProperty -ResourceGroupName <resource-group> `
 -StorageAccountName <storage-account>
$properties.ContainerDeleteRetentionPolicy.Enabled
$properties.ContainerDeleteRetentionPolicy.Days
`

To disable container soft delete, call the Disable-AzStorageContainerDeleteRetentionPolicy command.

To enable container soft delete with Azure CLI, first install Azure CLI, version 2.26.0 or later. Next, call the az storage account blob-service-properties update command and specify the number of days for the retention period. Replace the values in angle brackets with your own values:

`az storage account blob-service-properties update \
 --enable-container-delete-retention true \
 --container-delete-retention-days 7 \
 --account-name <storage-account> \
 --resource-group <resource_group>
`

To check the current settings for container soft delete, call the az storage account blob-service-properties show command:

`az storage account blob-service-properties show --account-name <storage-account> \
 --resource-group <resource-group>
`

To disable container soft delete, specify `false` for the `--enable-container-delete-retention` parameter.

To enable container soft delete with an Azure Resource Manager template, create a template that sets the containerDeleteRetentionPolicy property. The following steps describe how to create a template in the Azure portal.

- In the Azure portal, choose Create a resource.

- In Search the Marketplace, type template deployment, and then press ENTER.

- Choose Template deployment, choose Create, and then choose Build your own template in the editor.

- In the template editor, paste the following JSON. Replace the `<account-name>` placeholder with the name of your storage account.

`{
 "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
 "contentVersion": "1.0.0.0",
 "parameters": {},
 "variables": {},
 "resources": [
 {
 "type": "Microsoft.Storage/storageAccounts/blobServices",
 "apiVersion": "2019-06-01",
 "name": "<account-name>/default",
 "properties": {
 "containerDeleteRetentionPolicy": {
 "enabled": true,
 "days": 7
 }
 }
 }
 ]
}
`

- Specify the retention period. The default value is 7.

- Save the template.

- Specify the resource group of the account, and then choose the Review + create button to deploy the template and enable container soft delete.

## View soft-deleted containers

When you enable soft delete, you can view soft-deleted containers in the Azure portal. Soft-deleted containers are visible during the specified retention period. After the retention period expires, a soft-deleted container is permanently deleted and is no longer visible.

To view soft-deleted containers in the Azure portal, follow these steps:

- Go to your storage account in the Azure portal and view the list of your containers.

- Toggle the Show deleted containers switch to include deleted containers in the list.

## Restore a soft-deleted container

You can restore a soft-deleted container and its contents within the retention period. To restore a soft-deleted container in the Azure portal, follow these steps:

- Go to your storage account in the Azure portal and view the list of your containers.

- Open the context menu for the container you want to restore, and select Undelete.

## Next steps

- Soft delete for containers

- Soft delete for blobs

- Blob versioning

 
 

 
 

 

 
 
 
 
 
 
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
 2026-10-05
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
