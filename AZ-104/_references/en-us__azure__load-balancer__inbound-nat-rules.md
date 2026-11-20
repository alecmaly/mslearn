# https://learn.microsoft.com/en-us/azure/load-balancer/inbound-nat-rules

Source: https://learn.microsoft.com/en-us/azure/load-balancer/inbound-nat-rules

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
 

 

 

 

 
 
# Inbound NAT rules

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 An inbound NAT rule is used to forward traffic from a load balancer frontend to one or more instances in the backend pool.

## Why use an inbound NAT rule?

An inbound NAT rule is used for port forwarding. Port forwarding lets you connect to virtual machines by using the load balancer frontend IP address and port number. The load balancer receives the traffic on a port, and based on the inbound NAT rule, forwards the traffic to a designated virtual machine on a specific backend port. Note, unlike load balancing rules, inbound NAT rules don't need a health probe attached to it.

## Types of inbound NAT rules

There are two types of inbound NAT rule available for Azure Load Balancer, version 1 and version 2.

Note

The recommendation is to use Inbound NAT rule V2 for Standard Load Balancer deployments targeting multiple virtual machines or virtual machine scale sets. For single virtual machine port, Inbound NAT rule V1 continues to be fully supported.

### Inbound NAT rule V2

An inbound NAT rule targeting multiple virtual machines references the entire backend pool. A range of frontend ports are preallocated based on the rule settings of Frontend port range start and Maximum number of machines in the backend pool.

During inbound port rule creation, port mappings are made to the backend pool from the preallocated range that's defined in the rule.

When the backend pool is scaled down, existing port mappings for the remaining virtual machines persist. When the backend pool is scaled up, new port mappings are created automatically for the new virtual machines added to the backend pool. An update to the inbound NAT rule settings isn't required.

Note

If the predefined frontend port range doesn't have a sufficient number of frontend ports available, scaling up the backend pool is blocked. This blockage could result in a lack of network connectivity for the new instances.

### Inbound NAT rule V1 - single virtual machine

Inbound NAT rule V1 for a single virtual machine provides a 1:1 port mapping between a load balancer frontend IP/port and a specific backend virtual machine. This is used for scenarios such as SSH or RDP access to individual VMs through the load balancer.

### Inbound NAT Pools (Azure Virtual Machine Scale Sets) â Retiring September 30, 2027

Inbound NAT Pools are a feature of Inbound NAT rules V1 that automatically create Inbound NAT rules per Azure Virtual Machine Scale Set instance. The load balancer's frontend IP address and a range of frontend ports are used to map connections to individual Virtual Machine Scale Sets instances.

Important

On September 30, 2027, Inbound NAT Pools (the Virtual Machine Scale Sets-specific feature of Inbound NAT rules V1) will be retired and starting November 15, 2026, you will not be able to create new Inbound NAT Pools. If you are currently using Inbound NAT Pools with Virtual Machine Scale Sets, upgrade to Inbound NAT rules V2 prior to the retirement date. Single VM Inbound NAT rules V1 are not affected by this retirement.

## Port mapping retrieval

You can use the portal to retrieve the port mappings for virtual machines in the backend pool. For more information, see Manage inbound NAT rules.

## Next steps

For more information about Azure Load Balancer inbound NAT rules, see:

- Manage inbound NAT rules

- Tutorial: Create a multiple virtual machines inbound NAT rule using the Azure portal

- Tutorial: Create a single virtual machine inbound NAT rule using the Azure portal

- Tutorial: Migrate from Inbound NAT Pools to NAT Rules

 
 

 
 

 

 
 
 
 
 
 
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
 2026-05-22
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
