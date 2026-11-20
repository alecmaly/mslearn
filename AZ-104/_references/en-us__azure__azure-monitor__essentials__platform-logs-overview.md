# https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/platform-logs-overview

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/platform-logs-overview

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
 

 

 

 

 
 
# Azure Monitor data sources and data collection methods

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Monitor is based on a common monitoring data platform that you can use to analyze different types of data from multiple types of resources together by using a common set of tools. Currently, different sources of data for Azure Monitor use different methods to deliver their data, and each typically requires different types of configuration. This article describes common sources of monitoring data that Azure Monitor collects and their data collection methods. Use this article as a starting point to understand the options for collecting different types of data generated in your environment.

Important

There is a cost for collecting and retaining most types of data in Azure Monitor. To minimize your cost, ensure that you don't collect any more data than you require and that your environment is configured to optimize your costs. See Cost optimization in Azure Monitor for a summary of recommendations.

## Azure resources

Most resources in Azure generate a standard set of monitoring data described in the following table. Some services have more collectable data, described in other sections in this article. Regardless of the services that you're monitoring, start by understanding and configuring the collection of this core data.

Create diagnostic settings for each of the following data types to send them to a Log Analytics workspace, archive them to a storage account, or stream them to an event hub for ingestion by services outside of Azure. See Create diagnostic settings in Azure Monitor.

Data type
Description
Data collection method

Activity log
Provides insight into subscription-level events for Azure services, including service health records and configuration changes.
Collected automatically. View in the Azure portal or create a diagnostic setting to send it to other destinations. You can collect it in a Log Analytics workspace at no charge. See Azure Monitor activity log.

Platform metrics
Numerical values automatically collected at regular intervals for different aspects of a resource. Specific metrics vary for each type of resource.
Collected automatically and stored in Azure Monitor Metrics. View in metrics explorer or create a diagnostic setting to send it to other destinations. See Azure Monitor Metrics overview and Supported metrics with Azure Monitor for a list of metrics for different services.

Resource logs
Provides insight into operations that were performed within an Azure resource. The content of resource logs varies by the Azure service and resource type.
You must create a diagnostic setting to collect resource logs. See Azure resource logs and Supported services, schemas, and categories for Azure resource logs for details on each service.

## Log data from Microsoft Entra ID

Audit logs and sign in logs in Microsoft Entra ID are similar to the activity logs in Azure Monitor. Create diagnostic settings for each of the following data types to be sent to a Log Analytics workspace, archived to a storage account, or streamed to an event hub for ingestion by services outside of Azure. See Configure Microsoft Entra diagnostic settings for activity logs.

Data type
Description
Data collection method

Audit logs

Sign-in logs
Enable you to assess many aspects of your Microsoft Entra ID environment, including history of sign-in activity, audit trail of changes made within a particular tenant, and activities performed by the provisioning service.
Collected automatically with activity logs. View in the Azure portal or create a diagnostic setting to send it to other destinations.

## Apps and workloads

### Application data

Application monitoring in Azure Monitor is done with Application Insights, which collects data from applications running on various platforms in Azure, another cloud, or on-premises. When you enable Application Insights for an application, it collects metrics and logs related to the performance and operation of the application and stores it in the same Azure Monitor data platform used by other data sources.

For more information about the data that Application Insights collects and links to articles on onboarding your application, see Application Insights overview.

Data type
Description
Data collection method

Application logs
Operational data about your application, including page views, application requests, exceptions, and traces. Also includes dependency information between application components to support Application Map and data correlation.
Application logs are stored in a Log Analytics workspace that you select as part of the onboarding process.

Metrics
Numeric data measuring the performance of your application and user requests measured over intervals of time.
Metric data is stored in both Azure Monitor Metrics and the Log Analytics workspace.

Traces
Traces are a series of related events tracking end-to-end requests through the components of your application.
Traces are stored in the Log Analytics workspace for the app.

## Infrastructure

### Virtual machine data

Azure virtual machines create the same activity logs and platform metrics as other Azure resources. In addition to this host data, you need to monitor the guest operating system and the workloads running on it. This monitoring requires the Azure Monitor Agent or Azure Monitor SCOM Managed Instance. The following table includes the most common data to collect from VMs. For a more complete description of the different kinds of data you can collect from virtual machines, see Monitor virtual machines with Azure Monitor: Collect data.

Data type
Description
Data collection method

Windows Events
Logs for the client operating system and different applications on Windows VMs.
Deploy the Azure Monitor Agent (AMA) and create a data collection rule (DCR) to send data to Log Analytics workspace. See Collect data with Azure Monitor Agent.

Syslog
Logs for the client operating system and different applications on Linux VMs.
Deploy the Azure Monitor Agent (AMA) and create a data collection rule (DCR) to send data to Log Analytics workspace. See Collect Syslog events with Azure Monitor Agent. To use the VM as a Syslog forwarder, see Tutorial: Forward Syslog data to a Log Analytics workspace with Microsoft Sentinel by using Azure Monitor Agent.

Client Performance data
Performance counter values for the operating system and applications running on the virtual machine.
Deploy the Azure Monitor Agent (AMA) and create a data collection rule (DCR) to send data to Azure Monitor Metrics and/or Log Analytics workspace. See Collect data with Azure Monitor Agent.

Enable VM Insights to send predefined aggregated performance data to Log Analytics workspace. See Enable VM Insights overview for installation options.

Processes and dependencies
Details about processes running on the machine and their dependencies on other machines and external services. Enables the map feature in VM Insights.
Enable VM Insights on the machine with the processes and dependencies option. See Enable VM Insights overview for installation options.

Text logs
Application logs written to a text file.
Deploy the Azure Monitor Agent (AMA) and create a data collection rule (DCR) to send data to Log Analytics workspace. See Collect logs from a text or JSON file with Azure Monitor Agent.

IIS logs
Logs created by Internet Information Service (IIS).
Deploy the Azure Monitor Agent (AMA) and create a data collection rule (DCR) to send data to Log Analytics workspace. See Collect IIS logs with Azure Monitor Agent.

SNMP traps
Widely deployed management protocol for monitoring and configuring Linux devices and appliances.
See Collect SNMP trap data with Azure Monitor Agent.

Management pack data
If you have an existing investment in System Center Operations Manager, you can migrate to the cloud while retaining your investment in existing management packs by using Azure Monitor SCOM Managed Instance.
Azure Monitor SCOM Managed Instance stores data collected by management packs in an instance of SQL MI. See Configure Log Analytics for Azure Monitor SCOM Managed Instance to send this data to a Log Analytics workspace.

### Kubernetes cluster data

Azure Kubernetes Service (AKS) clusters create the same activity logs and platform metrics as other Azure resources. In addition to this host data though, they generate a common set of cluster logs and metrics that you can collect from your AKS clusters and Arc-enabled Kubernetes clusters.

Data type
Description
Data collection method

Cluster Metrics
Usage and performance data for the cluster, nodes, deployments, and workloads.
Enable managed Prometheus for the cluster to send cluster metrics to an Azure Monitor workspace. See Enable Prometheus and Grafana for onboarding and Default Prometheus metrics configuration in Azure Monitor for a list of metrics that are collected by default.

Kubernetes logs
Standard Kubernetes logs including events for the cluster, nodes, deployments, and workloads.
Enable Container Insights for the cluster to send container logs to a Log Analytics workspace. See Enable Container Insights for onboarding and Configure data collection in Container Insights using data collection rule to configure which logs are collected.

## Custom sources

Custom data sources, especially those outside of Azure, require custom data collection methods. Refer to the following table to understand the options.

Data type
Description
Data collection method

Event Hubs logs
Collect data from Azure Event Hubs.
Create a data collection rule to define destination workspace and structure of incoming data. See Ingest events from Azure Event Hubs into Azure Monitor Logs (preview).

REST API logs
Collect log data from any REST client and store in Log Analytics workspace.
Create a data collection rule to define destination workspace and any data transformations. See Logs ingestion API in Azure Monitor.

Metrics
Collect custom metrics for Azure resources from any REST client.
See Send custom metrics for an Azure resource to the Azure Monitor metric store by using a REST API.

## Next steps

- Learn more about the types of monitoring data collected by Azure Monitor and how to view and analyze this data.

- Review Cost optimization in Azure Monitor to control what you collect and retain.

- Create diagnostic settings in Azure Monitor to route platform logs and metrics to your destinations.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-08-07
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
