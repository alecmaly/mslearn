# https://learn.microsoft.com/en-us/azure/azure-functions/functions-best-practices

Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-best-practices

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
 

 

 

 

 
 
# Best practices for reliable Azure Functions

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Functions is an event-driven, compute-on-demand service that extends the existing Azure App Service application platform. It adds capabilities to implement code triggered by events occurring in Azure, in a partner service, and in on-premises systems. By using Functions, you can build solutions that connect to data sources or messaging solutions, which makes it easier to process and react to events. Functions runs in Azure data centers, which are complex with many integrated components. In a hosted cloud environment, it's expected that VMs can occasionally restart or move, and systems upgrades occur. Your function apps also likely depend on external APIs, Azure Services, and other databases, which are also prone to periodic unreliability.

This article details some best practices for designing and deploying efficient function apps that remain healthy and perform well in a cloud-based environment.

## Choose the correct hosting plan

When you create a function app in Azure, you must choose a hosting plan for your app. The plan you choose affects performance, reliability, and cost. Azure Functions provides the following hosting plans:

- Flex Consumption plan

- Premium plan

- Dedicated (App Service) plan

- Consumption plan

When possible, use the Flex Consumption plan to host your dynamic scale apps.

In the context of the App Service platform, the Premium plan that dynamically hosts your functions is the Elastic Premium plan (EP). Other Dedicated (App Service) plans are called Premium. For more information, see Azure Functions Premium plan.

The hosting plan you choose determines the following behaviors:

- How your function app scales based on demand and how instance allocation is managed.

- The resources available to each function app instance.

- Support for advanced functionality, such as Azure Virtual Network connectivity.

For more information about choosing the correct hosting plan and a detailed comparison between the plans, see Azure Functions hosting options.

Choose the correct plan when you create your function app. Functions provides a limited ability to switch your hosting plan, primarily between Consumption and Elastic Premium plans. For more information, see Plan migration.

## Configure storage correctly

Functions requires a storage account be associated with your function app. The Functions host uses the storage account connection for operations such as managing triggers and logging function executions. It's also used when dynamically scaling function apps. For more information, see Storage considerations for Azure Functions.

A misconfigured file system or storage account in your function app can affect the performance and availability of your functions. For help with troubleshooting an incorrectly configured storage account, see the storage troubleshooting article.

### Storage connection settings

Function apps that scale dynamically can run either from an Azure Files endpoint in your storage account or from the file servers associated with your scaled-out instances. This behavior is controlled by the following application settings:

- WEBSITE_CONTENTAZUREFILECONNECTIONSTRING

- WEBSITE_CONTENTSHARE

The Premium plan and the Consumption plan on Windows support these settings. The Flex Consumption plan doesn't require these settings. Flex code-package apps use a Blob storage container to host deployment packages instead of an Azure Files share, while apps that use a container image store the application and its dependencies in the image.

When you create your function app in the Azure portal or by using Azure CLI or Azure PowerShell, you create these settings for your function app when needed. When you create your resources from an Azure Resource Manager template (ARM template), you need to also include `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` in the template.

On your first deployment using an ARM template, don't include `WEBSITE_CONTENTSHARE`, which is generated for you.

You can use the following ARM template examples to help correctly configure these settings:

- Consumption plan

- Dedicated plan

- Premium plan with VNET integration

- Consumption plan with a deployment slot

Important

The Azure Files service doesn't currently support identity-based connections. The Flex Consumption plan fully supports managed identities. For more information, see Create an app without Azure Files.

### Storage account configuration

When creating a function app, you must create or link to a general-purpose Azure Storage account that supports Blob, Queue, and Table storage. Functions relies on Azure Storage for operations such as managing triggers and logging function executions. The storage account connection string for your function app is found in the `AzureWebJobsStorage` and `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` application settings.

Keep in mind the following considerations when creating this storage account:

- To reduce latency, create the storage account in the same region as the function app.

- To improve performance in production, use a separate storage account for each function app. This aspect is especially true with Durable Functions and Event Hubs triggered functions.

- For Event Hubs triggered functions, don't use an account with Data Lake Storage enabled.

### Handling large data sets

When running on Linux, you can add extra storage by mounting a file share. Mounting a share is a convenient way for a function to process a large existing data set. For more information, see Mount file shares.

## Organize your functions

As part of your solution, you likely develop and publish multiple functions. These functions are often combined into a single function
app, but they can also run in separate function apps. In Premium and Dedicated (App Service) hosting plans, multiple function apps can also share the same resources by running in the same plan. How you group your functions and function apps can affect the performance, scaling, configuration, deployment, and security of your overall solution.

For Consumption and Premium plan, all functions in a function app are dynamically scaled together.

For more information on how to organize your functions, see Function organization best practices.

## Optimize deployments

When you deploy a function app, remember that the unit of deployment for functions in Azure is the function app. You deploy all functions in a function app at the same time, usually from the same deployment package.

Consider these options for a successful deployment:

- Have your functions run from the deployment package. This run from package approach provides the following benefits:

- Reduces the risk of file copy locking problems.

- Can be deployed directly to a production app and doesn't trigger a restart.

- All files in the package are available to your app.

- Improves the performance of ARM template deployments.

- Might reduce cold-start times, particularly for JavaScript functions with large npm package trees.

- Consider using continuous deployment to connect deployments to your source control solution. Continuous deployments also let you run from the deployment package.

- For Premium plan hosting, consider adding a warmup trigger to reduce latency when new instances are added. For more information, see Azure Functions warm-up trigger.

- To minimize deployment downtime, use deployment slots for Consumption, Premium, and Dedicated plans. Or, configure rolling updates for zero-downtime deployments in the Flex Consumption plan. For more information, see Azure Functions deployment slots and site update strategies in Flex Consumption.

## Write robust functions

Follow design principles that help with the general performance and availability of your functions. These principles include:

- Avoid long running functions

- Plan cross-function communication

- Write functions to be stateless

- Write defensive functions

Transient failures are common in cloud computing, so use a retry pattern when accessing cloud-based resources. Many triggers and bindings already implement retry.

Prioritize integration testing by continuously testing your functions in the context of the full application and in your build automation pipelines.

## Design for security

Consider security during the planning phase, not after your functions are ready. For more information, see Securing Azure Functions.

## Consider concurrency

As demand builds on your function app because of incoming events, Consumption and Premium plans scale out the function apps. It's important to understand how your function app responds to load and how the triggers can be configured to handle incoming events. For a general overview, see Event-driven scaling in Azure Functions.

Dedicated (App Service) plans require you to provide scaling for your function apps.

### Worker process count

In some cases, it's more efficient to handle the load by creating multiple processes, called language worker processes, in the instance before scale-out. The FUNCTIONS_WORKER_PROCESS_COUNT setting controls the maximum number of language worker processes allowed. The default for this setting is `1`, which means that multiple processes aren't used. After the maximum number of processes are reached, the function app scales out to more instances to handle the load. This setting doesn't apply for C# class library functions, which run in the host process.

When you use `FUNCTIONS_WORKER_PROCESS_COUNT` on a Premium plan or Dedicated (App Service) plan, consider the number of cores provided by your plan. For example, the Premium plan `EP2` provides two cores, so you should start with a value of `2` and increase by two as needed, up to the maximum.

### Trigger configuration

When you plan for throughput and scaling, understand how the different types of triggers process events. Some triggers give you control over batching behaviors and concurrency. Adjusting these values can help each instance scale appropriately for the demands of the invoked functions. You apply these configuration options to all triggers in a function app, and maintain them in the host.json file for the app. For settings details, see the Configuration section of the specific trigger reference.

To learn more about how Functions processes message streams, see Azure Functions reliable event processing.

### Plan for connections

Connection limits apply to function apps running in Consumption plan. These limits apply to each instance. Because of these limits and as a general best practice, optimize your outbound connections from your function code. For more information, see Manage connections in Azure Functions.

### Language-specific considerations

For your language of choice, keep in mind the following considerations:

- 
C#

- 
Java

- 
JavaScript

- 
PowerShell

- 
Python

- Use async code but avoid blocking calls.

- Use cancellation tokens (in-process only).

- For applications that are a mix of CPU-bound and IO-bound operations, consider using more worker processes.

- Use `async` and `await`.

- Use multiple worker processes for CPU bound applications.

- Review the concurrency considerations.

- Improve throughput performance of Python apps in Azure Functions

## Maximize availability

Cold start is a key consideration for serverless architectures. For more information, see Cold starts. If cold start is a concern for your scenario, see Understanding serverless cold start.

Both Flex Consumption and Premium plans are recommended for reducing cold starts while maintaining dynamic scale. Use the following guidance to reduce cold starts and improve availability in all hosting plans.

Plan
Guidance

Flex Consumption plan
â¢ Use always ready instances to keep instances running
â¢ Set always ready instance counts

Premium plan
â¢ Implement a Warmup trigger in your function app
â¢ Set the values for Always-Ready instances and Max Burst limit
â¢ Use virtual network trigger support when using non-HTTP triggers on a virtual network

Dedicated plans
â¢ Run on at least two instances with Azure App Service Health Check enabled
â¢ Implement autoscaling

Consumption plan
â¢ Review your use of Singleton patterns and the concurrency settings for bindings and triggers to avoid artificially placing limits on how your function app scales.
â¢ Review the `functionAppScaleLimit` setting, which can limit scale-out
â¢ Check for a Daily Usage Quota (GB-Sec) limit set during development and testing. Consider removing this limit in production environments.

## Monitor effectively

Azure Functions offers built-in integration with Azure Application Insights to monitor your function execution and traces written from your code. For more information, see Monitor executions in Azure Functions. Azure Monitor also provides facilities for monitoring the health of the function app itself. For more information, see Monitor Azure Functions.

When using Application Insights integration to monitor your functions, review the Application Insights logs. If data you expect to find is missing, consider adjusting the sampling settings to better capture your monitoring scenario. Use the `excludedTypes` setting to exclude certain types from sampling, such as `Request` or `Exception`. For more information, see Configure sampling.

Azure Functions also allows you to send system-generated and user-generated logs to Azure Monitor Logs. Integration with Azure Monitor Logs is currently in preview.

## Build in redundancy

Your business needs might require that your functions always be available, even during a data center outage. To learn how to use a multiregional approach to keep your critical functions always running, see Reliability in Azure Functions.

## Next steps

Manage your function app

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-09
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
