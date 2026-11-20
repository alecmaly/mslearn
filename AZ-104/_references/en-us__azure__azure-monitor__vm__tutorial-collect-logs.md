# https://learn.microsoft.com/en-us/azure/azure-monitor/vm/tutorial-collect-logs

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/vm/tutorial-collect-logs

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
 

 

 

 

 
 
# Tutorial: Collect guest logs from an Azure virtual machine

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 After you enable monitoring for an Azure virtual machine to collect guest metrics, you can create additional data collection rules (DCRs) to collect guest logs. These logs provide rich insights into the behavior of the operating system and applications running on the virtual machine, which can be used for troubleshooting, performance monitoring, and security analysis.

This tutorial shows how to collect event logs from Windows machines and syslog from Linux machines. These are two of the data sources available for virtual machines. Other data sources are documented in Collect guest log data from virtual machines with Azure Monitor.

In this tutorial, you learn how to:

- Create a DCR that sends guest log data to a Log Analytics workspace.

- View guest logs in Log Analytics.

## Prerequisites

To complete this tutorial, you need either:

- A virtual machine with monitoring enabled by following Tutorial: Enable enhanced monitoring for an Azure virtual machine.

- Virtual machine scale set with monitoring enabled by following Tutorial: Enable monitoring for an Azure virtual machine scale set.

## Create a data collection rule

Data collection rules in Azure Monitor define data to collect and where it should be sent. On the Monitor menu in the Azure portal, select Data Collection Rules. Then select Create to create a new DCR.

On the Basics tab, enter a Rule Name, which is the name of the rule displayed in the Azure portal. Select a Subscription, Resource Group, and Region where the DCR and its associations are stored. These settings don't need to be the same as the resources being monitored.

The Platform Type defines the options that are available as you define the rest of the DCR. Select Windows or Linux if the rule is associated only with those resources or select Custom if it's associated with both types.

## Select resources

On the Resources tab, select Add resources and then select your virtual machine. Add any other machines that should share the same log collection. The DCR applies to all virtual machines in the selected scope.

## Select data sources

Select Add data source and then either Windows event logs or Linux Syslog.

- 
Windows Event Logs

- 
Linux Syslog

Select the event logs and levels that you want to collect. A common selection is Critical, Error, Warning events for Application and System logs.

For more detail about configuring this data source, see Collect Windows events with Azure Monitor Agent.

Select the facilities and log levels that you want to collect. To collect warning levels and above for all facilities, check the box next the Facility to select all facilities and then select LOG_WARNING for Set minimum log level for selected facilities.

For more detail about configuring this data source, see Collect Syslog events with Azure Monitor Agent.

## Select destinations

Select the Destination tab. Azure Monitor Logs should already be selected for Destination type. Select your Log Analytics workspace for Account or namespace. If you don't already have a workspace, you can select the default workspace for your subscription, which is created automatically. Select Add data source to save the data source.

## Save DCR

Select Review + create to create the DCR.

## View logs

Data is retrieved from a Log Analytics workspace by using a log query written in Kusto Query Language (KQL). Although a set of precreated queries is available for virtual machines, here you use a simple query to inspect the events being collected.

Select Logs from your virtual machine's menu. Log Analytics opens with an empty query window with the scope set to that machine. Any queries include only records collected from that machine.

Note

The Queries window might open when you open Log Analytics. It includes precreated queries that you can use. For now, close this window because we're going to manually create a simple query.

In the empty query window, run one of the following queries depending on the data source you configured.

- 
Windows event logs

- 
Syslog

To verify that data is being collected, check for records in the Event table. From the virtual machine or from the Log Analytics workspace in the Azure portal, select Logs and then click the Tables button. Under the Virtual machines category, click Run next to Event.

To verify that data is being collected, check for records in the Syslog table. From the virtual machine or from the Log Analytics workspace in the Azure portal, select Logs and then click the Tables button. Under the Virtual machines category, click Run next to Syslog.

## 

Note

If the query doesn't return any data, you might need to wait a few minutes until events are created on the virtual machine to be collected. You might also need to modify the data source in the DCR to include other categories of events.

For a tutorial on using Log Analytics to analyze log data, see Log Analytics tutorial. For a tutorial on creating alert rules from log data, see Tutorial: Create a log search alert for an Azure resource.

Create a log search alert for an Azure resource

 
 

 
 

 

 
 
 
 
 
 
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
 2026-06-02
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
