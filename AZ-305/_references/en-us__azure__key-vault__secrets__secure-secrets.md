# https://learn.microsoft.com/en-us/azure/key-vault/secrets/secure-secrets

Source: https://learn.microsoft.com/en-us/azure/key-vault/secrets/secure-secrets

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
 

 

 

 

 
 
# Secure your Azure Key Vault secrets

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Key Vault secrets store sensitive application credentials like passwords, connection strings, and access keys. This article provides security recommendations specific to secrets management.

Note

This article focuses on security practices specific to Key Vault secrets. For comprehensive Key Vault security guidance including network security, identity and access management, and vault architecture, see Secure your Azure Key Vault.

## What to store as secrets

Azure Key Vault secrets are designed for storing service or application credentials. Store the following types of data as secrets:

- Application credentials: Client application secrets, API keys, service principal credentials.

- Connection strings: Database connection strings, storage account connection strings.

- Passwords: Service passwords, application passwords.

- Access keys: Redis Cache keys, Azure Event Hubs keys, Azure Cosmos DB keys, Azure Storage keys.

- SSH keys: Private SSH keys for secure shell access.

Don't store configuration data in Key Vault. IP addresses, service names, feature flags, and other configuration settings should be stored in Azure App Configuration rather than in Key Vault. Key Vault is optimized for cryptographic secrets, not general configuration management.

For more information about secrets, see About Azure Key Vault secrets.

## Secrets storage format

When storing secrets in Key Vault, follow these formatting best practices:

- Store compound credentials properly: For credentials with multiple components (like username/password), store them as:

- A properly formatted connection string, or

- A JSON object containing the credential components

- Use tags for metadata: Store management information like rotation schedules, expiration dates, and ownership in secret tags rather than in the secret value itself.

- Minimize secret size: Keep secret values concise. Large payloads should be stored in Azure Storage with encryption, using a Key Vault key for encryption and a Key Vault secret for the storage access token.

## Secrets rotation

Secrets stored in application memory or configuration files persist for the entire application lifecycle, increasing exposure risk. Implement regular secret rotation to minimize compromise risk:

- Rotate secrets regularly: Rotate secrets frequently based on your organization's security policy and the sensitivity of the credential. Shorter rotation intervals (for example, 60-90 days) reduce exposure risk from compromised secrets.

- Automate rotation: Use Azure Key Vault's rotation capabilities to automate the rotation process

- Use dual credentials: For zero-downtime rotation, implement resources with two sets of authentication credentials

For more information about secrets rotation, see:

- Automate secret rotation for resources with one set of authentication credentials

- Automate secret rotation for resources with two sets of authentication credentials

## Secrets caching and performance

Key Vault enforces service limits to prevent abuse. To optimize secrets access while maintaining security:

- Cache secrets in memory: Cache secrets in your application to reduce Key Vault API calls and avoid throttling. Reuse cached values whenever possible and refresh them when secrets are rotated. For more information, see Azure Key Vault throttling guidance.

- Implement retry logic: Use exponential back-off retry logic to handle transient failures and throttling

- Refresh on rotation: Update cached values when secrets are rotated to ensure applications use current credentials

## Secrets monitoring

Enable monitoring to track secret access patterns and detect potential security issues:

- Enable Key Vault logging: Log all secret access operations to detect unauthorized access attempts. See Azure Key Vault logging

- Set up Event Grid notifications: Monitor secret lifecycle events (created, updated, expired, near expiry) for automated workflows. See Azure Key Vault as Event Grid source

- Configure alerts: Set up Azure Monitor alerts for suspicious access patterns or failed authentication attempts. See Monitoring and alerting for Azure Key Vault

- Review access regularly: Periodically audit who has access to secrets and remove unnecessary permissions

## Related security articles

- Secure your Azure Key Vault: Comprehensive Key Vault security guidance.

- Secure your Azure Key Vault keys: Security best practices for cryptographic keys.

- Secure your Azure Key Vault certificates: Security best practices for certificates.

## Next steps

- About Azure Key Vault secrets

- Azure Key Vault developer's guide

- Monitor Key Vault with Azure Monitor

 
 

 
 

 

 
 
 
 
 
 
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
 2026-07-10
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
