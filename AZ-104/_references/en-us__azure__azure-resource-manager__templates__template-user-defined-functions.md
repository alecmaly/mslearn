# https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/template-user-defined-functions

Source: https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/template-user-defined-functions

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
 

 

 

 

 
 
# User-defined functions in ARM template

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 User-defined functions help simplify and reuse complex expressions in your ARM templates. By encapsulating logic in custom functions, you can improve template readability, maintainability, and scalability-especially when the same logic appears in multiple places. These functions are distinct from the built-in template functions that are always available. To define user-defined functions in Bicep, see User-defined functions in Bicep.

## Define the function

Your functions require a namespace value to avoid naming conflicts with template functions. The following example shows a function that returns a unique name:

`"functions": [
 {
 "namespace": "contoso",
 "members": {
 "uniqueName": {
 "parameters": [
 {
 "name": "namePrefix",
 "type": "string"
 }
 ],
 "output": {
 "type": "string",
 "value": "[concat(toLower(parameters('namePrefix')), uniqueString(resourceGroup().id))]"
 }
 }
 }
 }
],
`

## Use the function

The following example shows a template that includes a user-defined function to get a unique name for a storage account. The template has a parameter named `storageNamePrefix` that is passed as a parameter to the function.

`{
 "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
 "contentVersion": "1.0.0.0",
 "parameters": {
 "storageNamePrefix": {
 "type": "string",
 "maxLength": 11
 }
 },
 "functions": [
 {
 "namespace": "contoso",
 "members": {
 "uniqueName": {
 "parameters": [
 {
 "name": "namePrefix",
 "type": "string"
 }
 ],
 "output": {
 "type": "string",
 "value": "[format('{0}{1}', toLower(parameters('namePrefix')), uniqueString(resourceGroup().id))]"
 }
 }
 }
 }
],
 "resources": [
 {
 "type": "Microsoft.Storage/storageAccounts",
 "apiVersion": "2025-06-01",
 "name": "[contoso.uniqueName(parameters('storageNamePrefix'))]",
 "location": "South Central US",
 "sku": {
 "name": "Standard_LRS"
 },
 "kind": "StorageV2",
 "properties": {
 "supportsHttpsTrafficOnly": true
 }
 }
 ]
}
`

During deployment, the `storageNamePrefix` parameter is passed to the function:

- The template defines a parameter named `storageNamePrefix`.

- The function uses `namePrefix` because you can only use parameters defined in the function. For more information, see Limitations.

- In the template's `resources` section, the `name` element uses the function and passes the `storageNamePrefix` value to the function's `namePrefix`.

## Limitations

When defining a user function, there are some restrictions:

- The function can't access variables.

- The function can only use parameters that are defined in the function. When you use the parameters function within a user-defined function, you're restricted to the parameters for that function.

- The function can't call other user-defined functions.

- The function can't use the reference function or any of the list functions.

- Parameters for the function can't have default values.

## Next steps

- To learn about the available properties for user-defined functions, see Understand the structure and syntax of ARM templates.

- For a list of the available template functions, see ARM template functions.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-06-26
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
