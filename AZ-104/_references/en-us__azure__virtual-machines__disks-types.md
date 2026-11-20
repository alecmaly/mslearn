# https://learn.microsoft.com/en-us/azure/virtual-machines/disks-types

Source: https://learn.microsoft.com/en-us/azure/virtual-machines/disks-types

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
 

 

 

 

 
 
# Azure managed disk types

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Applies to: âï¸ Linux VMs âï¸ Windows VMs âï¸ Flexible scale sets âï¸ Uniform scale sets

Azure offers five managed disk types, each designed to address a specific customer scenario:

- Ultra Disk

- Premium SSD v2

- Premium SSD (solid-state drive)

- Standard SSD

- Standard HDD (hard disk drive)

## Compare Azure managed disk types

The following table provides a comparison of the five disk types to help you decide which to use.

Note

On September 8, 2028, the ability to use Standard HDDs as OS disks will be retired. To learn more, see Migrate your Standard HDD OS disks by September 08, 2028.

Ultra Disk
Premium SSD v2
Premium SSD
Standard SSD
Standard HDD

Disk type
SSD
SSD
SSD
SSD
HDD

Scenario
I/O-intensive workloads such as SAP HANA, top-tier databases (for example, SQL Server and Oracle Database), and other transaction-heavy workloads.
Production and performance-sensitive workloads that consistently require low latency, high IOPS, and high throughput.
Production workloads that require high performance and low latency.
Web servers, lightly used enterprise applications, and development and test environments.
Backup and other noncritical, infrequently accessed workloads.

Max disk size
65,536 GiB
65,536 GiB
32,767 GiB
32,767 GiB
32,767 GiB

Max throughput
10,000 MB/s
2,000 MB/s
900 MB/s
750 MB/s
500 MB/s

Max IOPS
400,000
80,000
20,000
6,000
2,000, 3,000*

Usable as OS Disk?
No
No
Yes
Yes
Yes (retiring Sept 8, 2028)

* Only applies to disks with performance plus enabled.

For more help deciding which disk type suits your needs, this decision tree should help with typical scenarios:

For a video that covers some high level differences for the different disk types, and some ways for determining what impacts your workload requirements, see Block storage options with Azure Disk Storage and Elastic SAN.

## Ultra Disks

Azure Ultra Disks are the highest-performing storage option for Azure virtual machines (VMs). You can change the performance parameters of an Ultra Disk without having to restart your VMs. Ultra Disks are suited for data-intensive workloads such as SAP HANA, top-tier databases, and transaction-heavy workloads.

Ultra Disks must be used as data disks and can only be created as empty disks. When using Ultra Disks as data disks, use Premium solid-state drives (SSDs) as operating system (OS) disks.

### Ultra Disk size

Ultra Disk sizes range from 4 GiB up to 64 TiB, in 1 GiB increments. Ultra Disk capacity works like Premium SSD v2 disks and you're billed on a per GiB ratio.

By default, for each individual region, you can deploy a total of 100 TiB of capacity as Ultra Disks per subscription. If you need more than 100 TiB of Ultra Disk capacity per region per subscription, request a quota increase or contact Azure Support.

The following table provides an example of performance caps an Ultra Disk has depending on the size you set for the disk.

Disk Size (GiB)
IOPS Cap
Throughput Cap (MB/s)

4
4,000
1,000

8
8,000
2,000

16
16,000
4,000

32
32,000
8,000

64
64,000
10,000

128
128,000
10,000

256
256,000
10,000

512
400,000
10,000

1,024
400,000
10,000

2,048-65,536
400,000
10,000

### Ultra Disk performance

Ultra Disks are designed to provide consistently low submillisecond latency and the highest limits for IOPS and throughput. With Ultra Disks, you can individually set the capacity, throughput, and IOPS of a disk based on your workload needs, increasing flexibility and reducing costs. Each of these values determines the cost of your disk. Within a 24-hour period, you can change the performance of a disk four times. It can take up to an hour for a performance change to take effect.

### Ultra Disk IOPS

Ultra Disks support IOPS limits of 1,000 IOPS per GiB, up to a maximum of 400,000 IOPS per disk. To achieve the target IOPS for the disk, ensure that the selected disk IOPS are less than the VM IOPS limit. Use Ultra Disks with greater IOPS as shared disks to support multiple VMs. The minimum baseline IOPS per disk is 100.

For more information about IOPS, see Virtual machine and disk performance.

### Ultra Disk throughput

The maximum throughput limit of an Ultra Disk is 0.25 MB/s for each provisioned IOPS, up to a maximum of 10,000 MB/s per disk (where MB/s = 10^6 Bytes per second). The minimum guaranteed throughput of an Ultra Disk is 1 MB/s.

You can adjust Ultra Disk IOPS and throughput performance at runtime without detaching the disk from the virtual machine. After a performance resize operation has been issued on a disk, it can take up to an hour for the change to take effect. Up to four performance resize operations are permitted during a 24-hour window.

It's possible for a performance resize operation to fail because of a lack of performance bandwidth capacity.

### Ultra Disk limitations

The following list contains Ultra Disk's limitations:

- Ultra Disks can't be used as an OS disk or with Azure Compute Gallery.

- Currently, Ultra Disks only support Single VM and Availability zone infrastructure options as locally redundant storage (LRS). Ultra Disks don't support zone redundant storage (ZRS).

- Ultra Disks don't support availability sets.

- Ultra Disks don't support disk caching.

Ultra Disks support a 4k physical sector size by default but also supports a 512E sector size. Most applications are compatible with 4k sector sizes, but some require 512-byte sector sizes. Oracle Database, for example, requires release 12.2 or later in order to support 4k native disks. For older versions of Oracle DB, 512-byte sector size is required.

The following table outlines the regions Ultra Disks are available in, and their corresponding availability options.

Note

If a region in the following list lacks availability zones that support Ultra Disks, then a VM in that region must be deployed without infrastructure redundancy to attach an Ultra Disk.

Redundancy options
Regions

Regional
Australia Central
Australia Central 2
Australia Southeast
Brazil Southeast
Canada East
Korea South
North Central US
Norway West
Taiwan North
UAE Central
UK West
US Gov Arizona
US Gov Texas
West US

One availability zone
Brazil South
Central India
East Asia
Korea Central
US Gov Virginia

Two availability zones
Germany West Central
Japan West
Qatar Central
South Central US
Spain Central

Three availability zones
Australia East
Austria East
Canada Central
Central US
China North 3
East US
East US 2
France Central
Indonesia Central
Italy North
Japan East
Malaysia West
New Zealand North
North Europe
Poland Central
South Africa North
Southeast Asia
Sweden Central
Switzerland North
UAE North
UK South
West Europe
West US 2
West US 3

Not every VM size is available in every supported region with Ultra Disks. The following table lists VM series that are compatible with Ultra Disks.

VM Type
Sizes
Description

General purpose
DSv3-series, Ddsv4-series, Dsv4-series, Dasv4-series, Dsv5-series, Ddsv5-series, Dasv5-series, Dplsv6-series, Dpldsv6-series, Dpsv6-series, Dpdsv6-series
Balanced CPU-to-memory ratio. Ideal for testing and development, small to medium databases, and low to medium traffic web servers.

Compute optimized
FSv2-series, Famsv6-series
High CPU-to-memory ratio. Good for medium traffic web servers, network appliances, batch processes, and application servers.

Memory optimized
ESv3-series, Easv4-series, Edsv4-series, Esv4-series, Esv5-series, Edsv5-series, Easv5-series, Ebsv5 series, Ebdsv5 series, M-series, Mv2-series, Msv2, Mdsv2-series, Mbsv3, Mbdsv3-series, Epsv6-series, Epdsv6-series
High memory-to-CPU ratio. Great for relational database servers, medium to large caches, and in-memory analytics.

Storage optimized
LSv2-series, Lsv3-series, Lasv3-series
High disk throughput and IO ideal for Big Data, SQL, NoSQL databases, data warehousing, and large transactional databases.

GPU optimized
NCv3-series, NCasT4_v3-series, ND-series, NDv2-series, NVv3-series, NVv4-series, NVadsA10 v5-series
Specialized virtual machines targeted for heavy graphic rendering and video editing, as well as model training and inferencing (ND) with deep learning. Available with single or multiple GPUs.

Performance optimized
HC-series, HBv2-series
The fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).

If you would like to start using Ultra Disks, see the article on using Azure Ultra Disks.

## Premium SSD v2

Premium SSD v2 offers higher performance than Premium SSDs while also generally being less costly. You can individually tweak the performance (capacity, throughput, and IOPS) of Premium SSD v2 disks at any time, allowing workloads to be cost efficient while meeting shifting performance needs. For example, a transaction-intensive database may need a large amount of IOPS at a small size, or a gaming application may need a large amount of IOPS but only during peak hours. Because of this, for most general purpose workloads, Premium SSD v2 can provide the best price performance.

Premium SSD v2 is suited for a broad range of workloads such as SQL Server, Oracle, MariaDB, SAP, Cassandra, MongoDB, big data and analytics, and gaming on virtual machines or stateful containers.

Premium SSD v2 supports a 4k physical sector size by default but can be configured to use a 512E sector size. While most applications are compatible with 4k sector sizes, some require 512-byte sector sizes. Oracle Database, for example, requires release 12.2 or later to support 4k native disks.

### Differences between Premium SSD and Premium SSD v2

Unlike Premium SSDs, Premium SSD v2 doesn't have dedicated sizes. You can set a Premium SSD v2 to any supported size you prefer, and make granular adjustments to the performance without downtime. Premium SSD v2 doesn't support host caching but, benefits significantly from lower latency, which addresses some of the same core problems host caching addresses. The ability to adjust IOPS, throughput, and size at any time also means you can avoid the maintenance overhead of having to stripe disks to meet your needs.

### Premium SSD v2 limitations

- Premium SSD v2 disks can't be used as an OS disk or with Azure Compute Gallery.

- Premium SSD v2 doesn't support host caching.

- In most regions that support availability zones, you can only attach Premium SSD v2 disks to zonal VMs. When you create a new VM, specify the availability zone you want before adding Premium SSD v2 disks to your configuration.

- In a subset of regions that support availability zones, you can attach nonzonal Premium SSD v2 disks to nonzonal VMs, which have extra limitations.

### Premium SSD v2 regional availability

You can deploy Premium SSD v2 disks as zonal resources or as nonzonal resources. Use a zonal disk when your workload runs in an availability zone. Use a nonzonal disk for a nonzonal VM or in a region without availability zones.

#### Zonal disks

Currently only available in the following regions:

Three Availability Zones

Austria East 
 Australia East 
 Brazil South 
 Canada Central 
 Central India 
 China North 3 
 East Asia 
 North Europe, West Europe 
 France Central 
 Germany West Central 
 Indonesia Central 
 Israel Central 
 Italy North 
 Japan East, Japan West 
 Korea Central 
 Malaysia West 
 Mexico Central 
 New Zealand North 
 Norway East 
 Poland Central 
 South African North 
 Southeast Asia 
 Spain Central 
 Sweden Central 
 Switzerland North 
 UAE North 
 UK South 
 Central US, East US, East US 2, South Central US, West US 2, West US 3 
 US Gov Virginia

To learn when support for particular regions was added, see either Azure Updates or What's new for Azure Disk Storage.

#### Nonzonal disks

Azure supports nonzonal (regional) Premium SSD v2 deployments in the following regions. A nonzonal disk isn't explicitly assigned to an availability zone.

Regions without availability zones
Regions with availability zones

- Australia Central 2 
 - Australia Southeast 
 - Brazil Southeast 
 - Canada East 
 - Germany North 
 - North Central US 
 - Norway West 
 - South India 
 - Switzerland West 
 - Taiwan North 
 - UK West 
 - US Gov Arizona 
 - West Central US 
 - West US
- Australia East 
 - Austria East 
 - Brazil South 
 - Canada Central 
 - Central India 
 - Central US 
 - East Asia 
 - East US 
 - East US 2 
 - France Central 
 - Germany West Central 
 - India South Central 
 - Indonesia Central 
 - Italy North 
 - Japan East 
 - Japan West 
 - Korea Central 
 - Malaysia West 
 - Mexico Central 
 - New Zealand North 
 - North Europe 
 - Norway East 
 - Poland Central 
 - South Africa North 
 - South Central US 
 - Spain Central 
 - South African North 
 - Southeast Asia 
 - Sweden Central 
 - Switzerland North 
 - UK South 
 - West Europe 
 - West US 2 
 - West US 3

To learn when support for particular regions was added, see either Azure Updates or What's new for Azure Disk Storage.

### Premium SSD v2 performance

Premium SSD v2 disks are designed to provide provisioned IOPS and throughput 99.9% of the time. Premium SSD v2 disks are also designed to provide submillisecond latency. With Premium SSD v2 disks, you can individually set the capacity, throughput, and IOPS of a disk based on your workload needs, providing you with more flexibility and reduced costs. Each of these values determines the cost of your disk. You can adjust the performance of a Premium SSD v2 four times within a 24-hour period. Creating a disk counts as one of these times, so for the first 24 hours after creating a Premium SSD v2 you can only adjust its performance up to three times.

#### Premium SSD v2 capacities

Premium SSD v2 capacities range from 1 GiB to 64 TiB, in 1-GiB increments. You're billed on a per GiB ratio, see the pricing page for details.

Premium SSD v2 offers up to 100 TiB per region per subscription by default, but supports higher capacity by request. To request an increase in capacity, request a quota increase or contact Azure Support.

#### Premium SSD v2 IOPS

All Premium SSD v2 disks have a baseline IOPS of 3,000 that is free of charge. After 6 GiB, the maximum IOPS a disk can have increases at a rate of 500 per GiB, up to 80,000 IOPS. So an 8-GiB disk can have up to 4,000 IOPS, and a 10-GiB disk can have up to 5,000 IOPS. To set 80,000 IOPS on a disk, that disk must have at least 160 GiB. Increasing your IOPS beyond 3,000 increases the price of your disk.

#### Premium SSD v2 throughput

All Premium SSD v2 disks have a baseline throughput of 125 MB/s that is free of charge. After 6 GiB, the maximum throughput that can be set increases by 0.25 MB/s per set IOPS. If a disk has 3,000 IOPS, the max throughput it can set is 750 MB/s. To raise the throughput for this disk beyond 750 MB/s, its IOPS must be increased. For example, if you increased the IOPS to 4,000, then the max throughput that can be set is 1,000 MB/s. 2,000 MB/s is the maximum throughput supported for disks that have 8,000 IOPS or more. Increasing your throughput beyond 125 MB/s increases the price of your disk.

#### Premium SSD v2 sector sizes

Premium SSD v2 supports a 4k physical sector size by default. A 512E sector size is also supported. While most applications are compatible with 4k sector sizes, some require 512-byte sector sizes. Oracle Database, for example, requires release 12.2 or later in order to support 4k native disks.

#### Premium SSD v2 performance summary

The following table provides an overview of disk capacities and performance maximums to help you decide which to use.

Disk Size
Maximum available IOPS
Maximum available throughput (MB/s)

1 GiB-64 TiBs
3,000-80,000 (Increases by 500 IOPS per GiB)
125-2,000 (increases by 0.25 MB/s per set IOPS)

To deploy a Premium SSD v2, see Deploy a Premium SSD v2.

## Premium SSDs

Azure Premium SSDs deliver high-performance and low-latency disk support for virtual machines (VMs) with input/output (I/O)-intensive workloads. To take advantage of the speed and performance of Premium SSDs, you can migrate existing VM disks to Premium SSDs. Premium SSDs are suitable for mission-critical production applications, but you can use them only with compatible VM series. Premium SSDs support the 512E sector size.

To learn more about individual Azure VM types and sizes for Windows or Linux, including size compatibility for premium storage, see Sizes for virtual machines in Azure. You'll need to check each individual VM size article to determine if it's premium storage-compatible.

### Premium SSD size

Premium SSD sizes 
P1
P2
P3
P4
P6
P10
P15
P20
P30
P40
P50
P60
P70
P80

Disk size in GiB
4
8
16
32
64
128
256
512
1,024
2,048
4,096
8,192
16,384
32,767

Base provisioned IOPS per disk
120
120
120
120
240
500
1,100
2,300
5,000
7,500
7,500
16,000
18,000
20,000

**Expanded provisioned IOPS per disk
N/A
N/A
N/A
N/A
N/A
N/A
N/A
N/A
8,000
16,000
20,000
20,000
20,000
20,000

Base provisioned Throughput per disk
25 MB/s
25 MB/s
25 MB/s
25 MB/s
50 MB/s
100 MB/s
125 MB/s
150 MB/s
200 MB/s
250 MB/s
250 MB/s
500 MB/s
750 MB/s
900 MB/s

**Expanded provisioned throughput per disk
N/A
N/A
N/A
N/A
N/A
N/A
N/A
N/A
300 MB/s
600 MB/s
900 MB/s
900 MB/s
900 MB/s
900 MB/s

Max burst IOPS per disk
3,500
3,500
3,500
3,500
3,500
3,500
3,500
3,500
30,000*
30,000*
30,000*
30,000*
30,000*
30,000*

Max burst throughput per disk
170 MB/s
170 MB/s
170 MB/s
170 MB/s
170 MB/s
170 MB/s
170 MB/s
170 MB/s
1,000 MB/s*
1,000 MB/s*
1,000 MB/s*
1,000 MB/s*
1,000 MB/s*
1,000 MB/s*

Max burst duration
30 min
30 min
30 min
30 min
30 min
30 min
30 min
30 min
Unlimited*
Unlimited*
Unlimited*
Unlimited*
Unlimited*
Unlimited*

Eligible for reservation
No
No
No
No
No
No
No
No
Yes, up to one year
Yes, up to one year
Yes, up to one year
Yes, up to one year
Yes, up to one year
Yes, up to one year

*Applies only to disks with on-demand bursting enabled.

** Only applies to disks with performance plus enabled.

Capacity, IOPS, and throughput are guaranteed when a Premium SSD is provisioned. For example, if you create a P50 disk, Azure provisions 4,095-GB storage capacity, 7,500 IOPS, and 250-MB/s throughput for that disk. Your application can use all or part of the capacity and performance. Premium SSDs are designed to provide the single-digit millisecond latencies, target IOPS, and throughput described in the Premium SSD size table 99.9% of the time.

### Premium SSD bursting

Premium SSDs offer disk bursting, which provides better tolerance for unpredictable changes in I/O patterns. Disk bursting is especially useful during OS disk boot and for applications with spiky traffic. To learn more about how bursting for Azure disks works, see Disk-level bursting.

### Premium SSD transactions

For Premium SSDs, each I/O operation less than or equal to 256 KiB of throughput is considered a single I/O operation. I/O operations larger than 256 KiB of throughput are considered multiple I/Os of size 256 KiB.

## Standard SSDs

Azure Standard SSDs are optimized for workloads that need consistent performance at lower IOPS levels. They're an especially good choice for customers with varying workloads supported by on-premises hard disk drive (HDD) solutions. Compared to Standard HDDs, Standard SSDs deliver better availability, consistency, reliability, and latency. Standard SSDs are suitable for web servers, low IOPS application servers, lightly used enterprise applications, and non-production workloads. Like Standard HDDs, Standard SSDs are available on all Azure VMs. Standard SSDs support the 512E sector size.

### Standard SSD size

Standard SSD sizes
E1
E2
E3
E4
E6
E10
E15
E20
E30
E40
E50
E60
E70
E80

Disk size in GiB
4
8
16
32
64
128
256
512
1,024
2,048
4,096
8,192
16,384
32,767

Base IOPS per disk
Up to 500
Up to 500
Up to 500
Up to 500
Up to 500
Up to 500
Up to 500
Up to 500
Up to 500
Up to 500
Up to 500
Up to 2,000
Up to 4,000
Up to 6,000

*Expanded IOPS per disk
N/A
N/A
N/A
N/A
N/A
N/A
N/A
N/A
Up to 1,500
Up to 3,000
Up to 6,000
Up to 6,000
Up to 6,000
Up to 6,000

Base throughput per disk
Up to 100 MB/s
Up to 100 MB/s
Up to 100 MB/s
Up to 100 MB/s
Up to 100 MB/s
Up to 100 MB/s
Up to 100 MB/s
Up to 100 MB/s
Up to 100 MB/s
Up to 100 MB/s
Up to 100 MB/s
Up to 400 MB/s
Up to 600 MB/s
Up to 750 MB/s

*Expanded throughput per disk
N/A
N/A
N/A
N/A
N/A
N/A
N/A
N/A
Up to 150 MB/s
Up to 300 MB/s
Up to 600 MB/s
Up to 750 MB/s
Up to 750 MB/s
Up to 750 MB/s

Max burst IOPS per disk
600
600
600
600
600
600
600
600
1000

Max burst throughput per disk
150 MB/s
150 MB/s
150 MB/s
150 MB/s
150 MB/s
150 MB/s
150 MB/s
150 MB/s
250 MB/s

Max burst duration
30 min
30 min
30 min
30 min
30 min
30 min
30 min
30 min
30 min

* Only applies to disks with performance plus enabled.

Standard SSDs are designed to provide single-digit millisecond latencies and the IOPS and throughput up to the limits described in the Standard SSD size table 99% of the time. Actual IOPS and throughput might vary depending on the traffic patterns. Standard SSDs provide lower latency and more consistent performance than Standard HDDs.

### Standard SSD transactions

For Standard SSDs, each I/O operation less than or equal to 256 KiB of throughput is considered a single I/O operation. I/O operations larger than 256 KiB of throughput are considered multiple I/Os of size 256 KiB. These transactions incur a billable cost but, there's an hourly limit on the number of transactions that can incur a billable cost. If that hourly limit is reached, additional transactions during that hour no longer incur a cost. For details, see Standard SSD transaction billing caps.

### Standard SSD bursting

Standard SSDs offer disk bursting, which provides better tolerance for unpredictable changes in I/O patterns. OS boot disks and applications prone to traffic spikes both benefit from disk bursting. To learn more about how bursting for Azure disks works, see Disk-level bursting.

## Standard HDDs

Azure Standard HDDs are suitable for latency-tolerant workloads that use large, sequential I/O, such as light data processing workloads that read or write large files sequentially. Standard HDDs aren't suitable for workloads that require low latency or frequent small-block access, such as OS disks or transactional databases. Use either Standard SSDs or Premium SSD managed disks for these workloads. Standard HDDs are designed to deliver write latencies of less than 10 ms and read latencies of less than 20 ms for most I/O operations. Performance can vary more widely than the performance of SSD-based disks, depending on I/O size and workload pattern. Standard HDDs are available in all Azure regions and can be used with all Azure VMs. Standard HDDs support the 512E sector size.

### Standard HDD size

Standard Disk Type
S4
S6
S10
S15
S20
S30
S40
S50
S60
S70
S80

Disk size in GiB
32
64
128
256
512
1,024
2,048
4,096
8,192
16,384
32,767

Base IOPS per disk
Up to 500
Up to 500
Up to 500
Up to 500
Up to 500
Up to 500
Up to 500
Up to 500
Up to 1,300
Up to 2,000
Up to 2,000

*Expanded IOPS per disk
N/A
N/A
N/A
N/A
N/A
Up to 1,500
Up to 3,000
Up to 3,000
Up to 3,000
Up to 3,000
Up to 3,000

Base throughput per disk
Up to 60 MB/s
Up to 60 MB/s
Up to 60 MB/s
Up to 60 MB/s
Up to 60 MB/s
Up to 60 MB/s
Up to 60 MB/s
Up to 60 MB/s
Up to 300 MB/s
Up to 500 MB/s
Up to 500 MB/s

*Expanded throughput per disk
N/A
N/A
N/A
N/A
N/A
Up to 150 MB/s
Up to 300 MB/s
Up to 500 MB/s
Up to 500 MB/s
Up to 500 MB/s
Up to 500 MB/s

* Only applies to disks with performance plus enabled.

### Standard HDD transactions

For Standard HDD managed disks, each I/O operation less than or equal to 16 KiB of throughput is considered a single billable transaction. I/O operations larger than 16 KiB of throughput are considered multiple billable transactions of size 16 KiB for billing purposes. Cost is incurred for every 10,000 billable transactions but, thereâs an hourly limit on the number of billable transactions that can incur a billable cost. If your individual diskâs billable transactions reach that hourly limit, any additional billable transactions during that hour donât incur a cost. For details, see the blog post.

## Azure managed disk billing

When using managed disks, the following billing considerations apply:

- Disk type

- Managed disk size

- Snapshots

- Outbound data transfers

- Number of transactions

### Managed disk size

Managed disks are billed according to their provisioned size. Azure maps the provisioned size (rounded up) to the nearest offered disk size. For the disk sizes offered for each managed disk type, see Ultra Disk size, Premium SSD v2 capacities, Premium SSD size, Standard SSD size, and Standard HDD size. Each disk maps to a supported provisioned disk-size offering and is billed accordingly. For example, if you provisioned a 200-GiB Standard SSD, it maps to the disk size offer of E15 (256 GiB). Billing for any provisioned disk is prorated hourly by using the monthly price for the storage offering. For example, you provision an E10 disk and delete it after 20 hours of use. In this case, you're billed for the E10 offering prorated to 20 hours, regardless of the amount of data written to the disk.

### Snapshots

Snapshots are billed based on the size used. For example, you create a snapshot of a managed disk with provisioned capacity of 64 GiB and actual used data size of 10 GiB. In this case, the snapshot is billed only for the used data size of 10 GiB.

For more information on snapshots, see Create a snapshot of a virtual hard disk.

### Outbound data transfers

Outbound data transfers (data going out of Azure data centers) incur billing for bandwidth usage.

### Transactions

You're billed for the number of transactions performed on a standard managed disk. For Standard SSDs, each I/O operation less than or equal to 256 KiB of throughput is considered a single I/O operation. I/O operations larger than 256 KiB of throughput are considered multiple I/Os of size 256 KiB. For Standard HDDs, each I/O operation less than or equal to 16 KiB of throughput is considered a single billable transaction. I/O operations larger than 16 KiB of throughput are considered multiple I/Os of size 16 KiB. For details, see Standard HDD transactions. 

For detailed information on pricing for managed disks (including transaction costs), see managed disk pricing.

### Ultra Disk VM reservation fee

Azure VMs have the capability to indicate if they're compatible with Ultra Disks. An Ultra Disk-compatible VM allocates dedicated bandwidth capacity between the compute VM instance and the block storage scale unit to optimize the performance and reduce latency. When you add this capability on the VM, it results in a reservation charge. The reservation charge is only imposed if you enabled Ultra Disk capability on the VM without an attached Ultra Disk. When an Ultra Disk is attached to the Ultra Disk compatible VM, the reservation charge wouldn't be applied. This charge is per vCPU provisioned on the VM.

Note

For constrained core VM sizes, the reservation fee is based on the actual number of vCPUs and not the constrained cores. For Standard_E32-8s_v3, the reservation fee will be based on 32 cores.

For Ultra Disk pricing details, see the Azure managed disk pricing page.

### Azure disk reservation

An Azure disk reservation provides a discount when you purchase one year of disk storage in advance. When you purchase a disk reservation, you select a specific disk SKU in a target region. For example, you might choose five P30 (1 TiB) Premium SSDs in the Central US region for a one-year term. The disk reservation experience is similar to Azure reserved VM instances. You can bundle VM and disk reservations to maximize your savings. Azure disk reservations offer a one-year commitment plan for Premium SSD SKUs from P30 (1 TiB) to P80 (32 TiB) in all production regions. For more information about reserved disk pricing, see the Azure managed disk pricing page.

## Next steps

- Learn more about how managed disks are billed, see Understand Azure Disk Storage billing.

- Learn the Best practices for achieving high availability with Azure virtual machines and managed disks.

- Learn about the Performance options for managed disks.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-09-15
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
