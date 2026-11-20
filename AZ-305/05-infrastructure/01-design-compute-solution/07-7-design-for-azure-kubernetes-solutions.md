# Unit 7: 7-design-for-azure-kubernetes-solutions

Source: https://learn.microsoft.com/en-us/training/modules/design-compute-solution/7-design-for-azure-kubernetes-solutions

---

unit-inner-section" class="section is-uniform position-relative">
 
# Design for Azure Kubernetes Service solutions

 
 
 
 Completed
 
 
 

 

 
 
- 6 minutes

 
 

 

 
 Kubernetes is a portable, extensible open-source platform for automating deployment, scaling, and the management of containerized workloads. This orchestration platform provides the same ease of use and flexibility as with Platform as a Service (PaaS) and Infrastructure as a Service (IaaS) offerings. Kubernetes provides both container management and container orchestration.

Container management is the process of organizing, adding, removing, or updating a significant number of containers. Most of these tasks are manual and error prone. Container orchestration is a system that automatically deploys and manages containerized applications. The orchestrator can dynamically increase or decrease the deployed instances of the managed application. The orchestrator can also ensure all deployed container instances get updated if a new version of a service is released.

Azure Kubernetes Service (AKS) manages your hosted Kubernetes environment and makes it simple to deploy and manage containerized applications in Azure.

### Things to know about Azure Kubernetes Service

The Azure Kubernetes Service (AKS) environment is enabled with many features, such as automated updates, self-healing, and easy scaling. Review the following characteristics that make AKS an appealing compute option to build new workloads and support lift and shift migrations.

- AKS has three cluster management pricing tiers: Free, Standard, and Premium. The Free tier has no control plane charge but no SLA guarantee, suitable for dev/test. The Standard tier includes an hourly control plane charge with an uptime SLA, recommended for production. The Premium tier adds 24-month Long Term Support. All tiers require you to pay separately for agent node virtual machines.

- When you create the cluster, you can use Azure Resource Manager (ARM) templates or Bicep files. With these infrastructure-as-code options, you specify features such as advanced networking, Microsoft Entra ID integration, and monitoring.

- AKS gives you the benefits of open-source Kubernetes. You don't have the complexity or operational overhead of running your own custom Kubernetes cluster.

### Things to consider when using Azure Kubernetes Service

There are several factors to consider when deciding whether Azure Kubernetes Service is the right compute solution for your infrastructure. A good approach is to plan your strategy from two points of view. Consider the features from the approach of a green field new project, and also from the perspective of a lift-and-shift migration. The following features are configurable when you create a new cluster and also after you deploy.

Feature
Consideration
Solution

Identity and security management
Do you already use existing Azure resources and make use of Microsoft Entra ID?
You can configure an Azure Kubernetes Service cluster to integrate with Microsoft Entra ID and reuse existing identities and group membership.

Integrated logging and monitoring
Are you using Azure Monitor?
Azure Monitor provides performance visibility of the cluster.

Automatic cluster node and pod scaling
Do you need to scale up or down a large containerization environment?
AKS supports two auto cluster scaling options. The horizontal pod autoscaler watches the resource demand of pods and increases pods to meet demand. The cluster autoscaler component watches for pods that can't be scheduled because of node constraints. It automatically scales cluster nodes to deploy scheduled pods.

Cluster node upgrades
Do you want to reduce the number of cluster management tasks?
AKS manages Kubernetes software upgrades and the process of cordoning off nodes and draining them.

Storage volume support
Does your application require persisted storage?
AKS supports both static and dynamic storage volumes. Pods can attach and reattach to these storage volumes as they're created or rescheduled on different nodes.

Virtual network support
Do you need pod-to-pod network communication or access to on-premises networks from your AKS cluster?
An AKS cluster can be deployed into an existing virtual network with ease.

Application routing and ingress
Do you need to make your deployed applications publicly available?
AKS supports application routing through the application routing add-on. AKS is transitioning to the Kubernetes Gateway API as the long-term standard for ingress.

Docker image support
Do you already use Docker images for your containers?
By default, AKS supports the Docker file image format.

Private container registry
Do you need a private container registry?
AKS integrates with Azure Container Registry (ACR). You aren't limited to ACR though, you can use other container repositories, public, or private.

Tip

Learn more about Kubernetes in the Introduction to Kubernetes Service module.

 

 
 

 

 
 
 
 <section
