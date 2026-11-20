# https://learn.microsoft.com/en-us/azure/traffic-manager/traffic-manager-overview

Source: https://learn.microsoft.com/en-us/azure/traffic-manager/traffic-manager-overview

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
 

 

 

 

 
 
# What is Azure Traffic Manager?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Traffic Manager is a DNS-based traffic load balancer that distributes traffic to your public-facing applications across global Azure regions. Traffic Manager provides your public endpoints with high availability and quick responsiveness.

Traffic Manager uses DNS to direct client requests to the appropriate service endpoint based on a traffic-routing method. Traffic Manager also provides health monitoring for every endpoint. The endpoint can be any Internet-facing service hosted inside or outside of Azure. Traffic Manager provides a range of traffic-routing methods and endpoint monitoring options to suit different application needs and automatic failover models. Traffic Manager is resilient to failure, including the failure of an entire Azure region.

Note

Azure provides a suite of fully managed load-balancing solutions for your scenarios.

- If you want to load balance between your servers in a region at the application layer, review Application Gateway.

- If you need to optimize global routing of your web traffic and optimize top-tier end-user performance and reliability through quick global failover, see Front Door.

- To do network layer load balancing, review Load Balancer.

Your end-to-end scenarios might benefit from combining these solutions as needed.
For an Azure load-balancing options comparison, see Overview of load-balancing options in Azure.

For more information about Traffic Manager, see:

- How Traffic Manager works

- Traffic Manager FAQs

- Traffic Manager profiles

- Traffic Manager endpoints

## Key features

### Increase application availability

Traffic Manager monitors your endpoints and provides automatic failover when an endpoint goes down, delivering high availability for your critical applications.

### Improve application performance

Traffic Manager improves your application's responsiveness by directing traffic to the endpoint with the lowest latency for each user.

### Service maintenance without downtime

Perform planned maintenance on your applications without downtime. Traffic Manager directs traffic to alternative endpoints while maintenance is in progress.

### Combine hybrid applications

Traffic Manager supports external, non-Azure endpoints, enabling hybrid cloud and on-premises deployments including burst-to-cloud, migrate-to-cloud, and failover-to-cloud scenarios.

### Distribute traffic for complex deployments

Combine multiple traffic-routing methods with nested Traffic Manager profiles to create sophisticated and flexible rules that scale to larger, more complex deployments.

### Link DNS records directly to Traffic Manager

Traffic Manager Linked Records is an Azure DNS feature that connects a DNS record set directly to a Traffic Manager profile. Clients receive endpoint IP addresses directly from DNSâwithout an intermediate CNAME lookup to `trafficmanager.net`. This means `trafficmanager.net` is never exposed in DNS responses, which simplifies firewall configurations and preserves the DNSSEC chain of trust for signed zones. Endpoint type consistency is enforced through Strictly Typed Profiles.

## Pricing

For pricing information, see Traffic Manager Pricing.

## Next steps

- Learn how to create a Traffic Manager profile.

- Learn how Traffic Manager Works.

- Learn about Traffic Manager Linked Records for direct DNS-to-Traffic Manager integration.

- View frequently asked questions about Traffic Manager.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-10-19
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
