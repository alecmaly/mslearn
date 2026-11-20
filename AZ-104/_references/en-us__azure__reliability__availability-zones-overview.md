# https://learn.microsoft.com/en-us/azure/reliability/availability-zones-overview

Source: https://learn.microsoft.com/en-us/azure/reliability/availability-zones-overview

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
 

 

 

 

 
 
# What are availability zones?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 

Many Azure regions provide availability zones, which are separated groups of datacenters within a region. Each availability zone has independent power, cooling, and networking infrastructure, so that if one zone experiences an outage, then regional services, capacity, and high availability are supported by the remaining zones. Some Azure services automatically use multiple zones, while others require you to configure multiple-zone deployment.

Availability zones don't only protect against large-scale outages that affect an entire zone. They also provide resilience against smaller-scoped failures, such as a server rack or cluster failure within a zone. In these scenarios, workloads can continue running in other zones, even if parts of the affected zone remain operational.

The following diagram shows several example Azure regions. Regions 1 and 2 support availability zones, and regions 3 and 4 don't have availability zones. Some zones have one datacenter and others have multiple.

Tip

To see which regions support availability zones, see List of Azure regions.

## Datacenters and availability zones

An availability zone is a logical grouping of one or more physically separate datacenters within a region. Each availability zone is built in a way that if something goes wrong in one (like a power outage or network issue), the others keep working. A single datacenter doesnât offer this level of protection on its own.

Availability zones are typically separated by several kilometers, and usually are within 100 kilometers of each other. This provides low-latency connectivity while reducing the likelihood local outages or weather events impact multiple zones simultaneously.

Datacenter locations are selected by using rigorous vulnerability risk assessment criteria. This process identifies all significant datacenter-specific risks and considers shared risks between availability zones.

## Types of availability zone support

Azure services can provide different types of availability zone support for their resources, and most services support deploying either zone-redundant or zonal resources:

- Zone-redundant resources: Zone-redundant resources are replicated or distributed across multiple availability zones by the service. For example, zone-redundant data services replicate the data across multiple zones so that a failure in one zone doesn't affect the availability of the data. Some services are automatically zone-redundant in supported regions, while other services require that you configure your resource to be zone-redundant.

For most services, Microsoft selects the zones your resources use, but sometimes you can select the set of zones. Services might use a different number or subset of zones in a region depending on their design. A resource is resilient to a zone failure as long as it uses two or more zones.

When you plan an architecture that uses availability zones, distinguish between the following counts:

- Zones in the region: The total number of availability zones that the region provides.

- Zones used by a service or resource: The number of zones across which a specific service or resource distributes its components. A service might use only a subset of the zones in the region.

- Instances or replicas: The number of deployed resource instances or data replicas. This number doesn't have to match either zone count. Depending on the service, a zone might contain multiple instances or replicas, and some zones might contain none for that service or resource.

These counts don't necessarily match. For example, a region might provide four availability zones while a service uses three of those zones and maintains more than three instances or replicas. Review each service's reliability guide to understand its topology.

With zone-redundant deployments, Microsoft manages spreading requests across zones and the replication of data across zones. If an outage occurs in an availability zone, Microsoft manages failover to another zone automatically.

- Zonal resources: A zonal resource is deployed to a single availability zone that you select yourself.

Zonal deployments don't automatically provide resiliency to availability zone outages. However, zonal resources are isolated from faults in other zones. They can also help you achieve unusually stringent latency or performance requirements. For example, for a chatty workload built using virtual machines, you might choose to deploy multiple virtual machines to the same zone to reduce the latency of the connections between them.

To make zonal resources resilient to availability zone outages, you need to design an architecture with separate resources in multiple availability zones within the region. Microsoft doesn't manage the process for you. If an outage occurs in an availability zone, you're responsible for failover to another zone.

When you configure a resource to be zone redundant, or if you use multiple instances of a zonal resource in different availability zones, then your resource is considered to be zone-resilient: that is, it's resilient to the outage of a single availability zone. To learn more about how to use zonal deployments and maintain zone resiliency, see Zonal resources and zone resiliency.

When designing your reliability strategy, make sure that you understand how each service in your workload supports availability zones. Availability zone support can depend on the service tier or SKU. To identify supported tiers or SKUs, check the availability zone requirements in each service's reliability guide. Don't assume that all tiers or SKUs support availability zones.

If a resource isn't configured to use availability zones, either due to the region you use not supporting zones or because of your configuration choices, it's called a nonzonal or regional deployment. Azure might place nonzonal resources across any zones in the region. You don't choose which resources go into which zones. If any availability zone in the region experiences an outage, nonzonal resources might be in the affected zone and could experience downtime.

## Configuring resources for availability zone support

Each service has its own method for configuring availability zone support, and some services don't require any configuration. To learn about how each service supports availability zones and how to configure that support, see Azure reliability guides by service.

## Physical and logical availability zones

Each datacenter is assigned to a physical zone. Physical zones are mapped to logical zones in your Azure subscription, and different subscriptions might have a different mapping order. Azure subscriptions are automatically assigned their mapping at the time the subscription is created. Because of this, the zone mapping for one subscription could be different for other subscriptions.

For example, subscription A may have physical zone 1 mapped to logical zone 2, while subscription B has physical zone 1 mapped to logical zone 3:

When Microsoft adds new availability zones to an existing region, the zone mappings for existing subscriptions don't change. The new zone uses the same logical zone number as its physical zone number in existing subscriptions. New subscriptions created after the zone is added might have a different mapping.

To understand the mapping between logical and physical zones for your subscription, use the Azure CLI or Azure PowerShell, or the Azure Resource Manager APIs.

- 
Azure CLI

- 
Azure PowerShell

- 
Azure Resource Manager APIs

Use the az account list-locations command:

`az account list-locations \
 --query "[?availabilityZoneMappings].{availabilityZoneMappings: availabilityZoneMappings, displayName: displayName, name: name}"
`

Use the Invoke-AzRestMethod cmdlet to retrieve the current subscription's availability zone mappings from the List Locations Resource Manager API:

`$subscriptionId = (Get-AzContext).Subscription.ID
$response = Invoke-AzRestMethod -Method GET -Path "/subscriptions/$subscriptionId/locations?api-version=2022-12-01"
$locations = ($response.Content | ConvertFrom-Json).value
$locations | Where-Object {$null -ne $_.availabilityZoneMappings} | Select-Object -Property name,displayName,@{name='availabilityZoneMappings';expression={$_.availabilityZoneMappings | convertto-json}} | Format-List
`

Use one of these Azure Resource Manager APIs:

- List Locations API: Retrieves the zone mappings for a single Azure subscription.

- Check Zone Peers API: Retrieves the zone mappings for multiple Azure subscriptions.

Note

To use the Check Zone Peers API, the feature `Microsoft.Resources/AvailabilityZonePeering` needs to be enabled on your subscription. For more information about how to enable features, see Register features in Azure subscription.

## Availability zones and Azure updates

For each region, Microsoft aims to deploy updates to Azure services within a single availability zone at a time. This approach reduces the impact that updates might have on an active workload, allowing the workload to continue to run in other zones while the update is in process. To take advantage of sequenced zone updates, your workload must be already configured to run across multiple zones. For more information about how Azure deploys updates, see Advancing safe deployment practices.

## Inter-zone networking

Within each region, availability zones are connected through a high-performance network. Microsoft strives to achieve an inter-zone communication with round-trip latency of less than approximately 2 milliseconds. Low latency allows for high-performance communication within a region, and for synchronous replication of data across multiple availability zones. The target latency refers to the latency of the network links. Depending on the communication protocol you use and the network hops required for any specific network flow, the latency you observe might be different.

In most workloads, you can distribute components of your solution across availability zones without a noticeable effect on your performance. If you have a workload with a high degree of sensitivity to inter-zone latency, it's important to test the latency between your selected availability zones with your actual protocols and configuration. To reduce inter-zone traffic, it's possible to use zonal deployments, but optimally, you should use multiple availability zones in your reliability strategy plan. To learn more about how to use zonal deployments and maintain zone resiliency, see Zonal resources and zone resiliency.

Azure doesn't charge for data transfer between availability zones in the same region, whether you use private or public IP addressing.

## Availability zone architectural guidance

To achieve reliable workloads:

- Production workloads should be configured to use multiple availability zones if the region they are in supports availability zones.

- For mission-critical workloads, you should consider a solution that is both multiregion and multi-zone.

For workloads constrained to a single region by data residency or sovereignty requirements, deploying across multiple availability zones is the primary recommended way to maximize availability without moving data outside the region. A zone-resilient configuration keeps replicas inside the regional boundary while maintaining continuity if a single zone fails.

Availability zones don't protect against a full-region outage. If your compliance requirements don't permit you to use a secondary Azure region, plan in-region redundancy together with backup and restore procedures, such as by using Azure Backup and other backup approaches. Set recovery objectives that reflect the time required to recover from a region-wide disruption.

For more detailed information on how to use regions and availability zones in a solution architecture, see Recommendations for using availability zones and regions.

## Regions with availability zones

The regions in the following table support availability zones. For more comprehensive information about each region, see List of Azure regions.

Note

Even when a region provides availability zones, some services might not support them in that region. To learn about region support for availability zone-enabled services, refer to the Azure service reliability guides.

- 
All

- 
Americas

- 
Europe

- 
Middle East

- 
Africa

- 
Asia Pacific

Region
Number of availability zones

Australia East
3

Austria East
3

Belgium Central
3

Brazil South
3

Canada Central
3

Central India
3

Central US
3

Chile Central
3

Denmark East
3

East Asia
3

East US
3

East US 2
4

France Central
3

Germany West Central
3

India South Central
3

Indonesia Central
3

Israel Central
3

Italy North
3

Japan East
3

Japan West
3

Korea Central
3

Malaysia West
3

Mexico Central
3

New Zealand North
3

North Central US
3 

North Europe
3

Norway East
3

Poland Central
3

Qatar Central
3

 Saudi Arabia East
3

South Africa North
3

South Central US
3

Southeast Asia
3

 Southeast Asia 3
3

Spain Central
3

Sweden Central
3

Switzerland North
3

 Taiwan North
3

UAE North
3

UK South
3

West Europe
3

West US 2
3

West US 3
3

Legend:

 In the Region column, this icon indicates that the region is in preview. To learn more about availability zones and available services support in this region, contact your Microsoft sales or customer representative.

 In the Number of availability zones column, this icon indicates that one or more availability zones are in preview in this region.

Region
Number of availability zones

Brazil South
3

Canada Central
3

Central US
3

Chile Central
3

East US
3

East US 2
4

Mexico Central
3

North Central US
3 

South Central US
3

West US 2
3

West US 3
3

Legend:

 In the Number of availability zones column, this icon indicates that one or more availability zones are in preview in this region.

Region
Number of availability zones

Austria East
3

Belgium Central
3

Denmark East
3

France Central
3

Germany West Central
3

Italy North
3

North Europe
3

Norway East
3

Poland Central
3

Spain Central
3

Sweden Central
3

Switzerland North
3

UK South
3

West Europe
3

Region
Number of availability zones

Israel Central
3

Qatar Central
3

 Saudi Arabia East
3

UAE North
3

Legend:

 In the Region column, this icon indicates that the region is in preview. To learn more about availability zones and available services support in this region, contact your Microsoft sales or customer representative.

Region
Number of availability zones

South Africa North
3

Region
Number of availability zones

Australia East
3

Central India
3

East Asia
3

India South Central
3

Indonesia Central
3

Japan East
3

Japan West
3

Korea Central
3

Malaysia West
3

New Zealand North
3

Southeast Asia
3

 Southeast Asia 3
3

 Taiwan North
3

Legend:

 In the Region column, this icon indicates that the region is in preview. To learn more about availability zones and available services support in this region, contact your Microsoft sales or customer representative.

## Related content

- What are Azure regions?

- List of Azure regions

- Azure services with availability zones

- Recommendations for using availability zones and regions

 
 

 
 

 

 
 
 
 
 
 
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
 2026-09-23
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
