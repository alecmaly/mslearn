# https://learn.microsoft.com/en-us/azure/azure-monitor/reference/queries/syslog

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/reference/queries/syslog

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
 

 

 

 

 
 
# Queries for the Syslog table

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 For information on using these queries in the Azure portal, see Log Analytics tutorial. For the REST API, see Query.

### Find Linux kernel events

Find events reported by Linux kernel process, regarding killed processes.

`// To create an alert for this query, click '+ New alert rule'
Syslog
| where ProcessName == "kernel" and SyslogMessage contains "Killed process"
`

### All Syslog

Last 100 Syslog.

`Syslog
| top 100 by TimeGenerated desc
`

### All Syslog with errors

Last 100 Syslog with erros.

`Syslog
| where SeverityLevel == "err" or SeverityLevel == "error"
| top 100 by TimeGenerated desc
`

### All Syslog by facility

All Syslog by facility.

`Syslog
| summarize count() by Facility
`

### All Syslog by process name

All Syslog by process name.

`Syslog
| summarize count() by ProcessName
`

### Users Added to Linux Group by Computer

Lists computers with users added to Linux group.

`Syslog
| where Facility == 'authpriv' and SyslogMessage has 'to group' and (SyslogMessage has 'add' or SyslogMessage has 'added')
| summarize by Computer
`

### New Linux Group Created by Computer

Lists computers with new Linux group created.

`Syslog
| where Facility == 'authpriv' and SyslogMessage has 'new group'
| summarize count() by Computer
`

### Failed Linux User Password Change

Lists computers wih failed Linux user password change.

`Syslog
| where Facility == 'authpriv' and ((SyslogMessage has 'passwd:chauthtok' and SyslogMessage has 'authentication failure') or SyslogMessage has 'password change failed')
| summarize count() by Computer
`

### Computers With Failed Ssh Logons

Lists computers with failed ssh logons.

`Syslog
| where (Facility == 'authpriv' and SyslogMessage has 'sshd:auth' and SyslogMessage has 'authentication failure') or (Facility == 'auth' and ((SyslogMessage has 'Failed' and SyslogMessage has 'invalid user' and SyslogMessage has 'ssh2') or SyslogMessage has 'error: PAM: Authentication failure'))
| summarize count() by Computer
`

### Computers With Failed Su Logons

Lists computers with failed su logons.

`Syslog
| where (Facility == 'authpriv' and SyslogMessage has 'su:auth' and SyslogMessage has 'authentication failure') or (Facility == 'auth' and SyslogMessage has 'FAILED SU')
| summarize count() by Computer
`

### Computers With Failed Sudo Logons

Lists computers with failed sudo logons.

`Syslog
| where (Facility == 'authpriv' and SyslogMessage has 'sudo:auth' and (SyslogMessage has 'authentication failure' or SyslogMessage has 'conversation failed')) or ((Facility == 'auth' or Facility == 'authpriv') and SyslogMessage has 'user NOT in sudoers')
| summarize count() by Computer
`

 
 

 
 

 

 
 
 
 
 
 
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
 2026-01-27
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
