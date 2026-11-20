# https://learn.microsoft.com/en-us/azure/azure-monitor/agents/azure-monitor-agent-troubleshoot-linux-vm

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/agents/azure-monitor-agent-troubleshoot-linux-vm

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
 

 

 

 

 
 
# Troubleshooting guidance for the Azure Monitor agent on Linux virtual machines and scale sets

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 
## Overview for Azure Monitor agent

Before you read further, you must be familiar with Azure Monitor agent and Data Collection Rules.

### Terminology

Name
Acronym
Description

Azure Monitor Agent
AMA
The new Azure Monitor agent

Data Collection Rules
DCR
Rules to configure collection of data by the agent, i.e. what to collect, where to send to, and more

Azure Monitor Configuration Service
AMCS
Regional service hosted in Azure, which controls data collection for this agent and other parts of Azure Monitor. The agent calls into this service to fetch DCRs.

Logs endpoint
--
Endpoint for sending data to Log Analytics workspaces

Metrics endpoint
--
Endpoint for sending data to Azure Monitor Metrics databases.

Instance Metadata Service and Hybrid
IMDS and HIMDS
Services hosted in Azure which provide information about currently running virtual machines, scale sets (via IMDS) and Arc-enabled servers (via HIMDS) respectively

Log Analytics workspace
LAW
The destination in Azure Monitor that you can send logs collected by the agent to

Custom Metrics
--
The destination in Azure Monitor that you can send guest metrics collected by the agent to

## Basic troubleshooting steps

Use the following steps to troubleshoot the latest version of the Azure Monitor agent running on your Linux virtual machine:

- Carefully review the prerequisites here.

- Verify that the extension was successfully installed and provisioned, which installs the agent binaries on your machine:

- Open Azure portal > select your virtual machine > Open Settings : Extensions + applications from the pane on the left > 'AzureMonitorLinuxAgent'should show up with Status: 'Provisioning succeeded'

- If you don't see the extension listed, check if machine can reach Azure and find the extension to install using the following command:

`az vm extension image list-versions --location <machine-region> --name AzureMonitorLinuxAgent --publisher Microsoft.Azure.Monitor
`

- Wait for 10-15 minutes as extension maybe in transitioning status. If it still doesn't show up as described previously, uninstall and install the extension again.

- Check if you see any errors in extension logs located at `/var/log/azure/Microsoft.Azure.Monitor.AzureMonitorLinuxAgent/` on your machine

- Verify that the agent is running:

- Check if the agent is emitting heartbeat logs to Log Analytics workspace using the following query. Skip if 'Custom Metrics' is the only destination in the data collection rule (DCR):

`Heartbeat | where Category == "Azure Monitor Agent" and Computer == "<computer-name>" | take 10
`

- Check if the agent service is running

`systemctl status azuremonitoragent
`

- Check if you see any errors in core agent logs located at `/var/opt/microsoft/azuremonitoragent/log/mdsd.*` on your machine

- Verify that the DCR exists and is associated with the virtual machine:

- If using Log Analytics workspace as destination, verify that DCR exists in the same physical region as the Log Analytics workspace.

- Open Azure portal > select your data collection rule > Open Configuration : Resources from the pane on the left > You should see the virtual machine listed here.

- If not listed, select Add and select your virtual machine from the resource picker. Repeat across all DCRs.

- Verify that agent was able to download the associated DCR(s) from AMCS service:

- Check if you see the latest DCR downloaded at this location `/etc/opt/microsoft/azuremonitoragent/config-cache/configchunks/`

- If the directory or files are missing:

- The Azure Monitor Agent was unable to download the Data Collection Rule (DCR) from the Azure Monitor Configuration Service (AMCS).

- This usually indicates one of the following:

- The virtual machine isnât associated with any DCR.

- The virtual machine canât reach AMCS due to network or DNS restrictions.

- The Azure Monitor Agent service isnât running or failed during startup.

- Take these actions:

- Confirm the DCR is associated with the VM:

- Azure portal â Data collection rules â Select your DCR â Resources

- Ensure the virtual machine appears in the list.

- Check outbound connectivity from the VM:

`curl -v https://global.handler.control.monitor.azure.com
`

- A successful TLS connection confirms the VM can reach AMCS.

- Restart the agent:

`sudo systemctl restart azuremonitoragent
sudo systemctl status azuremonitoragent
`

- Check agent error logs:

`sudo tail -f /var/opt/microsoft/azuremonitoragent/log/mdsd.err
`

- What a valid configuration file looks like:

- Each file under `/etc/opt/microsoft/azuremonitoragent/config-cache/configchunks/`represents a parsed Data Collection Rule downloaded from Azure.

- Example:

`ls /etc/opt/microsoft/azuremonitoragent/config-cache/configchunks/
`

- Output:

`dcr_1a2b3c4d.json
dcr_5e6f7g8h.json
`

- Inspect a file:

`cat /etc/opt/microsoft/azuremonitoragent/config-cache/configchunks/dcr_1a2b3c4d.json
`

- Typical contents include:

`{
"dataSources": {
"syslog": [
{
"facilityNames": ["daemon"],
"logLevels": ["Info", "Warning", "Error"]
}
]
},
"destinations": {
"logAnalytics": [
{
"workspaceResourceId": "/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.OperationalInsights/workspaces/<workspace-name>"
}
]
}
}
`

If these files are empty, missing, or malformed, the agent wonât collect or upload data.

## Issues collecting Syslog

For more information on how to troubleshoot syslog issues with Azure Monitor Agent, see here.

- The quality of service (QoS) file `/var/opt/microsoft/azuremonitoragent/log/mdsd.qos` provides CSV-format 15-minute aggregations of the processed events and contains the information on the amount of the processed syslog events in the given timeframe. This file is useful in tracking Syslog event ingestion drops.

The following example shows that in the 15 minutes preceding `2022-02-28T19:55:23.5432920Z`, the agent received 77 syslog events with facility daemon and level info and sent 77 of said events to the upload task. Additionally, the agent upload task received 77 and successfully uploaded all 77 of these daemon.info messages.

`#Time: 2022-02-28T19:55:23.5432920Z
#Fields: Operation,Object,TotalCount,SuccessCount,Retries,AverageDuration,AverageSize,AverageDelay,TotalSize,TotalRowsRead,TotalRowsSent
...
MaRunTaskLocal,daemon.debug,15,15,0,60000,0,0,0,0,0
MaRunTaskLocal,daemon.info,15,15,0,60000,46.2,0,693,77,77
MaRunTaskLocal,daemon.notice,15,15,0,60000,0,0,0,0,0
MaRunTaskLocal,daemon.warning,15,15,0,60000,0,0,0,0,0
MaRunTaskLocal,daemon.error,15,15,0,60000,0,0,0,0,0
MaRunTaskLocal,daemon.critical,15,15,0,60000,0,0,0,0,0
MaRunTaskLocal,daemon.alert,15,15,0,60000,0,0,0,0,0
MaRunTaskLocal,daemon.emergency,15,15,0,60000,0,0,0,0,0
...
MaODSRequest,https://e73fd5e3-ea2b-4637-8da0-5c8144b670c8_LogManagement,15,15,0,455067,476.467,0,7147,77,77
`

Troubleshooting steps

- Review the generic Linux AMA troubleshooting steps first. If agent is emitting heartbeats, proceed to step 2.

- The parsed configuration is stored at `/etc/opt/microsoft/azuremonitoragent/config-cache/configchunks/`. Check that Syslog collection is defined and the log destinations are the same as constructed in DCR UI / DCR JSON.

- If yes, proceed to step 3. If not, the issue is in the configuration workflow.

- Investigate `mdsd.err`,`mdsd.warn`, `mdsd.info` files under `/var/opt/microsoft/azuremonitoragent/log` for possible configuration errors.

- Validate the layout of the Syslog collection workflow to ensure all necessary pieces are in place and accessible:

- For `rsyslog` users, ensure the `/etc/rsyslog.d/10-azuremonitoragent.conf` file is present, isn't empty, and is accessible by the `rsyslog` daemon (syslog user).

- Check your rsyslog configuration at `/etc/rsyslog.conf` and `/etc/rsyslog.d/*` to see if you have any inputs bound to a nondefault ruleset, as messages from these inputs don't get forwarded to Azure Monitor Agent. For instance, messages from an input configured with a nondefault ruleset like `input(type="imtcp" port="514" ``ruleset="myruleset"``)` aren't forwarded.

- For `syslog-ng` users, ensure the `/etc/syslog-ng/conf.d/azuremonitoragent.conf` file is present, isn't empty, and is accessible by the `syslog-ng` daemon (syslog user).

- Ensure the file `/run/azuremonitoragent/default_syslog.socket` exists and is accessible by `rsyslog` or `syslog-ng` respectively.

- Check that syslog daemon queue isn't overflowing, causing the upload to fail, by referring the guidance here: Rsyslog data not uploaded due to Full Disk space issue on AMA Linux Agent

- To debug syslog events ingestion further, you can append trace flag `-T 0x2002` at the end of MDSD_OPTIONS in the file `/etc/default/azuremonitoragent`, and restart the agent:

`export MDSD_OPTIONS="-A -c /etc/opt/microsoft/azuremonitoragent/mdsd.xml -d -r $MDSD_ROLE_PREFIX -S $MDSD_SPOOL_DIRECTORY/eh -L $MDSD_SPOOL_DIRECTORY/events -e $MDSD_LOG_DIR/mdsd.err -w $MDSD_LOG_DIR/mdsd.warn -o $MDSD_LOG_DIR/mdsd.info -T 0x2002"
`

- After the issue is reproduced with the trace flag on, you'll find more debug information in `/var/opt/microsoft/azuremonitoragent/log/mdsd.info`. Inspect the file for the possible cause of syslog collection issue, such as parsing / processing / configuration / upload errors.

Warning

Ensure to remove trace flag setting `-T 0x2002` after the debugging session, since it generates many trace statements that could fill up the disk more quickly or make visually parsing the log file difficult.

## Troubleshooting issues on Arc-enabled server

If after checking basic troubleshooting steps you don't see the Azure Monitor Agent emitting logs or find 'Failed to get MSI token from IMDS endpoint' errors in `/var/opt/microsoft/azuremonitoragent/log/mdsd.err` log file, it's likely `syslog` user isn't a member of the group `himds`. Add `syslog` user to `himds` user group if the user isn't a member of this group. Create user `syslog` and the group `syslog`, if necessary, and make sure that the user is in that group. For more information, check out Azure Arc-enabled server authentication requirements here.

For a full list of Linux user accounts that the Azure Monitor Agent and Azure Arc create, see Linux user accounts created during installation.

## Issues with automatic upgrades on Virtual Machine Scale Sets

When you enable automatic extension upgrade for `AzureMonitorLinuxAgent` on a Virtual Machine Scale Set, the flag first updates the scale set model. If your scale set's upgrade policy is set to Manual, this change doesn't propagate to existing instances until you apply the model update.

You can apply the latest model in the Azure portal or programmatically.

- 
Portal

- 
Azure CLI

- 
PowerShell

- Go to the Azure portal.

- Open your Virtual Machine Scale Set.

- Go to Instances.

- Select the instances to upgrade.

- In the top menu bar, select Upgrade > Apply latest model.

Run the following command and replace `<resource-group>` and `<vmss>` with the names of your resource group and virtual machine scale set:

`az vmss update-instances -g <resource-group> -n <vmss> --instance-ids "*"
`

Run the following command and replace `<resource-group>` and `<vmss>` with the names of your resource group and virtual machine scale set:

`Update-AzVmssInstance -ResourceGroupName <resource-group> -VMScaleSetName <vmss> -InstanceId "*"
`

This forces the current scale set model (including the updated `enableAutomaticUpgrade` flag) onto the selected instances.

Tip

You can change upgrade policy to Rolling so future model changes flow automatically. Run the following CLI command and replace `<resource-group>` and `<vmss>` with the names of your resource group and virtual machine scale set:

`az vmss update -g <resource-group> -n <vmss> --set upgradePolicy.mode=Rolling
`

If specific virtual machines still don't update, check Instance protection (protect from scale set actions) and clear it if set.

## Next steps

- Use the Azure Monitor Agent Troubleshooter for Linux

 
 

 
 

 

 
 
 
 
 
 
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
 2026-04-10
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
