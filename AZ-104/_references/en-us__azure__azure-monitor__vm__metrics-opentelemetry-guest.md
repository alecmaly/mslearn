# https://learn.microsoft.com/en-us/azure/azure-monitor/vm/metrics-opentelemetry-guest

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/vm/metrics-opentelemetry-guest

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
 

 

 

 

 
 
# Metrics experience for virtual machines in Azure Monitor

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 When you enable enhanced monitoring for Azure virtual machines or Arc-enabled servers in Azure Monitor, you choose between two experiences for collecting and visualizing performance data from the guest operating system: OpenTelemetry metrics-based monitoring (recommended for new deployments) and logs-based monitoring (classic). This article describes the differences between these experiences and provides guidance on which to select.

In the portal onboarding workflow, OpenTelemetry metrics are enabled by default. The same workflow can also include logs-based metrics, OpenTelemetry per-process metrics, recommended alerts, and dashboards with Grafana depending on your monitoring selections.

## Compare experiences

The following table compares the OpenTelemetry-based and logs-based monitoring experiences for Azure virtual machines in Azure Monitor.

Feature
Metrics-based
Logs-based (classic)

Data storage
Azure Monitor workspace
Log Analytics workspace

Applies to
Azure VMs
Arc-enabled servers
Azure VMs
Arc-enabled servers
VM Scale Sets

Data model
OpenTelemetry system metrics with consistent cross-platform naming
Platform-specific performance counters

Query language
PromQL (Prometheus Query Language)
KQL (Kusto Query Language)

Latency
Near real-time with low latency
Typically 1-3 minutes

Cost
Default metrics free
Standard Log Analytics ingestion and retention costs

Multi-VM views
At-scale default-metrics Grafana dashboard
Full VM insights multi-VM dashboards and workbooks

Correlation with logs
Requires separate queries
Single workspace for metrics and logs enables correlation in one query

## When to enable the logs-based experience

You should enable the metrics-based experience in all cases since collection of default metrics is free. Choose to also enable logs-based metrics if:

- You need to monitor VM Scale Sets.

- You need the broader VM insights multi-VM dashboards, workbooks, and trending views.

- You want to correlate metrics and logs in a single query.

- You already use queries, dashboards, or alerts based on the `InsightsMetrics` table.

## Benefits of OpenTelemetry

Cross-OS observability

The OpenTelemetry semantic convention for system metrics streamlines the cross-OS end-user experience by converging Windows and Linux performance counters into a consistent naming convention and metric data model. This makes it easier for you to manage all virtual machines with a single set of queries used for either Windows or Linux operating systems. The same configuration-as-code deployment methods and the same PromQL queries can be used for any hosting resource that adopts OpenTelemetry system metrics.

More performance counters

The OpenTelemetry Collector Host Metrics Receiver collects more performance counters than Azure Monitor currently makes available for logs-based collection. For example, you can monitor per-process CPU utilization, disk I/O, and memory usage.

Simpler metric model

In many scenarios, multiple performance counters map to a single OpenTelemetry (OTel) system metric with metric dimensions, also called resource attributes. This simplifies both collection and querying.

For example, OTel includes a `system.cpu.time` metric. You can filter on the `State` dimension for values such as user, system, and idle. With logs-based collection, you would need to collect and query the following performance counters.

- Windows: `\Processor Information(_Total)\% Processor Time`, `\Processor Information(_Total)\% Privileged Time`, `\Processor Information(_Total)\% User Time`

- Linux: `Cpu/usage_user`, `Cpu/usage_system`, `Cpu/usage_idle`, `Cpu/usage_active`, `Cpu/usage_nice`, `Cpu/usage_iowait`, `Cpu/usage_irq`

## Benefits of Azure Monitor workspaces

Metrics stored in Azure Monitor workspaces are cheaper and faster to query than the same data stored in Log Analytics workspaces because Azure Monitor workspaces are optimized for time-series retrieval. Using OTel metrics in an Azure Monitor workspace also avoids the multiple schemas used in logs-based collection. Default logs-based metrics are stored in the `InsightsMetrics` table, while additional enabled metrics are stored in the `Perf` table, which uses a different schema.

Enhanced monitoring with OpenTelemetry uses a subset of the available system metrics, which helps standardize dashboards, alerts, and PromQL queries across teams.

## Limitations of metrics-based collection

- Metrics-based collection is currently only available for individual VMs and Arc-enabled servers. Logs-based collection can also be used for VM Scale Sets.

- Metrics-based collection doesn't currently support private link.

- You can't perform a single query across data in a Log Analytics workspace and Azure Monitor workspace. With logs-based collection, logs and metrics for your VMs are stored together, allowing you to correlate between them in a single KQL query. With metrics-based collection, metrics are stored in an Azure Monitor workspace and logs are stored in a Log Analytics workspace, requiring separate queries for each.

- You can create custom workbooks and dashboards to view multi-VM OpenTelemetry metrics. The built-in multi-VM experience for metrics-based collection is limited to the at-scale Grafana dashboard for default OpenTelemetry metrics. For broader multi-VM analysis and trending views, use logs-based VM insights dashboards and workbooks.

Tip

Share your feedback on new performance counters or functionality you would like to see by posting to the Azure Monitor GitHub Community or via Portal feedback.

## Related content

- Tutorial: Enable enhanced monitoring for an Azure virtual machine - Enable monitoring for a single VM by using the Azure portal.

- Customize OpenTelemetry metrics for Azure virtual machines - Change the default OpenTelemetry metrics collected from guest operating systems.

- Collect performance counters from virtual machines with Azure Monitor - Configure additional performance counter collection by using data collection rules.

- Migrate from logs-based to OpenTelemetry metrics for Azure virtual machines - Decide when to retire the logs-based experience and move fully to metrics-based monitoring.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-08-03
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
