# https://learn.microsoft.com/en-us/azure/storage/blobs/scalability-targets

Source: https://learn.microsoft.com/en-us/azure/storage/blobs/scalability-targets

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
 

 

 

 

 
 
# Scalability and performance targets for Blob storage

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This reference details scalability and performance targets for Azure Storage. The scalability and performance targets listed here are high-end targets, but they're achievable. In all cases, the request rate and bandwidth that your storage account achieves depend on the size of objects stored, the access patterns used, and the type of workload your application performs.

Test your service to determine whether its performance meets your requirements. If possible, avoid sudden spikes in the rate of traffic and ensure that traffic is well-distributed across partitions.

When your application reaches the limit of what a partition can handle for your workload, Azure Storage begins to return error code 503 (Server Busy) or error code 500 (Operation Timeout) responses. If 503 errors occur, consider modifying your application to use an exponential backoff policy for retries. The exponential backoff decreases the load on the partition and eases spikes in traffic to that partition.

For the service-level agreement (SLA) for Azure Storage accounts, see SLA for Storage Accounts.

## Scale targets for Blob storage

Resource
Target

Maximum size of single blob container
Same as maximum storage account capacity

Maximum number of blocks in a block blob or append blob
50,000 blocks

Maximum size of a block in a block blob
4,000 MiB

Maximum size of a block blob
50,000 x 4,000 MiB (approximately 190.7 TiB)

Maximum size of a block in an append blob
4 MiB

Maximum size of an append blob
50,000 x 4 MiB (approximately 195 GiB)

Maximum size of a page blob
8 TiB2

Maximum number of stored access policies per blob container
5

Target request rate for a single block blob
Up to 3,000 requests per second

Target request rate for a single page blob
Up to 500 requests per second

Target throughput for a single page blob
Up to 60 MiB per second2

Target throughput for a single block blob
Up to storage account ingress/egress limits1

1 Throughput for a single blob depends on several factors. These factors include but aren't limited to concurrency, request size, performance tier, speed of source for uploads, and destination for downloads. To take advantage of the performance enhancements of high-throughput block blobs, upload larger blobs or blocks. Specifically, call the Put Blob or Put Block operation with a blob or block size that's greater than 256 KiB.

2 Page blobs aren't yet supported in accounts that have a hierarchical namespace enabled.

The following table describes the maximum block and blob sizes permitted by service version.

Service version
Maximum block size (via Put Block)
Maximum blob size (via Put Block List)
Maximum blob size via single write operation (via Put Blob)

Version 2019-12-12 and later
4,000 MiB
Approximately 190.7 TiB (4,000 MiB x 50,000 blocks)
5,000 MiB

Version 2016-05-31 through version 2019-07-07
100 MiB
Approximately 4.75 TiB (100 MiB x 50,000 blocks)
256 MiB

Versions prior to 2016-05-31
4 MiB
Approximately 195 GiB (4 MiB x 50,000 blocks)
64 MiB

## Hot partitions: detection, monitoring, and mitigation

Azure Blob Storage distributes data and requests across partitions to help scale workloads. A storage account can have available capacity and throughput while workloads that concentrate traffic on a narrow range of partition keys experience partition-level throughput constraints.

When a single partition receives significantly more traffic than other partitions, it becomes a hot partition. The partition key for a blob combines the storage account name, container name, and blob name, so sequential or append-only naming schemes can concentrate traffic on a single partition.

When a partition becomes hot, your application might observe increased latency and receive HTTP 503 (Server Busy) or HTTP 500 (Operation Timeout) responses before the storage account approaches its documented scalability limits.

To mitigate hot partitions:

- Avoid sequential or append-only blob naming schemes that concentrate traffic on a single partition.

- Use an exponential backoff retry strategy when throttling errors occur.

- Increase request rates gradually when you introduce new workloads.

To detect throttling and identify the source of excessive demand, use Azure Monitor metrics and resource logs.

For more information, see Mitigate hot partitions in Azure Blob Storage.

## See also

- Performance and scalability checklist for Blob storage

- Scalability targets for standard storage accounts

- Scalability targets for premium block blob storage accounts

- Scalability targets for the Azure Storage resource provider

- Azure subscription limits and quotas

 
 

 
 

 

 
 
 
 
 
 
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
 2026-07-27
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
