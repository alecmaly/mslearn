# https://learn.microsoft.com/en-us/azure/storage/files/storage-how-to-create-file-share

Source: https://learn.microsoft.com/en-us/azure/storage/files/storage-how-to-create-file-share

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
 

 

 

 

 
 
# Create an Azure classic file share

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 âï¸ Applies to: Classic SMB and NFS file shares created with the Microsoft.Storage resource provider

âï¸ Doesn't apply to: File shares created with the Microsoft.FileShares resource provider

Tip

Creating an NFS file share? Use Microsoft.FileShares. Classic file shares support NFS, but use the Microsoft.FileShares resource provider for new NFS deployments. To create an NFS file share with Microsoft.FileShares, see Create an Azure file share with Microsoft.FileShares. For the differences between the resource providers, see Azure Files management concepts.

This article describes how to create a storage account and a classic file share in it. Before you create a classic file share, decide on these properties:

- Media tier: SSD file shares provide consistent high performance and low latency. HDD file shares provide cost-effective storage for general-purpose use.

- Protocol: SMB file shares are available on both media tiers. NFS file shares require the SSD media tier.

- Redundancy: HDD file shares support locally redundant storage (LRS), zone-redundant storage (ZRS), geo-redundant storage (GRS), and geo-zone-redundant storage (GZRS). SSD file shares support LRS and ZRS. For more information, see Azure Files data redundancy.

For more information, see Plan an Azure Files deployment.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, create a free account.

- To use Azure PowerShell, install the latest version.

- To use Azure CLI, install the latest version.

## Create a storage account for classic file shares

You deploy classic file shares into a storage account. A storage account is a top-level resource that represents a shared pool of storage, IOPS, and throughput. You can deploy multiple file shares in one storage account. If you already have a storage account that you want to use, go to Create a classic file share.

Two storage account properties, kind and SKU, determine the billing model, media tier, and redundancy of the file shares in the storage account. Azure Files supports these combinations:

Media tier
Billing model
Storage account kind
Storage account SKUs

SSD and HDD
Provisioned v2
FileStorage

- PremiumV2_LRS

- PremiumV2_ZRS

- StandardV2_LRS

- StandardV2_ZRS

- StandardV2_GRS

- StandardV2_GZRS

SSD
Provisioned v1
FileStorage

- Premium_LRS

- Premium_ZRS

HDD
Pay-as-you-go
StorageV2

- Standard_LRS

- Standard_ZRS

- Standard_GRS

- Standard_GZRS

Use the provisioned v2 billing model for all new file share deployments. The provisioned v1 and pay-as-you-go billing models remain fully supported for new and existing deployments. Provisioned v2 file shares are available in most regions. For more information, see Provisioned v2 availability.

- 
Portal

- 
PowerShell

- 
Azure CLI

To create a storage account in the Azure portal, search for storage accounts in the search box at the top of the portal. Under Services, select Storage accounts.

Select + Create to open the Create a storage account page.

The Create a storage account page has a tab for each group of settings. The following sections describe the settings that apply to Azure Files.

### Basics

The Basics tab contains the required settings for the storage account.

Field
Values
Description

Subscription
Available Azure subscriptions
The subscription for the storage account.

Resource group
Resource groups in the subscription
The resource group for the storage account.

Storage account name
Text
A globally unique name for the storage account. The name must be 3 to 24 characters long and contain only numbers and lowercase letters.

Region
Available Azure regions
The region for the storage account.

Primary service

- Azure Blob Storage or Azure Data Lake Storage

- Azure Files

- Other (tables and queues)

Select Azure Files. The provisioned v2 billing model is available only when you select Azure Files.

Media tier

- HDD (standard)

- SSD (premium)

The media tier for the file shares in the storage account.

File share billing

- HDD: Pay-as-you-go file shares or Provisioned v2

- SSD: Provisioned v1 or Provisioned v2

We recommend Provisioned v2 for all new deployments.

Redundancy

- HDD: LRS, GRS, ZRS, or GZRS

- SSD: LRS or ZRS

For more information, see Azure Files data redundancy.

Make read access to data available in the event of regional unavailability
Checkbox
Appears only for HDD pay-as-you-go storage accounts with GRS or GZRS. This setting doesn't apply to Azure Files. Azure Files doesn't support read access to the secondary region without a failover.

Zone options

- None

- Self-selected zone

- Azure-selected zone

Appears for SSD storage accounts with LRS. To place the storage account in a specific availability zone, see Use zonal placement for Azure file shares.

### Advanced

The Advanced tab has a section for Azure Blob Storage and a section for Azure Files. Settings in the Azure Blob Storage section don't apply to Azure Files.

For SSD storage accounts, the portal enables SMB Multichannel by default. You can disable it after you create the storage account. For more information, see Improve performance for SMB Azure file shares.

Field
Default
Description

Enable Managed Identity for SMB
Not selected
Lets applications and virtual machines access SMB file shares with a managed identity. For more information, see Access SMB Azure file shares by using managed identities with Microsoft Entra ID.

Require Encryption in Transit for SMB
Selected
Requires encryption for SMB access to the file shares in the storage account.

Require Encryption in Transit for NFS
Selected
Requires encryption for NFS access to the file shares in the storage account. Appears only for SSD storage accounts.

The portal saves each Require Encryption in Transit setting as enabled or disabled, so these settings control SMB and NFS encryption whether or not you select them. The Require secure transfer for REST API operations setting on the Security tab applies only to FileREST (HTTPS) traffic. For more information, see Configure encryption in transit for Azure Files.

### Networking

The networking settings are optional when you create the storage account. You can configure them later.

Field
Default
Description

Public network access
Enable
Enable, Disable, or Secure by perimeter. Controls access to the storage account's public endpoint.

Public network access scope
Enable from all networks
To allow access only from specific networks, select Enable from selected virtual networks and IP addresses.

Virtual networks
None
Appears when you select Enable from selected virtual networks and IP addresses. Allows access from the selected subnets through the `Microsoft.Storage` service endpoint.

IPv4 Addresses
None
Appears when you select Enable from selected virtual networks and IP addresses. Allows access from public IPv4 addresses or ranges. IP address rules don't grant NFS access.

For more information, see Azure Files networking considerations and Restrict access to the public endpoint to specific networks.

### Data protection

The Data protection tab has a section for Azure Blob Storage and a section for Azure Files. Settings in the Azure Blob Storage section don't apply to Azure Files.

Field
Default
Description

Enable soft delete for classic file shares
Selected
Protects file shares against accidental deletion. For more information, see Azure file share soft delete.

Days to retain deleted classic file shares
7
The number of days that Azure Files keeps a deleted file share before it purges the file share. You're billed for the used capacity of soft-deleted file shares, including provisioned file shares. A longer retention period can increase your costs.

### Security

The Security tab combines settings for all storage services. The following table shows which settings apply to Azure Files.

Field
Applies to Azure Files
Description

Require secure transfer for REST API operations
Yes
Requires HTTPS for FileREST requests. The Require Encryption in Transit settings on the Advanced tab control SMB and NFS encryption.

Allow enabling anonymous access on individual containers
No
Applies only to Blob Storage.

Enable storage account key access
Yes
Controls whether clients can use the storage account keys to mount SMB file shares or to authorize FileREST requests.

Default to Microsoft Entra authorization in the Azure portal
Yes
Controls whether the Azure portal uses your Microsoft Entra identity, instead of the storage account key, when you browse file shares.

Minimum TLS version
Yes
The minimum TLS version for FileREST requests. SMB doesn't use TLS. For NFS, the AzNFS mount helper uses TLS 1.2 or TLS 1.3. For more information, see FileREST.

Permitted scope for copy operations (Preview)
Yes
Limits which storage accounts can be the source of FileREST copy operations into this storage account. Tools such as AzCopy use these operations.

### Encryption

The Encryption tab controls encryption at rest. For more information, see Encryption at rest for Azure Files.

Field
Applies to Azure Files
Description

Encryption type
Yes
Microsoft-managed keys (MMK) or Customer-managed keys (CMK). For the steps to use customer-managed keys, see Configure encryption at rest with customer-managed keys for Azure Files.

Enable support for customer-managed keys
No
All classic file shares support customer-managed keys, regardless of this setting.

Enable infrastructure encryption
Yes
Adds a second layer of encryption. You can enable infrastructure encryption only when you create the storage account. For more information, see Infrastructure encryption.

### Tags

Tags are name/value pairs that you use to categorize resources and to view consolidated billing. Tags are optional, and you can add them after you create the storage account.

### Review + create

- Select Review and create.

- Check the settings on the Review + create tab, and then select Create.

### Create the storage account (PowerShell)

To create a storage account, use the New-AzStorageAccount cmdlet. The following `New-AzStorageAccount` parameters set the storage account settings that apply to Azure Files. If you omit a parameter, the storage account uses the default.

Portal setting
Parameter
Values

Resource group
`ResourceGroupName`
Required. The name of an existing resource group.

Storage account name
`Name`
Required. A globally unique name, 3 to 24 characters long, with only numbers and lowercase letters.

Region
`Location`
Required. For example, `westus2`.

Media tier, File share billing, Redundancy
`Kind`, `SkuName`
See the table at the start of this section.

Zone options
`Zone` or `ZonePlacementPolicy`
SSD storage accounts with LRS only. See Use zonal placement for Azure file shares.

Enable Managed Identity for SMB
`EnableSmbOAuth`
`$true` or `$false`. The default is `$false`.

Public network access
`PublicNetworkAccess`
`Enabled` (default), `Disabled`, or `SecuredByPerimeter`.

Public network access scope
`NetworkRuleSet`, `defaultAction` key
`Allow` (default) or `Deny`. To allow access only from the virtual networks and IP addresses in the network rules, use `Deny`.

Virtual networks
`NetworkRuleSet`, `virtualNetworkRules` key
Subnet resource IDs. Each subnet must have the `Microsoft.Storage` service endpoint.

IPv4 Addresses
`NetworkRuleSet`, `ipRules` key
Public IPv4 addresses or CIDR ranges. IP address rules don't grant NFS access.

Exceptions (not in the create wizard)
`NetworkRuleSet`, `bypass` key
`AzureServices` (default) or `None`. `AzureServices` allows trusted Azure services to access the storage account. The create wizard always uses `AzureServices`.

Require secure transfer for REST API operations
`EnableHttpsTrafficOnly`
`$true` (default) or `$false`.

Enable storage account key access
`AllowSharedKeyAccess`
`$true` (default) or `$false`.

Default to Microsoft Entra authorization in the Azure portal
None
Azure PowerShell doesn't have a parameter for this setting. Use the Azure portal or Azure CLI.

Minimum TLS version
`MinimumTlsVersion`
`TLS1_2`, which is the default and the lowest TLS version that Azure Files accepts.

Permitted scope for copy operations
`AllowedCopyScope`
`AAD` (same Microsoft Entra tenant) or `PrivateLink` (private endpoint to the same virtual network). If you omit it, copies from any storage account are allowed.

Encryption type
Several
See Configure encryption at rest with customer-managed keys for Azure Files.

Enable infrastructure encryption
`RequireInfrastructureEncryption`
Include the switch to enable it. You can enable infrastructure encryption only when you create the storage account.

Tags
`Tag`
A hashtable, for example `@{ environment = "test" }`.

The following example creates an SSD provisioned v2 storage account. For a different media tier, billing model, or redundancy, change `Kind` and `SkuName` to a combination from the table at the start of this section. Replace `<resource-group>`, `<storage-account-name>`, and `<region>` with your own values.

`$resourceGroupName = "<resource-group>"
$storageAccountName = "<storage-account-name>"

$params = @{
 ResourceGroupName = $resourceGroupName
 Name = $storageAccountName
 Location = "<region>"
 Kind = "FileStorage"
 SkuName = "PremiumV2_LRS"
 EnableHttpsTrafficOnly = $true
 MinimumTlsVersion = "TLS1_2"
 AllowSharedKeyAccess = $true
}
New-AzStorageAccount @params
`

To allow access only from specific networks, add a `NetworkRuleSet` entry to `$params` in the previous example. Replace `<subnet-resource-id>` and `<public-ip-address-or-range>` with your own values. For more information, see Restrict access to the public endpoint to specific networks.

`NetworkRuleSet = @{
 defaultAction = "Deny"
 bypass = "AzureServices"
 virtualNetworkRules = @(@{ VirtualNetworkResourceId = "<subnet-resource-id>" })
 ipRules = @(@{ IPAddressOrRange = "<public-ip-address-or-range>" })
}
`

### Configure file service settings (PowerShell)

The encryption in transit, SMB Multichannel, and soft delete settings belong to the storage account's file service. To configure them, use the Update-AzStorageFileServiceProperty cmdlet after you create the storage account.

A storage account that you create with PowerShell starts with soft delete enabled for 7 days. On SSD storage accounts, SMB Multichannel is enabled. Both Require Encryption in Transit settings start as not configured, so Require secure transfer for REST API operations controls SMB and NFS encryption until you configure them. For more information, see Encryption in transit settings.

The following `Update-AzStorageFileServiceProperty` parameters set the file service settings:

Portal setting
Parameter
Values

Require Encryption in Transit for SMB
`SmbEncryptionInTransitRequired`
`$true` or `$false`.

Require Encryption in Transit for NFS
`NfsEncryptionInTransitRequired`
`$true` or `$false`. Applies to NFS file shares, which require SSD.

SMB Multichannel
`EnableSmbMultichannel`
`$true` or `$false`. SSD storage accounts only.

Enable soft delete for classic file shares
`EnableShareDeleteRetentionPolicy`
`$true` (default) or `$false`.

Days to retain deleted classic file shares
`ShareRetentionDays`
1 to 365. The default is 7.

The following example configures the same settings that the Azure portal uses by default:

`$params = @{
 ResourceGroupName = $resourceGroupName
 StorageAccountName = $storageAccountName
 SmbEncryptionInTransitRequired = $true
 NfsEncryptionInTransitRequired = $true
 EnableShareDeleteRetentionPolicy = $true
 ShareRetentionDays = 7
}
Update-AzStorageFileServiceProperty @params
`

The same cmdlet also configures the SMB protocol versions, authentication methods, and encryption algorithms. For more information, see SMB security settings.

For a provisioned v2 storage account, you can view the provisioning limits and usage with the Get-AzStorageFileServiceUsage cmdlet:

`$params = @{
 ResourceGroupName = $resourceGroupName
 StorageAccountName = $storageAccountName
}
Get-AzStorageFileServiceUsage @params
`

### Create the storage account (Azure CLI)

To create a storage account, use the az storage account create command. The following `az storage account create` parameters set the storage account settings that apply to Azure Files. If you omit a parameter, the storage account uses the default.

Portal setting
Parameter
Values

Resource group
`--resource-group`
Required. The name of an existing resource group.

Storage account name
`--name`
Required. A globally unique name, 3 to 24 characters long, with only numbers and lowercase letters.

Region
`--location`
For example, `westus2`. If you omit it, the storage account uses the region of the resource group.

Media tier, File share billing, Redundancy
`--kind`, `--sku`
See the table at the start of this section.

Zone options
`--zones` or `--zone-placement-policy`
SSD storage accounts with LRS only. See Use zonal placement for Azure file shares.

Enable Managed Identity for SMB
`--enable-smb-oauth`
`true` or `false`. The default is `false`.

Public network access
`--public-network-access`
`Enabled` (default), `Disabled`, or `SecuredByPerimeter`.

Public network access scope
`--default-action`
`Allow` (default) or `Deny`. To allow access only from the virtual networks and IP addresses in the network rules, use `Deny`.

Virtual networks
`--vnet-name` and `--subnet`
One subnet. The subnet must have the `Microsoft.Storage` service endpoint. To add more subnets after you create the storage account, use `az storage account network-rule add`.

IPv4 Addresses
None
`az storage account create` doesn't have a parameter for IP address rules. After you create the storage account, use `az storage account network-rule add` with `--ip-address`. IP address rules don't grant NFS access.

Exceptions (not in the create wizard)
`--bypass`
`AzureServices` (default) or `None`. `AzureServices` allows trusted Azure services to access the storage account. The create wizard always uses `AzureServices`.

Require secure transfer for REST API operations
`--https-only`
`true` (default) or `false`.

Enable storage account key access
`--allow-shared-key-access`
`true` (default) or `false`.

Default to Microsoft Entra authorization in the Azure portal
None
`az storage account create` doesn't have a parameter for this setting. After you create the storage account, run `az storage account update` with `--set defaultToOAuthAuthentication=true`.

Minimum TLS version
`--min-tls-version`
`TLS1_2`, which is the default and the lowest TLS version that Azure Files accepts.

Permitted scope for copy operations
`--allowed-copy-scope`
`AAD` (same Microsoft Entra tenant) or `PrivateLink` (private endpoint to the same virtual network). If you omit it, copies from any storage account are allowed.

Encryption type
Several
See Configure encryption at rest with customer-managed keys for Azure Files.

Enable infrastructure encryption
`--require-infrastructure-encryption`
Include the parameter to enable it. You can enable infrastructure encryption only when you create the storage account.

Tags
`--tags`
Space-separated `key=value` pairs, for example `environment=test`.

The following example creates an SSD provisioned v2 storage account. For a different media tier, billing model, or redundancy, change `--kind` and `--sku` to a combination from the table at the start of this section. Replace `<resource-group>`, `<storage-account-name>`, and `<region>` with your own values.

`resourceGroupName="<resource-group>"
storageAccountName="<storage-account-name>"

az storage account create \
 --resource-group $resourceGroupName \
 --name $storageAccountName \
 --location "<region>" \
 --kind FileStorage \
 --sku PremiumV2_LRS \
 --https-only true \
 --min-tls-version TLS1_2 \
 --allow-shared-key-access true \
 --output none
`

To allow access only from specific networks, add `--default-action Deny`, `--bypass AzureServices`, `--vnet-name`, and `--subnet` to the previous command. To add an IP address rule, run az storage account network-rule add after you create the storage account. Replace `<public-ip-address-or-range>` with your own value. For more information, see Restrict access to the public endpoint to specific networks.

`az storage account network-rule add \
 --resource-group $resourceGroupName \
 --account-name $storageAccountName \
 --ip-address "<public-ip-address-or-range>" \
 --output none
`

### Configure file service settings (Azure CLI)

The encryption in transit, SMB Multichannel, and soft delete settings belong to the storage account's file service. To configure them, use the az storage account file-service-properties update command after you create the storage account.

A storage account that you create with Azure CLI starts with soft delete enabled for 7 days. On SSD storage accounts, SMB Multichannel is enabled. Both Require Encryption in Transit settings start as not configured, so Require secure transfer for REST API operations controls SMB and NFS encryption until you configure them. For more information, see Encryption in transit settings.

The following `az storage account file-service-properties update` parameters set the file service settings:

Portal setting
Parameter
Values

Require Encryption in Transit for SMB
`--require-smb-encryption-in-transit`
`true` or `false`.

Require Encryption in Transit for NFS
`--require-nfs-encryption-in-transit`
`true` or `false`. Applies to NFS file shares, which require SSD.

SMB Multichannel
`--enable-smb-multichannel`
`true` or `false`. SSD storage accounts only.

Enable soft delete for classic file shares
`--enable-delete-retention`
`true` (default) or `false`.

Days to retain deleted classic file shares
`--delete-retention-days`
1 to 365. The default is 7.

The following example configures the same settings that the Azure portal uses by default:

`az storage account file-service-properties update \
 --resource-group $resourceGroupName \
 --account-name $storageAccountName \
 --require-smb-encryption-in-transit true \
 --require-nfs-encryption-in-transit true \
 --enable-delete-retention true \
 --delete-retention-days 7 \
 --output none
`

The same command also configures the SMB protocol versions, authentication methods, and encryption algorithms. For more information, see SMB security settings.

For a provisioned v2 storage account, you can view the provisioning limits and usage with the az storage account file-service-usage command:

`az storage account file-service-usage \
 --account-name $storageAccountName \
 --resource-group $resourceGroupName
`

## Create a classic file share

The steps to create a classic file share depend on the billing model of the storage account. Provisioned file shares require a `FileStorage` storage account. Pay-as-you-go file shares require a `StorageV2` storage account.

To check the billing model of a storage account, go to the storage account's Overview page. Under Essentials, check Account kind and File share billing.

A file share name can contain only lowercase letters, numbers, and single hyphens. It must start and end with a lowercase letter or number, and it can't contain two consecutive hyphens. For more information, see Naming and referencing shares, directories, files, and metadata.

### Create a provisioned v2 classic file share

For a provisioned v2 file share, you provision storage, IOPS, and throughput. Your bill depends on the amount of each that you provision. Azure Files recommends IOPS and throughput based on the provisioned storage. You can use the recommendation, or specify your own values. For more information, see Provisioned v2 model.

- 
Portal

- 
PowerShell

- 
Azure CLI

- Go to your storage account. From the service menu, under Data storage, select Classic file shares.

- Select + Classic file share.

- On the Basics tab of the New classic file share page, complete these fields:

- Name: The name of the file share.

- Provisioned storage (GiB): The amount of storage to provision. You're billed for the provisioned storage, regardless of how much you use.

- Provisioned IOPS and throughput: Select Recommended provisioning to use the recommended IOPS and throughput, or select Manually specify IOPS and throughput. If you don't know your IOPS and throughput requirements, use the recommendation and adjust it later.

- IOPS and Throughput (MiB/sec): If you selected Manually specify IOPS and throughput, enter the values to provision. The range for each value appears under the field.

- Protocol: Select SMB or NFS. NFS is available only in SSD storage accounts. For an NFS file share, you can also set Root Squash. For more information, see Configure root squash for Azure Files.

- Select the Backup tab. For an SMB file share, Azure Backup is enabled by default. To disable it, clear Enable backup. To keep it, use the default vault and policy, or create a new Recovery Services vault or backup policy. Azure Backup isn't available for NFS file shares.

- Select Review + create, and then select Create.

To create a provisioned v2 classic file share, use the New-AzRmStorageShare cmdlet. The commands use the `$resourceGroupName` and `$storageAccountName` variables from Create the storage account. Replace `<file-share-name>` with your own value.

`# QuotaGiB is the provisioned storage in GiB. The valid range is 32 to 262,144.
# EnabledProtocol is "SMB" or "NFS". NFS requires an SSD storage account.
$params = @{
 ResourceGroupName = $resourceGroupName
 StorageAccountName = $storageAccountName
 Name = "<file-share-name>"
 QuotaGiB = 1024
 EnabledProtocol = "SMB"
}
New-AzRmStorageShare @params
`

The command provisions the recommended IOPS and throughput. To provision your own values, add `ProvisionedIops` and `ProvisionedBandwidthMibps` to the parameters, for example `ProvisionedIops = 3000` and `ProvisionedBandwidthMibps = 130`.

To create a provisioned v2 classic file share, use the az storage share-rm create command. The commands use the `resourceGroupName` and `storageAccountName` variables from Create the storage account. Replace `<file-share-name>` with your own value.

`# --quota is the provisioned storage in GiB. The valid range is 32 to 262,144.
# --enabled-protocols is SMB or NFS. NFS requires an SSD storage account.
az storage share-rm create \
 --resource-group $resourceGroupName \
 --storage-account $storageAccountName \
 --name "<file-share-name>" \
 --quota 1024 \
 --enabled-protocols SMB \
 --output none
`

The command provisions the recommended IOPS and throughput. To provision your own values, add the `--provisioned-iops` and `--provisioned-bandwidth-mibps` parameters, for example `--provisioned-iops 3000 --provisioned-bandwidth-mibps 130`.

### Create an SSD provisioned v1 classic file share

For a provisioned v1 file share, you provision storage. Azure Files sets the IOPS and throughput based on the provisioned storage. To get more IOPS or throughput, provision more storage. For more information, see Provisioned v1 model.

- 
Portal

- 
PowerShell

- 
Azure CLI

- Go to your storage account. From the service menu, under Data storage, select Classic file shares.

- Select + Classic file share.

- On the Basics tab of the New classic file share page, complete these fields:

- Name: The name of the file share.

- Provisioned storage (GiB): The amount of storage to provision. The minimum is 100 GiB. You're billed for the provisioned storage, regardless of how much you use. Under Performance, the page shows the IOPS, burst IOPS, and throughput for the provisioned storage.

- Protocol: Select SMB or NFS. For an NFS file share, you can also set Root Squash. For more information, see Configure root squash for Azure Files.

- Select the Backup tab. For an SMB file share, Azure Backup is enabled by default. To disable it, clear Enable backup. To keep it, use the default vault and policy, or create a new Recovery Services vault or backup policy. Azure Backup isn't available for NFS file shares.

- Select Review + create, and then select Create.

To create a provisioned v1 classic file share, use the New-AzRmStorageShare cmdlet. The commands use the `$resourceGroupName` and `$storageAccountName` variables from Create the storage account. Replace `<file-share-name>` with your own value.

`# QuotaGiB is the provisioned storage in GiB. The valid range is 100 to 102,400.
# EnabledProtocol is "SMB" or "NFS".
$params = @{
 ResourceGroupName = $resourceGroupName
 StorageAccountName = $storageAccountName
 Name = "<file-share-name>"
 QuotaGiB = 1024
 EnabledProtocol = "SMB"
}
New-AzRmStorageShare @params
`

To create a provisioned v1 classic file share, use the az storage share-rm create command. The commands use the `resourceGroupName` and `storageAccountName` variables from Create the storage account. Replace `<file-share-name>` with your own value.

`# --quota is the provisioned storage in GiB. The valid range is 100 to 102,400.
# --enabled-protocols is SMB or NFS.
az storage share-rm create \
 --resource-group $resourceGroupName \
 --storage-account $storageAccountName \
 --name "<file-share-name>" \
 --quota 1024 \
 --enabled-protocols SMB \
 --output none
`

### Create an HDD pay-as-you-go classic file share

Pay-as-you-go file shares support only SMB. Each pay-as-you-go file share has an access tier: transaction optimized, hot, or cool. All three access tiers use the same HDD hardware. Cooler tiers have lower storage prices and higher transaction prices. For more information, see Differences in access tiers.

- 
Portal

- 
PowerShell

- 
Azure CLI

- Go to your storage account. From the service menu, under Data storage, select Classic file shares.

- Select + Classic file share.

- On the Basics tab of the New classic file share page, complete these fields:

- Name: The name of the file share.

- Access tier: The access tier of the file share. The default is Transaction optimized. During a migration, use the transaction optimized tier to minimize transaction costs. After the migration, you can change to a cooler tier.

- Select the Backup tab. Azure Backup is enabled by default. To disable it, clear Enable backup. To keep it, use the default vault and policy, or create a new Recovery Services vault or backup policy.

- Select Review + create, and then select Create.

To create a pay-as-you-go classic file share, use the New-AzRmStorageShare cmdlet. The commands use the `$resourceGroupName` and `$storageAccountName` variables from Create the storage account. Replace `<file-share-name>` with your own value.

`# Valid values for AccessTier are "TransactionOptimized", "Hot", and "Cool".
$params = @{
 ResourceGroupName = $resourceGroupName
 StorageAccountName = $storageAccountName
 Name = "<file-share-name>"
 AccessTier = "TransactionOptimized"
}
New-AzRmStorageShare @params
`

To create a pay-as-you-go classic file share, use the az storage share-rm create command. The commands use the `resourceGroupName` and `storageAccountName` variables from Create the storage account. Replace `<file-share-name>` with your own value.

`# Valid values for --access-tier are TransactionOptimized, Hot, and Cool.
az storage share-rm create \
 --resource-group $resourceGroupName \
 --storage-account $storageAccountName \
 --name "<file-share-name>" \
 --access-tier TransactionOptimized \
 --output none
`

## Set up networking for classic file shares

SMB file shares don't require network configuration. NFS file shares require it, because NFS uses network-based access control. Clients can access an NFS file share only from a virtual network, through a private endpoint or a service endpoint.

- A private endpoint gives the storage account a private IP address in your virtual network. Clients in peered virtual networks and on-premises networks can use it. Data processing charges apply.

- A service endpoint lets clients in specific subnets use the public endpoint. The subnets can be in a different subscription or Microsoft Entra tenant. Service endpoints don't have extra charges.

For more information, see Azure Files networking considerations.

Important

NFS uses TCP port 2049. Ensure that your clients can send traffic on port 2049, and that the network security groups of the virtual network don't block inbound traffic on port 2049.

### Set up a private endpoint or service endpoint

The following steps create a private endpoint for an NFS file share in the Azure portal. To configure a service endpoint, or to use PowerShell or Azure CLI, see Configure network endpoints for Azure file shares.

- Go to your storage account. From the service menu, under Data storage, select Classic file shares, and then select your NFS file share.

- On the Connect from Linux tab, under Network configuration, select Review options. The Configure network security tab opens.

- Select Setup a private endpoint. The Private endpoint connections tab of the storage account's networking page opens.

- Select + Private endpoint.

- On the Basics tab, enter a Name for the private endpoint. The portal fills in Network Interface Name. Set Region to the region of your virtual network, and then select Next : Resource.

- On the Resource tab, make sure that Target sub-resource is file, and then select Next : Virtual Network.

- On the Virtual Network tab, select your Virtual network and Subnet. The portal might select a different virtual network by default. Leave Dynamically allocate IP address selected, and then select Next : DNS.

- On the DNS tab, leave Integrate with private DNS zone set to Yes. Make sure that the subscription and resource group are correct, and then select Next : Tags.

- Optionally, add tags, and then select Next : Review + create.

- After validation passes, select Create.

### Enable hybrid access through VPN or ExpressRoute (optional)

To access an NFS file share from an on-premises network, connect the network to your virtual network with a VPN or Azure ExpressRoute, and configure DNS for the private endpoint. For the steps, see Connect from on-premises.

## Related content

- Mount SMB Azure file share on Windows

- Mount NFS Azure file shares on Linux

- Modify an Azure file share

 
 

 
 

 

 
 
 
 
 
 
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
