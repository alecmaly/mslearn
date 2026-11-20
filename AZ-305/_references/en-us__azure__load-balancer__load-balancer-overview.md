# https://learn.microsoft.com/en-us/azure/load-balancer/load-balancer-overview

Source: https://learn.microsoft.com/en-us/azure/load-balancer/load-balancer-overview

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
 

 

 

 

 
 
# What is Azure Load Balancer?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 
Important

On September 30, 2025, Basic Load Balancer was retired. For more information, see the official announcement. If you're currently using Basic Load Balancer, upgrade to Standard Load Balancer as soon as possible. For guidance on upgrading, see Upgrading from Basic Load Balancer - Guidance.

Azure Load Balancer is a cloud service that distributes incoming network traffic across backend virtual machines (VMs) or virtual machine scale sets (VMSS). This article explains Azure Load Balancer's key features, architecture, and scenarios, helping you decide if it fits your organization's load balancing needs for scalable, highly available workloads.

Load balancing refers to efficiently distributing incoming network traffic across a group of backend virtual machines (VMs) or virtual machine scale sets (VMSS).

Use Azure Load Balancer when you need to distribute Layer 4 TCP or UDP traffic across VMs or virtual machine scale sets. Choose a scenario to get started:

- Create a public load balancer for internet-facing traffic.

- Create an internal load balancer for private traffic within a virtual network.

- Configure outbound connectivity for backend instances.

- Upgrade a retired Basic Load Balancer to Standard Load Balancer.

Note

Azure Load Balancer is one of the services that make up the Load Balancing and Content Delivery category in Azure. Other services in this category include Azure Front Door and Azure Application Gateway. Each service has its own unique features and use cases. For more information on this service category, see Load Balancing and Content Delivery.

## How Azure Load Balancer distributes Layer 4 traffic

Azure Load Balancer operates at layer 4 of the Open Systems Interconnection (OSI) model. It's the single point of contact for clients. The service distributes inbound flows that arrive at the load balancer's frontend to backend pool instances. These flows are distributed according to configured load-balancing rules and health probes. The backend pool instances can be Azure virtual machines (VMs) or virtual machine scale sets.

A public load balancer can provide both inbound and outbound connectivity for the VMs inside your virtual network. For inbound traffic scenarios, Azure Load Balancer can load balance internet traffic to your VMs. For outbound traffic scenarios, the service can translate the VMs' private IP addresses to public IP addresses for any outbound connections that originate from your VMs.

Alternatively, an internal (or private) load balancer is used to load balance traffic inside a virtual network. By using an internal load balancer, you can provide inbound connectivity to your VMs in private network connectivity scenarios, such as accessing a load balancer frontend from an on-premises network in a hybrid scenario.

For more information on the service's individual components, see Azure Load Balancer components.

Azure Load Balancer offers two current SKUs: Standard and Gateway. Each SKU caters to a specific scenario and has differences in scale, features, and pricing. A third SKU, Basic, was retired on September 30, 2025. For more information, see Azure Load Balancer SKUs.

## Why use Azure Load Balancer?

By using Azure Load Balancer, you can scale your applications and create highly available services. The service supports both inbound and outbound scenarios, provides low latency and high throughput, and scales up to millions of flows for all TCP and UDP applications.

### Core capabilities

Azure Load Balancer provides:

- High availability: Distribute resources within and across availability zones.

- Scalability: Handle millions of flows for TCP and UDP applications.

- Low latency: Use pass-through load balancing for ultralow latency.

- Flexibility: Support for multiple ports, multiple IP addresses, or both.

- Health monitoring: Use health probes to ensure traffic is only sent to healthy instances.

### Traffic distribution scenarios

- Load balance internal and external traffic to Azure virtual machines.

- Configure outbound connectivity for Azure virtual machines.

- Load balance TCP and UDP flow on all ports simultaneously using high-availability ports.

- Enable port forwarding to access virtual machines by public IP address and port.

### Advanced features

- IPv6 support: Enable load balancing of IPv6 traffic.

- Cross-region mobility: Move internal and external load balancer resources across Azure regions.

- Gateway load balancer integration: Chain Standard Load Balancer and Gateway Load Balancer.

- Global load balancing integration: Distribute traffic across multiple Azure regions for global applications.

- Admin State: Override health probe behavior for maintenance and operational management.

### Monitoring and insights

- Comprehensive metrics: Use multidimensional metrics through Azure Monitor.

- Prebuilt dashboards: Access Insights for Azure Load Balancer with useful visualizations.

- Diagnostics: Review Standard load balancer diagnostics for performance insights.

- Health Event Logs: Monitor load balancer health events and status changes for proactive management.

- Load Balancer health status: Gain deeper insights into the health of your load balancer through health status monitoring.

### Security features

Azure Load Balancer implements security through multiple layers:

#### Zero Trust security model

- Standard Load Balancer is built on the Zero Trust network security model.

- Part of your virtual network, which is private and isolated by default.

#### Network access controls

- Standard load balancers and public IP addresses are closed to inbound connections by default.

- Network Security Groups (NSGs) must explicitly permit allowed traffic.

- Traffic is blocked if no NSG exists on a subnet or NIC.

#### Data protection

- Azure Load Balancer doesn't store customer data.

- All traffic processing happens in real-time without data persistence.

Important

Basic Load Balancer is open to the internet by default and was retired on September 30, 2025. Migrate to Standard Load Balancer for enhanced security.

To learn about NSGs and how to apply them to your scenario, see Network security groups.

## Pricing and SLA

For Standard Load Balancer pricing information, see Load Balancer pricing. For service-level agreements (SLAs), see the Microsoft licensing information for online services.

Microsoft retired Basic Load Balancer on September 30, 2025. It was offered at no charge and had no SLA. To move existing deployments, see Upgrading from Basic Load Balancer - Guidance.

## What's new?

Subscribe to the RSS feed and view the latest Azure Load Balancer updates on the Azure Updates page.

## Related content

- Create a public load balancer

- Azure Load Balancer components

 
 

 
 

 

 
 
 
 
 
 
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
 2026-08-21
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
