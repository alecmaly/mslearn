# https://learn.microsoft.com/en-us/azure/backup/backup-mabs-protection-matrix

Source: https://learn.microsoft.com/en-us/azure/backup/backup-mabs-protection-matrix

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
 

 

 

 

 
 
# MABS (Azure Backup Server) V4 (and later) protection matrix

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This article lists the various servers and workloads that you can protect with Azure Backup Server. The following matrix lists what can be protected with Azure Backup Server.

The following table lists the support matrix for MABS v4 (and later):

Scenario
Description

Workloads
The workload type of technology.

Version
Supported MABS version for the workloads.

MABS installation
The computer/location where you wish to install MABS.

Protection and recovery
List the detailed information about the workloads such as supported storage container or supported deployment.

Note

Support for the 32-bit protection agent isn't supported with MABS v4 (and later). See 32-Bit protection agent deprecation.

## Protection support matrix

The following sections details the protection support matrix for MABS:

- Applications Backup

- VM Backup

- Linux

## Applications Backup

Workload
Version
Azure Backup Server installation
Azure Backup Server
Protection and recovery

Client computers (64-bit)
Windows 11, Windows 10
Physical server 

 Hyper-V virtual machine 

 VMware virtual machine
V4
Volume, share, folder, files, deduped volumes 

 Protected volumes must be NTFS. FAT and FAT32 aren't supported. 

 Volumes must be at least 1 GB. Azure Backup Server uses Volume Shadow Copy Service (VSS) to take the data snapshot and the snapshot only works if the volume is at least 1 GB.

Servers (64-bit)
Windows Server 2025, 2022, 2019, 2016 

(Including Windows Server Core edition)
Azure virtual machine (when workload is running as Azure virtual machine) 

 Physical server 

 Hyper-V virtual machine 

 VMware virtual machine 

 Azure Stack
V4

MABS V4 UR1 and later for Windows Server 2025
Volume, share, folder, file 

 Deduped volumes (NTFS only) 

 System state and bare metal (Not supported when workload is running as Azure virtual machine).

SQL Server
SQL Server 2022, 2019, 2017
Physical server 

 Hyper-V virtual machine 

 VMware virtual machine 

 Azure virtual machine (when workload is running as Azure virtual machine) 

 Azure Stack
V4
All deployment scenarios: database 

 SQL database, stored on the Cluster Shared Volume and ReFS volumes. 

 MABS doesn't support SQL Server databases hosted on Scale-Out File Servers (SOFS). 

 MABS can't protect SQL server Distributed Availability Group (DAG) or Availability Group (AG), where the role name on the failover cluster is different than the named AG on SQL.

Exchange
Exchange 2019, 2016
Physical server 

 Hyper-V virtual machine 

 VMware virtual machine 

 Azure Stack 

 Azure virtual machine (when workload is running as Azure virtual machine)
V4
Protect (all deployment scenarios): Standalone Exchange server, database under a database availability group (DAG) 

 Recover (all deployment scenarios): Mailbox, mailbox databases under a DAG 

 Backup of Exchange over ReFS is supported with MABS v3 UR1

SharePoint
SharePoint 2019, 2016 with latest SPs
Physical server 

 Hyper-V virtual machine 

 VMware virtual machine 

 Azure virtual machine (when workload is running as Azure virtual machine) 

 Azure Stack
V4
Protect (all deployment scenarios): Farm, frontend web server content 

 Recover (all deployment scenarios): Farm, database, web application, file, or list item, SharePoint search, frontend web server 

 Protecting a SharePoint farm that's using the SQL Server 2012 Always On feature for the content databases isn't supported.

## VM Backup

Workload
Version
Azure Backup Server installation
Supported Azure Backup Server
Protection and recovery

Hyper-V host - MABS protection agent on Hyper-V host server, cluster, or VM
Windows Server 2025, 2022, 2019, 2016
Physical server 

 Hyper-V virtual machine 

 VMware virtual machine
V4

MABS V4 UR1 and later for Windows Server 2025
Protect: Virtual machines, cluster shared volumes (CSVs) 

 Recover: Virtual machine, Item-level recovery of files and folders available only for Windows, volumes, virtual hard drives 

 Note that Item Level Recovery isn't supported for Virtual Machine volumes that have BitLocker enabled.

Azure Local
Lastest Major Release Learn More
Physical server 

 Hyper-V / Azure Local virtual machine 

 VMware virtual machine
V4
Protect: Virtual machines, cluster shared volumes (CSVs) 

 Recover: Virtual machine, Item-level recovery of files and folders available only for Windows, volumes, virtual hard drives 

 Recovery of Arc VMs is supported in a limited capacity in Azure Local, version 23H2. Learn more. 

 Note that Application Control should be in audit mode for agent installation.

VMware VMs
VMware server 6.5, 6.7, 7.0, 8.0, 9.0 (Licensed Version)
Hyper-V virtual machine 

 VMware virtual machine
V4

V4 UR2 or later for vSphere 9.0
Protect: VMware VMs on cluster-shared volumes (CSVs), NFS, and SAN storage 

 Recover: Virtual machine, Item-level recovery of files and folders available only for Windows, volumes, virtual hard drives 

 Note that Item Level Recovery isn't supported for Virtual Machine volumes that have BitLocker enabled. 

 VMware vApps aren't supported. 

 vSphere 8.0 DataSets feature isn't supported for backup.

Note

MABS doesn't support backup of virtual machines with pass-through disks or those that use a remote VHD. We recommend that in these scenarios you use guest-level backup using MABS, and install an agent on the virtual machine to back up the data.

## Linux

Workload
Version
Azure Backup Server installation
Supported Azure Backup Server
Protection and recovery

Linux
Linux running as Hyper-V or VMware or Stack guest
Physical server, On-premises Hyper-V VM, Stack VM or VMware VM running Windows Server.
V4

MABS V4 UR1 and later for Windows Server 2025 Hyper-V hosts
Hyper-V must be running on Windows Server 2016, Windows Server 2019, Windows Server 2022, or Windows Server 2025. Protect: Entire virtual machine 

 Recover: Entire virtual machine 

 Only file-consistent snapshots are supported. 

 For a complete list of supported Linux distributions and versions, see the article, Linux on distributions endorsed by Azure.

## Operating systems and applications at end of support

Support for the following operating systems and applications in MABS are deprecated. We recommended you to upgrade them to continue protecting your data.

If the existing commitments prevent upgrading Windows Server or SQL Server, migrate them to Azure and use Azure Backup to protect the servers. For more information, see migration of Windows Server, apps and workloads.

For on-premises or hosted environments that you can't upgrade or migrate to Azure, activate Extended Security Updates for the machines for protection and support. Note that only limited editions are eligible for Extended Security Updates. For more information, see Frequently asked questions.

Workload
Version
Azure Backup Server installation
Azure Backup Server
Protection and recovery

Servers (64-bit)
Windows Server 2008 R2 SP1, Windows Server 2008 SP2 (You need to install Windows Management Framework), Windows Server 2012, Windows Server 2012 R2.
Physical server 

 Hyper-V virtual machine 

 VMware virtual machine
Volume, share, folder, file, system state/bare metal

Note

Windows Server 2008, 2008 R2, 2012 and 2012 R2 have reached End of Support (EOS). Review your usage and plan OS upgrades and migrations accordingly. For more information, see End of support for:

- Windows Server 2008 and Windows Server 2008 R2

- Windows Server 2012

- Windows Server 2012 R2

Perform in-place upgrade to Windows Server 2016, 2019, 2022, or 2025.

## Cluster support

Azure Backup Server can protect data in the following clustered applications:

- File servers

- SQL Server

- Hyper-V - If you protect a Hyper-V cluster using scaled-out MABS protection agent, you can't add secondary protection for the protected Hyper-V workloads.

- Exchange Server - Azure Backup Server can protect non-shared disk clusters for supported Exchange Server versions (cluster-continuous replication), and can also protect Exchange Server configured for local continuous replication.

- SQL Server - Azure Backup Server doesn't support backing up SQL Server databases hosted on cluster-shared volumes (CSVs).

Note

MABS V4 supports the protection of Hyper-V virtual machines and SQL Server Failover Cluster Instance (FCI) on Cluster Shared Volumes (CSVs). Protection of other workloads hosted on CSVs isn't supported.

Azure Backup Server can protect cluster workloads that are located in the same domain as the MABS server, and in a child or trusted domain. If you want to protect data sources in untrusted domains or workgroups, use NTLM or certificate authentication for a single server, or certificate authentication only for a cluster.

## Data protection issues

- MABS can't back up VMs using shared drives (which are potentially attached to other VMs) as the Hyper-V VSS writer can't back up volumes that are backed up by shared VHDs.

- When you protect a shared folder, the path to the shared folder includes the logical path on the volume. If you move the shared folder, protection will fail. If you must move a protected shared folder, remove it from its protection group and then add it to protection after the move. Also, if you change the path of a protected data source on a volume that uses the Encrypting File System (EFS) and the new file path exceeds 5120 characters, data protection will fail.

- You can't change the domain of a protected computer and continue protection without disruption. Also, you can't change the domain of a protected computer and associate the existing replicas and recovery points with the computer when it's reprotected. If you must change the domain of a protected computer, then first remove the data sources on the computer from protection. Then protect the data source on the computer after it has a new domain.

- You can't change the name of a protected computer and continue protection without disruption. Also, you can't change the name of a protected computer and associate the existing replicas and recovery points with the computer when it's reprotected. If you must change the name of a protected computer, then first remove the data sources on the computer from protection. Then protect the data source on the computer after it has a new name.

- MABS automatically identifies the time zone of a protected computer during installation of the protection agent. If a protected computer is moved to a different time zone after protection is configured, ensure that you change the computer time in Control Panel. Then update the time zone in the MABS database.

- MABS can protect workloads in the same domain as the MABS server, or in child and trusted domains. You can also protect the following workloads in workgroups and untrusted domains using NTLM or certificate authentication:

- SQL Server

- File Server

- Hyper-V

These workloads can be running on a single server or in a cluster configuration. To protect a workload that isn't in a trusted domain, see Prepare computers in workgroups and untrusted domains for exact details of what's supported and what authentication is required.

## Unsupported data types

MABS doesn't support protecting the following data types:

- Hard links

- Reparse points, including DFS links and junction points

- Mount point metadata - A protection group can contain data with mount points. In this case DPM protects the mounted volume that is the target of the mount point, but it doesn't protect the mount point metadata. When you recover data containing mount points, you'll need to manually recreate your mount point hierarchy.

- Data in mounted volumes within mounted volumes

- Recycle Bin

- Paging files

- System Volume Information folder. To protect system information for a computer, you'll need to select the computer's system state as the protect group member.

- Non-NTFS volumes

- Files containing hard links or symbolic links from Windows Vista.

- Data on file shares hosting UPDs (User Profile Disks)

- Files with any of the following combinations of attributes:

- Encryption and reparse

- Encryption and Single Instance Storage (SIS)

- Encryption and case-sensitivity

- Encryption and sparse

- Case-sensitivity and SIS

- Compression and SIS

## Next steps

- Support matrix for backup with Microsoft Azure Backup Server or System Center DPM.

## Related content

- Run an unattended installation of MABS.

- Back up a SharePoint farm on Azure Stack.

- Back up SQL Server on Azure Stack.

- Azure Backup Server V3 RTM protection matrix.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-10-17
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
