# https://learn.microsoft.com/en-us/azure/active-directory/conditional-access/what-if-tool

Source: https://learn.microsoft.com/en-us/azure/active-directory/conditional-access/what-if-tool

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
 

 

 

 

 
 
# Troubleshoot Conditional Access Policies with the What If Tool

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 
## Overview

The Conditional Access What If policy tool helps you understand the result of Conditional Access policies in your environment. It can be useful when simulating uncommon scenarios, enabling you to design more comprehensive security policies. Instead of manually testing your policies with multiple sign-ins, this tool helps you simulate a sign-in for a user, agent identity, or single tenant service principal. The simulation estimates how your policies affect this sign-in and generates a report.

The What If tool and APIs let you quickly determine the policies that apply to a specific user, agent identity, or single tenant service principal. Use this information to troubleshoot issues, understand which policies apply to specific sign-in conditions, and test complex sign-in scenarios.

## How it works

The Conditional Access What If tool is powered by the What If Evaluation API. To use the tool, start by configuring the conditions of the sign-in scenario you want to simulate. The configuration should include:

- The user, agent identity (Preview), or single tenant service principal you want to test.

- The cloud apps, user action they would attempt to perform, or sensitive data protected by authentication context they would attempt to access.

- The sign-in conditions under which access would be attempted.

Important

The What If tool doesn't test for Conditional Access service dependencies. For example, if you're using What If to test a Conditional Access policy for Microsoft Teams, the result doesn't consider any policy that applies to Office 365 Exchange Online, a Conditional Access service dependency for Microsoft Teams.

Next, initiate a simulation run that evaluates your settings. Only policies that are enabled or in report-only mode are included in an evaluation run.

When the evaluation finishes, the tool generates a report of the affected policies. To gather more information about a Conditional Access policy, use Conditional Access per-policy reporting or the Conditional Access insights and reporting workbook for details about policies in report-only mode or currently enabled.

## Run the What If tool

You can find the What If tool in the Microsoft Entra admin center > Entra ID > Conditional Access > Policies > What If.

To run the What If evaluation, provide the conditions you want to evaluate.

## Conditions

The following conditions are required: identity, target resource, device platform, and client app. All other conditions are optional and are assumed to be set to none by default if no value is provided. For definitions of these conditions, see the article Building a Conditional Access policy.

## Evaluation

Start an evaluation by selecting What If. The evaluation result provides you with a report that consists of:

- An indicator showing whether classic policies exist in your environment.

- Policies that apply to your user, agent, or workload identity.

- Policies that don't apply to your user or workload identity.

The list of policies that apply also includes grant controls and session controls that must be satisfied.

The list of policies that don't apply includes the reasons why these policies don't apply. For each listed policy, the reason represents the first condition that wasn't satisfied.

Has filter indicates whether the policy has app filters that use custom security attributes.

## Key differences between the What If evaluation API and the legacy experience

The What If Evaluation API is a Microsoft Graph API that is called by the Conditional Access experience. The API is different from the legacy What If evaluation in a few ways:

- The What If API is a public and fully supported API. You can use it through the Conditional Access experience and the Microsoft Graph API.

- The logic aligns with the authentication logic used during sign-in to provide more accurate policy evaluation.

- The What If API expects all sign-in parameters to be defined for the evaluation to provide the most accurate results. If your tenant has policies with specific conditions and the sign-in details for those conditions aren't provided, the What If API can't evaluate those conditions.

Note

For application specification, provide the App ID. Groups of apps, such as Office 365 or Microsoft Admin Portals, don't result in a match.

### Examples

This example highlights key differences:

Suppose you have a Conditional Access policy with the following configuration:

- User: All users

- Resource: Office 365

- Location: United States

- Sign-in risk: High

Example
Parameters
Result based on legacy What If evaluation
Result based on the new What If evaluation API

1
UserId = â00aa00aa-bb11-cc22-dd33-44ee44ee44ee"
Applies
Does not apply

2
UserId = â00aa00aa-bb11-cc22-dd33-44ee44ee44ee" 
 ApplicationId = â00000003-0000-0ff1-ce00-000000000000"â¯
Applies
Does not apply

3
UserId = â00aa00aa-bb11-cc22-dd33-44ee44ee44ee" 
 ApplicationId = â00000003-0000-0ff1-ce00-000000000000" 
 Location = âUSâ
Applies
Does not apply

4
UserId = â00aa00aa-bb11-cc22-dd33-44ee44ee44ee"â¯
 ApplicationId = â00000003-0000-0ff1-ce00-000000000000"â¯
â¯Location = âUSââ¯
â¯Sign-in Risk = âHighââ¯

Applies
Applies

## Related content

- Learn more about Conditional Access policy application by using the policies report-only mode in Conditional Access insights and reporting.

- To configure Conditional Access policies for your environment, see Conditional Access common policies.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-08-27
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
