# https://learn.microsoft.com/en-us/azure/load-balancer/backend-pool-management

Source: https://learn.microsoft.com/en-us/azure/load-balancer/backend-pool-management

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
 

 

 

 

 
 
# Backend pool management

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 The backend pool is a critical component of the load balancer. The backend pool defines the group of resources that serve traffic for a given load-balancing rule.

There are two ways of configuring a backend pool:

- Network Interface Card (NIC)

- IP address

To preallocate a backend pool with an IP address range that contains virtual machines and Virtual Machine Scale Sets, configure the pool by IP address and virtual network ID. IP-based backend pools require a Standard Load Balancer.

This article focuses on configuration of IP-based backend pools.

## Configure backend pool by IP address and virtual network

In scenarios with prepopulated backend pools, use IP addresses and a virtual network.

Before you begin, ensure that you have:

- An existing Standard Load Balancer and virtual network.

- Backend resources in the same virtual network as the load balancer.

- Permission to create or update load balancer, network interface, and virtual machine resources.

- An authenticated Azure PowerShell or Azure CLI session for the tool you use.

You configure backend pool management on the backend pool object as highlighted in the following examples.

### PowerShell

Create a new backend pool:

`$be = @{
 ResourceGroupName = 'myResourceGroup'
 LoadBalancerName = 'myLoadBalancer'
 Name = 'myBackendPool'
}
$backendPool = New-AzLoadBalancerBackendAddressPool @be

`

Update backend pool with a new IP from existing virtual network:
 

`$vnet = @{
 Name = 'myVnet'
 ResourceGroupName = 'myResourceGroup'
}
$virtualNetwork = Get-AzVirtualNetwork @vnet

$add1 = @{
 IpAddress = '10.0.0.5'
 Name = 'TestVNetRef'
 VirtualNetworkId = $virtualNetwork.Id
}
$ip1 = New-AzLoadBalancerBackendAddressConfig @add1
 
$backendPool.LoadBalancerBackendAddresses.Add($ip1) 

Set-AzLoadBalancerBackendAddressPool -InputObject $backendPool

`

Retrieve the backend pool information for the load balancer to confirm that the backend addresses are added to the backend pool:

`$pool = @{
 ResourceGroupName = 'myResourceGroup'
 LoadBalancerName = 'myLoadBalancer'
 Name = 'myBackendPool'
}
Get-AzLoadBalancerBackendAddressPool @pool

`

Create a network interface and add it to the backend pool. Set the IP address to one of the backend addresses:

`$net = @{
 Name = 'myNic'
 ResourceGroupName = 'myResourceGroup'
 Location = 'eastus'
 PrivateIpAddress = '10.0.0.5'
 Subnet = $virtualNetwork.Subnets[0]
}
$nic = New-AzNetworkInterface @net

`

Create a VM and attach the NIC with an IP address in the backend pool:

`# Create a username and password for the virtual machine
$cred = Get-Credential

# Create a virtual machine configuration
$net = @{
 Name = 'myNic'
 ResourceGroupName = 'myResourceGroup'
}
$nic = Get-AzNetworkInterface @net

$vmc = @{
 VMName = 'myVM1'
 VMSize = 'Standard_DS1_v2'
}

$vmos = @{
 ComputerName = 'myVM1'
 Credential = $cred
}

$vmi = @{
 PublisherName = 'MicrosoftWindowsServer'
 Offer = 'WindowsServer'
 Skus = '2019-Datacenter'
 Version = 'latest'
}
$vmConfig = 
New-AzVMConfig @vmc | Set-AzVMOperatingSystem -Windows @vmos | Set-AzVMSourceImage @vmi | Add-AzVMNetworkInterface -Id $nic.Id

# Create a virtual machine using the configuration
$vm = @{
 ResourceGroupName = 'myResourceGroup'
 Zone = '1'
 Location = 'eastus'
 VM = $vmConfig

}
$vm1 = New-AzVM @vm

`

### CLI

By using Azure CLI, you can populate the IP-based backend pool through command-line parameters or a JSON configuration file.

#### Create an IP-based backend pool with Azure CLI

Create and populate the backend pool via the command-line parameters:

`az network lb address-pool create \
--resource-group myResourceGroup \
--lb-name myLB \
--name myBackendPool \
--vnet {VNET resource ID} \
--backend-address name=addr1 ip-address=10.0.0.4 \
--backend-address name=addr2 ip-address=10.0.0.5
`

Create and populate the Backend Pool via JSON configuration file:

`az network lb address-pool create \
--resource-group myResourceGroup \
--lb-name myLB \
--name myBackendPool \
--vnet {VNET resource ID} \
--backend-address-config-file @config_file.json
`

JSON configuration file:

` [
 {
 "name": "address1",
 "virtualNetwork": "/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/virtualNetworks/{vnet-name}",
 "ipAddress": "10.0.0.4"
 },
 {
 "name": "address2",
 "virtualNetwork": "/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/virtualNetworks/{vnet-name}",
 "ipAddress": "10.0.0.5"
 }
 ]
`

#### Verify backend addresses with Azure CLI

Retrieve the backend pool information for the load balancer to confirm that the backend addresses are added to the backend pool:

`az network lb address-pool show \
--resource-group myResourceGroup \
--lb-name MyLb \
--name MyBackendPool
`

#### Create a network interface with Azure CLI

Create a network interface and add it to the backend pool. Set the IP address to one of the backend addresses:

`az network nic create \
--resource-group myResourceGroup \
--name myNic \
--vnet-name myVnet \
--subnet mySubnet \
--network-security-group myNetworkSecurityGroup \
--lb-name myLB \
--private-ip-address 10.0.0.4
`

#### Create a virtual machine with Azure CLI

Create a VM and attach the NIC with an IP address in the backend pool:

`az vm create \
--resource-group myResourceGroup \
--name myVM \
--nics myNic \
--image Ubuntu2204 \
--admin-username azureuser \
--generate-ssh-keys
`

## Limitations for IP-based backend pools

- You can only use IP-based backend pools with Standard Load Balancers.

- The backend resources must be in the same virtual network as the load balancer.

- Backend instances in an IP-based backend pool must be virtual machines or virtual machine scale sets. You can't attach other PaaS services.

- A load balancer with an IP-based backend pool can't function as a Private Link service.

- You can't place Private endpoint resources in an IP-based backend pool.

- IP-based backend pools don't support ACI containers.

- Load balancers or services such as Application Gateway can't be placed in the backend pool of the load balancer.

- Inbound NAT Rules can't be specified by IP address.

- You can configure both IP-based and NIC-based backend pools for the same load balancer. You can't create a single backend pool that mixes backend addresses targeted by NIC and IP address within the same pool.

- A virtual machine in the same virtual network as an internal load balancer can't access the frontend of the ILB and its backend VMs simultaneously.

- Internet routing preference IPs aren't currently supported with IP-based backend pools. If you use internet routing preference IPs in IP-based backend pools, they're billed and routed through the default Microsoft global network.

- Performing move-related operations on VNETs that are attached to IP-based backend pools isn't supported.

- If backend pools are constantly changing (due to the constant addition or removal of backend resources). This can cause reset signals sent back to the source from the backend resource. As a workaround, you can use retries.

Important

An IP-based backend pool still requires a Standard Load Balancer. Its default outbound behavior resembles Basic Load Balancer behavior because default outbound access is enabled. This statement doesn't mean that Basic Load Balancer supports IP-based backend pools. For secure-by-default configuration and applications with demanding outbound needs, configure the backend pool by NIC.

## Next steps

In this article, you learned about Azure Load Balancer backend pool management and how to configure a backend pool by IP address and virtual network.

Learn more about Azure Load Balancer.

Review the REST API for IP-based backend pool management.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-08-18
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
