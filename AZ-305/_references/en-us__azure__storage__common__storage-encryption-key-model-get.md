# https://learn.microsoft.com/en-us/azure/storage/common/storage-encryption-key-model-get

Source: https://learn.microsoft.com/en-us/azure/storage/common/storage-encryption-key-model-get

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
 

 

 

 

 
 
# Determine which Azure Storage encryption key model is in use for the storage account

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Data in your storage account is automatically encrypted by Azure Storage. Azure Storage encryption offers two options for managing encryption keys at the level of the storage account:

- Microsoft-managed keys. By default, Microsoft manages the keys used to encrypt your storage account.

- Customer-managed keys. You can optionally choose to manage encryption keys for your storage account. Customer-managed keys must be stored in Azure Key Vault.

Additionally, you can provide an encryption key at the level of an individual request for some Blob storage operations. When an encryption key is specified on the request, that key overrides the encryption key that is active on the storage account. For more information, see Specify a customer-provided key on a request to Blob storage.

For more information about encryption keys, see Azure Storage encryption for data at rest.

## Check the encryption key model for the storage account

To determine whether a storage account is using Microsoft-managed keys or customer-managed keys for encryption, use one of the following approaches.

- 
Azure portal

- 
PowerShell

- 
Azure CLI

To check the encryption model for the storage account by using the Azure portal, follow these steps:

- In the Azure portal, navigate to your storage account.

- Select the Encryption setting and note the setting.

The following image shows a storage account that is encrypted with Microsoft-managed keys:

And the following image shows a storage account that is encrypted with customer-managed keys:

To check the encryption model for the storage account by using PowerShell, call the Get-AzStorageAccount command, then check the KeySource property for the account.

`$account = Get-AzStorageAccount -ResourceGroupName <resource-group> `
 -Name <storage-account>
$account.Encryption.KeySource
`

If the value of the KeySource property is `Microsoft.Storage`, then the account is encrypted with Microsoft-managed keys. If the value of the KeySource property is `Microsoft.Keyvault`, then the account is encrypted with customer-managed keys.

To check the encryption model for the storage account by using Azure CLI, call the az storage account show command, then check the keySource property for the account.

`key_source=$(az storage account show \
 --name <storage-account> \
 --resource-group <resource-group> \
 --query encryption.keySource \
 --output tsv)
`

If the value of the keySource property is `Microsoft.Storage`, then the account is encrypted with Microsoft-managed keys. If the value of the keySource property is `Microsoft.Keyvault`, then the account is encrypted with customer-managed keys.

## Next steps

- Azure Storage encryption for data at rest

- Customer-managed keys for Azure Storage encryption

 
 

 
 

 

 
 
 
 
 
 
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
 2023-03-10
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
