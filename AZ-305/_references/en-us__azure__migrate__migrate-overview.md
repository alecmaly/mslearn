# https://learn.microsoft.com/en-us/azure/migrate/migrate-overview

Source: https://learn.microsoft.com/en-us/azure/migrate/migrate-overview

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
 

 

 

 

 
 
# What is Azure Catalyst (formerly Azure Migrate)?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Catalyst (formerly Azure Migrate) is a service that helps you decide on, plan, and execute your migration to Azure. Azure Catalyst helps you find the best migration path, assess for Azure readiness and cost of hosting workloads on Azure, and perform the migration with minimal downtime and risk. Azure Catalyst provides support for servers, databases, web apps, virtual desktops, and large-scale offline migration by using Azure Data Box.

Note

Azure Migrate Classic is the classic Azure Migrate experience where you can discover, plan, and migrate workloads. This view doesn't support application and cross-workload views.

For more information on migrating or modernizing multi-tier applications using Azure Catalyst and how it simplifies planning and execution, see the Microsoft Community Hub blog.

## Azure Catalyst agent

Azure Catalyst contains the Azure Catalyst agent (formerly Azure Copilot Migration Agent) (preview), a planning-focused experience that helps you analyze and plan migrations using your Azure Catalyst project data. The agent provides a conversational interface to explore discovered inventory, assess Azure readiness, compare migration strategies, review business case insights, and create or download customized landing zone templates. It complements Azure Catalyst by helping you interpret discovery and assessment results and generate planning-level recommendations. Migration execution continues in the Azure Catalyst portal. Learn more.

## Benefits of Azure Catalyst

Azure Catalyst offers these benefits for your cloud migration journey:

- Unified migration platform: You use a single portal to start, run, and track your migration to Azure. The unified platform supports discovery, assessment, and migration of variety of workloads, like servers, databases, and web applications.

- Free service: Azure Catalyst is a free service that you can use to:

- Identify your inventory of workloads.

- Assess workloads for multiple infrastructure as a service (IaaS) and platform as a service (PaaS) Azure targets.

- Develop a plan for migration.

- Migrate the workloads by using in-product, Microsoft, and partner migration tools. (Partner tools might charge you for using their services.)

- Range of tools: Azure Catalyst provides tools for assessment and migration.

- Assessment, migration, and modernization: In the Azure Catalyst hub, you can assess, migrate, and modernize:

- Servers: Assess on-premises servers and migrate them to Azure.

- Databases: Assess on-premises SQL Server instances and databases to migrate them to a SQL server on an Azure VM, an Azure SQL managed instance, or an Azure SQL database.

- Web applications: Assess on-premises web apps and migrate them to Azure App Service and Azure Kubernetes Service.

- Data: Migrate large amounts of data to Azure quickly and cost-effectively by using Azure Data Box products.

For information about Azure Catalyst availability across Azure regions, see Supported regions for Azure Catalyst.

## Migration phases

Azure Catalyst provides a simplified migration, modernization, and optimization service for customers who want to migrate their on-premises workloads to Azure. It gives you a one-stop solution for migrating your infrastructure, data, and web application workloads.

A general migration journey includes the following phases. Azure Catalyst provides support at each phase.

Watch this video to learn how Azure Catalyst delivers enhanced experiences. It helps you identify and visualize workloads, estimate cost savings, create high-fidelity migration plans, and confidently migrate complex environments.

Important

For the required Azure Migrate builtâin roles and permission details to create a project and run discovery, assessments, and migrations, see Prepare Azure accounts for Azure Catalyst.

### Decide

The first step in a migration journey is to identify your workloads. This process of identification is called discovery. To discover your workloads, you can deploy a lightweight Azure Migrate appliance (recommended approach), deploy Azure Migrate collector or quickly import the inventory data for your workloads.

The Azure Migrate appliance is a virtual appliance you can deploy on a server in your datacenter. The appliance collects the configuration and performance data for your servers and continually sends it to the Azure Catalyst service.

Azure Migrate Collector

Azure Migrate Collector enables a quick snapshot discovery of your on-premises environment without requiring continuous Azure connectivity. This mode supports discovery in air-gapped or restricted networks where deploying an appliance isn't feasible. Learn more.

After you identify the inventory of workloads, you can create a business case to make your decision to migrate your on-premises workloads to Azure. A business case helps you estimate the costs and savings of moving to Azure. It helps you identify:

- Total cost of ownership for on-premises versus Azure.

- Year-over-year comparison of cash flows.

- Resource utilization-based insights on Azure targets.

- Long-term cost reduction by switching from a capital expenditure (CapEx) model to an operating expenditure (OpEx) model.

Learn more about business cases.

### Plan

After you make the decision to migrate to Azure, the next important phase of migration is planning. To plan migration in detail, use Azure Migrate assessments to find:

- Azure readiness: Assess whether on-premises servers, SQL servers, and web apps are ready for migration to Azure.

- Right-sizing: Estimate the size of Azure virtual machines (VMs), the Azure SQL configuration, and the number of Azure VMware Solution nodes after migration.

- Azure cost estimation: Estimate costs for running on-premises servers in Azure.

- Dependency analysis: Understand the network dependencies between servers in your datacenter so that you can make high-confidence migration plans without missing any critical dependency. Learn more about dependency analysis.

### Execute

In the execution phase, you perform the migration or modernization of your workloads to move to Azure. You can use the Azure Catalyst service or partner tools to migrate your servers, databases, web apps, or virtual desktops with minimal downtime and risk.

You can migrate the following workloads by using the integrated Azure Migrate and Modernize tool:

Workload
Details

On-premises VMware VMs
Migrate VMs to Azure by using agentless or agent-based migration.

For agentless migration, the Azure Migrate and Modernize tool uses the same appliance that's used for discovery and assessment of servers.

For agent-based migration, the Azure Migrate and Modernize tool uses a replication appliance.

On-premises Hyper-V VMs
Migrate VMs to Azure.

The Azure Migrate and Modernize tool uses provider agents installed on a Hyper-V host for the migration.

On-premises physical servers or servers hosted on other clouds
Migrate physical servers to Azure. You can also migrate other virtualized servers, and VMs from other public clouds, by treating them as physical servers for the purpose of migration. The Azure Migrate and Modernize tool uses a replication appliance for the migration.

Web apps hosted on Windows in a VMware environment
Perform agentless migration of ASP.NET web apps at scale to Azure App Service by using Azure Catalyst.

For detailed information on how to migrate servers to Azure, see Tutorial: Migrate VMware. This tutorial is a step-by-step walkthrough of discovering VMware virtual machines, assessing their readiness for Azure, and performing replication and migration by using Azure Catalyst.

## Integrated tools and features

Azure Migrate includes the following integrated tools:

Tool
Function
Details

Discovery and Assessment
Discover and assess servers, including servers for SQL and web apps.
Discover and assess on-premises servers running on VMware, Hyper-V, and physical servers in preparation for migration to Azure.

Migrate and Modernize
Migrate servers.
Migrate VMware VMs, Hyper-V VMs, physical servers, other virtualized servers, and public cloud VMs to Azure.

Data Migration Assistant
Assess SQL Server databases for migration to Azure SQL Database, Azure SQL Managed Instance, or Azure VMs running SQL Server.
Data Migration Assistant is a standalone tool to assess SQL servers. It helps pinpoint potential problems that block migration. It finds unsupported features, new features that can benefit you after migration, and the right path for database migration. Learn more.

Azure Database Migration Service
Migrate on-premises databases to Azure VMs running SQL Server, Azure SQL Database, or Azure SQL Managed Instance.
Learn more about Database Migration Service.

Azure App Service Migration Assistant
Assess on-premises web apps and migrate them to Azure.
Azure App Service Migration Assistant is a standalone tool to assess on-premises websites for migration to Azure App Service.

Use Migration Assistant to migrate .NET and PHP web apps to Azure. Learn more.

Azure Data Box
Migrate offline data.
Use Azure Data Box products to move large amounts of offline data to Azure. Learn more.

Movere
Discover and assess on-premises workloads.
This tool is retired. Use Azure Migrate for your migration journey.

The following features from software development companies (SDCs) are integrated into Azure Migrate:

SDC
Function of feature

Carbonite
Migrate servers.

Cloudamize
Assess servers.

CloudSphere
Assess servers.

Corent
Assess and migrate servers.

Device42
Assess servers.

Lakeside
Assess virtual desktop infrastructure.

RackWare
Migrate servers.

Turbonomic
Assess servers.

CloudRecon
Assess servers and databases.

Zerto
Migrate servers.

For detailed capabilities and latest updates, see What's new.

## Related content

- Try tutorials to discover VMware VMs, Hyper-V VMs, or physical servers.

- Review frequently asked questions about Azure Migrate.

- Learn about the Azure VMware Solution landing zone accelerator.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-17
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
