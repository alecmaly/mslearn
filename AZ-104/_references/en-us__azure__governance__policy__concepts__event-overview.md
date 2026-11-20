# https://learn.microsoft.com/en-us/azure/governance/policy/concepts/event-overview

Source: https://learn.microsoft.com/en-us/azure/governance/policy/concepts/event-overview

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
 

 

 

 

 
 
# Reacting to Azure Policy state change events

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Policy events enable applications to react to state changes. This integration is done without the need for complicated code or expensive and inefficient polling services. Instead, events are pushed through Azure Event Grid to subscribers such as Azure Functions, Azure Logic Apps, or even to your own custom HTTP listener. Critically, you only pay for what you use.

Azure Policy events are sent to the Azure Event Grid, which provides reliable delivery services to your applications through rich retry policies and dead-letter delivery. Event Grid takes care of the proper routing, filtering, and multicasting of the events to destinations via Event Grid subscriptions. To learn more, see Event Grid message delivery and retry.

Note

Azure Policy state change events are sent to Event Grid after an
evaluation trigger finishes resource
evaluation.

Event Grid notifications for resource compliance state changes can take up to 20 minutes.

## Event Grid Benefits

Event Grid has a few benefits for customers and services in the Azure ecosystem:

- Automation: To stay current with your policy environment, Event Grid offers an automated mechanism to generate alerts and trigger tasks depending on compliance states.

- Durable delivery: In order for services and user applications to respond in real-time to policy compliance events, Event Grid seeks to offer policy events with minimum latency. Event Grid retries transmission of an event if a subscriber's endpoint fails to acknowledge receipt of it or if it doesn't, according to a predetermined retry schedule and retry policy.

- Custom event producer: Event Grid event producers and consumers don't need to be Azure or Microsoft services. External applications can receive an alert, show the creation of a remediation task or collect messages on who responds to the state change. See Route policy state change events to Event Grid with Azure CLI for a full tutorial.

There are two primary entities when using Event Grid:

- Events: These events can be anything a user might want to react to for an Azure resource. For example, if a policy compliance state is created, changed, and deleted for a resource such as a virtual machine or storage accounts.

- Event Grid Subscriptions: These event subscriptions are user configured entities that direct the proper set of events from a publisher to a subscriber. Event subscriptions can filter events based on the resource path the event originated from and the type of event. Additionally, Event Subscriptions can also filter by scope between Azure subscription and Management group.

A common Azure Policy event scenario is tracking when the compliance state of a resource changes during policy evaluation. Event-based architecture is an efficient way to react to these changes and aids in the event based reaction to compliance state changes.

Another scenario is to automatically trigger remediation tasks without manually selecting create remediation task on the policy page. Event Grid checks for compliance state and resources that are currently noncompliant can be remedied. Learn more about remediation structure. Remediation requires a managed identity and policies must be in `modify` or `deployIfNotExists` effect. Learn more about effect types.

Event Grid is helpful as an audit system to store state changes and understand cause of noncompliance over time. The scenarios for Event Grid are endless and based on the motivation, Event Grid is configurable.

## Available event types

Azure Policy emits the following event types:

Event type
Description

Microsoft.PolicyInsights.PolicyStateCreated
Raised when a policy compliance state is created.

Microsoft.PolicyInsights.PolicyStateChanged
Raised when a policy compliance state is changed.

Microsoft.PolicyInsights.PolicyStateDeleted
Raised when a policy compliance state is deleted.

## Event properties

- 
Event Grid event schema

- 
Cloud event schema

An event has the following top-level data:

Property
Type
Description

`topic`
string
Full resource path to the event source. This field isn't writeable. Event Grid provides this value.

`subject`
string
The fully qualified ID of the resource that the compliance state change is for, including the resource name and resource type. Uses the format, `/subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroup>/providers/<ProviderNamespace>/<ResourceType>/<ResourceName>`

`eventType`
string
One of the registered event types for this event source.

`eventTime`
string
The time the event is generated based on the provider's UTC time.

`id`
string
Unique identifier for the event.

`data`
object
Azure Policy event data.

`dataVersion`
string
The schema version of the data object. The publisher defines the schema version.

`metadataVersion`
string
The schema version of the event metadata. Event Grid defines the schema of the top-level properties. Event Grid provides this value.

An event has the following top-level data:

Property
Type
Description

`source`
string
Full resource path to the event source. This field isn't writeable. Event Grid provides this value.

`subject`
string
The fully qualified ID of the resource that the compliance state change is for, including the resource name and resource type. Uses the format, `/subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroup>/providers/<ProviderNamespace>/<ResourceType>/<ResourceName>`

`type`
string
One of the registered event types for this event source.

`time`
string
The time the event is generated based on the provider's UTC time.

`id`
string
Unique identifier for the event.

`data`
object
Azure Policy event data.

`specversion`
string
CloudEvents schema specification version.

The data object has the following properties:

Property
Type
Description

`timestamp`
string
The time (in UTC) that the resource was scanned by Azure Policy. For ordering events, use this property instead of the top-level `eventTime` or `time` properties.

`policyAssignmentId`
string
The resource ID of the policy assignment.

`policyDefinitionId`
string
The resource ID of the policy definition.

`policyDefinitionReferenceId`
string
The reference ID for the policy definition inside the initiative definition, if the policy assignment is for an initiative. May be empty.

`complianceState`
string
The compliance state of the resource with respect to the policy assignment.

`subscriptionId`
string
The subscription ID of the resource.

`complianceReasonCode`
string
The compliance reason code. May be empty.

## Example event

- 
Event Grid event schema

- 
Cloud event schema

The following example shows the schema of a policy state created event scoped at the subscription level:

`[{
 "id": "5829794FCB5075FCF585476619577B5A5A30E52C84842CBD4E2AD73996714C4C",
 "topic": "/subscriptions/<SubscriptionID>",
 "subject": "/subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroup>/providers/<ProviderNamespace>/<ResourceType>/<ResourceName>",
 "data": {
 "timestamp": "2021-03-27T18:37:42.4496956Z",
 "policyAssignmentId": "<policy-assignment-scope>/providers/microsoft.authorization/policyassignments/<policy-assignment-name>",
 "policyDefinitionId": "<policy-definition-scope>/providers/microsoft.authorization/policydefinitions/<policy-definition-name>",
 "policyDefinitionReferenceId": "",
 "complianceState": "NonCompliant",
 "subscriptionId": "<subscription-id>",
 "complianceReasonCode": ""
 },
 "eventType": "Microsoft.PolicyInsights.PolicyStateCreated",
 "eventTime": "2021-03-27T18:37:42.5241536Z",
 "dataVersion": "1",
 "metadataVersion": "1"
}]
`

The schema for a policy state changed event scoped at the subscription level is similar:

`[{
 "id": "5829794FCB5075FCF585476619577B5A5A30E52C84842CBD4E2AD73996714C4C",
 "topic": "/subscriptions/<SubscriptionID>",
 "subject": "/subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroup>/providers/<ProviderNamespace>/<ResourceType>/<ResourceName>",
 "data": {
 "timestamp": "2021-03-27T18:37:42.4496956Z",
 "policyAssignmentId": "<policy-assignment-scope>/providers/microsoft.authorization/policyassignments/<policy-assignment-name>",
 "policyDefinitionId": "<policy-definition-scope>/providers/microsoft.authorization/policydefinitions/<policy-definition-name>",
 "policyDefinitionReferenceId": "",
 "complianceState": "NonCompliant",
 "subscriptionId": "<subscription-id>",
 "complianceReasonCode": ""
 },
 "eventType": "Microsoft.PolicyInsights.PolicyStateChanged",
 "eventTime": "2021-03-27T18:37:42.5241536Z",
 "dataVersion": "1",
 "metadataVersion": "1"
}]
`

The following example shows the schema of a policy state created event scoped at the subscription level:

`[{
 "id": "5829794FCB5075FCF585476619577B5A5A30E52C84842CBD4E2AD73996714C4C",
 "source": "/subscriptions/<SubscriptionID>",
 "subject": "/subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroup>/providers/<ProviderNamespace>/<ResourceType>/<ResourceName>",
 "data": {
 "timestamp": "2021-03-27T18:37:42.4496956Z",
 "policyAssignmentId": "<policy-assignment-scope>/providers/microsoft.authorization/policyassignments/<policy-assignment-name>",
 "policyDefinitionId": "<policy-definition-scope>/providers/microsoft.authorization/policydefinitions/<policy-definition-name>",
 "policyDefinitionReferenceId": "",
 "complianceState": "NonCompliant",
 "subscriptionId": "<subscription-id>",
 "complianceReasonCode": ""
 },
 "type": "Microsoft.PolicyInsights.PolicyStateCreated",
 "time": "2021-03-27T18:37:42.5241536Z",
 "specversion": "1.0"
}]
`

The schema for a policy state changed event scoped at the subscription level is similar:

`[{
 "id": "5829794FCB5075FCF585476619577B5A5A30E52C84842CBD4E2AD73996714C4C",
 "source": "/subscriptions/<SubscriptionID>",
 "subject": "/subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroup>/providers/<ProviderNamespace>/<ResourceType>/<ResourceName>",
 "data": {
 "timestamp": "2021-03-27T18:37:42.4496956Z",
 "policyAssignmentId": "<policy-assignment-scope>/providers/microsoft.authorization/policyassignments/<policy-assignment-name>",
 "policyDefinitionId": "<policy-definition-scope>/providers/microsoft.authorization/policydefinitions/<policy-definition-name>",
 "policyDefinitionReferenceId": "",
 "complianceState": "NonCompliant",
 "subscriptionId": "<subscription-id>",
 "complianceReasonCode": ""
 },
 "type": "Microsoft.PolicyInsights.PolicyStateChanged",
 "time": "2021-03-27T18:37:42.5241536Z",
 "specversion": "1.0"
}]
`

- 
Event Grid event schema

- 
Cloud event schema

The following example shows the schema of a policy state created event scoped at the management group level:

`[{
 "id": "5829794FCB5075FCF585476619577B5A5A30E52C84842CBD4E2AD73996714C4C",
 "topic": "/tenants/<tenantId>/providers/Microsoft.Management/managementGroups/<managementGroupId>",
 "subject": "/subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroup>/providers/<ProviderNamespace>/<ResourceType>/<ResourceName>",
 "data": {
 "timestamp": "2021-03-27T18:37:42.4496956Z",
 "policyAssignmentId": "<policy-assignment-scope>/providers/microsoft.authorization/policyassignments/<policy-assignment-name>",
 "policyDefinitionId": "<policy-definition-scope>/providers/microsoft.authorization/policydefinitions/<policy-definition-name>",
 "policyDefinitionReferenceId": "",
 "complianceState": "NonCompliant",
 "subscriptionId": "<subscription-id>",
 "complianceReasonCode": ""
 },
 "eventType": "Microsoft.PolicyInsights.PolicyStateCreated",
 "eventTime": "2021-03-27T18:37:42.5241536Z",
 "dataVersion": "1",
 "metadataVersion": "1"
}]
`

The schema for a policy state changed event scoped at the management group level is similar:

`[{
 "id": "5829794FCB5075FCF585476619577B5A5A30E52C84842CBD4E2AD73996714C4C",
 "topic": "/tenants/<tenantId>/providers/Microsoft.Management/managementGroups/<managementGroupId>",
 "subject": "/subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroup>/providers/<ProviderNamespace>/<ResourceType>/<ResourceName>",
 "data": {
 "timestamp": "2021-03-27T18:37:42.4496956Z",
 "policyAssignmentId": "<policy-assignment-scope>/providers/microsoft.authorization/policyassignments/<policy-assignment-name>",
 "policyDefinitionId": "<policy-definition-scope>/providers/microsoft.authorization/policydefinitions/<policy-definition-name>",
 "policyDefinitionReferenceId": "",
 "complianceState": "NonCompliant",
 "subscriptionId": "<subscription-id>",
 "complianceReasonCode": ""
 },
 "eventType": "Microsoft.PolicyInsights.PolicyStateChanged",
 "eventTime": "2021-03-27T18:37:42.5241536Z",
 "dataVersion": "1",
 "metadataVersion": "1"
}]
`

The following example shows the schema of a policy state created event scoped at the management group level:

`[{
 "id": "5829794FCB5075FCF585476619577B5A5A30E52C84842CBD4E2AD73996714C4C",
 "source": "/tenants/<tenantId>/providers/Microsoft.Management/managementGroups/<managementGroupId>",
 "subject": "/subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroup>/providers/<ProviderNamespace>/<ResourceType>/<ResourceName>",
 "data": {
 "timestamp": "2021-03-27T18:37:42.4496956Z",
 "policyAssignmentId": "<policy-assignment-scope>/providers/microsoft.authorization/policyassignments/<policy-assignment-name>",
 "policyDefinitionId": "<policy-definition-scope>/providers/microsoft.authorization/policydefinitions/<policy-definition-name>",
 "policyDefinitionReferenceId": "",
 "complianceState": "NonCompliant",
 "subscriptionId": "<subscription-id>",
 "complianceReasonCode": ""
 },
 "type": "Microsoft.PolicyInsights.PolicyStateCreated",
 "time": "2021-03-27T18:37:42.5241536Z",
 "specversion": "1.0"
}]
`

The schema for a policy state changed event scoped at the management group level is similar:

`[{
 "id": "5829794FCB5075FCF585476619577B5A5A30E52C84842CBD4E2AD73996714C4C",
 "source": "/tenants/<tenantId>/providers/Microsoft.Management/managementGroups/<managementGroupId>",
 "subject": "/subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroup>/providers/<ProviderNamespace>/<ResourceType>/<ResourceName>",
 "data": {
 "timestamp": "2021-03-27T18:37:42.4496956Z",
 "policyAssignmentId": "<policy-assignment-scope>/providers/microsoft.authorization/policyassignments/<policy-assignment-name>",
 "policyDefinitionId": "<policy-definition-scope>/providers/microsoft.authorization/policydefinitions/<policy-definition-name>",
 "policyDefinitionReferenceId": "",
 "complianceState": "NonCompliant",
 "subscriptionId": "<subscription-id>",
 "complianceReasonCode": ""
 },
 "type": "Microsoft.PolicyInsights.PolicyStateChanged",
 "time": "2021-03-27T18:37:42.5241536Z",
 "specversion": "1.0"
}]
`

## Practices for consuming events

Applications that handle Azure Policy events should follow these recommended practices:

- Multiple subscriptions can be configured to route events to the same event handler, so don't
assume events are from a particular source. Instead, check the topic of the message to ensure the
policy assignment, policy definition, and resource the state change event is for.

- Check the `eventType` and don't assume that all events you receive are the types you expect.

- Use `data.timestamp` to determine the order of the events in Azure Policy, instead of the
top-level `eventTime` or `time` properties.

- Use the subject field to access the resource that had a policy state change.

## Next steps

Learn more about Event Grid and give Azure Policy state change events a try:

- Route policy state change events to Event Grid with Azure CLI

- Azure Policy schema details for Event Grid

- About Event Grid

 
 

 
 

 

 
 
 
 
 
 
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
 2025-03-04
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
