# https://learn.microsoft.com/en-us/azure/azure-monitor/fundamentals/activity-log

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/fundamentals/activity-log

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
 

 

 

 

 
 
# Activity log in Azure Monitor

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Monitor records management operations for your Azure resources through the activity log feature. The activity log records operations like creating a virtual machine, changing a key vault access policy, or Resource Manager deployment errors. These management operations are also called control plane operations. Use the activity log to review or audit this information, or create an alert to be proactively notified when an event occurs.

In contrast to the activity log, Azure resource logs capture data plane operations performed within a resource. For example, these operations include getting a secret from a key vault or making a request to a database. Resource logs aren't collected by default and require configuration with a diagnostic setting.

Tip

If a deployment operation error directs you to this article, see Troubleshoot common Azure deployment errors.

## Activity log entries

Azure Monitor collects activity log entries by default with no required configuration. The system generates these entries, and you can't change or delete them. Entries typically result from changes (create, update, and delete operations) or an action being initiated. The activity log doesn't typically capture read operations.

Important

Activity Log isn't an authentication or authorization audit log. Requests that Azure Resource Manager rejects during authentication or authorization before an operation starts don't generate Activity Log entries. Because no entry is generated, these requests don't appear in Activity Log, trigger Activity Log alerts, or flow to destinations configured through diagnostic settings.

Activity log entries are usually available for analysis and alerting within 3 to 20 minutes of the event occurring. For a description of activity log categories, see Azure activity log event schema.

## Retention period

Azure retains activity log events for 90 days and then deletes them. You aren't charged for entries during this time, regardless of volume. For more functionality, such as longer retention, create a diagnostic setting and collect the entries in another location based on your needs. One of the most common reasons to extend the retention period is to preserve resource creator information, which is only available in the activity log.

## View and retrieve the activity log

View activity log events for a subscription, resource group, or an individual resource. Use the Azure portal or programmatically query them by using the Activity Log REST API.

The Azure portal provides the Activity log blade from most service menus. Each of these areas also support programmatic access with REST or through specific Azure CLI and Azure PowerShell commands.

Specify a time interval of events to retrieve. To retrieve events by using the REST API, you must include the `$filter` parameter along with at least an `eventTimestamp` start value. By default, the activity log retains events for 90 days. Make sure both the start and end of your time range fall within that 90-day window.

### Activity log access scenarios

The following sections present common scenarios showing different ways to access and retrieve activity log events through the Azure portal, programmatically using Azure CLI and Azure PowerShell, or with REST calls:

- 
Portal

- 
Azure CLI

- 
Azure PowerShell

- 
REST

Azure portal samples provide extra context around what kind of events to expect in that view.

Azure CLI samples highlight the specific commands available through the az monitor activity-log list command.

Note

The native Azure CLI examples use the subscription selected in your current context. The Bash examples that call REST APIs use `jq` to URL-encode filters.

Azure PowerShell samples highlight the specific cmdlets available through the Get-AzActivityLog cmdlet.

Note

The native Azure PowerShell examples use the subscription selected in your current context.

REST API samples show how to retrieve events by using the required `$filter` parameter with the Activity Log REST API.

The List activity log events for a resource group sample also demonstrates how to explicitly set a timeout for your client to match the maximum timeout period for the activity log REST API of 75 seconds by using the `Prefer` header.

Supported `$filter` patterns
Details

default subscription with a time range
`$filter=eventTimestamp ge '{startTime}' and eventTimestamp le '{endTime}'`

resource group
`$filter=eventTimestamp ge '{startTime}' and eventTimestamp le '{endTime}' and resourceGroupName eq '{resourceGroupName}'`

specific resource
`$filter=eventTimestamp ge '{startTime}' and eventTimestamp le '{endTime}' and resourceUri eq '{resourceURI}'`

resource provider
`$filter=eventTimestamp ge '{startTime}' and eventTimestamp le '{endTime}' and resourceProvider eq '{resourceProviderName}'`

correlation ID
`$filter=eventTimestamp ge '{startTime}' and eventTimestamp le '{endTime}' and correlationId eq '{correlationID}'`

#### List activity log events for a subscription

Subscription level events capture events created directly by resource providers and is the default scope for listing activity log events. Tenant level and management group level events only capture Azure Resource Manager events in those hierarchies. These higher-level scopes do not include events generated directly by resource providers outside of Azure Resource Manager operations.

The following example retrieves activity log events for a subscription during a specific time range.

- 
Portal

- 
Azure CLI

- 
Azure PowerShell

- 
REST

The menu you open Activity log from determines its initial filter. If you open it from the Monitor menu, the only filter selected by default is the subscription. This is the same as opening it from Subscriptions > select subscription > Activity Log.

The following Azure CLI example uses the `az monitor activity-log list` command.

Explicit time range:

Azure CLI supports the same kind of explicit time range as REST by using `--start-time` and `--end-time`:

`# Set variables
startTime="<StartTime>"
endTime="<EndTime>"

# Retrieve activity log events
az monitor activity-log list \
 --start-time "$startTime" \
 --end-time "$endTime"
`

Relative time range:

Azure CLI also supports relative time ranges by using `--offset`.

For example, `--offset 14d` returns events from the last 14 days.

`# Set variables
offset="14d"

# Retrieve activity log events
az monitor activity-log list \
 --offset "$offset"
`

Note

Azure CLI commands use the Azure Resource Manager endpoint from the current CLI context, so management.azure.com doesn't need to be specified in the command syntax.

The following Azure PowerShell example uses the `Get-AzActivityLog` cmdlet.

Explicit time range:

Azure PowerShell supports specifying an exact time range by using `StartTime` and `EndTime`, similar to REST:

`# Set variables
$startTime = [datetime]"<StartTime>"
$endTime = [datetime]"<EndTime>"

# Define parameters for Get-AzActivityLog
$getAzActivityLogParams = @{
 StartTime = $startTime
 EndTime = $endTime
}

# Retrieve activity log events
Get-AzActivityLog @getAzActivityLogParams
`

Relative time range:

Azure PowerShell also supports querying a relative time range by using `Get-Date` expressions for `StartTime` and `EndTime`.

The following example returns events from the last 14 days, ending at the time the command runs.

`# Set variables
$lookbackDays = 14

# Define parameters for Get-AzActivityLog
$getAzActivityLogParams = @{
 StartTime = (Get-Date).AddDays(-$lookbackDays)
 EndTime = Get-Date
}

# Retrieve activity log events
Get-AzActivityLog @getAzActivityLogParams
`

Note

Azure PowerShell cmdlets use the Azure Resource Manager endpoint from the current Az context, so management.azure.com doesnât need to be specified in the cmdlet syntax.

The following REST example uses the `Activity Logs - List` REST API operation.

`GET https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Insights/eventtypes/management/values?api-version={apiVersion}&$filter=eventTimestamp ge '{startTime}' and eventTimestamp le '{endTime}'
Authorization: Bearer {accessToken}
`

#### List activity log events for a resource group

Add `resourceGroupName` to the `$filter` to scope Azure Monitor activity log results to a specific resource group.

- 
Portal

- 
Azure CLI

- 
Azure PowerShell

- 
REST

The menu you open Activity log from determines its initial filter. If you open it from a resource's menu, the filter is set to that resource. Select Add Filter to add more properties to the filter. Here are the other properties you can filter by in the portal:

- Resource - Items that are part of your Azure solution, such as a database or virtual machine.

- Resource type â The category to which a resource belongs, such as virtual machines, web apps, or databases.

- Operation - An action or command, such as create, delete, and write, that affects Azure Resource Manager resources.

- Event initiated by â Filter events by the identity that initiated the event.

- Event category â Filter the event types for certain operations.

The following Azure CLI example uses the `az monitor activity-log list` command.

Note

The REST header `Prefer: wait=75` doesn't have a direct equivalent in the Azure CLI command for this operation. This command issues the query directly and returns the matching Activity Log records.

Use the az monitor activity-log list command to retrieve activity log events scoped to a resource group. Specific Azure CLI commands reduce the complexity of the equivalent REST API call.

`# Set variables
resourceGroupName="<ResourceGroupName>"
offset="30d"

# Retrieve activity log events
az monitor activity-log list \
 --resource-group "$resourceGroupName" \
 --offset "$offset"
`

Note

Azure CLI commands use the Azure Resource Manager endpoint from the current CLI context, so management.azure.com doesn't need to be specified in the command syntax.

The following Azure PowerShell example uses the `Get-AzActivityLog` cmdlet.

Note

The REST header `Prefer: wait=75` doesn't have a direct equivalent in the Azure PowerShell cmdlet for this operation. This command issues the query directly and returns the matching Activity Log records.

Azure PowerShell provides the Get-AzActivityLog cmdlet to retrieve activity log events scoped to a resource group over a relative time range.

`# Set variables
$resourceGroupName = "<ResourceGroupName>"
$lookbackDays = 30

# Define parameters for Get-AzActivityLog
$getAzActivityLogParams = @{
 ResourceGroupName = $resourceGroupName
 StartTime = (Get-Date).AddDays(-$lookbackDays)
 EndTime = Get-Date
}

# Retrieve activity log events
Get-AzActivityLog @getAzActivityLogParams
`

Note

Azure PowerShell cmdlets use the Azure Resource Manager endpoint from the current Az context, so management.azure.com doesnât need to be specified in the cmdlet syntax.

The following REST example uses the `Activity Logs - List` REST API operation.

`GET https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Insights/eventtypes/management/values?api-version={apiVersion}&$filter=eventTimestamp ge '{startTime}' and eventTimestamp le '{endTime}' and resourceGroupName eq '{resourceGroupName}'
Authorization: Bearer {accessToken}
Prefer: wait=75
`

#### Return specific activity log properties

Use a parameter to return only specified properties, which reduces the response payload size. For more information, see Activity log schema property descriptions.

- 
Portal

- 
Azure CLI

- 
Azure PowerShell

- 
REST

The Azure portal doesn't provide a way to limit the properties returned from activity log events directly. To reduce the amount of data viewed, use the Edit columns option in the Activity log blade to select which columns are displayed in the portal view.

The following Azure CLI example uses the `az monitor activity-log list` command.

Use the `--max-events` parameter of `az monitor activity-log list` to limit the number of records returned.

`# Set variables
offset="30d"
maxEvents=100
selectFields=(
 eventName
 operationName
 status
 eventTimestamp
 correlationId
 submissionTimestamp
 level
)

# Retrieve activity log events
az monitor activity-log list \
 --offset "$offset" \
 --max-events "$maxEvents" \
 --select "${selectFields[@]}"
`

Note

Azure CLI commands use the Azure Resource Manager endpoint from the current CLI context, so management.azure.com doesn't need to be specified in the command syntax.

The following Azure PowerShell example uses the `Get-AzActivityLog` cmdlet.

Use the `-MaxRecord` parameter of `Get-AzActivityLog` to limit the number of records returned.

`# Set variables
$lookbackDays = 30
$maxRecord = 100
$selectProperties = @(
 "EventName"
 "OperationName"
 "Status"
 "EventTimestamp"
 "CorrelationId"
 "SubmissionTimestamp"
 "Level"
)

# Define parameters for Get-AzActivityLog
$getAzActivityLogParams = @{
 StartTime = (Get-Date).AddDays(-$lookbackDays)
 EndTime = Get-Date
 MaxRecord = $maxRecord
}

# Retrieve activity log events
Get-AzActivityLog @getAzActivityLogParams |
 Select-Object -Property $selectProperties
`

Note

Azure PowerShell cmdlets use the Azure Resource Manager endpoint from the current Az context, so management.azure.com doesnât need to be specified in the cmdlet syntax.

The following REST example uses the `Activity Logs - List` REST API operation.

`GET https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Insights/eventtypes/management/values?api-version={apiVersion}&$filter=eventTimestamp ge '{startTime}' and eventTimestamp le '{endTime}'&$select=eventName,operationName,status,eventTimestamp,correlationId,submissionTimestamp,level
Authorization: Bearer {accessToken}
`

#### List tenant-level activity log events

Tenant-level activity log events typically have limited entries but might include important events such as management group or subscription creation. These events are separate from subscription-level activity log events, but might contain duplicate resource management events.

Querying at this scope uses a different REST API than the subscription-level activity log events API. Azure CLI and Azure PowerShell don't provide dedicated commands.

- 
Portal

- 
Azure CLI

- 
Azure PowerShell

- 
REST

Go to Monitor > Activity log in the Azure portal. Change the Activity pull down menu and select Directory Activity.

The following Azure CLI example uses az rest to call the `Tenant Activity Logs - List` REST API operation.

`# Set variables
apiVersion="<ApiVersion>"
startTime="<StartTime>"
endTime="<EndTime>"
filter="eventTimestamp ge '$startTime' and eventTimestamp le '$endTime'"
encodedFilter=$(jq -rn --arg filter "$filter" '$filter | @uri')

# Build request URL
apiEndpoint="https://management.azure.com"
provider="Microsoft.Insights/eventtypes/management/values"
queryString="?api-version=$apiVersion&\$filter=$encodedFilter"
url="$apiEndpoint/providers/$provider$queryString"

# Retrieve tenant-level activity log events
az rest --method get --url "$url"
`

The following Azure PowerShell example uses Invoke-AzRestMethod to call the `Tenant Activity Logs - List` REST API operation.

`# Set variables
$apiVersion = "<ApiVersion>"
$startTime = "<StartTime>"
$endTime = "<EndTime>"
$filter = "eventTimestamp ge '$startTime' and eventTimestamp le '$endTime'"
$encodedFilter = [uri]::EscapeDataString($filter)

# Build request URL
$apiEndpoint = "https://management.azure.com"
$provider = "Microsoft.Insights/eventtypes/management/values"
$queryString = "?api-version=$apiVersion&`$filter=$encodedFilter"
$url = "$apiEndpoint/providers/$provider$queryString"

# Define parameters for Invoke-AzRestMethod
$invokeAzRestMethodParams = @{
 Uri = $url
 Method = "GET"
}

# Send request
Invoke-AzRestMethod @invokeAzRestMethodParams
`

The following REST example uses the `Tenant Activity Logs - List` REST API operation.

`GET https://management.azure.com/providers/Microsoft.Insights/eventtypes/management/values?api-version={apiVersion}&$filter=eventTimestamp ge '{startTime}' and eventTimestamp le '{endTime}'
Authorization: Bearer {accessToken}
`

#### List management group-level activity log events

Management group-level activity log events capture events scoped to a specific management group, such as policy assignments and management group membership changes.

Note

- The following examples use the `2017-03-01-preview` API version, which is required for management group-level activity log queries.

- 
Portal

- 
Azure CLI

- 
Azure PowerShell

- 
REST

To view management group-level activity log events in the Azure portal, go to Management groups > select a management group > Activity log.

The following Azure CLI example uses az rest to call the `Management group activity log query` REST API operation.

`# Set variables
apiVersion="<ApiVersion>"
managementGroupId="<ManagementGroupId>"
startTime="<StartTime>"
endTime="<EndTime>"
filter="eventTimestamp ge '$startTime' and eventTimestamp le '$endTime'"
encodedFilter=$(jq -rn --arg filter "$filter" '$filter | @uri')

# Build request URL
apiEndpoint="https://management.azure.com"
path="/providers/Microsoft.Management/managementGroups/$managementGroupId"
provider="Microsoft.Insights/eventtypes/management/values"
queryString="?api-version=$apiVersion&\$filter=$encodedFilter"
url="$apiEndpoint$path/providers/$provider$queryString"

# Retrieve management-group activity log events
az rest --method get --url "$url"
`

The following Azure PowerShell example uses Invoke-AzRestMethod to call the `Management group activity log query` REST API operation.

`# Set variables
$apiVersion = "<ApiVersion>"
$managementGroupId = "<ManagementGroupId>"
$startTime = "<StartTime>"
$endTime = "<EndTime>"
$filter = "eventTimestamp ge '$startTime' and eventTimestamp le '$endTime'"
$encodedFilter = [uri]::EscapeDataString($filter)

# Build request URL
$apiEndpoint = "https://management.azure.com"
$path = "/providers/Microsoft.Management/managementGroups/$managementGroupId"
$provider = "Microsoft.Insights/eventtypes/management/values"
$queryString = "?api-version=$apiVersion&`$filter=$encodedFilter"
$url = "$apiEndpoint$path/providers/$provider$queryString"

# Define parameters for Invoke-AzRestMethod
$invokeAzRestMethodParams = @{
 Method = "GET"
 Uri = $url
}

# Send request
Invoke-AzRestMethod @invokeAzRestMethodParams
`

The following REST example uses the `Management group activity log query` REST API operation.

`GET https://management.azure.com/providers/Microsoft.Management/managementGroups/{managementGroupId}/providers/Microsoft.Insights/eventtypes/management/values?api-version={apiVersion}&$filter=eventTimestamp ge '{startTime}' and eventTimestamp le '{endTime}'
Authorization: Bearer {accessToken}
`

The following table describes the parameters used in the preceding examples.

Variable
Example value
Purpose

`apiEndpoint`
`https://management.azure.com`
ARM endpoint.

`subscriptionId`
Current subscription
REST URL scope; native commands use the current context.

`resourceGroupName`
`<ResourceGroupName>`
Resource group to query.

`managementGroupId`
`<ManagementGroupId>`
Management group to query.

`apiVersion`
`<ApiVersion>`
Version for the selected operation in the REST API index.

## View change history

For some events, you can view the change history, which shows what changes happened during that event time. Select an event from the activity log that you want to look at more deeply. Select the Change history tab to view any changes on the resource up to 30 minutes before and after the time of the operation.

If any changes are associated with the event, the portal shows you a selectable list of changes. Selecting a change opens the Change history page. This page displays the changes to the resource.

The following example shows that the VM changed sizes. The page displays the VM size before the change and after the change. To learn more about change history, see Get resource changes.

## Activity log insights

Activity log insights is an Azure Monitor workbook that provides a set of dashboards that monitor the changes to resources and resource groups in a subscription. The dashboards also present data about which users or services performed activities in the subscription and the activities' status.

To enable activity log insights, export the activity log to a Log Analytics workspace as described in Export activity log. This process sends events to the `AzureActivity` table, which activity log insights uses.

You can open activity log insights at the subscription or resource level. For the subscription, select Activity Logs Insights from the Workbooks section of the Monitor menu.

For an individual resource, select Activity Logs Insights from the Workbooks section of the resource's menu.

## Export activity log

Create a diagnostic setting to send activity log entries to other destinations for extra retention time and functionality.

In the Azure portal, select Activity log on the Azure Monitor menu and then select Export Activity Logs. For more information and other methods for creating diagnostic settings, see Diagnostic settings in Azure Monitor. Make sure you disable any legacy configuration for the activity log.

The following sections provide details on each configurable destination for resource logs.

Note

The legacy method of exporting the activity log is log profiles. See Legacy collection methods.

- 
Log Analytics workspace

- 
Azure Event Hubs

- 
Azure Storage

Send the activity log to a Log Analytics workspace for the following functionality:

- Correlate activity logs with other log data by using log queries.

- Create log alerts, which can use more complex logic than activity log alerts.

- Access activity log data with Power BI.

- Retain activity log data for longer than 90 days.

There are no data ingestion charges for activity logs. Retention charges for activity logs apply only to the period extended past the default retention period of 90 days. You can increase the retention period to up to 12 years.

Activity log data in a Log Analytics workspace is stored in a table called AzureActivity. The structure of this table varies depending on the category of the log entry.

For example, to view a count of activity log records for each category, use the following query:

`AzureActivity
| summarize count() by CategoryValue
`

To retrieve all records in the administrative category, use the following query:

`AzureActivity
| where CategoryValue == "Administrative"
`

Important

In some scenarios, values in fields of `AzureActivity` might have different case from otherwise equivalent values. When querying data in `AzureActivity`, use case-insensitive operators for string comparisons, or use a scalar function to force a field to a uniform casing before any comparisons. For example, use the tolower() function on a field to force it to always be lowercase or the =~ operator when performing a string comparison.

Send the activity log to Azure Event Hubs to send entries outside of Azure, for example, to a third-party SIEM or other log analysis solutions. Activity log events from event hubs are consumed in JSON format with a `records` element that contains the records in each payload. The schema depends on the category and is described in Azure activity log event schema.

The following sample output data is from event hubs for an activity log:

View activity log output from Event Hubs
`{
 "records": [
 {
 "time": "2019-01-21T22:14:26.9792776Z",
 "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
 "operationName": "microsoft.support/supporttickets/write",
 "category": "Write",
 "resultType": "Success",
 "resultSignature": "Succeeded.Created",
 "durationMs": 2826,
 "callerIpAddress": "192.0.2.1",
 "correlationId": "aaaa0000-bb11-2222-33cc-444444dddddd",
 "identity": {
 "authorization": {
 "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
 "action": "microsoft.support/supporttickets/write",
 "evidence": {
 "role": "Subscription Admin"
 }
 },
 "claims": {
 "aud": "https://management.core.windows.net/",
 "iss": "https://sts.windows.net/aaaabbbb-0000-cccc-1111-dddd2222eeee/",
 "iat": "1421876371",
 "nbf": "1421876371",
 "exp": "1421880271",
 "ver": "1.0",
 "http://schemas.microsoft.com/identity/claims/tenantid": "aaaabbbb-0000-cccc-1111-dddd2222eeee",
 "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
 "http://schemas.microsoft.com/identity/claims/objectidentifier": "aaaa0000-bb11-2222-33cc-444444dddddd",
 "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
 "puid": "1003BFFD8EC002D4",
 "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
 "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
 "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
 "name": "John Smith",
 "groups": "bbbb1111-cc22-3333-44dd-555555eeeeee,aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb,cccc2222-dd33-4444-55ee-666666ffffff",
 "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
 "appid": "00001111-aaaa-2222-bbbb-3333cccc4444",
 "appidacr": "2",
 "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
 "http://schemas.microsoft.com/claims/authnclassreference": "1"
 }
 },
 "level": "Information",
 "location": "global",
 "properties": {
 "statusCode": "Created",
 "serviceRequestId": "bbbbbbbb-1111-2222-3333-cccccccccccc"
 }
 }
 ]
}
`

Send the activity log to an Azure Storage account if you want to retain your log data longer than 90 days for audit, static analysis, or backup. If you need to retain your events for 90 days or less, you don't need to set up archival to a storage account.

When you send the activity log to storage, a storage container is created in the storage account as soon as an event occurs. The blobs in the container use the following naming convention:

`insights-activity-logs/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
`

For example, a particular blob might have a name similar to:

`insights-activity-logs/resourceId=/SUBSCRIPTIONS/a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1/y=2020/m=06/d=08/h=18/m=00/PT1H.json
`

Each `PT1H.json` blob contains a JSON object with events. The `y=`, `m=`, `d=`, and `h=` values in the blob path reflect the blob's original generation time, not the time the logs arrive in Azure Storage. All times are in UTC. These path segments identify blobs within the container, not separate containers. The minute value, `m=00`, is always `00` because Azure Monitor creates blobs hourly.

Each event is stored in the PT1H.json file with the following format. This format uses a common top-level schema but is otherwise unique for each category, as described in Activity log schema.

`{
 "time": "2020-06-12T13:07:46.766Z",
 "resourceId": "/SUBSCRIPTIONS/a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.COMPUTE/VIRTUALMACHINES/MV-VM-01",
 "correlationId": "bbbb1111-cc22-3333-44dd-555555eeeeee",
 "operationName": "Microsoft.Resourcehealth/healthevent/Updated/action",
 "level": "Information",
 "resultType": "Updated",
 "category": "ResourceHealth",
 "properties": {
 "eventCategory": "ResourceHealth",
 "eventProperties": {
 "title": "This virtual machine is starting as requested by an authorized user or process. It will be online shortly.",
 "details": "VirtualMachineStartInitiatedByControlPlane",
 "currentHealthStatus": "Unknown",
 "previousHealthStatus": "Unknown",
 "type": "Downtime",
 "cause": "UserInitiated"
 }
 }
}
`

## Export management group activity logs

When you create a diagnostic setting for a management group, it exports Azure Monitor activity log events for that management group and all management groups under it in the hierarchy. If multiple management groups in the hierarchy have diagnostic settings, you receive duplicate events. A diagnostic setting on the highest-level management group is sufficient for management group events, but it doesn't capture every subscription-level activity log event.

Azure Resource Manager includes a `hierarchy` property when writing activity log events, but the property isn't required. Resource providers outside Azure Resource Manager don't populate it. Subscription-level events without this property don't propagate to management-group diagnostic settings, including a setting on the root management group.

To capture events that don't propagate to the management group, create a subscription-level diagnostic setting for each subscription you need to monitor. Select all activity log categories if you need to export all subscription-level events.

If the subscription and management group export the same events to the same destination, you receive duplicate events. Keep the subscription-level diagnostic setting to avoid missing events without the `hierarchy` property.

For example, if MG1 contains MG2, which contains Subscription1, a diagnostic setting on MG1 captures activity log events for MG1, MG2, and many of the events collected by a diagnostic setting on Subscription1. Configure a diagnostic setting on Subscription1 to also capture events without the `hierarchy` property. You don't need a diagnostic setting on MG2 to collect the same management group events.

If you have duplicate events, combine them by using a query that uses a hash of all fields to identify unique records.

The following example Kusto query shows a sample for logs collected in a Log Analytics workspace:

`AzureActivity
| extend Hash = hash(dynamic_to_json(pack_all()))
| summarize arg_max(TimeGenerated, *) by Hash
`

## Export the activity log to a file

- 
Portal

- 
Azure CLI

- 
Azure PowerShell

Select Download as CSV to export the activity log to a CSV file in the Azure portal.

Important

Exporting a large number of log entries can take a long time. To improve performance, reduce the time range of the export. In the Azure portal, set the Timespan setting.

The following Azure CLI example uses the `az monitor activity-log list` command.

`# Set variables
startTime="<StartTime>"
endTime="<EndTime>"
maxItems=1000
outputFile="<OutputFilePath>"

# Retrieve activity log events
az monitor activity-log list \
 --start-time "$startTime" \
 --end-time "$endTime" \
 --max-items "$maxItems" \
 > "$outputFile"
`

Note

Azure CLI commands use the Azure Resource Manager endpoint from the current CLI context, so management.azure.com doesn't need to be specified in the command syntax.

The following Azure PowerShell example uses the `Get-AzActivityLog` cmdlet.

`# Set variables
$startTime = "<StartTime>"
$endTime = "<EndTime>"
$outputFile = "<OutputFilePath>"

# Define parameters for Get-AzActivityLog
$getAzActivityLogParams = @{
 StartTime = $startTime
 EndTime = $endTime
}

# Retrieve activity log events
Get-AzActivityLog @getAzActivityLogParams |
 Export-Csv -Path $outputFile -NoTypeInformation
`

The following example PowerShell script exports the activity log to CSV files in one-hour intervals, and saves each interval to a separate file.

`# Set variables
$startTime = [datetime]"<StartTime>"
$endTime = [datetime]"<EndTime>"
$outputFolder = "<OutputFolder>"

# Ensure output folder exists
if (-not (Test-Path $outputFolder)) {
 New-Item -Path $outputFolder -ItemType Directory
}

# Loop through 1-hour intervals
$currentStart = $startTime
while ($currentStart -lt $endTime) {
 $currentEnd = $currentStart.AddHours(1)
 if ($currentEnd -gt $endTime) { $currentEnd = $endTime }
 $timestamp = $currentStart.ToString("yyyyMMdd-HHmm")
 $csvFile = Join-Path $outputFolder "ActivityLog_$timestamp.csv"

 # Define parameters for Get-AzActivityLog
 $getAzActivityLogParams = @{
 StartTime = $currentStart
 EndTime = $currentEnd
 ErrorAction = "Stop"
 }

 Write-Host "Fetching logs from $currentStart to $currentEnd..."
 Get-AzActivityLog @getAzActivityLogParams |
 Export-Csv -Path $csvFile -NoTypeInformation

 $currentStart = $currentEnd
}

Write-Host "Export completed. Files saved to $outputFolder."
`

Note

Azure PowerShell cmdlets use the Azure Resource Manager endpoint from the current Az context, so management.azure.com doesnât need to be specified in the cmdlet syntax.

## Identify resource creation

Use the activity log to find out when the system created a resource and who created it. The activity log is the only place that stores the creator of a resource. Because the activity log only retains data for 90 days by default, you must export the logs to a location that allows you to extend the retention period, like a Log Analytics workspace. Then find the creator of a resource by querying the `AzureActivity` table. The data is retained for the duration you specified in the retention period for this table.

## Related content

- Activity log event schema

- Resource logs

- Diagnostic settings

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-03
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
