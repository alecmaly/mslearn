# https://learn.microsoft.com/en-us/azure/azure-subscription-service-limits

Source: https://learn.microsoft.com/en-us/azure/azure-subscription-service-limits

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
 

 

 

 

 
 
# Azure subscription and service limits, quotas, and constraints

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This document lists some of the most common Microsoft Azure limits, which are also sometimes called quotas.

- To learn more about Azure pricing, see the Azure pricing overview and details page.

- The Azure pricing page provides details for specific services; for example, Windows Virtual Machines.

- You can also use the Azure pricing calculator to estimate your costs.

- See What is Microsoft Billing? for tips to help manage your costs.

## How to manage limits

Note

Some services have adjustable limits.

When the limit can be adjusted, the tables include Default limit and Maximum limit headers. The limit can be raised above the default limit but not above the maximum limit. Some services with adjustable limits use different headers with information about adjusting the limit.

When a service doesn't have adjustable limits, the following tables use the header Limit without any additional information about adjusting the limit. In those cases, the default and the maximum limits are the same.

If you want to raise the limit or quota above the default limit, open an online customer support request at no charge.

The terms soft limit and hard limit are often used informally to describe the current, adjustable limit (soft limit) and the maximum limit (hard limit). If a limit isn't adjustable, there won't be a soft limit but only a hard limit.

Free Azure trial subscriptions aren't eligible for limit or quota increases. If you have this type of subscription, you can upgrade to a Pay-as-you-go one. For more information, see Upgrade your Azure account and the overviews for Try Azure for free or pay as you go.

Some limits are managed at a regional level. You decide what your quotas must be for your workload in any one region, and then request that amount for each region into which you want to deploy.

For example, with virtual central processing unit (vCPU) quotas:

- To request a quota increase with support for vCPUs, you decide how many vCPUs to use in which regions.

- You then request an increase in vCPU quotas for the amounts and regions that you want.

- If you need to use 30 vCPUs in West Europe to run your application there, you specifically request 30 vCPUs in West Europe.

- Your vCPU quota doesn't increase in any other region; only West Europe has the 30-vCPU quota.

See Resolve errors for resource quotas for more information about how to determine quotas for specific regions.

## General limits

- See Naming rules and restrictions for Azure resources for limits on resource names.

- See Understand how Azure Resource Manager throttles requests to learn about Resource Manager API read and write limits.

### Azure management group limits

The following limits apply to Azure management groups.

Resource
Limit

Management groups per Microsoft Entra tenant
10,000

Subscriptions per management group
Unlimited

Levels of management group hierarchy
Root level plus 6 levels1

Direct parent management group per management group
One

Management group level deployments
8002

Locations of Management group level deployments
10

1The 6 levels don't include the subscription level.

2If you reach the limit of 800 deployments, delete deployments from the history that are no longer needed. To delete management group level deployments, use Remove-AzManagementGroupDeployment or az deployment mg delete. Deployments are automatically deleted from the history as you near the limit. Deleting an entry from the deployment history doesn't affect the deployed resources. For more information, see Automatic deletions from deployment history.

### Azure subscription limits

The following limits apply when you use Azure Resource Manager and Azure resource groups.

Resource
Limit

Azure subscriptions associated with a Microsoft Entra tenant
Unlimited

Coadministrators per subscription
Unlimited

Resource groups per subscription
980

Azure Resource Manager API request size
4,194,304 bytes

Tags per subscription1
50

Unique tag calculations per subscription2
80,000

Subscription-level deployments
8003

Locations of Subscription-level deployments
10

1You can apply up to 50 tags directly to a subscription. Within the subscription, each resource or resource group is also limited to 50 tags. However, the subscription can contain an unlimited number of tags that are dispersed across resources and resource groups.

2Resource Manager returns a list of tag name and values in the subscription only when the number of unique tags is 80,000 or less. A unique tag is defined by the combination of resource ID, tag name, and tag value. For example, two resources with the same tag name and value would be calculated as two unique tags. You still can find a resource by tag when the number exceeds 80,000.

3Deployments are automatically deleted from the history as you near the limit. For more information, see Automatic deletions from deployment history.

Note that subscription IDs must be non-empty GUIDs.

### Azure resource group limits

Resource
Limit

Resources per resource group
Resources aren't limited by resource group. Instead, they're limited by resource type in a resource group. See next row.

Resources per resource group, per resource type
800 - Some resource types can exceed the 800 limit. See Resources not limited to 800 instances per resource group.

Deployments per resource group in the deployment history
8001

Resources per deployment
800

Management locks per unique scope
20

Number of tags per resource or resource group
50

Tag key length
512

Tag value length
256

1Deployments are automatically deleted from the history as you near the limit. Deleting an entry from the deployment history doesn't affect the deployed resources. For more information, see Automatic deletions from deployment history.

#### Template limits

Value
Limit

Parameters
256

Variables
256

Resources (including copy count)
800

Outputs
64

Template expression
24,576 chars

Resources in exported templates
200

Template size
4 MB

Resource definition size
1 MB

Parameter file size
4 MB

You can exceed some template limits by using a nested template. For more information, see Use linked templates when you deploy Azure resources. To reduce the number of parameters, variables, or outputs, you can combine several values into an object. For more information, see Objects as parameters.

You may get an error with a template or parameter file of less than 4 MB, if the total size of the request is too large. For more information about how to simplify your template to avoid a large request, see Resolve errors for job size exceeded.

## Azure API Center limits

Resource
Free plan1
Standard plan2

APIs
200
10,000

Versions per API
5
100

Definitions per version
5
5

Deployments per API
10
10

Environments
20
20

Workspaces
1 (Default)
1 (Default)

Custom metadata properties per entity3
10
20

Child properties in custom metadata property of type "object"
10
10

Requests per minute (data plane)
3,000
6,000

API definitions analyzed per 24 hours
10
2,0004

Analysis profiles
1
3

AI asset assessments per 24 hours
N/A
2,000

Linked (integrated) API sources5
1
5

APIs synchronized from a linked API source
200
10,0004

Assets synchronized from a linked Git source
100
10,0004

Files per asset from a linked Git source
5
15

Files from a linked Git source
500
10,000

File size limit (per file) from a linked Git source
100 KB
2 MB

Dependencies
200
200

Semantic search in API Center portal
No
Yes

1 Use of full service features including API analysis is limited.

2 To increase a limit in the Standard plan, contact support.

3 Custom metadata properties assigned to APIs, deployments, and environments.

4 Process can take a few minutes to up to 24 hours to complete.

5 Sources such as linked API Management instances.

## Azure API Management limits

This section provides information about limits that apply to Azure API Management instances in different service tiers, including the following:

- Resource limits in API Management classic and v2 tiers

- Resource limits in API Management workspaces

- Resource limits in developer portal in API Management v2 tiers

- Gateway runtime limits

### Limits - API Management classic and v2 tiers

The following limits are introduced starting March 2026. Services in the classic tiers that surpass the revised limits are allowed to keep their existing capacity. For more information, see Understanding API Management service limits.

Note

- Limits are per service instance unless stated otherwise.

- When counting the number of API-related resources (such as API operations and tags), API Management also includes API versions and revisions.

Entity/Resource
Consumption
Developer
Basic/
Basic v2
Standard/
Standard v2
Premium/
Premium v2

API operations
3,000
3,000
10,000
50,000
75,000

API tags
1,500
1,500
1,500
2,500
15,000

Named values
5,000
5,000
5,000
10,000
18,000

Loggers
100
100
100
200
400

Products
100
100
200
500
2,000

Subscriptions
N/A
10,000
15,000
25,000
75,000

Users
N/A
20,000
20,000
50,000
75,000

User-assigned managed identities
10
10
10
10
10

Workspaces per workspace gateway
N/A
N/A
301
301
30

Self-hosted gateways
N/A
5
N/A
N/A
1002

1 Currently applies to v2 tiers only.

2 Applies to Premium tier only.

### Limits - API Management workspaces

The following are resource limits per workspace in Azure API Management:

Resource
Workspace - Premium tier

Workspaces per instance
100

Scale units per premium workspace gateway
12

APIs (including versions and revisions)
200

API operations
5,000

Operations per API
100

Releases per API
100

Schemas per API
100

Subscriptions per API
200

Tags per API
100

Backends
200

Certificates
200

Groups
50

Loggers
50

Named values
200

Policy fragments
50

Products
100

APIs per product
200

Groups per product
200

Subscriptions per product
1,000

Tags per product
50

Schemas
500

Subscriptions
5,000

Tags
200

Groups per user
200

Version sets
50

### Limits - Developer portal in API Management v2 tiers

Item
Basic v2
Standard v2
Premium v2

Number of media files to upload
15
15
15

Size of a media file
500 KB
500 KB
500 KB

Number of pages
30
50
50

Number of widgets1
30
50
50

Size of metadata per page
350 KB
350 KB
350 KB

Size of metadata per widget1
350 KB
350 KB
350 KB

Number of client requests per minute
200
200
200

1 Limit for built-in widgets such as text, images, or APIs list. Currently, custom widgets and custom HTML code widgets aren't supported in the v2 tiers.

### API Management gateway runtime limits

Runtime limit
Classic
V2
Consumption

Concurrent back-end connections1 per HTTP authority
2,0482 per unit
2,048
Unlimited

Cached response size
2 MiB
2 MiB
2 MiB

Policy document size
512 KiB
512 KiB
16 KiB

Request payload size
Unlimited
1 GiB
1 GiB

Buffered payload size
500 MiB
2 MiB
2 MiB

Request/response payload size in diagnostic logs
8,192 bytes
8,192 bytes
8,192 bytes

Request URL size3
Unlimited
16,384 bytes
16,384 bytes

Length of URL path segment
1,024 characters
1,024 characters
1,024 characters

Length of named value
4,096 characters
4,096 characters
4,096 characters

Size of request or response body in validate-content policy
100 KiB
100 KiB
100 KiB

Size of API schema used by validation policy
4 MB
4 MB
4 MB

Total request duration
Unlimited
Unlimited
30 seconds

Active WebSocket connections per unit4
5,000
5,000
N/A

1 Connections are pooled and reused unless explicitly closed by the backend.

2 Limit is 1,024 in the Developer tier.

3 Includes an up to 2048-bytes long query string.

4 Up to a maximum of 60,000 connections per service instance.

## Azure App Service limits

Resource
Free
Shared
Basic
Standard
Premium (v1-v4)
Isolated 

Apps per Azure App Service plan1
10
100
Unlimited2
Unlimited2
Unlimited2
Unlimited2

App Service environments

X

Windows code-only
X
X
X
X
X
X

Windows containers

X
X

Linux code-only and containers
X

X
X
X
X

Compute instance type
Shared
Shared
Dedicated3
Dedicated3
Dedicated3

Dedicated3

App Service plan
10 per region
10 per resource group
100 per resource group
100 per resource group
100 per resource group
100 per resource group

Compute instance type
Shared
Shared
Dedicated3
Dedicated3
Dedicated3

Dedicated3

Scale out (maximum instances)
1 shared
1 shared
3 dedicated3
10 dedicated3
20 dedicated for v1; 30 dedicated for v2, v3, and v4.3
100 dedicated4

Storage5
1 GB5
1 GB5
10 GB5
50 GB5
250 GB5
1 TB12 

 The available storage quota is 999 GB.

CPU time (5 minutes)6
3 minutes
3 minutes
Unlimited, pay at standard rates
Unlimited, pay at standard rates
Unlimited, pay at standard rates
Unlimited, pay at standard rates

CPU time (day)6
60 minutes
240 minutes
Unlimited, pay at standard rates
Unlimited, pay at standard rates
Unlimited, pay at standard rates
Unlimited, pay at standard rates

Memory (1 hour)
1,024 MB per App Service plan
1,024 MB per app
N/A
N/A
N/A
N/A

Bandwidth
165 MB
Unlimited, data transfer rates apply
Unlimited, data transfer rates apply
Unlimited, data transfer rates apply
Unlimited, data transfer rates apply
Unlimited, data transfer rates apply

Application architecture
32-bit
32-bit
32-bit/64-bit
32-bit/64-bit
32-bit/64-bit
32-bit/64-bit

WebSockets per instance (Windows)7
5
35
350
Unlimited
Unlimited
Unlimited

WebSockets per instance (Linux)7
5
N/A
~50K
~50K
~50K
~50K

Outbound IP connections per instance
600
600
Depends on instance size8
Depends on instance size8
Depends on instance size8
16,000

Concurrent debugger connections per application
1
1
1
5
5
5

App Service Certificates per subscription
Not supported
Not supported
10
10
10
10

Custom domains per app
0 (azurewebsites.net subdomain only)
500
500
500
500
500

Custom domain SSL support
Not supported, wildcard certificate for *.azurewebsites.net available by default
Not supported, wildcard certificate for *.azurewebsites.net available by default
Unlimited SNI SSL connections
Unlimited SNI SSL and 1 IP SSL connections included
Unlimited SNI SSL and 1 IP SSL connections included
Unlimited SNI SSL and 1 IP SSL connections included

Hybrid connections

5 per plan
25 per plan
220 per app
220 per app

Virtual Network Integration

X
X
X
X

Private Endpoints

100 per app
100 per app
100 per app

Integrated load balancer

X
X
X
X
X9

Access restrictions
512 rules per app
512 rules per app
512 rules per app
512 rules per app
512 rules per app
512 rules per app

Always On

X
X
X
X

Custom scheduled backups

Scheduled backups every 2 hours, a maximum of 12 backups per day (manual + scheduled
Scheduled backups every 2 hours, a maximum of 12 backups per day (manual + scheduled)
Scheduled backups every hour, a maximum of 50 backups per day (manual + scheduled)
Scheduled backups every hour, a maximum of 50 backups per day (manual + scheduled)

Autoscale

X
X
X

WebJobs10
X
X
X
X
X
X

Endpoint monitoring

X
X
X
X

Staging slots per app

5
20
20

Testing in Production

X
X
X

Diagnostic Logs
X
X
X
X
X
X

Kudu
X
X
X
X
X
X

Authentication and Authorization
X
X
X
X
X
X

App Service Managed Certificates11

X
X
X
X

SLA

99.95%
99.95%
99.95%
99.95%

1 Apps and storage quotas are per App Service plan unless noted otherwise.

2 The actual number of apps that you can host on these machines depends on the activity of the apps, the size of the machine instances, and the corresponding resource utilization.

3 Dedicated instances can be of different sizes. For more information, see App Service pricing.

4 More are allowed upon request.

5 The storage limit is the total content size across all apps in the same App service plan. The total content size of all apps across all App service plans in a single resource group and region cannot exceed 500 GB. The file system quota for App Service hosted apps is determined by the aggregate of App Service plans created in a region and resource group.

6 These resources are constrained by physical resources on the dedicated instances (the instance size and the number of instances).

7If you scale a Windows app in the Basic tier to two instances, you have 350 concurrent connections for each of the two instances. For Windows apps on Standard tier and above, there are no theoretical limits to WebSockets, but other factors can limit the number of WebSockets. For example, maximum concurrent requests allowed (defined by `maxConcurrentRequestsPerCpu`) are: 7,500 per small VM, 15,000 per medium VM (7,500 x 2 cores), and 75,000 per large VM (18,750 x 4 cores). Linux apps are limited 5 concurrent WebSocket connections on Free SKU and ~50k concurrent WebSocket connections per instance on all other SKUs.

8 The maximum IP connections are per instance and depend on the instance size: 1,920 per B1/S1/P0V3/P1V3/P0V4/P1V4 instance, 3,968 per B2/S2/P2V3/P2V4 instance, 8,064 per B3/S3/P3V3/P4V4 instance.

9 App Service Isolated SKUs can be internally load balanced (ILB) with Azure Load Balancer, so there's no public connectivity from the internet. As a result, some features of an ILB Isolated App Service must be used from machines that have direct access to the ILB network endpoint.

10 Run custom executables and/or scripts on demand, on a schedule, or continuously as a background task within your App Service instance. Always On is required for continuous WebJobs execution. There's no predefined limit on the number of WebJobs that can run in an App Service instance. There are practical limits that depend on what the application code is trying to do.

11 Only issuing standard certificates (wildcard certificates aren't available). Limited to only one free certificate per custom domain.

12 Total storage usage across all apps deployed in a single App Service environment (regardless of how they're allocated across different resource groups).

## Azure Automation limits

#### Process automation

Resource
Limit
Notes

Maximum number of active Automation accounts in a subscription in a region
10
Enterprise and CSP subscriptions can create Automation accounts in any of the publicâ¯regions supported by the service. Create a Support request to request for Quota increase. Learn more.

2
Pay-as-you-go, Sponsored, MSDN, MPN, Azure Pass subscriptions can create Automation accounts in any of theâ¯public regions supportedâ¯by the service. Create a Support request to request for Quota increase. Learn more.

1
Free trial and Azure for Student subscriptions can create only one Automation account per region per subscription. Allowed list of regions: EastUS, EastUS2, WestUS, NorthEurope, SoutheastAsia, and JapanWest2 2

Maximum number of concurrent running jobs at the same instance of time per Automation account
50
When this limit is reached, the subsequent requests to create a job fail. The client receives an error response. 
 Enterprise and CSP subscription in public regions. Create a Support request to request for Quota increase. Learn more.

10
Pay-as-you-go, Sponsored, MSDN, MPN, Azure Pass subscriptions in public regions. Create a support request to request for a Quota increase.

5
Free trial and Azure for Student Azure in open subscriptions in public regions 2.

Maximum number of new jobs that can be submitted every 30 seconds per Azure Automation account
100
When this limit is reached, the subsequent requests to create a job fail. The client receives an error response.

Maximum storage size of job metadata for a 30-day rolling period
10 GB (approximately 4 million jobs)
When this limit is reached, the subsequent requests to create a job fail.

Maximum job stream limit
1 MiB
A single stream cannot be larger than 1 MiB.

Maximum job stream limit on Azure Automation portal
200KB
Portal limit to show the job logs.

Maximum number of modules that can be imported every 30 seconds per Automation account
5

Maximum size of a module
100 MB

Maximum size of a node configuration file
1 MB
Applies to state configuration

Job run time, Free tier
500 minutes per subscription per calendar month

Maximum amount of disk space allowed per sandbox1
1 GB
Applies to Azure sandboxes only.

Maximum amount of memory given to a sandbox1
400 MB
Applies to Azure sandboxes only.

Maximum number of network sockets allowed per sandbox1
1,000
Applies to Azure sandboxes only.

Maximum runtime allowed per runbook1
3 hours
Applies to Azure sandboxes only.

Maximum number of runbooks per Automation account
800

Maximum number of system hybrid runbook workers per Automation Account
4,000

Maximum number of user hybrid runbook workers per Automation Account
4,000

Maximum number of concurrent jobs that can be run on a single Hybrid Runbook Worker
50

Maximum runbook job parameter size
512 kilobytes

Maximum runbook parameters
50
If you reach the 50-parameter limit, you can pass a JSON or XML string to a parameter and parse it with the runbook.

Maximum webhook payload size
512 kilobytes

Maximum days that job data is retained
30 days

Maximum PowerShell workflow state size
5 MB
Applies to PowerShell workflow runbooks when checkpointing workflow.

Maximum number of tags supported by an Automation account
15

Maximum number of characters in the value field of a variable
1048576

1A sandbox is a shared environment that can be used by multiple jobs. Jobs that use the same sandbox are bound by the resource limitations of the sandbox.

2Free subscriptions including Azure Free Account and Azure for Students aren't eligible for limit or quota changes. If you have a free subscription, you can upgrade to pay-as-you-go subscription.
3Limits for Government clouds: 200 concurrent running jobs at the same instance of time per Automation account, no limit on number of Automation accounts per subscription.

#### Change Tracking and Inventory

The following table shows the tracked item limits per machine for change tracking.

Resource
Limit
Notes

File
500

File size
5 MB

Registry
250

Windows software
250
Doesn't include software updates.

Linux packages
1,250

Services
250

Daemon
250

#### Azure Update Manager

The following are the Dynamic scope recommended limits for each dynamic scope:

Resource
Limit

Resource associations
1000

Number of tag filters
50

Number of Resource Group filters
50

The following are the limits for schedule patching:

Indicator
Public Cloud Limit
Mooncake/Fairfax Limit

Number of schedules per subscription per region
250
250

Total number of resource associations to a schedule
3,000
3,000

Resource associations on each dynamic scope
1,000
1,000

Number of dynamic scopes per resource group or subscription per region
250
250

Number of dynamic scopes per schedule
200
100

Total number of subscriptions attached to all dynamic scopes per schedule
200
100

## Azure App Configuration

Resource
Limit
Comment

Configuration stores for Free tier
3 stores per region per subscription.

Configuration stores for Developer tier
Unlimited stores per subscription.

Configuration stores for Standard tier
Unlimited stores per subscription.

Configuration stores for Premium tier
Unlimited stores per subscription.

Configuration store requests for Free tier
1,000 requests per day
Once the quota is exhausted, HTTP status code 429 is returned for all requests until the end of the day.

Configuration store requests for Developer tier
6,000 requests per hour
Once the quota is exhausted, requests may return HTTP status code 429 indicating Too Many Requests - until the end of the hour.

Configuration store requests for Standard tier
30,000 requests per hour
Once the quota is exhausted, requests may return HTTP status code 429 indicating Too Many Requests - until the end of the hour.

Configuration store requests for Premium tier
No quota limit on requests.

Throughput for Free tier
No guaranteed throughput.

Throughput for Developer tier
No guaranteed throughput.

Throughput for Standard tier
Allow up to 300 requests per second (RPS) for read requests and up to 60 RPS for write requests.

Throughput for Premium tier
Allow up to 450 requests per second (RPS) for read requests and up to 100 RPS for write requests.

Storage for Free tier
10 MB
There is no limit on the number of keys and labels as long as their total size is below the storage limit.

Storage for Developer tier
500 MB
There is no limit on the number of keys and labels as long as their total size is below the storage limit.

Storage for Standard tier
1 GB
There is no limit on the number of keys and labels as long as their total size is below the storage limit.

Storage for Premium tier
4 GB
There is no limit on the number of keys and labels as long as their total size is below the storage limit.

Keys and values
10 KB
For a single key-value item, including all metadata.

Length for key, label, feature flag name, tag name, and tag value
256 characters each
Applies to each field individually. For key-value based feature flags, the reserved prefix counts toward the key length limit. The default key might need to be shortened to accommodate longer key-value based feature flag names.

Snapshots storage for Free tier
10 MB
Snapshots storage is extra and in addition to "Storage for Free Tier". Storage for both archived and active snapshots is counted towards this limit.

Snapshots storage for Developer tier
500 MB
Snapshots storage is extra and in addition to "Storage for Free Tier". Storage for both archived and active snapshots is counted towards this limit.

Snapshots storage for Standard tier
1 GB
Snapshots storage is extra and in addition to "Storage for Standard Tier". Storage for both archived and active snapshots is counted towards this limit.

Snapshots storage for Premium tier
4 GB
Snapshots storage is extra and in addition to "Storage for Premium Tier". Storage for both archived and active snapshots is counted towards this limit.

Snapshot size
1 MB

## Azure Cache for Redis limits

Resource
Limit

Cache size
1.2 TB

Databases
64

Maximum connected clients
40,000

Azure Cache for Redis replicas, for high availability
3

Shards in a premium cache with clustering
10

Azure Cache for Redis limits and sizes are different for each pricing tier. To see the pricing tiers and their associated sizes, see Azure Cache for Redis pricing.

For more information on Azure Cache for Redis configuration limits, see Default Redis server configuration.

Because configuration and management of Azure Cache for Redis instances is done by Microsoft, not all Redis commands are supported in Azure Cache for Redis. For more information, see Redis commands not supported in Azure Cache for Redis.

## Azure Cloud Services limits

Resource
Limit

Web or worker roles per deployment1
25

Instance input endpoints per deployment
25

Input endpoints per deployment
25

Internal endpoints per deployment
25

Hosted service certificates per deployment
199

1Each Azure Cloud Service with web or worker roles can have two deployments, one for production and one for staging. This limit refers to the number of distinct roles, that is, configuration. This limit doesn't refer to the number of instances per role, that is, scaling.

## Azure AI Search limits

Pricing tiers determine the capacity and limits of your search service. These tiers include:

- Free: Multitenant service that's shared with other Azure subscribers and helps with evaluations and small development projects

- Basic: Provides dedicated computing resources for production workloads at a smaller scale and with up to three replicas for highly available query workloads

- Standard: Includes S1, S2, S3, and S3 High Density; is for larger production workloads; multiple levels exist within the Standard tier for you to choose a resource configuration that best matches your workload profile

Limits per subscription

You can create multiple billable search services (Basic and higher), up to the maximum number of services allowed at each tier, per region. For example, you could create up to 16 services at the Basic tier and another 16 services at the S1 tier within the same subscription and region. You could then create an additional 16 Basic services in another region for a combined total of 32 Basic services under the same subscription. For more information about tiers, see Choose a tier (or SKU) for Azure AI Search.

Maximum service limits can be raised upon request. If you need more services within the same subscription, file a support request.

Resource
Free 1
Basic
S1
S2
S3
S3 HD
L1
L2

Maximum services per region
1
16
16
8
6
6
6
6

Maximum search units (SU)2
N/A
3 SU
36 SU
36 SU
36 SU
36 SU
36 SU
36 SU

1 You can have one free search service per Azure subscription. The free tier is based on infrastructure shared with other customers. Because the hardware isn't dedicated, scale-up isn't supported, and storage is limited to 50 MB. A free search service might be deleted after extended periods of inactivity to make room for more services.

2 Search units (SU) are billing units, allocated as either a replica or a partition. You need both. To learn more about SU combinations, see Estimate and manage capacity of a search service.

Limits per search service

The following table covers SLA, partition counts, and replica counts at the service level.

Resource
Free
Basic
S1
S2
S3
S3 HD
L1
L2

Service level agreement (SLA)
No
Yes
Yes
Yes
Yes
Yes
Yes
Yes

Partitions
N/A
3 1
12
12
12
3
12
12

Replicas
N/A
3
12
12
12
12
12
12

1 Basic tier supports three partitions and three replicas, for a total of nine search units (SU) on new search services created after April 3, 2024. Older basic services are limited to one partition and three replicas.

A search service is subject to a maximum storage limit (partition size multiplied by the number of partitions) or by a hard limit on the maximum number of indexes or indexers, whichever comes first.

Service-level agreements (SLAs) apply to billable services that have two or more replicas for query workloads, or three or more replicas for query and indexing workloads. The number of partitions isn't an SLA consideration. For more information, see Reliability in Azure AI Search.

Free services don't have fixed partitions or replicas and share resources with other subscribers.

### Partition storage (GB)

Per-service storage limits vary by two things: service creation date and region. There are higher limits for newer services in most supported regions.

This table shows the progression of storage quota increases in GB over time. Starting in April 2024, higher capacity partitions were brought online in the regions listed in the footnotes. If you have an older service in a supported region, check if you can upgrade your service to the higher storage limits.

Service creation date
Basic
S1
S2
S3/HD
L1
L2

Before April 3, 2024
2
25
100
200
1,024
2,048

April 3, 2024 through May 17, 2024 1
15
160
512
1,024
1,024
2,048

After May 17, 2024 2
15
160
512
1,024
2,048
4,096

After February 10, 2025 3
15
160
512
1,024
2,048
4,096

1 Higher capacity storage for Basic, S1, S2, S3 in these regions. Americas: Brazil Southâ, Canada Centralâ, Canada Eastââ, East USâ, East US 2, âCentral USâ, North Central USâ, South Central USâ, West USâ, West US 2â, West US 3â, West Central US. Europe: France Centralâ. Italy Northââ, North Europeââ, Norway East, Poland Centralââ, Switzerland Northâ, Sweden Centralâ, UK Southâ, UK Westâ. Middle East: UAE North. Africa: South Africa North. Asia Pacific: Australia Eastâ, Australia Southeastââ, Central India, Jio India Westâ, East Asia, Southeast Asiaâ, Japan East, Japan Westâ, Korea Central, Korea Southâ.

2 Higher capacity storage for L1 and L2. More regions provide higher capacity at every billable tier. Americas: East US 2 EUAP. Europe: Germany Northâ, Germany West Central, Switzerland Westâ. Azure Government: Texas, Arizona, Virginia. Africa: South Africa Northâ. Asia Pacific: China North 3, China East 3.

3 Higher capacity storage is available in West Europe.

Important

Currently, higher storage limits aren't available in the following regions, which are subject to the pre-April 3 limits.

- Israel Central

- Qatar Central

- â Spain Central

- South India

See Service limits in Azure AI Search for more details about limits, including document size, queries per second, keys, requests, and responses.

## Foundry Tools limits

The following limits are for the number of Azure AI services resources per Azure subscription.
There is a limit of only one allowed 'Free' account, per resource type, per subscription.
Each of the Foundry Tools may have other limitations, for more information, see Foundry Tools.

Type
Limit
Example

A mixture of Azure AI services resources
Maximum of 200 total Azure AI services resources per region.
100 Azure Vision in Foundry Tools resources in West US, 50 Azure Speech in Foundry Tools resources in West US, and 50 Azure Language in Foundry Tools resources in West US.

A single type of Azure AI services resources.
Maximum of 100 resources per region
100 Vision resources in West US 2, and 100 Vision resources in East US.

## Azure Chaos Studio limits

For Chaos Studio Workspaces, see Chaos Studio Workspaces limitations. For Experiments (classic), see Service limits for Experiments (classic).

## Azure Container Apps limits

See Quotas in Azure Container Apps for Azure Container Apps limits.

The amount of disk space available to your application varies based on the associated workload profile. Available disk space determines the image size limit you can deploy to your container apps.

For dedicated workload profiles, the image size limit is per instance.

Display name
Name
Image Size Limit (GB)

Consumption
consumption
8*

Dedicated-D4
D4
90

Dedicated-D8
D8
210

Dedicated-D16
D16
460

Dedicated-D32
D32
940

Dedicated-E4
E4
90

Dedicated-E8
E8
210

Dedicated-E16
E16
460

Dedicated-E32
E32
940

Dedicated-NC24-A100 (preview)
NC24-A100
210

Dedicated-NC48-A100 (preview)
NC48-A100
460

Dedicated-NC96-A100 (preview)
NC96-A100
940

* The image size limit for a consumption workload profile is a shared among both image and app. For example, logs used by your app are subject to this size limit.

## Azure Cosmos DB limits

See Limits in Azure Cosmos DB for Azure Cosmos DB limits.

## Azure Data Explorer limits

The following table describes the maximum limits for Azure Data Explorer clusters.

Resource
Limit

Clusters per region per subscription
20

Instances per cluster
1,000

Number of databases in a cluster
10,000

Number of follower clusters (data share consumers) per leader cluster (data share producer)
100

Recommended maximum extents per cluster
10,000,000

Note

You can request higher limits for Number of databases in a cluster and Clusters per region per subscription. To request an increase, contact Azure Support.

The following table describes the limits on management operations performed on Azure Data Explorer clusters.

Scope
Operation
Limit

Cluster
read (for example, get a cluster)
500 per 5 minutes

Cluster
write (for example, create a database)
1,000 per hour

## Azure Database for MySQL flexible server

See Limitations in Azure Database for MySQL - Flexible Server for Azure Database for MySQL - Flexible Server limits.

## Azure Database for PostgreSQL flexible server

See Limits in Azure Database for PostgreSQL flexible server for Azure Database for PostgreSQL flexible server limits.

## Azure Deployment Environments limits

Subscription
Runtime limit per deploymentâ
Runtime limit per month per region per subscriptionâ
Storage limit per Environmentâ

Enterprise
30 min
5000 min
1 GB

Pay as you go
10 min
200 min
1 GB

Azure Pass
10 min
200 min
1 GB

MSDN
10 min
200 min
1 GB

CSP
10 min
200 min
1 GB

Free trial
10 min
200 min
1 GB

Azure for students
10 min
200 min
1 GB

## Azure Files and Azure File Sync

See Scalability and performance targets for Azure Files and Azure File Sync to learn more about the limits for Azure Files and Azure File Sync.

## Azure Functions limits

Resource
Flex Consumption plan
Premium plan
Dedicated plan/ASE
Container Apps
Consumption plan

Default timeout duration (min)
30
30
30
3016
5

Max timeout duration (min)
unbounded9
unbounded9
unbounded2
unbounded17
10

Max outbound connections (per instance)
unbounded
unbounded
see App Service limits
unbounded
600 active (1200 total)

Max request size (MB)3
210
210
210
210
210

Max query string length3
4096
4096
4096
4096
4096

Max request URL length3
8192
8192
8192
8192
8192

ACU per instance
210-840
100-840/210-25010
varies
100
varies

Max memory (GB per instance)
414
3.5-14
1.75-256/8-256
varies
1.5

Max instance count (Windows | Linux)15
n/a | 1000
20-100
10-30 (100 ASE)11
300-10001
200 | 100

Function apps per plan13
1
100
unbounded4
unbounded4
100

App Service plans
n/a
100 per resource group
100 per resource group
n/a
100 per region

Deployment slots per app12
n/a
3
1-2011
not supported
2

Storage (temporary)5
0.8 GB
11-61 GB
11-140 GB
n/a
0.5 GB

Storage (persisted)
0 GB7
250 GB
10-1000 GB11
n/a
1 GB6,7

Custom domains per app
258
500
500
not supported
5008

Custom domain TSL/SSL support
unbounded SNI SSL and one IP SSL connection included
unbounded SNI SSL and one IP SSL connection included
unbounded SNI SSL and one IP SSL connection included
not supported
unbounded SNI SSL connection included

Notes on service limits:

- On Container Apps, you can set the maximum number of replicas, which the platform honors as long as there's enough cores quota available.

- Requires the App Service plan be set to Always On. Pay at standard rates. A grace period of 10 minutes is given for HTTP triggered functions during platform updates but not for other triggers.

- These limits are set in the host.

- The actual number of function apps that you can host depends on the activity of the apps, the size of the machine instances, and the corresponding resource utilization.

- The storage limit is the total content size in temporary storage across all apps in the same App Service plan. For Consumption plans on Linux, the storage is currently 1.5 GB.

- Consumption plan uses an Azure Files share for persisted storage. When you provide your own Azure Files share, the specific share size limits depend on the storage account you set for WEBSITE_CONTENTAZUREFILECONNECTIONSTRING.

- On Linux, you must explicitly mount your own Azure Files share.

- When your function app is hosted in a Consumption plan, only the CNAME option is supported. For function apps in a Premium plan or an App Service plan, you can map a custom domain using either a CNAME or an A record.

- There's no maximum execution timeout duration enforced. However, the grace period given to a function execution is 60 minutes during scale in and 10 minutes during platform updates.

- Workers are roles that host customer apps. Workers are available in three fixed sizes: One vCPU/3.5 GB RAM; Two vCPU/7 GB RAM; Four vCPU/14 GB RAM.

- See App Service limits for details.

- Including the production slot.

- There's currently a limit of 5,000 function apps in a given subscription.

- Flex Consumption plan instance sizes are currently defined as 512 MB, 2,048 MB, or 4,096 MB. For more information, see Instance memory.

- For details, see Scale in the Hosting comparison article.

- When the minimum number of replicas is set to zero, the default timeout depends on the specific triggers used in the app.

- When the minimum number of replicas is set to one or more.

See Azure Functions hosting options for more information.

## Azure Health Data Services

### Azure Health Data Services limits

Health Data Services is a set of managed API services based on open standards and frameworks. Health Data Services enables workflows to improve healthcare and offers scalable and secure healthcare solutions. Health Data Services includes Fast Healthcare Interoperability Resources (FHIR) service, the Digital Imaging and Communications in Medicine (DICOM) service, and MedTech service.

FHIR service is an implementation of the FHIR specification within Health Data Services. It enables you to combine in a single workspace one or more FHIR service instances with optional DICOM and MedTech service instances. Azure API for FHIR is generally available as a stand-alone service offering.

Each FHIR service instance in Azure Health Data Services has a storage limit of 4 TB by default. If you have more data, you can ask Microsoft to increase storage up to 100 TB for your FHIR service. To request storage greater than 4 TB, create a support request on the Azure portal and use the issue type Service and Subscription limit (quotas).

Quota Name
Default Limit
Maximum Limit
Notes

Workspace
10
Contact support
Limit per subscription

FHIR service
10
Contact support
Limit per workspace

DICOM service
10
Contact support
Limit per workspace

The per-subscription and per-workspace limits are enforced independently. To deploy more than 10 FHIR services in a subscription, distribute them across multiple workspaces.

### Azure API for FHIR service limits

Azure API for FHIR is a managed, standards-based, compliant API for clinical health data that enables solutions for actionable analytics and machine learning.

Quota Name
Default Limit
Maximum Limit
Notes

Request Units (RUs)
100,000 RUs
Contact support Maximum available is 1,000,000.
You need a minimum of 400 RUs or 40 RUs/GB, whichever is larger.

Concurrent connections
15 concurrent connections on two instances (for a total of 30 concurrent requests)
Contact support

Azure API for FHIR Service Instances per Subscription
10
Contact support

## Azure Kubernetes Service limits

Resource
Limit

Maximum number of clusters per subscription globally
5,000

Maximum nodes per cluster with Virtual Machine Scale Sets and Standard Load Balancer SKU
5,000 across all node pools 
Note: If you're unable to scale up to 5,000 nodes per cluster, see Best Practices for Large Clusters.

Maximum nodes per node pool (Virtual Machine Scale Sets node pools)
1000

Maximum node pools per cluster
100

Maximum pods per node: with Kubenet networking plug-in
Maximum: 250 
 Azure CLI default: 110 
 Azure Resource Manager template default: 110 
 Azure portal deployment default: 30

Maximum pods per node: with Azure Container Networking Interface (Azure CNI)1
Maximum: 250 
 Maximum recommended for Windows Server containers: 110 
 Default: 30

Open Service Mesh (OSM) AKS addon
Kubernetes Cluster Version: AKS Supported Versions
OSM controllers per cluster: 1
Pods per OSM controller: 1600
Kubernetes service accounts managed by OSM: 160

Maximum load-balanced kubernetes services per cluster with Standard Load Balancer SKU
300

Maximum nodes per cluster with Virtual Machine Availability Sets and Basic Load Balancer SKU
100

1 Windows Server containers must use Azure CNI networking plug-in. Kubenet isn't supported for Windows Server containers.

Kubernetes Control Plane tier
Limit

Standard tier
Automatically scales Kubernetes API server based on load. Larger control plane component limits and API server/etcd instances.

Free tier
Limited resources with inflight requests limit. Recommended node limit of 10 nodes per cluster. Best for experimenting, learning, and simple testing. Not advised for production/critical workloads.

Subscription Type
Default number of AKS clusters per subscription per region for new subscriptions1
Maximum number of AKS clusters per subscription per region via self service using Azure portal Quotas page2

Enterprise Agreement subscriptions
100
1,000

CSP, Pay-as-you-go, Sponsored, MSDN, MPN, Azure Pass, Azure In Open, and Azure Pass subscriptions
10
100

Free Trial and Azure for Students subscriptions
3
3

1 The default number of AKS clusters per subscription per region for new subscriptions may vary in regions with capacity constraints.

2 To request an increase of the quota limit, use the Azure portal Quotas request process. Quota increase requests above the maximum self service amount will require a support ticket. Free Trial and Azure for Students subscriptions aren't eligible for limit or quota increases. If you have a Free Trial or Azure for Students subscription, you can upgrade to a pay-as-you-go subscription to get higher quota limits.

## Azure Lab Services

The following limits are for the number of Azure Lab Services resources.

#### Per resource type

Grouping
Resource type
Limit

Per subscription
Labs
980

Per resource group
Labs
800

Lab plans
800

Per lab
Schedules
250

Virtual machines (VMs)
400

#### Per region - Lab plans and labs

Subscription type
Lab plan limits
Lab limits

Default
2
2

Pay As You Go
500
500

MPN
500
500

Azure In Open
500
500

Enterprise Agreement
500
500

MSDN
500
500

Sponsored
100
15

CSP
500
500

Azure Pass
100
25

Free Trial
100
15

Azure for Students
100
15

For more information about Azure Lab Services capacity limits, see Capacity limits in Azure Lab Services.

Contact support to request an increase your limit. 

## Azure Load Testing limits

For Azure Load Testing limits, see Service limits in Azure Load Testing.

## Azure Machine Learning limits

See Manage and increase quotas and limits for resources with Azure Machine Learning for the latest values for Azure Machine Learning Compute quotas.

## Azure Maps limits

Note

Azure Maps Gen1 Price Tier Retirement

Gen1 pricing tier is now deprecated and will be retired on September 15, 2026. Gen2 pricing tier replaces Gen1 (both S0 and S1) pricing tier. If your Azure Maps account has Gen1 pricing tier selected, you can switch to Gen2 pricing before Gen1 is retired, otherwise it will automatically be updated. For more information, see Manage the pricing tier of your Azure Maps account.

For Azure Maps queries per second (QPS) limits, see Azure Maps QPS rate limits

The following table shows the cumulative data size limit for Azure Maps accounts in an Azure subscription. The Azure Maps Data service is available only at the Gen1 (S1) and Gen2 pricing tier.

Resource
Limit

Maximum storage per Azure subscription
1 GB

Maximum size per file upload
100 MB

Note

Azure Maps Data Registry service Retirement

The Azure Maps Data Registry service is now deprecated and is retired as of September 30, 2025. For more information, see How to create data registry.

## Azure Managed Grafana limits

Note

The Essential tier is deprecated. Existing Essential instances continue to run during the transition period, but you can't create new Essential instances. The Essential tier is scheduled to retire on March 31, 2027.

Limit
Description
Essential (deprecated; existing instances only)
Standard X1
Standard X2

Alert rules
Maximum number of alert rules that you can create.
Not supported
500 per instance
1000 per instance

Memory for Grafana instance
Amount of memory for Grafana in your dedicated instance.
Basic
Standard
Expanded

Dashboards
Maximum number of dashboards that you can create.
20 per instance
Unlimited
Unlimited

Data sources
Maximum number of data sources that you can create.
5 per instance
Unlimited
Unlimited

Git Sync repositories
Maximum number of GitHub repositories that you can connect with Git Sync.
10 per instance
10 per instance
10 per instance

Git Sync resources per repository
Maximum number of resources per repository that you can synchronize with Git Sync.
1,000 per repository
1,000 per repository
1,000 per repository

API keys
Maximum number of API keys that you can create.
2 per instance
100 per instance
100 per instance

Data query timeout
Maximum wait duration for the reception of data query response headers, before Grafana times out.
200 seconds
200 seconds
200 seconds

Data source query size
Maximum number of bytes that are read or accepted from responses of outgoing HTTP requests.
80 MB
80 MB
80 MB

Render image or PDF report wait time
Maximum duration for an image or report PDF rendering request to complete before Grafana times out.
Not supported
220 seconds
220 seconds

Instance count
Maximum number of instances in a single subscription per Azure region.
1
50
50

Requests per IP
Maximum number of requests per IP per second.
90 requests per second
90 requests per second
90 requests per second

Requests per HTTP host
Maximum number of requests per HTTP host per second. The HTTP host stands for the Host header in incoming HTTP requests, which can describe each unique host client.
45 requests per second
45 requests per second
45 requests per second

## Azure Monitor limits

For Azure Monitor limits, see Azure Monitor service limits.

## Azure Data Factory limits

Azure Data Factory is a multitenant service that has the following default limits in place to make sure customer subscriptions are protected from each other's workloads. To raise the limits up to the maximum for your subscription, contact support.

Resource
Default limit
Maximum limit

Total number of entities, such as pipelines, data sets, triggers, linked services, Private Endpoints, and integration runtimes, within a data factory
5,000
5,000

Total CPU cores for Azure-SSIS Integration Runtimes under one subscription
64
Find out how to request a quota increase from support.

Concurrent pipeline runs per data factory shared among all pipelines in the factory
10,000
10,000

Concurrent External activity runs per subscription per Azure Integration Runtime region
External activities are managed on integration runtime but execute on linked services, including Databricks, stored procedure, Web, and others. This limit doesn't apply to Self-hosted IR.
3,000
3,000

Concurrent Pipeline activity runs per subscription per Azure Integration Runtime region 
Pipeline activities execute on integration runtime, including Lookup, GetMetadata, and Delete. This limit doesn't apply to Self-hosted IR.
1,000
1,000

Concurrent authoring operations per subscription per Azure Integration Runtime region
Including test connection, browse folder list and table list, preview data. This limit doesn't apply to Self-hosted IR.
200
200

Concurrent Data Integration Units1 consumption per subscription per Azure Integration Runtime region
Region group 12: 6,000
Region group 22: 3,000
Region group 32: 1,500
Region group 12: 6,000
Region group 22: 3,000
Region group 32: 1,500

Concurrent Data Integration Units1 consumption per subscription per Azure Integration Runtime region in managed virtual network
2,400
2,400

Maximum activities per pipeline, which includes inner activities for containers
120
120

Maximum number of linked integration runtimes that can be created against a single self-hosted integration runtime
100
100

Maximum number of nodes that can be created against a single self-hosted integration runtime
4
4

Maximum parameters per pipeline
50
50

ForEach items
100,000
100,000

ForEach parallelism
20
50

Maximum queued runs per pipeline
100
100

Characters per expression
8,192
8,192

Minimum tumbling window trigger interval
5 min
15 min

Minimum timeout for pipeline activity runs
10 min
10 min

Maximum timeout for pipeline activity runs
7 days
7 days

Bytes per object for pipeline objects3
200 KB
200 KB

Bytes per object for dataset and linked service objects3
100 KB
2,000 KB

Bytes per payload for each activity run4
896 KB
896 KB

Data Integration Units1 per copy activity run
256
256

Write API calls
1,200/h
1,200/h

 This limit is imposed by Azure Resource Manager, not Azure Data Factory.

Read API calls
12,500/h
12,500/h

 This limit is imposed by Azure Resource Manager, not Azure Data Factory.

Monitoring queries per minute
1,000
1,000

Maximum time of data flow debug session
8 hrs
8 hrs

Concurrent number of data flows per integration runtime
50
50

Concurrent number of data flows per integration runtime in managed vNet
50
50

Concurrent number of data flow debug sessions per user per factory
3
3

Data Flow Azure IR TTL (time to live) limit
4 hrs
4 hrs

Meta Data Entity Size limit in a factory
2 GB
2 GB

1 The data integration unit (DIU) is used in a cloud-to-cloud copy operation. Learn more from Data integration units (version 2). For information on billing, see Azure Data Factory pricing.

2 Azure Integration Runtime is globally available to ensure data compliance, efficiency, and reduced network egress costs.

Region group
Regions

Region group 1
Central US, East US, East US 2, North Europe, West Europe, West US, West US 2

Region group 2
Australia East, Australia Southeast, Brazil South, Central India, Japan East, North Central US, South Central US, Southeast Asia, West Central US

Region group 3
Other regions

If managed virtual network is enabled, the data integration unit (DIU) in all region groups are 2,400.

3 Pipeline, data set, and linked service objects represent a logical grouping of your workload. Limits for these objects don't relate to the amount of data you can move and process with Azure Data Factory. Data Factory is designed to scale to handle petabytes of data.

4 The payload for each activity run includes the activity configuration, one or more associated datasets, and linked service configurations if any, and a small portion of system properties generated per activity type. Limit for this payload size doesn't relate to the amount of data you can move and process with Azure Data Factory. Learn about the symptoms and recommendation if you hit this limit.

#### Web service call limits

Azure Resource Manager has limits for API calls. You can make API calls at a rate within the Azure Resource Manager API limits.

## Azure NetApp Files

Azure NetApp Files has a regional limit for capacity. The standard capacity limit for each subscription is 25 TiB, per region, across all service levels. To increase the capacity, use the Service and subscription limits (quotas) support request.

To learn more about the limits for Azure NetApp Files, see Resource limits for Azure NetApp Files.

## Azure Policy limits

There's a maximum count for each object type for Azure Policy. For definitions, an entry of Scope means the management group or subscription. For assignments and exemptions, an entry of Scope means the management group, subscription, resource group, or individual resource.

Where
What
Maximum count

Scope
Policy definitions
500

Scope
Initiative definitions
200

Tenant
Initiative definitions
2,500

Scope
Policy or initiative assignments
200

Scope
Exemptions
1000

Policy definition
Parameters
20

Initiative definition
Policies
1000

Initiative definition
Parameters
400

Policy or initiative assignments
Exclusions (notScopes)
400

Policy rule
Nested conditionals
512

Remediation task
Resources
50,000

Policy definition, initiative, or assignment request body
Bytes
1,048,576

Policy rules have more limits to the number of conditions and their complexity. For more information, see Policy rule limits.

## Azure Quantum limits

### Provider Limits & Quota

The Azure Quantum Service supports both first and third-party service providers.
Third-party providers own their limits and quotas. Users can view offers and limits in the Azure portal when configuring third-party providers.

You can find the published quota limits for Microsoft's first party Optimization Solutions provider below.

#### Learn & Develop SKU

Resource
Limit

CPU-based concurrent jobs
up to 51 concurrent jobs

FPGA-based concurrent jobs
up to 21 concurrent jobs

CPU-based solver hours
20 hours per month

FPGA-based solver hours
1 hour per month

While on the Learn & Develop SKU, you cannot request an increase on your quota limits. Instead you should switch to the Performance at Scale SKU.

#### Performance at Scale SKU

Resource
Default Limit
Maximum Limit

CPU-based concurrent jobs
up to 1001 concurrent jobs
same as default limit

FPGA-based concurrent jobs
up to 101 concurrent jobs
same as default limit

Solver hours
1,000 hours per month
up to 50,000 hours per month

Reach out to Azure Support to request a limit increase.

For more information, please review the Azure Quantum pricing page.
Review the relevant provider pricing pages in the Azure portal for details on third-party offerings.

1 Describes the number of jobs that can be queued at the same time.

## Azure RBAC limits

The following limits apply to Azure role-based access control (Azure RBAC).

Area
Resource
Limit

Azure role assignments

Number of Azure role assignments per Azure subscription
5,000

Number of Azure role assignments per management group
500

Size of description for Azure role assignments
Recommended maximum: 512 chars
Maximum: 2,048 chars

Size of condition for Azure role assignments
8 KB

Azure custom roles

Number of Azure custom roles per tenant
5,000

Number of Azure custom roles per tenant
(for Microsoft Azure operated by 21Vianet)
2,000

Size of role name for Azure custom roles
Recommended maximum: 256 chars
Maximum: 512 chars

Size of description for Azure custom roles
Recommended maximum: 512 chars
Maximum: 2,048 chars

Size of an Azure custom role definition
1 MB

Number of assignable scopes for Azure custom roles
2,000

Number of management group assignable scopes for Azure custom roles
1

Azure deny assignments

Number of system-managed deny assignments per Azure subscription
2,000

## Azure SignalR Service limits

Resource
Default limit
Maximum limit

Azure SignalR Service units per instance for Free tier
1
1

Azure SignalR Service units per instance for Standard/Premium_P1 tier
100
100

Azure SignalR Service units per instance for Premium_P2 tier
100 - 1,000
100 - 1,000

Azure SignalR Service units per subscription per region for Free tier
5
5

Total Azure SignalR Service unit counts per subscription per region
150
Unlimited

Concurrent connections per unit for Free tier
20
20

Concurrent connections per unit for Standard/Premium tier
1,000
1,000

Included messages per unit per day for Free tier
20,000
20,000

Additional messages per unit per day for Free tier
0
0

Included messages per unit per day for Standard/Premium tier
1,000,000
1,000,000

Additional messages per unit per day for Standard/Premium tier
Unlimited
Unlimited

To request an update to your subscription's default limits, open a support ticket.

For more information about how connections and messages are counted, see Messages and connections in Azure SignalR Service.

If your requirements exceed the limits, switch from Free tier to Standard tier and add units. For more information, see How to scale an Azure SignalR Service instance?

If your requirements exceed the limits of a single instance, add instances. For more information, see How to enable Geo-Replication in Azure SignalR Service.

## Azure Spring Apps limits

See Quotas and service plans for Azure Spring Apps to learn more about the limits for Azure Spring Apps.

## Azure Storage limits

This section lists the following limits for Azure Storage:

- Standard storage account limits

- Azure Storage resource provider limits

- Azure Blob Storage limits

- Azure Queue storage limits

- Azure Table storage limits

### Standard storage account limits

The following table describes default limits for Azure general-purpose v2 (GPv2), general-purpose v1 (GPv1), and Blob Storage accounts.

A few entries in the table also apply to disk access and are explicitly labeled. Disk access is a resource that is exclusively used for importing or exporting managed disks through private links.

Customers should use a GPv2 storage account, because GPv1 is being retired. You can easily upgrade a GPv1 or Blob Storage account to a GPv2 account with no downtime and no need to copy data. For more information, see Upgrade to a GPv2 storage account.

The ingress limit refers to all data sent to a storage account or disk access. The egress limit refers to all data received from a storage account or disk access.

Note

You can request higher capacity and ingress limits. To request an increase, contact Azure Support.

Resource
Limit

Maximum number of storage accounts with standard endpoints per region per subscription, including standard and premium storage accounts.
250 by default, 1000 by request1

Maximum number of storage accounts with Azure DNS zone endpoints (preview) per region per subscription, including standard and premium storage accounts.
5,000 (preview)

Default maximum storage account capacity.
5 PiB 2

Maximum number of blob containers, blobs, directories, and subdirectories (if hierarchical namespace is enabled), file shares, tables, queues, entities, or messages per storage account.
No limit

Default maximum request rate per general-purpose v2, Blob Storage account, and disk access resources in the following regions:

- Americas: Brazil South, Canada Central, Central US, East US, East US 2, North Central US, South Central US, West US, West US 2, West US 3

- Asia Pacific: Australia East, Central India, China East 2, China North 3, East Asia, Japan East, Jio India West, Korea Central, Southeast Asia

- Europe: France Central, Germany West Central, North Europe, Norway East, Sweden Central, UK South, West Europe

- Africa: South Africa North

- Azure Government: USGov Arizona, USGov Virginia

40,000 requests per second2

Default maximum request rate per general-purpose v2, Blob Storage account, and disk access resources in regions that aren't listed in the previous row.
20,000 requests per second2

Default maximum ingress per general-purpose v2, Blob Storage account, and disk access resources in the following regions:

- Americas: Brazil South, Canada Central, Central US, East US, East US 2, North Central US, South Central US, West US, West US 2, West US 3

- Asia Pacific: Australia East, Central India, China East 2, China North 3, East Asia, Japan East, Jio India West, Korea Central, Southeast Asia

- Europe: France Central, Germany West Central, North Europe, Norway East, Sweden Central, UK South, West Europe

- Africa: South Africa North

- Azure Government: USGov Arizona, USGov Virginia

60 Gbps2

Default maximum ingress per general-purpose v2, Blob Storage account, and disk access resources in regions that aren't listed in the previous row.
25 Gbps2

Default maximum ingress for general-purpose v1 storage accounts (all regions).
10 Gbps2

Default maximum egress for general-purpose v2, Blob Storage accounts, and disk access resources in the following regions:

- Americas: Brazil South, Canada Central, Central US, East US, East US 2, North Central US, South Central US, West US, West US 2, West US 3

- Asia Pacific: Australia East, Central India, China East 2, China North 3, East Asia, Japan East, Jio India West, Korea Central, Southeast Asia

- Europe: France Central, Germany West Central, North Europe, Norway East, Sweden Central, UK South, West Europe

- Africa: South Africa North

- Azure Government: USGov Arizona, USGov Virginia

200 Gbps2

Default maximum egress for general-purpose v2, Blob Storage accounts, and disk access resources in regions that aren't listed in the previous row.
50 Gbps2

Maximum egress for general-purpose v1 storage accounts (US regions).
20 Gbps if RA-GRS/GRS is enabled, 30 Gbps for LRS/ZRS

Maximum egress for general-purpose v1 storage accounts (non-US regions).
10 Gbps if RA-GRS/GRS is enabled, 15 Gbps for LRS/ZRS

Maximum number of IP address rules per storage account.
400

Maximum number of virtual network rules per storage account.
400

Maximum number of resource instance rules per storage account.
200

Maximum number of private endpoints per storage account.
200

1 With a quota increase, you can create up to 1000 storage accounts with standard endpoints per region. For more information, see Increase Azure Storage account quotas.

2 Azure Storage standard accounts support higher capacity limits and higher limits for ingress and egress by request. To request an increase in account limits, contact Azure Support.

### Azure Storage resource provider limits

The following limits apply only when you perform management operations by using Azure Resource Manager with Azure Storage and the Storage Resource Provider. The limits apply per subscription per region of the resource in the request.

Resource
Limit

Storage account management operations (read)
800 per 5 minutes

Storage account management operations (write)
10 per second / 1200 per hour

Storage account management operations (list)
100 per 5 minutes

### Azure Blob Storage limits

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

### Azure Queue storage limits

Resource
Target

Maximum size of a single queue
500 TiB

Maximum size of a message in a queue
64 KiB

Maximum number of stored access policies per queue
5

Maximum request rate per storage account
20,000 messages per second, which assumes a 1-KiB message size

Target throughput for a single queue (1-KiB messages)
Up to 2,000 messages per second

### Azure Table storage limits

The following table describes capacity, scalability, and performance targets for Table storage.

Resource
Target

Number of tables in an Azure storage account
Limited only by the capacity of the storage account

Number of partitions in a table
Limited only by the capacity of the storage account

Number of entities in a partition
Limited only by the capacity of the storage account

Maximum size of a single table
500 TiB

Maximum size of a single entity, including all property values
1 MiB

Maximum number of properties in a table entity
255 (including the three system properties, PartitionKey, RowKey, and Timestamp)

Maximum total size of an individual property in an entity
Varies by property type. For more information, see Property Types in Understanding the Table Service Data Model.

Size of the PartitionKey
A string up to 1024 characters in size

Size of the RowKey
A string up to 1024 characters in size

Size of an entity group transaction
A transaction can include at most 100 entities and the payload must be less than 4 MiB in size. An entity group transaction can include an update to an entity only once.

Maximum number of stored access policies per table
5

Maximum request rate per storage account
20,000 transactions per second, which assumes a 1-KiB entity size

Target throughput for a single table partition (1 KiB-entities)
Up to 2,000 entities per second

## Azure subscription creation limits

See Billing accounts and scopes in the Azure portal to learn more about creating limits for Azure subscriptions.

## Azure Virtual Desktop Service limits

The following table describes the maximum limits for Azure Virtual Desktop.

Azure Virtual Desktop Object
Per Parent Container Object
Service Limit

Workspace
Microsoft Entra tenant
1300

HostPool
Workspace
400

Application group
Microsoft Entra tenant
10001

RemoteApp
Application group
500

Role Assignment
Any Azure Virtual Desktop Object
200

Session Host
HostPool
10,000

1If you require over 1000 Application groups then please raise a support ticket via the Azure portal.

All other Azure resources used in Azure Virtual Desktop such as Virtual Machines, Storage, Networking etc. are all subject to their own resource limitations documented in the relevant sections of this article.
To visualise the relationship between all the Azure Virtual Desktop objects, review this article Relationships between Azure Virtual Desktop logical components.

To get started with Azure Virtual Desktop, use the getting started guide.
For deeper architectural content for Azure Virtual Desktop, use the Azure Virtual Desktop section of the Cloud Adoption Framework.
For pricing information for Azure Virtual Desktop, add "Azure Virtual Desktop" within the Compute section of the Azure Pricing Calculator.

## Azure VMware Solution limits

The following table describes the maximum limits for Azure VMware Solution.

Resource
Limit

vSphere clusters per private cloud
12

Minimum number of ESXi hosts per cluster
3 (hard limit)

Maximum number of ESXi hosts per cluster
16 (hard limit)

Maximum number of ESXi hosts per private cloud
96

Maximum number of vCenter Servers per private cloud
1 (hard limit)

Maximum number of HCX site pairings
25 (any edition)

Maximum number of HCX service meshes
10 (any edition)

Maximum number of Azure VMware Solution private clouds linked Azure ExpressRoute from a single location to a single virtual network gateway
4
The virtual network gateway used determines the actual maximum number of linked private clouds. For more information, see About ExpressRoute virtual network gateways.
If you exceed this threshold, use Azure VMware Solution interconnect to aggregate private cloud connectivity within the Azure region.

Maximum Azure VMware Solution ExpressRoute throughput
10 Gbps (use Ultra Performance Gateway version with FastPath enabled)**
The virtual network gateway that's used determines the actual bandwidth. For more information, see About ExpressRoute virtual network gateways.
An Azure VMware Solution ExpressRoute doesn't have any port speed limitations and performs above 10 Gbps. Rates over 10 Gbps aren't guaranteed because of quality of service.

Maximum number of Azure Public IPv4 addresses assigned to NSX
2,000

Maximum number of Azure VMware Solution interconnects per private cloud
10

Maximum number of Azure ExpressRoute Global Reach connections per Azure VMware Solution private cloud
8

vSAN capacity limits
75% of total usable (keep 25% available for service-level agreement)

VMware Site Recovery Manager: Maximum number of protected virtual machines
3,000

VMware Site Recovery Manager: Maximum number of virtual machines per recovery plan
2,000

VMware Site Recovery Manager: Maximum number of protection groups per recovery plan
250

VMware Site Recovery Manager: Recovery point objective (RPO) values
Five minutes or higher* (hard limit)

VMware Site Recovery Manager: Maximum number of virtual machines per protection group
500

VMware Site Recovery Manager: Maximum number of recovery plans
250

* For information about an RPO lower than 15 minutes, see How the 5-minute RPO works in the vSphere Replication Administration documentation.

** This soft recommended limit can support higher throughput based on the scenario.

For other VMware-specific limits, use the VMware by Broadcom configuration maximum tool.

## Azure Web PubSub limits

Resource
Default limit
Maximum limit

Azure Web PubSub Service units per instance for Free tier
1
1

Azure Web PubSub Service units per instance for Standard/Premium_P1 tier
100
100

Azure Web PubSub Service units per instance for Premium_P2 tier
100 - 1,000
100 - 1,000

Azure Web PubSub Service units per subscription per region for Free tier
5
5

Total Azure Web PubSub Service unit counts per subscription per region
150
Unlimited

Concurrent connections per unit for Free tier
20
20

Concurrent connections per unit for Standard/Premium tier
1,000
1,000

Included messages per unit per day for Free tier
20,000
20,000

Additional messages per unit per day for Free tier
0
0

Included messages per unit per day for Standard/Premium tier
1,000,000
1,000,000

Additional messages per unit per day for Standard/Premium tier
Unlimited
Unlimited

To request an update to your subscription's default limits, open a support ticket.

For more information about how connections and messages are counted in billing, see Billing model in Azure Web PubSub Service.

If your requirements exceed the limits, scale up from Free tier to Standard/Premium tier or scale out units. For more information, see How to scale an Azure Web PubSub Service instance.

If your requirements exceed the limits of a single instance, add instances. For more information, see How to use Geo-Replication in Azure Web PubSub.

## Backup limits

For a summary of Azure Backup support settings and limitations, see Azure Backup Support Matrices.

## Batch limits

Resource
Default limit
Maximum limit

Azure Batch accounts per region per subscription
1-3
50

Dedicated cores per Batch account
0-9001
Contact support

Low-priority cores per Batch account
0-1001
Contact support

Active jobs and job schedules per Batch account (completed jobs have no limit)
100-300
1,0002

Pools per Batch account
0-1001
5002

Private endpoint connections per Batch account
100
100

1 For capacity management purposes, the default quotas for new Batch accounts in some regions and for some subscription
types have been reduced from the above range of values. In some cases, these limits have been reduced to zero. When you create a
new Batch account, check your quotas and
request an appropriate core or service quota increase, if necessary.
Alternatively, consider reusing Batch accounts that already have sufficient quota or user subscription pool allocation
Batch accounts to maintain core and VM family quota across all Batch accounts on the subscription. Service quotas like
active jobs or pools apply to each distinct Batch account even for user subscription pool allocation Batch accounts.

2 To request an increase beyond this limit, contact Azure Support.

Note

Default limits vary depending on the type of subscription you use to create a Batch account. Cores quotas shown are for Batch
accounts in Batch service mode. View the quotas in your Batch account.

## Classic deployment model limits

The following limits apply if you use a classic deployment model instead of the Azure Resource Manager deployment model.

Resource
Default limit
Maximum limit

vCPUs per subscription1
20
10,000

Coadministrators per subscription
200
200

Storage accounts per subscription2
100
100

Cloud services per subscription
20
200

Local networks per subscription
10
500

DNS servers per subscription
9
100

Reserved IPs per subscription
20
100

Affinity groups per subscription
256
256

Subscription name length (characters)
64
64

1Extra small instances count as one vCPU toward the vCPU limit despite using a partial CPU core.

2The storage account limit includes both Standard and Premium storage accounts.

## Container Instances limits

Resource
Actual Limit

Standard sku container groups per region per subscription
100

Dedicated sku container groups per region per subscription
01

Number of containers per container group
60

Number of volumes per container group
20

Standard sku cores (CPUs) per region per subscription
100

Standard sku cores (CPUs) for K80 GPU per region per subscription
0

Standard sku cores (CPUs) for V100 GPU per region per subscription
0

Ports per IP
5

Container instance log size - running instance
4 MB

Container instance log size - stopped instance
16 KB or 1,000 lines

Container group creates per hour
3001

Container group creates per 5 minutes
1001

Container group deletes per hour
3001

Container group deletes per 5 minutes
1001

1To request a limit increase, create an Azure Support request. Free subscriptions including Azure Free Account and Azure for Students aren't eligible for limit or quota increases. If you have a free subscription, you can upgrade to a Pay-As-You-Go subscription.

2Default limit for Pay-As-You-Go subscription. Limit may differ for other category types.

## Azure Container Registry limits

The following table details the features and limits of the Basic, Standard, and Premium Azure Container Registry service tiers.

Resource
Basic
Standard
Premium

Included storage1 (GiB)
10
100
500

Storage limit (TiB)
40
40
100

Maximum image layer size (GiB)
195
195
195

Maximum manifest size (MiB)
4
4
4

Webhooks
2
10
500

Private link with private endpoints
N/A
N/A
Supported

â¢ Private endpoints
N/A
N/A
200

Public IP network rules
N/A
N/A
200

Service endpoint VNet access
N/A
N/A
Preview

â¢ Virtual network rules
N/A
N/A
100

Repository-scoped permissions with Microsoft Entra role assignments
Supported
Supported
Supported

Repository-scoped permissions with non-Microsoft Entra tokens and scope maps
Supported
Supported
Supported

â¢ Non-Microsoft Entra tokens
100
500
50,000

â¢ Non-Microsoft Entra token scope maps
100
500
50,000

â¢ Actions per non-Microsoft Entra token scope map
500
500
500

â¢ Repositories per non-Microsoft Entra token scope map2
500
500
500

Anonymous pull access
N/A
Supported
Supported

Geo-replication
N/A
N/A
Supported

Dedicated data endpoints
N/A
N/A
Supported

Availability zones
Supported
Supported
Supported

Content trust
N/A
N/A
Supported

Customer-managed keys
N/A
N/A
Supported

Connected registries
N/A
N/A
Supported

Artifact streaming
N/A
N/A
Supported

Artifact cache rules
N/A
Supported
Supported

IP access rule configuration
N/A
N/A
Supported

Retention policy for untagged manifests
N/A
N/A
Supported

Artifact transfer
N/A
N/A
Supported

Export policy
N/A
N/A
Supported

Dedicated agent pools for Tasks
N/A
N/A
Supported

1 Storage included in the daily rate for each tier. Additional storage may be used, up to the registry storage limit, at an additional daily rate per GiB. For rate information, see Azure Container Registry pricing. If you need storage beyond the registry storage limit, please contact Azure Support.

2 Individual actions of `content/delete`, `content/read`, `content/write`, `metadata/read`, `metadata/write` correspond to the limit of repositories per non-Microsoft Entra token scope map.

## Azure Content Delivery Network limits

Resource
Limit

Azure Content Delivery Network profiles
25

Content Delivery Network endpoints per profile
25

Custom domains per endpoint
25

Maximum origin group per profile
10

Maximum origin per origin group
10

Maximum number of rules per CDN endpoint
25

Maximum number of match conditions per rule
10

Maximum number of actions per rule
5

Maximum bandwidth per profile*
75 Gbps

Maximum requests per second per profile
100,000

HTTP header size limit (per header)
32 KB

*These two limits are only applicable to Azure CDN Standard from Microsoft (classic). If the traffic isn't globally distributed and concentrated in one or two regions, or if a higher quota limit is needed, create an Azure Support request.

A Content Delivery Network subscription can contain one or more Content Delivery Network profiles. A Content Delivery Network profile can contain one or more Content Delivery Network endpoints. You might want to use multiple profiles to organize your Content Delivery Network endpoints by internet domain, web application, or some other criteria.

## Azure Data Lake Analytics limits

Azure Data Lake Analytics makes the complex task of managing distributed infrastructure and complex code easy. It dynamically provisions resources, and you can use it to do analytics on exabytes of data. When the job completes, it winds down resources automatically. You pay only for the processing power that was used. As you increase or decrease the size of data stored or the amount of compute used, you don't have to rewrite code. To raise the default limits for your subscription, contact support.

Resource
Limit
Comments

Maximum number of concurrent jobs
20

Maximum number of analytics units (AUs) per account
250
Use any combination of up to a maximum of 250 AUs across 20 jobs. To increase this limit, contact Microsoft Support.

Maximum script size for job submission
3 MB

Maximum number of Data Lake Analytics accounts per region per subscription
5
To increase this limit, contact Microsoft Support.

## Azure Data Lake Storage limits

Azure Data Lake Storage Gen2 is not a dedicated service or storage account type. It is the latest release of capabilities that are dedicated to big data analytics. These capabilities are available in a general-purpose v2 or BlockBlobStorage storage account, and you can obtain them by enabling the Hierarchical namespace feature of the account. For scale targets, see these articles.

- Scale targets for Blob storage.

- Scale targets for standard storage accounts.

Azure Data Lake Storage Gen1 is a dedicated service. It's an enterprise-wide hyper-scale repository for big data analytic workloads. You can use Data Lake Storage Gen1 to capture data of any size, type, and ingestion speed in one single place for operational and exploratory analytics. There's no limit to the amount of data you can store in a Data Lake Storage Gen1 account.

Resource
Limit
Comments

Maximum number of Data Lake Storage Gen1 accounts, per subscription, per region
10
To request an increase for this limit, contact support.

Maximum number of access ACLs, per file or folder
32
This is a hard limit. Use groups to manage access with fewer entries.

Maximum number of default ACLs, per file or folder
32
This is a hard limit. Use groups to manage access with fewer entries.

## Azure Data Share limits

Azure Data Share enables organizations to simply and securely share data with their customers and partners.

Resource
Limit

Maximum number of Data Share resources per Azure subscription
100

Maximum number of sent shares per Data Share resource
200

Maximum number of received shares per Data Share resource
100

Maximum number of invitations per sent share
200

Maximum number of share subscriptions per sent share
200

Maximum number of datasets per share
200

Maximum number of snapshot schedules per share
1

## Azure Database Migration Service Limits

Azure Database Migration Service is a fully managed service designed to enable seamless migrations from multiple database sources to Azure data platforms with minimal downtime.

Resource
Limit
Comments

Maximum number of services per subscription, per region
10
To request an increase for this limit, contact support.

## Azure Device Registry limits

The following tables list the limits that apply to the Azure Device Registry resources. Use Azure Device Registry with Azure IoT Hub and Azure IoT Operations.

### General

Resource type
Limit type
Limit

Azure Device Registry namespaces
Count per Azure subscription
100

IoT Hub instances
Count per namespace
10

### Assets and devices

Resource type
Limit type
Limit

Devices
Count per Azure subscription
1,000,0001

Devices / discovered devices
Count per Kubernetes cluster
1,000

Devices / discovered devices (read)
Operations per minute per Azure subscription
5,000

Devices / discovered devices (create/update)
Operations per minute per Azure subscription
500

Assets
Count per Azure subscription
100,000

Assets / discovered assets
Count per Azure Device Registry namespace
10,000

Assets / discovered assets
Count per Kubernetes cluster
1,000

Assets / discovered assets (read)
Operations per minute per Azure subscription
5,000

Assets / discovered assets (create/update)
Operations per minute per Azure subscription
500

Assets: datasets, event groups, and management groups
Count per asset
100

Assets: data points, events, and management actions
Count per asset
1,000

Assets (classic)
Count per Azure subscription
10,000

1 If you require a higher limit, open a support ticket to submit a request for consideration.

### Certificate management

The following table lists the resource count limits for certificate management in Azure Device Registry.

Resource type
Limit type
Limit

Certificate authority
Count per subscription
8

Root certificate authorities
Count per Azure Device Registry namespace
1

Intermediate certificate authorities
Count per Azure Device Registry namespace
3

Certificate policies
Count per intermediate certificate authority
1

The following table lists the certificate validity limits.

Resource type
Limit type
Limit

Root certificate authority
Maximum validity (years)
10

Intermediate certificate authority
Maximum validity (years)
1

Leaf certificate
Minimum validity (days)
1

Leaf certificate
Maximum validity (days)
90

The following table lists the certificate issuance and revocation limits.

Resource type
Limit type
Limit

Leaf certificate
Maximum issued per minute by a single namespace
1,000

Leaf certificate
Maximum issued per minute by a single intermediate certificate authority
1,000

Leaf certificate
Maximum unique certificates issued to a single device within 24 hours
20

Leaf certificate
Maximum leaf certificate revocations per minute
1,000

### Schema registries

Resource type
Limit type
Limit

Schema registries
Count per Azure subscription
100

Schemas
Read operations per minute per Azure subscription
600

Schema versions
Read operations per minute per Azure subscription
600

Schema registries
Read operations per minute per Azure subscription
600

## Azure Device Update for IoT Hub limits

Limits can be adjusted only for the Standard SKU. Limit adjustment requests are evaluated on a case-by-case basis, and approvals aren't guaranteed.

Limit adjustment requests aren't accepted for the Free SKU. Also, Free SKU instances can't be upgraded to Standard SKU instances.

The following table shows the limits for the Device Update for IoT Hub resource in Azure Resource Manager.

Resource
Standard SKU limit
Free SKU limit
Adjustable for Standard SKU?

Accounts per subscription
50
1
No

Instances per account
50
1
No

Length of account name
3-24 characters
3-24 characters
No

Length of instance name
3-36 characters
3-36 characters
No

The following table shows the limits associated with various Device Update operations.

Operation
Standard SKU limit
Free SKU limit
Adjustable for Standard SKU?

Number of devices per instance
1 million
10
Yes

Number of device groups per instance
100
10
Yes

Number of device classes per instance
80
10
Yes

Number of active deployments per instance
50, including one reserved for cancellations
5, including one reserved for cancellations
Yes

Number of total deployments per instance, including all active, inactive, and canceled deployments that aren't deleted
100
20
No

Number of update providers per instance
25
2
No

Number of update names per provider per instance
25
2
No

Number of update versions per update provider and name per instance
100
5
No

Total number of updates per instance
100
10
No

Maximum single update file size
2 GB
2 GB
Yes

Maximum combined size of all files in a single import action
2 GB
2 GB
Yes

Maximum number of files in a single update
10
10
No

Total data storage included per instance
100 GB
5 GB
No

Note

Canceled or inactive deployments count toward your total deployment limit. Make sure to clean up these deployments periodically so you aren't prevented from creating new deployments.

## Azure Digital Twins limits

Note

Some areas of this service have adjustable limits, and others do not. The following tables use the Adjustable? column to represent this condition. When the limit can be adjusted, the Adjustable? value is Yes.

### Functional limits

The following table lists the functional limits of Azure Digital Twins.

Area
Capability
Default limit
Adjustable?

Azure resource
Number of Azure Digital Twins instances in a region, per subscription
10
Yes, up to 50

Digital twins
Number of twins in an Azure Digital Twins instance
2,000,000
Yes

Digital twins
Number of digital twins that can be imported in a single Import Jobs API job
2,000,000
No

Digital twins
Number of incoming relationships to a single twin
50,000
No

Digital twins
Number of outgoing relationships from a single twin
50,000
No

Digital twins
Total number of relationships in an Azure Digital Twins instance
20,000,000
Yes

Digital twins
Number of relationships that can be imported in a single Import Jobs API job
10,000,000
No

Digital twins
Maximum size (of JSON body in a PUT or PATCH request) of a single twin
32 KB
No

Digital twins
Maximum request payload size
32 KB
No

Digital twins
Maximum size of a string property value (UTF-8)
4 KB
No

Digital twins
Maximum size of a property name
1 KB
No

Routing
Number of endpoints for a single Azure Digital Twins instance
6
No

Routing
Number of routes for a single Azure Digital Twins instance
6
Yes

Models
Number of models within a single Azure Digital Twins instance
10,000
Yes

Models
Number of models that can be imported in a single API call (not using the Import Jobs API)
250
No

Models
Number of models that can be imported in a single Import Jobs API job
10,000
No

Models
Maximum size (of JSON body in a PUT or PATCH request) of a single model
1 MB
No

Models
Number of items returned in a single page
100
No

Query
Number of items returned in a single page
1000
Yes

Query
Number of `AND` / `OR` expressions in a query
50
Yes

Query
Number of array items in an `IN` / `NOT IN` clause
50
Yes

Query
Number of characters in a query
8,000
Yes

Query
Number of `JOINS` in a query
5
Yes

### Rate limits

The following table lists the rate limits of different APIs.

API
Capability
Default limit
Adjustable?

Jobs API
Number of requests per second
1
Yes

Jobs API
Number of bulk jobs running concurrently (including import and delete)
1
Yes

Models API
Number of requests per second
100
Yes

Digital Twins API
Number of read requests per second
1,000
Yes

Digital Twins API
Number of patch requests per second
1,000
Yes

Digital Twins API
Number of create/delete operations per second across all twins and relationships
500
Yes

Digital Twins API
Number of create/update/delete operations per second on a single twin or its incoming/outgoing relationships
10
No

Digital Twins API
Number of outstanding operations on a single twin or its incoming/outgoing relationships
500
No

Query API
Number of requests per second
500
Yes

Query API
Query Units per second
4,000
Yes

Event Routes API
Number of requests per second
100
Yes

### Other limits

Limits on data types and fields within DTDL documents for Azure Digital Twins models can be found in its spec documentation in GitHub: Digital Twins Definition Language (DTDL) - version 3.

Query latency details are described in Query language. Limitations of particular query language features can be found in the query reference documentation.

## Azure Event Grid limits

Note

The following limits are per region.

## Event Grid throttle limits

Event Grid offers a Standard tier and a Basic tier. The Event Grid Standard tier enables publish-subscribe by using Message Queuing Telemetry Transport (MQTT) broker functionality and pull delivery of messages through the Event Grid namespace. The Event Grid Basic tier enables push delivery by using Event Grid custom topics, Event Grid system topics, Event Grid domains, and Event Grid partner topics. For more information, see Choose the right Event Grid tier. This article describes the quota and limits for both tiers.

## Event Grid namespace resource limits

Event Grid namespaces enable MQTT messaging and HTTP pull delivery.
The following limits apply to namespace resources in Event Grid.

Limit description
Limit

Event Grid namespaces per Azure subscription
50

Maximum throughput units (TUs) per Event Grid namespace
40 (To request an increase beyond 40 TUs, contact Microsoft at askmqtt@microsoft.com.)

IP firewall rules per Event Grid namespace
16

## MQTT limits in the Event Grid namespace

The following limits apply to MQTT in the Event Grid namespace resource.

Throughput units define the ingress and egress event rate capacity in namespaces. You can use TUs to control the capacity of your namespace resource for message ingress and egress.

Limit description
Limit

MQTT sessions per Event Grid namespace
10,000 per TU

Sessions per Event Grid namespace
10,000 per TU

Session expiry interval
8 hours, configurable on the Event Grid namespace

Inbound MQTT publishing requests per Event Grid namespace
1,000 messages per second per TU

Inbound MQTT bandwidth per Event Grid namespace
1 MB per second per TU

Inbound MQTT publishing requests per session
1,000 messages per second

Inbound MQTT bandwidth per session
1 MB per second

Inbound in-flight MQTT messages*
1,000 messages

Inbound MQTT/HTTP publishing requests per Event Grid namespace
1,000 messages per second per TU

Inbound MQTT/HTTP bandwidth per Event Grid namespace
1 MB per second per TU

Inbound MQTT/HTTP publishing requests per session
1,000 messages per second

Inbound MQTT/HTTP bandwidth per session
1 MB per second

Inbound in-flight MQTT/HTTP messages*
1,000 messages

Inbound in-flight MQTT/HTTP bandwidth*
64 KB

Maximum Retain message size**
64 KB

Maximum Retain message per TU
10,000 messages or 640 MB (whichever is reached first)

Total Retain storage per TU
640 MB

Retain message expiry (MQTT 3.1.1)
365 days (default). To configure a Retain Expiry less than 365 days, contact Microsoft at askmqtt@microsoft.com

Retain message expiry (MQTT 5.0)
Configurable by using the message expiry interval with a range of 0 to 31,536,000 seconds (365 days)

Outbound MQTT publishing requests per Event Grid namespace
1,000 messages per second per TU

Outbound MQTT bandwidth per Event Grid namespace
1 MB per second per TU

Outbound MQTT publishing requests per session
100 messages per second

Outbound MQTT bandwidth per session
1 MB per second

Outbound in-flight MQTT messages*
100 messages

Outbound in-flight MQTT bandwidth*
64 KB

Maximum message size
1 MB (1024 KB)

Segments per topic/topic filter
15

Topic size
256 B

MQTTv5 response topic
256 B

MQTTv5 topic aliases
10 per session

MQTTv5 total size of all user properties
32 KB

MQTT connect rate per client session
1 connection attempt per second per client session

MQTTv5 content type size
256 B

MQTTv5 correlation data size
256 B

Connect requests
200 requests per second per TU

MQTTv5 authentication data size
8 KB

Maximum Keep Alive interval
1,160

Topic filters per MQTT SUBSCRIBE packet
10

Subscribe and unsubscribe requests per Event Grid namespace
200 requests per second

Subscribe and unsubscribe requests per session
5 requests per second

Subscriptions per MQTT session
50

Subscriptions per Event Grid namespace
1 million

Subscriptions per MQTT topic
Unlimited, if they don't exceed the limit for subscriptions per Event Grid namespace or session

Maximum number of shared subscription groups per Namespace
100

Maximum number of subscriptions in a shared subscription group
100

Maximum number of shared subscriptions per session
10 (included within total 50 subscriptions per session)

Maximum outgoing message rate per shared subscription
100 Ã number of shared subscribers

Maximum sessions per shared subscription
100

Maximum shared subscriptions per broker
100

Registered client resources
10,000 clients per TU

Certificate Authority certificates
10

Client groups
10

Topic spaces
10

Topic templates
10 per topic space

Permission bindings
100

* For MQTTv5, learn more about flow control support.

** Retained messages count against the total MQTT storage quota for the namespace. When the quota is reached, publishing new retained messages fails until existing messages are expired or deleted (for example, via an empty payload publish).

## Events limits in the Event Grid namespace

The following limits apply to events in the Event Grid namespace resource.

Limit description
Limit

Event Grid namespace topics
100 per TU

Event ingress
1,000 events per second or 1 MB per second per TU (whichever comes first)

Event egress (push and pull APIs)
Up to 2,000 events per second or 2 MB per second per TU

Event egress (acknowledge, release, reject, and renew lock APIs)
Up to 2,000 events per second or 2 MB per second per TU

Maximum event retention on Event Grid namespace topics
7 days

Subscriptions per topic
500

Maximum event size
1 MB

Batch size
1 MB

Events per request
1,000

## Custom topic, system topic, and partner topic resource limits

The following limits apply to Event Grid custom topic, system topic, and partner topic resources.

Limit description
Limit

Custom topics per Azure subscription
100
When the limit is reached, you can consider a different region or consider using domains, which can support 100,000 topics.

Event subscriptions per topic
500. For Event Subscriptions on Azure Subscriptions the limit is 100. 
This limit can't be increased.

Publish rate for a custom or a partner topic (ingress)
5,000 events or 5 MB per second (whichever comes first)
An event is counted for limits and pricing purposes as a 64-KB data chunk. So, if the event is 128 KB, it counts as two events.

Event size
1 MB
This limit can't be increased.

Maximum event retention on topics
1 day
This limit can't be increased.

Number of incoming events per batch
5,000
This limit can't be increased.

Private endpoint connections per topic
64
This limit can't be increased.

IP firewall rules per topic
128

## Domain resource limits

The following limits apply to the Event Grid domain resource.

Limit description
Limit

Domains per Azure subscription
100

Topics per domain
100,000

Event subscriptions per topic within a domain
500
This limit can't be increased.

Domain scope event subscriptions
50
This limit can't be increased.

Publish rate for a domain (ingress)
5,000 events or 5 MB per second (whichever comes first)
An event is counted for limits and pricing purposes as a 64-KB data chunk. So, if the event is 128 KB, it counts as two events.

Maximum event retention on domain topics
1 day
This limit can't be increased.

Private endpoint connections per domain
64

IP firewall rules per topic
128

## Azure Event Hubs limits

The following tables provide quotas and limits specific to Azure Event Hubs. For information about Event Hubs pricing, see Event Hubs pricing.

### Common limits for all tiers

The following limits are common across all tiers.

Limit
Notes
Value

Size of an event hub name
-
256 characters

Size of a consumer group name
Kafka protocol doesn't require the creation of a consumer group.
Kafka: 256 characters
Advanced Message Queuing Protocol (AMQP): 50 characters

Number of non-epoch receivers per consumer group
-
5

Number of authorization rules per namespace
Subsequent requests for authorization rule creation are rejected.
12

Number of calls to the GetRuntimeInformation method
-
50 per second per consumer group

Number of virtual networks
-
128

Number of IP Config rules
-
128

Maximum length of a schema group name

50

Maximum length of a schema name

100

Size in bytes per schema

1 MB

Number of properties per schema group

1024

Size in bytes per schema group property key

256

Size in bytes per schema group property value

1024

Number of concurrent receive requests on a hub/topic
Subsequent receive requests are throttled. This quota applies to the combined number of concurrent receive operations across all consumers/consumer groups
5000

### Basic vs. standard vs. premium vs. dedicated tiers

The following table shows limits that are different for Basic, Standard, Premium, and Dedicated tiers.

Note

- In the table, CU is capacity unit, PU is processing unit, and TU is throughput unit.

- You can configure TUs for a Basic or Standard tier namespace or PUs for a Premium tier namespace.

- When you create a dedicated cluster, Azure Event Hubs assigns one CU to the cluster. You can scale out by increasing CUs or scale in by decreasing CUs for the cluster. For step-by-step instructions, see Scale dedicated cluster. To scale beyond 10 CUs, submit a support request.

Limit
Basic
Standard
Premium
Dedicated

Maximum size of Event Hubs publication
256 KB
1 MB
1 MB
20 MB

Number of consumer groups per event hub
1
20
100
1,000
No limit per CU

Number of Kafka consumer groups per namespace
N/A
1,000
1,000
1,000

Number of brokered connections per namespace
100
5,000
10,000 per PU

For example, if the namespace is assigned 4 PUs, the limit is 40,000.
100,000 per CU

Maximum retention period of event data
1 day
7 days
90 days
90 days

Event storage for retention
84 GB per TU
84 GB per TU
1 TB per PU
10 TB per CU

Maximum TUs or PUs or CUs
40 TUs
40 TUs
16 PUs
10 CUs (more via support request)

Number of partitions per event hub
32
32
100 per event hub, but there's a limit of 200 per PU at the namespace level.

 For example, if a namespace is assigned 2 PUs, the limit for total number of partitions in all event hubs in the namespace is 2 * 200 = 400.
1,024 per event hub
 2,000 per CU

Number of namespaces per subscription per region
1,000 (all tiers)
1,000 (all tiers)
1,000 (all tiers)
1,000 (50 per CU)

Number of event hubs per namespace
10
10
100 per PU
1,000

Capture
N/A
Pay per hour
Included
Included

Size of compacted event hub
N/A
1 GB per partition
250 GB per partition
250 GB per partition

Size of the schema registry (namespace) in megabytes
N/A
25
100
1,024

Number of schema groups in a schema registry or namespace
N/A
1: excluding the default group
100 
1 MB per schema
1,000
1 MB per schema

Number of schema versions across all schema groups
N/A
25
1,000
10,000

Throughput per unit
Ingress: 1 MB/sec or 1,000 events per second
Egress: 2 MB/sec or 4,096 events per second
Ingress: 1 MB/sec or 1,000 events per second
Egress: 2 MB/sec or 4,096 events per second
No limits per PU *
No limits per CU *

* Depends on factors such as resource allocation, number of partitions, and storage.

Note

You can publish events individually or batched. The publication limit (according to tier) applies regardless of whether it's a single event or a batch. Publishing events larger than the maximum threshold is rejected.

## Azure IoT Central limits

IoT Central limits the number of applications you can deploy in a subscription to 100. To learn more, see Azure IoT Central quota and limits.

## Azure IoT Hub limits

The following table lists the limits associated with the different service tiers S1, S2, S3, and F1. For information about the cost of each unit in each tier, see Azure IoT Hub pricing.

Resource
S1 Standard
S2 Standard
S3 Standard
F1 Free

Messages/day
400,000
6,000,000
300,000,000
8,000

Maximum units
200
200
10
1

The following table lists the limits that apply to IoT Hub resources.

Resource
Limit

Maximum paid IoT hubs per Azure subscription
50

Maximum free IoT hubs per Azure subscription
1

Maximum number of characters in a device ID
128

Maximum number of device identities
 returned in a single call
1,000

IoT Hub message maximum retention for device-to-cloud messages
7 days

Maximum size of device-to-cloud message
256 KB

Maximum size of device-to-cloud batch
AMQP and HTTP: 256 KB for the entire batch 
MQTT: 256 KB for each message

Maximum messages in device-to-cloud batch
500

Maximum size of cloud-to-device message
64 KB

Maximum TTL for cloud-to-device messages
2 days

Maximum delivery count for cloud-to-device 
 messages
100

Maximum cloud-to-device queue depth per device
50

Maximum delivery count for feedback messages 
 in response to a cloud-to-device message
100

Maximum TTL for feedback messages in 
 response to a cloud-to-device message
2 days

Maximum size of device twin
8 KB for tags section, and 32 KB for desired and reported properties sections each

Maximum length of device twin string key
1 KB

Maximum length of device twin string value
4 KB

Maximum depth of object in device twin
10

Maximum size of direct method payload
128 KB

Job history maximum retention
30 days

Maximum concurrent jobs
10 (for S3), 5 for (S2), 1 (for S1)

Maximum additional endpoints (beyond built-in endpoints)
10 (for S1, S2, and S3)

Maximum message routing rules
100 (for S1, S2, and S3)

Maximum number of concurrently connected device streams
50 (for S1, S2, S3, and F1 only)

Maximum device stream data transfer
300 MB per day (for S1, S2, S3, and F1 only)

Note

The total number of devices plus modules that can be registered to a single IoT hub is capped at 1,000,000.

IoT Hub throttles requests when the following quotas are exceeded.

Throttle
Per-hub value

Identity registry operations 
 (create, retrieve, list, update, and delete), 
 individual or bulk import/export
83.33/sec/unit (5,000/min/unit) (for S3). 
 1.67/sec/unit (100/min/unit) (for S1 and S2).

Device connections
6,000/sec/unit (for S3), 120/sec/unit (for S2), 12/sec/unit (for S1). 
Minimum of 100/sec.

Device-to-cloud sends
6,000/sec/unit (for S3), 120/sec/unit (for S2), 12/sec/unit (for S1). 
Minimum of 100/sec.

Cloud-to-device sends
83.33/sec/unit (5,000/min/unit) (for S3), 1.67/sec/unit (100/min/unit) (for S1 and S2).

Cloud-to-device receives
833.33/sec/unit (50,000/min/unit) (for S3), 16.67/sec/unit (1,000/min/unit) (for S1 and S2).

File upload operations
83.33 file upload initiations/sec/unit (5,000/min/unit) (for S3), 1.67 file upload initiations/sec/unit (100/min/unit) (for S1 and S2). 
 10 concurrent file uploads per device.

Direct methods
24 MB/sec/unit (for S3), 480 KB/sec/unit (for S2), 160 KB/sec/unit (for S1).
 Based on 8-KB throttling meter size.

Device twin reads
500/sec/unit (for S3), Maximum of 100/sec or 10/sec/unit (for S2), 100/sec (for S1)

Device twin updates
250/sec/unit (for S3), Maximum of 50/sec or 5/sec/unit (for S2), 50/sec (for S1)

Jobs operations 
 (create, update, list, and delete)
83.33/sec/unit (5,000/min/unit) (for S3), 1.67/sec/unit (100/min/unit) (for S2), 1.67/sec/unit (100/min/unit) (for S1).

Jobs per-device operation throughput
50/sec/unit (for S3), maximum of 10/sec or 1/sec/unit (for S2), 10/sec (for S1).

Device stream initiation rate
5 new streams/sec (for S1, S2, S3, and F1 only).

### IoT Hub with ADR integration limits

The following table lists the limits that apply to IoT Hub instances with ADR integration.

Feature
Limit

Number of devices per IoT Hub instance
1,000,000

Number of IoT Hub instances per ADR namespace
10

Protocols supported for certificate provisioning
HTTP, MQTT, and MQTT-Web-Sockets protocols.

For more information about ADR namespaces, see the full list of ADR limits.

## Azure IoT Hub Device Provisioning Service limits

Some areas of this service have adjustable limits. The tables below include an Adjustable? column. If the limit is adjustable, the Adjustable? value is Yes.

The actual value that you can adjust a limit to might vary based on your deployment. Very large deployments might require multiple instances of DPS.

If your business requires a higher adjustable limit or quota, open a support ticket to request additional resources. An increase request isn't guaranteed because each case requires individual review. Contact Microsoft support as early as possible during your implementation so the team can determine whether to approve your request and help you plan accordingly.

The following table lists the limits that apply to Azure IoT Hub Device Provisioning Service resources.

Resource
Limit
Adjustable?

Maximum device provisioning services per Azure subscription
10
Yes

Maximum number of registrations
1,000,000
Yes

Maximum number of individual enrollments
1,000,000
Yes

Maximum number of enrollment groups (X.509 certificate)
100
Yes

Maximum number of enrollment groups (symmetric key)
100
No

Maximum number of CAs
25
Yes

Maximum number of linked IoT hubs
50
No

Maximum size of message
96 KB
No

Tip

If the hard limit on symmetric key enrollment groups is a blocking issue, use individual enrollments as a workaround.

The Device Provisioning Service has the following rate limits.

Rate
Per-unit value
Adjustable?

Operations
1,000/min/service
Yes

Device registrations
1,000/min/service
Yes

Device polling operation
5/10 sec/device
No

## Azure Key Vault limits

### Resource type: vault

This section describes service limits for resource type `vaults`.

#### Key transactions (maximum transactions allowed in 10 seconds, per vault per region1)

Key type
HSM key
CREATE key / RELEASE key
HSM key
All other transactions
Software key
CREATE key / RELEASE key
Software key
All other transactions

RSA 2,048-bit
10
2,000
20
4,000

`oct-HSM` (AES; Premium only)
10
2,000
Not supported
Not supported

RSA 3,072-bit
10
500
20
1,000

RSA 4,096-bit
10
250
20
500

ECC P-256
10
2,000
20
4,000

ECC P-384
10
2,000
20
4,000

ECC P-521
10
2,000
20
4,000

ECC SECP256K1
10
2,000
20
4,000

Note

The `CREATE key` and `RELEASE key` (secure key release, SKR) operations share the same throttling category, so the combined rate for these two operations is limited to 10 transactions per 10 seconds for HSM-protected keys, and 20 transactions per 10 seconds for software-protected keys. If your workload requires higher SKR throughput, use Azure Key Vault Managed HSM, which offers dedicated HSM instances with higher limits. For more information, see Managed HSM scaling guidance.

Note

In the previous table, we see that for RSA 2,048-bit software keys, 4,000 GET transactions per 10 seconds are allowed. For RSA 2,048-bit HSM-keys, 2,000 GET transactions per 10 seconds are allowed.

The throttling thresholds are weighted, and enforcement is on their sum. For example, as shown in the previous table, when you perform GET operations on RSA HSM-keys, it's eight times more expensive to use 4,096-bit keys compared to 2,048-bit keys because 2,000/250 = 8.

In a given 10-second interval, an Azure Key Vault client can do only one of the following operations before it encounters a `429` throttling HTTP status code:

- 4,000 RSA 2,048-bit software-key GET transactions

- 2,000 RSA 2,048-bit HSM-key GET transactions

- 250 RSA 4,096-bit HSM-key GET transactions

- 248 RSA 4,096-bit HSM-key GET transactions and 16 RSA 2,048-bit HSM-key GET transactions

#### Secrets, managed storage account keys, and vault transactions

Transactions type
Maximum transactions allowed in 10 seconds, per vault per region1

Secret
CREATE secret
300 (collectively across all three operations)

Certificate
IMPORT certificate
300 (collectively across all three operations)

Key
IMPORT key
300 (collectively across all three operations)

All other transactions
4,000

Note

The 300-transaction limit applies collectively across the "CREATE secret," "IMPORT certificate," and "IMPORT key" operations. For example, if within 10 seconds you create 100 secrets, import 100 certificates, and import 100 keys, you will reach the limit and encounter throttling. For information on how to handle throttling when these limits are exceeded, see Azure Key Vault throttling guidance.

1 A subscription-wide limit for all transaction types is five times per key vault limit.

#### Backup keys, secrets, certificates

When you back up a key vault object, such as a secret, key, or certificate, the backup operation downloads the object as an encrypted blob. This blob cannot be decrypted outside of Azure. To get usable data from this blob, you must restore the blob into a key vault within the same Azure subscription and Azure geography

Transactions type
Maximum key vault object versions allowed

Back up individual key, secret, certificate
500

Note

If you attempt to back up a key, secret, or certificate object with more versions than the limit, the operation results in an error. It is not possible to delete previous versions of a key, secret, or certificate.

### Limits on count of keys, secrets, and certificates

Key Vault does not restrict the number of keys, secrets or certificates that can be stored in a vault. The transaction limits on the vault should be taken into account to ensure that operations are not throttled.

Key Vault does not restrict the number of versions on a secret, key or certificate, but storing a large number of versions (500+) can impact the performance of backup operations. See Azure Key Vault Backup.

## Azure Key Vault: Managed HSM limits

### Resource type: Managed HSM

This section describes service limits for resource type `managed HSM`.

#### Object limits

Item
Limits

Number of HSM instances per subscription per region
5

Number of keys per HSM instance
5000

Number of versions per key
100

Number of custom role definitions per HSM instance
50

Number of role assignments at HSM scope
50

Number of role assignments at each individual key scope
10

For detailed performance capacity planning and scaling guidance, see Azure Managed HSM scaling guidance.

## Azure Managed Identity limits

- Each managed identity counts towards the object quota limit in a Microsoft Entra tenant as described in Microsoft Entra service limits and restrictions.

- The rate at which managed identities can be created have the following limits:

- Per Microsoft Entra tenant per Azure region: 400 create operations per 20 seconds.

- Per Azure Subscription per Azure region : 80 create operations per 20 seconds.

- The rate at which a user-assigned managed identity can be assigned with an Azure resource :

- Per Microsoft Entra tenant per Azure region: 400 assignment operations per 20 seconds.

- Per Azure Subscription per Azure region : 300 assignment operations per 20 seconds.

## Azure Media Services limits

Note

For resources that aren't fixed, open a support ticket to ask for an increase in the quotas. Don't create additional Azure Media Services accounts in an attempt to obtain higher limits.

### Account limits

Resource
Default Limit

Media Services accounts in a single subscription
100 (fixed)

### Asset limits

Resource
Default Limit

Assets per Media Services account
1,000,000

### Storage (media) limits

Resource
Default Limit

File size
In some scenarios, there is a limit on the maximum file size supported for processing in Media Services. (1)

Storage accounts
100(2) (fixed)

1 The maximum size supported for a single blob is currently up to 5 TB in Azure Blob Storage. Additional limits apply in Media Services based on the VM sizes that are used by the service. The size limit applies to the files that you upload and also the files that get generated as a result of Media Services processing (encoding or analyzing). If your source file is larger than 260-GB, your Job will likely fail.

2 The storage accounts must be from the same Azure subscription.

### Jobs (encoding & analyzing) limits

Resource
Default Limit

Jobs per Media Services account
500,000 (3) (fixed)

Job inputs per Job
50 (fixed)

Job outputs per Job
20 (fixed)

Transforms per Media Services account
100 (fixed)

Transform outputs in a Transform
20 (fixed)

Files per job input
10 (fixed)

3 This number includes queued, finished, active, and canceled Jobs. It does not include deleted Jobs.

Any Job record in your account older than 90 days will be automatically deleted, even if the total number of records is below the maximum quota.

### Live streaming limits

Resource
Default Limit

Live Events (4) per Media Services account
5

Live Outputs per Live Event
3 (5)

Max Live Output duration
Size of the DVR window

4 For detailed information about Live Event limitations, see Live Event types comparison and limitations.

5 Live Outputs start on creation and stop when deleted.

### Packaging & delivery limits

Resource
Default Limit

Streaming Endpoints (stopped or running) per Media Services account
2

Dynamic Manifest Filters
100

Streaming Policies
100 (6)

Unique Streaming Locators associated with an Asset at one time
100(7) (fixed)

6 When using a custom Streaming Policy, you should design a limited set of such policies for your Media Service account, and re-use them for your StreamingLocators whenever the same encryption options and protocols are needed. You should not be creating a new Streaming Policy for each Streaming Locator.

7 Streaming Locators are not designed for managing per-user access control. To give different access rights to individual users, use Digital Rights Management (DRM) solutions.

### Protection limits

Resource
Default Limit

Options per Content Key Policy
30

Licenses per month for each of the DRM types on Media Services key delivery service per account
1,000,000

### Support ticket

For resources that are not fixed, you may ask for the quotas to be raised, by opening a support ticket. Include detailed information in the request on the desired quota changes, use-case scenarios, and regions required. 
Do not create additional Azure Media Services accounts in an attempt to obtain higher limits.

### Azure Media Services v2 (legacy)

For limits specific to Media Services v2 (legacy), see [Media Services v2 (legacy)]

## Azure Mobile Services limits

Tier
Free
Basic
Standard

API calls
500,000
1.5 million per unit
15 million per unit

Active devices
500
Unlimited
Unlimited

Scale
N/A
Up to 6 units
Unlimited units

Push notifications
Azure Notification Hubs Free tier included, up to 1 million pushes
Notification Hubs Basic tier included, up to 10 million pushes
Notification Hubs Standard tier included, up to 10 million pushes

Real-time messaging/
WebSockets
Limited
350 per mobile service
Unlimited

Offline synchronizations
Limited
Included
Included

Scheduled jobs
Limited
Included
Included

Azure SQL Database (required) 
Standard rates apply for additional capacity
20 MB included
20 MB included
20 MB included

CPU capacity
60 minutes per day
Unlimited
Unlimited

Outbound data transfer
165 MB per day (daily rollover)
Included
Included

For more information on limits and pricing, see Azure Mobile Services pricing.

## Azure networking limits

### Networking limits - Azure Resource Manager

The following limits apply only for networking resources managed through Azure Resource Manager per region per subscription. Learn how to view your current resource usage against your subscription limits.

Note

We have increased all default limits to their maximum limits. If there's no maximum limit column, the resource doesn't have adjustable limits. If you had these limits manually increased by support in the past and are currently seeing limits lower than what is listed in the following tables, open an online customer support request at no charge

Resource
Limit

Virtual networks
1,000

Subnets per virtual network
3,000

Virtual network peerings per virtual network
650

Virtual network gateways (VPN gateways) per virtual network
1

Virtual network gateways (ExpressRoute gateways) per virtual network
1

DNS servers per virtual network
20

DNS servers per network interface
20

Private IP addresses per virtual network
65,536

Total Private Addresses for a group of Peered Virtual networks
128,000

Private IP addresses per network interface
256

Private IP addresses per virtual machine
256 * N (N is number of NICs on VM)

Public IP addresses per network interface
256

Public IP addresses per virtual machine
256

Concurrent TCP or UDP flows per NIC of a virtual machine or role instance
500,000

Network interface cards
65,536

Network Security Groups
5,000

NSG rules per NSG
2,000

IP addresses and ranges specified for source or destination in a security group (The limit applies separately to source and destination)
6,000

Application security groups
3,000

Application security groups per IP configuration, per NIC
20

Application security groups referenced as source/destination per NSG rule
10

IP configurations per application security group
4,000

Application security groups that can be specified within all security rules of a network security group
100

User-defined route tables
600

User-defined routes per route table
1,000

Routes with service tag per route table
25

Point-to-site root certificates per Azure VPN Gateway
20

Point-to-site revoked client certificates per Azure VPN Gateway
300

Virtual network TAP configurations per subscription
10

#### Public IP address limits

Resource
Default limit
Maximum limit

Basic Public IPv4, IPv6 addresses1,2,3
10
Contact support

Standard Public IPv4, IPv6 addresses1
10
Contact support

Global Tier Public IPv4, IPv6 addresses1
10
Contact support

Routing Preference Internet Public IPv4, IPv6 addresses1
10
Contact support

Public IP prefixes
limited by number of Standard Public IPs in a subscription
Contact support

Public IP prefix length
/28
Contact support

Custom IP prefixes
5
Contact support

1Default limits for Public IPv4/v6 addresses vary by offer category type, such as Free Trial, pay-as-you-go, CSP. For example, the default for Enterprise Agreement subscriptions is 1000 and the default for pay-as-you-go is 20. The majority of offers start at 10. There's also an overall maximum number of Public IP addresses per subscription.

2Basic Public IP addresses are retired as of September 30, 2025. See here for more details.

The following limits apply only for networking resources managed through the classic deployment model per subscription. Learn how to view your current resource usage against your subscription limits.

Resource
Default limit
Maximum limit

Virtual networks
100
100

Local network sites
20
50

DNS servers per virtual network
20
20

Private IP addresses per virtual network
4,096
4,096

Concurrent TCP or UDP flows per NIC of a virtual machine or role instance
500,000, up to 1,000,000 for two or more NICs.
500,000, up to 1,000,000 for two or more NICs.

Network Security Groups (NSGs)
200
200

NSG rules per NSG
200
1,000

User-defined route tables
200
200

User-defined routes per route table
600
600

Public IP addresses (dynamic)
500
500

Reserved public IP addresses
500
500

Public IP per deployment
5
Contact support

Private IP (internal load balancing) per deployment
1
1

Endpoint access control lists (ACLs)
50
50

### Azure Load Balancer limits

### Standard Load Balancer

Resource
Limit

Load balancers
1,000

Frontend IP configurations
600

Rules (Load Balancer + Inbound NAT) per resource
1,500

Rules per NIC (across all IPs on a NIC)1
300

High-availability ports rule
1 per internal frontend

Outbound rules per Load Balancer
600

Backend pool size
5,000

IP configurations per Load Balancer (across all backend pools)
20,000

Azure global Load Balancer Backend pool size
300

Backend IP configurations per frontend 2
10,000

Backend IP configurations across all frontends
500,000

1 Each NIC can have a total of 300 rules (load balancing, inbound NAT, and outbound rules combined) configured across all IP configurations on the NIC.
2 Backend IP configurations are aggregated across all load balancer rules including load balancing, inbound NAT, and outbound rules. Each rule a backend pool instance is configured to counts as one configuration.

Load Balancer doesn't apply any throughput limits. However, throughput limits for virtual machines and virtual networks still apply. For more information, see Virtual machine network bandwidth.

### Gateway Load Balancer

Resource
Limit

Resources chained per Gateway Load Balancer frontend (Load Balancer frontend configurations or VM NIC IP configurations combined)
100

All limits for Standard Load Balancer also apply to Gateway Load Balancer.

### Basic Load Balancer

Resource
Limit

Load balancers
1,000

Rules per resource
250

Rules per NIC (across all IPs on a NIC)
300

Frontend IP configurations 3
200

Backend pool size
300 IP configurations, single availability set

Availability sets per Load Balancer
1

Load Balancers per VM
2 (1 Public and 1 internal)

3 The limit for a single discrete resource in a backend pool (standalone virtual machine, availability set, or virtual machine scale-set placement group) is to have up to 250 Frontend IP configurations across a single Basic Public Load Balancer and Basic Internal Load Balancer.

### Azure Application Gateway limits

The following table applies to v1, v2, Standard, and WAF SKUs unless otherwise stated.

Resource
Limit
Note

Azure Application Gateway
1,000 per region per subscription

Frontend IP configurations
4
IPv4 - 1 public and 1 private.
IPv6 - 1 public and 1 private.

Frontend ports
1001

Backend address pools
100

Backend targets per pool
1,200

HTTP listeners
2001
Limited to 100 active listeners that are routing traffic. Active listeners = total number of listeners - listeners not active.
If a default configuration inside a routing rule is set to route traffic (for example, it has a listener, a backend pool, and HTTP settings) then that also counts as a listener. For more information, see Frequently asked questions about Application Gateway.

HTTP load-balancing rules
4001

Backend HTTP settings
1001

Instances per gateway
V1 SKU - 32
V2 SKU - 125

SSL certificates
1001
1 per HTTP listener

Maximum SSL certificate size
V1 SKU - 10 KB
V2 SKU - 16 KB

Maximum trusted client CA certificate size
25 KB
25 KB is the maximum aggregated size of root and intermediate certificates contained in an uploaded pem or cer file.

Maximum trusted client CA certificates
200
100 per SSL Profile

Authentication certificates
100

Trusted root certificates
100

Request timeout minimum
1 second

Request timeout maximum to private backend
24 hours

Request timeout maximum to external backend
4 minutes

Number of sites
1001
1 per HTTP listener

URL maps per listener
1

Host names per listener
5

Maximum path-based rules per URL map
100

Redirect configurations
1001

Number of rewrite rule sets
400

Number of Header or URL configuration per rewrite rule set
40

Number of conditions per rewrite rule set
40

Concurrent WebSocket connections
Medium gateways 20k2
 Large gateways 50k2

Maximum URL length
32 KB

Maximum header size
32 KB

Maximum header field size for HTTP/2
8 KB

Maximum header size for HTTP/2
16 KB

Maximum requests per HTTP/2 connection
1000
The total number of requests that can share the same frontend HTTP/2 connection

Maximum file upload size (Standard SKU)
V1 - 2 GB
V2 - 4 GB
This maximum size limit is shared with the request body

Maximum file upload size (WAF SKU)3
V1 Medium - 100 MB
V1 Large - 500 MB
V2 - 750 MB
V2 (with CRS 3.2 or DRS) - 4 GB4
1 MB - Minimum Value
100 MB - Default value
V2 with CRS 3.2 or DRS - can be turned On/Off

Maximum request size limit Standard SKU (without files)
V1 - 2 GB
V2 - 4 GB

Maximum custom request size limit WAF SKU (without files)
V1 or V2 (with CRS 3.1 and older) - 128 KB
V2 (with CRS 3.2 or DRS) - 2 MB4 with feature enabled
2GB - with feature disabled
8 KB - Minimum Value
128 KB - Default value
V2 with CRS 3.2 or DRS - can be turned On/Off

Maximum request inspection limit WAF SKU
V1 or V2 (with CRS 3.1 and older) - 128 KB
V2 (with CRS 3.2 or DRS) - 2 MB4
8 KB - Minimum Value
128 KB - Default value
V2 with CRS 3.2 or DRS - can be turned On/Off

Maximum Private Link Configurations
2
1 for public IP, 1 for private IP

Maximum Private Link IP Configurations
8

Maximum WAF custom rules per WAF policy
100

Maximum WAF match conditions per custom rule
10
This limit is not enforced by the WAF. Adding more than 10 match conditions can lead to performance degradation

WAF IP address ranges per match condition
540
600 - with CRS 3.2 or DRS

Maximum WAF exclusions per Application Gateway
40
200 - with CRS 3.2 or DRS

WAF string match values per match condition
10

1 The number of resources listed in the table applies to standard Application Gateway SKUs and WAF-enabled SKUs running CRS 3.2 or DRS. For WAF-enabled SKUs running CRS 3.1 or lower, the supported number is 40. For more information, see WAF engine.

2 Limit is per Application Gateway instance not per Application Gateway resource.

3 There is a 4 KB buffer on the file upload limit. The file size restriction won't be enforced until the file upload exceeds your set limit plus this buffer.

4 Must define the value via WAF Policy for Application Gateway.

### Azure Application Gateway for Containers limits

Resource
Limit

Application Gateway for Containers
1000 per subscription

Associations
1 per gateway

Frontends
5 per gateway

Kubernetes Ingress and Gateway API configuration limits

Resource
Limit

Resource naming
128 characters

Namespace naming
128 characters

Listeners per gateway
64 listeners per gateway resource (enforced by Gateway API)

Total AGC references
5 per ALB controller

Total certificate references
100 per AGC

Total listeners
200 per AGC

Total routes
200 per AGC

Total rules
200 per AGC

Total services
100 per AGC

Total endpoints
5000 per AGC

### Azure Bastion limits

An instance is an optimized Azure VM that is created when you configure Azure Bastion. When you configure Azure Bastion using the Basic SKU, 2 instances are created. If you use the Standard SKU, you can specify the number of instances between 2-50.

Workload Type*
Session Limit per Instance**

Light
25

Medium
20

Heavy
2

*These workload types are defined here: Remote Desktop workloads

**These limits are based on RDP performance tests for Azure Bastion. The numbers may vary due to other on-going RDP sessions or other on-going SSH sessions.

### Azure DNS limits

#### Public DNS

##### Public DNS zones

Resource
Limit

Public DNS zones per subscription
250 1

Record sets per public DNS zone
10,000 1

Records per record set in public DNS zone
20 1

TXT Records per record set in public DNS zone
400

Number of Alias records for a single Azure resource
50

1If you need to increase these quota limits, contact Azure Support.

##### Public DNS zone operations

Operation
Limit (per zone)

Create
40/min

Delete
40/min

Get
1000/min

List
60/min

List By Resource Group
60/min (per resource group)

Update
40/min

##### Public DNS resource record operations

Operation
Limit (per zone)

Create
200/min

Delete
200/min

Get
2000/min

List By DNS Zone
60/min

List By Type
60/min

Update
200/min

#### Private DNS

##### Private DNS zones

Resource
Limit

Private DNS zones per subscription
1000

Record sets per private DNS zone
25000

Records per record set for private DNS zones
20

Virtual Network Links per private DNS zone
1000

Virtual Networks Links per private DNS zones with autoregistration enabled
100

Number of private DNS zones a virtual network can get linked to with autoregistration enabled
1

Number of private DNS zones a virtual network can get linked
1000

##### Private DNS zone operations

Operation
Limit (per subscription)

Create
40/min

Delete
40/min

Get
200/min (per zone)

List by subscription
60/min

List by resource group
100/min (per resource group)

Update
40/min

##### Private DNS resource record operations

Operation
Limit (per zone)

Create
60/min

Delete
60/min

Get
200/min

List
100/min

Update
60/min

#### Virtual network links operations

Operation
Limit (per zone)

Create
60/min

Delete
60/min

Get
100/min

List by virtual network
20/min

Update
60/min

#### Azure-provided DNS resolver VM limits

Resource
Limit

Number of DNS queries a virtual machine can send to Azure DNS resolver, per second
1000 1

Maximum number of DNS queries queued (pending response) per virtual machine
200 1

1These limits are applied to every individual virtual machine and not at the virtual network level. DNS queries exceeding these limits are dropped. These limits apply to the default Azure resolver, not the DNS private resolver.

#### DNS Private Resolver1

Resource
Limit

DNS private resolvers per subscription
15

DNS private resolvers per virtual network
1

Inbound endpoints per DNS private resolver
5

Outbound endpoints per DNS private resolver
5

Forwarding rules per DNS forwarding ruleset
1000

Virtual network links per DNS forwarding ruleset
500

DNS forwarding ruleset linked to a virtual network
1

Outbound endpoints per DNS forwarding ruleset
2

DNS forwarding rulesets per outbound endpoint
2

Target DNS servers per forwarding rule
6

QPS per endpoint
10,000

1Different limits might be enforced by the Azure portal until the portal is updated. Use PowerShell to provision elements up to the most current limits.

### Azure Firewall limits

Resource
Limit

Azure Firewalls per virtual network
1

Max Data throughput
100 Gbps for Premium, 30 Gbps for Standard, 250 Mbps for Basic (preview) SKU

 For more information, see Azure Firewall performance.

Rule limits
20,000 unique source-destination combinations in network rules 

 Unique source-destination combinations in network rules = (number of IP protocols) Ã (number of source IP addresses) Ã (number of destination IP addresses) Ã (number of destination ports Ã· 14, rounded up to the nearest whole number)

You can track the Firewall Policy network rule count in the policy analytics under the Insights tab. As a proxy, you can also monitor your Firewall Latency Probe metrics to ensure it stays within 20 ms even during peak hours.

Total size of rules within a single Rule Collection Group
1 MB for Firewall policies created before July 2022
2 MB for Firewall policies created after July 2022

Number of Rule Collection Groups in a firewall policy
50 for Firewall policies created before July 2022
90 for Firewall policies created after July 2022

Number of firewalls referenced by a single firewall policy
50

Maximum DNAT rules (Maximum external destinations)
250 maximum [number of firewall public IP addresses + unique destinations (destination address, port, and protocol)]

 The DNAT limitation is due to the underlying platform.

For example, you can configure 500 UDP rules to the same destination IP address and port (one unique destination), while 500 rules to the same IP address but to 500 different ports exceeds the limit (500 unique destinations).

If you need more than 250, you'll need to add another firewall in a separate virtual network

Minimum AzureFirewallSubnet size
/26

Port range in network and application rules
1 - 65535

Public IP addresses
250 maximum. All public IP addresses can be used in DNAT rules and they all contribute to available SNAT ports.

IP addresses in IP Groups
It is recommended to have a maximum of 50 unique IP Groups per classic firewall. 
Maximum of 600 unique IP Groups per firewall policy.
Maximum 5000 individual IP addresses or IP prefixes per each IP Group.

Firewalls referencing a single IP Group
50 (soft limit). Exceeding this limit might affect performance and cause IP Group updates to fail.

Route table
By default, AzureFirewallSubnet has a 0.0.0.0/0 route with the NextHopType value set to Internet.

Azure Firewall must have direct Internet connectivity. If your AzureFirewallSubnet learns a default route to your on-premises network via BGP, you must override that with a 0.0.0.0/0 UDR with the NextHopType value set as Internet to maintain direct Internet connectivity. By default, Azure Firewall doesn't support forced tunneling to an on-premises network.

However, if your configuration requires forced tunneling to an on-premises network, Microsoft will support it on a case by case basis. Contact Support so that we can review your case. If accepted, we'll allow your subscription and ensure the required firewall Internet connectivity is maintained.

FQDNs in network rules
For good performance, do not exceed more than 1000 FQDNs across all network rules per firewall.

TLS inspection timeout
120 seconds

### Azure Front Door (classic) limits

In addition to the following limits, there's a composite limit on the number of routing rules, front-end domains, protocols, and paths.

Resource
Classic tier limit

Azure Front Door resources per subscription
100

Front-end hosts, which include custom domains per resource
500

Routing rules per resource
500

Rules per Rule set
25

Back-end pools per resource 2
50

Back ends per back-end pool
100

Path patterns to match for a routing rule
25

URLs in a single cache purge call
100

Maximum bandwidth 1
75 Gbps

Maximum requests per second per profile 1
100,000

HTTP header size limit (per header)
64 KB

Custom web application firewall rules per policy
100

Web application firewall policy per subscription
100

Web application firewall match conditions per custom rule
10

Web application firewall IP address ranges per custom rule
600

Web application firewall string match values per match condition
10

Web application firewall string match value length
256

Web application firewall POST body parameter name length
256

Web application firewall HTTP header name length
256

Web application firewall cookie name length
256

Web application firewall exclusion limit
100

Web application firewall HTTP request body inspection limit
128 KB

Web application firewall custom response body length
32 KB

1 If the traffic isn't globally distributed and concentrated in one or more regions, or if a higher quota limited is need, create an Azure support request.

2 To request a limit increase, create an Azure Support request. Free subscriptions including Azure Free Account and Azure for Students aren't eligible for limit or quota increases. If you have a free subscription, you can upgrade to a Pay-As-You-Go subscription.

### Azure Front Door Standard and Premium service limits

- Maximum of 500 total Standard and Premium profiles per subscription.

- In addition to the following limits, there's a composite limit on the number of routes, domains, protocols, and paths.

Resource
Standard tier limit
Premium tier limit

Maximum profiles per subscription
500
500

Maximum endpoint per profile
10
25

Maximum custom domain per profile
100
500

Maximum origin groups per profile
100
200

Maximum origins per origin group
50
50

Maximum origins per profile
100
200

Maximum origin timeout
16 - 240 secs
16 - 240 secs

Maximum routes per profile
100
200

Maximum rule set per profile
100
200

Maximum rules per route
100
100

Maximum rules per rule set
100
100

Maximum bandwidth 1
75 Gbps
75 Gbps

Maximum requests per second per profile 1, 2
100,000
100,000

Maximum concurrent WebSocket connections per profile 3
1,000,000
1,000,000

Path patterns to match for a routing rule
100
100

URLs in a single cache purge call
100
100

Maximum security policy per profile
100
200

Maximum associations per security policy
110
225

Maximum secrets per profile
100
500

Maximum key groups per profile
100
200

HTTP header size limit (total header size)
64 KB
64 KB

HTTP header size limit (total header size - Private Link Service origin)
32 KB
32 KB

Web Application Firewall (WAF) policy per subscription
100
100

WAF custom rules per policy
100
100

WAF match conditions per custom rule
10
10

WAF custom regex rules per policy
5
5

WAF IP address ranges per match conditions
600
600

WAF string match values per match condition
10
10

WAF string match value length
256
256

WAF POST body parameter name length
256
256

WAF HTTP header name length
256
256

WAF cookie name length
256
256

WAF exclusion per policy
100
100

WAF HTTP request body and file upload inspection limit
128 KB
128 KB

WAF custom response body length
32 KB
32 KB

Edge action code size 4
16 KB
16 KB

Edge action version counts 4
3
3

Edge action execution time 4
10 ms
10 ms

Maximum number of Edge Actions resources per subscription 4
100
100

1 If the traffic isn't globally distributed and concentrated in one or more regions, or if a higher quota limit is needed, create an Azure support request.

2 There's currently a 15,000 requests per second per PoP limit for each Front Door profile. Beyond this limit, the PoP location drops connections. If requests are concentrated in one or more regions and exceed this limit, you can request a higher PoP limit by submitting an Azure support request.

3 If you need more than 1,000,000 concurrent WebSocket connections, submit an Azure support request.

4 Currently, JavaScript is the only supported language.

#### Timeout values

##### From client to Front Door

- Header timeout - After establishing TCP/TLS connection, Front Door has a 5-second timeout for receiving all headers from the client. The connection is terminated if the client doesn't send headers within 5 seconds. You can't configure this timeout value.

- HTTP keep-alive timeout - Front Door has a 90-second HTTP keep-alive timeout. The connection is terminated if the client doesn't send data for 90 seconds. You can't configure this timeout value.

##### Front Door to application back-end

- After the HTTP request gets forwarded to the back end, Azure Front Door waits for 60 seconds (Standard and Premium) or 30 seconds (classic) for the first packet from the back end. Then it returns a 503 error to the client, or 504 for a cached request. You can configure this value using the originResponseTimeoutSeconds field in Azure Front Door Standard and Premium API, or the sendRecvTimeoutSeconds field in the Azure Front Door (classic) API.

- After the back end receives the first packet, if the origin pauses for any reason in the middle of the response body beyond the originResponseTimeoutSeconds or sendRecvTimeoutSeconds, the response is canceled.

- Front Door uses HTTP keep-alive to keep connections open for reuse from previous requests. These connections have an idle timeout of 90 seconds. Azure Front Door disconnects idle connections after reaching the 90-second idle timeout. You can't configure this timeout value.

#### Upload and download data limit

With chunked transfer encoding (CTE)
Without HTTP chunking

Download
There's no limit on the download size.
There's no limit on the download size.

Upload
There's no limit as long as each CTE upload is less than 2 GB.
The size can't be larger than 2 GB.

#### Other limits

- Maximum URL size - 8,192 bytes - Specifies maximum length of the raw URL (scheme + hostname + port + path + query string of the URL)

- Maximum Query String size - 4,096 bytes - Specifies the maximum length of the query string, in bytes.

- Maximum HTTP response header size from health probe URL - 4,096 bytes - Specifies the maximum length of all the response headers of health probes.

- Maximum rules engine action header value character: 640 characters.

- Maximum rules engine condition header value character: 256 characters.

- Maximum ETag header size: 128 bytes

- Maximum endpoint name for Standard and Premium: 46 characters.

For more information about limits that apply to Rules Engine configurations, see rules engine terminology.

### Azure Network Watcher limits

Resource
Limit

Network Watcher instances per region per subscription
1 (One instance in a region to enable access to the service in the region)

Connection monitors per region per subscription
100

Maximum test groups per a connection monitor
20

Maximum sources and destinations per a connection monitor
100

Maximum test configurations per a connection monitor
20

Packet capture sessions per region per subscription
10,000 (Number of sessions only, not saved captures)

VPN troubleshoot operations per subscription
1 (Number of operations at one time)

### Azure Route Server limits

Resource
Limit

Number of BGP peers
16

Number of routes each BGP peer can advertise to Azure Route Server 1
4,000

Number of VMs in the virtual network (including peered virtual networks) that Azure Route Server can support
50,000

Number of virtual networks that Azure Route Server can support
500

Number of total on-premises and Azure Virtual Network prefixes that Azure Route Server can support
10,000

1 If your NVA advertises more routes than the limit, the BGP session gets dropped.

Note

The total number of routes advertised from virtual network address space and Route Server towards ExpressRoute circuit, when Branch-to-branch enabled, must not exceed 1,000. For more information, see Route advertisement limits of ExpressRoute.

### Azure ExpressRoute limits

Resource
Limit

ExpressRoute circuits per subscription
50 (Submit a support request to increase limit)

ExpressRoute circuits per region per subscription, with Azure Resource Manager
10

Maximum number of circuits in the same peering location linked to the same virtual network
4

Maximum number of circuits in different peering locations linked to the same virtual network
Standard / ERGw1Az - 4 
 High Perf / ERGw2Az - 8 
 Ultra Performance / ErGw3Az - 16

Maximum number of IPs for ExpressRoute provider circuit with Fastpath
25,000

Maximum number of IPs for ExpressRoute Direct 10 Gbps with Fastpath
100,000

Maximum number of IPs for ExpressRoute Direct 100 Gbps with Fastpath
200,000

Maximum number of flows for ExpressRoute Traffic Collector
300,000

#### Route advertisement limits

Resource
Local / Standard SKU
Premium SKU

Maximum number of IPv4 on-prem routes advertised over Azure private peering to the ExpressRoute circuit
4,000
10,000

Maximum number of IPv6 on-prem routes advertised over Azure private peering to the ExpressRoute circuit
100
100

Maximum number of IPv4 Virtual Network routes advertised by the Gateway to the ExpressRoute circuit over Azure private peering
1,000
1,000

Maximum number of IPv6 Virtual Network routes advertised by the Gateway to the ExpressRoute circuit over Azure private peering
100
100

Maximum number of IPv4 routes advertised to Microsoft peering from on-premises
200
200

Maximum number of IPv6 routes advertised to Microsoft peering from on-premises
200
200

#### Virtual networks links allowed for each ExpressRoute circuit limit

Circuit size
Local / Standard SKU
Premium SKU

50 Mbps
10
20

100 Mbps
10
25

200 Mbps
10
25

500 Mbps
10
40

1 Gbps
10
50

2 Gbps
10
60

5 Gbps
10
75

10 Gbps
10
100

40 Gbps*
10
100

100 Gbps*
10
100

*100-Gbps ExpressRoute Direct Only

Note

Global Reach connections count against the limit of virtual network connections per ExpressRoute Circuit. For example, a 10 Gbps Premium Circuit would allow for 5 Global Reach connections and 95 connections to the ExpressRoute Gateways or 95 Global Reach connections and 5 connections to the ExpressRoute Gateways or any other combination up to the limit of 100 connections for the circuit.

#### ExpressRoute gateway performance limits

The following tables provide an overview of the different types of gateways, their respective limitations, and their expected performance metrics.

#### Maximum supported limits

This table applies to both the Azure Resource Manager and classic deployment models.

Gateway SKU
Megabits per second
Packets per second
Supported number of VMs in the virtual network 1
Flow count limit
Number of routes learned by gateway

Standard/ERGw1Az
1,000
100,000
2,000
200,000
4,000

High Performance/ERGw2Az
2,000
200,000
4,500
400,000
9,500

Ultra Performance/ErGw3Az
10,000
1,000,000
11,000
1,000,000
9,500

ErGwScale (per scale unit 1-10)
1,000 per scale unit
100,000 per scale unit
2,000 per scale unit
100,000 per scale unit
9,500 total per gateway

ErGwScale (per scale unit 11-40)
1,000 per scale unit
200,000 per scale unit
1,000 per scale unit
100,000 per scale unit
9,500 total per gateway

1 "Supported number of VMs in the virtual network" refers to the count of resources that communicate through the gateway. This includes:

- Virtual Machines in the hub virtual network

- Virtual Machines in peered spoke virtual networks (Hub-Spoke topology)

- Private Endpoints

- Network Virtual Appliances (such as Application Gateway, Azure Firewall)

- Backend instances of PaaS services deployed in virtual networks (such as SQL Managed Instance, App Service Environment, Azure API Management in VNet mode)

The values in the table are estimates and vary depending on the CPU utilization of the gateway. If the CPU utilization is high and the number of supported VMs is exceeded, the gateway will start to drop packets.

Note

ExpressRoute can facilitate up to 11,000 routes that span virtual network address spaces, on-premises networks, and any relevant virtual network peering connections. To ensure stability of your ExpressRoute connection, refrain from advertising more than 11,000 routes to ExpressRoute. The maximum number of routes advertised by gateway is 1,000 routes.

Important

- Application performance depends on multiple factors, such as end-to-end latency and the number of traffic flows that the application opens. The numbers in the table represent the upper limit that the application can theoretically achieve in an ideal environment. Additionally, we perform routine host and OS maintenance on the ExpressRoute virtual network gateway, to maintain reliability of the service. During a maintenance period, the control plane and data path capacity of the gateway is reduced.

- During a maintenance period, you might experience intermittent connectivity problems to private endpoint resources.

- ExpressRoute supports a maximum TCP and UDP packet size of 1,400 bytes. Fragmented packets are not supported by ExpressRoute Gateways. Please adjust your application to prevent IP fragmentation. If IP fragmentation support is required, enable the ExpressRoute FastPath feature to bypass the ExpressRoute gateway.

- Azure Route Server can support up to 4,000 VMs. This limit includes VMs in virtual networks that are peered. For more information, see Azure Route Server limitations.

- The values in the table above represent the limits at each Gateway SKU.

### Azure NAT Gateway limits

The following limits apply to Standard and StandardV2 NAT gateway resources managed through Azure Resource Manager per region per subscription. Learn how to view your current resource usage against your subscription limits.

Note

Each subscription has a combined quota for both Standard and StandardV2 NAT gateways. For example, if your subscription has a quota of 100 NAT gateways, you can create any combination of Standard and StandardV2 NAT gateways up to that quota.

Resource
Standard SKU
StandardV2 SKU

Public IP addresses
16 IPv4 addresses
16 IPv4 addresses, 16 IPv6 addresses

Subnets
800 per NAT gateway
800 per NAT gateway

Data throughput1
50 Gbps per NAT gateway
100 Gbps per NAT gateway, 1 Gbps per connection

NAT gateways for Enterprise and CSP agreements2
1,000 per subscription per region
see previous column for combined quota

NAT gateways for Sponsored and pay-as-you-go2
100 per subscription per region
see previous column for combined quota

NAT gateways for Free Trial and all other offer types2
15 per subscription per region
see previous column for combined quota

Packets processed
5 million packets per second per NAT gateway, split across directions (2.5 million PPS outbound and 2.5 million PPS return traffic)
10M packets per second per NAT Gateway, 100,000 PPS per connection

Connections to same destination endpoint
50,000 connections to the same destination per public IP
50,000 connections to the same destination per public IP

Connections total
2M connections per NAT gateway
2M connections per NAT gateway

1 For a Standard SKU NAT gateway resource, the total data throughput of 50 Gbps is split between outbound and inbound (return) data. Data throughput is supported up to 25 Gbps for outbound data and up to 25 Gbps for inbound (response) data through NAT gateway.

2 Default limits for NAT gateways vary by offer category type, such as Free Trial, pay-as-you-go, and CSP. For example, the default for Enterprise Agreement subscriptions is 1000.

### Azure Private Link limits

The following limits apply to Azure private link:

Resource
Limit

Number of private endpoints per virtual network
1000

Number of private endpoints across peered virtual networks
4000

Number of private endpoints per subscriptionâ¯â¯â¯ â¯
64000

Number of private link services per subscription â¯â¯â¯â¯â¯
800

Number of private link services per Standard Load Balancer â¯â¯â¯â¯â¯
8

Number of IP Configurations on a private link service â¯â¯
8 (This number is for the NAT IP addresses used per PLS)

Number of private endpoints on the same private link serviceâ¯
1000

Number of subscriptions allowed in visibility setting on private link serviceâ¯
100

Number of subscriptions allowed in auto-approval setting on private link serviceâ¯
100

Number of private endpoints per key vault
64

Number of private DNS zone groups that can be linked to a private endpoint
1

Number of DNS zones in each group
5

Number of private IP addresses on private endpoint network interface â¯â¯
500

### Azure Traffic Manager limits

#### Resource limits

Resource
Limit

Profiles per subscription
200 1

Endpoints per profile
200

1If you need to increase these limits, contact Azure Support.

#### Default throttling limits

##### Profiles

Operation
Limit (per minute)

Create/update
600

Get
450

Delete
150

List in resource group or subscription
450

Check DNS name availability
300

##### Endpoints

Operation
Limit (per minute)

Create/update/delete
300

Get
1500

##### Metrics & heatmap

Operation
Limit (per minute)

Get/create/delete user metrics key
150

Get heat map
150

##### Geo hierarchy

Operation
Limit (per minute)

Get
150

### Azure VPN Gateway limits

Unless stated otherwise, the following limits apply to Azure VPN Gateway resources and virtual network gateways.

Resource
Limit

VNet Address Prefixes
600 per VPN gateway

Aggregate BGP routes
4,000 per VPN gateway

Local Network Gateway address prefixes
1000 per local network gateway

S2S connections
Limit depends on the gateway SKU. See the Limits by gateway SKU table.

P2S connections
Limit depends on the gateway SKU. See the Limits by gateway SKU table.

P2S route limit - IKEv2
256 for non-Windows / 25 for Windows

P2S route limit - OpenVPN
1000

Max. flows
500K inbound and 500K outbound for VpnGw1-5/AZ

Traffic Selector Policies
100

Custom APIPA BGP addresses
32

Supported number of VMs in the virtual network
Limit depends on the gateway SKU. See the Limits by gateway SKU table.

#### Limits by gateway SKU

The following SKUs can be used to deploy new VPN gateways. They have zone-redundant options and are recommended for all new deployments.

VPN
Gateway
Generation
SKU
S2S/VNet-to-VNet
Tunnels
P2S
 SSTP Connections
P2S
 IKEv2/OpenVPN Connections
Aggregate
Throughput Benchmark
BGP
Zone-redundant
Supported Number of VMs in the Virtual Network

Generation1
Basic
Max. 10
Max. 128
IKEv2 supported; OpenVPN not supported
100 Mbps
Not Supported
No
200

Generation1
VpnGw1AZ
Max. 30
Max. 128
Max. 250
650 Mbps
Supported
Yes
1000

Generation1
VpnGw2AZ
Max. 30
Max. 128
Max. 500
1 Gbps
Supported
Yes
2000

Generation1
VpnGw3AZ
Max. 30
Max. 128
Max. 1000
1.25 Gbps
Supported
Yes
5000

Generation2
VpnGw2AZ
Max. 30
Max. 128
Max. 500
1.25 Gbps
Supported
Yes
2000

Generation2
VpnGw3AZ
Max. 30
Max. 128
Max. 1000
2.5 Gbps
Supported
Yes
3300

Generation2
VpnGw4AZ
Max. 100*
Max. 128
Max. 5000
5 Gbps
Supported
Yes
4400

Generation2
VpnGw5AZ
Max. 100*
Max. 128
Max. 10000
10 Gbps
Supported
Yes
9000

VpnGw1~5 are slated for migration and should not be used to create new VPN gateways. For more information, see VPN Gateway SKU consolidation and migration.

VPN
Gateway
Generation
SKU
S2S/VNet-to-VNet
Tunnels
P2S
 SSTP Connections
P2S
 IKEv2/OpenVPN Connections
Aggregate
Throughput Benchmark
BGP
Zone-redundant
Supported Number of VMs in the Virtual Network

Generation1
VpnGw1
Max. 30
Max. 128
Max. 250
650 Mbps
Supported
No
450

Generation1
VpnGw2
Max. 30
Max. 128
Max. 500
1 Gbps
Supported
No
1300

Generation1
VpnGw3
Max. 30
Max. 128
Max. 1000
1.25 Gbps
Supported
No
4000

Generation2
VpnGw2
Max. 30
Max. 128
Max. 500
1.25 Gbps
Supported
No
685

Generation2
VpnGw3
Max. 30
Max. 128
Max. 1000
2.5 Gbps
Supported
No
2240

Generation2
VpnGw4
Max. 100*
Max. 128
Max. 5000
5 Gbps
Supported
No
5300

Generation2
VpnGw5
Max. 100*
Max. 128
Max. 10000
10 Gbps
Supported
No
6700

Note

"Supported Number of VMs in the Virtual Network" refers to the count of resources that communicate through the gateway. This includes:

- Virtual Machines in the hub and peered spoke virtual networks

- Private Endpoints

- Network Virtual Appliances (such as Application Gateway, Azure Firewall)

- Backend instances of PaaS services deployed in virtual networks (such as SQL Managed Instance, App Service Environment)

For more information about gateway SKUs and limits, see About gateway SKUs.

#### Gateway performance limits

The table in this section lists the results of performance tests for VpnGw SKUs. A VPN tunnel connects to a VPN gateway instance. Each instance throughput is mentioned in the throughput table in the previous section and is available aggregated across all tunnels connecting to that instance. The table shows the observed bandwidth and packets per second throughput per tunnel for the different gateway SKUs. All testing was performed between gateways (endpoints) within Azure across different regions with 100 connections and under standard load conditions. We used publicly available iPerf and CTSTraffic tools to measure performances for site-to-site connections

- The best performance was obtained when we used the GCMAES256 algorithm for both IPsec Encryption and Integrity.

- Average performance was obtained when using AES256 for IPsec Encryption and SHA256 for Integrity.

- The lowest performance was obtained when we used DES3 for IPsec Encryption and SHA256 for Integrity.

Generation
SKU
Algorithms
used
Throughput
observed per tunnel
Packets per second per tunnel
observed

Generation1
VpnGw1
GCMAES256
AES256 & SHA256
DES3 & SHA256
650 Mbps
500 Mbps
130 Mbps
62,000
47,000
12,000

Generation1
VpnGw2
GCMAES256
AES256 & SHA256
DES3 & SHA256
1.2 Gbps
650 Mbps
140 Mbps
100,000
61,000
13,000

Generation1
VpnGw3
GCMAES256
AES256 & SHA256
DES3 & SHA256
1.25 Gbps
700 Mbps
140 Mbps
120,000
66,000
13,000

Generation1
VpnGw1AZ
GCMAES256
AES256 & SHA256
DES3 & SHA256
650 Mbps
500 Mbps
130 Mbps
62,000
47,000
12,000

Generation1
VpnGw2AZ
GCMAES256
AES256 & SHA256
DES3 & SHA256
1.2 Gbps
650 Mbps
140 Mbps
110,000
61,000
13,000

Generation1
VpnGw3AZ
GCMAES256
AES256 & SHA256
DES3 & SHA256
1.25 Gbps
700 Mbps
140 Mbps
120,000
66,000
13,000

Generation2
VpnGw2
GCMAES256
AES256 & SHA256
DES3 & SHA256
1.25 Gbps
550 Mbps
130 Mbps
120,000
52,000
12,000

Generation2
VpnGw3
GCMAES256
AES256 & SHA256
DES3 & SHA256
1.5 Gbps
700 Mbps
140 Mbps
140,000
66,000
13,000

Generation2
VpnGw4
GCMAES256
AES256 & SHA256
DES3 & SHA256
2.3 Gbps
700 Mbps
140 Mbps
220,000
66,000
13,000

Generation2
VpnGw5
GCMAES256
AES256 & SHA256
DES3 & SHA256
2.3 Gbps
700 Mbps
140 Mbps
220,000
66,000
13,000

Generation2
VpnGw2AZ
GCMAES256
AES256 & SHA256
DES3 & SHA256
1.25 Gbps
550 Mbps
130 Mbps
120,000
52,000
12,000

Generation2
VpnGw3AZ
GCMAES256
AES256 & SHA256
DES3 & SHA256
1.5 Gbps
700 Mbps
140 Mbps
140,000
66,000
13,000

Generation2
VpnGw4AZ
GCMAES256
AES256 & SHA256
DES3 & SHA256
2.3 Gbps
700 Mbps
140 Mbps
220,000
66,000
13,000

Generation2
VpnGw5AZ
GCMAES256
AES256 & SHA256
DES3 & SHA256
2.3 Gbps
700 Mbps
140 Mbps
220,000
66,000
13,000

### Azure Virtual WAN limits

Resource
Limit

VPN (branch) connections per hub
1,000

Aggregate throughput per Virtual WAN Site-to-site VPN gateway
20 Gbps

Throughput per Virtual WAN VPN connection (2 tunnels)
2 Gbps with 1 Gbps/IPsec tunnel

Point-to-site users per hub
100,000

Aggregate throughput per Virtual WAN User VPN (Point-to-site) gateway
200 Gbps

Aggregate throughput per Virtual WAN ExpressRoute gateway
20 Gbps

ExpressRoute circuit connections per hub
8 - Read more here

VNet connections per hub without Routing Intent enabled
500 minus total number of hubs in Virtual WAN

Address spaces across all VNets directly connected to single hub with Routing Intent with private routing policies enabled
600 per Virtual WAN hub - Read more here

Aggregate throughput per Virtual WAN hub router
50 Gbps for VNet to VNet transit

VM workload across all VNets connected to a single Virtual WAN hub
2000 (If you want to raise the limit or quota above the default limit, see hub settings).

Total number of routes the hub can accept from its connected resources (virtual networks, branches, other virtual hubs, etc.)
10,000

## Azure Notification Hubs limits

Tier
Free
Basic
Standard

Included pushes
1 million
10 million
10 million

Active devices
500
200,000
10 million

Tag quota per installation or registration
60
60
60

For more information on limits and pricing, see Notification Hubs pricing.

## Microsoft Dev Box limits

Subscription type
VM Cores
Network Connections
Dev centers
Dev box definitions
Dev box projects

Pay as you go
20
5
2
200
500

Azure Pass
20
5
2
200
500

CSP
20
5
2
200
500

Free trial
0
0
0
0
0

Azure for Students
0
0
0
0
0

Enterprise
80
10
5
200
500

MSDN
n/a
5
2
200
500

## Microsoft Entra service limits

See Microsoft Entra service limits for Microsoft Entra service limits.

## Microsoft Purview limits

See Classic Microsoft Purview data governance limits for the most current Microsoft Purview quotas.

## Microsoft Sentinel limits

See Service limits for Microsoft Sentinel for Microsoft Sentinel limits.

## Azure Service Bus limits

The following table lists quota information specific to Azure Service Bus messaging. For information about pricing and other quotas for Service Bus, see Service Bus pricing.

### Common limits for all tiers

The following limits are common across all tiers.

Quota name
Value
Notes

Maximum number of namespaces per Azure subscription per region
1000 (default and maximum)
This limit is based on the `Microsoft.ServiceBus` provider, not based on the tier. Therefore, it's the total number of namespaces across all tiers. Subsequent requests for additional namespaces are rejected.

Number of concurrent connections on a namespace
AMQP: 5,000.
Subsequent requests for additional connections are rejected. REST operations don't count toward concurrent TCP connections.

Number of concurrent receive requests on a queue, topic, or subscription entity
5,000
Subsequent receive requests are rejected with a server busy error. This quota applies to the combined number of concurrent receive operations across all subscriptions on a topic. For more information, see Throttling when concurrent receive requests exceed the limit.

Maximum size of any messaging entity path: queue or topic
260 characters.
 

Maximum size of any messaging entity name: namespace, subscription, or subscription rule
50 characters.
 

Maximum size of a message ID
128
 

Maximum number of session states per messaging entity: queue or subscription
1,000,000
 

Maximum size of a message session ID
128
 

Message property size for a queue, topic, or subscription entity
Maximum message property size for each property is 32 KB.
Cumulative size of all properties can't exceed 64 KB. This limit applies to the entire header of the brokered message, which has both user properties and system properties, such as sequence number, label, and message ID.
Maximum number of header properties in property bag: byte/int.MaxValue.

The exception `SerializationException` is generated.

Number of SQL filters per topic
2,000
Subsequent requests for creation of additional filters on the topic are rejected, and the calling code receives an exception.

Number of correlation filters per topic
100,000
Subsequent requests for creation of additional filters on the topic are rejected, and the calling code receives an exception.

Size of SQL filters or actions
Maximum length of filter condition string: 1,024 (1 K).

Maximum length of rule action string: 1,024 (1 K).

Maximum number of expressions per rule action: 32.
Subsequent requests for creation of additional filters are rejected, and the calling code receives an exception.

Number of shared access authorization rules per namespace, queue, or topic
Maximum number of rules per entity type: 12. 

 Rules that are configured on a Service Bus namespace apply to all types: queues, topics.
Subsequent requests for creation of additional rules are rejected, and the calling code receives an exception.

Number of messages per transaction
100 

 For both Send() and SendAsync() operations.
Additional incoming messages are rejected, and the calling code receives an exception with the message: Can't send more than 100 messages in a single transaction.

Maximum number of messages deleted in DeleteMessagesAsync call
500
The DeleteMessagesAsync API supports deleting up to 500 messages per call. Requests exceeding this limit (e.g., 4000) will throw an ArgumentOutOfRangeException.

Maximum number of messages returned in PeekMessagesAsync call
250

Number of virtual network and IP filter rules
128
 

### Basic vs. standard vs. premium tiers

The following table shows limits that are different for Basic, Standard, and Premium tiers.

Quota name
Basic
Standard
Premium
Notes

Queue or topic size
1, 2, 3, 4 GB, or 5 GB

80 GB, if partitioning is enabled.
1, 2, 3, 4 GB, or 5 GB

80 GB, if partitioning is enabled.
80 GB
You can configure and update after creation the maximum size. Choose from the supported values shown, up to a maximum of 80 GB, which is the largest supported value and can't be increased beyond it. Sizes above 5 GB require partitioning on the Basic and Standard tiers. The Premium tier supports 80 GB natively. The total size of all entities in a namespace can't exceed the namespace size limit documented in the next row.
Subsequent incoming messages are rejected, and the calling code receives an exception.
 A large message (size > 1 MB) sent to a queue is counted twice. A large message (size > 1 MB) sent to a topic is counted X + 1 times, where X is the number of subscriptions whose filter condition matches the message. 

Namespace size
400 GB
400 GB
1 TB per messaging unit (MU).
Total size of all entities in a namespace can't exceed this limit.

Number of topics or queues per namespace
10,000
10,000
1,000 per messaging unit (MU), up to 16,000 per namespace.
Subsequent requests for creation of a new topic or queue on the namespace are rejected. As a result, if configured through the Azure portal, an error message is generated. If called from the management API, the calling code receives an exception.

Number of partitioned topics or queues per namespace
100
100
N/A
Each partitioned queue or topic counts toward the quota of 1,000 entities per namespace. Subsequent requests for creation of a new partitioned topic or queue in the namespace are rejected. As a result, if configured through the Azure portal, an error message is generated. If called from the management API, the exception QuotaExceededException is received by the calling code.
 If you want to have more partitioned entities in a basic or a standard tier namespace, create additional namespaces.
The Premium tier uses namespace-level partitioning instead, which is configured during namespace creation.

Number of Premium namespace partitions
N/A
N/A
1, 2, or 4
Set during namespace creation and can't be changed afterward. The number of messaging units must be a multiple of the number of partitions. MUs are distributed equally across partitions. For more information, see Enable partitioning for a Premium namespace.

Message size or batch size for a queue, topic, or subscription entity
256 KB
256 KB
AMQP protocol: Up to 100 MB for single message.

HTTP protocol: Up to 1 MB for single message.

All protocols: Up to 1 MB for message batch.
The message size includes the size of properties (system and user) and the size of payload. The size of system properties varies depending on your scenario. Incoming messages that exceed these quotas are rejected, and the calling code receives an exception.For Premium, the default maximum message size per entity is 1 MB. You can increase it up to 100 MB per queue or topic when using AMQP. For more information, see Large messages support.

Number of subscriptions per topic
2,000
2,000
2,000
Subsequent requests for creating additional subscriptions for the topic are rejected. As a result, if configured through the portal, an error message is shown. If called from the management API, the calling code receives an exception.

Operations per second
1,000
1,000
N/A
Premium doesn't have fixed limitations on the operations per second. The throughput varies depending on the number of MUs and the characteristics of the workload. For more information on how the workload impacts the throughput, and how to optimize this, see Best Practices for performance improvements using Service Bus Messaging.

## Azure Site Recovery limits

The following limits apply to Azure Site Recovery.

Limit identifier
Limit

Number of vaults per subscription
500

Number of protected disks per subscription (Both Data and OS)
3000

Number of appliances per Recovery Services vault
250

Number of protection groups per Recovery Services vault
No limit

Number of recovery plans per Recovery Services vault
No limit

Number of servers per protection group
No limit

Number of servers per recovery plan
100

## Azure SQL Database limits

For Azure SQL Database limits see:

- Overview of Azure SQL Managed Instance resource limits

- Resource limits for single databases using the vCore purchasing model

- Resource limits for elastic pools using the vCore purchasing model

The maximum number of private endpoints per Azure SQL Database logical server is 250.

## Azure Synapse Analytics limits

Azure Synapse Analytics has the following default limits to ensure customer's subscriptions are protected from each other's workloads. To raise the limits to the maximum for your subscription, contact support.

### Azure Synapse limits for workspaces

For Pay-As-You-Go, Free Trial, Azure Pass, and Azure for Students subscription offer types:

Resource
Default limit
Maximum limit

Synapse workspaces in an Azure subscription
2
2

For other subscription offer types:

Resource
Default limit
Maximum limit

Synapse workspaces in an Azure subscription per region
20
100

### Azure Synapse limits for Apache Spark

For Pay-As-You-Go, Free Trial, Azure Pass, and Azure for Students subscription offer types:

Resource
Memory Optimized cores
GPU cores

Spark cores in a Synapse workspace
12
48

For other subscription offer types:

Resource
Memory Optimized cores
GPU cores

Spark cores in a Synapse workspace
50
50

For additional limits for Spark pools, see Concurrency and API rate limits for Apache Spark pools in Azure Synapse Analytics.

### Azure Synapse limits for pipelines

Resource
Default limit
Maximum limit

Synapse pipelines in a Synapse workspace
800
800

Total number of entities, such as pipelines, data sets, triggers, linked services, Private Endpoints, and integration runtimes, within a workspace
5,000
5,000

Total CPU cores for Azure-SSIS Integration Runtimes under one workspace
256
Find out how to request a quota increase from support.

Concurrent pipeline runs per workspace that's shared among all pipelines in the workspace
10,000
10,000

Concurrent External activity runs per workspace per Azure Integration Runtime region
External activities are managed on integration runtime but execute on linked services, including Databricks, stored procedure, HDInsight, Web, and others. This limit doesn't apply to Self-hosted IR.
3,000
3,000

Concurrent Pipeline activity runs per workspace per Azure Integration Runtime region 
Pipeline activities execute on integration runtime, including Lookup, GetMetadata, and Delete. This limit doesn't apply to Self-hosted IR.
1,000
1,000

Concurrent authoring operations per workspace per Azure Integration Runtime region
Including test connection, browse folder list and table list, preview data. This limit doesn't apply to Self-hosted IR.
200
200

Concurrent Data Integration Units1 consumption per workspace per Azure Integration Runtime region
Region group 12: 6,000
Region group 22: 3,000
Region group 32: 1,500
Managed virtual network2: 2,0
Region group 12: 6,000
Region group 22: 3,000
Region group 32: 1,500

Concurrent Data Integration Units1 consumption per subscription per Azure Integration Runtime region in managed virtual network
2,0
2,0

Maximum activities per pipeline, which includes inner activities for containers
120
120

Maximum number of linked integration runtimes that can be created against a single self-hosted integration runtime
100
100

Maximum parameters per pipeline
50
50

ForEach items
100,000
100,000

ForEach parallelism
20
50

Maximum queued runs per pipeline
100
100

Characters per expression
8,192
8,192

Minimum tumbling window trigger interval
5 min
15 min

Maximum timeout for pipeline activity runs
7 days
7 days

Bytes per object for pipeline objects3
200 KB
200 KB

Bytes per object for dataset and linked service objects3
100 KB
2,000 KB

Bytes per payload for each activity run4
896 KB
896 KB

Data Integration Units1 per copy activity run
256
256

Write API calls
1,200/h
1,200/h

 This limit is imposed by Azure Resource Manager, not Azure Synapse Analytics.

Read API calls
12,500/h
12,500/h

 This limit is imposed by Azure Resource Manager, not Azure Synapse Analytics.

Monitoring queries per minute
1,000
1,000

Maximum time of data flow debug session
8 hrs
8 hrs

Concurrent number of data flows per integration runtime
50
50

Concurrent number of data flows per integration runtime in managed vNet
20
20

Concurrent number of data flow debug sessions per user per workspace
3
3

Data Flow Azure IR TTL limit
4 hrs
4 hrs

Meta Data Entity Size limit in a workspace
2 GB
2 GB

1 The data integration unit (DIU) is used in a cloud-to-cloud copy operation, learn more from Data integration units (version 2). For information on billing, see Azure Synapse Analytics Pricing.

2 Azure Integration Runtime is globally available to ensure data compliance, efficiency, and reduced network egress costs.

Region group
Regions

Region group 1
Central US, East US, East US 2, North Europe, West Europe, West US, West US 2

Region group 2
Australia East, Australia Southeast, Brazil South, Central India, Japan East, North Central US, South Central US, Southeast Asia, West Central US

Region group 3
Other regions

If managed virtual network is enabled, the data integration unit (DIU) in all region groups are 2,400.

3 Pipeline, data set, and linked service objects represent a logical grouping of your workload. Limits for these objects don't relate to the amount of data you can move and process with Azure Synapse Analytics. Synapse Analytics is designed to scale to handle petabytes of data.

4 The payload for each activity run includes the activity configuration, the associated dataset(s), and linked service(s) configurations if any, and a small portion of system properties generated per activity type. Limit for this payload size doesn't relate to the amount of data you can move and process with Azure Synapse Analytics. Learn about the symptoms and recommendation if you hit this limit.

### Azure Synapse limits for dedicated SQL pools

For details of capacity limits for dedicated SQL pools in Azure Synapse Analytics, see dedicated SQL pool resource limits.

### Azure Resource Manager limits for web service calls

Azure Resource Manager has limits for API calls. You can make API calls at a rate within the Azure Resource Manager API limits.

### Azure virtual machine disk limits

You can attach a number of data disks to an Azure virtual machine (VM). Based on the scalability and performance targets for a VM's data disks, you can determine the number and type of disk that you need to meet your performance and capacity requirements.

Important

For optimal performance, limit the number of highly utilized disks attached to the virtual machine to avoid possible throttling. If all attached disks aren't highly utilized at the same time, the virtual machine can support a larger number of disks. Additionally, when creating a managed disk from an existing managed disk, only 49 disks can be created concurrently. More disks can be created after some of the initial 49 are created.

For Azure managed disks:

The following table illustrates the default and maximum limits of the number of resources per region per subscription. The limits remain the same irrespective of disks encrypted with either platform-managed keys or customer-managed keys. There's no limit for the number of Managed Disks, snapshots and images per resource group.

Resource
Limit

Standard managed disks
50,000

Standard SSD managed disks
50,000

Premium SSD managed disks
50,000

Premium SSD v2 managed disks
1,0003, 5,000

Total Premium SSD v2 managed disks capacity in GiB2
102,4003,1,048,576

Ultra disks
1,000

Total Ultra Disk capacity in GiB2
102,400

Standard_LRS snapshots1
75,000

Standard_ZRS snapshots1
75,000

Managed image
50,000

1An individual disk can have 500 incremental snapshots.

2This is the default max but higher capacities are supported by request. To request an increase in capacity, request a quota increase or contact Azure Support.

3These smaller limits only apply to the following regions: Europe North, UK South, US East, US East 2, US West 2.

For standard storage accounts:

A Standard storage account has a maximum total request rate of 20,000 IOPS. The total IOPS across all of your virtual machine disks in a Standard storage account shouldn't exceed this limit.

For unmanaged disks, you can roughly calculate the number of highly utilized disks supported by a single standard storage account based on the request rate limit. For example, for a Basic tier VM, the maximum number of highly utilized disks is about 66, which is 20,000/300 IOPS per disk. The maximum number of highly utilized disks for a Standard tier VM is about 40, which is 20,000/500 IOPS per disk.

For premium storage accounts:

A premium storage account has a maximum total throughput rate of 50 Gbps. The total throughput across all of your VM disks shouldn't exceed this limit.

See sizes for virtual machines in Azure for more information.

For VM Applications

When working with VM applications in Azure, you may encounter an error message that says "Operation could not be completed as it results in exceeding approved UnmanagedStorageAccountCount quota." This error occurs when you have reached the limit for the number of unmanaged storage accounts that you can use.

When you publish a VM application, Azure needs to replicate it across multiple regions. To do this, Azure creates an unmanaged storage account for each region. The number of unmanaged storage accounts that an application uses is determined by the number of replicas across all applications.

As a general rule, each storage account can accommodate up to 200 simultaneous connections. Below are options for resolving the "UnmanagedStorageAccountCount" error:

- Use page blobs for your source application blobs. Unmanaged accounts are only used for block blob replication. Page blobs have no such limits.

- Reduce the number of replicas for your VM Application versions or delete applications you no longer need.

- File a support request to obtain a quota increase.

See VM Applications overview for more information.

#### Azure disk encryption sets

Each region and subscription supports up to 5,000 disk encryption sets. Contact Azure support to increase the quota.

See the following documentation to learn more about encryption restrictions:

- Linux

- Windows virtual machines

### Azure managed disks

### Standard HDD managed disks

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

### Standard SSD managed disks

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

### Premium SSD managed disks: Per-disk limits

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

### Premium SSD v2 managed disks

Unlike Premium SSDs, Premium SSD v2 doesn't have dedicated sizes. You can set a Premium SSD v2 to any supported size you prefer, and make granular adjustments to the performance without downtime.

Disk Size
Maximum available IOPS
Maximum available throughput (MB/s)

1 GiB-64 TiBs
3,000-80,000 (Increases by 500 IOPS per GiB)
125-2,000 (increases by 0.25 MB/s per set IOPS)

### Ultra Disks

Ultra Disk sizes work like Premium SSD, Standard SSD, and Standard HDD sizes. When you create or modify an Ultra Disk, the size you set is billed as the next largest provisioned disk size. So if you deploy a 200 GiB Ultra Disk or set a 200 GiB Ultra Disk, you'd have a 200 GiB Ultra Disk that's billed as if it was 256 GiB, since that's the next largest provisioned disk size.

The following table provides a comparison of disk sizes and performance caps to help you decide which to use.

Disk Size (GiB)
IOPS Cap
Throughput Cap (MB/s)

4
1,200
300

8
2,400
600

16
4,800
1,200

32
9,600
2,400

64
19,200
4,900

128
38,400
9,800

256
76,800
10,000

512
153,600
10,000

1,024
307,200
10,000

2,048-65,536 (sizes in this range increasing in increments of 1 TiB)
400,000
10,000

### Unmanaged virtual machine disks

Standard unmanaged virtual machine disks: Per-disk limits

VM tier
Basic tier VM
Standard tier VM

Disk size
4,095 GB
4,095 GB

Maximum 8-KB IOPS per persistent disk
300
500

Maximum number of disks that perform the maximum IOPS
66
40

Premium unmanaged virtual machine disks: Per-account limits

Resource
Limit

Total disk capacity per account
35 TB

Total snapshot capacity per account
10 TB

Maximum bandwidth per account (ingress + egress)1
<=50 Gbps

1Ingress refers to all data from requests that are sent to a storage account. Egress refers to all data from responses that are received from a storage account.

Premium unmanaged virtual machine disks: Per-disk limits

Premium storage disk type
P10
P20
P30
P40
P50

Disk size
128 GiB
512 GiB
1,024 GiB (1 TB)
2,048 GiB (2 TB)
4,095 GiB (4 TB)

Maximum IOPS per disk
500
2,300
5,000
7,500
7,500

Maximum throughput per disk
100 MB/sec
150 MB/sec
200 MB/sec
250 MB/sec
250 MB/sec

Maximum number of disks per storage account
280
70
35
17
8

Premium unmanaged virtual machine disks: Per-VM limits

Resource
Limit

Maximum IOPS per VM
80,000 IOPS with GS5 VM

Maximum throughput per VM
2,000 MB/sec with GS5 VM

## Azure StorSimple System limits

Limit identifier
Limit
Comments

Maximum number of storage account credentials
64

Maximum number of volume containers
64

Maximum number of volumes
255

Maximum number of schedules per bandwidth template
168
A schedule for every hour, every day of the week.

Maximum size of a tiered volume on physical devices
64 TB for StorSimple 8100 and StorSimple 8600
StorSimple 8100 and StorSimple 8600 are physical devices.

Maximum size of a tiered volume on virtual devices in Azure
30 TB for StorSimple 8010 

 64 TB for StorSimple 8020
StorSimple 8010 and StorSimple 8020 are virtual devices in Azure that use Standard storage and Premium storage, respectively.

Maximum size of a locally pinned volume on physical devices
9 TB for StorSimple 8100 

 24 TB for StorSimple 8600
StorSimple 8100 and StorSimple 8600 are physical devices.

Maximum number of iSCSI connections
512

Maximum number of iSCSI connections from initiators
512

Maximum number of access control records per device
64

Maximum number of volumes per backup policy
24

Maximum number of backups retained per backup policy
64

Maximum number of schedules per backup policy
10

Maximum number of snapshots of any type that can be retained per volume
256
This amount includes local snapshots and cloud snapshots.

Maximum number of snapshots that can be present in any device
10,000

Maximum number of volumes that can be processed in parallel for backup, restore, or clone
16

- If there are more than 16 volumes, they're processed sequentially as processing slots become available.

- New backups of a cloned or a restored tiered volume can't occur until the operation is finished. For a local volume, backups are allowed after the volume is online.

Restore and clone recover time for tiered volumes
<2 minutes

- The volume is made available within 2 minutes of a restore or clone operation, regardless of the volume size.

- The volume performance might initially be slower than normal as most of the data and metadata still resides in the cloud. Performance might increase as data flows from the cloud to the StorSimple device.

- The total time to download metadata depends on the allocated volume size. Metadata is automatically brought into the device in the background at the rate of 5 minutes per TB of allocated volume data. This rate might be affected by Internet bandwidth to the cloud.

- The restore or clone operation is complete when all the metadata is on the device.

- Backup operations can't be performed until the restore or clone operation is fully complete.

Restore recover time for locally pinned volumes
<2 minutes

- The volume is made available within 2 minutes of the restore operation, regardless of the volume size.

- The volume performance might initially be slower than normal as most of the data and metadata still resides in the cloud. Performance might increase as data flows from the cloud to the StorSimple device.

- The total time to download metadata depends on the allocated volume size. Metadata is automatically brought into the device in the background at the rate of 5 minutes per TB of allocated volume data. This rate might be affected by Internet bandwidth to the cloud.

- Unlike tiered volumes, if there are locally pinned volumes, the volume data is also downloaded locally on the device. The restore operation is complete when all the volume data has been brought to the device.

- The restore operations might be long and the total time to complete the restore will depend on the size of the provisioned local volume, your Internet bandwidth, and the existing data on the device. Backup operations on the locally pinned volume are allowed while the restore operation is in progress.

Thin-restore availability
Last failover

Maximum client read/write throughput, when served from the SSD tier*
920/720 MB/sec with a single 10-gigabit Ethernet network interface
Up to two times with MPIO and two network interfaces.

Maximum client read/write throughput, when served from the HDD tier*
120/250 MB/sec

Maximum client read/write throughput, when served from the cloud tier*
11/41 MB/sec
Read throughput depends on clients generating and maintaining sufficient I/O queue depth.

*Maximum throughput per I/O type was measured with 100 percent read and 100 percent write scenarios. Actual throughput might be lower and depends on I/O mix and network conditions.

## Azure Stream Analytics limits

Limit identifier
Limit
Comments

Maximum number of streaming units per subscription per region
83
To request an increase in streaming units for your subscription beyond 83, contact Microsoft Support.

Maximum number of inputs per job
60
There's a hard limit of 60 inputs per Azure Stream Analytics job.

Maximum number of outputs per job
60
There's a hard limit of 60 outputs per Stream Analytics job.

Maximum number of functions per job
60
There's a hard limit of 60 functions per Stream Analytics job.

Maximum number of streaming units per job
66
There's a hard limit of 66 streaming units per Stream Analytics job.

Maximum number of jobs per region
1,500
Each subscription can have up to 1,500 jobs per geographical region.

Reference data blob MB
5 GB
Up to 5 GB when using 1 or more SUs.

Maximum number of characters in a query
512000
There's a hard limit of 512k characters in an Azure Stream Analytics job query.

## Azure Virtual Machines limits

### Azure Virtual Machines limits

Resource
Limit

Virtual machines per cloud service 1
50

Input endpoints per cloud service 2
150

1 Virtual machines created by using the classic deployment model instead of Azure Resource Manager are automatically stored in a cloud service. You can add more virtual machines to that cloud service for load balancing and availability.

2 Input endpoints allow communications to a virtual machine from outside the virtual machine's cloud service. Virtual machines in the same cloud service or virtual network can automatically communicate with each other.

### Azure Virtual Machines limits - Azure Resource Manager

The following limits apply when you use Azure Resource Manager and Azure resource groups.

Resource
Limit

VMs per subscription
25,0001 per region.

VM total cores per subscription
201 per region. Contact support to increase limit.

Azure Spot VM total cores per subscription
201 per region. Contact support to increase limit.

VM per series, such as Dv2 and F, cores per subscription
201 per region. Contact support to increase limit.

Availability sets per subscription
2,500 per region.

Virtual machines per availability set
200

Proximity placement groups per resource group
800

Certificates per availability set
1992

Certificates per subscription
Unlimited3

1 Default limits vary by offer category type, such as Free Trial and Pay-As-You-Go, and by series, such as Dv2, F, and G. For example, the default for Enterprise Agreement subscriptions is 350. For security, subscriptions default to 20 cores to prevent large core deployments. If you need more cores, submit a support ticket.

2 Properties such as SSH public keys are also pushed as certificates and count towards this limit. To bypass this limit, use the Azure Key Vault extension for Windows or the Azure Key Vault extension for Linux to install certificates.

3 With Azure Resource Manager, certificates are stored in the Azure Key Vault. The number of certificates is unlimited for a subscription. There's a 1-MB limit of certificates per deployment, which consists of either a single VM or an availability set.

Note

Virtual machine cores have a regional total limit. They also have a limit for regional per-size series, such as Dv2 and F. These limits are separately enforced. For example, consider a subscription with a US East total VM core limit of 30, an A series core limit of 30, and a D series core limit of 30. This subscription can deploy 30 A1 VMs, or 30 D1 VMs, or a combination of the two not to exceed a total of 30 cores. An example of a combination is 10 A1 VMs and 20 D1 VMs.

### Azure Compute Gallery limits

There are limits per subscription for deploying resources when you use Compute Galleries:

- 100 compute galleries per subscription and per region

- 1,000 image definitions per subscription and per region

- 10,000 image versions per subscription and per region

### Managed Run Command limit

The maximum allowed Managed Run Commands is currently limited to 25.

## Azure Virtual Machine Scale Sets limits

Resource
Limit

Maximum number of VMs in a scale set
1,000

Maximum number of VMs based on a custom VM image in a scale set
600

Maximum number of scale sets per subscription per region
2,500

Maximum number of nodes supported in VMSS for IB cluster
100

## Azure Virtual Network Manager limits

Category
Limitation

General Limitations

Cross-tenant Support
Only with static membership network groups

Azure Subscriptions
Policy application limited to fewer than 15,000 subscriptions

Policy Enforcement Mode
No addition to network group if set to Disabled

Policy Evaluation Cycle
Standard evaluation cycle not supported

Subscription Movement
Moving subscription to another tenant not supported

Limits for Connectivity Configurations

Virtual Networks in a Connected Group
A connected group can include up to 250 virtual networks by default. In supported regions, you can increase the limit to 3,000 by registering the high-scale connected group feature. You can request an increase to 5,000 by submitting the scaling request form.

Private Endpoints
2,000 private endpoints per connected group

Hub-and-Spoke Configuration
Up to 1,000 virtual networks peered to the hub

Direct Connectivity
Up to 250 virtual networks by default. In supported regions, you can increase the limit to 3,000 by registering the high-scale connected group feature. You can request an increase to 5,000 by submitting the scaling request form.

Group Membership
A virtual network can be part of up to two connected groups. You can request an increase to 1,000 by submitting the connected group limit request form.

Overlapping IP Spaces
Communication to an overlapping IP address is dropped

Limits for Security Admin Rules

IP Prefixes
Max 20,000 IP prefixes combined per one Azure Virtual Network Manager resource

Admin Rules
Max 100 admin rules combined per one Azure Virtual Network Manager resource

Limits for User Defined Routes

User Defined Routes per Route Table
Max 1,000

## Dev tunnels limits

The following limits apply to dev tunnels. The limits reset monthly.

Resource
Limit

Bandwidth
5 GB per user

Tunnels
10 per user

Active connections
1000 per port

Ports
10 per tunnel

HTTP request rate
1500/min per port

Data transfer rate
Up to 20 MB/s per tunnel

Max web-forwarding HTTP request body size
16 MB

For questions on these limits, open an issue in our GitHub repo.

## Network security perimeter limits

### Scale limitations

Network security perimeter functionality can be used to support deployments of PaaS resources with common public network controls with following scale limitations:

Limitation
Description

Number of network security perimeters
Supported up to 100 as recommended limit per subscription.

Profiles per network security perimeters
Supported up to 200 as recommended limit.

Number of rule elements per profile
Supported up to 200 for inbound and outbound each as hard limit.

Number of PaaS resources across subscriptions associated with the same network security perimeter
Supported up to 1000 as recommended limit.

### Other limitations

Network security perimeter has other limitations as follows:

Limitation/Issue
Description

Missing field in network security perimeter access logs
Network security perimeter access logs can be aggregated. If the fields 'count' and 'timeGeneratedEndTime' are missing, consider the aggregation count as 1.

Association creations through SDK fails with permission issue
'Status: 403 (Forbidden); ErrorCode: AuthorizationFailed' might be received while performing action 'Microsoft.Network/locations/networkSecurityPerimeterOperationStatuses/read' over scope '/subscriptions/xyz/providers/Microsoft.Network/locations/xyz/networkSecurityPerimeterOperationStatuses/xyz'. 
 
 Until the fix, use permission 'Microsoft.Network/locations/*/read' or use WaitUntil.Started in CreateOrUpdateAsync SDK API for association creations.

Resource names cannot be longer than 44 characters to support network security perimeter
The network security perimeter resource association created from the Azure portal has the format `{resourceName}-{perimeter-guid}`. To align with the requirement name field can't have more than 80 characters, resources names would have to be limited to 44 characters.

Note

Refer to individual PaaS documentation for respective limitations for each service.

## Next steps

Continue to the following resources to learn more:

- Understand Azure Limits and Increases

- Sizes for virtual machines in Azure

- Sizes for Cloud Services (classic)

- Naming rules and restrictions for Azure resources

 
 

 
 

 

 
 
 
 
 
 
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
 2026-08-04
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
