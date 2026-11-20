# https://learn.microsoft.com/en-us/azure/azure-sql/database/recovery-using-backups

Source: https://learn.microsoft.com/en-us/azure/azure-sql/database/recovery-using-backups

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
 

 

 

 

 
 
# Restore a database from a backup in Azure SQL Database

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Applies to: 
 Azure SQL Database

- Azure SQL Database

- Azure SQL Managed Instance

This article provides steps to recover any database from a backup in Azure SQL Database, including Hyperscale databases.

## Overview

Automated database backups help protect your databases from user and application errors, accidental database deletion, and prolonged outages. This built-in capability is available for all service tiers and compute sizes. The following options are available for database recovery through automated backups:

- Create a new database on the same server, recovered to a specified point in time within the retention period with Point-in-time restore.

- Create a database on the same server, recovered to the deletion time for a deleted database.

- Create a new database on any server in the same region, recovered to the time of a recent backup with long-term retention restore or geo-restore.

- Create a new database on any server in any other region, recovered to the point of the most recent replicated backups with geo-restore.

If you configured long-term retention (LTR), you can also create a new database from any long-term retention backup on any server.

Important

- You can't overwrite an existing database during restore.

- Database restore operations don't restore the tags of the original database.

When you're using the Standard or Premium service tier in the DTU purchasing model, your database restore might incur an extra storage cost. The extra cost happens when the maximum size of the restored database is greater than the amount of storage included with the target database's service tier and service objective.

For pricing details of extra storage, see the SQL Database pricing page. If the actual amount of used space is less than the amount of storage included, you can avoid this extra cost by setting the maximum database size to the included amount.

Note

Restoring databases between the Hyperscale service tier and the other service tiers of Azure SQL Database is not currently supported.

## Recovery time

Several factors affect the recovery time to restore a database through automated database backups:

- The size of the database

- The compute size of the database

- The size of the transaction log backups involved

- The amount of activity that needs to be replayed to recover to the restore point

- The network bandwidth if the restore is to a different region

- The number of concurrent restore requests that are processed in the target region

For a large or very active database in the service tiers other than Hyperscale, the restore might take several hours. A prolonged outage in a region might cause a high number of geo-restore requests for disaster recovery. When there are many requests, the recovery time for individual databases can increase. For information on recovery times, see RTO and RPO.

For a single subscription, you have the following limitations on the number of concurrent restore requests. These limitations apply to any combination of point-in-time restores, geo-restores, and restores from long-term retention backup.

Deployment option
Max # of concurrent requests being processed
Max # of concurrent requests being submitted

Single database (per subscription)
30
100

Elastic pool (per pool)
4
2,000

## Permissions

To recover by using automated backups, you must be either:

- A member of the Contributor role or the SQL Server Contributor role in the subscription or resource group that contains the logical server

- The subscription or resource group owner

For more information, see Azure RBAC: Built-in roles.

You can recover by using the Azure portal, PowerShell, or the REST API. You can't use Transact-SQL.

Azure SQL Database backups are managed automatically. No one has direct access to the backups. The backups are deleted once the configured retention period expires. For more information, see Automated backups in Azure SQL Database and Long-term retention.

## Point-in-time restore

You can restore any database to an earlier point in time within its retention period. The restore request can specify any service tier or compute size for the restored database. When you're restoring a database into an elastic pool, ensure that you have sufficient resources in the pool to accommodate the database.

When the restore is complete, it creates a new database on the same server as the original database. The restored database is charged at normal rates, based on its service tier and compute size. You don't incur charges until the database restore is complete.

You generally restore a database to an earlier point for recovery purposes. You can treat the restored database as a replacement for the original database or use it as a data source to update the original database.

- Database replacement

If you want the restored database to be a replacement for the original database, you should specify the original database's compute size and service tier. You can then rename the original database and give the restored database the original name by using the ALTER DATABASE command in T-SQL.

- Data recovery

If you plan to retrieve data from the restored database to recover from a user or application error, you need to write and run a data recovery script that extracts data from the restored database and applies to the original database. Although the restore operation might take a long time to complete, the restoring database is visible in the database list throughout the restore process.

If you delete the database during the restore, the restore operation is canceled. You won't be charged for the database that didn't complete the restore.

- 
Azure portal

- 
Azure CLI

- 
PowerShell

- 
REST API

To recover a database to a point in time by using the Azure portal, open the database overview page and select Restore on the toolbar to open the Create SQL Database - Restore database page:

On the Create SQL Database - Restore database page, specify the source for the backup and then select the point-in-time backup point from which a new database will be created. Since the chosen database is to be restored to the current server, the source database and target server are grayed out.

To restore a database from a PITR backup by using the Azure CLI, see az sql db restore.

Note

This article uses the Azure Az PowerShell module, which is the recommended PowerShell module for interacting with Azure. To get started with the Az PowerShell module, see Install Azure PowerShell. To learn how to migrate to the Az PowerShell module, see Migrate Azure PowerShell from AzureRM to Az.

For a sample PowerShell script that shows how to perform a point-in-time restore of a database, see Restore a database by using PowerShell.

To recover a database from a PITR backup by using PowerShell, use the following cmdlets:

Cmdlet
Description

Get-AzSqlDatabase
Gets one or more databases.

Restore-AzSqlDatabase
Use the `-FromPointInTimeBackup` parameter to restore to a point in time.

Important

- Restore points represent a period between the earliest restore point and the latest log backup point. Information on the latest restore point is currently unavailable on Azure PowerShell.

To recover a database from a PITR backup by using the REST API:

API
Description

Databases - Create Or Update
Use `createMode=PointInTimeRestore` to restore a database.

Database Operations - List By Database
Gets a list of operations performed on the database.

### Point-in-time restore considerations

- You can perform a point-in-time restore of a database to the same server. Cross-server, cross-subscription, and cross-geo point-in-time restore is not currently supported. To restore a database to a different region using geo-replicated backups, see Geo-restore.

- You can't perform a point-in-time restore on a geo-secondary database. You can do so only on a primary database.

- The `BackupFrequency` parameter isn't supported for Hyperscale databases.

- Database restore operations are resource-intensive and might require a service tier of S3 or greater for the restoring (target) database. Once restore completes, the database or elastic pool might be scaled down, if required.

- If you created any In-Memory OLTP objects in a database in the Business Critical or Premium service tiers, then you must use the Business Critical or Premium service tiers for the restored database. For more information, see Restore a database with In-Memory OLTP objects.

- When you do a point-in-time restore on a database that has change data capture (CDC) enabled, ensure the source database has enough allocated space.

## Long-term backup restore

To perform a restore operation on a long-term backup, you can use the Azure portal, the Azure CLI, Azure PowerShell, or the REST API. For more information, see Restore a long-term backup.

Important

Some older APIs used for long-term retention (LTR) backup operations are deprecated and no longer supported. Avoid using legacy PowerShell cmdlets such as `Copy-AzSqlDatabaseLongTermRetentionBackup`. Use the supported restore methods described in this article instead.

- 
Azure portal

- 
Azure CLI

- 
PowerShell

- 
REST API

To recover a long-term backup by using the Azure portal, go to your logical server. Select Backups under Data Management, and then select Manage under Available LTR backups for the database you're trying to restore.

To restore a database by using the Azure CLI, see az sql db ltr-backup restore.

To restore a database by using PowerShell, use the following cmdlets:

Cmdlet
Description

Get-AzSqlDatabase
Gets one or more databases.

Get-AzSqlDatabaseGeoBackup
Gets a geo-redundant backup of a database.

Restore-AzSqlDatabase -FromLongTermRetentionBackup
Use the `-FromLongTermRetentionBackup` parameter to restore a database from long-term backup.

Warning

The `Copy-AzSqlDatabaseLongTermRetentionBackup` cmdlet uses a deprecated API and is not supported. Do not use this cmdlet. Use the supported restore methods documented in this article.

For more information, see Restore-AzSqlDatabase.

To restore a database by using the REST API:

API
Description

Databases - Create Or Update
Use `createMode=RestoreLongTermRetentionBackup` to restore a database from long-term retention.

Get Create or Update Database Status
Restores a database from long-term backup.

## Restore deleted database

You can restore a deleted database to the deletion time, or an earlier point in time, on the same server by using the Azure portal, the Azure CLI, Azure PowerShell, and the REST API.

Important

If you delete a server, all of its databases and their PITR backups are also deleted. You can't restore a deleted server, and you can't restore the deleted databases from PITR backups.

If you had configured LTR backups for those databases, you can use those backups to restore the databases to a different server. If the logical server has been deleted, use Azure CLI or PowerShell commands to view and restore LTR backups.

- 
Azure portal

- 
Azure CLI

- 
PowerShell

- 
REST API

To recover a deleted database to the deletion time by using the Azure portal, open the server's overview page and select Deleted databases. Select a deleted database that you want to restore, and then enter the name for the new database that will be created with data restored from the backup.

Tip

It might take several minutes for recently deleted databases to appear on the Deleted databases page in the Azure portal, or when you want to display deleted databases programmatically.

To restore a database by using the Azure CLI, see az sql db restore.

To restore a deleted database by using PowerShell, use the following cmdlets:

Cmdlet
Description

Get-AzSqlDatabase
Gets one or more databases.

Get-AzSqlDeletedDatabaseBackup
Gets a deleted database that you can restore.

Restore-AzSqlDatabase
Use the `-FromDeletedDatabaseBackup` parameter to restore a deleted database.

For a sample PowerShell script that shows how to restore a deleted database in Azure SQL Database, see Restore a database by using PowerShell.

To restore a deleted database by using the REST API:

API
Description

Databases - Create Or Update
Use `createMode=Restore` to restore a database.

Get Create or Update Database Status
Returns the status during a restore operation.

## Geo-restore

Geo-restore uses geo-replicated backups as the source. You can restore a database on any logical server in any Azure region from the most recent geo-replicated backups. You can request a geo-restore even if an outage has made the database or the entire region inaccessible.

Important

- Geo-restore is available only for databases configured with geo-redundant or geo-zone redundant (GZRS) backup storage. If you're not currently using geo-replicated backups for a database, you can change this by configuring backup storage redundancy.

- You can perform geo-restore only on databases that reside in the same subscription.

Geo-restore is the default recovery option when your database is unavailable because of an incident in the hosting region. You can restore the database to a server in any other region.

Restoring from geo-redundant backups could potentially result in data loss in certain scenarios because Azure Geo-Redundant Storage (GRS) replicates data asynchronously to a secondary region. There is some latency involved in the replication process, but the exact latency can vary based on several factors, including the distance between the primary and secondary regions and the current network conditions. Typically, the replication latency for GRS is in the range of minutes, but it is not guaranteed to be within a specific time frame. It can take considerable time, depending on the size of each database. For more information, see RTO and RPO.

The following illustration shows a database restore from the last available backup in another region.

You can use geo-restore to restore a deleted database by using the Azure portal, the Azure CLI, Azure PowerShell, and the REST API.

- 
Azure portal

- 
Azure CLI

- 
PowerShell

- 
REST API

From the Azure portal, you create a new single database and select an available geo-restore backup. The newly created database contains the geo-restored backup data.

To geo-restore a single database from the Azure portal in the region and server of your choice, follow these steps:

- Open the Create SQL Database pane in the Azure portal. On the Basics tab, enter the required information.

- Select Additional settings.

- For Use existing data, select Backup.

- Select a backup from the list of available geo-restore backups.

Complete the process of creating a database from the backup. When you create a database in Azure SQL Database, it contains the restored geo-restore backup.

To restore a database by using the Azure CLI, see az sql db restore.

To geo-restore a database by using PowerShell, use the following cmdlets:

Cmdlet
Description

Get-AzSqlDatabase
Gets one or more databases.

Get-AzSqlDatabaseGeoBackup
Gets a geo-redundant backup of a database.

Restore-AzSqlDatabase
Use the `-FromGeoBackup` parameter to restore a geo-replicated database.

For a PowerShell script that shows how to perform geo-restore for a single database, see Use PowerShell to restore a single database to an earlier point in time.

To restore a database by using the REST API:

API
Description

Databases - Create Or Update
Use `createMode=Recovery` to restore a database.

Get Create or Update Database Status
Returns the status during a restore operation.

### Geo-restore considerations

For more information on using geo-restore, see Recovery using Geo-restore.

Note

For detailed information about recover from an outage, see disaster recovery guidance and the high availability and disaster recovery checklist.

Geo-restore is the most basic disaster-recovery solution available in SQL Database. It relies on automatically created geo-replicated backups. For information on recovery times, see RTO and RPO. It doesn't guarantee that the target region will have the capacity to restore your databases after a regional outage, because a sharp increase of demand is likely. If your application uses relatively small databases and isn't critical to the business, geo-restore is an appropriate disaster-recovery solution.

For business-critical applications that require large databases and must ensure business continuity, use failover groups. That feature offers a much lower RPO and RTO, and the capacity is always guaranteed.

For more information about business continuity choices, see Overview of business continuity.

Note

If you plan to use geo-restore as disaster-recovery solution, we recommend that you conduct periodic drills to verify application tolerance to any loss of recent data modifications, along with all operational aspects of the recovery procedure.

## Restore database to another server

You can use the following methods to restore a database to another server:

- Long-term backup restore

- Geo-restore

- Database copy

- Active geo-replication

## Related content

- Automated backups

- Long-term retention

- Active geo-replication

- Failover groups overview & best practices

- Modifiable configuration reference for Azure SQL Database

 
 

 
 

 

 
 
 
 
 
 
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
 2026-01-26
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
