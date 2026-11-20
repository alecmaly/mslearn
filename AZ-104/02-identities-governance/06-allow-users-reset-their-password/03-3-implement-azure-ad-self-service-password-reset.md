# Unit 3: 3-implement-azure-ad-self-service-password-reset

Source: https://learn.microsoft.com/en-us/training/modules/allow-users-reset-their-password/3-implement-azure-ad-self-service-password-reset

---

# Implement Microsoft Entra self-service password reset

 
 
 
 Completed
 
 
 

 

 
 
- 5 minutes

 
 

 

 
 You've decided to implement self-service password reset (SSPR) in Microsoft Entra ID for your organization. You want to start using SSPR for a group of 20 users in the marketing department as a trial deployment. If everything works well, you'll enable SSPR for your whole organization.

In this unit, you'll learn how to enable SSPR in Microsoft Entra ID.

## Prerequisites

Before you start to configure SSPR, you need a:

- Microsoft Entra organization: This organization must have at least a P1 or P2 trial license enabled.

- Microsoft Entra account with Authentication Policy Administrator role: You'll use this account to set up SSPR.

- Non-administrative user account: You'll use this account to test SSPR. It's important that this account isn't an administrator, because Microsoft Entra imposes extra requirements on administrative accounts for SSPR. This user, and all user accounts, must have a valid license to use SSPR.

- Security group with which to test the configuration: The non-administrative user account must be a member of this group. You'll use this security group to limit who you roll SSPR out to.

## Scope of SSPR rollout

There are three settings for the Self-service password reset enabled property:

- None: No users in the Microsoft Entra organization can use SSPR. This value is the default.

- Selected: Only the members of the specified security group can use SSPR. You can use this option to enable SSPR for a targeted group of users who can test it and verify that it works as expected. When you're ready to roll it out broadly, set the property to Enabled so that all users have access to SSPR.

- All: All users in the Microsoft Entra organization can use SSPR.

## Configure SSPR

Here are the high-level steps to configure SSPR:

- Go to the Azure portal, then to Microsoft Entra ID > Manage > Password reset.

- Properties:

- Enable SSPR.

- You can enable it for all users in the Microsoft Entra organization or for selected users.

- To enable for selected users, you must specify the security group. Members of this group can use SSPR.

- Authentication methods:

- Choose whether to require one or two authentication methods.

- Choose the authentication methods that the users can use.

- Registration:

- Specify whether users are required to register for SSPR when they next sign in.

- Specify how often users are asked to reconfirm their authentication information.

- Notifications: Choose whether to notify users and administrators of password resets.

- Customization: Provide an email address or web page URL where your users can get help.

 

 
 

 

 
 
 
 <section
