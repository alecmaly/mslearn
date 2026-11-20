# https://learn.microsoft.com/en-us/azure/backup/backup-support-matrix-iaas

Source: https://learn.microsoft.com/en-us/azure/backup/backup-support-matrix-iaas

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
 

 

 

 

 
 
# Support matrix for Azure VM backups

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 You can use the Azure Backup service to back up on-premises machines and workloads, along with Azure virtual machines (VMs). This article summarizes support settings and limitations when you back up Azure VMs by using Azure Backup.

Other support matrices include:

- General support matrix for Azure Backup

- Support matrix for Azure Backup servers and System Center Data Protection Manager (DPM) backup

- Support matrix for backup with the Microsoft Azure Recovery Services (MARS) agent

## Supported scenarios

Here's how you can back up and restore Azure VMs by using the Azure Backup service.

Scenario
Backup
Agent
Restore

Direct backup of Azure VMs
Back up the entire VM.
For application or file-system consistent backups, no additional agent is needed on the Azure VM. Azure Backup installs and uses an extension to the Azure VM agent that's running on the VM. 

 You can also use agentless crash-consistent backups. Learn more.
Restore as follows:

 - Create a basic VM. This is useful if the VM has no special configuration, such as multiple IP addresses.

 - Restore the VM disk. Restore the disk. Then attach it to an existing VM, or create a new VM from the disk by using PowerShell.

 - Replace the VM disk. If a VM exists and it uses managed disks (unencrypted), you can restore a disk and use it to replace an existing disk on the VM.

 - Restore specific files or folders. You can restore files or folders from a VM instead of restoring the entire VM.

Direct backup of Azure VMs (Windows only)
Back up specific files, folders, or volumes.
Install the Azure Recovery Services agent.

 You can run the MARS agent alongside the backup extension for the Azure VM agent to back up the VM at the file or folder level.
Restore specific files or folders.

Backup of Azure VMs to the backup server
Back up files, folders, or volumes; system state or bare metal files; and app data to System Center DPM or to Microsoft Azure Backup Server (MABS).

 DPM or MABS then backs up to the backup vault.
Install the DPM or MABS protection agent on the VM. The MARS agent is installed on DPM or MABS.
Restore files, folders, or volumes; system state or bare metal files; and app data.

Learn more about using a backup server and about support requirements.

## Supported backup actions

Action
Support

Back up a VM that's shut down or offline
Supported.

 Snapshot is crash-consistent only, not app consistent.

Back up disks after migrating to managed disks
Supported.

 Backup will continue to work. No action is required.

Back up managed disks after enabling a resource group lock
Not supported.

 Azure Backup can't delete the older restore points. Backups will start to fail when the limit of restore points is reached.

Modify backup policy for a VM
Supported.

 The VM will be backed up according to the schedule and retention settings in the new policy. If retention settings are extended, existing recovery points are marked and kept. If they're reduced, existing recovery points will be pruned in the next cleanup job and eventually deleted.

Cancel a backup job
Supported during the snapshot process.

 Not supported when the snapshot is being transferred to the vault.

Back up the VM to a different region
Not supported.

The VM and Recovery Services vault must be in the same region.

Back up the VM to a different subscription
Supported when the VM and Recovery Services vault are in the same tenant and same region. Available in all Azure regions.

- Cross-subscription backup isn't supported for Confidential VMs (CVMs), including ADE encrypted CVMs.
 - Movement of backed-up data between vaults isn't supported. 

 Learn how to Back up Azure VMs in a Recovery Services vault and review the vault move guidance for backup continuity requirements.

Back up daily via the Azure VM extension
Four backups per day: one scheduled backup as defined in the backup policy, and three on-demand backups. 

 To allow user retries in case of failed attempts, the hard limit for on-demand backups is set to nine attempts in a 24 hour UTC period.

Back up daily via the MARS agent
Three scheduled backups per day.

Back up daily via DPM or MABS
Two scheduled backups per day.

Back up monthly or yearly
Not supported when you're backing up with the Azure VM extension. Only daily and weekly are supported.

 You can set up the policy to retain daily or weekly backups for a monthly or yearly retention period.

Automatically adjust the clock
Not supported.

 Azure Backup doesn't automatically adjust for daylight saving time when you're backing up a VM.

 Modify the policy manually as needed.

Disable security features for hybrid backup
Not supported.

Back up Azure VMs with Azure Extended zones
Supported through Enhanced policy.

 Snapshot is crash-consistent only, you can also retain snapshots locally for instant restore.

Back up a VM whose machine time is changed
Not supported.

 If you change the machine time to a future date/time after enabling backup for that VM, even if the time change is reverted, successful backup isn't guaranteed.

Do multiple backups per day
Supported through Enhanced policy. 

 For hourly backup, the minimum recovery point objective (RPO) is 4 hours and the maximum is 24 hours. You can set the backup schedule to 4, 6, 8, 12, and 24 hours, respectively. 

 Note that the maximum limit of instant recovery point retention range depends on the number of snapshots you take per day. If the snapshot count is more (for example, every 4 hours frequency in 24 hours duration - 6 scheduled snapshots), then the maximum allowed days for retention reduces. However, if you choose lower RPO of 12 hours, the snapshot retention is increased to 30 days. 

 Learn about how to back up an Azure VM using Enhanced policy.

Back up a VM with a deprecated plan when the publisher has removed it from Azure Marketplace
Not supported. 

 Backup is supported. 

 Restore to existing/original VM is supported. Restore by creating a new VM will fail. 

 If you've already configured backup for a VM with a deprecated virtual machine offer and encounter a restore error, see Troubleshoot backup errors with Azure VMs.

Back up VMs with docker (containers)
Not supported

Soft Delete for backups
Not Supported with Azure role-based access control (Azure RBAC) permissions at the resource group level. Requires Azure RBAC permissions at the subscription level, including the `Microsoft.DataProtection/locations/checkFeatureSupport/action` permission.

## Operating system support (Windows)

The following table summarizes the supported operating systems when you're backing up Azure VMs running Windows.

Scenario
OS support

Back up with the Azure VM agent extension for application-consistent backup
- Windows 11 client (64 bit only) 

 - Windows 10 client (64 bit only) 

- Windows Server 2025 (Datacenter, Datacenter Core, and Standard) 

- Windows Server 2022 (Datacenter, Datacenter Core, and Standard) 

- Windows Server 2019 (Datacenter, Datacenter Core, and Standard) 

 - Windows Server 2016 (Datacenter, Datacenter Core, and Standard) 

 Note that 32 bit Operating Systems aren't supported.

Back up Azure VM directly using agentless crash-consistent backup
Agentless crash-consistent backups are operating system agnostic.

Back up with the MARS agent
Supported operating systems

Back up with DPM or MABS
Supported operating systems for backup with MABS and DPM

## Support for Linux backup

Here's what's supported if you want to back up Linux machines.

Action
Support

Back up Linux Azure VMs with the Linux Azure VM agent
Supported for file-consistent backup.

 Also supported for app-consistent backup that uses custom scripts.

 During restore, you can create a new VM, restore a disk and use it to create a VM, or restore a disk and use it to replace a disk on an existing VM. You can also restore individual files and folders.

 Note: Azure Backup requires the /var and /var/lib directories on Linux machines not to be mounted with the noexec flag. Certain backup operations rely on executing helper scripts from /var/lib, and enforcing noexec prevents these components from running.

Back up Azure VM directly by using agentless crash-consistent backup
Agentless crash-consistent backups are operating system agnostic.

Back up Linux Azure VMs with the MARS agent
Not supported.

 The MARS agent can be installed only on Windows machines.

Back up Linux Azure VMs with DPM or MABS
Not supported.

Back up Linux Azure VMs with Docker mount points
Currently, Azure Backup doesn't support exclusion of Docker mount points because these are mounted at different paths every time.

Backup Linux Azure VMs with ZFS Pool Configuration
Not supported

## Operating system support (Linux)

For Linux VM backups using the Linux Azure VM agent, Azure Backup supports the list of Linux distributions endorsed by Azure. Note the following:

- Agent-based VM backup doesn't support CoreOS Linux.

- Agent-based VM backup doesn't support 32-bit operating systems.

- Other bring-your-own Linux distributions might work as long as the Azure VM agent for Linux is available on the VM, and as long as Python is supported.

- Agent-based VM backup doesn't support a proxy-configured Linux VM if it doesn't have Python version 2.7 or later installed.

- Agentless crash-consistent backups are operating system agnostic and can be used to back up VMs whose operating system isn't supported for agent-based backups.

- Azure Backup doesn't support backing up Network File System (NFS) files that are mounted from storage, or from any other NFS server, to Linux or Windows machines. It backs up only disks that are locally attached to the VM.

## Support matrix for managed pre and post scripts for Linux databases

Azure Backup provides the following support for customers to author their own pre and post scripts.

Supported database
OS version
Database version

Oracle in Azure VMs
Oracle Linux
Oracle 12.x or later

## Support for Confidential VM backup (preview)

The following table lists the supported scenarios for Confidential VM backup:

Scenario
Supportability

Virtual Machine size
v6-series is supported. 
 v5-series isn't supported.

Region availability
Public preview is available in all Azure public regions.

Key rotation for backups
When you rotate keys associated with a disk of a confidential virtual machine, the keys of the related restore points and snapshots update automatically. 

 You might observe performance degradations or failures if you attach more than 6,000 disks to one DES and (only) restore points are associated with these disks. If you directly create disk snapshots outside of Azure backup for these disks connected to the same DES, it lowers the safe threshold of 6,000 disks to DES mapping.

Backup capabilities
- You can back up Confidential VMs with OS disk encryption only. 
 - Backup and restore fail if the CVM v2 opt-out feature flag is enabled for your subscription. 
 - Multi-disk crash-consistent backup isn't supported.

Restore capabilities
- Cross-region restore is supported only to the Azure paired region; restore to a region of your choice isn't supported. 
 - Cross-tenant restore isn't supported. 
 - Bulk restore isn't supported.

## Support for agentless multi-disk crash-consistent VM backup

The following table lists the supported scenarios for agentless multi-disk crash-consistent Azure Virtual Machine (VM) backup:

Scenario
Supportability

Region availability
Supported in all Azure public regions.

Backup policy type
Agentless crash-consistent backup is supported only with Enhanced Policy.

VM type and size
- Supported for VM sizes that are premium storage capable (VM size that include "s" in their name) such as `DSv2`. 
 - Trusted Launch VMs are supported. 
 - VMs with Ultra Disks, Premium SSD v2, Ephemeral OS disks, Shared disks, and Write Accelerated disks aren't supported. 
 - VM sizes using Azure Boost aren't supported - Intel V6 and above (Dsv6-series, Edsv6-series, Esv6-series, and more) and AMD V7 and above (Dasv7-series, Dadsv7-series, Easv7-series, Faldsv7-series, and more)

Pre/post script
Not applicable 
 Pre/Post scripts are used for app-consistent Linux VM backup.

Learn more about Agentless multi-disk crash-consistent VM backup.

## Backup frequency and retention

Setting
Limits

Maximum recovery points per protected instance (machine or workload)
9999.

Maximum expiry time for a recovery point
No limit (99 years).

Maximum backup frequency to a vault (Azure VM extension)
Once a day.

Maximum backup frequency to a vault (MARS agent)
Three backups per day.

Maximum backup frequency to DPM or MABS
Every 15 minutes for SQL Server.

 Once an hour for other workloads.

Recovery point retention
Daily, weekly, monthly, and yearly.

Maximum retention period
Depends on backup frequency.

Recovery points on DPM or MABS disk
64 for file servers, and 448 for app servers.

 Tape recovery points are unlimited for on-premises DPM.

## Supported restore methods

Restore option
Details

Create a new VM
This option quickly creates and gets a basic VM up and running from a restore point.

 You can specify a name for the VM, select the resource group and virtual network in which it will be placed, and specify a storage account for the restored VM. The new VM must be created in the same region as the source VM.

Restore disk
This option restores a VM disk, which can you can then use to create a new VM.

 Azure Backup provides a template to help you customize and create a VM. 

 The restore job generates a template that you can download and use to specify custom VM settings and create a VM.

 The disks are copied to the resource group that you specify.

 Alternatively, you can attach the disk to an existing VM, or create a new VM by using PowerShell.

 This option is useful if you want to customize the VM, add configuration settings that weren't there at the time of backup, or add settings that must be configured via the template or PowerShell.

Replace existing
You can restore a disk and use it to replace a disk on the existing VM.

 The current VM must exist. If it has been deleted, you can't use this option.

 Azure Backup takes a snapshot of the existing VM before replacing the disk, and it stores the snapshot in the staging location that you specify. Existing disks connected to the VM are replaced with the selected restore point.

 The snapshot is copied to the vault and retained in accordance with the retention policy. 

 After the replace-disk operation, the original disk is retained in the resource group. You can choose to manually delete the original disks if they aren't needed. 

This option is supported for unencrypted managed VMs and for VMs created from custom images. It's not supported for unmanaged disks and VMs, classic VMs, and generalized VMs.

 If the restore point has more or fewer disks than the current VM, the number of disks in the restore point will only reflect the VM configuration.

 This option is also supported for VMs with linked resources, like user-assigned managed identity and Azure Key Vault.

Cross Region (secondary region)
You can use cross-region restore to restore Azure VMs in the secondary region, which is an Azure paired region.

 You can restore all the Azure VMs for the selected recovery point if the backup is done in the secondary region.

 This feature is available for the following options:
 - Create a VM 
 - Restore disks 

 We don't currently support the Replace existing disks option.

 Backup admins and app admins have permissions to perform the restore operation on a secondary region.

Cross Subscription
Allowed only if the Cross Subscription Restore property is enabled for the required target scenario. 

 You can restore managed Azure virtual machines or disks to a different subscription within the same tenant by using the following options:
 - Create a VM 
 - Restore disks 

 The default target subscription is the protected VM subscription. Snapshot-tier recovery points can be restored only in the protected VM subscription. Vault-tier recovery points can be restored in the protected VM subscription or the vault subscription. To restore a vault-tier recovery point to another subscription, Cross Subscription Restore must be enabled on the vault. 

 Original location restore and Replace existing remain supported only in the protected VM subscription. 

 Cross Subscription Restore is unsupported for: 
 - Legacy recovery points from VMs that used unmanaged disks and VMs with disks having Azure Encryptions (ADE). 
 - VMs with CMK encrypted disks.

Cross Zonal Restore
You can use cross-zonal restore to restore Azure zone-pinned VMs in available zones. You can restore Azure VMs or disks to different zones (one of the Azure RBAC capabilities) from restore points. Note that when you select a zone to restore, it selects the logical zone (and not the physical zone) as per the Azure subscription you will use to restore to. 

 This feature is available for the following options:
 - Create a VM 
 - Restore disks 

 Cross-zonal restore is unsupported for snapshots of restore points. 

 Cross-zonal restore doesn't support restoring encrypted Azure VMs directly. If you perform a restore, the restored VM uses SSE encryption by default. You must manually reapply CMK encryption to the restored VM after the restore process is complete.

Cross Tenant (preview)
You can restore vaulted recovery points of managed Azure virtual machines to a different tenant by using cross-tenant restore. Only alternate location restore is supported. 

 Cross-tenant restore is unsupported for Confidential VMs, VMs encrypted with Azure Disk Encryption (ADE), original location restore, and archive-tier recovery points.

## Support for file-level restore

Restore
Supported

Restore files across operating systems
You can restore files on any machine that has the same OS as the backed-up VM, or a compatible OS. See the compatible OS table.

Restore files from encrypted VMs
Not supported.

Restore files from network-restricted storage accounts
Not supported.

Restore files on VMs by using Windows Storage Spaces
Not supported.

Restore files on a Linux VM by using LVM or RAID arrays
Not supported on the same VM.

 Restore on a compatible VM.

Restore files with special network settings
Not supported on the same VM. 

 Restore on a compatible VM.

Restore files from Premium SSD v2 or Ultra disks
Supported for disks with 512-byte or 4-KB logical sector sizes, including recovery points from VMs with mixed disk types. See supported disks and recovery scope.

Restore files from a shared disk, temporary drive, deduplicated disk, or disk with a write accelerator enabled
Not supported. 

See Azure VM storage support.

## Support for VM management

The following table summarizes support for backup during VM management tasks, such as adding or replacing VM disks.

Restore
Supported

Restore across a subscription
Cross-subscription restore is now supported in Azure VMs.

Restore across a region
Supported.

Restore across a zone
Cross-zonal restore is now supported in Azure VMs.

Restore to an existing VM
Use the replace-disk option.

Restore a disk with a storage account enabled for Azure Storage service-side encryption (SSE)
Not supported.

 Restore to an account that doesn't have SSE enabled.

Restore to mixed storage accounts
Not supported.

 Based on the storage account type, all restored disks will be either premium or standard, and not mixed.

Restore a VM directly to an availability set
For managed disks, you can restore the disk and use the availability set option in the template.

 For legacy recovery points from VMs that used unmanaged disks, restore the disks as managed disks, and then create a VM in the availability set.

Restore backup of unmanaged VMs after upgrading to a managed VM
Supported.

 You can restore legacy recovery points as managed disks and then create a managed VM.

Restore a VM from a restore point before the VM was migrated to managed disks
Supported.

 Restore the recovery point as managed disks, and then create a VM with the restored managed disks.

Restore a VM that has been deleted
Supported.

 You can restore the VM from a recovery point.

Restore a domain controller VM
Supported. For details, see Restore domain controller VMs.

Restore a VM in a different virtual network
Supported.

 The virtual network must be in the same subscription and region.

## VM compute support

Compute
Support

Back up VMs of a certain size
You can back up any Azure VM that has at least two CPU cores and 1 GB of RAM.

 Learn more.

Back up VMs in availability sets
Supported.

 You can't restore a VM in an availability set by using the option to quickly create a VM. Instead, when you restore the VM, restore the disk and use it to deploy a VM, or restore a disk and use it to replace an existing disk.

Back up VMs that are deployed with Azure Hybrid Benefit
Supported.

Back up VMs that are deployed from Azure Marketplace (published by Microsoft or a third party)
Supported.

 The VMs must be running a supported operating system.

 When you're recovering files on the VM, you can restore only to a compatible OS (not an earlier or later OS). We don't restore Azure Marketplace VMs backed as VMs, because these need purchase information. They're restored only as disks.

Back up VMs that are deployed from a custom image (third-party)
Supported.

 The VMs must be running a supported operating system.

 When you're recovering files on VMs, you can restore only to a compatible OS (not an earlier or later OS).

Back up VMs that are migrated to Azure
Supported.

 To back up a VM, make sure that the VM agent is installed on the migrated machine.

Back up multiple VMs and provide consistency
Azure Backup doesn't provide data and application consistency across multiple VMs.

Back up a VM with diagnostic settings
Not supported. 

 If the restore of the Azure VM with diagnostic settings is triggered via the Create new option, the restore fails.

Restore zone-pinned VMs
Supported (where availability zones are available).

Azure Backup now supports restoring Azure VMs to a any availability zones other than the zone that's pinned in VMs. This support enables you to restore VMs when the primary zone is unavailable.

Back up Gen2 VMs
Supported. 

 Azure Backup supports backup and restore of Gen2 VMs. When these VMs are restored from a recovery point, they're restored as Gen2 VMs.

Back up Azure VMs with locks
Supported for managed VMs. 

 Not supported for unmanaged VMs.

Restore spot VMs
Not supported. 

 Azure Backup restores spot VMs as regular Azure VMs.

Restore VMs in an Azure dedicated host
Supported.

When you're restoring an Azure VM through the Create new option, the VM can't be restored in the dedicated host, even when the restore is successful. To achieve this, we recommend that you restore as disks. While you're restoring as disks by using the template, create a VM in a dedicated host, and then attach the disks.

This is not applicable in a secondary region while you're performing cross-region restore.

Configure standalone Azure VMs in Windows Storage Spaces
Not supported.

Configure standalone Azure VMs in Windows Storage Spaces direct
Not supported.

Restore Virtual Machine Scale Sets
Supported for the flexible orchestration model to back up and restore a single Azure VM.

Restore with managed identities
Supported for managed Azure VMs. 

 Not supported for classic and unmanaged Azure VMs. 

 Cross-region restore isn't supported with managed identities. 

 Currently, this is available in all Azure public and national cloud regions. 

 Learn more.

Back up trusted launch VMs
Supported via Enhanced policy and Standard policy. 

 Feature details: 

 - Backup of a VM with Data disks having Security Type 'TrustedLaunch' or 'ConfidentialVM' is not supported. This can happen if you attach the OS disk from a Trusted Launch as a Data disk to another VM. 
 - Item-level restore is supported for the applicable scenarios. 

 Backup support via Enhanced policy: 

 - Azure portal, PowerShell, and REST API clients support trusted launch VM backup with Enhanced policy. 
 - The Azure portal allows you to enable backup through a Recovery Services vault, the VM management pane, and the VM creation pane. 
 - Resiliency supports backup, alerts, and monitoring for trusted launch VMs. 

 Backup support via Standard policy: 

 - CLI (version 2.73.0 and later), PowerShell (version Az 14.0.0 and later), and REST API (version 2025-01-01 and later) only support trusted launch VM backup with Standard policy. 
 - Trusted Launch virtual machines with standard policy use managed disk snapshots for Instant Restore. In this scenario, you incur Snapshot storage cost same as that of Enhanced policy. Learn more. 

 Note that migration of an existing Gen2 VM (protected by Azure Backup Standard policy) to Trusted Launch VM requires first switching to Enhanced policy.

Back up confidential VMs
Supported (in preview). Learn more about the supported scenarios.

## VM storage support

Component
Support

Azure VM data disks
Support for backup of Azure VMs is up to 32 disks.

 Backup of Azure VMs that use unmanaged disks isn't supported. Backup for classic VMs is no longer available. 

 To ensure continued functionality, migrate disks in Azure Classic Storage to Azure Resource Manager (ARM) Storage, because Classic Storage accounts don't support ARM-based Virtual Machines (VMs).

Data disk size
Individual disk size can be up to 64 TB and a maximum of 512 TB combined for all disks in a VM.

Storage type
Standard HDD, Standard SSD, Premium SSD, Premium SSD v2 and Ultra Disk. 

 Backup and restore of zone-redundant storage disks is supported.

Managed disks
Supported.

Encrypted disks
Supported.

 Azure VMs enabled with Azure Disk Encryption can be backed up (with or without the Microsoft Entra app).

 Encrypted VMs can't be recovered at the file or folder level. You must recover the entire VM.

 You can enable encryption on VMs that Azure Backup is already protecting. 

 You can back up and restore disks encrypted via platform-managed keys or customer-managed keys. You can also assign a disk-encryption set while restoring in the same region. That is, providing a disk-encryption set while performing cross-region restore is currently not supported. However, you can assign the disk-encryption set to the restored disk after the restore is complete.

Disks with a write accelerator enabled
Azure VMs with disk backup for a write accelerator became available in all Azure public regions on May 18, 2022. If disk backup for a write accelerator is not required as part of VM backup, you can choose to remove it by using the selective disk feature. 

Important 
 Virtual machines with write accelerator disks need internet connectivity for a successful backup, even though those disks are excluded from the backup.

Disks enabled for access with a private endpoint
Supported.

Disks with both public and private access disabled
Supported.

Backup and restore of deduplicated VMs or disks
Azure Backup doesn't support deduplication. For more information, see this article. 
 
 Azure Backup doesn't deduplicate across VMs in the Recovery Services vault. 
 
 If there are VMs in a deduplication state during restore, the files can't be restored because the vault doesn't understand the format. However, you can successfully perform the full VM restore.

Adding a disk to a protected VM
Supported.

Resizing a disk on a protected VM
Supported.

Shared storage
Backing up VMs by using Cluster Shared Volumes (CSV) or Scale-Out File Server isn't supported. CSV writers are likely to fail during backup. On restore, disks that contain CSV volumes might not come up.

Shared disks
Not supported. 

 - You can exclude shared disk with Enhanced policy and backup the other supported disks in the VM. 

 - You can use S2D to create a shared disk or standalone volumes by combining capacities from disks in different VMs. Azure Backup doesn't support backup of a shared volume (between VMs for database cluster or cluster Configuration) created using S2D.

Ultra Disks
Supported with Enhanced policy.Learn about the disk considerations for Azure VM. 

 - Configuration of Ultra Disk protection is supported via Recovery Services vault and via virtual machine blade. 

 - File-level restore is supported for disks with 512-byte or 4-KB logical sector sizes. See supported disks and recovery scope. 

 - GRS vaults and Cross-Region Restore are currently supported in the following regions for machines using Ultra Disks: South Central US, Brazil South, Canada East, Canada Central, East US2, South East Asia, West US, Central US, Korea South, Korea Central, South Central US, West Europe, North Central US, East Asia, USGov Texas, USGov Arizona, USGov Texas, West US2, North Europe, East US, West Central US, East US.

Premium SSD v2
Supported with Enhanced policy. Learn about the disk considerations for Azure VM. 

 - Configuration of Premium SSD v2 protection is supported via Recovery Services vault and via virtual machine blade. 

 - File-level restore is supported for disks with 512-byte or 4-KB logical sector sizes. See supported disks and recovery scope. 

 - GRS vaults and Cross-Region Restore are currently supported in the following regions for machines using Premium SSD v2 disks: Brazil South, Central US, East Asia, East US, East US2, North Central US, North Europe, South Central US, South East Asia, UK South, UK West, West Europe, West US, West US3, Norway West, Norway East, Japan West, Japan East.

Temporary disks
Azure Backup doesn't back up temporary disks.

NVMe/ephemeral disks
Supported.

Resilient File System (ReFS) restore
Supported. Volume Shadow Copy Service (VSS) supports app-consistent backups on ReFS.

Dynamic disk with spanned or striped volumes
Supported, unless you enable the selective disk feature on an Azure VM.

VMs with encryption at host
Supported

Disks with enabled Data Access with Microsoft Entra authentication for disk upload/download
Not Supported

Storage Replicas
Not supported

Performance-plus disks
Recovering from snapshot tier (instant restore) will recover disks as performance-plus disks. Recovering from vault does not respect the performance-plus flag and will restore disks as normal disks.

## VM network support

Component
Support

Number of network interfaces (NICs)
Supported up to the maximum number for a specific Azure VM size.

 NICs are created when the VM is created during the restore process.

 The number of NICs on the restored VM mirrors the number of NICs on the VM at the time of the backup. The number of NICs on the restore VM depends on the NICs in the restore point, which in turn depends on the NICs in the source VM at the time of backup.

External or internal load balancer
Supported. 

 Learn more about restoring VMs with special network settings.

Multiple reserved IP addresses
Supported. 

 Learn more about restoring VMs with special network settings.

VMs with multiple network adapters
Supported. 

 Learn more about restoring VMs with special network settings.

VMs with public IP addresses
Supported.

 Associate an existing public IP address with the NIC, or create an address and associate it with the NIC after the restore is done.

Network security group (NSG) on a NIC or subnet
Supported.

Static IP address
Not supported.

 A new VM that's created from a restore point is assigned a dynamic IP address.

 For classic VMs, you can't back up a VM with a reserved IP address and no defined endpoint.

Dynamic IP address
Supported.

 If the NIC on the source VM uses dynamic IP addressing, the NIC on the restored VM will also use it by default.

Azure Traffic Manager
Supported.

If the backed-up VM is in Traffic Manager, manually add the restored VM to the same Traffic Manager instance.

Azure DNS
Supported.

Custom DNS
Supported.

Outbound connectivity via HTTP proxy
Supported.

 An authenticated proxy isn't supported.

Virtual network service endpoints
Supported.

 Storage account settings for a firewall and a virtual network should allow access from all networks.

## Support for VM security and encryption

Azure Backup supports encryption for in-transit and at-rest data.

For network traffic to Azure:

- The Backup traffic from servers to the Recovery Services vault is encrypted via Advanced Encryption Standard 256.

- Backup data is sent over a secure HTTPS link.

- Backup data is stored in the Recovery Services vault in encrypted form.

- Only you have the encryption key to unlock this data. Microsoft can't decrypt the backup data at any point.

Warning

After you set up the vault, only you have access to the encryption key. Microsoft never maintains a copy and doesn't have access to the key. If the key is misplaced, Microsoft can't recover the backup data.

For data security:

- When you're backing up Azure VMs, you need to set up encryption within the virtual machine.

- Azure Backup supports Azure Disk Encryption, which uses BitLocker on virtual machines running Windows and uses dm-crypt on Linux virtual machines.

- On the back end, Azure Backup uses Azure Storage service-side encryption to help protect data at rest.

Machine
In transit
At rest

On-premises Windows machines without DPM or MABS

Azure VMs

On-premises or Azure VMs with DPM

On-premises or Azure VMs with MABS

## VM compression support

Azure Backup supports the compression of backup traffic. Note the following:

- For Azure VMs, the VM extension reads the data directly from the Azure storage account over the storage network. It isn't necessary to compress this traffic.

- If you're using DPM or MABS, you can save bandwidth by compressing the data before it's backed up.

Machine
Compress to DPM/MABS (TCP)
Compress to vault (HTTPS)

On-premises Windows machines without DPM or MABS
Not applicable

Azure VMs
Not applicable
Not applicable

On-premises or Azure VMs with DPM

On-premises or Azure VMs with MABS

## Next steps

- Back up Azure VMs.

- Back up Windows machines directly, without a backup server.

- Set up MABS for backup to Azure, and then back up workloads to MABS.

- Set up DPM for backup to Azure, and then back up workloads to DPM.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-16
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
