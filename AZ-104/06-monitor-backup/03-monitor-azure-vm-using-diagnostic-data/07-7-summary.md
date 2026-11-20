# Unit 7: 7-summary

Source: https://learn.microsoft.com/en-us/training/modules/monitor-azure-vm-using-diagnostic-data/7-summary

---

# Summary

 
 
 
 Completed
 
 
 

 

 
 
- 2 minutes

 
 

 

 
 Azure Monitor helps you collect, analyze, and alert on various types of host and client monitoring data from your Azure VMs.

- Azure Monitor provides a set of VM host logs and performance and usage metrics for all Azure VMs.

- You can enable recommended alert rules when you create VMs or afterwards to alert on important VM host metrics.

- Azure Monitor Metrics Explorer lets you graph and analyze metrics for Azure VMs and other resources.

- Logs-based VM insights monitoring uses Azure Monitor Agent and a predefined data collection rule (DCR) to collect guest performance data for Performance views and KQL analysis.

- You can create data collection rules to collect other metrics and logs from your VM client.

- You can use Log Analytics to query and analyze log data.

Now that you understand these tools, you're confident that Azure Monitor can effectively monitor your Azure VMs and help you keep your website running effectively.

## Clean up resources

Delete the resources created solely for this exercise to avoid ongoing charges.

Warning

Don't delete an existing or shared workspace, identity, action group, DCR, or resource group. Remove only this exercise's associations or dedicated resources when others still depend on shared resources.

- Open learn-monitor-vm-rg and review its resources. Confirm that it contains only resources created for this lab. If it contains existing or shared resources, retain the group and remove only this exercise's dedicated resources or associations.

- Only if the resource group is dedicated to this lab, select Delete resource group, enter the group name, and confirm deletion. Use normal deletion; force deletion isn't required for an ordinary successful cleanup.

- Review the names and actual resource groups recorded during onboarding. If this lab created DCRs, workspaces, alert rules, action groups, identities, or other resources outside the deleted group, remove only those that are dedicated to this lab and no longer needed.

- If you deleted only the VM instead of its dedicated resource group, review retained disks, public IP addresses, network interfaces, and monitoring resources separately. Their deletion isn't guaranteed by deleting the VM.

- Confirm that the intended lab resources have been removed.

## Learn more

To learn more about monitoring your VMs with Azure Monitor, see the following resources:

- Azure Monitor documentation

- Monitor virtual machines with Azure Monitor

- Supported metrics with Azure Monitor

- Send Azure Monitor Activity log data

- Supported metrics for Microsoft.Compute/virtualMachines

- Overview of VM insights

- Create interactive reports with VM insights workbooks

- Compare guest metrics monitoring experiences

- Application Insights Application map (requires application instrumentation with Application Insights; VM insights performance collection alone doesn't provide application dependency telemetry)

- Azure Monitor Agent overview

- Collect log data from virtual machines

- Tutorial: Collect guest logs from an Azure virtual machine

 

 
 

 

 
 
 
 <section
