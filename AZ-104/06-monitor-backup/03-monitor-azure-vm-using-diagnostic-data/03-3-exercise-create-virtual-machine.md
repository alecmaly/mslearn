# Unit 3: 3-exercise-create-virtual-machine

Source: https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/3-exercise-create-virtual-machine

---

# Monitor VM host data

 
 
 
 Completed
 
 
 

 

 
 
- 6 minutes

 
 

 

 
 You want to monitor the VMs that host your website, so you decide to quickly create a VM in the Azure portal and evaluate its built-in monitoring capabilities. In this unit, you use the Azure portal to create a Linux VM with recommended alerts and boot diagnostics enabled. As soon as the VM starts up, Azure automatically begins collecting basic metrics and activity logs. You can then view built-in metrics graphs, activity logs, and boot diagnostics.

## Create a VM and enable recommended alerts

- Sign in to the Azure portal, and in the Search field, enter virtual machines.

- On the Virtual machines page, select Create, and then select Azure virtual machine.

- On the Basics tab of the Create a virtual machine page:

- In the Subscription field, select the correct subscription if not already selected.

- Under Resource group:

- Select Create new.

- Under Name, enter learn-monitor-vm-rg.

- Select OK.

- For Virtual machine name, enter monitored-linux-vm.

- For Image, select Ubuntu Server 24.04 LTS, x64, Gen2, published by Canonical. Use the full server image for this exercise.

- Leave the other settings at their current values, and select the Monitoring tab.

- On the Monitoring tab, select Enable recommended alert rules if the option is available.

- If the Set up recommended alert rules screen opens:

- Select all the listed alert rules if not already selected, and adjust the values if desired.

- Under Notify me by, select the checkbox next to Email, and enter an email address to receive alert notifications.

- Select Save.

- Under Diagnostics, for Boot diagnostics, ensure that Enable with managed storage account (recommended) is selected.

Note

Keep boot diagnostics enabled with managed storage. Boot diagnostics and host metrics don't require Azure Monitor Agent. Later in this module, you enable Azure Monitor Agent and associated data collection rules to collect guest performance data and Linux Syslog. Don't enable a separate OS guest diagnostics extension.

- Select Review + create at the bottom of the page, and when validation passes, select Create.

- On the Generate new key pair popup dialog box, select Download private key and create resource.

It can take a few minutes to create the VM. When you get the notification that the VM is created, select Go to resource to see basic metrics data.

If the creation screen didn't offer recommended alerts, open the VM's Alerts page and select View + set up. Configure the desired host alert rules and the email notification action group, then select Save. For details, see Enable recommended alert rules.

Record the alert rule and action group names and their resource groups. You use this information during cleanup and avoid creating another set of recommended alerts when you enable guest monitoring.

## Prepare the Log Analytics workspace

- In the Azure portal, search for Log Analytics workspaces and select Create.

- Select the same subscription and the dedicated learn-monitor-vm-rg resource group used for this exercise.

- Enter an available workspace name, such as learn-monitor-vm-law. Record the name you use.

- Select the VM's region. Using one region for this lab simplifies configuration; it isn't a universal requirement that a VM and its Log Analytics workspace share a region.

- Select Review + Create, then Create.

- Record the workspace name, region, and resource group. Explicitly select this workspace in both the performance-monitoring configuration and the Syslog DCR.

Important

Use a dedicated lab resource group. Record any resources the portal creates outside that group. Don't delete a shared workspace or action group during cleanup.

For more information, see Create a Log Analytics workspace and Azure Monitor Agent supported operating systems.

## View built-in metrics graphs

Once your VM is created, Azure starts collecting basic metrics data automatically. Built-in metrics graphs, along with the recommended alerts you enabled, can help you monitor whether and when your VM encounters health or performance issues. You can then use more advanced monitoring and analytics capabilities to investigate issue causes and remediation.

- To view basic metrics graphs, on the VMs Overview page, select the Monitoring tab.

- Under Performance and utilization > Platform metrics, review the following metrics graphs related to the VMs performance and utilization. Select Show more metrics if all the graphs don't appear immediately.

- VM Availability

- CPU (average)

- Disk bytes (total)

- Network (total)

- Disk operations/sec (average)

You haven't configured AMA guest performance collection yet. In the next units, you enable logs-based VM insights monitoring and use its Performance views and Log Analytics to analyze guest data.

## View the activity log

You can view the VMs activity log by selecting Activity log from the VMs left navigation menu. You can also retrieve entries by using PowerShell or the Azure CLI.

## View boot diagnostics

You enabled boot diagnostics when you created the VM. You can view boot diagnostics to view boot data and troubleshoot startup issues.

- In the left navigation menu for the VM, select Boot diagnostics under Help.

- On the Boot diagnostics page, select Screenshot to see a startup screenshot from the VMs hypervisor. Select Serial log to view log messages created when the VM started.

 

 
 
 
 
 
 1.
 What do you need to do to enable recommended alert rules when you create a VM?

 
 

 
 
 
 
 
 Nothing, they're enabled by default.

 

 
 
 
 

 
 
 

 
 
 
 
 Go to Alerts and select Create.

 

 
 
 
 

 
 
 

 
 
 
 
 Select Enable recommended alert rules on the Monitoring tab.

 

 
 
 
 

 
 
 

 

 

 

 
 
 
 2.
 Which metrics graph isn't available by default on the Monitoring tab when you create a VM?

 
 

 
 
 
 
 
 VM Availability

 

 
 
 
 

 
 
 

 
 
 
 
 Guest OS Available Memory

 

 
 
 
 

 
 
 

 
 
 
 
 Percentage CPU (average)

 

 
 
 
 

 
 
 

 

 

 

 

 

 You must answer all questions before checking your work.

 

 

 
 

 

 

 You must answer all questions before checking your work.

 

 
 

 

 
 
 
 <section
