# https://learn.microsoft.com/en-us/azure/load-balancer/secure-load-balancer

Source: https://learn.microsoft.com/en-us/azure/load-balancer/secure-load-balancer

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
 

 

 

 

 
 
# Secure your Azure Load Balancer deployment

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Load Balancer provides Layer 4 load balancing capabilities to distribute incoming and outbound traffic among healthy backend instances. Because Load Balancer operates at the transport layer, you must combine it with network controls, identity controls, monitoring, and workload-level encryption to secure the full deployment.

This article provides security recommendations for Azure Load Balancer. Implementing these recommendations helps you fulfill your security obligations and improves the overall security posture of your deployment. For an overview of Azure's network security services and how they work together, see What is Azure network security?.

The security recommendations in this article implement Zero Trust principles: "Verify explicitly", "Use least privilege access", and "Assume breach". For comprehensive Zero Trust guidance, see the Zero Trust Guidance Center.

Important

Basic Load Balancer was retired on September 30, 2025. Existing Basic Load Balancers remain operational but are unsupported and not covered by SLA guarantees. Upgrade to Standard Load Balancer as soon as possible. For more information, see Upgrading from Basic Load Balancer - Guidance.

## Network security

Network security for Azure Load Balancer focuses on limiting inbound exposure, controlling outbound connectivity, validating backend health, and integrating with other Azure network security services.

- Use Standard Load Balancer SKU: Deploy Standard Load Balancer for production workloads. Standard Load Balancer follows a secure-by-default model with closed inbound connections, supports availability zones, and provides a 99.99% SLA. Basic Load Balancer was retired on September 30, 2025, and shouldn't be used for new deployments. For more information, see Azure Load Balancer overview.

- Implement network security groups on subnets and network interfaces: Apply network security groups (NSGs) to backend subnets and network interfaces to explicitly permit only required application traffic. Load-balancing rules map frontend traffic to backend pools, while NSGs independently determine whether that traffic is allowed. For more information, see Azure Load Balancer security baseline.

- Allow Azure Load Balancer health probe traffic: Check health-probe access separately from application-traffic access. Allow the `AzureLoadBalancer` service tag in NSGs and IP address 168.63.129.16 in local firewall policies so probes can reach backend instances. For more information, see Azure Load Balancer health probes.

- Use internal load balancer for private workloads: Deploy an internal load balancer with private frontend IP addresses when the service doesn't need direct internet exposure. Use virtual network peering, VPN, ExpressRoute, Azure Firewall, or private access patterns to control who can reach the frontend. For more information, see Azure Load Balancer components.

- Protect public load balancers with Azure DDoS Protection: Enable Azure DDoS Network Protection on the virtual network that hosts public load balancers. DDoS Protection provides enhanced DDoS mitigation and detection capabilities that monitor endpoints for threats and signs of abuse. For more information, see Protect your public load balancer with Azure DDoS Protection.

- Use explicit outbound connectivity: Don't rely on default outbound access. For API versions released after March 31, 2026, new virtual networks use private subnets by default and require an explicit outbound method to reach public endpoints. Existing virtual networks aren't changed automatically. Use Azure NAT Gateway for predictable outbound IP addresses, or configure explicit Standard Load Balancer outbound rules when NAT Gateway isn't appropriate. For more information, see Outbound connections in Azure and Azure NAT Gateway overview.

- Configure appropriate distribution mode: Select the distribution mode that fits your application and security requirements. Use the default 5-tuple hash for most workloads, and use session persistence only when the application requires it because persistence can create uneven distribution and reduce resiliency. For more information, see Azure Load Balancer distribution modes.

- Enable TCP reset for clearer connection handling: Configure TCP reset on load-balancing rules so clients and backend applications receive bidirectional TCP reset packets on idle timeout. Clear connection state helps applications recover faster and reduces ambiguous half-open connections. For more information, see Azure Load Balancer best practices.

- Secure floating IP and Gateway Load Balancer designs: When you use floating IP for high-availability scenarios, configure loopback interfaces correctly and apply host firewall controls. For Gateway Load Balancer and network virtual appliances, separate trusted and untrusted traffic on different tunnel interfaces and account for VXLAN header overhead. For more information, see Azure Load Balancer best practices.

- Integrate inspection services when needed: Azure Load Balancer is a Layer 4 service and doesn't inspect application payloads. Route traffic through Azure Firewall, network virtual appliances, Application Gateway, or Azure Front Door when you need firewalling, web application firewall, or Layer 7 inspection. For more information, see Architecture best practices for Azure Load Balancer.

## Identity and access management

Identity and access management for Azure Load Balancer controls who can create, update, delete, and review load balancer resources, rules, probes, frontend IPs, backend pools, and outbound connectivity.

- Use Microsoft Entra ID for management-plane access: Require administrators to authenticate with Microsoft Entra ID when using the Azure portal, Azure CLI, Azure PowerShell, or Azure Resource Manager APIs. Apply Conditional Access controls such as multifactor authentication, compliant device requirements, and sign-in risk policies for privileged networking roles. For more information, see Microsoft Entra Conditional Access.

- Implement Azure role-based access control: Assign Azure RBAC roles to users, groups, managed identities, and automation accounts that manage load balancers. Use built-in roles such as Network Contributor only where the full network-management scope is required. For more information, see What is Azure role-based access control?.

- Use least privilege access: Avoid broad Owner or Contributor assignments for routine load balancer operations. Create custom roles when operators need only specific permissions for load balancer read, write, rule, probe, or backend pool operations. For more information, see Azure custom roles.

- Use Privileged Identity Management for elevated access: Make high-impact roles eligible instead of permanently assigned by using Microsoft Entra Privileged Identity Management (PIM). Require approval, multifactor authentication, justification, and time-bound activation for roles that can change production load balancers. For more information, see What is Microsoft Entra Privileged Identity Management?.

- Separate duties for networking and workload teams: Limit who can change load-balancing rules, inbound NAT rules, outbound rules, backend pool membership, and probe settings. Separation of duties reduces the risk that a single compromised identity can both expose a service and change the workload behind it. For more information, see Azure RBAC best practices.

- Audit management-plane changes: Monitor Azure Activity Log events for load balancer configuration changes, role assignments, and diagnostic setting changes. Alert on unexpected updates to frontend IP configurations, rule mappings, outbound rules, or backend pool membership. For more information, see Monitor Azure Load Balancer.

## Data protection

Data protection for Azure Load Balancer focuses on protecting traffic handled by backend workloads and protecting configuration and telemetry because Load Balancer doesn't store customer application data.

- Encrypt application traffic end to end: Azure Load Balancer operates at Layer 4 and doesn't terminate TLS or inspect payloads. Configure TLS on the backend application or on a Layer 7 service in front of the backend so traffic remains encrypted where required. For more information, see Architecture best practices for Azure Load Balancer.

- Use the right service for TLS termination: If your HTTP or HTTPS workload requires TLS termination, certificate management, URL routing, or web application firewall inspection, use Azure Application Gateway or Azure Front Door instead of relying on Load Balancer for those functions. For more information, see Azure Load Balancer overview.

- Protect backend secrets and certificates: Store TLS certificates, private keys, and application secrets used by backend instances in Azure Key Vault. Use managed identities for backend workloads instead of embedding secrets in scripts, templates, or VM extensions. For more information, see Azure Key Vault overview.

- Secure diagnostic data destinations: Load balancer metrics, flow logs, and archived diagnostics can include IP addresses, ports, and topology details. Restrict access to Log Analytics workspaces, storage accounts, and Event Hubs that receive diagnostics, and use customer-managed keys for storage accounts when your compliance requirements call for them. For more information, see Azure Storage encryption.

- Avoid exposing sensitive topology in names and tags: Don't include secrets, internal project names, or sensitive network details in load balancer names, rule names, public IP DNS labels, or resource tags. These values can appear in logs, exports, alerts, and access reviews. For more information, see Naming rules and restrictions for Azure resources.

## Logging and monitoring

Logging and monitoring for Azure Load Balancer provides visibility into availability, health probes, traffic patterns, and configuration changes so teams can detect security and reliability issues quickly.

- Enable diagnostic settings: Configure diagnostic settings to send load balancer metrics and supported logs to a Log Analytics workspace, storage account, or Event Hubs for analysis and retention. For more information, see Monitor Azure Load Balancer.

- Use Azure Monitor Insights: Deploy Load Balancer Insights to view preconfigured dashboards, functional dependency diagrams, resource health, and metrics for proactive monitoring. For more information, see Use Insights to monitor and configure Azure Load Balancer.

- Configure health probe monitoring: Implement health probes that accurately represent application readiness, not just host availability. Monitor probe status so backend failures, firewall blocks, and application outages are detected before users are affected. For more information, see Manage health probes for Azure Load Balancer.

- Monitor connection and availability metrics: Track metrics such as Data Path Availability, Health Probe Status, SYN Count, SNAT Connection Count, and Allocated SNAT Ports. Use alerts to identify failed backends, anomalous connection spikes, or outbound port exhaustion. For more information, see Standard Load Balancer diagnostics with metrics, alerts, and resource health.

- Enable virtual network flow logs: Configure virtual network flow logs to analyze traffic patterns around backend subnets and identify suspicious or unexpected flows. Forward logs to your security information and event management (SIEM) system for correlation with workload and identity events. For more information, see Monitor Azure Load Balancer.

- Set up security and operations alerts: Create Azure Monitor alerts for failed health probes, low data path availability, unusual traffic increases, SNAT exhaustion indicators, and unexpected Activity Log changes. Include runbook links and owner information in alert actions. For more information, see Monitor Azure Load Balancer.

## Compliance and governance

Compliance and governance for Azure Load Balancer helps ensure consistent, supportable, and auditable configurations across subscriptions, regions, and environments.

- Implement Azure Policy controls: Use Azure Policy to audit and enforce load balancer requirements such as Standard SKU usage, diagnostic settings, tagging, and NSG associations on backend subnets. For more information, see Azure Load Balancer security baseline.

- Standardize deployment with infrastructure as code: Deploy load balancers, public IPs, rules, probes, backend pools, and outbound configurations with ARM templates, Bicep, or other approved infrastructure-as-code pipelines. Version-controlled templates reduce drift and provide evidence for compliance reviews. For more information, see Create a public load balancer using Bicep and Create a public load balancer using an ARM template.

- Use resource tagging: Apply consistent tags for workload owner, data classification, environment, business criticality, and disaster recovery tier. Tags support cost management, compliance tracking, incident routing, and ownership reviews. For more information, see Azure resource naming and tagging decision guide.

- Review unsupported and legacy configurations: Inventory Basic Load Balancers, implicit outbound dependencies, unmanaged public IPs, and missing diagnostics. Prioritize migration to Standard Load Balancer, NAT Gateway or explicit outbound rules, and monitored configurations. For more information, see Upgrade from Basic to Standard Load Balancer.

- Control changes through approved workflows: Require change review for frontend IPs, inbound rules, NAT rules, outbound rules, backend pool membership, probe paths, and idle timeout settings. Use Azure Activity Log and deployment history to validate that changes came from approved identities and pipelines. For more information, see Azure Resource Manager deployment history.

## Backup and recovery

Backup and recovery for Azure Load Balancer focuses on preserving the configuration, documenting dependencies, and designing resilient topologies that keep traffic flowing during instance, zone, or regional failures.

- Export and version the load balancer configuration: Export the Standard Load Balancer configuration as an ARM template or Bicep file and store it in source control. Capture frontend IP configurations, public IP resources, backend pools, load-balancing rules, inbound NAT rules, outbound rules, health probes, and dependencies so you can restore or recreate the deployment quickly. For more information, see Export templates in the Azure portal and Export templates with Azure CLI.

- Document the topology before changes: Record frontend IP addresses, DNS names, backend pool members, rule-to-probe mappings, NAT mappings, outbound connectivity design, NSG dependencies, route tables, and owning teams before planned changes. Current documentation reduces recovery time when a rollback or regional rebuild is needed. For more information, see Azure Load Balancer components.

- Use cross-region load balancer for multi-region failover: Deploy Cross-region Load Balancer, also known as Global Load Balancer, when you need a single global frontend that distributes traffic across regional load balancers. Pair it with regional health monitoring and tested failover procedures. For more information, see Cross-region load balancer and Deploy a cross-region load balancer using an ARM template.

- Use zone-redundant frontends for availability zone resilience: Use Standard Load Balancer with zone-redundant frontend IP configurations where availability zones are supported. Standard SKU includes built-in support for zone redundancy, and a zone-redundant frontend helps keep the data path available if a zone fails. For more information, see Azure Load Balancer best practices.

- Distribute backend pools across zones: Place backend instances in multiple availability zones by using Virtual Machine Scale Sets or zonal virtual machines. Zone-redundant backend pools reduce the chance that a single zone failure removes all healthy instances from rotation. For more information, see Migrate Load Balancer to availability zone support.

- Configure health probes for automatic in-region failover: Health probes determine which backend instances receive traffic. Configure probes against application-ready endpoints, choose appropriate intervals and thresholds, and test probe behavior during maintenance so traffic automatically fails over to healthy instances within the region. For more information, see Manage health probes for Azure Load Balancer.

- Test failover regularly: Exercise instance, zone, and regional failover scenarios on a defined schedule. Validate that probes remove unhealthy instances, Cross-region Load Balancer or DNS routing sends traffic to the secondary region, outbound connectivity still works, and monitoring alerts reach the right responders. For more information, see Azure Load Balancer best practices.

## Next steps

- Azure Load Balancer security baseline

- What is Azure network security?

 
 

 
 

 

 
 
 
 
 
 
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
