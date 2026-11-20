# https://learn.microsoft.com/en-us/azure/dms/dms-overview

Source: https://learn.microsoft.com/en-us/azure/dms/dms-overview

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
 

 

 

 

 
 
# What is Azure Database Migration Service?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Database Migration Service (Azure DMS) is a fully managed service designed to enable seamless migrations from multiple database sources to Azure data platforms with minimal downtime (online migrations).

Azure DMS is available through the Azure portal, PowerShell, and Azure CLI.

Currently, it supports SQL Database modernization to Azure. For improved functionality and supportability, consider migrating to Azure SQL Database by using DMS.

## Tracking resource

Azure DMS provides a capability to create a free and optional SQL Server instance Azure resource to improve your migration tracking experience. Specify the SQL Server instance name and subscription, resource group, and location where you want to create the tracking resource. You must register your subscription to the `Microsoft.AzureArcData` resource provider to create the Azure resource. We attempt to register your subscription to the resource provider if your subscription isn't already registered to it.

## Compare versions

The following table compares the functionality of the versions of Azure DMS:

Feature
DMS (Azure portal)
Notes

Assessment
No
Assess compatibility of the source.

SKU recommendation
No
SKU recommendations for the target based on the assessment of the source.

Azure SQL Database - Offline migration
Yes
Migrate to Azure SQL Database offline.

Azure SQL Managed Instance - Online migration
Yes
Migrate to Azure SQL Managed Instance online with minimal downtime.

Azure SQL Managed Instance - Offline migration
Yes
Migrate to Azure SQL Managed Instance offline.

SQL Server on Azure SQL Virtual Machine - Online migration
Yes
Migrate to SQL Server on Azure VMs online with minimal downtime.

SQL Server on Azure SQL Virtual Machine - Offline migration
Yes
Migrate to SQL Server on Azure VMs offline.

Migrate logins
No
Migrate logins from your source to your target.

Migrate schemas
Yes
Migrate schemas from your source to your target.

Azure portal support
Yes
Create and monitor your migration by using the Azure portal.

Regional availability
Yes
For regional availability, see Products available by region.

Improved user experience
Yes
The DMS is faster, more secure, and easier to troubleshoot.

Automation
Yes
The DMS supports PowerShell and Azure CLI.

Private endpoints
Yes
Connect to your source and target using private endpoints.

TDE support
No
Migrate databases encrypted with TDE.

## Migrate databases to Azure with familiar tools

Azure DMS integrates some of the functionality of our existing tools and services. It provides customers with a comprehensive, highly available solution.

The service uses the same underlying technology as the Azure Arc readiness assessment to provide recommendations to guide you through the required changes before a migration. It's up to you to perform any remediation required.

Azure DMS performs all the required steps when ready to begin the migration process. Knowing that the process takes advantage of Microsoft's best practices, you can fire and forget your migration projects with peace of mind.

## Regional availability

For up-to-date info about the regional availability of Azure DMS, see Products available by region.

## Related content

- Azure Database Migration Service supported scenarios

- Services and tools available for data migration scenarios

- FAQ about using Azure Database Migration Service

 
 

 
 

 

 
 
 
 
 
 
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
 2026-02-20
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
