# https://learn.microsoft.com/en-us/azure/app-service/configure-common

Source: https://learn.microsoft.com/en-us/azure/app-service/configure-common

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
 

 

 

 

 
 
# Configure an App Service app

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This article explains how to configure common settings for web apps, a mobile back end, or an API app. For Azure Functions, see App settings reference for Azure Functions.

## Configure app settings

In Azure App Service, app settings are variables passed as environment variables to the application code. The following conditions apply to app settings:

- App setting names can contain only letters, numbers (0-9), periods (.), and underscores (_).

- Special characters in the value of an app setting must be escaped as needed by the target operating system.

For example, to set an environment variable in App Service for Linux with the value `"pa$$w0rd\"`, the string for the app setting should be `"pa\$\$w0rd\\"`.

For Linux apps and custom containers, App Service passes app settings to the container by using the `--env` flag to set the environment variable in the container. In either case, they're injected into your app environment at app startup. When you add, remove, or edit app settings, App Service triggers an app restart.

For ASP.NET and ASP.NET Core developers, configuring app settings in App Service is like configuring them in `<appSettings>` in `Web.config` or `appsettings.json`. The values in App Service override the ones in `Web.config` or `appsettings.json`. You can keep development settings, such as local MySQL password, in `Web.config` or `appsettings.json`. You can keep production secrets, such as Azure MySQL database password, safely in App Service. The same code uses your development settings when you debug locally. It uses your production secrets when you deploy it to Azure.

Other language stacks get the app settings as environment variables at runtime. For steps that are specific to each language stack, see:

- ASP.NET Core

- Java

- Node.js

- Python

- PHP

- Custom containers

App settings are always encrypted when they're stored (encrypted at rest).

Note

If you store secrets in app settings, consider using Azure Key Vault references. If your secrets are for connectivity to back-end resources, consider connectivity options that are more secure and that don't require secrets. For more information, see Secure connectivity to Azure services and databases from Azure App Service.

- 
Azure portal

- 
Azure CLI

- 
Azure PowerShell

- In the Azure portal, search for and select App Services, and then select your app.

- On the app's left menu, select Settings > Environment variables. Then select App settings.

By default, values for app settings are hidden in the portal for security. To see a hidden value of an app setting, under Value, select Show value. To see the hidden values of all app settings, select Show values.

Note

Read/Write user permissions are required to view this section in the Azure portal. RBAC built-in roles with sufficient permissions are Owner, Contributor, and Website Contributor. The Reader role alone wouldn't be allowed to access this page.

- To add a new app setting, select Add. To edit a setting, select the setting.

- In the dialog, you can stick the setting to the current slot.

Note

In a default Linux app service or a custom Linux container, any nested JSON key structure in the app setting name needs to be configured differently for the key name. Replace any colon (`:`) with a double underscore (`__`). Replace any period (`.`) with a single underscore (`_`). For example, `ApplicationInsights:InstrumentationKey` needs to be configured in App Service as `ApplicationInsights__InstrumentationKey` for the key name.

- When you finish, select Apply. Then select Apply on the Environment variables page.

Add or edit an app setting by using az webapp config app settings set:

`az webapp config appsettings set --resource-group <group-name> --name <app-name> --settings <setting-name>="<value>"
`

Replace `<setting-name>` with the name of the setting. Replace `<value>` with the value to assign to the setting.

Show all settings and their values by using az webapp config appsettings list:

`az webapp config appsettings list --resource-group <group-name> --name <app-name>
`

Remove one or more settings by using az webapp config app settings delete:

`az webapp config appsettings delete --resource-group <group-name> --name <app-name> --setting-names {<setting-name1>,<setting-name2>,...}
`

Set one or more app settings by using Set-AzWebApp:

`Set-AzWebApp -ResourceGroupName <group-name> -Name <app-name> -AppSettings @{"<setting-name1>"="<value1>"; "<setting-name2>"="<value2>";...}
`

This cmdlet replaces the entire set of app settings with the ones that you specify. To add or edit an app setting within an existing set, include the existing app settings in your input hash table by using the Get-AzWebApp cmdlet. For example:

`# Get app configuration
$webapp=Get-AzWebApp -ResourceGroupName <group-name> -Name <app-name>

# Copy app settings to a new hash table
$appSettings = @{}
ForEach ($item in $webapp.SiteConfig.AppSettings) {
$appSettings[$item.Name] = $item.Value
}

# Add or edit one or more app settings
$appSettings['<setting-name1>'] = '<value1>'
$appSettings['<setting-name2>'] = '<value2>'

# Save changes
Set-AzWebApp -ResourceGroupName <group-name> -Name <app-name> -AppSettings $appSettings
`

To check if an app setting is slot specific, use Get-AzWebAppSlotConfigName:

`Get-AzWebAppSlotConfigName -ResourceGroupName <group-name> -Name <app-name> | select AppSettingNames
`

To make one or more app settings slot specific, use Set-AzWebAppSlotConfigName:

`Set-AzWebAppSlotConfigName -ResourceGroupName <group-name> -Name <app-name> -AppSettingNames <setting-name1>,<setting-name2>,...
`

### Edit app settings in bulk

- 
Azure portal

- 
Azure CLI

- 
Azure PowerShell

- Select Advanced edit.

- Edit the settings in the text area.

- When you finish, select OK. Then select Apply on the Environment variables page.

App settings have the following JSON formatting:

`[
 {
 "name": "<key-1>",
 "value": "<value-1>",
 "slotSetting": false
 },
 {
 "name": "<key-2>",
 "value": "<value-2>",
 "slotSetting": false
 },
 ...
]
`

Run az webapp config app settings set with the name of the JSON file:

`az webapp config appsettings set --resource-group <group-name> --name <app-name> --settings "@fileName.json"
`

Tip

Wrapping the file name with quotation marks is required only in PowerShell.

The necessary file format is a JSON array of settings where the slot setting field is optional. For example:

`[
 {
 "name": "key1",
 "slotSetting": false,
 "value": "value1"
 },
 {
 "name": "key2",
 "value": "value2"
 }
]
`

For convenience, you can save existing settings in a JSON file by using az webapp config appsettings list.

`# Save the settings
az webapp config appsettings list --resource-group <group-name> --name <app-name> > settings.json

# Edit the JSON file
...

# Update the app with the JSON file
az webapp config appsettings set --resource-group <group-name> --name <app-name> --settings @settings.json
`

It's not possible to edit app settings in bulk by using a JSON file with Azure PowerShell.

## Configure connection strings

This section describes how to configure connection strings.

Note

Consider connectivity options that are more secure and that don't require connection secrets. For more information, see Secure connectivity to Azure services and databases from Azure App Service.

For ASP.NET and ASP.NET Core developers, setting connection strings in App Service is like setting them in `<connectionStrings>` in `Web.config`. The values that you set in App Service override the ones in `Web.config`. You can keep development settings, such as a database file, in `Web.config`. You can keep production secrets, such as SQL database credentials, safely in App Service. The same code uses your development settings when you debug locally. It uses your production secrets when you deploy it to Azure.

For other language stacks, it's better to use app settings instead. Connection strings require special formatting in the variable keys to access the values.

There's one case where you might want to use connection strings instead of app settings for non-.NET languages. Certain Azure database types are backed up along with the app only if you configure a connection string for the database in your App Service app. For more information, see Create a custom backup. If you don't need this automated backup, use app settings.

At runtime, connection strings are available as environment variables, prefixed with the following connection types:

- SQL Server: `SQLCONNSTR_`

- MySQL: `MYSQLCONNSTR_`

- Azure SQL: `SQLAZURECONNSTR_`

- Custom: `CUSTOMCONNSTR_`

- PostgreSQL: `POSTGRESQLCONNSTR_`

- Azure Notification Hubs: `NOTIFICATIONHUBCONNSTR_`

- Azure Service Bus: `SERVICEBUSCONNSTR_`

- Azure Event Hubs: `EVENTHUBCONNSTR_`

- Azure Cosmos DB: `DOCDBCONNSTR_`

- Redis cache: `REDISCACHECONNSTR_`

Note

.NET apps that target PostgreSQL, Notification Hubs, Service Bus, Event Hubs, Azure Cosmos DB, and Redis cache should set the connection string to Custom as a workaround for a known issue in .NET EnvironmentVariablesConfigurationProvider.

For example, a MySQL connection string named connectionstring1 can be accessed as the environment variable `MYSQLCONNSTR_connectionString1`. For steps that are specific to each language stack, see:

- ASP.NET Core

- Java

- Node.js

- Python

- PHP

- Custom containers

Connection strings are always encrypted when they're stored (encrypted at rest).

Note

You can also resolve connection strings from Key Vault by using Key Vault references.

- 
Azure portal

- 
Azure CLI

- 
Azure PowerShell

- In the Azure portal, search for and select App Services, and then select your app.

- On the app's left menu, select Settings > Environment variables. Then select Connection strings.

By default, values for connection strings are hidden in the portal for security. To see a hidden value of a connection string, under Value, select Show value. To see the hidden values of all connection strings, select Show values.

- To add a new connection string, select Add. To edit a connection string, select the connection string.

- In the dialog, you can stick the connection string to the current slot.

- When you finish, select Apply. Then select Apply on the Environment variables page.

Add or edit an app setting by using az webapp config connection-string set:

`az webapp config connection-string set --resource-group <group-name> --name <app-name> --connection-string-type <type> --settings <string-name>='<value>'
`

Replace `<string-name>` with the name of the connection string. Replace `<value>` with the value to assign to the connection string. For possible values of `<type>` such as `SQLAzure`, see the CLI command documentation.

Show all connection strings and their values by using az webapp config connection-string list:

`az webapp config connection-string list --resource-group <group-name> --name <app-name>
`

Remove one or more connection strings by using az webapp config connection-string delete:

`az webapp config connection-string delete --resource-group <group-name> --name <app-name>--setting-names {<string-name1>,<string-name2>,...}
`

Set one or more connection strings by using Set-AzWebApp:

`$PropertiesObject = @{
 "<string-name1>" = @{
 value="<connection-string1>";
 type="<type>"};
 "<string-name2>" = @{
 value="<connection-string2>";
 type="<type>"}
}

Set-AzWebApp -ResourceGroupName <group-name> -Name <app-name> -ConnectionStrings $PropertiesObject
`

Each connection string contains a name (`<string-name1>`), a value (`<connection-string1>`), and the type. The type is a numerical value that corresponds to one of the ConnectionStringType enumerator fields. For example, for Azure SQL, specify `type="2"`.

This cmdlet replaces the entire set of connection strings with the ones that you specify. To add or edit an app setting within an existing set, include the existing app settings in your input hash table by using the Get-AzWebApp cmdlet. For example:

`# Get app configuration
$webapp=Get-AzWebApp -ResourceGroupName <group-name> -Name <app-name>

# Copy connection strings to a new hash table
$connStrings = @{}
ForEach ($item in $webapp.SiteConfig.ConnectionStrings) {
 $connStrings[$item.Name] = @{value=$item.ConnectionString; type=$item.Type.ToString()}
}

# Add or edit one or more connection strings
$connStrings['<string-name1>'] = @{value='<connection-string1>'; type='<type>'}
$connStrings['<string-name2>'] = @{value='<connection-string2>'; type='<type>'}

# Save changes
Set-AzWebApp -ResourceGroupName <group-name> -Name <app-name> -ConnectionStrings $connStrings
`

To check if a connection string is slot specific, use Get-AzWebAppSlotConfigName:

`Get-AzWebAppSlotConfigName -ResourceGroupName <group-name> -Name <app-name> | select ConnectionStringNames
`

To make one or more connection strings slot specific, use Set-AzWebAppSlotConfigName:

`Set-AzWebAppSlotConfigName -ResourceGroupName <group-name> -Name <app-name> -ConnectionStringNames <string-name1>,<string-name2>,...
`

### Edit connection strings in bulk

- 
Azure portal

- 
Azure CLI

- 
Azure PowerShell

- Select Advanced edit.

- Edit the connection strings in the text area.

- When you finish, select Apply. Don't forget to also select Apply on the Environment variables page.

Connection strings have the following JSON formatting:

`[
 {
 "name": "name-1",
 "value": "conn-string-1",
 "type": "SQLServer",
 "slotSetting": false
 },
 {
 "name": "name-2",
 "value": "conn-string-2",
 "type": "PostgreSQL",
 "slotSetting": false
 },
 ...
]
`

Run az webapp config connection-string set with the name of the JSON file:

`az webapp config connection-string set --resource-group <group-name> --name <app-name> --settings "@fileName.json"
`

Tip

Wrapping the file name with quotation marks is required only in PowerShell.

The necessary file format is a JSON array of connection strings where the slot setting field is optional. For example:

`[
 {
 "name": "name-1",
 "value": "conn-string-1",
 "type": "SQLServer",
 "slotSetting": false
 },
 {
 "name": "name-2",
 "value": "conn-string-2",
 "type": "PostgreSQL",
 },
 ...
]
`

For convenience, you can save existing connection strings in a JSON file by using az webapp config connection-string list.

`# Save the connection strings
az webapp config connection-string list --resource-group <group-name> --name <app-name> > settings.json

# Edit the JSON file
...

# Update the app with the JSON file
az webapp config connection-string set --resource-group <group-name> --name <app-name> --settings @settings.json
`

It's not possible to edit connection strings in bulk by using a JSON file with Azure PowerShell.

## Configure language stack settings

To configure language stack settings, see these resources:

- ASP.NET Core

- Java

- Node.js

- Python

- PHP

## Configure general settings

To configure general settings, follow the steps for your preferred tools.

- 
Azure portal

- 
Azure CLI

- 
Azure PowerShell

- In the Azure portal, search for and select App Services, and then select your app.

- On the app's left menu, select Settings > Configuration. Then select General settings.

Here, you can configure some common settings for the app. Some settings require you to scale up to higher pricing tiers.

- Platform settings: Configure settings for the hosting platform, including:

- Platform: Choose 32-bit or 64-bit. For Windows apps only.

- FTP state: Allow only FTPS, or disable FTP altogether.

- HTTP version: Set to 2.0 to enable support for the HTTPS/2 protocol.

Note

Most modern browsers support the HTTP/2 protocol over TLS only. Unencrypted traffic continues to use HTTP/1.1. To ensure that client browsers connect to your app with HTTP/2, secure your custom DNS name. For more information, see Provide security for a custom DNS name with a TLS/SSL binding in App Service.

- Web sockets: Configure for ASP.NET SignalR or socket.io, for example.

- Always On: Turn on if you want to keep the app loaded even when there's no traffic.

When Always On is turned off (default), the app is unloaded after 20 minutes without any incoming requests. The unloaded app can cause high latency for new requests because of its warm-up time.

When Always On is turned on, the front-end load balancer sends a `GET` request to the application root every five minutes. The continuous ping prevents the app from being unloaded.

Always On is required for continuous WebJobs or for WebJobs that a cron expression triggers.

- Session affinity: In a multiple-instance deployment, ensure that the client is routed to the same instance for the life of the session. You can set this option to Off for stateless applications.

- Session affinity proxy: Turn on if your app is behind a reverse proxy (like Azure Application Gateway or Azure Front Door) and you're using the default host name. The domain for the session affinity cookie aligns with the forwarded host name from the reverse proxy.

- HTTPS Only: Enable if you want to redirect all HTTP traffic to HTTPS.

- Minimum TLS version: Select the minimum TLS encryption version that your app requires.

Note

Post-quantum hybrid key exchange is managed by the platform and has no app-level setting. Setting the minimum TLS version to 1.3 doesn't require the hybrid group `X25519MLKEM768`. Neither the minimum TLS version nor the minimum cipher-suite setting enables, disables, or requires this group.

- Debugging: Enable remote debugging for ASP.NET, ASP.NET Core, or Node.js apps. This option turns off automatically after 48 hours.

- Incoming client certificates: Require client certificates in mutual authentication.

You may also choose the Stack settings tab to configure settings for the software stack to run the app, including the language and SDK versions. For Linux apps, you can select the language runtime version and set an optional startup command.

You can set many of the common configurable options by using az webapp config set. The following example shows a subset of the configurable options:

`az webapp config set --resource-group <group-name> --name <app-name> --use-32bit-worker-process [true|false] --web-sockets-enabled [true|false] --always-on [true|false]--http20-enabled --auto-heal-enabled [true|false] --remote-debugging-enabled [true|false] --number-of-workers
`

For a Windows app, set `--use-32bit-worker-process false` to use a 64-bit (x64) process. This setting doesn't increase the tier's resource quotas.

To show the existing settings, use the az webapp config show command.

You can set many of the common configurable options by using Set-AzWebApp. The following example shows a subset of the configurable options:

`Set-AzWebApp -ResourceGroupName <group-name> -Name <app-name> -Use32BitWorkerProcess [$True|$False] -WebSocketsEnabled [$True|$False] -AlwaysOn [$True|$False] -NumberOfWorkers
`

For a Windows app, set `-Use32BitWorkerProcess $False` to use a 64-bit (x64) process. This setting doesn't increase the tier's resource quotas.

To show the existing settings, use the Get-AzWebApp command.

## Configure default documents

The default document is the webpage that appears at the root URL of an App Service app. The first matching file in the list is used. If the app uses modules that route based on URL instead of serving static content, there's no need for default documents.

The setting to configure default documents is only for Windows apps.

- 
Azure portal

- 
Azure CLI

- 
Azure PowerShell

- In the Azure portal, search for and select App Services, and then select your app.

- On the app's left menu, select Configuration. Then select Default documents.

- To add a default document, add a list item, and select Apply. To remove a default document, select the Delete icon to its right.

Add a default document by using az resource update:

`az resource update --resource-group <group-name> --resource-type "Microsoft.Web/sites/config" --name <app-name>/config/web --add properties.defaultDocuments <filename>
`

Add a default document by modifying the updating app's PowerShell object:

`$webapp = Get-AzWebApp -ResourceGroupName <group-name> -Name <app-name>
$webapp.SiteConfig.DefaultDocuments.Add("<filename>")
Set-AzWebApp $webapp
`

## Map a URL path to a directory

By default, App Service starts your app from the root directory of your app code. But certain web frameworks don't start in the root directory. For example, Laravel starts in the `public` subdirectory. Such an app would be accessible at `http://contoso.com/public`, for example, but you typically want to direct `http://contoso.com` to the `public` directory instead. If your app's startup file is in a different folder, or if your repository has more than one application, you can edit or add virtual applications and directories.

The feature of mapping a virtual directory to a physical path is available only on Windows apps.

- 
Azure portal

- 
Azure CLI

- 
Azure PowerShell

- In the Azure portal, search for and select App Services, and then select your app.

- On the app's left menu, select Settings > Configuration. Then select Path mappings.

- Select Add virtual application or directory. Then take one of these actions:

- To map a virtual directory to a physical path, select Directory. Specify the virtual directory and the corresponding relative (physical) path to the website root (`D:\home`).

- To mark a virtual directory as a web application, select Virtual application.

- Select Add to save.

The following example sets the root path `/` to the `public` subdirectory, which works for Laravel. It also adds a second virtual application at the `/app2` path. To run it, create a file called `json.txt` with the following contents:

`[
 {
 "physicalPath"':' "site\\wwwroot\\public",
 "preloadEnabled"':' false,
 "virtualDirectories"':' null,
 "virtualPath"':' "/"
 },
 {
 "physicalPath"':' "site\\wwwroot\\app2",
 "preloadEnabled"':' false,
 "virtualDirectories"':' null,
 "virtualPath"':' "/app2"
 }
]
`

Change `<group-name>` and `<app-name>` for your resources and run the following command. Be aware of escape characters when you run this command. For more information on escape characters, see Tips for using the Azure CLI successfully.

`az resource update --resource-group <group-name> --resource-type Microsoft.Web/sites/config --name <app-name>/config/web --set properties.virtualApplications="@json.txt"
`

The following example sets the root path `/` to the `public` subdirectory, which works for Laravel. It also adds a second virtual application at the `/app2` path. To run it, change `<group-name>` and `<app-name>`.

`$webapp=Get-AzWebApp -ResourceGroupName <group-name> -Name <app-name>

# Set default / path to public subdirectory
$webapp.SiteConfig.VirtualApplications[0].PhysicalPath= "site\wwwroot\public"

# Add a virtual application
$virtualApp = New-Object Microsoft.Azure.Management.WebSites.Models.VirtualApplication
$virtualApp.VirtualPath = "/app2"
$virtualApp.PhysicalPath = "site\wwwroot\app2"
$virtualApp.PreloadEnabled = $false
$webapp.SiteConfig.VirtualApplications.Add($virtualApp)

# Save settings
Set-AzWebApp $webapp
`

## Configure handler mappings

For Windows apps, you can customize the IIS handler mappings and virtual applications and directories. Handler mappings let you add custom script processors to handle requests for specific file extensions.

To add a custom handler:

- In the Azure portal, search for and select App Services, and then select your app.

- On the app's left menu, select Settings > Configuration. Then select Path mappings.

- Select Add handler mapping. Configure the handler as follows:

- Extension. The file extension that you want to handle, such as `*.php` or `handler.fcgi`.

- Script processor. The absolute path of the script processor to you. The script processor processes requests to files that match the file extension. Use the path `D:\home\site\wwwroot` to refer to your app's root directory.

- Arguments. Optional command-line arguments for the script processor.

- Select Add to save.

## Configure custom containers

- Configure a custom container for Azure App Service

- Mount Azure Storage as a local share in App Service

## Related content

- Environment variables and app settings in Azure App Service

- Set up an existing custom domain in Azure App Service

- Set up staging environments in Azure App Service

- Enable HTTPS for a custom domain in Azure App Service

- Enable diagnostics logging for apps in Azure App Service

- Scale up an app in Azure App Service

- Azure App Service quotas and alerts

- Change applicationHost.config settings with applicationHost.xdt

 
 

 
 

 

 
 
 
 
 
 
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
 2026-11-06
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
