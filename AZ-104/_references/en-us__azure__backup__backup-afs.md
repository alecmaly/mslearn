# https://learn.microsoft.com/en-us/azure/backup/backup-afs

Source: https://learn.microsoft.com/en-us/azure/backup/backup-afs

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
 

 

 

 

 
 
# Back up Azure Files

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This article describes how to back up Azure Files from the Azure portal. You can also back up Azure Files using CLI, Azure PowerShell, and REST API.

Azure Files backup is a native cloud solution that protects your data and eliminates on-premises maintenance overheads. Azure Backup seamlessly integrates with Azure File Sync, centralizing your file share data and backups. The simple, reliable, and secure solution allows you to protect your enterprise file shares using snapshot and vaulted backups, ensuring data recovery for accidental or malicious deletion.

Azure Backup supports configuring snapshot and vaulted backups for Azure Files in your storage accounts. You can:

- Define backup schedules and retention settings.

- Store backup data in the Recovery Service vault, retaining it for up to 10 years.

Note

Snapshot backup for NFS Azure file shares is currently in private preview. The preview is intended for evaluation with non-production subscriptions. To request access, complete the preview sign-up form.

Vaulted backup support for NFS Azure file shares is coming soon and isn't yet available in private preview.

## Prerequisites

- Ensure the file share is present in one of the supported storage account types. Review the support matrix.

- Identify or create a Recovery Services vault in the same region and subscription as the storage account that hosts the file share.

- Create a backup policy for protection of Azure Files.

- If the storage account access has restrictions, check the firewall settings of the account to ensure the exception Allow Azure services on the trusted services list to access this storage account is in grant state. You can refer to this link for the steps to grant an exception.

- Ensure the storage account either permits access via account keys or has public network access disabled.

- Ensure that the target storage account has the supported configurations.

Important

To perform Cross Subscription Backup (CSB) for protecting Azure Files in another subscription, ensure you register `Microsoft.RecoveryServices` in the subscription of the file share in addition to the given prerequisites.

To learn about the supported Azure Files backup and restore scenarios, region availability, and limitations, see the support matrix. For common questions, see the frequently asked questions.

## Configure the backup

You can configure snapshot backup and vaulted backup for Azure Files from the Recovery Services vault or File share pane.

Choose an entry point

- 
Recovery Services vault

- 
File share pane

To configure backup for multiple file shares from the Recovery Services vault, follow these steps:

- In the Azure portal, go to the Recovery Services vault and select +Backup.

- On the Backup Goal pane, select Azure Files (Azure Storage) as the datasource type, select the vault that you want to protect the file shares with, and then select Continue.

- On the Configure backup pane, click Select to select the storage account that contains the file shares to be backed up.

The Select storage account pane opens, which lists a set of discovered supported storage accounts. They're either associated with this vault or present in the same region as the vault, but not yet associated with any Recovery Services vault.

- On the Select storage account pane, by default it list the storage accounts from the current subscription. Select an account, and select OK.

If you want to configure the backup operation with a storage account in a different subscription (Cross Subscription Backup), choose the other subscription from the Subscription filter. The storage accounts from the selected subscription appear.

Note

If a storage account is present in a different region than the vault, then the storage account doesn't appear in the discovery list.

- On the Configure Backup pane, under the FileShares to Backup section, select the file shares type you want to back up, and then select Add.

- The Select file shares context pane opens. Azure searches the storage account for file shares that can be backed up. If you recently added your file shares and don't see them in the list, allow some time for the file shares to appear.

- On the Select file shares pane, from the file shares list, select one or more file shares you want to back up, and then select OK.

- On the Configure Backup pane, under Policy Details, choose an existing backup policy from the list for your file share protection or create a new policy.

To create a new backup policy, you can configure the following attributes in the backup policy:

- On the Configure Backup pane, select Create new under Policy Details.

- On the Create policy pane, provide the policy name.

- On Backup tier, select one of the following tiers:

- Snapshot: Enables only snapshot-based backups that are stored locally and can only provide protection during accidental deletions.

- Vault-Standard: Provides comprehensive data protection.

- Configure the backup schedule as per the requirement. You can configure up to 24 snapshots per day. The snapshots are taken as per the schedule defined in the policy. For vaulted backup, the data from the last snapshot of the day is transferred to the vault.

- Configure the Snapshot retention and Vault retention duration to determine the expiry date of the recovery points.

Note

The vault tier provides longer retention than the snapshot tier.

- Select OK to create the backup policy.

- On the Configure Backup pane, select Enable Backup to start protecting the file share.

The following steps explain how you can configure backup for individual file shares from the respective file share pane:

- In the Azure portal, open the storage account hosting the file share you want to back up.

- On the storage account, select the File shares tile.

Alternatively, you can go to File shares from the table of contents for the storage account.

- On the File share settings pane, all the file shares present in the storage account appear. Select the file share you want to back up.

- On the file share pane, under the Operations section, select Backup.

The Azure Backup configuration pane appears.

- To select the Recovery Services vault, consider one of the following methods:

- If you already have a vault, click Select existing under Recovery Services vault, and choose one of the existing vaults from Vault Name drop down menu.

- If you don't have a vault, select Create new under Recovery Services vault, and then specify a name for the vault. The vault gets created in the same region as the file share. By default, the vault is created in the same resource group as the file share. If you want to choose a different resource group, under the Resource Type dropdown, select Create new, and then specify a name for the resource group. Select OK to continue.

Important

If the storage account is registered with a vault or contains protected shares, the Recovery Services vault name is prepopulated and can't be edited. Learn more here.

- Under Choose backup policy, select an existing backup policy from the list or create a new backup policy for Azure Files.

To create a new backup policy, follow these steps:

- Select Create a new policy.

- On the Create policy pane, provide the policy name.

- On Backup tier, select one of the following tiers:

- Snapshot: Enables only snapshot-based backups that are stored locally and can only provide protection for accidental deletions.

- Vault-Standard: Provides comprehensive data protection.

- Configure the backup schedule as per your requirement. You can configure up to 24 snapshots per day. The snapshots are taken as per the schedule defined in the policy. For vaulted backup, the data from the last snapshot of the day is transferred to the vault.

- Configure the Snapshot retention and Vault retention duration to determine the expiry date of the recovery points.

Note

The vault tier provides longer retention than the snapshot tier.

- Select OK to create the backup policy.

- On the Azure Files datasource pane, select Enable Backup to start protecting the file share.

- You can track the configuration progress in the portal notifications, or by monitoring the backup jobs under the vault you're using to protect the file share.

- After the configuration of backup is complete, select Backup under the Operations section of the file share pane.

The context pane opens. From the list of Vault Essentials, you can trigger on-demand backup and restore operations.

Once the backup configuration is complete, you can run an on-demand backup to create the recovery point.

## Next steps

- Restore Azure Files using Azure portal.

- Restore Azure Files using Azure PowerShell, Azure CLI, REST API.

- Manage Azure Files backups using Azure portal, Azure PowerShell, Azure CLI, REST API.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-03
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
