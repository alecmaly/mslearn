# https://learn.microsoft.com/en-us/azure/azure-arc/overview

Source: https://learn.microsoft.com/en-us/azure/azure-arc/overview

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
 

 

 

 

 
 
# Azure Arc overview

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Today, companies struggle to control and govern increasingly complex environments that extend across data centers, multiple clouds, and edge. Each environment and cloud possesses its own set of management tools, and new DevOps and ITOps operational models can be hard to implement across resources.

Azure Arc simplifies governance and management by delivering a consistent multicloud and on-premises management platform.

Azure Arc provides a centralized, unified way to:

- Manage your entire environment together by projecting your existing non-Azure and/or on-premises resources into Azure Resource Manager.

- Manage virtual machines, Kubernetes clusters, and databases as if they are running in Azure.

- Use familiar Azure services and management capabilities, regardless of where your resources live.

- Continue using traditional ITOps while introducing DevOps practices to support new cloud native patterns in your environment.

- Configure custom locations as an abstraction layer on top of Azure Arc-enabled Kubernetes clusters and cluster extensions.

To download architecture diagrams in high resolution, visit Jumpstart Gems.

Currently, Azure Arc allows you to manage the following resource types hosted outside of Azure:

- Servers and virtual machines: Manage Windows and Linux physical servers and virtual machines hosted outside of Azure. Provision, resize, delete, and manage virtual machines based on Azure Local and on VMware vCenter or System Center Virtual Machine Manager managed on-premises environments.

- Kubernetes clusters: Attach and configure Kubernetes clusters running anywhere, with multiple supported distributions.

- Azure data services: Run SQL Managed Instance on-premises, at the edge, and in public clouds using Kubernetes and the infrastructure of your choice.

- SQL Server: Extend Azure services to SQL Server instances hosted outside of Azure.

Note

For more information regarding the different services Azure Arc offers, see Choosing the right Azure Arc service for machines.

### Indirectly connected mode

As of September, 2025 indirectly connected mode is retired.

## Key features and benefits

Some of the key scenarios that Azure Arc supports are:

- Implement consistent inventory, management, governance, and security for servers across your environment.

- Configure Azure VM extensions to use Azure management services to monitor, secure, and update your servers.

- Manage and govern Kubernetes clusters at scale.

- Use GitOps to deploy configurations across one or more clusters from Git repositories.

- Zero-touch compliance and configuration for Kubernetes clusters using Azure Policy.

- Run Azure data services on any Kubernetes environment as if it runs in Azure (specifically Azure SQL Managed Instance, with benefits such as upgrades, updates, security, and monitoring). Use elastic scale and apply updates without any application downtime, even without continuous connection to Azure.

- Create custom locations on top of your Azure Arc-enabled Kubernetes clusters, using them as target locations for deploying Azure services instances. Deploy your Azure service cluster extensions for Azure Arc-enabled data services, Azure Container Apps on Azure Arc, and Event Grid on Kubernetes.

- Perform virtual machine lifecycle and management operations on Azure Local and on-premises environments managed by VMware vCenter and System Center Virtual Machine Manager (SCVMM) through interactive and non-interactive methods. Empower developers and application teams to self-serve VM operations on-demand using Azure role-based access control (RBAC).

- A unified experience viewing your Azure Arc-enabled resources, whether you are using the Azure portal, the Azure CLI, Azure PowerShell, or Azure REST API.

## Pricing

Below is pricing information for the features available today with Azure Arc.

### Azure Arc-enabled servers

The following Azure Arc control plane functionality is offered at no extra cost:

- Resource organization through Azure management groups and tags

- Searching and indexing through Azure Resource Graph

- Access and security through Azure Role-based access control (RBAC)

- Environments and automation through templates and extensions

Any Azure service that is used on Azure Arc-enabled servers, such as Microsoft Defender for Cloud or Azure Monitor, will be charged as per the pricing for that service. For more information, see the Azure pricing page.

### Azure Arc-enabled VMware vSphere and System Center Virtual Machine Manager

The following Azure Arc-enabled VMware vSphere and System Center Virtual Machine Manager (SCVMM) capabilities are offered at no extra cost:

- All the Azure Arc control plane functionalities that are offered at no extra cost with Azure Arc-enabled servers.

- Discovery and single pane of glass inventory view of your VMware vCenter and SCVMM managed estate (VMs, templates, networks, datastores, clouds/clusters/hosts/resource pools).

- Lifecycle (create, resize, update, and delete) and power cycle (start, stop, and restart) operations of VMs, including the ability to delegate self-service access for these operations using Azure role-based access control (RBAC).

- Management of VMs using Azure portal, CLI, REST APIs, SDKs, and automation through Infrastructure as Code (IaC) templates such as ARM, Terraform, and Bicep.

Any Azure service that is used on Azure Arc-enabled VMware vSphere and SCVMM VMs, such as Microsoft Defender for Cloud or Azure Monitor, will be charged as per the pricing for that service. For more information, see the Azure pricing page.

### Azure Arc-enabled Kubernetes

Any Azure service that is used on Azure Arc-enabled Kubernetes, such as Microsoft Defender for Cloud or Azure Monitor, will be charged as per the pricing for that service.

For more information on pricing for configurations on top of Azure Arc-enabled Kubernetes, see the Azure pricing page.

### Azure Arc-enabled data services

For information, see the Azure pricing page.

## Azure Arc and the adaptive cloud approach

Azure Arc is a key part of Microsoftâs adaptive cloud approach. This approach helps organizations run and manage apps and services across many environments, including Azure, other cloud providers, on-premises datacenters, and edge locations. Azure Arc supports this approach by extending Azureâs management, security, and governance tools to resources outside Azure. This ability makes it easier to keep operations consistent and secure, no matter where your workloads run.

## Next steps

- Choose the right Azure Arc service for your physical and virtual machines.

- Learn about Azure Arc-enabled servers.

- Learn about Azure Arc-enabled Kubernetes.

- Learn about Azure Arc-enabled data services.

- Learn about SQL Server enabled by Azure Arc.

- Learn about Azure Arc-enabled VM Management on Azure Local.

- Learn about Azure Arc-enabled VMware vSphere.

- Learn about Azure Arc-enabled System Center Virtual Machine Manager.

- Experience Azure Arc by exploring the Azure Arc Jumpstart.

- Learn about best practices and design patterns through the Azure Arc Landing Zone Accelerators.

- Understand network requirements for Azure Arc.

 
 

 
 

 

 
 
 
 
 
 
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
 2025-08-26
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
