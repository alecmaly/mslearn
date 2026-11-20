# https://learn.microsoft.com/en-us/azure/api-management/api-management-key-concepts

Source: https://learn.microsoft.com/en-us/azure/api-management/api-management-key-concepts

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
 

 

 

 

 
 
# What is Azure API Management?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 APPLIES TO: All API Management tiers

This article provides an overview of common scenarios and key components of Azure API Management. Azure API Management is a hybrid, multicloud management platform for APIs across all environments. As a platform-as-a-service, API Management supports the complete API lifecycle.

Tip

If you're already familiar with API Management and ready to start, see these resources:

- Features and service tiers

- Create an API Management instance

- Import and publish an API

- API Management policies

## Scenarios

APIs enable digital experiences, simplify application integration, underpin new digital products, and make data and services reusable and universally accessible. âWith the proliferation and increasing dependency on APIs, organizations need to manage them as first-class assets throughout their lifecycle.â

Azure API Management helps organizations meet these challenges:

- Provide a comprehensive API platform for different stakeholders and teams to produce and manage APIs

- Abstract backend architecture diversity and complexity from API consumers

- Securely expose services hosted on and outside of Azure as APIs

- Protect, accelerate, and observe APIs

- Enable API discovery and consumption by internal and external users

Common scenarios include:

- Unlocking legacy assets - APIs are used to abstract and modernize legacy backends and make them accessible from new cloud services and modern applications. APIs allow innovation without the risk, cost, and delays of migration.

- API-centric app integration - APIs are easily consumable, standards-based, and self-describing mechanisms for exposing and accessing data, applications, and processes. They simplify and reduce the cost of app integration.

- Multi-channel user experiences - APIs are frequently used to enable user experiences such as web, mobile, wearable, or Internet of Things applications. Reuse APIs to accelerate development and ROI.

- B2B integration - APIs exposed to partners and customers lower the barrier to integrate business processes and exchange data between business entities. APIs eliminate the overhead inherent in point-to-point integration. Especially with self-service discovery and onboarding enabled, APIs are the primary tools for scaling B2B integration.

Tip

Visit aka.ms/apimlove for a library of useful resources, including videos, blogs, and customer stories about using Azure API Management.

## API Management components

Azure API Management is made up of an API gateway, a management plane, and a developer portal, with features designed for different audiences in the API ecosystem. These components are Azure-hosted and fully managed by default. API Management is available in various tiers differing in capacity and features.

## API gateway

All requests from client applications first reach the API gateway (also called data plane or runtime), which then forwards them to respective backend services. The API gateway acts as a facade to the backend services, allowing API providers to abstract API implementations and evolve backend architecture without impacting API consumers. The gateway enables consistent configuration of routing, security, throttling, caching, and observability.

Specifically, the gateway:

- Acts as a facade to backend services by accepting API calls and routing them to appropriate backends

- Verifies API keys and other credentials such as JWTs and certificates presented with requests

- Enforces usage quotas and rate limits

- Optionally transforms requests and responses as specified in policy statements

- If configured, caches responses to improve response latency and minimize the load on backend services

- Emits logs, metrics, and traces for monitoring, reporting, and troubleshooting

### Self-hosted gateway

With the self-hosted gateway, an API provider can deploy the API gateway to the same environments where they host their APIs, to optimize API traffic and ensure compliance with local regulations and guidelines. The self-hosted gateway enables organizations with hybrid IT infrastructure to manage APIs hosted on-premises and across clouds from a single API Management service in Azure.

The self-hosted gateway is packaged as a Linux-based Docker container and is commonly deployed to Kubernetes, including to Azure Kubernetes Service and Azure Arc-enabled Kubernetes.

More information:

- API gateway in Azure API Management

## Management plane

API providers interact with the service through the management plane (also called control plane), which provides full access to the API Management service capabilities.

Customers interact with the management plane through Azure tools that include the Azure portal, Azure PowerShell, Azure CLI, a Visual Studio Code extension, and a REST API. Or they can interact through client SDKs in several popular programming languages.

Use the management plane to:

- Provision and configure API Management service settings.

- Define or import API schemas from a wide range of sources. Including, OpenAPI, WSDL, OData definitions, Azure compute services, WebSocket, GraphQL, and gRPC backends.

- Package APIs into products.

- Set up policies like quotas or transformations on the APIs.

- Get insights from analytics.

- Manage users such as app developers.

## Developer portal

The open-source developer portal is an automatically generated, fully customizable website with the documentation of your APIs.

API providers can customize the look and feel of the developer portal by adding custom content, customizing styles, and adding their branding. Extend the developer portal further by self-hosting.

API consumers such as app developers access the open-source developer portal to discover the APIs, onboard to use them, and learn how to consume them in applications. (APIs can also be exported to the Power Platform for discovery and use by citizen developers.)

When they use the developer portal, API consumers can:

- Read API documentation

- Call an API via the interactive console

- Create an account and subscribe to get API keys

- Access analytics on their own usage

- Download API definitions

- Manage API keys

## Federated API management with workspaces

For organizations that want to empower decentralized teams to develop and manage their own APIs with the advantages of centralized API governance and discovery, API Management offers first-class support for a federated API management model with workspaces.

In API Management, workspaces bring a new level of autonomy to an organization's API teams, enabling them to create, manage, and publish APIs faster, more reliably, securely, and productively within an API Management service. By providing isolated administrative access and API runtime, workspaces empower API teams while allowing the API platform team to retain oversight. This includes central monitoring, enforcement of API policies and compliance, and publishing APIs for discovery through a unified developer portal.

More information:

- Workspaces in API Management

## API Management tiers

API Management is offered in various pricing tiers to meet the needs of different customers. Each tier offers a distinct combination of features, performance, capacity limits, scalability, SLA, and pricing for different scenarios. The tiers are grouped as follows:

- Classic - The original API Management offering, including the Developer, Basic, Standard, and Premium tiers. The Premium tier is designed for enterprises that require access to private backends, enhanced security features, multi-region deployments, availability zones, and high scalability. The Developer tier is an economical option for nonproduction use, while the Basic, Standard, and Premium tiers are production-ready tiers.

- V2 - A new set of tiers that offer fast provisioning and scaling, including Basic v2 for development and testing, and Standard v2 and Premium v2 for production workloads. Standard v2 and Premium v2 support virtual network integration for simplified connection to network-isolated backends. Premium v2 also supports virtual network injection for full isolation of network traffic to and from the gateway.

- Consumption - A serverless gateway for managing APIs that scales based on demand and bills per execution. This tier is designed for applications with serverless compute, microservices-based architectures, and variable traffic patterns.

More information:

- Feature-based comparison of the Azure API Management tiers

- V2 service tiers

- Understanding API Management limits

- API Management pricing

## Integration with Microsoft services

API Management integrates with many complementary Microsoft and Azure services to create enterprise solutions, including:

- Azure API Center to build a complete inventory of APIsâ in the organization - regardless of their type, lifecycle stage, or deployment locationâ - for API discovery, reuse, and governance

- Azure Copilot to help author API Management policies or explain already configured policiesâ

- Microsoft Foundry to govern AI model endpoints deployed in Microsoft Foundry as APIs.

- Azure Key Vault for secure safekeeping and management of client certificates and secretsâ

- Azure Monitor for logging, reporting, and alerting on management operations, systems events, and API requestsâ

- Application Insights for live metrics, end-to-end tracing, and troubleshooting

- Virtual networks, private endpoints, Application Gateway, and Azure Front Door for network-level protectionâ

- Microsoft Defender for APIs and Azure DDoS Protection for runtime protection against malicious attacksâ

- Microsoft Entra ID for developer authentication and request authorizationâ

- Event Hubs for streaming eventsâ

- Azure Redis for caching responsesâ with Azure Cache for Redis or Azure Managed Redisâ

- Several Azure compute offerings commonly used to build and host APIs on Azure, including Functions, Logic Apps, Web Apps, Service Fabric, and others.â

- Azure database offerings, including Azure Cosmos DB, enabling direct CRUD (Create, Read, Update, Delete) operations without requiring intermediate compute resources.

More information:

- Basic enterprise integration

- Landing zone accelerator

- AI gateway capabilities in API Management

- Synchronize APIs to API Center from API Management

## Key concepts

### APIs

APIs are the foundation of an API Management service instance. Each API represents a set of operations available to app developers. Each API contains a reference to the backend service that implements the API, and its operations map to backend operations.

Operations in API Management are highly configurable. You have control over URL mapping, query and path parameters, request and response content, and operation response caching.

More information:

- Import and publish your first API

- Mock API responses

### Products

Products are how APIs are surfaced to API consumers such as app developers. Products in API Management have one or more APIs and can be open or protected. Protected products require a subscription key, while open products can be consumed freely.

When a product is ready for use by consumers, it can be published. Once published, it can be viewed or subscribed to by users through the developer portal. Subscription approval is configured at the product level and can either require an administrator's approval or be automatic.

More information:

- Create and publish a product

- Subscriptions in API Management

### Users and groups

Users (API consumers) can be created or invited to join by service administrators, or they can sign up from the developer portal. Each user is a member of one or more groups, and can subscribe to the products that grant visibility to those groups.

API Management has the following built-in groups:

- Developers - Authenticated developer portal users that build applications using your APIs. Developers are granted access to the developer portal and build applications that call the operations of an API.

- Guests - Unauthenticated developer portal users, such as prospective customers visiting the developer portal. They can be granted certain read-only access, such as the ability to view APIs but not call them.

API Management service owners can also create custom groups or use external groups in an associated Microsoft Entra tenant to give users visibility and access to API products. For example, create a custom group for developers in a partner organization to access a specific subset of APIs in a product. A user can belong to more than one group.

More information:

- How to create and use groups

- How to manage user accounts

### Workspaces

Workspaces support a federated API management model by allowing decentralized API development teams to manage and productize their own APIs, while a central API platform team maintains the API Management infrastructure. Each workspace contains APIs, products, subscriptions, and related entities that are accessible only to the workspace collaborators. Access is controlled through Azure role-based access control (RBAC). Depending on the service tier, each workspace routes API traffic through either the service's default managed gateway and/or one or more separate workspace gateways.

More information:

- Workspaces in API Management

### Policies

With policies, an API provider can change the behavior of an API through configuration. Policies are a collection of statements that are executed sequentially on the request or response of an API. Popular statements include format conversion from XML to JSON and call-rate limiting to restrict the number of incoming calls from a developer. For a complete list, see API Management policies.

Policy expressions can be used as attribute values or text values in many of the API Management policies. Some policies such as the Control flow and Set variable policies are based on policy expressions.

Policies can be applied at different scopes, depending on your needs: global (all APIs), a workspace, a product, a specific API, or an API operation.

More information:

- Transform and protect your API.

- Policy expressions

## Next steps

Complete the following quickstart and start using Azure API Management:

Create an Azure API Management instance by using the Azure portal

 
 

 
 

 

 
 
 
 
 
 
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
 2025-10-13
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
