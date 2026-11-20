# https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview

Source: https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview

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
 

 

 

 

 
 
# What is Azure Service Bus?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Azure Service Bus is a fully managed enterprise message broker with message queues and publish-subscribe topics. Use Service Bus to decouple applications and services from each other. It provides the following benefits:

Tip

To see the latest Azure Service Bus releases, visit the Azure Updates page.

- Load-balances work across competing workers

- Safely routes and transfers data and control across service and application boundaries

- Coordinates transactional work that requires a high degree of reliability

## Overview

Applications and services transfer data between each other by using messages. A message is a container that holds data and is decorated with metadata. The data can be any kind of information, including structured data encoded with common formats such as JSON, XML, Apache Avro, or plain text.

Some common messaging scenarios include:

- Messaging. Transfer business data, such as sales or purchase orders, journals, or inventory movements.

- Decouple applications. Improve reliability and scalability of applications and services. Producer and consumer don't have to be online or readily available at the same time. The load is leveled such that traffic spikes don't overtax a service.

- Load balancing. Allow for multiple competing consumers to read from a queue at the same time, each safely obtaining exclusive ownership to specific messages.

- Topics and subscriptions. Enable 1:n relationships between publishers and subscribers, allowing subscribers to select particular messages from a published message stream.

- Transactions. Perform several operations, all in the scope of an atomic transaction. For example, the following operations can be done in the scope of a transaction:

- Obtain a message from one queue.

- Post results of processing to one or more different queues.

- Move the input message from the original queue.

The results become visible to downstream consumers only upon success, including the successful settlement of input message, allowing for once-only processing semantics. This transaction model is a robust foundation for the compensating transactions pattern in the greater solution context.

- Message sessions. Implement high-scale coordination of workflows and multiplexed transfers that require strict message ordering or message deferral.

If you're familiar with other message brokers like Apache ActiveMQ, Service Bus concepts are similar to what you know. As Service Bus is a platform as a service (PaaS) offering, a key difference is that you don't need to worry about the following actions. Azure takes care of those chores for you.

- Worrying about hardware failures

- Keeping the operating systems or the products patched

- Placing logs and managing disk space

- Handling backups

- Failing over to a reserve machine

## Concepts

This section discusses basic concepts of Service Bus.

### Queues

You send and receive messages through queues. Queues store messages until the receiving application is available to receive and process them.

Messages in queues are ordered and timestamped on arrival. Once the broker accepts the message, it always holds the message durably in triple-redundant storage, spread across availability zones if the namespace is zone-enabled. Service Bus keeps messages in memory or volatile storage until the client reports them as accepted.

Messages are delivered in pull mode, so the system only delivers messages when requested. Unlike the busy-polling model of some other cloud queues, the pull operation can be long-lived and only completes once a message is available.

Note

For a comparison of Service Bus queues with Storage queues, see Storage queues and Service Bus queues - compared and contrasted.

### Topics

You can also use topics to send and receive messages. While a queue is often used for point-to-point communication, topics are useful in publish-subscribe scenarios.

Topics can have multiple, independent subscriptions. These subscriptions attach to the topic and otherwise work exactly like queues from the receiver side. A subscriber to a topic can receive a copy of each message sent to that topic. Subscriptions are named entities. Subscriptions are durable by default, but you can configure them to expire and then be automatically deleted. Through the Java Message Service (JMS) API, Service Bus Premium also allows you to create volatile subscriptions that exist for the duration of the connection.

You can define rules on a subscription. A subscription rule has a filter to define a condition for the message to be copied into the subscription and an optional action that can modify message metadata. For more information, see Topic filters and actions. This feature is useful in the following scenarios:

- You don't want a subscription to receive all messages sent to a topic.

- You want to mark up messages with extra metadata when they pass through a subscription.

Note

For more information about queues and topics, see Service Bus queues, topics, and subscriptions.

### Namespaces

A namespace is a container for all messaging components, such as queues and topics. A namespace can have one or more queues and topics, and it often serves as an application container.

You can compare a namespace to a server in the terminology of other brokers, but the concepts aren't directly equivalent. A Service Bus namespace is your own capacity slice of a large cluster made up of dozens of all-active virtual machines. It optionally spans three Azure availability zones. You get the availability and robustness benefits of running the message broker at enormous scale. And, you don't need to worry about underlying complexities. Service Bus is serverless messaging.

## Advanced features

Service Bus also has advanced features that enable you to solve more complex messaging problems. The following sections describe these key features:

### Message sessions

To realize a first-in, first-out (FIFO) guarantee in processing messages in Service Bus queues or subscriptions, use sessions. You can also use sessions to implement request-response patterns. The request-response pattern enables the sender application to send a request and provides a way for the receiver to correctly send a response back to the sender application. For more information, see Message sessions.

### Autoforwarding

The autoforwarding feature enables you to chain a queue or subscription to another queue or topic that is part of the same namespace. When you enable autoforwarding, Service Bus automatically removes messages that are placed in the first queue or subscription (source) and puts them in the second queue or topic (destination). For more information, see Chaining Service Bus entities with autoforwarding.

### Dead-lettering

Service Bus queues and topic subscriptions provide a secondary subqueue, called a dead-letter queue (DLQ). The dead letter queue holds messages that can't be delivered to any receiver, or messages that can't be processed. You can then remove messages from the DLQ and inspect them. An application might, with help of an operator, correct issues and resubmit the message, log the fact that there was an error, and take a corrective action. For more information, see Overview of Service Bus dead-letter queues.

### Scheduled delivery

You can submit messages to a queue or topic for delayed processing. For example, to schedule a job to become available for processing by a system at a certain time. For more information, see Scheduled messages.

### Message deferral

When a queue or subscription client receives a message that it's willing to process, but processing isn't currently possible because of special circumstances within the application, the entity can defer retrieval of the message to a later point. The message remains in the queue or subscription, but it's set aside. For more information, see Message deferral.

### Transactions

A transaction groups two or more operations together into an execution scope. Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within the scope of a transaction. For more information, see Overview of Service Bus transaction processing.

### Filters and actions

Subscribers can define which messages they want to receive from a topic. These messages are specified in the form of one or more named subscription rules. Each rule consists of a filter condition that selects particular messages, and optionally contains an action that annotates the selected message. For each matching rule condition, the subscription produces a copy of the message, which can be differently annotated for each matching rule. For more information, see Topic filters and actions.

### Auto-delete on idle

By using Auto-delete on idle, you can specify an idle interval after which the queue is automatically deleted. The interval resets when there's traffic on the queue. The minimum duration is five minutes.

### Duplicate detection

If an error occurs that causes the client to doubt the outcome of a send operation, duplicate detection removes doubt in these situations. The sender can resend the same message, and the queue or topic discards any duplicate copies. For more information, see Duplicate detection.

## Batch deletion of messages

Azure Service Bus supports deletion of messages in batches. This feature is useful when messages within queues or subscriptions become expired or no longer relevant, necessitating a cleanup. For more information, see Batch delete.

### Security

Service Bus supports security protocols such as Shared Access Signatures (SAS), Role Based Access Control (RBAC), and Managed identities for Azure resources.

Service Bus supports standard Advanced Message Queuing Protocol (AMQP) 1.0 and HTTP/REST protocols.

### Geo-Replication

When Azure regions or datacenters experience downtime, Geo-Replication enables data processing to continue operating in a different region.

Note

For more information about these features, see Advanced features of Azure Service Bus.

## Compliance with standards and protocols

The primary wire protocol for Service Bus is Advanced Messaging Queueing Protocol (AMQP) 1.0, an open ISO/IEC standard. It allows customers to write applications that work against Service Bus and on-premises brokers such as ActiveMQ or RabbitMQ. The AMQP protocol guide provides detailed information in case you want to build such an abstraction.

Service Bus Premium is fully compliant with the Java/Jakarta EE Java Message Service (JMS) 2.0 API. And, Service Bus Standard supports the JMS 1.1 subset focused on queues. JMS is a common abstraction for message brokers and integrates with many applications and frameworks, including the popular Spring framework. To switch from other brokers to Azure Service Bus, you just need to recreate the topology of queues and topics, and change the client provider dependencies and configuration. For an example, see the ActiveMQ migration guide.

## Client libraries

Fully supported Service Bus client libraries are available via the Azure SDK.

- Azure Service Bus for .NET

- Third-party frameworks providing higher-level abstractions built on top of the SDK include NServiceBus and MassTransit.

- Azure Service Bus libraries for Java

- Azure Service Bus provider for Java JMS 2.0

- Azure Service Bus modules for JavaScript and TypeScript

- Azure Service Bus libraries for Python

Azure Service Bus' primary protocol is AMQP 1.0 and it can be used from any AMQP 1.0 compliant protocol client. Several open-source AMQP clients have samples that explicitly demonstrate Service Bus interoperability. Review the AMQP 1.0 protocol guide to understand how to use Service Bus features with AMQP 1.0 clients directly.

Language
Library

Java
Apache Qpid Proton-J

C/C++
Azure uAMQP C, Apache Qpid Proton-C

Python
Apache Qpid Proton Python

Ruby
Apache Qpid Proton Ruby

Go
Azure Go AMQP, Apache Qpid Proton Go

C#/F#/VB
AMQP .NET Lite, Apache NMS AMQP

JavaScript/Node
Rhea

## Integration

Service Bus fully integrates with many Microsoft and Azure services, such as:

- Event Grid

- Logic Apps

- Azure Functions

- Power Platform

- Dynamics 365

- Azure Stream Analytics

## Next steps

To get started using Service Bus messaging, see the following articles:

- Service Bus queues, topics, and subscriptions

- Quickstarts: .NET, Java, JMS 2.0, or NServiceBus

- Service Bus pricing.

- Premium Messaging.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-03-13
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
