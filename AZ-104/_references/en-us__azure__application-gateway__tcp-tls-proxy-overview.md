# https://learn.microsoft.com/en-us/azure/application-gateway/tcp-tls-proxy-overview

Source: https://learn.microsoft.com/en-us/azure/application-gateway/tcp-tls-proxy-overview

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
 

 

 

 

 
 
# Application Gateway TCP/TLS proxy overview

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 In addition to the existing Layer 7 capabilities (HTTP, HTTPS, WebSockets and HTTP/2), Azure Application Gateway now also supports Layer 4 (TCP protocol) and TLS (Transport Layer Security) proxying.

## TLS/TCP proxy capabilities on Application Gateway

As a reverse proxy service, the Layer 4 operations of Application Gateway work similar to its Layer 7 proxy operations. A client establishes a TCP connection with Application Gateway, and Application Gateway itself initiates a new TCP connection to a backend server from the backend pool. The following figure shows typical operation.

Process flow:

- A client initiates a TCP or TLS connection with the application gateway using its frontend listener's IP address and port number. This establishes the frontend connection. Once the connection is established, the client sends a request using the required application layer protocol.

- The application gateway establishes a new connection with one of the backend targets from the associated backend pool (forming the backend connection) and sends the client request to that backend server.

- The response from the backend server is sent back to the client by the application gateway.

- The same frontend TCP connection is used for subsequent requests from the client unless the TCP idle timeout closes that connection.

### Comparing Azure Load Balancer with Azure Application Gateway:

Product
Type

Azure Load Balancer
A pass-through load balancer where a client directly establishes a connection with a backend server selected by the Load Balancer's distribution algorithm.

Azure Application Gateway
Terminating load balancer where a client directly establishes a connection with Application Gateway and a separate connection is initiated with a backend server selected by Application Gateway's distribution algorithm.

#### Azure Application Gateway (TLS/TCP proxy)

- Type â Layer-4 terminating proxy.

- Protocols â Supports TCP or TLS protocols.

- Versatility â Use a single endpoint (frontend IP) to serve HTTP and non-HTTP workloads.

- Scaling â Configure autoscaling (up to 125 instances) to serve your TCP and TLS traffic.

- Security through TLS termination â Simplify security with centralized TLS termination and certificate management ensuring consistent compliance across all applications, including non-HTTP workloads. Seamlessly integrates with Azure Key Vault for secure certificate management.

- Backend types â Flexibly connect your applications to backends anywhere; within the same Virtual Network, across peered VNets, through remote FQDNs or IPs, or even via hybrid connectivity to your on-premises servers.

#### Azure Load Balancer

- Type â Layer-4 pass-through network device.

- Protocols â Supports TCP or UDP protocols.

- Performance â Provides low latency and high throughput. Built for millions of simultaneous connections with microsecond-level latency.

- Scaling â Handles long-lived connections and scales up to millions of flows for all TCP and UDP applications.

- Inbound and outbound â Azure Load Balancer delivers complete traffic control with both inbound and outbound capabilities. Seamlessly connect external clients to your applications, while enabling your backend instances to securely reach the internet and other services.

- Direct server return - For the return traffic, the backend instance sends the response packet directly back to the client's IP address, reducing latency and improving performance.

## Features

- Use a single endpoint (frontend IP) to serve HTTP and non-HTTP workloads. The same application gateway deployment can support Layer 7 and Layer 4 protocols: HTTP(S), TCP, or TLS. All your clients can connect to the same endpoint and access different backend applications.

- Use a custom domain to front any backend service. With the frontend for the Application Gateway V2 SKU as public and private IP addresses, you can configure any custom domain name to point its IP address using an address (A) record. Additionally, with TLS termination and support for certificates from a private certification authority (CA), you can ensure a secure connection on the domain of your choice.

- Use a backend server from any location (Azure or On-premises). The backends for the application gateway can be:

- Azure resources such as IaaS virtual machines, virtual machine scale sets, or PaaS (App Services, Event Hubs, SQL)

- Remote resources such as on-premises servers accessible via FQDN or IP addresses

- Supported for a private-only gateway. With TLS and TCP proxy support for private Application Gateway deployments, you can support HTTP and non-HTTP clients in an isolated environment for enhanced security.

## Limitations

- A WAF v2 SKU gateway allows the creation of TLS or TCP listeners and backends to support HTTP and non-HTTP traffic through the same resource. However, it does not inspect traffic on TLS and TCP listeners for exploits and vulnerabilities.

- The default draining timeout value for backend servers is 30 seconds. At present, a user-defined draining value is not supported.

- A configuration update (PUT) on Application Gateway ends the active connections after the default draining timeout period.

- Application Gateway Ingress Controller (AGIC) is not supported and works only with L7 proxy through HTTP(S) listeners.

## Next steps

- Configure Azure Application Gateway TCP/TLS proxy

- Visit frequently asked questions (FAQs)

 
 

 
 

 

 
 
 
 
 
 
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
 2025-11-26
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
