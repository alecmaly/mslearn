# https://learn.microsoft.com/en-us/azure/governance/policy/concepts/definition-structure-basics

Source: https://learn.microsoft.com/en-us/azure/governance/policy/concepts/definition-structure-basics

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
 

 

 

 

 
 
# Azure Policy definition structure basics

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Policy definitions describe resource compliance conditions and the effect to take if a condition is met. A condition compares a resource property field or a value to a required value. Resource property fields are accessed by using aliases. When a resource property field is an array, a special array alias can be used to select values from all array members and apply a condition to each one. Learn more about conditions.

By using policy assignments, you can control costs and manage your resources. For example, you can specify that only certain types of virtual machines are allowed. Or, you can require that resources have a particular tag. Assignments at a scope apply to all resources at that scope and below. If a policy assignment is applied to a resource group, it's applicable to all the resources in that resource group.

You use JSON to create a policy definition that contains elements for:

- `displayName`

- `description`

- `mode`

- `version`

- `metadata`

- `parameters`

- `policyRule`

- logical evaluations

- `effect`

For example, the following JSON shows a policy that limits where resources are deployed:

`{
 "properties": {
 "displayName": "Allowed locations",
 "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
 "mode": "Indexed",
 "metadata": {
 "version": "1.0.0",
 "category": "Locations"
 },
 "parameters": {
 "allowedLocations": {
 "type": "array",
 "metadata": {
 "description": "The list of locations that can be specified when deploying resources",
 "strongType": "location",
 "displayName": "Allowed locations"
 },
 "defaultValue": [
 "westus2"
 ]
 }
 },
 "policyRule": {
 "if": {
 "not": {
 "field": "location",
 "in": "[parameters('allowedLocations')]"
 }
 },
 "then": {
 "effect": "deny"
 }
 }
 }
}
`

For more information, go to the policy definition schema. Azure Policy built-ins and patterns are at Azure Policy samples.

## Display name and description

You use `displayName` and `description` to identify the policy definition and provide context for when the definition is used. The `displayName` has a maximum length of 128 characters and `description` a maximum length of 512 characters.

Note

During the creation or updating of a policy definition, `id`, `type`, and `name` are defined
by properties external to the JSON and aren't necessary in the JSON file. Fetching the policy
definition via SDK returns the `id`, `type`, and `name` properties as part of the JSON, but
each are read-only information related to the policy definition.

## Policy type

While the `policyType` property can't be set, there are three values returned by SDK and visible in the portal:

- `Builtin`: Microsoft provides and maintains these policy definitions.

- `Custom`: All policy definitions created by customers have this value.

- `Static`: Indicates a Regulatory Compliance policy definition with Microsoft Ownership. The compliance results for these policy definitions are the results of non-Microsoft audits of Microsoft infrastructure. In the Azure portal, this value is sometimes displayed as Microsoft managed. For more information, see Shared responsibility in the cloud.

## Mode

The `mode` is configured depending on if the policy is targeting an Azure Resource Manager property or a Resource Provider property.

### Resource Manager modes

The `mode` determines which resource types are evaluated for a policy definition. The supported modes are:

- `all`: evaluate resource groups, subscriptions, and all resource types

- `indexed`: only evaluate resource types that support tags and location

For example, resource `Microsoft.Network/routeTables` supports tags and location and is evaluated in both modes. However, resource `Microsoft.Network/routeTables/routes` can't be tagged and isn't evaluated in `indexed` mode.

We recommend that you set `mode` to `all` in most cases. All policy definitions created through the portal use the `all` mode. If you use PowerShell or Azure CLI, you can specify the `mode` parameter manually. If the policy definition doesn't include a `mode` value, it defaults to `all` in Azure PowerShell and to `null` in Azure CLI. A `null` mode is the same as using `indexed` to support backward compatibility.

`indexed` should be used when creating policies that enforce tags or locations. While not required, it prevents resources that don't support tags and locations from showing up as non-compliant in the compliance results. The exception is resource groups and subscriptions. Policy definitions that enforce location or tags on a resource group or subscription should set `mode` to `all` and specifically target the `Microsoft.Resources/subscriptions/resourceGroups` or `Microsoft.Resources/subscriptions` type. For an example, see Pattern: Tags - Sample #1. For a list of resources that support tags, see Tag support for Azure resources.

### Resource Provider modes

The following Resource Provider modes are fully supported:

- `Microsoft.Kubernetes.Data` for managing Kubernetes clusters and components such as pods, containers, and ingresses. Supported for Azure Kubernetes Service clusters and Azure Arc-enabled Kubernetes clusters. Definitions using this Resource Provider mode use the effects audit, deny, and disabled.

- `Microsoft.KeyVault.Data` for managing vaults and certificates in Azure Key Vault. For more information on these policy definitions, see Integrate Azure Key Vault with Azure Policy.

- `Microsoft.Network.Data` for managing Azure Virtual Network Manager custom membership policies using Azure Policy.

The following Resource Provider modes are currently supported as a preview:

- `Microsoft.ManagedHSM.Data` for managing Managed Hardware Security Module (HSM) keys using Azure Policy.

- `Microsoft.DataFactory.Data` for using Azure Policy to deny Azure Data Factory outbound traffic domain names not specified in an allowlist. This Resource Provider mode is enforcement only and doesn't report compliance in public preview.

- `Microsoft.MachineLearningServices.v2.Data` for managing Azure Machine Learning model deployments. This Resource Provider mode reports compliance for newly created and updated components. During public preview, compliance records remain for 24 hours. Model deployments that exist before these policy definitions are assigned don't report compliance.

- `Microsoft.LoadTestService.Data` for restricting Azure Load Testing instances to private endpoints.

Note

Unless explicitly stated, Resource Provider modes only support built-in policy definitions, and exemptions are not supported at the component-level.

The following resource provider modes don't support built-in versioning:

- `Microsoft.DataFactory.Data`

- `Microsoft.MachineLearningServices.v2.Data`

- `Microsoft.ManagedHSM.Data`

- `Microsoft.CognitiveServices.Data`

Custom policy versioning isn't supported for any resource provider mode during public preview, including:

- `Microsoft.KeyVault.Data`

## Version

Both built-in and custom policy definitions can host multiple versions with the same `definitionID`. If you don't specify a version number, all experiences show the latest version of the definition. To see a specific version of a built-in policy, specify it in the API, SDK, or UI. To reference a specific version of a definition within an assignment, see definition version within assignment.

Custom policy versioning is in public preview. During preview, each custom definition or initiative can hold up to four versions.

The Azure Policy service uses the `version`, `preview`, and `deprecated` properties to convey state and level of change to a policy definition or initiative. The format of `version` is: `{Major}.{Minor}.{Patch}`. When a policy definition is in preview state, the suffix preview is appended to the `version` property and treated as a boolean. When a policy definition is deprecated, the deprecation is captured as a boolean in the definition's metadata using `"deprecated": "true"`.

- Major Version (example: 2.0.0): introduce breaking changes such as major rule logic changes, removing parameters, adding an enforcement effect by default.

- Minor Version (example: 2.1.0): introduce changes such as minor rule logic changes, adding new parameter allowed values, change to `roleDefinitionIds`, adding or moving definitions within an initiative.

- Patch Version (example: 2.1.4): introduce string or metadata changes and break glass security scenarios (rare).

For more information about Azure Policy versions built-ins, see Built-in versioning. To learn more about what it means for a policy to be deprecated or in preview, see Preview and deprecated policies.

## Metadata

The optional `metadata` property stores information about the policy definition. Customers can define any properties and values useful to their organization in `metadata`. However, there are some common properties used by Azure Policy and in built-ins. Each `metadata` property has a limit of 1,024 characters.

### Common metadata properties

- `version` (string): Tracks details about the version of the contents of a policy definition.

- `category` (string): Determines under which category in the Azure portal the policy definition is displayed.

- `preview` (boolean): True or false flag for if the policy definition is preview.

- `deprecated` (boolean): True or false flag for if the policy definition is marked as deprecated.

- `portalReview` (string): Determines whether parameters should be reviewed in the portal, regardless of the required input.

## Definition location

While creating an initiative or policy, it's necessary to specify the definition location. The definition location must be a management group or a subscription. This location determines the scope to which the initiative or policy can be assigned. Resources must be direct members of or children within the hierarchy of the definition location to target for assignment.

If the definition location is a:

- Subscription - Only resources within that subscription can be assigned the policy definition.

- Management group - Only resources within child management groups and child subscriptions can be assigned the policy definition. If you plan to apply the policy definition to several subscriptions, the location must be a management group that contains each subscription.

For more information, see Understand scope in Azure Policy.

## Next steps

- For more information about policy definition structure, go to parameters, policy rule, and alias.

- For initiatives, go to initiative definition structure.

- Review examples at Azure Policy samples.

- Review Understanding policy effects.

- Understand how to programmatically create policies.

- Learn how to get compliance data.

- Learn how to remediate non-compliant resources.

- Review what a management group is with Organize your resources with Azure management groups.

 
 

 
 

 

 
 
 
 
 
 
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
