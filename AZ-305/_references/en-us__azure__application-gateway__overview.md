# https://learn.microsoft.com/en-us/azure/application-gateway/overview

Source: https://learn.microsoft.com/en-us/azure/application-gateway/overview

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
 

 

 

 

 
 
# What is Azure Application Gateway?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Application Gateway is a web traffic load balancer that helps you manage traffic to your web applications. Unlike traditional load balancers that route traffic based on IP address and port, Application Gateway makes intelligent routing decisions based on HTTP request attributes like URL paths and host headers.

For example, you can route requests with `/images` in the URL to servers optimized for images, while routing `/video` requests to servers optimized for video content. This application layer routing gives you more control over how traffic flows to your applications.

This overview describes the Application Gateway v2 SKU family (Standard_v2 and WAF_v2), which is the current generation of the service. The v1 SKUs, Standard and WAF, retire on April 28, 2026, and are no longer supported. If you still run a v1 gateway, see Migrate Azure Application Gateway and Web Application Firewall from V1 to V2.

Application Gateway operates at the application layer (OSI layer 7) and provides features like SSL/TLS termination, autoscaling, zone redundancy, and integration with Web Application Firewall for security.

Note

Azure provides a suite of fully managed load-balancing solutions for your scenarios.

- If you want to do DNS based global routing and don't need Transport Layer Security (TLS) protocol termination ("SSL offload"), per-HTTP/HTTPS request, or application-layer processing, review Traffic Manager.

- If you need to optimize global routing of your web traffic and optimize top-tier end-user performance and reliability through quick global failover, see Front Door.

- To do transport layer load balancing, review Load Balancer.

Your end-to-end scenarios can benefit from combining these solutions as needed.
For an overview of the load balancing and content delivery services in Azure, see Load Balancing and Content Delivery.

## Retirement of Application Gateway V1

Microsoft deprecated Application Gateway V1 on April 28, 2023 and retired it on April 28, 2026. Microsoft no longer supports Application Gateway V1 resources, and V1 deployments that aren't migrated might experience traffic disruption as the underlying hardware is decommissioned.

If you still use Application Gateway V1, migrate to Application Gateway v2 as soon as possible. For answers to common questions about the retirement timeline and migration process, see the V1 retirement FAQ.

## Features

Application Gateway features fall into four main categories:

- Traffic routing: URL path-based routing, multiple-site hosting, redirection, rewriting HTTP headers and URLs, and cookie-based session affinity.

- Security: SSL/TLS termination at the gateway, end-to-end SSL/TLS encryption to the backend, and Web Application Firewall (WAF).

- Scale and resiliency: autoscaling, zone redundancy, a static VIP, and connection draining during backend pool changes.

- Protocol and platform support: native WebSocket and HTTP/2 support, custom error pages, and the Application Gateway Ingress Controller (AGIC) for Azure Kubernetes Service (AKS).

To learn about Application Gateway features, see Azure Application Gateway features.

## Infrastructure

An application gateway is a dedicated deployment in your virtual network that requires its own subnet, which can't contain other resource types. Infrastructure configuration covers:

- The virtual network and dedicated subnet, including subnet sizing and DNS servers for name resolution.

- The permissions and role scope needed to deploy a gateway into the subnet.

- Network security groups (NSGs) and the security rules Application Gateway requires.

- Supported user-defined routes (UDRs).

To learn about Application Gateway infrastructure, see Azure Application Gateway infrastructure configuration.

## Security

- Protect your applications against L7 layer DDoS protection by using WAF. For more information, see Application DDoS protection.

- Protect your apps from malicious actors with Bot manager rules based on Microsoftâs own Threat Intelligence.

- Secure applications against L3 and L4 DDoS attacks with Azure DDoS Protection plan.

- Privately connect to your backend behind Application Gateway with Private Link and embrace a zero-trust access model.

- Eliminate risk of data exfiltration and control privacy of communication from within the virtual network with a fully Private-only Application Gateway deployment.

- Provide a centralized security experience for your application via Azure Policy, Azure Advisor, and Microsoft Sentinel integration that ensures consistent security features across apps.

## Pricing and SLA

For Application Gateway pricing information, see Application Gateway pricing.

For Application Gateway SLA information, see Application Gateway SLA.

## What's new

To learn what's new with Azure Application Gateway, see Azure updates.

## Next steps

Depending on your requirements and environment, you can create a test Application Gateway by using the Azure portal, Azure PowerShell, or Azure CLI.

- Quickstart: Direct web traffic with Azure Application Gateway - Azure portal

- Quickstart: Direct web traffic with Azure Application Gateway - Azure PowerShell

- Quickstart: Direct web traffic with Azure Application Gateway - Azure CLI

- Learn module: Introduction to Azure Application Gateway

- How an application gateway works

- Frequently asked questions about Azure Application Gateway

 
 

 
 

 

 
 
 
 
 
 
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
 2026-09-10
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
