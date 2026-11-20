# https://learn.microsoft.com/en-us/azure/load-balancer/whats-new

Source: https://learn.microsoft.com/en-us/azure/load-balancer/whats-new

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
 

 

 

 

 
 
# What's new in Azure Load Balancer?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Load Balancer is updated regularly. Stay up to date with the latest announcements. This article provides you with information about:

- The latest releases

- Known issues

- Bug fixes

- Deprecated functionality (if applicable)

You can also find the latest Azure Load Balancer updates and subscribe to the RSS feed on the Azure updates page.

## Recent releases

Type
Name
Description
Date added

Feature
Azure Load Balancer bandwidth metrics now support Protocol dimension
Bandwidth metrics for Azure Load Balancer are now published with metric dimension Protocol. When viewing Byte, Packet, and SYN Count metrics, you can now filter by Protocol dimension where TCP traffic is denoted by Protocol=6 and UDP traffic by Protocol=17. The Protocol dimension is available in all Azure public regions, China cloud regions, and Government cloud regions. Learn more about Azure Load Balancer supported metrics.
December 2025

Feature
Azure Load Balancer health event logs generally available
Health event logs are now fully available in all public, Azure China, and Government regions under the Azure Monitor resource log category LoadBalancerHealthEvent, providing you with enhanced capabilities to monitor and troubleshoot your load balancer resources. Learn more about Azure Load Balancer health overview.
February 2025

Feature
Azure Load Balancer health status general availability
Announcing the general availability of Azure Load Balancer Health Status, a powerful feature designed to provide detailed information about the health of backend instances in your Azure Load Balancer backend pool. The Health Status feature offers valuable insights into the state of health of your backend instances and specific reasons for their health status. Learn more about Azure Load Balancer health status.
November 2024

Feature
Azure Load Balancer Admin State general availability
Admin State enables you to override the health probe behavior for each instance without additional configuration changes to your Load Balancer such as changing network security rules or closing ports. This makes management, especially during maintenance easy, allowing you to set instances as up or down and control connection behavior with no extra overhead. Learn more about Azure Load Balancer Admin State.
November 2024

Feature
Azure cross-subscription Load Balancer general availability
Cross-subscription load balancing enables the load balancers components to be located in different subscriptions. For example, the frontend IP address or the backend instances could be located in a different subscription from the one that the load balancer belongs to. Learn more about cross-subscription load balancing.
November 2024

Feature
Azure Load Balancer health event logs public preview
By using health event logs, you can collect, store, and analyze information to help understand the health of your Azure Load Balancer resource. These built-in logs help you troubleshoot specific scenarios and allow you to identify and alert on availability issues affecting your load balancer. Learn more about Azure Load Balancer health overview.
May 2024

Feature
Gateway Load Balancer IPv6 support is now generally available
Azure Gateway Load Balancer now supports IPv6 traffic, enabling you to distribute IPv6 traffic through Gateway Load Balancer before it reaches your dual-stack applications. Now you can add IPv6 frontend IP addresses and backend pools to Gateway Load Balancer. This allows you to inspect, protect, or mirror both IPv4 and IPv6 traffic flows using third-party or custom network virtual appliances (NVAs). Both internet inbound and outbound IPv6 traffic flows can now be routed through Gateway Load Balancer. Learn more about Gateway Load Balancer or our supported third-party partners.
September 2023

Feature
Azureâs cross-region Load Balancer is now generally available
Azure Load Balancerâs Global tier is a cloud-native global network load balancing solution. With cross-region Load Balancer, you can distribute traffic across multiple Azure regions with ultra-low latency and high performance. Azure cross-region Load Balancer provides customers a static globally anycast IP address. Through this global IP address, you can easily add or remove regional deployments without interruption. Learn more about cross-region load balancer
July 2023

Feature
Inbound ICMPv6 pings and traceroute are now supported on Azure Load Balancer (General Availability)
Azure Load Balancer now supports ICMPv6 pings to its frontend and inbound traceroute support to both IPv4 and IPv6 frontends. Learn more about how to test reachability of your load balancer.
June 2023

Feature
Inbound ICMPv4 pings are now supported on Azure Load Balancer (General Availability)
Azure Load Balancer now supports ICMPv4 pings to its frontend, enabling the ability to test reachability of your load balancer. Learn more about how to test reachability of your load balancer.
May 2023

SKU
Basic Load Balancer retired on September 30, 2025
Basic Load Balancer was retired on September 30, 2025. If you're still using Basic Load Balancer, migrate to Standard SKU as soon as possible.
September 2022

SKU
Gateway Load Balancer now generally available
Gateway Load Balancer is a new SKU of Azure Load Balancer targeted for scenarios requiring transparent NVA (network virtual appliance) insertion. Learn more about Gateway Load Balancer or our supported third party partners.
July 2022

SKU
Gateway Load Balancer public preview
Gateway Load Balancer is a fully managed service enabling you to deploy, scale, and enhance the availability of third party network virtual appliances (NVAs) in Azure. You can add your favorite third party appliance whether it's a firewall, inline DDoS appliance, deep packet inspection system, or even your own custom appliance into the network path transparently â all with a single action.
November 2021

Feature
Support for IP-based backend pools (General Availability)
Azure Load Balancer supports adding and removing resources from a backend pool via an IPv4 or IPv6 addresses. This enables easy management of containers, virtual machines, and Virtual Machine Scale Sets associated with Load Balancer. It will also allow IP addresses to be reserved as part of a backend pool before the associated resources are created. Learn more about backend pool management
March 2021

Feature
Instance Metadata support for Standard SKU Load Balancers and Public IPs
Metadata of Standard Public IP addresses and Standard Load Balancer can now be retrieved through Azure Instance Metadata Service (IMDS). The metadata is available from within the running instances of virtual machines (VMs) and Virtual Machine Scale Sets instances. You can use the metadata to manage your virtual machines. Learn more about Instance Metadata Service for Load Balancer
February 2021

Feature
Public IP SKU upgrade from Basic to Standard without losing IP address
As you move from Basic to Standard Load Balancers, retain your public IP address. Learn more about upgrading a public IP address
January 2021

Feature
Support for moves across resource groups
Standard Load Balancer and Standard Public IP support for resource group moves.
October 2020

Feature
Cross-region load balancing with Global tier on Standard LB
Azure Load Balancer supports Cross Region Load Balancing. Previously, Standard Load Balancer had a regional scope. With this release, you can load balance across multiple Azure regions via a single, static, global anycast Public IP address.
September 2020

Feature
Azure Load Balancer Insights using Azure Monitor
Built as part of Azure Monitor for Networks, customers now have topological maps for all their Load Balancer configurations and health dashboards for their Standard Load Balancers preconfigured with metrics in the Azure portal. Get started and learn more
June 2020

Validation
Addition of validation for HA ports
A validation was added to ensure that HA port rules and non HA port rules are only configurable when Floating IP is enabled. Previously, this configuration would go through, but not work as intended. No change to functionality was made. You can learn more about HA ports limitations
June 2020

Feature
IPv6 support for Azure Load Balancer (generally available)
You can have IPv6 addresses as your frontend for your Azure Load Balancers. Learn how to create a dual stack application here
April 2020

Feature
TCP Resets on Idle Timeout (generally available)
Use TCP resets to create a more predictable application behavior. Learn more
February 2020

## Blog posts

Stay informed with the latest insights, tutorials, and deep-dive blogs from the Azure Load Balancer team and community:

Title
Description
Date

Accelerate designing, troubleshooting & securing your network with Gen-AI powered tools, now GA
Learn how to leverage Gen-AI powered tools to accelerate network design, troubleshooting, and security for Azure Load Balancer and other networking services.
June 2025

A Guide to Azure Data Transfer Pricing
Comprehensive guide to understanding data transfer costs and pricing models for Azure Load Balancer and related networking services.
May 2025

Announcing the General Availability of Azure Load Balancer Health Event Logs
Deep dive into the new health event logs feature for enhanced monitoring and troubleshooting capabilities.
March 2025

How to build highly resilient applications with Azure Load Balancer
Best practices and architectural patterns for building resilient applications using Azure Load Balancer.
December 2024

Introducing Azure Copilot for Networking: Your AI-Powered Azure Networking Assistant
Discover how AI-powered assistance can help manage and optimize your Azure Load Balancer configurations.
December 2024

Troubleshoot health probe failures with Azure Load Balancer Health Status
Step-by-step guide to diagnosing and resolving health probe issues using the Health Status feature.
October 2024

Routing options for VMs from Private Subnets
Explore different routing strategies for VMs in private subnets when using Azure Load Balancer.
October 2024

Using Admin State to Control Your Azure Load Balancer Backend Instances
Practical guide to using the Admin State feature for easier maintenance and instance management.
August 2024

Build scalable cross-subscription applications with Azure Load Balancer
Learn how to architect applications that span multiple subscriptions using Azure Load Balancer.
June 2024

Tip

Subscribe to the Azure Networking blog to receive notifications about new Load Balancer articles and updates.

## Retirements

Name
Description
Retirement Date

Azure Load Balancer numberOfProbes property
Support for Azure Load Balancer numberOfProbes property ends on September 1, 2027. To avoid service disruption, upgrade your apps to API version 2022-05-01 or higher and start using Azure Load Balancer probeThreshold property. We will not be supporting the property numberOfProbes after September 1, 2027.
September 2027

Inbound NAT Pools for Azure Virtual Machine Scale Sets
On September 30, 2027, Inbound NAT Pools (the Azure Virtual Machine Scale Sets-specific feature of Inbound NAT rules V1) are retired. Starting November 15, 2026, you can't create new Inbound NAT Pools. To avoid service disruptions, migrate to Inbound NAT rule V2 by that date. Single VM Inbound NAT rules V1 aren't affected by this retirement.
September 2027

Azure Basic Load Balancer
Azure Basic Load Balancer retired on September 30, 2025. Existing Basic Load Balancers remain operational but are unsupported and aren't covered by SLA guarantees. Except for Cloud Services (extended support) deployments, new Basic Load Balancer deployments aren't available since March 31, 2025. For migration guidance, see Upgrade from Basic Load Balancer.
September 2025

## Known issues

The following are known issues and limitations that may affect your deployment. Where a resolution is in progress, it is noted. For issues without a planned resolution, recommended mitigations are provided.

Issue
Description
Mitigation

IP-based Load Balancer outbound IP
IP-based Load Balancers are currently not secure-by-default and will use the backend instances' default outbound access IPs for outbound connections. If the Load Balancer is a public Load Balancer, either the default outbound access IPs or the Load Balancer's frontend IP may be used.
In order to prevent backend instances behind an IP-based Load Balancer from using default outbound access, use NAT Gateway for a predictable IP address and to prevent SNAT port exhaustion, or use the private subnet feature to secure your Load Balancer.

numberOfProbes, "Unhealthy threshold"
Health probe configuration property numberOfProbes, otherwise known as "Unhealthy threshold" in Portal, isn't respected. Load Balancer health probes will probe up/down immediately after one probe regardless of the property's configured value.
To control the number of successful or failed consecutive probes necessary to mark backend instances as healthy or unhealthy, use the property "probeThreshold" instead.

## Next steps

For more information about Azure Load Balancer, see What is Azure Load Balancer? and frequently asked questions.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-08-27
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
