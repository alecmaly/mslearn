# https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/azure-pim-resource-rbac

Source: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/azure-pim-resource-rbac

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
 

 

 

 

 
 
# View activity and audit history for Azure resource roles in Privileged Identity Management

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 
## Overview

Privileged Identity Management (PIM) in Microsoft Entra ID enables you to view activity, activations, and audit history for Azure resource roles within your organization. This includes subscriptions, resource groups, and even virtual machines. Any resource within the Microsoft Entra admin center that uses the Azure role-based access control functionality can take advantage of the security and lifecycle management capabilities in Privileged Identity Management. If you want to keep audit data for longer than the default retention period, you can use Azure Monitor to route it to an Azure storage account. For more information, see Archive Microsoft Entra logs to an Azure storage account.

Note

If your organization has outsourced management functions to a service provider who uses Azure Lighthouse, role assignments authorized by that service provider won't be shown here.

## View activity and activations

To see the actions a specific user took in various resources, view the Azure resource activity associated with their activation period.

- Sign in to the Microsoft Entra admin center as at least a Privileged Role Administrator.

- Browse to ID Governance > Privileged Identity Management > Azure resources.

- Select the resource you want to view activity and activations for.

- Select Roles or Members.

- Select a user.

You see a summary of the user's actions in Azure resources by date. It also shows the recent role activations over that same time period.

- Select a specific role activation to see details and corresponding Azure resource activity that occurred while that user was active.

## Export role assignments with children

You might have a compliance requirement where you must provide a complete list of role assignments to auditors. Privileged Identity Management enables you to query role assignments at a specific resource, which includes role assignments for all child resources. Previously, it was difficult for administrators to get a complete list of role assignments for a subscription and they had to export role assignments for each specific resource. Using Privileged Identity Management, you can query for all active and eligible role assignments in a subscription including role assignments for all resource groups and resources.

- Sign in to the Microsoft Entra admin center as at least a Privileged Role Administrator.

- Browse to ID Governance > Privileged Identity Management > Azure resources.

- Select the resource you want to export role assignments for, such as a subscription.

- Select Assignments.

- Select Export to open the Export membership pane.

- Select Export all members to export all role assignments in a CSV file.

## View resource audit history

Resource audit gives you a view of all role activity for a resource.

- Sign in to the Microsoft Entra admin center as at least a Privileged Role Administrator.

- Browse to ID Governance > Privileged Identity Management > Azure resources.

- Select the resource you want to view audit history for.

- Select Resource audit.

- Filter the history using a predefined date or custom range.

- For Audit type, select Activate (Assigned + Activated).

- Under Action, select (activity) for a user to see that user's activity detail in Azure resources.

## View my audit

My audit enables you to view your personal role activity.

- Sign in to the Microsoft Entra admin center as at least a Privileged Role Administrator.

- Browse to ID Governance > Privileged Identity Management > Azure resources.

- Select the resource you want to view audit history for.

- Select My audit.

- Filter the history using a predefined date or custom range.

Note

Access to audit history requires at least the Privileged Role Administrator role.

## Get reason, approver, and ticket number for approval events

- Sign in to the Microsoft Entra admin center as at least a Privileged Role Administrator.

- Browse to Entra ID > Monitoring & health > Audit logs.

- Use the Service filter to display only audit events for the Privileged Identity Management service. On the Audit logs page, you can:

- See the reason for an audit event in the Status reason column.

- See the approver in the Initiated by (actor) column for the "add member to role request approved" event.

- Select an audit log event to see the ticket number on the Activity tab of the Details pane.

- You can view the requester (person activating the role) on the Targets tab of the Details pane for an audit event. There are three target types for Azure resource roles:

- The role (Type = Role)

- The requester (Type = Other)

- The approver (Type = User)

Typically, the log event immediately above the approval event is an event for Add member to role completed where the Initiated by (actor) is the requester. In most cases, you won't need to find the requester in the approval request from an auditing perspective.

## View session activity (preview)

Use Session Analytics to view an identity's PIM role lifecycle and Azure Bastion connection activity for a selected Azure subscription or resource group. The view covers role activation, Bastion access to an Azure Virtual Machine, and role deactivation or expiration. It doesn't show Azure resource operations, such as creating a resource group, or commands run inside a virtual machine.

For graphical recordings, use Session Recordings. Recordings have separate setup and viewing requirements.

### Session Analytics prerequisites

Microsoft Entra ID Governance licensing is required for Session Analytics in preview. See Microsoft Entra ID Governance licensing fundamentals.

Configure diagnostic settings on each Azure Bastion host you want to monitor to send `BastionAuditLogs` to a Log Analytics workspace. Use a workspace in the same tenant. Only Azure Bastion audit logs need this routing for Session Analytics. You don't need to route additional PIM log sources to the workspace.

Complete Set up Azure Bastion audit-log collection with the setup roles, then verify Bastion log collection. Use the separate roles listed in View Session Analytics to view the results.

### Set up Azure Bastion audit-log collection

Configure the destination for each host before viewing its Bastion connection activity. If log collection is already configured, continue to Verify Bastion log collection.

For setup with an existing Log Analytics workspace, use these recommended roles:

Resource
Recommended role
Role assignment scope

Azure Bastion host
Monitoring Contributor
The Azure Bastion resource.

Existing Log Analytics workspace
Monitoring Contributor
The Log Analytics workspace.

These are sufficient built-in setup recommendations, not minimum permissions. Custom roles can grant narrower permissions. See Monitoring Contributor permissions and Log Analytics workspace permissions.

- Create or reuse a Log Analytics workspace in the same tenant. Follow Create a Log Analytics workspace for creation steps and permissions.

- For each Azure Bastion host you want to monitor, follow Diagnostic settings in Azure Monitor to configure a setting, for example, `SendToLogAnalytics`, that sends `BastionAuditLogs` to the workspace. For the log category and `MicrosoftAzureBastionAuditLogs` table, see Azure Bastion resource logs.

- Before viewing Bastion activity in PIM, verify the host's connection records in the destination workspace.

### Verify Bastion log collection

Use the Log Analytics Reader role on the destination Log Analytics workspace to check for Bastion connection records before viewing Bastion activity in PIM.

- Sign in to the Azure portal.

- After a user connects through a monitored Bastion host, check for that connection's records in the workspace's `MicrosoftAzureBastionAuditLogs` table. Use `_ResourceId` to identify the Bastion host, `TargetResourceId` to identify the virtual machine, and `SessionStartTime` to check the connection time. For column details, see MicrosoftAzureBastionAuditLogs.

If the expected record isn't present, verify the host's diagnostic settings, the destination workspace, and the time range you're checking before viewing Bastion activity in PIM.

After verifying log collection, continue to View Session Analytics.

### View Session Analytics

To view Session Analytics, you need both of the following:

- At least the Reports Reader role in Microsoft Entra ID.

- The Azure resource and Log Analytics workspace viewing roles.

If your directory role assignment is eligible, activate it before viewing Session Analytics. See Microsoft Entra activity-log prerequisites.

The following Azure resource and workspace viewing roles apply at the listed resource scopes. These are separate from the setup roles.

Resource
Role
Role assignment scope

Log Analytics workspace
Log Analytics Reader
The Log Analytics workspace.

Azure Bastion host
Reader
The Azure Bastion resource.

Azure Virtual Machine
Reader
The Azure Virtual Machine resource.

Network interface
Reader
The Azure Virtual Machine's network interface.

Virtual network
Reader
The relevant virtual network, including a peered virtual network where applicable.

- Sign in to the Azure portal.

- Open Privileged Identity Management, select Azure resources, and select the Azure subscription or resource group whose activity you want to view.

- Under Activity, select Session Analytics (Preview).

- Use Date range or search by identity, role, or scope to find the activity you want to view.

- View the identity, activated role, scope, scope type, and start and end times. Select Refresh to reload the results.

## View Azure Bastion session recordings (preview)

Use Session Recordings to find recording-enabled Azure Bastion hosts in the selected scope and open their graphical recordings.

### Session Recordings prerequisites

- Microsoft Entra ID Governance licensing is required for the PIM Session Recordings view in preview. See Microsoft Entra ID Governance licensing fundamentals.

- Azure Bastion must use the Premium SKU with session recording and storage configured. Follow Record Bastion sessions for setup and storage requirements.

- To view or list recordings in Azure Bastion, you need the Storage Blob Data Reader role. Follow the Bastion recording guide for the viewing requirements.

### Azure Bastion recording support

A recording-enabled Azure Bastion Premium host records RDP and SSH connections through that host. It records all connections through the host, not just connections initiated from My Access. The following table summarizes supported and unsupported connection combinations for graphical recording:

Protocol
Authentication
Client
Graphical recording

SSH
Microsoft Entra ID or other supported SSH authentication.
Azure portal (browser).
Supported.

RDP
Supported authentication other than Microsoft Entra ID.
Azure portal (browser).
Supported.

RDP
Microsoft Entra ID.
Azure portal (browser).
Not supported concurrently with Microsoft Entra ID RDP.

RDP or SSH
Any authentication method.
Native client.
Not supported.

Use this table when selecting a connection method for a recording requirement. For recording setup and considerations, see Record Bastion sessions. For Microsoft Entra connection requirements, see Configure Microsoft Entra ID authentication for Azure Bastion.

### Session Recordings (Preview)

After recording setup is complete, use the PIM view to locate the host and open its recordings.

- Sign in to the Azure portal.

- Open Privileged Identity Management and select Azure resources. Use the scope selector to select the subscription or resource group that contains the Azure Bastion host whose recordings you want to view.

- Under Activity, select Session Recordings (Preview).

- Select a Bastion host to open its recordings in the Bastion experience.

## Next steps

- View audit history for Microsoft Entra roles in Privileged Identity Management

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-17
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
