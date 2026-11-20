# https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/expressroute

Source: https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/expressroute

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
 

 

 

 

 
 
# Use site-to-site VPN as failover for Azure ExpressRoute

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This article helps network and cloud architects design resilient hybrid connectivity between an on-premises network and an Azure virtual network. It describes how to use Azure ExpressRoute private peering as the primary connection and a site-to-site VPN as a failover path. Use this pattern when the workload can tolerate the VPN path's lower and less predictable performance during an ExpressRoute outage. Don't use it as the sole backup for latency-sensitive, mission-critical, or bandwidth-intensive workloads. Use ExpressRoute multi-site resiliency for those workloads.

## Architecture

This architecture connects an on-premises network to an Azure virtual network by using ExpressRoute private peering. A site-to-site VPN connection provides a backup path in case the ExpressRoute connection becomes unavailable.

Diagram that shows a hybrid network architecture that uses ExpressRoute as the primary connectivity path and a site-to-site VPN tunnel as a failover path between an on-premises network and an Azure virtual network. On the left is a box labeled On-premises network, which contains a router at the network boundary. Two connectivity paths extend from the on-premises network toward an Azure region on the right. The first path is the ExpressRoute path. A line connects the on-premises network to a box labeled Partner edge. The partner edge connects to a box labeled Microsoft edge through two parallel links: a primary link and a secondary link. From the Microsoft edge, a line extends rightward into the Azure region and connects to the ExpressRoute gateway. The second path is the VPN backup path. A line labeled IPsec S2S VPN tunnel extends from the on-premises network, bypassing the partner edge and Microsoft edge, and connects to the VPN gateway in the Azure region. In the Azure region, a box contains two gateway icons: the ExpressRoute gateway and the VPN gateway.

Download a PowerPoint file of this architecture.

## Components

The architecture contains the following primary components:

- On-premises network. Your corporate network, including the edge router or VPN device that terminates both the ExpressRoute connection and the site-to-site VPN tunnel.

- ExpressRoute private peering. A dedicated private connection between the on-premises network and the Azure virtual network, established through a connectivity provider and terminated on an ExpressRoute virtual network gateway in Azure.

- Site-to-site VPN. An IPsec VPN tunnel over the public internet between the on-premises VPN device and an Azure VPN gateway.

For information about the ExpressRoute components, see Connect an on-premises network by using Azure ExpressRoute.

For information about the VPN connectivity components, see Connect an on-premises network by using Azure VPN Gateway.

## Scenario details

ExpressRoute provides dedicated, high-bandwidth connectivity between your on-premises infrastructure and Azure. A standard-resiliency ExpressRoute circuit has two active-active connections at one peering location, so that peering location remains a site-level failure domain. This architecture adds resilience by configuring a site-to-site VPN as a backup path. Under normal conditions, traffic flows through the ExpressRoute connection because you configure routing to prefer ExpressRoute over the VPN path. If the ExpressRoute peering location or circuit becomes unavailable, traffic fails over to the IPsec VPN tunnel.

In failover mode, the VPN path carries only the traffic that uses ExpressRoute private peering. Traffic that uses ExpressRoute Microsoft peering continues to reach Microsoft services over the internet rather than over the VPN tunnel.

## Considerations

These considerations implement the pillars of the Azure Well-Architected Framework, which is a set of guiding tenets that you can use to improve the quality of a workload. For more information, see Well-Architected Framework.

### Reliability

Reliability helps ensure that your application can meet the commitments you make to your customers. For more information, see Design review checklist for Reliability.

- Failover isn't instantaneous. When the ExpressRoute circuit becomes unavailable, the on-premises edge router detects the loss through Border Gateway Protocol (BGP) and converges onto the VPN path. Convergence time depends on the BGP timers and keepalive settings on the on-premises device. Stateful sessions that traverse ExpressRoute at the moment of failure generally drop and re-establish over the VPN path.

- Plan for failback. Because the on-premises network is configured to prefer ExpressRoute, traffic shifts back automatically when the ExpressRoute circuit recovers and BGP reconverges. Failback is itself a routing event that can disrupt stateful sessions a second time. Decide whether automatic failback is acceptable for your workload, or whether you need to gate it so operators control when traffic returns to ExpressRoute. You can gate it, for example, by using route dampening or a manual cutback.

- The backup path isn't an equivalent substitute. The site-to-site VPN runs over the public internet and is bounded by the throughput and SLA of the Azure VPN gateway SKU you choose. Treat the VPN as a degraded-mode path, not as an equivalent replacement for ExpressRoute, especially during an extended ExpressRoute outage.

- Tradeoff: resilience versus steady-state cost. This pattern improves availability by paying continuously for a backup path that's unused under normal conditions. If your workload can tolerate a longer recovery objective, or if you have an alternative such as a second ExpressRoute circuit at a different peering location, evaluate whether the cost of an always-on VPN backup matches the resilience benefit.

### Cost Optimization

Cost Optimization focuses on ways to reduce unnecessary expenses and improve operational efficiencies. For more information, see Design review checklist for Cost Optimization.

- The backup path has a steady-state cost. The Azure VPN gateway runs continuously to keep the backup tunnel ready, and it incurs costs whether or not failover ever occurs. Include the VPN gateway, the tunnel, and any associated egress charges in your baseline cost model, not only in your incident cost model.

- Size the VPN gateway for failover load, not minimum cost. The VPN gateway SKU sets the ceiling on backup-path throughput. A gateway sized for minimum steady-state cost can produce a backup that nominally exists but degrades the workload under realistic failover load. Size the gateway against the traffic the workload actually needs to carry during an ExpressRoute outage.

- Tradeoff: performance during failover versus VPN gateway cost. A higher VPN gateway SKU preserves more of the workload's normal performance envelope during failover but increases steady-state cost. Decide which of your workloads must continue at full capacity during an ExpressRoute outage and which can run in a degraded mode, and size accordingly.

### Operational Excellence

Operational Excellence covers the operations processes that deploy an application and keep it running in production. For more information, see Design review checklist for Operational Excellence.

- Validate the failover path on a regular cadence. A backup path that's never used tends to drift out of working order, through VPN misconfiguration, on-premises route-preference changes, or firmware updates that alter BGP behavior. Run controlled failover drills, or, at a minimum, monitor the health of the VPN tunnel and that BGP sessions are established on both paths, so that failover works on the day you need it.

- Monitor both paths and the routing state. Operators need visibility into ExpressRoute circuit health, VPN tunnel state, and BGP session state on the on-premises edge. Without those signals, a degraded ExpressRoute circuit or a silently broken VPN tunnel can go unnoticed until an incident.

- Govern configuration on the on-premises edge. The route-preference logic that makes failover correct is located on a device outside Azure that the cloud team often doesn't own. Treat the on-premises edge configuration as part of the workload's operational scope: include it in change management, document the route-preference policy, and review it when the on-premises network team upgrades or replaces the device.

- Decide failback policy deliberately. Whether failback is automatic on BGP reconvergence or operator-gated is an operational policy choice, not a default to inherit. Document the decision so operators know what to expect when the ExpressRoute circuit recovers.

- Tradeoff: simplicity versus operational ownership. Delegating route preference and failover behavior to the on-premises edge keeps the Azure side simple but transfers a meaningful ongoing obligation to the network team that owns the on-premises device. This obligation includes route configuration, BGP timers, validation, and change control. Make that ownership boundary explicit so the resilience of the design doesn't quietly degrade over time.

## Deployment guidance

Prerequisite. You must have an existing on-premises infrastructure that's already configured with a suitable network appliance.

This deployment guidance starts from the Deploy to Azure link for the ExpressRoute private peering virtual network quickstart template. The template starts the Azure deployment, but it doesn't complete private peering connectivity or the site-to-site VPN backup path.

- Select the following link:

- When the Azure portal opens, select the Resource group that you want to deploy these resources into, or create a new resource group. The Region and Location automatically change to match the resource group.

- Update the remaining fields if you want to change the resource names, providers, SKU, or network IP addresses for your environment.

- Select Review + create, and then select Create to deploy these resources.

- Wait for the deployment to finish.

- Before adding the VPN gateway, verify the ExpressRoute and VPN coexistence requirements: use a route-based, non-Basic VPN gateway and use a `GatewaySubnet` of /27 or shorter. Then follow the steps in Create a site-to-site VPN connection to configure the backup path.

- After you configure a VPN connection to the same on-premises network that you configured for ExpressRoute, configure your on-premises network to prefer ExpressRoute routes over the site-to-site VPN routes. For example, set a higher BGP local preference on routes learned from ExpressRoute. This setting controls the on-premises-to-Azure direction. For Azure-to-on-premises traffic, Azure prefers ExpressRoute only when both paths advertise the same prefix. The longest-prefix match takes precedence. Keep route advertisements aligned, or explicitly design more specific routes, to avoid asymmetric routing. With these routing rules in place, the site-to-site VPN serves as a backup if the ExpressRoute peering location fails.

## Contributors

Microsoft maintains this article. The following contributors wrote this article.

Principal authors:

- Sarah Parkes | Senior Cloud Solution Architect

- Cynthia Treger | Solution Engineer Global Black Belt

To see nonpublic LinkedIn profiles, sign in to LinkedIn.

## Next steps

For more information about the services in this architecture, see the following product documentation:

- Azure ExpressRoute documentation

- Create and modify an ExpressRoute circuit

- Azure VPN Gateway documentation

- Configure ExpressRoute and site-to-site coexisting connections by using PowerShell

To get foundational skills for this scenario, see the following Microsoft Learn module:

- Design and implement Azure ExpressRoute

## Related resources

For more information about hybrid networking patterns related to this architecture, see the following articles:

- Get started with Azure hybrid and adaptive cloud architecture

- Azure hybrid options

- Hub-spoke network topology in Azure

- Virtual network connectivity options and spoke-to-spoke communication

- Connect an on-premises network to Azure

- Implement a secure hybrid network

- Architecture best practices for Azure ExpressRoute

 
 

 
 

 

 
 
 
 
 
 
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
 2026-08-12
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
