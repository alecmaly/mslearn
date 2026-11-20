# https://learn.microsoft.com/en-us/azure/storage/blobs/soft-delete-blob-enable

Source: https://learn.microsoft.com/en-us/azure/storage/blobs/soft-delete-blob-enable

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
 

 

 

 

 
 
# Enable soft delete for blobs

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Blob soft delete protects an individual blob and its versions, snapshots, and metadata from accidental deletes or overwrites by maintaining the deleted data in the system for a specified period of time. During the retention period, you can restore the blob to its state at deletion. After the retention period has expired, the blob is permanently deleted. For more information about blob soft delete, see Soft delete for blobs.

Blob soft delete is part of a comprehensive data protection strategy for blob data. To learn more about Microsoft's recommendations for data protection, see Data protection overview.

## Enable blob soft delete

You can enable or disable soft delete for a storage account at any time by using Azure built-in-policy, Azure portal, PowerShell, or Azure CLI.

To enable blob and container soft delete at scale via Azure built-in policy, reference Configure soft delete for blobs and containers on storage accounts.

- 
Portal

- 
PowerShell

- 
Azure CLI

- 
Template

Blob soft delete is enabled by default when you create a new storage account with the Azure portal. The setting to enable or disable blob soft delete when you create a new storage account is on the Data protection tab. For more information about creating a storage account, see Create a storage account.

To enable blob soft delete for an existing storage account by using the Azure portal, follow these steps:

- In the Azure portal, navigate to your storage account.

- Locate the Data Protection option under Data management.

- In the Recovery section, select Turn on soft delete for blobs.

- Enter a retention period between 1 and 365 days. Microsoft recommends a minimum retention period of seven days.

- Save your changes.

Blob soft delete isn't enabled when you create a new storage account with PowerShell. You can enable blob soft delete after the new account is created.

To enable blob soft delete for an existing storage account with PowerShell, call the Enable-AzStorageBlobDeleteRetentionPolicy command and specify the retention period in days.

The following example enables blob soft delete and sets the retention period to seven days. Replace the placeholder values in brackets with your own values:

`Enable-AzStorageBlobDeleteRetentionPolicy -ResourceGroupName <resource-group> `
 -StorageAccountName <storage-account> `
 -RetentionDays 7
`

To check the current settings for blob soft delete, call the Get-AzStorageBlobServiceProperty command:

`$properties = Get-AzStorageBlobServiceProperty -ResourceGroupName <resource-group> `
 -StorageAccountName <storage-account>
$properties.DeleteRetentionPolicy.Enabled
$properties.DeleteRetentionPolicy.Days
`

Blob soft delete isn't enabled when you create a new storage account with Azure CLI. You can enable blob soft delete after the new account is created.

To enable blob soft delete for an existing storage account with Azure CLI, call the az storage account blob-service-properties update command and specify the retention period in days.

The following example enables blob soft delete and sets the retention period to seven days. Replace the placeholder values in brackets with your own values:

`az storage account blob-service-properties update --account-name <storage-account> \
 --resource-group <resource-group> \
 --enable-delete-retention true \
 --delete-retention-days 7
`

To check the current settings for blob soft delete, call the az storage account blob-service-properties show command:

`az storage account blob-service-properties show --account-name <storage-account> \
 --resource-group <resource-group>
`

To enable blob soft delete with an Azure Resource Manager template, create a template that sets the deleteRetentionPolicy property. The following steps describe how to create a template in the Azure portal.

- In the Azure portal, choose Create a resource.

- In Search the Marketplace, type Deploy a custom template, and then press ENTER.

- Choose Build your own template in the editor.

- In the template editor, paste the following JSON. Replace the `<account-name>` placeholder with the name of your storage account.

` {
 "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
 "contentVersion": "1.0.0.0",
 "parameters": {},
 "variables": {},
 "resources": [
 {
 "type": "Microsoft.Storage/storageAccounts/blobServices",
 "apiVersion": "2023-04-01",
 "name": "<account-name>/default",
 "properties": {
 "deleteRetentionPolicy": {
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

## Enable blob soft delete (hierarchical namespace)

Blob soft delete can also protect blobs and directories in accounts that have the hierarchical namespace feature enabled on them.

- 
Portal

- 
PowerShell

- 
Azure CLI

- 
Template

To enable blob soft delete for your storage account by using the Azure portal, follow these steps:

- In the Azure portal, navigate to your storage account.

- Find the Data Protection option under Data Management.

- In the Recovery section, select Enable soft delete for blobs.

- Enter a retention period between 1 and 365 days. Microsoft recommends a minimum retention period of seven days.

- Save your changes.

- Install the latest PowershellGet module. Then, close and reopen the PowerShell console.

`Install-Module PowerShellGet -Repository PSGallery -Force
`

- Install Az.Storage preview module.

`Install-Module Az.Storage -Repository PsGallery -RequiredVersion 3.7.1-preview -AllowClobber -AllowPrerelease -Force
`

For more information about how to install PowerShell modules, see Install the Azure PowerShell module.

- Obtain storage account authorization by using either a storage account key, a connection string, or Microsoft Entra ID. For more information, see Connect to the account.

The following example obtains authorization by using a storage account key.

`$ctx = New-AzStorageContext -StorageAccountName '<storage-account-name>' -StorageAccountKey '<storage-account-key>'
`

- To enable blob soft delete with PowerShell, use the Enable-AzStorageDeleteRetentionPolicy command, and specify the retention period in days.

The following example enables soft delete for an account, and sets the retention period to 4 days.

`Enable-AzStorageDeleteRetentionPolicy -RetentionDays 4 -Context $ctx
`

- To check the current settings for blob soft delete, use the `Get-AzStorageServiceProperty` command:

` Get-AzStorageServiceProperty -ServiceType Blob -Context $ctx
`

- Open the Azure Cloud Shell, or if you installed the Azure CLI locally, open a command console application such as Windows PowerShell.

- Install the `storage-preview` extension.

`az extension add -n storage-preview
`

- Connect to your storage account. For more information, see Connect to the account.

Note

The following example shows Microsoft Entra authorization. To learn more about authorization methods, see Authorize access to blob or queue data with Azure CLI.

- To enable soft delete with Azure CLI, call the `az storage fs service-properties update` command and specify the retention period in days.

The following example enables blob and directory soft delete and sets the retention period to 5 days.

`az storage fs service-properties update --delete-retention --delete-retention-period 5 --auth-mode login
`

- To check the current settings for blob soft delete, call the `az storage fs service-properties update` command:

`az storage fs service-properties update --delete-retention false --connection-string $con
`

To enable blob soft delete with an Azure Resource Manager template, create a template that sets the deleteRetentionPolicy property. The following steps describe how to create a template in the Azure portal.

- In the Azure portal, choose Create a resource.

- In Search the Marketplace, type Deploy a custom template, and then press ENTER.

- Choose Build your own template in the editor.

- In the template editor, paste the following JSON. Replace the `<account-name>` placeholder with the name of your storage account.

` {
 "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
 "contentVersion": "1.0.0.0",
 "parameters": {},
 "variables": {},
 "resources": [
 {
 "type": "Microsoft.Storage/storageAccounts/blobServices",
 "apiVersion": "2023-04-01",
 "name": "<account-name>/default",
 "properties": {
 "deleteRetentionPolicy": {
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

## Next steps

- Soft delete for blobs

- Manage and restore soft-deleted blobs

 
 

 
 

 

 
 
 
 
 
 
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
