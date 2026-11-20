# https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/decision-guides/resource-tagging

Source: https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/decision-guides/resource-tagging

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
 

 

 

 

 
 
# Define your naming convention

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Naming conventions provide standardized formats for assigning names to Azure resources. Every organization needs a tailored naming convention that meets both Azure requirements and specific cloud adoption needs. This guidance provides a foundation that you can adapt to align with your organizational requirements.

See examples: Example Azure resource names

## Understand resource names in Azure

An Azure resource name is the identifier assigned to a specific instance of an Azure resource, such as a web app, database, or storage account. To establish a consistent Azure naming convention, you need to understand how Azure works. Here's what you need to know:

- Understand name permanence. Most Azure resource names can't be changed after creation. Include only information that remains constant in the name. Use tags to capture other details.

- Understand Azure naming rules. There are naming rules for every Azure resource. Not all Azure resource names can follow the same patterns. Make sure you understand the limitations of the resource types you're working with. Azure names must follow three general principles:

- Names need to be unique within the scope of the Azure resource (varies by resource).

- Names need to meet length requirements (varies by resource).

- Names can only contain valid characters (varies by resource).

- Understand Azure name scope. Azure resource names must be unique within their defined scope. Each resource type has a specific scope level that determines where the name must be unique. Understanding these scope levels ensures proper naming conventions and avoids conflicts.

Scope
Description
Example

Global
Unique across all of Azure. This scope applies to PaaS resources with public IP endpoints, as their names serve as the initial default public DNS name.
For example, a web app named `app-workload1-prod-001.azurewebsites.net` must be globally unique.

Resource group
Unique within the resource group. Resources in the same group can't share the same name, but identical names can exist in different resource groups.
For example, a virtual network named `vnet-prod-westus-001` can exist in multiple resource groups, but only once within a single resource group.

Resource
Unique within the parent resource. Resources nested within another resource must have unique names to avoid conflicts.
For example, subnets within a virtual network must have unique names to prevent segment overlap.

## Choose naming components

The following list provides examples of naming components (what to include in the name) that are useful for constructing Azure resource names:

Naming component
Description
Example component
Example Azure resource

Resource type
An abbreviation that represents the type of Azure resource or asset.
`rg`, `vm`, `st`, `app`
`rg-workload1-prod-001`, `vm-web-prod-001`

Workload, application, or project
Name of a workload or project that the resource is a part of.
`workload1`, `workload2`, `workload3`, `workload4`
`app-workload1-prod`, `vm-workload3-dev-001`

Environment
Production, development, quality assurance, stage, test.
`prod`, `dev`, `qa`, `stage`, `test`
`app-workload1-prod`, `sqldb-dev`

Region
The Azure region or cloud provider location where the resource is deployed.
`westus`, `eastus2`, `westeu`, `usva`, `ustx`
`vnet-shared-eastus2-001`, `pip-workload4-prod-westus-001`

Instance number
The instance count for a specific resource, to differentiate it from other resources that have the same naming convention and naming components.
`01`, `001`
`vm-sql-test-001`, `vm-sql-test-002`

### Develop your naming convention

To construct your Azure naming convention, identify the key pieces of information that you want to reflect in a resource name. Different information is relevant for different resource types.

- Standardize component order. In addition to defining the naming components, you must also consider the order in which the naming components are listed.

- Choose to use a delimiter or not. To improve readability, use a hyphen `-` to separate naming components. However, not every resource in Azure allows you to use a delimiter. If you need absolute consistency across all your Azure resource names, don't use a hyphen. For many customers, the benefits of using a delimiter outweigh some inconsistency in the naming convention.

- Use abbreviations. Use Azure resource abbreviations to keep resource names within length limits.

- Use the Azure Naming Tool. The Azure Naming Tool helps you generate names for Azure resources. You configure the tool to use your preferred naming convention, and it generates names for your Azure resources. For more information, see Azure Naming Tool.

Note

Don't include any personal, sensitive, or confidential information in resource names (for example, table name, database name) and resource tags. Data you enter in these fields isn't considered customer data.

## Example Azure resource names

Consider these examples when you define your Azure naming convention. The examples are based on the naming components and considerations that are described in this article.

### AI and machine learning

Asset type
Scope
Format and examples

Azure AI Search
Global
srch-<workload, application, or project>-<environment> 

 
- `srch-workload1-prod` 

- `srch-workload2-dev`

Microsoft Foundry resource
Resource group
aif-<workload, application, or project>-<environment> 

 
- `aif-workload1-prod` 

- `aif-workload2-dev`

Azure Machine Learning workspace
Resource group
mlw-<workload, application, or project>-<environment> 

 
- `mlw-workload1-prod` 

- `mlw-workload2-dev`

### Analytics and IoT

Asset type
Scope
Format and examples

Azure Data Factory
Global
adf-<workload, application, or project>-<environment> 

 
- `adf-workload1-prod` 

- `adf-workload2-dev`

Data Lake Storage account
Global
dls<workload, application, or project><environment> 

 
- `dlsworkload1prod` 

- `dlsworkload2dev`

IoT hub
Global
iot-<workload, application, or project>-<environment> 

 
- `iot-workload1-prod` 

- `iot-workload2-dev`

### Compute and web

Asset type
Scope
Format and examples

Virtual machine
Resource group
vm-<workload, application, or project>-<environment>-<###> 

 
- `vm-sql-test-001` 

- `vm-workload4-prod-001` 

- `vm-workload3-dev-001`

Web app
Global
app-<workload, application, or project>-<environment>-<###>.azurewebsites.net 

 
- `app-workload1-prod-001.azurewebsites.net` 

- `app-accountlookup-dev-001.azurewebsites.net`

Function app
Global
func-<workload, application, or project>-<environment>-<###>.azurewebsites.net 

 
- `func-workload1-prod-001.azurewebsites.net` 

- `func-accountlookup-dev-001.azurewebsites.net`

### Databases

Asset type
Scope
Format and examples

Azure SQL database
Azure SQL Server
sqldb-<workload, application, or project>-<environment> 

 
- `sqldb-users-prod` 

- `sqldb-users-dev`

Azure Cosmos DB database
Global
cosmos-<workload, application, or project>-<environment> 

 
- `cosmos-workload1-prod` 

- `cosmos-workload2-dev`

Azure Managed Redis instance
Global
redis-<workload, application, or project>-<environment> 

 
- `redis-workload1-prod` 

- `redis-workload2-dev`

### Integration

Asset type
Scope
Format and Examples

API management service instance
Global
apim-<app or service name> 

 `apim-workload1-prod`

Service Bus namespace
Global
sbns-<workload, application, or project>-<environment>.servicebus.windows.net 

 
- `sbns-workload1-prod.servicebus.windows.net` 

- `sbns-workload2-dev.servicebus.windows.net`

Service Bus queue
Service Bus
sbq-<workload, application, or project> 

 
- `sbq-workload1`

Service Bus topic
Service Bus
sbt-<workload, application, or project> 

 
- `sbt-workload1`

### Management and governance

Asset type
Scope
Format and examples

Management group
Tenant
Provide a globally unique identifier (GUID) for the management group ID. Display names are editable and should represent the platform function or workload types within them.

Subscription
Azure account or Enterprise agreement
Descriptive name that aligns with IT standards. You can change the display name. Example: (Business Unit (optional)) (Function or Workload) (Environment) 

 
- `Marketing Web App Production` 

- `Connectivity` 

- `Security`

Resource group
Subscription
rg-workload name/type-workload component (optional)-environment (optional) 

 
- `rg-webapp-prod` 

- `rg-webapp-database-dev`

### Networking

Asset type
Scope
Format and examples

Virtual network
Resource group
vnet-<subscription purpose>-<region>-<###> 

 
- `vnet-shared-eastus2-001` 

- `vnet-prod-westus-001` 

- `vnet-client-eastus2-001`

Subnet
Virtual network
snet-<subscription purpose>-<region>-<###> 

 
- `snet-shared-eastus2-001` 

- `snet-prod-westus-001` 

- `snet-client-eastus2-001`

Network interface (NIC)
Resource group
nic-<##>-<vm name>-<subscription purpose>-<###> 

 
- `nic-01-dc1-shared-001` 

- `nic-02-vmworkload41-prod-001` 

- `nic-02-vmtest1-client-001`

Public IP address
Resource group
pip-<vm name or app name>-<environment>-<region>-<###> 

 
- `pip-dc1-shared-eastus2-001` 

- `pip-workload4-prod-westus-001`

Load balancer (external)
Resource group
lbe-<app name or role>-<environment>-<###> 

 
- `lbe-workload1-prod-001` 

- `lbe-workload3-dev-001`

Network security group (NSG)
Subnet or NIC
nsg-<policy name or app name>-<###> 

 
- `nsg-weballow-001` 

- `nsg-rdpallow-001` 

- `nsg-sqlallow-001` 

- `nsg-dnsblocked-001`

Local network gateway
Virtual gateway
lgw-<subscription purpose>-<region>-<###> 

 
- `lgw-shared-eastus2-001` 

- `lgw-prod-westus-001` 

- `lgw-client-eastus2-001`

Virtual network gateway
Virtual network
vgw-<subscription purpose>-<region>-<###> 

 
- `vgw-shared-eastus2-001` 

- `vgw-prod-westus-001` 

- `vgw-client-eastus2-001`

VPN connection
Resource group
vcn-<subscription1 purpose>>-<region1>-to-<subscription2 purpose>>-<region2>- 

 
- `vcn-shared-eastus2-to-shared-westus` 

- `vcn-prod-eastus2-to-prod-westus`

Route table
Resource group
rt-<route table name> 

 
- `rt-workload1` 

- `rt-workload3`

DNS label
Global
<DNS A record for VM>.<region>.cloudapp.azure.com 

 
- `dc1.westus.cloudapp.azure.com` 

- `web1.eastus2.cloudapp.azure.com`

### Security

Asset type
Scope
Format and examples

Managed identity
Resource group
id-<app or service name>-<environment>-<region name>-<###> 

 
- `id-appcn-keda-prod-eastus2-001`

### Storage

Asset type
Scope
Format and examples

Storage account (general use)
Global
st<workload, application, or project><###> 

 
- `stworkload1data001` 

- `stworkload2output001`

Azure Container Registry
Global
cr<workload, application, or project><environment><###> 

 
- `crworkload1prod001`

## Next step

A good next step is to define your tagging strategy.

Define your tagging strategy

 
 

 
 

 

 
 
 
 
 
 
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
 2026-06-25
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
