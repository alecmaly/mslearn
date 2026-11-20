# https://learn.microsoft.com/en-us/azure/backup/backup-support-matrix-mars-agent

Source: https://learn.microsoft.com/en-us/azure/backup/backup-support-matrix-mars-agent

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
 

 

 

 

 
 
# Support matrix for backup with the Microsoft Azure Recovery Services (MARS) agent

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 You can use the Azure Backup service to back up on-premises machines and apps and to back up Azure virtual machines (VMs). This article summarizes support settings and limitations when you use the Microsoft Azure Recovery Services (MARS) agent to back up machines.

Note

Windows Server 2008, 2008 R2, 2012 and 2012 R2 have reached End of Support (EOS). Review your usage and plan OS upgrades and migrations accordingly. For more information, see End of support for:

- Windows Server 2008 and Windows Server 2008 R2

- Windows Server 2012

- Windows Server 2012 R2

Perform in-place upgrade to Windows Server 2016, 2019, 2022, or 2025.

## Supported MARS agent deployment scenarios for backup operations

Azure Backup uses the MARS agent to back up data from on-premises machines and Azure VMs to a backup Recovery Services vault in Azure. The MARS agent can:

- Run on on-premises Windows machines so that they can back up directly to a backup Recovery Services vault in Azure.

- Run on Windows VMs so that they can back up directly to a vault.

- Run on Microsoft Azure Backup Server (MABS) or a System Center Data Protection Manager (DPM) server. In this scenario, machines and workloads back up to MABS or to the DPM server. The MARS agent then backs up this server to a vault in Azure.

Note

Azure Backup doesn't support automatic adjustment of clock for daylight savings time (DST). Modify the policy to ensure daylight savings is taken into account to prevent discrepancy between the actual time and scheduled backup time.

Your backup options depend on where the agent is installed. For more information, see Azure Backup architecture using the MARS agent. For information about MABS and DPM backup architecture, see Back up to DPM or MABS. Also see requirements for the backup architecture.

Installation
Details

Download the latest MARS agent
You can download the latest version of the agent from the vault, or download it directly.

Install directly on a machine
You can install the MARS agent directly on an on-premises Windows server or on a Windows VM that's running any of the supported operating systems.

Install on a backup server
When you set up DPM or MABS to back up to Azure, you download and install the MARS agent on the server. You can install the agent on supported operating systems in the backup server support matrix.

Note

By default, Azure VMs that are enabled for backup have an Azure Backup extension installation. This extension backs up the entire VM. You can install and run the MARS agent on an Azure VM alongside the extension if you want to back up specific folders and files, rather than the complete VM.
When you run the MARS agent on an Azure VM, it backs up files or folders that are in temporary storage on the VM. Backups fail if the files or folders are removed from the temporary storage or if the temporary storage is removed.

## Cache folder support

When you use the MARS agent to back up data, the agent takes a snapshot of the data and stores it in a local cache folder before it sends the data to Azure. The cache (scratch) folder has several requirements:

Cache
Details

Size
Free space in the cache folder should be at least 5 to 10 percent of the overall size of your backup data.

Location
The cache folder must be locally stored on the machine that's being backed up, and it must be online. The cache folder shouldn't be on a network share, on removable media, or on an offline volume.

Folder
The cache folder shouldn't be encrypted on a deduplicated volume or in a folder that's compressed, that's sparse, or that has a reparse point.

Location changes
You can change the cache location by stopping the backup engine (`net stop obengine`) and copying the cache folder to a new drive. (Ensure the new drive has sufficient space.) Then update two registry entries under HKLM\SOFTWARE\Microsoft\Windows Azure Backup (Config/ScratchLocation and Config/CloudBackupProvider/ScratchLocation) to the new location and restart the engine.

## Networking and access support

The MARS agent requires access to Microsoft Entra ID, Azure Storage, and Azure Backup service endpoints. To obtain the public IP ranges, see the JSON file. Allow access to the IPs corresponding to Azure Backup (`AzureBackup`), Azure Storage (`Storage`), and Microsoft Entra ID (`AzureActiveDirectory`). Also, depending on your Windows version, network connectivity checks of the operating system will need access to `www.msftconnecttest.com`, or `www.msftncsi.com`.

If your machine has limited internet access, ensure that firewall, proxy, and network settings allow access to the following FQDNs and public IP addresses.

### URL and IP access

FQDNs

- `*.microsoft.com`

- `*.windowsazure.com`

- `*.microsoftonline.com`

- `*.windows.net`

- `*.blob.core.windows.net`

- `*.queue.core.windows.net`

- `*.blob.storage.azure.net`

If you are a US Government customer, ensure that you have access to the following URLs:

- `www.msftncsi.com`

- `*.microsoft.com`

- `*.windowsazure.us`

- `*.microsoftonline.us`

- `*.windows.net`

- `*.usgovcloudapi.net`

- `*.blob.core.windows.net`

- `*.queue.core.windows.net`

- `*.blob.storage.azure.net`

Access to all of the URLs and IP addresses listed above uses the HTTPS protocol on port 443.

When backing up files and folders from Azure VMs using the MARS Agent, you also need to configure the Azure virtual network to allow access. If you use Network Security Groups (NSG), use the AzureBackup service tag to allow outbound access to Azure Backup. In addition to the Azure Backup tag, you also need to allow connectivity for authentication and data transfer by creating similar NSG rules for Microsoft Entra ID (`AzureActiveDirectory`) and Azure Storage (`Storage`).

To create a rule for the Azure Backup tag, follow these steps:

- In All Services, go to Network security groups and select the network security group.

- Select Outbound security rules under Settings.

- Select Add.

- Provide all required details for creating a new rule as described in security rule settings.
Ensure the options are set as below:

- Destination is set to Service Tag.

- Destination service tag is set to AzureBackup.

- Select Add to save the newly created outbound security rule.

You can similarly create NSG outbound security rules for Azure Storage and Microsoft Entra ID. To learn more about service tags, see Virtual network service tags.

### Azure ExpressRoute support

You can back up your data through Azure ExpressRoute by using public peering (available for old circuits). When private endpoint is enabled on the vault, use ExpressRoute private peering; if private endpoint is not enabled, use Microsoft peering and add Microsoft Entra IDâs in ExpressRoute setup and router filter.

To use public peering, ensure that the following domains and addresses have HTTPS access on port 443 to:

- `*.microsoft.com`

- `*.windowsazure.com`

- `*.microsoftonline.com`

- `*.windows.net`

- `*.blob.core.windows.net`

- `*.queue.core.windows.net`

- `*.blob.storage.azure.net`

To use Microsoft peering, select the following services, regions, and relevant community values:

- Microsoft Entra ID (12076:5060)

- Azure region, according to the location of your Recovery Services vault

- Azure Storage, according to the location of your Recovery Services vault

Learn more about ExpressRoute routing requirements.

Note

Public peering is deprecated for new circuits.

### Private Endpoint support

You can now use Private Endpoints to back up your data securely from servers to your Recovery Services vault. As Microsoft Entra ID canât be accessed via private endpoints, you need to allow IPs and FQDNs required for Microsoft Entra ID for outbound access separately.

When you use the MARS agent to back up your on-premises resources, ensure that your on-premises network (containing your resources to be backed up) is peered with the Azure VNet that contains a private endpoint for the vault. You can then continue to install the MARS agent and configure backup. However, you must ensure all communication for backup happens through the peered network only.

If you remove private endpoints for the vault after a MARS agent has been registered to it, you'll need to re-register the container with the vault. You don't need to stop protection for them. For more information, see Private endpoints for Azure Backup.

### Throttling support

Feature
Details

Bandwidth control
Supported. In the MARS agent, use Change Properties to adjust bandwidth.

Network throttling
Not available for backed-up machines that run Windows Server 2008 R2, Windows Server 2008 SP2, or Windows 7.

## Supported operating systems

Note

The MARS agent does not support Windows Server Core SKUs.

You can use the MARS agent to back up directly to Azure on the operating systems listed below that run on:

- On-premises Windows or Windows Servers

- Azure VMs running Windows

The operating systems must be 64 bit and should be running the latest services packs and updates. The following table summarizes these operating systems:

Operating system
Files/folders
System state
Software/Module requirements

Windows 11 (Enterprise, Pro, Home, IoT Enterprise)
Yes
No
Check the corresponding server version for software/module requirements

Windows 10 (Enterprise, Pro, Home, IoT Enterprise)
Yes
No
Check the corresponding server version for software/module requirements

Windows 8.1 (Enterprise, Pro)
Yes
No
Check the corresponding server version for software/module requirements

Windows 8 (Enterprise, Pro)
Yes
No
Check the corresponding server version for software/module requirements

Windows Server 2025 (Standard, Datacenter, Essentials, Server IoT)
Yes
Yes
- .NET 4.8 
 - Windows PowerShell 
 - Latest Compatible Microsoft VC++ Redistributable 
 - Microsoft Management Console (MMC) 3.0

Windows Server 2022 (Standard, Datacenter, Essentials, Server IoT)
Yes
Yes
- .NET 4.8 
 - Windows PowerShell 
 - Latest Compatible Microsoft VC++ Redistributable 
 - Microsoft Management Console (MMC) 3.0

Windows Server 2019 (Standard, Datacenter, Essentials, Server IoT)
Yes
Yes
- .NET 4.8 
 - Windows PowerShell 
 - Latest Compatible Microsoft VC++ Redistributable 
 - Microsoft Management Console (MMC) 3.0

Windows Server 2016 (Standard, Datacenter, Essentials)
Yes
Yes
- .NET 4.8 
 - Windows PowerShell 
 - Latest Compatible Microsoft VC++ Redistributable 
 - Microsoft Management Console (MMC) 3.0

Windows Storage Server 2016/2012 R2/2012 (Standard, Workgroup)
Yes
No
- .NET 4.8 
 - Windows PowerShell 
 - Latest Compatible Microsoft VC++ Redistributable 
 - Microsoft Management Console (MMC) 3.0

Windows Server 2012 R2 (Standard, Datacenter, Foundation, Essentials)
Yes
Yes
- .NET 4.8 
 - Windows PowerShell 
 - Latest Compatible Microsoft VC++ Redistributable 
 - Microsoft Management Console (MMC) 3.0

Windows Server 2012 (Standard, Datacenter, Foundation)
Yes
Yes
- .NET 4.8 
 -Windows PowerShell 
 - Latest Compatible Microsoft VC++ Redistributable 
 - Microsoft Management Console (MMC) 3.0 
 - Deployment Image Servicing and Management (DISM.exe)

For more information, see Supported MABS and DPM operating systems.

### Operating Systems at end of support

The following operating systems are at the end of support and it's strongly recommended to upgrade the operating system to continue to stay protected.

If existing commitments prevent upgrading the operating system, consider migrating the Windows servers to Azure VMs and leverage Azure VM backups to continue staying protected. Visit the migration page here for more information about migrating your Windows server.

For on-premises or hosted environments, where you can't upgrade the operating system or migrate to Azure, activate Extended Security Updates for the machines to continue staying protected and supported. Notice that only specific editions are eligible for Extended Security Updates. Visit the FAQ page to learn more.

Operating system
Files/folders
System state
Software/Module requirements

Windows 7 (Ultimate, Enterprise, Pro, Home Premium/Basic, Starter)
Yes
No
Check the corresponding server version for software/module requirements

Windows Server 2008 R2 (Standard, Enterprise, Datacenter, Foundation)
Yes
Yes
- .NET 3.5, .NET 4.5 
 - Windows PowerShell 
 - Compatible Microsoft VC++ Redistributable 
 - Microsoft Management Console (MMC) 3.0 
 - Deployment Image Servicing and Management (DISM.exe)

Windows Server 2008 SP2 (Standard, Datacenter, Foundation)
Yes
No
- .NET 3.5, .NET 4.5 
 - Windows PowerShell 
 - Compatible Microsoft VC++ Redistributable 
 - Microsoft Management Console (MMC) 3.0 
 - Deployment Image Servicing and Management (DISM.exe) 
 - Virtual Server 2005 base + KB KB948515

## Backup limits

### Size limits

Azure Backup limits the size of a file or folder data source that can be backed up. The items that you back up from a single volume can't exceed the sizes summarized in this table:

Operating system
Size limit

Windows Server 2012 or later
54,400 GB

Windows Server 2008 R2 SP1
1,700 GB

Windows Server 2008 SP2
1,700 GB

Windows 8 or later
54,400 GB

Windows 7
1,700 GB

Note

During Azure VM restore, you might experience performance issues in the following scenarios:

- The number of files to restore exceeds 8 million

- The total data size to restore is greater than 1 TB

- The backup set includes more than 20 chained incremental snapshots.

The restore process can also interrupt due to operational issues such as high latency between the vault and the source machine, low download speed from Azure to the source machine, or limited bandwidth on your machine.

### Retention limits

The following are the retention durations that can be set for the different recovery points:

Recovery point
Minimum
Maximum

Daily recovery point
7 days
9999 days

Weekly recovery point
4 weeks
5163 weeks

Monthly recovery point
3 months
1188 months

Yearly recovery point
1 year
99 years

### Other limitations

- MARS doesn't support protection of multiple machines with the same name to a single vault.

- Recovery Services vaults encrypted using customer-managed keys (CMKs) aren't supported for backup via the MARS agent.

## Supported file types for backup

Type
Support

Encrypted*
Supported.

Compressed
Supported.

Sparse
Supported.

Compressed and sparse
Supported.

Hard links
Not supported. Skipped.

Reparse point
Not supported. Skipped.

Encrypted and sparse
Not supported. Skipped.

Compressed stream
Not supported. Skipped.

Sparse stream
Not supported. Skipped.

OneDrive (synced files are sparse streams)
Not supported.

Folders with DFS Replication enabled
Not supported.

* Ensure that the MARS agent has access to the required certificates to access the encrypted files. Inaccessible files will be skipped.

## Supported drives or volumes for backup

Drive/volume
Support
Details

Read-only volumes
Not supported
Volume Copy Shadow Service (VSS) works only if the volume is writable.

Offline volumes
Not supported
VSS works only if the volume is online.

Network share
Not supported
The volume must be local on the server.

BitLocker-locked volumes
Not supported
The volume must be unlocked before the backup starts.

File system identification
Not supported
Only NTFS is supported.

Removable media
Not supported
All backup item sources must have a fixed status.

Deduplicated drives
Supported
Azure Backup converts deduplicated data to normal data. It optimizes, encrypts, stores, and sends the data to the vault.

## Support for initial offline backup

Azure Backup supports offline seeding to transfer initial backup data to Azure by using disks. This support is helpful if your initial backup is likely to be in the size range of terabytes (TBs). Offline backup is supported for:

- Direct backup of files and folders on on-premises machines that are running the MARS agent.

- Backup of workloads and files from a DPM server or MABS.

Offline backup can't be used for system state files.

## Support for data restoration

By using the Instant Restore feature of Azure Backup, you can restore data before it's copied to the vault. The machine you're backing up must be running .NET Framework 4.5.2 or higher.

Backups can't be restored to a target machine that's running an earlier version of the operating system. For example, a backup taken from a computer that's running Windows 7 can be restored on Windows 8 or later. But a backup taken from a computer that's running Windows 8 can't be restored on a computer that's running Windows 7.

## Previous MARS agent versions

The following table lists the previous versions of the agent with their download links. We recommend you to upgrade the agent version to the latest, so you can leverage the latest features and optimal performance.

Versions
KB Articles

2.0.9145.0
Not available

2.0.9151.0
Not available

2.0.9153.0
Not available

2.0.9162.0
Not available

2.0.9169.0
4515971

2.0.9170.0
Not available

2.0.9173.0
4538314

2.0.9177.0
Not available

2.0.9181.0
Not available

2.0.9190.0
4575948

2.0.9195.0
4582474

2.0.9197.0
4589598

2.0.9207.0
5001305

2.0.9415.0
5059322

2.0.9506.0
5068415

2.0.9615.0
5085049

2.0.9625.0
5095917

2.0.9663.0
5130846

Note

MARS agent versions with minor reliability and performance improvements don't have a KB article.

## Next steps

- Learn more about backup architecture that uses the MARS agent.

- Learn what's supported when you run the MARS agent on MABS or a DPM server.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-03-09
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
