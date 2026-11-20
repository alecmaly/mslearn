# https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-manage-subnet

Source: https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-manage-subnet

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
 

 

 

 

 
 
# Add, change, or delete a virtual network subnet

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure virtual network subnets are essential containers where all Azure resources are deployed within a virtual network. This comprehensive guide explains how to add, change, or delete virtual network subnets using the Azure portal, Azure CLI, or Azure PowerShell, helping you effectively manage your network infrastructure.

## Prerequisites

- 
Portal

- 
Azure CLI

- 
PowerShell

- An Azure account with an active subscription. Create an account for free.

- An existing Azure virtual network. To create one, see Quickstart: Create a virtual network by using the Azure portal.

- To run the procedures, sign in to the Azure portal with your Azure account.

- An Azure account with an active subscription. Create an account for free.

- An existing Azure virtual network. To create one, see Quickstart: Create a virtual network by using Azure CLI.

You can run the commands either in the Azure Cloud Shell or from Azure CLI on your computer.

- Azure Cloud Shell is a free interactive shell that has common Azure tools preinstalled and configured to use with your account. To run the commands in the Cloud Shell, select Open Cloud shell at the upper-right corner of a code block. Select Copy to copy the code, and paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

- If you install Azure CLI locally to run the commands, you need Azure CLI version 2.31.0 or later. Run az version to find your installed version, and run az upgrade to upgrade.

Run `az login` to connect to Azure.

- An Azure account with an active subscription. Create an account for free.

- An existing Azure virtual network. To create one, see Quickstart: Create a virtual network by using Azure PowerShell.

You can run the commands either in the Azure Cloud Shell or from PowerShell on your computer.

- Azure Cloud Shell is a free interactive shell that has common Azure tools preinstalled and configured to use with your account. To run the commands in the Cloud Shell, select Open Cloud shell at the upper-right corner of a code block. Select Copy to copy the code, and paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

- If you install Azure PowerShell locally to run the commands, you need Azure PowerShell module version 5.4.1 or later. Run `Get-Module -ListAvailable Az` to find your installed version. If you need to upgrade, see Update the Azure PowerShell module.

Also make sure your `Az.Network` module is 4.3.0 or later. To verify the installed module, use `Get-InstalledModule -Name Az.Network`. To update, use the command `Update-Module -Name Az.Network`.

Run `Connect-AzAccount` to connect to Azure.

### Permissions

To do tasks on subnets, your account must be assigned to the Network contributor role or to a custom role assigned the appropriate actions in the following list:

Action
Name

Microsoft.Network/virtualNetworks/subnets/read
Read a virtual network subnet.

Microsoft.Network/virtualNetworks/subnets/write
Create or update a virtual network subnet.

Microsoft.Network/virtualNetworks/subnets/delete
Delete a virtual network subnet.

Microsoft.Network/virtualNetworks/subnets/join/action
Join a virtual network.

Microsoft.Network/virtualNetworks/subnets/joinViaServiceEndpoint/action
Enable a service endpoint for a subnet.

Microsoft.Network/virtualNetworks/subnets/virtualMachines/read
Get the virtual machines in a subnet.

Note

If attempts to add, change, or delete a subnet in your virtual network fail, ensure there are no connections to other resources that may block the action:

- Gateway connections

- Gateways

- IPs

- Virtual network peerings

- App Service Environment (ASE)

## Add a subnet

- 
Portal

- 
Azure CLI

- 
PowerShell

- In the Azure portal, search for and select virtual networks.

- On the Virtual networks page, select the virtual network you want to add a subnet to.

- On the virtual network page, select Subnets from the left navigation.

- On the Subnets page, select + Subnet.

- On the Add subnet screen, enter or select values for the subnet settings.

- Select Save.

Run the az network vnet subnet create command with the options you want to configure.

`az network vnet subnet create \
 --name <subnetName> \
 --resource-group <resourceGroupName> \
 --vnet-name <virtualNetworkName>
`

- Use the Add-AzVirtualNetworkSubnetConfig command to configure the subnet.

`$vnet = Get-AzVirtualNetwork @vnetParams
$subnetParams = @{
 Name = "<subnetName>"
 VirtualNetwork = $vnet
 AddressPrefix = "<String[]>"
}
Add-AzVirtualNetworkSubnetConfig @subnetParams
`

- Then associate the subnet configuration to the virtual network with Set-AzVirtualNetwork.

`Set-AzVirtualNetwork -VirtualNetwork $vnet
`

You can configure the following settings for a subnet:

Setting
Description

Name
The name must be unique within the virtual network. For maximum compatibility with other Azure services, use a letter as the first character of the name. For example, Azure Application Gateway can't deploy into a subnet whose name starts with a number.

Subnet address range
The range must be unique within the address space and can't overlap with other subnet address ranges in the virtual network. You must specify the address space by using Classless Inter-Domain Routing (CIDR) notation.

For example, in a virtual network with address space `10.0.0.0/16`, you might define a subnet address space of `10.0.0.0/22`. The smallest range you can specify is `/29`, which provides eight IP addresses for the subnet. Azure reserves the first and last address in each subnet for protocol conformance, and three more addresses for Azure service usage. So defining a subnet with a /29 address range gives three usable IP addresses in the subnet.

If you plan to connect a virtual network to a virtual private network (VPN) gateway, you must create a gateway subnet. For more information, see Gateway subnet.

Add IPv6 address space
You can create a dual-stack virtual network that supports IPv4 and IPv6 by adding an existing IPv6 address space. Currently, IPv6 isn't fully supported for all services in Azure. For more information, see Overview of IPv6 for Azure Virtual Network

Private Subnet
Setting a subnet as private prevents the use of default outbound access for any virtual machines created in the subnet. This feature is in Preview.

NAT gateway
To provide network address translation (NAT) to resources on a subnet, you can associate an existing NAT gateway to a subnet. The NAT gateway must exist in the same subscription and location as the virtual network. For more information, see Virtual network NAT and Quickstart: Create a NAT gateway by using the Azure portal.

Network security group
To filter inbound and outbound network traffic for the subnet, you can associate an existing network security group (NSG) to a subnet. The NSG must exist in the same subscription and location as the virtual network. For more information, see Network security groups and Tutorial: Filter network traffic with a network security group by using the Azure portal.

Route table
To control network traffic routing to other networks, you can optionally associate an existing route table to a subnet. The route table must exist in the same subscription and location as the virtual network. For more information, see Virtual network traffic routing and Tutorial: Route network traffic with a route table by using the Azure portal.

Service endpoints
You can optionally enable one or more service endpoints for a subnet. To enable a service endpoint for a service during portal subnet setup, select the service or services that you want service endpoints for from the popup list under Services. Azure configures the location automatically for an endpoint. To remove a service endpoint, deselect the service you want to remove the service endpoint for. For more information, see Virtual network service endpoints.

By default, Azure configures the service endpoints for the virtual network's region. To support regional failover scenarios, Azure automatically configures endpoints to Azure paired regions for Azure Storage.

Once you enable a service endpoint, you must also enable subnet access for resources the service creates. For example, if you enable the service endpoint for Microsoft.Storage, you must also enable network access to all Azure Storage accounts you want to grant network access to. To enable network access to subnets that a service endpoint is enabled for, see the documentation for the individual service.

To validate that a service endpoint is enabled for a subnet, view the effective routes for any network interface in the subnet. When you configure an endpoint, you see a default route with the address prefixes of the service, and a next hop type of VirtualNetworkServiceEndpoint. For more information, see Virtual network traffic routing.

Subnet delegation
You can optionally enable one or more delegations for a subnet. Subnet delegation gives explicit permissions to the service to create service-specific resources in the subnet by using a unique identifier during service deployment. To delegate for a service during portal subnet setup, select the service you want to delegate to from the popup list.

Network policy for private endpoints
To control traffic going to a private endpoint, you can use Network security groups or Route tables. During portal subnet setup, select either or both of these options under Private endpoint network policy to use these controls on a subnet. Once enabled, network policy applies to all private endpoints on the subnet. For more information, see Manage network policies for private endpoints.

## Change subnet settings

- 
Portal

- 
Azure CLI

- 
PowerShell

- In the Azure portal, search for and select virtual networks.

- On the Virtual networks page, select the virtual network you want to change subnet settings for.

- On the virtual network's page, select Subnets from the left navigation.

- On the Subnets page, select the subnet you want to change settings for.

- On the subnet screen, change the subnet settings, and then select Save.

Run the az network vnet subnet update command with the options you want to change.

`az network vnet subnet update
`

Run the Set-AzVirtualNetworkSubnetConfig command with the options you want to change. Then set the configuration with `Set-AzVirtualNetwork`.

You can change the following subnet settings after the subnet is created:

Setting
Description

Subnet address range
If no resources are deployed within the subnet, you can change the address range. If any resources exist in the subnet, you must first either move the resources to another subnet or delete them from the subnet. The steps you take to move or delete a resource vary depending on the resource. To learn how to move or delete resources that are in subnets, read the documentation for each resource type.

Add IPv6 address space, NAT gateway, Network security group, and Route table
You can add IPv6, NAT gateway, NSG, or route table support after you create the subnet.

Service endpoints
To enable a service endpoint for an existing subnet, ensure that no critical tasks are running on any resource in the subnet. Service endpoints switch routes on every network interface in the subnet. The service endpoints change from using the default route with the `0.0.0.0/0` address prefix and next hop type of `Internet` to using a new route with the address prefix of the service and a next hop type of `VirtualNetworkServiceEndpoint`.

During the switch, any open TCP connections might be terminated. The service endpoint isn't enabled until traffic to the service for all network interfaces updates with the new route. For more information, see Virtual network traffic routing.

Subnet delegation
You can modify subnet delegation to enable zero or multiple delegations. If a resource for a service is already deployed in the subnet, you can't add or remove subnet delegations until you remove all the resources for the service. To delegate for a different service in the portal, select the service you want to delegate to from the popup list.

Network policy for private endpoints
You can change private endpoint network policy after subnet creation.

## Delete a subnet

- 
Portal

- 
Azure CLI

- 
PowerShell

You can delete a subnet only if there are no resources in the subnet. If resources are in the subnet, you must delete those resources before you can delete the subnet. The steps you take to delete a resource vary depending on the resource. To learn how to delete the resources, see the documentation for each resource type.

- In the Azure portal, search for and select virtual networks.

- On the Virtual networks page, select the virtual network you want to delete a subnet from.

- On the virtual network's page, select Subnets from the left navigation.

- On the Subnets page, select the subnet you want to delete.

- Select Delete, and then select Yes in the confirmation dialog box.

Run the az network vnet subnet delete command.

`az network vnet subnet delete \
 --name <subnetName> \
 --resource-group <resourceGroupName> \
 --vnet-name <virtualNetworkName>
`

Run the Remove-AzVirtualNetworkSubnetConfig command and then set the configuration.

`$subnetParams = @{
 Name = "<subnetName>"
 VirtualNetwork = $vnet
}
Remove-AzVirtualNetworkSubnetConfig @subnetParams | Set-AzVirtualNetwork
`

## Next steps

- Create, change, or delete a virtual network.

- PowerShell sample scripts

- Azure CLI sample scripts

- Azure Resource Manager template samples

- Azure Policy built-in definitions for Azure Virtual Network

 
 

 
 

 

 
 
 
 
 
 
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
 2025-07-29
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
