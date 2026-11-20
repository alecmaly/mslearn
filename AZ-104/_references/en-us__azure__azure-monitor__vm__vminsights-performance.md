# https://learn.microsoft.com/en-us/azure/azure-monitor/vm/vminsights-performance

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/vm/vminsights-performance

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
 

 

 

 

 
 
# Analyze the health and status of your virtual machine with Azure Monitor

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 VM insights includes a set of performance charts that target several key performance indicators to help you determine how well a virtual machine is performing. The charts show resource utilization over a period of time. Use them to identify bottlenecks and anomalies. You can also switch to a perspective that lists each machine to view resource utilization based on the metric selected.

Note

This article describes the logs-based experience for monitoring virtual machines in Azure Monitor. This experience isn't available for machines configured only for the metrics-based experience using OpenTelemetry metrics. For more information, see Metrics experience for virtual machines in Azure Monitor.

VM insights monitors key operating system performance indicators related to processor, memory, network adapter, and disk utilization. Performance helps to:

- Expose issues that indicate a possible system component failure.

- Support tuning and optimization to achieve efficiency.

- Support capacity planning.

Note

The network chart on the Performance tab looks different from the network chart on the Azure VM overview page because the overview page displays charts based on the host's measurement of activity in the guest VM. The network chart on the Azure VM overview only displays network traffic that gets billed. Inter-virtual network traffic isn't included. The data and charts shown for VM insights are based on data from the guest VM. The network chart displays all TCP/IP traffic that's inbound and outbound to that VM, including inter-virtual network traffic.

## Limitations

Limitations in performance collection with VM insights:

- Available memory isn't available in all Linux versions, including Red Hat Enterprise Linux (RHEL) 6. It's available in Linux versions that use kernel version 3.14 or higher. It might be available in some kernel versions between 3.0 and 3.14.

- Metrics are only available for data disks on Linux virtual machines that use XFS filesystem or EXT filesystem family (EXT2, EXT3, EXT4).

- Collecting performance metrics from network shared drives isn't supported.

## Permissions required

You must have the Monitoring reader permissions on the virtual machines and on the VM Insights Data Collection Rule (DCR).

## Multi-VM perspective from Azure Monitor

From Azure Monitor, the Performance feature provides a view of all monitored VMs deployed across work groups in your subscriptions or in your environment.

To access from Azure Monitor:

- In the Azure portal, select Monitor.

- In the Solutions section, select Virtual Machines.

- Select the Performance tab.

On the Top N Charts tab, if you have more than one Log Analytics workspace, select the workspace enabled with the solution from the Workspace selector at the top of the page. The Group selector returns subscriptions, resource groups, computer groups, and virtual machine scale sets of computers related to the selected workspace that you can use to further filter results presented in the charts on this page and across the other pages. Your selection only applies to the Performance feature and doesn't carry over to Map.

By default, the charts show performance counters for the last hour. By using the TimeRange selector, you can query for historical time ranges of up to 30 days to show how performance looked in the past.

Five capacity utilization charts are shown on the page:

- CPU Utilization %: Shows the top five machines with the highest average processor utilization.

- Available Memory: Shows the top five machines with the lowest average amount of available memory.

- Logical Disk Space Used %: Shows the top five machines with the highest average disk space used percent across all disk volumes.

- Bytes Sent Rate: Shows the top five machines with the highest average of bytes sent.

- Bytes Receive Rate: Shows the top five machines with the highest average of bytes received.

Note

Each chart described above only shows the top 5 machines.

Selecting the pushpin icon in the upper-right corner of a chart pins it to the last Azure dashboard you viewed. From the dashboard, you can resize and reposition the chart. Selecting the chart from the dashboard redirects you to VM insights and loads the correct scope and view.

Select the icon to the left of the pushpin icon on a chart to open the Top N List view. This list view shows the resource utilization for a performance metric by individual VM. It also shows which machine is trending the highest.

When you select the virtual machine, the Properties pane opens on the right side. It shows properties like system information reported by the operating system and the properties of the Azure VM. Selecting an option under the Quick Links section redirects you to that feature directly from the selected VM.

You can switch to the Aggregated Charts tab to view the performance metrics filtered by average or percentiles measured.

The following capacity utilization charts are provided:

- CPU Utilization %: Defaults show the average and top 95th percentile.

- Available Memory: Defaults show the average, top 5th, and 10th percentile.

- Logical Disk Space Used %: Defaults show the average and 95th percentile.

- Bytes Sent Rate: Defaults show the average bytes sent.

- Bytes Receive Rate: Defaults show the average bytes received.

You can also change the granularity of the charts within the time range by selecting Avg, Min, Max, 50th, 90th, and 95th in the percentile selector.

To view the resource utilization by individual VM and see which machine is trending with highest utilization, select the Top N List tab. The Top N List page shows the top 20 machines sorted by the most utilized by 95th percentile for the metric CPU Utilization %. To see more machines, select Load More. The results expand to show the top 500 machines.

Note

The list can't show more than 500 machines at a time.

To filter the results on a specific virtual machine in the list, enter its computer name in the Search by name text box.

If you want to view utilization from a different performance metric, from the Metric dropdown list, select Available Memory, Logical Disk Space Used %, Network Received Byte/s, or Network Sent Byte/s. The list updates to show utilization scoped to that metric.

Selecting a virtual machine from the list opens the Properties pane on the right side of the page. From here, you can select Performance detail. The Virtual Machine Detail page opens and is scoped to that VM. The experience is similar to accessing VM Insights Performance directly from the Azure VM.

## View performance directly from an Azure VM

To access performance data directly from a virtual machine:

- In the Azure portal, open Virtual machines and select the VM that you want to run diagnostics on.

- In the left-hand navigation menu, expand the Monitoring section, and then select Insights.

- Switch to the Performance tab.

This page shows Performance insights and performance utilization charts. It also shows a table for each logical disk discovered with its capacity, utilization, and total average by each measure.

The following capacity utilization charts are provided:

Chart
Description

CPU Utilization %
Defaults show the average and top 95th percentile.

Available Memory
Defaults show the average, top 5th, and 10th percentile.

Logical Disk Space Used %
Defaults show the average and 95th percentile.

Logical Disk IOPS
Defaults show the average and 95th percentile.

Logical Disk MB/s
Defaults show the average and 95th percentile.

Max Logical Disk Used %
Defaults show the average and 95th percentile.

Bytes Sent Rate
Defaults show the average bytes sent.

Bytes Receive Rate
Defaults show the average bytes received.

Selecting the pushpin icon in the upper-right corner of a chart pins it to the last Azure dashboard you viewed. From the dashboard, you can resize and reposition the chart. Selecting the chart from the dashboard redirects you to VM insights and loads the performance detail view for the VM.

## Troubleshoot VM performance problems with Performance Diagnostics

Performance Diagnostics helps you troubleshoot performance problems on Windows or Linux virtual machines by quickly diagnosing issues and providing insights on problems it finds on your machines. It supports two modes: Continuous diagnostics and On-demand diagnostics. For details on each mode, see Performance diagnostics modes.

## View performance directly from an Azure virtual machine scale set

To access performance data directly from an Azure virtual machine scale set:

- In the Azure portal, select Virtual machine scale sets.

- From the list, select a VM.

- In the Monitoring section, select Insights to view the Performance tab.

This page loads the Azure Monitor performance view scoped to the selected scale set. This view enables you to see the top instances in the scale set across the set of monitored metrics. You can also view the aggregate performance across the scale set. You can see the trends for selected metrics across the individual instances in the scale set. Selecting an instance from the list view lets you load its map or move into a detailed performance view for that instance.

Selecting the pushpin icon in the upper-right corner of a chart pins it to the last Azure dashboard you viewed. From the dashboard, you can resize and reposition the chart. Selecting the chart from the dashboard redirects you to VM insights and loads the performance detail view for the VM.

Note

You can also access a detailed performance view for a specific instance from the Instances view for your scale set. Under the Settings section, go to Instances and select Insights.

## Next steps

- Learn how to use workbooks that are included with VM insights to further analyze performance and network metrics.

- To learn about discovered application dependencies, see View VM insights Map.

 
 

 
 

 

 
 
 
 
 
 
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
