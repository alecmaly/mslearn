# https://learn.microsoft.com/en-us/azure/event-grid/compare-messaging-services

Source: https://learn.microsoft.com/en-us/azure/event-grid/compare-messaging-services

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
 

 

 

 

 
 
# Choose between Azure Event Grid, Event Hubs, and Service Bus

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure provides several services for delivering events and messages throughout a solution. Each service targets different scenarios, from reactive event routing to high-throughput streaming to enterprise-grade transactional messaging.

This article compares the following services:

- Azure Event Grid

- Azure Event Hubs

- Azure Service Bus

## Choose a candidate service

This section helps you select the most likely services for your needs.

Use the following table to quickly narrow down which service fits your scenario:

Criterion
Event Grid
Event Hubs
Service Bus

Primary purpose
Reactive event routing
Big data streaming and ingestion
Enterprise transactional messaging

Data model
Events (discrete notifications)
Event streams (time-ordered series)
Messages (high-value payloads)

Delivery guarantee
At least once
At least once
At least once (optional ordered, exactly once with sessions)

When to use
React to status changes, serverless architectures
Telemetry, distributed data streaming, real-time analytics
Order processing, financial transactions, workflows

The result of this section is a starting point for consideration. Use the following sections to perform a detailed evaluation of the services.

## Events vs. messages in Azure messaging services

There's an important distinction between Azure services that deliver an event and services that deliver a message.

Event: A lightweight notification of a condition or state change. The publisher has no expectation about how the event is handled. Events can be discrete (reporting a state change that's actionable) or part of a time-ordered series (reporting a condition that's analyzable). Discrete events are ideal for serverless solutions that need to scale.

Message: Raw data produced by a service to be consumed or stored elsewhere. The message contains the data that triggered the message pipeline. A contract exists between publisher and consumer. For example, the publisher sends a message with raw data, and expects the consumer to create a file from that data and send a response when the work is done.

## Scalability and throughput

The following table compares how Azure Event Grid, Azure Event Hubs, and Azure Service Bus handle scalability and throughput.

Criterion
Event Grid
Event Hubs
Service Bus

Throughput
Dynamically scalable, serverless
Millions of events per second
Reliable asynchronous delivery

Latency model
Near-real-time event delivery
Low latency streaming
Brokered with optional long polling

Scaling model
Automatic (serverless)
Throughput units / processing units
Messaging units (Premium)

## Messaging features

The following table compares the messaging features of Azure Event Grid, Azure Event Hubs, and Azure Service Bus.

Criterion
Event Grid
Event Hubs
Service Bus

Protocol
MQTT, HTTP
AMQP, Kafka, HTTP
AMQP, HTTP

Pub/Sub
Yes (publish-subscribe)
Yes (consumer groups)
Yes (topics and subscriptions)

Ordering
No guarantee
Per partition
FIFO (sessions)

Transactions
No
No
Yes

Duplicate detection
No
No
Yes

Dead-lettering
Yes
No
Yes

Batching
Yes
Yes (event batches)
Yes (sessions)

Capture / replay
No
Yes (Event Hubs Capture)
No

## Integration and deployment

The following table compares integration and deployment options for Azure Event Grid, Azure Event Hubs, and Azure Service Bus.

Criterion
Event Grid
Event Hubs
Service Bus

Azure service integration
Deep integration with Azure services and third-party services
Stream-processing infrastructures and analytics services
Enterprise applications, hybrid cloud, on-premises connectivity

Editions
Azure Event Grid (PaaS), Event Grid on Kubernetes with Azure Arc
Standard, Premium, Dedicated
Basic, Standard, Premium

## Use Event Grid, Event Hubs, and Service Bus together

In some cases, you use the services side by side to fulfill distinct roles. For example, an e-commerce site can use Service Bus to process orders, Event Hubs to capture site telemetry, and Event Grid to respond to events like an item being shipped.

In other cases, you link them together to form an event and data pipeline. You use Event Grid to respond to events in the other services. For an example of using Event Grid with Event Hubs to migrate data to Azure Synapse Analytics, see Stream big data into Azure Synapse Analytics. The following image shows the workflow for streaming the data.

## Related content

- Asynchronous messaging options in Azure

- Events, Data Points, and Messages - Choosing the right Azure messaging service for your data

 
 

 
 

 

 
 
 
 
 
 
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
 2026-06-12
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
