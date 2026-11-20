# https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/default-outbound-access

Source: https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/default-outbound-access

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
 

 

 

 

 
 
# Default outbound access in Azure

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 In Azure, when you deploy a virtual machine (VM) in a virtual network without an explicitly defined outbound connectivity method, Azure automatically assigns it an outbound public IP address. This IP address enables outbound connectivity from the resources to the internet and to other public endpoints within Microsoft. This access is referred to as default outbound access.

Examples of explicit outbound connectivity for virtual machines are:

- Deployed in a subnet associated to a NAT gateway.

- Deployed in the backend pool of a standard load balancer with outbound rules defined.

- Deployed in the backend pool of a basic public load balancer.

- Virtual machines with public IP addresses explicitly associated to them.

## How and when default outbound access is provided

If a Virtual Machine (VM) is deployed without an explicit outbound connectivity method, Azure assigns it a default outbound public IP address. This IP, known as the default outbound access IP, is owned by Microsoft and can change without notice. Additionally, default outbound connectivity relies on an implicit platform behavior and may be affected by platformâlevel changes. For scenarios requiring deterministic outbound behavior, we recommend using an explicit configuration.

Note

In some cases, a default outbound IP is still assigned to virtual machines in a nonprivate subnet, even when an explicit outbound methodâsuch as a NAT Gateway or a UDR directing traffic to an NVA/firewallâis configured. This doesn't mean the default outbound IPs are used for egress unless those explicit methods are removed. To completely remove the default outbound IPs, the subnet must be made private, and the virtual machines must be stopped and deallocated.

Important

For the API released after March 31, 2026, new virtual networks default to using private subnets. Virtual machines in those subnets need an explicit outbound method to reach public endpoints on the internet and within Microsoft. This default behavior change doesn't modify existing virtual networks. For details and transition guidance, see Retirement of default outbound access: scope and impact and the official announcement.

## Retirement of default outbound access: scope and impact

Azure is changing the default subnet configuration for new virtual networks to require explicit outbound connectivity. This change isn't a blanket shutdown of default outbound access for existing virtual networks. Because default outbound access is an implicit platform behavior rather than a resource you configure, check your subnet configuration and outbound connectivity method to understand the impact on your workloads.

For the timeline and the latest announcement details, see the official announcement.

### What's affected

For the API version released after March 31, 2026, subnets in new virtual networks have `defaultOutboundAccess` set to `false` by default. Virtual machines in these private subnets can't rely on default outbound access. Configure an explicit outbound method if they need to reach public endpoints. The Azure portal already defaults to private subnets. Deployments that use earlier API versions retain the earlier default behavior.

### What isn't affected

Existing virtual networks aren't changed. Both existing virtual machines and new virtual machines created in those networks can continue to receive default outbound IP addresses unless the subnets are explicitly changed to private. We still recommend explicit outbound connectivity for predictable egress behavior.

Virtual machines that already use an explicit outbound connectivity method continue to use that method. Examples include:

- Azure NAT Gateway associated with the subnet.

- A public IP address assigned to the virtual machine's network interface.

- Outbound rules on a Standard public load balancer that includes the virtual machine in its backend pool.

Outbound connectivity for these virtual machines continues to use the explicit method you configured.

Note

A default outbound IP address might still be assigned to a virtual machine in a nonprivate subnet even when an explicit outbound method is configured. The virtual machine doesn't use that address for egress unless the explicit method is removed. For more information, see How and when default outbound access is provided.

### How to transition

For a new private subnet, configure an explicit outbound method before a workload needs to access public endpoints. For an existing nonprivate subnet, plan and configure explicit outbound connectivity before you change the subnet to private. To choose a method and configure it, see How can I transition to an explicit method of public connectivity (and disable default outbound access)? later in this article, and the design guidance in Azure NAT Gateway and Outbound connectivity with Azure Load Balancer.

## Why is disabling default outbound access recommended?

Security: Default internet access contradicts Zero Trust principles.

Clarity: Explicit connectivity is preferred over implicit access.

Stability: The default outbound IP isnât customer-owned and can change; service updates may also affect default outbound behavior, both of which can cause disruptions.

Some examples of configurations that don't work when using default outbound access:

- Multiple NICs on a VM can yield inconsistent outbound IPs

- Scaling Azure Virtual Machine Scale Sets can result in changing outbound IPs

- Outbound IPs aren't consistent or contiguous across Virtual Machine Scale Set instances

Additionally,

- Default outbound access IPs don't support fragmented packets

- Default outbound access IPs don't support ICMP pings

## How can I transition to an explicit method of public connectivity (and disable default outbound access)?

### Private subnets overview

- Creating a subnet to be Private prevents any virtual machines on the subnet from utilizing default outbound access to connect to public endpoints.

- VMs on a Private subnet can still access the internet (or any public endpoints within Microsoft) using explicit outbound connectivity.

Note

Certain services don't function on a virtual machine in a private subnet without an explicit method of egress (examples are Windows Activation and Windows Updates).

### How to configure private subnets

- 
Portal

- 
PowerShell

- 
Azure CLI

- 
ARM Template

Manual configuration steps in the Azure portal (no wizard)

- Open the Azure portal.

- Go to Virtual networks.

- Select the virtual network that contains the subnet you want to modify.

- In the left menu, select Subnets.

- Select the subnet you want to make private.

- Locate the Default outbound access setting.

- Set Default outbound access to Disabled.

- Select Save.

This explicitly sets the subnet property:

`defaultOutboundAccess = false
`

which prevents Azure from assigning default outbound public IPs to virtual machines in this subnet.

The following script takes the names of the Resource Group and Virtual Network and loops through each subnet to enable private subnet.

`$resourceGroupName = ""
$vnetName = ""
 
$vnet = Get-AzVirtualNetwork -ResourceGroupName $resourceGroupName -Name $vnetName
 
foreach ($subnet in $vnet.Subnets) {
 if ($subnet.DefaultOutboundAccess -eq $null) {
 $subnet.DefaultOutboundAccess = $false
 Write-Output "Set 'defaultoutboundaccess' to \$false for subnet: $($subnet.Name)"
 } 
 elseif ($subnet.DefaultOutboundAccess -eq $false) {
 # Output message if the value is already $false
 Write-Output "already private for subnet: $($subnet.Name)"
 }
}
Set-AzVirtualNetwork -VirtualNetwork $vnet
`

Update the subnet with az network vnet subnet update and set `--default-outbound` to "false"

`az network vnet subnet update --resource-group rgname --name subnetname --vnet-name vnetname --default-outbound false
`

Set the value of `defaultOutboundAccess` parameter to be "false"

`{
 "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
 "contentVersion": "1.0.0.0",
 "parameters": {
 "vnetName": {
 "type": "string",
 "defaultValue": "testvm-vnet"
 },
 "subnetName": {
 "type": "string",
 "defaultValue": "default"
 },
 "subnetPrefix": {
 "type": "string",
 "defaultValue": "10.1.0.0/24"
 },
 "vnetAddressPrefix": {
 "type": "string",
 "defaultValue": "10.1.0.0/16"
 }
 },
 "resources": [
 {
 "type": "Microsoft.Network/virtualNetworks",
 "apiVersion": "2023-11-01",
 "name": "[parameters('vnetName')]",
 "location": "westus2",
 "properties": {
 "addressSpace": {
 "addressPrefixes": [
 "[parameters('vnetAddressPrefix')]"
 ]
 },
 "subnets": [
 {
 "name": "[parameters('subnetName')]",
 "properties": {
 "addressPrefix": "[parameters('subnetPrefix')]",
 "defaultoutboundaccess": false
 }
 }
 ]
 }
 }
 ]
}
`

Important

Existing virtual machines must be stopped and deallocated for the change of a subnet (either from non-private to private, or the reverse) to take effect on their network interfaces.

### Limitations of private subnets

- To activate or update virtual machine operating systems, such as Windows, an explicit outbound connectivity method is required.

- In configurations using User Defined Routes (UDRs), any configured routes with next hop type `Internet` break in a Private subnet.

- A common example is the use of a UDR to steer traffic to an upstream network virtual appliance/firewall, with exceptions for certain Azure Service Tags to bypass inspection. This is done by configuring routes to these Service Tags with next hop type `Internet`. In this scenario you configure the following:

- A default route for the destination 0.0.0.0/0, with a next hop type of Virtual Appliance applies in the general case.

- One or more routes are configured to Service Tag destinations with next hop type `Internet`, to bypass the NVA/firewall. Unless an explicit outbound connectivity method is also configured for the source of the connection to these destinations, attempts to connect to these destinations fail, because default outbound access isn't available by default in a Private subnet.

- This limitation doesn't apply to the use of Service Endpoints, which use a different next hop type `VirtualNetworkServiceEndpoint`. See Virtual Network service endpoints.

- Virtual machines are still able to access Azure Storage accounts in the same region in a private subnet without an explicit method of outbound. NSGs are recommended to control egress connectivity.

- Private subnets aren't applicable to delegated or managed subnets used for hosting PaaS services. In these scenarios, outbound connectivity is managed by the individual service. Please refer to service-specific documentation for more information.

Important

When a load balancer backend pool is configured by IP address, it uses default outbound access due to an ongoing known issue. For secure by default configuration and applications with demanding outbound needs, associate a NAT gateway to the VMs in your load balancer's backend pool to secure traffic. See more on existing known issues.

### Add an explicit outbound method

- Associate a NAT gateway to the subnet of your virtual machine. Note this is the recommended method for most scenarios.

- Associate a standard load balancer configured with outbound rules.

- Associate a Standard public IP to any of the virtual machine's network interfaces.

- Add a Firewall or Network Virtual Appliance (NVA) to your virtual network and point traffic to it using a User Defined Route (UDR).

#### Use flexible orchestration mode for Virtual Machine Scale Sets

- Flexible scale sets are secure by default. Any instances created via Flexible scale sets don't have the default outbound access IP associated with them, so an explicit outbound method is required. For more information, see Flexible orchestration mode for Virtual Machine Scale Sets

### FAQs: Clearing Default Outbound IP Alert

#### Why do I see an alert showing I have a default outbound IP on my VM?

There's a NIC-level parameter (defaultOutboundConnectivityEnabled) which tracks if default outbound IP is allocated to a VM/Virtual Machine Scale Set instance. This is used to generate an Azure portal banner for VM/Virtual Machine Scale Set that flags this state. There are also specific Azure Advisor recommendations with this information for your subscriptions. If you want to view which of your virtual machines or Virtual Machine Scale Sets have a default outbound IP assigned to them, follow these steps:

- Type 'Advisor' into the search bar in the Azure portal and then select this option when it comes up.

- Select 'Operational Excellence'

- Look for the recommendations 'Add explicit outbound method to disable default outbound' and/or 'Add explicit outbound method to disable default outbound for Virtual Machine Scale Sets' (note these are two different items)

- If either of these exist, select the respective recommendation name and you will see the network interface cards (NICs) of all the virtual machnes/Virtual Machine Scale Set instances that have default outbound enabled.

#### How do I clear this alert?

- An explicit method of outbound must be utilized for the flagged VM/Virtual Machine Scale Set. See the section above for different options.

- The subnet should be made private to prevent new default outbound IPs from being created.

- Any applicable virtual machines in the subnet with the flag must be stopped and deallocated for the changes to be reflected in the NIC-level parameter and the flag to clear. (Note this is also true in the reverse; in order for a machine to be given a default outbound IP after having the subnet-level parameter set to false, a stop/deallocate of the virtual machine is required.)

#### I already am using an explicit method of outbound, so why do I still see this alert?

In some cases, a default outbound IP is still assigned to virtual machines in a nonprivate subnet, even when an explicit outbound methodâsuch as a NAT Gateway or a UDR directing traffic to an NVA/firewallâis configured. This doesn't mean the default outbound IPs are used for egress unless those explicit methods are removed. To completely remove the default outbound IPs (and remove the alert), the subnet must be made private, and the virtual machines must be stopped and deallocated.

### FAQs: Default Behavior Change to Private Subnets

#### What does making private subnets default mean, and how will it be implemented?

In the API version released after March 31, 2026, the defaultOutboundAccess property for subnets in new VNETs will be set to "false" by default. This change makes subnets private by default and prevents generation of default outbound IPs for virtual machines in those subnets. (Azure portal already defaults to subnets as private by default.) This behavior applies across all other configuration methods--ARM templates, PowerShell, and CLI. Earlier versions of ARM templates (or tools like Terraform that can specify older versions) will continue to set defaultOutboundAccess as null, which implicitly allows outbound access.

#### What happens to my existing VNETs and virtual machines? What about new virtual machines created in existing VNETs?

No changes are made to existing VNETs. This means that both existing virtual machines and newly created virtual machines in these VNETs continue to generate default outbound IP addresses unless the subnets are manually modified to become private.

#### What about new virtual network deployments? My infrastructure has a dependency on default outbound IPs and isn't ready to move to private subnets at this time.

You can still configure subnets as nonprivate using any supported method (ARM templates, portal, CLI, PowerShell). This ensures compatibility for infrastructures that rely on default outbound IPs and aren't yet ready to transition to private subnets. Please note if you already have a private subnet enabled and want to transistion back to using default outbound for a virtual machine, you will need to modify the subnet to not be private and then perform a stop/deallocate on the virtual machine.

## Next steps

For more information on outbound connections in Azure, see:

- Source Network Address Translation (SNAT) for outbound connections.

- What is Azure NAT Gateway?

 
 

 
 

 

 
 
 
 
 
 
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
