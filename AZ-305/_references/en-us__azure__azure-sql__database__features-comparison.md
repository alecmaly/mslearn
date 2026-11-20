# https://learn.microsoft.com/en-us/azure/azure-sql/database/features-comparison

Source: https://learn.microsoft.com/en-us/azure/azure-sql/database/features-comparison

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
 

 

 

 

 
 
# Features comparison: Azure SQL Database and Azure SQL Managed Instance

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Applies to: 
 Azure SQL Database 
 Azure SQL Managed Instance

Azure SQL Database and SQL Managed Instance share a common code base with the latest stable version of SQL Server.
Most of the standard SQL language, query processing, and database management features are identical. The features that are common between SQL Server and SQL Database or SQL Managed Instance are:

- Language features - Control of flow language keywords, Cursors, Data types, DML statements, Predicates, Sequence numbers, Stored procedures, and Variables.

- Database features - Automatic tuning (plan forcing), Change tracking, Database collation, Contained databases, Contained users, Data compression, Database configuration settings, Online index operations, Partitioning, and Temporal tables.

- Security features - Application roles, Dynamic data masking, Row Level Security, and Advanced Threat Protection (see getting started guides for SQL Database and SQL Managed Instance.)

- Multi-model capabilities - Graph processing, JSON data, OPENXML, Spatial, OPENJSON, and XML indexes. For more information, see Multi-model capabilities of Azure SQL Database and SQL Managed Instance.

Azure manages your databases and guarantees their high availability. Some features that might affect high availability or can't be used in PaaS world have limited functionalities in Azure SQL Database and Azure SQL Managed Instance.

If you need more details about the differences, see the following articles:

- T-SQL differences between SQL Server and Azure SQL Database

- T-SQL differences

## Features of SQL Database and SQL Managed Instance

The following table lists the major features of SQL Server and provides information about whether the feature is partially or fully supported in Azure SQL Database and Azure SQL Managed Instance, with a link to more information about the feature.

Feature
Azure SQL Database
Azure SQL Managed Instance

Database compatibility
100 - 160
100 - 160

Always Encrypted
Yes, see Cert store and Key vault
Yes, see Cert store and Key vault

Always On Availability Groups
Enterprise class SLA availability is guaranteed for every database. Disaster recovery is discussed in Overview of business continuity with Azure SQL Database.
Enterprise class SLA availability is guaranteed for every database and can't be managed by user. Disaster recovery is discussed in Overview of business continuity with Azure SQL Database. Use failover groups to configure a secondary SQL Managed Instance in another region. SQL Server instances and SQL Database can't be used as secondaries for SQL Managed Instance.

Attach a database
No
No

Auditing
Yes, see Auditing
Yes, see Auditing, with some differences

Microsoft Entra authentication (formerly Azure Active Directory)
Yes. Both database-level users and server-level logins.
Yes. Both database-level users and server-level logins.

BACKUP command
No, only system-initiated automatic backups, see Automated backups in Azure SQL Database
Yes, user initiated copy-only backups to Azure Blob storage (automatic system backups can't be initiated by user), see Backup differences and Automated backups in Azure SQL Managed Instance.

Built-in functions
Most, see individual functions
Yes, see Stored procedures, functions, triggers differences

BULK INSERT statement
Yes, but just from Azure Blob storage as a source.
Yes, but just from Azure Blob Storage as a source, see differences.

Certificates and asymmetric keys
Yes, without access to file system for `BACKUP` and `CREATE` operations.
Yes, without access to file system for `BACKUP` and `CREATE` operations, see certificate differences.

Change data capture - CDC
Yes, for S3 tier and above. Basic, S0, S1, S2 aren't supported.
Yes

Collation - server/instance
Yes, the default database collation is `SQL_Latin1_General_CP1_CI_AS`. The database collation can be set on database creation and can't be updated. Specify a collation for data (`COLLATE`) and a catalog collation for system metadata and object identifiers (`CATALOG_COLLATION`). In Azure SQL Database, there's no server collation.
Yes, can be set when the instance is created and can't be updated later.

Columnstore indexes
Yes - Premium tier, Standard tier - S3 and above, General Purpose tier, Business Critical, and Hyperscale tiers.
Yes

Common language runtime - CLR
No
Yes, but without access to file system in `CREATE ASSEMBLY` statement, see CLR differences

Credentials
Yes, but only database scoped credentials.
Yes, but only Azure Key Vault and `SHARED ACCESS SIGNATURE` are supported, see details

Cross-database/three-part name queries
No, see Elastic queries
Yes

Cross-database transactions
No
Yes, within the instance. See Linked server differences for cross-instance queries.

Data virtualization
Yes, for CSV, Delta 1.0, and Parquet. See Data Virtualization for Azure SQL Database. You can also query data in the files placed on Azure Blob Storage using `OPENROWSET` function. In SQL Server, this feature is known as PolyBase.
Yes, for Azure Data Lake Storage (ADLS) and Azure Blob Storage as data source. See Data virtualization with Azure SQL Managed Instance for more details. In SQL Server, this feature is known as PolyBase.

Database mail - DbMail
No
Yes

Database mirroring (deprecated)
No
No

Database mirroring in Microsoft Fabric
Yes
Yes

Database snapshots
No
No

Database virtualization
No
Yes

DBCC statements
Most, see individual statements
Yes, see DBCC differences

DDL statements
Most, see individual statements
Yes, see T-SQL differences

DDL triggers
Database only
Yes

Distributed partition views
No
Yes

Distributed transactions - MS DTC
No, see Elastic transactions
Yes, DTC for Azure SQL Managed Instance, 
 and Elastic transactions

DML triggers
Most, see individual statements
Yes

DMVs
Most, see individual DMVs
Yes, see T-SQL differences

Elastic query
Yes, with required RDBMS type (preview)
No, use native cross-DB queries and Linked Server

Event notifications
No, see Alerts
No

Expressions
Yes
Yes

Extended events (XEvent)
Some, see Extended Events in Azure SQL Database and Azure SQL Managed Instance
Yes, see Extended events differences.

Extended stored procedures
No
No

Files and file groups
Primary file group only
Yes. File paths are automatically assigned and the file location can't be specified in ALTER DATABASE ADD FILE.

Filestream
No
No, see SQL managed instances features.

Full-text search (FTS)
Yes, but non-Microsoft filters and word breakers aren't supported
Yes, but non-Microsoft filters and word breakers aren't supported

Functions
Most, see individual functions
Yes, see Stored procedures, functions, triggers differences

In-memory optimization
Yes in Premium and Business Critical service tiers.
 Limited support for non-persistent In-Memory OLTP objects such as memory-optimized table variables in Hyperscale service tier.
Yes in Business Critical service tier.

Language elements
Most, see individual elements
Yes, see T-SQL differences

Ledger
Yes
Yes

Link feature
No
Yes

Linked servers
No, see Elastic query
Yes. Only to SQL Server and SQL Database without distributed transactions.

Linked servers that read from files (CSV, Excel)
No. Use BULK INSERT or OPENROWSET as an alternative for CSV format.
No. Use BULK INSERT or OPENROWSET as an alternative for CSV format. Track these requests on SQL Managed Instance feedback item

Log shipping
Availability through redundancy is included with every database. Disaster recovery is discussed in Overview of business continuity.
Natively built in as a part of Azure Database Migration Service (DMS) migration process. Natively built for custom data migration projects as an external Log Replay Service.
 Not available as High availability solution, because other Availability through redundancy methods are included with every database and it isn't recommended to use Log-shipping as HA alternative. Disaster recovery is discussed in Overview of business continuity. Not available as a replication mechanism between databases - use secondary replicas on Business Critical tier, failover groups, or transactional replication as the alternatives.

Logins and users
Yes, but `CREATE LOGIN` and `ALTER LOGIN` statements are limited. Windows logins aren't supported. `EXECUTE AS LOGIN` isn't supported - use `EXECUTE AS USER`.
Yes, with some differences. See Windows Authentication for Azure SQL Managed Instance - the process requires Active Directory synchronization to Microsoft Entra ID.

Maintenance window selection
Yes
Yes

Configure advance notifications for planned maintenance events
Yes
Yes

Minimal logging in bulk import
No, only Full Recovery model is supported.
No, only Full Recovery model is supported.

Modifying system data
No
Yes

OLE Automation
No
No

OPENDATASOURCE
No
Yes, only to SQL Database, SQL Managed Instance, and SQL Server. See T-SQL differences

OPENQUERY
No
Yes, only to SQL Database, SQL Managed Instance, and SQL Server. See T-SQL differences

OPENROWSET
Yes, only to import from Azure Blob storage.
Yes, only to SQL Database, SQL Managed Instance and SQL Server, and to import from Azure Blob storage. See T-SQL differences

Operators
Most, see individual operators
Yes, see T-SQL differences

Query Notifications
No
Yes

Query Store
Yes
Yes

Query Store for secondary replicas
Yes
Yes

Machine Learning Services (Formerly R Services)
No
Yes, with the SQL Server 2022 update policy. See Machine Learning Services in Azure SQL Managed Instance.

Recovery models
Only Full Recovery that guarantees high availability is supported. Simple and Bulk Logged recovery models aren't available.
Only Full Recovery that guarantees high availability is supported. Simple and Bulk Logged recovery models aren't available.

Resource governor
No
Yes

RESTORE statements
No
Yes, with mandatory `FROM URL` options for the backups files placed on Azure Blob Storage. See Restore differences

Restore database from backup
From automated backups only, see Restore a database from a backup
From automated backups, see Restore a database from a backup and from full backups placed on Azure Blob Storage, see Backup differences

Restore database to SQL Server
No. Use BACPAC or BCP instead of native restore.
Yes, but only to SQL Server 2022, or SQL Server 2025 based on the update policy of the SQL managed instance. Restore databases to SQL Server 2022 from instances that have the SQL Server 2022 update policy. Restore databases to SQL Server 2025 from instances that have the SQL Server 2025 update policy. For more information, review Restore a database to SQL Server 2022 from Azure SQL Managed Instance. Otherwise, use BACPAC, BCP, or Transactional replication.

Semantic search
No
No

Service Broker
No
Yes. See Service Broker differences

Server configuration settings
No
Yes, see T-SQL differences

Set statements
Most, see individual statements
Yes, see T-SQL differences

SQL Server Agent
No, see Elastic jobs
Yes, see SQL Server Agent differences

SQL Server Auditing
No, see Auditing for Azure SQL Database
Yes, see Auditing differences

Azure Synapse Link for SQL
Yes
No

System functions
Most, see individual functions
Yes, see Stored procedures, functions, triggers differences

System stored procedures
Some, see individual stored procedures
Yes, see Stored procedures, functions, triggers differences

System tables
Some, see individual tables
Yes, see T-SQL differences

System catalog views
Some, see individual views
Yes, see T-SQL differences

TempDB
Yes. 32-GB size per core for every database.
Yes. 24-GB size per vCore for entire GP tier and limited by instance size on BC tier

Temporary tables
Local and database-scoped global temporary tables
Local and instance-scoped global temporary tables

Time zone choice
Yes, at database and session scope (preview).
Yes, at database and session scope (preview), only with the always-up-to-date update policy. See Time zones.

Trace flags
No
Yes, but only limited set of global trace flags. See DBCC differences

Transactional replication
Yes, Transactional and snapshot replication subscriber only
Yes, see limitations of replication in SQL Managed Instance.

Transparent data encryption (TDE)
Yes, see TDE for Azure SQL
Yes, see TDE for Azure SQL

Windows authentication
No
Yes, see Windows Authentication for Microsoft Entra principals

Windows Server Failover Clustering
No. Other techniques that provide high availability are included with every database. Disaster recovery is discussed in Overview of business continuity with Azure SQL Database.
No. Other techniques that provide high availability are included with every database. Disaster recovery is discussed in Overview of business continuity with Azure SQL Database.

Note

Some Azure SQL Managed Instance feature availability depends on the configured instance update policy.

## Platform capabilities

The Azure platform provides a number of PaaS capabilities that it adds as extra value to the standard database features. You can use many external services with Azure SQL Database and Azure SQL Managed Instance.

Platform feature
Azure SQL Database
Azure SQL Managed Instance

Active geo-replication
Yes, see Active geo-replication - all service tiers.
No, see failover groups as an alternative.

Auto-scale
Yes, but only in serverless model. In the non-serverless model, the change of service tier (change of vCore, storage, or DTU) is fast and online. The service tier change requires minimal or no downtime.
No, you need to choose reserved compute and storage. The change of service tier (vCore or max storage) is online and requires minimal or no downtime.

Automatic backups
Yes, see automated backups in Azure SQL Database. Full backups are taken every seven days, differential every 12 hours, and log backups every 5-10 minutes.
Yes, see automated backups in Azure SQL Managed Instance. Full backups are taken every seven days, differential every 12 hours, and log backups every 5-10 minutes.

Automatic tuning (indexes)
Yes, see Automatic tuning
No

Availability Zones
Yes
Yes. For General Purpose service tier in preview, and for Business Critical service tier generally available

Azure Resource Health
Yes
Yes

Short-term backup retention
Yes, see short-term retention. 7 days default, max 35 days.
Yes, see short-term retention. 1-35 days, 7 days default.

Azure Database Migration Service (DMS)
Yes
Yes

Elastic jobs
Yes, see Elastic jobs
No. Use SQL Agent or Azure Automation.

Failover groups
Yes, see failover groups - all service tiers.
Yes, see failover groups.

File system access
No. Use BULK INSERT or OPENROWSET to access and load data from Azure Blob Storage as an alternative.
No. Use BULK INSERT or OPENROWSET to access and load data from Azure Blob Storage as an alternative.

Geo-restore
Yes, see Geo-restore
Yes, see Geo-restore

Long-term retention (LTR)
Yes, see long-term retention, keep automatically taken backups up to 10 years.
Yes, see long-term retention, keep automatically taken backups up to 10 years.

Pause/resume
Yes, in serverless model
Yes, with Stop / start

Policy-based management
No
No

Public IP address
Yes. Restrict access by using firewall or service endpoints.
Yes. You need to explicitly enable it and enable port 3342 in NSG rules. You can disable Public IP if needed. See Public endpoint for more details.

Point in time database restore
Yes, see Point-in-time restore
Yes, see Point-in-time restore

Resource pools
Yes, as Elastic pools
Yes. A single instance of SQL Managed Instance can have multiple databases that share the same pool of resources. In addition, you can deploy multiple instances of SQL Managed Instance in instance pools that share the resources.

Scaling up or down (online)
Yes, you can either change DTU or reserved vCores or max storage with minimal downtime.
Yes, you can change reserved vCores or max storage with minimal downtime.

SQL Alias
No, use DNS Alias
No, use Cliconfg to set up alias on the client machines.

Database watcher (preview)
Yes
Yes

Database Hub in Microsoft Fabric (preview)
Yes
Yes

SQL Data Sync
Yes, but SQL Data Sync retires in 2027. Instead, see SQL Data Sync retirement: Migrate to alternative solutions.
No, use transactional replication.

SQL Server Analysis Services (SSAS)
No, Azure Analysis Services is a separate Azure cloud service.
No, Azure Analysis Services is a separate Azure cloud service.

SQL Server Integration Services (SSIS)
Yes, with a managed SSIS in Azure Data Factory (ADF) environment, where packages are stored in SSISDB hosted by Azure SQL Database and executed on Azure SSIS Integration Runtime (IR), see Create Azure-SSIS IR in ADF. 

To compare the SSIS features in SQL Database and SQL Managed Instance, see Compare SQL Database to SQL Managed Instance.
Yes, with a managed SSIS in Azure Data Factory (ADF) environment, where packages are stored in SSISDB hosted by SQL Managed Instance and executed on Azure SSIS Integration Runtime (IR), see Create Azure-SSIS IR in ADF. 

To compare the SSIS features in SQL Database and SQL Managed Instance, see Compare SQL Database to SQL Managed Instance.

SQL Server Reporting Services (SSRS)
No - see Power BI
No - use Power BI paginated reports instead or host SSRS on an Azure VM. While SQL Managed Instance can't run SSRS as a service, it can host SSRS catalog databases for a reporting server installed on Azure Virtual Machine, using SQL Server authentication.

Query Performance Insight
Yes
No. Use built-in reports in SQL Server Management Studio.

VNet
Partial, it enables restricted access by using VNet Endpoints
Yes, SQL Managed Instance is injected in the VNet.

VNet Service endpoint
Yes, see virtual network service endpoints.
Yes, see service endpoint policies.

VNet Global peering
Yes, using Private IP and service endpoints
Yes, using Virtual network peering.

Private connectivity
Yes, using Private Link
Yes, using VNet-local endpoint or private endpoint

## Resource limits

The following table compares the maximum resource limits available for Azure SQL Database and Azure SQL Managed Instance:

Category
Azure SQL Database
Azure SQL Managed Instance

Compute size
Up to 192 vCores
Up to 128 vCores

Storage size
1 GB - 128 TB
32 GB - 16 TB (32 TB with Next-Gen General Purpose tier)

Tempdb size
32 GB per vCore, up to 2,560 GB
Up to 4 TB - limited by reserved storage size

Log write throughput
Up to 100mb/sec
Depends on service tier and hardware 4.5 MiB/s - 16 MiB/s per vCore (max 220 MiB/s). Next-gen General Purpose supports 6 MiB/s per vCore, up to 220 MiB/s per instance.

Availability
Default enterprise class SLA 
 Increased SLA with zone redundancy
Default enterprise class SLA 
 Increased SLA with zone redundancy

Backups
A choice of locally redundant (LRS), zone-redundant (ZRS), or geo-redundant (GRS) storage 
 1-35 days (7 days by default) retention, with up to 10 years of long-term retention available
A choice of locally redundant (LRS), zone-redundant (ZRS), geo-redundant (GRS) or geo-zone-redundant (GZRS) storage 
 1-35 days (7 days by default) retention, with up to 10 years of long-term retention available

Read-only replicas
Read scale with 1-4 high availability replicas or 1-30 named replicas 
 0 - 4 geo-replicas
1 built-in high availability replica is readable 
 0 - 1 geo-replicas using failover groups

Discount models
Reserved instances
Azure Hybrid Benefit (not available on dev/test subscriptions)
Enterprise and Pay-As-You-Go Dev/Test offer subscriptions
Reserved instances
Azure Hybrid Benefit (not available on dev/test subscriptions)
Enterprise and Pay-As-You-Go Dev/Test offer subscriptions

To learn more about resource limits for Azure SQL Database, review:

- Logical server

- In the vCore model: single databases, elastic pools

- In the DTU model: single databases, elastic pools

To learn more about resource limits for Azure SQL Managed Instance, review: Resource limits.

## Tools

Azure SQL Database and Azure SQL Managed Instance support various data tools that can help you manage your data.

Tool
Azure SQL Database
Azure SQL Managed Instance

Azure portal
Yes
Yes

Azure portal Query editor
Yes
No

Azure CLI
Yes
Yes

Azure PowerShell
Yes
Yes

BACPAC file (export)
Yes, see SQL Database export
Yes, see SQL Managed Instance export

BACPAC file (import)
Yes, see SQL Database import
Yes, see SQL Managed Instance import

Data Quality Services (DQS)
No
No

Master Data Services (MDS)
No
No. Host MDS on an Azure VM. While SQL Managed Instance can't run MDS as a service, it can host MDS databases for an MDS service installed on Azure Virtual Machine, using SQL Server authentication.

SMO
Yes, see SMO.
Yes, since SMO version 150.

SQL Server Data Tools (SSDT)
Yes
Yes

SQL Server Management Studio (SSMS)
Yes
Yes (version 18.0 and higher)

SQL Server PowerShell
Yes
Yes

SQL Server Profiler
No, see Extended events
Yes

System Center Operations Manager
Yes, see Microsoft System Center Management Pack for Azure SQL Database.
Yes, see Microsoft System Center Management Pack for Azure SQL Managed Instance.

## Migration methods

You can use different migration methods to move your data between SQL Server, Azure SQL Database, and Azure SQL Managed Instance. Some methods are Online and pick up all changes that you make on the source while you're running migration. In Offline methods, you need to stop your workload that modifies data on the source while the migration is in progress.

Source
Azure SQL Database
Azure SQL Managed Instance

SQL Server (on-premises, Azure VM, Amazon RDS)
Online: Transactional Replication 
 Offline: BACPAC file (import), BCP
Online: Managed Instance link, Log Replay Service, SQL Server migration experience in Azure Arc, Azure Database Migration Service (DMS), Transactional Replication 
 Offline: Azure Database Migration Service, Native backup/restore, BACPAC file (import), BCP, Snapshot replication

Azure SQL Database
Offline: Azure Database Migration Service (DMS), BACPAC file (import), BCP
Offline: BACPAC file (import), BCP

Azure SQL Managed Instance
Online: Transactional Replication 
 Offline: BACPAC file (import), BCP, Snapshot replication
Online: Database copy/move, Transactional Replication 
 Offline: Cross-instance point-in-time restore (Azure PowerShell or Azure CLI), Native backup/restore, BACPAC file (import), BCP, Snapshot replication

## Related content

Microsoft continues to add features to Azure SQL Database. Visit the Service Updates webpage for Azure for the newest updates using these filters:

- Filtered to Azure SQL Database.

- Filtered to General Availability (GA) announcements for SQL Database features.

For more information about Azure SQL Database and Azure SQL Managed Instance, see:

- What is Azure SQL Database?

- What is Azure SQL Managed Instance?

 
 

 
 

 

 
 
 
 
 
 
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
 2026-10-30
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
