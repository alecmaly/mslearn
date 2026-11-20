# Unit 3: exercise-assign-licenses-users

Source: https://learn.microsoft.com/en-us/training/modules/create-configure-manage-identities/3-exercise-assign-licenses-users

---

unit-inner-section" class="section is-uniform position-relative">
 
# Exercise - assign licenses to users

 
 
 
 Completed
 
 
 

 

 
 
- 5 minutes

 
 

 

 
 Exercise environment needs - this lab assumes you have a basic Microsoft Entra tenant with at least User Administrator rights to complete it. You can get a free trial subscription for at Try Azure for Free.

## Create a new user in Microsoft Entra ID

You can skip creating this user if you created the same user in the earlier module.

- Browse to the Identity menu in the Microsoft Entra admin center.

- In the left navigation, under select Users, then All Users.

- Within the Users page, on the menu, select + New user and Create new user.

- Create a user using the following information:

Setting
Value

User principal name
ChrisG

Name
Chris Green

First name
Chris

Last name
Green

Password
make up a unique password

- When complete, verify the account for Chris Green is shown in the All users list.

## Create a security group in Microsoft Entra ID

- Browse to the Microsoft Entra admin center screen.

- In the left navigation, under Identity, select Groups and then All groups.

- In the Groups screen, on the menu, select New group.

- Create a group using the following information:

Setting
Value

Group type
Security

Group name
Marketing

Membership type
Assigned

Owners
Assign your own administrator account as the group owner

Members
Chris Green

- When complete, verify the group named Marketing is shown in the All groups list.

## Assign a license to a group

License assignment to groups is managed through the Microsoft 365 admin center.

- Go to the Microsoft 365 admin center at https://admin.microsoft.com.

- Select Billing from the menu on the left.

- Select Licenses.

- From the list of licenses you have available, select one.

- Select Groups from the list near the top of the screen.

- On the Groups page, select + Assign license.

- Search for and select the Marketing group you created earlier.

- Select the Assign button at the bottom of the dialog.

- You should get a message that licenses were successfully assigned.

## Restore or remove a recently deleted user with Microsoft Entra ID

After you delete a user, the account remains in a suspended state for 30 days. During that 30-day window, the user account can be restored, along with all its properties. After that 30-day window passes, the permanent deletion process is automatically started.

You can view your restorable users, restore a deleted user, or permanently delete a user using Microsoft Entra ID user interface.

Important

You can't restore a permanently deleted user.

## Required permissions

You must have one of the following roles to restore or permanently delete users.

- Global administrator

- Partner Tier-1 Support

- Partner Tier-2 Support

- User administrator

 

 
 

 

 
 
 
 <section
