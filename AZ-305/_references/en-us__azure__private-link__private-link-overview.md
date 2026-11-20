# https://learn.microsoft.com/en-us/azure/private-link/private-link-overview

Source: https://learn.microsoft.com/en-us/azure/private-link/private-link-overview

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
 

 

 

 

 
 
# What is Azure Private Link?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Private Link enables you to access Azure PaaS Services (for example, Azure Storage and SQL Database) and Azure hosted customer-owned/partner services over a private endpoint in your virtual network.

Traffic between your virtual network and the service travels the Microsoft backbone network. Exposing your service to the public internet is no longer necessary. You can create your own private link service in your virtual network and deliver it to your customers. Setup and consumption using Azure Private Link is consistent across Azure PaaS, customer-owned, and shared partner services.

Important

Azure Private Link is now generally available. Both Private Endpoint and Private Link service (service behind standard load balancer) are generally available. Different Azure PaaS will onboard to Azure Private Link at different schedules. See Private Link availability for an accurate status of Azure PaaS on Private Link. For known limitations, see Private Endpoint and Private Link Service.

Note

The feature Private Link Service Direct Connect, which allows you to connect to any privately routable destination IP address, is now in public preview. For more information and known limitations, see Private Link Service Direct Connect

Important

Azure Private Link support over IPv6 is now in public preview in limited regions. For more information, see Azure Private Link over IPv6 (Preview).

Note

Azure Private Link is one of the services that make up the Network Foundations category in Azure. Other services in this category include Azure DNS and Azure Virtual Networks. Each service has its own unique features and use cases. For more information on this service category, see Network Foundations.

For scenarios that involve public internet PaaS traffic, configure network security perimeter to set up a secure logical boundary. Network security perimeter restricts communication to services within its perimeter, and it allows nonperimeter public traffic through inbound and outbound access rules. For scalable IaaS-to-PaaS connectivity with centralized access control, see standard service endpoint.

Important

Network security perimeter is now generally available in all Azure public cloud regions and in Azure Government regions (US Gov Virginia, US Gov Texas, US Gov Arizona, US DoD East and US DoD Central). For information on supported services, see Onboarded private link resources for supported PaaS services.

## Key benefits

Azure Private Link provides the following benefits:

- Privately access services on the Azure platform: Connect your virtual network using private endpoints to all services that can be used as application components in Azure. Service providers can render their services in their own virtual network and consumers can access those services in their local virtual network. The Private Link platform handles the connectivity between the consumer and services over the Azure backbone network.

- On-premises and peered networks: Access services running in Azure from on-premises over ExpressRoute private peering, VPN tunnels, and peered virtual networks using private endpoints. There's no need to configure ExpressRoute Microsoft peering or traverse the internet to reach the service. Private Link provides a secure way to migrate workloads to Azure.

- Protection against data leakage: A private endpoint is mapped to an instance of a PaaS resource instead of the entire service. Consumers can only connect to the specific resource. Access to any other resource in the service is blocked. This mechanism provides protection against data leakage risks.

- Global reach: Connect privately to services running in other regions. The consumer's virtual network could be in region A and it can connect to services behind Private Link in region B.

- Extend to your own services: Enable the same experience and functionality to render your service privately to consumers in Azure. By placing your service behind a standard Azure Load Balancer, you can enable it for Private Link. The consumer can then connect directly to your service using a private endpoint in their own virtual network. You can manage the connection requests using an approval call flow. Azure Private Link works for consumers and services belonging to different Microsoft Entra tenants.

Note

Azure Private Link, along with Azure Virtual Network, span across Azure Availability Zones and are therefore zone resilient. To provide high availability for the Azure resource using a private endpoint, ensure that resource is zone resilient.

## Availability

For information on Azure services that support Private Link, see Azure Private Link availability.

For the most up-to-date notifications, check the Azure Private Link updates page.

## Logging and monitoring

Azure Private Link has integration with Azure Monitor. This combination allows:

- Archival of logs to a storage account.

- Streaming of events to your Event Hubs.

- Azure Monitor logging.

You can access the following information on Azure Monitor:

- Private endpoint:

- Data processed by the Private Endpoint â¯(IN/OUT)

- Private Link service:

- Data processed by the Private Link service (IN/OUT)

- NAT port availability

## Pricing

For pricing details, see Azure Private Link pricing.

## FAQs

For FAQs, see Azure Private Link FAQs.

## Limits

For limits, see Azure Private Link limits.

## Service Level Agreement

For service level agreement, see SLA for Azure Private Link.

## Next steps

- Quickstart: Create a Private Endpoint using Azure portal

- Quickstart: Create a Private Link service by using the Azure portal

- Learn module: Introduction to Azure Private Link

 
 

 
 

 

 
 
 
 
 
 
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
 2026-07-23
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
