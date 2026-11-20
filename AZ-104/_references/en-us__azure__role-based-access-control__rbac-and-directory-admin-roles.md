# https://learn.microsoft.com/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles

Source: https://learn.microsoft.com/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles

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
 

 

 

 

 
 
# Azure roles, Microsoft Entra roles, and classic subscription administrator roles

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 If you're new to Azure, you may find it a little challenging to understand all the different roles in Azure. This article helps explain the following roles and when you would use each:

- Azure roles

- Microsoft Entra roles

- Classic subscription administrator roles

## How the roles are related

To better understand roles in Azure, it helps to know some of the history. When Azure was initially released, access to resources was managed with just three administrator roles: Account Administrator, Service Administrator, and Co-Administrator. Later, Azure role-based access control (Azure RBAC) was added. Azure RBAC is a newer authorization system that provides fine-grained access management to Azure resources. Azure RBAC includes many built-in roles, can be assigned at different scopes, and allows you to create your own custom roles. To manage resources in Microsoft Entra ID, such as users, groups, and domains, there are several Microsoft Entra roles.

The following diagram is a high-level view of how the Azure roles, Microsoft Entra roles, and classic subscription administrator roles are related.

## Azure roles

Azure RBAC is an authorization system built on Azure Resource Manager that provides fine-grained access management to Azure resources, such as compute and storage. Azure RBAC includes over 100 built-in roles. There are five fundamental Azure roles. The first three apply to all resource types:

Azure role
Permissions
Notes

Owner

- Grants full access to manage all resources

- Assign roles in Azure RBAC

The Service Administrator and Co-Administrators are assigned the Owner role at the subscription scope
Applies to all resource types.

Contributor

- Grants full access to manage all resources

- Can't assign roles in Azure RBAC

- Can't manage assignments in Azure Blueprints or share image galleries

Applies to all resource types.

Reader

- View Azure resources

Applies to all resource types.

Role Based Access Control Administrator

- Manage user access to Azure resources

- Assign roles in Azure RBAC

- Assign themselves or others the Owner role

- Can't manage access using other ways, such as Azure Policy

User Access Administrator

- Manage user access to Azure resources

- Assign roles in Azure RBAC

- Assign themselves or others the Owner role

The rest of the built-in roles allow management of specific Azure resources. For example, the Virtual Machine Contributor role allows the user to create and manage virtual machines. For a list of all the built-in roles, see Azure built-in roles.

Only the Azure portal and the Azure Resource Manager APIs support Azure RBAC. Users, groups, and applications that are assigned Azure roles can't use the Azure classic deployment model APIs.

In the Azure portal, role assignments using Azure RBAC appear on the Access control (IAM) page. This page can be found throughout the portal, such as management groups, subscriptions, resource groups, and various resources.

When you click the Roles tab, you'll see the list of built-in and custom roles.

For more information, see Assign Azure roles using the Azure portal.

## Microsoft Entra roles

Microsoft Entra roles are used to manage Microsoft Entra resources in a directory such as create or edit users, assign administrative roles to others, reset user passwords, manage user licenses, and manage domains. The following table describes a few of the more important Microsoft Entra roles.

Microsoft Entra role
Permissions
Notes

Global Administrator

- Manage access to all administrative features in Microsoft Entra ID, as well as services that federate to Microsoft Entra ID

- Assign administrator roles to others

- Reset the password for any user and all other administrators

The person who signs up for the Microsoft Entra tenant becomes a Global Administrator.

User Administrator

- Create and manage all aspects of users and groups

- Manage support tickets

- Monitor service health

- Change passwords for users, Helpdesk administrators, and other User Administrators

Billing Administrator

- Make purchases

- Manage subscriptions

- Manage support tickets

- Monitors service health

In the Azure portal, you can see the list of Microsoft Entra roles on the Roles and administrators page. For a list of all the Microsoft Entra roles, see Administrator role permissions in Microsoft Entra ID.

## Differences between Azure roles and Microsoft Entra roles

At a high level, Azure roles control permissions to manage Azure resources, while Microsoft Entra roles control permissions to manage Microsoft Entra resources. The following table compares some of the differences.

Azure roles
Microsoft Entra roles

Manage access to Azure resources
Manage access to Microsoft Entra resources

Supports custom roles
Supports custom roles

Scope can be specified at multiple levels (management group, subscription, resource group, resource)
Scope can be specified at the tenant level (organization-wide), administrative unit, or on an individual object (for example, a specific application)

Role information can be accessed in Azure portal, Azure CLI, Azure PowerShell, Azure Resource Manager templates, REST API
Role information can be accessed in the Azure portal, Microsoft Entra admin center, Microsoft 365 admin center, Microsoft Graph, Microsoft Graph PowerShell

### Do Azure roles and Microsoft Entra roles overlap?

By default, Azure roles and Microsoft Entra roles don't span Azure and Microsoft Entra ID. However, if a Global Administrator elevates their access by choosing the Access management for Azure resources switch in the Azure portal, the Global Administrator will be granted the User Access Administrator role (an Azure role) on all subscriptions for a particular tenant. The User Access Administrator role enables the user to grant other users access to Azure resources. This switch can be helpful to regain access to a subscription. For more information, see Elevate access to manage all Azure subscriptions and management groups.

Several Microsoft Entra roles span Microsoft Entra ID and Microsoft 365, such as the Global Administrator and User Administrator roles. For example, if you're a member of the Global Administrator role, you have global administrator capabilities in Microsoft Entra ID and Microsoft 365, such as making changes to Microsoft Exchange and Microsoft SharePoint. However, by default, the Global Administrator doesn't have access to Azure resources.

## Classic subscription administrator roles

Important

As of August 31, 2024, Azure classic administrator roles (along with Azure classic resources and Azure Service Manager) are retired and no longer supported. Starting in December 2025, Azure automatically assigned the Owner role at subscription scope to users in the public cloud who were still assigned the Co-Administrator or Service Administrator role. As of May 2026, classic administrator roles are fully retired and you must assign roles in Azure role-based access control (RBAC) to manage access.

For more information, see Azure classic subscription administrators.

Account Administrator, Service Administrator, and Co-Administrator are the three classic subscription administrator roles in Azure. Classic subscription administrators had full access to the Azure subscription. They could manage resources using the Azure portal, Azure Resource Manager APIs, and the classic deployment model APIs. The account that is used to sign up for Azure is automatically set as both the Account Administrator and Service Administrator. Then, additional Co-Administrators could be added. The Service Administrator and the Co-Administrators had the equivalent access of users who have been assigned the Owner role (an Azure role) at the subscription scope. The following table describes the differences between these three classic subscription administrative roles.

Classic subscription administrator
Limit
Permissions
Notes

Account Administrator
1 per Azure account

- Can access the Azure portal and manage billing

- Manage billing for all subscriptions in the account

- Create new subscriptions

- Cancel subscriptions

- Change the billing for a subscription

- Change the Service Administrator

- Can't cancel subscriptions unless they have the Service Administrator or subscription Owner role

Conceptually, the billing owner of the subscription.

Service Administrator
1 per Azure subscription

- Manage services in the Azure portal

- Cancel the subscription

- Assign users to the Co-Administrator role

By default, for a new subscription, the Account Administrator is also the Service Administrator.
The Service Administrator has the equivalent access of a user who is assigned the Owner role at the subscription scope.
The Service Administrator has full access to the Azure portal.

Co-Administrator
200 per subscription

- Same access privileges as the Service Administrator, but canât change the association of subscriptions to Microsoft Entra directories

- Assign users to the Co-Administrator role, but can't change the Service Administrator

The Co-Administrator has the equivalent access of a user who is assigned the Owner role at the subscription scope.

For more information, see Azure classic subscription administrators.

### Azure account and Azure subscriptions

An Azure account is used to establish a billing relationship. An Azure account is a user identity, one or more Azure subscriptions, and an associated set of Azure resources. The person who creates the account is the Account Administrator for all subscriptions created in that account. That person is also the default Service Administrator for the subscription.

Azure subscriptions help you organize access to Azure resources. They also help you control how resource usage is reported, billed, and paid for. Each subscription can have a different billing and payment setup, so you can have different subscriptions and different plans by office, department, project, and so on. Most services belong to a subscription, and the subscription ID may be required for programmatic operations.

Each subscription is associated with a Microsoft Entra directory. To find the directory the subscription is associated with, open Subscriptions in the Azure portal and then select a subscription to see the directory.

Accounts and subscriptions are managed in the Azure portal.

## Next steps

- Assign Azure roles using the Azure portal

- Assign Microsoft Entra roles to users

- Roles for Microsoft 365 services in Microsoft Entra ID

 
 

 
 

 

 
 
 
 
 
 
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
 2026-05-06
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
