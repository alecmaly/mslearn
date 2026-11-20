# https://learn.microsoft.com/en-us/azure/logic-apps/logic-apps-enterprise-integration-overview

Source: https://learn.microsoft.com/en-us/azure/logic-apps/logic-apps-enterprise-integration-overview

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
 

 

 

 

 
 
# B2B enterprise integration workflows with Azure Logic Apps

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 For business-to-business (B2B) solutions and seamless communication between organizations, you can build automated, scalable, enterprise integration workflows by using Azure Logic Apps, which includes the Enterprise Integration Pack (EIP).

## What is the Enterprise Integration Pack?

If you're familiar with Microsoft BizTalk Server, the EIP follows similar concepts and makes B2B capabilities easy to use. However, one major difference is that the EIP is architecturally based on integration accounts. These accounts are cloud-based containers in Azure that simplify how you store, manage, and use B2B artifacts for B2B communication, including trading partners, agreements, maps, schemas, certificates, and so on.

With these artifacts, you can build B2B workflows and integration solutions that include cloud services, such as Azure, Microsoft, and other software-as-service (SaaS) apps, on-premises systems, and custom apps by using Azure Logic Apps and choosing from 1,400+ connectors. For example, you can create and run custom code from your workflows using the built-in and Azure Functions connectors. You can also use enterprise integration connectors that support the following industry standards:

- Electronic Data Interchange (EDI)

- Enterprise Application Integration (EAI)

Although organizations use different protocols and formats for B2B communication, you can still electronically exchange messages with other organizations. You can transform these different formats into a format that your organization's systems can process when you use the EIP, which supports industry-standard protocols, including AS2, X12, EDIFACT, and RosettaNet. You can also improve message security by using both encryption and digital signatures.

## What do I need to get started?

- An Azure account and subscription. Get a free Azure account.

- An integration account to store the B2B artifacts that you define and want to use.

- B2B artifacts, such as trading partners, agreements, maps, schemas, certificates, and so on.

- To create maps and schemas, you can use Visual Studio 2019 and the Microsoft Azure Logic Apps Enterprise Integration Tools Extension. The extension is currently unavailable for Visual Studio 2022 and later.

Note

Don't install this extension alongside the BizTalk Server extension. Having both extensions might
produce unexpected behavior. Make sure that you only have one of these extensions installed.

On high resolution monitors, you might experience a display problem with the map designer. To resolve this display scaling problem for Visual Studio, either restart Visual Studio in DPI-unaware mode or add the DPIUNAWARE registry value.

To install the extension from inside Visual Studio, follow these steps:

- After you open Visual Studio, from the Extensions menu, select Manage Extensions.

- In the search box, enter enterprise integration.

- Next to Azure Logic Apps Enterprise Integration Tools, select Download.

Visual Studio downloads and installs the extension.

- To create, manage, and deploy logic app resources, you can use the Azure portal, Visual Studio Code, or PowerShell.

After you create an integration account and add your artifacts, you can start building B2B workflows by creating a logic app resource.

Important

If you use the Logic App (Consumption) resource type, you have to link your integration account
to your logic app resource before you can select B2B artifacts to use in your workflow. However,
to define and add those artifacts to your integration account, you don't need a logic app resource.

If you use the Logic App (Standard) resource type, you can add schemas and maps directly to your
logic app resource and use those artifacts across multiple workflows within the same logic app resource.
You still need an integration account to store other artifacts such as partners and agreements, but linking
is optional. For more information about these resource types, review
What is Azure Logic Apps - Resource type and host environments.

The following diagram shows the high-level steps to start building B2B logic app workflows:

## Try now sample

To try this sample, which deploys logic apps that send and receive AS2 messages through Azure, select Deploy to Azure. Before you run the sample, make sure that you manually update FabrikamSales-AS2Send logic app workflow so that the HTTP action's URI property uses the URI that's dynamically generated for the Request trigger in the Contoso-AS2Receive logic app.

## Related content

- Create trading partners

- Create agreements

- Add schemas

- Add maps

- Migrate from BizTalk Server

 
 

 
 

 

 
 
 
 
 
 
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
 2026-03-10
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
