# https://learn.microsoft.com/en-us/azure/storage/common/nfs-comparison

Source: https://learn.microsoft.com/en-us/azure/storage/common/nfs-comparison

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
 

 

 

 

 
 
# Compare access to Azure Files, Blob Storage, and Azure NetApp Files with NFS

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This article provides a comparison between each of these offerings if you access them through the Network File System (NFS) protocol. This comparison doesn't apply if you access them through any other method.

For more general comparisons, see this article to compare Azure Blob Storage and Azure Files, or this article to compare Azure Files and Azure NetApp Files.

## Comparison

Category
Azure Blob Storage
Azure Files
Azure NetApp Files

Use cases
Blob Storage is best suited for large scale read-heavy sequential access workloads where data is ingested once and minimally modified further.

Blob Storage offers the lowest total cost of ownership, if there is little or no maintenance.

Some example scenarios are: Large scale analytical data, throughput sensitive high-performance computing, backup and archive, autonomous driving, media rendering, or genomic sequencing.
Azure Files is a highly available service best suited for random access workloads.

For NFS shares, Azure Files provides full POSIX file system support and can easily be used from container platforms like Azure Container Instance (ACI) and Azure Kubernetes Service (AKS) with the built-in CSI driver, in addition to VM-based platforms.

Some example scenarios are: Shared files, databases, home directories, traditional applications, ERP, CMS, NAS migrations that don't require advanced management, and custom applications requiring scale-out file storage.
Fully managed file service in the cloud, powered by NetApp, with advanced management capabilities.

Azure NetApp Files is suited for workloads that require random access and provides broad protocol support and data protection capabilities.

Some example scenarios are: On-premises enterprise NAS migration that requires rich management capabilities, latency sensitive workloads like SAP HANA, latency-sensitive or IOPS intensive high performance compute, or workloads that require simultaneous multi-protocol access.

Available protocols
NFSv3

REST

Data Lake Storage
SMB

NFSv4.1

 REST
NFSv3 and NFSv4.1

SMB

Dual protocol (SMB and NFSv3, SMB and NFSv4.1)

Key features
Integrated with HPC cache for low latency workloads. 
 
 Integrated management, including lifecycle, immutable blobs, data failover, and metadata index.
Zone redundant for high availability. 

 Consistent single-digit millisecond latency. 

Predictable performance and cost that scales with capacity.
Extremely low latency (as low as sub-ms).

Rich ONTAP management capabilities such as snapshots, backup, cross-region replication, and cross-zone replication.

Consistent hybrid cloud experience.

Performance (Per volume)
Up to 20,000 IOPS, up to 15 GiB/s throughput.
Up to 100,000 IOPS, up to 10 GiB/s throughput.
Up to 460,000 IOPS, up to 4.5 GiB/s throughput per regular volume, up to 12.5 GiB/s throughput per large volume.

Scale
Up to 5 PiB for a single volume. 

 Up to 190.7 TiB for a single blob.

No minimum capacity requirements.
Up to 100 TiB for a single file share.

Up to 4 TiB for a single file.

50 GiB min capacity.
Up to 100 TiB for a single regular volume, up to 2 PiB for a large volume.

Up to 16 TiB for a single file.

Consistent hybrid cloud experience.

Pricing
Azure Blob Storage pricing
Azure Files pricing
Azure NetApp Files pricing

## Next steps

- To access Blob storage with NFS, see Network File System (NFS) 3.0 protocol support in Azure Blob Storage.

- To access Azure Files with NFS, see NFS file shares in Azure Files.

- To access Azure NetApp Files with NFS, see Quickstart: Set up Azure NetApp Files and create an NFS volume.

 
 

 
 

 

 
 
 
 
 
 
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
 2025-05-20
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
