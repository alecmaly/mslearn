# https://learn.microsoft.com/en-us/azure/azure-monitor/vm/data-collection

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/vm/data-collection

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
 

 

 

 

 
 
# Collect guest log data from virtual machines with Azure Monitor

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Monitor automatically collects host metrics and activity logs from Azure virtual machines, virtual machine scale sets, and Azure Arc-enabled servers. To fully monitor the guest operating system and workloads, you typically also need to collect log data that isn't collected by default. This article describes how to use the Azure portal to create data collection rules (DCRs) for common virtual machine data sources.

## Scope of article

If you have basic data collection requirements, the guidance in this article and the related articles for each data source should be sufficient. The Azure portal can create and edit the DCR without requiring you to understand its structure or manually associate it with the VM. Creating a DCR and adding VM resources is also the recommended way to install the Azure Monitor Agent through the Azure portal. The Azure Monitor Agent is installed automatically if necessary, and an association is created between the DCR and each VM you select.

If you need advanced features such as transformations or want to create and assign DCRs by using Azure CLI, Azure Policy, or other methods, see Create data collection rules (DCRs) using JSON. You can also review sample DCRs created by this process at Data collection rule (DCR) samples for VMs in Azure Monitor.

## Prerequisites

- Log Analytics workspace where you have at least contributor rights to collect the data you configure.

- Permissions to create DCR objects in the workspace.

- To send data across tenants, you must first enable Azure Lighthouse.

- See the detailed article for each data source for any additional prerequisites.

Important

If your Log Analytics workspace is associated with a network security perimeter, see Configure Azure Monitor with Network Security Perimeter to configure your Log Analytics workspace.

## Create data collection rule (DCR)

Warning

If you edit an existing data collection rule (DCR) using the Azure portal, it will overwrite any changes that were made by editing the JSON of the DCR directly if those features aren't supported in the portal. For example, if you add a transformation to a DCR for a data source that doesn't allow a transformation to be created in the portal, then that transformation will be removed if you subsequently edit the DCR in the portal. In this case, you must continue to make any changes to the DCR by editing the JSON directly.

In the Azure portal, on the Monitor menu, select Data Collection Rules > Create to open the DCR creation pane.

When you create a DCR in the Azure portal, you use the default experience. A banner at the top of the pane links to the classic creation experience if you need it. Select the tab below for guidance on the experience you want to use.

- 
Default experience

- 
Classic experience

The Basics tab includes basic information about the DCR.

Setting
Description

Rule Name
A name for the DCR. The name should be something descriptive that helps you identify the rule.

Subscription
The subscription to store the DCR. The subscription doesn't need to be the same subscription as the virtual machines.

Resource group
A resource group to store the DCR. The resource group doesn't need to be the same resource group as the virtual machines.

Region
The Azure region to store the DCR. The region must be the same region as any Log Analytics workspace or Azure Monitor workspace that's used in a destination of the DCR. If you have workspaces in different regions, create multiple DCRs to associate with the same set of machines.

Type of telemetry
Specifies the type of telemetry the DCR collects. This selection affects the resources that you can select and the data flows that you can create for the DCR. Select the drop-down to get a short description of each option. Select Help me choose to get further details, including the types of data source and destination you can select for each option and whether they require a DCE or a managed entity.1

For Platform Telemetry, see Create a data collection rule (DCR) for Platform Metrics Export.

Data Collection Endpoint
Specifies the data collection endpoint (DCE) that's used to collect data. A DCE is required only if you're using a data source that requires one. Select Help me choose next to Type of telemetry to identify the data sources that require a DCE. For most implementations, you can use a single DCE for each Log Analytics workspace. See Create a data collection endpoint for details on how to create a DCE.

Enable Managed Identity
Specifies whether to enable managed identity for the DCR. Select Help me choose next to Type of telemetry to identify the data sources that require a managed identity.

1 This option sets the `kind` attribute in the DCR. You can set other values for this attribute, but the values aren't available to select in the portal.

### Add resources

On the Resources pane, select Add resources to add resources that use the DCR. You don't need to add any resources yet since you can update the DCR after creation and add or remove any resources. The portal displays the region of the DCR as a reminder since some telemetry types require the DCR and resources to be in the same region. You can't add a virtual machine scale set with flexible orchestration as a resource for a DCR. Instead, add each VM included in the virtual machine scale set.

Important

When resources are added to a DCR, the default option in the Azure portal is to enable a system-assigned managed identity for the resources. For existing applications, if a user-assigned managed identity is already set, if you don't specify the user-assigned identity when you add the resource to a DCR by using the portal, the machine defaults to using a system-assigned identity that's applied by the DCR.

### Add dataflows

On Collect and deliver, select Add new dataflow to add and configure data sources and destinations for the DCR. You can add multiple data sources to the same DCR or create multiple DCRs with different data sources. A DCR can have up to 10 data sources, and a VM can use any number of DCRs.

Setting
Description

Data source
Select a Data source type and provide values for the fields based on the data source type you select. See Add data sources for details about configuring each type of data source.

Destination
Add one or more destinations for each data source. Some data sources allow only a single destination. If you need multiple destinations, create another DCR.

While you can select multiple destinations of the same type for some data sources, be aware that this sends duplicate data to each destination and increases cost. See the details for each data type for the destinations it supports.

The Basics tab includes basic information about the DCR.

Setting
Description

Rule Name
A name for the DCR. The name should be something descriptive that helps you identify the rule.

Subscription
The subscription to store the DCR. The subscription doesn't need to be the same subscription as the virtual machines.

Resource
A resource group to store the DCR. The resource group doesn't need to be the same resource group as the virtual machines.

Region
The Azure region to store the DCR. The region must be the same region as any Log Analytics workspace or Azure Monitor workspace that's used in a destination of the DCR. If you have workspaces in different regions, create multiple DCRs to associate with the same set of machines.

Platform Type
Specifies the type of data sources that are available for the DCR, either Windows or Linux. None allows for both. 1

Data Collection Endpoint
Specifies the data collection endpoint (DCE) that's used to collect data. A DCE is required only if you're using a data source that requires one. These data sources appear grayed out in the Add data source tab if a DCE isn't selected. For most implementations, you can use a single DCE for each Log Analytics workspace. See Create a data collection endpoint for details on how to create a DCE.

1 This option sets the `kind` attribute in the DCR. You can set other values for this attribute, but the values aren't available to select in the portal.

### Add resources

On the Resources pane, select Add resources to add VMs that use the DCR. You don't need to add any VMs yet since you can update the DCR after creation and add or remove any resources. You can't add a virtual machine scale set with flexible orchestration as a resource for a DCR. Instead, add each VM included in the virtual machine scale set. If you select Enable Data Collection Endpoints on the Resources tab, you can select a DCE for each VM. This selection is only required if you're using Azure Monitor Private Links. Otherwise, don't select this option.

Important

When resources are added to a DCR, the default option in the Azure portal is to enable a system-assigned managed identity for the resources. For existing applications, if a user-assigned managed identity is already set, if you don't specify the user-assigned identity when you add the resource to a DCR by using the portal, the machine defaults to using a system-assigned identity that's applied by the DCR.

### Add data sources

On Collect and deliver, select Add data source to add and configure data sources and destinations for the DCR. You can add multiple data sources to the same DCR or create multiple DCRs with different data sources. A DCR can have up to 10 data sources, and a VM can use any number of DCRs.

Setting
Description

Data source
Select a Data source type and provide values for the fields based on the data source type you select. See Add data sources for details about configuring each type of data source.

Destination
Add one or more destinations for each data source. Some data sources allow only a single destination. If you need multiple destinations, create another DCR.

While you can select multiple destinations of the same type for some data sources, be aware that this sends duplicate data to each destination and increases cost. See the details for each data type for the destinations it supports.

## Add data sources

The following table lists the types of data you can collect from a VM client with Azure Monitor and where you can send that data. See the linked article for each to learn how to configure that data source.

Data source
Description
Client OS
Destinations

Windows events
Information sent to the Windows event logging system, including sysmon events
Windows
Log Analytics workspace

Performance counters
Numerical values that measure the performance of different aspects of the operating system and workloads
Windows
Linux
Azure Monitor metrics (preview) 
Log Analytics workspace

OpenTelemetry metrics
OpenTelemetry performance counters from the guest operating system
Windows
Linux
Azure Monitor workspace

Syslog
Information sent to the Linux event logging system
Linux
Log Analytics workspace

Text log
Information sent to a text log file on a local disk
Windows
Linux
Log Analytics workspace

JSON log
Information sent to a JSON log file on a local disk
Windows
Linux
Log Analytics workspace

IIS logs
Internet Information Service (IIS) logs from the local disk of Windows machines
Windows
Log Analytics workspace

SNMP traps
SNMP poll and trap data sent to the Syslog data table or custom text table
Linux
Log Analytics workspace

Windows Firewall logs
Windows client and server firewall log data collected by DCR and the Security and Audit solution from Marketplace in the Azure portal
Windows
Log Analytics workspace

## Verify operation

It can take up to 5 minutes for data to be sent to the destinations after you create a DCR. You can verify that the agent is operational and that data is being collected by querying the data in the Log Analytics workspace.

### Verify agent operation

Verify that the agent is operational and communicating properly with Azure Monitor by checking the Heartbeat for the VM. When an agent is properly communicating with Azure Monitor, it sends a record to the Heartbeat table every minute.

From the virtual machine in the Azure portal, select Logs and then click the Tables button. Under the Virtual machines category, click Run next to Heartbeat. If the agent is communicating correctly, you should see heartbeat records for the VM.

### Verify that records are received

Once you verify that the agent is communicating properly, make sure that the data you expect is being collected. Use the same process as above to view the data in the table for the data source that you configured. The following table lists the category and table for each data source.

Data source
Category
Table

Windows events
Virtual Machines
Event

Performance counters
Virtual Machines
Perf

OpenTelemetry metrics
Virtual Machines
Azure Monitor workspace

Syslog
Virtual Machines
Syslog

IIS logs
Virtual Machines
W3CIISLog

Text log
Custom Logs
<Custom table name>

JSON log
Custom Logs
<Custom table name>

## Duplicate data warning

Be careful of the following scenarios which may result in collecting duplicate data which will increase your billing charges:

- Creating multiple DCRs that have the same data source and associating them to the same VM. If you do have DCRs with the same data source, make sure that you configure them to filter for unique data.

- Creating a DCR that collects security logs and enabling Microsoft Sentinel for the same VMs. In this case, the same events will be sent to both the Event table (Azure Monitor) and in the SecurityEvent table (Microsoft Sentinel).

- Creating a DCR for a VM that's also running the legacy Log Analytics agent on the same machine. Both may be collecting identical data and storing it in the same table. Follow the guidance at Migrate to Azure Monitor Agent from Log Analytics agent to migrate from the legacy agent.

To list the DCRs associated with a VM in the Azure portal, see Manage data collection rule associations in Azure Monitor. You can also use the following PowerShell command to list all DCRs for a VM:

`Get-AzDataCollectionRuleAssociation -resourceUri <vm-resource-id>
`

## Related content

- Azure Monitor Agent overview - Review how Azure Monitor Agent collects data from virtual machines.

- Data collection rules in Azure Monitor - Learn how DCRs define sources, destinations, and associations.

- Collect performance counters from virtual machines with Azure Monitor - Configure performance counter collection for logs-based monitoring.

- Tutorial: Collect guest logs from an Azure virtual machine - Walk through collecting Windows event logs or Syslog from a monitored VM.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-03-20
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
