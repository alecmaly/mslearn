# https://learn.microsoft.com/en-us/azure/aks/what-is-aks

Source: https://learn.microsoft.com/en-us/azure/aks/what-is-aks

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
 

 

 

 

 
 
# What is Azure Kubernetes Service (AKS)?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Kubernetes Service (AKS) is a managed Kubernetes service for deploying and managing containerized applications. AKS offloads the complexity and operational overhead of managing Kubernetes to Azure. AKS offers two cluster modes:

- AKS Automatic: A fully managed experience with production-ready defaults. Azure handles node management, scaling, security, monitoring, and upgrades automatically. Recommended for most teams and workloads.

- AKS Standard: Full control over cluster configuration and node pool management. Recommended when you have specific infrastructure requirements or existing automation.

This article is intended for platform administrators or developers looking for a scalable, automated, managed Kubernetes solution. If you want to minimize operational overhead and get a production-ready cluster fast, AKS Automatic is purpose-built for you.

## Overview of AKS

AKS reduces the complexity and operational overhead of managing Kubernetes by shifting that responsibility to Azure. When you create an AKS cluster, Azure automatically creates and configures a control plane for you at no cost. The Azure platform manages the AKS control plane, which is responsible for the Kubernetes objects and worker nodes that you deploy to run your applications. Azure takes care of critical operations like health monitoring and maintenance, and you only pay for the AKS nodes that run your applications.

Note

AKS is CNCF-certified and is compliant with SOC, ISO, PCI DSS, and HIPAA. For more information, see the Microsoft Azure compliance overview.

## Choose your AKS mode

AKS offers two modes for creating and operating clusters. Use the following table to choose the mode that fits your needs:

Feature
AKS Automatic
AKS Standard

Best for
Developer teams, new workloads, quick onboarding, and production applications
Platform teams that require full infrastructure control

Node management
Fully managed - Azure provisions, scales, and upgrades nodes automatically by using node auto-provisioning
You create and manage node pools manually

Security defaults
Azure RBAC, Workload Identity, OIDC Issuer, deployment safeguards in enforcement mode, and Image Cleaner are all on by default
Opt-in per feature

Monitoring
Managed Prometheus, Container Insights, and Azure Monitor dashboards with Grafana are on by default
Opt-in per feature

Cluster upgrades
Automatic via the stable channel; OS image upgrades run on the NodeImage channel
Manual by default; automatic upgrade channel is optional

Scaling
HPA, KEDA, and VPA are preconfigured; nodes are created on demand
Manual scaling by default; cluster autoscaler and KEDA are optional

Pod readiness SLA
Financially backed guarantee: pod readiness SLA that guarantees 99.9% of qualifying pods ready within five minutes
Not included

Cluster pricing tier
Standard pricing tier with uptime SLA - included at no extra charge
Free pricing tier by default; Standard or Premium pricing tier is optional

Ingress
Managed NGINX with Azure DNS and Key Vault integration - preconfigured
Optional; bring your own ingress controller or use the application routing add-on

Use AKS Automatic when you want Azure to manage infrastructure operations so your team can focus on applications. Use AKS Standard when you need custom networking configurations, Windows node pools, specific VM SKUs not yet available in Automatic, or have existing automation built around manual cluster management.

For a full feature-by-feature comparison, see AKS Automatic and Standard feature comparison.

## Container solutions in Azure

Azure offers a range of container solutions designed to accommodate various workloads, architectures, and business needs.

Container solution
Resource type

Azure Kubernetes Service
Managed Kubernetes

Azure Red Hat OpenShift
Managed Kubernetes

Azure Arc-enabled Kubernetes
Unmanaged Kubernetes

Azure Container Instances (ACI)
Managed Docker container instance

Azure Container Apps
Managed Kubernetes

For more information comparing the various solutions, see the following resources:

- Comparing the service models of Azure container solutions

- Comparing Azure compute service options

## When to use AKS

Note

For most new workloads, we recommend using AKS Automatic. It comes production-ready with automatic node provisioning, built-in security defaults, preconfigured monitoring, automatic upgrades, and a pod readiness SLA that guarantees 99.9% of qualifying pods are ready within five minutes. No additional configuration is required to get these features. For more information, see What is AKS Automatic?

The following list describes some common use cases for AKS:

- Lift and shift to containers with AKS: Migrate existing applications to containers and run them in a fully managed Kubernetes environment.

- Microservices with AKS: Simplify the deployment and management of microservices-based applications with streamlined horizontal scaling, self-healing, load balancing, and secret management.

- Secure DevOps for AKS: Efficiently balance speed and security by implementing secure DevOps with Kubernetes.

- Bursting from AKS with ACI: Use virtual nodes to provision pods inside ACI that start in seconds and scale to meet demand.

- Machine learning model training with AKS: Train models using large datasets with familiar tools, such as TensorFlow and Kubeflow.

- Data streaming with AKS: Ingest and process real-time data streams with millions of data points collected via sensors, and perform fast analyses and computations to develop insights into complex scenarios.

- Using Windows containers on AKS: Run Windows Server containers on AKS to modernize your Windows applications and infrastructure.

## Features of AKS

The following table lists key features of AKS. Features marked Automatic: preconfigured are enabled by default on every AKS Automatic cluster and require no extra configuration.

Feature
Description

Identity and security management
â¢ Enforce regulatory compliance controls using Azure Policy with built-in guardrails and internet security benchmarks. 
 â¢ Integrate with Kubernetes RBAC to limit access to cluster resources. 
 â¢ Use Microsoft Entra ID to set up Kubernetes access based on existing identity and group membership. 
 Automatic: preconfigured - Azure RBAC for Kubernetes authorization, Workload Identity, OIDC Issuer, deployment safeguards in enforcement mode, and Image Cleaner are all on by default.

Logging and monitoring
â¢ Integrate with Container Insights, a feature in Azure Monitor, to monitor the health and performance of your clusters and containerized applications. 
 â¢ Set up Advanced Container Networking Services to collect and visualize network traffic data from your clusters. 
 Automatic: preconfigured - Managed Prometheus, Container Insights, and Azure Monitor dashboards with Grafana are on by default.

Streamlined deployments
â¢ Use prebuilt cluster configurations for Kubernetes with smart defaults. 
 â¢ Autoscale your applications using the Kubernetes Event-driven Autoscaling (KEDA). 
 â¢ Use Draft for AKS to ready source code and prepare your applications for production. 
 Automatic: preconfigured - HPA, KEDA, and VPA are enabled and ready to use on every Automatic cluster.

Clusters and nodes
â¢ Connect storage to nodes and pods, upgrade cluster components, and use GPUs. 
 â¢ Create clusters that run multiple node pools to support mixed operating systems and Windows Server containers. 
 â¢ Configure automatic scaling using the cluster autoscaler and horizontal pod autoscaler. 
 â¢ Deploy clusters with confidential computing nodes to allow containers to run in a hardware-based trusted execution environment. 
 Automatic: preconfigured - Node Auto-Provisioning fully manages node creation and scaling; no manual node pool configuration is required.

Storage volume support
â¢ Mount static or dynamic storage volumes for persistent data. 
 â¢ Use Azure Container Storage for fully managed, cloud-based volume management and orchestration of block storage. Azure Container Storage integrates with Kubernetes, allowing dynamic and automatic provisioning of persistent volumes. 
 â¢ Use Azure Disks CSI driver for single pod access and Azure Files CSI driver for multiple, concurrent pod access. 
 â¢ Use Azure NetApp Files for high-performance, high-throughput, and low-latency file shares.

Networking
â¢ Choose from our networking options for your needs. 
 â¢ Bring your own Container Network Interface (CNI) to use a third-party CNI plugin. 
 â¢ Easily access applications deployed to your clusters using the application routing add-on with nginx. 
 Automatic: preconfigured - Azure CNI Overlay powered by Cilium for high-performance networking, managed NGINX ingress with Azure DNS and Key Vault integration, and a managed NAT gateway for egress are configured by default.

Development tooling integration
â¢ Develop on AKS with Helm. 
 â¢ Install the Kubernetes extension for Visual Studio Code to manage your workloads. 
 â¢ Leverage the features of Istio with the Istio-based service mesh add-on.

## Get started with AKS

### Get started with AKS Automatic (recommended)

AKS Automatic is the fastest path to a production-ready cluster with built-in security, monitoring, and autoscaling. Choose a quickstart based on where you're starting from:

- Start from a container image: Deploy an AKS Automatic cluster - get a fully configured cluster in minutes.

- Start from source code: Go from source code to Kubernetes with AKS Automatic - automated deployments generate Kubernetes manifests and CI/CD workflows directly from your repository.

### Get started with AKS Standard

Use AKS Standard when you need full control over cluster configuration:

- Learn the core Kubernetes concepts for AKS.

- Evaluate application deployment on AKS with our AKS tutorial series.

### Resources for all AKS users

- Review the Azure Well-Architected Framework for AKS to learn how to design and operate reliable, secure, efficient, and cost-effective applications on AKS.

- Plan your design and operations for AKS using our reference architectures.

- Explore configuration options and recommended best practices for cost optimization on AKS.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-06-04
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
