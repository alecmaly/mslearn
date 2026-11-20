# https://learn.microsoft.com/en-us/azure/azure-monitor/vm/data-collection-syslog

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/vm/data-collection-syslog

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
 

 

 

 

 
 
# Collect Syslog events from virtual machine client with Azure Monitor

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Syslog is an event logging protocol that's common to Linux. Use the Syslog daemon built into Linux devices and appliances to collect local events of the types you specify. Applications send messages that are either stored on the local machine or delivered to a Syslog collector. Collect Syslog events from virtual machines by using a data collection rule (DCR) with a Linux Syslog data source.

Tip

To collect data from devices that don't allow local installation of Azure Monitor agent, configure a dedicated Linux-based log forwarder as described in Forward Syslog data to a Log Analytics workspace with Microsoft Sentinel by using Azure Monitor Agent.

Details for the creation of the DCR are provided in Collect data from VM client with Azure Monitor. This article provides other details for the Linux Syslog data source type.

Note

To work with the DCR definition directly or to deploy with other methods such as ARM templates, see Data collection rule (DCR) samples in Azure Monitor.

## Create the DCR

Create the DCR using the process in Collect data from virtual machine client with Azure Monitor.

## Configure Syslog data source

On the Collect and deliver tab of the DCR, select Linux Syslog from the Data source type dropdown.

Select a Minimum log level for each facility or NONE to collect no events for that facility. You can configure multiple facilities at once by selecting their checkbox and then selecting a log level in Set minimum log level for selected facilities. Checkboxes are cleared each time you open an existing DCR, so they don't show which facilities are currently collected.

All logs with the selected severity level and higher are collected for the facility. The supported severity levels and their relative severity are as follows:

- Debug

- Info

- Notice

- Warning

- Error

- Critical

- Alert

- Emergency

## Add destinations

Syslog data can only be sent to a Log Analytics workspace where it's stored in the Syslog table. Add a destination of type Azure Monitor Logs and select a Log Analytics workspace. While you can add multiple workspaces, be aware that this will send duplicate data to each which will result in additional cost.

## Verify data collection

To verify that data is being collected, check for records in the Syslog table. From the virtual machine or from the Log Analytics workspace in the Azure portal, select Logs and then click the Tables button. Under the Virtual machines category, click Run next to Syslog.

Note

To confirm which facilities a DCR collects, check the `facilityNames` property in the DCR definition rather than the portal form. See View DCR definition.

Note

When ingesting syslog data using a log forwarder, inconsistencies may arise between the TimeGenerated and EventTime fields.

- TimeGenerated reflects the UTC time when the syslog message was processed by the machine hosting the log forwarder or collector.

- EventTime is extracted from the syslog header, which doesn't include time zone information and is converted to UTC using the local time zone offset of the forwarder/collector.

This can lead to differences between the two fields when the forwarder/collector and the device generating the log are in different time zones.

## Configure Syslog on the Linux agent

When Azure Monitor Agent is installed on a Linux machine, it installs a default Syslog configuration file that defines the facility and severity of the messages that are collected if Syslog is enabled in a DCR. The configuration file is different depending on the Syslog daemon that the client has installed.

Note

Azure Monitor Linux Agent versions 1.15.2 and higher support syslog RFC formats including Cisco Meraki, Cisco ASA, Cisco FTD, Sophos XG, Juniper Networks, Corelight Zeek, CipherTrust, NXLog, McAfee, and Common Event Format (CEF).

### Rsyslog

On many Linux distributions, the rsyslogd daemon is responsible for consuming, storing, and routing log messages sent by using the Linux Syslog API. Azure Monitor Agent uses the TCP forward output module (`omfwd`) in rsyslog to forward log messages.

The Azure Monitor Agent installation includes default config files located in `/etc/opt/microsoft/azuremonitoragent/syslog/rsyslogconf/`. When you add Syslog to a DCR, Azure Monitor Agent installs this configuration under the `etc/rsyslog.d` system directory and automatically restarts `rsyslog` for the changes to take effect.

Note

On rsyslog-based systems, Azure Monitor Linux Agent adds forwarding rules to the default ruleset defined in the rsyslog configuration. If multiple rulesets are used, inputs bound to nondefault rulesets are not forwarded to Azure Monitor Agent. For more information about multiple rulesets in rsyslog, see the official documentation.

The following default configuration collects Syslog messages sent from the local agent for all facilities with all log levels.

`$ cat /etc/rsyslog.d/10-azuremonitoragent-omfwd.conf
# Azure Monitor Agent configuration: forward logs to azuremonitoragent

template(name="AMA_RSYSLOG_TraditionalForwardFormat" type="string" string="<%PRI%>%TIMESTAMP% %HOSTNAME% %syslogtag%%msg:::sp-if-no-1st-sp%%msg%")
# queue.workerThreads sets the maximum worker threads, it will scale back to 0 if there is no activity
# Forwarding all events through TCP port
*.* action(type="omfwd"
template="AMA_RSYSLOG_TraditionalForwardFormat"
queue.type="LinkedList"
queue.filename="omfwd-azuremonitoragent"
queue.maxFileSize="32m"
queue.maxDiskSpace="1g"
action.resumeRetryCount="-1"
action.resumeInterval="5"
action.reportSuspension="on"
action.reportSuspensionContinuation="on"
queue.size="25000"
queue.workerThreads="100"
queue.dequeueBatchSize="2048"
queue.saveonshutdown="on"
target="127.0.0.1" Port="28330" Protocol="tcp")
`

The following configuration is used when you use SELinux and decide to use Unix sockets.

`$ cat /etc/rsyslog.d/10-azuremonitoragent.conf
# Azure Monitor Agent configuration: forward logs to azuremonitoragent
$OMUxSockSocket /run/azuremonitoragent/default_syslog.socket
template(name="AMA_RSYSLOG_TraditionalForwardFormat" type="string" string="<%PRI%>%TIMESTAMP% %HOSTNAME% %syslogtag%%msg:::sp-if-no-1st-sp%%msg%")
$OMUxSockDefaultTemplate AMA_RSYSLOG_TraditionalForwardFormat
# Forwarding all events through Unix Domain Socket
*.* :omuxsock:
`

`$ cat /etc/rsyslog.d/05-azuremonitoragent-loadomuxsock.conf
# Azure Monitor Agent configuration: load rsyslog forwarding module.
$ModLoad omuxsock
`

On some legacy systems, you might see rsyslog log formatting issues when a traditional forwarding format is used to send Syslog events to Azure Monitor Agent. For these systems, Azure Monitor Agent automatically places a legacy forwarder template instead:

`template(name="AMA_RSYSLOG_TraditionalForwardFormat" type="string" string="%TIMESTAMP% %HOSTNAME% %syslogtag%%msg:::sp-if-no-1st-sp%%msg%\n")`

### Syslog-ng

The Azure Monitor Agent installation includes default config files located in `/etc/opt/microsoft/azuremonitoragent/syslog/syslog-ngconf/azuremonitoragent-tcp.conf`. When Syslog is added to a DCR, this configuration is installed under the `/etc/syslog-ng/conf.d/azuremonitoragent-tcp.conf` system directory and syslog-ng is automatically restarted for the changes to take effect.

The default contents are shown in the following example. This example collects Syslog messages sent from the local agent for all facilities and all severities.

`$ cat /etc/syslog-ng/conf.d/azuremonitoragent-tcp.conf
# Azure MDSD configuration: syslog forwarding config for mdsd agent
options {};

# during install time, we detect if s_src exist, if it does then we
# replace it by appropriate source name like in redhat 's_sys'
# Forwrding using tcp
destination d_azure_mdsd {
 network("127.0.0.1"
 port(28330)
 log-fifo-size(25000));
};

log {
 source(s_src); # will be automatically parsed from /etc/syslog-ng/syslog-ng.conf
 destination(d_azure_mdsd);
 flags(flow-control);
};
`

The following configuration is used when you use SELinux and decide to use Unix sockets.

`$ cat /etc/syslog-ng/conf.d/azuremonitoragent.conf
# Azure MDSD configuration: syslog forwarding config for mdsd agent options {};
# during install time, we detect if s_src exist, if it does then we
# replace it by appropriate source name like in redhat 's_sys'
# Forwrding using unix domain socket
destination d_azure_mdsd {
 unix-dgram("/run/azuremonitoragent/default_syslog.socket"
 flags(no_multi_line) );
};

log {
 source(s_src); # will be automatically parsed from /etc/syslog-ng/syslog-ng.conf
 destination(d_azure_mdsd);
};
`

Note

Azure Monitor supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is the default daemon. The default Syslog daemon on version 5 of Red Hat Enterprise Linux and Oracle Linux version (sysklog) isn't supported for Syslog event collection. To collect Syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.

If you edit the Syslog configuration, you must restart the Syslog daemon for the changes to take effect.

## Supported facilities

The following facilities are supported with the Syslog collector:

Pri index
Pri Name

0
Kern

1
user

2
mail

3
daemon

4
auth

5
syslog

6
lpr

7
news

8
uucp

9
cron

10
authpriv

11
ftp

12
ntp

13
audit

14
alert

15
clock

16
local0

17
local1

18
local2

19
local3

20
local4

21
local5

22
local6

23
local7

24
{no priority}

## Semicolons get removed from Syslog messages

The Azure Monitor Agent (AMA) forwards Syslog data as it receives it. It doesnât modify the message content. However, during ingestion into Azure Log Analytics, semicolon (;) characters in Syslog messages get removed.

If you need to preserve semicolons, consider modifying the Syslog message at the source before ingestion. For example, you might replace semicolons with a different character, such as a comma or pipe (|), or you might encode the message content before sending it to Azure Monitor.

## Next steps

- Learn more about Azure Monitor Agent.

- Learn more about data collection rules.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-09-02
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
