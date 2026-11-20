# https://learn.microsoft.com/en-us/entra/fundamentals/how-to-manage-groups

Source: https://learn.microsoft.com/en-us/entra/fundamentals/how-to-manage-groups

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
 

 

 

 

 
 
# Manage Microsoft Entra groups and group membership

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Microsoft Entra groups are used to manage users that all need the same access and permissions to resources, such as potentially restricted apps and services. Instead of adding special permissions to individual users, you create a group that applies the special permissions to every member of that group.

This article covers basic group scenarios where a single group is added to a single resource and users are added as members to that group. For more complex scenarios like dynamic membership groups and rule creation, see the Microsoft Entra user management documentation.

Before adding groups and members, learn about groups and membership types to help you decide which options to use when you create a group.

## Prerequisites

The following prerequisites are required to manage groups in Microsoft Entra:

- User Administrator or Groups Administrator role is required to manage group membership settings.

- An Azure subscription. If you don't have one, create a free account.

- Access to a Microsoft Entra tenant. For more information, see Create a new tenant.

## Create a basic group and add members

You can create a basic group and add your members at the same time using the Microsoft Entra admin center. You must have at least the Groups Administrator or User Administrator role assigned to create groups. Review the appropriate Microsoft Entra roles for managing groups.

Note

Cross-tenant delegated administration uses granular delegated admin privileges (GDAP). Group creation by GDAP administrators isn't supported if the target tenant uses a group naming policy prefix or suffix that references attributes of the calling user, such as department or company name. Use an administrator account in the target tenant to create the group.

To create a basic group and add members:

- Sign in to the Microsoft Entra admin center as at least a Groups Administrator.

- Browse to Entra ID > Groups > All groups.

- Select New group.

- Select a Group type. For more information on group types, see the learn about groups and membership types article.

- Selecting the Microsoft 365 Group type enables the Group email address option.

- Enter a Group name. Choose a name that you'll remember and that makes sense for the group. A check will be performed to determine if the name is already in use. If the name is already in use, you'll be asked to change the name of your group.

- The name of the group can't start with a space. Starting the name with a space prevents the group from appearing as an option for steps such as adding role assignments to group members.

- Group email address: Only available for Microsoft 365 group types. Enter an email address manually or use the email address built from the Group name you provided.

- Group description. Add an optional description to your group.

- Switch the Microsoft Entra roles can be assigned to the group setting to yes to use this group to assign Microsoft Entra roles to members.

- This option is only available with P1 or P2 licenses.

- You must have at least the Privileged Role Administrator role.

- Enabling this option automatically selects Assigned as the Membership type.

- The ability to add roles while creating the group is added to the process.

- Learn more about role-assignable groups.

- Select a Membership type. For more information on membership types, see the learn about groups and membership types article.

- Optionally add Owners or Members. Members and owners can be added after creating your group.

- Select the link under Owners or Members to populate a list of every user in your directory.

- Choose users from the list and then select the Select button at the bottom of the window.

- Select Create. Your group is created and ready for you to manage other settings.

### Turn off group welcome email

A welcome notification is sent to all users when they're added to a new Microsoft 365 group, regardless of the membership type. When an attribute of a user or device changes, all rules for dynamic membership groups in the organization are processed for potential membership changes. Users who are added then also receive the welcome notification. You can turn off this behavior in Exchange PowerShell.

## Add members or owners of a group

Members and owners can be added from existing groups. The process is the same for members and owners. You'll need the Groups Administrator or User Administrator role to add members and owners.

Note

Need to add multiple members at one time? Learn about the add members in bulk option.

- Sign in to the Microsoft Entra admin center as at least a Groups Administrator.

- Browse to Entra ID > Groups > All groups.

- Select the group you need to manage.

- Select either Members or Owners.

- Select + Add (members or owners).

- Scroll through the list or enter a name in the search box. You can choose multiple names at one time. When you're ready, select the Select button.

The Group Overview page updates to show the number of members who are now added to the group.

## Remove members or owners of a group

Members and owners can be removed from existing groups. The process is the same for members and owners. You'll need the Groups Administrator or User Administrator role to remove members and owners.

- Sign in to the Microsoft Entra admin center as at least a Groups Administrator.

- Browse to Entra ID > Groups > All groups.

- Select the group you need to manage.

- Select either Members or Owners.

- Check the box next to a name from the list and select the Remove button.

## Edit group settings

You can edit a group's name, description, or membership type. You'll need the Groups Administrator or User Administrator role to edit a group's settings.

To edit your group settings:

- Sign in to the Microsoft Entra admin center as at least a Groups Administrator.

- Browse to Entra ID > Groups > All groups.

- Scroll through the list or enter a group name in the search box. Select the group you need to manage.

- Select Properties from the side menu.

- Update the General settings information as needed, including:

- Group name. Edit the existing group name.

- Group description. Edit the existing group description.

- Group type. You can't change the type of group after it's been created. To change the Group type, you must delete the group and create a new one.

- Membership type. Change the membership type. If you enabled the Microsoft Entra roles can be assigned to the group option, you can't change the membership type. For more info about the available membership types, see the learn about groups and membership types article.

- Object ID. You can't change the Object ID, but you can copy it to use in your PowerShell commands for the group. For more info about using PowerShell cmdlets, see Microsoft Entra cmdlets for configuring group settings.

## Add a group to another group

For the security group type, you can add an existing group to another group (also known as nested groups). Depending on the group membership types, you can add a group as a member of another group. Nested groups can be used for membership and Conditional Access scopes. Nested groups don't gain access to shared resources and applications that are assigned to the parent group.

We currently don't support:

- Adding groups to a group synced with on-premises Active Directory.

- Adding security groups to Microsoft 365 groups.

- Adding Microsoft 365 groups to security groups or other Microsoft 365 groups.

- Assigned membership to shared resources and apps for nested security groups.

- Applying licenses to nested security groups.

- Adding distribution groups in nesting scenarios.

- Adding security groups as members of mail-enabled security groups.

- Adding groups as members of a role-assignable group.

- Sign in to the Microsoft Entra admin center as at least a Groups Administrator.

- Browse to Entra ID > Groups > All groups.

- On the All groups page, search for and select the group you want to become a member of another group.

Note

You only can add your group as a member to one other group at a time. Wildcard characters aren't supported in the Select Group search box.

- On the group Overview page, select Group memberships from the side menu.

- Select + Add memberships.

- Locate the group you want your group to be a member of and choose Select.

For this exercise, we're adding "MDM policy - West" to the "MDM policy - All org" group. The "MDM - policy - West" group will have the same access as the "MDM policy - All org" group.

Now you can review the "MDM policy - West - Group memberships" page to see the group and member relationship.

For a more detailed view of the group and member relationship, select the parent group name (MDM policy - All org) and take a look at the "MDM policy - West" page details.

## Remove a group from another group

You can remove an existing Security group from another Security group; however, removing the group also removes any inherited access for its members.

- On the All groups page, search for and select the group you need to remove as a member of another group.

- On the group Overview page, select Group memberships.

- Select the parent group from the Group memberships page.

- Select Remove.

For this exercise, we're now going to remove "MDM policy - West" from the "MDM policy - All org" group.

## Delete a group

You can delete a group for any number of reasons, but typically it will be because you:

- Choose the incorrect Group type option.

- Created a duplicate group by mistake.

- No longer need the group.

- Sign in to the Microsoft Entra admin center as at least a Groups Administrator.

- Browse to Entra ID > Groups > All groups.

- Search for and select the group you want to delete.

- Select Delete.

## Related content

- Learn about groups and assigning access rights to groups

- Set up groups for self-service

- Manage groups using PowerShell commands

 
 

 
 

 

 
 
 
 
 
 
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
 2026-06-23
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
