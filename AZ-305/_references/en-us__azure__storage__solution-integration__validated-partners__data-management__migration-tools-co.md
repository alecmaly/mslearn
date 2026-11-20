# https://learn.microsoft.com/en-us/azure/storage/solution-integration/validated-partners/data-management/migration-tools-comparison

Source: https://learn.microsoft.com/en-us/azure/storage/solution-integration/validated-partners/data-management/migration-tools-comparison

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
 

 

 

 

 
 
# Comparison matrix

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 The following comparison matrix shows basic functionality of different tools that can be used for migration of unstructured data.

Tip

Azure File Sync can be utilized for migrating data to Azure Files, even if you don't intend to use a hybrid solution for on-premises caching or syncing. This migration process is efficient and causes no downtime. To use Azure File Sync as a migration tool, simply deploy it and, after the migration is finished, remove the server endpoint. Ideally Azure File Sync would be used long-term, while Storage Mover and AzCopy are intended for migration focused activities.

## Overview comparison

Microsoft
Microsoft
Microsoft
Data Dynamics
Komprise
Atempo
Cirrus Data

Solution name
AzCopy
Azure Data Box
Azure Storage Mover
Data Mobility and Migration
Elastic Data Migration
Miria
Migrate Cloud

Support provided by
Microsoft
Microsoft
Microsoft
Data Dynamics1
Komprise1
Atempo1
Cirrus Data1

Assessment
No
No
No
Yes
Yes
Yes
Yes

SAN Migration
No
No
No
No
No
No
Yes

NFS to Azure Blob
Yes
Yes
Yes
Yes
Yes
Yes
No

NFS to NFS
No
No
No
Yes
Yes
Yes
No

SMB to Azure Files
Yes
Yes
Yes
Yes
Yes
Yes
No

SMB to Azure NetApp Files
No
No
No
Yes
Yes
Yes
No

Lustre
No
No
No
No
No
Yes
No

Tip

As Cirrus Data specializes in SAN / Block data migrations, we have omitted them from the remainder of this document, which compares File data migration features. For more information about Cirrus Data and their Migrate Cloud solution, please review the Cirrus Data getting Started Guide.

## Supported Azure services

Microsoft
Microsoft
Microsoft
Data Dynamics
Komprise
Atempo

Solution name
AzCopy
Azure Data Box
Azure Storage Mover
Data Mobility and Migration
Elastic Data Migration
Miria

Support provided by
Microsoft
Microsoft
Microsoft
Data Dynamics1
Komprise1
Atempo1

Azure Files support (all tiers)
Yes
Yes
Yes
Yes
Yes
Yes

Azure NetApp Files support
No
No
No
No
Yes
Yes

Azure Blob Hot / Cool support
Yes
Yes
Yes
Yes
Yes
Yes

Azure Blob Archive tier support
Yes
Yes
No
No
Yes
Yes

Azure Data Lake Storage support
Yes
Yes
No
Yes
Yes
No

Supported Sources
Any NAS, Azure Blob, Azure Files, Google Cloud Storage, and AWS S3
Any SMB/NFS share on servers and NAS devices
Any SMB/NFS share on servers and NAS devices
Any NAS, and S3
Any NAS, Cloud File Storage, or S3
Any NAS, S3, PFS, and Swift

## Supported protocols (source / destination)

Microsoft
Microsoft
Microsoft
Data Dynamics
Komprise
Atempo

Solution name
AzCopy
Azure Data Box
Azure Storage Mover
Data Mobility and Migration
Elastic Data Migration
Miria

SMB 2.1
Source
Yes
Yes
Yes
Yes
Yes

SMB 3.0
Source
Source
Source
Yes
Yes
Yes

SMB 3.1
Source/Destination (Azure Files SMB)
Source/Destination (Azure Files SMB)
Source/Destination (Azure Files SMB)
Yes
Yes
Yes

NFS v3
Source/Destination (Azure Blob NFSv3)
Source/Destination (Azure Blob NFSv3)
Source/Destination (Azure Blob NFSv3)
Yes
Yes
Yes

NFS v4.1
Source
Source
Source
Yes
No
Yes

Blob REST API
Yes
Destination
Destination
Yes
Yes
Yes

S3
Source
No
Source
Yes
Yes
Yes

Google Cloud Storage
Source
No
No
Yes
Yes
Yes

## Extended features

Microsoft
Microsoft
Microsoft
Data Dynamics
Komprise
Atempo

Solution name
AzCopy
Azure Data Box
Azure Storage Mover
Data Mobility and Migration
Elastic Data Migration
Miria

UID / SID remapping
No
No
No
Yes
No
No

Protocol ACL remapping
No
No
No
No
No
No

Azure Data Lake Storage
Yes
No
No
Yes
Yes
No

Throttling support
Yes
No
No
Yes
No
Yes

File pattern exclusions
Yes
No
No
Yes
Yes
Yes

Support for selective file attributes
No
No
No
Yes
Yes
Yes

Delete propagations
No
No
Yes
Yes
Yes
Yes

Follow NTFS junctions
No
No
No
No
Yes
Yes

Override SMB Owner and Group Owner
No
No
No
Yes
No
Yes

Chain of custody reporting
No
No
No
Yes
Yes
Yes

Support for alternate data streams
No
No
No
Yes
No
Yes

Scheduling for migration
No
No
No
Yes
Yes
Yes

Preserving ACL
Yes
Yes
Yes
Yes
Yes
Yes

DACL support
Yes
Yes
Yes
Yes
Yes
Yes

SACL support
Yes
Yes
Yes
Yes
No
Yes

Preserving access time
Yes (Azure Files)
Yes
Yes
Yes
Yes
Yes

Preserving modified time
Yes (Azure Files)
Yes
Yes
Yes
Yes
Yes

Preserving creation time
Yes (Azure Files)
Yes
Yes
Yes
Yes
Yes

Azure Data Box support
Yes
Yes
Yes
Yes
No
Yes

Migration of snapshots
No
No
No
Yes
No
No

Symbolic link support
Yes
Yes
No
No
Yes
Yes

Hard link support
Migrated as separate files
Migrated as separate files
Migrated as separate files
Yes
Yes
Yes

Support for open / locked files
No
No
No
Yes
Yes
Yes

Incremental migration
Yes
No
No
Yes
Yes
Yes

Switchover support
No
No
No
Yes
No (manual only)
Yes

Other features
Link

Link
Link
Link

## Assessment and reporting

Microsoft
Microsoft
Microsoft
Data Dynamics
Komprise
Atempo

Solution name
AzCopy
Azure Data Box
Azure Storage Mover
Data Mobility and Migration
Elastic Data Migration
Miria

Capacity
No
Reporting
Reporting
Yes
Yes
Yes

# of files / folders
Yes
Reporting
Reporting
Yes
Yes
Yes

Age distribution over time
No
No
No
Yes
Yes
Yes

Access time
No
No
No
Yes
Yes
Yes

Modified time
No
No
No
Yes
Yes
Yes

Creation time
No
No
No
Yes
Yes
Yes

Per file / object report status
Yes
Reporting
Reporting
Yes
Yes
Yes

## Licensing

Microsoft
Microsoft
Microsoft
Data Dynamics
Komprise
Atempo

Solution name
AzCopy
Azure Data Box
Azure Storage Mover
Data Mobility and Migration
Elastic Data Migration
Miria

BYOL
Free
Free
Free
Yes
Yes
Yes

Azure Commitment
Free
Free
Free
Yes
Yes
No

## Other features

### AzCopy

- Multi-platform support

- Windows 32-bit / 64-bit

- Linux x86-64 and ARM64

- macOS Intel and ARM64

- Benchmarking azcopy bench

- Supports block blobs, page blobs, and append blobs

- MD5 checks for downloads

- Customizable transfer rate to preserve bandwidth on the client

- Tagging

### Data Dynamics Data Mobility and Migration

- Hash validation

### Komprise Elastic Data Migration

- Project/directory based migrations

- Migration prechecks with analytics

- Migration planning with analytics

- Assessment / reporting: File types, file size, project based

- Assessment / reporting: Custom metadata-based searches

- Simple UI migration management

- API access to automate large migration jobs

- Automatic retry of failures

- Access time-based analytics for Azure Blob Storage, and S3

- Tagging support

- Support 24 x 7 x 365

- In-product support via chat built-in

- Hash validation

### Atempo Miria

- Custom metadata management

- Automation through API

- Petabyte-scale data movements

- Hash validation

Note

List was last verified on August 24, 2023

## See also

- Storage migration overview

- Choose an Azure solution for data transfer

- Migrate to Azure file shares

- Migrate to Data Lake Storage with WANdisco LiveData Platform for Azure

- Copy or move data to Azure Storage with AzCopy

- Migrate large datasets to Azure Blob Storage with AzReplicate (sample application)

Important

1 Support provided by ISV, not Microsoft

 
 

 
 

 

 
 
 
 
 
 
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
 2025-07-02
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
