# https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/template-parameters

Source: https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/template-parameters

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
 

 

 

 

 
 
# Parameters in ARM templates

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This article describes how to define and use parameters in your Azure Resource Manager template (ARM template). By providing different values for parameters, you can reuse a template for different environments.

Resource Manager resolves parameter values before starting the deployment operations. Wherever the parameter is used in the template, Resource Manager replaces it with the resolved value.

Each parameter must be set to one of the data types.

In addition to minValue, maxValue, minLength, maxLength, and allowedValues, languageVersion 2.0 introduces some aggregate type validation constraints to be used in definitions, parameters and outputs definitions. These constraints include:

- additionalProperties

- discriminator

- items

- nullable

- prefixItems

- properties

Tip

We recommend Bicep because it offers the same capabilities as ARM templates and the syntax is easier to use. To learn more, see parameters.

You're limited to 256 parameters in a template. For more information, see Template limits.

For parameter best practices, see Parameters.

## Minimal declaration

At a minimum, every parameter needs a name and type.

When you deploy a template via the Azure portal, camel-cased parameter names are turned into space-separated names. For example, demoString in the following example is shown as Demo String. For more information, see Use a deployment button to deploy templates from GitHub repository and Deploy resources with ARM templates and Azure portal.

`"parameters": {
 "demoString": {
 "type": "string"
 },
 "demoInt": {
 "type": "int"
 },
 "demoBool": {
 "type": "bool"
 },
 "demoObject": {
 "type": "object"
 },
 "demoArray": {
 "type": "array"
 }
}
`

## Secure parameters

You can mark string or object parameters as secure. The value of a secure parameter isn't saved to the deployment history and isn't logged.

Redaction applies to the secure value itself. It isn't guaranteed to apply to a value that a template transforms or derives from the secure value, such as a reversed string, substring, re-encoded value, or concatenated value. Avoid placing secrets in expressions that transform them when the result might appear in an error message.

Secure parameters reduce the risk of exposing secrets, but they don't make every value derived from a secret safe to disclose. Don't include secrets in resource names, error-prone configuration strings, outputs, tags, or other values that might be returned by a resource provider. When you troubleshoot a failed deployment, treat error messages as potentially sensitive and review them before sharing them.

`"parameters": {
 "demoPassword": {
 "type": "secureString"
 },
 "demoSecretObject": {
 "type": "secureObject"
 }
}
`

## Allowed values

You can define allowed values for a parameter. You provide the allowed values in an array. The deployment fails during validation if a value is passed in for the parameter that isn't one of the allowed values.

`"parameters": {
 "demoEnum": {
 "type": "string",
 "allowedValues": [
 "one",
 "two"
 ]
 }
}
`

## Default value

You can specify a default value for a parameter. The default value is used when a value isn't provided during deployment.

`"parameters": {
 "demoParam": {
 "type": "string",
 "defaultValue": "Contoso"
 }
}
`

To specify a default value along with other properties for the parameter, use the following syntax.

`"parameters": {
 "demoParam": {
 "type": "string",
 "defaultValue": "Contoso",
 "allowedValues": [
 "Contoso",
 "Fabrikam"
 ]
 }
}
`

You can use expressions with the default value. You can't use the reference function or any of the list functions in the parameters section. These functions get the runtime state of a resource, and can't be executed before deployment when parameters are resolved.

Expressions aren't allowed with other parameter properties.

`"parameters": {
 "location": {
 "type": "string",
 "defaultValue": "[resourceGroup().location]"
 }
}
`

You can use another parameter value to build a default value. The following template constructs a host plan name from the site name.

`"parameters": {
 "siteName": {
 "type": "string",
 "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
 },
 "hostingPlanName": {
 "type": "string",
 "defaultValue": "[concat(parameters('siteName'),'-plan')]"
 }
}
`

However, you can't reference a variable as the default value.

## Length constraints

You can specify minimum and maximum lengths for string and array parameters. You can set one or both constraints. For strings, the length indicates the number of characters. For arrays, the length indicates the number of items in the array.

The following example declares two parameters. One parameter is for a storage account name that must have 3-24 characters. The other parameter is an array that must have from 1-5 items.

`"parameters": {
 "storageAccountName": {
 "type": "string",
 "minLength": 3,
 "maxLength": 24
 },
 "appNames": {
 "type": "array",
 "minLength": 1,
 "maxLength": 5
 }
}
`

## Integer constraints

You can set minimum and maximum values for integer parameters. You can set one or both constraints.

`"parameters": {
 "month": {
 "type": "int",
 "minValue": 1,
 "maxValue": 12
 }
}
`

## Object constraints

The object constraints are only allowed on objects, and can only be used with languageVersion 2.0.

### Properties

The value of `properties` is a map of property name => type definition.

The following example would accept `{"foo": "string", "bar": 1}`, but reject `{"foo": "string", "bar": -1}`, `{"foo": "", "bar": 1}`, or any object without a `foo` or `bar` property.

`"parameters": {
 "objectParameter": {
 "type": "object",
 "properties": {
 "foo": {
 "type": "string",
 "minLength": 3
 },
 "bar": {
 "type": "int",
 "minValue": 0
 }
 }
 }
}
`

All properties are required unless the property's type definition has the "nullable": true constraint. To make both properties in the preceding example optional, it would look like:

`"parameters": {
 "objectParameter": {
 "type": "object",
 "properties": {
 "foo": {
 "type": "string",
 "minLength": 3,
 "nullable": true
 },
 "bar": {
 "type": "int",
 "minValue": 0,
 "nullable": true
 }
 }
 }
}
`

### additionalProperties

The value of `additionalProperties` is a type definition or a boolean value. If no `additionalProperties` constraint is defined, the default value is `true`.

If value is a type definition, the value describes the schema that is applied to all properties not mentioned in the `properties` constraint. The following example would accept `{"fizz": "buzz", "foo": "bar"}` but reject `{"property": 1}`.

`"parameters": {
 "dictionaryParameter": {
 "type": "object",
 "properties": {
 "foo": {
 "type": "string",
 "minLength": 3,
 "nullable": true
 },
 "bar": {
 "type": "int",
 "minValue": 0,
 "nullable": true
 }
 },
 "additionalProperties": {
 "type": "string"
 }
 }
}
`

If the value is `false`, no properties beyond those defined in the `properties` constraint may be supplied. The following example would accept `{"foo": "string", "bar": 1}`, but reject `{"foo": "string", "bar": 1, "fizz": "buzz"}`.

`"parameters": {
 "dictionaryParameter": {
 "type": "object",
 "properties": {
 "foo": {
 "type": "string",
 "minLength": 3
 },
 "bar": {
 "type": "int",
 "minValue": 0
 }
 },
 "additionalProperties": false
 }
}
`

If the value is `true`, any property not defined in the `properties` constraint accepts any value. The following example would accept `{"foo": "string", "bar": 1, "fizz": "buzz"}`.

`"parameters": {
 "dictionaryParameter": {
 "type": "object",
 "properties": {
 "foo": {
 "type": "string",
 "minLength": 3
 },
 "bar": {
 "type": "int",
 "minValue": 0
 }
 },
 "additionalProperties": true
 }
}
`

### discriminator

The value `discriminator` defines what schema to apply based on a discriminator property. The following example would accept either `{"type": "ints", "foo": 1, "bar": 2}` or `{"type": "strings", "fizz": "buzz", "pop": "goes", "the": "weasel"}`, but reject `{"type": "ints", "fizz": "buzz"}`.

`"parameters": {
 "taggedUnionParameter": {
 "type": "object",
 "discriminator": {
 "propertyName": "type",
 "mapping": {
 "ints": {
 "type": "object",
 "additionalProperties": {"type": "int"}
 },
 "strings": {
 "type": "object",
 "additionalProperties": {"type": "string"}
 }
 }
 }
 }
}
`

## Array constraints

The array constraints are only allowed on arrays, and can only be used with languageVersion 2.0.

### prefixItems

The value of `prefixItems` is an array of type definitions. Each type definition in the value is the schema to be used to validate the element of an array at the same index. The following example would accept `[1, true]` but reject `[1, "string"]` or `[1]`:

`"parameters": {
 "tupleParameter": {
 "type": "array",
 "prefixItems": [
 {"type": "int"},
 {"type": "bool"}
 ]
 }
}
`

### items

The value of `items` is a type definition or a boolean. If no `items` constraint is defined, the default value is `true`.

If value is a type definition, the value describes the schema that is applied to all elements of the array whose index is greater than the largest index of the `prefixItems` constraint. The following example would accept `[1, true, 1]` or `[1, true, 1, 1]` but reject `[1, true, "foo"]`:

`"parameters": {
 "tupleParameter": {
 "type": "array",
 "prefixItems": [
 { "type": "int" },
 { "type": "bool" }
 ],
 "items": { "type": "int" },
 "defaultValue": [1, true, "foo"]
 }
}
`

You can use `items` without using `prefixItems`. The following example would accept `[1, 2]` or `[1]` but reject `["foo"]`:

`"parameters": {
 "intArrayParameter": {
 "type": "array",
 "items": {"type": "int"}
 }
}
`

If the value is `false`, the validated array must be the exact same length as the `prefixItems` constraint. The following example would accept `[1, true]`, but reject `[1, true, 1]`, and `[1, true, false, "foo", "bar"]`.

`"parameters": {
 "tupleParameter": {
 "type": "array",
 "prefixItems": [
 {"type": "int"},
 {"type": "bool"}
 ],
 "items": false
 }
}
`

If the value is true, elements of the array whose index is greater than the largest index of the `prefixItems` constraint accept any value. The following examples would accept `[1, true]`, `[1, true, 1]` and `[1, true, false, "foo", "bar"]`.

`"parameters": {
 "tupleParameter": {
 "type": "array",
 "prefixItems": [
 {"type": "int"},
 {"type": "bool"}
 ]
 }
}
`

`"parameters": {
 "tupleParameter": {
 "type": "array",
 "prefixItems": [
 {"type": "int"},
 {"type": "bool"}
 ]
 },
 "items": true
}
`

## nullable constraint

The nullable constraint can only be used with languageVersion 2.0. It indicates that the value may be `null` or omitted. See Properties for an example.

## Description

You can add a description to a parameter to help users of your template understand the value to provide. When deploying the template through the portal, the text you provide in the description is automatically used as a tip for that parameter. Only add a description when the text provides more information than can be inferred from the parameter name.

`"parameters": {
 "virtualMachineSize": {
 "type": "string",
 "metadata": {
 "description": "Must be at least Standard_A3 to support 2 NICs."
 },
 "defaultValue": "Standard_DS1_v2"
 }
}
`

## Use parameter

To reference a parameter's value, use the parameters function. The following example uses a parameter value for a key vault name.

`{
 "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
 "contentVersion": "1.0.0.0",
 "parameters": {
 "vaultName": {
 "type": "string",
 "defaultValue": "[format('keyVault{0}', uniqueString(resourceGroup().id))]"
 }
 },
 "resources": [
 {
 "type": "Microsoft.KeyVault/vaults",
 "apiVersion": "2025-05-01",
 "name": "[parameters('vaultName')]",
 ...
 }
 ]
}
`

## Objects as parameters

You can organize related values by passing them in as an object. This approach also reduces the number of parameters in the template.

The following example shows a parameter that is an object. The default value shows the expected properties for the object. Those properties are used when defining the resource to deploy.

`{
 "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
 "contentVersion": "1.0.0.0",
 "parameters": {
 "vNetSettings": {
 "type": "object",
 "defaultValue": {
 "name": "VNet1",
 "location": "eastus",
 "addressPrefixes": [
 {
 "name": "firstPrefix",
 "addressPrefix": "10.0.0.0/22"
 }
 ],
 "subnets": [
 {
 "name": "firstSubnet",
 "addressPrefix": "10.0.0.0/24"
 },
 {
 "name": "secondSubnet",
 "addressPrefix": "10.0.1.0/24"
 }
 ]
 }
 }
 },
 "resources": [
 {
 "type": "Microsoft.Network/virtualNetworks",
 "apiVersion": "2025-01-01",
 "name": "[parameters('vNetSettings').name]",
 "location": "[parameters('vNetSettings').location]",
 "properties": {
 "addressSpace": {
 "addressPrefixes": [
 "[parameters('vNetSettings').addressPrefixes[0].addressPrefix]"
 ]
 },
 "subnets": [
 {
 "name": "[parameters('vNetSettings').subnets[0].name]",
 "properties": {
 "addressPrefix": "[parameters('vNetSettings').subnets[0].addressPrefix]"
 }
 },
 {
 "name": "[parameters('vNetSettings').subnets[1].name]",
 "properties": {
 "addressPrefix": "[parameters('vNetSettings').subnets[1].addressPrefix]"
 }
 }
 ]
 }
 }
 ]
}
`

## Example templates

The following examples demonstrate scenarios for using parameters.

Template
Description

parameters with functions for default values
Demonstrates how to use template functions when defining default values for parameters. The template doesn't deploy any resources. It constructs parameter values and returns those values.

parameter object
Demonstrates using an object for a parameter. The template doesn't deploy any resources. It constructs parameter values and returns those values.

## Next steps

- To learn about the available properties for parameters, see Understand the structure and syntax of ARM templates.

- To learn about passing in parameter values as a file, see Create Resource Manager parameter file.

- For recommendations about creating parameters, see Best practices - parameters.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-04
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
