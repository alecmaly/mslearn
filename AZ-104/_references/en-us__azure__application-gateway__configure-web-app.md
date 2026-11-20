# https://learn.microsoft.com/en-us/azure/application-gateway/configure-web-app

Source: https://learn.microsoft.com/en-us/azure/application-gateway/configure-web-app

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
 

 

 

 

 
 
# Configure App Service with Application Gateway

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 
Azure Application Gateway allows you to have an App Service app or other multitenant service as a backend pool member. In this article, you learn to configure an App Service app with Application Gateway. The configuration for Application Gateway differs depending on how App Service can be accessed:

- The first option makes use of a custom domain on both Application Gateway and the App Service in the backend.

- The second option is to have Application Gateway access App Service using its default domain, suffixed as ".azurewebsite.net."

- 
Custom domain (recommended)

- 
Default domain

This configuration is recommended for production-grade scenarios and meets the practice of not changing the host name in the request flow. You're required to have a custom domain (and associated certificate) available to avoid having to rely on the default ".Azurewebsite" domain.

The same domain name to both Application Gateway and App Service in the backend pool, the request flow doesn't need to override the host name. The backend web application sees the original host as was used by the client.

This configuration is the easiest and doesn't require a custom domain. As such it allows for a quick convenient setup.

Warning

This configuration comes with limitations. We recommend reviewing the implications of using different host names between the client and Application Gateway and between Application and App Service in the backend. For more information, please review the article in Architecture Center: Preserve the original HTTP host name between a reverse proxy and its backend web application

When App Service doesn't have a custom domain associated with it: the host header on the incoming request on the web application needs to be set to the default domain, suffixed with ".azurewebsites.net" or else the platform won't able to properly route the request.

The host header in the original request received by the Application Gateway is different from the host name of the backend App Service.

In this article you learn how to:

- Configure DNS

- Add App Service as backend pool to the Application Gateway

- Configure HTTP Settings for the connection to App Service

- Configure an HTTP Listener

- Configure a Request Routing Rule

## Prerequisites

- 
Custom domain (recommended)

- 
Default domain

- Application Gateway: Create an application gateway without a backend pool target. For more information, see Quickstart: Direct web traffic with Azure Application Gateway - Azure portal

- App Service: If you don't have an existing App Service, see App Service documentation.

- A custom domain name and associated certificate (signed by a well known authority), stored in Key Vault. For more information on how to store certificates in Key Vault, see Tutorial: Import a certificate in Azure Key Vault

- A custom health probe configured in Application Gateway that uses the custom domain name as its host name. To create a custom health probe, see Create a custom health probe.

- Application Gateway: Create an application gateway without a backend pool target. For more information, see Quickstart: Direct web traffic with Azure Application Gateway - Azure portal

- App Service: If you don't have an existing App Service, see App Service documentation.

## Configuring DNS

In the context of this scenario, DNS is relevant in two places:

- The DNS name, which the user or client is using towards Application Gateway and what is shown in a browser

- The DNS name, which Application Gateway is internally using to access the App Service in the backend

- 
Custom domain (recommended)

- 
Default domain

Route the user or client to Application Gateway using the custom domain. Set up DNS using a CNAME alias pointed to the DNS for Application Gateway. The Application Gateway DNS address is shown on the overview page of the associated Public IP address. Alternatively create an A record pointing to the IP address directly. (For Application Gateway V1 the VIP can change if you stop and start the service, which makes this option undesired.)

App Service should be configured so it accepts traffic from Application Gateway using the custom domain name as the incoming host. For more information on how to map a custom domain to the App Service, see Tutorial: Map an existing custom DNS name to Azure App Service To verify the domain, App Service only requires adding a TXT record. No change is required on CNAME or A-records. The DNS configuration for the custom domain remains directed towards Application Gateway.

To accept connections to App Service over HTTPS, configure its TLS binding. For more information, see Secure a custom DNS name with an TLS/SSL binding in Azure App Service Configure App Service to pull the certificate for the custom domain from Azure Key Vault.

When no custom domain is available, the user or client can access Application Gateway using either the IP address of the gateway or its DNS address. The Application Gateway DNS address can be found on the overview page of the associated Public IP address. Not having a custom domain available implies that no publicly signed certificate isn't available for TLS on Application Gateway. Clients are restricted to use HTTP or HTTPS with a self-signed certificate, both of which are undesired.

To connect to App Service, Application Gateway uses the default domain as provided by App Service (suffixed "azurewebsites.net").

## Add App service as backend pool

- 
Azure portal

- 
PowerShell

- In the Azure portal, select your Application Gateway.

- Under Backend pools, select the backend pool.

- Under Target type, select App Services.

- Under Target select your App Service.

Note

The dropdown only populates those app services that are in the same subscription as your Application Gateway. If you want to use an app service that is in a different subscription than the one in which the Application Gateway is, then instead of choosing App Services in the Targets dropdown, choose IP address or hostname option and enter the hostname (example.azurewebsites.net) of the app service. If you're using private endpoints with your App Service, you should use the private endpoint's FQDN or IP address instead.

- Select Save.

`# Fully qualified default domain name of the web app:
$webAppFQDN = "<nameofwebapp>.azurewebsite.net"

# For Application Gateway: both name, resource group and name for the backend pool to create:
$rgName = "<name of resource group for App Gateway>"
$appGwName = "<name of the App Gateway>"
$appGwBackendPoolNameForAppSvc = "<name for backend pool to be added>"

# Get existing Application Gateway:
$gw = Get-AzApplicationGateway -Name $appGwName -ResourceGroupName $rgName

# Add a new Backend Pool with App Service in there:
Add-AzApplicationGatewayBackendAddressPool -Name $appGwBackendPoolNameForAppSvc -ApplicationGateway $gw -BackendFqdns $webAppFQDN

# Update Application Gateway with the new added Backend Pool:
Set-AzApplicationGateway -ApplicationGateway $gw
`

## Edit HTTP settings for App Service

- 
Azure portal

- 
Azure portal

- 
PowerShell

- 
PowerShell

An HTTP Setting is required that instructs Application Gateway to access the App Service backend using the custom domain name. The HTTP Setting is by default use the default health probe. While default health probes forward requests with the hostname in which traffic is received, the health probes can utilize 127.0.0.1 as the hostname to the Backend Pool since no hostname explicitly been defined. For this reason, we need to create a custom health probe that is configured with the correct custom domain name as its host name.

We connect to the backend using HTTPS.

- Under HTTP Settings, select an existing HTTP setting or add a new one.

- When creating a new HTTP Setting, give it a name

- Select HTTPS as the desired backend protocol using port 443

- If the certificate is signed by a well known authority, select "Yes" for "User well known CA certificate." Alternatively Add authentication/trusted root certificates of backend servers

- Make sure to set "Override with new host name" to "No"

- Select the custom HTTPS health probe in the dropdown for "Custom probe."

An HTTP Setting is required that instructs Application Gateway to access the App Service backend using the default ("azurewebsites.net") domain name. To do so, the HTTP Setting will explicitly override the host name.

- Under HTTP Settings, select an existing HTTP setting or add a new one.

- When creating a new HTTP Setting, give it a name

- Select HTTPS as the desired backend protocol using port 443

- If the certificate is signed by a well known authority, select "Yes" for "User well known CA certificate". Alternatively Add authentication/trusted root certificates of backend servers

- Make sure to set "Override with new host name" to "Yes"

- Under "Host name override," select "Pick host name from backend target". This setting causes the request towards App Service to use the "azurewebsites.net" host name, as is configured in the Backend Pool.

`# Configure Application Gateway to connect to App Service using the incoming hostname
$rgName = "<name of resource group for App Gateway>"
$appGwName = "<name of the App Gateway>"
$customProbeName = "<name for custom health probe>"
$customDomainName = "<FQDN for custom domain associated with App Service>"
$httpSettingsName = "<name for http settings to be created>"

# Get existing Application Gateway:
$gw = Get-AzApplicationGateway -Name $appGwName -ResourceGroupName $rgName

# Add custom health probe using custom domain name:
Add-AzApplicationGatewayProbeConfig -Name $customProbeName -ApplicationGateway $gw -Protocol Https -HostName $customDomainName -Path "/" -Interval 30 -Timeout 120 -UnhealthyThreshold 3
$probe = Get-AzApplicationGatewayProbeConfig -Name $customProbeName -ApplicationGateway $gw

# Add HTTP Settings to use towards App Service:
Add-AzApplicationGatewayBackendHttpSettings -Name $httpSettingsName -ApplicationGateway $gw -Protocol Https -Port 443 -Probe $probe -CookieBasedAffinity Disabled -RequestTimeout 30

# Update Application Gateway with the new added HTTP settings and probe:
Set-AzApplicationGateway -ApplicationGateway $gw
`

`# Configure Application Gateway to connect to backend using default App Service hostname
$rgName = "<name of resource group for App Gateway>"
$appGwName = "<name of the App Gateway>"
$httpSettingsName = "<name for http settings to be created>"

# Get existing Application Gateway:
$gw = Get-AzApplicationGateway -Name $appGwName -ResourceGroupName $rgName

# Add HTTP Settings to use towards App Service:
Add-AzApplicationGatewayBackendHttpSettings -Name $httpSettingsName -ApplicationGateway $gw -Protocol Https -Port 443 -PickHostNameFromBackendAddress -CookieBasedAffinity Disabled -RequestTimeout 30

# Update Application Gateway with the new added HTTP settings and probe:
Set-AzApplicationGateway -ApplicationGateway $gw
`

## Configure an HTTP listener

To accept traffic, we need to configure a Listener. For more info on Listener, see Application Gateway listener configuration.

- 
Azure portal

- 
Azure portal

- 
PowerShell

- 
PowerShell

- Open the "Listeners" section and choose "Add listener" or select an existing one to edit

- For a new listener: give it a name

- Under "Frontend IP," select the IP address to listen on

- Under "Port," select 443

- Under "Protocol," select "HTTPS"

- Under "Choose a certificate," select "Choose a certificate from Key Vault." For more information, see Using Key Vault where you find more information on how to assign a managed identity and provide it with rights to your Key Vault.

- Give the certificate a name

- Select the Managed Identity

- Select the Key Vault from where to get the certificate

- Select the certificate

- Under "Listener Type," select "Basic"

- Select "Add" to add the listener

Assuming there's no custom domain available or associated certificate, configure Application Gateway to listen for HTTP traffic on port 80. Alternatively, see the instructions on how to Create a self-signed certificate

- Open the "Listeners" section and choose "Add listener" or select an existing one to edit

- For a new listener: give it a name

- Under "Frontend IP," select the IP address to listen on

- Under "Port," select 80

- Under "Protocol," select "HTTP"

`# This script assumes that:
# - a certificate was imported in Azure Key Vault already
# - a managed identity was assigned to Application Gateway with access to the certificate
# - there is no HTTP listener defined yet for HTTPS on port 443

$rgName = "<name of resource group for App Gateway>"
$appGwName = "<name of the App Gateway>"
$appGwSSLCertificateName = "<name for ssl cert to be created within Application Gateway"
$appGwSSLCertificateKeyVaultSecretId = "<key vault secret id for the SSL certificate to use>"
$httpListenerName = "<name for the listener to add>"

# Get existing Application Gateway:
$gw = Get-AzApplicationGateway -Name $appGwName -ResourceGroupName $rgName

# Create SSL certificate object for Application Gateway:
Add-AzApplicationGatewaySslCertificate -Name $appGwSSLCertificateName -ApplicationGateway $gw -KeyVaultSecretId $appGwSSLCertificateKeyVaultSecretId
$sslCert = Get-AzApplicationGatewaySslCertificate -Name $appGwSSLCertificateName -ApplicationGateway $gw

# Fetch public ip associated with Application Gateway:
$ipAddressResourceId = $gw.FrontendIPConfigurations.PublicIPAddress.Id
$ipAddressResource = Get-AzResource -ResourceId $ipAddressResourceId
$publicIp = Get-AzPublicIpAddress -ResourceGroupName $ipAddressResource.ResourceGroupName -Name $ipAddressResource.Name

$frontendIpConfig = $gw.FrontendIpConfigurations | Where-Object {$_.PublicIpAddress -ne $null}

$port = New-AzApplicationGatewayFrontendPort -Name "port_443" -Port 443
Add-AzApplicationGatewayFrontendPort -Name "port_443" -ApplicationGateway $gw -Port 443
Add-AzApplicationGatewayHttpListener -Name $httpListenerName -ApplicationGateway $gw -Protocol Https -FrontendIPConfiguration $frontendIpConfig -FrontendPort $port -SslCertificate $sslCert

# Update Application Gateway with the new HTTPS listener:
Set-AzApplicationGateway -ApplicationGateway $gw

`

In many cases, a public listener for HTTP on port 80 exists. The below script creates one if that isn't yet the case.

`$rgName = "<name of resource group for App Gateway>"
$appGwName = "<name of the App Gateway>"
$httpListenerName = "<name for the listener to add if not exists yet>"

# Get existing Application Gateway:
$gw = Get-AzApplicationGateway -Name $appGwName -ResourceGroupName $rgName

# Check if HTTP listener on port 80 already exists:
$port = $gw.FrontendPorts | Where-Object {$_.Port -eq 80}
$listener = $gw.HttpListeners | Where-Object {$_.Protocol.ToString().ToLower() -eq "http" -and $_.FrontendPort.Id -eq $port.Id}

if ($listener -eq $null){
 $frontendIpConfig = $gw.FrontendIpConfigurations | Where-Object {$_.PublicIpAddress -ne $null}
 Add-AzApplicationGatewayHttpListener -Name $httpListenerName -ApplicationGateway $gw -Protocol Http -FrontendIPConfiguration $frontendIpConfig -FrontendPort $port

 # Update Application Gateway with the new HTTPS listener:
 Set-AzApplicationGateway -ApplicationGateway $gw
}
`

## Configure request routing rule

The earlier configured Backend Pool and the HTTP Settings, the request routing rule can be set up to take traffic from a listener and route it to the Backend Pool using the HTTP Settings. For this, make sure you have an HTTP or HTTPS listener available that isn't already bound to an existing routing rule.

- 
Azure portal

- 
PowerShell

- Under "Rules", select to add a new "Request routing rule"

- Provide the rule with a name

- Select an HTTP or HTTPS listener that isn't bound yet to an existing routing rule

- Under "Backend targets", choose the Backend Pool in which App Service has been configured

- Configure the HTTP settings with which Application Gateway should connect to the App Service backend

- Select "Add" to save this configuration

`$rgName = "<name of resource group for App Gateway>"
$appGwName = "<name of the App Gateway>"
$httpListenerName = "<name for existing http listener (without rule) to route traffic from>"
$httpSettingsName = "<name for http settings to use>"
$appGwBackendPoolNameForAppSvc = "<name for backend pool to route to>"
$reqRoutingRuleName = "<name for request routing rule to be added>"

# Get existing Application Gateway:
$gw = Get-AzApplicationGateway -Name $appGwName -ResourceGroupName $rgName

# Get HTTP Settings:
$httpListener = Get-AzApplicationGatewayHttpListener -Name $httpListenerName -ApplicationGateway $gw
$httpSettings = Get-AzApplicationGatewayBackendHttpSettings -Name $httpSettingsName -ApplicationGateway $gw
$backendPool = Get-AzApplicationGatewayBackendAddressPool -Name $appGwBackendPoolNameForAppSvc -ApplicationGateway $gw

# Add routing rule:
Add-AzApplicationGatewayRequestRoutingRule -Name $reqRoutingRuleName -ApplicationGateway $gw -RuleType Basic -BackendHttpSettings $httpSettings -HttpListener $httpListener -BackendAddressPool $backendPool

# Update Application Gateway with the new routing rule:
Set-AzApplicationGateway -ApplicationGateway $gw
`

## Testing

Before we do so, make sure that the backend health shows as healthy:

- 
Azure portal

- 
Azure portal

- 
PowerShell

- 
PowerShell

Open the "Backend health" section and ensure the "Status" column indicates the combination for HTTP Setting and Backend Pool shows as "Healthy."

Now browse to the web application using either the Application Gateway IP Address or the associated DNS name for the IP Address. Both can be found on the Application Gateway "Overview" page as a property under "Essentials." Alternatively the Public IP Address resource also shows the IP address and associated DNS name.

Pay attention to the following nonexhaustive list of potential symptoms when testing the application:

- redirections pointing to ".azurewebsite.net" directly instead of to Application Gateway

- includes authentication redirects that try access ".azurewebsite.net" directly

- domain-bound cookies not being passed on to the backend

- include the use of the "ARR affinity" setting in App Service

The above conditions (explained in more detail in Architecture Center) would indicate that your web application doesn't deal well with rewriting the host name. This is commonly seen. The recommended way to deal with this is to follow the instructions for configuration Application Gateway with App Service using a custom domain. Also see: Troubleshoot App Service issues in Application Gateway.

Open the "Backend health" section and ensure the "Status" column indicates the combination for HTTP Setting and Backend Pool shows as "Healthy."

Now browse to the web application using the custom domain which you associated with both Application Gateway and the App Service in the backend.

Check if the backend health for the backend and HTTP Settings shows as "Healthy":

`$rgName = "<name of resource group for App Gateway>"
$appGwName = "<name of the App Gateway>"

# Get existing Application Gateway:
$gw = Get-AzApplicationGateway -Name $appGwName -ResourceGroupName $rgName

# Check health:
Get-AzApplicationGatewayBackendHealth -ResourceGroupName $rgName -Name $appGwName
`

To test the configuration, we request content from the App Service through Application Gateway using the custom domain:

`$customDomainName = "<FQDN for custom domain pointing to Application Gateway>"
Invoke-WebRequest $customDomainName
`

Check if the backend health for the backend and HTTP Settings shows as "Healthy":

`$rgName = "<name of resource group for App Gateway>"
$appGwName = "<name of the App Gateway>"

# Get existing Application Gateway:
$gw = Get-AzApplicationGateway -Name $appGwName -ResourceGroupName $rgName

# Check health:
Get-AzApplicationGatewayBackendHealth -ResourceGroupName $rgName -Name $appGwName
`

To test the configuration, we request content from the App Service through Application Gateway using the IP address:

`$rgName = "<name of resource group for App Gateway>"
$appGwName = "<name of the App Gateway>"

# Get existing Application Gateway:
$gw = Get-AzApplicationGateway -Name $appGwName -ResourceGroupName $rgName

# Get ip address:
$ipAddressResourceId = $gw.FrontendIPConfigurations.PublicIPAddress.Id
$ipAddressResource = Get-AzResource -ResourceId $ipAddressResourceId
$publicIp = Get-AzPublicIpAddress -ResourceGroupName $ipAddressResource.ResourceGroupName -Name $ipAddressResource.Name
Write-Host "Public ip address for Application Gateway is $($publicIp.IpAddress)"
Invoke-WebRequest "http://$($publicIp.IpAddress)"
`

Pay attention to the following nonexhaustive list of potential symptoms when testing the application:

- redirections pointing to ".azurewebsites.net" directly instead of to Application Gateway

- this includes App Service Authentication redirects that try access ".azurewebsites.net" directly

- domain-bound cookies not being passed on to the backend

- this includes the use of the "ARR affinity" setting in App Service

The above conditions (explained in more detail in Architecture Center) would indicate that your web application doesn't deal well with rewriting the host name. This is commonly seen. The recommended way to deal with this condition is to follow the instructions for configuration Application Gateway with App Service using a custom domain. Also see: Troubleshoot App Service issues in Application Gateway.

## Restrict access

The web apps deployed in these examples use public IP addresses that can be accessed directly from the Internet. This helps with troubleshooting when you're learning about a new feature and trying new things. But if you intend to deploy a feature into production, you want to add more restrictions. Consider the following options:

- Configure Access restriction rules based on service endpoints. This allows you to lock down inbound access to the app making sure the source address is from Application Gateway.

- Use Azure App Service static IP restrictions. For example, you can restrict the web app so that it only receives traffic from the application gateway. Use the app service IP restriction feature to list the application gateway VIP as the only address with access.

 
 

 
 

 

 
 
 
 
 
 
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
 2025-10-06
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
