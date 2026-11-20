# https://learn.microsoft.com/en-us/azure/container-apps/overview

Source: https://learn.microsoft.com/en-us/azure/container-apps/overview

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
 

 

 

 

 
 
# Azure Container Apps overview

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Container Apps is a serverless platform for running containerized applications without managing the underlying infrastructure. Instead of configuring servers, orchestrating containers, and handling deployment details yourself, let Container Apps provide the up-to-date resources that keep your applications stable, secure, and scalable. This approach reduces operational overhead and helps you save on costs.

Common uses of Azure Container Apps include:

- Deploying API endpoints

- Hosting background processing jobs

- Handling event-driven processing

- Running microservices

Additionally, applications built on Azure Container Apps can dynamically scale based on the following characteristics:

- HTTP traffic

- Event-driven processing

- CPU or memory load

- Any KEDA-supported scaler

To begin working with Container Apps, select the description that best describes your situation.

Description
Resource

I'm new to containers
Start here if you have yet to build your first container but are curious how containers can serve your development needs.
Learn more about containers

I'm using serverless containers
Container Apps provides automatic scaling, reduces operational complexity, and allows you to focus on your application rather than infrastructure.

Start here if you're interested in the management, scalability, and pay-per-use features of cloud computing.
Learn more about serverless containers

## Features

With Azure Container Apps, you can:

- Use the Azure CLI extension, Azure portal or ARM templates to manage your applications.

- Enable HTTPS or TCP ingress without having to manage other Azure infrastructure.

- Build microservices with Dapr and access its rich set of APIs.

- Run jobs on-demand, on a schedule, or based on events.

- Run Azure Functions for event-driven scenarios using triggers, bindings, and automatic scaling.

- Use specialized hardware for access to increased compute resources.

- Run multiple container revisions and manage the container app's application lifecycle.

- Autoscale your apps based on any KEDA-supported scale trigger. Most applications can scale to zero1.

- Split traffic across multiple versions of an application for Blue/Green deployments and A/B testing scenarios.

- Use internal ingress and service discovery for secure internal-only endpoints with built-in DNS-based service discovery.

- Run containers from any registry, public or private, including Docker Hub and Azure Container Registry (ACR).

- Provide an existing virtual network when creating an environment for your container apps.

- Securely manage secrets directly in your application.

- Monitor logs using Azure Log Analytics.

- Generous quotas, which can be overridden to increase limits on a per-account basis.

1 Applications that scale on CPU or memory load can't scale to zero.

## Introductory video

## Next steps

Deploy your first container app

 
 

 
 

 

 
 
 
 
 
 
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
 2026-07-07
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
