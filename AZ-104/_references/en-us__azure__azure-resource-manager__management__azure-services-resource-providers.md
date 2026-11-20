# https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/azure-services-resource-providers

Source: https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/azure-services-resource-providers

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
 

 

 

 

 
 
# What are the resource providers for Azure services

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 A resource provider is a collection of REST operations that enables functionality for an Azure service. Each resource provider has a namespace in the format of `company-name.service-label`. This article shows the resource providers for Azure services. If you don't know the resource provider, see Find resource provider.

## AI and machine learning resource providers

The resource providers for AI and machine learning services are:

Resource provider namespace
Azure service

Microsoft.AutonomousSystems
Autonomous Systems

Microsoft.BotService
Azure Bot Service

Microsoft.CognitiveServices
Cognitive Services

Microsoft.EnterpriseKnowledgeGraph
Enterprise Knowledge Graph

Microsoft.MachineLearningServices
Azure Machine Learning

Microsoft.Search
Azure AI Search

## Analytics resource providers

The resource providers for analytics services are:

Resource provider namespace
Azure service

Microsoft.AnalysisServices
Azure Analysis Services

Microsoft.Databricks
Azure Databricks

Microsoft.DataCatalog
Data Catalog

Microsoft.DataFactory
Data Factory

Microsoft.DataLakeAnalytics
Data Lake Analytics

Microsoft.DataLakeStore
Azure Data Lake Storage Gen2

Microsoft.DataShare
Azure Data Share

Microsoft.HDInsight
HDInsight

Microsoft.Kusto
Azure Data Explorer

Microsoft.PowerBI
Power BI

Microsoft.PowerBIDedicated
Power BI Embedded

Microsoft.ProjectBabylon
Azure Data Catalog

Microsoft.Purview
Microsoft Purview

Microsoft.StreamAnalytics
Azure Stream Analytics

Microsoft.Synapse
Azure Synapse Analytics

## Blockchain resource providers

The resource providers for Blockchain services are:

Resource provider namespace
Azure service

Microsoft.Blockchain
Azure Blockchain Service

Microsoft.BlockchainTokens
Azure Blockchain Tokens

## Compute resource providers

The resource providers for compute services are:

Resource provider namespace
Azure service

Microsoft.AppPlatform
Azure Spring Apps

Microsoft.AVS
Azure VMware Solution

Microsoft.Batch
Batch

Microsoft.ClassicCompute
Classic deployment model virtual machine

Microsoft.Compute
Virtual Machines
Virtual Machine Scale Sets

Microsoft.DesktopVirtualization
Azure Virtual Desktop

Microsoft.DevTestLab
Azure Lab Services

Microsoft.HanaOnAzure
SAP HANA on Azure Large Instances

Microsoft.LabServices
Azure Lab Services

Microsoft.Maintenance
Azure Maintenance

Microsoft.Microservices4Spring
Azure Spring Apps

Microsoft.Quantum
Azure Quantum

Microsoft.SerialConsole - registered by default
Azure Serial Console for Windows

Microsoft.ServiceFabric
Service Fabric

Microsoft.VirtualMachineImages
Azure Image Builder

Microsoft.VMware
Azure VMware Solution

Microsoft.VMwareCloudSimple
Azure VMware Solution by CloudSimple

## Container resource providers

The resource providers for container services are:

Resource provider namespace
Azure service

Microsoft.App
Azure Container Apps

Microsoft.ContainerInstance
Container Instances

Microsoft.ContainerRegistry
Container Registry

Microsoft.ContainerService
Azure Kubernetes Service (AKS)

Microsoft.RedHatOpenShift
Azure Red Hat OpenShift

## Core resource providers

The resource providers for core services are:

Resource provider namespace
Azure service

Microsoft.Addons
core

Microsoft.AzureStack
core

Microsoft.Capacity
core

Microsoft.Commerce - registered by default
core

Microsoft.Marketplace
core

Microsoft.MarketplaceApps
core

Microsoft.MarketplaceOrdering - registered by default
core

Microsoft.SaaS
core

Microsoft.Services
core

Microsoft.Subscription
core

microsoft.support - registered by default
core

## Database resource providers

The resource providers for database services are:

Resource provider namespace
Azure service

Microsoft.Cache
Azure Managed Redis and Azure Cache for Redis 

Note: Azure Cache for Redis is being retired. For more information, see Azure Cache for Redis retirement FAQ.

Microsoft.DBforMariaDB
Azure Database for MariaDB

Microsoft.DBforMySQL
AzureÃ Database for MySQL

Microsoft.DBforPostgreSQL
Azure Database for PostgreSQL

Microsoft.DocumentDB
Azure Cosmos DB
 Azure DocumentDB

Microsoft.Sql
Azure SQL Database
 Azure SQL Managed Instance 
Azure Synapse Analytics

Microsoft.SqlVirtualMachine
SQL Server on Azure Virtual Machines

Microsoft.AzureData
SQL Server enabled by Azure Arc

## Developer tools resource providers

The resource providers for developer tools services are:

Resource provider namespace
Azure service

Microsoft.AppConfiguration
Azure App Configuration

Microsoft.DevCenter
Microsoft Dev Box

Microsoft.DevSpaces
Azure Dev Spaces

Microsoft.LoadTestService
Azure Load Testing

Microsoft.Notebooks
Azure Notebooks

## DevOps resource providers

The resource providers for DevOps services are:

Resource provider namespace
Azure service

microsoft.visualstudio
Azure DevOps

Microsoft.VSOnline
Azure DevOps

Microsoft.DevOpsInfrastructure
Managed DevOps Pools

## Hybrid resource providers

The resource providers for hybrid services are:

Resource provider namespace
Azure service

Microsoft.AzureArcData
Azure Arc-enabled data services

Microsoft.AzureStackHCI
Azure Local

Microsoft.HybridCompute
Azure Arc-enabled servers

Microsoft.Kubernetes
Azure Arc-enabled Kubernetes

Microsoft.KubernetesConfiguration
Azure Arc-enabled Kubernetes

Microsoft.Edge
Azure Arc site manager

## Identity resource providers

The resource providers for identity services are:

Resource provider namespace
Azure service

Microsoft.AAD
Microsoft Entra Domain Services

Microsoft.ADHybridHealthService - registered by default
Microsoft Entra ID

Microsoft.AzureActiveDirectory
Microsoft Entra ID B2C

Microsoft.ManagedIdentity
Managed identities for Azure resources

Microsoft.Token
Token

## Integration resource providers

The resource providers for integration services are:

Resource provider namespace
Azure service

Microsoft.ApiManagement
API Management

Microsoft.Communication
Azure Communication Services

Microsoft.EventGrid
Event Grid

Microsoft.EventHub
Event Hubs

Microsoft.HealthcareApis (Azure API for FHIR)
Azure API for FHIR

Microsoft.HealthcareApis (Healthcare APIs)
Healthcare APIs

Microsoft.Logic
Logic Apps

Microsoft.NotificationHubs
Notification Hubs

Microsoft.PowerPlatform
Power Platform

Microsoft.Relay
Azure Relay

Microsoft.ServiceBus
Service Bus

## IoT resource providers

The resource providers for IoT services are:

Resource provider namespace
Azure service

Microsoft.IoTOperations
Azure IoT Operations

Microsoft.DeviceRegistry
Azure Device Registry

Microsoft.Devices
Azure IoT Hub
Azure IoT Hub Device Provisioning Service

Microsoft.DeviceUpdate
Device Update for IoT Hub

Microsoft.DigitalTwins
Azure Digital Twins

Microsoft.IoTSpaces
Azure Digital Twins

Microsoft.IoTCentral
Azure IoT Central

Microsoft.WindowsIoT
Windows 10 IoT Core Services

## Management resource providers

The resource providers for management services are:

Resource provider namespace
Azure service

Microsoft.Advisor
Azure Advisor

Microsoft.Authorization - registered by default
Azure Resource Manager

Microsoft.Automation
Automation

Microsoft.Billing - registered by default
Cost Management and Billing

Microsoft.Blueprint
Azure Blueprints

Microsoft.ChangeSafety - registered by default
Safety checks that help Microsoft reduce risk and improve reliability in Microsoft service deployment

Microsoft.ClassicSubscription - registered by default
Classic deployment model

Microsoft.Consumption - registered by default
Cost Management

Microsoft.CostManagement - registered by default
Cost Management

Microsoft.CostManagementExports
Cost Management

Microsoft.CustomProviders
Azure Custom Providers

Microsoft.DynamicsLcs
Lifecycle Services

Microsoft.Features - registered by default
Azure Resource Manager

Microsoft.GuestConfiguration
Azure Policy

Microsoft.ManagedServices
Azure Lighthouse

Microsoft.Management
Management Groups

Microsoft.PolicyInsights
Azure Policy

Microsoft.Portal - registered by default
Azure portal

Microsoft.RecoveryServices
Azure Site Recovery

Microsoft.ResourceGraph - registered by default
Azure Resource Graph

Microsoft.ResourceHealth
Azure Service Health

Microsoft.ResourceNotification - registered by default
Azure Resource Notifications

Microsoft.Resources - registered by default
Azure Resource Manager

Microsoft.Scheduler
Scheduler

Microsoft.SoftwarePlan
License

Microsoft.Solutions
Azure Managed Applications

## Migration resource providers

The resource providers for migration services are:

Resource provider namespace
Azure service

Microsoft.ClassicInfrastructureMigrate
Classic deployment model migration

Microsoft.DataBox
Azure Data Box

Microsoft.DataBoxEdge
Azure Stack Edge

Microsoft.DataMigration
Azure Database Migration Service

Microsoft.OffAzure
Azure Migrate

Microsoft.Migrate
Azure Migrate

## Monitoring resource providers

The resource providers for monitoring services are:

Resource provider namespace
Azure service

Microsoft.AlertsManagement
Azure Monitor

Microsoft.ChangeAnalysis
Azure Monitor

Microsoft.Insights
Azure Monitor

Microsoft.Intune
Azure Monitor

Microsoft.Monitor
Azure Monitor

Microsoft.OperationalInsights
Azure Monitor

Microsoft.OperationsManagement
Azure Monitor

Microsoft.WorkloadMonitor
Azure Monitor

## Network resource providers

The resource providers for network services are:

Resource provider namespace
Azure service

Microsoft.Cdn
Content Delivery Network

Microsoft.ClassicNetwork
Classic deployment model virtual network

Microsoft.ManagedNetwork
Virtual networks managed by PaaS services

Microsoft.Network
Application Gateway
Azure Bastion
Azure DDoS Protection
Azure DNS
Azure ExpressRoute
Azure Firewall
Azure Front Door Service
Azure Private Link
Azure Route Server
Load Balancer
Network Watcher
Traffic Manager
Virtual Network
Virtual Network NAT
 Virtual Network Manager
Virtual WAN
VPN Gateway

Microsoft.Peering
Azure Peering Service

## Security resource providers

The resource providers for security services are:

Resource provider namespace
Azure service

Microsoft.Attestation
Azure Attestation Service

Microsoft.CustomerLockbox
Customer Lockbox for Microsoft Azure

Microsoft.DataProtection
Data Protection

Microsoft.HardwareSecurityModules
Azure Dedicated HSM

Microsoft.KeyVault
Key Vault

Microsoft.Security
Security Center

Microsoft.SecurityInsights
Microsoft Sentinel

Microsoft.WindowsDefenderATP
Microsoft Defender Advanced Threat Protection

Microsoft.WindowsESU
Extended Security Updates

## Storage resource providers

The resource providers for storage services are:

Resource provider namespace
Azure service

Microsoft.ClassicStorage
Classic deployment model storage

Microsoft.ElasticSan
Elastic SAN

Microsoft.HybridData
StorSimple

Microsoft.ImportExport
Azure Import/Export

Microsoft.NetApp
Azure NetApp Files

Microsoft.ObjectStore
Object Store

Microsoft.Storage
Storage

Microsoft.StorageCache
Azure HPC Cache

Microsoft.StorageSync
Storage

Microsoft.StorSimple
StorSimple

## Web resource providers

The resource providers for web services are:

Resource provider namespace
Azure service

Microsoft.BingMaps
Bing Maps

Microsoft.CertificateRegistration
App Service Certificates

Microsoft.DomainRegistration
App Service

Microsoft.Maps
Azure Maps

Microsoft.SignalRService
Azure SignalR Service

Microsoft.Web
App Service
Azure Functions

## 5G & Space resource providers

The resource providers for 5G & space services are:

Resource provider namespace
Azure service

Microsoft.HybridNetwork
Network Function Manager

Microsoft.MobileNetwork
Azure Private 5G Core

## Registration

Resource providers marked with - registered by default in the previous section are automatically registered for your subscription. For other resource providers, you need to register them. However, many resource providers are registered automatically when you perform specific actions. For example, when you create resources through the portal or by deploying an Azure Resource Manager template, Azure Resource Manager automatically registers any required unregistered resource providers.

Important

Register a resource provider only when you're ready to use it. This registration step helps maintain least privileges within your subscription. A malicious user can't use unregistered resource providers.

Registering unnecessary resource providers may result in unrecognized apps appearing in your Microsoft Entra tenant. Microsoft adds the app for a resource provider when you register it. These apps are typically added by the Windows Azure Service Management API. To prevent unnecessary apps in your tenant, only register needed resource providers.

## Find resource provider

To identify resource providers used for your existing Azure infrastructure, list the deployed resources. Specify the resource group containing the resources.

The following example uses Azure CLI:

`az resource list --resource-group examplegroup
`

The results include the resource type. The resource provider namespace is the first part of the resource type. The following example shows the Microsoft.KeyVault resource provider.

`[
 {
 ...
 "type": "Microsoft.KeyVault/vaults"
 }
]
`

The following example uses PowerShell:

`Get-AzResource -ResourceGroupName examplegroup
`

The results include the resource type. The resource provider namespace is the first part of the resource type. The following example shows the Microsoft.KeyVault resource provider.

`Name : examplekey
ResourceGroupName : examplegroup
ResourceType : Microsoft.KeyVault/vaults
...
`

The following example uses Python:

`import os
from azure.identity import DefaultAzureCredential
from azure.mgmt.resource import ResourceManagementClient

subscription_id = os.environ["AZURE_SUBSCRIPTION_ID"]
credential = DefaultAzureCredential()
resource_client = ResourceManagementClient(credential, subscription_id)

resource_group_name = "examplegroup"
resources = resource_client.resources.list_by_resource_group(resource_group_name)

for resource in resources:
 print(resource.type)
`

The results list the resource type. The resource provider namespace is the first part of the resource type. The following example shows the Microsoft.KeyVault resource provider.

`Microsoft.KeyVault/vaults
`

## Next steps

For more information about resource providers, including how to register a resource provider, see Azure resource providers and types.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-02-27
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
