# https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-enable-password-reset-customers

Source: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-enable-password-reset-customers

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
 

 

 

 

 
 
# Enable self-service password reset

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Self-service password reset (SSPR) in Microsoft Entra External ID gives customers the ability to change or reset their password, with no administrator or help desk involvement. If a customer's account is locked or they forget their password, they can follow prompts to unblock themselves and get back to work.

Applies to external tenants: Feature support varies by authentication approach and API or SDK version. Compare Microsoft-hosted authentication, Embedded native authentication, and Bring Your Own UX (BYO UX) in the authentication approach overview. Check feature availability in the authentication support matrix.

## How the password reset process works

For Microsoft-hosted authentication, self-service password reset (SSPR) supports email one-time passcode (Email OTP) and SMS. When SSPR is enabled, users who forget their password can verify their identity using a configured recovery method. After entering the passcode, the user is prompted to create a new password. Password-recovery availability through the Native Authentication API or SDK is scoped separately in the comparison.

The Microsoft-hosted password-reset process works as follows:

- From the app, the user selects Sign in.

- On the sign-in page, they enter their email address and choose Next.

- If the user forgot their password, they select Forgot password?.

- The user is prompted to choose how to verify their identity. They can select a one-time passcode sent to their email or phone, based on the methods they registered.

- A one-time passcode is sent to the email address they entered on the first page or to their registered phone number.

- The user enters the passcode to continue.

- After successfully verifying their identity, the user is prompted to create a new password.

## Prerequisites

- If you haven't already created your own external tenant, create one now.

- Have at least the Security Administrator role.

- If you haven't already created a User flow, create one now.

## Enable self-service password reset for customers

- Sign in to the Microsoft Entra admin center.

- If you have access to multiple tenants, use the Settings icon 
 in the top menu to switch to the external tenant you created earlier from the Directories + subscriptions menu.

- Browse to Entra ID > External Identities > User flows.

- From the list of User flows, select the user flow you want to enable SSPR.

- Make sure that the sign-up user flow registers Email with password as an authentication method under Identity providers.

### Enable authentication method for password reset

To enable self-service password reset, configure the authentication method for all users or for a specific group in your tenant. Choose one of the following tabs to see the steps for each method.

- 
Email OTP

- 
SMS

The following steps show how to enable Email OTP as an authentication method for self-service password reset.

- Sign in to the Microsoft Entra admin center. If you have access to multiple tenants, use the Settings icon 
 in the top menu and switch to your external tenant from the Directories + subscriptions menu.

- Browse to Entra ID > Authentication methods.

- Under Policies > Method select Email OTP.

- Under Enable and Target, turn on Email OTP.

- Under Include, choose All users or Select groups to specify who can use this method.

- Select Save.

To use SMS for self-service password reset, users need to register their phone number as a multifactor authentication (MFA) method. There are two ways to do this:

- MFA registration happens automatically when an admin sets up a Conditional Access policy that requires MFA.

- Admins can manually add their phone number under Authentication methods.

The following steps show how to enable SMS as an authentication method for self-service password reset.

- Sign in to the Microsoft Entra admin center. If you have access to multiple tenants, use the Settings icon 
 in the top menu and switch to your external tenant from the Directories + subscriptions menu.

- Browse to Entra ID > Authentication methods.

- Under Policies > Method select SMS.

- Under Enable and Target, turn on SMS.

- Under Include, choose All users or Select groups to specify who can use this method.

Note

Self-service password reset with Phone SMS includes built-in integration with the Phone Reputation platform to detect telephony fraud in real time. Each request returns an Allow, Block, or Challenge decision to help protect users. SMS-based password reset is part of an add-on feature with tiered pricing based on location or region. Charges per SMS include fraud protection services.

- Select I Acknowledge to accept the SMS terms of use.

- Select Save.

### Enable the password reset link (optional)

You can hide, show, or customize the self-service password reset link on the sign-in page.

- In the search bar, type and select Company Branding.

- Under Default sign-in select Edit.

- On the Sign-in form tab, scroll to the Self-service password reset section and select Show self-service password reset.

- Select Review + save and Save on the Review tab.

For more details, check out the Customize the neutral branding in your external tenant article.

## Test self-service password reset

To go through the self-service password reset flow:

- Open your application, and select Sign-in.

- In the sign-in page, enter your Email address and select Next.

- Select the Forgot password? link.

- If SMS is available for self-service password reset, you can choose to receive a one-time passcode by email or phone. Enter the passcode sent to your email address or phone number.

- Once you're authenticated, you're prompted to enter a new password. Provide a New password, and Confirm password, then select Reset password to sign in to your application.

## Related content

- Add Google, Facebook, Apple, or a custom OIDC federation federation.

 
 

 
 

 

 
 
 
 
 
 
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
