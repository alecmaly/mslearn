# https://learn.microsoft.com/en-us/azure/azure-app-configuration/overview

Source: https://learn.microsoft.com/en-us/azure/azure-app-configuration/overview

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
 

 

 

 

 
 
# What is Azure App Configuration?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure App Configuration provides a service to centrally manage application settings and feature flags. Modern programs, especially programs running in a cloud, generally have many components that are distributed in nature. Spreading configuration settings across these components can lead to hard-to-troubleshoot errors during an application deployment. Use App Configuration to store all the settings for your application and secure their accesses in one place.

## Why use App Configuration?

Cloud-based applications often run on multiple virtual machines or containers in multiple regions and use multiple external services. Creating a robust and scalable application in a distributed environment presents a significant challenge.

Various programming methodologies help developers deal with the increasing complexity of building applications. For example, the Twelve-Factor App describes many well-tested architectural patterns and best practices for use with cloud applications. One key recommendation from this guide is to separate configuration from code. An applicationâs configuration settings should be kept external to its executable and read in from its runtime environment or an external source.

While any application can make use of App Configuration, the following examples are the types of application that benefit from the use of it:

- Microservices based on Azure Kubernetes Service, Azure Service Fabric, or other containerized apps deployed in one or more geographies

- Serverless apps, which include Azure Functions or other event-driven stateless compute apps

- Continuous deployment pipeline

App Configuration offers the following benefits:

- A fully managed service that can be set up in minutes

- Flexible key representations and mappings

- Tagging with labels

- Point-in-time replay of settings

- Dedicated UI for feature flag management

- Comparison of two sets of configurations on custom-defined dimensions

- Enhanced security through Azure-managed identities

- Encryption of sensitive information at rest and in transit

- Native integration with popular frameworks

App Configuration complements Azure Key Vault, which is used to store application secrets. App Configuration makes it easier to implement the following scenarios:

- Centralize management and distribution of hierarchical configuration data for different environments and geographies

- Dynamically change application settings without the need to redeploy or restart an application

- Control feature availability in real-time

## Use App Configuration

The easiest way to add an App Configuration store to your application is through a client library provided by Microsoft. The following methods are available to connect with your application, depending on your chosen language and framework.

Programming language and framework
How to connect
Quickstart

.NET
App Configuration provider for .NET
.NET quickstart

ASP.NET Core
App Configuration provider for .NET
ASP.NET Core quickstart

.NET Framework and ASP.NET
App Configuration builder for .NET
.NET Framework quickstart

Java Spring
App Configuration provider for Spring Cloud
Java Spring quickstart

JavaScript/Node.js
App Configuration provider for JavaScript
JavaScript/Node.js quickstart

Python
App Configuration provider for Python
Python quickstart

Go
App Configuration provider for Go
Go quickstart

Other
App Configuration REST API
None

## Next steps

Best practices

FAQ

Create an App Configuration store

 
 

 
 

 

 
 
 
 
 
 
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
 2025-11-21
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
