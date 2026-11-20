# https://learn.microsoft.com/en-us/azure/virtual-network/tutorial-filter-network-traffic

Source: https://learn.microsoft.com/en-us/azure/virtual-network/tutorial-filter-network-traffic

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
 

 

 

 

 
 
# Tutorial: Filter network traffic with a network security group

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 You can use a network security group to filter inbound and outbound network traffic to and from Azure resources in an Azure virtual network.

Network security groups contain security rules that filter network traffic by IP address, port, and protocol. When a network security group is associated with a subnet, security rules are applied to resources deployed in that subnet.

In this tutorial, you learn how to:

- Create a network security group and security rules

- Create application security groups

- Create a virtual network and associate a network security group to a subnet

- Deploy virtual machines and associate their network interfaces to the application security groups

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

- 
Portal

- 
PowerShell

- 
CLI

The following procedure creates a virtual network with a resource subnet.

- In the portal, search for and select Virtual networks.

- On the Virtual networks page, select + Create.

- On the Basics tab of Create virtual network, enter or select the following information:

Setting
Value

Project details

Subscription
Select your subscription.

Resource group
Select Create new. 
 Enter test-rg in Name. 
 Select OK.

Instance details

Name
Enter vnet-1.

Region
Select East US 2.

- Select Next to proceed to the Security tab.

- Select Next to proceed to the IP addresses tab.

- In the address space box under Subnets, select the default subnet.

- On the Edit subnet pane, enter or select the following information:

Setting
Value

Subnet details

Subnet template
Leave the default as Default.

Name
Enter subnet-1.

Starting address
Leave the default of 10.0.0.0.

Subnet size
Leave the default of /24(256 addresses).

- Select Save.

- Select Review + create at the bottom of the screen. After validation passes, select Create.

First create a resource group for all the resources created in this article with New-AzResourceGroup. The following example creates a resource group in the westus2 location:

`$rg = @{
 ResourceGroupName = "test-rg"
 Location = "westus2"
}

New-AzResourceGroup @rg
`

Create a virtual network with New-AzVirtualNetwork. The following example creates a virtual named vnet-1:

`$vnet = @{
 ResourceGroupName = "test-rg"
 Location = "westus2"
 Name = "vnet-1"
 AddressPrefix = "10.0.0.0/16"
}

$virtualNetwork = New-AzVirtualNetwork @vnet
`

Create a subnet configuration with New-AzVirtualNetworkSubnetConfig, and then write the subnet configuration to the virtual network with Set-AzVirtualNetwork. The following example adds a subnet named subnet-1 to the virtual network and associates the nsg-1 network security group to it:

`$subnet = @{
 Name = "subnet-1"
 VirtualNetwork = $virtualNetwork
 AddressPrefix = "10.0.0.0/24"
}
Add-AzVirtualNetworkSubnetConfig @subnet

$virtualNetwork | Set-AzVirtualNetwork
`

First create a resource group for all the resources created in this article with az group create. The following example creates a resource group in the westus2 location:

`az group create \
 --name test-rg \
 --location westus2
`

Create a virtual network with az network vnet create. The following example creates a virtual named vnet-1:

`az network vnet create \
 --name vnet-1 \
 --resource-group test-rg \
 --address-prefixes 10.0.0.0/16
`

Add a subnet to a virtual network with az network vnet subnet create. The following example adds a subnet named subnet-1 to the virtual network and associates the nsg-1 network security group to it:

`az network vnet subnet create \
 --vnet-name vnet-1 \
 --resource-group test-rg \
 --name subnet-1 \
 --address-prefix 10.0.0.0/24
`

## Create application security groups

An application security group (ASGs) enables you to group together servers with similar functions, such as web servers.

- 
Portal

- 
PowerShell

- 
CLI

- In the search box at the top of the portal, enter Application security group. Select Application security groups in the search results.

- Select + Create.

- On the Basics tab of Create an application security group, enter, or select this information:

Setting
Value

Project details

Subscription
Select your subscription.

Resource group
Select test-rg.

Instance details

Name
Enter asg-web.

Region
Select West US 2.

- Select Review + create.

- Select + Create.

- Repeat the previous steps, specifying the following values:

Setting
Value

Project details

Subscription
Select your subscription.

Resource group
Select test-rg.

Instance details

Name
Enter asg-mgmt.

Region
Select West US 2.

- Select Review + create.

- Select Create.

Create an application security group with New-AzApplicationSecurityGroup. An application security group enables you to group servers with similar port filtering requirements. The following example creates two application security groups.

`$web = @{
 ResourceGroupName = "test-rg"
 Name = "asg-web"
 Location = "westus2"
}
$webAsg = New-AzApplicationSecurityGroup @web

$mgmt = @{
 ResourceGroupName = "test-rg"
 Name = "asg-mgmt"
 Location = "westus2"
}
$mgmtAsg = New-AzApplicationSecurityGroup @mgmt
`

Create an application security group with az network asg create. An application security group enables you to group servers with similar port filtering requirements. The following example creates two application security groups.

`az network asg create \
 --resource-group test-rg \
 --name asg-web \
 --location westus2

az network asg create \
 --resource-group test-rg \
 --name asg-mgmt \
 --location westus2
`

## Create a network security group

A network security group (NSG) secures network traffic in your virtual network.

- 
Portal

- 
PowerShell

- 
CLI

- In the search box at the top of the portal, enter Network security group. Select Network security groups in the search results.

Note

In the search results for Network security groups, you may see Network security groups (classic). Select Network security groups.

- Select + Create.

- On the Basics tab of Create network security group, enter, or select this information:

Setting
Value

Project details

Subscription
Select your subscription.

Resource group
Select test-rg.

Instance details

Name
Enter nsg-1.

Location
Select West US 2.

- Select Review + create.

- Select Create.

Create a network security group with New-AzNetworkSecurityGroup. The following example creates a network security group named nsg-1:

`$nsgParams = @{
 ResourceGroupName = "test-rg"
 Location = "westus2"
 Name = "nsg-1"
}
$nsg = New-AzNetworkSecurityGroup @nsgParams
`

Create a network security group with az network nsg create. The following example creates a network security group named nsg-1:

`# Create a network security group
az network nsg create \
 --resource-group test-rg \
 --name nsg-1
`

## Associate network security group to subnet

In this section, you associate the network security group with the subnet of the virtual network you created earlier.

- 
Portal

- 
PowerShell

- 
CLI

- In the search box at the top of the portal, enter Network security group. Select Network security groups in the search results.

- Select nsg-1.

- Select Subnets from the Settings section of nsg-1.

- In the Subnets page, select + Associate:

- Under Associate subnet, select vnet-1 (test-rg) for Virtual network.

- Select subnet-1 for Subnet, and then select OK.

Use Get-AzVirtualNetwork to retrieve the virtual network object, and then use Set-AzVirtualNetworkSubnetConfig to associate the network security group with the subnet. The following example retrieves the virtual network object and updates the subnet configuration to associate the network security group:

`# Retrieve the virtual network
$vnet = Get-AzVirtualNetwork -Name "vnet-1" -ResourceGroupName "test-rg"

# Update the subnet configuration to associate the network security group
$subnetConfigParams = @{
 VirtualNetwork = $vnet
 Name = "subnet-1"
 AddressPrefix = $vnet.Subnets[0].AddressPrefix
 NetworkSecurityGroup = Get-AzNetworkSecurityGroup -Name "nsg-1" -ResourceGroupName "test-rg"
}
Set-AzVirtualNetworkSubnetConfig @subnetConfigParams

# Update the virtual network with the new subnet configuration
$vnet | Set-AzVirtualNetwork
`

Use az network vnet subnet update to associate the network security group with the subnet. The following example associates the nsg-1 network security group with the subnet-1 subnet:

`az network vnet subnet update \
 --resource-group test-rg \
 --vnet-name vnet-1 \
 --name subnet-1 \
 --network-security-group nsg-1
`

## Create security rules

- 
Portal

- 
PowerShell

- 
CLI

- Select Inbound security rules from the Settings section of nsg-1.

- In Inbound security rules page, select + Add.

- Create a security rule that allows port 80 to the asg-web application security group. In Add inbound security rule page, enter or select the following information:

Setting
Value

Source
Leave the default of Any.

Source port ranges
Leave the default of (*).

Destination
Select Application security group.

Destination application security groups
Select asg-web.

Service
Leave the default of Custom.

Destination port ranges
Enter 80.

Protocol
Select TCP.

Action
Leave the default of Allow.

Priority
Leave the default of 100.

Name
Enter allow-http-web.

- Select Add.

- Complete the previous steps with the following information:

Setting
Value

Source
Leave the default of Any.

Source port ranges
Leave the default of (*).

Destination
Select Application security group.

Destination application security group
Select asg-mgmt.

Service
Leave the default of Custom.

Destination port ranges
Enter 8080.

Protocol
Select TCP.

Action
Leave the default of Allow.

Priority
Leave the default of 110.

Name
Enter allow-8080-mgmt.

- Select Add.

Create a security rule with New-AzNetworkSecurityRuleConfig. The following example creates a rule that allows traffic inbound from the internet to the asg-web application security group over port 80:

`$webAsgParams = @{
 Name = "asg-web"
 ResourceGroupName = "test-rg"
}
$webAsg = Get-AzApplicationSecurityGroup @webAsgParams

$webRuleParams = @{
 Name = "Allow-HTTP-Web"
 Access = "Allow"
 Protocol = "Tcp"
 Direction = "Inbound"
 Priority = 100
 SourceAddressPrefix = "Internet"
 SourcePortRange = "*"
 DestinationApplicationSecurityGroupId = $webAsg.id
 DestinationPortRange = 80
}
$webRule = New-AzNetworkSecurityRuleConfig @webRuleParams
`

The following example creates a rule that allows traffic inbound from the internet to the asg-mgmt application security group over port 8080:

`$mgmtAsgParams = @{
 Name = "asg-mgmt"
 ResourceGroupName = "test-rg"
}
$mgmtAsg = Get-AzApplicationSecurityGroup @mgmtAsgParams

$mgmtRuleParams = @{
 Name = "Allow-8080-Mgmt"
 Access = "Allow"
 Protocol = "Tcp"
 Direction = "Inbound"
 Priority = 110
 SourceAddressPrefix = "Internet"
 SourcePortRange = "*"
 DestinationApplicationSecurityGroupId = $mgmtAsg.id
 DestinationPortRange = 8080
}
$mgmtRule = New-AzNetworkSecurityRuleConfig @mgmtRuleParams
`

Use Get-AzNetworkSecurityGroup to retrieve the existing network security group, and then add the new rules with the `+=` operator. Finally, update the network security group with Set-AzNetworkSecurityGroup:

`# Retrieve the existing network security group
$nsg = Get-AzNetworkSecurityGroup -Name "nsg-1" -ResourceGroupName "test-rg"

# Add the new rules to the security group
$nsg.SecurityRules += $webRule
$nsg.SecurityRules += $mgmtRule

# Update the network security group with the new rules
Set-AzNetworkSecurityGroup -NetworkSecurityGroup $nsg
`

Create a security rule with az network nsg rule create. The following example creates a rule that allows traffic inbound from the internet to the asg-web application security group over port 80:

`az network nsg rule create \
 --resource-group test-rg \
 --nsg-name nsg-1 \
 --name Allow-HTTP-Web \
 --access Allow \
 --protocol Tcp \
 --direction Inbound \
 --priority 100 \
 --source-address-prefix Internet \
 --source-port-range "*" \
 --destination-asgs "asg-web" \
 --destination-port-range 80
`

The following example creates a rule that allows traffic inbound from the Internet to the asg-mgmt application security group over port 8080:

`az network nsg rule create \
 --resource-group test-rg \
 --nsg-name nsg-1 \
 --name Allow-8080-Mgmt \
 --access Allow \
 --protocol Tcp \
 --direction Inbound \
 --priority 110 \
 --source-address-prefix Internet \
 --source-port-range "*" \
 --destination-asgs "asg-mgmt" \
 --destination-port-range 8080
`

## Create virtual machines

Create two virtual machines (VMs) in the virtual network.

- 
Portal

- 
PowerShell

- 
CLI

- In the portal, search for and select Virtual machines.

- In Virtual machines, select + Create, then Virtual machine.

- In Create a virtual machine, enter or select this information in the Basics tab:

Setting
Value

Project details

Subscription
Select your subscription.

Resource group
Select test-rg.

Instance details

Virtual machine name
Enter vm-web.

Region
Select (US) West US 2.

Availability options
Leave the default of No infrastructure redundancy required.

Security type
Select Standard.

Image
Select Ubuntu Server 24.04 LTS - x64 Gen2.

Azure Spot instance
Leave the default of unchecked.

Size
Select a size.

Administrator account

Authentication type
Select SSH public key.

Username
Enter azureuser.

SSH public key source
Select Generate new key pair.

Key pair name
Enter vm-web-key.

Inbound port rules

Select inbound ports
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
Leave the default of a new public IP.

NIC network security group
Select None.

- Select the Review + create tab, or select the blue Review + create button at the bottom of the page.

- Select Create.

- When prompted to Generate new key pair, select Download private key and create resource. The private key is downloaded to your local computer. The VM might take a few minutes to deploy.

- Repeat the previous steps to create a second virtual machine named vm-mgmt with key pair name vm-mgmt-key.

Before creating the VMs, retrieve the virtual network object with the subnet with Get-AzVirtualNetwork:

`$virtualNetworkParams = @{
 Name = "vnet-1"
 ResourceGroupName = "test-rg"
}
$virtualNetwork = Get-AzVirtualNetwork @virtualNetworkParams
`

Create a public IP address for each VM with New-AzPublicIpAddress:

`$publicIpWebParams = @{
 AllocationMethod = "Static"
 ResourceGroupName = "test-rg"
 Location = "westus2"
 Name = "public-ip-vm-web"
}
$publicIpWeb = New-AzPublicIpAddress @publicIpWebParams

$publicIpMgmtParams = @{
 AllocationMethod = "Static"
 ResourceGroupName = "test-rg"
 Location = "westus2"
 Name = "public-ip-vm-mgmt"
}
$publicIpMgmt = New-AzPublicIpAddress @publicIpMgmtParams
`

Create two network interfaces with New-AzNetworkInterface, and assign a public IP address to the network interface. The following example creates a network interface, associates the public-ip-vm-web public IP address to it.

`$webNicParams = @{
 Location = "westus2"
 Name = "vm-web-nic"
 ResourceGroupName = "test-rg"
 SubnetId = $virtualNetwork.Subnets[0].Id
 PublicIpAddressId = $publicIpWeb.Id
}
$webNic = New-AzNetworkInterface @webNicParams
`

The following example creates a network interface, associates the public-ip-vm-mgmt public IP address to it.

`$mgmtNicParams = @{
 Location = "westus2"
 Name = "vm-mgmt-nic"
 ResourceGroupName = "test-rg"
 SubnetId = $virtualNetwork.Subnets[0].Id
 PublicIpAddressId = $publicIpMgmt.Id
}
$mgmtNic = New-AzNetworkInterface @mgmtNicParams
`

Create two VMs in the virtual network so you can validate traffic filtering in a later step.

Generate SSH keys in Azure with New-AzSshKey. The following example creates SSH key resources for each VM:

`# Create SSH key for vm-web
$webSshKeyParams = @{
 ResourceGroupName = "test-rg"
 Name = "vm-web-key"
}
New-AzSshKey @webSshKeyParams

# Create SSH key for vm-mgmt
$mgmtSshKeyParams = @{
 ResourceGroupName = "test-rg"
 Name = "vm-mgmt-key"
}
New-AzSshKey @mgmtSshKeyParams
`

Create a VM configuration with New-AzVMConfig, then create the VM with New-AzVM. The following example creates a VM that serves as a web server. The `-AsJob` option creates the VM in the background, so you can continue to the next step:

`# Get the SSH public key
$sshKey = Get-AzSshKey -Name "vm-web-key" -ResourceGroupName "test-rg"

$webVmConfigParams = @{
 VMName = "vm-web"
 VMSize = "Standard_DS1_V2"
}

$vmImageParams = @{
 PublisherName = "Canonical"
 Offer = "ubuntu-24_04-lts"
 Skus = "server"
 Version = "latest"
}

$webVmConfig = New-AzVMConfig @webVmConfigParams | `
 Set-AzVMOperatingSystem -Linux -ComputerName "vm-web" -Credential (New-Object System.Management.Automation.PSCredential("azureuser", (ConvertTo-SecureString "DummyP@ssw0rd" -AsPlainText -Force))) -DisablePasswordAuthentication | `
 Set-AzVMSourceImage @vmImageParams | `
 Add-AzVMNetworkInterface -Id $webNic.Id | `
 Set-AzVMOSDisk -CreateOption FromImage | `
 Set-AzVMBootDiagnostic -Disable | `
 Add-AzVMSshPublicKey -KeyData $sshKey.publicKey -Path "/home/azureuser/.ssh/authorized_keys"

$webVmParams = @{
 ResourceGroupName = "test-rg"
 Location = "westus2"
 VM = $webVmConfig
}

New-AzVM @webVmParams -AsJob
`

Create a VM to serve as a management server:

`# Get the SSH public key
$sshKey = Get-AzSshKey -Name "vm-mgmt-key" -ResourceGroupName "test-rg"

$mgmtVmConfigParams = @{
 VMName = "vm-mgmt"
 VMSize = "Standard_DS1_V2"
}

$vmImageParams = @{
 PublisherName = "Canonical"
 Offer = "ubuntu-24_04-lts"
 Skus = "server"
 Version = "latest"
}

$mgmtVmConfig = New-AzVMConfig @mgmtVmConfigParams | `
 Set-AzVMOperatingSystem -Linux -ComputerName "vm-mgmt" -Credential (New-Object System.Management.Automation.PSCredential("azureuser", (ConvertTo-SecureString "DummyP@ssw0rd" -AsPlainText -Force))) -DisablePasswordAuthentication | `
 Set-AzVMSourceImage @vmImageParams | `
 Add-AzVMNetworkInterface -Id $mgmtNic.Id | `
 Set-AzVMOSDisk -CreateOption FromImage | `
 Set-AzVMBootDiagnostic -Disable | `
 Add-AzVMSshPublicKey -KeyData $sshKey.publicKey -Path "/home/azureuser/.ssh/authorized_keys"

$mgmtVmParams = @{
 ResourceGroupName = "test-rg"
 Location = "westus2"
 VM = $mgmtVmConfig
}

New-AzVM @mgmtVmParams
`

The virtual machine takes a few minutes to create. Don't continue with the next step until Azure finishes creating the VM.

Create two VMs in the virtual network so you can validate traffic filtering in a later step.

Create a VM with az vm create. The following example creates a VM that serves as a web server. The `--nsg ""` option is specified to prevent Azure from creating a default network security group for the network interface Azure creates when it creates the VM. The `--generate-ssh-keys` parameter causes the CLI to look for an available ssh key in `~/.ssh`. If one is found, that key is used. If not, one is generated and stored in `~/.ssh`:

`az vm create \
 --resource-group test-rg \
 --name vm-web \
 --image Ubuntu2404 \
 --vnet-name vnet-1 \
 --subnet subnet-1 \
 --nsg "" \
 --admin-username azureuser \
 --generate-ssh-keys
`

The VM takes a few minutes to create. After the VM is created, output similar to the following example is returned:

`{
 "fqdns": "",
 "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/test-rg/providers/Microsoft.Compute/virtualMachines/vm-web",
 "location": "westus2",
 "macAddress": "00-0D-3A-23-9A-49",
 "powerState": "VM running",
 "privateIpAddress": "10.0.0.4",
 "publicIpAddress": "203.0.113.24",
 "resourceGroup": "test-rg"
}
`

Create a VM with az vm create. The following example creates a VM that serves as a management server:

`az vm create \
 --resource-group test-rg \
 --name vm-mgmt \
 --image Ubuntu2404 \
 --vnet-name vnet-1 \
 --subnet subnet-1 \
 --nsg "" \
 --admin-username azureuser \
 --generate-ssh-keys
`

The VM takes a few minutes to create. Don't continue with the next step until Azure finishes creating the VM.

## Associate network interfaces to an ASG

- 
Portal

- 
PowerShell

- 
CLI

When you created the VMs, Azure created a network interface for each VM, and attached it to the VM.

Add the network interface of each VM to one of the application security groups you created previously:

- In the search box at the top of the portal, enter Virtual machine. Select Virtual machines in the search results, then select vm-web.

- Select Application security groups from the Networking section of vm-web.

- Select Add application security groups, then in the Add application security groups tab, select asg-web. Finally, select Add.

- Repeat the previous steps for vm-mgmt, selecting asg-mgmt in the Add application security groups tab.

Use Get-AzNetworkInterface to retrieve the network interface of the virtual machine, and then use Get-AzApplicationSecurityGroup to retrieve the application security group. Finally, use Set-AzNetworkInterface to associate the application security group with the network interface. The following example associates the asg-web application security group with the vm-web-nic network interface:

`$params1 = @{
 Name = "vm-web-nic"
 ResourceGroupName = "test-rg"
}
$nic = Get-AzNetworkInterface @params1

$params2 = @{
 Name = "asg-web"
 ResourceGroupName = "test-rg"
}
$asg = Get-AzApplicationSecurityGroup @params2

$nic.IpConfigurations[0].ApplicationSecurityGroups = @($asg)

$params3 = @{
 NetworkInterface = $nic
}
Set-AzNetworkInterface @params3
`

Repeat the command to associate the asg-mgmt application security group with the vm-mgmt-nic network interface.

`$params1 = @{
 Name = "vm-mgmt-nic"
 ResourceGroupName = "test-rg"
}
$nic = Get-AzNetworkInterface @params1

$params2 = @{
 Name = "asg-mgmt"
 ResourceGroupName = "test-rg"
}
$asg = Get-AzApplicationSecurityGroup @params2

$nic.IpConfigurations[0].ApplicationSecurityGroups = @($asg)

$params3 = @{
 NetworkInterface = $nic
}
Set-AzNetworkInterface @params3
`

Use az network nic update to associate the network interface with the application security group. The following example associates the asg-web application security group with the vm-web-nic network interface:

`# Retrieve the network interface name associated with the virtual machine
nic_name=$(az vm show --resource-group test-rg --name vm-web --query 'networkProfile.networkInterfaces[0].id' -o tsv | xargs basename)

# Associate the application security group with the network interface
az network nic ip-config update \
 --name ipconfigvm-web \
 --nic-name $nic_name \
 --resource-group test-rg \
 --application-security-groups asg-web
`

Repeat the command to associate the asg-mgmt application security group with the vm-mgmt-nic network interface.

`# Retrieve the network interface name associated with the virtual machine
nic_name=$(az vm show --resource-group test-rg --name vm-mgmt --query 'networkProfile.networkInterfaces[0].id' -o tsv | xargs basename)

# Associate the application security group with the network interface
az network nic ip-config update \
 --name ipconfigvm-mgmt \
 --nic-name $nic_name \
 --resource-group test-rg \
 --application-security-groups asg-mgmt
`

## Test traffic filters

- 
Portal

- 
PowerShell

- 
CLI

- In the search box at the top of the portal, enter Virtual machine. Select Virtual machines in the search results.

- Select vm-web.

- Select Run command from the Operations section.

- Select RunShellScript.

- In the Run Command Script pane, enter the following commands:

`sudo apt-get update -y
sudo apt-get install -y nginx
sudo systemctl enable nginx
sudo systemctl start nginx
`

- Select Run. Wait for the script to complete successfully.

- On the Overview page of vm-web, note the Public IP address for your VM.

- To confirm that you can access the vm-web web server from the internet on port 80, open an internet browser on your computer and browse to `http://<public-ip-address-from-previous-step>`.

You see the nginx default page, because inbound traffic from the internet to the asg-web application security group is allowed through port 80.

The network interface attached for vm-web is associated with the asg-web application security group and allows the connection.

- Try to access vm-web on port 443 by browsing to `https://<public-ip-address-vm-web>` in your browser. The connection fails or times out because the security rule for the asg-web doesn't allow port 443 inbound from the internet.

- Now configure vm-mgmt with nginx on port 8080. Select vm-mgmt from the Virtual machines page.

- Select Run command from the Operations section.

- Select RunShellScript.

- In the Run Command Script pane, enter the following commands to install nginx on port 8080:

`sudo apt-get update -y
sudo apt-get install -y nginx

# Configure nginx to listen on port 8080
sudo tee /etc/nginx/sites-available/default > /dev/null <<EOF
server {
 listen 8080 default_server;
 listen [::]:8080 default_server;
 root /var/www/html;
 index index.html index.htm index.nginx-debian.html;
 server_name _;
 location / {
 try_files \$uri \$uri/ =404;
 }
}
EOF

sudo systemctl restart nginx
`

- Select Run. Wait for the script to complete successfully.

- On the Overview page of vm-mgmt, note the Public IP address for your VM.

- To confirm that you can access the vm-mgmt web server from the internet on port 8080, open an internet browser on your computer and browse to `http://<public-ip-address-vm-mgmt>:8080`.

You see the nginx default page because inbound traffic from the internet to the asg-mgmt application security group is allowed through port 8080.

- Try to access vm-mgmt on port 80 by browsing to `http://<public-ip-address-vm-mgmt>` in your browser. The connection fails or times out because no security rule allows port 80 inbound to the asg-mgmt application security group.

The network interface attached for vm-web is associated with the asg-web application security group and allows the connection.

Install nginx on vm-web using Invoke-AzVMRunCommand:

`$webInstallParams = @{
 ResourceGroupName = "test-rg"
 VMName = "vm-web"
 CommandId = "RunShellScript"
 ScriptString = @"
sudo apt-get update -y
sudo apt-get install -y nginx
sudo systemctl enable nginx
sudo systemctl start nginx
"@
}
Invoke-AzVMRunCommand @webInstallParams
`

The command might take a few minutes to complete. After completion, test web access on vm-web.

Get the public IP address of vm-web:

`$webIPParams = @{
 Name = "public-ip-vm-web"
 ResourceGroupName = "test-rg"
}
$webIP = Get-AzPublicIpAddress @webIPParams
Write-Host "vm-web IP: $($webIP.IpAddress)"
`

To confirm that you can access the vm-web web server from the internet on port 80, open an internet browser on your computer and browse to `http://<vm-web-ip-address>`.

You see the nginx default page because inbound traffic from the internet to the asg-web application security group is allowed through port 80. The network interface attached to the vm-web VM is in this group.

Try to access vm-web on port 443 by browsing to `https://<vm-web-ip-address>` in your browser. The connection fails or times out because the security rule for the asg-web doesn't allow port 443 inbound from the internet.

Now install nginx on port 8080 on vm-mgmt:

`$mgmtInstallParams = @{
 ResourceGroupName = "test-rg"
 VMName = "vm-mgmt"
 CommandId = "RunShellScript"
 ScriptString = @"
sudo apt-get update -y
sudo apt-get install -y nginx

# Configure nginx to listen on port 8080
sudo tee /etc/nginx/sites-available/default > /dev/null <<'EOF'
server {
 listen 8080 default_server;
 listen [::]:8080 default_server;
 root /var/www/html;
 index index.html index.htm index.nginx-debian.html;
 server_name _;
 location / {
 try_files \$uri \$uri/ =404;
 }
}
EOF

sudo systemctl restart nginx
"@
}
Invoke-AzVMRunCommand @mgmtInstallParams
`

Get the public IP address of vm-mgmt:

`$mgmtIPParams = @{
 Name = "public-ip-vm-mgmt"
 ResourceGroupName = "test-rg"
}
$mgmtIP = Get-AzPublicIpAddress @mgmtIPParams
Write-Host "vm-mgmt IP: $($mgmtIP.IpAddress)"
`

To confirm that you can access the vm-mgmt web server from the internet on port 8080, open an internet browser on your computer and browse to `http://<vm-mgmt-ip-address>:8080`.

You see the nginx default page because inbound traffic from the internet to the asg-mgmt application security group is allowed through port 8080.

Try to access vm-mgmt on port 80 by browsing to `http://<vm-mgmt-ip-address>` in your browser. The connection fails or times out because no security rule allows port 80 inbound to the asg-mgmt application security group.

Install nginx on vm-web using az vm run-command invoke:

`az vm run-command invoke \
 --resource-group test-rg \
 --name vm-web \
 --command-id RunShellScript \
 --scripts "sudo apt-get update -y && sudo apt-get install -y nginx && sudo systemctl enable nginx && sudo systemctl start nginx"
`

Get the public IP address of vm-web:

`webIP=$(az vm show --show-details --resource-group test-rg --name vm-web --query publicIps --output tsv)
echo "vm-web IP: $webIP"
`

To confirm that you can access the vm-web web server from the internet on port 80, use curl:

`curl http://$webIP
`

The connection succeeds because the asg-web application security group, which the network interface attached to the vm-web VM is in, allows port 80 inbound from the Internet.

Try to access vm-web on port 443:

`curl -k https://$webIP
`

The connection fails or times out because the security rule for the asg-web doesn't allow port 443 inbound from the internet.

Now install nginx on port 8080 on vm-mgmt:

`az vm run-command invoke \
 --resource-group test-rg \
 --name vm-mgmt \
 --command-id RunShellScript \
 --scripts "sudo apt-get update -y && \
sudo apt-get install -y nginx && \
sudo bash -c 'cat > /etc/nginx/sites-available/default <<EOF
server {
 listen 8080 default_server;
 listen [::]:8080 default_server;
 root /var/www/html;
 index index.html index.htm index.nginx-debian.html;
 server_name _;
 location / {
 try_files \\\$uri \\\$uri/ =404;
 }
}
EOF' && \
sudo systemctl restart nginx"
`

Get the public IP address of vm-mgmt:

`mgmtIP=$(az vm show --show-details --resource-group test-rg --name vm-mgmt --query publicIps --output tsv)
echo "vm-mgmt IP: $mgmtIP"
`

To confirm that you can access the vm-mgmt web server from the internet on port 8080, use curl:

`curl http://$mgmtIP:8080
`

The connection succeeds because inbound traffic from the internet to the asg-mgmt application security group is allowed through port 8080.

Try to access vm-mgmt on port 80:

`curl http://$mgmtIP
`

The connection fails or times out because no security rule allows port 80 inbound to the asg-mgmt application security group.

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

When no longer needed, you can use Remove-AzResourceGroup to remove the resource group and all of the resources it contains:

`$params = @{
 Name = "test-rg"
 Force = $true
}
Remove-AzResourceGroup @params
`

When no longer needed, use az group delete to remove the resource group and all of the resources it contains.

`az group delete \
 --name test-rg \
 --yes \
 --no-wait
`

## Next steps

In this tutorial, you:

- Created a network security group and associated it to a virtual network subnet.

- Created application security groups for web and management traffic.

- Created two Linux virtual machines with SSH key authentication and associated their network interfaces with the application security groups.

- Installed nginx web servers on both VMs with different port configurations.

- Tested the application security group network filtering by demonstrating that vm-web allows port 80 (HTTP) but denies port 443, while vm-mgmt allows port 8080 but denies port 80 (HTTP).

To learn more about network security groups, see Network security group overview and Manage a network security group.

Azure routes traffic between subnets by default. You might instead, choose to route traffic between subnets through a VM, serving as a firewall, for example.

To learn how to create a route table, advance to the next tutorial.

Create a route table

 
 

 
 

 

 
 
 
 
 
 
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
 2026-02-02
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
