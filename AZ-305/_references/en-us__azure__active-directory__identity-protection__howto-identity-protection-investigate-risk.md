# https://learn.microsoft.com/en-us/azure/active-directory/identity-protection/howto-identity-protection-investigate-risk

Source: https://learn.microsoft.com/en-us/azure/active-directory/identity-protection/howto-identity-protection-investigate-risk

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
 

 

 

 

 
 
# How to investigate risk

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Microsoft Entra ID Protection provides several risk reports that can be used to investigate identity risks in your environment. Investigation of events is key to better understanding and identifying any weak points in your security strategy. ID Protection reports can be archived for storage or integrated with Security Information and Event Management (SIEM) tools for further analysis. Organizations can also take advantage of Microsoft Defender, Microsoft Sentinel, and Microsoft Graph API integrations to aggregate data with other sources.

There are many ways to investigate risk in your environment and even more details to consider during your investigation. This article provides a framework to help you get started and outlines some of the most common scenarios and recommended actions.

## Prerequisites

- Microsoft Entra ID P2 or Microsoft Entra Suite license is required for full access to Microsoft Entra ID Protection features.

- Global Reader is the least privileged role required to view the risk reports.

- Reports Reader is the least privileged role required to view the sign-in and audit logs.

## Initial triage

When starting the initial triage, we recommend the following actions:

- Review the ID Protection dashboard to visualize number of attacks, number of high risk users, and other important metrics based on detections in your environment.

- Review the risk reports to examine the details of any recent risky users, sign-ins, or detections.

- Review the Impact analysis workbook to understand the scenarios where risk is evident in your environment and what risk-based access policies should be enabled to manage high-risk users and sign-ins.

- Review the sign-in logs to identify similar activities with the same characteristics. This activity could be an indication of more compromised accounts.

- If there are common characteristics, like IP address, geography, success/failure, etc., consider blocking them with a Conditional Access policy.

- Review which resources might be compromised, including potential data downloads or administrative modifications.

- Enable self-remediation policies through Conditional Access.

- With Insider Risk Management through Microsoft Purview, you can check to see if the user performed other risky activities, such as downloading a large volume of files from a new location. This behavior is a strong indication of a possible compromise.

If you suspect an attacker can impersonate the user, you should require the user to reset their password and perform MFA or block the user and revoke all refresh and access tokens.

## Investigation and risk remediation framework

Organizations can use the following framework to investigate suspicious activity. When risk is detected, the recommended first step is self-remediation, if it's an option. Self-remediation can take place through self-service password reset or through remediation flow of a risk-based Conditional Access policy.

If self-remediation isn't an option, an administrator needs to remediate the risk. Remediation is done by invoking a password reset, requiring user to reregister for MFA, blocking the user, or revoking user sessions. The following flow chart shows the recommended flow once a risk is detected:

Once the risk is contained, more investigation might be required to mark the risk as safe, compromised, or to dismiss it.

- Check the sign-in logs and validate whether the activity is normal for the given user.

- Look at the user's past activities including the following properties to see if they're normal for the given user.

- Application - Is the app commonly used by the user?

- Device - Is the device registered or compliant?

- Location - Is the user traveling to a different location or accessing devices from multiple locations?

- IP address

- User agent string

- Investigate using other security tools, where available.

- If you have Microsoft Sentinel, check for corresponding alerts that might indicate a larger issue.

- If you haveâ¯Microsoft Defender XDR, you can follow a user risk event through other related alerts and incidents.

- The MITRE ATT&CK chain through Microsoft Sentinel in Microsoft Defender XDR might also provide insights. In the Microsoft Defender portal, browse to Incidents & alerts > Alerts > and set the Product name filter to AAD Identity Protection to find alerts from Microsoft Entra ID Protection.

- Contact the user to confirm if they recognize the sign-in; however, keep in mind that email or Teams might be compromised.

- Confirm the information you have such as:

- Timestamp

- Application

- Device

- Location

- IP address

- Depending on the results of the investigation, mark the user or sign-in as confirmed compromised, confirmed safe, or dismiss the risk. You can confirm compromise in the Microsoft Entra admin center or programmatically using Microsoft Graph.

- Set up risk-based Conditional Access policies to prevent similar attacks or to address any gaps in coverage.

## Investigate identity verification outcomes

For a risk-based policy using Require Identity Verification (preview), investigate verification completion, the policy's access decision, and the relevant risk record as separate outcomes. An issued credential, successful access attempt, or registered passkey alone isn't evidence that the risk was remediated.

To view users' verification status and history, enable verification data collection as described in the Verified ID authentication method prerequisites.

Note

Creating an identity verification profile automatically enables Collect identity verification history; otherwise, enable it in the authentication methods policy under Authentication Methods > Policies > Verified ID > Configure > Data collection.

- Review the applicable risk condition, policy, and sign-in result for the tested access attempt.

- Review available identity verification status and history. Distinguish credential issuance and presentation from a completed verification outcome.

- Check the relevant user-risk or sign-in-risk record for the expected remediation outcome. Successful verification can remediate risk in supported scenarios, but isn't proof that every risk was cleared.

- If verification succeeds but risk remains, continue the investigation and record both outcomes. Don't dismiss risk solely because verification succeeded.

- Record cancellation, failed verification, missing or unavailable credentials, and the return to the original access attempt as separate test outcomes. Use the existing remediation process when self-remediation doesn't complete.

If you review credential provenance, remember that during preview it applies only to passkeys. It isn't a substitute for verification history or the risk record. Collect only approved diagnostic evidence.

## Investigate specific detections

Certain risk detections require specific investigation steps. The following sections outline some of the most common risk detections and recommended actions.

### Microsoft Entra threat intelligence

To investigate a Microsoft Entra threat intelligence risk detection, follow these steps based on the information provided in the "additional info" field of the Risk Detection Details pane:

- If the sign-in was from a suspicious IP Address:

- Confirm if the IP address shows suspicious behavior in your environment.

- Does the IP generate a high number of failures for a user or set of users in your directory?

- Is the traffic of the IP coming from an unexpected protocol or application, for example Exchange legacy protocols?

- If the IP address corresponds to a cloud service provider, rule out that there are no legitimate enterprise applications running from the same IP.

- Account was the victim of a password spray attack

- Validate that no other users in your directory are targets of the same attack.

- Determine if other users have sign-ins with similar atypical patterns seen in the detected sign-in within the same time frame. Password spray attacks might display unusual patterns in:

- User agent string

- Application

- Protocol

- Ranges of IPs/ASNs

- Time and frequency of sign-ins

- Detection was triggered by a real-time rule

- Validate that no other users in your directory are targets of the same attack. This information can be found using the TI_RI_#### number assigned to the rule.

- Real-time rules protect against novel attacks identified by Microsoft's threat intelligence research. If multiple users in your directory were targets of the same attack, investigate unusual patterns in other attributes of the sign in.

### Atypical travel detections

- If you confirm the activity was not performed by a legitimate user:

- Mark the sign-in as compromised, and invoke a password reset if not already performed by self-remediation.

- Block the user if attacker has access to reset password or perform MFA and reset password.

- If a user is known to use the IP address in the scope of their duties, confirm sign-in as safe.

- If you confirm that the user recently traveled to the destination mentioned detailed in the alert, confirm sign-in as safe.

- If you confirm that the IP address range is from a sanctioned VPN, confirm sign-in as safe and add the VPN IP address range to named locations in Microsoft Entra ID and Microsoft Defender for Cloud Apps.

### Anomalous token and token issuer anomaly detections

- If you confirm that the activity was not performed by a legitimate user using a combination of risk alert, location, application, IP address, User Agent, or other characteristics that are unexpected for the user:

- Mark the sign-in as compromised, and invoke a password reset if not already performed by self-remediation.

- Block the user if an attacker has access to reset password or perform.

- Set up risk-based Conditional Access policies to require password reset, perform MFA, or block access for all high-risk sign-ins.

- If you confirm location, application, IP address, User Agent, or other characteristics are expected for the user and there aren't other indications of compromise, allow the user to self-remediate with a risk-based Conditional Access policy or have an admin confirm sign-in as safe.

For further investigation of token based detections, see the blog post Token tactics: How to prevent, detect, and respond to cloud token theftâ¯theâ¯Token theft investigation playbook.

### Suspicious browser detections

This detection indicates the user doesn't commonly use the browser or activity within the browser doesn't match the user's normal behavior.

- Confirm the sign-in as compromised, and invoke a password reset if not already performed by self-remediation. Block the user if an attacker has access to reset password or perform MFA.

- Set up risk-based Conditional Access policies to require password reset, perform MFA, or block access for all high-risk sign-ins.

### Malicious IP address detections

- If you confirm that the activity was not performed by a legitimate user:

- Confirm the sign-in as compromised, and invoke a password reset if not already performed by self-remediation.

- Block the user if an attacker has access to reset password or perform MFA and reset password and revoke all tokens.

- Set up risk-based Conditional Access policies to require password reset or perform MFA for all high-risk sign-ins.

- If you confirm the user does use the IP address in the scope of their duties, confirm the sign-in as safe.

### Password spray detections

A password spray detection means Microsoft observed an attacker conducting a spray attack and achieving a successful credential validation against a user in your tenant. The spray attack might have targeted users across many tenants â the detection fires only in tenants where a successful password match was confirmed. Unsuccessful spray attempts don't generate a detection.

- If you confirm that the activity was not performed by a legitimate user:

- Mark the sign-in as compromised, and invoke a password reset if not already performed by self-remediation.

- Block the user if an attacker has access to reset password or perform MFA and reset password and revoke all tokens.

- If you confirm the user does use the IP address in the scope of their duties, confirm the sign-in as safe.

- If you confirm that the account isn't compromised and see no brute force or password spray indicators against the account:

- Allow the user to self-remediate with a risk-based Conditional Access policy or have an admin confirm sign-in as safe.

- Ensure you have Microsoft Entra smart lockout configured appropriately to avoid unnecessary account lockouts.

For further investigation of password spray risk detections, see the article Password spray investigation.

### Leaked credentials detections

Leaked credentials detections are always high risk because they represent confirmed credential exposure. When this detection fires, investigate right away.

If this detection identified a leaked credential for a user:

- Assess the scope of exposure. Review the user's risk history and sign-in logs to determine if the leaked credential was used for unauthorized access. Look for correlated sign-in risk events such as sign-ins from unfamiliar locations, anonymous IP addresses, or atypical travel.

- Check if the password was already changed. Verify whether the user changed their password after the date the leak was detected. A cloud-based password reset triggered by a Microsoft Entra Conditional Access policy fully remediates the user risk for this detection. If the password was changed, the risk might already be self-remediated. If not, confirm the user as compromised and initiate a password reset.

- Block access if an attacker is active. If sign-in logs show unauthorized access, or if an attacker has the ability to reset the password or perform MFA, block the user, reset the password, and revoke all refresh tokens. Revoking sessions is critical when there's evidence of active compromise.

- Review for lateral movement. Check the user's recent activity for signs of privilege escalation, new app registrations, mailbox rule changes, or access to sensitive resources that might indicate post-compromise activity.

- Verify connected accounts. If the user reuses passwords across services, consider the credential compromised beyond your tenant. Advise the user to change passwords on other services where they use the same credential.

## Mitigate future risks

- Add corporate VPNs and IP address ranges to named locations in your Conditional Access policies to reduce false positives.

- Consider creating a known traveler database for updated organizational travel reporting and use it to cross-reference travel activity.

- Provide feedback in ID Protection to improve detection accuracy and reduce false positives.

## Next steps

- Remediate and unblock users

- Policies available to mitigate risks

- Enable sign-in and user risk policies

 
 

 
 

 

 
 
 
 
 
 
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
