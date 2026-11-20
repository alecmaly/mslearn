# https://learn.microsoft.com/en-us/azure/azure-monitor/agents/azure-monitor-agent-overview

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/agents/azure-monitor-agent-overview

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
 

 

 

 

 
 
# Azure Monitor Agent overview

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 The Azure Monitor Agent collects monitoring data from the guest operating system of Azure and hybrid virtual machines (VMs). It delivers the data to Azure Monitor for use by features, insights, and other services, such as Microsoft Sentinel and Microsoft Defender for Cloud. This article covers the Azure Monitor Agent's capabilities and supported use cases.

For a short introduction to the Azure Monitor Agent, including a demo of deploying the agent in the Azure portal, see the video ITOps Talk: Azure Monitor Agent.

Note

The Azure Monitor Agent is the supported agent for collecting guest OS data in Azure Monitor. If you're currently using the legacy Log Analytics agent, see Migrate to the Azure Monitor Agent for guidance.

## Installation

The Azure Monitor Agent is one method of data collection for Azure Monitor. You install it on VMs running in Azure, in other clouds, or on-premises, where it has access to local logs and performance data. Without the agent, you can collect data only from the host machine because you have no access to the client operating system and running processes.

You can install the agent on a single machine or at scale using various methods, including a VM extension, Azure Policy, or enabling features like VM insights. For detailed installation options and instructions, see Install and manage the Azure Monitor Agent.

On Linux, the agent creates local user accounts to run its services. For the full list of accounts and their purpose, see Linux user accounts created during installation.

## Data collection

The Azure Monitor Agent collects data according to data collection rules (DCRs) associated with the agent. DCRs define what data is collected, how it gets processed, and where it gets sent.

When you install the agent, it retrieves and applies any associated DCRs and periodically checks for updates. It enables centralized and consistent configuration of data collection across multiple agents and environments.

For a full conceptual and architectural description of data collection rules, associations, transformations, and destinations, see Data collection rules (DCRs) in Azure Monitor. For guidance on organizing DCRs across environments and scenarios, see Best practices for DCR creation and management in Azure Monitor.

## Cost

There's no cost to use the Azure Monitor Agent, but you might incur charges for data ingestion and storage. For information on Log Analytics data collection and retention and for customer metrics, see Azure Monitor logs cost calculations and options and Analyze usage in a Log Analytics workspace.

## Supported regions

The Azure Monitor Agent is available for general availability features in all global Azure regions, Azure Government, and Azure operated by 21Vianet. The VM extension isn't supported in air-gapped clouds. However, the Windows MSI client installer supports air-gapped clouds. For more information, see Product availability by region.

## Supported services and features

The following tables identify the different environments and features that the Azure Monitor Agent and the legacy agent currently support. This information can help you determine whether the Azure Monitor Agent supports your current requirements. For guidance about migrating specific features, see Migrate to the Azure Monitor Agent from the Log Analytics agent.

### Windows agents

The following tables compare Azure Monitor Agent and legacy agent capabilities on Windows.

#### Supported environments

Environment
Azure Monitor Agent
Legacy agent

Azure
â
â

Other clouds (Azure Arc)
â
â

On-premises (Azure Arc)
â
â

Windows Client OS
â

#### Data collected

Data source
Azure Monitor Agent
Legacy agent

Event Logs
â
â

Performance
â
â

File-based logs
â
â

Internet Information Services (IIS) logs
â
â

#### Data destinations

Destination
Azure Monitor Agent
Legacy agent

Azure Monitor logs
â
â

#### Supported services and features

Service or feature
Azure Monitor Agent
Legacy agent

Microsoft Sentinel
â (Scope)
â

VM insights
â
â

Microsoft Defender for Cloud (uses only the Microsoft Defender for Endpoint agent)

Automation Update Management (moved to Azure Update Manager)
â
â

Azure Local
â

Update Manager (no longer uses agents)

Change tracking
â
â

SQL Best Practices Assessment
â

### Linux agents

The following tables compare Azure Monitor Agent and legacy agent capabilities on Linux.

#### Supported environments

Environment
Azure Monitor Agent
Legacy agent

Azure
â
â

Other clouds (Azure Arc)
â
â

On-premises (Azure Arc)
â
â

#### Data collected

Data source
Azure Monitor Agent
Legacy agent

Syslog
â
â

Performance
â
â

File-based logs
â

#### Data destinations

Destination
Azure Monitor Agent
Legacy agent

Azure Monitor logs
â
â

#### Supported services and features

Service or feature
Azure Monitor Agent
Legacy agent

Microsoft Sentinel
â (Scope)
â

VM insights
â
â

Microsoft Defender for Cloud (uses only the Microsoft Defender for Endpoint agent)

Automation Update Management (moved to Azure Update Manager)
â
â

Update Manager (no longer uses agents)

Change tracking
â
â

## Supported data sources

For a list of data sources that the Azure Monitor Agent can collect and instructions on how to configure them, see Collect data with the Azure Monitor Agent.

## Related content

- Install the Azure Monitor Agent on Windows and Linux virtual machines.

- Create a data collection rule to collect data from the agent and send it to Azure Monitor.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-07-28
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
