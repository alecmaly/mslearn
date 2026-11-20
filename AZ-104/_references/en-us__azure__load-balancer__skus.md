# https://learn.microsoft.com/en-us/azure/load-balancer/skus

Source: https://learn.microsoft.com/en-us/azure/load-balancer/skus

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
 

 

 

 

 
 
# Azure Load Balancer SKUs

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 
Important

On September 30, 2025, Basic Load Balancer was retired. For more information, see the official announcement. If you are currently using Basic Load Balancer, make sure to upgrade to Standard Load Balancer as soon as possible. For guidance on upgrading, visit Upgrading from Basic Load Balancer - Guidance.

## SKU comparison

Azure Load Balancer has three stock-keeping units (SKUs) - Basic(Retired), Standard, and Gateway. Each SKU is catered towards a specific scenario and has differences in scale, features, and pricing.

To compare and understand the differences between Basic(Retired) and Standard SKU, see the following table.

Standard Load Balancer
Basic Load Balancer (retired)

Scenario
Equipped for load-balancing network layer traffic when high performance and ultra-low latency is needed. Routes traffic within and across regions, and to availability zones for high resiliency.
Equipped for small-scale applications that don't need high availability or redundancy. Not compatible with availability zones.

Backend type
IP based, NIC based
NIC based

Protocol
TCP, UDP
TCP, UDP

Backend pool endpoints
Any virtual machines or virtual machine scale sets in a single virtual network
Virtual machines in a single availability set or virtual machine scale set

Health probes
TCP, HTTP, HTTPS
TCP, HTTP

Health probe down behavior
TCP connections stay alive on an instance probe down and on all probes down.
TCP connections stay alive on an instance probe down. All TCP connections end when all probes are down.

Availability Zones
Zone-redundant or zonal frontend IP configurations can be used for inbound and outbound traffic
Not available

Type
Internal, Public
Internal, Public

Frontend IP configuration
When using a Public Standard Load Balancer, the SKU of the public IP must be Standard. Basic Public IPs are not supported on Standard LB
When using a Public Basic Load Balancer, the SKU of the public IP must be Basic. Standard Public IPs are not supported on Basic LB

Diagnostics
Azure Monitor multi-dimensional metrics
Not supported

HA Ports
Available for Internal Load Balancer
Not available

Secure by default
Closed to inbound flows unless allowed by a network security group. Internal traffic from the virtual network to the internal load balancer is allowed.
Open by default. Network security group optional.

Outbound Rules
Declarative outbound NAT configuration
Not available

TCP Reset on Idle
Available on any rule
Not available

Multiple front ends
Inbound and outbound
Inbound only

Management Operations
Most operations < 30 seconds
60-90+ seconds typical

SLA
99.99%
Not available

Global VNet Peering Support
Standard Internal Load Balancer is supported via Global VNet Peering
Not supported

NAT Gateway Support
Both Standard Internal Load Balancer and Standard Public Load Balancer are supported via Nat Gateway
Not supported

Private Link Support
Standard Internal Load Balancer is supported via Private Link
Not supported

Global tier
Standard Load Balancer supports the Global tier for Public Load Balancers enabling cross-region load balancing
Not supported

For more information, see Load balancer limits. For Standard Load Balancer details, see overview, pricing, and SLA. For information on Gateway SKU - catered for third-party network virtual appliances (NVAs), see Gateway Load Balancer overview

## Limitations

- A standalone virtual machine resource, availability set resource, or virtual machine scale set resource can reference one SKU, never both.

- Move operations:

- Resource group move operations (within same subscription) are supported for Standard Load Balancer and Standard Public IP.

- Subscription move operations are not supported for Standard Load Balancers.

## Next steps

- See Create a public Standard Load Balancer to get started with using a Load Balancer.

- Learn about using Standard Load Balancer and Availability Zones.

- Learn about Health Probes.

- Learn about using Load Balancer for outbound connections.

- Learn about Standard Load Balancer with HA Ports load balancing rules.

- Learn more about Network Security Groups.

 
 

 
 

 

 
 
 
 
 
 
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
 2025-10-17
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
