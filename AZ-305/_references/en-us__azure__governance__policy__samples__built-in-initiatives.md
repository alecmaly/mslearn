# https://learn.microsoft.com/en-us/azure/governance/policy/samples/built-in-initiatives

Source: https://learn.microsoft.com/en-us/azure/governance/policy/samples/built-in-initiatives

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
 

 

 

 

 
 
# Azure Policy built-in initiative definitions

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This page is an index of Azure Policy built-in initiative definitions.

The name on each built-in links to the initiative definition source on the
Azure Policy GitHub repo. The built-ins are grouped by the
category property in metadata. To go to a specific category, use Ctrl-F for your browser's search feature.

## Automanage

Name
Description
Policies
Version

[Preview]: Audit configuration against Automanage Best Practices
Automanage Machine Best Practices ensures that managed resources are setup in accordance with the desired state as defined in the assigned Configuration Profile.
6
1.0.1-preview

## ChangeTrackingAndInventory

Name
Description
Policies
Version

Enable ChangeTracking and Inventory for Arc-enabled virtual machines
Enable ChangeTracking and Inventory for Arc-enabled virtual machines. Takes Data Collection Rule ID as parameter and asks for an option to input applicable locations.
6
1.1.0

Enable ChangeTracking and Inventory for virtual machine scale sets
Enable ChangeTracking and Inventory for virtual machine scale sets. Takes Data Collection Rule ID as parameter and asks for an option to input applicable locations and user-assigned identity for Azure Monitor Agent.
7
1.2.0

Enable ChangeTracking and Inventory for virtual machines
Enable ChangeTracking and Inventory for virtual machines. Takes Data Collection Rule ID as parameter and asks for an option to input applicable locations and user-assigned identity for Azure Monitor Agent.
7
1.3.0

## Cognitive Services

Name
Description
Policies
Version

[Preview]: Guardrail for Cognitive Services Deployments
Mandate guardrail configuration for model deployments within your organization.
12
1.0.0-preview

## Cosmos DB

Name
Description
Policies
Version

Enable Azure Cosmos DB throughput policy
Enable throughput control for Azure Cosmos DB resources in the specified scope (Management group, Subscription or resource group). Takes max throughput as parameter. Use this policy to help enforce throughput control via the resource provider.
2
1.0.0

## EssentialManagement

Name
Description
Policies
Version

[Preview]: Enable Essential Machine Management
Policy initiative to enable Essential Machine Management for Azure Virtual Machines and Arc-enabled servers.
26
1.0.0-preview

## General

Name
Description
Policies
Version

[Preview]: Azure Baseline Security Mode
Azure Baseline Security Mode (https://aka.ms/AzureBSM) helps you secure your Azure environment with a curated set of Microsoft-recommended security controls. It simplifies the adoption of high-impact security protections, helping reduce risk and strengthen your security posture with minimal effort.
7
1.0.0-preview

Allow Usage Cost Resources
Allow resources to be deployed except MCPP, M365.
2
1.0.0

## Guest Configuration

Name
Description
Policies
Version

[Preview]: Deploy prerequisites to enable Guest Configuration policies on virtual machines using user-assigned managed identity
This initiative adds a user-assigned managed identity and deploys the platform-appropriate Guest Configuration extension to virtual machines that are eligible to be monitored by Guest Configuration policies. This is a prerequisite for all Guest Configuration policies and must be assigned to the policy assignment scope before using any Guest Configuration policy. For more information on Guest Configuration, visit https://aka.ms/gcpol.
3
1.0.0-preview

[Preview]: Windows machines should meet requirements for the Azure compute security baseline
This initiative audits Windows machines with settings that do not meet the Azure compute security baseline. For details, please visit https://aka.ms/gcpol
29
2.0.1-preview

Audit machines with insecure password security settings
This initiative deploys the policy requirements and audits machines with insecure password security settings. For more information on Guest Configuration policies, please visit https://aka.ms/gcpol
9
1.1.0

Configure secure communication protocols(TLS 1.1 or TLS 1.2) on Windows machine(including prerequisites)
Creates a Guest Configuration assignment(including prerequisites) to configure specified secure protocol version(TLS 1.1 or TLS 1.2) on Windows machine. For details, visit https://aka.ms/SetSecureProtocol
3
1.0.0

Deploy prerequisites to enable Guest Configuration policies on virtual machines
This initiative adds a system-assigned managed identity and deploys the platform-appropriate Guest Configuration extension to virtual machines that are eligible to be monitored by Guest Configuration policies. This is a prerequisite for all Guest Configuration policies and must be assigned to the policy assignment scope before using any Guest Configuration policy. For more information on Guest Configuration, visit https://aka.ms/gcpol.
4
1.0.0

## Kubernetes

Name
Description
Policies
Version

[Preview]: Use Image Integrity to ensure only trusted images are deployed
Use Image Integrity to ensure AKS clusters deploy only trusted images by enabling the Image Integrity and Azure Policy Add-Ons on AKS clusters. Image Integrity Add-On and Azure Policy Add-On are both pre-requisites to using Image Integrity to verify if image is signed upon deployment. For more info, visit https://aka.ms/aks/image-integrity.
3
1.1.0-preview

[Preview]: Kubernetes cluster should follow the security control recommendations of Center for Internet Security (CIS) Kubernetes benchmark
This initiative includes the policies for the security recommendation for Center for Internet Security (CIS) Kubernetes benchmark, you can use this initiative to stay compliant with CIS Kubernetes benchmark. For more information of CIS compliance, visit: https://aka.ms/aks/cis-kubernetes
7
1.0.0-preview

Deployment safeguards should help guide developers towards AKS recommended best practices
A collection of Kubernetes best practices that are recommended by Azure Kubernetes Service (AKS). For the best experience, use deployment safeguards to assign this policy initiative: https://aka.ms/aks/deployment-safeguards. Azure Policy Add-On for AKS is a pre-requisite for applying these best practices to your clusters. For instructions on enabling the Azure Policy Add-On, go to aka.ms/akspolicydoc
27
3.1.0

Kubernetes cluster pod security baseline standards for Linux-based workloads
This initiative includes the policies for the Kubernetes cluster pod security baseline standards. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For instructions on using this policy, visit https://aka.ms/kubepolicydoc.
5
1.4.0

Kubernetes cluster pod security restricted standards for Linux-based workloads
This initiative includes the policies for the Kubernetes cluster pod security restricted standards. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For instructions on using this policy, visit https://aka.ms/kubepolicydoc.
8
2.5.0

## Managed Identity

Name
Description
Policies
Version

[Preview]: Managed Identity Federated Credentials should be of approved types from approved federation sources
Control use of federated credentials for Managed Identities. This initiative incudes policies to block federated identity credentials altogether, to limit use to specific federation provider types, and to limit federation reationships to approved sources.
3
1.0.0-preview

## Mission

Name
Description
Policies
Version

Control the use of AKS for Cloud in Mission Platforms
This policy initiative applies exclusively to Mission Platform products and services; usage outside of these scopes is not supported. This initiative deploys Azure policies for AKS ensuring boundary protection of this resource while it operates within the logically separated structure of Mission Platform.
8
1.0.0

Control the use of App Service for Cloud in Mission Platforms
This policy applies exclusively to Mission Platform products and services; usage outside of these scopes is not supported. This initiative deploys Azure policies for App Service ensuring boundary protection of this resource while it operates within the logically separated structure of Mission Platform.
60
1.0.0

Control the use of AVD for Cloud in Mission Platforms
This policy initiative applies exclusively to Mission Platform products and services; usage outside of these scopes is not supported. This policy set deploys the required policy guardrails governing the use of Azure Virtual Desktops within the Environment. See the list of policies of the services that are included.
3
1.0.0

Control the use of Azure SQL in Mission Platforms
This policy set applies exclusively to Mission Platform products and services; usage outside of these scopes is not supported. It deploys coordinated Azure SQL controls to enforce private networking, outbound restrictions, and customer-managed encryption for mission workloads (see https://learn.microsoft.com/azure/azure-sql/database/security-overview).
27
1.0.0

Control the use of Compute for Cloud in Mission Platforms
This policy applies exclusively to Mission Platform products and services; usage outside of these scopes is not supported. This policy set deploys the required policy guardrails governing the use of Azure Virtual Machines within the Environment. See the list of policies of the services that are included.
3
1.0.0

Control the use of Container Registry in Mission Platforms
This policy set applies exclusively to Mission Platform products and services; usage outside of these scopes is not supported. It deploys coordinated Container Registry controls that enforce private network access, tenant isolation, and boundary protection across Mission Platform workloads; refer to https://learn.microsoft.com/azure/container-registry/container-registry-private-link for architectural guidance.
9
1.0.0

Control the use of CosmosDB in Mission Platforms
This policy applies exclusively to Mission Platform products and services; usage outside of these scopes is not supported. This initiative ensures Cosmos DB resources operate securely within logically separated Mission Platform environments by enforcing boundary protection and access controls.
10
1.0.0

Control the use of Event Grid in Mission Platforms
This policy applies exclusively to Mission Platform products and services; usage outside of these scopes is not supported. These guardrails reduce unintended network exposure and local-authentication risks for Azure Event Grid resources. Learn more at https://aka.ms/privateendpoints.
7
1.0.0

Control the use of PostgreSQL in Mission Platforms
This policy applies exclusively to Mission Platform products and services; usage outside of these scopes is not supported. This initiative enforces PostgreSQL boundary protections to maintain security and compliance requirements. For more information, visit https://aka.ms/mission-platforms
11
1.0.0

Control the use of Service Bus in Mission Platforms
This initiative deploys Azure policies for Service Bus ensuring boundary protection of this resource while it operates within the logically separated structure of Mission Platforms.
8
1.0.0

Control the use of Storage Accounts for Cloud in Mission Platforms
This policy applies exclusively to Mission Platform products and services; usage outside of these scopes is not supported. This initiative deploys Azure policies for Storage Accounts ensuring boundary protection of this resource while it operates within the logically separated enclaves.
15
1.0.0

Control the use of Virtual Network Guardrails for Cloud in Mission Platforms
This policy applies exclusively to Mission Platform products and services; usage outside of these scopes is not supported. This policy set deploys the required policy guardrails governing the use of Azure Virtual Networks within the Environment. See the list of policies of the services that are included.
5
1.0.0

Key Vault should enforce network and access guardrails in mission platforms
This policy set applies exclusively to Mission Platform products and services; usage outside of these scopes is not supported. Apply Key Vault network restrictions, soft-delete checks, and RBAC permission-model checks to reduce unintended access and data loss. The modifier disables unrestricted public access while audit policies report configurations that require review.
6
1.0.0

## Monitoring

Name
Description
Policies
Version

[Preview]: Configure Azure Defender for SQL agents on virtual machines
Configure virtual machines to automatically install the Azure Defender for SQL agents where the Azure Monitor Agent is installed. Security Center collects events from the agents and uses them to provide security alerts and tailored hardening tasks (recommendations). Creates a resource group and Log Analytics workspace in the same region as the machine. This policy only applies to VMs in a few regions.
2
1.0.0-preview

Configure Linux machines to run Azure Monitor Agent and associate them to a Data Collection Rule
Monitor and secure your Linux virtual machines, virtual machine scale sets, and Arc machines by deploying the Azure Monitor Agent extension and associating the machines with a specified Data Collection Rule. Deployment will occur on machines with supported OS images (or machines matching the provided list of images) in supported regions.
4
3.2.0

Configure Windows machines to run Azure Monitor Agent and associate them to a Data Collection Rule
Monitor and secure your Windows virtual machines, virtual machine scale sets, and Arc machines by deploying the Azure Monitor Agent extension and associating the machines with a specified Data Collection Rule. Deployment will occur on machines with supported OS images (or machines matching the provided list of images) in supported regions.
4
3.2.0

Deploy Linux Azure Monitor Agent with user-assigned managed identity-based auth and associate with Data Collection Rule
Monitor your Linux virtual machines and virtual machine scale sets by deploying the Azure Monitor Agent extension with user-assigned managed identity authentication and associating with specified Data Collection Rule. Azure Monitor Agent Deployment will occur on machines with supported OS images (or machines matching the provided list of images) in supported regions.
5
2.4.0

Deploy Windows Azure Monitor Agent with user-assigned managed identity-based auth and associate with Data Collection Rule
Monitor your Windows virtual machines and virtual machine scale sets by deploying the Azure Monitor Agent extension with user-assigned managed identity authentication and associating with specified Data Collection Rule. Azure Monitor Agent Deployment will occur on machines with supported OS images (or machines matching the provided list of images) in supported regions.
5
2.3.0

Enable allLogs category group resource logging for supported resources to Event Hub
Resource logs should be enabled to track activities and events that take place on your resources and give you visibility and insights into any changes that occur. This initiative deploys diagnostic setting using the allLogs category group to route logs to Event Hub for all supported resources.
140
1.0.0

Enable allLogs category group resource logging for supported resources to Log Analytics
Resource logs should be enabled to track activities and events that take place on your resources and give you visibility and insights into any changes that occur. This initiative deploys diagnostic setting using the allLogs category group to route logs to an Event Hub for all supported resources
140
1.0.0

Enable allLogs category group resource logging for supported resources to storage
Resource logs should be enabled to track activities and events that take place on your resources and give you visibility and insights into any changes that occur. This initiative deploys diagnostic setting using the allLogs category group to route logs to storage for all supported resources.
140
1.0.0

Enable audit category group resource logging for supported resources to Event Hub
Resource logs should be enabled to track activities and events that take place on your resources and give you visibility and insights into any changes that occur. This initiative deploys diagnostic setting using the audit category group to route logs to Event Hub for all supported resources
69
1.1.0

Enable audit category group resource logging for supported resources to Log Analytics
Resource logs should be enabled to track activities and events that take place on your resources and give you visibility and insights into any changes that occur. This initiative deploys diagnostic setting using the audit category group to route logs to Log Analytics for all supported resources.
69
1.1.0

Enable audit category group resource logging for supported resources to storage
Resource logs should be enabled to track activities and events that take place on your resources and give you visibility and insights into any changes that occur. This initiative deploys diagnostic setting using the audit category group to route logs to storage for all supported resources.
69
1.1.0

Enable Azure Monitor for Hybrid VMs with AMA
Enable Azure Monitor for the hybrid virtual machines with AMA.
4
1.1.0

Enable Azure Monitor for VMs with Azure Monitoring Agent(AMA)
Enable Azure Monitor for the virtual machines (VMs) with AMA.
5
1.3.0

Enable Azure Monitor for VMSS with Azure Monitoring Agent(AMA)
Enable Azure Monitor for the virtual machines scale set (VMSS) with AMA.
5
1.3.0

## Network

Name
Description
Policies
Version

Enable VNet Flowlog and Traffic Analytics with regional Storage and centralized Log Analytics
This policy set enables VNet Flowlog and Traffic Analytics by creating a regional Storage Account, a Log Analytics Workspace in a centrally managed region, and creates a Network Watcher Resource if needed in the Region.
4
1.0.0

Flow logs should be configured and enabled for every network security group
Audit for network security groups to verify if flow logs are configured and if flow log status is enabled. Enabling flow logs allows to log information about IP traffic flowing through network security group. It can be used for optimizing network flows, monitoring throughput, verifying compliance, detecting intrusions and more.
2
1.0.0

## Nexus

Name
Description
Policies
Version

[Preview]: Nexus Compute Cluster Security Baseline
This initiative includes policies designed to reflect the security baseline expectations of Nexus Compute Clusters. It ensures that the cluster configurations adhere to specific security controls that are critical for maintaining a secure environment.
13
2.1.0-preview

## Regulatory Compliance

Name
Description
Policies
Version

ACAT for Microsoft 365 Certification
App Compliance Automation Tool for Microsoft 365 (ACAT) simplifies the process to achieve Microsoft 365 Certification, see https://aka.ms/acat. This certification ensures that apps have strong security and compliance practices in place to protect customer data, security, and privacy. This initiative includes policies that address a subset of the Microsoft 365 Certification controls. Additional policies will be added in upcoming releases.
16
1.1.0

APRA CPS 234 2019
Australian Prudential Regulation Authority (APRA) standard for managing information security risks in regulated entities.
18
1.0.1

Australian Government ISM PROTECTED
This initiative includes policies that address a subset of Australian Government Information Security Manual (ISM) controls. Additional policies will be added in upcoming releases. For more information, visit https://aka.ms/auism-initiative.
38
8.10.0

Brazilian General Data Protection Law (LGPD) 2018
Brazil's comprehensive data protection law, regulating the processing of personal data.
18
1.1.0

Canada Federal PBMM
This initiative includes policies that address a subset of Canada Federal PBMM controls. Additional policies will be added in upcoming releases. For more information, visit https://aka.ms/canadafederalpbmm-init.
41
8.9.0

Canada Federal PBMM 3-1-2020
Security standards for Canadian federal systems, ensuring the confidentiality, integrity, and availability of sensitive information.
189
1.7.0

CIS Azure Foundations v2.1.0
Security guidance for Microsoft Azure, providing best practices to enhance security posture.
31
1.1.0

CIS Azure Foundations v3.0.0
CIS Azure Foundations 3.0 defines benchmark controls to improve cloud security in Microsoft Azure. The standard aligns with industry best practices for risk reduction and secure configurations.
53
1.3.0

CIS Controls v8.1
Globally recognized cybersecurity best practices, offering actionable steps to protect against cyber threats.
167
1.7.0

CIS Microsoft Azure Foundations Benchmark v1.1.0
The Center for Internet Security (CIS) is a nonprofit entity whose mission is to 'identify, develop, validate, promote, and sustain best practice solutions for cyberdefense.' CIS benchmarks are configuration baselines and best practices for securely configuring a system. These policies address a subset of CIS Microsoft Azure Foundations Benchmark v1.1.0 controls. For more information, visit https://aka.ms/cisazure110-initiative
151
16.12.0

CIS Microsoft Azure Foundations Benchmark v1.3.0
The Center for Internet Security (CIS) is a nonprofit entity whose mission is to 'identify, develop, validate, promote, and sustain best practice solutions for cyberdefense.' CIS benchmarks are configuration baselines and best practices for securely configuring a system. These policies address a subset of CIS Microsoft Azure Foundations Benchmark v1.3.0 controls. For more information, visit https://aka.ms/cisazure130-initiative
167
8.16.0

CIS Microsoft Azure Foundations Benchmark v1.4.0
The Center for Internet Security (CIS) is a nonprofit entity whose mission is to 'identify, develop, validate, promote, and sustain best practice solutions for cyberdefense.' CIS benchmarks are configuration baselines and best practices for securely configuring a system. These policies address a subset of CIS Microsoft Azure Foundations Benchmark v1.4.0 controls. For more information, visit https://aka.ms/cisazure140-initiative
166
1.15.0

CIS Microsoft Azure Foundations Benchmark v2.0.0
The Center for Internet Security (CIS) is a nonprofit entity whose mission is to 'identify, develop, validate, promote, and sustain best practice solutions for cyberdefense.' CIS benchmarks are configuration baselines and best practices for securely configuring a system. These policies address a subset of CIS Microsoft Azure Foundations Benchmark v2.0.0 controls. For more information, visit https://aka.ms/cisazure200-initiative
108
1.10.0

CMMC 2.0 Level 2
This initiative includes policies that address a subset of CMMC 2.0 Level 2 practices. Additional policies will be added in upcoming releases. For more information, visit https://aka.ms/cmmc2l2-initiative.
214
2.24.0

CMMC Level 3
This initiative includes policies that address a subset of Cybersecurity Maturity Model Certification (CMMC) Level 3 requirements. Additional policies will be added in upcoming releases. For more information, visit https://aka.ms/cmmc-initiative.
142
11.16.0

CSA CSA Cloud Controls Matrix v4.0.12
Cybersecurity framework by the Cloud Security Alliance (CSA), offering security controls specifically for cloud environments.
201
1.9.0

Cyber Essentials v3.1
UK certification scheme to protect against common cyber threats through basic security controls.
106
1.2.0

Cybersecurity Maturity Model Certification (CMMC) Level 2 v1.9.0
Focuses on protecting Controlled Unclassified Information (CUI) in defense contracting with advanced security controls.
199
1.8.0

DORA 2022 2554
DORA establishes resilience standards for digital operations in the European Union (EU) financial sector. The regulation governs information and communication technology (ICT) risk, incident response, and third-party oversight.
134
1.6.0

EU 2022/2555 (NIS2) 2022
Enhances cybersecurity across the EU with security measures and incident reporting for critical sectors.
179
1.8.0

EU AI Act 2024 1689
EU AI Act defines obligations for AI systems based on their risk to safety and fundamental rights. The regulation promotes transparency, oversight, and risk-based AI controls.
6
1.0.1

EU General Data Protection Regulation (GDPR) 2016/679
Comprehensive data protection law regulating personal data processing within the EU.
279
1.9.0

FBI Criminal Justice Information Services (CJIS) v5.9.5
Standards by the FBI to secure criminal justice information, covering data access, transmission, and storage.
211
1.9.0

FedRAMP High
FedRAMP is a US government-wide program that provides a standardized approach to security assessment, authorization, and continuous monitoring for cloud-based products and services. FedRAMP defines a set of controls for Low, Moderate, or High security impact level systems based on NIST baseline controls. These policies address a subset of FedRAMP (High) controls. For more information, visit https://docs.microsoft.com/azure/compliance/offerings/offering-fedramp
707
17.22.0

FedRAMP Moderate
FedRAMP is a U.S. government-wide program that provides a standardized approach to security assessment, authorization, and continuous monitoring for cloud-based products and services. FedRAMP defines a set of controls for Low, Moderate, or High security impact level systems based on NIST baseline controls. These policies address a subset of FedRAMP (Moderate) controls. Additional policies will be added in upcoming releases. For more information, visit https://www.fedramp.gov/documents-templates/
638
17.21.0

FFIEC CAT 2017
Assessment tool for financial institutions to measure cybersecurity preparedness, from the FFIEC.
131
1.6.0

HITRUST CSF v11.3
A comprehensive security and privacy framework for managing compliance in industries like healthcare and finance.
215
1.9.0

HITRUST/HIPAA
Health Information Trust Alliance (HITRUST) helps organizations from all sectors-but especially healthcare-effectively manage data, information risk, and compliance. HITRUST certification means that the organization has undergone a thorough assessment of the information security program. These policies address a subset of HITRUST controls. For more information, visit https://docs.microsoft.com/azure/governance/policy/samples/hipaa-hitrust-9-2
586
14.15.0

IRS1075 September 2016
This initiative includes policies that address a subset of IRS1075 September 2016 controls. Additional policies will be added in upcoming releases. For more information, visit https://aka.ms/irs1075-init.
43
8.9.0

ISO 27001:2013
The International Organization for Standardization (ISO) 27001 standard provides requirements for establishing, implementing, maintaining, and continuously improving an Information Security Management System (ISMS). These policies address a subset of ISO 27001:2013 controls. Additional policies will be added in upcoming releases. For more information, visit https://aka.ms/iso27001-init
448
8.9.0

ISO/IEC 27001 2022
International standard for managing information security via an Information Security Management System (ISMS).
58
1.3.0

ISO/IEC 27002 2022
Provides specific guidance on implementing controls for information security, complementing ISO 27001.
145
1.8.0

ISO/IEC 27017 2015
Cloud-specific extension to ISO 27001, providing security guidelines for cloud service providers and customers.
91
1.7.0

K ISMS P 2023
K-ISMS-P establishes requirements for protecting personal data and securing information systems in South Korea. The framework establishes administrative, physical, and technical controls for data privacy and system security.
413
2.1.0

Motion Picture Association of America (MPAA)
This initiative includes audit and virtual machine extension deployment policies that address a subset of Motion Picture Association of America (MPAA) security and guidelines controls. Additional policies will be added in upcoming releases. For more information, visit https://aka.ms/mpaa-init.
28
4.7.0

NCSC Cyber Assurance Framework (CAF) v3.2
UK framework providing cybersecurity guidance for critical national infrastructure to protect systems and data.
71
1.6.0

New Zealand ISM
NZISM v3.8. The New Zealand Information Security Manual (NZISM) details processes and controls essential for the protection of all New Zealand Government information and systems. This initiative includes policies that address a subset of NZISM controls. Additional policies will be added in upcoming releases. For full details on controls, please refer to https://www.nzism.gcsb.govt.nz/ism-document. This policy set includes definitions that have a Deny effect by default.
205
1.11.0

NIS2
The NIS2 Directive enhances the cybersecurity and resilience of critical infrastructure and digital services across the European Union, ensuring a higher level of protection against cyber threats.
236
1.2.0

NIST 800-171 R3
Guidelines for protecting Controlled Unclassified Information (CUI) in non-federal systems and organizations.
205
1.9.0

NIST AI RMF v1.0
NIST AI RMF provides guidance for managing AI risks across sectors. The framework promotes trustworthy, transparent, and responsible AI development and use.
1
1.0.0

NIST CSF v2.0
Risk-based approach to managing cybersecurity threats, offering guidance for improving cybersecurity practices.
102
1.7.0

NIST SP 800-171 Rev. 2
The US National Institute of Standards and Technology (NIST) promotes and maintains measurement standards and guidelines to help protect the information and information systems of federal agencies. In response to Executive Order 13556 on managing controlled unclassified information (CUI), it published NIST SP 800-171. These policies address a subset of NIST SP 800-171 Rev. 2 controls. For more information, visit https://docs.microsoft.com/azure/compliance/offerings/offering-nist-800-171
432
15.24.0

NIST SP 800-53 R5.1.1
Comprehensive security and privacy controls framework for U.S. federal information systems and organizations.
219
1.9.0

NIST SP 800-53 Rev. 4
National Institute of Standards and Technology (NIST) SP 800-53 R4 provides a standardized approach for assessing, monitoring and authorizing cloud computing products and services to manage information security risk.These policies address a subset of NIST SP 800-53 R4 controls. Additional policies will be added in upcoming releases. For more information, visit https://aka.ms/nist800-53r4-initiative
708
17.21.0

NIST SP 800-53 Rev. 5
National Institute of Standards and Technology (NIST) SP 800-53 Rev. 5 provides a standardized approach for assessing, monitoring and authorizing cloud computing products and services to manage information security risk. These policies address a subset of NIST SP 800-53 R5 controls. Additional policies will be added in upcoming releases. For more information, visit https://aka.ms/nist800-53r5-initiative
693
14.21.0

NL BIO Cloud Theme
This initiative includes policies that address the Dutch Baseline Informatiebeveiliging (BIO) controls specifically for the 'thema-uitwerking Clouddiensten' and include policies covered under the SOC2 and ISO 27001:2013 controls.
227
1.17.0

NL BIO Cloud Theme V2
This initiative includes policies that address the Dutch Baseline Informatiebeveiliging (BIO) controls specifically for the 'thema-uitwerking Clouddiensten' and include policies covered under the SOC2 and ISO 27001:2013 controls.
277
2.10.0

NZISM v3.7
New Zealand's Information Security Manual, providing security guidance for government agencies.
208
1.10.0

PCI DSS v4
The Payment Card Industry (PCI) Data Security Standards (DSS) is a global information security standard designed to prevent fraud through increased control of credit card data. Compliance with PCI DSS is required for any organization that stores, processes, or transmits payment and cardholder data. These policies address a subset of PCI-DSS v4 controls. For more information, visit https://docs.microsoft.com/azure/governance/policy/samples/pci-dss-3-2-1
269
1.8.0

PCI DSS v4.0.1
Payment Card Industry Data Security Standard, focusing on protecting credit card transaction data.
201
1.8.0

PCI v3.2.1:2018
This initiative includes policies that address a subset of PCI v3.2.1:2018 controls. Additional policies will be added in upcoming releases. For more information, visit https://aka.ms/pciv321-init.
30
6.6.0

Reserve Bank of India - IT Framework for Banks
This initiative includes policies that address a subset of Reserve Bank of India IT Framework for Banks controls. Additional policies will be added in upcoming releases. For more information, visit https://aka.ms/rbiitfbanks-initiative.
146
1.22.0

Reserve Bank of India - IT Framework for NBFC
This initiative includes policies that address a subset of Reserve Bank of India IT Framework for Non-Banking Financial Companies (NBFC) controls. Additional policies will be added in upcoming releases. For more information, visit https://aka.ms/rbiitfnbfc-initiative.
112
2.20.0

RMIT Malaysia
This initiative includes policies that address a subset of RMIT requirements. Additional policies will be added in upcoming releases. For more information, visit aka.ms/rmit-initiative.
182
9.21.0

Sarbanes Oxley Act 2022
U.S. federal law aimed at improving corporate transparency and accountability, including provisions for cybersecurity and IT controls.
89
1.2.0

SOC 2 Type 2
A System and Organization Controls (SOC) 2 is a report based on the Trust Service Principles and Criteria established by the American Institute of Certified Public Accountants (AICPA). The Report evaluates an organization's information system relevant to the following principles: security, availability, processing integrity, confidentiality and privacy. These policies address a subset of SOC 2 Type 2 controls. For more information, visit https://docs.microsoft.com/azure/compliance/offerings/offering-soc-2
306
1.13.0

SOC 2023
Service Organization Control reports that ensure organizations manage sensitive data securely and comply with trust service criteria.
219
1.9.0

Sovereignty Baseline - Confidential Policies
The Microsoft Cloud for Sovereignty recommends confidential policies to help organizations achieve their sovereignty goals by default denying the creation of resources outside of approved regions, denying resources that are not backed by Azure Confidential Computing, and denying data storage resources that are not using Customer-Managed Keys. More details can be found here: https://aka.ms/SovereigntyBaselinePolicies
22
1.2.0

Sovereignty Baseline - Global Policies
The Microsoft Cloud for Sovereignty recommends global policies to help organizations achieve their sovereignty goals by default denying the creation of resources outside of approved regions. More details can be found here: https://aka.ms/SovereigntyBaselinePolicies
5
1.2.0

Spain ENS
This initiative includes policies that address National Security Scheme (ENS) controls specifically for the 'CCN-STIC 884'. This policy set includes definitions that have a Deny effect by default.
821
1.11.0

SWIFT CSP-CSCF v2020
This initiative includes audit and virtual machine extension deployment policies that address a subset of SWIFT CSP-CSCF v2020 controls. Additional policies will be added in upcoming releases. For more information, visit https://aka.ms/swift2020-init.
44
6.8.0

SWIFT CSP-CSCF v2021
This initiative includes policies that address a subset of the SWIFT Customer Security Program's Customer Security Controls Framework v2021 controls. Additional policies will be added in upcoming releases. For more information, visit https://aka.ms/swift2021-init.
116
4.18.0

SWIFT CSP-CSCF v2022
SWIFT's Customer Security Programme (CSP) helps financial institutions ensure their defences against cyberattacks are up to date and effective, to protect the integrity of the wider financial network. Users compare the security measures they have implemented with those detailed in the Customer Security Controls Framework (CSCF). These policies address a subset of SWIFT controls. For more information, visit https://docs.microsoft.com/azure/governance/policy/samples/swift-cscf-v2021
321
2.14.0

SWIFT Customer Security Controls Framework 2024
Ensures secure transactions for organizations using SWIFT, the global financial messaging service.
192
1.9.0

UK OFFICIAL and UK NHS
This initiative includes audit and virtual machine extension deployment policies that address a subset of UK OFFICIAL and UK NHS controls. Additional policies will be added in upcoming releases. For more information, visit https://aka.ms/ukofficial-init and https://aka.ms/uknhs-init.
45
9.7.0

## Resilience

Name
Description
Policies
Version

[Preview]: Resources should be Zone Resilient
Some resource types can be deployed Zone Redundant (e.g. SQL Databases); some can be deploy Zone Aligned (e.g. Virtual Machines); and some can be deployed either Zone Aligned or Zone Redundant (e.g. Virtual Machine Scale Sets). Being zone aligned does not guarantee resilience, but it is the foundation on which a resilient solution can be built (e.g. three Virtual Machine Scale Sets zone aligned to three different zones in the same region with a load balancer). See https://aka.ms/AZResilience for more info.
34
1.10.0-preview

## SDN

Name
Description
Policies
Version

Audit Public Network Access
Audit Azure resources that allow access from the public internet
34
4.3.0

Evaluate Private Link Usage Across All Supported Azure Resources
Compliant resources have at least one approved private endpoint connection
28
1.2.0

## Security Center

Name
Description
Policies
Version

[Preview]: Deploy Microsoft Defender for Endpoint agent
Deploy Microsoft Defender for Endpoint agent on applicable images.
4
1.0.0-preview

Configure Advanced Threat Protection to be enabled on open-source relational databases
Enable Advanced Threat Protection on your non-Basic tier open-source relational databases to detect anomalous activities indicating unusual and potentially harmful attempts to access or exploit databases. See https://aka.ms/AzDforOpenSourceDBsDocu.
5
1.2.0

Configure Azure Defender to be enabled on SQL Servers and SQL Managed Instances
Enable Azure Defender on your SQL Servers and SQL Managed Instances to detect anomalous activities indicating unusual and potentially harmful attempts to access or exploit databases.
3
3.0.0

Configure Microsoft Defender for Cloud plans
Microsoft Defender for Cloud provides comprehensive, cloud-native protections from development to runtime in multi-cloud environments. Use the policy initiative to configure Defender for Cloud plans and extensions to be enabled on selected scope(s).
12
2.0.0

Configure Microsoft Defender for Databases to be enabled
Configure Microsoft Defender for Databases to protect your Azure SQL Databases, Managed Instances, Open-source relational databases and Cosmos DB.
4
1.0.0

Configure multiple Microsoft Defender for Endpoint integration settings with Microsoft Defender for Cloud
Configure the multiple Microsoft Defender for Endpoint integration settings with Microsoft Defender for Cloud (WDATP, WDATP_EXCLUDE_LINUX_PUBLIC_PREVIEW, WDATP_UNIFIED_SOLUTION etc.). See: https://learn.microsoft.com/azure/defender-for-cloud/integration-defender-for-endpoint for more information.
3
1.0.0

Configure SQL VMs and Arc-enabled SQL Servers to install Microsoft Defender extension
Microsoft Defender for SQL collects events from the agents and uses them to provide security alerts and tailored hardening tasks (recommendations).
3
1.0.0

Configure SQL VMs and Arc-enabled SQL Servers to install Microsoft Defender for SQL and AMA with a LA workspace
Microsoft Defender for SQL collects events from the agents and uses them to provide security alerts and tailored hardening tasks (recommendations). Creates a resource group and a Data Collection Rule and Log Analytics workspace in the same region as the machine.
9
1.3.0

Configure SQL VMs and Arc-enabled SQL Servers to install Microsoft Defender for SQL and AMA with a user-defined LA workspace
Microsoft Defender for SQL collects events from the agents and uses them to provide security alerts and tailored hardening tasks (recommendations). Creates a resource group and a Data Collection Rule in the same region as the user-defined Log Analytics workspace.
8
1.2.0

Microsoft cloud security benchmark
The Microsoft cloud security benchmark initiative represents the policies and controls implementing security recommendations defined in Microsoft cloud security benchmark, see https://aka.ms/azsecbm. This also serves as the Microsoft Defender for Cloud default policy initiative. You can directly assign this initiative, or manage its policies and compliance results within Microsoft Defender for Cloud.
216
57.60.0

Microsoft cloud security benchmark v2
The Microsoft cloud security benchmark initiative represents the policies and controls implementing security recommendations defined in Microsoft cloud security benchmark, see https://aka.ms/MCSB. This also serves as the Microsoft Defender for Cloud default policy initiative. You can directly assign this initiative, or manage its policies and compliance results within Microsoft Defender for Cloud.
718
1.8.0

## Sovereignty

Name
Description
Policies
Version

[Preview]: Assess workload readiness for continuity on Azure Local
Assess whether the Azure resource types used by a workload are supported on connected Azure Local to help determine continuity readiness if Azure Public access is disrupted. Use Audit to report unsupported resource types, Deny to prevent their creation, or Disabled to turn off the assessment.
1
1.0.0-preview

[Preview]: Assess workload readiness for continuity on Azure Local disconnected operations
Assess whether the Azure resource types used by a workload are supported in Azure Local disconnected operations, so that the workload can continue to operate if it must move off public Azure into a disconnected environment. Set the effect to Audit to report resource types that are not supported, to Deny to prevent those resource types from being created so that the migration path stays open, or to Disabled to turn the assessment off.
1
1.0.0-preview

[Preview]: Data Residency for Replication across Azure Services
Help restrict replication, replicated backups, and data processing to approved locations and security boundaries across supported Azure services.
1
1.0.0-preview

[Preview]: Enforce Data Residency across Azure Services
Help restrict and audit the Azure Regions that Azure Services can be deployed into. Helping to enforce Level 1 - Data Residency Sovereignty Controls detailed here: https://aka.ms/sovereign/controls
6
1.0.0-preview

[Preview]: Enforce Encryption-at-Rest with Customer Managed Keys (CMK) across Azure Services
Help restrict and audit Azure services to use customer-managed keys for encryption at rest across supported services.
49
2.0.0-preview

[Preview]: Enforce Encryption-at-Rest with Customer Managed Keys (CMK) with Azure Key Vault Managed HSM Keys across Azure Services
Help restrict and audit Azure Services to use CMK with Azure Key Vault Premium Managed HSM keys
1
1.0.0-preview

[Preview]: Enforce Encryption-in-Transit across Azure Services - HTTPS
Help restrict and audit Azure Services to use HTTPS/SSL
19
1.1.0-preview

[Preview]: Enforce Encryption-in-Transit across Azure Services - TLS Version
Help restrict and audit Azure Services to use latest TLS versions
29
1.2.0-preview

[Preview]: Enforce Encryption-in-Use across Azure Services
Help restrict and audit Azure Services to only allow Azure Confidential Compute (ACC) VM SKUs or ACC backed PaaS Services and associated SKUs
4
1.0.0-preview

[Preview]: Private Endpoint configured across Azure Services
Help audit Azure services to ensure private endpoints are configured by leveraging Azure Private Link
48
1.1.0-preview

[Preview]: Restrict Public Network Access across Azure Services
Help restrict Azure services to disable public network access, reducing exposure to the public internet
51
1.1.0-preview

## SQL

Name
Description
Policies
Version

Azure SQL Database should have Microsoft Entra-only authentication
Require Microsoft Entra-only authentication for Azure SQL Database, disabling local authentication methods. This allows access exclusively via Microsoft Entra identities, enhancing security with modern authentication enhancements including MFA, SSO, and secret-less programmatic access with managed identities.
2
1.0.0

Azure SQL Managed Instance should have Microsoft Entra-only authentication
Require Microsoft Entra-only authentication for Azure SQL Managed instance, disabling local authentication methods. This allows access exclusively via Microsoft Entra identities, enhancing security with modern authentication enhancements including MFA, SSO, and secret-less programmatic access with managed identities.
2
1.0.0

## Synapse

Name
Description
Policies
Version

Configure Synapse Workspaces to mandate Microsoft Entra-only identities for authentication
Require and configure Microsoft Entra-only authentication for Synapse Workspaces, disabling local authentication methods. This allows access exclusively via Microsoft Entra identities, enhancing security with modern authentication enhancements including MFA, SSO, and secret-less programmatic access with managed identities.
2
1.0.0

Synapse Workspaces should have Microsoft Entra-only authentication
Require Microsoft Entra-only authentication for Synapse Workspaces, disabling local authentication methods. This allows access exclusively via Microsoft Entra identities, enhancing security with modern authentication enhancements including MFA, SSO, and secret-less programmatic access with managed identities.
2
1.0.0

## Trusted Launch

Name
Description
Policies
Version

[Preview]: Configure prerequisites to enable Guest Attestation on Trusted Launch enabled VMs
Configure the Trusted Launch enabled virtual machines to automatically install the Guest Attestation extension and enable system-assigned managed identity to allow Azure Security Center to proactively attest and monitor the boot integrity. Boot integrity is attested via Remote Attestation. For more details, please refer to the following link - https://aka.ms/trustedlaunch
7
3.0.0-preview

## VirtualEnclaves

Name
Description
Policies
Version

[Preview]: Control the use of AKS in a Virtual Enclave
This initiative deploys Azure policies for AKS ensuring boundary protection of this resource while it operates within the logically separated structure of Azure Virtual Enclaves. https://aka.ms/VirtualEnclaves
9
1.0.0-preview

[Preview]: Control the use of App Service in a Virtual Enclave
This initiative deploys Azure policies for App Service ensuring boundary protection of this resource while it operates within the logically separated structure of Azure Virtual Enclaves. https://aka.ms/VirtualEnclaves
43
1.1.0-preview

[Preview]: Control the use of Container Registry in a Virtual Enclave
This initiative deploys Azure policies for Container Registry ensuring boundary protection of this resource while it operates within the logically separated structure of Azure Virtual Enclaves. https://aka.ms/VirtualEnclaves
8
1.0.0-preview

[Preview]: Control the use of CosmosDB in a Virtual Enclave
This initiative deploys Azure policies for CosmosDB ensuring boundary protection of this resource while it operates within the logically separated structure of Azure Virtual Enclaves. https://aka.ms/VirtualEnclaves
8
1.0.0-preview

[Preview]: Control the use of diagnostic settings for specific resources in a Virtual Enclave
This initiative deploys Azure policies to ensure configuration of specific resource types in Azure Virtual Enclaves. https://aka.ms/VirtualEnclaves
25
1.0.0-preview

[Preview]: Control the use of Key Vault in a Virtual Enclave
This initiative deploys Azure policies for Key Vaults ensuring boundary protection of this resource while it operates within the logically separated structure of Azure Virtual Enclaves. https://aka.ms/VirtualEnclaves
2
1.0.0-preview

[Preview]: Control the use of Microsoft SQL in a Virtual Enclave
This initiative deploys Azure policies for Microsoft SQL ensuring boundary protection of this resource while it operates within the logically separated structure of Azure Virtual Enclaves. https://aka.ms/VirtualEnclaves
24
1.0.0-preview

[Preview]: Control the use of PostgreSql in a Virtual Enclave
This initiative deploys Azure policies for PostgreSql ensuring boundary protection of this resource while it operates within the logically separated structure of Azure Virtual Enclaves. https://aka.ms/VirtualEnclaves
10
1.0.0-preview

[Preview]: Control the use of Service Bus in a Virtual Enclave
This initiative deploys Azure policies for Service Bus ensuring boundary protection of this resource while it operates within the logically separated structure of Azure Virtual Enclaves. https://aka.ms/VirtualEnclaves
7
1.0.0-preview

[Preview]: Control the use of Storage Accounts in a Virtual Enclave
This initiative deploys Azure policies for Storage Accounts ensuring boundary protection of this resource while it operates within the logically separated structure of Azure Virtual Enclaves. https://aka.ms/VirtualEnclaves
11
1.1.0-preview

## Next steps

- See the built-ins on the Azure Policy GitHub repo.

- Review the Azure Policy definition structure.

- Review Understanding policy effects.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-07-08
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
