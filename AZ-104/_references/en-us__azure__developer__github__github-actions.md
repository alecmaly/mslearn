# https://learn.microsoft.com/en-us/azure/developer/github/github-actions

Source: https://learn.microsoft.com/en-us/azure/developer/github/github-actions

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
 

 

 

 

 
 
# What is GitHub Actions for Azure

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 GitHub Actions helps you automate your software development workflows from within GitHub. You can deploy workflows in the same place where you store code and collaborate on pull requests and issues.

In GitHub Actions, a workflow is an automated process that you set up in your GitHub repository. You can build, test, package, release, or deploy any project on GitHub with a workflow.

Each workflow is made up of individual actions that run after a specific event (like a pull request) occur. The individual actions are packaged scripts that automate software development tasks.

With GitHub Actions for Azure, you can create workflows that you can set up in your repository to build, test, package, release, and deploy to Azure. GitHub Actions for Azure supports Azure services, including Azure App Service, Azure Functions, and Azure Key Vault.

GitHub Actions also include support for utilities, including Azure Resource Manager templates, Azure CLI, and Azure Policy.

Watch this video from GitHub Universe 2020 to learn more about continuous delivery with GitHub Actions.

## Why should I use GitHub Actions for Azure

Microsoft developed GitHub Actions for Azure and designed them be used with Azure. You can see all of the GitHub Actions for Azure in the GitHub Marketplace. See Finding and customizing actions to learn more about incorporating actions into your workflows.

## What is the difference between GitHub Actions and Azure Pipelines

Azure Pipelines and GitHub Actions both help you automate software development workflows. Learn more about how the services differ and how to migrate from Azure Pipelines to GitHub Actions.

## What do I need to use GitHub Actions for Azure

You'll need Azure and GitHub accounts:

- An Azure account with an active subscription. Create an account for free.

- A GitHub account. If you don't have one, sign up for free.

## How do I connect GitHub Actions and Azure

Depending on the action, you can use service principal or publish profile to connect to Azure from GitHub. You'll use a service principal each time you use the Azure login action. When you use a service principal you can use OpenID Connect or a secret.

The Azure App Service action supports using a publish profile or service principal. See Application and service principal objects in Microsoft Entra ID to learn more about service principals.

You can use the Azure login action in combination with both the Azure CLI and Azure Azure PowerShell actions. The Azure login action also works with most other GitHub actions for Azure including deploying to web apps. You can also use Azure login with community-contributed actions like Enhanced Azure key vault that aren't officially supported by Microsoft.

## What is included in a GitHub Actions workflow

Workflows are made up of one or more jobs. Within a job, there are steps made up of individual actions. See Introduction to GitHub Actions to learn more about GitHub Actions concepts.

## Where can I see complete workflow examples

The Azure starter action workflows repository includes end-to-end workflows to build and deploy Web apps of any language, any ecosystem to Azure.

## Where can I see all the available actions

Visit the Marketplace for GitHub Actions for Azure to see all the available GitHub Actions for Azure.

- Azure Spring Cloud

- Deploy Bicep file or Azure Resource Manager template

- Deploy to a static web app

- Azure App Service settings

- Deploy to Azure Functions

- Deploy to Azure Functions for Containers

- Docker login

- Deploy to Azure Container Instances

- Container scanning action

- Kubectl tool installer

- Kubernetes set context

- AKS set context

- Kubernetes create secret

- Kubernetes deploy

- Setup Helm

- Kubernetes bake

- Build Azure virtual machine images

- Machine learning login

- Machine learning training

- Machine learning - deploy model

- Deploy to Azure SQL database

- Deploy to Azure MySQL action

- Azure Policy Compliance Scan

- Manage Azure Policy

- Trigger an Azure Pipelines run

 
 

 
 

 

 
 
 
 
 
 
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
 2024-03-13
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
