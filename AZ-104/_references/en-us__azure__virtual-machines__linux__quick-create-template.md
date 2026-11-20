# https://learn.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-template

Source: https://learn.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-template

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
 

 

 

 

 
 
# Quickstart: Create an Ubuntu Linux virtual machine by using an ARM template

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Applies to: âï¸ Linux VMs

This quickstart shows you how to use an Azure Resource Manager template (ARM template) to deploy an Ubuntu Linux virtual machine (VM) in Azure.

An Azure Resource Manager template is a JavaScript Object Notation (JSON) file that defines the infrastructure and configuration for your project. The template uses declarative syntax. You describe your intended deployment without writing the sequence of programming commands to create the deployment.

If your environment meets the prerequisites and you're familiar with ARM templates, select the Deploy to Azure button. The template opens in the Azure portal.

## Prerequisites

If you don't have an Azure subscription, create a free account before you begin.

## Review the template

For more information on this template, see Deploy a simple Ubuntu Linux VM 18.04-LTS.

`{
 "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
 "contentVersion": "1.0.0.0",
 "metadata": {
 "_generator": {
 "name": "bicep",
 "version": "0.34.1.11899",
 "templateHash": "6608977399677963554"
 }
 },
 "parameters": {
 "vmName": {
 "type": "string",
 "defaultValue": "simpleLinuxVM",
 "metadata": {
 "description": "The name of your Virtual Machine."
 }
 },
 "adminUsername": {
 "type": "string",
 "metadata": {
 "description": "Username for the Virtual Machine."
 }
 },
 "authenticationType": {
 "type": "string",
 "defaultValue": "password",
 "allowedValues": [
 "sshPublicKey",
 "password"
 ],
 "metadata": {
 "description": "Type of authentication to use on the Virtual Machine. SSH key is recommended."
 }
 },
 "adminPasswordOrKey": {
 "type": "securestring",
 "metadata": {
 "description": "SSH Key or password for the Virtual Machine. SSH key is recommended."
 }
 },
 "dnsLabelPrefix": {
 "type": "string",
 "defaultValue": "[toLower(format('{0}-{1}', parameters('vmName'), uniqueString(resourceGroup().id)))]",
 "metadata": {
 "description": "Unique DNS Name for the Public IP used to access the Virtual Machine."
 }
 },
 "ubuntuOSVersion": {
 "type": "string",
 "defaultValue": "Ubuntu-2004",
 "allowedValues": [
 "Ubuntu-2004",
 "Ubuntu-2204"
 ],
 "metadata": {
 "description": "The Ubuntu version for the VM. This will pick a fully patched image of this given Ubuntu version."
 }
 },
 "location": {
 "type": "string",
 "defaultValue": "[resourceGroup().location]",
 "metadata": {
 "description": "Location for all resources."
 }
 },
 "vmSize": {
 "type": "string",
 "defaultValue": "Standard_D2s_v3",
 "metadata": {
 "description": "The size of the VM"
 }
 },
 "virtualNetworkName": {
 "type": "string",
 "defaultValue": "vNet",
 "metadata": {
 "description": "Name of the VNET"
 }
 },
 "subnetName": {
 "type": "string",
 "defaultValue": "Subnet",
 "metadata": {
 "description": "Name of the subnet in the virtual network"
 }
 },
 "networkSecurityGroupName": {
 "type": "string",
 "defaultValue": "SecGroupNet",
 "metadata": {
 "description": "Name of the Network Security Group"
 }
 },
 "securityType": {
 "type": "string",
 "defaultValue": "TrustedLaunch",
 "allowedValues": [
 "Standard",
 "TrustedLaunch"
 ],
 "metadata": {
 "description": "Security Type of the Virtual Machine."
 }
 }
 },
 "variables": {
 "imageReference": {
 "Ubuntu-2004": {
 "publisher": "Canonical",
 "offer": "0001-com-ubuntu-server-focal",
 "sku": "20_04-lts-gen2",
 "version": "latest"
 },
 "Ubuntu-2204": {
 "publisher": "Canonical",
 "offer": "0001-com-ubuntu-server-jammy",
 "sku": "22_04-lts-gen2",
 "version": "latest"
 }
 },
 "publicIPAddressName": "[format('{0}PublicIP', parameters('vmName'))]",
 "networkInterfaceName": "[format('{0}NetInt', parameters('vmName'))]",
 "osDiskType": "Standard_LRS",
 "subnetAddressPrefix": "10.1.0.0/24",
 "addressPrefix": "10.1.0.0/16",
 "linuxConfiguration": {
 "disablePasswordAuthentication": true,
 "ssh": {
 "publicKeys": [
 {
 "path": "[format('/home/{0}/.ssh/authorized_keys', parameters('adminUsername'))]",
 "keyData": "[parameters('adminPasswordOrKey')]"
 }
 ]
 }
 },
 "securityProfileJson": {
 "uefiSettings": {
 "secureBootEnabled": true,
 "vTpmEnabled": true
 },
 "securityType": "[parameters('securityType')]"
 },
 "extensionName": "GuestAttestation",
 "extensionPublisher": "Microsoft.Azure.Security.LinuxAttestation",
 "extensionVersion": "1.0",
 "maaTenantName": "GuestAttestation",
 "maaEndpoint": "[substring('emptystring', 0, 0)]"
 },
 "resources": [
 {
 "type": "Microsoft.Network/networkInterfaces",
 "apiVersion": "2023-09-01",
 "name": "[variables('networkInterfaceName')]",
 "location": "[parameters('location')]",
 "properties": {
 "ipConfigurations": [
 {
 "name": "ipconfig1",
 "properties": {
 "subnet": {
 "id": "[reference(resourceId('Microsoft.Network/virtualNetworks', parameters('virtualNetworkName')), '2023-09-01').subnets[0].id]"
 },
 "privateIPAllocationMethod": "Dynamic",
 "publicIPAddress": {
 "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIPAddressName'))]"
 }
 }
 }
 ],
 "networkSecurityGroup": {
 "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('networkSecurityGroupName'))]"
 }
 },
 "dependsOn": [
 "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('networkSecurityGroupName'))]",
 "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIPAddressName'))]",
 "[resourceId('Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]"
 ]
 },
 {
 "type": "Microsoft.Network/networkSecurityGroups",
 "apiVersion": "2023-09-01",
 "name": "[parameters('networkSecurityGroupName')]",
 "location": "[parameters('location')]",
 "properties": {
 "securityRules": [
 {
 "name": "SSH",
 "properties": {
 "priority": 1000,
 "protocol": "Tcp",
 "access": "Allow",
 "direction": "Inbound",
 "sourceAddressPrefix": "*",
 "sourcePortRange": "*",
 "destinationAddressPrefix": "*",
 "destinationPortRange": "22"
 }
 }
 ]
 }
 },
 {
 "type": "Microsoft.Network/virtualNetworks",
 "apiVersion": "2023-09-01",
 "name": "[parameters('virtualNetworkName')]",
 "location": "[parameters('location')]",
 "properties": {
 "addressSpace": {
 "addressPrefixes": [
 "[variables('addressPrefix')]"
 ]
 },
 "subnets": [
 {
 "name": "[parameters('subnetName')]",
 "properties": {
 "networkSecurityGroup": {
 "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('networkSecurityGroupName'))]"
 },
 "addressPrefix": "[variables('subnetAddressPrefix')]",
 "privateEndpointNetworkPolicies": "Enabled",
 "privateLinkServiceNetworkPolicies": "Enabled"
 }
 }
 ]
 },
 "dependsOn": [
 "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('networkSecurityGroupName'))]"
 ]
 },
 {
 "type": "Microsoft.Network/publicIPAddresses",
 "apiVersion": "2023-09-01",
 "name": "[variables('publicIPAddressName')]",
 "location": "[parameters('location')]",
 "sku": {
 "name": "Basic"
 },
 "properties": {
 "publicIPAllocationMethod": "Dynamic",
 "publicIPAddressVersion": "IPv4",
 "dnsSettings": {
 "domainNameLabel": "[parameters('dnsLabelPrefix')]"
 },
 "idleTimeoutInMinutes": 4
 }
 },
 {
 "type": "Microsoft.Compute/virtualMachines",
 "apiVersion": "2023-09-01",
 "name": "[parameters('vmName')]",
 "location": "[parameters('location')]",
 "properties": {
 "hardwareProfile": {
 "vmSize": "[parameters('vmSize')]"
 },
 "storageProfile": {
 "osDisk": {
 "createOption": "FromImage",
 "managedDisk": {
 "storageAccountType": "[variables('osDiskType')]"
 }
 },
 "imageReference": "[variables('imageReference')[parameters('ubuntuOSVersion')]]"
 },
 "networkProfile": {
 "networkInterfaces": [
 {
 "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('networkInterfaceName'))]"
 }
 ]
 },
 "osProfile": {
 "computerName": "[parameters('vmName')]",
 "adminUsername": "[parameters('adminUsername')]",
 "adminPassword": "[parameters('adminPasswordOrKey')]",
 "linuxConfiguration": "[if(equals(parameters('authenticationType'), 'password'), null(), variables('linuxConfiguration'))]"
 },
 "securityProfile": "[if(equals(parameters('securityType'), 'TrustedLaunch'), variables('securityProfileJson'), null())]"
 },
 "dependsOn": [
 "[resourceId('Microsoft.Network/networkInterfaces', variables('networkInterfaceName'))]"
 ]
 },
 {
 "condition": "[and(and(equals(parameters('securityType'), 'TrustedLaunch'), variables('securityProfileJson').uefiSettings.secureBootEnabled), variables('securityProfileJson').uefiSettings.vTpmEnabled)]",
 "type": "Microsoft.Compute/virtualMachines/extensions",
 "apiVersion": "2023-09-01",
 "name": "[format('{0}/{1}', parameters('vmName'), variables('extensionName'))]",
 "location": "[parameters('location')]",
 "properties": {
 "publisher": "[variables('extensionPublisher')]",
 "type": "[variables('extensionName')]",
 "typeHandlerVersion": "[variables('extensionVersion')]",
 "autoUpgradeMinorVersion": true,
 "enableAutomaticUpgrade": true,
 "settings": {
 "AttestationConfig": {
 "MaaSettings": {
 "maaEndpoint": "[variables('maaEndpoint')]",
 "maaTenantName": "[variables('maaTenantName')]"
 }
 }
 }
 },
 "dependsOn": [
 "[resourceId('Microsoft.Compute/virtualMachines', parameters('vmName'))]"
 ]
 }
 ],
 "outputs": {
 "adminUsername": {
 "type": "string",
 "value": "[parameters('adminUsername')]"
 },
 "hostname": {
 "type": "string",
 "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses', variables('publicIPAddressName')), '2023-09-01').dnsSettings.fqdn]"
 },
 "sshCommand": {
 "type": "string",
 "value": "[format('ssh {0}@{1}', parameters('adminUsername'), reference(resourceId('Microsoft.Network/publicIPAddresses', variables('publicIPAddressName')), '2023-09-01').dnsSettings.fqdn)]"
 }
 }
}
`

Several resources are defined in the template:

- Microsoft.Network/virtualNetworks/subnets: create a subnet.

- Microsoft.Storage/storageAccounts: create a storage account.

- Microsoft.Network/networkInterfaces: create a NIC.

- Microsoft.Network/networkSecurityGroups: create a network security group.

- Microsoft.Network/virtualNetworks: create a virtual network.

- Microsoft.Network/publicIPAddresses: create a public IP address.

- Microsoft.Compute/virtualMachines: create a virtual machine.

## Deploy the template

- Select the following image to sign in to Azure and open a template. The template creates a key vault and a secret.

- Select or enter the following values. Use the default values, when available.

- Subscription: select an Azure subscription.

- Resource group: select an existing resource group from the drop-down, or select Create new, enter a unique name for the resource group, and select OK.

- Region: select a region. For example, Central US.

- Admin username: provide a username, such as azureuser.

- Authentication type: You can choose between an SSH key or a password.

- Admin Password Or Key depending on what you choose for authentication type:

- If you choose password, the password must be at least 12 characters long and meet the defined complexity requirements.

- If you choose sshPublicKey, paste in the contents of your public key.

- DNS label prefix: enter a unique identifier to use as part of the DNS label.

- Ubuntu OS version: select which version of Ubuntu you want to run on the VM.

- Location: the default is the same location as the resource group, if it already exists.

- VM size: select the size to use for the VM.

- Virtual Network Name: name to be used for the vNet.

- Subnet Name: name for the subnet the VM should use.

- Network Security Group Name: name for the NSG.

- Select Review + create. After validation completes, select Create to create and deploy the VM.

Cost information isn't presented during the virtual machine creation process for ARM templates like it is for the Azure portal. If you want to learn more about how cost works for virtual machines, see the Cost optimization Overview page.

The Azure portal is used to deploy the template. In addition to the Azure portal, you can also use the Azure CLI, Azure PowerShell, and REST API. To learn other deployment methods, see Deploy templates.

## Review deployed resources

You can use the Azure portal to check on the VM and other resource that were created. After the deployment is finished, select Resource groups to see the VM and other resources.

## Clean up resources

When no longer needed, delete the resource group, which deletes the VM and all of the resources in the resource group.

- Select the Resource group.

- On the page for the resource group, select Delete resource group.

- When prompted, type the name of the resource group and then select Delete.

## Next steps

In this quickstart, you deployed a virtual machine by using an ARM template. To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.

Create and Manage Linux VMs with the Azure CLI

 
 

 
 

 

 
 
 
 
 
 
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
 2024-08-22
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
