# https://learn.microsoft.com/en-us/azure/storage/files/storage-files-active-directory-overview

Source: https://learn.microsoft.com/en-us/azure/storage/files/storage-files-active-directory-overview

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
 

 

 

 

 
 
# Overview of Azure Files identity-based authentication for SMB access

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Applies to: âï¸ SMB file shares

This article explains how you can use identity-based authentication, either on-premises or in Azure, to enable identity-based access to Azure Files over Server Message Block (SMB) protocol. Just like Windows file servers, you can grant permissions to an identity at the share, directory, or file level. There's no extra service charge to enable identity-based authentication on your storage account.

Azure Files supports identity-based authentication over SMB for Windows, Linux, and macOS clients. To configure Linux clients, see Configure Linux clients for Azure Files with on-premises AD DS or Configure Linux clients for Azure Files with Microsoft Entra Domain Services. Azure Files doesn't currently support identity-based authentication for Network File System (NFS) file shares.

## Why use identity-based authentication?

For security reasons, use identity-based authentication to access SMB file shares instead of the storage account key. It's also more convenient than using storage account keys in many scenarios:

- Using identity-based authentication provides a seamless migration experience when replacing on-premises file servers, allowing end users to continue to access their data with the same credentials.

- Identity-based authentication eliminates the need to change your directory service when moving applications to the cloud, expediting cloud adoption.

- For file share DR scenarios, you can configure identity-based authentication to support proper access control enforcement upon failover.

## How it works

Azure Files uses the Kerberos protocol to authenticate with an identity source. When an identity associated with a user or application running on a client attempts to access data in Azure Files, the request is sent to the identity source to authenticate the identity. If authentication is successful, the identity source returns a Kerberos ticket. The client then sends a request that includes the Kerberos ticket, and Azure Files uses that ticket to authorize the request. The Azure Files service only receives the Kerberos ticket, not the user's access credentials.

All three identity sources require Kerberos to be enabled under Authentication methods in the storage account's SMB security settings. For instructions, see SMB security settings.

## Choose an identity source for your storage account

Before you enable identity-based authentication on your storage account, decide which identity source to use. Most companies and organizations have some type of domain environment configured, so you likely already have one. Consult your Active Directory (AD) or IT admin to be sure. If you don't already have an identity source, you need to configure one before you can enable identity-based authentication.

### Supported authentication scenarios

You can enable identity-based authentication over SMB by using one of three identity sources: On-premises Active Directory Domain Services (AD DS), Microsoft Entra Domain Services, or Microsoft Entra Kerberos. You can use only one identity source for file access authentication per storage account, and it applies to all file shares in the account.

Use the following table to choose an identity source.

Identity source
Best fit
Identities and clients
Key requirements

AD DS
Organizations with an existing AD DS environment and clients that can reach its domain controllers
AD DS users on Windows and Linux
Sync identities to Microsoft Entra ID for user- and group-specific share permissions. Clients must reach the domain controllers. Manage file and directory permissions from a Windows client by using File Explorer or `icacls`.

Microsoft Entra Domain Services
Organizations that already use or need a managed domain in Azure
Cloud-only or hybrid identities on Windows and Linux
Join clients to the managed domain and provide connectivity to its domain controllers. Manage file and directory permissions from a Windows client by using File Explorer or `icacls`.

Microsoft Entra Kerberos
Cloud-first or hybrid/mixed environments, Microsoft Entra-joined clients, FSLogix profiles, macOS clients, or clients without domain-controller connectivity
Hybrid or cloud-only identities on Windows and macOS (preview). Linux user authentication isn't supported.
Clients don't need domain-controller connectivity for authentication. Exclude the storage account application from applicable multifactor authentication (MFA) policies. For cloud-only identities, manage file and directory permissions by using the Azure portal or `RestSetAcls`. Organizations with a mix of cloud-first/cloud-only clients and on-premises joined clients should configure the on-premises clients with cloud trust and configure cloud-first/cloud-only clients to use Microsoft Entra Kerberos.

For applications and Azure compute workloads that need keyless SMB access, consider using a managed identity. Managed identity is separate from the three user identity sources and can coexist with user identity-based authentication on the same storage account.

After you choose an identity source:

- Enable the identity source on the storage account.

- Assign share-level permissions.

- Configure file and directory permissions.

- Configure network access and DNS.

- Prepare the clients and mount the file share.

Authentication is only one part of access. To access a file or directory, the identity needs share-level permission and the appropriate file or directory permission. Configure network connectivity separately.

Tip

You can change the identity source on a storage account later if your requirements change. For example, if you're moving from on-premises AD DS to cloud-only or hybrid identities backed by Microsoft Entra ID, you can migrate the storage account from AD DS to Microsoft Entra Kerberos authentication. Changing the identity source temporarily interrupts identity-based access to all file shares in the storage account. For guidance, see Change the identity source for Azure file shares.

## Enable an identity source on your storage account

After you choose an identity source, enable it on your storage account.

### AD DS

For AD DS authentication, you can host your AD domain controllers on Azure VMs or on-premises. Either way, your clients must have unimpeded network connectivity to the domain controller, so they must be within the corporate network or virtual network (VNET) of your domain service. We recommend domain-joining your client machines or VMs so that users don't have to provide explicit credentials each time they access the share.

The following diagram depicts on-premises AD DS authentication to Azure file shares over SMB. You must sync the on-premises AD DS to Microsoft Entra ID by using Microsoft Entra Connect Sync or Microsoft Entra Connect cloud sync. Only hybrid user identities that exist in both on-premises AD DS and Microsoft Entra ID can be authenticated and authorized for Azure file share access. This requirement exists because you configure the share-level permission against the identity represented in Microsoft Entra ID, whereas the directory and file-level permission is enforced with that in AD DS. Configure the permissions correctly for the same hybrid user.

To enable AD DS authentication, first read Overview - on-premises Active Directory Domain Services authentication over SMB for Azure file shares and then see Enable AD DS authentication for Azure file shares.

### Microsoft Entra Kerberos

By enabling and configuring Microsoft Entra ID to authenticate hybrid or cloud-only identities, Microsoft Entra users can access Azure file shares by using Kerberos authentication. This configuration uses Microsoft Entra ID to issue the Kerberos tickets to access the file share by using the industry-standard SMB protocol. This means end users can access Azure file shares without requiring network connectivity to domain controllers.

Important

To use Microsoft Entra Kerberos to authenticate hybrid identities, you need a traditional AD DS deployment. You must sync it to Microsoft Entra ID by using Microsoft Entra Connect Sync or Microsoft Entra Connect cloud sync. Clients must be Microsoft Entra-joined or Microsoft Entra hybrid joined.

The following diagram represents the workflow for Microsoft Entra Kerberos authentication for hybrid (that is, not cloud-only) identities over SMB.

For more information, see Enable Microsoft Entra Kerberos authentication on Azure Files.

You can also use this feature to store FSLogix profiles on Azure file shares for Microsoft Entra-joined VMs. For more information, see Store FSLogix profile containers on Azure Files using Microsoft Entra ID.

### Microsoft Entra Domain Services

For Microsoft Entra Domain Services authentication, you must enable Microsoft Entra Domain Services and join the virtual machines to the domain. These virtual machines access Azure file shares by using Kerberos authentication. These virtual machines need network connectivity to the Microsoft Entra Domain Services managed domain.

The authentication flow is similar to on-premises AD DS authentication, with the following differences:

- The process automatically creates the storage account identity during enablement.

- All Microsoft Entra ID users can authenticate and be authorized. Users can be cloud-only or hybrid. The platform manages user synchronization from Microsoft Entra ID to Microsoft Entra Domain Services.

#### Access requirements for Microsoft Entra Domain Services

Clients must meet the following requirements to authenticate by using Domain Services authentication.

- Kerberos authentication requires the client to be joined to the Domain Services managed domain.

- Non-Azure clients can't be joined to the Domain Services managed domain.

- Clients that aren't domain-joined can still access Azure file shares by using explicit credentials only if the client has unimpeded network connectivity to the Domain Services domain controllers, for example through VPN or other supported connections.

For more information, see Enable Microsoft Entra Domain Services authentication on Azure Files.

## See also

- Overview of Azure Files authorization and access control

- Kerberos Authentication Overview

 
 

 
 

 

 
 
 
 
 
 
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
 2026-09-21
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
