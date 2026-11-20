# https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/tag-resources

Source: https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/tag-resources

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
 

 

 

 

 
 
# Use tags to organize your Azure resources and management hierarchy

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Tags are metadata elements that you apply to your Azure resources. They are key-value pairs that help you identify resources based on settings that are relevant to your organization. If you want to track the deployment environment for your resources, add a key named `Environment`. To identify the resources deployed to production, give them a value of `Production`. The full key-value pair is `Environment = Production`.

This article describes the conditions and limitations for using tags.

## Tag usage and recommendations

You can apply tags to your Azure resources, resource groups, and subscriptions but not to management groups.

For recommendations on how to implement a tagging strategy, see Resource naming and tagging decision guide.

Resource tags support all cost-accruing services. To ensure that cost-accruing services are provisioned with a tag, use one of the tag policies.

Warning

Tags are stored as plain text. Do not add sensitive values to tags. Sensitive values could be exposed through many methods, including cost reports, commands that return existing tag definitions, deployment histories, exported templates, and monitoring logs.

Warning

Be careful when using non-English language in your tags. It can cause decoding progress failure while loading your virtual machine's metadata from IMDS (Instance Metadata Service).

Important

Tag names are case-insensitive for operations. An operation updates or retrieves a tag with a tag name, regardless of the casing. However, the resource provider might keep the casing you provide for the tag name. You see that casing in cost reports.

Tag values are case-sensitive.

Note

This article provides steps about how to delete personal data from the device or service and can be used to support your obligations under the GDPR. For general information about GDPR, see the GDPR section of the Microsoft Trust Center and the GDPR section of the Service Trust portal.

## Required access

There are two ways to get the required access to tag resources:

- You can have write access to the `Microsoft.Resources/tags` resource type. This access lets you tag any resource, even if you don't have access to the resource itself. The Tag Contributor role grants this access. For example, this role can't apply tags to resources or resource groups through the Azure portal. However, it can apply tags to subscriptions through the Azure portal. It supports all tag operations through Azure PowerShell and REST API.

- You can have write access to the resource itself. The Contributor role grants the required access to apply tags to any entity. To apply tags to only one resource type, use the Contributor role for that resource. To apply tags to virtual machines, use the Virtual Machine Contributor role.

## Inherit tags

Resources don't inherit the tags you apply to a resource group or a subscription. To apply tags from a subscription or resource group to the resources, see Assign policy definitions for tag compliance.

You can group costs for an Azure resource by using the cm-resource-parent tag. This tag lets you review tagged costs in Microsoft Cost Management without having to use filters. The key for this tag is `cm-resource-parent` and its value is the resource ID of the Azure resource you want to group costs by. For example, to group costs by an Azure Virtual Desktop host pool, provide the resource ID of the host pool. For more information, see Group related resources in the Resources view.

## Tags and billing

Use tags to group your billing data. For example, if you're running multiple virtual machines for different organizations, use the tags to group usage by cost center. You can also use tags to categorize costs by runtime environment, including the billing usage for virtual machines running in the production environment.

To retrieve information about tags, download the usage file from the Azure portal. For more information, see Download or view your Azure billing invoice. For services that support tags with billing, the tags appear in the Tags column.

For REST API operations, see the Azure Billing REST API overview.

## Unique tags pagination

When you call the Unique tags API, there's a limit to the size of each API response page. A tag that has a large set of unique values requires the API to fetch the next page to retrieve the remaining set of values. When the results are divided over multiple pages, the API response shows the tag key again to indicate that the values are still under this key.

This behavior can cause some tools like the Azure portal to show the tag key twice.

## Limitations

The following limitations apply to tags:

- Not all resource types support tags. To determine if you can apply a tag to a resource type, see Tag support for Azure resources.

- Each resource type might have specific requirements when working with tags. For example, you can only update tags on virtual machine extensions when the virtual machine is running. If you receive an error message while trying to update a tag, follow the instructions in the message.

- Each resource, resource group, and subscription can have a maximum of 50 tag name-value pairs. If you need to apply more tags than the maximum allowed number, use a JSON string for the tag value. The JSON string can contain many of the values that you apply to a single tag name. A resource group or subscription can contain many resources that each have 50 tag name-value pairs.

- The tag name has a limit of 512 characters and the tag value has a limit of 256 characters. For storage accounts, the tag name has a limit of 128 characters and the tag value has a limit of 256 characters.

- Classic resources such as Cloud Services don't support tags.

- Azure IP Groups and Azure Firewall policies don't support PATCH operations. Therefore, PATCH API method operations can't update tags through the Azure portal. Instead, use the update commands for those resources. For example, you can update tags for an IP group with the `az network ip-group update` command.

- Tag names can't contain these characters: `<`, `>`, `%`, `&`, `\`, `?`, `/`

Note

- Azure DNS zones don't support the use of spaces or parentheses in the tag or a tag that starts with a number. Azure DNS tag names don't support special and Unicode characters. The value can contain all characters.

- Traffic Manager doesn't support the use of spaces, `#`, or `:` in the tag name. The tag name can't start with a number.

- Azure Front Door doesn't support the use of `#` or `:` in the tag name.

- The following Azure resources only support 15 tags:

- Azure Automation

- Azure Content Delivery Network

- Azure Public DNS (Zone and A records)

- Azure Private DNS (Zone and A records)

- Azure Log Analytics saved search

## Next steps

For more information on how to work with tags, see:

- Azure portal

- Azure CLI

- Azure PowerShell

- Python

- ARM templates

- Bicep

 
 

 
 

 

 
 
 
 
 
 
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
 2025-09-15
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
