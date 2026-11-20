# https://learn.microsoft.com/en-us/azure/governance/policy/how-to/policy-safe-deployment-practices

Source: https://learn.microsoft.com/en-us/azure/governance/policy/how-to/policy-safe-deployment-practices

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
 

 

 

 

 
 
# Safe deployment of Azure Policy assignments

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 As your environment expands, so does the demand for a controlled continuous deployment (CD) pipeline with progressive exposure control. Accordingly, Microsoft recommends DevOps teams follow the safe deployment practices (SDP) framework. The safe deployment of Azure Policy definitions and assignments helps limiting the impact of unintended behaviors of policy resources.

The high-level approach of implementing SDP with Azure Policy is to gradually rollout policy assignments by tiers to detect policy changes that affect the environment in early stages before it affects the critical cloud infrastructure.

Deployment tiers can be organized in diverse ways. In this how-to tutorial, tiers are divided by different Azure regions with Tier 5 representing non-critical, low traffic locations, and Tier 0 denoting the most critical, highest traffic locations.

## Steps for safe deployment of Azure Policy assignments with deny or append effects

Use the following flowchart as a reference as we work through how to apply the SDP framework to Azure
Policy assignments that use the `deny` or `append` policy effects.

Note

To learn more about Azure policy effects, see Understand how effects work.

Flowchart step numbers:

- Once you've selected your policy definition, assign the policy at the highest-level scope inclusive
of all deployment tiers. Apply resource selectors to narrow the applicability to the least
critical tier by using the `"kind": "resource location"` property. Configure the `audit` effect type
by using assignment overrides. Sample selector with `eastUS` location and effect as `audit`:

`"resourceSelectors": [{
 "name": "SDPRegions",
 "selectors": [{
 "kind": "resourceLocation",
 "in": [ "eastUS" ]
 }]
}],
"overrides":[{
 "kind": "policyEffect",
 "value": "Audit"
}]
`

- Once the assignment is deployed and the initial compliance scan has completed,
validate that the compliance result is as expected.

You should also configure automated tests that run compliance checks. A compliance check should
encompass the following logic:

- Gather compliance results

- If compliance results are as expected, the pipeline should continue

- If compliance results aren't as expected, the pipeline should fail and you should start debugging

For example, you can configure the compliance check by using other tools within
your particular continuous integration/continuous deployment (CI/CD) pipeline.

At each rollout stage, the application health checks should confirm the stability of the service
and impact of the policy. If the results aren't as expected due to application configuration,
refactor the application as appropriate.

- Repeat by expanding the resource selector property values to include the next tiers.
locations and validating the expected compliance results and application health. Example selector with an added location value:

`"resourceSelectors": [{
 "name": "SDPRegions",
 "selectors": [{
 "kind": "resourceLocation",
 "in": [ "eastUS", "westUS"]
 }]
}]
`

- Once you have successfully assigned the policy to all tiers using `audit` mode,
the pipeline should trigger a task that changes the policy effect to `deny` and reset
the resource selectors to the location associated with Tier 0. Example selector with one region and effect set to deny:

`"resourceSelectors": [{
 "name": "SDPRegions",
 "selectors": [{
 "kind": "resourceLocation",
 "in": [ "eastUS" ]
 }]
}],
"overrides":[{
 "kind": "policyEffect",
 "value": "Deny"
}]
`

- Once the effect is changed, automated tests should check whether enforcement is taking place as
expected.

- Repeat by including more tiers in your resource selector configuration.

- Repeat this process for all production tiers.

## Steps for safe deployment of Azure Policy assignments with modify or deployIfNotExists effects

The steps for policies using the `modify` or `deployIfNotExists` effects are similar to steps previously explained with the additional action of using enforcement mode and triggering a remediation task.
Review the following flowchart with modified steps 5-9:

Flowchart step numbers:

- Once you've selected your policy definition, assign the policy at the highest-level scope inclusive
of all deployment tiers. Apply resource selectors to narrow the applicability to the least
critical tier by using the `"kind": "resource location"` property. Configure the enforcement mode of the assignment to DoNotEnforce. Sample selector with `eastUS` location and enforcementMode as DoNotEnforce:

`"resourceSelectors": [{
 "name": "SDPRegions",
 "selectors": [{
 "kind": "resourceLocation",
 "in": [ "eastUS" ]
 }]
}],
"enforcementMode": "DoNotEnforce"
`

- Once the assignment is deployed and the initial compliance scan has completed,
validate that the compliance result is as expected.

You should also configure automated tests that run compliance checks. A compliance check should
encompass the following logic:

- Gather compliance results

- If compliance results are as expected, the pipeline should continue

- If compliance results aren't as expected, the pipeline should fail and you should start debugging

You can configure the compliance check by using other tools within
your continuous integration/continuous deployment (CI/CD) pipeline.

At each rollout stage, the application health checks should confirm the stability of the service
and impact of the policy. If the results aren't as expected due to application configuration,
refactor the application as appropriate.

You may also trigger remediation tasks to remediate existing non-compliant resources. Ensure the remediation tasks are bringing resources into compliance as expected.

- Repeat by expanding the resource selector property values to include the next tier's locations and validating the expected compliance results and application health. Example selector with an added location value:

`"resourceSelectors": [{
 "name": "SDPRegions",
 "selectors": [{
 "kind": "resourceLocation",
 "in": [ "eastUS", "westUS"]
 }]
}]
`

- Once you have successfully assigned the policy to all tiers using DoNotEnforce mode,
the pipeline should trigger a task that changes the policy `enforcementMode` to Default enablement and reset
the resource selectors to the location associated with Tier 0. Example selector with one region and effect set to deny:

`"resourceSelectors": [{
 "name": "SDPRegions",
 "selectors": [{
 "kind": "resourceLocation",
 "in": [ "eastUS" ]
 }]
}],
"enforcementMode": "Default",
`

- Once the effect is changed, automated tests should check whether enforcement is taking place as
expected.

- Repeat by including more tiers in your resource selector configuration.

- Repeat this process for all production tiers.

## Steps for safely updating built-in definition version within Azure Policy assignment

- Within the existing assignment, apply overrides to update the version of the definition for the least
critical tier. We're using a combination of overrides to change the definitionVersion and selectors within the overrides condition to narrow the applicability by `"kind": "resource location"` property. Any resources that are outside of the locations specified will continue to be assessed against the version from the `definitionVersion` top-level property in the assignment. Example override updating the version of the definition to `2.0.*` and only apply it to resources in `EastUs`.

`"overrides":[{
 "kind": "definitionVersion",
 "value": "2.0.*",
 "selectors": [{
 "kind": "resourceLocation",
 "in": [ "eastus"]
 }]
}]
`

- Once the assignment is updated and the initial compliance scan has completed,
validate that the compliance result is as expected.

You should also configure automated tests that run compliance checks. A compliance check should
encompass the following logic:

- Gather compliance results

- If compliance results are as expected, the pipeline should continue

- If compliance results aren't as expected, the pipeline should fail and you should start debugging

For example, you can configure the compliance check by using other tools within
your particular continuous integration/continuous deployment (CI/CD) pipeline.

At each rollout stage, the application health checks should confirm the stability of the service
and impact of the policy. If the results aren't as expected due to application configuration,
refactor the application as appropriate.

- Repeat by expanding the resource selector property values to include the next tiers.
locations and validating the expected compliance results and application health. Example with an added location value:

` "overrides":[{
 "kind": "definitionVersion",
 "value": "2.0",
 "selectors": [{
 "kind": "resourceLocation",
 "in": [ "eastus", "westus"]
 }]
}]
`

- Once you have successfully included all the necessary locations within the _selectors, you can remove the override and update the definitionVersion property within the assignment:

`"properties": {
 "displayName": "Enforce resource naming rules",
 "description": "Force resource names to begin with DeptA and end with -LC",
 "definitionVersion": "2.0.*",
}
`

## Next steps

- Learn how to programmatically create policies.

- Review Azure Policy as code workflows.

- Study Microsoft's guidance concerning safe deployment practices.

- Review Remediate non-compliant resources with Azure Policy.

 
 

 
 

 

 
 
 
 
 
 
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
 2025-09-06
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
