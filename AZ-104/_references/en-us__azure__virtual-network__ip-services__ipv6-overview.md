# https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/ipv6-overview

Source: https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/ipv6-overview

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
 

 

 

 

 
 
# What is IPv6 for Azure Virtual Network?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 IPv6 for Azure Virtual Network enables you to host applications in Azure with IPv6 and IPv4 connectivity both within a virtual network and to and from the Internet. Due to the exhaustion of public IPv4 addresses, new networks for mobility and Internet of Things (IoT) are often built on IPv6. Even long established ISP and mobile networks are being transformed to IPv6. IPv4-only services can find themselves at a real disadvantage in both existing and emerging markets. Dual stack IPv4/IPv6 connectivity enables Azure-hosted services to traverse this technology gap with globally available, dual-stacked services that readily connect with both the existing IPv4 and these new IPv6 devices and networks.

Azure's original IPv6 connectivity makes it easy to provide dual stack (IPv4/IPv6) Internet connectivity for applications hosted in Azure. It allows for simple deployment of VMs with load balanced IPv6 connectivity for both inbound and outbound initiated connections. This feature is still available and more information is available here.
IPv6 for Azure virtual network is much more full featured- enabling full IPv6 solution architectures to be deployed in Azure.

The following diagram depicts a simple dual stack (IPv4/IPv6) deployment in Azure:

## Benefits

IPv6 for Azure Virtual Network benefits:

- Helps expand the reach of your Azure-hosted applications into the growing mobile and Internet of Things markets.

- Dual stacked IPv4/IPv6 VMs provide maximum service deployment flexibility. A single service instance can connect with both IPv4 and IPv6-capable Internet clients.

- Builds on long-established, stable Azure VM-to-Internet IPv6 connectivity.

- Secure by default since IPv6 connectivity to the Internet is only established when you explicitly request it in your deployment.

## Capabilities

IPv6 for Azure Virtual Network includes the following capabilities:

- Azure customers can define their own IPv6 virtual network address space to meet the needs of their applications, customers, or seamlessly integrate into their on-premises IP space.

- Dual stack (IPv4 and IPv6) virtual networks with dual stack subnets enable applications to connect with both IPv4 and IPv6 resources in their virtual network or - the Internet.

Important

The subnets for IPv6 must be exactly /64 in size. This ensures future compatibility should you decide to enable routing of the subnet to an on-premises network since some routers can only accept /64 IPv6 routes.

- Protect your resources with IPv6 rules for Network Security Groups.

- And the Azure platform's Distributed Denial of Service (DDoS) protections are extended to Internet-facing public IPs

- Customize the routing of IPv6 traffic in your virtual network with User-Defined Routes especially when using Network Virtual Appliances to augment your application.

- Linux and Windows Virtual Machines can all use IPv6 for Azure Virtual Network.

- Standard IPv6 public load balancer support to create resilient, scalable applications, which include:

- Optional IPv6 health probe to determine which backend pool instances are health and thus can receive new flows.

- Optional outbound rules that provide full declarative control over outbound connectivity to scale and tune this ability to your specific needs.

- Optional multiple front-end configurations that enable a single load balancer to use multiple IPv6 public IP addresses- the same frontend protocol and port can be reused across frontend addresses.

- Optional IPv6 ports can be reused on backend instances using the Floating IP feature of load-balancing rules

- Note: Load balancing doesn't perform any protocol translation (no NAT64).

- Standard IPv6 internal load balancer support to create resilient multi-tier applications within Azure VNETs.

- Basic IPv6 public Load Balancer support for compatibility with legacy deployments

- Reserved IPv6 public IP addresses and address ranges provide stable, predictable IPv6 addresses that ease filtering of your Azure hosted applications for your company and your customers.

- Instance-level public IP provides IPv6 Internet connectivity directly to individual VMs.

- Add IPv6 to Existing IPv4-only deployments- this feature enables you to easily add IPv6 connectivity to existing IPv4-only deployments without the need to recreate deployments. The IPv4 network traffic is unaffected during this process so depending on your application and OS you might be able to add IPv6 even to live services.

- Let Internet clients seamlessly access your dual stack application using their protocol of choice with Azure DNS support for IPv6 (AAAA) records.

- Create dual stack applications that automatically scale to your load with virtual machine scale sets with IPv6.

- Virtual Network Peering - both within-regional and global peering - enables you to seamlessly connect dual stack virtual networks - both the IPv4 and IPv6 endpoints on VMs in the peered networks are able to communicate with each other. You can even peer dual stack with IPv4-only virtual networks as you're transitioning your deployments to dual stack.

- IPv6 Troubleshooting and Diagnostics are available with load balancer metrics/alerting and Network Watcher features such as packet capture, NSG flow logs, connection troubleshooting and connection monitoring.

## Scope

IPv6 for Azure Virtual Network is a foundational feature set that enables customers to host dual stack (IPv4+IPv6) applications in Azure. Our intention is to add IPv6 support to more Azure networking features over time and eventually to offer dual stack versions of Azure PaaS services. All Azure PaaS services can be accessed via the IPv4 endpoints on dual stack Virtual Machines.

## Limitations

The current IPv6 for Azure Virtual Network release has the following limitations:

- The Azure platforms, such as Azure Container Instances and Azure Container Apps, don't support IPv6 communication for containers

- IPv6-only Virtual Machines or Virtual Machines Scale Sets aren't supported. Each NIC must include at least one IPv4 IP configuration.

- To add IPv6 to existing IPv4 deployments, you can't add IPv6 ranges to a virtual network that has existing resource navigation links.

- While it's possible to create NSG rules for IPv4 and IPv6 within the same NSG, it isn't currently possible to combine an IPv4 subnet with an IPv6 subnet in the same rule when specifying IP prefixes.

- When using a dual stack configuration with a load balancer, health probes don't function for IPv6 if a Network Security Group isn't active.

- ICMPv6 isn't currently supported in Network Security Groups.

- Azure Virtual WAN currently supports IPv4 traffic only.

- Azure Route Server currently supports IPv4 traffic only.

- Azure Firewall doesn't currently support IPv6. It can operate in a dual stack virtual network using only IPv4, but the firewall subnet must be IPv4-only.

- Azure Database for PostgreSQL - Flexible Server doesn't currently support IPv6. Even if the subnet for the Postgres Flexible Server doesn't have any IPv6 addresses assigned, it can't be deployed if there are IPv6 addresses in the virtual network.

## Pricing

There's no charge to use Public IPv6 Addresses or Public IPv6 Prefixes. Associated resources and bandwidth are charged at the same rates as IPv4. You can find details about pricing for public IP addresses, network bandwidth, or Load Balancer.

## Next steps

- Learn how to deploy an IPv6 dual stack application using Azure PowerShell.

- Learn how to deploy an IPv6 dual stack application using Azure CLI.

- Learn how to deploy an IPv6 dual stack application using Resource Manager Templates (JSON)

 
 

 
 

 

 
 
 
 
 
 
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
 2024-10-16
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
