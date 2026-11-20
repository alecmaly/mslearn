# https://learn.microsoft.com/en-us/azure/azure-monitor/data-collection/data-collection-endpoint-overview

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/data-collection/data-collection-endpoint-overview

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
 

 

 

 

 
 
# Data collection endpoints in Azure Monitor

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 A data collection endpoint (DCE) is an Azure resource that defines a unique set of endpoints related to data collection, configuration, and ingestion in Azure Monitor. This article provides an overview of data collection endpoints and explains how to create and set them up based on your deployment.

Note

This article only relates to data collection scenarios in Azure Monitor that use a data collection rule (DCR). Legacy data collection scenarios such as collecting resource logs with diagnostic settings or Application Insights data collection don't yet use DCEs in any way.

## When is a DCE required?

A DCE isn't always required for data collection since the data source might use a public endpoint or the ingestion endpoints in the DCR. The following sections describe the scenarios where a DCE is required.

### Azure Monitor Agent (AMA)

Azure Monitor Agent uses a public endpoint by default to retrieve its configuration from Azure Monitor. A DCE is only required if you're using Private Link.

Important

Since Azure Monitor Private Link Scope (AMPLS) is dependent on DNS Private Link zones, any Azure Monitor Agent installation connected to a network that shares DNS with AMPLS resources requires a DCE. For more information, see Enable network isolation for Azure Monitor Agent by using Private Link.

View the agents associated with a DCE from its Resources page. Select Add to add more agents. To remove them, select one or more agents and select Disassociate.

A DCE is required for certain AMA data sources. In this case, the DCE is specified in the DCR using that data source. If an agent is associated with multiple DCRs, a DCE is only required in those DCRs with data sources that require it. Other data sources can continue to use the public endpoint.

Important

If the data source is sending to a destination configured for Private Link, the DCE configured in the DCR for that data source must be added to AMPLS.

The following data sources currently require a DCE:

- Windows Firewall Logs

- Prometheus Metrics (Container Insights)

View the DCE for a DCR from the Overview page of the DCR. Select Configure DCE to modify it.

### Logs ingestion API

When you create a DCR for Logs ingestion API, the DCR has a `logsIngestion` property, which is an endpoint for sending logs by using the API. If you use this endpoint, you don't need a DCE. Use a DCE instead of the DCR endpoint if you prefer. You must use a DCE if you're sending data to a Log Analytics workspace configured for Private Link.

## Components of a DCE

A data collection endpoint includes the components required to ingest data into Azure Monitor and send configuration files to Azure Monitor Agent.

How you set up endpoints for your deployment depends on whether your monitored resources and Log Analytics workspaces are in one or more regions.

This table describes the components of a data collection endpoint, related regionality considerations, and how to set up the data collection endpoint when you create a data collection rule using the portal:

Component
Description
Regionality considerations
Data collection rule configuration

Logs ingestion endpoint
The endpoint that ingests logs into the data ingestion pipeline. Azure Monitor transforms the data and sends it to the defined destination Log Analytics workspace and table based on a DCR ID sent with the collected data.
Example: `<unique-dce-identifier>.<regionname>-1.ingest`.
Same region as the destination Log Analytics workspace.
Set on the Basics tab when you create a data collection rule using the portal.

Metrics ingestion endpoint
The endpoint that ingests metrics into the data ingestion pipeline. Azure Monitor transforms the data and sends it to the defined destination Azure Monitor workspace and table based on a DCR ID sent with the collected data.
Example: `<unique-dce-identifier>.<regionname>-1.metrics.ingest`.
Same region as the destination Azure Monitor workspace.
Set on the Basics tab when you create a data collection rule using the portal.

Configuration access endpoint
The endpoint from which Azure Monitor Agent retrieves data collection rules (DCRs).
Example: `<unique-dce-identifier>.<regionname>-1.handler.control`.
Same region as the monitored resources.
Set on the Resources tab when you create a data collection rule using the portal.

## How to set up data collection endpoints based on your deployment

- Scenario: All monitored resources are in the same region as the destination Log Analytics workspace

Set up one data collection endpoint to send configuration files and receive collected data.

- Scenario: Monitored resources send data to a Log Analytics workspace in a different region

- Create a data collection endpoint in each region where you have Azure Monitor Agent deployed to send configuration files to the agents in that region.

- Send data from all resources to a data collection endpoint in the region where your destination Log Analytics workspaces are located.

- Scenario: Monitored resources in one or more regions send data to multiple Log Analytics workspaces in different regions

- Create a data collection endpoint in each region where you have Azure Monitor Agent deployed to send configuration files to the agents in that region.

- Create a data collection endpoint in each region with a destination Log Analytics workspace to send data to the Log Analytics workspaces in that region.

- Send data from each monitored resource to the data collection endpoint in the region where the destination Log Analytics workspace is located.

## Prerequisites

You must register the `Microsoft.Insights` resource provider in your subscription before you create a data collection endpoint. By default, this provider isn't registered. Register it by running the following command:

`az provider register --namespace Microsoft.Insights
`

## Create a data collection endpoint

- 
Azure portal

- 
CLI

- 
REST API

- On the Azure Monitor menu in the Azure portal, select Data collection endpoints under the Settings section.

 

- Select Create to create a new data collection endpoint. Enter a Name and specify a Subscription, Resource group, and Region. This information specifies where the DCE is created.

 

- Select Review + create to review the details of the DCE, and then select Create.

- After deployment finishes, select Go to resource. On the endpoint's Overview page, confirm that Provisioning state shows Succeeded to verify that the DCE was created.

Create a data collection endpoint by using az monitor data-collection endpoint create. The following example creates a DCE with public network access disabled. Replace the placeholder values with your own.

`az monitor data-collection endpoint create \
 --name "myCollectionEndpoint" \
 --resource-group "myResourceGroup" \
 --location "eastus" \
 --public-network-access "Disabled"
`

Verify that the endpoint was created and review its provisioning state by using az monitor data-collection endpoint show:

Create DCEs by using the DCE REST APIs.

Create associations between endpoints to your target machines or resources by using the DCRA REST APIs.

## Sample data collection endpoint

The following sample data collection endpoint (DCE) is for virtual machines with Azure Monitor Agent, with public network access disabled so that the agent only uses Private Link to communicate and send data to Azure Monitor and Log Analytics.

`{
 "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Insights/dataCollectionEndpoints/myCollectionEndpoint",
 "name": "myCollectionEndpoint",
 "type": "Microsoft.Insights/dataCollectionEndpoints",
 "location": "eastus",
 "tags": {
 "tag1": "A",
 "tag2": "B"
 },
 "properties": {
 "configurationAccess": {
 "endpoint": "https://mycollectionendpoint-abcd.eastus-1.handler.control.monitor.azure.com"
 },
 "logsIngestion": {
 "endpoint": "https://mycollectionendpoint-abcd.eastus-1.ingest.monitor.azure.com"
 },
 "metricsIngestion": {
 "endpoint": "https://mycollectionendpoint-abcd.eastus-1.metrics.ingest.monitor.azure.com"
 },
 "networkAcls": {
 "publicNetworkAccess": "Disabled"
 }
 },
 "systemData": {
 "createdBy": "user1",
 "createdByType": "User",
 "createdAt": "yyyy-mm-ddThh:mm:ss.sssssssZ",
 "lastModifiedBy": "user2",
 "lastModifiedByType": "User",
 "lastModifiedAt": "yyyy-mm-ddThh:mm:ss.sssssssZ"
 },
 "etag": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
`

## Limitations

Data collection endpoints only support Log Analytics workspaces and Azure Monitor Workspace as destinations for collected data. Custom metrics (preview) collected and uploaded via Azure Monitor Agent aren't currently controlled by DCEs.

## Next steps

- Add an endpoint to an Azure Monitor Private Link Scope resource

- Data Collection Endpoint (DCE) Private IP Endpoint compression (preview).

 
 

 
 

 

 
 
 
 
 
 
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
 2026-08-09
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
