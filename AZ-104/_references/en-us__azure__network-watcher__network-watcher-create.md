# https://learn.microsoft.com/en-us/azure/network-watcher/network-watcher-create

Source: https://learn.microsoft.com/en-us/azure/network-watcher/network-watcher-create

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
 

 

 

 

 
 
# Enable or disable Azure Network Watcher

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Network Watcher is a regional service that enables you to monitor and diagnose conditions at a network scenario level in, to, and from Azure. Scenario level monitoring enables you to diagnose problems at an end to end network level view. Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights to your network in Azure.

Network Watcher is enabled in an Azure region through the creation of a Network Watcher instance in that region. This instance allows you to utilize Network Watcher capabilities in that particular region.

Note

- By default, Network Watcher is automatically enabled. When you create or update a virtual network in your subscription, Network Watcher will be automatically enabled in your Virtual Network's region.

- Automatically enabling Network Watcher doesn't affect your resources or associated charge.

- If you previously chose to opt out of Network Watcher automatic enablement, you must manually enable Network Watcher in each region where you want to use Network Watcher capabilities.

## Prerequisites

- 
Portal

- 
PowerShell

- 
Azure CLI

- An Azure account with an active subscription. Create an account for free.

- Sign in to the Azure portal with your Azure account.

- An Azure account with an active subscription. Create an account for free.

- Azure Cloud Shell or Azure PowerShell.

The steps in this article run the Azure PowerShell cmdlets interactively in Azure Cloud Shell. To run the commands in the Cloud Shell, select Open Cloud Shell at the upper-right corner of a code block. Select Copy to copy the code and then paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also install PowerShell locally to run the cmdlets. This article requires the Az PowerShell module. For more information, see How to install Azure PowerShell. To find the installed version, run Get-Module -ListAvailable Az cmdlet. If you run PowerShell locally, sign in to Azure using the Connect-AzAccount cmdlet.

- An Azure account with an active subscription. Create an account for free.

- Azure Cloud Shell or Azure CLI.

The steps in this article run the Azure CLI commands interactively in Azure Cloud Shell. To run the commands in the Cloud Shell, select Open Cloud Shell at the upper-right corner of a code block. Select Copy to copy the code, and paste it into Cloud Shell to run it. You can also run the Cloud Shell from within the Azure portal.

You can also install Azure CLI locally to run the commands. To find the installed version, run az version command. If you run Azure CLI locally, sign in to Azure using the az login command.

## Enable Network Watcher for your region

If you choose to opt out of Network Watcher automatic enablement, you must manually enable Network Watcher in each region where you want to use Network Watcher capabilities. To enable Network Watcher in a region, create a Network Watcher instance in that region using the Azure portal, PowerShell, the Azure CLI, REST API, or an Azure Resource Manager template (ARM template).

- 
Portal

- 
PowerShell

- 
Azure CLI

- In the search box at the top of the portal, enter network watcher. Select Network Watcher from the search results.

- On the Overview page, select + Create.

- On Add network watcher, select your Azure subscription, then select the region that you want to enable Azure Network Watcher for.

- Select Add.

Note

When you create a Network Watcher instance using the Azure portal:

- The name of the Network Watcher instance is automatically set to NetworkWatcher_{region}, where region corresponds to the Azure region of the Network Watcher instance. For example, a Network Watcher enabled in the East US region is named NetworkWatcher_eastus.

- The Network Watcher instance is created in a resource group named NetworkWatcherRG. The resource group is created if it doesn't already exist.

If you wish to customize the name of a Network Watcher instance and resource group, you can use PowerShell or REST API methods. In each option, the resource group must exist before you create a Network Watcher in it.

Create a Network Watcher instance using New-AzNetworkWatcher cmdlet:

`# Create a resource group for the Network Watcher instance (if it doesn't already exist).
New-AzResourceGroup -Name 'NetworkWatcherRG' -Location 'eastus'

# Create an instance of Network Watcher in East US region.
New-AzNetworkWatcher -Name 'NetworkWatcher_eastus' -ResourceGroupName 'NetworkWatcherRG' -Location 'eastus'
`

Note

When you create a Network Watcher instance using PowerShell, you can customize the name of a Network Watcher instance and resource group. However, the resource group must exist before you create a Network Watcher instance in it.

Create a Network Watcher instance using az network watcher configure command:

`# Create a resource group for the Network Watcher instance (if it doesn't already exist).
az group create --name 'NetworkWatcherRG' --location 'eastus'

# Create an instance of Network Watcher in East US region.
az network watcher configure --resource-group 'NetworkWatcherRG' --locations 'eastus' --enabled
`

Note

When you create a Network Watcher instance using the Azure CLI:

- The name of the Network Watcher instance is automatically set to {region}-watcher, where region corresponds to the Azure region of the Network Watcher instance. For example, a Network Watcher enabled in the East US region is named eastus-watcher.

- You can customize the name of the Network Watcher resource group. However, the resource group must exist before you create a Network Watcher instance in it.

If you wish to customize the name of the Network Watcher instance, you can use PowerShell or REST API methods.

## Disable Network Watcher for your region

You can disable Network Watcher for a region by deleting the Network Watcher instance in that region. You can delete a Network Watcher instance using the Azure portal, PowerShell, the Azure CLI, or REST API.

Warning

Deleting a Network Watcher instance deletes all Network Watcher running operations, historical data, and alerts with no option to revert. For example, if you delete `NetworkWatcher_eastus` instance, all flow logs, connection monitors, and packet captures in East US region will be deleted.

- 
Portal

- 
PowerShell

- 
Azure CLI

- In the search box at the top of the portal, enter network watcher. Select Network Watcher from the search results.

- On the Overview page, select the Network Watcher instances that you want to delete, then select Disable.

- Enter yes, then select Delete.

Delete a Network Watcher instance using Remove-AzNetworkWatcher:

`# Disable Network Watcher in the East US region by deleting its East US instance.
Remove-AzNetworkWatcher -Location 'eastus'
`

Use az network watcher configure to delete an instance of Network Watcher:

`# Disable Network Watcher in the East US region.
az network watcher configure --locations 'eastus' --enabled 'false'
`

## Opt out of Network Watcher automatic enablement

You can opt out of Network Watcher automatic enablement using Azure PowerShell or Azure CLI.

Caution

Opting-out of Network Watcher automatic enablement is a permanent change. Once you opt out, you can't opt in without contacting Azure support.

- 
Portal

- 
PowerShell

- 
Azure CLI

Opting-out of Network Watcher automatic enablement isn't available in the Azure portal. Use PowerShell or Azure CLI to opt out of Network Watcher automatic enablement.

To opt out of Network Watcher automatic enablement, use Register-AzProviderFeature cmdlet to register the `DisableNetworkWatcherAutocreation` feature for the `Microsoft.Network` resource provider. Then, use Register-AzResourceProvider cmdlet to register the `Microsoft.Network` resource provider.

`# Register the "DisableNetworkWatcherAutocreation" feature.
Register-AzProviderFeature -FeatureName 'DisableNetworkWatcherAutocreation' -ProviderNamespace 'Microsoft.Network'

# Register the "Microsoft.Network" resource provider.
Register-AzResourceProvider -ProviderNamespace 'Microsoft.Network'
`

To opt out of Network Watcher automatic enablement, use az feature register command to register the `DisableNetworkWatcherAutocreation` feature for the `Microsoft.Network` resource provider. Then, use az provider register command to register the `Microsoft.Network` resource provider.

`# Register the "DisableNetworkWatcherAutocreation" feature.
az feature register --name 'DisableNetworkWatcherAutocreation' --namespace 'Microsoft.Network'

# Register the "Microsoft.Network" resource provider.
az provider register --name 'Microsoft.Network'
`

Note

After you opt out of Network Watcher automatic enablement, you must manually enable Network Watcher in each region where you want to use Network Watcher capabilities. For more information, see Enable Network Watcher for your region.

## List Network Watcher instances

You can view all regions where Network Watcher is enabled in your subscription by listing available Network Watcher instances in your subscription. Use the Azure portal, PowerShell, the Azure CLI, or REST API to list Network Watcher instances in your subscription.

- 
Portal

- 
PowerShell

- 
Azure CLI

- In the search box at the top of the portal, enter network watcher. Select Network Watcher from the search results.

- On the Overview page, you can see all Network Watcher instances in your subscription.

List all Network Watcher instances in your subscription using Get-AzNetworkWatcher.

`# List all Network Watcher instances in your subscription.
Get-AzNetworkWatcher
`

List all Network Watcher instances in your subscription using az network watcher list.

`# List all Network Watcher instances in your subscription.
az network watcher list --out table
`

## Related content

To get started with Network Watcher, see:

- Virtual network flow logs

- Connection monitor

- Connection troubleshoot

 
 

 
 

 

 
 
 
 
 
 
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
 2025-09-23
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
