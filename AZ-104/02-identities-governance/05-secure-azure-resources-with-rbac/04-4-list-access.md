# Unit 4: 4-list-access

Source: https://learn.microsoft.com/en-us/training/modules/secure-azure-resources-with-rbac/4-list-access

---

unit-inner-section" class="section is-uniform position-relative">
 
# Exercise - List access using Azure RBAC and the Azure portal

 
 
 
 Completed
 
 
 

 

 
 
- 8 minutes

 
 

 

 
 At First Up Consultants, you've been granted access to a resource group for the marketing team. You want to familiarize yourself with the Azure portal and see what roles are currently assigned.

## Before you begin

Use an existing non-production resource group that you're authorized to inspect. If your subscription has no suitable resource group, follow the resource-group creation guidance in the Summary unit's More info section, or ask an administrator to provide one. Read-only access doesn't grant permission to create a resource group.

To list role assignments, your account needs `Microsoft.Authorization/roleAssignments/read` at the selected scope, for example through the Reader role at that scope or an applicable parent scope. Record the resource group's name and subscription so that you use the same scope throughout the exercises.

## List role assignments for yourself

Follow these steps to see what roles are currently assigned to you:

- Sign in to the Azure portal. The portal link is in the Summary unit's More info section.

- On the Profile menu, select the ellipsis (...) to see more links.

- Select My permissions to open the My permissions pane.

You'll find the roles that you've been assigned and the scope. Your list will look different.

## List role assignments for a resource group

Follow these steps to see what roles are assigned at the resource group scope:

- In the Search box at the top, search for and select Resource groups.

- In the list of resource groups, select a resource group.

These steps use a resource group named example-group, but your resource group's name will be different.

- On the left menu pane, select Access control (IAM).

- Select the Role assignments tab.

This tab shows who has access to the resource group. Notice that some roles are scoped to This resource, while others are (Inherited) from a parent scope.

Note

Where PIM integration is available, the list can distinguish active and eligible assignments. An eligible assignment isn't active access until the user activates it, and time-bound access applies only within the configured time window. Use Check access to inspect a particular user's assignments. The Check access pane shows assignments at the selected scope and inherited to it, not assignments that exist only at child scopes.

## List roles

As you learned in the previous unit, a role is a collection of permissions. Azure has more than 70 built-in roles that you can use in your role assignments. To list the roles:

- In the menu bar at the top of the pane, select the Roles tab to list all the built-in and custom roles.

Select a role's View link in the Details column, then select the Assignments tab to display the number of users and groups assigned to that role.

In this unit, you learned how to list the role assignments for yourself in the Azure portal. You also learned how to list the role assignments for a resource group.

 

 
 

 

 
 
 
 <section
