# https://learn.microsoft.com/en-us/azure/dms/dms-tools-matrix

Source: https://learn.microsoft.com/en-us/azure/dms/dms-tools-matrix

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
 

 

 

 

 
 
# Services and tools available for data migration scenarios

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This article provides a matrix of the Microsoft and third-party services and tools available to assist you with various database and data migration scenarios and specialty tasks.

The following tables identify the services and tools you can use to plan for data migration and complete its various phases successfully.

Note

In the following tables, items marked with an asterisk (`*`) represent third-party tools.

## Business justification phase

Source
Target
Discover / inventory
Target and SKU recommendation

SQL Server
Azure SQL Database
- SQL Server migration in Azure Arc
- Azure Migrate
- Cloudamize1
- SQL Server migration in Azure Arc
- Azure Migrate
- Cloud Atlas1
- Cloudamize1

SQL Server
Azure SQL Managed Instance
- SQL Server migration in Azure Arc
- Azure Migrate
- Cloudamize1
- SQL Server migration in Azure Arc
- Azure Migrate
- Cloud Atlas1
- Cloudamize1

SQL Server
SQL Server on Azure Virtual Machine
- SQL Server migration in Azure Arc
- Azure Migrate
- Cloudamize1
- SQL Server migration in Azure Arc
- Azure Migrate
- Cloud Atlas1
- Cloudamize1

SQL Server
Azure Synapse Analytics
- Azure Migrate
- Cloudamize1

Amazon RDS for SQL Server
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM
Azure Migrate
Azure Migrate

Oracle
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM
SSMA
- SSMA
- MigVisor1

Oracle
Azure Synapse Analytics
Azure Migrate
SSMA

Oracle
Azure Database for PostgreSQL flexible server
Azure Migrate

MongoDB
Azure DocumentDB
Azure Migrate
Azure Migrate

MongoDB
Azure Cosmos DB
Cloudamize1
Cloudamize1

Cassandra
Azure Cosmos DB

MySQL
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM
Azure Migrate
- SSMA
- Cloud Atlas1

MySQL
Azure Database for MySQL
Azure Migrate

Amazon RDS for MySQL
Azure Database for MySQL

PostgreSQL
Azure Database for PostgreSQL flexible server
Azure Migrate

Amazon RDS for PostgreSQL
Azure Database for PostgreSQL flexible server

DB2
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM
Azure Migrate
SSMA

Access
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM
Azure Migrate
SSMA

Sybase - SAP ASE
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM
Azure Migrate
SSMA

Sybase - SAP IQ
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM

1 This is a non-Microsoft product or service, provided by a third-party.

## Premigration phase

Source
Target
App data access layer assessment
Database assessment
Performance assessment

SQL Server
Azure SQL Database

- SQL Server migration in Azure Arc
- Cloud Atlas1
- Cloudamize1
Cloudamize1

SQL Server
Azure SQL Managed Instance

- SQL Server migration in Azure Arc
- Cloud Atlas1
- Cloudamize1
Cloudamize1

SQL Server
SQL Server on Azure VM

- SQL Server migration in Azure Arc
- Cloud Atlas1
- Cloudamize1
Cloudamize1

SQL Server
Azure Synapse Analytics

Amazon RDS for SQL
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM

Azure portal

Oracle
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM
SSMA
SSMA

Oracle
Azure Synapse Analytics
SSMA
SSMA

Oracle
Azure Database for PostgreSQL flexible server

Ora2Pg1

MongoDB
Azure DocumentDB

Azure DocumentDB Migration extension in Visual Studio Code

MongoDB
Azure Cosmos DB

Cloudamize1
Cloudamize1

Cassandra
Azure Cosmos DB

MySQL
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM
SSMA
- SSMA
- Cloud Atlas1

MySQL
Azure Database for MySQL

Amazon RDS for MySQL
Azure Database for MySQL

PostgreSQL
Azure Database for PostgreSQL flexible server

Migration Service for Azure Database for PostgreSQL

Amazon RDS for PostgreSQL
Azure Database for PostgreSQL flexible server

Migration Service for Azure Database for PostgreSQL

Amazon Aurora PostgreSQL
Azure Database for PostgreSQL flexible server

Migration Service for Azure Database for PostgreSQL

Google Cloud SQL for PostgreSQL
Azure Database for PostgreSQL flexible server

Migration Service for Azure Database for PostgreSQL

DB2
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM
SSMA
SSMA

Access
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM

SSMA

Sybase - SAP ASE
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM
SSMA
SSMA

Sybase - SAP IQ
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM

1 This is a non-Microsoft product or service, provided by a third-party.

## Migration phase

Source
Target
Schema
Offline data
Online data

SQL Server
Azure SQL Database
- SQL Database Projects extension
- Cloudamize1
Cloudamize1
- Cloudamize1
- Qlik1
- Striim1

SQL Server
Azure SQL Managed Instance
Cloudamize1
Cloudamize1
- SQL Server migration in Azure Arc
- Cloudamize1
- Qlik1
- Striim1

SQL Server
SQL Server on Azure VM
Cloudamize1
Cloudamize1
- Cloudamize1
- Qlik1
- Striim1

SQL Server
Azure Synapse Analytics

Amazon RDS for SQL Server
Azure SQL Database
SQL Database Projects extension
Azure portal
- Qlik1
- Striim1

Amazon RDS for SQL
Azure SQL Managed Instance
Azure portal
Azure portal
Striim1

Amazon RDS for SQL Server
SQL Server on Azure VM
Azure portal
Azure portal
- Qlik1
- Striim1

Oracle
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM
- SSMA
- SharePlex1
- Ispirer1
- SSMA
- SharePlex1
- Ispirer1
- SharePlex1
- Qlik1
- Striim1

Oracle
Azure Synapse Analytics
- SSMA
- Ispirer1
- SSMA
- Ispirer1
- SharePlex1
- Qlik1
- Striim1

Oracle
Azure Database for PostgreSQL flexible server
- Ora2Pg1
- Ispirer1
- Ora2Pg1
- Ispirer1
Striim1

MongoDB
Azure DocumentDB
Azure DocumentDB Migration extension in Visual Studio Code
Azure DocumentDB Migration extension in Visual Studio Code
Azure DocumentDB Migration extension in Visual Studio Code

MongoDB
Azure Cosmos DB
- Azure DMS
- Cloudamize1
- Imanis Data1
- Azure DMS
- Cloudamize1
- Imanis Data1
- Azure DMS
- Cloudamize1
- Imanis Data1
- Striim1

Cassandra
Azure Cosmos DB
Imanis Data1
Imanis Data1
Imanis Data1

MySQL
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM
- SSMA
- Ispirer1
- SSMA
- Ispirer1
- Qlik1
- Striim1

MySQL
Azure Database for MySQL
- Azure DMS
- MySQL dump1
Azure DMS
- Azure DMS
- MyDumper/MyLoader1 with data-in replication

Amazon RDS for MySQL
Azure Database for MySQL
- Azure DMS
- MySQL dump1
Azure DMS
- Azure DMS
- MyDumper/MyLoader1 with data-in replication

Amazon Aurora MySQL
Azure Database for MySQL
- Azure DMS
- MySQL dump1
Azure DMS
- Azure DMS
- MyDumper/MyLoader1 with data-in replication

Google Cloud SQL for MySQL
Azure Database for MySQL
- Azure DMS
- MySQL dump1
Azure DMS
- Azure DMS
- MyDumper/MyLoader1 with data-in replication

PostgreSQL
Azure Database for PostgreSQL flexible server
Migration Service for Azure Database for PostgreSQL
Migration Service for Azure Database for PostgreSQL
Migration Service for Azure Database for PostgreSQL

Amazon RDS for PostgreSQL
Azure Database for PostgreSQL flexible server
Migration Service for Azure Database for PostgreSQL
Migration Service for Azure Database for PostgreSQL
Migration Service for Azure Database for PostgreSQL

Google Cloud SQL for PostgreSQL
Azure Database for PostgreSQL flexible server
Migration Service for Azure Database for PostgreSQL
Migration Service for Azure Database for PostgreSQL
Migration Service for Azure Database for PostgreSQL

Amazon Aurora PostgreSQL
Azure Database for PostgreSQL flexible server
Migration Service for Azure Database for PostgreSQL
Migration Service for Azure Database for PostgreSQL
Migration Service for Azure Database for PostgreSQL

DB2
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM
- SSMA
- Ispirer1
- SSMA
- Ispirer1
- Qlik1
- Striim1

Access
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM
SSMA
SSMA
SSMA

Sybase - SAP ASE
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM
- SSMA
- Ispirer1
- SSMA
- Ispirer1
- Qlik1
- Striim1

Sybase - SAP IQ
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM
Ispirer1
Ispirer1

1 This is a non-Microsoft product or service, provided by a third-party.

## Post-migration phase

Source
Target
Optimize

SQL Server
Azure SQL Database
- Cloud Atlas1
- Cloudamize1

SQL Server
Azure SQL Managed Instance
- Cloud Atlas1
- Cloudamize1

SQL Server
SQL Server on Azure VM
- Cloud Atlas1
- Cloudamize1

SQL Server
Azure Synapse Analytics

RDS SQL
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM

Oracle
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM

Oracle
Azure Synapse Analytics

Oracle
Azure Database for PostgreSQL -
- Single server

MongoDB
Azure DocumentDB

MongoDB
Azure Cosmos DB
Cloudamize1

Cassandra
Azure Cosmos DB

MySQL
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM

MySQL
Azure Database for MySQL

Amazon RDS for MySQL
Azure Database for MySQL

PostgreSQL
Azure Database for PostgreSQL flexible server

Amazon RDS for PostgreSQL
Azure Database for PostgreSQL flexible server

DB2
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM

Access
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM

Sybase - SAP ASE
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM

Sybase - SAP IQ
Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VM

1 This is a non-Microsoft product or service, provided by a third-party.

## Related content

- What is Azure Database Migration Service?

 
 

 
 

 

 
 
 
 
 
 
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
 2026-08-18
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
