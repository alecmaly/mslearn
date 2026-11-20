# https://learn.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview

Source: https://learn.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview

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
 

 

 

 

 
 
# Introduction to Application Insights - OpenTelemetry observability

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Monitor Application Insights is an application performance monitoring (APM) feature of Azure Monitor. For supported scenarios, you can use OpenTelemetry (OTel), a vendor-neutral observability framework, to instrument your applications and collect telemetry data, then analyze that telemetry in Application Insights.

## Application Insights Experiences

Application Insights supports OpenTelemetry (OTel) to collect telemetry data in a standardized format across platforms. Integration with Azure services allows for efficient monitoring and diagnostics, improving application observability and performance.

### Investigate

Use these tools to diagnose issues and understand your application's runtime behavior.

- Application dashboard: An at-a-glance assessment of your application's health and performance.

- Application map: A visual overview of application architecture and components' interactions.

- Live metrics: A real-time analytics dashboard for insight into application activity and performance.

- Search view: Trace and diagnose transactions to identify issues and optimize performance.

- Availability view: Proactively monitor and test the availability and responsiveness of application endpoints.

- Failures view: Identify and analyze failures in your application to minimize downtime.

- Performance view: Review application performance metrics and potential bottlenecks.

- Agents details: A unified view for monitoring AI agents across Microsoft Foundry, Copilot Studio, and third-party agents.

### Monitoring

Use these tools to continuously track your application's health and set up proactive notifications.

- Alerts: Monitor a wide range of aspects of your application and trigger various actions.

- Metrics: Dive deep into metrics data to understand usage patterns and trends.

- Diagnostic settings: Configure streaming export of platform logs and metrics to the destination of your choice.

- Logs: Retrieve, consolidate, and analyze all data collected into Azure Monitoring Logs.

- Workbooks: Create interactive reports and dashboards that visualize application monitoring data.

- Dashboards with Grafana: Create, customize, and share Grafana dashboards for Application Insights data directly in the Azure portal.

- SDK Stats: Visualize exporter success, dropped counts, retry counts, and drop reasons from Application Insights SDKs and agents.

### Usage

Use these tools to understand how users interact with your application.

- Users, sessions, and events: Determine when, where, and how users interact with your web app.

- Funnels: Analyze conversion rates to identify where users progress or drop off in the funnel.

- Flows: Visualize user paths on your site to identify high engagement areas and exit points.

- Cohorts: Group users by shared characteristics to simplify trend identification, segmentation, and performance troubleshooting.

### Code analysis

Use these tools to profile and debug your application code.

- .NET Profiler: Capture, identify, and view performance traces for your application.

- Code optimizations: Harness AI to create better and more efficient applications.

- Snapshot debugger: Automatically collect debug snapshots when exceptions occur in .NET application

## Logic model

The logic model diagram visualizes components of Application Insights and how they interact.

Note

Firewall settings must be adjusted for data to reach ingestion endpoints. For more information, see Azure Monitor endpoint access and firewall configuration.

## Getting started

This section covers getting started with OpenTelemetry-based data collection in Azure Monitor Application Insights.

Entry points include:

- Server-side web apps

- Server-side web apps hosted on a Virtual Machine (VM)

- Client-side JavaScript apps

- Azure Functions

- AI Agents

Tip

- For most code-based server-side scenarios, use the Microsoft OpenTelemetry Distro for .NET, Node.js, and Python, or the Azure Monitor OpenTelemetry Distro for Java.

- Scenarios where OpenTelemetry isn't available are clearly identified.

Choose the tab that best matches your workload or hosting model. Each tab shows the recommended data-collection path for that scenario.

### Set up data collection

- 
Web apps

- 
VM

- 
JavaScript

- 
Functions

- 
Kubernetes

- 
Agents

Use this path for server-side web apps that you instrument in code.

- Create an Application Insights resource.

- Get the resource's connection string.

- For .NET, Node.js, and Python, add the Microsoft OpenTelemetry Distro to your app. For Java, use the Azure Monitor OpenTelemetry Distro.

- Configure the connection string.

Tip

Some platforms enable data collection automatically through automatic instrumentation. Switch to code-based instrumentation with the Microsoft OpenTelemetry Distro for .NET, Node.js, and Python, or the Azure Monitor OpenTelemetry Distro for Java, if you want more configuration and extensibility options.

Use this path when your app runs on a virtual machine or virtual machine scale set. The code-based flow is the same as for other server-side apps.

- Create an Application Insights resource.

- Get the resource's connection string.

- For .NET, Node.js, and Python, add the Microsoft OpenTelemetry Distro to your app. For Java, use the Azure Monitor OpenTelemetry Distro.

- Configure the connection string.

Tip

Some platforms enable data collection automatically through automatic instrumentation. Switch to code-based instrumentation with the Microsoft OpenTelemetry Distro for .NET, Node.js, and Python, or the Azure Monitor OpenTelemetry Distro for Java, if you want more configuration and extensibility options.

Use this path for browser telemetry such as page views and user interactions. Browser apps use the Application Insights JavaScript SDK, not OpenTelemetry.

- Create an Application Insights resource.

- Get the resource's connection string.

- Add the JavaScript SDK to your app.

- Configure the connection string.

Note

The Application Insights JavaScript SDK doesn't use OpenTelemetry. For more information, see Can OpenTelemetry be used for web browsers?

Use this path for Azure Functions. Start with the function app settings, and then follow the Functions article for the language-specific steps.

- Enable OpenTelemetry in your function app's `host.json` file by setting `"telemetryMode": "OpenTelemetry"`.

- Add the `APPLICATIONINSIGHTS_CONNECTION_STRING` application setting by using your Application Insights connection string.

- Complete the language-specific instrumentation and any required worker settings in Use OpenTelemetry with Azure Functions.

Note

OpenTelemetry isn't currently supported for C# in-process apps.

Use this path for apps running on Azure Kubernetes Service (AKS). The code-based flow is the same as for other server-side apps.

- Create an Application Insights resource.

- Get the resource's connection string.

- For .NET, Node.js, and Python, add the Microsoft OpenTelemetry Distro to your app. For Java, use the Azure Monitor OpenTelemetry Distro.

- Configure the connection string.

Note

Automatic instrumentation for Azure Kubernetes Service (AKS) is available as a public preview.

Use this path for AI agents. Choose the setup that matches your hosting model.

- Managed hosting

- Azure AI Foundry: For Foundry-managed agents and workflows, start with tracing setup in Foundry. For app-side instrumentation, you can also use the Microsoft OpenTelemetry Distro with the Foundry SDK.

- Self-hosting

- Microsoft Agent Framework: If you're building an agent from scratch and self-hosting, use the Microsoft Agent Framework to orchestrate your agent and emit telemetry to Azure Monitor.

- Third-party agents: If you built an agent elsewhere, use the Azure AI OpenTelemetry Tracer to emit telemetry to Azure Monitor. These agents can also be registered in Azure AI Foundry. For framework-specific guidance, see Enable tracing for agents built on LangChain & LangGraph and Enable tracing for agents built on OpenAI Agents SDK.

After telemetry is flowing, you're ready to explore the Application Insights agent details view.

If you choose to collect full prompt information, for example by using the `EnableSensitiveData` flag in Agent Framework, you can search through prompts in the Search view and review conversations, including assistant messages, system prompts, and tool usage, in the Transaction Details view.

Give each agent a distinct name so you can tell them apart in the Agent details view. If your agentic components are part of a larger application, consider sending them to an existing Application Insights resource.

If you also want to see your agents in Azure AI Foundry in addition to Azure Monitor, connect an Application Insights resource to your Foundry project.

You can also set up evaluations in these ways:

- Batch evaluations

- Local evaluations with Azure AI Evaluation SDK: Run evaluations on your development machine during testing.

- Cloud evaluations with the Foundry SDK: Execute evaluations in Azure for larger datasets or team collaboration.

- Foundry portal-based evaluations: Use the Foundry portal for no-code evaluation workflows.

- Continuous evaluations: Set up automated evaluations that run against production traffic to detect quality regressions.

After you complete the setup for your scenario, run your app and wait a few minutes for telemetry to appear in Application Insights. Then explore Application Insights experiences.

Important

If you're migrating from older Application Insights SDKs, see Migrate to Azure Monitor OpenTelemetry.

## Other OpenTelemetry integrations on Azure

Azure Monitor Application Insights integrates with other Azure services that use OpenTelemetry. Use the following resources for Azure services, software development kits (SDKs), and tools that use OpenTelemetry:

Integration
Description

Azure SDK semantic conventions
OpenTelemetry attribute naming conventions used across all Azure SDKs.

Java tracing in the Azure SDK
Distributed tracing support for Azure SDK for Java clients.

Azure Cosmos DB SDK observability
OpenTelemetry traces and metrics emitted by the Azure Cosmos DB SDK.

.NET observability with OpenTelemetry
OpenTelemetry instrumentation guidance for .NET applications.

Azure Monitor pipeline at edge and multicloud
Collect and forward OpenTelemetry data from edge and multicloud environments to Azure Monitor.

OpenTelemetry ingestion into Azure Data Explorer
Ingest OpenTelemetry data into Azure Data Explorer, Synapse Data Explorer, and Real-Time Intelligence.

Azure Container Apps OpenTelemetry agent
Built-in OpenTelemetry agent for Azure Container Apps.

Aspire dashboard
Local development dashboard for viewing OpenTelemetry traces and metrics from .NET Aspire apps.

## Troubleshooting

For assistance with troubleshooting Application Insights, see our dedicated troubleshooting documentation.

## Help and support

### Azure technical support

For Azure support issues, open an Azure support ticket.

### General Questions

Post general questions to the Microsoft Questions and Answers forum.

### Coding Questions

Post coding questions to Stack Overflow by using an `azure-application-insights` tag.

### Feedback Community

Leave product feedback for the engineering team in the Feedback Community.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-10-09
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
