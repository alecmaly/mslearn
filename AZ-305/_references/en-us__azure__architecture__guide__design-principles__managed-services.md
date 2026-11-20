# https://learn.microsoft.com/en-us/azure/architecture/guide/design-principles/managed-services

Source: https://learn.microsoft.com/en-us/azure/architecture/guide/design-principles/managed-services

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
 

 

 

 

 
 
# Use platform as a service (PaaS) options

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Infrastructure as a service (IaaS) and platform as a service (PaaS) are cloud service models.

IaaS offers access to computing resources like servers, storage, and networks. The IaaS provider hosts and manages this infrastructure. Customers use the internet to access the hardware and resources.

In contrast, PaaS provides a framework for developing and running apps. As with IaaS, the PaaS provider hosts and maintains the platform's servers, networks, storage, and other computing resources. But PaaS also includes tools, services, and systems that support the web application lifecycle. Developers use the platform to build apps without having to manage backups, security solutions, upgrades, and other administrative tasks.

## Advantages of PaaS over IaaS

When your workload doesn't require the control granted by IaaS, use PaaS instead. IaaS is like having a box of parts. You can build anything, but you have to assemble it yourself. PaaS options are easier to configure and administer. You don't need to set up virtual machines (VMs). You also don't have to handle all of the component's maintenance tasks, such as installing patches and updates.

Many PaaS solutions offer a native scaling option that allow you to configure how the service will scale in and out or up and down. While scaling is possible in IaaS, it often comes with added complexity, such as dealing with attached storage.

For example, suppose your application needs a message queue. You can set up your own messaging service on a virtual machine by using something like RabbitMQ. But Azure Service Bus provides a reliable messaging service, and it's simpler to maintain. You can create a Service Bus namespace as part of a deployment script. Then you can use a client SDK to call Service Bus.

## PaaS alternatives to IaaS solutions

Your application might have specific requirements that make IaaS a more suitable approach than PaaS. But you can still look for places to incorporate PaaS options. A few examples include caches, queues, and data storage. The following table provides other examples.

Instead of running ...
Consider using ...

Active Directory
Microsoft Entra ID

Elasticsearch
Azure AI Search

Hadoop
Azure HDInsight

IIS
Azure App Service

MongoDB
Azure DocumentDB

Redis
Azure Managed Redis

SQL Server
Azure SQL Database

File share
Azure Files

This list isn't exhaustive. There are many ways that you can exchange self-managed, IaaS technologies for related PaaS solutions.

 
 

 
 

 

 
 
 
 
 
 
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
 2025-12-03
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
