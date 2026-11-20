# https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/template-outputs

Source: https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/template-outputs

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
 

 

 

 

 
 
# Outputs in ARM templates

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This article describes how to define output values in your Azure Resource Manager template (ARM template). You use outputs when you need to return values from the deployed resources.

The format of each output value must resolve to one of the data types.

Tip

Bicep is recommended since it offers the same capabilities as ARM templates, and the syntax is easier to use. To learn more, see outputs.

You are limited to 64 outputs in a template. For more information, see template limits.

## Define output values

The following example shows how to return a property from a deployed resource. Add the outputs section to the template. The output value gets the fully qualified domain name for a public IP address:

`"outputs": {
 "hostname": {
 "type": "string",
 "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses', variables('publicIPAddressName'))).dnsSettings.fqdn]"
 },
}
`

If you need to output a property that has a hyphen in the name, use brackets around the name instead of dot notation. For example, use `['property-name']` instead of `.property-name`.

`{
 "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
 "contentVersion": "1.0.0.0",
 "variables": {
 "user": {
 "user-name": "Test Person"
 }
 },
 "resources": [
 ],
 "outputs": {
 "nameResult": {
 "type": "string",
 "value": "[variables('user')['user-name']]"
 }
 }
}
`

## Conditional output

You can use the `condition` element to conditionally return a value. Typically, you use a conditional output when you've conditionally deployed a resource. The following example shows how to conditionally return the resource ID for a public IP address based on if a new one was deployed:

`"outputs": {
 "resourceID": {
 "condition": "[equals(parameters('publicIpNewOrExisting'), 'new')]",
 "type": "string",
 "value": "[resourceId('Microsoft.Network/publicIPAddresses', parameters('publicIPAddresses_name'))]"
 }
}
`

For a simple example of conditional output, see conditional output template.

## Dynamic number of outputs

In some scenarios, you don't know the number of instances of a value you need to return when creating the template. You can return a variable number of values by using iterative output. Add the `copy` element to iterate an output:

`"outputs": {
 "storageEndpoints": {
 "type": "array",
 "copy": {
 "count": "[parameters('storageCount')]",
 "input": "[reference(concat(copyIndex(), variables('baseName'))).primaryEndpoints.blob]"
 }
 }
}
`

For more information, see output iteration in ARM templates.

## Linked templates

You can deploy related templates by using linked templates. To retrieve the output value from a linked template, use the `reference` function in the parent template. The syntax in the parent template is:

`"[reference('<deploymentName>').outputs.<propertyName>.value]"
`

The following example shows how to set the IP address on a load balancer by retrieving a value from a linked template:

`"publicIPAddress": {
 "id": "[reference('linkedTemplate').outputs.resourceID.value]"
}
`

If the property name has a hyphen, use brackets around the name instead of dot notation.

`"publicIPAddress": {
 "id": "[reference('linkedTemplate').outputs['resource-ID'].value]"
}
`

You can't use the `reference` function in the outputs section of a nested template. To return the values for a deployed resource in a nested template, convert your nested template to a linked template.

- The public-IP-address template creates a public IP address and outputs the resource ID.

- The load-balancer template links to the preceding template. It uses the resource ID in the output when creating the load balancer.

## Example template

The following template doesn't deploy any resources. It shows some ways of returning outputs of different types:

`{
 "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
 "contentVersion": "1.0.0.0",
 "resources": [],
 "outputs": {
 "stringOutput": {
 "type": "string",
 "value": "[deployment().name]"
 },
 "integerOutput": {
 "type": "int",
 "value": "[length(environment().authentication.audiences)]"
 },
 "booleanOutput": {
 "type": "bool",
 "value": "[contains(deployment().name, 'demo')]"
 },
 "arrayOutput": {
 "type": "array",
 "value": "[environment().authentication.audiences]"
 },
 "objectOutput": {
 "type": "object",
 "value": "[subscription()]"
 }
 }
}
`

## Get output values

When the deployment succeeds, the output values are automatically returned in the results of the deployment.

To get output values from the deployment history, you can use script.

- 
PowerShell

- 
Azure CLI

`(Get-AzResourceGroupDeployment `
 -ResourceGroupName <resource-group-name> `
 -Name <deployment-name>).Outputs.resourceID.value
`

`az deployment group show \
 -g <resource-group-name> \
 -n <deployment-name> \
 --query properties.outputs.resourceID.value
`

## Sort objects in outputs

In JSON, an object is an unordered collection of zero or more key/value pairs. The ordering can be different depending on the implementations. For example, the Bicep items() function sorts the objects in the alphabetical order. In other places, the original ordering can be preserved. Because of this non-determinism, avoid making any assumptions about the ordering of object keys when writing code, which interacts with deployments parameters & outputs.

## Next steps

To learn about the available properties for outputs, see the structure and syntax of ARM templates.

 
 

 
 

 

 
 
 
 
 
 
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
