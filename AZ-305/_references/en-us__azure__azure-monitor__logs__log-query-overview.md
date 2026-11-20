# https://learn.microsoft.com/en-us/azure/azure-monitor/logs/log-query-overview

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/logs/log-query-overview

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
 

 

 

 

 
 
# Log queries in Azure Monitor

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Monitor Logs is based on Azure Data Explorer and uses the same Kusto Query Language (KQL) to write log queries. This rich language is designed to be easy to read and author, which allows you to start writing queries with minimal guidance.

Areas in Azure Monitor where you use queries include:

Area
Description

Log Analytics
Use this primary tool in the Azure portal to edit log queries and interactively analyze their results. Even if you intend to use a log query elsewhere in Azure Monitor, you typically write and test it in Log Analytics before you copy it to its final location.

Log search alert rules
Proactively identify issues from data in your workspace. Each alert rule is based on a log query that runs automatically at regular intervals. The results are inspected to determine if an alert should be created.

Workbooks
Include the results of log queries by using different visualizations in interactive visual reports in the Azure portal.

Azure dashboards
Pin the results of any query into an Azure dashboard, which allows you to visualize log and metric data together and optionally share with other Azure users.

Azure Logic Apps
Use the results of a log query in an automated workflow by using a logic app workflow.

PowerShell
Use the results of a log query in a PowerShell script from a command line or an Azure Automation runbook that uses `Invoke-AzOperationalInsightsQuery`.

Log Analytics query API
Retrieve log data from the workspace from any REST API client. The API request includes a query that runs against Azure Monitor to determine the data to retrieve.

Important

Since July 1, 2025, querying log data and events requires TLS 1.2 or higher when using query API endpoints for Log Analytics or Application Insights. For more information, see Secure data in transit.

### Azure Monitor query client libraries

Retrieve log data from the workspace via an idiomatic client library for the following ecosystems:

- .NET

- Go

- Java

- JavaScript

- Python

For an example of how to implement the Azure Monitor Query client library for Python, see Analyze data in Azure Monitor Logs using a notebook.

## Get started

The best way to get started learning to write log queries by using KQL is to use the following tutorials and examples:

- Log Analytics tutorial - Tutorial on using the features of Log Analytics, which is the tool that you use in the Azure portal to edit and run queries. It also allows you to write simple queries without directly working with the query language. If you haven't used Log Analytics before, start here so that you understand the tool you use with the other tutorials and samples.

- KQL tutorial - Guided walk through basic KQL concepts and common operators. This is the best place to start to come up to speed with the language itself and the structure of log queries.

- Example queries - Description of the example queries available in Log Analytics. You can use the queries without modification or use them as samples to learn KQL.

- Chat with your data - Use the Observability Agent to explore and analyze your log data using natural language. The agent runs KQL queries on your behalf and surfaces insights without requiring you to write queries.

## Reference documentation

Documentation for KQL, including the reference for all commands and operators, is available in the Azure Data Explorer documentation. Even as you get proficient at using KQL, you still regularly use the reference to investigate new commands and scenarios that you haven't used before.

## Language differences

Although Azure Monitor uses the same KQL as Azure Data Explorer, there are some differences. The KQL documentation specifies those operators that aren't supported by Azure Monitor or that have different functionality. Operators specific to Azure Monitor are documented in the Azure Monitor content. The following sections list the differences between versions of the language for quick reference.

### Not supported in Azure Monitor

Statements

- Alias

- Query parameters

Functions

- cluster()

- cursor_after()

- cursor_before_or_at()

- cursor_current(), current_cursor()

- database()

- current_principal()

- extent_id()

- extent_tags()

Operator

Cross-Cluster Join

Plug-ins

- Python plugin

- sql_request plugin

### Operators exclusive to Azure Monitor

The following operators support specific Azure Monitor features and aren't available outside of Azure Monitor:

- workspace()

- app()

- resource()

## Next steps

- Walk through a tutorial on writing queries.

- Access the complete reference documentation for KQL.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-04-29
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
