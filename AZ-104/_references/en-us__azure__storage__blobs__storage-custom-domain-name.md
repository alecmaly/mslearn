# https://learn.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name

Source: https://learn.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name

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
 

 

 

 

 
 
# Map a custom domain to an Azure Blob Storage endpoint

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 You can map a custom domain to a blob service endpoint or a static website endpoint.

This article assumes that you have an existing Azure storage account, access to your domain registrar's DNS management page, and a custom subdomain to map. Root domains aren't supported.

Note

This mapping works only for subdomains (for example: `www.contoso.com`). If you want your web endpoint to be available on the root domain (for example: `contoso.com`), then you need to use Azure CDN. For guidance, see the Map a custom domain with HTTPS enabled section of this article. Because you're going to that section of this article to enable the root domain of your custom domain, the step within that section for enabling HTTPS is optional.

## Map a custom domain with only HTTP enabled

This approach is easier, but it only enables HTTP access. If the storage account is configured to require secure transfer over HTTPS, then you must enable HTTPS access for your custom domain.

To enable HTTPS access, see the Map a custom domain with HTTPS enabled section of this article.

### Map a custom domain

Important

Your custom domain is briefly unavailable to users while you complete the configuration. If your domain currently supports an application with a service-level agreement (SLA) that requires zero downtime, follow the steps in the Map a custom domain with zero downtime section of this article to ensure that users can access your domain while the DNS mapping takes place.

If a brief interruption is acceptable, follow these steps.

Step 1: Get the host name of your storage endpoint.
Step 2: Create a canonical name (CNAME) record with your domain provider.
Step 3: Register the custom domain with Azure.
Step 4: Test your custom domain.

#### Step 1: Get the host name of your storage endpoint

The host name is the storage endpoint URL without the protocol identifier and the trailing slash.

- In the Azure portal, go to your storage account.

- In the menu pane, under Settings, select Endpoints.

- Copy the value of the Blob service endpoint or the Static website endpoint to a text file.

Note

The Data Lake storage endpoint isn't supported (for example, `https://mystorageaccount.dfs.core.windows.net/`).

- Remove the protocol identifier (for example, `HTTPS`) and the trailing slash from that string. The following table contains examples.

Type of endpoint
endpoint
host name

blob service
`https://mystorageaccount.blob.core.windows.net/`
`mystorageaccount.blob.core.windows.net`

static website
`https://mystorageaccount.z5.web.core.windows.net/`
`mystorageaccount.z5.web.core.windows.net`

Set this value aside for later.

#### Step 2: Create a canonical name (CNAME) record with your domain provider

Create a CNAME record to point to your host name. A CNAME record is a type of Domain Name System (DNS) record that maps a source domain name to a destination domain name.

Note

CNAME records must be accessible to public networks. If CNAME records are private, registration with Azure fails.

- Sign in to your domain registrar's website, and then go to the page for managing DNS settings.

You might find the page in a section named Domain Name, DNS, or Name Server Management.

- Find the section for managing CNAME records.

You might have to go to an advanced settings page and look for CNAME, Alias, or Subdomains.

- Create a CNAME record. As part of that record, provide the following items:

- The subdomain alias such as `www` or `photos`. You must provide a subdomain. Root domains aren't supported.

- The host name that you obtained in the Get the host name of your storage endpoint section earlier in this article.

#### Step 3: Register your custom domain with Azure

- 
Portal

- 
PowerShell

- 
Azure CLI

- In the Azure portal, go to your storage account.

- In the menu pane, under Security + networking, select Networking.

- In the Networking page, choose the Custom domain tab.

Note

This option doesn't appear in accounts that have the hierarchical namespace feature enabled. For those accounts, use either PowerShell or the Azure CLI to complete this step.

- In the Domain name text box, enter the name of your custom domain, including the subdomain.

For example, if your domain is contoso.com and your subdomain alias is www, enter `www.contoso.com`. If your subdomain is photos, enter `photos.contoso.com`.

- To register the custom domain, choose the Save button.

After the CNAME record propagates through the Domain Name System (DNS), and if your users have the appropriate permissions, they can view blob data by using the custom domain.

Run the following PowerShell command:

`Set-AzStorageAccount -ResourceGroupName <resource-group-name> -Name <storage-account-name> -CustomDomainName <custom-domain-name> -UseSubDomain $false
`

- Replace the `<resource-group-name>` placeholder with the name of the resource group.

- Replace the `<storage-account-name>` placeholder with the name of the storage account.

- Replace the `<custom-domain-name>` placeholder with the name of your custom domain, including the subdomain.

For example, if your domain is contoso.com and your subdomain alias is www, enter `www.contoso.com`. If your subdomain is photos, enter `photos.contoso.com`.

After the CNAME record propagates through the Domain Name System (DNS), and if your users have the appropriate permissions, they can view blob data by using the custom domain.

Run the following Azure CLI command:

`az storage account update \
 --resource-group <resource-group-name> \
 --name <storage-account-name> \
 --custom-domain <custom-domain-name> \
 --use-subdomain false
`

- Replace the `<resource-group-name>` placeholder with the name of the resource group.

- Replace the `<storage-account-name>` placeholder with the name of the storage account.

- Replace the `<custom-domain-name>` placeholder with the name of your custom domain, including the subdomain.

For example, if your domain is contoso.com and your subdomain alias is www, enter `www.contoso.com`. If your subdomain is photos, enter `photos.contoso.com`.

After the CNAME record propagates through the Domain Name System (DNS), and if your users have the appropriate permissions, they can view blob data by using the custom domain.

#### Step 4: Test your custom domain

To confirm that your custom domain is mapped to your blob service endpoint, create a blob in a public container within your storage account. Then, in a web browser, access the blob by using a URI in the following format: `http://<subdomain.customdomain>/<mycontainer>/<myblob>`

For example, to access a web form in the `myforms` container in the photos.contoso.com custom subdomain, you might use the following URI: `http://photos.contoso.com/myforms/applicationform.htm`

### Map a custom domain with zero downtime

Note

If a brief interruption is acceptable, consider the steps in the Map a custom domain section of this article. It's a simpler approach with fewer steps.

If your domain currently supports an application with a service-level agreement (SLA) that requires zero downtime, follow these steps to ensure that users can access your domain while the DNS mapping takes place.

Step 1: Get the host name of your storage endpoint.
Step 2: Create an intermediary canonical name (CNAME) record with your domain provider.
Step 3: Pre-register the custom domain with Azure.
Step 4: Create a CNAME record with your domain provider.
Step 5: Test your custom domain.

#### Step 1: Get the host name of your storage endpoint

The host name is the storage endpoint URL without the protocol identifier and the trailing slash.

- In the Azure portal, go to your storage account.

- In the menu pane, under Settings, select Endpoints.

- Copy the value of the Blob service endpoint or the Static website endpoint to a text file.

- Remove the protocol identifier (for example, `HTTPS`) and the trailing slash from that string. The following table contains examples.

Type of endpoint
endpoint
host name

blob service
`https://mystorageaccount.blob.core.windows.net/`
`mystorageaccount.blob.core.windows.net`

static website
`https://mystorageaccount.z5.web.core.windows.net/`
`mystorageaccount.z5.web.core.windows.net`

Set this value aside for later.

#### Step 2: Create an intermediary canonical name (CNAME) record with your domain provider

Create a temporary CNAME record to point to your host name. A CNAME record is a type of DNS record that maps a source domain name to a destination domain name.

Note

CNAME records must be accessible to public networks. If CNAME records are private, registration with Azure fails.

- Sign in to your domain registrar's website, and then go to the page for managing DNS settings.

You might find the page in a section named Domain Name, DNS, or Name Server Management.

- Find the section for managing CNAME records.

You might have to go to an advanced settings page and look for CNAME, Alias, or Subdomains.

- Create a CNAME record. As part of that record, provide the following items:

- The subdomain alias such as `www` or `photos`. The subdomain is required. Root domains aren't supported.

Add the `asverify` subdomain to the alias. For example: `asverify.www` or `asverify.photos`.

- The host name that you obtained in the Get the host name of your storage endpoint section earlier in this article.

Add the subdomain `asverify` to the host name. For example: `asverify.mystorageaccount.blob.core.windows.net`.

#### Step 3: Pre-register your custom domain with Azure

When you preregister your custom domain with Azure, you permit Azure to recognize your custom domain without having to modify the DNS record for the domain. That way, when you do modify the DNS record for the domain, it is mapped to the blob endpoint with no downtime.

- 
Portal

- 
PowerShell

- 
Azure CLI

- In the Azure portal, go to your storage account.

- In the menu pane, under Security + networking, select Networking.

- In the Networking page, choose the Custom domain tab.

Note

This option doesn't appear in accounts that have the hierarchical namespace feature enabled. For those accounts, use either PowerShell or the Azure CLI to complete this step.

- In the Domain name text box, enter the name of your custom domain, including the subdomain.

For example, if your domain is contoso.com and your subdomain alias is www, enter `www.contoso.com`. If your subdomain is photos, enter `photos.contoso.com`.

- Select the Use indirect CNAME validation check box.

- To register the custom domain, choose the Save button.

If the registration is successful, the portal notifies you that your storage account was successfully updated. Azure verified your custom domain, but traffic to your domain isn't yet being routed to your storage account until you create a CNAME record with your domain provider. You'll do that in the next section.

Run the following PowerShell command:

`Set-AzStorageAccount -ResourceGroupName <resource-group-name> -Name <storage-account-name> -CustomDomainName <custom-domain-name> -UseSubDomain $true
`

- Replace the `<resource-group-name>` placeholder with the name of the resource group.

- Replace the `<storage-account-name>` placeholder with the name of the storage account.

- Replace the `<custom-domain-name>` placeholder with the name of your custom domain, including the subdomain.

For example, if your domain is contoso.com and your subdomain alias is www, enter `www.contoso.com`. If your subdomain is photos, enter `photos.contoso.com`.

Traffic to your domain isn't yet being routed to your storage account until you create a CNAME record with your domain provider. You'll do that in the next section.

Run the following Azure CLI command:

`az storage account update \
 --resource-group <resource-group-name> \
 --name <storage-account-name> \
 --custom-domain <custom-domain-name> \
 --use-subdomain true
`

- Replace the `<resource-group-name>` placeholder with the name of the resource group.

- Replace the `<storage-account-name>` placeholder with the name of the storage account.

- Replace the `<custom-domain-name>` placeholder with the name of your custom domain, including the subdomain.

For example, if your domain is contoso.com and your subdomain alias is www, enter `www.contoso.com`. If your subdomain is photos, enter `photos.contoso.com`.

Traffic to your domain isn't yet being routed to your storage account until you create a CNAME record with your domain provider. You'll do that in the next section.

#### Step 4: Create a CNAME record with your domain provider

Create a temporary CNAME record to point to your host name.

- Sign in to your domain registrar's website, and then go to the page for managing DNS settings.

You might find the page in a section named Domain Name, DNS, or Name Server Management.

- Find the section for managing CNAME records.

You might have to go to an advanced settings page and look for CNAME, Alias, or Subdomains.

- Create a CNAME record. As part of that record, provide the following items:

- The subdomain alias such as `www` or `photos`. The subdomain is required. Root domains aren't supported.

- The host name that you obtained in the Get the host name of your storage endpoint section earlier in this article.

#### Step 5: Test your custom domain

To confirm that your custom domain is mapped to your blob service endpoint, create a blob in a public container within your storage account. Then, in a web browser, access the blob by using a URI in the following format: `http://<subdomain.customdomain>/<mycontainer>/<myblob>`

For example, to access a web form in the `myforms` container in the photos.contoso.com custom subdomain, you might use the following URI: `http://photos.contoso.com/myforms/applicationform.htm`

### Remove a custom domain mapping

To remove a custom domain mapping, deregister the custom domain. Use one of the following procedures.

- 
Portal

- 
PowerShell

- 
Azure CLI

- In the Azure portal, go to your storage account.

- In the menu pane, under Security + networking, select Networking.

- In the Networking page, choose the Custom domain tab.

- Clear the contents of the text box that contains your custom domain name.

- Select the Save button.

After the custom domain is removed, the portal notifies you that your storage account was successfully updated.

Note

We recommend that you use the Azure Az PowerShell module to interact with Azure. To get started, see Install Azure PowerShell. To learn how to migrate to the Az PowerShell module, see Migrate Azure PowerShell from AzureRM to Az.

To remove a custom domain registration, use the Set-AzStorageAccount PowerShell cmdlet, and then specify an empty string (`""`) for the `-CustomDomainName` argument value.

- Command format:

`Set-AzStorageAccount `
 -ResourceGroupName "<resource-group-name>" `
 -AccountName "<storage-account-name>" `
 -CustomDomainName ""
`

- Command example:

`Set-AzStorageAccount `
 -ResourceGroupName "myresourcegroup" `
 -AccountName "mystorageaccount" `
 -CustomDomainName ""
`

To remove a custom domain registration, use the az storage account update CLI command, and then specify an empty string (`""`) for the `--custom-domain` argument value.

- Command format:

`az storage account update \
 --name <storage-account-name> \
 --resource-group <resource-group-name> \
 --custom-domain ""
`

- Command example:

`az storage account update \
 --name mystorageaccount \
 --resource-group myresourcegroup \
 --custom-domain ""
`

## Map a custom domain with HTTPS enabled

This approach involves more steps, but it enables HTTPS access.
If you don't need users to access your blob or web content by using HTTPS, then see the Map a custom domain with only HTTP enabled section of this article.
This approach uses Azure Front Door (preferred) or Azure CDN which are Content Delivery Network services offered by Azure.

Note

Custom domain mapping requires the use of CNAME records. Public networks must be able to access CNAME records. If CNAME records are private, registration with Azure fails.

### Use Azure Front Door

- Enable Azure Front Door on your blob or website endpoint.

For steps, see Integrate an Azure storage account with Azure Front Door.

- Configure a custom domain on Azure Front Door.

- Configure HTTPS on an Azure Front Door custom domain.

Note

When you update your static website, be sure to clear cached content on the AFD edge POPs by purging the AFD endpoint. For more information, see Cache purging in Azure Front Door.

- (Optional) Review the following guidance:

- Learn how to use Azure Front Door with Azure Storage blobs.

- Learn how to enable Azure Front Door Private Link with Azure Blob Storage.

- Learn how to enable Azure Front Door Private Link with Storage Static Website.

- HTTP-to-HTTPS redirection with AFD.

- Front Door Billing.

### Use Azure CDN

- Enable Azure CDN on your blob or web endpoint. For step-by-step guidance, see Integrate an Azure storage account with Azure CDN.

- Map Azure CDN content to a custom domain.

- Enable HTTPS on an Azure CDN custom domain.

Note

When you update your static website, clear cached content on the CDN edge servers by purging the CDN endpoint. For more information, see Purge an Azure CDN endpoint.

- (Optional) Review the following guidance:

- Shared access signature (SAS) tokens with Azure CDN.

- HTTP-to-HTTPS redirection with Azure CDN.

- Pricing and billing when using Blob Storage with Azure CDN.

## Feature support

Support for this feature might be impacted by enabling Data Lake Storage Gen2, Network File System (NFS) 3.0 protocol, or the SSH File Transfer Protocol (SFTP). If you've enabled any of these capabilities, see Blob Storage feature support in Azure Storage accounts to assess support for this feature.

## Next steps

- Learn about static website hosting in Azure Blob storage

 
 

 
 

 

 
 
 
 
 
 
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
 2026-08-25
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
