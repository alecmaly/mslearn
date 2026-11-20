# https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-queues-topics-subscriptions

Source: https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-queues-topics-subscriptions

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
 

 

 

 

 
 
# Service Bus queues, topics, and subscriptions

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Service Bus supports reliable message queuing and durable publish/subscribe messaging. The messaging entities that form the core of the messaging capabilities in Service Bus are queues, topics and subscriptions.

This article explains these core messaging entities, their benefits, and when to use each one in your application architecture.

Important

If you're new to Azure Service Bus, read through Introduction to Azure Service Bus before going through this article.

## Choose between queues and topics

The following table summarizes the key differences between queues and topics to help you choose the right messaging entity for your scenario.

Feature
Queues
Topics and subscriptions

Communication pattern
Point-to-point
Publish/subscribe (one-to-many)

Message delivery
Single consumer per message
Multiple subscribers can receive copies

Use case
Task distribution, load leveling
Event broadcasting, fan-out scenarios

Filtering
Not supported
Subscription filters for selective message delivery

## Queues

Queues offer First In, First Out (FIFO) message delivery to one or more competing consumers. That is, receivers typically receive and process messages in the order in which they were added to the queue. And, only one message consumer receives and processes each message.

### Benefits of using queues

Benefit
Description

Temporal decoupling
Producers (senders) and consumers (receivers) don't have to send and receive messages at the same time, because messages are stored durably in the queue. The producer doesn't have to wait for a reply from the consumer to continue processing.

Load leveling
Producers and consumers can send and receive messages at different rates. The consuming application only needs to handle average load instead of peak load, saving infrastructure costs.

Competing consumers
Multiple worker processes can read from the queue, with each message processed by only one worker. This pull-based load balancing allows workers to process at their own maximum rate.

Loose coupling
Because producers and consumers aren't aware of each other, a consumer can be upgraded without affecting the producer.

### Create queues

You can create queues using one of the following options:

- Azure portal

- PowerShell

- CLI

- Azure Resource Manager templates (ARM templates)

Service Bus supports hierarchical entity names with forward slashes as separators, for example `orders/region/west`. When using ARM-based tools (portal, CLI, PowerShell, or templates), replace `/` with `~` in entity names. For details, see Entity names with forward slashes.

Then, send and receive messages using clients written in programming languages including the following ones:

- C#

- Java

- Python

- JavaScript

### Receive modes

You can specify two different modes in which consumers can receive messages from Service Bus.

#### Receive and delete mode

When Service Bus receives the request from the consumer, it marks the message as consumed and returns it to the consumer application. This mode is the simplest model and works best for scenarios where the application can tolerate not processing a message if a failure occurs.

If the consumer crashes before processing the message, the message is lost because Service Bus already marked it as consumed. This process is often called at-most once processing.

#### Peek lock mode

The Receive operation becomes two-stage, which makes it possible to support applications that can't tolerate missing messages:

- Finds the next message to be consumed, locks it to prevent other consumers from receiving it, and then returns the message to the application.

- After the application finishes processing the message, it requests the Service Bus service to complete the second stage of the receive process. Then, the service marks the message as consumed.

Handling failures in peek lock mode:

- Abandon: If the application can't process the message, it can request Service Bus to abandon the message. Service Bus unlocks the message and makes it available to be received again.

- Lock timeout: If the application fails to process the message before the lock timeout expires, Service Bus unlocks the message and makes it available to be received again.

- Application crash: If the application crashes after processing the message but before completing it, Service Bus redelivers the message when the application restarts. This process is often called at-least once processing.

If your scenario can't tolerate duplicate processing, add extra logic in your application to detect duplicates. For more information, see Duplicate detection, which is known as exactly once processing.

Note

For more information about these two modes, see Settling receive operations.

## Topics and subscriptions

A queue allows processing of a message by a single consumer. In contrast to queues, topics and subscriptions provide a one-to-many form of communication in a publish and subscribe pattern. It's useful for scaling to large numbers of recipients. Each published message is made available to each subscription registered with the topic. Publisher sends a message to a topic and one or more subscribers receive a copy of the message.

Publishers send messages to a topic in the same way that they send messages to a queue. But, consumers don't receive messages directly from the topic. Instead, consumers receive messages from subscriptions of the topic. A topic subscription resembles a virtual queue that receives copies of the messages that are sent to the topic. Consumers receive messages from a subscription identically to the way they receive messages from a queue. The message-sending functionality of a queue maps directly to a topic and its message-receiving functionality maps to a subscription. Among other things, this feature means that subscriptions support the same patterns described earlier in this section regarding queues: competing consumer, temporal decoupling, load leveling, and load balancing.

### Subscription filters

Subscriptions can define which messages they want to receive from a topic. These messages are specified in the form of one or more named subscription rules. Each rule consists of a filter condition that selects particular messages, and optionally contains an action that annotates the selected message. By default, a subscription to a topic receives all messages sent to the topic. The subscription has an initial default rule with a true filter that enables all messages to be selected into the subscription. The default rule has no associated action. You can define filters with rules and actions on a subscription so that the subscription receives only a subset of messages sent to the topic.

For more information about filters, see Filters and actions.

### Create topics and subscriptions

Creating a topic is similar to creating a queue, as described in the previous section. You can create topics and subscriptions using one of the following options:

- Azure portal

- PowerShell

- CLI

- ARM templates

Then, send messages to a topic and receive messages from subscriptions using clients written in programming languages including the following ones:

- C#

- Java

- Python

- JavaScript

### Rules and actions

In many scenarios, messages that have specific characteristics must be processed in different ways. To enable this processing, you can configure subscriptions to find messages with desired properties and then perform certain modifications to those properties. While Service Bus subscriptions see all messages sent to the topic, it's possible to only copy a subset of those messages to the virtual subscription queue. This filtering is accomplished using subscription filters. Such modifications are called filter actions. When a subscription is created, you can supply a filter expression that operates on the properties of the message. The properties can be both the system properties (for example, Label) and custom application properties (for example, StoreName.) The SQL filter expression is optional in this case. Without a SQL filter expression, any filter action defined on a subscription is done on all the messages for that subscription.

For a full working example, see the TopicFilters sample on GitHub. For more information about filters, see Topic filters and actions.

## Java message service (JMS) 2.0 entities

The following entities are accessible through the Java message service (JMS) 2.0 API.

- Temporary queues

- Temporary topics

- Shared durable subscriptions

- Unshared durable subscriptions

- Shared nondurable subscriptions

- Unshared nondurable subscriptions

Learn more about the JMS 2.0 entities and about how to use them.

## Express entities

Important

Express entities aren't recommended for new applications. The throughput and latency advantages are currently minimal due to optimizations in Service Bus. The Premium tier of Service Bus doesn't support Express entities.

Express entities were created for high throughput and reduced latency scenarios. With express entities, if a message is sent to a queue or topic, it isn't immediately stored in the messaging store. Instead, the message is initially cached in memory. Messages that remain in the entity are written to the message store after a delay, at which point they're protected against loss due to an outage.

In regular entities, any runtime operation (like `Send`, `Complete`, `Abandon`, `Deadletter`) is persisted to the store first, and only after the operation is acknowledged to the client as successful. In express entities, a runtime operation is acknowledged to the client as successful first, and only later lazily persisted to the store. As a result, when a machine reboots or when a hardware issue occurs, some acknowledged runtime operations might not be persisted at all. In this case, the client gets lower latency and higher throughput with express entities, at the expense of potential data loss and/or redelivery of messages.

## Next steps

Try the samples in the language of your choice:

- Azure Service Bus client library samples for .NET (latest)

- Azure Service Bus client library samples for Java (latest)

- Azure Service Bus client library samples for Python

- Azure Service Bus client library samples for JavaScript

- Azure Service Bus client library samples for TypeScript

 
 

 
 

 

 
 
 
 
 
 
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
 2026-10-13
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
