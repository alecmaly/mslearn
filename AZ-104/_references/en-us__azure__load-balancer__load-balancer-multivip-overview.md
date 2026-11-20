# https://learn.microsoft.com/en-us/azure/load-balancer/load-balancer-multivip-overview

Source: https://learn.microsoft.com/en-us/azure/load-balancer/load-balancer-multivip-overview

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
 

 

 

 

 
 
# Multiple frontends for Azure Load Balancer

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Load Balancer supports multiple frontend IP configurations on a single resource. Each frontend provides an independent entry point for inbound traffic, so you can expose multiple services, domains, or protocols through one load balancer.

This article explains when multiple frontends are useful, how traffic flows from frontends through rules to backend pools, and what to consider when designing a multi-frontend topology.

Tip

If you only need a single frontend, start with the public load balancer quickstart or internal load balancer quickstart. You can add frontends later without recreating the resource.

## When to use multiple frontends

Use multiple frontends when you need to:

- Host multiple websites or services â Assign a dedicated public IP to each service (for example, `app1.contoso.com` and `app2.contoso.com`) while sharing a single backend pool.

- Separate protocols on different IPs â Expose HTTP on one frontend IP and TCP/UDP on another to simplify network security group rules and monitoring.

- Scale beyond single-IP inbound NAT port limits â A single IP supports up to 65,535 ports per protocol. In large-scale deployments that use inbound NAT rules to map a unique port to each backend instance (for example, per-VM SSH or RDP access), a second frontend IP provides an additional full port range.

Note

Each load balancer supports a maximum number of frontend configurations. See Load Balancer service limits for current limits. Each public frontend IP also incurs a charge. See IP address pricing for details.

## How multiple frontends work

A frontend IP configuration is the entry point for traffic into the load balancer. Each frontend is referenced by one or more rules that determine how traffic is handled:

Rule type
Relationship to frontend

Load balancing rule
Distributes inbound traffic arriving on a frontend IP:port across all healthy instances in a backend pool.

Inbound NAT rule
Maps a specific frontend IP:port to a single backend instance:port, enabling direct access to individual VMs.

Outbound rule
Designates which frontend IP(s) provide SNAT ports for outbound connections initiated by backend instances.

Multiple rules of any type can reference the same frontend, and multiple frontends can target the same backend pool. When multiple rules share a backend pool, those rules can share a single health probe as long as they target the same backend port and protocol.

### Same backend port versus different backend port

When multiple load balancing rules from different frontends target the same backend pool, you can route to:

- Different backend ports â Each rule specifies a unique backend port. No extra configuration is needed.

- The same backend port â You must enable Floating IP on each rule.

Without Floating IP, the load balancer translates the destination address to the backend VM's private IP. When two frontends both route to the same backend port, the VM receives traffic on the same IP:port regardless of which frontend it arrived on. The VM has no way to distinguish between the two flows or respond on the correct frontend IP.

Enabling Floating IP changes this behavior because the load balancer delivers packets with the original frontend IP preserved as the destination address. When you use Floating IP, you must configure the targeted backend VMs with a loopback interface or secondary IP that matches each frontend IP so the VMs can accept and respond to traffic correctly. For more information, see Floating IP configuration.

## Next steps

- Learn how to manage rules for Azure Load Balancer, including adding and removing frontend IP configurations.

- Learn about Floating IP configuration for same-port scenarios.

- Learn about Azure Load Balancer outbound connections.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-05-04
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
