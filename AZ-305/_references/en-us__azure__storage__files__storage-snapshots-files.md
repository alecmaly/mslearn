# https://learn.microsoft.com/en-us/azure/storage/files/storage-snapshots-files

Source: https://learn.microsoft.com/en-us/azure/storage/files/storage-snapshots-files

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
 

 

 

 

 
 
# Use share snapshots with Azure Files

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 âï¸ Applies to: Classic SMB and NFS file shares created with the Microsoft.Storage resource provider

âï¸ Applies to: File shares created with the Microsoft.FileShares resource provider

Azure Files provides the capability to take snapshots of SMB and NFS file shares. Share snapshots capture the share state at that point in time. This article describes the capabilities that file share snapshots provide and how you can use them to recover previous versions of files.

Important

Share snapshots don't prevent accidental deletion of a file share or storage account. To help protect a storage account from accidental deletion, enable soft delete or lock the storage account or the resource group.

## When to use share snapshots

### Protect against application error and data corruption

Applications that use file shares perform operations such as writing, reading, storage, transmission, and processing. If an application is misconfigured or an unintentional bug is introduced, accidental overwrite or damage can happen to a few blocks. To help protect against these scenarios, take a share snapshot before you deploy new application code. If a bug or application error is introduced by the new deployment, you can go back to a previous version of your data on that file share.

### Protect against accidental deletions or unintended changes

Imagine that you're working on a text file in a file share. After you close the text file, you lose the ability to undo your changes. In these cases, you need to recover a previous version of the file. You can use share snapshots to recover previous versions of the file if it's accidentally renamed or deleted.

### General backup purposes

After you create a file share, you can periodically create a share snapshot of the file share to use it for data backup. A share snapshot, when taken periodically, helps maintain previous versions of data that can be used for future audit requirements or disaster recovery. Use Azure file share backup for taking and managing snapshots. You can also take and manage snapshots yourself by using the Azure portal, Azure PowerShell, or Azure CLI.

## Share snapshot capabilities

A share snapshot is a point-in-time, read-only copy of your data. Share snapshot capability is provided at the file share level. You can use snapshots to restore individual files. For SMB shares that are approved for the limited preview, you can also revert an entire share to a snapshot by using the FileREST API. Share snapshots have the same redundancy as the Azure file share for which they were taken. If you select geo-redundant storage for your account, your share snapshot is also stored redundantly in the paired region.

You can restore a complete file share by using SMB, NFS, REST API, the Azure portal, the client library, or PowerShell/CLI. You can view snapshots of a share by using the REST API, SMB, or NFS. You can retrieve the list of versions of the directory or file, and you can mount a specific version directly as a drive (only available on Windows - see Share snapshot limits).

After you create a share snapshot, you can read, copy, or delete it, but you can't modify it. You can't copy a whole share snapshot to another storage account. You have to copy that data file by file, by using AzCopy or other copying mechanisms.

A share snapshot of a file share is identical to its base file share. The only difference is that a DateTime value is appended to the share URI to indicate the time at which the share snapshot was taken. For example, if a file share URI is `https://storagesample.file.core.windows.net/myshare`, the share snapshot URI is similar to:

`https://storagesample.file.core.windows.net/myshare?sharesnapshot=2024-12-09T17:44:51.0000000Z
`

Share snapshots persist until you explicitly delete them, or until the file share is deleted. You can't delete a file share and keep the share snapshots. The delete workflow automatically deletes the snapshots when you delete the share. You can enumerate the snapshots associated with the base file share to track your current snapshots.

When you create a share snapshot of a file share, the files in the share's system properties are copied to the share snapshot with the same values. The base files and the file share's metadata are also copied to the share snapshot, unless you specify separate metadata for the share snapshot when you create it.

## Share snapshot space usage

Share snapshots are incremental. Only the data that changed after your most recent share snapshot is saved. This feature minimizes the time required to create the share snapshot and saves on storage costs, because you pay only for the changed content. Any write operation to the object or property, or metadata update operation, counts toward "changed content" and is stored in the share snapshot.

To conserve space, you can delete the share snapshot for the period when the churn was highest.

Even though share snapshots are saved incrementally, you need to retain only the most recent share snapshot to restore the share. When you delete a share snapshot, only the data unique to that share snapshot is removed. Active snapshots contain all the information that you need to browse and restore your data (from the time the share snapshot was taken) to the original location or an alternate location. You can restore at the item level.

Snapshots don't count towards the maximum share size limit. There's no limit to how much space share snapshots occupy in total, or that share snapshots of a particular file share can consume. Storage account limits still apply.

## Share snapshot limits

Azure Files supports up to 200 share snapshots per share. After reaching 200 share snapshots, you must delete older share snapshots to create new ones. You can retain snapshots for up to 10 years.

There's no limit to the simultaneous calls for creating share snapshots.

Only file management APIs (`AzRmStorageShare`) are supported for NFS Azure file share snapshots. File data plane APIs (`AzStorageShare`) aren't supported.

## Copying data back to a share from share snapshot

Copy operations that involve files and share snapshots follow these rules:

- You can copy individual files in a file share snapshot over to its base share or any other location. You can restore an earlier version of a file or restore the complete file share by copying file by file from the share snapshot. The share snapshot isn't promoted to base share.

- The share snapshot remains intact after copying, but the base file share is overwritten with a copy of the data that was available in the share snapshot. All the restored files count toward "changed content."

- You can copy a file in a share snapshot to a different destination with a different name. The resulting destination file is a writable file and not a share snapshot. In this case, your base file share remains intact.

- When a destination file is overwritten with a copy, any share snapshots associated with the original destination file remain intact.

## Copying data back to a local drive from share snapshot

If you want to restore data from a snapshot of an SMB Azure file share to a local drive on Windows, you can use Robocopy to copy files and folders from the snapshot.

On Windows, you can access SMB file share snapshots from the Previous Versions tab in Windows File Explorer. When you access a snapshot view by using this method, you can copy files and folders to a local path by using standard file operations or Robocopy.

If you run Robocopy from an elevated command prompt, mapped drives might not be accessible, and referencing a drive letter might fail. In that case, use a UNC path that references the snapshot view. Ensure the path references the snapshot and not the live file share. If you reference the live file share instead of the snapshot, the copy operation uses the current state of the file share rather than the point-in-time state captured in the snapshot.

## Share snapshot best practices

Automate backups for data recovery whenever possible. Automated actions are more reliable than manual processes, so automation helps improve data protection and recoverability. For automation, you can use Azure file share backup (SMB file shares only), the REST API, the Client SDK, or scripting.

Before you deploy the share snapshot scheduler, carefully consider your share snapshot frequency and retention settings to avoid incurring unnecessary charges.

## SMB file share snapshots

Users of SMB Azure file shares can create, list, delete, and restore from share snapshots.

### Revert an SMB file share to a snapshot (preview)

The SMB share revert feature restores an entire live file share to the data and properties captured in a snapshot of that same share. Revert is available in a limited preview to approved subscriptions through the FileREST API.

Note

Access to the preview is enabled per subscription. Complete the preview sign-up form: Sign up for Preview: Azure Files Share Revert.

The team enables the preview for approved subscriptions and contacts you when the feature is available.

Important

This feature is currently in preview. See the Supplemental Terms of Use for Microsoft Azure Previews for legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

Share revert has the following behavior and limitations:

- Revert applies to the entire SMB file share. You can't revert an individual directory or file. To recover individual items, use the restore options described in Restore from an SMB file share snapshot.

- The source must be a snapshot of the same file share. Reverting from a snapshot in another share or storage account isn't supported.

- The restored data and properties match the source snapshot, including file and directory attributes, access control lists (ACLs), and timestamps.

- Existing share snapshots are retained. During asynchronous processing, Azure Files blocks I/O and then creates another snapshot that captures the current live share state before applying the source snapshot.

- You can start up to eight share revert operations per day for a file share.

Warning

The live share is blocked from read and write I/O while a revert is in progress. Azure Files blocks new SMB and FileREST I/O and forcibly closes existing SMB handles and REST leases. Disconnect clients and close handles before starting a revert to minimize disruption.

### Create an SMB file share snapshot

You can create a snapshot of an SMB Azure file share by using the Azure portal, Azure PowerShell, or Azure CLI.

- 
Azure portal

- 
Azure PowerShell

- 
Azure CLI

To create a snapshot of an existing file share, sign in to the Azure portal and follow these steps.

- In the portal, go to your file share.

- Select Snapshots, select + Add snapshot, and then select OK.

To create a snapshot of an existing file share, run the following PowerShell command. Replace `<resource-group-name>`, `<storage-account-name>`, and `<file-share-name>` with your own values.

`New-AzRmStorageShare -ResourceGroupName "<resource-group-name>" -StorageAccountName "<storage-account-name>" -Name "<file-share-name>" -Snapshot
`

To create a snapshot of an existing file share, run the following Azure CLI command. Replace `<file-share-name>` and `<storage-account-name>` with your own values.

`az storage share snapshot --name <file-share-name> --account-name <storage-account-name>
`

### List SMB file share snapshots

You can list all the snapshots for a file share by using the Azure portal, Azure PowerShell, or Azure CLI.

- 
Azure portal

- 
Azure PowerShell

- 
Azure CLI

To list all the snapshots for an existing file share, sign in to the Azure portal and follow these steps:

- In the portal, go to your file share.

- On your file share, select Snapshots.

- On the Snapshots tab, select a snapshot from the list.

- Open that snapshot to browse the files it contains.

To list all file shares and snapshots in a storage account, run the following PowerShell command. Replace `<resource-group-name>` and `<storage-account-name>` with your own values.

`Get-AzRmStorageShare -ResourceGroupName "<resource-group-name>" -StorageAccountName "<storage-account-name>" -IncludeSnapshot
`

To list all file shares and snapshots in a storage account, run the following Azure CLI command. Replace `<storage-account-name>` with your own value.

`az storage share list --account-name <storage-account-name> --include-snapshots
`

### Restore from an SMB file share snapshot

To restore files from a snapshot, sign in to the Azure portal and follow these steps:

- In the portal, go to your file share.

- On your file share, select Snapshots.

- From the file share snapshot tab, right-click the file you want to restore, and select the Restore button.

- Select Overwrite original file and then select OK.

The unmodified version of the file is now restored.

### Delete SMB file share snapshots

Existing share snapshots are never overwritten. You must delete them explicitly. You can delete share snapshots by using the Azure portal, Azure PowerShell, or Azure CLI.

Before you can delete a share snapshot, you need to remove any locks on the storage account. Go to the storage account and select Settings > Locks. If any locks are listed, delete them.

- 
Azure portal

- 
Azure PowerShell

- 
Azure CLI

To delete a snapshot of an existing file share, sign in to the Azure portal and follow these steps.

- In the search box at the top of the Azure portal, type and select storage accounts.

- Select the storage account that contains the file share for which you want to delete snapshots.

- From the service menu, under Data storage, select Classic file shares.

- Select the file share for which you want to delete one or more snapshots, and then select Operations > Snapshots. The portal lists any existing snapshots for the file share.

- Select the snapshots that you want to delete, and then select Delete.

To delete a file share snapshot, run the following PowerShell command. Replace `<resource-group-name>`, `<storage-account-name>`, and `<file-share-name>` with your own values. The `SnapshotTime` parameter must follow the correct name format, such as `2024-05-10T08:04:08Z`.

`Remove-AzRmStorageShare -ResourceGroupName "<resource-group-name>" -StorageAccountName "<storage-account-name>" -Name "<file-share-name>" -SnapshotTime "<snapshot-time>"
`

To delete a file share and all its snapshots, run the following PowerShell command. Replace `<resource-group-name>`, `<storage-account-name>`, and `<file-share-name>` with your own values.

`Remove-AzRmStorageShare -ResourceGroupName "<resource-group-name>" -StorageAccountName "<storage-account-name>" -Name "<file-share-name>" -Include Snapshots
`

To delete a file share snapshot, run the following Azure CLI command. Replace `<storage-account-name>` and `<file-share-name>` with your own values. The `--snapshot` parameter must follow the correct name format, such as `2024-05-10T08:04:08Z`.

`az storage share delete --account-name <storage-account-name> --name <file-share-name> --snapshot <snapshot-time>
`

To delete a file share and all its snapshots, run the following Azure CLI command. Replace `<storage-account-name>` and `<file-share-name>` with your own values.

`az storage share delete --account-name <storage-account-name> --name <file-share-name> --delete-snapshots include
`

### Use an SMB file share snapshot in Windows

Just like with on-premises Volume Shadow Copy (VSS) snapshots, you can view the snapshots from your mounted Azure file share by using the Previous versions tab in Windows.

- In File Explorer, locate the mounted share.

- Browse to the item or parent item that you need to restore. Right-click the item and select Properties from the menu.

- Select Previous Versions to see the list of share snapshots for this directory.

- Select Open to open the snapshot.

- Select Restore. This action copies the contents of the entire directory recursively to the original location at the time the share snapshot was created.

Note

If your file didn't change, you won't see a previous version for that file because that file is the same version as the snapshot. This behavior is consistent with how it works on a Windows file server.

### Mount an SMB file share snapshot on Linux

To mount a specific snapshot of an SMB Azure file share on Linux, include the `snapshot` option in the `mount` command. The `snapshot` option specifies the time when the snapshot was created, in a format such as `@GMT-2023.01.05-00.08.20`. The Linux kernel supports the `snapshot` option starting with version 4.19.

After you create the file share snapshot, follow these instructions to mount it.

- In the Azure portal, go to the storage account that contains the file share you want to mount a snapshot of.

- From the service menu, under Data storage, select Classic file shares.

- Select the file share.

- Select Operations > Snapshots and take note of the name of the snapshot you want to mount. The snapshot name is a GMT timestamp, such as in the following screenshot.

- Convert the timestamp to the format expected by the `mount` command, which is @GMT-year.month.day-hour.minutes.seconds. In this example, convert 2023-01-05T00:08:20.0000000Z to @GMT-2023.01.05-00.08.20.

- Run the `mount` command using the GMT time to specify the `snapshot` value. Replace `<storage-account-name>`, `<file-share-name>`, and the GMT timestamp with your values. The `.cred` file contains the credentials to use to mount the share.

`sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<file-share-name> /media/<file-share-name>/snapshot1 -o credentials=/etc/smbcredentials/snapshottestlinux.cred,snapshot=@GMT-2023.01.05-00.08.20
`

- If you can browse the snapshot under the path `/media/<file-share-name>/snapshot1`, the mount succeeded.

If the mount fails, see Troubleshoot Azure Files connectivity and access issues (SMB).

## NFS file share snapshots

Users of NFS Azure file shares (both classic file shares, and file shares with Microsoft.FileShares) can create, list, delete, and restore from share snapshots.

Important

You should mount your file share before creating snapshots. If you create a new NFS file share and take snapshots before mounting the share, attempting to list the snapshots for the share returns an empty list. Delete any snapshots taken before the first mount and re-create them after you mount the share.

### NFS snapshot limitations

Azure Backup doesn't support NFS file shares.

NFS Azure file share snapshots are available in all Azure public cloud regions.

### Create a snapshot of an NFS classic file share

You can create a snapshot of an NFS classic file share by using the Azure portal, Azure PowerShell, or Azure CLI.

- 
Azure portal

- 
Azure PowerShell

- 
Azure CLI

To create a snapshot of an existing classic file share, sign in to the Azure portal and follow these steps.

- In the search box at the top of the Azure portal, type and select storage accounts.

- Select the FileStorage storage account that contains the NFS classic file share that you want to take a snapshot of.

- From the service menu, under Data storage, select Classic file shares.

- Select the classic file share that you want to snapshot, and then select Operations > Snapshots.

- Select + Add snapshot. Add an optional comment, and select OK.

To create a snapshot of an existing classic file share, run the following PowerShell command. Replace `<resource-group-name>`, `<storage-account-name>`, and `<file-share-name>` with your own values.

`New-AzRmStorageShare -ResourceGroupName "<resource-group-name>" -StorageAccountName "<storage-account-name>" -Name "<file-share-name>" -Snapshot
`

To create a snapshot of an existing classic file share, run the following Azure CLI command. Replace `<file-share-name>` and `<storage-account-name>` with your own values.

`az storage share snapshot --name <file-share-name> --account-name <storage-account-name>
`

### List NFS classic file share snapshots

You can list all the snapshots for a classic file share by using the Azure portal, Azure PowerShell, or Azure CLI.

- 
Azure portal

- 
Azure PowerShell

- 
Azure CLI

To list all the snapshots for an existing classic file share, sign in to the Azure portal and follow these steps.

- In the search box at the top of the Azure portal, type and select storage accounts.

- Select the storage account that contains the NFS classic file share that you want to list the snapshots for.

- From the service menu, under Data storage, select Classic file shares.

- Select the classic file share for which you want to list the snapshots.

- Select Operations > Snapshots, and the portal lists any existing snapshots for the classic file share.

To list all classic file shares and snapshots in a storage account, run the following PowerShell command. Replace `<resource-group-name>` and `<storage-account-name>` with your own values.

`Get-AzRmStorageShare -ResourceGroupName "<resource-group-name>" -StorageAccountName "<storage-account-name>" -IncludeSnapshot
`

To list all classic file shares and snapshots in a storage account, run the following Azure CLI command. Replace `<storage-account-name>` with your own value.

`az storage share list --account-name <storage-account-name> --include-snapshots
`

### Restore from an NFS classic file share snapshot

To mount an NFS classic file share snapshot to a Linux VM (NFS client) and restore files, follow these steps:

- Run the following command in a console. See NFS mount options for other recommended mount options. To improve copy performance, mount the snapshot by using nconnect to use multiple TCP channels. Replace the placeholder values, including brackets, with your own values. Replace `/media/nfs` with your local mount path, if different.

`sudo mount -o vers=4,minorversion=1,proto=tcp,sec=sys <StorageAccountName>.file.core.windows.net:/<StorageAccountName>/<FileShareName> /media/nfs
`

- Change the directory to `/media/nfs/.snapshots` so you can view the available snapshots. The `.snapshots` directory is hidden by default, but you can access and read from it like any directory. If you just created the snapshot, wait at least 30 seconds for the `.snapshots` directory to become available.

`cd /media/nfs/.snapshots
`

- List the contents of the `.snapshots` directory.

`ls
`

- Each snapshot has its own directory that serves as a recovery point. Change to the snapshot directory for which you want to restore files.

`cd <snapshot-name>
`

- List the contents of the directory to view a list of files and directories that you can recover.

`ls
`

- Copy all files and directories from the snapshot to a restore directory to complete the restore.

`cp -r . ../../restore
`

The files and directories from the snapshot are now available in the `/media/nfs/restore` directory.

### Delete NFS classic file share snapshots

Existing share snapshots are never overwritten. You must delete them explicitly. You can delete classic share snapshots by using the Azure portal, Azure PowerShell, or Azure CLI.

Before you can delete a share snapshot, you need to remove any locks on the storage account. Go to the storage account and select Settings > Locks. If any locks are listed, delete them.

- 
Azure portal

- 
Azure PowerShell

- 
Azure CLI

To delete a snapshot of an existing classic file share, sign in to the Azure portal and follow these steps.

- In the search box at the top of the Azure portal, type and select storage accounts.

- Select the FileStorage storage account that contains the NFS classic file share for which you want to delete snapshots.

- From the service menu, under Data storage, select Classic file shares.

- Select the file share for which you want to delete one or more snapshots, and then select Operations > Snapshots. The portal lists any existing snapshots for the file share.

- Select the snapshots that you want to delete, and then select Delete.

To delete a classic file share snapshot, run the following PowerShell command. Replace `<resource-group-name>`, `<storage-account-name>`, and `<file-share-name>` with your own values. The `SnapshotTime` parameter must follow the correct name format, such as `2024-05-10T08:04:08Z`.

`Remove-AzRmStorageShare -ResourceGroupName "<resource-group-name>" -StorageAccountName "<storage-account-name>" -Name "<file-share-name>" -SnapshotTime "<snapshot-time>"
`

To delete a classic file share and all its snapshots, run the following PowerShell command. Replace `<resource-group-name>`, `<storage-account-name>`, and `<file-share-name>` with your own values.

`Remove-AzRmStorageShare -ResourceGroupName "<resource-group-name>" -StorageAccountName "<storage-account-name>" -Name "<file-share-name>" -Include Snapshots
`

To delete a classic file share snapshot, run the following Azure CLI command. Replace `<storage-account-name>` and `<file-share-name>` with your own values. The `--snapshot` parameter must follow the correct name format, such as `2024-05-10T08:04:08Z`.

`az storage share delete --account-name <storage-account-name> --name <file-share-name> --snapshot <snapshot-time>
`

To delete a classic file share and all its snapshots, run the following Azure CLI command. Replace `<storage-account-name>` and `<file-share-name>` with your own values.

`az storage share delete --account-name <storage-account-name> --name <file-share-name> --delete-snapshots include
`

### Create an NFS file share snapshot with Microsoft.FileShares

You can create a snapshot of an NFS file share created with the Microsoft.FileShares resource provider by using the Azure portal, Azure PowerShell, or Azure CLI.

- 
Azure portal

- 
Azure PowerShell

- 
Azure CLI

To create a snapshot of an existing file share, sign in to the Azure portal and follow these steps.

- In the search box at the top of the Azure portal, type and select File Shares.

- Select the file share that you want to take a snapshot of.

- Select Operations > Snapshots.

- Select + Add snapshot. Add an optional comment, and select OK.

To create a snapshot of an existing file share, run the following PowerShell command. Replace the variables with your own values. You need the Az PowerShell module version 16.0.0 or later. This version includes the Az.FileShare module.

`$resourceGroup = "<resource-group-name>"
$shareName = "<file-share-name>" 
$snapshotName = "<snapshot-name>"

# -InitiatorId is an optional free-form caller tag surfaced in Get-AzFileShareSnapshot output.
New-AzFileShareSnapshot -ResourceGroupName $resourceGroup -ResourceName $shareName -Name $snapshotName #-InitiatorId "<your-name-or-id>" -Metadata @{metakey1 = "metavalue1"}
`

To create a snapshot of an existing file share, run the following Azure CLI commands. Replace the variables with your own values. You need the `fileshare` extension for the Azure CLI. To install it, run `az extension add --name fileshare`.

`# Specify your values
shareName="<file-share-name>"
snapshotName="<snapshot-name>"
resourceGroup="<resource-group-name>"

# Create the snapshot. Use --initiator-id for an optional caller tag and --metadata for key=value pairs.
az fileshare snapshot create --name $snapshotName --resource-group $resourceGroup --resource-name $shareName #--initiator-id "<your-name-or-id>" --metadata test=value1
`

### Update an NFS file share snapshot with Microsoft.FileShares

You can update an existing NFS file share snapshot (for example, to modify its metadata) by using the Azure portal, Azure PowerShell, or Azure CLI.

- 
Azure portal

- 
Azure PowerShell

- 
Azure CLI

- In the search box at the top of the Azure portal, type and select File Shares.

- Select the file share that you want to update the snapshot for.

- Select Operations > Snapshots.

- Check the box for the specific snapshot that you want to update, and then select Properties.

- Update the metadata for the snapshot in the pop-up pane, and then select Save.

To update a file share snapshot, run the following PowerShell commands. Replace the variables with your own values. You need the Az PowerShell module version 16.0.0 or later. This version includes the Az.FileShare module.

`$resourceGroup = "<resource-group-name>"
$shareName = "<file-share-name>"
$snapshotName = "<snapshot-name>"

Update-AzFileShareSnapshot -ResourceGroupName $resourceGroup -ResourceName $shareName -Name $snapshotName -Metadata @{meta1="value1";meta2="value2"}
`

To update a file share snapshot, run the following Azure CLI commands. Replace the variables with your own values. You need the `fileshare` extension for the Azure CLI. To install it, run `az extension add --name fileshare`.

`# Specify your values
shareName="<file-share-name>"
snapshotName="<snapshot-name>"
resourceGroup="<resource-group-name>"

# Update the snapshot metadata
az fileshare snapshot update --name $snapshotName --resource-group $resourceGroup --resource-name $shareName --metadata key1=value1 key2=value2
`

### List NFS file share snapshots with Microsoft.FileShares

You can list all the snapshots for an NFS file share by using the Azure portal, Azure PowerShell, or Azure CLI.

- 
Azure portal

- 
Azure PowerShell

- 
Azure CLI

To list all the snapshots for an existing file share, sign in to the Azure portal and follow these steps:

- In the search box at the top of the Azure portal, type and select File Shares.

- Select the file share that you want to view the snapshots for.

- Select Operations > Snapshots. The portal lists any existing snapshots for the file share.

To list all file share snapshots, run the following PowerShell command. Replace the variables with your own values. You need the Az PowerShell module version 16.0.0 or later. This version includes the Az.FileShare module.

`$resourceGroup = "<resource-group-name>"
$shareName = "<file-share-name>"
$snapshotName = "<snapshot-name>"

Get-AzFileShareSnapshot -ResourceGroupName $resourceGroup -ResourceName $shareName -Name $snapshotName
`

To list all file share snapshots, run the following Azure CLI commands. Replace the variables with your own values. You need the `fileshare` extension for the Azure CLI. To install it, run `az extension add --name fileshare`.

`# Specify your values
shareName="<file-share-name>"
resourceGroup="<resource-group-name>"

# List the snapshots
az fileshare snapshot list --resource-group $resourceGroup --resource-name $shareName
`

### Restore from an NFS file share snapshot (Microsoft.FileShares)

To mount an NFS file share snapshot to a Linux VM (NFS client) and restore files, follow these steps.

- Sign in to the Azure portal and go to your file share.

- Select JSON view from the upper right. In the JSON view, under properties, copy the value for hostName. The format looks like `fs-xxxxxxxxxxxxxxxxx.xx.file.storage.azure.net`. To extract hostName by using PowerShell, run `Get-AzFileShare -ResourceGroupName $resourceGroup -ResourceName $shareName` and look for the `hostName` property in the output. To extract hostName by using Azure CLI, run `az fileshare show --resource-group $resourceGroup --name $shareName` and look for the `hostName` property in the output. Be sure to replace `$resourceGroup` and `$shareName` with your own values.

- Run the following command in a console. Replace the placeholder values, including brackets, with your own values. The value for `<hostName>` should be the entire value you copied in step 2. The value for `<hostNamePrefix>` is the first segment of the hostName (up to but not including the first period), which includes everything before `.xx.file.storage.azure.net`.

Replace `/media/nfs` with your local mount path for the file share, if different. To improve copy performance, mount the snapshot by using nconnect to use multiple TCP channels. See NFS mount options for other recommended mount options.

`sudo mount -o vers=4,minorversion=1,proto=tcp,sec=sys <hostName>:/<hostNamePrefix>/<fileShareName> /media/nfs
`

- Change the directory to `/media/nfs/.snapshots` so you can view the available snapshots. The `.snapshots` directory is hidden by default, but you can access and read from it like any directory. If you just created the snapshot, wait at least 30 seconds for the `.snapshots` directory to become available.

`cd /media/nfs/.snapshots
`

- List the contents of the `.snapshots` directory.

`ls
`

- Each snapshot has its own directory that serves as a recovery point. Change to the snapshot directory for which you want to restore files.

`cd <snapshot-name>
`

- List the contents of the directory to view a list of files and directories that you can recover.

`ls
`

- Copy all files and directories from the snapshot to a restore directory to complete the restore.

`cp -r . ../../restore
`

The files and directories from the snapshot are now available in the `/media/nfs/restore` directory.

### Delete NFS file share snapshots (Microsoft.FileShares)

Existing share snapshots are never overwritten. You must delete them explicitly. You can delete share snapshots by using the Azure portal, Azure PowerShell, or Azure CLI.

- 
Azure portal

- 
Azure PowerShell

- 
Azure CLI

To delete a snapshot of an existing file share, sign in to the Azure portal and follow these steps.

- In the search box at the top of the Azure portal, type and select File Shares.

- Select the file share for which you want to delete snapshots.

- To delete one or more snapshots, select Operations > Snapshots. The portal lists any existing snapshots for the file share.

- Select the snapshots that you want to delete, and then select Delete.

You need the Az PowerShell module version 16.0.0 or later. This version includes the Az.FileShare module.

`$resourceGroup = "<resource-group-name>"
$shareName = "<file-share-name>"
$snapshotName = "<snapshot-name>"

Remove-AzFileShareSnapshot -ResourceGroupName $resourceGroup -ResourceName $shareName -Name $snapshotName
`

To delete a file share snapshot, run the following Azure CLI commands. Replace the variables with your own values. You need the `fileshare` extension for the Azure CLI. To install it, run `az extension add --name fileshare`.

`# Specify your values
shareName="<file-share-name>"
snapshotName="<snapshot-name>"
resourceGroup="<resource-group-name>"

# Delete the snapshot
az fileshare snapshot delete --name $snapshotName --resource-group $resourceGroup --resource-name $shareName -y
`

## See also

- Working with share snapshots in:

- Azure file share backup

- Azure PowerShell

- Azure CLI

 
 

 
 

 

 
 
 
 
 
 
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
 2026-10-28
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
