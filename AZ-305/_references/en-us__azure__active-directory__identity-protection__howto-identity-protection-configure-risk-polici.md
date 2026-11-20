# https://learn.microsoft.com/en-us/azure/active-directory/identity-protection/howto-identity-protection-configure-risk-policies

Source: https://learn.microsoft.com/en-us/azure/active-directory/identity-protection/howto-identity-protection-configure-risk-policies

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
 

 

 

 

 
 
# Configure and enable risk policies

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 There are two types of risk policies in Microsoft Entra Conditional Access you can set up. You can use these policies to automate the response to risks allowing users to self-remediate when risk is detected:

- User risk policy

- Sign-in risk policy

Warning

Don't combine sign-in risk and user risk conditions in the same Conditional Access policy. Create separate policies for each risk condition.

## Prerequisites

- The Microsoft Entra ID P2 or Microsoft Entra Suite license is required for full access to Microsoft Entra ID Protection features.

- For a detailed list of capabilities for each license tier, see What is Microsoft Entra ID Protection.

- The Conditional Access Administrator role is the least privileged role required to create or edit Conditional Access policies.

- If your policy requires identity verification, create an eligible identity verification profile before configuring the policy. Set Profile purpose to All or Verification, and choose a provider and credential type that support your risk scenario. All supports identity verification providers; for tenant-issued credentials, select Verification. Don't use an Onboarding- or Recovery-purpose profile for this resource-access policy.

- For identity verification tests, prepare eligible test users, permissions for the verification and investigation views, and the applicable identity verification licensing.

- To view verification status and history during validation, enable verification data collection. See the Verified ID authentication method prerequisites.

Note

Creating an identity verification profile automatically enables Collect identity verification history; otherwise, enable it in the authentication methods policy under Verified ID > Configure > Data collection.

## Choosing acceptable risk levels

Organizations must decide the level of risk they want to require access control on, while balancing security posture and user productivity.

Choosing to apply access control on a High risk level reduces the number of times a policy is triggered and minimizes friction for users. However, it excludes Low and Medium risks from the policy, which might not block an attacker from exploiting a compromised identity. Selecting Medium and/or Low risk levels usually introduces more user interrupts.

Configured trusted network locations are used by Microsoft Entra ID Protection in some risk detections to reduce false positives.

### Risk remediation

Organizations can choose to block access when risk is detected. Blocking sometimes stops legitimate users from doing what they need to. A better solution is to configure user and sign-in risk-based Conditional Access policies that allow users to self-remediate.

Warning

Users must register for Microsoft Entra multifactor authentication before they face a situation requiring remediation. For hybrid users that are synced from on-premises, password writeback must be enabled. Users not registered are blocked and require administrator intervention.

Password change (I know my password and want to change it to something new) outside of the risky user policy remediation flow doesn't meet the requirement for secure password change.

### Microsoft recommendations

Microsoft recommends the following risk policy configurations to protect your organization:

### User risk policy

Organizations should select Require risk remediation when user risk level is High. For passwordless users, Microsoft Entra revokes the user's sessions so they must reauthenticate. For users with passwords, they're prompted to complete a secure password change after a successful Microsoft Entra multifactor authentication.

When Require risk remediation is selected, two settings are automatically applied:

- Require authentication strength is automatically selected as a grant control.

- Sign-in frequency - Every time is automatically applied as a session control.

### Sign-in risk policy

Require Microsoft Entra multifactor authentication when sign-in risk level is Medium or High. This configuration allows users to prove it's them by using one of their registered authentication methods, remediating the sign-in risk.

We also recommend including the sign-in frequency session control to require reauthentication for risky sign-ins. For policies that require multifactor authentication, successful strong authentication via multifactor authentication or passwordless authentication remediates sign-in risk.

For the separate identity verification remediation path, see Configure identity verification for risk.

## Enable policies

Organizations can choose to deploy risk-based policies in Conditional Access using the following steps or use Conditional Access templates.

Before organizations enable these policies, they should take action to investigate and remediate any active risks.

### Policy exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- Emergency access or break-glass accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.

- More information can be found in the article, Manage emergency access accounts in Microsoft Entra ID.

- Service accounts and Service principals, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.

- If your organization uses these accounts in scripts or code, replace them with managed identities.

### User risk policy in Conditional Access

- Sign in to the Microsoft Entra admin center as at least a Conditional Access Administrator.

- Browse to Entra ID > Conditional Access.

- Select New policy.

- Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.

- Under Assignments, select Users or workload identities.

- Under Include, select All users.

- Under Exclude, select Users and groups and choose your organization's emergency access or break-glass accounts.

- Select Done.

- Under Target resources > Include, select All resources (formerly 'All cloud apps').

- Under Conditions > User risk, set Configure to Yes.

- Under Configure user risk levels needed for policy to be enforced, select High. This guidance is based on Microsoft recommendations and might be different for each organization

- Select Done.

- Under Access controls > Grant, select Grant access.

- Select Require risk remediation. The Require authentication strength grant control is automatically selected. Choose the strength appropriate for your organization.

- Select Select.

- Under Session, Sign-in frequency - Every time is automatically applied as a session control and is mandatory.

- Confirm your settings and set Enable policy to Report-only.

- Select Create to create your policy.

After confirming your settings using policy impact or report-only mode, move the Enable policy toggle from Report-only to On.

### Sign-in risk policy in Conditional Access

- Sign in to the Microsoft Entra admin center as at least a Conditional Access Administrator.

- Browse to Entra ID > Conditional Access.

- Select New policy.

- Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.

- Under Assignments, select Users or workload identities.

- Under Include, select All users.

- Under Exclude, select Users and groups and choose your organization's emergency access or break-glass accounts.

- Select Done.

- Under Cloud apps or actions > Include, select All resources (formerly 'All cloud apps').

- Under Conditions > Sign-in risk, set Configure to Yes.

- Under Select the sign-in risk level this policy will apply to, select High and Medium. This guidance is based on Microsoft recommendations and might be different for each organization

- Select Done.

- Under Access controls > Grant, select Grant access.

- Select Require authentication strength, then select the built-in Multifactor authentication authentication strength from the list.

- Select Select.

- Under Session.

- Select Sign-in frequency.

- Ensure Every time is selected.

- Select Select.

- Confirm your settings and set Enable policy to Report-only.

- Select Create to create to enable your policy.

After confirming your settings using policy impact or report-only mode, move the Enable policy toggle from Report-only to On.

### Passwordless scenarios

For organizations that adopt passwordless authentication methods make the following changes:

#### Update your passwordless sign-in risk policy

- Under Users:

- Include, select Users and groups and target your passwordless users.

- Under Exclude, select Users and groups and choose your organization's emergency access or break-glass accounts.

- Select Done.

- Under Cloud apps or actions > Include, select All resources (formerly 'All cloud apps').

- Under Conditions > Sign-in risk, set Configure to Yes.

- Under Select the sign-in risk level this policy will apply to, select High and Medium. For more information on risk levels, see Choosing acceptable risk levels.

- Select Done.

- Under Access controls > Grant, select Grant access.

- Select Require authentication strength, then select the built-in Passwordless MFA or Phishing-resistant MFA based on which method the targeted users have.

- Select Select.

- Under Session:

- Select Sign-in frequency.

- Ensure Every time is selected.

- Select Select.

## Configure identity verification for risk

Use Require Identity Verification (preview) with a User risk or Sign-in risk condition to require identity verification as a risk-remediation action. Successful verification remediates the risk targeted by the triggering policy: user risk or sign-in risk. Failed verification doesn't remediate risk. Check verification completion, the access decision, and the risk record separately.

The independent Require risk remediation control manages adaptive remediation based on the observed threat and authentication method. It isn't an identity-verification-specific challenge. Don't treat these two controls as interchangeable or copy session revocation and reauthentication behavior from one to the other.

Use a narrowly scoped test before rollout:

- Define the risk condition, test users, and protected resources for your scenario. Create separate policies for user risk and sign-in risk; don't combine both conditions in one policy.

- Configure an eligible identity verification profile and credential type for the scenario. Set Profile purpose to All or Verification, and confirm that the profile applies to the pilot users.

- Sign in to the Microsoft Entra admin center as at least a Conditional Access Administrator.

- Browse to Entra ID > Conditional Access, select New policy, and enter a meaningful policy name.

- Under Assignments, select Users or workload identities. Include the approved pilot users or groups and exclude your organization's emergency access accounts.

- Under Target resources > Include, select the resources in your pilot. This is a resource-access policy, not a policy targeting the Account onboarding and recovery user action.

- Under Conditions, configure one risk condition:

- For User risk, set Configure to Yes and select the user-risk levels for your pilot.

- For Sign-in risk, set Configure to Yes and select the sign-in-risk levels for your pilot.

Select Done. Don't combine the two risk conditions in one policy. Use Choosing acceptable risk levels to plan your selection.

- Under Conditions > Client apps, set Configure to Yes and select only Browser and Mobile apps and desktop clients. Legacy client types aren't supported for identity verification step-up.

- Under Access controls > Grant, select Grant access, select Require identity verification, and select Select. Don't substitute Require risk remediation or assume that control's automatic grant and session settings apply.

- Review interactions with existing policies and safe-rollout guidance. Don't add broad resource exclusions as a workaround for credential issuance. Don't copy the onboarding and recovery user-action configuration into a risk-based resource-access policy.

- Set Enable policy to Report-only and select Create for initial policy-impact evaluation. See Configure a risk-based identity verification policy for the scenario boundaries.

- Record separate success criteria for verification completion, the access decision, and the expected risk outcome. Confirm whether session revocation, reauthentication, or another action applies to this flow.

- Use report-only evaluation to review which policies could apply. Report-only mode doesn't trigger identity verification. Test the interactive verification journey separately with approved test cases in the test environment; a nonblocking evaluation isn't proof that the user completed remediation. Don't manufacture risk on production users.

- Validate the user's verification journey, then verify the remediation outcome before expanding the policy.

## Migrate risk policies to Conditional Access

If you have legacy risk policies enabled in Microsoft Entra ID Protection, you should plan to migrate them to Conditional Access:

Warning

The legacy risk policies configured in Microsoft Entra ID Protection will be retired on October 1, 2026.

### Migrate to Conditional Access

- Create equivalent user risk-based and sign-in risk-based policies in Conditional Access in report-only mode. You can create a policy with the previous steps or using Conditional Access templates based on Microsoft's recommendations and your organizational requirements.

- After administrators confirm the settings using report-only mode, they can move the Enable policy toggle from Report-only to On.

- Disable the old risk policies in ID Protection.

- Browse to ID Protection > Dashboard > Select the User risk or Sign-in risk policy.

- Set Enforce policy to Disabled.

- Create other risk policies if needed in Conditional Access.

#### Help and support for migrating risk policies

If you need help migrating your risk policies to Conditional Access, please submit a support request in the Microsoft Entra admin center.

- Go to New support request in the Microsoft Entra admin center.

- Describe your issue: Migrate legacy ID Protection policy.

- Select Microsoft Entra Sign-in and Multifactor Authentication > Next.

- Select Configuring new or existing policy settings > Next.

- Close the solution page.

- Select Create a support request.

- Use the following selections to get your request to the right team:

- Issue type: Technical.

- Service type: Microsoft Entra Sign-in and Multifactor Authentication.

- Summary: Migrate legacy ID Protection policy.

- Problem type: Identity Protection.

- Problem subtype: Configure risk policies.

- Select Next and navigate to the Additional details tab to fill out your details.

- Fill out the required details and submit your request.

## Related content

- Enable Microsoft Entra multifactor authentication registration policy

- What is risk

- Investigate risk detections

- Simulate risk detections

 
 

 
 

 

 
 
 
 
 
 
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
