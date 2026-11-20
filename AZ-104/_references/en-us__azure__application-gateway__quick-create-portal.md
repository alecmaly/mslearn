# https://learn.microsoft.com/en-us/azure/application-gateway/quick-create-portal

Source: https://learn.microsoft.com/en-us/azure/application-gateway/quick-create-portal

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
 

 

 

 

 
 
# Quickstart: Direct web traffic with Azure Application Gateway - Azure portal

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 In this quickstart, you use the Azure portal to create an Azure Application Gateway and test it to make sure it works correctly. You configure a public frontend IP address, a basic listener, a request routing rule, and two virtual machines (VMs) in the backend pool.

For more information about the components of an application gateway, see Application gateway components.

You can also complete this quickstart by using Azure PowerShell or Azure CLI.

Note

Application Gateway frontend now supports dual-stack IP addresses. You can create up to four frontend IP addresses: two IPv4 addresses (public and private) and two IPv6 addresses (public and private).

## Prerequisites

- An Azure account with an active subscription. Create an account for free.

## Create a resource group and virtual network

Create a resource group and virtual network for the application gateway and its related resources.

Note

The application gateway must be in a separate subnet from the backend targets. In this quickstart, myAGSubnet is for the application gateway and myBackendSubnet is for the backend targets.

Important

An Application Gateway subnet must meet the following requirements:

- Use a subnet that is /28 or larger in address space. A /29 or smaller subnet isn't supported.

- For Accelerated gateways, keep at least 10 IP addresses free in the gateway subnet when you create the Application Gateway.

- Account for the five IP addresses that Azure reserves in every subnet for infrastructure use.

- Use a dedicated subnet for Application Gateway.

A /28 subnet meets the minimum requirement but provides limited room for scaling. For production deployments, use /26 or larger. A /24 or larger subnet is preferred for scale-out, zone-redundant deployments, and maintenance upgrades.

Plan the subnet size before deployment because you can't resize an Application Gateway subnet after deployment.

As of May 5, 2025, new and existing deployments of Private Application Gateway require subnet delegation to `Microsoft.Network/applicationGateways`. Follow the steps to configure subnet delegation.

Note

To try the Accelerated deployment tier during preview, open the preview-enabled Azure portal before following this quickstart. Select Accelerated (Preview) under Deployment tier and choose a supported preview region.

- Sign in to the Azure portal with your Azure account. If you're trying Accelerated during preview, use the preview-enabled portal from the preceding note instead.

- On the Azure portal menu or from the Home page, enter Resource groups in the search box, and then select Resource groups from the search results.

- On the Resource groups page, select + Create.

- On the Create a resource group page, enter the following values:

Setting
Value

Subscription
Select your Azure subscription.

Resource group
Enter myResourceGroupAG.

Region
Select a region. Use the same region when you create other resources in this quickstart.

- Select Review + create and then select Create.

- Browse to the resource group by selecting Resource groups from the Azure portal menu, and then select myResourceGroupAG.

- On the myResourceGroupAG page, select + Create.

- In the Search the Marketplace box, enter Virtual Network and select Virtual Network from the search results.

- Select Create on the Virtual Network page.

- On the Create virtual network page, enter the following values:

Setting
Value

Subscription
Select your Azure subscription.

Resource group
Verify that myResourceGroupAG is selected.

Name
Enter myVNet.

Region
Select the same region as the resource group.

- Select Next > Next or select the IP Addresses tab.

- On the IP Addresses tab, configure the address space to 10.21.0.0/16.

- Select + Add a subnet and enter the following values:

Setting
Value

Subnet name
Enter myBackendSubnet.

Starting address
Enter 10.21.1.0.

Subnet size
Select /24 (256 addresses).

- Select Add.

- From the Subnets list, select the default subnet and select the pencil icon to edit it. Change the name to myAGSubnet, set the starting address to 10.21.0.0 with a subnet size of /24 (256 addresses), and then select Save.

- Select Review + create and then select Create to create the virtual network.

## Create an application gateway

Create the application gateway by using the tabs on the Create application gateway page. This example uses the Standard v2 SKU.

- On the Azure portal menu or from the Home page, enter Application Gateway in the search box, and then select Application Gateways from the search results.

- On the Application Gateways page, select + Create > Application Gateway.

- On the Basics tab, enter the following values:

Setting
Value

Subscription
Select your Azure subscription.

Resource group
Select myResourceGroupAG.

Application gateway name
Enter myAppGateway.

Region
Select the same region as the resource group.

Tier
Select Standard V2.

Deployment tier
Select Standard, or Accelerated (Preview) to try the preview tier.

Configure virtual network

Virtual network
Select myVNet.

Subnet
Select myAGSubnet.

Note

Application Gateways are zone-redundant by default in regions that support multiple availability zones.
Virtual network service endpoint policies aren't currently supported in an Application Gateway subnet.

### Frontends tab

The frontend IP address is the entry point for incoming traffic. You can configure it as public or private. In this example, you configure a public frontend IP address.

- Select Next: Frontends.

- On the Frontends tab, verify that Frontend IP address type is set to Public.

Note

- Application Gateway v2 also supports private-frontend-only deployments when you register the `EnableApplicationGatewayNetworkIsolation` feature. To deploy a private-only gateway without registering the feature, select Network Isolated as the Deployment tier. For more information, see Private Application Gateway deployment.

- Application Gateway frontend now supports dual-stack IP addresses. You can create up to four frontend IP addresses: two IPv4 addresses (public and private) and two IPv6 addresses (public and private).

- Select Add new for the Public IP address and enter myAGPublicIPAddress for the public IP address name, and then select OK.

- Select Next: Backends.

### Backends tab

The backend pool routes requests to the backend servers that serve the request. Backend pools can include NICs, Virtual Machine Scale Sets, public IP addresses, internal IP addresses, fully qualified domain names (FQDN), and multitenant backends like Azure App Service. In this example, you create an empty backend pool and then add backend targets later.

- On the Backends tab, select Add a backend pool.

- In the Add a backend pool window, enter the following values:

Setting
Value

Name
Enter myBackendPool.

Add backend pool without targets
Select Yes. You add backend targets after creating the application gateway.

- Select Add to save the backend pool configuration and return to the Backends tab.

- On the Backends tab, select Next: Configuration.

### Configuration tab

On the Configuration tab, you connect the frontend and backend pool by using a routing rule.

- Select Add a routing rule in the Routing rules column.

- In the Add a routing rule window, enter the following values:

- Rule name: Enter myRoutingRule.

- Priority: Enter 100. Priority values range from 1 (highest) to 20000 (lowest).

- On the Listener tab, enter the following values:

Setting
Value

Listener name
Enter myListener.

Frontend IP
Select Public IPv4.

- Accept the default values for the other settings on the Listener tab, then select the Backend targets tab to configure the rest of the routing rule.

- On the Backend targets tab, select or enter the following:

Setting
Value

Target type
Select Backend pool radio button

Backend target
Select myBackendPool.

Backend settings
Select Add new.

Backend settings name
Enter myBackendSetting.

Backend port
Enter 80.

- Accept the default values for the other settings and select Add to return to the Add a routing rule window.

- Select Add to save the routing rule and return to the Configuration tab.

- Select Next: Tags and then Next: Review + create.

### Review + create tab

Review the settings on the Review + create tab, and then select Create to create the virtual network, the public IP address, and the application gateway. It might take several minutes for Azure to create the application gateway. Wait until the deployment finishes successfully before you continue.

## Add backend targets

In this example, you use virtual machines as the target backend. You create two virtual machines as backend servers for the application gateway.

To add backend targets, you:

- Create two new VMs, myVM and myVM2, to use as backend servers.

- Install IIS on the virtual machines to verify that the application gateway was created successfully.

- Add the backend servers to the backend pool.

### Create a virtual machine

- On the Azure portal menu or from the Home page, select Create a resource. The New window appears.

- Select Windows Server 2022 Datacenter in the Popular list.
Application Gateway can route traffic to any type of virtual machine in its backend pool. In this example, you use a Windows Server 2022 Datacenter virtual machine.

- On the Basics tab, enter the following values:

Setting
Value

Resource group
Select myResourceGroupAG.

Virtual machine name
Enter myVM.

Region
Select the same region as the application gateway.

Username
Enter an administrator user name.

Password
Enter a password.

Public inbound ports
Select None.

- Accept the other defaults and then select Next: Disks.

- Accept the Disks tab defaults and then select Next: Networking.

- On the Networking tab, verify that myVNet is selected for the Virtual network and the Subnet is set to myBackendSubnet. For Public IP, select None. Accept the other defaults and then select Next: Management.

Note

Application Gateway can communicate with instances outside of its virtual network, but you need to ensure there's IP connectivity.

- Select Next: Monitoring and set Boot diagnostics to Disable. Accept the other defaults and then select Review + create.

- On the Review + create tab, review the settings, correct any validation errors, and then select Create.

- Wait for the virtual machine creation to complete before continuing.

Note

The default network security group rules block all inbound internet access, including RDP. To connect to the virtual machine, use Azure Bastion. For more information, see Quickstart: Deploy Azure Bastion with default settings.

### Install IIS for testing

In this example, you install IIS on the virtual machines to verify that the application gateway was created successfully.

- In the Azure portal, select Cloud Shell from the top navigation bar, and then select PowerShell from the dropdown list.

Note

You can also use Azure Bastion to connect to the virtual machines and install IIS. For more information, see Quickstart: Deploy Azure Bastion with default settings.

- In the Azure PowerShell terminal, run the following command to install IIS on the virtual machine. Change the `Location` parameter if necessary:

`Set-AzVMExtension `
 -ResourceGroupName myResourceGroupAG `
 -ExtensionName IIS `
 -VMName myVM `
 -Publisher Microsoft.Compute `
 -ExtensionType CustomScriptExtension `
 -TypeHandlerVersion 1.4 `
 -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
 -Location EastUS
`

- Create a second virtual machine and install IIS by repeating the previous steps. Use myVM2 for the virtual machine name and for the `VMName` setting of the `Set-AzVMExtension` cmdlet.

### Add backend servers to backend pool

- On the Azure portal menu, select All resources or search for and select All resources. Then select myAppGateway.

- Select Backend pools from the left menu.

- Select myBackendPool.

- Under Backend targets, Target type, select Virtual machine from the dropdown list.

- Under Target, select the myVM and myVM2 virtual machines and their associated network interfaces from the dropdown lists.

- Select Save.

- Wait for the deployment to complete before proceeding to the next step.

## Test the application gateway

Although IIS isn't required to create the application gateway, you installed it in this quickstart to verify that the application gateway was created successfully.

To test the application gateway with IIS:

- Find the public IP address for the application gateway on its Overview page. Or, select All resources, enter myAGPublicIPAddress in the search box, and then select it in the search results. Azure displays the public IP address on the Overview page.

- Copy the public IP address, and then paste it into the address bar of your browser to browse that IP address.

- Check the response. A valid response verifies that the application gateway was created successfully and can connect with the backend.

Refresh the browser multiple times to verify connections to both myVM and myVM2.

## Clean up resources

When you no longer need the resources that you created with the application gateway, delete the resource group. Deleting the resource group also removes the application gateway and all related resources.

To delete the resource group:

- On the Azure portal menu, select Resource groups or search for and select Resource groups.

- On the Resource groups page, search for myResourceGroupAG, and then select it.

- On the Resource group page, select Delete resource group.

- Enter myResourceGroupAG under TYPE THE RESOURCE GROUP NAME and then select Delete.

## Next steps

Tutorial: Configure an application gateway with TLS termination using the Azure portal

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-17
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
