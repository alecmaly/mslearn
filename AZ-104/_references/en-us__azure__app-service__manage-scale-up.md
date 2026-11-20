# https://learn.microsoft.com/en-us/azure/app-service/manage-scale-up

Source: https://learn.microsoft.com/en-us/azure/app-service/manage-scale-up

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
 

 

 

 

 
 
# Scale up an app in Azure App Service

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This article shows how to scale your app in Azure App Service. There are two workflows for scaling: scale up and scale out. This article explains the scale up workflow.

- Scale up: Get more CPU, memory, or disk space, or extra features
like dedicated virtual machines (VMs), custom domains and certificates, staging slots, or autoscaling. You scale up by changing the pricing tier of the
App Service plan that your app belongs to.

- Scale out: Increase the number of VM instances that run your app.
Basic, Standard, and Premium service plans scale out to as many as 3, 10, and 30 instances, respectively. App Service Environments
in the Isolated tier further increase your scale-out count to 100 instances. For more information about scaling out, see
Scale instance count manually or automatically. In that article, you find out how
to use autoscaling, which is scaling instance count automatically based on predefined rules and schedules.

Important

App Service provides an automatic scale-out option to handle varying incoming HTTP requests.

The scale settings take only seconds to apply and affect all apps in your App Service plan.
They don't require you to change your code or redeploy your application.

For information about the pricing and features of individual App Service plans, see Azure App Service on Windows pricing.

Note

Before you switch an App Service plan from the Free tier, you must first remove the spending limits in place for your Azure subscription. To view or change options for your App Service subscription, see Cost Management + Billing in the Azure portal.

## Scale up your pricing tier

Note

For information about scaling up to the Premium V4 tier, see Configure Premium V4 tier for App Service.

- In your browser, open the Azure portal.

- In the left pane of your App Service app page, under App Service plan, select Scale up.

- Select one of the pricing tiers and then select Select.

When the operation is complete, you see a notification that has a green success check mark.

## Scale related resources

If your app depends on other services, such as Azure SQL Database or Azure Storage, you can scale up these resources separately. These resources aren't managed by the App Service plan.

- On the Overview page for your app, select the link to the resource group.

- On the Overview page for the resource group, select a resource that you want to scale. The following screenshot
shows a SQL Database resource.

To scale up the related resource, see the documentation for the specific resource type. For example, for information about scaling up a single SQL database, see Scale single database resources in Azure SQL Database.

## Compare pricing tiers

For detailed information, such as VM sizes for each pricing tier, see Azure App Service on Windows pricing.

For a table of service limits, quotas, and constraints, and supported features in each tier, see App Service limits.

## Related content

- Get started with autoscale in Azure

- Configure Premium V4 tier for App Service

- Tutorial: Run a load test to identify performance bottlenecks in a web app

 
 

 
 

 

 
 
 
 
 
 
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
 2025-09-08
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
