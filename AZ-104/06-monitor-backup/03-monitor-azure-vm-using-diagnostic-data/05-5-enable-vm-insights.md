# Unit 5: 5-enable-vm-insights

Source: https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/5-enable-vm-insights

---

unit-inner-section" class="section is-uniform position-relative">
 
# Collect client performance counters by using VM insights

 
 
 
 Completed
 
 
 

 

 
 
- 5 minutes

 
 

 

 
 Host metrics describe the Azure resources allocated to your VM. To inspect performance inside the guest operating system, enable Azure Monitor Agent (AMA) and a performance data collection rule (DCR).

This exercise uses logs-based VM insights monitoring. Its predefined performance data is stored in the `InsightsMetrics` table in the Log Analytics workspace you prepared. You analyze it with VM insights Performance views and Kusto Query Language (KQL).

Note

Azure Monitor also offers generally available OpenTelemetry metrics-based monitoring, the recommended metrics experience for new VM deployments. It stores guest metrics in an Azure Monitor workspace and uses PromQL. That workspace isn't a Log Analytics workspace, and those metrics don't automatically populate `InsightsMetrics`. This exercise selects logs-based collection so you can analyze performance and Syslog with KQL. See Compare monitoring experiences.

## Enable logs-based performance monitoring

- Open monitored-linux-vm in the Azure portal and select Monitor from its menu.

- Select Configure to open Configure monitor.

- Select the logs-based collection option and clear OpenTelemetry metrics for this exercise.

- Select Customize infrastructure monitoring. Select the Log Analytics workspace created earlier rather than accepting an unspecified default workspace.

- Allow the portal to create the performance DCR. If you select an existing DCR instead, confirm that it's configured for logs-based VM insights performance collection, sends data to the intended workspace, and doesn't enable process/dependency mapping.

- Leave process/dependency mapping disabled. Don't install Dependency Agent.

- Recommended host alerts were configured in the preceding VM exercise. Clear Enable recommended alerts in this onboarding operation to avoid creating an additional set.

- Review the configuration. Confirm logs-based collection, the intended Log Analytics workspace, and the selected VM. Record the DCR name and its actual resource group for cleanup.

- Select Review + Enable, then Enable.

Note

AMA requires a managed identity. The portal enables a system-assigned managed identity when needed. The identity and DCR association are part of monitoring setup; installing an extension alone doesn't define the data to collect. For more information, see Enable enhanced VM monitoring.

Allow several minutes for installation, configuration, and initial data delivery. On the VM, open Settings > Extensions + applications and confirm that AzureMonitorLinuxAgent reports successful provisioning.

## View and confirm performance data

- In the VM menu, expand Monitoring, select Insights, and open Performance.

- Select a time range that includes the period after onboarding. Inspect the CPU, memory, and logical-disk performance views.

- Open Logs from the VM menu. Confirm the query scope is this VM.

- If Logs opens in Simple mode, switch to KQL mode. Close the example-query dialog if necessary.

- Run the following query:

`InsightsMetrics
| where TimeGenerated > ago(30m)
| where Origin == "vm.azm.ms"
| summarize Samples = count() by Namespace, Name
| order by Namespace asc, Name asc
`

The results should list recently collected performance measurements for this VM. The Performance charts and recent `InsightsMetrics` records are the success criteria; a VM Overview widget or an agent heartbeat alone isn't proof of performance collection.

For example, chart guest CPU utilization:

`InsightsMetrics
| where TimeGenerated > ago(30m)
| where Origin == "vm.azm.ms"
| where Namespace == "Processor" and Name == "UtilizationPercentage"
| summarize AverageCpu = avg(Val) by bin(TimeGenerated, 5m), Computer
| render timechart
`

These queries assume the VM resource scope. If you open Logs from a workspace instead, constrain the query to the VM's full resource ID with an `_ResourceId` filter.

If no performance records appear, check the extension, managed identity, DCR association, destination workspace, and required outbound connectivity. Initial charts need time to accumulate samples. See Troubleshoot AMA on Linux.

Important

Keep the predefined VM insights performance DCR intact. In the next unit, create an additional DCR for Linux Syslog. The performance DCR doesn't collect Syslog automatically.

For more examples, see InsightsMetrics queries and VM insights Performance views.

## Application dependency monitoring

For a website instrumented with Application Insights, Application map can visualize application components and recorded dependencies. This requires an application, supported instrumentation, and generated request/dependency telemetry. This lab creates a VM, not an instrumented website, so an application map isn't an expected output.

Application-level mapping isn't a replacement for arbitrary host-process and port discovery. AMA guest performance collection alone doesn't create either kind of map.

 

 
 
 
 
 
 1.
 What does enabling logs-based VM insights monitoring in this exercise provide?

 
 

 
 
 
 
 
 Prebuilt Performance views and guest performance records in a Log Analytics workspace.

 

 
 
 
 

 
 
 

 
 
 
 
 Graphs that show several host metrics on one graph with customizable timeframes.

 

 
 
 
 

 
 
 

 
 
 
 
 Automatic Linux Syslog collection.

 

 
 
 
 

 
 
 

 

 

 

 
 
 
 2.
 With authentication and connectivity prerequisites met, what starts guest data collection with Azure Monitor Agent in this exercise?

 
 

 
 
 
 
 
 Enable only boot diagnostics.

 

 
 
 
 

 
 
 

 
 
 
 
 Create a Log Analytics workspace without configuring the VM.

 

 
 
 
 

 
 
 

 
 
 
 
 Install Azure Monitor Agent and associate a DCR that defines the data and destination.

 

 
 
 
 

 
 
 

 

 

 

 

 

 You must answer all questions before checking your work.

 

 

 
 

 

 

 You must answer all questions before checking your work.

 

 
 

 

 
 
 
 <section
