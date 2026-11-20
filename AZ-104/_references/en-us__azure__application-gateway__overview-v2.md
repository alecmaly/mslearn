# https://learn.microsoft.com/en-us/azure/application-gateway/overview-v2

Source: https://learn.microsoft.com/en-us/azure/application-gateway/overview-v2

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
 

 

 

 

 
 
# What is Azure Application Gateway v2?

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Application Gateway v2 is the latest version of Application Gateway. It provides advantages over Application Gateway v1 such as performance enhancements, autoscaling, zone redundancy, and static VIPs.

Important

Deprecation of Application Gateway V1 was announced on April 28, 2023. Application Gateway V1 retired on April 28, 2026, and is no longer supported. If you still use the Application Gateway V1 SKU, migrate to Application Gateway v2 now. For answers to common migration questions, see the V1 retirement FAQ.

## Key capabilities

The v2 SKU includes the following enhancements. Availability depends on the SKU type: Basic, Standard_v2, or WAF_v2. This section explains what each capability does. For per-SKU availability, see the Basic and Standard_v2 comparison in SKU types, and see Feature comparison between v1 SKU and v2 SKU for the authoritative v1 and v2 feature inventory.

- TCP/TLS proxy: Azure Application Gateway now also supports Layer 4 (TCP protocol) and TLS (Transport Layer Security) proxying. This capability isn't available in the Basic SKU. For more information, see Application Gateway TCP/TLS proxy overview.

- Autoscaling: Application Gateway or WAF deployments under the autoscaling SKU can scale out or in based on changing traffic load patterns. Autoscaling also removes the requirement to choose a deployment size or instance count during provisioning. This SKU offers true elasticity. In the Standard_v2 and WAF_v2 SKU, Application Gateway can operate both in fixed capacity (autoscaling disabled) and in autoscaling enabled mode. Fixed capacity mode is useful for scenarios with consistent and predictable workloads. Autoscaling mode is beneficial in applications that see variance in application traffic.

- Zone redundancy: Application Gateway or WAF deployments span multiple Availability Zones by default, removing the need to provision separate Application Gateway instances in each zone with a Traffic Manager. Application Gateway instances are deployed (by default) in a minimum of two availability zones, which makes it more resilient to zone failure. The backend pool for applications can be similarly distributed across availability zones.

Zone redundancy is available only where Azure availability zones are available. In other regions, all other features are supported. For more information, see Azure regions with availability zone support.

- Static VIP: Application Gateway v2 SKU supports the static VIP type exclusively. Static VIP ensures that the VIP associated with the application gateway doesn't change for the lifecycle of the deployment, even after a restart. You must use the application gateway URL for domain name routing to App Services via the application gateway, as v1 doesn't have a static VIP.

- Header Rewrite: Application Gateway allows you to add, remove, or update HTTP request and response headers with v2 SKU. For more information, see Rewrite HTTP headers with Application Gateway

- Key Vault Integration: Application Gateway v2 supports integration with Key Vault for server certificates that are attached to HTTPS enabled listeners. For more information, see TLS termination with Key Vault certificates.

- Mutual Authentication (mTLS): Application Gateway v2 supports authentication of client requests. This capability isn't available in the Basic SKU. For more information, see Overview of mutual authentication with Application Gateway.

- Azure Kubernetes Service Ingress Controller: The Application Gateway v2 Ingress Controller allows the Azure Application Gateway to be used as the ingress for an Azure Kubernetes Service (AKS) known as AKS Cluster. This capability isn't available in the Basic SKU. For more information, see What is Application Gateway Ingress Controller.

- Private link: The v2 SKU offers private connectivity from other virtual networks in other regions and subscriptions by using private endpoints. This capability isn't available in the Basic SKU.

- Performance enhancements: The v2 SKU offers up to 5X better TLS offload performance as compared to the Standard/WAF SKU.

- Faster deployment and update time: The v2 SKU provides faster deployment and update time as compared to Standard/WAF SKU. The faster time also includes WAF configuration changes.

## SKU types

Application Gateway v2 is available in three SKUs: Basic, Standard_v2, and WAF_v2.

- Basic (preview): The Basic SKU is designed for applications that have lower traffic and SLA requirements, and don't need advanced traffic management features. Register for the Basic SKU preview.

- Standard_v2: The Standard_v2 SKU is designed for running production workloads and high traffic. It includes autoscaling, which can automatically adjust the number of instances to match your traffic needs.

- WAF_v2: The WAF_v2 SKU adds Azure Web Application Firewall protection, which inspects the entire request to detect and block threats.

The following table compares only the Basic and Standard_v2 SKUs. It doesn't include WAF_v2. For the features available in the v2 SKUs overall, see Feature comparison between v1 SKU and v2 SKU.

Feature
Capabilities
Basic SKU (preview)
Standard_v2 SKU

Reliability
SLA
99.9
99.95

Functionality - basic
HTTP/HTTP2/HTTPS
WebSocket
Public/Private IP
Cookie Affinity
Path-based affinity
Wildcard
Multisite
KeyVault
Zone
Header rewrite
â
â
â
â
â
â
â
â
â
â
â
â
â
â
â
â
â
â
â
â

Functionality - advanced
AKS (via AGIC)
URL rewrite
mTLS
Private Link
Private-only
TCP/TLS Proxy

â
â
â
â
â
â

Scale
Max. connections per second
Number of listeners
Number of backend pools
Number of backend servers per pool
Number of rules
2001
5
5
5
5
625001
100
100
1200
400

Capacity Unit
Connections per second per compute unit
Throughput
Persistent new connections
10
2.22 Mbps
2500
50
2.22 Mbps
2500

1Estimated based on using an RSA 2048-bit key TLS certificate.

## Pricing

With the v2 SKU, consumption drives the pricing model and isn't tied to instance counts or sizes. To learn more, see Understanding pricing.

## Unsupported regions

Currently, the Standard_v2 and WAF_v2 SKUs aren't available in the following regions:

- China East

- China North

- US DOD East

- US DOD Central

## Migrate from v1 to v2

An Azure PowerShell script is available in the PowerShell gallery to help you migrate from your v1 Application Gateway/WAF to the v2 Autoscaling SKU. This script helps you copy the configuration from your v1 gateway. You're still responsible for traffic migration. For more information, see Migrate Azure Application Gateway from v1 to v2.

### Feature comparison between v1 SKU and v2 SKU

The following table shows the features available with each SKU.

Feature
v1 SKU
v2 SKU

Autoscaling

â

Zone redundancy

â

Static VIP

â

Azure Kubernetes Service (AKS) Ingress controller

â

Azure Key Vault integration

â

Rewrite HTTP(S) headers

â

Enhanced Network Control (NSG, Route Table, Private IP Frontend only)

â

URL-based routing
â
â

Multiple-site hosting
â
â

Mutual Authentication (mTLS)

â

Private Link support

â

Traffic redirection
â
â

Web Application Firewall (WAF)
â
â

WAF custom rules

â

WAF policy associations

â

Transport Layer Security (TLS)/Secure Sockets Layer (SSL) termination
â
â

End-to-end TLS encryption
â
â

Keyless TLS

â

Session affinity
â
â

Custom error pages
â
â

WebSocket support
â
â

HTTP/2 support
â
â

Connection draining
â
â

Proxy NTLM authentication
â
â

Path based rule encoding
â

DHE Ciphers
â

Note

The autoscaling v2 SKU now supports default health probes to automatically monitor the health of all resources in its backend pool and highlight those backend members that are considered unhealthy. The default health probe is automatically configured for backends that don't have any custom probe configuration. To learn more, see health probes in application gateway.

### Differences from the v1 SKU

This section describes features and limitations of the v2 SKU that differ from the v1 SKU.

Difference
Details

Mixing Standard_v2 and Standard Application Gateway on the same subnet
Not supported

User-Defined Route (UDR) on Application Gateway subnet
For information about supported scenarios, see Application Gateway configuration overview.

NSG for Inbound port range
- 65200 to 65535 for Standard_v2 SKU
- 65503 to 65534 for Standard SKU.
Not required for v2 SKUs in private deployment Learn more.
For more information, see the FAQ.

Performance logs in Azure diagnostics
Not supported.
Use Azure metrics.

FIPS mode
Currently not supported.

Path based rule encoding
Not supported.
 V2 decodes paths before routing. For example, V2 treats `/abc%2Fdef` the same as `/abc/def`.

Chunked file transfer
In the Standard_v2 configuration, turn off request buffering to support chunked file transfer. 
 In WAF_v2, turning off request buffering isn't possible because it has to look at the entire request to detect and block any threats. Therefore, the suggested alternative is to create a path rule for the affected URL and attach a disabled WAF policy to that path rule.

Cookie Affinity
Current V2 doesn't support appending the domain in session affinity Set-Cookie, which means that clients of the subdomains can't use the cookie.

Microsoft Defender for Cloud integration
Not yet available.

## Register for the preview

Run the following Azure PowerShell commands to register for the preview of Application Gateway Basic SKU.

`Set-AzContext -Subscription "<your subscription ID>"
Get-AzProviderFeature -FeatureName AllowApplicationGatewayBasicSku -ProviderNamespace "Microsoft.Network"
Register-AzProviderFeature -FeatureName AllowApplicationGatewayBasicSku -ProviderNamespace Microsoft.Network 
`

## Unregister the preview

To unregister from the public preview of Basic SKU:

- Delete all instances of Application Gateway Basic SKU from your subscription.

- Run the following Azure PowerShell commands:

`Set-AzContext -Subscription "<your subscription ID>"
Get-AzProviderFeature -FeatureName AllowApplicationGatewayBasicSku -ProviderNamespace "Microsoft.Network"
Unregister-AzProviderFeature -FeatureName AllowApplicationGatewayBasicSku -ProviderNamespace Microsoft.Network 
`

## Next steps

Ready to get started? Choose how you want to create your Application Gateway:

- Create an autoscaling application gateway (tutorial)

- Migrate from Application Gateway v1 to v2

 
 

 
 

 

 
 
 
 
 
 
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
 2026-09-10
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
