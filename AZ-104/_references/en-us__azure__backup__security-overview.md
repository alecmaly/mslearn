# https://learn.microsoft.com/en-us/azure/backup/security-overview

Source: https://learn.microsoft.com/en-us/azure/backup/security-overview

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
 

 

 

 

 
 
# Overview of security and cyber recovery in Azure Backup

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Backup helps protect vaulted backup data and supports recovery when production environments are compromised. A logically air-gapped vault combines isolation with controls that protect backup data from unauthorized access and deletion. Cyber recovery essentials helps you identify potential threats to recovery points and recover workloads after a cyber incident.

## Logically air-gapped vault

Azure Backup stores vaulted backup data in a Microsoft-managed Azure subscription and tenant, separate from the production environment where the protected data resides. This logical separation helps keep backup data out of reach of a compromised workload.

A logically air-gapped vault combines four layers of protection:

- Tenant isolation: Separate backup storage from the subscriptions and tenant that host production workloads.

- Indelibility: Preserve recovery points against premature deletion through soft delete and immutability.

- Authorization controls: Protect critical backup operations with multi-user authorization (MUA), separating backup administration from approval of sensitive changes.

- Data encryption: Protect the confidentiality of backup data at rest and in transit.

### Data isolation with Azure Backup

Vaulted backup data resides in storage accounts that Azure Backup manages in a Microsoft-managed subscription and tenant. These storage accounts are separate from the customer's production resources. External users and guest workloads have no direct access to the backup storage or its contents, isolating the backup copy from access to the production environment.

You access vaulted backup data through Azure Backup management operations, such as restore, rather than by accessing the underlying storage accounts. The vault provides the management interface, and its access controls determine who can perform these operations. This separation lets you manage backup and recovery permissions independently of access to the protected workload.

### Management and control of identity and user access

Azure role-based access control (Azure RBAC) lets you assign only the permissions users need to manage backup operations. Azure Backup provides three built-in roles to help you separate duties:

- Backup Contributor: Create and manage backups, except for deleting the Recovery Services vault or granting access to others.

- Backup Operator: Perform backup operations except for removing backups and managing backup policies.

- Backup Reader: View backup management operations.

Learn more about Azure RBAC for Azure Backup.

### Protect backup data from premature deletion

Soft delete and immutability protect recovery points from accidental or malicious deletion. Soft delete retains deleted backup data for a recovery window, giving you time to recover it after an unauthorized deletion. Immutability blocks operations that could delete recovery points before their retention period ends. Locking immutability makes that protection irreversible, helping preserve backups even if an attacker gains administrative access.

Learn more about soft delete and immutable vaults.

### Multi-user authorization

MUA adds an extra authorization layer to critical operations on Recovery Services vaults and Backup vaults. It uses Resource Guard so that a separate authorized user can approve protected operations. This separation of duties helps protect vault settings and backup data if a backup administrator's identity is compromised. Learn about MUA using Resource Guard.

### Encryption of data

Azure Backup encrypts backup data at rest by default with Microsoft-managed keys. For supported Recovery Services vault workloads, you can use customer-managed keys stored in Azure Key Vault. Azure Backup protects data in transit with HTTPS and TLS 1.2 or later. Azure Backup also supports backup and restore of Azure VMs with encrypted disks. For details, see encryption of backup data, customer-managed keys, and backup and restore of encrypted Azure VMs.

## Cyber recovery essentials

Cyber recovery essentials focuses on preparing to identify suspicious backup recovery points and restore data to a supported recovery destination. You can use threat detection, Safe Restore at scale, cross-subscription restore, and cross-tenant restore to prepare for and recover from cyber incidents.

### Threat detection in Azure Backup

Azure Backup threat detection uses security signals from Microsoft Defender for Servers to assess the health of Azure VM backup recovery points. Defender for Cloud scans the source VM for malware, and Azure Backup uses those signals to identify potentially compromised recovery points. This information helps you select a recovery point when planning recovery from ransomware or other attacks. Threat detection is in preview. Learn about threat detection for Azure VM backups.

### Safe Restore at scale

Safe Restore at scale helps you coordinate recovery of multiple protected items after a cyber incident. You specify common restore parameters across the selected items, while retaining control over individual recovery points and restore settings. Applying parameters at scale reduces repetitive work and saves time during incident response. Consistent settings and validation make recovery execution more predictable, while centralized job tracking lets you monitor progress, investigate failures, and trace the outcome of each restore in one place.

For an example of this experience, see restoring Azure VMs in bulk (preview). Workload-specific documentation and support matrices describe available restore options and limitations.

### Cross-subscription restore

Cross-subscription restore lets you recover backup data from Recovery Services vaults and Backup vaults to another subscription in the same Microsoft Entra tenant. During a cyber incident, you can use a separate recovery subscription to restore and validate workloads away from the affected production resources. Separating recovery resources from production also helps you assign recovery permissions independently and rehearse recovery without disrupting production.

### Cross-tenant restore

Cross-tenant restore lets you recover eligible vaulted backup data to a different Microsoft Entra tenant. If a cyberattack compromises the production tenant or leaves you locked out, you can recover workloads in a separate tenant with its own identities and access controls. A vault mapping established before an incident lets authorized users restore from the target tenant without signing in to the source tenant.

Cross-tenant restore is in preview, with support varying by workload and region. Learn about cross-tenant restore and preparing for recovery across tenants.

## Other security controls

Azure Backup also has built-in security controls to prevent, detect, and respond to security vulnerabilities. Learn about the Azure security baseline for Backup.

### Internet connectivity not required for Azure VM backup

Azure VM backup traffic uses the Azure backbone network and doesn't require access to your virtual network. You don't need to allow IP addresses or fully qualified domain names for backup of Azure VMs in secured networks.

### Private endpoints for Azure Backup

Private endpoints provide private connectivity for supported Recovery Services vault workloads, including SQL Server and SAP HANA in Azure VMs, MARS agent backups, DPM, and supported file recovery. For supported scenarios, see private endpoints for Azure Backup.

### Security features to help protect hybrid backups

Azure Backup provides security features for hybrid backups, including extra authentication for critical operations, email notifications for critical operations, and MARS backup data encryption with a passphrase before upload. Data is decrypted only after download, and the passphrase isn't transmitted to Azure Backup. For supported hybrid backup configurations that use these security features, deleted backup data is retained for an extra 14 days, and a minimum number of recovery points is maintained to help recover from corruption. Protect the passphrase so you can restore data when needed. Learn about security features for hybrid backups.

### Monitoring and alerts of suspicious activity

Azure Backup provides built-in monitoring and alerts for backup operations. Use Backup reports to track backup and restore activity and identify trends. For more monitoring options, see monitoring and reporting for Azure Backup.

## Security posture and security levels

Azure Backup security levels summarize security settings applied to protected items. Use them to identify configuration gaps across your backup environment.

Security level
Description
Requirements

Excellent
Backups are protected against accidental deletion and ransomware attacks.
Immutability or soft delete is enabled and irreversible (locked or always-on), and MUA is enabled on the vault.

Good
Existing backups are protected against accidental deletion and have better recovery options.
Immutability is locked or soft delete is enabled.

Fair
Critical backup operations have an extra layer of protection.
MUA is enabled on the vault.

Poor
Basic protection against accidental deletion only.
Advanced protection capabilities aren't enabled, or only reversible capabilities are enabled.

Learn how to review security levels across protected items.

### Compliance with standardized security requirements

Azure Backup provides service controls, certifications, and attestations that can help you assess applicable national, regional, and industry-specific requirements. Review Azure compliance offerings for details.

## Next steps

- Secure by default with soft delete for Azure Backup

- Security features to help protect hybrid backups that use Azure Backup

- Azure Policy regulatory compliance controls for Azure Backup

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-17
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
