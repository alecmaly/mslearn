# https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-decision-tree

Source: https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-decision-tree

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
 

 

 

 

 
 
# Choose an Azure compute service

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure provides many ways to host your application code. The term compute refers to the hosting model for the resources that your application runs on. This article helps you choose the right compute service for your scenario and focuses on general-purpose compute offerings.

## Architecture

Use the following flowchart to select a candidate compute service.

The image shows a flowchart for selecting an appropriate Azure service based on whether the user migrates an existing workload or builds a new workload. The flowchart begins with a start node and splits into two primary branches labeled migrate and build new. The migrate branch includes decision points that assess whether the application is optimized for the cloud and whether it can be lifted and shifted. Depending on the answers, the flow leads to services like Azure App Service, Azure VMware Solution, or Azure Virtual Machines. The build new branch includes decision points that evaluate the need for full control, high-performance computing (HPC), event-driven workloads, managed web hosting, and orchestration requirements. These decisions guide the user toward services like Virtual Machines, Azure Batch, Azure Functions, App Service, Azure Container Instances, Azure Red Hat OpenShift, Azure Kubernetes Service (AKS), or Azure Container Apps. A branching section for your own orchestration implementation on Virtual Machines includes Kubernetes on Virtual Machines and OpenShift on Virtual Machines. At the bottom of the image, two boxed sections list container-exclusive services and container-compatible services. The container-exclusive section includes Container Instances, Azure Red Hat OpenShift, Kubernetes on Virtual Machines, and OpenShift on Virtual Machines. The container-compatible section includes Azure Batch, Azure Functions, and App Service.

Download a Visio file of this architecture.

The previous diagram refers to two migration strategies:

- Lift and shift: A strategy for migrating a workload to the cloud without redesigning the application or making code changes. It's also known as rehosting. We recommend that workload teams that perform migrations use a like-for-like approach and defer optimization unless their timeline and budget support redesign for cloud-native functionality. For more information, see Migrate workloads to Azure from other cloud platforms.

- Cloud optimized: A strategy for migrating to the cloud by refactoring an application to take advantage of cloud-native features and capabilities. You can also use this strategy to describe greenfield (new) workloads designed from the start to use cloud-native features.

The output from this flowchart is your starting point. Then evaluate the service to see whether it meets your needs.

This article includes several tables that can help you choose a service. The initial candidate from the flowchart might not suit your application or workload. In that case, expand your analysis to include other compute services.

If your workload consists of distinct compute components, evaluate each application's needs separately. A complete solution can include two or more compute services.

## Understand the basic features

If you're unfamiliar with the Azure service that you select in the previous section, see the following overview documentation:

- Azure Virtual Machines is a service that you can use to deploy and manage virtual machines (VMs) inside an Azure virtual network.

- Azure App Service is a managed service for hosting web apps, mobile app back ends, RESTful APIs, or automated business processes.

- Azure Functions is a service that provides managed functions that run based on various trigger types for event-driven applications.

- Azure Kubernetes Service (AKS) is a managed Kubernetes service for running containerized applications. It provides direct access to the Kubernetes API and control plane.

- Azure Container Apps is a managed service built on Kubernetes, which simplifies the deployment of containerized applications in a serverless environment. It doesn't provide direct access to the underlying Kubernetes APIs. Use AKS if you require access to the Kubernetes APIs and control plane.

- Azure Container Instances is a service for running a single container or group of containers in Azure. Container Instances doesn't provide full container orchestration, but you can implement containers without the need to provision VMs or adopt a higher-level service.

- Azure Red Hat OpenShift is a fully managed OpenShift cluster for running containers in production with Kubernetes.

- Azure Batch is a managed service for running large-scale parallel and high-performance computing (HPC) applications.

- Azure VMware Solution is a managed service for running VMware workloads natively on Azure.

## Understand the hosting models

For hosting models, cloud services fall into three categories:

- Infrastructure as a service (IaaS) lets you provision VMs along with the associated networking and storage components. You can then deploy any software and applications on those VMs. This model is the most similar to a traditional on-premises environment. Microsoft manages the infrastructure, and you manage the VMs.

- Platform as a service (PaaS) provides a managed hosting environment where you can deploy your application without the need to manage VMs. App Service and Container Apps are PaaS services.

- Functions as a service (FaaS) lets you deploy your code to the service, which automatically runs it. Azure Functions is a FaaS service.

Note

Azure Functions is an Azure serverless compute offering. To see how this service compares with other Azure serverless offerings, like Azure Logic Apps for serverless workflows, see Choose the right integration and automation services in Azure.

Cloud compute services range from IaaS to fully managed FaaS. For example, Azure VMs can automatically scale by using virtual machine scale sets. Automatic scaling capabilities are often associated with PaaS or FaaS, but capabilities vary by service rather than by compute category.

A trade-off exists between control and ease of management. IaaS provides the most control, flexibility, and portability, but you must provision, set up, and manage the VMs and network components that you create. FaaS services automatically manage nearly all aspects of running an application. PaaS provides partial management and requires some user configuration.

Service
Application composition
Density
Minimum number of nodes
State management
Web hosting

Virtual Machines
Agnostic
Agnostic
1 1
Stateless or stateful
Agnostic

App Service
Applications, containers
Multiple apps for each instance by using an App Service plan
1
Stateless
Built-in

Azure Functions
Functions, containers
Serverless 2
Serverless 2
Stateless or stateful 3
Not applicable

AKS
Containers
Multiple containers for each node
Production: 6 4
Stateless or stateful
Agnostic

Container Apps
Containers
Serverless
Serverless
Stateless or stateful
Agnostic

Container Instances
Containers
No dedicated instances
No dedicated nodes
Stateless
Agnostic

Azure Red Hat OpenShift
Containers
Multiple containers for each node
6 5
Stateless or stateful
Agnostic

Batch
Scheduled jobs
Multiple apps for each VM
1 6
Stateless
No

Azure VMware Solution
Agnostic
Agnostic
3 7
Stateless or stateful
Agnostic

Notes:

1 Higher service-level agreement (SLA) that has two or more instances.

2 For Azure Functions, the Consumption and Flex Consumption plans are serverless. For an App Service plan, functions run on the VMs allocated for that plan. Choose the right service plan for Azure Functions.

3 When you use durable functions.

4 Three in the system node pool and three for each user node pool.

5 Three primary nodes and three worker nodes.

6 Can scale down to zero after the job completes.

7 See Hosts.

For more information, see Choose an Azure container service.

## Networking

Your application platform likely needs to interface with networks both as a server for your applications and as a client. For example, it might function as a client to get operating system (OS) updates. You must select a platform that supports both your east-west and north-south traffic requirements.

Service
Virtual network integration
Hybrid connectivity

Virtual Machines
Supported
Supported

App Service
Supported 1
Supported 2

Azure Functions
Supported 1
Supported 3

AKS
Supported
Supported

Container Apps
Supported
Supported

Container Instances
Supported
Supported

Azure Red Hat OpenShift
Supported
Supported

Batch
Supported
Supported

Azure VMware Solution
Supported
Supported

Notes:

1 Requires Basic tier or higher, or App Service Environment. See virtual network integration.

2 Use App Service Hybrid Connections.

3 Requires an App Service plan, Azure Functions Premium plan, or Azure Functions Flex Consumption plan.

## DevOps

Service
Local debugging
Remote debugging
Programming model
Application update

Virtual Machines
Agnostic
Remote Tools for Visual Studio
Agnostic
No built-in support

App Service
IIS Express, others 1
Limited support
Web and API applications, WebJobs for background tasks
Deployment slots

Azure Functions
Visual Studio or Azure Functions Core Tools
Not supported
Serverless, event-driven
Deployment slots

AKS
Minikube, Docker, others
Non-Microsoft tools 2
Agnostic
Rolling update

Container Apps
Local container runtime
Debug console
Agnostic
Revision management

Container Instances
Local container runtime
Not supported
Agnostic
Not applicable

Azure Red Hat OpenShift
Minikube, Docker, others
Non-Microsoft tools 2
Agnostic
Rolling update

Batch
Not supported
Not applicable
Command-line application
Not applicable

Azure VMware Solution
Agnostic
Remote Tools for Visual Studio
Agnostic
No built-in support

Notes:

1 Options include IIS Express, Visual Studio Code, and other standard development tools based on your application stack.

2 Use non-Microsoft tools like Telepresence or mirrord for local-to-cluster debugging.

## Team skills and operational overhead

Service
Required skills
Operational overhead
Best for teams that have these characteristics

Virtual Machines
OS administration, networking, security patching
High: Full infrastructure management
Traditional IT operations experience

App Service
Web development, application deployment
Low: Platform handles infrastructure
Application developers focused on code

Azure Functions
Event-driven programming, serverless patterns
Very low: Serverless management
Developers who build event-driven solutions

AKS
Kubernetes administration, container orchestration
High: Cluster management, upgrades, security
DevOps teams that have Kubernetes expertise

Container Apps
Container basics, cloud-native patterns
Low: Abstracted Kubernetes management
Teams that want modern patterns without Kubernetes complexity

Container Instances
Container basics
Very low: No orchestration
Teams that need simple container execution

Azure Red Hat OpenShift
OpenShift or Kubernetes administration
High: Cluster management
Teams that have OpenShift investment

Batch
Job scheduling, parallel processing
Medium: Job and pool management
Teams that run HPC or batch workloads

Azure VMware Solution
VMware administration
Medium: VMware-managed infrastructure
Teams that have VMware platform requirements

## Scalability

Service
Autoscaling
Load balancer
Scale limit

Virtual Machines
Virtual machine scale sets
Azure Load Balancer
- Platform image: 1,000 nodes for each scale set 

 - Custom image: 600 nodes for each scale set

App Service
Built-in service
Integrated
Plan limits: 30 instances per Premium v2, v3, or v4 plan; 100 per Isolated v2 plan (more allowed upon request). 

 App Service Environment v3: 200 instances total across all plans in one environment. Dedicated-host deployments are limited by available cores.

Azure Functions
Built-in service
Integrated
Varies by hosting plan. Examples: 

 Flex Consumption: Up to 1,000 on-demand instances per function group. 

 Premium: Up to 100 instances per plan. 

 See hosting plan scaling limits for all options and qualifications.

AKS
Pod autoscaling1, cluster autoscaling2
Load Balancer or Azure Application Gateway
5,000 nodes when you use Standard or Premium tier

Container Apps
Scaling rules3
Integrated
1,000 replicas for each revision, 15 environments in each region

Container Instances
Not supported
No built-in support
100 container groups for each subscription (default limit)

Azure Red Hat OpenShift
Pod autoscaling, cluster autoscaling
Load Balancer or Application Gateway
250 nodes for each cluster (default limit)

Batch
Not applicable
Load Balancer
Core limit of 900 dedicated cores and 100 low-priority cores (default limit)

Azure VMware Solution
Built-in service4
Integrated5
3 to 16 VMware ESXi hosts for each VMware vCenter

Notes:

1 See Autoscale pods.

2 See Scale a cluster automatically to meet application demands on AKS.

3 See Set scaling rules in Container Apps.

4 See Scale clusters in a private cloud.

5 See VMware NSX.

## Built-in multiregion capabilities

All of the application platforms that this decision guide addresses are regional. They require external routing to enable multiregion topologies, such as active-active for resiliency or active-passive for recoverability. When you deploy multiple instances of the application platform, with at least one instance in each region, an external router or load balancer can direct traffic where needed across regions.

Service
Multiregion option

Virtual Machines
Single region only. 

 Must use external router combined with multiple VM deployments.

App Service
Single region only. 

 Must use external router combined with multiple App Service Plan instances.

Azure Functions
Single region only. 

 Must use external router combined with multiple host instances.

AKS
Single region only. 

 Must use external router combined with multiple clusters.

Container Apps
Single region only. 

 Must use external router combined with multiple Container Apps environments.

Container Instances
Single region only.

Azure Red Hat OpenShift
Single region only. 

 Must use external router combined with multiple clusters.

Batch
Single region only.

Azure VMware Solution
Single region only. 

 Must use external router combined with multiple Azure VMware Solution instances.

## Security

Review and understand the available security controls and visibility for each of the following services:

- Virtual Machines for Linux

- Virtual Machines for Windows

- App Service

- Azure Functions

- AKS

- Container Apps

- Container Instances

- Azure VMware Solution

## Other criteria

Service
Transport Layer Security (TLS)
Cost
Graphics processing unit (GPU) support
Suitable architecture styles

Virtual Machines
Set up in VM
Windows, 
 Linux
Supported
N-tier, big compute (HPC)

App Service
Supported
App Service pricing
Not supported
Web-queue-worker

Azure Functions
Supported
Azure Functions pricing
Not supported
Microservices, event-driven architecture

AKS
Ingress controller
AKS pricing
Supported
Microservices, event-driven architecture

Container Apps
Ingress controller
Container Apps pricing
Supported
Microservices, event-driven architecture

Container Instances
Use sidecar container
Container Instances pricing
Not supported
Microservices, task automation, batch jobs

Azure Red Hat OpenShift
Supported
Azure Red Hat OpenShift pricing
Supported
Microservices, event-driven architecture

Batch
Supported
Batch pricing
Supported
Big compute (HPC)

Azure VMware Solution
Set up in VM
Azure VMware Solution pricing
Not supported
VM workload based on VMware format

## Consider limits and cost

Use the previous comparison tables as context and evaluate the following aspects of the candidate service in more detail:

- Azure pricing and cost calculator

- Azure service availability by region

- Service limits

- SLAs

## Specialty workloads

Some workloads have specific requirements and don't typically follow the general recommendations in this application platform selection guide. These workloads are usually software or database products that have characteristics that limit the service options to a narrow set of supported choices.

Scenario
Explore these options

HPC scheduling
Azure CycleCloud

SAP on Azure VMs
Use Azure to host and run SAP workload scenarios

Oracle on Azure VMs
Oracle databases on Azure infrastructure 

 Applications on Oracle Linux and WebLogic server

Complex, intermixed state and compute with opinionated programming models
Azure Service Fabric

Mainframe
Refactor a mainframe application for Azure

Marketplace offerings
Browse partner offerings on Azure compute

Quantum computing
Azure Quantum

Virtual desktop hosting
Virtual desktop architecture design

Bare metal or dedicated compute workloads
Azure Dedicated Hosts 

 Nutanix Cloud Clusters on Azure

## Contributors

Microsoft maintains this article. The following contributors wrote this article.

- Ayobami Ayodeji | Senior Program Manager

- Jelle Druyts | Principal Service Engineer

- Martin Gjoshevski | Senior Service Engineer

- Phil Huang | Senior Cloud Solution Architect

- Julie Ng | Senior Service Engineer

- Paolo Salvatori | Principal Service Engineer

To see nonpublic LinkedIn profiles, sign in to LinkedIn.

## Next step

- Azure compute options

## Related resources

- Choose an Azure compute option for microservices

- Technology choices for Azure solutions

 
 

 
 

 

 
 
 
 
 
 
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
 2026-02-19
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
