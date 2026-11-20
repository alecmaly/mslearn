# https://learn.microsoft.com/en-us/azure/application-gateway/ipv6-application-gateway-portal

Source: https://learn.microsoft.com/en-us/azure/application-gateway/ipv6-application-gateway-portal

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
 

 

 

 

 
 
# Configure Application Gateway with a frontend public IPv6 address using the Azure portal

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Application Gateway supports dual stack (IPv4 and IPv6) frontend connections from clients. To use IPv6 frontend connectivity, you need to create a new Application Gateway. Currently you can't upgrade existing IPv4 only Application Gateways to dual stack (IPv4 and IPv6) Application Gateways. Also, currently backend IPv6 addresses aren't supported.

In this article, you use the Azure portal to create an IPv6 Azure Application Gateway and test it to ensure it works correctly. You assign listeners to ports, create rules, and add resources to a backend pool. For the sake of simplicity, a simple setup is used with two public frontend IP addresses (IPv4 and IPv6), a basic listener to host a single site on the application gateway, a basic request routing rule, and two virtual machines (VMs) in the backend pool.

To support IPv6 connectivity, you must create a dual stack VNet. This dual stack VNet has subnets for both IPv4 and IPv6. Azure VNets already provide dual-stack capability.

For more information about the components of an application gateway, see Application gateway components.

## Overview

The Azure portal is used to create an IPv6 Azure Application Gateway. Testing is performed to verify it works correctly.

You learn how to:

- Set up a dual-stack network

- Create an application gateway with IPv6 frontend

- Create a virtual machine and install IIS for testing

You can also complete this quickstart using Azure PowerShell.

## Regions and availability

The IPv6 Application Gateway is available to all public cloud regions where Application Gateway v2 SKU is supported. It's also available in Microsoft Azure operated by 21Vianet and Azure Government

## Limitations

- Only v2 SKU supports a frontend with both IPv4 and IPv6 addresses

- A public IPv6 listener and a private IPv6 listener can't share a frontend port. Configure them with different frontend ports.

- IPv6 backends are currently not supported

- IPv6 private Link is currently not supported

- IPv6-only Application Gateway is currently not supported. Application Gateway must be dual stack (IPv6 and IPv4)

- Application Gateway Ingress Controller (AGIC) doesn't support IPv6 configuration

- Existing IPv4 application gateways can't be upgraded to dual stack application gateways

- The following limitations apply to WAF custom rules when IPv6 traffic is involved:

- Custom rules that use IP address-based match conditions do not support IPv6 traffic.

- Geo-based custom rules are not supported for IPv6 traffic.

## Prerequisites

An Azure account with an active subscription is required. If you don't already have an account, you can create an account for free.

Sign in to the Azure portal with your Azure account.

## Create an application gateway

Create the application gateway using the tabs on the Create application gateway page.

- On the Azure portal menu or from the Home page, select Create a resource.

- Under Categories, select Networking and then select Application Gateway in the Popular Azure services list.

### Basics tab

- On the Basics tab, enter the following values for the application gateway settings:

- Subscription: Select your subscription. For example, _mysubscription.

- Resource group: Select a resource group. If one doesn't exist, select Create new to create it. For example, myresourcegroupAG.

- Application gateway name: Enter a name for the application gateway. For example, myappgw.

- IP address type: Select Dual stack (IPv4 & IPv6).

- Configure virtual network: For Azure to communicate between the resources that you create, a dual stack virtual network is needed. You can either create a new dual stack virtual network or choose an existing dual stack network. In this example, you create a new dual stack virtual network at the same time that you create the application gateway.

Application Gateway instances are created in separate subnets. One dual-stack subnet and one IPv4-only are created in this example: The IPv4 and IPv6 subnets (provisioned as one dual-stack subnet) are assigned to the application gateway. The IPv4 subnet is for the backend servers.

Note

Virtual network service endpoint policies aren't currently supported in an Application Gateway subnet.

Under Configure virtual network, create a new virtual network by selecting Create new. In the Create virtual network pane, enter the following values to create the virtual network and two subnets:

- Name: Enter a name for the virtual network. For example, myVNet.

- Subnet name (Application Gateway subnet): The Subnets grid shows a subnet named default. Change the name of this subnet to myAGSubnet.

- Address range - The default IPv4 address ranges for the VNet and the subnet are 10.0.0.0/16 and 10.0.0.0/24, respectively. The default IPv6 address ranges for the VNet and the subnet are ace:cab:deca::/48 and ace:cab:deca::/64, respectively. If you see different default values, you might have an existing subnet that overlaps with these ranges.

Note

The application gateway subnet can contain only application gateways. No other resources are allowed.

Select OK to close the Create virtual network window and save the new virtual network and subnet settings.

- Select Next: Frontends.

### Frontends tab

- On the Frontends tab, verify Frontend IP address type is set to Public.

Important

For a private only Application Gateway, you can configure private IPv6 frontend IPs, but you must also configure a private IPv4 address. In other words, a private-only Application Gateway requires both private IPv4 and private IPv6 addresses.

- Select Add new for the Public IP address, enter a name for the public IP address, and select OK. For example, myAGPublicIPAddress.

Note

IPv6 Application Gateway supports up to 4 frontend IP addresses: two IPv4 addresses (Public and Private) and two IPv6 addresses (Public and Private)

- Select Next: Backends.

### Backends tab

The backend pool is used to route requests to the backend servers that serve the request. Backend pools can be composed of NICs, Virtual Machine Scale Sets, public IP addresses, internal IP addresses, fully qualified domain names (FQDN), and multitenant backends like Azure App Service. In this example, you create an empty backend pool with your application gateway and then add backend targets to the backend pool.

- On the Backends tab, select Add a backend pool.

- In the Add a backend pool pane, enter the following values to create an empty backend pool:

- Name: Enter a name for the backend pool. For example, myBackendPool.

- Add backend pool without targets: Select Yes to create a backend pool with no targets. Backend targets are added after creating the application gateway.

- Select Add to save the backend pool configuration and return to the Backends tab.

- On the Backends tab, select Next: Configuration.

### Configuration tab

On the Configuration tab, the frontend and backend pool are connected with a routing rule.

- Under Routing rules, select Add a routing rule.

- In the Add a routing rule pane, enter the following values:

- Rule name: Enter a name for the rule. For example, myRoutingRule.

- Priority: Enter a value between 1 and 20000, where 1 represents highest priority and 20000 represents lowest. For example, enter a priority of 100.

- A routing rule requires a listener. On the Listener tab, enter the following values:

- Listener name: Enter a name for the listener. For example, myListener.

- Frontend IP: Select Public IPv6.

Accept the default values for the other settings on the Listener tab and then select the Backend targets tab.

- On the Backend targets tab, select your backend pool for the Backend target. For example, myBackendPool.

- For the Backend setting, select Add new. The backend setting determines the behavior of the routing rule. In the Add backend setting pane, enter a backend settings name. For example, myBackendSetting.

- Accept the default values for other settings and then select Add.

- In the Add a routing rule pane, select Add to save the routing rule and return to the Configuration tab.

- Select Next: Tags, select Next: Review + create, and then select Create. Deployment of the application gateway takes a few minutes.

## Assign a DNS name to the frontend IPv6 address

A DNS name makes testing easier for the IPv6 application gateway. You can assign a public DNS name using your own domain and registrar, or you can create a name in azure.com. To assign a name in azure.com:

- From the Azure portal Home page, search for Public IP addresses.

- Select MyAGPublicIPv6Address.

- Under Settings, select Configuration.

- Under DNS name label (optional), enter a name. For example, myipv6appgw.

- Select Save.

- Copy the FQDN to a text editor for access later. In the following example, the FQDN is myipv6appgw.westcentralus.cloudapp.azure.com.

## Add a backend subnet

A backend IPv4 subnet is required for the backend targets. The backend subnet is IPv4-only.

- On the portal Home page, search for Virtual Networks and select the MyVNet virtual network.

- Next to Address space, select 10.0.0.0/16.

- Under Settings, select Subnets.

- Select + Subnet to add a new subnet.

- Under Name, enter MyBackendSubnet.

- The default address space is 10.0.1.0/24. Select Save to accept this and all other default settings.

## Add backend targets

Next, a backend target is added to test the application gateway:

- One VM is created: myVM and used as a backend target. You can also use existing virtual machines if they're available.

- IIS is installed on the virtual machine to verify that the application gateway was created successfully.

- The backend server (VM) is added to the backend pool.

Note

Only one virtual machine is deployed here as backend target because we are only testing connectivity. You can add multiple virtual machines if you also wish to test load balancing.

### Create a virtual machine

Application Gateway can route traffic to any type of virtual machine used in the backend pool. A Windows Server 2019 Datacenter virtual machine is used in this example.

- On the Azure portal menu or from the Home page, select Create a resource.

- Select Windows Server 2019 Datacenter in the Popular list. The Create a virtual machine page appears.

- Enter the following values on the Basics tab:

- Resource group: Select myResourceGroupAG.

- Virtual machine name: Enter myVM.

- Region: Select the same region where you created the application gateway.

- Username: Enter a name for the administrator user name.

- Password: Enter a password.

- Public inbound ports: None.

- Accept the other defaults and then select Next: Disks.

- Accept the Disks tab defaults and then select Next: Networking.

- Next to Virtual network, verify that myVNet is selected.

- Next to Subnet, verify that myBackendSubnet is selected.

- Next to Public IP, select None.

- Select Next: Management, Next: Monitoring, and then next to Boot diagnostics select Disable.

- Select Review + create.

- On the Review + create tab, review the settings, correct any validation errors, and then select Create.

- Wait for the virtual machine creation to complete before continuing.

### Install IIS for testing

In this example, you install IIS on the virtual machines to verify Azure created the application gateway successfully.

- Open Azure PowerShell.

Select Cloud Shell from the top navigation bar of the Azure portal and then select PowerShell from the drop-down list.

- Run the following command to install IIS on the virtual machine. Change the Location parameter if necessary:

`Set-AzVMExtension `
 -ResourceGroupName myResourceGroupAG `
 -ExtensionName IIS `
 -VMName myVM `
 -Publisher Microsoft.Compute `
 -ExtensionType CustomScriptExtension `
 -TypeHandlerVersion 1.4 `
 -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
 -Location WestCentralUS
`

See the following example:

### Add backend servers to backend pool

- On the Azure portal menu, select Application gateways or search for and select *Application gateways. Then select myAppGateway.

- Under Settings, select Backend pools and then select myBackendPool.

- Under Backend targets, Target type, select Virtual machine from the drop-down list.

- Under Target, select the myVM network interface from the drop-down list.

- Select Save.

- Wait for the deployment to complete before proceeding to the next step. Deployment takes a few minutes.

## Test the application gateway

IIS isn't required to create the application gateway. It's installed here to verify that you're able to successfully connect to the IPv6 interface of the application gateway.

Previously, we assigned the DNS name myipv6appgw.westcentralus.cloudapp.azure.com to the public IPv6 address of the application gateway. To test this connection:

- Paste the DNS name into the address bar of your browser to connect to it.

- Check the response. A valid response of myVM verifies that the application gateway was successfully created and can successfully connect with the backend.

Important

If the connection to the DNS name or IPv6 address fails, it might be because you can't browse IPv6 addresses from your device. To check if this is your problem, also test the IPv4 address of the application gateway. If the IPv4 address connects successfully, then it's likely you don't have a public IPv6 address assigned to your device. If this is the case, you can try testing the connection with a dual-stack VM.

## Clean up resources

When you no longer need the resources that you created with the application gateway, delete the resource group. When you delete the resource group, you also remove the application gateway and all the related resources.

To delete the resource group:

- On the Azure portal menu, select Resource groups or search for and select Resource groups.

- On the Resource groups page, search for myResourceGroupAG in the list, then select it.

- On the Resource group page, select Delete resource group.

- Enter myResourceGroupAG under TYPE THE RESOURCE GROUP NAME and then select Delete

## Next steps

- What is Azure Application Gateway v2?

 
 

 
 

 

 
 
 
 
 
 
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
 2026-08-04
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
