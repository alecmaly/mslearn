# https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/overview

Source: https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/overview

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
 

 

 

 

 
 
# What are ARM templates?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 With the move to the cloud, many teams adopted agile development methods. These teams iterate quickly. They need to repeatedly deploy their solutions to the cloud, and know their infrastructure is in a reliable state. As infrastructure became part of the iterative process, the division between operations and development disappeared. Teams need to manage infrastructure and application code through a unified process.

To meet these challenges, automate deployments and use the practice of infrastructure as code. In code, you define the infrastructure that needs to be deployed. The infrastructure code is part of your project. Just like application code, store the infrastructure code in a source repository and version it. Anyone on your team can run the code and deploy similar environments.

To implement infrastructure as code for your Azure solutions, use Azure Resource Manager templates (ARM templates). The template is a JavaScript Object Notation (JSON) file that defines the infrastructure and configuration for your project. The template uses declarative syntax, which lets you state what you intend to deploy without having to write the sequence of programming commands to create it. In the template, you specify the resources to deploy and the properties for those resources. You can also specify in which resource group those resources are deployed.

Tip

We introduced a new language named Bicep that offers the same capabilities as ARM templates but with a syntax that's easier to use. Each Bicep file is automatically converted to an ARM template during deployment. If you're considering infrastructure as code options, we recommend looking at Bicep. For more information, see What is Bicep?

## Why choose ARM templates?

If you're trying to decide between using ARM templates and one of the other infrastructure as code services, consider the following advantages of using templates:

- Declarative syntax: ARM templates allow you to create and deploy an entire Azure infrastructure declaratively. For example, you can deploy not only virtual machines, but also the network infrastructure, storage systems, and any other resources you need.

- Repeatable results: Repeatedly deploy your infrastructure throughout the development lifecycle and have confidence your resources are deployed in a consistent manner. Templates are idempotent, which means you can deploy the same template many times and get the same resource types in the same state. You can develop one template that represents the desired state, rather than developing lots of separate templates to represent updates. For example, the following file creates a storage account. If you deploy this template and the storage account with the specified properties already exists, no changes are made.

`{
 "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
 "contentVersion": "1.0.0.0",
 "parameters": {
 "location": {
 "type": "string",
 "defaultValue": "[resourceGroup().location]"
 }
 },
 "resources": [
 {
 "type": "Microsoft.Storage/storageAccounts",
 "apiVersion": "2025-06-01",
 "name": "mystorageaccount",
 "location": "[parameters('location')]",
 "sku": {
 "name": "Standard_LRS"
 },
 "kind": "StorageV2"
 }
 ]
}
`

- Orchestration: You don't have to worry about the complexities of ordering operations. Resource Manager orchestrates the deployment of interdependent resources so they're created in the correct order. When possible, Resource Manager deploys resources in parallel, so your deployments finish faster than serial deployments. You deploy the template through one command, rather than through multiple imperative commands.

- Modular files: You can break your templates into smaller, reusable components and link them together at deployment time. You can also nest one template inside another template.

- Create any Azure resource: You can immediately use new Azure services and features in templates. As soon as a resource provider introduces new resources, you can deploy those resources through templates. You don't have to wait for tools or modules to be updated before using the new services.

- Extensibility: With deployment scripts, you can add PowerShell or Bash scripts to your templates. The deployment scripts extend your ability to set up resources during deployment. You can include a script in the template or store it in an external source and reference it in the template. With deployment scripts, you can complete your end-to-end environment setup in a single ARM template.

- Testing: To ensure your template follows recommended guidelines, test it with the ARM template tool kit (arm-ttk). This test kit is a PowerShell script that you can download from GitHub. The tool kit makes it easier for you to develop expertise using the template language.

- Preview changes: Use the what-if operation to preview changes before deploying the template. With what-if, you see which resources to create, update, or delete, and any resource properties to change. The what-if operation checks the current state of your environment and eliminates the need to manage state.

- Built-in validation: Your template is deployed only after passing validation. Resource Manager checks the template before starting the deployment to make sure it succeeds. Your deployment is less likely to stop in a half-finished state.

- Tracked deployments: In the Azure portal, you can review the deployment history and get information about the template deployment. You can see the template that was deployed, the parameter values passed in, and any output values. Other infrastructure as code services aren't tracked through the portal.

- Policy as code: Azure Policy is a policy as code framework to automate governance. If you're using Azure policies, policy remediation is done on noncompliant resources when deployed through templates.

- Deployment Blueprints: You can take advantage of Blueprints provided by Microsoft to meet regulatory and compliance standards. These blueprints include prebuilt templates for various architectures.

- CI/CD integration: You can integrate templates into your continuous integration and continuous deployment (CI/CD) tools. This integration automates your release pipelines for fast and reliable application and infrastructure updates. By using Azure DevOps and Resource Manager template task, you can use Azure Pipelines to continuously build and deploy ARM template projects. To learn more, see VS project with pipelines and Tutorial: Continuous integration of Azure Resource Manager templates with Azure Pipelines.

- Exportable code: You can get a template for an existing resource group by either exporting the current state of the resource group or viewing the template used for a particular deployment. Viewing the exported template is a helpful way to learn about the template syntax.

- Authoring tools: You can author templates with Visual Studio Code and Visual Studio.

## Template file

Within your template, you can write template expressions that extend the capabilities of JSON. These expressions use the functions that Resource Manager provides.

The template has the following sections:

- Parameters - Provide values during deployment that you customize for different environments when using the same template.

- Variables - Define values that you reuse in your templates. You can construct them from parameter values.

- User-defined functions - Create customized functions that simplify your template.

- Resources - Specify the resources to deploy.

- Outputs - Return values from the deployed resources.

## Template deployment process

When you deploy a template, Resource Manager converts the template into REST API operations. For example, when Resource Manager receives a template with the following resource definition:

`"resources": [
 {
 "type": "Microsoft.Storage/storageAccounts",
 "apiVersion": "2025-06-01",
 "name": "mystorageaccount",
 "location": "centralus",
 "sku": {
 "name": "Standard_LRS"
 },
 "kind": "StorageV2"
 },
]
`

It converts the definition to the following REST API operation, which it sends to the Microsoft.Storage resource provider:

`PUT
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/mystorageaccount?api-version=2022-09-01
REQUEST BODY
{
 "location": "centralus",
 "sku": {
 "name": "Standard_LRS"
 },
 "kind": "StorageV2",
 "properties": {}
}
`

Notice that the apiVersion you set in the template for the resource is used as the API version for the REST operation. You can repeatedly deploy the template and have confidence it continues to work. By using the same API version, you don't have to worry about breaking changes that might be introduced in later versions.

To deploy a template, use any of the following options:

- Azure portal

- Azure CLI

- PowerShell

- REST API

- Button in GitHub repository

- Azure Cloud Shell

## Template design

Define templates and resource groups based on how you want to manage your solution. For example, you can deploy your three-tier application through a single template to a single resource group.

You don't have to define your entire infrastructure in a single template. Often, it makes sense to divide your deployment requirements into a set of targeted, purpose-specific templates. You can easily reuse these templates for different solutions. To deploy a particular solution, create a main template that links all the required templates. The following image shows how to deploy a three-tier solution through a parent template that includes three nested templates.

If you envision your tiers having separate lifecycles, you can deploy your three tiers to separate resource groups. The resources can still be linked to resources in other resource groups.

For information about nested templates, see Using linked templates with Azure Resource Manager.

## Share templates

After creating your template, you might want to share it with other users in your organization. Template specs enable you to store a template as a resource type. Use role-based access control to manage access to the template spec. Users with read access to the template spec can deploy it, but not change the template.

This approach means you can safely share templates that meet your organization's standards.

## Get support

Here are the steps for opening a support ticket for Azure Resource Manager (ARM) template related issues:

- Open the Azure portal.

- Select the Support + Troubleshooting icon from the upper right corner.

- Under Briefly describe the issue heading, enter ARM template, and then select Go.

- In Which service are you having an issue with?, select Portal under Monitoring & Management, and then select Next.

- Select a subscription, and then select Next.

- Select Issue with ARM templates, and then select Next.

## Next steps

- For a step-by-step tutorial that guides you through the process of creating a template, see Tutorial: Create and deploy your first ARM template.

- To learn about ARM templates through a guided set of Learn modules, see Deploy and manage resources in Azure by using ARM templates.

- For information about the properties in template files, see Understand the structure and syntax of ARM templates.

- To learn about exporting templates, see Quickstart: Create and deploy ARM templates by using the Azure portal.

- For answers to common questions, see Frequently asked questions about ARM templates.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-06-26
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
