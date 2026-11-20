# https://learn.microsoft.com/en-us/azure/storage/file-sync/file-sync-introduction

Source: https://learn.microsoft.com/en-us/azure/storage/file-sync/file-sync-introduction

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
 

 

 

 

 
 
# What is Azure File Sync?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure File Sync centralizes your organization's file shares in Azure Files while keeping the flexibility, performance, and compatibility of on-premises Windows file servers. Each registered Windows Server syncs its data to and from a central Azure file share, and can optionally use cloud tiering to cache only the most frequently accessed files locally.

You can have as many server caches as you need across the world â changes on any server sync through the Azure file share to all other servers automatically.

## Key benefits

- Cloud tiering â Cache only frequently accessed files locally; tier infrequently used files to Azure. The full namespace remains visible and browsable, and tiered files are recalled seamlessly on access. Reduces on-premises storage costs significantly. Learn more.

- Multi-site sync â Keep files consistent across multiple offices without direct server-to-server connectivity. Changes sync through the Azure file share, so every site sees the same data.

- Disaster recovery â Recover from a server failure by provisioning a new Windows Server, installing the Azure File Sync agent, and letting the namespace download from Azure. No local backup needed.

- Cloud-side backup â Take centralized backups via Azure Backup with native snapshot capabilities. Reduce on-premises backup infrastructure.

- Seamless migration â Move data from on-premises servers to Azure in the background without disrupting users. File structure, permissions, and access patterns remain intact.

## How it works

- Deploy a Storage Sync Service in Azure.

- Install the Azure File Sync agent on one or more Windows servers.

- Register each server with the Storage Sync Service.

- Create a sync group linking an Azure file share (cloud endpoint) with a folder on your server (server endpoint).

- Files sync automatically. Enable cloud tiering to free local disk space.

## Get started

- Plan for an Azure File Sync deployment

- Deploy Azure File Sync

- Cloud tiering overview

## Training and architecture

- Implement a hybrid file server infrastructure (self-paced training)

- Azure enterprise cloud file share (architecture guidance)

- Hybrid file services (architecture guidance)

 
 

 
 

 

 
 
 
 
 
 
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
