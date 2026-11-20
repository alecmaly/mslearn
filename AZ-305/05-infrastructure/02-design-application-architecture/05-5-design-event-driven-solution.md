# Unit 5: 5-design-event-driven-solution

Source: https://learn.microsoft.com/en-us/training/modules/design-application-architecture/5-design-event-driven-solution

---

# Design an event-driven solution

 
 
 
 Completed
 
 
 

 

 
 
- 7 minutes

 
 

 

 
 An event-driven architecture enables you to connect to the core application without needing to modify the existing code. When an event occurs, you can react with specific code to respond to the event. An event-driven application uses the send and forget principle. An event is sent toward the next system, which can be another service, an event hub, a stream, or a message broker.

Let's reconsider our design for the Tailwind Traders product demo application, and examine how to use a Web API that runs in Azure. When a new product review or demo video is uploaded, we need to notify all mobile apps on user devices around the world that are interested in the products. Azure Event Grid is an ideal solution for this requirement.

- The publisher of the review or video doesn't need to know about any subscribers who are interested in the affected products.

- We want to have a one-to-many relationship where we can have multiple subscribers. Subscribers can optionally decide whether they're interested in the affected products.

### Things to know about Azure Event Grid

Azure Event Grid is a fully managed event routing service. Event Grid exists to make it easier to build event-based and serverless applications on Azure.

Review the following characteristics of the service.

- Azure Event Grid aggregates all your events and provides routing from any source to any destination.

- Event Grid distributes events from sources like Azure Blob Storage accounts.

- Events are distributed to handlers like Azure functions and webhooks.

- The service manages the routing and delivery of events from many sources. The management helps to minimize cost and latency by eliminating the need for polling.

#### How Azure Event Grid works

The following illustration shows how Azure Event Grid manages the event process from multiple event sources to multiple event handlers.

- An event source such as Azure Blob Storage tags events with one or more topics, and sends events to Azure Event Grid.

- An event handler such as Azure Functions subscribes to topics they're interested in.

- Event Grid examines topic tags to decide which events to send to which handlers.

- Event Grid forwards relevant events to subscribers.

- Event Grid reacts when an event happens. However, the actual object that was changed (text file, video, audio, and so on) isn't part of the event data. Instead, Event Grid passes a URL or identifier to reference the changed object.

### Things to consider when using Azure Event Grid

Azure Event Grid can be an ideal solution for an event-driven application architecture. As you review the following considerations, think about how Event Grid can benefit the Tailwind Traders application architecture.

- Consider multiple services. Choose one or multiple Azure services to fulfill your design requirements.

Azure service
Purpose
Message or Event
Usage scenario

Azure Event Grid
Reactive programming
Event distribution (discrete)
React to status changes

Azure Event Hubs
Big data pipeline
Event streaming (series)
Conduct telemetry and distributed data streaming

Azure Service Bus
High-value enterprise messaging
Message
Fulfill order processing and financial transactions

- Consider distinct roles for services. Investigate using Azure services side by side to fulfill distinct roles. An e-commerce site can use Azure Service Bus to process an order, Azure Event Hubs to capture site telemetry, and Azure Event Grid to respond to events like an item being shipped.

- Consider push vs. pull delivery. Choose the appropriate delivery model based on your application needs:

- Push delivery (classic model): Event Grid routes events to registered handlers (webhooks, Azure Functions, etc.). Use when avoiding constant polling and the handler has a public endpoint.

- Pull delivery (namespace topics): Subscriber applications connect to Event Grid to read events at their own pace using queue-like semantics. Use when the consumer controls timing, needs private link connectivity, or can't expose a public endpoint.

- Consider linking services. Link Azure services together to form an event and data pipeline stream. In this scenario, Azure Event Grid responds to events in other services. The following illustration demonstrates how several Azure services can be linked together as an event and data pipeline to stream data.

Tip

Consider reviewing the Explore Azure Event Grid module.

 

 
 

 

 
 
 
 <section
