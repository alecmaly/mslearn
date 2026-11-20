# https://learn.microsoft.com/en-us/azure/azure-monitor/alerts/alerts-create-activity-log-alert-rule

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/alerts/alerts-create-activity-log-alert-rule

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
 

 

 

 

 
 
# Create or edit an activity log, service health, or resource health alert rule

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This article shows you how to create or edit an activity log, service health, or resource health alert rule in Azure Monitor. To learn more about alerts, see the alerts overview.

You create an alert rule by combining the resources to be monitored, the monitoring data from the resource, and the conditions that you want to trigger the alert. You can then define action groups and alert processing rules to determine what happens when an alert is triggered.

Alerts triggered by these alert rules contain a payload that uses the common alert schema.

## Prerequisites

To create or edit an alert rule, you must have the following permissions:

- Read permission on the target resource of the alert rule.

- Write permission on the resource group in which the alert rule is created. If you're creating the alert rule from the Azure portal, the alert rule is created by default in the same resource group in which the target resource resides.

- Read permission on any action group associated to the alert rule, if applicable.

## Access the alert rule wizard in the Azure portal

There are multiple ways to create or edit an alert rule.

### Create or edit an alert rule from the portal home page

- In the Azure portal, select Monitor.

- On the left pane, select Alerts.

- Select + Create > Alert rule.

### Create or edit an alert rule from a specific resource

- In the Azure portal, go to the resource.

- On the left pane, select Alerts.

- Select + Create > Alert rule.

- The scope of the alert rule is set to the resource you selected. Continue with setting the conditions for the alert rule.

### Edit an existing alert rule

- In the Azure portal, either from the home page or from a specific resource, select Alerts on the left pane.

- Select Alert rules.

- Select the alert rule you want to edit, and then select Edit.

- Select any of the tabs for the alert rule to edit the settings.

## Configure the scope of the alert rule

- On the Select a resource pane, set the scope for your alert rule. You can filter by subscription, resource type, or resource location.

- Select Apply.

## Configure alert rule conditions

- On the Condition tab, select Activity log, Resource health, or Service health. Or select See all signals if you want to choose a different signal for the condition.

- (Optional) If you selected See all signals in the previous step, use the Select a signal pane to search for the signal name or filter the list of signals. Filter by:

- Signal type: The type of alert rule that you're creating.

- Signal source: The service that sends the signal.

This table describes the available services for activity log alert rules:

Signal source
Description

Activity log â Policy
The service that provides the policy-related activity log events.

Activity log â Autoscale
The service that provides the autoscale-related activity log events.

Activity log â Security
The service that provides the security-related activity log events.

Resource health
The service that provides the resource-level health status.

Service health
The service that provides the subscription-level health status.

Select the signal name, and then select Apply.

- 
Activity log alert

- 
Resource health alert

- 
Service health alert

- On the Conditions pane, select the Chart period value.

The Preview chart shows the results of your selection.

- In the Alert logic section, select values for each of these fields:

Field
Description

Event level
Select the level of the events for this alert rule. Values are Critical, Error, Warning, Informational, Verbose, and All.

Status
Select the status levels for the alert.

Event initiated by
Select the user principal or service principal that initiated the event.

- On the Conditions pane, select values for each of these fields:

Field
Description

Event status
Select the statuses of resource health events. Values are Active, In Progress, Resolved, and Updated.

Current resource status
Select the current resource status. Values are Available, Degraded, and Unavailable.

Previous resource status
Select the previous resource status. Values are Available, Degraded, Unavailable, and Unknown.

Reason type
Select the causes of the resource health events. Values are Platform Initiated, Unknown, and User Initiated.

- On the Conditions pane, select values for each of these fields:

Field
Description

Services
Select the Azure services.

Regions
Select the Azure regions.

Event types
Select the types of service health events. Values are Service issue, Planned maintenance, Health advisories, and Security advisories.

## Configure alert rule actions

On the Actions tab, you can optionally select or create action groups for your alert rule.

You can optionally set a custom email subject for notifications. For more information, see Customize log search alert email subjects.

## Configure alert rule details

- On the Details tab, enter values for Alert rule name and Alert rule description.

- Select Enable alert rule upon creation for the alert rule to start running as soon as you finish creating it.

- (Optional) For Region, select a region in which your alert rule will be processed. If you need to make sure the rule is processed within the EU Data Boundary, select the North Europe or West Europe region. In all other cases, you can select the Global region (which is the default).

Note

Service Health alert rules can only be located in the Global region.

- 
(Optional) In the Custom properties section, if this alert rule contains action groups, you can add your own properties to include in the alert notification payload. You can use these properties in the actions that the action group calls, such as by a webhook, Azure function, or logic app action.

The custom properties are specified as key/value pairs by using static text, a dynamic value extracted from the alert payload, or a combination of both.

The format for extracting a dynamic value from the alert payload is: `${<path to schema field>}`. For example: `${data.essentials.monitorCondition}`.

Use the format of the common alert schema to specify the field in the payload, whether or not the action groups configured for the alert rule use the common schema.

Note

Add custom properties to the JSON payload that's sent to webhook, Logic Apps, Azure Functions, and Automation runbook actions. They aren't included in email, SMS, or push notifications, and they don't appear in the alert details page in the Azure portal.

The following examples use values in Custom properties to utilize data from a payload that uses the common alert schema.

This example creates an Additional Details tag with data regarding the window start time and window end time:

- Name: `Additional Details`

- Value: `Evaluation windowStartTime: ${data.alertContext.condition.windowStartTime}. windowEndTime: ${data.alertContext.condition.windowEndTime}`

- Result: `AdditionalDetails:Evaluation windowStartTime: 2023-04-04T14:39:24.492Z. windowEndTime: 2023-04-04T14:44:24.492Z`

This example adds data regarding the reason for resolving or firing the alert:

- Name: `Alert ${data.essentials.monitorCondition} reason`

- Value: `${data.alertContext.condition.allOf[0].metricName} ${data.alertContext.condition.allOf[0].operator} ${data.alertContext.condition.allOf[0].threshold} ${data.essentials.monitorCondition}. The value is ${data.alertContext.condition.allOf[0].metricValue}`

- Potential results:

- `Alert Resolved reason: Percentage CPU GreaterThan5 Resolved. The value is 3.585`

- `Alert Fired reason": "Percentage CPU GreaterThan5 Fired. The value is 10.585`

## Configure alert rule tags

On the Tags tab, you can optionally set any required tags on the alert rule resource.

## Review and create the alert rule

- On the Review + create tab, the rule is validated. If there's a problem, go back and fix it.

- When validation passes and you've reviewed the settings, select the Create button.

## Related content

- View and manage your alert instances.

 
 

 
 

 

 
 
 
 
 
 
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
 2025-07-09
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
