# https://learn.microsoft.com/en-us/azure/azure-monitor/logs/log-analytics-overview

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/logs/log-analytics-overview

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
 

 

 

 

 
 
# Overview of Log Analytics in Azure Monitor

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 The Log Analytics tool in the Azure portal lets you run and edit log queries against data in the Azure Monitor Logs store. It offers two modes that make log data simpler to explore and analyze for both basic and advanced users:

- Simple mode provides the most commonly used Azure Monitor Logs functionality in an intuitive, spreadsheet-like experience. Just point and click to filter, sort, and aggregate data to get to the insights you need most of the time.

- KQL mode gives advanced users the full power of Kusto Query Language (KQL) to derive deeper insights from their logs using the Log Analytics query editor.

Whether you work with the results of your queries interactively or use them with other Azure Monitor features, such as log search alerts or workbooks. Log Analytics is the tool that you use to write and test them.

This article describes the Log Analytics user interface and its features. If you want to jump right into a tutorial, see Log Analytics tutorial.

## Introduction video

## Open Log Analytics

To open Log Analytics in the Azure portal, select Logs either in Azure Monitor, in a Log Analytics workspace, or from a specific resource. The tool is always the same, but where you start determines the data that's available.

When you open Logs from Azure Monitor or a Log Analytics workspaces, you have access to all of the records in a workspace. When you select Logs from another type of resource, your data is limited to log data for that resource. For more information, see Log query scope and time range in Azure Monitor Log Analytics.

When you start Log Analytics, a dialog appears that contains example queries. The queries are categorized by solution. Browse or search for queries that match your requirements. You might find one that does exactly what you need. You can also load one to the editor and modify it as required. Browsing through example queries is a good way to learn how to write your own queries.

If you want to start with an empty script and write it yourself, close the example queries. If you want to access the example queries again, select Queries hub at the top of the screen or through the left sidebar.

## Log Analytics interface

- 
Simple mode

- 
KQL mode

The following image identifies four Log Analytics components in simple mode:

- Top action bar

- Left sidebar

- Results window

- More tools

The following image identifies five Log Analytics components in KQL mode:

- Top action bar

- Left sidebar

- Query window

- Results window

- More tools

### Top action bar

- 
Simple mode

- 
KQL mode

In simple mode, the top bar has controls for working with data and switching to KQL mode.

Option
Description

Time range
Select the time range for the data available to the query. In KQL mode, if you set a different time range in your query, the time range you set in the time picker is overridden.

Show
Configure the number of entries Log Analytics retrieves in simple mode. The default limit is 1000. For more information on query limits, see Configure query results limit.

Add
Add filters, and apply simple mode operators, as described in Explore and analyze data in simple mode.

Simple/KQL mode
Switch between Simple and KQL mode.

Note

In simple mode, the top action bar doesn't include a Run button. The results update automatically as the user refines the query.

In KQL mode, the top bar has controls for working with a query and switching to simple mode.

Option
Description

Run button
Run the selected query in the query window. You can also select Shift+Enter to run a query.

Time range
Select the time range for the data available to the query. In KQL mode, if you set a different time range in your query, the time range you set in the time picker is overridden.

Show
Configure the number of entries Log Analytics retrieves in simple mode. The default limit is 1000. For more information on query limits, see Configure query results limit.

Simple/KQL mode
Switch between Simple and KQL mode.

### Left sidebar

The collapsible left pane gives you access to tables, example and saved queries, functions, and query history.

Pin the left pane to keep it open while you work, or maximize your query window by selecting an icon from the left pane only when you need it.

Option
Description

Tables
Lists the tables that are part of the selected scope. Hover over a table name to view the table's description and a link to its documentation. Expand a table to view its columns. Select a table to run a preview on it.

Queries
Lists example and saved queries. This is the same list that's in the Queries hub. Open the context menu [...] next to the search bar and select Group by to change the grouping of the queries. Hover over a query to view the query's description. Select a query to run it.

Functions
Lists functions, which allow you to reuse predefined query logic in your log queries.

Query history
Lists your query history. Select a query to rerun it.

Note

The Tables view doesn't show empty tables by default.

- To change that for the current session, open the context menu `...` next to the search bar, then select Show tables with no data.

- To show or hide empty tables permanently, open the context menu `...` above the top action bar, select Log Analytics settings, toggle Show tables with no data, and Save your changes.

#### Query history

Query history records the queries you run against a resource and makes them available to rerun later. The following sections describe where query history is stored, how long it's kept, and which scenarios it doesn't support.

##### Regional storage and resource scoping

Query history is resource-centric and region-scoped. Log Analytics stores history in the same region as the resource you query, which supports data-residency and compliance requirements. As a result, the history you see depends on both the resource and its region:

- Regional resources, such as Log Analytics workspaces, Application Insights resources, and virtual machines, store history in the resource's own region. Two resources in different regions don't share history.

- Global resources that have no region route to a fixed default region for the cloud. In the public Azure cloud, the default region is West Europe.

Scoping also depends on the resource type. Each Log Analytics workspace keeps its own independent history, so the history for Workspace A differs from the history for Workspace B. For some other resource types, resources of the same type within the same region share a common history.

##### Retention and limits

Tabs represent the query history of your current session. In simple mode, you are allowed one query per tab.

Behavior
Detail

Retention
History is kept for 30 days.

Per-user limit
Up to 300 queries per user, per resource.

Query text size
Each stored query can be up to 40 KB. Larger queries aren't saved to history.

##### Clear query history

Clearing query history applies to an entire scope, so clearing history removes every query for that scope at once. For resource types that share history, clearing history affects all resources of that type in the same region.

##### Unsupported scenarios

Query history isn't available in the following cases:

- Customer-managed storage: Query history isn't supported when the workspace uses a customer-managed storage account.

- Resource move operations: Query history is keyed to the original resource ID and isn't carried over when you move a workspace to a different resource group or subscription. The history stored before the move isn't accessible from the moved resource.

Query history stores the full text of each query. This text isn't written to telemetry and isn't accessible to Microsoft operators.

### Query window

Note

The query window is only available in KQL mode.

The query window is where you edit your query. IntelliSense is used for KQL commands and color coding enhances readability. Select + at the top of the window to open another tab.

A single window can include multiple queries. A query can't include any blank lines, so you can separate multiple queries in a window with one or more blank lines. The current query is the one with the cursor positioned anywhere in it.

To run the current query, select the Run button or select Shift+Enter.

### Results window

The results of a query appear in the results window. By default, the results are displayed as a table. To display the results as a chart, select Chart in the results window. You can also add a render command to your query.

#### Results view

The results view displays query results in a table organized by columns and rows.

- Click to the left of a row to expand its values.

- Select the Columns dropdown to change the list of columns.

- Sort the results by selecting a column name.

- Filter the results by selecting the funnel next to a column name.

- Clear the filters and reset the sorting by running the query again.

- Select Group columns to display the grouping bar above the query results.

- Group the results by any column by dragging it to the bar.

- Create nested groups in the results by adding more columns.

#### Chart view

The chart view displays the results as one of multiple available chart types. You can specify the chart type in a render command in your query (KQL mode). You can also select it from the collapsible Chart formatting section to the right.

Option
Description

Chart type
Type of chart to display.

X axis
Column in the results to use for the x-axis.

Y axis
Column in the results to use for the y-axis. Typically, this is a numeric column.

Split-by
Column in the results that defines the series in the chart. A series is created for each value in the column.

Aggregation
Type of aggregation to perform on the numeric values in the y-axis.

### More tools

This section describes more tools available above the query results area of the screen, as shown in the following screenshot. The screenshot is numbered 1-8.

#
Option
Description

1
Tab context menu
From the ellipsis of a query tab, change query scope or rename, duplicate, or close the tab.

2
Observability Agent
Chat with your data by using natural language to explore logs, find common errors, analyze anomalies, and surface insights without writing KQL.

3
Save
Save a query to a query pack or as a function, or pin your query to a workbook, an Azure dashboard, or Grafana dashboard.

4
Share
Copy a link to your query, the query text, or query results, or export data to Excel, CSV, or Power BI.

5
Tools context menu
From the ellipsis of the query area:

New alert rule - Create a new alert rule from the current query. 
Search job - Run a search job by using the current query. 
Log Analytics settings - Define default Log Analytics Settings, including time zone, whether Log Analytics opens in Simple or KQL mode, and whether to display tables with no data.

6
Queries hub
Open the example queries dialog that appears when you first open Log Analytics.

7
Autosave
Log Analytics autosave automatically saves your current session state to your browser's local storage. If the browser crashes, the page refreshes, or you navigate away and return, your work is restored when you reopen Logs for the same resource in the same browser.

8
Columns
Reorder, hide, or show columns in the results table. Activate Pivot mode to display the table by one or more columns.

#### Log Analytics settings

This screenshot shows the Log Analytics settings dialog.

#### Autosave

Log Analytics automatically saves your current session state to your browser's local storage. If the browser crashes, the page refreshes, or you navigate away and return, your work is restored when you reopen Logs for the same resource in the same browser.

Autosave preserves the following state:

- Tab names and all query tabs (KQL and Simple)

- Work mode (Simple or KQL)

- Query scope

- Time range

- Show pill settings

##### Autosave scope and retention

Scope - State is saved per browser and device and per specific resource.
Retention - Saved state is retained for 30 days. After 30 days of inactivity for a resource, the saved state is automatically deleted.

## Relationship to Azure Data Explorer

If you've worked with the Azure Data Explorer web UI, Log Analytics should look familiar. It's built on top of Azure Data Explorer and uses the same Kusto Query Language.

Log Analytics adds features specific to Azure Monitor, such as filtering by time range and the ability to create an alert rule from a query. Both tools include an explorer that lets you scan through the structure of available tables. The Azure Data Explorer web UI primarily works with tables in Azure Data Explorer databases. Log Analytics works with tables in a Log Analytics workspace.

## Related content

- Walk through a tutorial on using Log Analytics in the Azure portal.

- Walk through a tutorial on writing queries.

- View the longer tutorial video replaced by the Intro video.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-07-20
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
