# https://learn.microsoft.com/en-us/azure/storage/common/infrastructure-encryption-enable

Source: https://learn.microsoft.com/en-us/azure/storage/common/infrastructure-encryption-enable

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
 

 

 

 

 
 
# Enable infrastructure encryption for double encryption of data

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Storage automatically encrypts all data in a storage account at the service level using 256-bit AES encryption, one of the strongest block ciphers available, and is FIPS 140-2 compliant. Customers who require higher levels of assurance that their data is secure can also enable 256-bit AES encryption at the Azure Storage infrastructure level for double encryption. Double encryption of Azure Storage data protects against a scenario where one of the encryption algorithms or keys might be compromised. In this scenario, the additional layer of encryption continues to protect your data.

Infrastructure encryption can be enabled for the entire storage account, or for an encryption scope within an account. When infrastructure encryption is enabled for a storage account or an encryption scope, data is encrypted twice â once at the service level and once at the infrastructure level â with two different encryption algorithms and two different keys.

Service-level encryption supports the use of either Microsoft-managed keys or customer-managed keys with Azure Key Vault or Key Vault Managed Hardware Security Model (HSM). Infrastructure-level encryption relies on Microsoft-managed keys and always uses a separate key. For more information about key management with Azure Storage encryption, see About encryption key management.

To doubly encrypt your data, you must first create a storage account or an encryption scope that is configured for infrastructure encryption. This article describes how to enable infrastructure encryption.

Important

Infrastructure encryption is recommended for scenarios where doubly encrypting data is necessary for compliance requirements. For most other scenarios, Azure Storage encryption provides a sufficiently powerful encryption algorithm, and there is unlikely to be a benefit to using infrastructure encryption.

## Create an account with infrastructure encryption enabled

To enable infrastructure encryption for a storage account, you must configure a storage account to use infrastructure encryption when you create the account. You can't enable or disable infrastructure encryption after you create the account. The storage account must be of type general-purpose v2, premium block blob, or premium page blob.

For information about infrastructure encryption for Azure Files, see Infrastructure encryption.

- 
Azure portal

- 
PowerShell

- 
Azure CLI

- 
Template

To use the Azure portal to create a storage account with infrastructure encryption enabled, follow these steps:

- In the Azure portal, navigate to the Storage accounts page.

- Select Add to add a new general-purpose v2, premium block blob, or premium page blob account.

- On the Encryption tab, locate Enable infrastructure encryption, and select Enabled.

- Select Review + create to finish creating the storage account.

To verify that infrastructure encryption is enabled for a storage account with the Azure portal, follow these steps:

- Navigate to your storage account in the Azure portal.

- Under Security + networking, choose Encryption.

To use PowerShell to create a storage account with infrastructure encryption enabled, make sure you have installed the Az.Storage PowerShell module, version 2.2.0 or later. For more information, see Install Azure PowerShell.

Next, create a general-purpose v2, premium block blob, or premium page blob storage account by calling the New-AzStorageAccount command. Include the `-RequireInfrastructureEncryption` option to enable infrastructure encryption.

The following example shows how to create a general-purpose v2 storage account that is configured for read-access geo-redundant storage (RA-GRS) and has infrastructure encryption enabled for double encryption of data. Remember to replace the placeholder values in brackets with your own values:

`New-AzStorageAccount -ResourceGroupName <resource_group> `
 -AccountName <storage-account> `
 -Location <location> `
 -SkuName "Standard_RAGRS" `
 -Kind StorageV2 `
 -AllowBlobPublicAccess $false `
 -RequireInfrastructureEncryption
`

To verify that infrastructure encryption is enabled for a storage account, call the Get-AzStorageAccount command. This command returns a set of storage account properties and their values. Retrieve the `RequireInfrastructureEncryption` field within the `Encryption` property and verify that it is set to `True`.

The following example retrieves the value of the `RequireInfrastructureEncryption` property. Remember to replace the placeholder values in angle brackets with your own values:

`$account = Get-AzStorageAccount -ResourceGroupName <resource-group> `
 -StorageAccountName <storage-account>
$account.Encryption.RequireInfrastructureEncryption
`

To use Azure CLI to create a storage account that has infrastructure encryption enabled, make sure you have installed Azure CLI version 2.8.0 or later. For more information, see Install the Azure CLI.

Next, create a general-purpose v2, premium block blob, or premium page blob account by calling the az storage account create command and include the `--require-infrastructure-encryption` option to enable infrastructure encryption.

The following example shows how to create a general-purpose v2 storage account that is configured for read-access geo-redundant storage (RA-GRS) and has infrastructure encryption enabled for double encryption of data. Remember to replace the placeholder values in brackets with your own values:

`az storage account create \
 --name <storage-account> \
 --resource-group <resource-group> \
 --location <location> \
 --sku Standard_RAGRS \
 --kind StorageV2 \
 --allow-blob-public-access false \
 --require-infrastructure-encryption
`

To verify that infrastructure encryption is enabled for a storage account, call the az storage account show command. This command returns a set of storage account properties and their values. Look for the `requireInfrastructureEncryption` field within the `encryption` property and verify that it is set to `true`.

The following example retrieves the value of the `requireInfrastructureEncryption` property. Remember to replace the placeholder values in angle brackets with your own values:

`az storage account show /
 --name <storage-account> /
 --resource-group <resource-group>
`

The following JSON example creates a general-purpose v2 storage account that is configured for read-access geo-redundant storage (RA-GRS) and has infrastructure encryption enabled for double encryption of data. Remember to replace the placeholder values in brackets with your own values:

`"resources": [
 {
 "type": "Microsoft.Storage/storageAccounts",
 "apiVersion": "2019-06-01",
 "name": "[parameters('<storage-account>')]",
 "location": "[parameters('<location>')]",
 "dependsOn": [],
 "tags": {},
 "sku": {
 "name": "[parameters('Standard_RAGRS')]"
 },
 "kind": "[parameters('StorageV2')]",
 "properties": {
 "accessTier": "[parameters('<accessTier>')]",
 "supportsHttpsTrafficOnly": "[parameters('supportsHttpsTrafficOnly')]",
 "largeFileSharesState": "[parameters('<largeFileSharesState>')]",
 "encryption": {
 "keySource": "Microsoft.Storage",
 "requireInfrastructureEncryption": true,
 "services": {
 "blob": { "enabled": true },
 "file": { "enabled": true }
 }
 }
 }
 }
],
`

Azure Policy provides a built-in policy to require that infrastructure encryption be enabled for a storage account. For more information, see the Storage section in Azure Policy built-in policy definitions.

## Create an encryption scope with infrastructure encryption enabled

If infrastructure encryption is enabled for an account, then any encryption scope created on that account automatically uses infrastructure encryption. If infrastructure encryption is not enabled at the account level, then you have the option to enable it for an encryption scope at the time that you create the scope. The infrastructure encryption setting for an encryption scope cannot be changed after the scope is created. For more information, see Create an encryption scope.

## Next steps

- Azure Storage encryption for data at rest

- Customer-managed keys for Azure Storage encryption

- Encryption scopes for Blob storage

 
 

 
 

 

 
 
 
 
 
 
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
 2026-10-27
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
