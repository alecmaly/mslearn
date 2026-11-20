# https://learn.microsoft.com/en-us/azure/networking/fundamentals/networking-overview

Source: https://learn.microsoft.com/en-us/azure/networking/fundamentals/networking-overview

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
 

 

 

 

 
 
# Azure networking services overview

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure networking services connect your Azure resources to each other, to on-premises networks, and to the internet. They load balance, secure, and monitor that traffic. Together, these services let you build a private, highly available, and protected network in the cloud without deploying or maintaining physical network hardware.

This article is the entry point to the Azure networking documentation. It groups the services into six categories, summarizes what each service does, and links to each category hub where you can explore that area in depth.

Azure networking services fall into six categories. Select a category to explore its services:

- Networking foundation: Core connectivity for your resources in Azure - Virtual Network (VNet), Private Link, Azure DNS, Azure Bastion, Route Server, NAT Gateway, and Traffic Manager.

- Load balancing and content delivery: Manage, distribute, and optimize your applications and workloads - Load Balancer, Application Gateway, and Azure Front Door.

- Hybrid connectivity: Secure communication to and from your resources in Azure - VPN Gateway, ExpressRoute, Virtual WAN, and Peering Service.

- Network security: Protect your web applications and IaaS services from DDoS attacks and malicious actors - Firewall Manager, Firewall, Web Application Firewall, and DDoS Protection.

- Network management and monitoring: Manage and monitor your network resources - Network Watcher, Azure Monitor, and Azure Virtual Network Manager.

- Container networking: Enhanced security and observability for containerized workloads on Azure Kubernetes Service (AKS) - Container network security and Container network observability.

The following table summarizes each networking category, its key services, and its primary use case:

Category
Key services
Primary use case
Learn more

Networking foundation
Virtual Network, Private Link, Azure DNS, Azure Bastion, Route Server, NAT Gateway, Traffic Manager
Core connectivity for resources in Azure
Azure networking foundation services

Load balancing and content delivery
Load Balancer, Application Gateway, Azure Front Door
Distribute and optimize application traffic
Azure load balancing and content delivery services

Hybrid connectivity
VPN Gateway, ExpressRoute, Virtual WAN, Peering Service
Connect on-premises networks to Azure
Azure hybrid connectivity services

Network security
Firewall Manager, Firewall, Web Application Firewall, DDoS Protection
Protect applications and resources from threats
Azure network security services

Network management and monitoring
Network Watcher, Azure Monitor, Azure Virtual Network Manager
Manage and monitor network resources
Azure network management and monitoring services

Container networking
Container network security, Container network observability
Secure and observe AKS container traffic
Advanced Container Networking Services

## Azure networking foundation services

This section describes services that provide the building blocks for designing and architecting a network environment in Azure - Virtual Network (VNet), Private Link, Azure DNS, Azure Bastion, Route Server, NAT Gateway, and Traffic Manager.

### Virtual network

Azure Virtual Network (VNet) is the fundamental building block for your private network in Azure. Use VNets to:

- Communicate between Azure resources: Deploy virtual machines and several other types of Azure resources to a virtual network, such as Azure App Service Environments, Azure Kubernetes Service (AKS), and Azure Virtual Machine Scale Sets. To view a complete list of Azure resources that you can deploy into a virtual network, see Virtual network service integration.

- Communicate between each other: Connect virtual networks to each other, enabling resources in either virtual network to communicate with each other, by using virtual network peering or Azure Virtual Network Manager. The virtual networks you connect can be in the same, or different, Azure regions. For more information, see Virtual network peering and Azure Virtual Network Manager.

- Communicate to the internet: All resources in a virtual network can communicate outbound to the internet, by default. You can communicate inbound to a resource by assigning a public IP address or a public Load Balancer. You can also use Public IP addresses or a public Load Balancer to manage your outbound connections.

- Communicate with on-premises networks: Connect your on-premises computers and networks to a virtual network by using VPN Gateway or ExpressRoute.

- Encrypt traffic between resources: Use Virtual network encryption to encrypt traffic between resources in a virtual network.

#### Network security groups

Filter network traffic to and from Azure resources in an Azure virtual network by using a network security group. For more information, see Network security groups.

#### Service endpoints

Virtual Network (VNet) service endpoints extend your virtual network private address space and the identity of your virtual network to the Azure services, over a direct connection. Endpoints allow you to secure your critical Azure service resources to only your virtual networks. Traffic from your virtual network to the Azure service always remains on the Microsoft Azure backbone network.

### Azure Private Link

Azure Private Link lets you access Azure PaaS services (for example, Azure Storage and SQL Database) and Azure hosted customer-owned or partner services over a private endpoint in your virtual network.
Traffic between your virtual network and the service travels through the Microsoft backbone network. You no longer need to expose your service to the public internet. You can create your own private link service in your virtual network and deliver it to your customers.

### Azure DNS

Azure DNS provides DNS hosting and resolution by using the Microsoft Azure infrastructure. Azure DNS consists of three services:

- Azure Public DNS is a hosting service for DNS domains. By hosting your domains in Azure, you can manage your DNS records by using the same credentials, APIs, tools, and billing as your other Azure services.

- Azure Private DNS is a DNS service for your virtual networks. Azure Private DNS manages and resolves domain names in the virtual network without configuring a custom DNS solution.

- Azure DNS Private Resolver is a service for querying Azure DNS private zones from an on-premises environment and vice versa without deploying VM-based DNS servers.

By using Azure DNS, you can host and resolve public domains, manage DNS resolution in your virtual networks, and enable name resolution between Azure and your on-premises resources.

### Azure Bastion

Azure Bastion is a service that you can deploy in a virtual network to connect to a virtual machine by using your browser and the Azure portal. You can also connect by using the native SSH or RDP client already installed on your local computer. The Azure Bastion service is a fully platform-managed PaaS service that you deploy inside your virtual network. It provides secure and seamless RDP/SSH connectivity to your virtual machines directly from the Azure portal over TLS. When you connect through Azure Bastion, your virtual machines don't need a public IP address, agent, or special client software. Azure Bastion offers four SKU tiers: Developer, Basic, Standard, and Premium. The tier you select affects the available features. For more information, see About Bastion configuration settings.

### Azure Route Server

Azure Route Server simplifies dynamic routing between your network virtual appliance (NVA) and your virtual network. You can exchange routing information directly through Border Gateway Protocol (BGP) routing protocol between any NVA that supports the BGP routing protocol and the Azure Software Defined Network (SDN) in the Azure Virtual Network (VNet) without manually configuring or maintaining route tables.

### NAT Gateway

NAT Gateway simplifies outbound-only internet connectivity for virtual networks. When you configure it on a subnet, all outbound connectivity uses your specified static public IP addresses. Outbound connectivity is possible without a load balancer or public IP addresses directly attached to virtual machines.
For more information, see What is Azure NAT gateway.

### Traffic Manager

Azure Traffic Manager is a DNS-based traffic load balancer that distributes traffic optimally to services across global Azure regions, while providing high availability and responsiveness. Traffic Manager provides a range of traffic-routing methods to distribute traffic such as priority, weighted, performance, geographic, multivalue, or subnet.

The following diagram shows endpoint priority-based routing with Traffic Manager:

For more information about Traffic Manager, see What is Azure Traffic Manager?

## Azure load balancing and content delivery services

This section describes networking services in Azure that help deliver applications and workloads - Load Balancer, Application Gateway, and Azure Front Door.

### Load Balancer

Important

On September 30, 2025, Basic Load Balancer was retired. For more information, see the official announcement. If you're currently using Basic Load Balancer, upgrade to Standard Load Balancer as soon as possible. For guidance on upgrading, see Upgrading from Basic Load Balancer - Guidance.

Azure Load Balancer provides high-performance, low-latency Layer 4 load-balancing for all UDP and TCP protocols. It manages inbound and outbound connections. You can configure public and internal load-balanced endpoints. You can define rules to map inbound connections to back-end pool destinations by using TCP and HTTP health-probing options to manage service availability.

Azure Load Balancer is available in Standard and Gateway SKUs.

The following diagram shows an internet-facing multitier application that uses both external and internal load balancers:

### Application Gateway

Azure Application Gateway is a web traffic load balancer that you can use to manage traffic to your web applications. It's an Application Delivery Controller (ADC) as a service, offering various Layer 7 load-balancing capabilities for your applications.

The following diagram shows URL path-based routing with Application Gateway.

### Azure Front Door

Azure Front Door helps you define, manage, and monitor the global routing for your web traffic by optimizing for best performance and instant global failover for high availability. By using Front Door, you can transform your global (multiregion) consumer and enterprise applications into robust, high-performance personalized modern applications, APIs, and content that reach a global audience with Azure. Use Front Door when you need a global, Layer 7 entry point that combines content delivery network (CDN) caching, SSL offload, and a web application firewall (WAF) in front of multiregion backends.

## Azure hybrid connectivity services

This section describes network connectivity services that securely connect your on-premises network and Azure - VPN Gateway, ExpressRoute, Virtual WAN, and Peering Service.

### VPN Gateway

VPN Gateway helps you create encrypted cross-premises connections to your virtual network from on-premises locations, or create encrypted connections between VNets. Different configurations are available for VPN Gateway connections. Some of the main features include:

- Site-to-site VPN connectivity

- Point-to-site VPN connectivity

- VNet-to-VNet VPN connectivity

The following diagram illustrates multiple site-to-site VPN connections to the same virtual network. To view more connection diagrams, see VPN Gateway - design.

### ExpressRoute

ExpressRoute extends your on-premises networks into the Microsoft cloud over a private connection that a connectivity provider facilitates. This connection is private. Traffic doesn't go over the internet. By using ExpressRoute, you can connect to Microsoft cloud services such as Microsoft Azure, Microsoft 365, and Dynamics 365.

### Virtual WAN

Azure Virtual WAN is a networking service that brings many networking, security, and routing functionalities together to provide a single operational interface. You connect to Azure VNets by using virtual network connections. Some of the main features include:

- Branch connectivity (via connectivity automation from Virtual WAN Partner devices such as SD-WAN or VPN CPE)

- Site-to-site VPN connectivity

- Remote user VPN connectivity (point-to-site)

- Private connectivity (ExpressRoute)

- Intra-cloud connectivity (transitive connectivity for virtual networks)

- VPN ExpressRoute inter-connectivity

- Routing, Azure Firewall, and encryption for private connectivity

### Peering Service

Azure Peering Service enhances customer connectivity to Microsoft cloud services such as Microsoft 365, Dynamics 365, software as a service (SaaS), Azure, or any Microsoft services accessible over the public internet. Peering Service partners provide optimized, reliable routing to Microsoft's network edge, which reduces latency and packet loss compared to typical internet transit for traffic bound for Microsoft cloud services.

## Azure network security services

This section describes networking services in Azure that protect and monitor your network resources - Firewall Manager, Firewall, Web Application Firewall, and DDoS Protection.

### Firewall Manager

Azure Firewall Manager is a security management service that provides central security policy and routing management for cloud-based security perimeters. Firewall Manager can provide security management for two types of network architecture: secure virtual hub and hub virtual network. Use Azure Firewall Manager to deploy multiple Azure Firewall instances across Azure regions and subscriptions, implement DDoS protection plans, manage web application firewall policies, and integrate with partner security-as-a-service for enhanced security.

### Azure Firewall

Azure Firewall is a managed, cloud-based network security service that protects your Azure Virtual Network resources. By using Azure Firewall, you can centrally create, enforce, and log application and network connectivity policies across subscriptions and virtual networks. Azure Firewall uses a static public IP address for your virtual network resources, so outside firewalls can identify traffic originating from your virtual network.

### Web Application Firewall

Azure Web Application Firewall (WAF) protects your web applications from common web exploits and vulnerabilities such as SQL injection and cross-site scripting. Azure WAF provides out-of-the-box protection from OWASP Top 10 vulnerabilities via managed rules. Additionally, you can configure custom rules to provide extra protection based on source IP range and request attributes such as headers, cookies, form data fields, or query string parameters.

You can deploy Azure WAF with Application Gateway, which provides regional protection to entities in public and private address space. You can also deploy Azure WAF with Front Door, which provides protection at the network edge to public endpoints.

### DDoS Protection

Azure DDoS Protection provides countermeasures against the most sophisticated DDoS threats. The service provides enhanced DDoS mitigation capabilities for your application and resources deployed in your virtual networks. Additionally, with Azure DDoS Protection, you have access to DDoS Rapid Response support to engage DDoS experts during an active attack.

Azure DDoS Protection consists of two tiers:

- DDoS Network Protection, combined with application design best practices, provides enhanced DDoS mitigation features to defend against DDoS attacks. It's automatically tuned to help protect your specific Azure resources in a virtual network.

- DDoS IP Protection is a pay-per-protected IP model. DDoS IP Protection contains the same core engineering features as DDoS Network Protection, but differs in the following value-added services: DDoS rapid response support, cost protection, and discounts on WAF.

## Azure network management and monitoring services

This section describes network management and monitoring services in Azure - Network Watcher, Azure Monitor, and Azure Virtual Network Manager.

### Azure Network Watcher

Azure Network Watcher provides tools to monitor, diagnose, view metrics, and enable or disable logs for resources in an Azure virtual network.

### Azure Monitor

Azure Monitor maximizes the availability and performance of your applications by delivering a comprehensive solution for collecting, analyzing, and acting on telemetry from your cloud and on-premises environments. It helps you understand how your applications are performing and proactively identifies issues affecting them and the resources they depend on.

### Azure Virtual Network Manager

Azure Virtual Network Manager is a management service that you use to group, configure, deploy, and manage virtual networks globally across subscriptions. By using Virtual Network Manager, you can define network groups to identify and logically segment your virtual networks. Then you can determine the connectivity and security configurations you want and apply them across all the selected virtual networks in network groups at once.

## Azure container networking services

This section describes services that secure and monitor network traffic for containerized workloads running on Azure Kubernetes Service (AKS) - Container network security and Container network observability. Both services are part of Advanced Container Networking Services.

### Container network security

Container network security provides enhanced control over AKS network security. By using features like fully qualified domain name (FQDN) filtering, clusters that use Azure CNI Powered by Cilium can implement FQDN-based network policies to achieve a Zero Trust security architecture in AKS.

### Container network observability

Container network observability uses Hubble's control plane to provide comprehensive visibility into AKS networking and performance. It offers real-time, detailed insights across node-level, pod-level, TCP, and DNS metrics, ensuring thorough monitoring of your network infrastructure.

## Related content

- Azure networking foundation services

- Azure load balancing and content delivery services

- Azure hybrid connectivity services

- Azure network security services

- Azure network management and monitoring services

- Advanced Container Networking Services

- Create your first virtual network

- Configure a point-to-site VPN connection

- Create an internet-facing load balancer

 
 

 
 

 

 
 
 
 
 
 
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
 2026-08-19
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
