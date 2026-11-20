# https://learn.microsoft.com/en-us/azure/redis/overview

Source: https://learn.microsoft.com/en-us/azure/redis/overview

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
 

 

 

 

 
 
# What is Azure Managed Redis?

 
 
 
 
 
 
- Applies to: â Azure Managed Redis

 
 

 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Managed Redis provides an in-memory data store based on the Redis Enterprise software. Redis Enterprise improves the performance and reliability of the community edition of Redis, while maintaining compatibility. Microsoft operates the service, hosts it on Azure, and any application within or outside of Azure can use it.
For more information on how Azure Managed Redis is built, see Azure Managed Redis Architecture.

Azure Managed Redis can improve the performance and scalability of an application that heavily uses backend data stores. It's able to process large volumes of application requests by keeping frequently accessed data in the server memory, which can be written to and read from quickly.

Redis brings a critical low-latency and high-throughput data storage solution to modern applications. Additionally, Redis is increasingly used for noncaching applications, including data ingestion, deduplication, messaging, and leaderboards

Azure Managed Redis can be deployed standalone, or deployed along with other Azure app or database services, such as Azure Container Apps, Azure App Service, Azure Functions, Azure SQL, or Azure Cosmos DB.

## Key scenarios

Azure Managed Redis improves application performance by supporting common application architecture patterns. Some of the most common patterns include the following:

Pattern
Description

Data cache
Databases are often too large to load directly into a cache. Use the cache-aside pattern to load data into the cache only as needed. When the system makes changes to the data, it can also update the cache, which is then distributed to other clients. Additionally, the system can set an expiration on data, or use an eviction policy to trigger data updates into the cache.

Content cache
Many web pages are generated from templates that use static content such as headers, footers, and banners. These static items shouldn't change often. Using an in-memory cache provides quick access to static content compared to backend datastores. This pattern reduces processing time and server load, allowing web servers to be more responsive. It can reduce the number of servers needed to handle loads. Azure Managed Redis provides the Redis Output Cache Provider to support this pattern with ASP.NET.

Session store
This pattern is commonly used with shopping carts and other user history data that a web application might associate with user cookies. Storing too much data in a cookie can negatively affect performance as the cookie size grows and is passed and validated with every request. A typical solution uses the cookie as a key to query the data in a database. When you use an in-memory cache, like Azure Managed Redis, associating information with a user is faster than interacting with a full relational database.

Deduplication
Often, you need to determine if an action already happened in a system, such as determining if a username is taken or if a customer was already sent an email. In Azure Managed Redis, bloom filters can rapidly determine duplicates and prevent problems.

Leaderboards
Redis offers simple and powerful support for developing leaderboards of all kinds using the sorted set data structure. Additionally, using active geo-replication can allow one leaderboard to be shared globally.

Job and message queuing
Applications often add tasks to a queue when the operations associated with the request take time to execute. Longer running operations are queued to be processed in sequence, often by another server. This method of deferring work is called task queuing. Azure Managed Redis provides a distributed queue to enable this pattern in your application.

PowerBI/Analytics Acceleration
You can use the Redis ODBC driver to utilize Redis for BI, reporting, and analytics use-cases. Because Redis is typically much faster than relational databases, using Redis in this way can dramatically increase query responsiveness.

Distributed transactions
Applications sometimes require a series of commands against a backend data-store to execute as a single atomic operation. All commands must succeed, or all must be rolled back to the initial state. Azure Managed Redis supports executing a batch of commands as a single transaction.

## Redis version

Azure Managed Redis supports Redis 7.4 (the default) and Redis 8.2 (preview). When you create an instance in the Azure portal, select the version from the Redis version drop-down list on the Advanced tab.

To try Redis 8.2, sign up for the Redis 8 preview.

Redis 8.2 (preview) is available for new instances in the Memory Optimized, Balanced, and Compute Optimized tiers, with all Redis modules included. It isn't supported with Flash Optimized SKUs, geo-replication, or custom data access policies. Upgrading existing instances to Redis 8.2 isn't supported.

For version availability by tier and upgrade guidance, see How to upgrade the version of your Azure Managed Redis instance. To create an instance, see Quickstart: Create an Azure Managed Redis instance.

## Choosing the right tier

Four tiers of Azure Managed Redis are available, each with different performance characteristics and price levels.

### Tiers and SKUs at a glance

Here are three tiers that store data in memory:

- Memory Optimized Ideal for memory-intensive use cases that require a high memory-to-vCPU ratio (8:1) but don't need the highest throughput performance. It provides a lower price point for scenarios where less processing power or throughput is necessary, making it an excellent choice for development and testing environments.

- Balanced (Memory + Compute) Offers a balanced memory-to-vCPU (4:1) ratio, making it ideal for standard workloads. This tier provides a healthy balance of memory and compute resources.

- Compute Optimized Designed for performance-intensive workloads requiring maximum throughput, with a low memory-to-vCPU (2:1) ratio. It's ideal for applications that demand the highest performance.

Here's the tier that stores data both in memory and on disk:

- Flash Optimized Enables Redis clusters to automatically move less frequently accessed data from memory (RAM) to NVMe storage. This reduction in memory use can reduce performance, but it allows for cost-effective scaling of caches with large datasets.

You can also use the data persistence feature to store data on-disk for the in-memory tiers. Data persistence stores a backup copy of data on-disk for quick recovery if you experience an unexpected outage. Data persistence is different from the Flash Optimized tier, which is designed to store data on-disk for typical operations.

Storing some data on-disk by using the Flash Optimized tier doesn't increase data resiliency. You can use data persistence on the Flash Optimized tier as well.

Note

For more information on how the Flash Optimized tier is architected, see Azure Managed Redis Architecture.

- For instructions on how to scale between tiers and SKUs, see Scale an Azure Managed Redis instance.

- For pricing information, see the Azure Managed Redis Pricing.

Important

All in-memory tiers that use over 350 GB of storage are in preview, including Memory Optimized M500 and higher; Balanced B500 and higher; and Compute Optimized X500 and higher. All these tiers and higher are in preview.

Flash Optimized tiers A2000 and A4500 are in preview.

### Feature comparison

The following table describes some of the features supported by each tier:

Feature Description
Memory Optimized
Balanced
Compute Optimized
Flash Optimized

Size (GB)
12 - 1920
0.5 - 960
3 - 720
250 - 4500

Service Level Agreement (SLA)
Yes
Yes
Yes
Yes

Data encryption in transit
Yes (Private endpoint)
Yes (Private endpoint)
Yes (Private endpoint)
Yes (Private endpoint)

Replication and failover
Yes
Yes
Yes
Yes

Network isolation
Yes
Yes
Yes
Yes

Microsoft Entra ID based authentication
Yes
Yes
Yes
Yes

Scaling
Yes
Yes
Yes
Yes

High availability
*Yes
*Yes
*Yes
*Yes

Data persistence
Yes
Yes
Yes
Yes

Geo-replication
Yes (Active, Redis 7.4 only)
Yes (Active, Redis 7.4 only)
Yes (Active, Redis 7.4 only)
No

Non-clustered instances
Yes
Yes
Yes
No

Connection audit logs
Yes (Event-based)
Yes (Event-based)
Yes (Event-based)
Yes (Event-based)

JSON data structures(that is, Redis JSON)
Yes
Yes
Yes
Yes

Search functionality (including vector search)
Yes
Yes
Yes
No

Probabilistic data structures (that is, Redis Bloom)
Yes
Yes
Yes
No

Time Series database capability (that is, Redis TimeSeries)
Yes
Yes
Yes
No

Import/Export
Yes
Yes
Yes
Yes

* When High availability is enabled, an Azure Managed Redis instance is deployed with primary and replica shards distributed across at least two nodes.

In regions that support availability zones, Azure Managed Redis distributes the nodes across zones by default. For more information, see Reliability in Azure Managed Redis.

Important

The Balanced B0 and B1 SKU options don't support active geo-replication.

Note

Scaling down support is limited in some situations. For more information, see Limitations of scaling Azure Managed Redis.

### Network performance

If you have a workload that requires high throughput, network bandwidth might cause a bottleneck. You can increase bandwidth by moving up to a higher performance tier or by moving to a large instance size. Larger size instances have more bandwidth because of the underlying VM that hosts the cache. Higher bandwidth limits help you avoid network saturation that causes timeouts in your application. For more information on bandwidth performance, see Performance testing.

### Maximum number of client connections

Each SKU has a maximum number of client connections. This limit increases with higher performance tiers and larger instance sizes. The following table shows the maximum client connections allowed per Azure Managed Redis SKU.

#### Memory Optimized, Balanced, and Compute Optimized SKUs

This table shows the max connections by tier and memory size in the Memory Optimized, Balanced, and Compute SKUs.

Size (GB)
Memory
Optimized
Balanced
Compute
Optimized

0.5
-
15,000
-

1
-
15,000
-

3
-
15,000
30,000

6
-
15,000
30,000

12
15,000
30,000
75,000

24
30,000
75,000
150,000

60
75,000
150,000
200,000

120
150,000
200,000
200,000

175
200,000
200,000
200,000

235
200,000
200,000
200,000

350
200,000
200,000
200,000

480 *
200,000
200,000
200,000

720 *
200,000
200,000
200,000

960 *
200,000
200,000
-

1440 *
200,000
-
-

1920 *
200,000
-
-

4500 *
-
-
-

* The sizes with an asterisk are in preview.

#### Flash Optimized SKU

This table shows the max connections by tier and memory size in the Flash optimized SKU.

Size (GB)
Flash
Optimized

235
75,000

480
150,000

720
200,000

960
200,000

1440
200,000

1920 *
200,000

4500 *
200,000

* The sizes with an asterisk are in preview.

### High availability

Azure Managed Redis provides high availability to the cache endpoints. For more information on the SLA, see the SLA. You can disable high availability in an Azure Managed Redis instance. Disabling high availability lowers the price but results in data loss and downtime. Only disable high availability for dev/test scenarios.

### Other pricing considerations

Important

Azure Managed Redis Enterprise requires an IP address for each cache instance. Currently, Azure Managed Redis absorbs the IP address charge and doesn't pass it on to customers. Billing can change in the future. For more information, see IP address pricing.

Important

Using active geo-replication produces data transfer between Azure regions. Currently, Azure Managed Redis absorbs these bandwidth charges and doesn't pass them on to customers. Billing can change in the future. For more information, see Bandwidth pricing.

### Availability by region

Azure Managed Redis is continually expanding into new regions. To check the availability by region, see Products available by region.

## Moving from Azure Cache for Redis

For more information about migrating from Azure Cache for Redis to Azure Managed Redis, see:

- Migrate Basic, Standard, and Premium tiers to Azure Managed Redis

- Migrate Enterprise tier to Azure Managed Redis

## Related content

- Create an Azure Managed Redis instance

- Azure Managed Redis Architecture

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-17
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
