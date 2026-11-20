# https://learn.microsoft.com/en-us/azure/governance/policy/concepts/scope

Source: https://learn.microsoft.com/en-us/azure/governance/policy/concepts/scope

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
 

 

 

 

 
 
# Understand scope in Azure Policy

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 There are many settings that determine which resources are capable of being evaluated and which resources Azure Policy evaluates. The primary concept for these controls is scope. Scope in Azure Policy is based on how scope works in Azure Resource Manager. For a high-level overview, see Scope in Azure Resource Manager.

This article explains the importance of scope in Azure Policy and the related objects and properties.

## Definition location

The first instance scope used by Azure Policy is when a policy definition is created. The definition might be saved in either a management group or a subscription. The location determines the scope to which the initiative or policy can be assigned. Resources must be within the resource hierarchy of the definition location to target for assignment. The resources covered by Azure Policy describes how policies are evaluated.

If the definition location is a:

- Subscription: The subscription where policy is defined and resources within that subscription can be assigned the policy definition.

- Management group: The management group where the policy is defined and resources within child management groups and child subscriptions can be assigned the policy definition. If you plan to apply the policy definition to several subscriptions, the location must be a management group that contains each subscription.

The location should be the resource container shared by all resources you want to use the policy definition on exist. This resource container is typically a management group near the root management group.

## Assignment scopes

An assignment has several properties that set a scope. The use of these properties determines which resource for Azure Policy to evaluate and which resources count toward compliance. These properties map to the following concepts:

- Inclusion: A definition evaluates compliance for a resource hierarchy or individual resource. The assignment object's scope determines what to include and evaluate for compliance. For more information, see Azure Policy assignment structure.

- Exclusion: A definition shouldn't evaluate compliance for a resource hierarchy or individual resource. The `properties.notScopes` array property on an assignment object determines what to exclude. Resources within these scopes aren't evaluated or included in the compliance count. For more information, see Azure Policy assignment structure excluded scopes.

In addition to the properties on the policy assignment, is the Azure Policy exemption structure object. Exemptions enhance the scope story by providing a method to identify a portion of an assignment to not be evaluated.

Exemption: A definition evaluates compliance for a resource hierarchy or individual resource, but doesn't evaluate for a reason such as a waiver or mitigation through another method. Resources in this state show as Exempted in compliance reports so that they can be tracked. The exemption object is created on the resource hierarchy or individual resource as a child object, which determines the scope of the exemption. A resource hierarchy or individual resource can be exempt from multiple assignments. The exemption might be configured to expire on a schedule by using the `expiresOn` property. For more information, see Azure Policy exemption structure.

Note

Due to the impact of granting an exemption for a resource hierarchy or individual resource, exemptions have additional security measures. In addition to requiring the `Microsoft.Authorization/policyExemptions/write` operation on the resource hierarchy or individual resource, the creator of an exemption must have the `exempt/Action` verb on the target assignment.

## Scope comparison

The following table is a comparison of the scope options:

Resources
Inclusion
Exclusion (notScopes)
Exemption

Resources are evaluated
â
-
-

Resource Manager object
-
-
â

Requires modifying policy assignment object
â
â
-

So how do you choose whether to use an exclusion or exemption? Typically exclusions are recommended to permanently bypass evaluation for a broad scope like a test environment that doesn't require the same level of governance. Exemptions are recommended for time-bound or more specific scenarios where a resource or resource hierarchy should still be tracked and would otherwise be evaluated, but there's a specific reason it shouldn't be assessed for compliance.

## Next steps

- Learn about the policy definition structure.

- Understand how to programmatically create policies.

- Learn how to get compliance data.

- Learn how to remediate non-compliant resources.

- Learn more about how to Organize your resources with Azure management groups.

 
 

 
 

 

 
 
 
 
 
 
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
 2025-03-04
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
