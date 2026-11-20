# https://learn.microsoft.com/en-us/azure/storage/files/storage-files-introduction

Source: https://learn.microsoft.com/en-us/azure/storage/files/storage-files-introduction

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
 

 

 

 

 
 
# What is Azure Files?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Files provides fully managed file shares in the cloud that you can access through the industry-standard SMB and NFS protocols. You can mount Azure file shares concurrently from cloud and on-premises clients on Windows, Linux, and macOS â no additional software required.

Protocol
Supported clients
Best for

SMB
Windows, Linux, macOS
General-purpose file shares, lift-and-shift apps, hybrid with Azure File Sync

NFS
Linux
Linux workloads, containers, HPC

REST API
All platforms
Programmatic access from applications

## Why use Azure Files?

- Replace or supplement on-premises file servers â Mount Azure file shares directly or cache them on Windows servers with Azure File Sync. Use identity-based authentication with on-premises Active Directory for seamless access control.

- Lift and shift applications â Migrate applications that expect shared file storage to Azure without code changes. Move both the application and its data, or keep the app on-premises and move only the data.

- Simplify cloud development â Store shared application settings, write diagnostic logs, and share dev/test tools across VMs â all from a centralized file share accessible via the REST API or standard file system I/O.

- Containerized workloads â Use Azure file shares as persistent volumes for stateful containers, providing shared storage regardless of which instance runs the container.

## Key benefits

- Fully managed â No hardware to manage, no OS to patch, no disks to replace. Azure handles infrastructure, updates, and backups.

- Shared access â Industry-standard SMB and NFS protocols ensure compatibility with existing applications, tools, and workflows.

- Resilient â Zone-redundant (ZRS) and geo-redundant (GRS) storage options protect against hardware failures and datacenter outages.

- Familiar programmability â Access data through file system I/O APIs, Azure Storage client libraries, or the REST API. Build applications that track file and directory changes by using Azure Files change feed.

- Scriptable â Create, mount, and manage file shares using PowerShell, Azure CLI, the Azure portal, or Azure Storage Explorer.

## Get started

- Plan for an Azure Files deployment

- Create a classic file share (SMB or NFS)

- Create a file share with Microsoft.FileShares (NFS only)

- Mount on Windows | Mount on Linux | Mount on macOS

- Migrate to SMB Azure file shares

- Migrate to NFS Azure file shares

- Azure Files FAQ

 
 

 
 

 

 
 
 
 
 
 
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
 2026-10-16
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
