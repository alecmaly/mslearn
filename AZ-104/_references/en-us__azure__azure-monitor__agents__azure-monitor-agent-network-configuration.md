# https://learn.microsoft.com/en-us/azure/azure-monitor/agents/azure-monitor-agent-network-configuration

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/agents/azure-monitor-agent-network-configuration

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
 

 

 

 

 
 
# Azure Monitor Agent network configuration

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 The Azure Monitor Agent supports connections by using direct proxies, a Log Analytics gateway, and private links. This article describes how to define network settings and enable network isolation for the Azure Monitor Agent.

## Virtual network service tags

You must enable Azure Virtual Network service tags on the virtual network for the virtual machine (VM). Both `AzureMonitor` and `AzureResourceManager` tags are required. See the `AzureMonitor` entry in Available service tags for any other requirements.

You can use Azure Virtual Network service tags to define network access controls on network security groups, Azure Firewall, and user-defined routes. Use service tags instead of specific IP addresses in security rules and routes. For scenarios where you can't use Azure Virtual Network service tags, see the firewall requirements later in this article.

Note

You can't use network service tags to define network access controls for Azure Monitor to include data collection endpoint (DCE) public IP addresses. If you have custom logs or Internet Information Services (IIS) log data collection rules (DCRs), consider allowing the DCE's public IP addresses. This configuration ensures the scenarios work until these scenarios are supported via network service tags.

## Firewall endpoints

The following table lists the endpoints that firewalls must allow for different clouds. Each endpoint is an outbound connection to port 443.

Important

For all endpoints, disable HTTPS inspection.

Endpoint
Purpose
Example

`global.handler.control.monitor.azure.com`
Access the control service
Not applicable

`global.prod.microsoftmetrics.com`
Access the metrics service
Not applicable

`<virtual-machine-region-name>.handler.control.monitor.azure.com`
Fetch DCRs for a specific machine
`westus2.handler.control.monitor.azure.com`

`<log-analytics-workspace-id>.ods.opinsights.azure.com`
Ingest log data
`a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1.ods.opinsights.azure.com`

`management.azure.com`
Needed only if you send time series data (metrics) to an Azure Monitor custom metrics database
Not applicable

`<virtual-machine-region-name>.monitoring.azure.com`
Needed only if you send time series data (metrics) to an Azure Monitor custom metrics database
`westus2.monitoring.azure.com`

`<data-collection-endpoint>.<virtual-machine-region-name>.ingest.monitor.azure.com`
Ingest log data
`my-dce-5kyl.eastus-1.ingest.monitor.azure.com`

Replace the endpoint suffix with the suffix in the following table for each cloud:

Cloud
Suffix

Azure Commercial
`.com`

Azure Government
`.us`

Microsoft Azure operated by 21Vianet
`.cn`

Note

- If you use private links on the agent, add only private DCEs. The agent doesn't use the nonprivate endpoints listed in the preceding table when you use private links or private DCEs.

- The Azure Monitor metrics (custom metrics) preview isn't available in Azure Government and Azure operated by 21Vianet clouds.

- When you use the Azure Monitor Agent with Azure Monitor Private Link Scope, all your DCRs must use DCEs. Add the DCEs to the Azure Monitor Private Link Scope configuration via a private link.

## Proxy configuration

The Azure Monitor Agent extensions for Windows and Linux can communicate through either a proxy server or a Log Analytics gateway to Azure Monitor by using the HTTPS protocol. Use the extensions for Azure VMs, scale sets, and Azure Arc for servers, configured as described in the following steps. Both anonymous authentication and basic authentication by using a username and password are supported.

Important

Azure Arc-enabled servers don't support OMS Gateway for proxy connectivity, private link connectivity, and public endpoint connectivity options.

Important

Proxy configuration isn't supported for Azure Monitor Metrics (preview) as a destination. If you send metrics to this destination, it uses the public internet without any proxy.

Note

Setting the Linux system proxy through environment variables like `http_proxy` and `https_proxy` is supported only when you use the Azure Monitor Agent for Linux version 1.24.2 or later. For the Azure Resource Manager template (ARM template), if you configure a proxy, use the example here to declare the proxy settings. Also, a user can set global environment variables that all systemd services pick up via the DefaultEnvironment variable in /etc/systemd/system.conf.

Use the commands in the following examples based on your environment and configuration.

- 
Windows VM

- 
Linux VM

- 
Windows VMSS (PowerShell)

- 
Linux VMSS (PowerShell)

- 
Windows VMSS (CLI)

- 
Linux VMSS (CLI)

- 
Windows Arc-enabled server

- 
Linux Arc-enabled server

- 
Azure Resource Manager policy template example

No proxy

`$settingsString = '{"proxy":{"mode":"none"}}';
Set-AzVMExtension -ExtensionName AzureMonitorWindowsAgent -ExtensionType AzureMonitorWindowsAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -VMName <virtual-machine-name> -Location <location> -SettingString $settingsString
`

Proxy with no authentication

`$settingsString = '{"proxy":{"mode":"application","address":"http://[address]:[port]","auth": "false"}}';
Set-AzVMExtension -ExtensionName AzureMonitorWindowsAgent -ExtensionType AzureMonitorWindowsAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -VMName <virtual-machine-name> -Location <location> -SettingString $settingsString
`

Proxy with authentication

`$settingsString = '{"proxy":{"mode":"application","address":"http://[address]:[port]","auth": "true"}}';
$protectedSettingsString = '{"proxy":{"username":"[username]","password": "[password]"}}';
Set-AzVMExtension -ExtensionName AzureMonitorWindowsAgent -ExtensionType AzureMonitorWindowsAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -VMName <virtual-machine-name> -Location <location> -SettingString $settingsString -ProtectedSettingString $protectedSettingsString
`

Revert proxy configuration to defaults

To restore proxy configuration to defaults, define `$settingsString = '{}'`; as in the following example:

`$settingsString = '{}';
Set-AzVMExtension -ExtensionName AzureMonitorWindowsAgent -ExtensionType AzureMonitorWindowsAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -VMName <virtual-machine-name> -Location <location> -SettingString $settingsString
`

No proxy

`$settingsString = '{"proxy":{"mode":"none"}}';
Set-AzVMExtension -ExtensionName AzureMonitorLinuxAgent -ExtensionType AzureMonitorLinuxAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -VMName <virtual-machine-name> -Location <location> -SettingString $settingsString
`

Proxy with no authentication

`$settingsString = '{"proxy":{"mode":"application","address":"http://[address]:[port]","auth": "false"}}';
Set-AzVMExtension -ExtensionName AzureMonitorLinuxAgent -ExtensionType AzureMonitorLinuxAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -VMName <virtual-machine-name> -Location <location> -SettingString $settingsString
`

Proxy with authentication

`$settingsString = '{"proxy":{"mode":"application","address":"http://[address]:[port]","auth": "true"}}';
$protectedSettingsString = '{"proxy":{"username":"[username]","password": "[password]"}}';
Set-AzVMExtension -ExtensionName AzureMonitorLinuxAgent -ExtensionType AzureMonitorLinuxAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -VMName <virtual-machine-name> -Location <location> -SettingString $settingsString -ProtectedSettingString $protectedSettingsString
`

Revert proxy configuration to defaults

To restore proxy configuration to defaults, define `$settingsString = '{}'`; as in the following example:

`$settingsString = '{}';
Set-AzVMExtension -ExtensionName AzureMonitorLinuxAgent -ExtensionType AzureMonitorLinuxAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -VMName <virtual-machine-name> -Location <location> -SettingString $settingsString
`

Use Azure PowerShell to configure proxy settings on a Windows virtual machine scale set.

No proxy

`$settingsString = '{"proxy":{"mode":"none"}}';
$vmss = Get-AzVmss -ResourceGroupName <resource-group-name> -VMScaleSetName <vmss-name>
Add-AzVmssExtension -VirtualMachineScaleSet $vmss -Name AzureMonitorWindowsAgent -Publisher Microsoft.Azure.Monitor -Type AzureMonitorWindowsAgent -TypeHandlerVersion <version-number> -Setting $settingsString
Update-AzVmss -ResourceGroupName <resource-group-name> -VMScaleSetName <vmss-name> -VirtualMachineScaleSet $vmss
`

Proxy with no authentication

`$settingsString = '{"proxy":{"mode":"application","address":"http://[address]:[port]","auth":"false"}}';
$vmss = Get-AzVmss -ResourceGroupName <resource-group-name> -VMScaleSetName <vmss-name>
Add-AzVmssExtension -VirtualMachineScaleSet $vmss -Name AzureMonitorWindowsAgent -Publisher Microsoft.Azure.Monitor -Type AzureMonitorWindowsAgent -TypeHandlerVersion <version-number> -Setting $settingsString
Update-AzVmss -ResourceGroupName <resource-group-name> -VMScaleSetName <vmss-name> -VirtualMachineScaleSet $vmss
`

Proxy with authentication

`$settingsString = '{"proxy":{"mode":"application","address":"http://[address]:[port]","auth":"true"}}';
$protectedSettingsString = '{"proxy":{"username":"[username]","password":"[password]"}}';
$vmss = Get-AzVmss -ResourceGroupName <resource-group-name> -VMScaleSetName <vmss-name>
Add-AzVmssExtension -VirtualMachineScaleSet $vmss -Name AzureMonitorWindowsAgent -Publisher Microsoft.Azure.Monitor -Type AzureMonitorWindowsAgent -TypeHandlerVersion <version-number> -Setting $settingsString -ProtectedSetting $protectedSettingsString
Update-AzVmss -ResourceGroupName <resource-group-name> -VMScaleSetName <vmss-name> -VirtualMachineScaleSet $vmss
`

Revert proxy configuration to defaults

`$settingsString = '{}';
$vmss = Get-AzVmss -ResourceGroupName <resource-group-name> -VMScaleSetName <vmss-name>
Add-AzVmssExtension -VirtualMachineScaleSet $vmss -Name AzureMonitorWindowsAgent -Publisher Microsoft.Azure.Monitor -Type AzureMonitorWindowsAgent -TypeHandlerVersion <version-number> -Setting $settingsString
Update-AzVmss -ResourceGroupName <resource-group-name> -VMScaleSetName <vmss-name> -VirtualMachineScaleSet $vmss
`

Note

If you set your scale set upgrade policy to Manual, you need to update existing instances by running Update-AzVmssInstance after modifying the VMSS model. For scale sets with Automatic or Rolling upgrade policy, the extension is applied to instances automatically.

Use Azure PowerShell to configure proxy settings on a Linux virtual machine scale set.

No proxy

`$settingsString = '{"proxy":{"mode":"none"}}';
$vmss = Get-AzVmss -ResourceGroupName <resource-group-name> -VMScaleSetName <vmss-name>
Add-AzVmssExtension -VirtualMachineScaleSet $vmss -Name AzureMonitorLinuxAgent -Publisher Microsoft.Azure.Monitor -Type AzureMonitorLinuxAgent -TypeHandlerVersion <version-number> -Setting $settingsString
Update-AzVmss -ResourceGroupName <resource-group-name> -VMScaleSetName <vmss-name> -VirtualMachineScaleSet $vmss
`

Proxy with no authentication

`$settingsString = '{"proxy":{"mode":"application","address":"http://[address]:[port]","auth":"false"}}';
$vmss = Get-AzVmss -ResourceGroupName <resource-group-name> -VMScaleSetName <vmss-name>
Add-AzVmssExtension -VirtualMachineScaleSet $vmss -Name AzureMonitorLinuxAgent -Publisher Microsoft.Azure.Monitor -Type AzureMonitorLinuxAgent -TypeHandlerVersion <version-number> -Setting $settingsString
Update-AzVmss -ResourceGroupName <resource-group-name> -VMScaleSetName <vmss-name> -VirtualMachineScaleSet $vmss
`

Proxy with authentication

`$settingsString = '{"proxy":{"mode":"application","address":"http://[address]:[port]","auth":"true"}}';
$protectedSettingsString = '{"proxy":{"username":"[username]","password":"[password]"}}';
$vmss = Get-AzVmss -ResourceGroupName <resource-group-name> -VMScaleSetName <vmss-name>
Add-AzVmssExtension -VirtualMachineScaleSet $vmss -Name AzureMonitorLinuxAgent -Publisher Microsoft.Azure.Monitor -Type AzureMonitorLinuxAgent -TypeHandlerVersion <version-number> -Setting $settingsString -ProtectedSetting $protectedSettingsString
Update-AzVmss -ResourceGroupName <resource-group-name> -VMScaleSetName <vmss-name> -VirtualMachineScaleSet $vmss
`

Revert proxy configuration to defaults

`$settingsString = '{}';
$vmss = Get-AzVmss -ResourceGroupName <resource-group-name> -VMScaleSetName <vmss-name>
Add-AzVmssExtension -VirtualMachineScaleSet $vmss -Name AzureMonitorLinuxAgent -Publisher Microsoft.Azure.Monitor -Type AzureMonitorLinuxAgent -TypeHandlerVersion <version-number> -Setting $settingsString
Update-AzVmss -ResourceGroupName <resource-group-name> -VMScaleSetName <vmss-name> -VirtualMachineScaleSet $vmss
`

Note

If you set your scale set upgrade policy to Manual, you need to update existing instances by running Update-AzVmssInstance after modifying the VMSS model. For scale sets with Automatic or Rolling upgrade policy, the extension is applied to instances automatically.

Use Azure CLI to configure proxy settings on a Windows virtual machine scale set.

No proxy

`az vmss extension set \
 --name AzureMonitorWindowsAgent \
 --publisher Microsoft.Azure.Monitor \
 --vmss-name <vmss-name> \
 --resource-group <resource-group-name> \
 --settings '{"proxy":{"mode":"none"}}'
`

Proxy with no authentication

`az vmss extension set \
 --name AzureMonitorWindowsAgent \
 --publisher Microsoft.Azure.Monitor \
 --vmss-name <vmss-name> \
 --resource-group <resource-group-name> \
 --settings '{"proxy":{"mode":"application","address":"http://[address]:[port]","auth":"false"}}'
`

Proxy with authentication

`az vmss extension set \
 --name AzureMonitorWindowsAgent \
 --publisher Microsoft.Azure.Monitor \
 --vmss-name <vmss-name> \
 --resource-group <resource-group-name> \
 --settings '{"proxy":{"mode":"application","address":"http://[address]:[port]","auth":"true"}}' \
 --protected-settings '{"proxy":{"username":"[username]","password":"[password]"}}'
`

Revert proxy configuration to defaults

`az vmss extension set \
 --name AzureMonitorWindowsAgent \
 --publisher Microsoft.Azure.Monitor \
 --vmss-name <vmss-name> \
 --resource-group <resource-group-name> \
 --settings '{}'
`

Note

If you set your scale set upgrade policy to Manual, you need to update existing instances by running az vmss update-instances to apply the extension. For scale sets with Automatic or Rolling upgrade policy, the extension is applied to instances automatically.

Use Azure CLI to configure proxy settings on a Linux virtual machine scale set.

No proxy

`az vmss extension set \
 --name AzureMonitorLinuxAgent \
 --publisher Microsoft.Azure.Monitor \
 --vmss-name <vmss-name> \
 --resource-group <resource-group-name> \
 --settings '{"proxy":{"mode":"none"}}'
`

Proxy with no authentication

`az vmss extension set \
 --name AzureMonitorLinuxAgent \
 --publisher Microsoft.Azure.Monitor \
 --vmss-name <vmss-name> \
 --resource-group <resource-group-name> \
 --settings '{"proxy":{"mode":"application","address":"http://[address]:[port]","auth":"false"}}'
`

Proxy with authentication

`az vmss extension set \
 --name AzureMonitorLinuxAgent \
 --publisher Microsoft.Azure.Monitor \
 --vmss-name <vmss-name> \
 --resource-group <resource-group-name> \
 --settings '{"proxy":{"mode":"application","address":"http://[address]:[port]","auth":"true"}}' \
 --protected-settings '{"proxy":{"username":"[username]","password":"[password]"}}'
`

Revert proxy configuration to defaults

`az vmss extension set \
 --name AzureMonitorLinuxAgent \
 --publisher Microsoft.Azure.Monitor \
 --vmss-name <vmss-name> \
 --resource-group <resource-group-name> \
 --settings '{}'
`

Note

If you set your scale set upgrade policy to Manual, you need to update existing instances by running az vmss update-instances to apply the extension. For scale sets with Automatic or Rolling upgrade policy, the extension is applied to instances automatically.

No proxy

`$settings = @{"proxy" = @{mode = "none"}}
New-AzConnectedMachineExtension -Name AzureMonitorWindowsAgent -ExtensionType AzureMonitorWindowsAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -MachineName <arc-server-name> -Location <arc-server-location> -Setting $settings
`

Proxy with no authentication

`$settings = @{"proxy" = @{mode = "application"; address = "http://[address]:[port]"; auth = "false"}}
New-AzConnectedMachineExtension -Name AzureMonitorWindowsAgent -ExtensionType AzureMonitorWindowsAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -MachineName <arc-server-name> -Location <arc-server-location> -Setting $settings 
`

Proxy with authentication

`$settings = @{"proxy" = @{mode = "application"; address = "http://[address]:[port]"; auth = "true"}}
$protectedSettings = @{"proxy" = @{username = "[username]"; password = "[password]"}}
New-AzConnectedMachineExtension -Name AzureMonitorWindowsAgent -ExtensionType AzureMonitorWindowsAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -MachineName <arc-server-name> -Location <arc-server-location> -Setting $settings -ProtectedSetting $protectedSettings
`

Revert proxy configuration to defaults

To restore proxy configuration to defaults, define `$settings = @{}`; as in the following example:

`$settings = @{}
New-AzConnectedMachineExtension -Name AzureMonitorWindowsAgent -ExtensionType AzureMonitorWindowsAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -MachineName <arc-server-name> -Location <arc-server-location> -Setting $settings
`

No proxy

`$settings = @{"proxy" = @{mode = "none"}}
New-AzConnectedMachineExtension -Name AzureMonitorLinuxAgent -ExtensionType AzureMonitorLinuxAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -MachineName <arc-server-name> -Location <arc-server-location> -Setting $settings
`

Proxy with no authentication

`$settings = @{"proxy" = @{mode = "application"; address = "http://[address]:[port]"; auth = "false"}}
New-AzConnectedMachineExtension -Name AzureMonitorLinuxAgent -ExtensionType AzureMonitorLinuxAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -MachineName <arc-server-name> -Location <arc-server-location> -Setting $settings 
`

Proxy with authentication

`$settings = @{"proxy" = @{mode = "application"; address = "http://[address]:[port]"; auth = "true"}}
$protectedSettings = @{"proxy" = @{username = "[username]"; password = "[password]"}}
New-AzConnectedMachineExtension -Name AzureMonitorLinuxAgent -ExtensionType AzureMonitorLinuxAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -MachineName <arc-server-name> -Location <arc-server-location> -Setting $settings -ProtectedSetting $protectedSettings
`

Revert proxy configuration to defaults

To restore proxy configuration to defaults, define `$settings = @{}`; as in the following example:

`$settings = @{}
New-AzConnectedMachineExtension -Name AzureMonitorLinuxAgent -ExtensionType AzureMonitorLinuxAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -MachineName <arc-server-name> -Location <arc-server-location> -Setting $settings
`

`{
 "properties": {
 "displayName": "Configure Windows Arc-enabled machines to run the Azure Monitor Agent",
 "policyType": "BuiltIn",
 "mode": "Indexed",
 "description": "Automate the deployment of the Azure Monitor Agent extension on your Windows Arc-enabled machines for collecting telemetry data from the guest OS. This policy installs the extension if the OS and region are supported and system-assigned managed identity is enabled, and skips install otherwise. Learn more at https://aka.ms/AMAOverview.",
 "metadata": {
 "version": "2.3.0",
 "category": "Monitoring"
 },
 "parameters": {
 "effect": {
 "type": "String",
 "metadata": {
 "displayName": "Effect",
 "description": "Enable or disable the execution of the policy."
 },
 "allowedValues": [
 "DeployIfNotExists",
 "Disabled"
 ],
 "defaultValue": "DeployIfNotExists"
 }
 },
 "policyRule": {
 "if": {
 "allOf": [
 {
 "field": "type",
 "equals": "Microsoft.HybridCompute/machines"
 },
 {
 "field": "Microsoft.HybridCompute/machines/osName",
 "equals": "Windows"
 },
 {
 "field": "location",
 "in": [
 "australiacentral",
 "australiaeast",
 "australiasoutheast",
 "brazilsouth",
 "canadacentral",
 "canadaeast",
 "centralindia",
 "centralus",
 "eastasia",
 "eastus",
 "eastus2",
 "eastus2euap",
 "francecentral",
 "germanywestcentral",
 "japaneast",
 "japanwest",
 "jioindiawest",
 "koreacentral",
 "koreasouth",
 "northcentralus",
 "northeurope",
 "norwayeast",
 "southafricanorth",
 "southcentralus",
 "southeastasia",
 "southindia",
 "swedencentral",
 "switzerlandnorth",
 "uaenorth",
 "uksouth",
 "ukwest",
 "westcentralus",
 "westeurope",
 "westindia",
 "westus",
 "westus2",
 "westus3"
 ]
 }
 ]
 },
 "then": {
 "effect": "[parameters('effect')]",
 "details": {
 "type": "Microsoft.HybridCompute/machines/extensions",
 "roleDefinitionIds": [
 "/providers/Microsoft.Authorization/roleDefinitions/cd570a14-e51a-42ad-bac8-bafd67325302"
 ],
 "existenceCondition": {
 "allOf": [
 {
 "field": "Microsoft.HybridCompute/machines/extensions/type",
 "equals": "AzureMonitorWindowsAgent"
 },
 {
 "field": "Microsoft.HybridCompute/machines/extensions/publisher",
 "equals": "Microsoft.Azure.Monitor"
 },
 {
 "field": "Microsoft.HybridCompute/machines/extensions/provisioningState",
 "equals": "Succeeded"
 }
 ]
 },
 "deployment": {
 "properties": {
 "mode": "incremental",
 "template": {
 "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
 "contentVersion": "1.0.0.0",
 "parameters": {
 "vmName": {
 "type": "string"
 },
 "location": {
 "type": "string"
 }
 },
 "variables": {
 "extensionName": "AzureMonitorWindowsAgent",
 "extensionPublisher": "Microsoft.Azure.Monitor",
 "extensionType": "AzureMonitorWindowsAgent"
 },
 "resources": [
 {
 "name": "[concat(parameters('vmName'), '/', variables('extensionName'))]",
 "type": "Microsoft.HybridCompute/machines/extensions",
 "location": "[parameters('location')]",
 "apiVersion": "2021-05-20",
 "properties": {
 "publisher": "[variables('extensionPublisher')]",
 "type": "[variables('extensionType')]",
 "autoUpgradeMinorVersion": true,
 "enableAutomaticUpgrade": true,
 "settings": {
 "proxy": {
 "auth": "false",
 "mode": "application",
 "address": "http://XXX.XXX.XXX.XXX"
 }
 },
 "protectedsettings": { }
 }
 }
 ]
 },
 "parameters": {
 "vmName": {
 "value": "[field('name')]"
 },
 "location": {
 "value": "[field('location')]"
 }
 }
 }
 }
 }
 }
 }
 },
 "id": "/providers/Microsoft.Authorization/policyDefinitions/94f686d6-9a24-4e19-91f1-de937dc171a4",
 "type": "Microsoft.Authorization/policyDefinitions",
 "name": "94f686d6-9a24-4e19-91f1-de937dc171a4"
}
`

## Log Analytics gateway configuration

- Follow the preceding guidance to configure proxy settings on the agent and provide the IP address and port number that correspond to the gateway server. If you deployed multiple gateway servers behind a load balancer, for the agent proxy configuration, use the virtual IP address of the load balancer.

- Add the configuration endpoint URL to fetch DCRs to the allow list for the gateway:

- Run `Add-OMSGatewayAllowedHost -Host global.handler.control.monitor.azure.com`.

- Run `Add-OMSGatewayAllowedHost -Host <gateway-server-region-name>.handler.control.monitor.azure.com`.

If you use private links on the agent, you must also add the DCEs.

- Add the data ingestion endpoint URL to the allow list for the gateway:

- Run `Add-OMSGatewayAllowedHost -Host <log-analytics-workspace-id>.ods.opinsights.azure.com`.

- To apply the changes, restart the Log Analytics gateway (OMS Gateway) service:

- Run `Stop-Service -Name <gateway-name>`.

- Run `Start-Service -Name <gateway-name>`.

## Related content

- Learn how to add an endpoint to an Azure Monitor Private Link Scope resource.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-08-25
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
