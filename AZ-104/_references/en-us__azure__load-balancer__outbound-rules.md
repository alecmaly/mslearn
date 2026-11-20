# https://learn.microsoft.com/en-us/azure/load-balancer/outbound-rules

Source: https://learn.microsoft.com/en-us/azure/load-balancer/outbound-rules

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
 

 

 

 

 
 
# Outbound rules for Azure Load Balancer

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Outbound rules allow you to explicitly define SNAT(source network address translation) for a public standard load balancer. This configuration allows you to use the public IPs of your load balancer to provide outbound internet connectivity for your backend instances.

This configuration enables:

- IP masquerading

- Simplifying your allow lists.

- Reduces the number of public IP resources for deployment.

With outbound rules, you have full declarative control over outbound internet connectivity. Outbound rules allow you to scale and tune this ability to your specific needs.

Outbound rules are only followed if the backend VM doesn't have an instance-level public IP address (ILPIP).

Note

For scalable outbound connectivity and to reduce the risk of SNAT port exhaustion, use Azure NAT Gateway. Alternatives include Load Balancer outbound rules and instance-level public IP addresses.

With outbound rules, you can explicitly define outbound SNAT behavior.

Outbound rules allow you to control:

- Which virtual machines are translated to which public IP addresses.

- Two rules where backend pool 1 uses both blue IP addresses, and backend pool 2 uses the yellow IP prefix.

- How outbound SNAT ports are allocated.

- If backend pool 2 is the only pool making outbound connections, give all SNAT ports to backend pool 2 and none to backend pool 1.

- Which protocols to provide outbound translation for.

- If backend pool 2 needs UDP ports for outbound, and backend pool 1 needs TCP, give TCP ports to 1 and UDP ports to 2.

- What duration to use for outbound connection idle timeout (4-120 minutes).

- If there are long running connections with keepalives, reserve idle ports for long running connections for up to 120 minutes. Assume stale connections are abandoned and release ports in 4 minutes for fresh connections

- Whether to send a TCP Reset on idle timeout.

- When timing out idle connections, do we send a TCP RST to the client and server so they know the flow is abandoned?

Important

When a backend pool is configured by IP address, it will behave as a Basic Load Balancer with default outbound enabled. For secure by default configuration and applications with demanding outbound needs, configure the backend pool by NIC.

## Outbound rule definition

Outbound rules use the same syntax as load balancing and inbound NAT rules: frontend, parameters, and backend pool.

An outbound rule sets up outbound NAT for all virtual machines in the backend pool, translating their traffic to the frontend. The parameters give you detailed control over the outbound NAT algorithm.

The parameters provide fine grained control over the outbound NAT algorithm.

## Scale outbound NAT with multiple IP addresses

Each extra IP address on a frontend gives the load balancer another 64,000 ephemeral ports to use as SNAT ports. The load balancer uses IPs based on the available ports. It moves to the next IP when the current IP can't handle more connections.

Use multiple IP addresses to plan for large-scale scenarios. Use outbound rules to mitigate SNAT exhaustion as described in Support and troubleshooting for Azure Load Balancer.

You can also use a public IP prefix directly with an outbound rule.

A public IP prefix increases the scaling of your deployment. Add the prefix to the allow list of flows coming from your Azure resources. You can set up a frontend IP configuration in the load balancer to reference a public IP address prefix.

The load balancer manages the public IP prefix. The outbound rule automatically uses other public IP addresses in the prefix when the current IP can't make more outbound connections.

Each of the IP addresses within public IP prefix provides an extra 64,000 ephemeral ports per IP address for load balancer to use as SNAT ports.

## Outbound flow idle timeout and TCP reset

Outbound rules include a parameter to control the outbound flow idle timeout so you can match it to your application's needs. Outbound idle timeouts default to 4 minutes. For more information, see configure idle timeouts.

By default, the load balancer drops the flow silently when the outbound idle timeout is reached. The `enableTCPReset` parameter gives you predictable application behavior and control. This parameter decides whether to send a bidirectional TCP Reset (TCP RST) when the outbound idle timeout occurs.

Review TCP Reset on idle timeout for details including region availability.

## Securing and controlling outbound connectivity explicitly

Load-balancing rules provide automatic programming of outbound NAT. Some scenarios benefit or require you to disable the automatic programming of outbound NAT by the load-balancing rule. Disabling via the rule allows you to control or refine the behavior.

You can use this parameter in two ways:

- Prevention of the inbound IP address for outbound SNAT. Disable outbound SNAT in the load-balancing rule.

- Tune the outbound SNAT parameters of an IP address used for inbound and outbound simultaneously. The automatic outbound NAT must be disabled to allow an outbound rule to take control. To change the SNAT port allocation of an address also used for inbound, the `disableOutboundSnat` parameter must be set to true.

The operation to configure an outbound rule fails if you attempt to redefine an IP address that is used for inbound.Disable the outbound NAT of the load-balancing rule first.

Important

Your virtual machine won't have outbound connectivity if you set this parameter to true and don't have an outbound rule to define outbound connectivity. Some operations of your VM or your application can depend on having outbound connectivity available. Make sure you understand the dependencies of your scenario and have considered impact of making this change.

Sometimes it's undesirable for a VM to create an outbound flow. There might be a requirement to manage which destinations receive outbound flows, or which destinations begin inbound flows. Use network security groups to manage the destinations that the VM reaches. Use NSGs to manage which public destinations start inbound flows.

When you apply an NSG to a load-balanced VM, pay attention to the service tags and default security rules.

Ensure that the VM can receive health probe requests from Azure Load Balancer.

If an NSG blocks health probe requests from the AZURE_LOADBALANCER default tag, your VM health probe fails and the VM is marked unavailable. The load balancer stops sending new flows to that VM.

## Azure Load Balancer outbound rule scenarios

- Configure outbound connections to a specific set of public IPs or prefix.

- Modify SNAT port allocation.

- Enable outbound only.

- Outbound NAT for VMs only (no inbound).

- Outbound NAT for internal standard load balancer.

- Enable both TCP & UDP protocols for outbound NAT with a public standard load balancer.

## Scenario 1: Configure outbound connections to a specific set of public IPs or prefix

Use this scenario to tailor outbound connections to originate from a set of public IP addresses. Add public IPs or prefixes to an allow or block list based on origination.

This public IP or prefix can be the same as used by a load-balancing rule.

To use a different public IP or prefix than what is used by a load-balancing rule:

- Create public IP prefix or public IP address.

- Create a public standard load balancer

- Create a frontend referencing the public IP prefix or public IP address you wish to use.

- Reuse a backend pool or create a backend pool and place the VMs into a backend pool of the public load balancer

- Configure an outbound rule on the public load balancer to enable outbound NAT for the VMs using the frontend. It isn't recommended to use a load-balancing rule for outbound. Disable outbound SNAT on the load-balancing rule.

## Scenario 2: Modify SNAT port allocation

You can use outbound rules to tune the automatic SNAT port allocation based on backend pool size.

If you experience SNAT exhaustion, increase the number of SNAT ports given from the default of 1024.

Each public IP address contributes up to 64,000 ephemeral ports. The number of VMs in the backend pool determines the number of ports distributed to each VM. One VM in the backend pool has access to the maximum of 64,000 ports. For two VMs, a maximum of 32,000 SNAT ports can be given with an outbound rule (2x 32,000 = 64,000).

You can use outbound rules to tune the SNAT ports given by default. You give more or less than the default SNAT port allocation provides. Each public IP address from a frontend of an outbound rule contributes up to 64,000 ephemeral ports for use as SNAT ports.

Load balancer gives SNAT ports in multiples of 8. If you provide a value not divisible by 8, the configuration operation is rejected. Each load balancing rule and inbound NAT rule consume a range of eight ports. If a load balancing or inbound NAT rule shares the same range of 8 as another, no extra ports are consumed.

If you attempt to give out more SNAT ports than are available (based on the number of public IP addresses), the configuration operation is rejected. For example, if you give 10,000 ports per VM and seven VMs in a backend pool share a single public IP, the configuration is rejected. Seven multiplied by 10,000 exceeds the 64,000 port limit. Add more public IP addresses to the frontend of the outbound rule to enable the scenario.

Revert to the default port allocation by specifying 0 for the number of ports. For more information on default SNAT port allocation, see SNAT ports allocation table.

## Scenario 3: Enable outbound only

Use a public standard load balancer to provide outbound NAT for a group of VMs. In this scenario, use an outbound rule by itself, without configuring extra rules.

Note

Azure NAT Gateway can provide outbound connectivity for virtual machines without the need for a load balancer. See What is Azure NAT Gateway? for more information.

## Scenario 4: Outbound NAT for VMs only (no inbound)

Note

Azure NAT Gateway can provide outbound connectivity for virtual machines without the need for a load balancer. See What is Azure NAT Gateway? for more information.

For this scenario:
Azure Load Balancer outbound rules and Virtual Network NAT are options available for egress from a virtual network.

- Create a public IP or prefix.

- Create a public standard load balancer.

- Create a frontend associated with the public IP or prefix dedicated for outbound.

- Create a backend pool for the VMs.

- Place the VMs into the backend pool.

- Configure an outbound rule to enable outbound NAT.

Use a prefix or public IP to scale SNAT ports. Add the source of outbound connections to an allow or block list.

## Scenario 5: Outbound NAT for internal standard load balancer

Note

Azure NAT Gateway can provide outbound connectivity for virtual machines utilizing an internal standard load balancer. See What is Azure NAT Gateway? for more information.

An internal standard load balancer doesn't have outbound connectivity until you explicitly enable it through instance-level public IPs or Virtual Network NAT, or by associating the backend pool members with an outbound-only load balancer configuration.

For more information, see Outbound-only load balancer configuration.

## Scenario 6: Enable both TCP and UDP protocols for outbound NAT with a public standard load balancer

By using a public standard load balancer, the automatic outbound NAT matches the transport protocol of the load-balancing rule.

- Disable outbound SNAT on the load-balancing rule.

- Configure an outbound rule on the same load balancer.

- Reuse the backend pool already used by your VMs.

- Specify "protocol": "All" as part of the outbound rule.

When you use only inbound NAT rules, no outbound NAT is provided.

- Place VMs in a backend pool.

- Define one or more frontend IP configurations with public IP addresses or public IP prefix.

- Configure an outbound rule on the same load balancer.

- Specify "protocol": "All" as part of the outbound rule

## Azure Load Balancer outbound rule limitations

- The maximum number of usable ephemeral ports per frontend IP address is 64,000.

- The range of the configurable outbound idle timeout is 4 to 120 minutes (240 to 7200 seconds).

- Load balancer doesn't support ICMP for outbound NAT, the only supported protocols are TCP and UDP.

- Outbound rules can only be applied to primary IPv4 configuration of a NIC. You can't create an outbound rule for the secondary IPv4 configurations of a VM or NVA. Multiple NICs are supported.

- Outbound rules for the secondary IP configuration are only supported for IPv6.

- All virtual machines within an availability set must be added to the backend pool for outbound connectivity.

- All virtual machines within a virtual machine scale set must be added to the backend pool for outbound connectivity.

## Next steps

- Learn more about Azure Standard Load Balancer

- See our frequently asked questions about Azure Load Balancer

 
 

 
 

 

 
 
 
 
 
 
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
 2026-09-03
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
