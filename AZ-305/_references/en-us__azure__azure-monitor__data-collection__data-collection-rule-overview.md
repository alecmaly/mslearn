# https://learn.microsoft.com/en-us/azure/azure-monitor/data-collection/data-collection-rule-overview

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/data-collection/data-collection-rule-overview

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
 

 

 

 

 
 
# Data collection rules (DCRs) in Azure Monitor

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Data collection rules (DCRs) provide a centralized Azure control plane for collection, processing, and routing in supported Azure Monitor data collection paths.

Depending on the scenario, a DCR controls all or some of the following aspects of data collection:

- Collection: The data sources and data to collect.

- Data shape: The schema of incoming data.

- Processing: Optional transformations that filter or modify data.

- Routing: The destinations where Azure Monitor sends the data.

Not every scenario uses every capability. For example, a DCR can define collection and routing without defining a transformation.

The DCR resource defines collection configuration. The experience that creates or manages the DCR can also perform setup outside the DCR. For example, the Azure portal workflow for virtual machines can install Azure Monitor agent and create resource-to-DCR associations. Destination resources retain their own configuration, such as workspace retention and table settings.

Important

A DCR is control-plane configuration, not a data-plane destination. Telemetry doesn't flow through the DCR resource. Collection components and Azure Monitor services retrieve or reference the DCR and apply its instructions at the appropriate stage of the data path.

## When to work with DCRs

Many Azure Monitor experiences create and manage DCRs and their associations for you. You don't need to work directly with these resources unless you need the control they provide.

Your goal
What to do

Enable an Azure Monitor experience such as VM insights or Container insights.
Use that experience. It creates and manages the required data collection resources. Continue to configure collection through the experience unless its documentation directs you to modify the DCR.

Inspect or troubleshoot configuration created by an Azure Monitor experience.
View the DCRs and their associated resources.

Apply a shared collection policy across resources, customize collection or processing, or manage configuration through infrastructure as code.
Work directly with DCRs. If the scenario assigns a DCR to resources, also manage the associations between them.

## Design DCRs as centralized collection policies

You centrally store and manage DCRs as Azure resources. Each DCR represents a collection policy that you can reuse wherever the same requirements apply. Design a DCR around a shared collection requirement, not an individual resource.

### Data collection rule associations (DCRAs)

Some data collection scenarios use a data collection rule association (DCRA) to apply a DCR to a monitored resource. Each DCRA connects one resource to one DCR.

The common reuse pattern is one DCR applied to many resources, with a separate DCRA for each resource:

- To apply one DCR to multiple resources, create an association for each resource.

- To apply multiple DCRs to one resource, create an association for each DCR.

The overall relationship between resources and DCRs is many-to-many, implemented through individual resource-to-DCR associations. Not all DCR scenarios use associations. For details, see Manage data collection rule associations.

For example, use one DCR for a central IT baseline and associate it with every applicable machine. Then layer a workload-specific DCR onto only the machines that run that workload. Create another DCR when the collection policy differs, not solely because you add another resource.

This centralized, reusable model provides:

- Consistent configuration across resources with the same collection requirements.

- Central updates that apply to all associated resources.

- Optional transformations that filter or modify incoming data before delivery.

- Scalable management through infrastructure as code and DevOps processes.

Before you change a shared DCR, identify the resources and clients that use it. For association-based scenarios, review its associations to understand which resources the change affects.

## Using a DCR

How Azure Monitor selects and applies a DCR depends on the data collection scenario.

Scenario
How Azure Monitor applies the DCR

Azure Monitor agent
Data collection rule association (DCRA)

Event hubs
Data collection rule association (DCRA)

Platform metrics (preview)
Data collection rule association (DCRA)

Platform logs (preview)
Data collection rule association (DCRA)

Direct ingestion
The API request identifies the DCR configuration that Azure Monitor applies.

Workspace transformation DCR
DCR is applied directly to the workspace.

## DCRs and the data path

Telemetry travels along a data path separate from the DCR resource. Depending on the scenario, collection components and Azure Monitor services use instructions in the DCR to collect data, optionally process it, and route it to a destination.

## Scenarios

The following sections summarize common scenarios and link to their detailed configuration guidance.

### Azure Monitor agent

Use the Azure Monitor agent to collect data from virtual machines and Kubernetes clusters.

Setup: When you use the Azure portal DCR creation experience and select virtual machines, Azure Monitor can install Azure Monitor agent if necessary and create an association between each machine and the DCR. After installation, the agent connects to Azure Monitor to retrieve its associated DCRs.

DCR role: The DCRs specify events and performance data to collect. For a Kubernetes cluster, this collection also includes Prometheus metrics. The agent uses that information to collect data and optionally apply a client-side transformation (Preview). After upload, Azure Monitor applies any ingestion-time transformation in the DCR and sends the data to the configured destination.

For more information, see Collect data from virtual machine client with Azure Monitor and Enable monitoring for Kubernetes clusters.

### Event Hubs (Preview)

Data path: Event Hubs sends data to Azure Monitor.

DCR role: Azure Monitor applies the collection, optional transformation, and routing configuration from DCRs associated with the event hub, then sends the data to the configured destinations.

For more information, see Ingest events from Azure Event Hubs into Azure Monitor Logs (preview).

### Platform metrics (Preview)

Azure resources automatically collect platform metrics and send them to Azure Monitor Metrics.

DCR role: For supported resources, a platform telemetry DCR identifies the metrics to export and their destination. A DCRA applies the DCR to each resource. Azure Monitor then exports the selected metrics to the configured Log Analytics workspace, storage account, or Event Hubs.

For more information, see Metrics export using data collection rules.

### Platform logs (Preview)

Platform logs, also called resource logs, are generated by Azure resources and services.

DCR role: For supported resources, a platform telemetry DCR identifies the log categories to collect and their destination. A DCRA applies the DCR to each resource, allowing one DCR to be reused across multiple resources. Azure Monitor routes the logs to the configured Log Analytics workspace, storage account, or Event Hubs. Continue to use diagnostic settings for resource types that don't support DCR-based platform log collection.

For supported resources, destinations, regions, and configuration steps, see Collect platform logs using data collection rules.

### Direct ingestion

Data path: A client sends a payload to a Logs Ingestion API endpoint and identifies the DCR in the request URI.

For evolving JSON attributes, schemaless ingestion (preview) can capture undeclared properties in a `dynamic` column before the ingestion-time transformation. Destination tables still have an explicit schema.

DCR role: The DCR declares the structure of the incoming data, includes any transformation instructions, and specifies the destination workspace and table.

For more information, see Logs ingestion API.

### Workspace transformation DCR

DCR role: A workspace transformation DCR provides transformations for data collection paths that don't otherwise use a DCR. Azure Monitor applies it directly to the Log Analytics workspace. After you create or update the DCR, allow some time for transformations to take effect on incoming data.

For more information, see Workspace transformation DCR.

## Transformations

Transformations are optional processing instructions in a DCR that filter or modify data. For details about standard Kusto Query Language (KQL) transformations, multi-stage processors, supported scenarios, and configuration, see Transformations in Azure Monitor.

## View DCRs

To view all the DCRs in your subscription, inspect a DCR definition, and see which resources are associated with it, see View data collection rules.

## Replace legacy data collection methods

DCR-based collection replaces selected legacy methods in Azure Monitor. Support varies by source and signal, so review the linked scenario guidance before migrating.

Legacy method
DCR method
Description

Log Analytics agent
Azure Monitor agent
Use the Azure Monitor agent to monitor virtual machines (VMs) and Kubernetes clusters that support VM insights and Container insights.

Diagnostic settings
Metrics export and platform log collection (preview)
Use DCR-based export for supported platform metrics and platform logs. Continue to use diagnostic settings for unsupported resource types and signals.

Data Collector API
Logs ingestion API
Use the Logs ingestion API to send data to a Log Analytics workspace from any REST client. It uses OAuth-based authentication (more secure than workspace keys), DCR-governed schema control and transformations, and provides improved reliability, scalability, and long-term platform support compared to the legacy HTTP Data Collector API.

## DCR regions

Availability: Data collection rules are available in all public regions where Log Analytics workspaces and the Azure Government and China clouds are supported. Air-gapped clouds aren't currently supported.

Resiliency: You create and store a DCR in a particular region, and the service backs it up to the paired-region within the same geography. The service is deployed to all three availability zones within the region, making it a zone-redundant service.

Single region data residency is a preview feature to enable storing customer data in a single region and is currently only available in the Southeast Asia Region (Singapore) of the Asia Pacific Geo and the Brazil South (Sao Paulo State) Region of the Brazil Geo. Single-region residency is enabled by default in these regions.

## Related content

For more information on how to work with DCRs, see:

- View data collection rules to inspect DCRs and their associated resources.

- Create data collection rules using the Azure portal for guided creation in supported scenarios.

- Manage data collection rule associations to apply DCRs to resources.

- Data collection rule structure for a description of the JSON structure of DCRs and the different elements used for different workflows.

- Sample data collection rules (DCRs) for sample DCRs for different data collection scenarios.

- Create data collection rules using JSON to author and deploy advanced configurations.

- Data collection endpoints (DCE) overview for the full context required for direct ingestion using the Logs Ingestion API.

- Azure Monitor service limits for limits that apply to each DCR.

 
 

 
 

 

 
 
 
 
 
 
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
