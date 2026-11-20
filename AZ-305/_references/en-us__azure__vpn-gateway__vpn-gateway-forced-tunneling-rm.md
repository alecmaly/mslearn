# https://learn.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-forced-tunneling-rm

Source: https://learn.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-forced-tunneling-rm

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
 

 

 

 

 
 
# About forced tunneling for site-to-site configurations

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This article helps you understand how forced tunneling works for site-to-site (S2S) IPsec connections. By default, Internet-bound traffic from your workloads and VMs within a virtual network is sent directly to the Internet.

Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via S2S VPN tunnel for inspection and auditing. This is a critical security requirement for most enterprise IT policies. Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.

The following example shows all Internet traffic being forced through the VPN gateway back to the on-premises location for inspection and auditing.

## Configuration methods for forced tunneling

There are a few different ways that you can configure forced tunneling.

### Configure using BGP

You can configure forced tunneling for VPN Gateway via BGP. You need to advertise a default route of 0.0.0.0/0 via BGP from your on-premises location to Azure so that all your Azure traffic is sent via the VPN Gateway S2S tunnel.

### Configure using Default Site

You can configure forced tunneling by setting the Default Site for your route-based VPN gateway. For steps, see Forced tunneling via Default Site.

- You assign a Default Site for the virtual network gateway using PowerShell.

- The on-premises VPN device must be configured using 0.0.0.0/0 as traffic selectors.

## Routing Internet-bound traffic for specific subnets

By default, all Internet-bound traffic goes directly to the Internet if you don't have forced tunneling configured. When forced tunneling is configured, all Internet-bound traffic is sent to your on-premises location.

In some cases, you might want Internet-bound traffic only from certain subnets (but not all subnets) to traverse from the Azure network infrastructure directly out to the Internet, rather than to your on-premises location. This scenario can be configured using a combination of forced tunneling and virtual network custom user-defined routes (UDRs). For steps, see Route Internet-bound traffic for specific subnets.

## Next steps

- See How to configure forced tunneling via Default Site for VPN Gateway S2S connections.

- For more information about virtual network traffic routing, see VNet traffic routing.

 
 

 
 

 

 
 
 
 
 
 
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
 2025-03-31
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
