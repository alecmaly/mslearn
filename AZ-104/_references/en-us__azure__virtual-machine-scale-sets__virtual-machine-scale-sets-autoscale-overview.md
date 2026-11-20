# https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview

Source: https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview

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
 

 

 

 

 
 
# Overview of autoscale with Azure Virtual Machine Scale Sets

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 An Azure Virtual Machine Scale Set can increase or decrease the number of virtual machines that run your application. Instance count can be updated in several ways:

- Manually increasing or decreasing scale set capacity

- Based on a set schedule

- According to rules based on metrics thresholds

- Automatically based on usage patterns discovered by predictive artificial intelligence

This automated and elastic behavior reduces the management overhead to monitor and optimize the performance of your application. This article provides an overview of which performance metrics are available and what actions autoscale can perform.

Note

Use of autoscaling requires that the scale set is defined with a virtual machine scaling profile that defines the configuration of instances to add. Learn more about Virtual Machine Scaling Profile.

## Manual scaling

You can manually increase or decrease the number of instances in the virtual machine scale set by updating the `sku.capacity` property.

- 
Azure portal

- 
Azure CLI

- 
Azure PowerShell

- Navigate to an existing Virtual machine scale set.

- Under Settings, select the Scaling tab.

- Choose Manual Scale, if it isn't already selected.

- Update the Instance count.

- Press the Save button.

`az vmss scale \
 --new-capacity 5 \
 --name scaleSetName \
 --resource-group resourceGroupName
`

`Update-AzVmss `
 -SkuCapacity 5 `
 -ResourceGroupName resourceGroupName ` 
 -VMScaleSetName scaleSetName `
`

## Benefits of autoscale

If your application demand increases, the load on the virtual machines in your scale set increases. If this increased load is consistent, rather than just a brief demand, you can configure autoscale rules to increase and decrease the number of virtual machines in the scale set.

Note

When using automatic instance repairs for your scale set, the maximum number of instances in the scale set can be 1,000. Learn more about Automatic Instance Repairs.

When these virtual machines are created and your applications are deployed, the scale set starts to distribute traffic to them through the load balancer. You control what metrics to monitor, such as CPU or memory, how long the application load must meet a given threshold, and how many virtual machines to add to the scale set.

On an evening or weekend, your application demand may decrease. If this decreased load is consistent over a period of time, you can configure autoscale rules to decrease the number of virtual machines in the scale set. This scale-in action reduces the cost to run your scale set as you only run the number of instances required to meet the current demand.

## Use host-based metrics

You can create autoscale rules that built-in host metrics available from your virtual machines. Host metrics give you visibility into the performance of the virtual machines in a scale set without the need to install or configure more agents and data collections. Autoscale rules that use these metrics can scale out or in the number of virtual machines in response to CPU usage, memory demand, or disk access.

Autoscale rules that use host-based metrics can be created with one of the following tools:

- Azure portal

- Azure PowerShell

- Azure CLI

- Azure template

To create autoscale rules that use more detailed performance metrics, you can install and configure the Azure diagnostics extension on virtual machines, or configure your application use App Insights.

Autoscale rules that use host-based metrics, in-guest virtual machine metrics with the Azure diagnostic extension, and App Insights can use the following configuration settings.

### Metric sources

Autoscale rules can use metrics from one of the following sources:

Metric source
Use case

Current scale set
For host-based metrics that don't require more agents to be installed or configured.

Storage account
The Azure diagnostic extension writes performance metrics to Azure storage that is then consumed to trigger autoscale rules.

Service Bus Queue
Your application or other components can transmit messages on an Azure Service Bus queue to trigger rules.

Application Insights
An instrumentation package installed in your application that streams metrics directly from the app.

### Autoscale rule criteria

The following host-based metrics are available for use when you create autoscale rules. If you use the Azure diagnostic extension or App Insights, you define which metrics to monitor and use with autoscale rules.

Metric name

Percentage CPU

Network In

Network Out

Disk Read Bytes

Disk Write Bytes

Disk Read Operations/Sec

Disk Write Operations/Sec

CPU Credits Remaining

CPU Credits Consumed

When you create autoscale rules to monitor a given metric, the rules look at one of the following metrics aggregation actions:

- Average

- Minimum

- Maximum

- Total

- Last

- Count

The autoscale rules are then triggered when the metrics are compared against your defined threshold with one of the following operators:

- Greater than

- Greater than or equal to

- Less than

- Less than or equal to

- Equal to

- Not equal to

### Actions when rules trigger

When an autoscale rule triggers, your scale set can automatically scale in one of the following ways:

Scale operation
Use case

Increase count by
A fixed number of virtual machines to create. Useful in scale sets with a smaller number of virtual machines.

Increase percent by
A percentage-based increase of virtual machines. Good for larger scale sets where a fixed increase may not noticeably improve performance.

Increase count to
Create as many virtual machines are required to reach a desired maximum amount.

Decrease count by
A fixed number of virtual machines to remove. Useful in scale sets with a smaller number of virtual machines.

Decrease percent by
A percentage-based decrease of virtual machines. Good for larger scale sets where a fixed decrease may not noticeably reduce resource consumption and costs.

Decrease count to
Remove as many virtual machines are required to reach a desired minimum amount.

## In-guest virtual machine metrics with the Azure diagnostics extension

The Azure diagnostics extension is an agent that runs inside a virtual machine. The agent monitors and saves performance metrics to Azure storage. These performance metrics contain more detailed information about the status of the virtual machine, such as AverageReadTime for disks or PercentIdleTime for CPU. You can create autoscale rules based on a more detailed awareness of the virtual machine performance, not just the percentage of CPU usage or memory consumption.

To use the Azure diagnostics extension, you must create Azure storage accounts for your virtual machines, install the Azure diagnostics agent, then configure the virtual machines to stream specific performance counters to the storage account.

For more information, see the articles for how to enable the Azure diagnostics extension on a Linux virtual machine or Windows virtual machine.

## Application-level metrics with App Insights

To gain more visibility in to the performance of your applications, you can use Application Insights. You install a small instrumentation package in your application that monitors the app and sends telemetry to Azure. You can monitor metrics such as the response times of your application, the page load performance, and the session counts. These application metrics can be used to create autoscale rules at a granular and embedded level as you trigger rules based on actionable insights that may impact the customer experience.

For more information about App Insights, see What is Application Insights.

## Scheduled autoscale

You can also create autoscale rules based on schedules. These schedule-based rules allow you to automatically scale the number of virtual machines at fixed times. With performance-based rules, there may be a performance impact on the application before the autoscale rules trigger and the new virtual machines are provisioned. If you can anticipate such demand, the extra virtual machines are provisioned and ready for the increased customer use and application demand.

The following examples are scenarios that may benefit the use of schedule-based autoscale rules:

- Automatically scale out the number of virtual machines at the start of the work day when customer demand increases. At the end of the work day, automatically scale in the number of virtual machines to minimize resource costs overnight when application use is low.

- For departments with applications that experience heavy usage during specific times of the month or fiscal cycle, automatically scale the number of virtual machines to handle the increased demand seamlessly.

- When there's a marketing event, promotion, or holiday sale, you can automatically scale the number of virtual machines ahead of anticipated customer demand.

## Limitations

- You can have up to 20 Autoscale rules for a given scale set.

## Next steps

You can create autoscale rules that use host-based metrics with one of the following tools:

- Azure PowerShell

- Azure CLI

- Azure template

For information on how to manage your virtual machines, see Manage Virtual Machine Scale Sets with Azure PowerShell.

To learn how to generate alerts when your autoscale rules trigger, see Use autoscale actions to send email and webhook alert notifications in Azure Monitor. You can also Use audit logs to send email and webhook alert notifications in Azure Monitor.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-05-19
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
