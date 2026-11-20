# https://learn.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings

Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings

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
 

 

 

 

 
 
# Azure Functions triggers and bindings

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 In this article, you learn the high-level concepts surrounding triggers and bindings for functions.

Triggers cause a function to run. A trigger defines how a function is invoked, and a function must have exactly one trigger. Triggers can also pass data into your function, as you would with method calls.

Binding to a function is a way of declaratively connecting your functions to other resources. Bindings either pass data into your function (an input binding) or enable you to write data out from your function (an output binding) by using binding parameters. Your function trigger is essentially a special type of input binding.

You can mix and match bindings to suit your function's specific scenario. Bindings are optional, and a function might have one or multiple input and/or output bindings.

Triggers and bindings let you avoid hardcoding access to other services. Your function receives data (for example, the content of a queue message) in function parameters. You send data (for example, to create a queue message) by using the return value of the function.

Consider the following examples of how you could implement functions:

Example scenario
Trigger
Input binding
Output binding

A new queue message arrives, which runs a function to write to another queue.
Queue*
None
Queue*

A scheduled job reads Azure Blob Storage contents and creates a new Azure Cosmos DB document.
Timer
Blob Storage
Azure Cosmos DB

Azure Event Grid is used to read an image from Blob Storage and a document from Azure Cosmos DB to send an email.
Event Grid
Blob Storage and Azure Cosmos DB
SendGrid

* Represents different queues.

These examples aren't meant to be exhaustive, but they illustrate how you can use triggers and bindings together. For a more comprehensive set of scenarios, see Azure Functions scenarios.

Tip

Azure Functions doesn't require you to use input and output bindings to connect to Azure services. You can always create an Azure SDK client in your code and use it instead for your data transfers. For more information, see Connect to services.

## Trigger and binding definitions

The following example shows an HTTP-triggered function with an output binding that writes a message to an Azure Storage queue.

For C# class library functions, you configure triggers and bindings by decorating methods and parameters with C# attributes. The specific attribute that you apply might depend on the C# runtime model:

- 
Isolated worker model

- 
In-process model

You define the HTTP trigger (`HttpTrigger`) on the `Run` method for a function named `HttpExample` that returns a `MultiResponse` object:

`[Function("HttpExample")]
public MultiResponse Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequest req)
`

This example shows the `MultiResponse` object definition. The object definition returns `HttpResponse` to the HTTP request and writes a message to a storage queue by using a `QueueOutput` binding:

`public class MultiResponse
{
 [QueueOutput("outqueue", Connection = "AzureWebJobsStorage")]
 public string[] Messages { get; set; }
 public IActionResult HttpResponse { get; set; }
}
`

For more information, see the C# guide for isolated worker models.

You define the HTTP trigger (`HttpTrigger`) on the `Run` method for a function named `HttpExample`. This function writes to a storage queue that the `Queue` and `StorageAccount` attributes define on the `msg` parameter:

`[FunctionName("HttpExample")]
public static async Task<IActionResult> Run(
 [HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)] HttpRequest req, 
 [Queue("outqueue"),StorageAccount("AzureWebJobsStorage")] ICollector<string> msg, 
 ILogger log)
{
`

For more information, see the C# guide for in-process models.

Legacy C# script functions use a `function.json` definition file. For more information, see the Azure Functions C# script (.csx) developer reference.

For Java functions, you configure triggers and bindings by annotating specific methods and parameters. You define this HTTP trigger (`@HttpTrigger`) on the `run` method for a function named `HttpExample`. The function writes to a storage queue named `outqueue` that the `@QueueOutput` annotation defines on the `msg` parameter:

`@FunctionName("HttpExample")
public HttpResponseMessage run(
 @HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) 
 HttpRequestMessage<Optional<String>> request, 
 @QueueOutput(name = "msg", queueName = "outqueue", 
 connection = "AzureWebJobsStorage") OutputBinding<String> msg, 
 final ExecutionContext context) {
 context.getLogger().info("Java HTTP trigger processed a request.");
`

For more information, see the Java developer guide.

The way that you define triggers and bindings for Node.js functions depends on the specific version of Node.js for Azure Functions:

- 
v4

- 
v3

In Node.js for Azure Functions version 4, you configure triggers and bindings by using objects exported from the `@azure/functions` module. For more information, see the Node.js developer guide.

In Node.js for Azure Functions version 3, you configure triggers and bindings in a function-specific `function.json` file in the same folder as your code. For more information, see the Node.js developer guide.

- 
v4

- 
v3

The exported `app` object's `http` method defines an HTTP trigger. The `storageQueue` method on `output` defines an output binding on this trigger.

`const { app, output } = require('@azure/functions');

const queueOutput = output.storageQueue({
 queueName: 'outqueue',
 connection: 'MyStorageConnectionAppSetting',
});

app.http('httpTrigger1', {
 methods: ['GET', 'POST'],
 authLevel: 'anonymous',
 extraOutputs: [queueOutput],
 handler: async (request, context) => {
 const body = await request.text();
 context.extraOutputs.set(queueOutput, body);
 return { body: 'Created queue item.' };
 },
});
`

This example `function.json` file defines the HTTP trigger function that returns an HTTP response and writes to a storage queue:

`{
 "bindings": [
 {
 "type": "httpTrigger",
 "direction": "in",
 "authLevel": "function",
 "name": "input"
 },
 {
 "type": "http",
 "direction": "out",
 "name": "$return"
 },
 {
 "type": "queue",
 "direction": "out",
 "name": "myQueueItem",
 "queueName": "outqueue",
 "connection": "MyStorageConnectionAppSetting"
 }
 ]
}
`

- 
v4

- 
v3

The exported `app` object's `http` method defines an HTTP trigger. The `storageQueue` method on `output` defines an output binding on this trigger.

`import { app, HttpRequest, HttpResponseInit, InvocationContext, output } from '@azure/functions';

const queueOutput = output.storageQueue({
 queueName: 'outqueue',
 connection: 'MyStorageConnectionAppSetting',
});

export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
 const body = await request.text();
 context.extraOutputs.set(queueOutput, body);
 return { body: 'Created queue item.' };
}

app.http('httpTrigger1', {
 methods: ['GET', 'POST'],
 authLevel: 'anonymous',
 extraOutputs: [queueOutput],
 handler: httpTrigger1,
});
`

This example `function.json` file defines the HTTP trigger function that returns an HTTP response and writes to a storage queue:

`{
 "bindings": [
 {
 "type": "httpTrigger",
 "direction": "in",
 "authLevel": "function",
 "name": "input"
 },
 {
 "type": "http",
 "direction": "out",
 "name": "$return"
 },
 {
 "type": "queue",
 "direction": "out",
 "name": "myQueueItem",
 "queueName": "outqueue",
 "connection": "MyStorageConnectionAppSetting"
 }
 ]
}
`

This example `function.json` file defines the function:

` {
 "authLevel": "function",
 "type": "httpTrigger",
 "direction": "in",
 "name": "Request",
 "methods": [
 "get",
 "post"
 ]
 },
 {
 "type": "http",
 "direction": "out",
 "name": "Response"
 },
 {
 "type": "queue",
 "direction": "out",
 "name": "msg",
 "queueName": "outqueue",
 "connection": "AzureWebJobsStorage"
 }
 ]
}
`

For more information, see the PowerShell developer guide.

The way that you define the function depends on the version of Python for Azure Functions:

- 
v2

- 
v1

In Python for Azure Functions version 2, you define the function directly in code by using decorators:

`app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)

@app.route(route="HttpExample")
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
def HttpExample(req: func.HttpRequest, msg: func.Out[func.QueueMessage]) -> func.HttpResponse:
 logging.info('Python HTTP trigger function processed a request.')
`

In Python for Azure Functions version 1, this example `function.json` file defines an HTTP trigger function that returns an HTTP response and writes to a storage queue:

` {
 "authLevel": "function",
 "type": "httpTrigger",
 "direction": "in",
 "name": "Request",
 "methods": [
 "get",
 "post"
 ]
 },
 {
 "type": "http",
 "direction": "out",
 "name": "Response"
 },
 {
 "type": "queue",
 "direction": "out",
 "name": "msg",
 "queueName": "outqueue",
 "connection": "AzureWebJobsStorage"
 }
 ]
}
`

## Binding considerations

- Not all services support both input and output bindings. See your specific binding extension for specific code examples for bindings.

- Triggers and bindings are defined differently depending on the development language. Make sure to select your language at the top of this article.

- Trigger and binding names are limited to alphanumeric characters and `_`, the underscore.

## Task to add bindings to a function

You can connect your function to other services by using input or output bindings. Add a binding by adding its specific definitions to your function. To learn how, see Add bindings to an existing function in Azure Functions.

Azure Functions supports multiple bindings, which you must configure correctly. For example, a function can read data from a queue (input binding) and write data to a database (output binding) at the same time.

## Supported bindings

This table shows the triggers and bindings available in Azure Functions:1

Type
Trigger
Input
Output

Blob Storage
â
â
â

Azure Cosmos DB
â
â
â

Azure Data Explorer

â
â

Azure SQL
â
â
â

Event Grid
â

â

Event Hubs
â

â

HTTP and webhooks
â

â

IoT Hub
â

Kafka2
â

â

Managed connector
â

Model Context Protocol
â

Queue Storage
â

â

Redis
â
â
â

RabbitMQ2
â

â

SendGrid

â

Service Bus
â

â

Azure SignalR Service
â
â
â

Table Storage

â
â

Timer
â

Twilio

â

- Register all bindings except HTTP and timer. See Register Azure Functions binding extensions.

- Triggers aren't supported in the Consumption plan. This binding type requires runtime-driven triggers.

For information about which bindings are in preview or are approved for production use, see Supported languages.

Specific versions of binding extensions are supported only while the underlying service SDK is supported. Changes to support in the underlying service SDK version affect the support for the consuming extension.

### Managed connectors

Managed connectors in Azure Connector Namespace extend the services available through supported bindings. You can use connector triggers and SDK actions to integrate with services such as Microsoft 365, Teams, and SharePoint while Connector Namespace manages webhooks, authentication, and retries. To learn more, see Use managed connectors in Azure Functions.

## SDK types

Azure Functions binding extensions use Azure service SDKs to connect to Azure services. The specific SDK types used by bindings can affect how you work with the data in your functions. Some bindings support SDK-specific types that provide richer functionality and better integration with the service, while others use more generic types like strings or byte arrays. When available, using SDK-specific types can provide benefits such as better type safety, easier data manipulation, and access to service-specific features.

This table indicates binding extensions that currently support SDK types:

Extension
Types
Support level

Azure Blob Storage
`BlobClient`
`BlobContainerClient`
`BlockBlobClient`
`PageBlobClient`
`AppendBlobClient`
Trigger: GA
Input: GA

Azure Cosmos DB
`CosmosClient`
`Database`
`Container`
Input: GA

Azure Event Grid
`CloudEvent`
`EventGridEvent`
Trigger: GA

Azure Event Hubs
`EventData`
`EventHubProducerClient`
Trigger: GA

Azure Queue Storage
`QueueClient`
`QueueMessage`
Trigger: GA

Azure Service Bus
`ServiceBusClient`
`ServiceBusReceiver`
`ServiceBusSender`
`ServiceBusMessage`
Trigger: GA

Azure Table Storage
`TableClient`
`TableEntity`
Input: GA

Considerations for SDK types:

- When using binding expressions that rely on trigger data, SDK types for the trigger itself cannot be used.

- For output scenarios where you might use an SDK type, create and work with SDK clients directly instead of using an output binding.

- The Azure Cosmos DB trigger uses the Azure Cosmos DB change feed and exposes change feed items as JSON-serializable types. As a result, SDK types aren't supported for this trigger.

For more information, see SDK types in the C# developer guide.

Extension
Types
Support level
Samples

Azure Blob Storage
`BlobClient`
`ContainerClient`
`StorageStreamDownloader`
Trigger: GA
Input: GA
Quickstart
`BlobClient`
`ContainerClient`
`StorageStreamDownloader`

Azure Cosmos DB
`CosmosClient`
`DatabaseProxy`
`ContainerProxy`
Input: preview
Quickstart
 `ContainerProxy`
`CosmosClient`
`DatabaseProxy`

Azure Event Hubs
`EventData`
Trigger: preview
Quickstart
 `EventData`

Azure Service Bus
`ServiceBusReceivedMessage`
Trigger: preview
Quickstart
 `ServiceBusReceivedMessage`

Considerations for SDK types:

- For output scenarios where you might use an SDK type, create and work with SDK clients directly instead of using an output binding.

- The Azure Cosmos DB trigger uses the Azure Cosmos DB change feed and exposes change feed items as JSON-serializable types. As a result, SDK types aren't supported for this trigger.

SDK types are supported only when using the Python v2 programming model. For more information, see SDK type bindings in the Python developer guide.

Extension
Types
Support level

Azure Blob Storage
`BlobClient`
`ContainerClient`
`ReadableStream`
Preview

Azure Service Bus
`ServiceBusClient`
`ServiceBusReceiver`
`ServiceBusSender`
`ServiceBusMessage`
Preview

SDK types are supported only when using the Node v4 programming model. For more information, see SDK types in the Node.js developer guide.

Extension
Types
Support level

Azure Blob Storage
`BlobClient`
`BlobContainerClient`
Preview

For more information, see SDK types in the Java developer guide.

Important

SDK types aren't currently supported for PowerShell apps.

Go supports SDK client injection for triggers that provide Azure SDK clients. Blob Storage triggers can receive an authenticated Azure SDK `*blob.Client` directly in the handler.

Extension
Types
Support level

Azure Blob Storage
`*blob.Client`
Generally available

For more information, see SDK type bindings in the Go developer reference.

## Agent bindings

Important

Agent bindings for Python function apps are currently in preview. Features, package names, and configuration can change before general availability.

Agent bindings let you inject an `Agent` object into a Python function while retaining standard Azure Functions triggers, bindings, and application logic. Use agent bindings when part of a function workflow benefits from agentic reasoning but your function code must remain in control of execution.

Agent bindings also support Durable Functions orchestrations. The replay-safe `context.call_agent()` API runs agent operations in an activity so that orchestration replay remains deterministic.

Agent bindings are available for the Python v2 programming model. For more information, see Agent bindings for Python function apps.

## Code examples for bindings

Use the following table to find more examples of specific binding types that show you how to work with bindings in your functions. First, choose the language tab that corresponds to your project.

Binding code for C# depends on the specific process model.

- 
Isolated process

- 
In-process

Service
Examples
Samples

Blob Storage
Trigger
Input
Output
Link

Azure Cosmos DB
Trigger
Input
Output
Link

Azure Data Explorer
Input
Output
Link

Azure SQL
Trigger
Input
Output
Link

Event Grid
Trigger
Output
Link

Event Hubs
Trigger
Output

IoT Hub
Trigger
Output

HTTP
Trigger
Link

Model Context Protocol
Tool Trigger
Resource Trigger
Prompt Trigger
Link

Queue Storage
Trigger
Output
Link

RabbitMQ
Trigger
Output

SendGrid
Output

Service Bus
Trigger
Output
Link

Azure SignalR Service
Trigger
Input
Output

Table Storage
Input
Output

Timer
Trigger
Link

Twilio
Output
Link

Managed connectors
Trigger
Link

Service
Examples
Samples

Blob Storage
Trigger
Input
Output
Link

Azure Cosmos DB
Trigger
Input
Output
Link

Azure Data Explorer
Input
Output
Link

Azure SQL
Trigger
Input
Output
Link

Event Grid
Trigger
Output
Link

Event Hubs
Trigger
Output

IoT Hub
Trigger
Output

HTTP
Trigger
Link

Queue Storage
Trigger
Output
Link

RabbitMQ
Trigger
Output

SendGrid
Output

Service Bus
Trigger
Output
Link

Azure SignalR Service
Trigger
Input
Output

Table Storage
Input
Output

Timer
Trigger
Link

Twilio
Output
Link

Service
Examples
Samples

Blob Storage
Trigger
Input
Output
Link

Azure Cosmos DB
Trigger
Input
Output
Link

Azure Data Explorer
Input
Output
Link

Azure SQL
Trigger
Input
Output

Event Grid
Trigger
Output
Link

Event Hubs
Trigger
Output

IoT Hub
Trigger
Output

HTTP
Trigger
Link

Model Context Protocol
Tool Trigger
Resource Trigger
Prompt Trigger
Link

Queue Storage
Trigger
Output
Link

RabbitMQ
Trigger
Output

SendGrid
Output

Service Bus
Trigger
Output
Link

Azure SignalR Service
Trigger
Input
Output

Table Storage
Input
Output

Timer
Trigger
Link

Twilio
Output

Service
Examples
Samples

Blob Storage
Trigger
Input
Output
Link

Azure Cosmos DB
Trigger
Input
Output
Link

Azure Data Explorer
Input
Output

Azure SQL
Trigger
Input
Output
Link

Event Grid
Trigger
Output

Event Hubs
Trigger
Output

IoT Hub
Trigger
Output

HTTP
Trigger
Link

Model Context Protocol
Tool Trigger
Resource Trigger
Prompt Trigger
Link

Queue Storage
Trigger
Output
Link

RabbitMQ
Trigger
Output

SendGrid
Output

Service Bus
Trigger
Output
Link

Azure SignalR Service
Trigger
Input
Output

Table Storage
Input
Output

Timer
Trigger

Twilio
Output

Managed connectors
Trigger
Link

Service
Examples
Samples

Blob Storage
Trigger
Input
Output

Azure Cosmos DB
Trigger
Input
Output

Azure SQL
Trigger
Input
Output

Event Grid
Trigger
Output

Event Hubs
Trigger
Output

IoT Hub
Trigger
Output

HTTP
Trigger
Link

Queue Storage
Trigger
Output

RabbitMQ
Trigger
Output

SendGrid
Output

Service Bus
Trigger
Output

Azure SignalR Service
Trigger
Input
Output

Table Storage
Input
Output

Timer
Trigger

Twilio
Output

Binding code for Python depends on the Python model version.

- 
v2

- 
v1

Service
Examples
Samples

Blob Storage
Trigger
Input
Output
Link

Azure Cosmos DB
Trigger
Input
Output
Link

Azure Data Explorer
Input
Output

Azure SQL
Trigger
Input
Output
Link

Event Grid
Trigger
Output

Event Hubs
Trigger
Output

IoT Hub
Trigger
Output

HTTP
Trigger
Link

Model Context Protocol
Tool Trigger
Resource Trigger
Prompt Trigger
Link

Queue Storage
Trigger
Output

RabbitMQ
Trigger
Output

SendGrid
Output

Service Bus
Trigger
Output
Link

Azure SignalR Service
Trigger
Input
Output

Table Storage
Input
Output

Timer
Trigger

Twilio
Output

Managed connectors
Trigger
Link

Service
Examples
Samples

Blob Storage
Trigger
Input
Output

Azure Cosmos DB
Trigger
Input
Output

Azure Data Explorer
Input
Output

Azure SQL
Trigger
Input
Output
Link

Event Grid
Trigger
Output

Event Hubs
Trigger
Output

IoT Hub
Trigger
Output

HTTP
Trigger

Queue Storage
Trigger
Output

RabbitMQ
Trigger
Output

SendGrid
Output

Service Bus
Trigger
Output

Azure SignalR Service
Trigger
Input
Output

Table Storage
Input
Output

Timer
Trigger

Twilio
Output

## Custom bindings

You can create custom input and output bindings. You must author bindings in .NET, but you can consume them from any supported language. For more information about creating custom bindings, see Creating custom input and output bindings.

## Related content

- Binding expressions and patterns

- Register Azure Functions binding extensions

- Manually run a non-HTTP-triggered function

- Handling binding errors

 
 

 
 

 

 
 
 
 
 
 
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
 2026-10-12
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
