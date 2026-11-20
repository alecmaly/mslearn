# https://learn.microsoft.com/en-us/azure/storage/common/storage-require-secure-transfer

Source: https://learn.microsoft.com/en-us/azure/storage/common/storage-require-secure-transfer

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
 

 

 

 

 
 
# Require secure transfer to ensure secure connections

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 âï¸ Applies to: Azure Blob Storage, Azure Data Lake Storage, Azure Queue Storage, Azure Table Storage

âï¸ Doesn't apply to: Azure Files (`Microsoft.Storage` or `Microsoft.FileShares`)

You can configure your storage account to accept requests from secure connections only by setting the Secure transfer required property for the storage account. When you require secure transfer, any requests originating from an insecure connection are rejected. Require secure transfer for all of your storage accounts.

When secure transfer is required, a call to an Azure Storage REST API operation must be made over HTTPS. Any request made over HTTP is rejected. By default, the Secure transfer required property is enabled when you create a storage account.

Azure Policy provides a built-in policy to ensure that secure transfer is required for your storage accounts. For more information, see the Storage section in Azure Policy built-in policy definitions.

For Azure Files, see Configure encryption in transit for Azure Files. Storage accounts that contain Azure file shares use the same setting, but it interacts with the SMB and NFS encryption settings. The Azure Files article describes considerations for Azure Files.

## Require secure transfer in the Azure portal

You can turn on the Secure transfer required property when you create a storage account in the Azure portal. You can also enable it for existing storage accounts.

### Require secure transfer for a new storage account

- Sign into the Azure portal and go to Storage accounts. Select + Create.

- On the Advanced tab, under Security, select the Require secure transfer for REST API operations checkbox.

### Require secure transfer for an existing storage account

- Select an existing storage account in the Azure portal.

- From the service menu, under Settings, select Configuration.

- Under Secure transfer required, select Enabled.

- Select Save.

## Require secure transfer from code

To require secure transfer programmatically, set the enableHttpsTrafficOnly property to True on the storage account. You can set this property by using the Storage Resource Provider REST API, client libraries, or tools:

- REST API

- PowerShell

- CLI

- NodeJS

- .NET SDK

- Python SDK

- Ruby SDK

## Require secure transfer with PowerShell

Note

We recommend that you use the Azure Az PowerShell module to interact with Azure. To get started, see Install Azure PowerShell. To learn how to migrate to the Az PowerShell module, see Migrate Azure PowerShell from AzureRM to Az.

This sample requires the Azure PowerShell module Az version 0.7 or later. Run `Get-Module -ListAvailable Az` to find the version. If you need to install or upgrade, see Install Azure PowerShell module.

Run `Connect-AzAccount` to create a connection with Azure.

Use the following command line to check the setting:

`Get-AzStorageAccount -Name "{StorageAccountName}" -ResourceGroupName "{ResourceGroupName}"
StorageAccountName : {StorageAccountName}
Kind : Storage
EnableHttpsTrafficOnly : False
...

`

Use the following command line to enable the setting:

`Set-AzStorageAccount -Name "{StorageAccountName}" -ResourceGroupName "{ResourceGroupName}" -EnableHttpsTrafficOnly $True
StorageAccountName : {StorageAccountName}
Kind : Storage
EnableHttpsTrafficOnly : True
...

`

## Require secure transfer with Azure CLI

To run this sample, install the latest version of the Azure CLI. To start, run `az login` to create a connection with Azure.

Samples for the Azure CLI are written for the `bash` shell. To run this sample in Windows PowerShell or Command Prompt, you may need to change
elements of the script.

If you don't have an Azure account, create a free account before you begin.

Use the following command to check the setting:

`az storage account show -g {ResourceGroupName} -n {StorageAccountName}
{
 "name": "{StorageAccountName}",
 "enableHttpsTrafficOnly": false,
 "type": "Microsoft.Storage/storageAccounts"
 ...
}

`

Use the following command to enable the setting:

`az storage account update -g {ResourceGroupName} -n {StorageAccountName} --https-only true
{
 "name": "{StorageAccountName}",
 "enableHttpsTrafficOnly": true,
 "type": "Microsoft.Storage/storageAccounts"
 ...
}

`

## Next steps

Security recommendations for Blob storage

 
 

 
 

 

 
 
 
 
 
 
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
 2026-10-26
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
