# https://learn.microsoft.com/en-us/azure/backup/backup-azure-vms-agentless-multi-disk-crash-consistent-overview

Source: https://learn.microsoft.com/en-us/azure/backup/backup-azure-vms-agentless-multi-disk-crash-consistent-overview

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
 

 

 

 

 
 
# What is agentless multidisk crash-consistent backup for Azure VMs?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Backup supports agentless virtual machine (VM) backups by using multidisk crash-consistent restore points.

The Enhanced VM backup policy enables you to configure the consistency type of backups as application-consistent or crash-consistent restore points for Azure VMs. For supported VMs, Azure Backup can also retry the backup operation by using a crash-consistent snapshot if the application-consistent snapshot fails.

Note

The agentless multi-disk crash consistent VM backup feature is generally available. This release includes changes to billing; see the pricing details.

## When do I choose crash-consistent backup over application-consistent backup?

Choose to perform crash-consistent backup in the following scenarios:

- If your workload is performance sensitive and can tolerate recovery from crash-consistent backups, crash-consistent backups help quiesce VM I/O for a shorter period during backup. Crash-consistent backup doesn't use Volume Shadow Copy Service (VSS) (for Windows) or fsfreeze (for Linux) to avoid the associated quiescing delays.

- If you don't want to install the VM Agent or snapshot extension required for application-consistent or file-system-consistent snapshots in your Azure VM, use crash-consistent backups for an agentless backup solution.

- If your operating system isn't supported for application or file-system-consistent backup, use crash-consistent backups. Crash-consistent backup is operating system agnostic as it doesn't rely on the VM agent or snapshot extension.

## When do I not use crash-consistent backups?

Don't use crash-consistent backups in the following scenarios:

- Your application can't tolerate recovery from crash-consistent backups.

- You use pre/post scripts for Linux VM backups.

- You use read/write host caching and your workload is sensitive to cached data not being flushed before backup.

## Pricing for agentless multi-disk crash-consistent backup

With general availability of agentless multi-disk crash consistent VM backup, you incur charges based on the size of the backed-up data, as detailed here. For each VM protected with agentless backup, a protected instance fee applies, similar to application-consistent VM backups. This fee depends on the VMâs used size, calculated as 50 percent of its provisioned size.

## Supported scenarios for agentless multi-disk crash-consistent VM backup

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

Note

For disks configured with read/write host caching, multi-disk crash consistency can't be guaranteed because writes that occur while the snapshot is taken might not be acknowledged by Azure Storage. If maintaining consistency is crucial, we recommend that you use the application-consistent backups.

## Next steps

Back up Azure VM with agentless multi-disk crash-consistent backup

 
 

 
 

 

 
 
 
 
 
 
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
 2026-07-30
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
