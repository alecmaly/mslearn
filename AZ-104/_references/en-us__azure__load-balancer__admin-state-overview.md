# https://learn.microsoft.com/en-us/azure/load-balancer/admin-state-overview

Source: https://learn.microsoft.com/en-us/azure/load-balancer/admin-state-overview

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
 

 

 

 

 
 
# Administrative State (Admin State) in Azure Load Balancer

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Administrative state (Admin state) is a feature of Azure Load Balancer that allows you to override the Load Balancer's health probe behavior on a per backend pool instance basis. This feature is useful in scenarios where you would like to take down your backend instance for maintenance, patching, or testing.

## Why use admin state?

Admin state is useful in scenarios where you want to have more control over the behavior of your Load Balancer. For example, you can set the admin state to up to always consider the backend instance eligible for new connections, even if the health probe indicates otherwise. Conversely, you can set the admin state to down to prevent new connections, even if the health probe indicates that the backend instance is healthy. This can be useful for maintenance or other scenarios where you want to temporarily take a backend instance out of rotation.

## Types of admin state values

There are three types of admin state values: Up, Down, None. The following table describes the effects of each state on new connections and existing connections:

Admin State
New Connections
Existing Connections

Up
Load balancer ignores the health probe and always considers the backend instance as eligible for new connections.
Load balancer disregards the configured health probe's response and always allows existing connections to persist to the backend instance.

Down
Load balancer ignores the health probe and doesn't allow new connections to the backend instance.
Load balancer ignores the health probe and existing connections are determined according to the following protocols: 
TCP: Established TCP connections to the backend instance persists.
UDP: Existing UDP flows move to another healthy instance in the backend pool.
 Note: This is similar to a Probe Down behavior.

None
Load balancer respects the health probe behavior.
Load balancer respects the health probe behavior.

Note

Load Balancer Health Probe Status metrics and Load Balancer's Insights topology reflect your configured admin state value changes.

## Design considerations

When deploying a load balancer with admin state, consider the following design considerations:

- Admin state takes effect on a per backend pool instance basis

- In a scenario where a virtual machine instance is in more than one backend pool, the admin state applied on one backend pool doesn't affect the other backend pool.

- In a scenario where a backend pool is part of multiple load balancing rules, the admin state applied on the backend pool affects all associated load balancing rules.

- Admin state will only take effect when there's a health probe configured on the load balancing rules.

## Limitations

When deploying a load balancer with admin state, consider the following limitations:

- Admin state isn't supported with inbound NAT rule.

- Admin state isn't supported for nonprobed load balancing rules.

- Admin state can't be configured during the creation of a NIC-based Load Balancer backend pool.

## Next steps

Manage Administrative State in Azure Load Balancer

 
 

 
 

 

 
 
 
 
 
 
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
 2026-01-07
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
