# https://learn.microsoft.com/en-us/azure/governance/resource-graph/changes/resource-graph-changes

Source: https://learn.microsoft.com/en-us/azure/governance/resource-graph/changes/resource-graph-changes

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
 

 

 

 

 
 
# Analyze changes to your Azure resources

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Resources change through the course of daily use, reconfiguration, and even redeployment. While most change is by design, sometimes it can break your application. With the power of Azure Resource Graph, you can find when a resource changed due to a control plane operation sent to the Azure Resource Manager URL.

Change Analysis goes beyond standard monitoring solutions, alerting you to live site issues, outages, or component failures and explaining the causes behind them.

## How it works

Change Analysis ingests data into Resource Graph for queries and to power the portal experience. Change Analysis data can be accessed using:

- The `POST Microsoft.ResourceGraph/resources` API (preferred) for querying across tenants and subscriptions.

- The following APIs (under a specific scope, such as `LIST` changes and snapshots for a specific virtual machine):

- `GET/LIST Microsoft.Resources/Changes`

- `GET/LIST Microsoft.Resources/Snapshots`

When a resource is created, updated, or deleted via the Azure Resource Manager control plane, Resource Graph uses its Change Actor functionality to identify the changes.

Note

Currently, Azure Resource Graph doesn't:

- Observe changes made to a resource's data plane API, such as writing data to a table in a storage account.

- Support file and configuration changes over App Service.

## Change Analysis in the portal

Change Analysis experiences across the Azure portal are powered using the Azure Resource Graph `Microsoft.ResourceGraph/resources` API. You can query this API for changes made to many of the Azure resources you interact with, including App Services (`Microsoft.Web/sites`) or Virtual Machines (`Microsoft.Compute/virtualMachines`).

The Azure Resource Graph Change Analysis portal experience provides:

- An onboarding-free experience, giving all subscriptions and resources access to change history.

- Tenant-wide querying, rather than select subscriptions.

- Change history summaries aggregated into cards at the top of the new Resource Graph Change Analysis.

- More extensive filtering capabilities.

- Improved accuracy and relevance of changed by information, using Change Actor functionality.

Learn how to view the new Change Analysis experience in the portal.

## Supported resource types

Change Analysis supports changes to resource types from the following Resource Graph tables:

- `resources`

- `resourcecontainers`

- `healthresources`

You can compose and join tables to project change data any way you want.

## Data retention

Changes are queryable for 14 days. For longer retention, you can integrate your Resource Graph query with Azure Logic Apps and manually export query results to any of the Azure data stores like Log Analytics for your desired retention.

## Cost

You can use Azure Resource Graph Change Analysis at no extra cost.

## Send feedback for more data

Submit feedback via the Change Analysis experience in the Azure portal.

## Next steps

Get resource changes

 
 

 
 

 

 
 
 
 
 
 
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
 2025-10-31
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
