# https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone

Source: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone

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
 

 

 

 

 
 
# What is an Azure landing zone?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 The Ready phase of the Cloud Adoption Framework helps you design your Azure landing zone to meet your organization's requirements. An Azure landing zone is a proven and flexible architecture for governing, securing, and scaling a multi-subscription Azure environment. An Azure landing zone consists of two components:

- Platform landing zone: The centralized foundation that establishes governance, security, and shared resources for all your Azure workloads.

- Workload landing zones: The environments where workload teams deploy and operate workload resources within the guardrails of the platform landing zone. A workload is a collection of Azure resources, code, AI models, data, and infrastructure that work together to achieve a defined business outcome.

You can implement each component of your Azure landing zone in one of two ways:

- Accelerators: Microsoft-provided accelerators for both platform landing zone and workload landing zone scenarios use infrastructure as code to deploy Azure environments based on recommended practices.

- Custom build: You design and build the solution internally or with support from Microsoft or Microsoft partners.

For most organizations, accelerators provide the fastest path to a deployment that aligns with Microsoft's recommended practices.

## Azure landing zone architecture

Every Azure landing zone starts with the platform landing zone. Before you build a platform landing zone, define organizational requirements across the Azure landing zone design areas. These decisions determine how you design your Azure landing zone.

### Conceptual architectures

Conceptual architecture diagrams help you understand the core components of an Azure landing zone and how they work together. Start with these diagrams to understand the relationship between the platform landing zone, workload landing zones, and Microsoft solutions.

- 
Conceptual

- 
Conceptual + enterprise integration

- 
Detailed conceptual

- 
Detailed conceptual + enterprise integration

Layered architecture diagram. A top banner labeled "Unified identity, security, and governance" contains Microsoft Agent 365, Microsoft Defender, Microsoft Entra, and Microsoft Purview. Below, a large Azure landing zone box contains a platform landing zone centered above a workload landing zones section. The workload landing zones section contains three workload landing zone boxes representing Azure workloads. Beneath the workloads, a Microsoft Foundry and Foundry IQ box connects by dashed arrows to the workload landing zones, indicating optional AI capabilities for selected workloads.

Conceptual Azure landing zone architecture. Download a PowerPoint file of this architecture.

Beneath the Azure landing zone, Microsoft Copilot Studio, Microsoft Fabric, and Microsoft 365 are shown as integrated business, data, and AI solutions. At the bottom, data sources including on-premises systems, Dataverse, Microsoft 365, Azure workloads, and other clouds connect to these solutions. Bidirectional arrows indicate integration between data sources, Microsoft platforms, and Azure workloads.

Conceptual Azure landing zone architecture plus enterprise integration with Microsoft solutions. Download a PowerPoint file of this architecture.

The Workload landing zones section shows how workloads are organized under the Azure landing zone architecture. Workloads are grouped into Internal, Online, and Local categories. Each workload receives a dedicated workload landing zone that contains all environments associated with that workload. Typical environments include development, test, and production, with each environment consisting of one or more Azure subscriptions. Internal workload examples include a Microsoft Fabric compute landing zone and a data and AI workload landing zone that uses services such as Azure Machine Learning, Azure Databricks, AI on Azure Infrastructure, and Azure Data Lake Storage. The diagram also shows that Microsoft Foundry resources can be added to workload environments where AI capabilities are required. Workload teams manage the workload landing zones, which remain separate from the platform landing zone managed by platform teams.

Detailed conceptual Azure landing zone architecture. Download a PowerPoint file of this architecture.

Beneath the Azure landing zone, Microsoft Copilot Studio, Microsoft Fabric, and Microsoft 365 are shown as integrated business, data, and AI solutions. At the bottom, data sources including on-premises systems, Dataverse, Microsoft 365, Azure workloads, and other clouds connect to these solutions. Bidirectional arrows indicate integration between data sources, Microsoft platforms, and Azure workloads.

Detailed conceptual Azure landing zone architecture plus enterprise integration with Microsoft solutions. Download a PowerPoint file of this architecture.

### Reference architectures

Reference architecture diagrams show recommended Azure landing zone implementation patterns and deployment models. Use these diagrams to understand how management groups, subscriptions, networking, and governance controls are organized in hub-and-spoke, Azure Virtual WAN, and other architecture designs.

- 
Hub-Spoke

- 
Virtual WAN

- 
Management group hierarchy

- 
Platform vs. workload landing zones

Around the middle are individual subscriptions as boxes. Security and Management subscriptions (D, upper left) contain Log Analytics workspaces, Microsoft Sentinel, and dashboards. The Identity subscription holds virtual networks with domain services and Recovery Services vaults. The Connectivity subscription (E) contains Azure DDoS Protection, Azure DNS, VPN/ExpressRoute gateways, Azure Firewall, and peered hub virtual networks across two regions. Workload landing zone A2 and P1 subscriptions (F) hold application virtual networks, resource groups, and workload resources (G) and a Sandbox subscription (H) at right. Each subscription repeats a common toolset row: Action Groups, Alerts, Cost Management, Role assignment, Policy assignment, Network Watcher, Defender for Cloud, and Azure Update Manager.

Azure landing zone reference architecture showing a hub & spoke networking topology. Download a Visio file or PDF file of this architecture.

Around the middle are individual subscriptions as boxes. Security and Management subscriptions (D, upper left) contain Log Analytics workspaces, Microsoft Sentinel, and dashboards. The Identity subscription holds virtual networks with domain services and Recovery Services vaults. The Connectivity subscription (E) contains Azure DDoS Protection, Azure DNS, Azure Firewall, and two Azure Virtual WAN hubs (Region 1 and Region N) with VPN/ExpressRoute gateways. VWAN Hub Connection lines link these hubs to the workload landing zone virtual networks. Workload landing zone A2 and P1 subscriptions (F) hold application virtual networks, resource groups, and workload resources (G) and a Sandbox subscription (H) at right. Each subscription repeats a common toolset row: Action Groups, Alerts, Cost Management, Role assignment, Policy assignment, Network Watcher, Defender for Cloud, and Azure Update Manager.

Azure landing zone reference architecture showing an Azure Virtual WAN networking topology. Download a Visio file or PDF file of this architecture.

In the Subscriptions band below, each management group links to its subscriptions. Security, Management, Identity, and Connectivity management groups each map to a matching subscription of the same name. Corp connects to the workload landing zone A1, Workload landing zone P1, and workload landing zone A2 subscriptions. Local connects to workload landing zone C1 subscription (Azure Local Clusters) and workload landing zone A1 subscription (Applications). Decommissioned maps to a Decommissioned subscription, and Sandbox maps to Sandbox subscription 1 and Sandbox subscription 2. The Online management group has no subscription shown beneath it.

Baseline Azure landing zone management group hierarchy. Download a Visio file of this architecture.

The central and upper structures remain unshaded, above is the the Enterprise Agreement/Microsoft Customer Agreement billing hierarchy (A), Identity and access management (B), Microsoft Entra ID with on-premises Active Directory Domain Services, and Git repository, boards, and pipelines.

Platform landing zone vs. workload landing zones in the Azure landing zone reference architecture. Download a Visio file or PDF file of this architecture.

## Platform landing zone

The platform landing zone establishes your organization's Azure foundation. It defines how you organize your Azure resources, enforce governance, and provide shared capabilities centrally. Most organizations should have only one platform landing zone per Microsoft Entra tenant.

A platform landing zone consists of a management group hierarchy and centralized resources (as needed). An important function of the platform is to have a way to distribute workload landing zones to workload teams.

- Management group hierarchy: The management group hierarchy provides the governance structure for the Azure environment. It organizes all of your Azure subscriptions and applies governance standards to those subscriptions. The hierarchy separates platform resources and workload resources. A well-designed hierarchy allows you to apply governance standards consistently without creating unnecessary administrative complexity.

- Centralized resources: Many organizations provide certain capabilities centrally so every workload can use the same approved services and standards. Common examples include connectivity and networking, security monitoring, Active Directory identity services, and management services. What you centralize depends on your requirements. Only centralize capabilities that provide clear governance, operational, or economic benefits across multiple workloads.

- Workload landing zone distribution: You need a repeatable process for requesting, creating, and distributing workload landing zones to workload teams. A standardized approach ensures every new workload landing zone follows your organization's governance and security baselines. You can do this process manually or automate it. As the number of workload landing zone requests grows, automation becomes increasingly important. See Subscription vending.

Implementation options: Microsoft provides several platform landing zone accelerators that implement recommended architecture patterns and organizational guardrails. See Platform landing zone implementation options. You can also develop your own implementation or work with Microsoft or Microsoft partners to build a customized platform landing zone.

## Workload landing zone

Each workload has a single workload landing zone. A workload landing zone contains all the environments required to support that workload, such as development, test, and production. Each environment consists of one or more Azure subscriptions based on workload requirements, team ownership boundaries, or Azure subscription limits. The workload landing zone includes all Azure resources that the workload team owns and operates across every environment.

Based on the requirements of the workload, the platform team places each workload landing zone subscription in either the Online, Internal ("Corp"), or Local management group under the "Workload landing zones" management group. Each subscription and its Azure resources inherit the governance and security policies from the Azure Policies applied to the management group hierarchy. This model provides consistent guardrails and allows flexibility to meet workload-specific requirements.

Implementation options: Microsoft provides several accelerators to deploy different types of workload landing zones. You can also implement your own approach or engage Microsoft or Microsoft partners for assistance. See the Azure Architecture Center for a list of workload landing zone accelerators.

## Technology adoption in an Azure landing zone

An Azure landing zone supports new and emerging technologies without requiring changes to the overall architecture. You deploy workload resources into workload landing zones regardless of workload type, such as AI. As new requirements emerge, you update the governance and security policies in the platform landing zone. Those policies are then applied consistently across workload landing zones, which helps you adopt new technologies faster and maintain consistency across all workloads of that type.

The Cloud Adoption Framework provides guidance for common adoption scenarios to help you prepare your people, processes, and platform for successful adoption. See Scenarios.

## Next steps

Design principles

 
 

 
 

 

 
 
 
 
 
 
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
 2026-10-01
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
