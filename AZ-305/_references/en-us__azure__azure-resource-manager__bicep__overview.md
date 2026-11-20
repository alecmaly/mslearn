# https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/overview

Source: https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/overview

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
 

 

 

 

 
 
# What is Bicep?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Bicep is a domain-specific language that uses declarative syntax to deploy Azure resources. In a Bicep file, you define the infrastructure you want to deploy to Azure and then use that file throughout the development lifecycle to repeatedly deploy that infrastructure. Your resources are deployed in a consistent manner.

Bicep provides concise syntax, reliable type safety, and support for reusing code. Bicep offers an optimal authoring experience for your infrastructure-as-code solutions in Azure.

Warning

Microsoft Customer Support doesn't provide assistance for issues resulting from the use of Bicep experimental features; use them at your own risk.

## Benefits of Bicep

Bicep provides the following advantages:

- Support for all resource types and API versions: Bicep immediately supports all preview and GA versions for Azure services. As soon as a resource provider introduces new resource types and API versions, you can use them in your Bicep file. You don't need to wait for tools to be updated before using new services.

- Simple syntax: When compared to the equivalent JSON template, Bicep files are more concise and easier to read. Bicep doesn't require prior knowledge of programming languages. Bicep syntax is declarative and specifies which resources and resource properties you want to deploy.

The following examples show the difference between a Bicep file and the equivalent JSON template. Both examples deploy a storage account:

- 
Bicep

- 
JSON

`param location string = resourceGroup().location
param storageAccountName string = 'toylaunch${uniqueString(resourceGroup().id)}'

resource storageAccount 'Microsoft.Storage/storageAccounts@2023-05-01' = {
 name: storageAccountName
 location: location
 sku: {
 name: 'Standard_LRS'
 }
 kind: 'StorageV2'
 properties: {
 accessTier: 'Hot'
 }
}
`

`{
 "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
 "contentVersion": "1.0.0.0",
 "parameters": {
 "location": {
 "type": "string",
 "defaultValue": "[resourceGroup().location]"
 },
 "storageAccountName": {
 "type": "string",
 "defaultValue": "[format('toylaunch{0}', uniqueString(resourceGroup().id))]"
 }
 },
 "resources": [
 {
 "type": "Microsoft.Storage/storageAccounts",
 "apiVersion": "2023-05-01",
 "name": "[parameters('storageAccountName')]",
 "location": "[parameters('location')]",
 "sku": {
 "name": "Standard_LRS"
 },
 "kind": "StorageV2",
 "properties": {
 "accessTier": "Hot"
 }
 }
 ]
}
`

- Authoring experience: When you use the Bicep Extension for VS Code to create your Bicep files, you get a first-class authoring experience. The editor provides rich type safety, IntelliSense, and syntax validation.

You can also create Bicep files in Visual Studio with the Bicep extension for Visual Studio.

- Repeatable results: Deploy your infrastructure throughout the development lifecycle with confidence that your resources are deployed consistently. Bicep files are idempotent, which means that you can deploy the same file many times and get the same resource types in the same state. You can develop one file that represents the desired state instead of developing many separate files to represent updates. For example, the following file creates a storage account. If you deploy this template and the storage account when the specified properties already exist, changes aren't made:

- 
Bicep

- 
JSON

`param location string = resourceGroup().location

resource mystore 'Microsoft.Storage/storageAccounts@2023-05-01' = {
 name: 'mystorageaccount'
 location: location
 sku: {
 name: 'Standard_LRS'
 }
 kind: 'StorageV2'
}
`

`{
 "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
 "contentVersion": "1.0.0.0",
 "parameters": {
 "location": {
 "type": "string",
 "defaultValue": "[resourceGroup().location]"
 }
 },
 "resources": {
 "mystore": {
 "type": "Microsoft.Storage/storageAccounts",
 "apiVersion": "2023-05-01",
 "name": "mystorageaccount",
 "location": "[parameters('location')]",
 "sku": {
 "name": "Standard_LRS"
 },
 "kind": "StorageV2"
 }
 }
}
`

- Orchestration: You don't have to worry about the complexities of ordering operations. Azure Resource Manager orchestrates the deployment of interdependent resources so that they're created in the correct order. When possible, Resource Manager deploys resources in parallel, which helps your deployments to finish faster than serial deployments. You deploy the file through one rather than multiple imperative commands.

- Modularity: Use modules to segment your Bicep code into manageable parts. Modules help you to reuse code and simplify development. A module deploys a set of related resources. Add a module to a Bicep file when you need to deploy those resources.

- Integration with Azure services: Bicep integrates with Azure services such as Azure Policy, template specs, and Azure Blueprints.

- Preview changes: You can use the what-if operation to preview changes before deploying the Bicep file. The what-if operation shows you which resources to create, update, or delete and any resource properties to change. It also checks the current state of your environment and eliminates the need to manage this state.

- No state or state files to manage: Azure stores all states. You can collaborate with others and be confident that your updates are handled as expected.

- No cost and open source: Since Bicep is free, you don't pay for premium capabilities. Microsoft Support supports it.

## Get started

To start with Bicep:

- Install the tools. For more information, see Set up Bicep development and deployment environments, or use the VS Code devcontainer/Codespaces repository to get a preconfigured authoring environment.

- **Complete the Quickstart.

To decompile an existing Resource Manager template to Bicep, see Decompile a JSON Azure Resource Manager template to Bicep. You can use Bicep Playground to view Bicep and its equivalent, JSON, side by side.

To learn about the resources that are available in your Bicep file, see Bicep resource reference.

You can find Bicep examples in the Bicep GitHub repo.

## About the language

Bicep isn't intended as a general programming language to write applications. A Bicep file declares Azure resources and resource properties without writing a sequence of programming commands to create them.

To track the status of the Bicep work, see the Bicep project repository.

To learn about Bicep, watch the following video:

You can use Bicep instead of JSON to develop Resource Manager templates. The JSON syntax to create a Resource Manager template can be verbose and require complicated expressions. Bicep syntax reduces that complexity and improves the development experience. Bicep is a transparent abstraction over a Resource Manager JSON template that doesn't lose the capabilities of a JSON template. During deployment, the Bicep CLI converts a Bicep file into a Resource Manager JSON template.

Resource types, API versions, and properties that are valid in a Resource Manager template are valid in a Bicep file.

Bicep offers an easier and more concise syntax than its equivalent, JSON. You don't use bracketed expressions `[...]`. Instead, you directly call functions and get values from parameters and variables. You give each deployed resource a symbolic name, which makes it easy to reference that resource in your template.

For a full comparison of the syntax, see Comparing JSON and Bicep for templates.

Bicep automatically manages dependencies between resources. You can avoid setting `dependsOn` when the symbolic name of a resource is used in another resource declaration.

The structure of the Bicep file is more flexible than a JSON template. You can declare parameters, variables, and outputs anywhere in the file. In JSON, you have to declare all parameters, variables, and outputs within the corresponding sections of the template.

## Get support

Here are the steps for opening a support ticket for Azure Resource Manager (ARM) template related issues:

- Open the Azure portal.

- Select the Support + Troubleshooting icon from the upper right corner.

- Under Briefly describe the issue heading, enter ARM template, and then select Go.

- In Which service are you having an issue with?, select Portal under Monitoring & Management, and then select Next.

- Select a subscription, and then select Next.

- Select Issue with ARM templates, and then select Next.

## Contribute to Bicep

Bicep is an open-source project. That means you can contribute to Bicep's development, and participate in the broader Bicep community. The contribution types include:

- Azure Quickstart Templates. You can contribute example Bicep files and ARM templates to the Azure Quickstart Templates repository. For more information, see the Azure Quickstart Templates contribution guide.

- Documentation. Bicep's documentation is open to contributions, too. For more information, see our contributor guide overview.

- Snippets. Do you have a favorite snippet you think the community would benefit from? You can add it to the Visual Studio Code extension's collection of snippets. For more information, see Contributing to Bicep.

- Code changes. If you're a developer and you have ideas you'd like to see in the Bicep language or tooling, you can contribute a pull request. For more information, see Contributing to Bicep.

## Next steps

- To get started, see the Quickstart: Create Bicep files with Visual Studio Code.

- For answers to common questions, see Frequently asked questions for Bicep.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-01-08
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
