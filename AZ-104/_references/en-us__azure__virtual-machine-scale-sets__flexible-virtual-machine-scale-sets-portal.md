# https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/flexible-virtual-machine-scale-sets-portal

Source: https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/flexible-virtual-machine-scale-sets-portal

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
 

 

 

 

 
 
# Create virtual machines in a scale set using Azure portal

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 This article steps through using Azure portal to create a Virtual Machine Scale Set.

## Sign in to Azure

Sign in to the Azure portal.

## Create a Virtual Machine Scale Set

You can deploy a scale set with a Windows Server image or Linux image such as RHEL, Ubuntu, or SLES.

- In the Azure portal search bar, search for and select Virtual Machine Scale Sets.

- Select Create on the Virtual Machine Scale Sets page.

- In the Basics tab, under Project details, make sure the correct subscription is selected and create a new resource group called myVMSSResourceGroup.

- Under Scale set details, set myScaleSet for your scale set name and select a Region that is close to your area.

- Under Orchestration, select Flexible Orchestration Mode.

- Under Security type, select Trusted launch virtual machines.

- Under Scaling, keep it the Scaling mode as Manual.

- Under Instance count, set the initial instance count field to 5. You can set this number up to 1000

- Under Instance details, select a marketplace image for Image. Select any of the Supported Distros.

- Under Administrator account configure the admin username and set up an associated password or SSH public key.

- A Password must be at least 12 characters long and meet three out of the four following complexity requirements: one lower case character, one upper case character, one number, and one special character. For more information, see username and password requirements.

- If you select a Linux OS disk image, you can instead choose SSH public key. You can use an existing key or create a new one. In this example, we will have Azure generate a new key pair for us. For more information on generating key pairs, see create and use SSH keys.

- Select Next: Spot to move to the Spot virtual machine configuration options. For this quickstart, leave the default Spot configurations.

- Select Next: Disks to move the disk configuration options. For this quickstart, leave the default disk configurations.

- Select Next: Networking to move the networking configuration options.

- On the Networking page, under Load balancing, select Azure load balancer.

- In Select a load balancer, select a load balancer or create a new one.

- When you're done, select Review + create.

- After it passes validation, select Create to deploy the scale set.

## Clean up resources

When no longer needed, delete the resource group, scale set, and all related resources. To do so, select the resource group for the scale set and then select Delete.

## Next steps

Learn how to create a Flexible scale with Azure CLI.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-05-19
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
