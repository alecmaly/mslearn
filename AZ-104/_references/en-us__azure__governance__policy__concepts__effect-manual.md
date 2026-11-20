# https://learn.microsoft.com/en-us/azure/governance/policy/concepts/effect-manual

Source: https://learn.microsoft.com/en-us/azure/governance/policy/concepts/effect-manual

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
 

 

 

 

 
 
# Azure Policy definitions manual effect

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 The new `manual` effect enables you to self-attest the compliance of resources or scopes. Unlike other policy definitions that actively scan for evaluation, the Manual effect allows for manual changes to the compliance state. To change the compliance of a resource or scope targeted by a manual policy, you need to create an attestation. The best practice is to design manual policies that target the scope that defines the boundary of resources whose compliance need attesting.

Note

Support for manual policy is available through various Microsoft Defender
for Cloud regulatory compliance initiatives. If you are a Microsoft Defender for Cloud Premium tier customer, refer to their experience overview.

The following are examples of regulatory policy initiatives that include policy definitions with the `manual` effect:

- FedRAMP High

- FedRAMP Medium

- HIPAA

- HITRUST

- ISO 27001

- Microsoft CIS 1.3.0

- Microsoft CIS 1.4.0

- NIST SP 800-171 Rev. 2

- NIST SP 800-53 Rev. 4

- NIST SP 800-53 Rev. 5

- PCI DSS 3.2.1

- PCI DSS 4.0

- SWIFT CSP CSCF v2022

The following example targets Azure subscriptions and sets the initial compliance state to `Unknown`.

`{
 "if": {
 "field": "type",
 "equals": "Microsoft.Resources/subscriptions"
 },
 "then": {
 "effect": "manual",
 "details": {
 "defaultState": "Unknown"
 }
 }
}
`

The `defaultState` property has three possible values:

- `Unknown`: The initial, default state of the targeted resources.

- `Compliant`: Resource is compliant according to your manual policy standards

- `Non-compliant`: Resource is non-compliant according to your manual policy standards

The Azure Policy compliance engine evaluates all applicable resources to the default state specified in the definition (`Unknown` if not specified). An `Unknown` compliance state indicates that you must manually attest the resource compliance state. If the effect state is unspecified, it defaults to `Unknown`. The `Unknown` compliance state indicates that you must attest the compliance state yourself.

The following screenshot shows how a manual policy assignment with the `Unknown` state appears in the Azure portal:

When a policy definition with `manual` effect is assigned, you can set the compliance states of targeted resources or scopes through custom attestations. Attestations also allow you to provide optional supplemental information through the form of metadata and links to evidence that accompany the chosen compliance state. The person assigning the manual policy can recommend a default storage location for evidence by specifying the `evidenceStorages` property of the policy assignment's metadata.

## Next steps

- Review examples at Azure Policy samples.

- Review the Azure Policy definition structure.

- Understand how to programmatically create policies.

- Learn how to get compliance data.

- Learn how to remediate non-compliant resources.

- Review Azure management groups.

 
 

 
 

 

 
 
 
 
 
 
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
