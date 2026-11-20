# https://learn.microsoft.com/en-us/azure/ddos-protection/ddos-protection-sku-comparison

Source: https://learn.microsoft.com/en-us/azure/ddos-protection/ddos-protection-sku-comparison

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
 

 

 

 

 
 
# About Azure DDoS Protection Tier Comparison

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 The sections in this article discuss the resources and settings of Azure DDoS Protection.

## Tiers

Azure DDoS Protection supports two tier types, DDoS IP Protection and DDoS Network Protection. The tier is configured in the Azure portal during the workflow when you configure Azure DDoS Protection.

The following table shows features and corresponding tiers.

Feature
DDoS IP Protection
DDoS Network Protection

Active traffic monitoring & always on detection
Yes
Yes

L3/L4 Automatic attack mitigation
Yes
Yes

Automatic attack mitigation
Yes
Yes

Application based mitigation policies
Yes
Yes

Metrics & alerts
Yes
Yes

Mitigation reports
Yes
Yes

Mitigation flow logs
Yes
Yes

Mitigation policies tuned to customers application
Yes
Yes

Integration with Firewall Manager
Yes
Yes

Microsoft Sentinel data connector and workbook
Yes
Yes

Protection of resources across subscriptions in a tenant
Yes
Yes

Public IP Standard tier protection
Yes
Yes

Public IP Basic tier protection
No
Yes

DDoS rapid response support
Not available
Yes

Cost protection
Not available
Yes

WAF discount
Not available
Yes

Price
Per protected IP
Per 100 protected IP addresses

For the Metrics and alerts feature, peacetime telemetry (preview) extends metric availability for eligible protected public IP addresses. It's enabled automatically for supported resources protected by either DDoS Network Protection or DDoS IP Protection. This tier support doesn't establish preview availability for every region, cloud, or IP version. Free infrastructure protection alone doesn't establish peacetime telemetry eligibility.

Note

At no additional cost, Azure DDoS infrastructure protection protects every Azure service that uses public IPv4 and IPv6 addresses. This DDoS protection service helps to protect all Azure services, including platform as a service (PaaS) services such as Azure DNS. For more information on supported PaaS services, see DDoS Protection reference architectures. Azure DDoS infrastructure protection requires no user configuration or application changes. Azure provides continuous protection against DDoS attacks. DDoS protection doesn't store customer data.

## Limitations

DDoS Network Protection and DDoS IP Protection have the following limitations:

- PaaS services (multitenant), which includes Azure App Service Environment for Power Apps, Azure API Management in deployment modes other than APIM with virtual network integration, and Azure Virtual WAN aren't currently supported. For more information, see Azure DDoS Protection APIM in VNET Integration

- Protecting public IP addresses attached to Standard SKU NAT Gateway isn't supported. DDoS Protection for StandardV2 IPv4 and IPv6 public IP addresses attached to NAT Gateway StandardV2 is in preview. For protection models and prerequisites, see DDoS protection for NAT Gateway StandardV2.

- Virtual machines in Classic/RDFE deployments aren't supported.

- VPN gateway or Virtual network gateway is protected by a DDoS policy. Adaptive tuning isn't supported at this stage.

- Protection of a public IP address prefix linked to a public load balancer frontend is supported with the Azure DDoS Network Protection SKU.

- DDoS telemetry for individual virtual machine instances in Virtual Machine Scale Sets is available with Flexible orchestration mode.

DDoS IP Protection is similar to Network Protection, but has the following additional limitation:

- Public IP Basic tier protection isn't supported.

Note

Scenarios in which a single VM is running behind a public IP is supported, but not recommended. For more information, see Fundamental best practices.

For more information, see Azure DDoS Protection reference architectures.

## Next steps

- Azure DDoS Protection features

- Reference architectures

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-17
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
