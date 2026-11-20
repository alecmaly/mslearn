# Unit 9: 9-design-for-logic-app-solutions

Source: https://learn.microsoft.com/en-us/training/modules/design-compute-solution/9-design-for-logic-app-solutions

---

unit-inner-section" class="section is-uniform position-relative">
 
# Design for Azure Logic Apps solutions

 
 
 
 Completed
 
 
 

 

 
 
- 6 minutes

 
 

 

 
 Azure Logic Apps is another type of serverless compute solution that offers a cloud-based platform for creating and running automated workflows. Workflows are step-by-step processes that integrate your applications, data, services, and systems. With Azure Logic Apps, you can quickly develop highly scalable integration solutions for your enterprise and business-to-business (B2B) scenarios.

### Things to know about Azure Logic Apps

Let's review some characteristics of Azure Logic Apps and scenarios for using the compute solution to build new workloads.

- Azure Logic Apps is a component of Azure Integration Services. Logic Apps simplifies the way you connect legacy, modern, and cutting-edge systems across cloud, on-premises, and hybrid environments.

- With Logic Apps, you can schedule and send email notifications by using Microsoft 365 when a specific event happens, such as a new file uploaded.

- Use Logic Apps to route and process customer orders across on-premises systems and cloud services.

- Implement Logic Apps to move uploaded files from an SFTP or FTP server to Azure Storage.

- Monitor tweets and analyze sentiment with Logic Apps, and create alerts or tasks for items that need review.

#### Compare Azure Logic Apps and Azure Functions

Azure Logic Apps is similar to Azure Functions as a compute service, but there are basic differences. Azure Functions is a code-first technology that uses durable functions. Azure Logic Apps is a design-first technology. Review the following flowchart and table to compare the two solutions.

Compare
Azure Functions
Azure Logic Apps

Development
Code-first
Design-first

Method
Write code and use the durable functions extension
Create orchestrations with a GUI or by editing configuration files

Connectivity
- Large selection of built-in binding types 
 - Write code for custom bindings
- Large collection of connectors 
 - Enterprise Integration Pack for B2B scenarios 
 - Build custom connectors

Monitoring
Azure Application Insights
Azure portal, Azure Monitor Logs (Log Analytics)

### Things to consider when using Azure Logic Apps

There are several points to consider when deciding whether Azure Logic Apps is the ideal compute solution for your infrastructure. Review the following considerations, and think about how Azure Logic Apps can enhance the compute strategy for Tailwind Traders.

- Consider integration. Use Logic Apps to provide the critical infrastructure component of integration with services. Logic Apps is a good option when you need to get multiple applications and systems to work together. If you're building an app with no external connections, Logic Apps is probably not the best option.

- Consider performance. Scale your apps automatically with the Logic Apps execution engine. Logic Apps can process large datasets in parallel to let you achieve high throughput. However, fast activation time isn't always guaranteed, nor enforcement of real-time constraints on execution time.

- Consider conditional expressions. Build highly complex and deeply nested conditionals into your Logic Apps. Logic Apps provides control constructs like Boolean expressions, switch statements, and loops so your apps can make decisions based on your data.

- Consider connectors. Investigate whether prebuilt connectors are available for all the services you need to access. You might need to create custom connectors. If a service has an existing REST or SOAP API, you can make the custom connector in a few hours without writing any code. Otherwise, you need to create the API first before making the connector.

- Consider mixing compute solutions. Take advantage of diverse features by mixing and matching services when you build an orchestration. You can call functions from Logic Apps, and call logic apps from an Azure function. Build each orchestration based on the service capabilities or your personal preference.

- Consider other options. Know when not to use Azure Logic Apps. There are cases where Logic Apps might not be the best option. Logic Apps isn't an ideal solution for real-time requirements, complex business rules, or if you're using nonstandard services.

- Consider Logic Apps hosting models. Consumption plan: multitenant, pay-per-execution, and one workflow per resource. The consumption plan is best for occasional workloads. Standard plan: single-tenant, virtual network integration, multiple workflows per app, and dedicated compute resources. The standard plan is best for enterprise integration or compliance-sensitive workloads.

#### Business application

This flowchart shows a detailed decision tree for when to use Azure Logic Apps.

Tip

Continue learning about Azure Logic Apps in the Introduction to Azure Logic Apps module.

 

 
 

 

 
 
 
 <section
