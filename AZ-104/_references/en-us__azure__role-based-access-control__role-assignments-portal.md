# https://learn.microsoft.com/en-us/azure/role-based-access-control/role-assignments-portal

Source: https://learn.microsoft.com/en-us/azure/role-based-access-control/role-assignments-portal

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
 

 

 

 

 
 
# Assign Azure roles using the Azure portal

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure role-based access control (Azure RBAC) is the authorization system you use to manage access to Azure resources. To grant access, you assign roles to users, groups, service principals, or managed identities at a particular scope. This article describes how to assign roles using the Azure portal.

If you need to assign administrator roles in Microsoft Entra ID, see Assign Microsoft Entra roles to users.

## Prerequisites

To assign Azure roles, you must have:

- `Microsoft.Authorization/roleAssignments/write` permissions, such as Role Based Access Control Administrator or User Access Administrator

## Step 1: Identify the needed scope

When you assign roles, you must specify a scope. A Scope is the set of resources the access applies to. In Azure, you can specify a scope at four levels from broad to narrow: management group, subscription, resource group, and resource. For more information, see Understand scope.

- Sign in to the Azure portal.

- In the Search box at the top, search for the scope you want to grant access to. For example, search for Management groups, Subscriptions, Resource groups, or a specific resource.

- Click the specific resource for that scope.

The following shows an example resource group.

## Step 2: Open the Add role assignment page

Access control (IAM) is the page that you typically use to assign roles to grant access to Azure resources. It's also known as identity and access management (IAM) and appears in several locations in the Azure portal.

- Click Access control (IAM).

The following shows an example of the Access control (IAM) page for a resource group.

- Click the Role assignments tab to view the role assignments at this scope.

- Click Add > Add role assignment.

If you don't have permissions to assign roles, the Add role assignment option will be disabled.

 Add role assignment menu." data-linktype="relative-path">

The Add role assignment page opens.

## Step 3: Select the appropriate role

To select a role, follow these steps:

- On the Role tab, select the tab for the type of role you want to assign.

- Job function roles â Roles for general Azure resource management or roles for specific services.

- Privileged administrator roles â Roles that grant privileged access, such as Owner, Contributor, User Access Administrator, or Role Based Access Control Administrator. For best practices when using privileged administrator role assignments, see Best practices for Azure RBAC.

- Select a role from the list by clicking on it.

Use the Search box to filter the list of roles by name or description. You can also filter roles by Type and Category to narrow down the results.

- In the Details column, click View to get more details about a role.

Tip

If you're unsure which role to assign, you can use Copilot to help you select the appropriate role. On the Role tab, click Copilot can help pick role to open the Copilot dialog box.

In the dialog box, describe what you need the user to be authorized to do. For example, "Help me select a role to deploy and manage Azure functions" or "Which role should I use if I want a user to manage and view a workspace?"

Copilot suggests one or more roles based on your requirements. Click Select permissions to confirm, and then Select role to apply the recommendation, or click Recommend other roles to see alternatives.

- Click Next.

## Step 4: Select who needs access

To select who needs access, follow these steps:

- On the Members tab, select User, group, or service principal to assign the selected role to one or more Microsoft Entra users, groups, or service principals (applications).

- Click Select members.

- Find and select the users, groups, or service principals.

You can type in the Select box to search the directory for display name or email address.

- Click Select to add the users, groups, or service principals to the Members list.

- To assign the selected role to one or more managed identities, select Managed identity.

- Click Select members.

- In the Select managed identities pane, select whether the type is user-assigned managed identity or system-assigned managed identity.

- Find and select the managed identities.

For system-assigned managed identities, you can select managed identities by Azure service instance.

- Click Select to add the managed identities to the Members list.

- In the Description box enter an optional description for this role assignment.

Later you can show this description in the role assignments list.

- Click Next.

## Step 5: (Optional) Add condition

If you selected a role that supports conditions, a Conditions tab will appear and you have the option to add a condition to your role assignment. A condition is an additional check that you can optionally add to your role assignment to provide more fine-grained access control.

The Conditions tab will look different depending on the role you selected.

### Delegate condition

If you selected one of the following privileged roles, follow the steps in this section.

- Owner

- Role Based Access Control Administrator

- User Access Administrator

- On the Conditions tab under What user can do, select the Allow user to only assign selected roles to selected principals (fewer privileges) option.

- Click Select roles and principals to add a condition that constrains the roles and principals this user can assign roles to.

- Follow the steps in Delegate Azure role assignment management to others with conditions.

### Storage condition

If you selected one of the following storage roles, follow the steps in this section.

- Storage Blob Data Contributor

- Storage Blob Data Owner

- Storage Blob Data Reader

- Storage Queue Data Contributor

- Storage Queue Data Message Processor

- Storage Queue Data Message Sender

- Storage Queue Data Reader

- Click Add condition if you want to further refine the role assignments based on storage attributes.

- Follow the steps in Add or edit Azure role assignment conditions.

## Step 6: Select assignment type

If you have a Microsoft Entra ID P2 or Microsoft Entra ID Governance license, an Assignment type tab will appear for management group, subscription, and resource group scopes. Use eligible assignments to provide just-in-time access to a role. Users with eligible and/or time-bound assignments must have a valid license.

If you don't want to use the PIM functionality, select the Active assignment type and Permanent assignment duration options. These settings create a role assignment where the principal always has permissions in the role.

This capability is being deployed in stages, so it might not be available yet in your tenant or your interface might look different. For more information, see Eligible and time-bound role assignments in Azure RBAC.

- On the Assignment type tab, select the Assignment type.

- Eligible - User must perform one or more actions to use the role, such as perform a multifactor authentication check, provide a business justification, or request approval from designated approvers. You can't create eligible role assignments for applications, service principals, or managed identities because they can't perform the activation steps.

- Active - User doesn't have to perform any action to use the role.

- Depending on your settings, for Assignment duration, select Permanent or Time bound.

Select permanent if you want member to always be allowed to activate or use role. Select time bound to specify start and end dates. This option might be disabled if permanent assignments creation is not allowed by PIM policy.

- If Time bound is selected, set Start date and time and Start date and time to specify when user is allowed to activate or use role.

It's possible to set the start date in the future. The maximum allowed eligible duration depends on your Privileged Identity Management (PIM) policy.

- (Optional) Use Configure PIM Policy to configure expiration options, role activation requirements (approval, multifactor authentication, or Conditional Access authentication context), and other settings.

When you select the Update PIM policy link, a PIM page is displayed. Select Settings to configure PIM policy for roles. For more information, see Configure Azure resource role settings in Privileged Identity Management.

- Click Next.

## Step 7: Assign role

- On the Review + assign tab, review the role assignment settings.

- Click Review + assign to assign the role.

After a few moments, the security principal is assigned the role at the selected scope.

- If you don't see the description for the role assignment, click Edit columns to add the Description column.

## Edit assignment

If you have a Microsoft Entra ID P2 or Microsoft Entra ID Governance license, you can edit your role assignment type settings. For more information, see Eligible and time-bound role assignments in Azure RBAC.

- On the Access control (IAM) page, click the Role assignments tab to view the role assignments at this scope.

- Find the role assignment that you want to edit.

- In the State column, click the link, such as Eligible time-bound or Active permanent.

The Edit assignment pane appears where you can update the role assignment type settings. The pane might take a few moments to open.

- When finished, click Save.

Your updates might take a while to be processed and reflected in the portal.

## Related content

- Assign a user as an administrator of an Azure subscription

- Remove Azure role assignments

- Troubleshoot Azure RBAC

 
 

 
 

 

 
 
 
 
 
 
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
 2026-03-17
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
