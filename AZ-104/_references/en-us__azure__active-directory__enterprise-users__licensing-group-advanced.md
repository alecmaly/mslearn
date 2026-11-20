# https://learn.microsoft.com/en-us/azure/active-directory/enterprise-users/licensing-group-advanced

Source: https://learn.microsoft.com/en-us/azure/active-directory/enterprise-users/licensing-group-advanced

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
 

 

 

 

 
 
# Assign or unassign licenses to a group in the Microsoft 365 admin center

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 If you have security groups, mail-enabled groups, or Microsoft 365 groups, you can assign or unassign licenses for those groups on the Licenses page in the Microsoft 365 admin center. We refer to this as group-based licensing.

Note

Some Microsoft services aren't available in all locations. Before a license can be assigned to a user, the administrator must specify the user's location setting. For group-based licensing, any users without a specific location inherit the location of the tenant. If you have users in multiple locations, set the user location as part of your user creation flow. For more information, see Add users and assign licenses in Microsoft 365.

## Before you begin

- You must be at least a Groups Administrator, License Administrator, or User Administrator to assign licenses.

- In addition to the steps described in this article, you can also use the Microsoft Graph PowerShell SDK to assign or unassign Microsoft 365 licenses to groups. For more information, see Set-MgGroupLicense.

- Group-based licensing doesn't currently support nested groups (groups that contain other groups). If you assign licenses to a nested group, only users in the first-level group are assigned licenses.

- When you assign or modify licenses for a large group, like 100,000 users, it can affect performance. In certain high load situations, it might take a long time to process license changes for groups or membership changes to groups with existing licenses.

## Limitations of group-based licensing in the Microsoft 365 admin center

- You can assign licenses to a maximum of 20 groups at a time.

- When you select Reprocess to resolve issues with group license assignment, the feature attempts to reprocess licenses up to a maximum of 20 users at a time.

- The lists of users who were and who weren't successfully assigned licenses are paginated lists that display 999 users at a time. You must scroll to the bottom of the list to load the next set of users.

## Assign licenses to a group

- Sign in to the Microsoft 365 admin center as at least a License Administrator.

- Go to the Billing > Licenses page.

- On the Licenses page, select Assign licenses.

- In the side panel, search for the group that you want to assign licenses to, then select the name from the dropdown list.

- Select the subscription that the assigned licenses should come from.

- To assign or remove access to specific items, select Turn apps and services on or off.

- When you're finished, select Assign licenses.

## Unassign licenses from a group

- In the Microsoft 365 admin center, go to Billing > Licenses.

- Select the product that you want to unassign licenses for.

- On the product details page, find the group in the list.

- Select the three dots (more actions) on the group's row, and then select Unassign.

- In the confirmation dialog, select Unassign.

## Move users between licensed groups

When you move a user from one licensed group to another, the order of operations matters. If you remove a user from a group before you add them to the new one, the user might experience a brief loss of access to licensed services while group-based licensing finishes processing the new assignment. However, you can prevent this temporary loss of access. To move a user between licensed groups without service interruption, use the following steps in this order:

- Add the user to the destination group first.

- Confirm the new license is applied on the user's Licenses page.

- Remove the user from the original group.

Note

If you remove the user from the source group first, the user is unlicensed until group-based licensing finishes processing the new group's assignment. Processing time varies based on tenant size and current load. In large tenants or during high-load periods, the temporary loss of access can last longer than expected.

## Group-based licensing errors

Group-based licensing can produce errors in the background when Azure Active Directory tries to apply licenses to users through group membership. Unlike direct user license assignment, where errors appear immediately, group-based licensing records the failure on the user object and surfaces it later in the admin portal.

### View group-based licensing errors

If you receive any errors during license assignment, you can view them on the product details page.

- In the Microsoft 365 admin center, go to Billing > Licenses.

- Select the product that you want to view licenses for.

- Select the Errors & issues tab to see a list of users who have license assignment problems.

- Select a user to inspect what type of error they encountered.

### Find group-based licensing errors

You can resolve common causes of group-based licensing errors.

#### Find all groups with license assignment errors

- In the [Microsoft Entra][https://entra.microsoft.com/] admin center, select Billing > Licenses > Overview.

- If any groups have licensing errors, an information box appears.

- Select the box to see all groups with errors.

- Open each group for details.

#### Find license assignment errors for users in a group

- In the [Microsoft Entra][https://entra.microsoft.com/] admin center, select Groups.

- Select a group from the list where one or more users has a licensing error.
If users are in an error state, a notification appears.

- Select the notification to view affected users.

- Select a user to see error details.

### Resolve group-based licensing errors

There are common group-based licensing error types and fixes.

#### Problems and solutions

The following table provides common group-based and user-specific licensing issues, problems, and fixes.

Issue
Problem 
Fix

Not enough licenses
There arenât enough available licenses for one of the products assigned to the group.
Buy more licenses, remove unused direct assignments, or free licenses from other groups or users.

Conflicting service plans
A service plan in one product conflicts with a service plan already assigned to the user through another product.Example:
A user has Office 365 E1 directly assigned, and then receives Office 365 E3 through a group. Some plans overlap or conflict, such as:

- Exchange Online Plan 1

- Exchange Online Plan 2

Disable one conflicting plan, remove the redundant direct license, or adjust the group license assignment.

Other products depend on this license
A license or service plan canât be removed because another assigned product depends on it.Example:
Audio Conferencing depends on Skype for Business. If a group license containing Skype for Business is removed, but the user still has Audio Conferencing directly assigned, removal can fail or the inherited license can be converted to direct.

Ensure the dependent service is removed or reassigned before removing the prerequisite.

Usage location isnât allowed
Some Microsoft services arenât available in all countries or regions. A userâs Usage location is either missing or set to an unsupported location.
Complete the following actions:
- Set the correct usage location on the user.

- Remove users in unsupported locations from the licensed group.

- Ensure user location is populated during user creation.
If a user has no usage location, group-based licensing uses the tenant location.

Duplicate proxy addresses
Exchange Online licensing can fail if two users have the same proxy address.
Correct the duplicate proxy address, then reprocess the user or group license assignment.

Mail and ProxyAddresses attribute changes
Updating license assignment can trigger recalculation of the userâs mail and proxyAddresses attributes.
Review how proxy addresses are populated in Azure AD / Entra ID and correct the underlying source of the change.

LicenseAssignmentAttributeConcurrencyException in audit logs
A user may show LicenseAssignmentAttributeConcurrencyException when multiple groups try to assign the same license concurrently.
No action required. Azure AD retries processing and resolves the issue automatically.

More than one product license assigned to a group
If a group has multiple products assigned, Azure AD tries to apply all of them to each user. If one product fails because of insufficient licenses, conflicts, or dependency issues, the other products in that group might not be assigned either.
Inspect the affected users and determine which product caused the failure.

Licensed group is deleted
Before deleting a group, all licenses assigned to it must be removed. During removal, dependency or proxy address issues can block cleanup.If a user has a direct license that depends on a service plan inherited from the group, Azure AD might convert the inherited license into a direct assignment so the dependent service keeps working.
Example:
A group has Office 365 E3/E5 with Skype for Business enabled. Some users also have Audio Conferencing directly assigned. When the group is deleted, the E3/E5 license might be converted to direct assignment for those users because Audio Conferencing depends on Skype for Business.

Check affected users for direct assignment of license.

Products with prerequisites or add-ons
Some products are add-ons and require a prerequisite service plan.Example:
 Microsoft Workplace Analytics requires one of the following plans:

- Exchange Online Plan 1

- Exchange Online Plan 2
If you assign the add-on alone to a group, licensing fails.

Assign the prerequisite and the add-on in the same group. For example:
- Office 365 E3 with only Exchange Online Plan 2 enabled

- Microsoft Workplace Analytics
This lets users receive the add-on without consuming extra full-suite licenses if they already receive E3 elsewhere.

### Force license processing

After you update your group licensing, you might need to reprocess the licenses for your tenant. Use the following methods to reprocess the licensing for a group or a user.

#### Reprocess a group or user

Use this method to reprocess the group or user after you fix a group-level or user-specific issue.

- In the Microsoft 365 admin center, select Billing > Licenses.

- Select the license product that has assignment problems.

- Select Errors & Issues.

- Review the groups and users with license assignment errors and correct the underlying issue.

- Select the affected group or user and choose Reprocess.

## Related content

- Assign or unassign licenses for users in the Microsoft 365 admin center

- Buy or remove licenses for a Microsoft business subscription

 
 

 
 

 

 
 
 
 
 
 
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
 2026-10-15
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
