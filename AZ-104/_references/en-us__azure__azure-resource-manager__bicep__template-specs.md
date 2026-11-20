# https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/template-specs

Source: https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/template-specs

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
 

 

 

 

 
 
# Azure Resource Manager template specs in Bicep

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 A template spec is a resource type for storing an Azure Resource Manager template (ARM template) to deploy it later. This resource type enables you to share ARM templates with other users in your organization. Just like any other Azure resource, you can use Azure role-based access control (Azure RBAC) to share the template spec. You can use Azure CLI or Azure PowerShell to create template specs by providing Bicep files. The Bicep files are transpiled into JSON ARM templates before they're stored. You can't import a Bicep file from the Azure portal to create a template spec resource at this time.

Microsoft.Resources/templateSpecs is the resource type for template specs. It consists of a main template and any number of linked templates. Azure securely stores template specs in resource groups. Both the main template and the linked templates must be in JSON. Template Specs support versioning.

To deploy the template spec, use standard Azure tools like PowerShell, Azure CLI, the Azure portal, REST, and other supported SDKs and clients. You use the same commands as you would for the template or the Bicep file.

Note

To use template specs in Bicep with Azure PowerShell, you must install version 6.3.0 or later. To use it with Azure CLI, use version 2.27.0 or later.

When designing your deployment, always consider the lifecycle of the resources and group the resources that share similar lifecycle into a single template spec. For instance, your deployments include multiple instances of Azure Cosmos DB with each instance containing its own databases and containers. Given the databases and the containers don't change much, you want to create one template spec to include a Cosmo DB instance and its underlying databases and containers. You can then use conditional statements in your Bicep along with copy loops to create multiple instances of these resources.

Tip

The choice between module registry and template specs is mostly a matter of preference. There are a few things to consider when you choose between the two:

- Module registry is only supported by Bicep. If you are not yet using Bicep, use template specs.

- Content in the Bicep module registry can only be deployed from another Bicep file. Template specs can be deployed directly from the API, Azure PowerShell, Azure CLI, and the Azure portal. You can even use `UiFormDefinition` to customize the Azure portal deployment experience.

- Bicep has some limited capabilities for embedding other project artifacts (including non-Bicep and non-ARM-template files. For example, PowerShell scripts, CLI scripts and other binaries) by using the `loadTextContent` and `loadFileAsBase64` functions. Template specs can't package these artifacts.

## Required permissions

Two roles are built into Azure and defined for template specs:

- Template Spec Reader

- Template Spec Contributor

In addition, you also need the permissions for deploying a Bicep file. See Deploy Bicep files with the Azure CLI or Azure PowerShell.

## Why use template specs

Template specs provide the following benefits:

- You use standard ARM templates or Bicep files for your template spec.

- You manage access through Azure RBAC rather than shared access signature tokens.

- Users can deploy the template spec without having write access to the Bicep file.

- You can integrate the template spec into an existing deployment process such as a PowerShell script or a DevOps pipeline.

Template specs enable you to create canonical templates and share them with teams in your organization. The template specs are secure because they're available to Azure Resource Manager for deployment, but not accessible to users without the correct permission. Users only need read access to the template spec to deploy its template, so you can share the template without allowing others to modify it.

If you currently have your templates in a GitHub repo or storage account, you run into several challenges when trying to share and use the templates. To deploy the template, you need to either make the template publicly accessible or manage access with SAS tokens. To get around this limitation, users might create local copies, which eventually diverge from your original template. Template specs simplify sharing templates.

The templates you include in a template spec should be verified by administrators in your organization to follow the organization's requirements and guidance.

## Create template spec

The following example shows a simple Bicep file for creating a storage account in Azure.

`@allowed([
 'Standard_LRS'
 'Standard_GRS'
 'Standard_ZRS'
 'Premium_LRS'
])
param storageAccountType string = 'Standard_LRS'

resource stg 'Microsoft.Storage/storageAccounts@2025-06-01' = {
 name: 'store${uniqueString(resourceGroup().id)}'
 location: resourceGroup().location
 sku: {
 name: storageAccountType
 }
 kind:'StorageV2'
}
`

Create a template spec by using:

- 
Azure PowerShell

- 
Azure CLI

`New-AzTemplateSpec -Name storageSpec -Version 1.0a -ResourceGroupName templateSpecsRg -Location westus2 -TemplateFile ./mainTemplate.bicep
`

`az ts create \
 --name storageSpec \
 --version "1.0a" \
 --resource-group templateSpecRG \
 --location "westus2" \
 --template-file "./mainTemplate.bicep"
`

You can also use Bicep files to create template specs. However, the content of `mainTemplate` must be in JSON. The following template creates a template spec to deploy a storage account:

`param templateSpecName string = 'CreateStorageAccount'
param templateSpecVersionName string = '0.1'
param location string = resourceGroup().location

resource createTemplateSpec 'Microsoft.Resources/templateSpecs@2022-02-01' = {
 name: templateSpecName
 location: location
 properties: {
 description: 'A basic templateSpec - creates a storage account.'
 displayName: 'Storage account (Standard_LRS)'
 }
}

resource createTemplateSpecVersion 'Microsoft.Resources/templateSpecs/versions@2022-02-01' = {
 parent: createTemplateSpec
 name: templateSpecVersionName
 location: location
 properties: {
 mainTemplate: {
 '$schema': 'https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#'
 'contentVersion': '1.0.0.0'
 'parameters': {
 'storageAccountType': {
 'type': 'string'
 'defaultValue': 'Standard_LRS'
 'allowedValues': [
 'Standard_LRS'
 'Standard_GRS'
 'Standard_ZRS'
 'Premium_LRS'
 ]
 }
 }
 'resources': [
 {
 'type': 'Microsoft.Storage/storageAccounts'
 'apiVersion': '2025-06-01'
 'name': 'store$uniquestring(resourceGroup().id)'
 'location': resourceGroup().location
 'kind': 'StorageV2'
 'sku': {
 'name': '[parameters(\'storageAccountType\')]'
 }
 }
 ]
 }
 }
}
`

The JSON template embedded in the Bicep file needs to make these changes:

- Remove the commas at the end of the lines.

- Replace double quotes with single quotes.

- Escape the single quotes within the expressions. For example, 'name': '[parameters(\'storageAccountType\')]'.

- To access the parameters and variables defined in the Bicep file, you can directly use the parameter names and the variable names. To access the parameters and variables defined in `mainTemplate`, you still need to use the JSON ARM template syntax. For example, 'name': '[parameters(\'storageAccountType\')]'.

- Use the Bicep syntax to call Bicep functions. For example, 'location': resourceGroup().location.

The size of a template spec is limited to approximated 2 megabytes. If a template spec size exceeds the limit, you get the TemplateSpecTooLarge error code. The error message says:

`The size of the template spec content exceeds the maximum limit. For large template specs with many artifacts, the recommended course of action is to split it into multiple template specs and reference them modularly via TemplateLinks.
`

You can view all template specs in your subscription by using:

- 
Azure PowerShell

- 
Azure CLI

`Get-AzTemplateSpec
`

`az ts list
`

You can view details of a template spec, including its versions with:

- 
Azure PowerShell

- 
Azure CLI

`Get-AzTemplateSpec -ResourceGroupName templateSpecsRG -Name storageSpec
`

`az ts show \
 --name storageSpec \
 --resource-group templateSpecRG \
 --version "1.0a"
`

## Deploy template spec

After you've created the template spec, users with the Template Spec Reader role can deploy it. Remember that you need the appropriate permissions to deploy an ARM template.

Template specs can be deployed through the Azure portal, PowerShell, Azure CLI, or as a Bicep module in a larger template deployment. Users in an organization can deploy a template spec to any scope in Azure (e.g., a resource group, subscription, management group, or tenant).

You deploy a template spec by providing its resource ID instead of passing it in a path or URI for a Bicep file. The resource ID has the following format; notice that it includes a version name for the template spec:

/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Resources/templateSpecs/{template-spec-name}/versions/{template-spec-version}

You can deploy a template spec with the following commands:

- 
Azure PowerShell

- 
Azure CLI

`$id = "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/templateSpecsRG/providers/Microsoft.Resources/templateSpecs/storageSpec/versions/1.0a"

New-AzResourceGroupDeployment `
 -TemplateSpecId $id `
 -ResourceGroupName demoRG
`

`id = "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/templateSpecsRG/providers/Microsoft.Resources/templateSpecs/storageSpec/versions/1.0a"

az deployment group create \
 --resource-group demoRG \
 --template-spec $id
`

In practice, you'll typically run `Get-AzTemplateSpec` or `az ts show` to get the ID of the template spec you want to deploy.

- 
Azure PowerShell

- 
Azure CLI

`$id = (Get-AzTemplateSpec -Name storageSpec -ResourceGroupName templateSpecsRg -Version 1.0a).Versions.Id

New-AzResourceGroupDeployment `
 -ResourceGroupName demoRG `
 -TemplateSpecId $id
`

`id = $(az ts show --name storageSpec --resource-group templateSpecRG --version "1.0a" --query "id")

az deployment group create \
 --resource-group demoRG \
 --template-spec $id
`

You can also deploy a template spec by opening a URL in the following format:

`https://portal.azure.com/#create/Microsoft.Template/templateSpecVersionId/%2fsubscriptions%2f{subscription-id}%2fresourceGroups%2f{resource-group-name}%2fproviders%2fMicrosoft.Resources%2ftemplateSpecs%2f{template-spec-name}%2fversions%2f{template-spec-version}
`

## Parameters

Passing parameters to a template spec is similar to passing parameters to a Bicep file. Add the parameter values either inline or in a parameters file.

### Inline parameters

To pass a parameter inline, use:

- 
Azure PowerShell

- 
Azure CLI

`New-AzResourceGroupDeployment `
 -TemplateSpecId $id `
 -ResourceGroupName demoRG `
 -StorageAccountType Standard_GRS
`

`az deployment group create \
 --resource-group demoRG \
 --template-spec $id \
 --parameters storageAccountType='Standard_GRS'
`

### Parameters files

- Use Bicep parameters files.

You must specify the `using` statement to create a Bicep parameters file. For example:

`using 'using 'ts:<subscription-id>/<resource-group-name>/<template-spec-name>:<tag>'

param StorageAccountType = 'Standard_GRS'
`

For more information, see Create parameters files for Bicep deployment.

Pass parameters files with:

- 
Azure PowerShell

- 
Azure CLI

You can't use PowerShell to deploy a template spec with a `.bicepparam` file at this time.

`az deployment group create \
 --resource-group demoRG \
 --parameters "./mainTemplate.bicepparam"
`

You don't need to specify the `--template-spec` parameter because of the `using` statement in the `.bicepparam` file.

- Use JSON parameters files.

The following JSON is a sample JSON parameters file:

`{
 "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
 "contentVersion": "1.0.0.0",
 "parameters": {
 "StorageAccountType": {
 "value": "Standard_GRS"
 }
 }
}
`

You can also pass a parameters file with:

- 
Azure PowerShell

- 
Azure CLI

`New-AzResourceGroupDeployment `
 -TemplateSpecId $id `
 -ResourceGroupName demoRG `
 -TemplateParameterFile ./mainTemplate.parameters.json
`

`az deployment group create \
 --resource-group demoRG \
 --template-spec $id \
 --parameters "./mainTemplate.parameters.json"
`

## Versioning

You provide a version name for a template spec when you create one. As you iterate on the template code, you can either update an existing version (for hotfixes) or publish a new version. The version is a text string. You can choose to follow any versioning system, including semantic versioning. Template spec users can provide the version name they want to use when deploying it and can have an unlimited number of versions.

## Use tags

Tags help you to logically organize your resources. You can use Azure PowerShell or Azure CLI to add tags to template specs. The following example shows how to specify tags when creating the template spec:

- 
Azure PowerShell

- 
Azure CLI

`New-AzTemplateSpec `
 -Name storageSpec `
 -Version 1.0a `
 -ResourceGroupName templateSpecsRg `
 -Location westus2 `
 -TemplateFile ./mainTemplate.bicep `
 -Tag @{Dept="Finance";Environment="Production"}
`

`az ts create \
 --name storageSpec \
 --version "1.0a" \
 --resource-group templateSpecRG \
 --location "westus2" \
 --template-file "./mainTemplate.bicep" \
 --tags Dept=Finance Environment=Production
`

The following example shows how to apply tags when updating an existing template spec:

- 
Azure PowerShell

- 
Azure CLI

`Set-AzTemplateSpec `
 -Name storageSpec `
 -Version 1.0a `
 -ResourceGroupName templateSpecsRg `
 -Location westus2 `
 -TemplateFile ./mainTemplate.bicep `
 -Tag @{Dept="Finance";Environment="Production"}
`

`az ts update \
 --name storageSpec \
 --version "1.0a" \
 --resource-group templateSpecRG \
 --location "westus2" \
 --template-file "./mainTemplate.bicep" \
 --tags Dept=Finance Environment=Production
`

Both the template and its versions can have tags. The tags are either applied or inherited depending on the parameters that you specify:

Template spec
Version
Version parameter
Tag parameter
Tag values

Exists
N/A
Not specified
Specified
applied to the template spec

Exists
New
Specified
Not specified
inherited from the template spec to the version

New
New
Specified
Specified
applied to both template spec and version

Exists
New
Specified
Specified
applied to the version

Exists
Exists
Specified
Specified
applied to the version

## Link to template specs

- After creating a template spec, you can link to that template spec in a Bicep module. The template spec is deployed when you deploy the Bicep file containing that module. For more information, see Path to a module.

- To create aliases for template specs intended for module linking, see Aliases for modules.

## Next steps

See the Create template specs for hands-on guidance about template specs.

 
 

 
 

 

 
 
 
 
 
 
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
 2025-12-10
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
