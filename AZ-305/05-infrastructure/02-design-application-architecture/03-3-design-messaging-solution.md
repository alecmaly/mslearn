# Unit 3: 3-design-messaging-solution

Source: https://learn.microsoft.com/en-us/training/modules/design-application-architecture/3-design-messaging-solution

---

unit-inner-section" class="section is-uniform position-relative">
 
# Design a messaging solution

 
 
 
 Completed
 
 
 

 

 
 
- 8 minutes

 
 

 

 
 Azure offers two message-based solutions, Azure Queue Storage and Azure Service Bus. Queue Storage stores large numbers of messages in Azure Storage. Service Bus is a message broker that decouples applications and services. We examine the different features and capabilities of these services and consider how to choose which service to implement.

One of your design tasks for Tailwind Traders is to recommend a design for their product demo application. Customers use the app to get the latest tips, reviews, and instructions for featured home improvement products. You have two requirements for the app design:

- Ensure all content files are uploaded to the web API reliably from the mobile app. Files include text, images, and video.

- Deliver details about new files directly to the app, such as when a customer posts a new product review or a video is added.

For these app requirements, the ideal solution is a message-based system. This video from the Developer course explains the different message queue solutions.

### Things to know about Azure Queue Storage

Azure Queue Storage is a service that uses Azure Storage to store large numbers of messages. Examine the following characteristics of the service.

- Queues in Azure Queue Storage can contain millions of messages.

- The number and size of queues is limited only by the capacity of the Azure storage account that owns the Queue Storage.

- Messages in Queue Storage can be securely accessed from anywhere in the world by using a simple REST-based interface.

- Queues generally provide increased reliability, guaranteed message delivery, and transactional support.

### Things to know about Azure Service Bus

Azure Service Bus is a fully managed enterprise message broker. Service Bus is used to decouple applications and services from each other. Review the following benefits characteristics of the service.

- Azure Service Bus supports message queues and publish-subscribe topics.

- Azure Service Bus lets you load-balance work across competing workers.

- You can use Service Bus to safely route and transfer data and control across service and application boundaries.

- Service Bus helps you coordinate transactional work that requires a high degree of reliability.

#### Message queues

Azure Service Bus message queues is a message broker system built on top of a dedicated messaging infrastructure. Like Azure queues, Service Bus holds messages until the target is ready to receive them.

Azure Service Bus message queues are intended for enterprise applications, such as an app that uses communication protocols and different data contracts.

#### Business scenario

Consider the scenario where a customer is watching a video on an app. The app supports both user history and fan lists. You can support both actions by using publish-subscribe topic attributes:

- The mobile app sends a message to the `Watched` topic.

- The topic has two subscriptions. The first subscription completes the `UpdateUserWatchHistory` action. A second subscription completes the `UpdateProductFanList` action.

- Each subscription for the `Watched` topic receives its own copy of the message.

### Things to consider when choosing messaging services

Each Azure messaging solution has a slightly different set of features and capabilities. You can choose one solution or use both to fulfill your design requirements. Review the following scenarios, and think about which messaging solutions can benefit the Tailwind Traders application architecture.

Messaging solution
Example scenarios

Azure Queue Storage
You want a simple queue to organize messages.

 You need an audit trail of all messages that pass through the queue.

 The queue storage exceeds 80 GB.

 You'd like to track progress for processing a message inside of the queue.

Azure Service Bus 
 message queues
You require an at-most-once delivery guarantee.

 You require at-least-once message processing (PeekLock receive mode).

 You require at-most-once message processing (ReceiveAndDelete receive mode).

 You want to group messages into transactions.

 You want to receive messages without polling the queue.

 You need to handle messages larger than 64 KB.

 The queue storage doesn't exceed 80 GB.

 You'd like to publish and consume batches of messages.

Azure Service Bus 
 publish-subscribe topics
You need multiple receivers to handle each message.

 You expect multiple destinations for a single message but need queue-like behavior.

Tip

Continue your learning with the Discover Azure message queues module.

 

 
 

 

 
 
 
 <section
