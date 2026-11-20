# https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/govern/enforce-cloud-governance-policies

Source: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/govern/enforce-cloud-governance-policies

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
 

 

 

 

 
 
# Enforce cloud governance policies

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Defining policies is not enough. The organization must enforce governance policies to ensure compliance. Cloud governance enforcement means implementing controls, processes, and tools so that cloud usage adheres to the governance policies. The cloud governance team sets the strategy and oversees enforcement, but enforcement is a shared responsibility. The cloud platform and workload teams handle day-to-day enforcement within their domains. It's generally recommended to automate enforcement wherever feasible, using cloud-native tools to enforce or check compliance. Use manual processes only where automation isn't possible.

## 1. Define an approach for enforcing cloud governance policies

Start by creating an overarching strategy for how policies will be enforced across the organization. Key considerations include:

- Delegate governance responsibilities. Empower individuals and teams to enforce governance within their scope of responsibility. For example, platform teams should apply policies that the workloads inherit and workload teams should enforce governance for their workload. The cloud governance team shouldn't be responsible for applying enforcement controls.

- Adopt an inheritance model. Apply a hierarchical governance model where specific workloads inherit governance policies from the platform. This model helps ensure that organizational standards apply to the correct environments, such as purchasing requirements for cloud services. Follow the design principles to establish a proper inheritance model.

- Discuss enforcement specifics. Discuss where and how you apply governance policies. The goal is to find cost-effective ways to enforce compliance that accelerates productivity. Without a discussion, you risk blocking the progress of specific teams. It's important to find a balance that supports the business objectives while managing risk effectively.

- Use a monitor-first approach. Don't block actions unless you understand them first. For lower-priority risk, start by monitoring compliance with cloud governance policies. After you understand the risk, you can move to more restrictive enforcement controls. A monitor-first approach gives you an opportunity to discuss the governance needs and realign the cloud governance policy and enforcement control to those needs.

- Prefer block lists. Prefer block lists over allow lists. Block lists prevent the deployment of specific services. It's better to have a small list of services that you shouldn't use than a long list of services you can use. To avoid lengthy block lists, don't add new services to the block list by default.

- Define a tagging and naming strategy. Establish systematic guidelines for naming and tagging cloud resources. It provides a structured framework for resource categorization, cost management, security, and compliance across the cloud environment. Allow teams, such as development teams, to add other tags for their unique needs.

## 2. Enforce cloud governance policies automatically

Use Azure's management and governance services to automate policy enforcement as much as possible. Automated enforcement improves consistency and reduces manual effort or error. Steps to implement automated governance:

- Start with a small set of automated policies. Automate compliance on a small set of essential cloud governance policies. Implement and test automation to avoid operational disruptions. Expand your list of automated enforcement controls when ready.

- Use cloud governance tools. Use the tools available in your cloud environment to enforce compliance. Azure's primary governance tool is Azure Policy. Supplement Azure Policy with Microsoft Defender for Cloud (security), Microsoft Purview (data), Microsoft Entra ID Governance (identity), Azure Monitor (operations), management groups (resource management), infrastructure as code (IaC) (resource management), and configurations within each Azure service.

- Apply governance policies at the right scope. Use an inheritance system where policies are set at a higher level, such as management groups. Policies at higher levels automatically apply to lower levels, such as subscriptions and resource groups. Policies apply even when there are changes within the cloud environment, lowering management overhead.

- Use policy enforcement points. Set up policy enforcement points within your cloud environments that automatically apply governance rules. Consider predeployment checks, runtime monitoring, and automated remediation actions.

- Use policy as code. Use IaC tools to enforce governance policies through code. Policy as code enhances the automation of governance controls and ensures consistency across different environments. Consider using Enterprise Azure Policy as Code (EPAC) to manage policies aligned with recommended Azure landing zone policies.

- Develop custom solutions as needed. For custom governance actions, consider developing custom scripts or applications. Use Azure service APIs to gather data or manage resources directly.

### Azure facilitation: Enforcing cloud governance policies automatically

The following guidance can help you find the right tools to automate compliance with cloud governance policies in Azure. It provides a sample starting point for major categories of cloud governance.

#### Automate regulatory compliance governance

- Apply regulatory compliance policies. Use built-in regulatory compliance policies that align with compliance standards, such as HITRUST/HIPAA, ISO 27001, CMMC, FedRAMP, and PCI DSSv4.

- Automate custom restrictions. Create custom policies to define your own rules for working with Azure.

#### Automate security governance

- Apply security policies. Use the built-in security policies and automated security compliance to align with common security standards. There are built-in policies for NIST SP 800 series, Center for Internet Security benchmarks, and the Microsoft cloud security benchmark. Use built-in policies to automate the security configuration of specific Azure services. Create custom policies to define your own rules for working with Azure.

- Apply identity governance. Enable Microsoft Entra multifactor authentication (MFA) and self-service password reset. Eliminate weak passwords. Automate other aspects of identity governance, such as access request workflows, access reviews, and identity lifecycle management. Enable just-in-time access to limit access to important resources. Use Conditional Access policies to grant or block user and device identities access to cloud services.

- Apply access controls. Use Azure role-based access control (RBAC) and attribute-based access control (ABAC) to govern access to specific resources. Grant and deny permissions to users and groups. Apply the permission at the appropriate scope (management group, subscription, resource group, or resource) to provide only the permission needed and limit management overhead.

#### Automate cost governance

- Automate deployment restrictions. Disallow certain cloud resources to prevent the use of cost-intensive resources.

- Automate custom restrictions. Create custom policies to define your own rules for working with Azure.

- Automate cost allocation. Enforce tagging requirements to group and allocate costs across environments (development, test, production), departments, or projects. Use tags to identify and track resources that are part of a cost optimization effort.

#### Automate operations governance

- Automate redundancy. Use built-in Azure policies to require a specified level of infrastructure redundancy, such as zone-redundant and geo-redundant instances.

- Apply backup policies. Use backup policies to govern the backup frequency, retention period, and storage location. Align backup policies with data governance, regulatory compliance requirements, recovery time objective (RTO), and recovery point objective (RPO). Use the backup settings in individual Azure services, such as Azure SQL Database, to configure the settings you need.

- Meet the target service-level objective. Restrict the deployment of certain services and service tiers (SKUs) that don't meet your target service-level objective. For example, use the `Not allowed resource types` policy definition in Azure Policy.

#### Automate data governance

- Automate data governance. Automate data governance tasks, such as cataloging, mapping, securely sharing, and applying policies.

- Automate data lifecycle management. Implement storage policies and lifecycle management for storage to ensure data is stored efficiently and compliantly.

- Automate data security. Review and enforce data protection strategies, such as data segregation, encryption, and redundancy.

#### Automate resource management governance

- Create a resource management hierarchy. Use management groups to organize your subscriptions so that you can efficiently govern policies, access, and spending. Follow Azure landing zone resource organization best practices.

- Enforce a tagging strategy. Ensure all Azure resources are consistently tagged to improve manageability, cost tracking, and compliance. Define your tagging strategy and manage tag governance.

- Restrict which resources you can deploy. Disallow resource types to restrict deployments of services that add unnecessary risk.

- Restrict deployments to specific regions. Control where resources are deployed to comply with regulatory requirements, manage costs, and reduce latency. For example, use the `Allowed locations` policy definition in Azure Policy. Also enforce regional restrictions in your deployment pipeline.

- Use infrastructure as code (IaC). Automate infrastructure deployments using Bicep, Terraform, or Azure Resource Manager templates (ARM templates). Store your IaC configurations in a source control system (GitHub or Azure Repos) to track changes and collaborate. Use Azure landing zone reference architectures to govern the deployment of your platform and application resources and avoid configuration drift over time.

- Govern hybrid and multicloud environments. Govern hybrid and multicloud resources. Maintain consistency in management and policy enforcement.

#### Automate AI governance

- Use the retrieval-augmented generation (RAG) pattern. RAG adds an information retrieval system to control the grounding data that a generative AI model uses to generate a response and constrain generative AI to your content. See Retrieval augmented generation (RAG) and indexes.

- Use AI development tools. Use AI tools, like Microsoft Agent Framework, that facilitate and standardize AI orchestration when developing applications that use AI.

- Govern output generation. Help prevent abuse and harmful content generation. Use AI content filtering and AI abuse monitoring.

- Configure data loss prevention. Configure data loss prevention for Foundry Tools. Configure the list of outbound URLs that your AI services resources are allowed to access.

- Use system messages. Use system messages to guide the behavior of an AI system and tailor the outputs.

- Apply the AI security baseline. Use the Azure AI security baseline to govern the security of AI systems.

## 3. Enforce cloud governance policies manually

Not everything can be automated perfectly. Sometimes a tool limitation or cost makes automated enforcement impractical. There will be cases, especially initially or for very custom processes, where manual governance is necessary. Also, smaller organizations might start with manual governance before automating. Key manual enforcement practices include:

- Use checklists. Use governance checklists to make it easy for your teams to follow the cloud governance policies. For more information, see the example compliance checklists.

- Provide regular training. Conduct frequent training sessions for all relevant team members to ensure they're aware of the governance policies.

- Schedule regular reviews. Implement a schedule for regular reviews and audits of cloud resources and processes to ensure compliance with governance policies. These reviews are critical for identifying deviations from established policies and taking corrective actions.

- Monitor manually. Assign dedicated personnel to monitor the cloud environment for compliance with governance policies. Consider tracking the use of resources, managing access controls, and ensuring data protection measures are in place to align with the policies. For example, define a comprehensive cost management approach to govern cloud costs.

## 4. Review policy enforcement

Regularly review and update compliance enforcement mechanisms. The goal is to keep cloud governance policy enforcement aligned with current needs, including developer, architect, workload, platform, and business requirements. To review policy enforcement, follow these recommendations:

- Engage with stakeholders. Discuss the effectiveness of enforcement mechanisms with stakeholders. Ensure cloud governance enforcement aligns with business objectives and compliance requirements.

- Monitor requirements. Update or remove enforcement mechanisms to align with new or updated requirements. Track changes in regulations and standards that require updates to your enforcement mechanisms. For example, Azure landing zone recommended policies can change over time. You should detect those policy changes, update to the latest Azure landing zone custom policies, or migrate to built-in policies as needed.

## Example cloud governance compliance checklists

Compliance checklists help teams understand the governance policies that apply to them. The example compliance checklists use the policy statement from the example cloud governance policies and contain the cloud governance policy ID for cross-referencing.

Category
Compliance requirement

Regulatory compliance
â Microsoft Purview must be used to monitor sensitive data (RC01). 
 â Daily sensitive data compliance reports must be generated from Microsoft Purview (RC02).

Security
â MFA must be enabled for all users (SC01). 
 â Access reviews must be conducted monthly in ID Governance (SC02). 
 â Use the specified GitHub organization to host all application and infrastructure code (SC03). 
 â Teams that use libraries from public sources must adopt the quarantine pattern (SC04).

Operations
â Production workloads should have an active-passive architecture across regions (OP01). 
 â All mission-critical workloads must implement a cross-region active-active architecture (OP02).

Cost
â Workload teams must set budget alerts at the resource group level (CM01). 
 â Azure Advisor cost recommendations must be reviewed (CM02).

Data
â Encryption in transit and at rest must be applied to all sensitive data (DG01). 
 â Data lifecycle policies must be enabled for all sensitive data (DG02).

Resource management
â Bicep must be used to deploy resources (RM01). 
 â Tags must be enforced on all cloud resources using Azure Policy (RM02).

AI
â The AI content filtering configuration must be set to medium or higher (AI01). 
 â Customer-facing AI systems must be red-teamed monthly (AI02).

## Next step

Monitor cloud governance

 
 

 
 

 

 
 
 
 
 
 
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
 2025-09-17
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
