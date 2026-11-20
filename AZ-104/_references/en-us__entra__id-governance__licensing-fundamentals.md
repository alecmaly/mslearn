# https://learn.microsoft.com/en-us/entra/id-governance/licensing-fundamentals

Source: https://learn.microsoft.com/en-us/entra/id-governance/licensing-fundamentals

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
 

 

 

 

 
 
# Microsoft Entra ID Governance licensing fundamentals

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This article discusses Microsoft Entra ID Governance licensing for employees. It's intended for IT decision makers, IT administrators, and IT professionals who are considering Microsoft Entra ID Governance services for their organizations.

For governance licensing for guest users, see Microsoft Entra ID Governance licensing for guest users. For agent identity licensing requirements, see Governing agent identities. For licensing that applies to Tenant Governance administrators and features, see Licensing for Microsoft Entra Tenant Governance.

## Types of licenses

The following licenses are available for use with Microsoft Entra ID Governance in the commercial and government clouds. The choice of licenses you need in a tenant depends on the features you're using in that tenant.

- Free - Included with Microsoft cloud subscriptions such as Microsoft Azure, Microsoft 365, and others.

- Microsoft Entra ID P1 - Microsoft Entra ID P1 is available as a standalone product or included with Microsoft 365 E3, E5 or E7 for enterprise customers and Microsoft 365 Business Premium for small to medium businesses.

- Microsoft Entra ID P2 - Microsoft Entra ID P2 is available as a standalone product or included with Microsoft 365 E5 or E7 for enterprise customers.

- Microsoft Entra ID Governance - Microsoft Entra ID Governance is an advanced set of identity governance capabilities available for Microsoft Entra ID P1 and P2 customers. Microsoft Entra ID Governance is available as six products Microsoft Entra ID Governance, Microsoft Entra ID Governance Step Up for Microsoft Entra ID P2, Entra ID Governance Frontline Worker, Microsoft Entra ID Governance Step up for Microsoft Entra ID F2, Microsoft Entra ID Governance for Government and Microsoft Entra ID Governance Add-on for Microsoft Entra ID P2 for Government. These six products differ only in their prerequisites; they contain both the entitlement management, privileged identity management and access reviews capabilities that were in Microsoft Entra ID P2, and additional advanced identity governance capabilities. The following section goes into more detail on the different prerequisites of these products.

- Microsoft Entra Suite - Microsoft Entra Suite is a complete cloud-based solution for workforce access, available for Microsoft Entra ID P1 and P2 customers. Microsoft Entra Suite brings together Microsoft Entra Private Access, Microsoft Entra Internet Access, Microsoft Entra ID Governance, Microsoft Entra ID Protection, and Microsoft Entra Verified ID. The Microsoft Entra ID Governance portion provides the same identity governance capabilities as the Microsoft Entra ID Governance product. The difference is that they have different prerequisites.

- Microsoft Agent 365 - Microsoft Agent 365 provides identity governance capabilities for agent identities, providing access governance for agents and service principals via Entra's Entitlement Management, additional automations via Lifecycle workflows as well as end user experiences for sponsors to manage agent identity and access lifecycle. The following section goes into more detail on the prerequisites and capabilities. For more information about Microsoft Agent 365, see: Microsoft Agent 365.

Note

Some Microsoft Entra ID Governance scenarios can be configured to depend upon other features that aren't covered by Microsoft Entra ID Governance. These features might have additional licensing requirements. For more information on governance scenarios using other features, see the Identity Governance overview page.

The Microsoft Entra ID Governance for Government and Microsoft Entra ID Governance Add-on for Microsoft Entra ID P2 for Government products are available in the US Government community cloud (GCC), GCC-High, and Department of Defense cloud environments.

### Governance products and prerequisites

The Microsoft Entra ID Governance capabilities for employees are currently available in six standalone products. These six products provide the same identity governance capabilities. The difference between the six products is that they have different prerequisites.

- A subscription to Microsoft Entra ID Governance or Microsoft Entra ID Governance for Government, listed in the product terms as the Microsoft Entra ID Governance (User SL) product, requires that the tenant also have an active subscription to another product, one that contains the `AAD_PREMIUM` or `AAD_PREMIUM_P2` service plan. Examples of products meeting this prerequisite include Microsoft Entra ID P1, Microsoft 365 E3/E5/A3/A5/G3/G5 or Enterprise Mobility + Security E3/E5.

- A subscription to Microsoft Entra ID Governance Step Up for Microsoft Entra ID P2 or Microsoft Entra ID Governance Add-on for Microsoft Entra ID P2 for Government, listed in the product terms as the Microsoft Entra ID Governance P2 product, requires that the tenant also have an active subscription to another product, one that contains the `AAD_PREMIUM_P2` service plan. Examples of products meeting this prerequisite include Microsoft Entra ID P2, Microsoft 365 E5/A5/G5, Enterprise Mobility + Security E5, Microsoft 365 E5/F5 Security or Microsoft 365 F5 Security + Compliance.

- A subscription to the Entra ID Governance Frontline Worker (User SL) product requires that the tenant also have an active subscription to another product, one that contains the `AAD_PREMIUM` or `AAD_PREMIUM_P2` service plan. Examples of products meeting this prerequisite include Microsoft Entra ID P1, Microsoft 365 E3/E5/A3/A5/G3/G5, Enterprise Mobility + Security E3/E5 or Microsoft 365 F1/F3.

- A subscription to Microsoft Entra ID Governance Step up for Microsoft Entra ID F2, listed in the product terms as the Microsoft Entra ID Governance F2 or Microsoft Entra ID Governance Step-Up for Microsoft Entra ID F2 for Frontline Worker (User SL) product, requires that the tenant also have an active subscription to another product, one that contains the `AAD_PREMIUM_P2` service plan. Examples of products meeting this prerequisite include Microsoft Entra ID F2.

- A subscription to Microsoft Agent 365 requires that the tenant also have an active subscription to another product, one that contains the `AAD_PREMIUM` service plan. Examples of products meeting this prerequisite include Microsoft Entra ID P1 or Microsoft 365 E3.

Microsoft Entra ID Governance capabilities are also included in the Microsoft Entra Suite and in Microsoft 365 E7. The available Microsoft Entra Suite products include Microsoft Entra Suite (User SL), Microsoft Entra Suite Add-on for Microsoft Entra ID F2 for FLW (User SL), Microsoft Entra Suite Add-on for Microsoft Entra ID P2 (User SL), Microsoft Entra Suite Add-on for Microsoft Entra ID P2 EDU (User SL), Microsoft Entra Suite FLW (User SL), and Microsoft Entra Suite for EDU (User SL).

The product names and service plan identifiers for licensing lists additional products that include the prerequisite service plans.

Note

A subscription to a prerequisite for a Microsoft Entra ID Governance product must be active in the tenant. If a prerequisite isn't present, or the subscription expires, then Microsoft Entra ID Governance scenarios might not function as expected.

To check if the prerequisite products for a Microsoft Entra ID Governance product are present in a tenant, you can use the Microsoft Entra admin center or the Microsoft 365 admin center to view the list of products.

- Sign into the Microsoft Entra admin center as a License Administrator.

- Browse to Billing > Licenses.

- In the Manage menu, select Licensed features. The information bar indicates the current Microsoft Entra ID license plan.

- To view the existing products in the tenant, in the Manage menu, select All products.

Governance of guest users requires an Azure subscription be selected for guest billing. For more information, see: Microsoft Entra ID Governance licensing for guest users.

## Starting a trial

A Global Administrator in a commercial tenant that has an appropriate prerequisite product, such as Microsoft Entra ID P1, already purchased, and isn't already using or has previously trialed Microsoft Entra ID Governance, can request a trial of Microsoft Entra ID Governance in their tenant.

- Sign in to the Microsoft 365 admin center as a Global Administrator

- In the Billing menu, select Purchase services.

- In the Search all product categories box, type `"Microsoft Entra ID Governance"`.

- Select Details below Microsoft Entra ID Governance to view the trial and purchase information for the product. If your tenant has Microsoft Entra ID P2, then select Details below Microsoft Entra ID Governance Step-Up for Microsoft Entra ID P2.

- In the product details page, select Start free trial.

## Microsoft Entra ID Governance features

The following table shows the licensing requirements for Microsoft Entra ID Governance features for member users. Microsoft Entra Suite includes all features of Microsoft Entra ID Governance. Microsoft 365 E7 also includes all ID Governance features through the Entra Suite and Agent 365. Licensing information for Entitlement management, Access reviews, and Lifecycle Workflows are provided following the table.

### Features by license

The following table shows what features associated with identity governance are available with each license. For more information on other features, see Microsoft Entra plans and pricing. Not all features are available in all clouds; see Microsoft Entra feature availability for Azure Government.

Feature
Free
Microsoft Entra ID P1
Microsoft Entra ID P2
Microsoft Entra ID Governance
Microsoft Entra Suite
Microsoft Agent 365
Microsoft 365 E7

Provisioning

API-driven provisioning

â
â
â
â

â

HR-driven provisioning

â
â
â
â

â

Account Discovery

â
â

â

Automated user provisioning to SaaS apps
â
â
â
â
â

â

Automated group provisioning to SaaS apps

â
â
â
â

â

Automated provisioning to on-premises apps

â
â
â
â

â

Cross-tenant synchronization for users (same cloud)

â
â
â
â

â

Cross-tenant synchronization for groups (same cloud)

â
â

â

Cross-cloud synchronization

â
â

â

Lifecycle Workflows (LCW)
Free
Microsoft Entra ID P1
Microsoft Entra ID P2
Microsoft Entra ID Governance
Microsoft Entra Suite
Microsoft Agent 365
Microsoft 365 E7

Lifecycle Workflows

â
â

â

LCW + Custom Extensions (Logic Apps)

â
â

â

LCW + Agent ID sponsorship tasks

â
â

Access reviews (AR)
Free
Microsoft Entra ID P1
Microsoft Entra ID P2
Microsoft Entra ID Governance
Microsoft Entra Suite
Microsoft Agent 365
Microsoft 365 E7

AR - Capabilities previously generally available in Microsoft Entra ID P2

â
â
â

â

AR - PIM For Groups (Preview)

â
â

â

AR - Reviews scoped to inactive users without active users in the review

â
â

â

AR - Reviews scoped to active and inactive users with review decision helpers for inactive users for the reviewer

â
â
â

â

AR - Machine learning assisted access certifications and reviews

â
â

â

AR - Catalog Access Reviews

â
â

â

AR - Custom data provided resource

â
â

â

Entitlement management (EM)
Free
Microsoft Entra ID P1
Microsoft Entra ID P2
Microsoft Entra ID Governance
Microsoft Entra Suite
Microsoft Agent 365
Microsoft 365 E7

EM - Capabilities previously generally available in Microsoft Entra ID P2

â
â
â

â

EM - Users assigned to access packages

â
â
â

â

EM - Agent IDs and service principals assigned to access packages

â
â

EM - Users request access for themselves

â
â
â

â

EM - Admins directly assign a user assignments(including guests)

â
â
â

â

EM - Admins directly assign agent IDs and service principals

â
â

EM - Admins directly assign any user - via email address for users not yet in your directory

â
â

â

EM - Managers requesting on behalf of employees

â
â

â

EM - Owners and sponsors request access on behalf of their agent IDs or service principals

â
â

EM - Supported resources
Free
Microsoft Entra ID P1
Microsoft Entra ID P2
Microsoft Entra ID Governance
Microsoft Entra Suite
Microsoft Agent 365
Microsoft 365 E7

EM - Groups and teams in access packages

â
â
â

â

EM - Eligible group ownerships and memberships in access packages (PIM for Groups)

â
â

â

EM - Applications in access packages

â
â
â

â

EM - SharePoint sites in access packages

â
â
â

â

EM - Microsoft Entra Roles (Preview)

â
â

â

EM - SAP Identity Access Governance (IAG) business roles (Preview)

â
â

â

EM - API permissions in access packages

â
â

EM - Approval options
Free
Microsoft Entra ID P1
Microsoft Entra ID P2
Microsoft Entra ID Governance
Microsoft Entra Suite
Microsoft Agent 365
Microsoft 365 E7

EM - Multi-stage approvals with alternate approvers if no action is taken

â
â
â
â
â

EM - Specific approvers

â
â
â
â
â

EM - Managers as approvers

â
â
â

â

EM - Internal sponsors as approvers (from assignees' connected organizations)

â
â
â

â

EM - External sponsors as approvers (from assignees' connected organizations)

â
â
â

â

EM - Sponsors as approvers (from assignees' user profile)

â
â

â

EM - Agent ID sponsors as approvers

â
â

EM - Externally determine approval requirements using custom extensions

â
â

â

EM - Collect additional requestor information for approval

â
â
â

â

EM - Lifecycle
Free
Microsoft Entra ID P1
Microsoft Entra ID P2
Microsoft Entra ID Governance
Microsoft Entra Suite
Microsoft Agent 365
Microsoft 365 E7

EM - Expiration of access package assignments

â
â
â
â
â

EM - Manage the lifecycle of external users

â
â
â

â

EM - Mark guest as governed

â
â

â

EM - Additional capabilities
Free
Microsoft Entra ID P1
Microsoft Entra ID P2
Microsoft Entra ID Governance
Microsoft Entra Suite
Microsoft Agent 365
Microsoft 365 E7

EM - Separation of duties

â
â
â

â

EM - Custom Extensions (Logic Apps)

â
â

â

EM - Auto Assignment Policies

â
â

â

EM - Verified ID integration

â
â

â

EM - Microsoft Entra ID Protection integration

â
â

â

EM - Microsoft Purview Insider Risk Management integration

â
â

â

EM - Conditional Access Scoping

â
â
â

â

My Access
Free
Microsoft Entra ID P1
Microsoft Entra ID P2
Microsoft Entra ID Governance
Microsoft Entra Suite
Microsoft Agent 365
Microsoft 365 E7

My Access portal

â
â
â
â
â

EM - My Access Search

â
â
â
â
â

EM - Suggested access packages in My Access

â
â

â

EM - Configure whether requestors can see approver details in My Access (Preview)

â
â

â

EM - Delegate approvals in My Access (Preview)

â
â

â

Privileged Identity Management (PIM)
Free
Microsoft Entra ID P1
Microsoft Entra ID P2
Microsoft Entra ID Governance
Microsoft Entra Suite
Microsoft Agent 365
Microsoft 365 E7

Privileged Identity Management (PIM)

â
â
â

â

PIM For Groups

â
â
â

â

PIM Conditional Access Controls

â
â
â

â

PIM - Custom extensions for role activation (Preview)

â
â

â

Other
Free
Microsoft Entra ID P1
Microsoft Entra ID P2
Microsoft Entra ID Governance
Microsoft Entra Suite
Microsoft Agent 365
Microsoft 365 E7

Identity governance dashboard

â
â
â
â

â

Insights and reporting - Inactive guest accounts

â
â

â

Conditional Access - Terms of use attestation

â
â
â
â

â

Agent ID default inactivity policy (preview)
â
â
â
â
â
â
â

Agent ID lifecycle policies (preview)

â
â

### Entitlement Management

Using this feature requires a Microsoft Entra ID Governance subscription for your organization's member users. Some capabilities within this feature can operate with a Microsoft Entra ID P2 subscription. Some capabilities within this feature require guest billing.

### Access reviews

Using this feature requires a Microsoft Entra ID Governance subscription for your organization's member users, including for all employees who are reviewing access or having their access reviewed. Some capabilities within this feature might operate with a Microsoft Entra ID P2 subscription. Some capabilities within this feature require guest billing.

### Lifecycle Workflows

With Microsoft Entra ID Governance licenses for Lifecycle Workflows, you can:

- Create, manage, and delete workflows up to the total limit of 50 workflows.

- Trigger on-demand and scheduled workflow execution.

- Manage and configure existing tasks to create workflows that are specific to your needs.

- Create up to 100 custom task extensions to be used in your workflows.

Using this feature, for tasks other than agent ID sponsor reassignment, requires a Microsoft Entra ID Governance subscription for your organization's member users. Some capabilities within this feature require guest billing.

## Privileged Identity Management

To use Microsoft Entra Privileged Identity Management, a tenant must have a valid license. This article describes the license requirements to use Privileged Identity Management. To use Privileged Identity Management, you must have one of the following licenses:

### Valid licenses for PIM

You need either Microsoft Entra ID Governance licenses or Microsoft Entra ID P2 licenses to use PIM and all of its settings. Currently, you can scope an access review to service principals with access to Microsoft Entra ID, resource roles with a Microsoft Entra ID P2 or users with Microsoft Entra ID Governance edition active in your tenant.

### Licenses you must have for PIM

Ensure that your directory has Microsoft Entra ID P2 or Microsoft Entra ID Governance licenses for the following categories of users:

- Users with eligible and/or time-bound assignments to Microsoft Entra ID or Azure roles managed using PIM

- Users with eligible and/or time-bound assignments as members or owners of PIM for Groups

- Users able to approve or reject activation requests in PIM

- Users assigned to an access review

- Users who perform access reviews

### When a license expires for PIM

If a Microsoft Entra ID P2, Microsoft Entra ID Governance, or trial license expires, Privileged Identity Management features are no longer available in your directory:

- Permanent role assignments to Microsoft Entra roles are unaffected.

- The Privileged Identity Management service in the Microsoft Entra admin center, and the Graph API cmdlets and PowerShell interfaces of Privileged Identity Management, will no longer be available for users to activate privileged roles, manage privileged access, or perform access reviews of privileged roles.

- Eligible role assignments of Microsoft Entra roles are removed, as users will no longer be able to activate privileged roles.

- Any ongoing access reviews of Microsoft Entra roles ends, and Privileged Identity Management configuration settings are removed.

- Privileged Identity Management no longer sends emails on role assignment changes.

## API-driven provisioning

This feature is available with Microsoft Entra ID P1, P2, and Microsoft Entra ID Governance subscriptions. A subscription license is required with enough seats for every identity that is sourced using the /bulkUpload API and provisioned to either on-premises Active Directory or Microsoft Entra ID.

### License scenarios

Customer License
Usage limits enforced at tenant level for API-driven provisioning

Microsoft Entra ID P1 or P2
Daily usage quota (number of user records that can be uploaded over 24-hour period): 100K user records (2000 /bulkUpload API calls with each request containing max of 50 records).

Max number of API-driven provisioning jobs for each flow: 2
o Max 2 apps for API-driven provisioning to on-premises Active Directory.
o Max 2 apps for API-driven provisioning to Microsoft Entra ID.

Microsoft Entra ID Governance alongside Microsoft Entra ID P1 or P2
Daily usage quota (number of user records that can be uploaded over 24-hour period): 300K user records (6000 /bulkUpload API calls with each request containing max of 50 records).

Max number of API-driven provisioning jobs for each flow: 20
o Max 20 apps for API-driven provisioning to on-premises Active Directory.
o Max 20 apps for API-driven provisioning to Microsoft Entra ID.

## Account Discovery

Account Discovery requires the Microsoft Entra ID Governance add-on or Microsoft Entra Suite. This feature allows administrators to discover existing user accounts in target applications and identify which users have matching Entra accounts or are orphan accounts. For more information, see Discover identities in target applications with Account Discovery.

## Licensing FAQs

### Do licenses need to be assigned to users to use Identity Governance features?

Users don't need to be assigned a Microsoft Entra ID Governance license, but there needs to be as many licenses to include all member users in scope of, or who configures, the Identity Governance features. In addition, the guest billing model must be enabled if there are guest users to be governed, as described in the next answer.

### How can I license usage of Microsoft Entra ID Governance features for business guests?

Microsoft Entra ID Governance utilizes Monthly Active User (MAU) licensing for guest users which is different than licensing for employees and requires an Azure subscription.

Under the guest billing model, guests are identified by a userType of Guest regardless of where the user authenticates. A userType of Guest is the default userType for all B2B invitation methods and can also be set by an Identity administrator. The bill for each month includes a record for each guest user with one or more governance actions in that month. See the Azure pricing page for pricing details.

For more information, see: Microsoft Entra ID Governance licensing for guest users.

### What happens to PIM when a license expires?

If a Microsoft Entra ID P2 or Microsoft Entra ID Governance license expires or trial ends, Privileged Identity Management features will no longer be available in your directory. The following changes listed are applicable to PIM for Microsoft Entra roles, PIM for Azure resources, and PIM for Groups.

- Active permanent assignments aren't affected.

- Active time-bound assignments become active permanent, which means they'll no longer expire at a designated time.

- Eligible role assignments are removed, as users will no longer be able to activate privileged roles.

- Privileged Identity Management blades on Microsoft Entra admin center or Azure portal, API, and PowerShell interfaces of Privileged Identity Management, will no longer be available for users to activate roles, manage assignments, or perform access reviews of privileged roles.

- Any ongoing access reviews of Microsoft Entra roles end, and Privileged Identity Management configuration settings are removed.

- Privileged Identity Management will no longer send emails on role assignment changes and PIM Alerts.

### Will any IGA features and capabilities be added under the Microsoft Entra ID P2 License?

All currently Generally Available features in Microsoft Entra ID P2 will remain, but no new Identity Governance & Administration (IGA) features or capabilities will be added to the Microsoft Entra ID P2 SKU.

## Next steps

- What is Microsoft Entra ID Governance?

 
 

 
 

 

 
 
 
 
 
 
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
 2026-10-16
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
