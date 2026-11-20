# https://learn.microsoft.com/en-us/azure/azure-monitor/vm/vminsights-overview

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/vm/vminsights-overview

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
 

 

 

 

 
 
# Monitor virtual machines in Azure

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Monitor provides the tools to monitor the health, performance, and availability of Azure virtual machines and virtual machine scale sets. It combines host-level signals that Azure collects automatically with optional metrics and logs from the guest operating system. Together, this data helps you detect service issues, understand resource pressure, and troubleshoot the workloads running on each machine.

This article explains the monitoring capabilities for virtual machines in Azure Monitor, including host metrics, enhanced guest monitoring, log collection, and alerting. It also helps you understand which capabilities to use for different monitoring goals.

## Related resources

Resource type
Description

Hybrid machine
For virtual machines in other clouds and on-premises, use Azure Arc-enabled servers to connect them to Azure Monitor. After you install the Azure Connected Machine agent, you can monitor these machines by using the same methods as Azure VMs.

Virtual machine scale sets
Azure Virtual Machine Scale Sets (VMSS) support host metrics and guest performance data through Azure Monitor agent, similar to Azure VMs. VMSS doesn't support the new metrics experience. For setup guidance, see Tutorial: Enable monitoring for an Azure virtual machine scale set.

## View VM health

Open Monitor for any virtual machine in the Azure portal to see its current health. This view shows a summary of common metrics, although the available data depends on your monitoring configuration. Host metrics, including availability, are collected by default. Guest metrics and logs require the enhanced monitoring configuration described in Enable enhanced monitoring.

## Enable enhanced monitoring

Azure Monitor collects two types of metrics from virtual machines:

- Host metrics provide visibility into overall performance and load (CPU usage, network traffic, disk I/O). These are collected automatically at no cost.

- Guest metrics provide detailed insights into applications, components, and processes running inside the machine. For example, when troubleshooting performance issues, you might start with host metrics to identify which machines are under load, then use guest data to drill down into specific operating system and application behavior.

Enable enhanced monitoring to collect guest data and fully light up the Monitor view in the Azure portal. This process installs Azure Monitor agent on the virtual machine and starts collecting a default set of metrics.

When you enable guest monitoring in the Azure portal, choose between OpenTelemetry metrics (recommended for new deployments) and logs-based metrics (classic for existing implementations). Both provide guest monitoring, but they differ in how they store and process metrics. See Metrics experience for virtual machines in Azure Monitor for details on these options.

For step-by-step guidance on enabling enhanced monitoring, start with Tutorial: Enable enhanced monitoring for an Azure virtual machine.

## Enable at scale

Enable VM monitoring at scale by using Azure CLI, PowerShell, Azure Policy, ARM templates, Bicep, and other infrastructure as code (IaC) tools. For implementation guidance, see Enable VM monitoring in Azure Monitor.

Enable monitoring and other management features at scale for virtual machines by using Essential machine management.

## Collect logs

Azure Monitor collects several types of log data from your virtual machines that provide detailed information about events, operations, and system behavior.

### Activity logs

Activity logs record operations performed on a VM, such as when a VM is started or stopped, when configurations are changed, or when a VM is deleted. They're collected automatically for all Azure resources at no cost. View activity logs for a VM from its Activity log page in the Azure portal. This shows all operations for that specific VM. You can also view activity logs for all resources in a subscription from the Activity log page in the Azure Monitor menu. Send them to a Log Analytics workspace where you can query them with other log data. See Azure Monitor activity log for details on viewing and analyzing activity logs.

### Guest logs

Guest logs come from the operating system and applications running inside a VM. Unlike activity logs, you must configure guest logs before Azure Monitor can collect them, and ingestion and storage charges apply. Create data collection rules to define which logs to collect and where to send them. See Collect guest log data from virtual machines with Azure Monitor.

Common types of guest logs include:

- Windows Event Logs

- Syslog

- IIS Logs

- Custom text logs

- Custom JSON logs

- SNMP traps

- Windows Firewall logs

After Azure Monitor sends logs to a Log Analytics workspace, you can analyze them with Kusto Query Language (KQL). For example, you can query Windows Event Logs to identify common errors or security events, or analyze IIS logs to understand web traffic patterns. See Log Analytics overview for more information.

## Alerts

Alerts in Azure Monitor proactively notify you when specific conditions are found in your monitoring data. They allow you to identify and address issues in your system before your customers notice them. For example, you might create an alert to notify you when a VM is down, when its CPU usage exceeds a certain threshold, or when error events are discovered.

When you enable enhanced monitoring, Azure Monitor will create a baseline set of recommended alert rules for the VM based on your monitoring configuration. You can then customize thresholds, severity, and notifications from the Alerts experience.

### Additional alert rules

Beyond recommended alert rules, you can create custom alert rules based on any metric or log data collected from your VMs. Alert rules can notify you through email, SMS, or webhooks, and can trigger automated responses using Azure Automation runbooks or Azure Functions.

For guidance on creating custom alert rules for VMs, see:

- Create metric alerts in Azure Monitor

- Create log query alerts in Azure Monitor

### Azure Monitor Baseline Alerts (AMBA)

Azure Monitor Baseline Alerts (AMBA) provide a predefined alert baseline that you can customize for Azure Monitor agent data. You can use AMBA to monitor VM performance and health by enabling alert rules for metrics such as available memory or disk queue length.

## Performance Diagnostics

Performance Diagnostics is a troubleshooting tool that helps you identify and diagnose performance issues on your Azure VMs. Use Performance Diagnostics when you need to:

- Investigate ongoing performance issues such as high CPU, memory, or disk usage

- Collect comprehensive diagnostic data for Microsoft Support

- Run benchmark tests on VM disk performance

- Analyze Azure Files or SMB share performance

- Identify configuration issues or known problems affecting VM performance

See Use Performance Diagnostics in Azure Monitor to troubleshoot VM performance issues for details on using Performance Diagnostics.

## View Grafana dashboards

Dashboards with Grafana for Azure virtual machines are integrated into the VM monitoring experience in the Azure portal. You can use built-in dashboards for single-machine and at-scale views, and you can open dashboard links from relevant charts.

For details, see Use Azure Monitor dashboards with Grafana.

## Related content

- Tutorial: Enable monitoring for Azure virtual machine - Enable monitoring for a single VM.

- Tutorial: Enable monitoring for Azure virtual machine scale set - Enable monitoring for a scale set.

- Tutorial: Enable recommended alerts for Azure virtual machine scale set - Turn on recommended alert rules for a scale set.

- Enable monitoring for Azure virtual machine - Configure monitoring at scale.

- Migrate from logs-based to OpenTelemetry metrics - Move to the OpenTelemetry-based metrics experience.

- Best practices for monitoring virtual machines in Azure Monitor - Review architecture and operational recommendations.

- Collect guest log data from virtual machines with Azure Monitor - Configure custom performance counters, guest logs, and events.

- Analyze the health and status of your virtual machine with Azure Monitor - Use the VM insights Performance view to analyze health and performance data across machines.

- Monitor your Azure virtual machines with Azure Monitor - Complete the training module for VM monitoring.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-06-02
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
