# https://learn.microsoft.com/en-us/azure/load-balancer/gateway-overview

Source: https://learn.microsoft.com/en-us/azure/load-balancer/gateway-overview

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
 

 

 

 

 
 
# Gateway Load Balancer

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Gateway Load Balancer is a SKU of the Azure Load Balancer portfolio designed for high performance and high availability scenarios with third-party Network Virtual Appliances (NVAs). By using Gateway Load Balancer, you can easily deploy, scale, and manage NVAs. Chaining a Gateway Load Balancer to your public endpoint only requires one selection.

You can insert appliances transparently for different kinds of scenarios such as:

- Firewalls

- Advanced packet analytics

- Intrusion detection and prevention systems

- Traffic mirroring

- DDoS protection

- Custom appliances

By using Gateway Load Balancer, you can easily add or remove advanced network functionality without extra management overhead. It provides the bump-in-the-wire technology you need to ensure all traffic to and from a public endpoint is first sent to the appliance before your application. In scenarios with NVAs, it's especially important that flows are symmetrical. Gateway Load Balancer maintains flow stickiness to a specific instance in the backend pool, so packets traverse the same network path in both directions. This flow symmetry gives your network virtual appliance a consistent route without further manual configuration, which appliances that need this key capability require to function seamlessly.

The health probe listens across all ports and routes traffic to the backend instances by using the HA ports rule. Traffic sent to and from Gateway Load Balancer uses the VXLAN protocol.

## Gateway Load Balancer benefits

Gateway Load Balancer offers the following benefits:

- Integrate virtual appliances transparently into the network path.

- Easily add or remove network virtual appliances in the network path.

- Scale with ease while managing costs.

- Improve network virtual appliance availability.

- Chain applications across tenants and subscriptions.

## Chain Gateway Load Balancer to a consumer resource

You can chain a Standard Public Load Balancer or a Standard IP configuration of a virtual machine to a Gateway Load Balancer. "Chaining" means the load balancer frontend or NIC IP configuration contains a reference to a Gateway Load Balancer frontend IP configuration. After you chain the Gateway Load Balancer to a consumer resource, you don't need any other configuration, such as UDRs, to ensure traffic to and from the application endpoint is sent to the Gateway Load Balancer.

Gateway Load Balancer supports both inbound and outbound traffic inspection. To insert NVAs in the path of outbound traffic by using Standard Load Balancer, you must chain the Gateway Load Balancer to the frontend IP configurations selected in the configured outbound rules.

Note

You can't configure a Gateway Load Balancer's frontend IP as the next hop in user-defined routes (UDRs). A supported consumer resource, such as a Standard Public Load Balancer or Standard NIC IP configuration, must chain or reference Gateway Load Balancer resources.

## How traffic flows through Gateway Load Balancer

When you use Gateway Load Balancer, traffic intended for the consumer application through a Standard Load Balancer is encapsulated with VXLAN headers. The Gateway Load Balancer forwards this traffic first to itself and its configured NVAs in the backend pool. The traffic then returns to the consumer resource (in this case a Standard Load Balancer) and arrives at the consumer application virtual machines with its source IP preserved. The consumer virtual network and provider virtual network can be in different subscriptions or tenants, reducing management overhead.

Figure: Diagram of gateway load balancer.

## Gateway Load Balancer components

Gateway Load Balancer consists of the following components. For general Azure Load Balancer component definitions, see Azure Load Balancer components.

- Frontend IP configuration - The IP address of your Gateway Load Balancer. This IP is private only.

- Load-balancing rules - Gateway Load Balancer rules can only be HA port rules, and a rule can be associated with up to two backend pools.

- Backend pools - The group of virtual machines or instances in a Virtual Machine Scale Set that's serving the incoming request. Gateway Load Balancer backend pools also use tunnel interfaces, described next.

- Tunnel interfaces - Gateway Load Balancer backend pools have another component called the tunnel interfaces. The tunnel interface enables the appliances in the backend to ensure network flows are handled as expected. Each backend pool can have up to two tunnel interfaces. Tunnel interfaces can be either internal or external. For traffic coming to your backend pool, use the external type. For traffic going from your appliance to the application, use the internal type.

- Chain - A Standard Public Load Balancer frontend or a Standard Public IP configuration on a virtual machine can reference a Gateway Load Balancer. The addition of advanced networking capabilities in a specific sequence is known as service chaining. As a result, this reference is called a chain. A Cross tenant chain involves chaining a Load Balancer frontend or Public IP configuration to a Gateway Load Balancer that is in another subscription. For cross tenant chaining, users need:

- Permission for the resource provider operation `Microsoft.Network/loadBalancers/frontendIPConfigurations/join/action`.

- Guest access to the subscription of the Gateway Load Balancer.

## Gateway Load Balancer pricing

For pricing, see Load Balancer pricing.

## Gateway Load Balancer limitations

- Gateway Load Balancer doesn't work with the Global Load Balancer tier, which distributes traffic across regional load balancers. For more information, see Global load balancer.

- Cross-tenant chaining isn't supported through the Azure portal.

## Next steps

- See Create a Gateway Load Balancer using the Azure portal to create a gateway load balancer.

- Learn how to use Gateway Load Balancer for outbound connectivity scenarios.

- Learn more about Azure Load Balancer.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-08-19
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
