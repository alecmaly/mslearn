# https://learn.microsoft.com/en-us/azure/azure-monitor/vm/vminsights-maps-retirement

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/vm/vminsights-maps-retirement

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
 

 

 

 

 
 
# VM Insights Map and Dependency Agent retirement guidance

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 The VM Insights Map feature and the Dependency Agent are deprecated. They retire and aren't supported after June 30, 2028. VM Insights Map is a feature of Azure Monitor VM insights that discovers running processes on virtual machines and the network connections between those machines and external services. The Dependency Agent collects the process and connection data that powers the map. This article calls out impacted functionality, provides offboarding guidance, and lists key dates.

## Customer impact

With this retirement, all functionality associated with the VM Insights Map and the Dependency Agent will be retired.

Specifically, customers can't:

- Access the Map tab in VM Insights in the Azure portal

- Access the Connections Overview workbook, which uses VM Insights Map data

- Install the Dependency Agent on new VMs from the Azure portal. Customers might still install the Dependency Agent through existing downloaded binaries, but these binaries can't send data

- Send new data to a Log Analytics workspace by using the Dependency Agent

- Query the Service Map API, the REST API that programmatically returns the same dependency data that powers VM Insights Map

Existing VM Insights Map data ingested by the Dependency Agent remains available in the associated tables (`VMComputer`, `VMProcess`, `VMConnection`, `VMBoundPort`). Your Log Analytics workspace settings determine data retention.

As part of the retirement process:

- No new operating system versions are supported for the Dependency Agent after June 30, 2025.

- No new Azure regions are supported for the Dependency Agent after June 30, 2025.

- Customers can't onboard new VMs from the Azure portal after September 30, 2025. Other onboarding methods remain available until the feature is no longer supported.

## Recommended action

Offboard from the VM Insights Map feature before the retirement date. To continue collecting data about processes running on virtual machines and external process dependencies, evaluate a replacement solution in the Azure Marketplace monitoring and diagnostics category. For inventory tracking, use the Azure Monitor Agent with Change Tracking and Inventory. If you deployed the Dependency Agent to your VMs through an Azure Policy initiative assignment, see Migrate Dependency Agent policy and initiative assignments for how to identify and update those assignments.

## Finding VMs currently using VM Insights Map

### Azure Advisor retirement recommendations

Azure Advisor shows a retirement recommendation, Migrate from Dependency Agent and VM Insights Map, for resources with Dependency Agent installed.

To find it, in the Azure portal go to Advisor > Recommendations > Reliability, add a filter with Recommendation Type set to Migrate from Dependency Agent and VM Insights Map, and select Apply.

Check the Advisor dashboard for this recommendation on the following resource types:

- Virtual Machines

- Virtual Machine Scale Sets

- Azure Arc Machines

### Query for finding VMs

The following query lists all the VMs that have Dependency Agent installed. The query provides all cloud VMs and Arc-connected VMs, on-premises VMs utilizing the Dependency Agent without Arc connectivity are not listed.

`Resources
| where type in ('microsoft.compute/virtualmachines/extensions',
 'microsoft.hybridcompute/machines/extensions',
 'microsoft.connectedvmwarevsphere/virtualmachines/extensions')
| where 'Microsoft.Azure.Monitoring.DependencyAgent' == properties.publisher
| project id = tolower(substring(id, 0, indexof_regex(id, '(?i)/extensions')))
| join kind = inner (resources | extend id = tolower(id)) on id
| extend systemType = tostring(dynamic ({'microsoft.hybridcompute/machines' : 'ARC VM',
 'microsoft.compute/virtualmachines' : 'VM',
 'microsoft.connectedvmwarevsphere/virtualmachines' : 'AVS'
 })[type])
| project subscriptionId, resourceGroup, name, systemType, id, tenantId
| union (
 resources
 | where ['type'] == 'microsoft.compute/virtualmachinescalesets'
 | where properties.virtualMachineProfile.extensionProfile.extensions has 'Microsoft.Azure.Monitoring.DependencyAgent'
 | project subscriptionId, resourceGroup, name, systemType = 'VMSS', id, tenantId
)
| sort by subscriptionId asc, resourceGroup asc, name asc
`

To run the query, use the Resource Graph Explorer. The query runs in the existing Azure portal scope. For more information on how to set scope and run Azure Resource Graph queries in the portal, see Quickstart: Run Resource Graph query using Azure portal.

### Find Dependency Agent installations using Log Analytics

Run the following query in your Log Analytics workspace to identify Dependency Agent installations.

`VMComputer
| where TimeGenerated >= ago(7d)
| extend IsVMSS = isnotempty(AzureVmScaleSetResourceId)
| extend
 ResourceId = tolower(iff(IsVMSS, AzureVmScaleSetResourceId,
 _ResourceId))
| extend _Key = iff(isnotempty(ResourceId), ResourceId, AgentId),
 Name = tolower(iff(IsVMSS, AzureVmScaleSetName, DisplayName)),
 SubscriptionId = tolower(AzureSubscriptionId)
| summarize arg_max(TimeGenerated, *) by _Key, SubscriptionId
| project-rename MostRecentData = TimeGenerated
| project
 SubscriptionId,
 Name,
 OperatingSystem = OperatingSystemFamily,
 DependencyAgentVersion,
 MostRecentData,
 ResourceGroup = extract(@"/resourcegroups/([^/]*)", 1, ResourceId),
 Type = case(
 ResourceId contains "microsoft.compute/virtualmachines/", "VM",
 ResourceId contains "microsoft.compute/virtualmachinescalesets/", "VMSS",
 ResourceId contains "microsoft.hybridcompute/machines/", "ARC",
 "Other"
 ),
 Notes = iff(
 OperatingSystemFamily == "linux" or
 parse_version(DependencyAgentVersion) >= parse_version("9.10.10"),
 "",
 "Caution"
 ),
 ResourceLink = iff(
 ResourceId startswith "/subscriptions/",
 strcat("https://portal.azure.com/#resource", ResourceId),
 ""
 )
| sort by
 SubscriptionId asc,
 ResourceGroup asc,
 Name asc,
 Type asc
`

The `Type` column classifies each system as follows:

Type
Description

VM
Azure Virtual Machine

VMSS
Azure Virtual Machine Scale Set

ARC
Azure Arc connected machine

Other
Couldn't be classified as VM, VMSS, or ARC. Might include standalone installations that aren't connected to an Azure resource. `ResourceId` and `ResourceLink` are empty for these.

For Azure connected resources (VM, VMSS, ARC), right-click a cell in the `ResourceLink` column and select Go to link to go directly to the resource in the Azure portal. The `ResourceLink` column is empty for installations that aren't connected to an Azure resource (`Type` = `Other`). If the `Notes` column shows `Caution` for a system, that machine is running an older version of Dependency Agent that might cause a system crash during uninstallation. Proceed carefully with those systems.

## Disabling the VM Insights Map experience

### Removing Dependency Agent from a single VM

For steps to uninstall, see Uninstall the Dependency Agent.

For manual uninstallation instructions:

- Manually uninstall Dependency Agent on Windows

- Manually uninstall Dependency Agent on Linux

## Key dates

Date
Event

June 30, 2025
No new operating system versions supported for the Dependency Agent

June 30, 2025
No new Azure regions supported for the Dependency Agent

July 2, 2025
Retirement announcement

September 30, 2025
Customers restricted from onboarding new VMs using the Azure portal

June 30, 2028
Product retired. Documentation archived and all experiences removed.

## Frequently asked questions

Does this retirement affect VM Insights performance monitoring?

No. VM Insights performance monitoring uses Azure Monitor Agent and isn't affected by this retirement.

Will my existing data in `VMComputer`, `VMProcess`, `VMConnection`, and `VMBoundPort` be deleted?

No. Your Log Analytics workspace retains already ingested data according to its retention settings.

The Dependency Agent was deployed to my VMs through a policy assignment that I don't manage. What should I do?

Contact your Azure administrator to remove the policy or initiative assignment that deploys the Dependency Agent. See Migrate Dependency Agent policy and initiative assignments.

Do I need to act before June 30, 2028?

Don't install the Dependency Agent on new systems. Existing installations reach end of support on June 30, 2028, and data ingestion is disabled sometime after that date. Offboard as soon as possible.

## Support

For assistance with offboarding and migration, use the following resources:

- Microsoft Q&A - post questions tagged with `azure-monitor`.

- Azure support plans - open a support ticket for migration assistance.

- Azure Advisor - check your Advisor dashboard for personalized retirement recommendations and affected resource lists.

Support for Dependency Agent issues is available until June 30, 2028. After that date, Microsoft provides no further support for the Dependency Agent.

 
 

 
 

 

 
 
 
 
 
 
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
