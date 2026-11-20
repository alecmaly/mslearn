# https://learn.microsoft.com/en-us/azure/virtual-network/tutorial-create-route-table-portal

Source: https://learn.microsoft.com/en-us/azure/virtual-network/tutorial-create-route-table-portal

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
 

 

 

 

 
 
# Tutorial: Route network traffic with a route table

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure routes traffic between all subnets within a virtual network by default. You can create your own routes to override Azure's default routing. Custom routes are helpful when, for example, you want to route traffic between subnets through a network virtual appliance (NVA).

In this tutorial, you learn how to:

- Create a virtual network and subnets

- Create an NVA that routes traffic

- Deploy virtual machines (VMs) into different subnets

- Create a route table

- Create a route

- Associate a route table to a subnet

- Route traffic from one subnet to another through an NVA

## Prerequisites

- 
Portal

- 
PowerShell

- 
CLI

- An Azure account with an active subscription. You can create an account for free.

- An Azure account with an active subscription. You can create an account for free.

## Azure Cloud Shell

Azure hosts Azure Cloud Shell, an interactive shell environment that you can use through your browser. You can use either Bash or PowerShell with Cloud Shell to work with Azure services. You can use the Cloud Shell preinstalled commands to run the code in this article, without having to install anything on your local environment.

To start Azure Cloud Shell:

Option
Example/Link

Select Try It in the upper-right corner of a code or command block. Selecting Try It doesn't automatically copy the code or command to Cloud Shell.

Go to https://shell.azure.com, or select the Launch Cloud Shell button to open Cloud Shell in your browser.

Select the Cloud Shell button on the menu bar at the upper right in the Azure portal.

To use Azure Cloud Shell:

- Start Cloud Shell.

- Select the Copy button on a code block (or command block) to copy the code or command.

- Paste the code or command into the Cloud Shell session by selecting Ctrl+Shift+V on Windows and Linux, or by selecting Cmd+Shift+V on macOS.

- Select Enter to run the code or command.

If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 1.0.0 or later. Run `Get-Module -ListAvailable Az` to find the installed version. If you need to upgrade, see Install Azure PowerShell module. If you're running PowerShell locally, you also need to run `Connect-AzAccount` to create a connection with Azure.

If you don't have an Azure account, create a free account before you begin.

- Use the Bash environment in Azure Cloud Shell. For more information, see Get started with Azure Cloud Shell.

- If you prefer to run CLI reference commands locally, install the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see How to run the Azure CLI in a Docker container.

- If you're using a local installation, sign in to the Azure CLI by using the az login command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see Authenticate to Azure using Azure CLI.

- When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see Use and manage extensions with the Azure CLI.

- Run az version to find the version and dependent libraries that are installed. To upgrade to the latest version, run az upgrade.

- This article requires version 2.0.28 or later of the Azure CLI. If using Azure Cloud Shell, the latest version is already installed.

## Create subnets

A DMZ and Private subnet are needed for this tutorial. The DMZ subnet is where you deploy the NVA and the Private subnet is where you deploy the private virtual machines you want to route traffic to. In the diagram, subnet-1 is the Public subnet used for the public virtual machine.

- 
Portal

- 
PowerShell

- 
CLI

## Create a resource group

- Sign in to the Azure portal.

- In the search box at the top of the portal, enter Resource group. Select Resource groups in the search results.

- Select + Create.

- In the Basics tab of Create a resource group, enter or select the following information:

Setting
Value

Subscription
Select your subscription.

Resource group
Enter test-rg.

Region
Select East US 2.

- Select Review + create.

- Select Create.

## Create a virtual network

- In the search box at the top of the portal, enter Virtual network. Select Virtual networks in the search results.

- Select + Create.

- On the Basics tab of Create virtual network, enter or select the following information:

Setting
Value

Project details

Subscription
Select your subscription.

Resource group
Select test-rg.

Instance details

Name
Enter vnet-1.

Region
Select East US 2.

- Select Next to proceed to the Security tab.

- Select Next to proceed to the IP Addresses tab.

- In the address space box in Subnets, select the default subnet.

- In Edit subnet, enter or select the following information:

Setting
Value

Subnet details

Subnet template
Leave the default Default.

Name
Enter subnet-1.

Starting address
Leave the default of 10.0.0.0.

Subnet size
Leave the default of /24 (256 addresses).

- Select Save.

- Select + Add a subnet.

- In Add a subnet, enter or select the following information:

Setting
Value

Subnet details

Subnet template
Leave the default Default.

Name
Enter subnet-private.

Starting address
Enter 10.0.2.0.

Subnet size
Leave the default of /24 (256 addresses).

- Select Add.

- Select + Add a subnet.

- In Add a subnet, enter or select the following information:

Setting
Value

Subnet details

Subnet template
Leave the default Default.

Name
Enter subnet-dmz.

Starting address
Enter 10.0.3.0.

Subnet size
Leave the default of /24 (256 addresses).

- Select Add.

- Select Review + create at the bottom of the screen, and when validation passes, select Create.

## Deploy Azure Bastion

Azure Bastion uses your browser to connect to VMs in your virtual network over secure shell (SSH) or remote desktop protocol (RDP) by using their private IP addresses. The VMs don't need public IP addresses, client software, or special configuration. For more information about Azure Bastion, see Azure Bastion.

Note

Hourly pricing starts from the moment that Bastion is deployed, regardless of outbound data usage. For more information, see Pricing and SKUs. If you're deploying Bastion as part of a tutorial or test, we recommend that you delete this resource after you finish using it.

- In the search box at the top of the portal, enter Bastion. Select Bastions in the search results.

- Select + Create.

- In the Basics tab of Create a Bastion, enter or select the following information:

Setting
Value

Project details

Subscription
Select your subscription.

Resource group
Select test-rg.

Instance details

Name
Enter bastion.

Region
Select East US 2.

Tier
Select Developer.

Configure virtual networks

Virtual network
Select vnet-1.

Subnet
The AzureBastionSubnet is created automatically with an address space of /26 or larger.

- Select Review + create.

- Select Create.

Create a resource group with New-AzResourceGroup. The following example creates a resource group named test-rg for all resources created in this article.

`$rg = @{
 ResourceGroupName = "test-rg"
 Location = "EastUS2"
}
New-AzResourceGroup @rg
`

Create a virtual network with New-AzVirtualNetwork. The following example creates a virtual network named vnet-1 with the address prefix 10.0.0.0/16.

`$vnet = @{
 ResourceGroupName = "test-rg"
 Location = "EastUS2"
 Name = "vnet-1"
 AddressPrefix = "10.0.0.0/16"
}

$virtualNetwork = New-AzVirtualNetwork @vnet
`

Create four subnets by creating four subnet configurations with New-AzVirtualNetworkSubnetConfig. The following example creates four subnet configurations for Public, Private, DMZ, and Azure Bastion subnets.

`$subnetConfigPublicParams = @{
 Name = "subnet-1"
 AddressPrefix = "10.0.0.0/24"
 VirtualNetwork = $virtualNetwork
}

$subnetConfigBastionParams = @{
 Name = "AzureBastionSubnet"
 AddressPrefix = "10.0.1.0/24"
 VirtualNetwork = $virtualNetwork
}

$subnetConfigPrivateParams = @{
 Name = "subnet-private"
 AddressPrefix = "10.0.2.0/24"
 VirtualNetwork = $virtualNetwork
}

$subnetConfigDmzParams = @{
 Name = "subnet-dmz"
 AddressPrefix = "10.0.3.0/24"
 VirtualNetwork = $virtualNetwork
}

$subnetConfigPublic = Add-AzVirtualNetworkSubnetConfig @subnetConfigPublicParams
$subnetConfigBastion = Add-AzVirtualNetworkSubnetConfig @subnetConfigBastionParams
$subnetConfigPrivate = Add-AzVirtualNetworkSubnetConfig @subnetConfigPrivateParams
$subnetConfigDmz = Add-AzVirtualNetworkSubnetConfig @subnetConfigDmzParams
`

Write the subnet configurations to the virtual network with Set-AzVirtualNetwork, which creates the subnets in the virtual network:

`$virtualNetwork | Set-AzVirtualNetwork
`

### Create Azure Bastion

Create a public IP address for the Azure Bastion host with New-AzPublicIpAddress. The following example creates a public IP address named public-ip-bastion in the vnet-1 virtual network.

`$publicIpParams = @{
 ResourceGroupName = "test-rg"
 Name = "public-ip-bastion"
 Location = "EastUS2"
 AllocationMethod = "Static"
 Sku = "Standard"
}
New-AzPublicIpAddress @publicIpParams
`

Create an Azure Bastion host with New-AzBastion. The following example creates an Azure Bastion host named bastion in the AzureBastionSubnet subnet of the vnet-1 virtual network. Azure Bastion is used to securely connect Azure virtual machines without exposing them to the public internet.

`$bastionParams = @{
 ResourceGroupName = "test-rg"
 Name = "bastion"
 VirtualNetworkName = "vnet-1"
 PublicIpAddressName = "public-ip-bastion"
 PublicIpAddressRgName = "test-rg"
 VirtualNetworkRgName = "test-rg"
 Sku = "Basic"
}
New-AzBastion @bastionParams -AsJob
`

Create a resource group with az group create for all resources created in this article.

`# Create a resource group.
az group create \
 --name test-rg \
 --location eastus2
`

Create a virtual network with one subnet with az network vnet create.

`az network vnet create \
 --name vnet-1 \
 --resource-group test-rg \
 --address-prefix 10.0.0.0/16 \
 --subnet-name subnet-1 \
 --subnet-prefix 10.0.0.0/24
`

Create two more subnets with az network vnet subnet create.

`# Create a bastion subnet.
az network vnet subnet create \
 --vnet-name vnet-1 \
 --resource-group test-rg \
 --name AzureBastionSubnet \
 --address-prefix 10.0.1.0/24

# Create a private subnet.
az network vnet subnet create \
 --vnet-name vnet-1 \
 --resource-group test-rg \
 --name subnet-private \
 --address-prefix 10.0.2.0/24

# Create a DMZ subnet.
az network vnet subnet create \
 --vnet-name vnet-1 \
 --resource-group test-rg \
 --name subnet-dmz \
 --address-prefix 10.0.3.0/24
`

### Create Azure Bastion

Create a public IP address for the Azure Bastion host with az network public-ip create. The following example creates a public IP address named public-ip-bastion in the vnet-1 virtual network.

`az network public-ip create \
 --resource-group test-rg \
 --name public-ip-bastion \
 --location eastus2 \
 --allocation-method Static \
 --sku Standard
`

Create an Azure Bastion host with az network bastion create. The following example creates an Azure Bastion host named bastion in the AzureBastionSubnet subnet of the vnet-1 virtual network. Azure Bastion is used to securely connect Azure virtual machines without exposing them to the public internet.

`az network bastion create \
 --resource-group test-rg \
 --name bastion \
 --vnet-name vnet-1 \
 --public-ip-address public-ip-bastion \
 --location eastus2 \
 --sku Basic \
 --no-wait
`

## Create an NVA virtual machine

Network virtual appliances (NVAs) are virtual machines that help with network functions, such as routing and firewall optimization. In this section, create an NVA using an Ubuntu 24.04 virtual machine.

- 
Portal

- 
PowerShell

- 
CLI

- In the search box at the top of the portal, enter Virtual machine. Select Virtual machines in the search results.

- Select + Create then Azure virtual machine.

- In Create a virtual machine enter or select the following information in the Basics tab:

Setting
Value

Project details

Subscription
Select your subscription.

Resource group
Select test-rg.

Instance details

Virtual machine name
Enter vm-nva.

Region
Select (US) East US 2.

Availability options
Select No infrastructure redundancy required.

Security type
Select Standard.

Image
Select Ubuntu Server 24.04 LTS - x64 Gen2.

VM architecture
Leave the default of x64.

Size
Select a size.

Administrator account

Authentication type
Select SSH public key.

Username
Enter a username.

SSH public key source
Select Generate new key pair.

Key pair name
Enter vm-nva-key.

Inbound port rules

Public inbound ports
Select None.

- Select Next: Disks then Next: Networking.

- In the Networking tab, enter or select the following information:

Setting
Value

Network interface

Virtual network
Select vnet-1.

Subnet
Select subnet-dmz (10.0.3.0/24).

Public IP
Select None.

NIC network security group
Select Advanced.

Configure network security group
Select Create new. 
 In Name enter nsg-nva. 
 Select OK.

- Leave the rest of the options at the defaults and select Review + create.

- Select Create.

Create the virtual machine with New-AzVM. The following example creates a virtual machine named vm-nva.

`# Create a credential object
$cred = Get-Credential

# Define the virtual machine parameters
$vmParams = @{
 ResourceGroupName = "test-rg"
 Location = "EastUS2"
 Name = "vm-nva"
 Image = "Ubuntu2204"
 Size = "Standard_DS1_v2"
 Credential = $cred
 VirtualNetworkName = "vnet-1"
 SubnetName = "subnet-dmz"
 PublicIpAddressName = "" # No public IP address
 SshKeyName = "vm-nva-ssh-key"
 GenerateSshKey = $true
}

# Create the virtual machine
New-AzVM @vmParams
`

Create a virtual machine to be used as the NVA in the subnet-dmz subnet with az vm create.

`az vm create \
 --resource-group test-rg \
 --name vm-nva \
 --image Ubuntu2204 \
 --public-ip-address "" \
 --subnet subnet-dmz \
 --vnet-name vnet-1 \
 --admin-username azureuser \
 --generate-ssh-keys
`

The virtual machine takes a few minutes to create. Don't continue to the next step until Azure finishes creating the virtual machine and returns output for the virtual machine.

## Create public and private virtual machines

Create two virtual machines in the vnet-1 virtual network. One virtual machine is in the subnet-1 subnet and the other virtual machine is in the subnet-private subnet. Use the same virtual machine image for both virtual machines.

### Create public virtual machine

The public virtual machine is used to simulate a machine in the public internet. The public and private virtual machines are used to test the routing of network traffic through the NVA virtual machine.

- 
Portal

- 
PowerShell

- 
CLI

- In the search box at the top of the portal, enter Virtual machine. Select Virtual machines in the search results.

- Select + Create then Azure virtual machine.

- In Create a virtual machine enter or select the following information in the Basics tab:

Setting
Value

Project details

Subscription
Select your subscription.

Resource group
Select test-rg.

Instance details

Virtual machine name
Enter vm-public.

Region
Select (US) East US 2.

Availability options
Select No infrastructure redundancy required.

Security type
Select Standard.

Image
Select Ubuntu Server 24.04 LTS - x64 Gen2.

VM architecture
Leave the default of x64.

Size
Select a size.

Administrator account

Authentication type
Select SSH public key.

Username
Enter a username.

SSH public key source
Select Generate new key pair.

Key pair name
Enter vm-public-key.

Inbound port rules

Public inbound ports
Select None.

- Select Next: Disks then Next: Networking.

- In the Networking tab, enter or select the following information:

Setting
Value

Network interface

Virtual network
Select vnet-1.

Subnet
Select subnet-1 (10.0.0.0/24).

Public IP
Select None.

NIC network security group
Select None.

- Leave the rest of the options at the defaults and select Review + create.

- Select Create.

### Create private virtual machine

- In the search box at the top of the portal, enter Virtual machine. Select Virtual machines in the search results.

- Select + Create then Azure virtual machine.

- In Create a virtual machine enter or select the following information in the Basics tab:

Setting
Value

Project details

Subscription
Select your subscription.

Resource group
Select test-rg.

Instance details

Virtual machine name
Enter vm-private.

Region
Select (US) East US 2.

Availability options
Select No infrastructure redundancy required.

Security type
Select Standard.

Image
Select Ubuntu Server 24.04 LTS - x64 Gen2.

VM architecture
Leave the default of x64.

Size
Select a size.

Administrator account

Authentication type
Select SSH public key.

Username
Enter a username.

SSH public key source
Select Generate new key pair.

Key pair name
Enter vm-private-key.

Inbound port rules

Public inbound ports
Select None.

- Select Next: Disks then Next: Networking.

- In the Networking tab, enter or select the following information:

Setting
Value

Network interface

Virtual network
Select vnet-1.

Subnet
Select subnet-private (10.0.2.0/24).

Public IP
Select None.

NIC network security group
Select None.

- Leave the rest of the options at the defaults and select Review + create.

- Select Create.

Create a virtual machine in the subnet-1 subnet with New-AzVM. The following example creates a virtual machine named vm-public in the subnet-public subnet of the vnet-1 virtual network.

`# Define the virtual machine parameters
$vmParams = @{
 ResourceGroupName = "test-rg"
 Location = "EastUS2"
 Name = "vm-public"
 Image = "Ubuntu2204"
 Size = "Standard_DS1_v2"
 Credential = $cred
 VirtualNetworkName = "vnet-1"
 SubnetName = "subnet-1"
 PublicIpAddressName = "" # No public IP address
 SshKeyName = "vm-public-ssh-key"
 GenerateSshKey = $true
}

# Create the virtual machine
New-AzVM @vmParams
`

Create a virtual machine in the subnet-private subnet.

`# Define the virtual machine parameters
$vmParams = @{
 ResourceGroupName = "test-rg"
 Location = "EastUS2"
 Name = "vm-private"
 Image = "Ubuntu2204"
 Size = "Standard_DS1_v2"
 Credential = $cred
 VirtualNetworkName = "vnet-1"
 SubnetName = "subnet-private"
 PublicIpAddressName = "" # No public IP address
 SshKeyName = "vm-private-ssh-key"
 GenerateSshKey = $true
}

# Create the virtual machine
New-AzVM @vmParams
`

The virtual machine takes a few minutes to create. Don't continue with the next step until the virtual machine is created and Azure returns the output to PowerShell.

Create a virtual machine in the subnet-1 subnet with az vm create. The `--no-wait` parameter enables Azure to execute the command in the background so you can continue to the next command.

`az vm create \
 --resource-group test-rg \
 --name vm-public \
 --image Ubuntu2204 \
 --vnet-name vnet-1 \
 --subnet subnet-1 \
 --public-ip-address "" \
 --admin-username azureuser \
 --generate-ssh-keys \
 --no-wait
`

Create a virtual machine in the subnet-private subnet.

`az vm create \
 --resource-group test-rg \
 --name vm-private \
 --image Ubuntu2204 \
 --vnet-name vnet-1 \
 --subnet subnet-private \
 --public-ip-address "" \
 --admin-username azureuser \
 --generate-ssh-keys
`

## Enable IP forwarding

To route traffic through the NVA, turn on IP forwarding in Azure and in the operating system of vm-nva. When IP forwarding is enabled, any traffic received by vm-nva destined for a different IP address isn't dropped and is forwarded to the correct destination.

### Enable IP forwarding in Azure

In this section, you turn on IP forwarding for the network interface of the vm-nva virtual machine.

- 
Portal

- 
PowerShell

- 
CLI

- In the search box at the top of the portal, enter Virtual machine. Select Virtual machines in the search results.

- In Virtual machines, select vm-nva.

- In vm-nva, expand Networking then select Network settings.

- Select the name of the interface next to Network Interface:. The name begins with vm-nva and has a random number assigned to the interface. The name of the interface in this example is vm-nva313.

- In the network interface overview page, select IP configurations from the Settings section.

- In IP configurations, select the box next to Enable IP forwarding.

- Select Apply.

Enable IP forwarding for the network interface of the vm-nva virtual machine with Set-AzNetworkInterface. The following example enables IP forwarding for the network interface named vm-nva313.

`$nicParams = @{
 Name = "vm-nva"
 ResourceGroupName = "test-rg"
}
$nic = Get-AzNetworkInterface @nicParams

$nic.EnableIPForwarding = $true

Set-AzNetworkInterface -NetworkInterface $nic
`

Enable IP forwarding for the network interface of the vm-nva virtual machine with az network nic update. The following example enables IP forwarding for the network interface named vm-nvaVMNic.

`az network nic update \
 --name vm-nvaVMNic \
 --resource-group test-rg \
 --ip-forwarding true
`

## Enable IP forwarding in the operating system

In this section, turn on IP forwarding for the operating system of the vm-nva virtual machine to forward network traffic. Use the Run Command feature to execute a script on the virtual machine.

- 
Portal

- 
PowerShell

- 
CLI

- In the search box at the top of the portal, enter Virtual machine. Select Virtual machines in the search results.

- In Virtual machines, select vm-nva.

- Expand Operations then select Run command.

- Select RunShellScript.

- Enter the following script in the Run Command Script window:

`sudo sed -i 's/#net.ipv4.ip_forward=1/net.ipv4.ip_forward=1/' /etc/sysctl.conf
sudo sysctl -p
`

- Select Run.

- Wait for the script to complete. The output shows the IP forwarding setting has been enabled.

- Return to the Overview page of vm-nva and select Restart to restart the virtual machine.

Enable IP forwarding in the operating system of the vm-nva virtual machine with Invoke-AzVMRunCommand. The following example enables IP forwarding in the operating system.

`$runCommandParams = @{
 ResourceGroupName = "test-rg"
 VMName = "vm-nva"
 CommandId = "RunShellScript"
 ScriptString = @"
sudo sed -i 's/#net.ipv4.ip_forward=1/net.ipv4.ip_forward=1/' /etc/sysctl.conf
sudo sysctl -p
"@
}
Invoke-AzVMRunCommand @runCommandParams
`

Enable IP forwarding in the operating system of the vm-nva virtual machine with az vm run-command invoke. The following example enables IP forwarding in the operating system.

`az vm run-command invoke \
 --resource-group test-rg \
 --name vm-nva \
 --command-id RunShellScript \
 --scripts "sudo sed -i 's/#net.ipv4.ip_forward=1/net.ipv4.ip_forward=1/' /etc/sysctl.conf" "sudo sysctl -p"
`

## Create a route table

In this section, create a route table to define the route of the traffic through the NVA virtual machine. The route table is associated to the subnet-1 subnet where the vm-public virtual machine is deployed.

- 
Portal

- 
PowerShell

- 
CLI

- In the search box at the top of the portal, enter Route table. Select Route tables in the search results.

- Select + Create.

- In Create Route table enter or select the following information:

Setting
Value

Project details

Subscription
Select your subscription.

Resource group
Select test-rg.

Instance details

Region
Select East US 2.

Name
Enter route-table-public.

Propagate gateway routes
Leave the default of Yes.

- Select Review + create.

- Select Create.

## Create a route

In this section, create a route in the route table that you created in the previous steps.

- In the search box at the top of the portal, enter Route table. Select Route tables in the search results.

- Select route-table-public.

- Expand Settings then select Routes.

- Select + Add in Routes.

- Enter or select the following information in Add route:

Setting
Value

Route name
Enter to-private-subnet.

Destination type
Select IP Addresses.

Destination IP addresses/CIDR ranges
Enter 10.0.2.0/24.

Next hop type
Select Virtual appliance.

Next hop address
Enter 10.0.3.4. 
 This is the IP address of the vm-nva you created in the earlier steps..

- Select Add.

- Select Subnets in Settings.

- Select + Associate.

- Enter or select the following information in Associate subnet:

Setting
Value

Virtual network
Select vnet-1 (test-rg).

Subnet
Select subnet-1.

- Select OK.

Create a route table with New-AzRouteTable. The following example creates a route table named route-table-public.

`$routeTableParams = @{
 Name = 'route-table-public'
 ResourceGroupName = 'test-rg'
 Location = 'eastus2'
}
$routeTablePublic = New-AzRouteTable @routeTableParams
`

Create a route by retrieving the route table object with Get-AzRouteTable, create a route with Add-AzRouteConfig, then write the route configuration to the route table with Set-AzRouteTable.

`$routeTableParams = @{
 ResourceGroupName = "test-rg"
 Name = "route-table-public"
}

$routeConfigParams = @{
 Name = "to-private-subnet"
 AddressPrefix = "10.0.2.0/24"
 NextHopType = "VirtualAppliance"
 NextHopIpAddress = "10.0.3.4"
}

$routeTable = Get-AzRouteTable @routeTableParams
$routeTable | Add-AzRouteConfig @routeConfigParams | Set-AzRouteTable
`

Associate the route table with the subnet-1 subnet with Set-AzVirtualNetworkSubnetConfig. The following example associates the route-table-public route table with the subnet-1 subnet.

`$vnetParams = @{
 Name = 'vnet-1'
 ResourceGroupName = 'test-rg'
}
$virtualNetwork = Get-AzVirtualNetwork @vnetParams

$subnetParams = @{
 VirtualNetwork = $virtualNetwork
 Name = 'subnet-1'
 AddressPrefix = '10.0.0.0/24'
 RouteTable = $routeTablePublic
}
Set-AzVirtualNetworkSubnetConfig @subnetParams | Set-AzVirtualNetwork
`

Create a route table with az network route-table create. The following example creates a route table named route-table-public.

`# Create a route table
az network route-table create \
 --resource-group test-rg \
 --name route-table-public
`

Create a route in the route table with az network route-table route create.

`az network route-table route create \
 --name to-private-subnet \
 --resource-group test-rg \
 --route-table-name route-table-public \
 --address-prefix 10.0.2.0/24 \
 --next-hop-type VirtualAppliance \
 --next-hop-ip-address 10.0.3.4
`

Associate the route-table-subnet-public route table to the subnet-1 subnet with az network vnet subnet update.

`az network vnet subnet update \
 --vnet-name vnet-1 \
 --name subnet-1 \
 --resource-group test-rg \
 --route-table route-table-public
`

## Test the routing of network traffic

Test routing of network traffic from vm-public to vm-private. Test routing of network traffic from vm-private to vm-public.

### Test network traffic from vm-public to vm-private

- In the search box at the top of the portal, enter Virtual machine. Select Virtual machines in the search results.

- In Virtual machines, select vm-public.

- Select Connect then Connect via Bastion in the Overview section.

- In the Bastion connection page, enter or select the following information:

Setting
Value

Authentication Type
Select SSH Private Key from Local File.

Username
Enter the username you created.

Local File
Select the vm-public-key private key file you downloaded.

- Select Connect.

- In the prompt, enter the following command to trace the routing of network traffic from vm-public to vm-private:

`tracepath vm-private
`

The response is similar to the following example:

`azureuser@vm-public:~$ tracepath vm-private
 1?: [LOCALHOST] pmtu 1500
 1: vm-nva.internal.cloudapp.net 1.766ms 
 1: vm-nva.internal.cloudapp.net 1.259ms 
 2: vm-private.internal.cloudapp.net 2.202ms reached
 Resume: pmtu 1500 hops 2 back 1 
`

You can see that there are two hops in this response for `tracepath` ICMP traffic from vm-public to vm-private. The first hop is vm-nva. The second hop is the destination vm-private.

Azure sent the traffic from subnet-1 through the NVA and not directly to subnet-private because you previously added the to-private-subnet route to route-table-public and associated it to subnet-1.

- Close the Bastion session.

### Test network traffic from vm-private to vm-public

- In the search box at the top of the portal, enter Virtual machine. Select Virtual machines in the search results.

- In Virtual machines, select vm-private.

- Select Connect then Connect via Bastion in the Overview section.

- In the Bastion connection page, enter or select the following information:

Setting
Value

Authentication Type
Select SSH Private Key from Local File.

Username
Enter the username you created.

Local File
Select the vm-private-key private key file you downloaded.

- Select Connect.

- In the prompt, enter the following command to trace the routing of network traffic from vm-private to vm-public:

`tracepath vm-public
`

The response is similar to the following example:

`azureuser@vm-private:~$ tracepath vm-public
 1?: [LOCALHOST] pmtu 1500
 1: vm-public.internal.cloudapp.net 2.584ms reached
 1: vm-public.internal.cloudapp.net 2.147ms reached
 Resume: pmtu 1500 hops 1 back 2 
`

You can see there's one hop in this response, which is the destination vm-public.

Azure sent the traffic directly from subnet-private to subnet-1. By default, Azure routes traffic directly between subnets.

- Close the Bastion session.

- 
Portal

- 
PowerShell

- 
CLI

When you finish using the resources that you created, you can delete the resource group and all its resources.

- In the Azure portal, search for and select Resource groups.

- On the Resource groups page, select the test-rg resource group.

- On the test-rg page, select Delete resource group.

- Enter test-rg in Enter resource group name to confirm deletion, and then select Delete.

When no longer needed, use Remove-AzResourcegroup to remove the resource group and all of the resources it contains.

`$rgParams = @{
 Name = "test-rg"
}
Remove-AzResourceGroup @rgParams -Force
`

When no longer needed, use az group delete to remove the resource group and all of the resources it contains.

`az group delete \
 --name test-rg \
 --yes \
 --no-wait
`

## Next steps

In this tutorial, you:

- Created a route table and associated it to a subnet.

- Created a simple NVA that routed traffic from a public subnet to a private subnet.

You can deploy different preconfigured NVAs from the Azure Marketplace, which provide many useful network functions.

To learn more about routing, see Routing overview and Manage a route table. Routing can also be automatically configured at scale with Azure Virtual Network Manager's user-defined route (UDR) management feature.

To learn how to restrict network access to PaaS resources with virtual network service endpoints, advance to the next tutorial.

Restrict network access using service endpoints

 
 

 
 

 

 
 
 
 
 
 
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
 2026-02-11
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
