# https://learn.microsoft.com/en-us/azure/azure-monitor/reference/supported-metrics/metrics-index

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/reference/supported-metrics/metrics-index

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
 

 

 

 

 
 
# Supported metrics with Azure Monitor

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This article is a list of platform, or automatically collected metrics currently available in Azure Monitor. To query for and access the list of metrics programmatically, use the 2018-01-01 api-version. Other metrics not in this list might be available in the portal or through legacy APIs.

The metrics are organized by resource provider and resource type. For a list of services and the resource providers and types that belong to them, see Resource providers for Azure services.

## Exporting platform metrics to other locations

You can export the platform metrics from the Azure monitor using the following methods:

- Metrics export via data collection rules (DCRs).

- Diagnostic settings.

- The metrics REST API.

Both metrics export via DCRs and diagnostic settings export metrics to the following locations:

- Azure Storage Accounts.

- Log Analytics workspaces.

- Event Hubs, allowing you to further export to non-Microsoft systems.

Using diagnostic settings is the easiest way to route the metrics, but there are some limitations:

- Exportability. All metrics are exportable through the REST API, but some can't be exported through diagnostic settings because of intricacies in the Azure Monitor backend. The column "Exportable via Diagnostic Settings" in the following tables lists which metrics can be exported in this way.

- Multi-dimensional metrics. Sending multi-dimensional metrics to other locations is supported by metrics export via data collection rules (DCRs). Exporting multiple dimensions via diagnostic settings isn't supported. Metrics with dimensions are exported by diagnostic settings as flattened single-dimensional metrics, aggregated across dimension values. For example, the Incoming Messages metric on an event hub can be explored and charted on a per-queue level. But when the metric is exported via diagnostic settings, it's represented as all incoming messages across all queues in the event hub.

## Guest OS and host OS metrics

Metrics for the guest operating system (guest OS) that runs in Azure Virtual Machines, Service Fabric, and Cloud Services are not listed here. Guest OS metrics must be collected through the Azure Monitor Agent that runs on or as part of the guest operating system. Guest OS metrics include performance counters that track guest CPU percentage or memory usage, both of which are frequently used for autoscaling or alerting. For a list of guest OS metrics, see Virtual machine guest performance counters.

Host OS metrics are available and listed in the tables. Host OS metrics relate to the Hyper-V session that's hosting your guest OS session.

Tip

A best practice is to use and configure the Azure Monitor agent to send guest OS performance metrics into the same Azure Monitor metric database where platform metrics are stored. The agent routes guest OS metrics through the custom metrics API. You can then chart, alert, and otherwise use guest OS metrics like platform metrics.

Alternatively or in addition, you can send the guest OS metrics to Azure Monitor Logs by using the same agent. There you can query on those metrics in combination with non-metric data by using Log Analytics. Standard Log Analytics workspace costs would then apply.

The Azure Monitor agent replaces the Azure Diagnostics extension and Logs Analytics agent, which were previously used for guest OS routing. For important additional information, see Overview of Azure Monitor agents.

## Supported metrics and log categories by resource type

Following table lists metrics and log categories available for each resource type.

Resource Provider
Metrics
Log Categories

`Microsoft.AAD` 
`DomainServices`
`DomainServices`

`Microsoft.AgFoodPlatform` 
N/A
`farmBeats`

`Microsoft.`
`AnalysisServices` 
`servers`
`servers`

`Microsoft.ApiManagement` 
`gateways`
`service`
`service`
`service/workspaces`

`Microsoft.App` 
`containerapps`
`jobs`
`managedEnvironments`
`sandboxgroups`
`sessionpools`
`managedEnvironments`

`Microsoft.`
`AppConfiguration` 
`configurationStores`
`configurationStores`

`Microsoft.AppLink` 
N/A
`applinks/applinkmembers`

`Microsoft.AppPlatform` 
`spring`
`spring`

`Microsoft.Attestation` 
N/A
`attestationProviders`

`Microsoft.Automation` 
`automationAccounts`
`automationAccounts`

`Microsoft.`
`AutonomousDevelopmentPlatform` 
N/A
`accounts`
`workspaces`

`microsoft.avs` 
`privateClouds`
`privateClouds`

`Microsoft.`
`AzureDataTransfer` 
`connections/flows`
`connections/flows`

`microsoft.`
`azureplaywrightservice` 
N/A
`accounts`

`microsoft.azuresphere` 
`catalogs`
`catalogs`

`Microsoft.Batch` 
`batchaccounts`
`batchaccounts`

`microsoft.botservice` 
`botservices`
`botservices`

`Microsoft.Cache` 
`redis`
`redisEnterprise`
`redis`
`redisEnterprise/databases`

`Microsoft.Cdn` 
`cdnwebapplicationfirewallpolicies`
`edgeactions`
`profiles`
`cdnwebapplicationfirewallpolicies`
`edgeactions`
`profiles`
`profiles/endpoints`

`Microsoft.Chaos` 
N/A
`experiments`

`Microsoft.CloudHealth` 
`healthmodels`
`healthmodels`

`Microsoft.CodeSigning` 
`codesigningaccounts`
`codesigningaccounts`

`Microsoft.`
`CognitiveServices` 
`accounts`
`accounts/projects`
`accounts`
`accounts/projects`

`microsoft.community` 
N/A
`communityTrainings`

`Microsoft.Compute` 
`cloudservices`
`cloudServices/roles`
`virtualMachines`
`virtualmachineScaleSets`
`virtualMachineScaleSets/virtualMachines`
`virtualMachines`

`Microsoft.`
`ConfidentialLedger` 
N/A
`Ledgers`
`ManagedCCF`
`ManagedCCFs`

`Microsoft.ConnectedCache` 
`CacheNodes`
`enterpriseMccCustomers`
`ispCustomers`
`CacheNodes`
`enterpriseMccCustomers`
`ispCustomers`

`Microsoft.`
`ConnectedVehicle` 
`platformAccounts`
`platformAccounts`

`Microsoft.`
`ContainerInstance` 
`containerGroups`
`containerScaleSets`
`containerGroups`

`Microsoft.`
`ContainerRegistry` 
`registries`
`registries`

`Microsoft.`
`ContainerService` 
`managedClusters`
`fleets`
`managedClusters`

`Microsoft.`
`CustomProviders` 
`resourceproviders`
`resourceproviders`

`Microsoft.`
`D365CustomerInsights` 
N/A
`instances`

`Microsoft.Dashboard` 
`grafana`
`dashboards`
`grafana`

`Microsoft.Databricks` 
N/A
`workspaces`

`Microsoft.DataFactory` 
`datafactories`
`factories`
`factories`

`Microsoft.`
`DataLakeAnalytics` 
`accounts`
`accounts`

`Microsoft.DataLakeStore` 
`accounts`
`accounts`

`Microsoft.DataProtection` 
`BackupVaults`
`BackupVaults`

`Microsoft.`
`DataReplication` 
N/A
`replicationVaults`

`Microsoft.DataShare` 
`accounts`
`accounts`

`Microsoft.DBforMariaDB` 
`servers`
`servers`

`Microsoft.DBforMySQL` 
`flexibleServers`
`servers`
`flexibleServers`
`servers`

`Microsoft.`
`DBforPostgreSQL` 
`flexibleServers`
`flexibleServers`

`Microsoft.`
`DBForPostgreSQL` 
`serverGroupsv2`
`serverGroupsv2`

`Microsoft.`
`DesktopVirtualization` 
N/A
`appAttachPackages`
`applicationgroups`
`hostpools`
`repositoryfolders`
`scalingplans`
`workspaces`

`Microsoft.DevCenter` 
`devcenters`
`devcenters`

`Microsoft.Devices` 
`IotHubs`
`provisioningServices`
`IotHubs`
`provisioningServices`

`Microsoft.`
`DevOpsInfrastructure` 
`pools`
`pools`

`Microsoft.DigitalTwins` 
`digitalTwinsInstances`
`digitalTwinsInstances`

`Microsoft.Discovery` 
N/A
`bookshelves`
`supercomputers`
`workspaces`

`Microsoft.DocumentDB` 
`cassandraClusters`
`DatabaseAccounts`
`fleets`
`garnetClusters`
`mongoClusters`
`cassandraClusters`
`DatabaseAccounts`
`mongoClusters`

`Microsoft.DurableTask` 
`schedulers`
`schedulers`

`Microsoft.Edge` 
N/A
`diagnostics`

`Microsoft.EventGrid` 
`domains`
`eventSubscriptions`
`extensionTopics`
`namespaces`
`partnerNamespaces`
`partnerTopics`
`systemTopics`
`topics`
`domains`
`namespaces`
`partnerNamespaces`
`partnerTopics`
`systemTopics`
`topics`

`Microsoft.EventHub` 
`clusters`
`Namespaces`
`Namespaces`

`Microsoft.`
`HardwareSecurityModules` 
N/A
`cloudHsmClusters`
`paymentHsmClusters`

`Microsoft.HealthcareApis` 
`services`
`workspaces/dicomservices`
`workspaces/fhirservices`
`workspaces/iotconnectors`
`services`
`workspaces/dicomservices`
`workspaces/fhirservices`
`workspaces/iotconnectors`

`Microsoft.`
`HealthcareInterop` 
`fhirQueryEventBatchChannels`
`fhirQueryFlatFileBatchChannels`
`fhirQueryEventBatchChannels`
`fhirQueryFlatFileBatchChannels`

`Microsoft.`
`HealthDataAIServices` 
N/A
`deidServices`

`Microsoft.HorizonDB` 
`clusters`
`clusters`

`microsoft.insights` 
`autoscalesettings`
`components`
`autoscalesettings`
`components`

`Microsoft.Insights` 
`datacollectionrules`
`datacollectionrules`

`microsoft.keyvault` 
`managedhsms`
`managedhsms`

`Microsoft.KeyVault` 
`vaults`
`vaults`

`microsoft.kubernetes` 
`connectedClusters`
`connectedClusters`

`Microsoft.Kusto` 
`clusters`
`clusters`

`microsoft.`
`loadtestservice` 
N/A
`loadtests`

`Microsoft.Logic` 
`automationProjects`
`automationProjects/applications`
`IntegrationServiceEnvironments`
`Workflows`
`automationProjects`
`automationProjects/applications`
`IntegrationAccounts`
`Workflows`

`Microsoft.`
`MachineLearningServices` 
`workspaces`
`workspaces/onlineEndpoints`
`workspaces/onlineEndpoints/deployments`
`registries`
`workspaces`
`workspaces/onlineEndpoints`

`Microsoft.`
`ManagedNetworkFabric` 
`internetGateways`
`l3IsolationDomains`
`networkDevices`
`networkFabricControllers`
`networkFabrics`
`networkDevices`

`Microsoft.Monitor` 
`accounts`
`pipelineGroups`
`accounts`
`pipelineGroups`

`Microsoft.NetApp` 
`elasticAccounts/elasticCapacityPools`
`elasticAccounts/elasticCapacityPools/elasticVolumes`
`netAppAccounts`
`netAppAccounts/capacityPools`
`netAppAccounts/capacityPools/caches`
`netAppAccounts/capacityPools/volumes`
`scaleAccounts/scaleCapacityPools`
`scaleAccounts/scaleCapacityPools/scaleVolumes`
`netAppAccounts/capacityPools`
`netAppAccounts/capacityPools/caches`

`Microsoft.Network` 
`applicationgateways`
`azureFirewalls`
`connections`
`dnsForwardingRulesets`
`dnsResolverDomainLists`
`dnsResolverPolicies`
`dnsResolvers`
`dnszones`
`expressRouteCircuits`
`expressRouteCircuits/peerings`
`expressRouteLags`
`expressRoutePorts`
`frontdoors`
`loadBalancers`
`natgateways`
`networkinterfaces`
`networkManagers/ipamPools`
`networkSecurityPerimeters`
`NetworkVirtualAppliances`
`networkWatchers/connectionMonitors`
`privateDnsZones`
`privateEndpoints`
`privateLinkServices`
`privateTrafficManagerProfiles`
`publicIPAddresses`
`publicIPPrefixes`
`trafficManagerProfiles`
`virtualHubs`
`virtualnetworkappliances`
`virtualNetworks`
`virtualRouters`
`applicationgateways`
`azureFirewalls`
`dnsResolverPolicies`
`expressRouteCircuits`
`frontdoors`
`loadBalancers`
`natgateways`
`networkManagers`
`networkManagers/ipamPools`
`networksecuritygroups`
`networkSecurityPerimeters`
`networkSecurityPerimeters/profiles`
`publicIPAddresses`
`publicIPPrefixes`
`trafficManagerProfiles`
`virtualNetworks`

`microsoft.network` 
`bastionHosts`
`expressroutegateways`
`p2svpngateways`
`virtualnetworkgateways`
`vpngateways`
`bastionHosts`
`p2svpngateways`
`virtualnetworkgateways`
`vpngateways`

`Microsoft.`
`NetworkAnalytics` 
N/A
`DataProducts`

`Microsoft.NetworkCloud` 
`bareMetalMachines`
`clusterManagers`
`clusters`
`storageAppliances`
`bareMetalMachines`
`clusterManagers`
`clusters`
`kubernetesClusters`
`storageAppliances`

`Microsoft.`
`NetworkFunction` 
`azureTrafficCollectors`
`azureTrafficCollectors`

`Microsoft.`
`NetworkSecurity` 
N/A
`agentFabrics`

`Microsoft.`
`NotificationHubs` 
`namespaces/notificationHubs`
`namespaces`
`namespaces/notificationHubs`

`microsoft.`
`onlineexperimentation` 
N/A
`workspaces`

`MICROSOFT.`
`OPENENERGYPLATFORM` 
`ENERGYSERVICES`
`ENERGYSERVICES`

`Microsoft.`
`OpenLogisticsPlatform` 
N/A
`Workspaces`

`Microsoft.`
`OperationalInsights` 
`workspaces`
`workspaces`

`Microsoft.Orbital` 
`contactProfiles`
`geocatalogs`
`l2Connections`
`spacecrafts`
`terminals`
`geocatalogs`

`Microsoft.Peering` 
N/A
`peerings`
`peeringServices`

`Microsoft.PlayFab` 
`titles`
`titles`

`Microsoft.PowerBI` 
N/A
`tenants`
`tenants/workspaces`

`Microsoft.`
`PowerBIDedicated` 
`capacities`
`capacities`

`Microsoft.ProviderHub` 
N/A
`providerMonitorSettings`
`providerRegistrations`

`microsoft.purview` 
`accounts`
`accounts`

`Microsoft.Quantum` 
`providerAccounts`
`providerAccounts`
`workspaces`

`Microsoft.`
`RecoveryServices` 
`Vaults`
`Vaults`

`Microsoft.`
`RedHatOpenShift` 
N/A
`hcpOpenShiftClusters`

`Microsoft.Relay` 
`clusters`
`namespaces`
`namespaces`

`Microsoft.`
`ResourceBuilder` 
`workspaces`
`workspaces/pipelines/jobs`
`workspaces`
`workspaces/pipelines/jobs`

`Microsoft.Search` 
`searchServices`
`searchServices`

`Microsoft.Security` 
N/A
`antiMalwareSettings`
`defenderForStorageSettings`

`microsoft.`
`securityinsights` 
N/A
`settings`

`Microsoft.ServiceBus` 
`Namespaces`
`Namespaces`

`Microsoft.`
`ServiceNetworking` 
`trafficControllers`
`trafficControllers`

`Microsoft.SignalRService` 
`SignalR`
`SignalR/replicas`
`WebPubSub`
`WebPubSub/replicas`
`SignalR`
`SignalR/replicas`
`WebPubSub`
`WebPubSub/replicas`

`microsoft.singularity` 
`accounts`
`accounts`

`Microsoft.Sql` 
`managedInstances`
`servers/databases`
`servers/elasticpools`
`servers/jobAgents`
`managedInstances`
`managedInstances/databases`
`servers/databases`

`Microsoft.StandbyPool` 
N/A
`standbycontainergrouppools`
`standbyvirtualmachinepools`

`Microsoft.Storage` 
`contextCaches/contextCacheContainers`
`storageAccounts`
`storageAccounts/blobServices`
`storageAccounts/fileServices`
`storageAccounts/objectReplicationPolicies`
`storageAccounts/queueServices`
`storageAccounts/storageTasks`
`storageAccounts/tableServices`
`storageTasks`
`storageAccounts/blobServices`
`storageAccounts/fileServices`
`storageAccounts/queueServices`
`storageAccounts/tableServices`

`Microsoft.StorageCache` 
`amlFilesystems`
`caches`
`amlFilesystems`
`caches`

`Microsoft.StorageMover` 
`storageMovers`
`storageMovers`

`Microsoft.`
`StreamAnalytics` 
`streamingjobs`
`streamingjobs`

`Microsoft.Synapse` 
`workspaces`
`workspaces/bigDataPools`
`workspaces/kustoPools`
`workspaces/scopePools`
`workspaces/sqlPools`
`workspaces`
`workspaces/bigDataPools`
`workspaces/kustoPools`
`workspaces/scopePools`
`workspaces/sqlPools`

`Microsoft.`
`ToolchainOrchestrator` 
N/A
`diagnostics`

`microsoft.videoindexer` 
N/A
`accounts`

`Microsoft.Web` 
`containerapps`
`hostingEnvironments`
`hostingenvironments/multirolepools`
`hostingenvironments/workerpools`
`serverfarms`
`sites`
`sites/slots`
`staticsites`
`hostingEnvironments`
`serverfarms`
`sites`
`sites/slots`
`staticsites`

`microsoft.workloads` 
N/A
`sapvirtualinstances`

`Microsoft.`
`ZeroTrustSegmentation` 
N/A
`segmentationManagers`

`NGINX.NGINXPLUS` 
`NGINX.NGINXPLUS/nginxDeployments`
`NGINX.NGINXPLUS/nginxDeployments`

`Oracle.Database` 
`Oracle.Database/autonomousDatabases`
`Oracle.Database/cloudVmClusters`
`Oracle.Database/dbSystems`
`Oracle.Database/exadbVmClusters`
`Oracle.Database/goldenGateDeployments`
`Oracle.Database/autonomousDatabases`
`Oracle.Database/cloudExadataInfrastructures`
`Oracle.Database/cloudVmClusters`
`Oracle.Database/dbSystems`
`Oracle.Database/exadbVmClusters`
`Oracle.Database/exascaleDbStorageVaults`
`Oracle.Database/goldenGateDeployments`

`Microsoft.azurestackhci` 
`clusters`
N/A

`Microsoft.AzureStackHCI` 
`edgeMachines`
N/A

`microsoft.bing` 
`accounts`
N/A

`Microsoft.BotService` 
`botServices/channels`
`botServices/connections`
`checknameavailability`
`hostsettings`
`listauthserviceproviders`
`listqnamakerendpointkeys`
N/A

`Microsoft.ClusterStor` 
`nodes`
N/A

`microsoft.compute` 
`disks`
N/A

`Microsoft.DataBoxEdge` 
`dataBoxEdgeDevices`
N/A

`microsoft.deviceregistry` 
`namespaces`
N/A

`microsoft.edgezones` 
`edgezones`
N/A

`Microsoft.ElasticSan` 
`elasticSans`
N/A

`Microsoft.FileShares` 
`fileShares`
N/A

`Microsoft.HDInsight` 
`clusters`
N/A

`Microsoft.HealthModel` 
`healthmodels`
N/A

`Microsoft.`
`HybridContainerService` 
`provisionedClusters`
N/A

`microsoft.hybridnetwork` 
`networkfunctions`
`virtualnetworkfunctions`
N/A

`Microsoft.IoTCentral` 
`IoTApps`
N/A

`Microsoft.`
`IoTFirmwareDefense` 
`workspaces`
N/A

`microsoft.`
`kubernetesconfiguration` 
`extensions`
N/A

`Microsoft.Maps` 
`accounts`
N/A

`Microsoft.`
`MessagingConnectors` 
`connectors`
N/A

`Microsoft.MobileNetwork` 
`mobilenetworks/sites`
`packetcorecontrolplanes`
`packetcorecontrolplanes/packetcoredataplanes`
`radioAccessNetworks`
N/A

`Microsoft.OrionDB` 
`clusters`
N/A

`Microsoft.`
`PowerPlatformMonitoringHub` 
`copilotstudio`
`microsoftapp`
`powerapps`
`powerautomate`
N/A

`microsoft.resources` 
`subscriptions`
N/A

`microsoft.`
`securitydetonation` 
`chambers`
N/A

`Microsoft.`
`SecurityDetonation` 
`SecurityDetonationChambers`
N/A

`Microsoft.StorageActions` 
`storageTasks`
N/A

`Microsoft.StorageSync` 
`storageSyncServices`
N/A

`Microsoft.StorageTasks` 
`storageTasks`
N/A

`Microsoft.VoiceServices` 
`CommunicationsGateways`
N/A

`Private.`
`MessagingConnectors` 
`Private.MessagingConnectors/connectors`
N/A

`Wandisco.Fusion` 
`Wandisco.Fusion/migrators`
`Wandisco.Fusion/migrators/dataTransferAgents`
`Wandisco.Fusion/migrators/liveDataMigrations`
`Wandisco.Fusion/migrators/metadataMigrations`
N/A

## Next steps

- Read about metrics in Azure Monitor

- Metrics export using data collection rules

- Create alerts on metrics

- Export metrics to storage, Event Hub, or Log Analytics

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-03
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
