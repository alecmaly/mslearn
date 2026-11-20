# https://learn.microsoft.com/en-us/azure/storage/blobs/versioning-enable

Source: https://learn.microsoft.com/en-us/azure/storage/blobs/versioning-enable

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
 

 

 

 

 
 
# Enable and manage blob versioning

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 You can enable Blob storage versioning to automatically maintain previous versions of a blob when it is modified or deleted. When blob versioning is enabled, then you can restore an earlier version of a blob to recover your data if it is erroneously modified or deleted.

This article shows how to enable or disable blob versioning for the storage account by using the Azure portal or an Azure Resource Manager template. To learn more about blob versioning, see Blob versioning.

## Enable blob versioning

You can enable blob versioning with the Azure portal, PowerShell, Azure CLI, or an Azure Resource Manager template.

- 
Azure portal

- 
PowerShell

- 
Azure CLI

- 
Template

To enable blob versioning for a storage account in the Azure portal:

- Navigate to your storage account in the portal.

- Under Data management, choose Data protection.

- In the Tracking section, select Enable versioning for blobs, and then choose whether to keep all versions or delete them after a period of time.

Important

If you set the Delete versions after option, a rule is automatically added to the lifecycle management policy of the storage account. Once that rule is added, the Delete versions after option no longer appears in the Data protection configuration page.

You can make that option reappear in the Data protection page by removing the rule. If your lifecycle management policy contains other rules that delete versions, then you'll have to remove those rules as well before the Delete versions after option can reappear.

To enable blob versioning for a storage account with PowerShell, first install the Az.Storage module version 2.3.0 or later. Then call the Update-AzStorageBlobServiceProperty command to enable versioning, as shown in the following example. Remember to replace the values in angle brackets with your own values:

`# Set resource group and account variables.
$rgName = "<resource-group>"
$accountName = "<storage-account>"

# Enable versioning.
Update-AzStorageBlobServiceProperty -ResourceGroupName $rgName `
 -StorageAccountName $accountName `
 -IsVersioningEnabled $true
`

To enable blob versioning for a storage account with Azure CLI, first install the Azure CLI version 2.2.0 or later. Then call the az storage account blob-service-properties update command to enable versioning, as shown in the following example. Remember to replace the values in angle brackets with your own values:

`az storage account blob-service-properties update \
 --resource-group <resource_group> \
 --account-name <storage-account> \
 --enable-versioning true
`

To enable blob versioning with a template, create a template with the IsVersioningEnabled property to true. The following steps describe how to create a template in the Azure portal.

- In the Azure portal, choose Create a resource.

- In Search the Marketplace, type template deployment, and then press ENTER.

- Choose Template deployment, choose Create, and then choose Build your own template in the editor.

- In the template editor, paste in the following JSON. Replace the `<accountName>` placeholder with the name of your storage account.

- Save the template.

- Specify the resource group of the account, and then choose the Purchase button to deploy the template and enable blob versioning.

`{
 "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
 "contentVersion": "1.0.0.0",
 "parameters": {},
 "variables": {},
 "resources": [
 {
 "type": "Microsoft.Storage/storageAccounts/blobServices",
 "apiVersion": "2019-06-01",
 "name": "<accountName>/default",
 "properties": {
 "IsVersioningEnabled": true
 }
 }
 ]
}
`

For more information about deploying resources with templates in the Azure portal, see Deploy resources with Azure portal.

## List blob versions

To display a blob's versions, use the Azure portal, PowerShell, or Azure CLI. You can also list a blob's versions using one of the Blob Storage SDKs.

- 
Azure portal

- 
PowerShell

- 
Azure CLI

- 
Template

To list a blob's versions in the Azure portal:

- Navigate to your storage account in the portal, then navigate to the container that contains your blob.

- Select the blob for which you want to list versions.

- Select the Versions tab to display the blob's versions.

- Toggle the Show deleted versions button to display soft-deleted versions. If blob soft delete is enabled for the storage account, then any soft-deleted versions that are still within the soft-delete retention interval will appear in the list.

To list a blob's versions with PowerShell, call the Get-AzStorageBlob command with the `-IncludeVersion` parameter:

`$account = Get-AzStorageAccount -ResourceGroupName <resource-group> -Name <storage-account>
$ctx = $account.Context
$container = "<container-name>"

$blobs = Get-AzStorageBlob -Container $container -Prefix "ab" -IncludeVersion -Context $ctx

foreach($blob in $blobs)
{
 Write-Host $blob.Name
 Write-Host $blob.VersionId
 Write-Host $blob.IsLatestVersion
}
`

To list a blob's versions with Azure CLI, call the az storage blob list command with the `--include v` parameter:

`storageAccount="<storage-account>"
containerName="<container-name>"

az storage blob list \
 --container-name $containerName \
 --prefix "ab" \
 --query "[[].name, [].versionId]" \
 --account-name $storageAccount \
 --include v \
 --auth-mode login \
 --output tsv 
`

N/A

## Next steps

- Blob versioning

- Soft delete for Azure Storage blobs

 
 

 
 

 

 
 
 
 
 
 
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
 2023-07-30
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
