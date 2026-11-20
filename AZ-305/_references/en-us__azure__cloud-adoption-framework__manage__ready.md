# https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/manage/ready

Source: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/manage/ready

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
 

 

 

 

 
 
# Ready your Azure cloud operations

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Managing your Azure environment isn't just about keeping the lights on. It's about maintaining governance and security while ensuring your cloud stays aligned with business goals over time. As your environment grows, you need to prevent configuration drift, improve deployments through infrastructure as code, and manage change effectively.

The Cloud Adoption Framework (CAF) Manage methodology introduces the RAMP approach (Ready, Administer, Monitor, Protect) to help you build these capabilities. RAMP provides a structured way to organize teams, define responsibilities, and implement the processes and tools that keep your Azure operations secure, compliant, and resilient. From day-to-day administration to monitoring health and protecting against disruptions, RAMP helps you establish a strong operational foundation for long-term success.

## Identify your management responsibilities

Effective Azure management spans two layers of accountability: central (platform) responsibilities and workload responsibilities. Central responsibilities apply across the entire cloud estate. Workload responsibilities focus on individual applications or services. Use Table 1 to ensure your operating model covers the essential areas of cloud management

Table 1. Primary cloud management responsibilities

Cloud management areas
Central (platform) responsibilities
Workload responsibilities

Compliance
âª Define operational procedures.
âª Enforce governance policies.
âª Monitor compliance and remediate or escalate as required.
âª Follow operational procedures.
âª Align design with governance policies.

Security
âª Manage organization-wide security operations.
âª Manage identities in Microsoft Entra ID.
âª Grant access to Azure subscriptions.
âª Define and maintain security baselines via Azure Policy and Microsoft Defender for Cloud.
âª Oversee threat protection and incident response integration with Microsoft Sentinel.
âª Implement secure workload design.
âª Respond to workload-specific security alerts and incidents.
âª Continuously assess vulnerabilities within the workload.

Resource management
âª Define and maintain resource hierarchy.
âª Create workload subscriptions as requested.
âª Define naming and tagging strategy.
âª Define network topology.
âª Configure shared networking (virtual network peering, on-premises connectivity).
âª Manage cross-workload or shared resources/services.
âª Monitor subscription limits and handle requests for quota increases.
âª Manage workload-specific subscriptions (if delegated).
âª Manage resource groups and resources for each workload.
âª Adhere to and apply naming and tagging standards.
âª Manage application-level resource utilization, ensuring resources remain within subscription quotas.

Deployment
âª Standardize and govern CI/CD pipelines and tools (Azure DevOps, GitHub Actions).
âª Define reference infrastructure-as-code templates (Bicep, Terraform, ARM templates).
âª Provide central best practices for pipeline security (code scanning, secrets management).
âª Use the central CI/CD framework and IaC templates for workload deployments.
 âª Implement workload-specific deployment tasks (configure app settings, database).
âª Adapt reference templates to workload needs while respecting central guidelines.

Development
âª Provide and enforce standardized development toolchains and frameworks to accelerate consistency (coding standards, DevOps best practices).
âª Maintain internal repositories or package feeds for shared libraries or modules.
âª Adopt and adapt standard toolchains for workload development.
âª Own the application lifecycle and incorporate best practices (unit testing, integration testing).
âª Manage continuous improvement for the workload's code base.

Monitoring
âª Plan monitoring strategy.
âª Alert on centralized responsibilities.
âª Provide dashboards for common operational metrics across the environment.
âª Monitor workload
âª Extend or fine-tune central alerts to capture workload-specific conditions.
âª Investigate and remediate workload-level incidents based on alerts and logs.

Cost
âª Allocate global or subscription-level cloud budgets
âª Monitor organization-wide cloud spend and create cost reports.
âª Allocate costs to business units or products, typically using tags or custom cost allocation models.
âª Apply tagging strategy for cost allocation.
âª Cost optimize workload design
âª Respect budget constraints.

Reliability
âª Define reliability requirements (SLO, RPO, RTO) per workload priority.
âª Provide guidance on business continuity and disaster recovery (BCDR).
âª Manage centralized disaster recovery solutions.
âª Support major incident management across all workloads.
âª Design workload to meet reliability requirements.

Performance
âª Monitor and maintain performance at centralized components (hub network, shared services).
âª Provide guidelines for performance optimization and capacity planning.
âª Monitor quota usage.
âª Design workload for performance efficiency.

## Establish your cloud operations

Use the responsibilities outlined in Table 1 to build an effective operational foundation. Clearly define teams, standards, and processes by following these steps:

- Define your cloud operations model. Choose a centralized, shared management, or decentralized cloud operating model based on your organization's size and maturity. For guidance, see Choose a cloud operating model.

- Assign central platform responsibilities. Form a dedicated team to handle central management tasks. Develop a skills matrix from Table 1 to identify required expertise.

- Assign workload responsibilities. Set up specialized teams for workload-specific tasks. Identify responsibilities using Table 1 then recruit accordingly. Use the Azure Well-Architected Framework and its Operational excellence pillar to guide your workload management responsibilities.

- Assign responsibility. Name specific owners for all cloud management responsibilities. In a shared management model, workload teams should have autonomy to manage their subscriptions.

## Document your cloud operations

Clearly document your cloud operations to enable efficient crisis response and smooth implementation of changes. Establish overarching procedures and create detailed guides for frequent and specific tasks.

### Document operational procedures

Define operational procedures for managing change, disaster recovery, and routine maintenance tasks that automation can't handle. Follow these steps:

- Define change management procedures. Change is the major cause of failure in the cloud. Develop a standardized process for managing changes to avoid failures in your cloud environment. See Manage change.

- Define deployment procedures (release management). To maintain consistent configuration, standardize your deployments, releases, and environment promotions. See Manage deployments.

- Define disaster recovery and business continuity procedures. To handle potential failures, prepare a standardized response plan. See Manage disaster recovery and business continuity.

- Define additional procedures. Document processes for managing service requests, patching, and configuration management. Clearly document these processes to ensure stakeholders know how to initiate or complete each task.

### Document operational guides

Create detailed step-by-step guides (runbooks or playbooks) for key operational tasks. This preparation ensures consistent execution, improves efficiency, and shortens resolution times during critical events.

- Define daily tasks. Prepare manuals covering daily responsibilities, such as privilege escalation requests and log reviews. Establish standard operating procedures (SOPs) for monitoring metrics, alert thresholds, and dashboards for each system.

- Create a library of Azure-centric runbooks. Create Azure-specific runbooks addressing scenarios such as:

Scenario
Example

High CPU usage
Manage scale up in Azure App Service

Failover and failback
Failover and failback in Azure Site Recovery

Blue/green deployments
Blue/green deployment in Azure Front Door

Backup restoration
Backup restore in Azure Blob Storage and Azure Cosmos DB

- Store these runbooks in a central repository. Maintain runbooks in a central repository accessible by on-call engineers for immediate use during incidents.

- Implement operations programmatically. Integrate infrastructure-as-code into your runbooks to deploy common resources consistently and accurately each time.

- Review and update. Periodically review and revise documentation to reflect operational adjustments and cloud service updates.

### Document tools and solutions

Clear documentation ensures consistency, reduces operational risks, and enhances team efficiency. Create and maintain comprehensive documentation for cloud tools. Regularly update documentation to reflect current practices and ensure easy accessibility for all team members.

Area
Example benefits

Integration
Standardization simplifies integrations by consolidating logs and code repositories.

Automation
Reuse IaC templates across teams, automation scripts, and best practices across projects.

Incident management
Capture issues and generate remediation actions that integrate into release cycles.

## Manage your cloud operations

Effective cloud management optimizes operational efficiency, reduces downtime, and clarifies roles and responsibilities. Standardize your cloud operations through automation and structured support processes. Follow these operational guidelines:

- Provide continuous cloud support. Establish 24/7 support coverage through either global teams adopting a follow-the-sun model or structured on-call rotations. Define responsibilities clearly to ensure timely response and resolution of critical incidents. Configure automated alerts to notify designated support personnel immediately.

- Automate repetitive work. Use Azure automation capabilities to minimize manual processes and reduce operational overhead. Automate routine activities to eliminate errors, streamline workflows, and enable teams to concentrate on strategic priorities.

Use Case
Examples

Automation
Automate workflows in Azure Boards or ITSM system. Templates for "Change Request" and "Incident" work items.

Incident response
To autogenerate incident tickets with standard fields populated, integrate Azure Monitor and Azure Service Health with ticketing system.

Change management
Use Azure Logic Apps to autoapprove low-risk changes or autoremediate certain incidents.

Compliance
Use Azure Policy to enforce and monitor cloud compliance.

Security
Use Microsoft Defender for Cloud and Microsoft Sentinel to automate security threat detection and response. Use Microsoft Entra ID Governance to review permissions and automate permissions management.

## Improve operations

Optimize your Azure cloud environment by promoting continuous improvement. Regularly evaluate operations and prioritize ongoing learning and feedback. Follow these steps:

- Review operations to improve. Follow best practices to monitor the health, compliance, security, costs, data, and cloud resources. Conduct weekly operational reviews to discuss key metrics, recent incidents, deployed changes, and anticipated risks. Actively address resource sprawl and technical debt.

- Train for operations. Foster ongoing skill development by prioritizing essential learning resources. Maintain dynamic cloud operations through practical training environments. The following table provides resources for operations training.

Operations training
Description

Get credentials
Set goals for Microsoft credentials, like applied skills and Microsoft Certifications to build expertise.

Use product documentation
Use Microsoft Learn to find guidance on Azure services.

Get hands-on practice
Encourage hands-on practice in nonproduction sandbox environments.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-10-27
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
