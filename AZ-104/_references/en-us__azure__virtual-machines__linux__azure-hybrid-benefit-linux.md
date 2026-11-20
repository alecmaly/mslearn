# https://learn.microsoft.com/en-us/azure/virtual-machines/linux/azure-hybrid-benefit-linux

Source: https://learn.microsoft.com/en-us/azure/virtual-machines/linux/azure-hybrid-benefit-linux

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
 

 

 

 

 
 
# Azure Hybrid Benefit for Linux virtual machines

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 You can use Azure Hybrid Benefit for Linux to easily switch the software subscription model for your Linux virtual machine (VM). Change your subscription model without redeploying your VM and with no risk of downtime. You gain flexibility and savings.

You can switch seamlessly between two subscription models on Azure by using Azure Hybrid Benefit:

- Bring your own subscription (BYOS): In the BYOS model, you bring your own Red Hat Enterprise Linux (RHEL) or SUSE Linux Enterprise Server (SLES) subscription directly to Azure. You pay only for the infrastructure costs of your VM on Azure. The software fee is covered by your RHEL or SLES subscription you bought from the vendor.

- Pay-as-you-go (PAYG): Use the pay-as-you-go subscription model in Azure to pay for RHEL and SLES subscriptions as you use them.

This article defines the BYOS and PAYG subscription models, compares the benefits of each model, and shows you how to use the Azure Hybrid Benefit to switch between the two subscription models for your Linux VMs on Azure.

This process applies to:

- Azure Virtual Machine Scale Sets

- Azure Spot Virtual Machines

- Custom images

Azure Hybrid Benefit gives you the option to make seamless bidirectional conversions between the two subscription models on eligible VM instances.

You might see combined savings estimated to up to 76% with Azure Hybrid Benefit for Linux and three-year Azure Reserved VM Instances. Savings estimates are based on one standard D2s v5 Azure VM, with an RHEL or SLES subscription, in the East US region, running at a pay-as-you-go rate versus a reduced rate for a three-year reserved instance plan. The savings estimates are based on Azure pricing as of September 2024. Prices are subject to change. Actual savings might vary based on location, instance type, or usage.

Tip

Try theâ¯Azure Pricing calculator to visualize the cost-saving benefits of this feature at a Virtual Machine level.

## PAYG vs. BYOS

Azure offers two main licensing pricing options: PAYG and BYOS. With PAYG, you pay only for the resources you use. You can scale up or scale down as needed.

With BYOS, you can use your existing license subscriptions. You don't pay the license fees in Azure.

VMs utilizing a PAYG subscription model, whether deployed from PAYG images or VMs converted to PAYG from BYOS, incur both an infrastructure fee and a software fee.

If you have an existing software subscription, use Azure Hybrid Benefit to convert from a PAYG model to a BYOS model.

You can use Azure Hybrid Benefit to switch between the two subscription options at any time.

## Linux VMs you can use with Azure Hybrid Benefit

### PAYG

The following PAYG RHEL and SLES Marketplace offers are eligible to use with Azure Hybrid Benefit:

- 
RHEL PAYG

- 
SLES PAYG

## Limitations

Only RHEL images published by Red Hat, Inc. are eligible for the PAYG to BYOS conversion using the Azure Hybrid Benefit. Images from other vendors aren't supported.

### Red Hat-published RHEL PAYG offers eligible for Azure Hybrid Benefit

The following Red Hat-published RHEL PAYG offers are eligible to use with the Azure Hybrid Benefit. Links to the offers in Azure Marketplace are included.

Within these offers, associated images are described as "Pay-As-You-Go".

- Red Hat Enterprise Linux (RHEL)

- Red Hat Enterprise Linux (RHEL)

- Red Hat Enterprise Linux (RHEL) for SAP Apps

- RHEL for SAP with HA and Update Services

- Red Hat Enterprise Linux (RHEL) with High Availability (HA) Add-On

- Red Hat Enterprise Linux (RHEL) Arm64

- Red Hat Enterprise Linux Confidential VM

- Red Hat Enterprise Linux (RHEL) RAW

## Limitations

Only SLES images published by SUSE are eligible to use for the PAYG to BYOS conversion with the Azure Hybrid Benefit. Images from other vendors aren't supported.

### SUSE-published SLES PAYG offers eligible for Azure Hybrid Benefit

The following SUSE-published SLES PAYG offers are eligible for Azure Hybrid Benefit. Links to the offers in Azure Marketplace are included.

Some of the offerings are end-of-support or end-of-life (EOL) (see Product Support Lifecycle Dates) and only valid with additional Long Term Servicepack Support (LTSS) subscription, purchased directly from SUSE.

Within these offers, associated plans and images are described as a "Pay-As-You-Go" subscription of SLES.

SUSE Linux Enterprise Server

- SUSE Linux Enterprise Server 16.0 + 24x7 Support

- SUSE Linux Enterprise Server 16.0 for Arm64 + 24x7 Support

- SUSE Linux Enterprise Server 16.0 + 24x7 Support

- SUSE Linux Enterprise Server 16.0 for Arm64 + 24x7 Support

- SUSE Linux Enterprise Server 16.0 + Patching

- SUSE Linux Enterprise Server 15 SP7 + 24x7 Support

- SUSE Linux Enterprise Server 15 SP7 Arm64 + 24x7 Support

- SUSE Linux Enterprise Server 15 SP7 + Patching

SLES 15 SP6 - End-of-Support: 31-Dec-2025 - LTSS 31-Dec-2028

- SUSE Linux Enterprise Server 15 SP6 + 24x7 Support

- SUSE Linux Enterprise Server 15 SP6 Arm64 + 24x7 Support

- SUSE Linux Enterprise Server 15 SP6 + Patching

SLES 15 SP5 - End-of-Support: 31-Dec-2024 - LTSS 31-Dec-2027

- SUSE Linux Enterprise Server 15 SP5 + 24x7 Support

- SUSE Linux Enterprise Server 15 SP5 Arm64 + 24x7 Support

- SUSE Linux Enterprise Server 15 SP5 + Patching

SUSE Linux Enterprise Server for SAP applications

- SUSE Linux Enterprise Server for SAP applications 16.0 + 24x7 Support

- SUSE Linux Enterprise Server for SAP applications 15 SP7 + 24x7 Support

- SUSE Linux Enterprise Server for SAP applications 15 SP7 Hardened + 24x7 Support

- SUSE Linux Enterprise Server for SAP applications 15 SP6 + 24x7 Support

- SUSE Linux Enterprise Server for SAP applications 15 SP6 Hardened + 24x7 Support

- SUSE Linux Enterprise Server for SAP applications 15 SP5 + 24x7 Support

- SUSE Linux Enterprise Server for SAP applications 15 SP5 Hardened + 24x7 Support

- SUSE Linux Enterprise Server for SAP applications 15 SP4 + 24x7 Support

- SUSE Linux Enterprise Server for SAP applications 15 SP4 Hardened + 24x7 Support

SLES for SAP applications 12 SP5 - End-of-Support: 31-Oct-2024 - LTSS 31-Oct-2027

- SUSE Linux Enterprise Server for SAP applications 12 SP5 + 24x7 Support

### BYOS

Azure Hybrid Benefit is also available for RHEL and SLES BYOS Azure Marketplace images and images brought from on-premises or other cloud providers.

Currently, one RHEL BYOS offer is available. This offer is a private listing. To gain access to this private listing, you must join the Red Hat Cloud Access program.

You can identify SUSE BYOS marketplace offers by their name, which includes "BYOS". An example is the ** SUSE Linux Enterprise Server 15 SP7 - BYOS** offering.

Azure dedicated host instances and SQL hybrid benefits aren't eligible to use with Azure Hybrid Benefit if you already use Azure Hybrid Benefit with Linux VMs.

Note

For Red Hat VMs, the Azure account must be part of the Red Hat Cloud Access program. Register with Red Hat Cloud Access before you try to enable Azure Hybrid Benefit on your VMs.

## Enable Azure Hybrid Benefit

You can enable Azure Hybrid Benefit on new VMs, on existing VMs, and on multiple VMs.

### New VM

You can invoke Azure Hybrid Benefit when you create a VM. The benefits of using this approach include:

- You can provision both PAYG and BYOS VMs by using the same image and process.

- You can change the licensing mode in the future.

- The PAYG VM is connected to Red Hat Update Infrastructure (RHUI) or SUSE Cloud Update Infrastructure (CUI) by default, to help keep it up to date and secure. You can change the update method after deployment.

- 
Azure portal

- 
Azure CLI

The SUSE workflow is the same as the RHEL example shown here.

To enable Azure Hybrid Benefit when you create a VM:

- In the Azure portal, go to Create a virtual machine.

- In the Licensing section, select the checkbox that asks if you want to use an existing RHEL subscription. Select the checkbox to confirm that your subscription is eligible.

- Create a virtual machine by following the steps that are presented.

- On the VM service menu, select Operating System. Under Licensing, verify that the option is enabled.

You can use the `az vm extension` and `az vm update` commands to update a new VM after you create them.

Note

You do not need to install the extension for SUSE offerings.

- Install the extension:

`az vm extension
`

- Update the VM with the correct license type:

`az vm update
`

RHEL license types:

- RHEL_BASE

- RHEL_EUS

- RHEL_SAPAPPS

- RHEL_SAPHA

- RHEL_BASESAPAPPS

- RHEL_BASESAPHAâ

SLES license types:

- SLES

- SLES_SAP

- SLES_HPCâ

### Existing VM

You can enable Azure Hybrid Benefit on an existing VM.

- 
Azure portal

- 
Azure CLI

To enable Azure Hybrid Benefit on an existing VM:

- In the Azure portal, go to the overview pane of the VM that you want to convert.

- Go to Operating System > Licensing. To enable the Azure Hybrid Benefit conversion, select Yes, and then select the confirmation checkbox.

You can use the `az vm extension` and `az vm update` commands to update an existing VM.

Note

You do not need to install the extension for SUSE offerings.

- Install the extension:

`az vm extension
`

Note

The complete `az vm extension` command depends on the particular distribution you're using. For complete information, see the next section.

- Update the VM with the correct license type:

`az vm update
`

RHEL license types:

- RHEL_BASE

- RHEL_EUS

- RHEL_SAPAPPS

- RHEL_SAPHA

- RHEL_BASESAPAPPS

- RHEL_BASESAPHAâ

SLES license types:

- SLES

- SLES_SAP

- SLES_HPCâ

## Check the current licensing model of a VM that has Azure Hybrid Benefit enabled

With Red Hat, the Azure Hybrid Benefit extension must be installed on the VM to switch the licensing model from BYOS to PAYG or vice versa. You can install the Azure Hybrid Benefit (AHB) extension for RHEL VMs by using the following CLI command.

`az vm extension set \
 --resource-group <RG> \
 --vm-name <VM_NAME> \
 --name AHBForRHEL \
 --publisher Microsoft.Azure.AzureHybridBenefit 
`

For SUSE you do not need the extension, the functionality is covered by the SUSE tooling itself.

- 
Azure CLI

- 
Azure PowerShell

- Red Hat: You can use the `az vm get-instance-view` command to check whether the extension is installed. Look for the `AHBForRHEL` extension. If the corresponding extension is installed, the Azure Hybrid Benefit is enabled. Review the license type to determine which licensing model is applied to your VM.

`az vm get-instance-view \
 --resource-group <RG> \
 --name <VM_NAME> \
 --query instanceView.extensions
`

- Red Hat and SUSE: Use the following command to review the license type applied to the VM:

`az vm get-instance-view \
 --resource-group <RG> \
 --name <VM_NAME> \
 --query licenseType
`

The following license types correspond to a PAYG subscription model:

For RHEL:

- RHEL_BASE

- RHEL_EUS

- RHEL_SAPAPPS

- RHEL_SAPHA

- RHEL_BASESAPAPPS

- RHEL_BASESAPHA

For SLES:

- SLES

- SLES_SAP

- SLES_HPC

These license types correspond to a BYOS subscription model:

For RHEL:

- RHEL_BYOS

For SLES:

- SLES_BYOS

If the license type of the VM isn't modified, this command returns an empty string and the VM continues to use the billing model of the image that you used to deploy it.

- Red Hat: You can use the `Get-AzVM` command to check whether the extension is installed. Look for the `AHBForSLES` or `AHBForRHEL` extension. If the corresponding extension is installed, the Azure Hybrid Benefit is enabled. Review the license type to determine which licensing model is applied to your VM.

`Get-AzVM -ResourceGroupName <RG> -Name <VM_NAME> -Status | Select-Object -ExpandProperty Extensions
`

- Red Hat and SUSE: Use the following command to review the VM's license type:

`(Get-AzVM -ResourceGroupName <RG> -Name <VM_NAME>).LicenseType
`

The following license types correspond to a PAYG subscription model:

For RHEL:

- RHEL_BASE

- RHEL_EUS

- RHEL_SAPAPPS

- RHEL_SAPHA

- RHEL_BASESAPAPPS

- RHEL_BASESAPHA

For SLES:

- SLES

- SLES_SAP

- SLES_HPC

These license types correspond to a BYOS subscription model:

For RHEL:

- RHEL_BYOS

For SLES:

- SLES_BYOS

If the license type of the VM isn't modified, this command returns an empty string and the VM continues to use the billing model of the image that you used to deploy it.

## Convert between PAYG and BYOS subscription models

Use the Azure CLI to convert a PAYG Azure Marketplace image to a BYOS subscription model, or to convert a BYOS or migrated VM to a PAYG subscription model.

### Convert a PAYG image to BYOS by using the Azure CLI

If you deployed an Azure Marketplace image by using a PAYG licensing model and want to convert licensing to BYOS, complete the following steps.

- 
Red Hat (RHEL)

- 
SUSE (SLES)

- Apply the `RHEL_BYOS` license type to the VM:

`# This enables BYOS on a RHEL PAYG VM by using Azure Hybrid Benefit.
az vm update \
 --resource-group <RG> \
 --name <VM_NAME> \
 --license-type RHEL_BYOS
`

- When the PAYG to BYOS conversion is finished, you must register the VM with Red Hat for system updates and usage compliance.

- If you want to return the original subscription model, set `license-type` to `NONE`.

`# In order to revert back to the original subscription model, set license-type to NONE.
az vm update \
 --resource-group <RG> \
 --name <VM_NAME> \
 --license-type NONE
`

- Apply the `SLES_BYOS` license type to the VM:

`# This enables BYOS on a SLES virtual machine.
az vm update \
 --resource-group <RG> \
 --name <VM_NAME> \
 --license-type SLES_BYOS
`

- When the conversion from PAYG to BYOS is finished, you must register the VM directly with SUSE for software updates and usage compliance.

- If you want to return the original subscription model, set `license-type` to `NONE`.

`# In order to revert back to the original subscription model, set license-type to NONE.
az vm update \
 --resource-group <RG> \
 --name <VM_NAME> \
 --license-type NONE
`

Note

This is not possible for the SUSE offerings "+ Patching", they can only be moved back to "SLES".

### Convert BYOS to PAYG

Converting to a PAYG subscription model is supported for Azure Marketplace images labeled "BYOS" and for machines imported from on-premises or from a third-party cloud provider.

- 
Red Hat (RHEL)

- 
SUSE (SLES)

- Install the Azure Hybrid Benefit extension on a running VM. You can use the following command via the Azure CLI:

`az vm extension set \
 --resource-group <RG> \
 --vm-name <VM_NAME> \
 --name AHBForRHEL \
 --publisher Microsoft.Azure.AzureHybridBenefit 
`

- After the extension is installed successfully, change the license type based on what you need:

`# This enables Azure Hybrid Benefit to fetch software updates for RHEL base/regular repositories.
az vm update \
 --resource-group <RG> \
 --name <VM_NAME> \
 --license-type RHEL_BASE

# This enables Azure Hybrid Benefit to fetch software updates for RHEL EUS repositories.
az vm update \
 --resource-group <RG> \
 --name <VM_NAME> \
 --license-type RHEL_EUS

# This enables Azure Hybrid Benefit to fetch software updates for RHEL SAP APPS repositories.
az vm update \
 --resource-group <RG> \
 --name <VM_NAME> \
 --license-type RHEL_SAPAPPS

# This enables Azure Hybrid Benefit to fetch software updates for RHEL SAP HA repositories.
az vm update \
 --resource-group <RG> \
 --name <VM_NAME> \
 --license-type RHEL_SAPHA

# This enables Azure Hybrid Benefit to fetch software updates for RHEL BASE SAP APPS repositories.
az vm update \
 --resource-group <RG> \
 --name <VM_NAME> \
 --license-type RHEL_BASESAPAPPS

# This enables Azure Hybrid Benefit to fetch software updates for RHEL BASE SAP HA repositories.
az vm update \
 --resource-group <RG> \
 --name <VM_NAME> \
 --license-type RHEL_BASESAPHA
`

- Check to see if the "AHB for RHEL" feature flag is enabled:

`az feature list --namespace Microsoft.Compute | grep "AHBEnabledForRHEL" -A 3
`

- If you want to return the original subscription model, set `license-type` to `NONE`.

`az vm update \
 --resource-group <RG> \
 --name <VM_NAME> \
 --license-type NONE
`

Note

You can NOT switch products, you can only switch between the billing types.

- You do not need to install the Azure Hybrid Benefit extension on a running VM.

- Simply change the license type based on what you need:

`# This enables Azure Hybrid Benefit to fetch software updates for SLES repositories.
az vm update \
 --resource-group <RG> \
 --name <VM_NAME> \
 --license-type SLES

# This enables Azure Hybrid Benefit to fetch software updates for SLES SAP repositories.
az vm update \
 --resource-group <RG> \
 --name <VM_NAME> \
 --license-type SLES_SAP

# This enables Azure Hybrid Benefit to fetch software updates for SLES HPC repositories.
az vm update \
 --resource-group <RG> \
 --name <VM_NAME> \
 --license-type SLES_HPC
`

- If you want to return the original subscription model, set `license-type` to `NONE`:

`# In order to revert back to the original subscription model, set license-type to NONE.
az vm update \
 --resource-group <RG> \
 --name <VM_NAME> \
 --license-type NONE
`

In some cases, you must utilize the Azure Management API to patch the license type in the virtual machine's metadata:

- Define a variable with a full path to the target virtual machine:
`VM_ID=$(az vm list --query "[?name=='YourVMName'].id" -o tsv)
`

- Update the license type by patching the VM's metadata. For example, change pay-as-you-go license to SLES_SAP:
`az rest --method patch --url "https://management.azure.com${VM_ID}?api-version=2024-07-01" --body '{"properties":{"licenseType":"SLES_SAP"}}'
`

- If you want to return the original subscription model, set `license-type` to `NONE`.
`az rest --method patch --url "https://management.azure.com${VM_ID}?api-version=2024-07-01" --body '{"properties":{"licenseType":"NONE"}}'
`

### Multiple VMs

The following command converts the VMs that are specified in the argument to BYOS:

`# This enables BYOS on a RHEL virtual machine. In this example, ids.txt is an
# existing text file that contains a delimited list of resource IDs corresponding
# to the virtual machines that use Azure Hybrid Benefit.
az vm update \
 --resource-group <RG> \
 --license-type RHEL_BYOS
 --ids $(cat ids.txt)
`

The following examples show two methods you can use to get a list of resource IDs. One method applies to a resource group, and one method applies to the subscription.

`# To get a list of all the VM IDs in a resource group:
az vm list 
 --resource-group <RG> 
 --query "[].id" 
 --output tsv

# To get a list of all the VM IDs in a subscription:
az vm list 
 --query "[].id" 
 --output tsv
`

### Convert the license type in the VM operating system

- 
Red Hat (RHEL)

- 
SUSE (SLES)

To start using Azure Hybrid Benefit for Red Hat:

- Install the `AHBForRHEL` extension on the VM on which you want to apply the Azure Hybrid Benefit BYOS benefit. You can install the extension by using the Azure CLI or Azure PowerShell.

- Depending on the software updates that you want, change the license type to a relevant value. Here are the available license type values and the software updates associated with them:

License type
Software updates
Allowed VMs

RHEL_BASE
Installs Red Hat regular/base repositories on your VM.
RHEL BYOS VMs, RHEL custom image VMs

RHEL_EUS
Installs Red Hat Extended Update Support (EUS) repositories on your VM.
RHEL BYOS VMs, RHEL custom image VMs

RHEL_SAPAPPS
Installs RHEL for SAP Business Apps repositories on your VM.
RHEL BYOS VMs, RHEL custom image VMs

RHEL_SAPHA
Installs RHEL for SAP with High Availability (HA) repositories on your VM.
RHEL BYOS VMs, RHEL custom image VMs

RHEL_BASESAPAPPS
Installs RHEL regular/base SAP Business Apps repositories on your VM.
RHEL BYOS VMs, RHEL custom image VMs

RHEL_BASESAPHA
Installs regular/base RHEL for SAP with HA repositories on your VM.
RHEL BYOS VMs, RHEL custom image VMs

- Wait one hour for the extension to read the license type value and install the repositories.

Note

If the extension isn't running by itself, you can run it on demand.

You should now be connected to Azure Red Hat Update. The relevant repositories are installed on your machine.

- If you want to switch back to the BYOS model, set `license-type` to `NONE` and run the extension. This action removes all RHUI repositories from your VM and stops associated billing.

Note

In the unlikely event that the extension can't install repositories or if there are any other issues, switch the license type back to empty and contact Microsoft support. Taking this step ensures that you aren't billed for software updates.

You can simply use the `az vm update` command to update the existing license type on your running VMs. For SLES VMs, run the command and set the `--license-type` parameter to one of the following license types: `SLES`, `SLES_SAP`, or `SLES_HPC`.

Note

You can NOT switch products, you can only switch between the billing types.

To start using Azure Hybrid Benefit for SLES VMs:

- Change the license type to the value that reflects the software updates you want. Here are the available license type values and the software updates associated with them:

License type
Software updates
Allowed VMs

SLES
Installs SLES Standard repositories on your VM.
SLES BYOS VMs, SLES custom image VMs

SLES_SAP
Installs SLES SAP repositories on your VM.
SLES SAP BYOS VMs, SLES custom image VMs

SLES_HPC
Installs SLES High Performance Computing repositories on your VM.
SLES HPC BYOS VMs, SLES custom image VMs

- Wait a little until the process reads the license type value and install the repositories.

You should now be connected to the SUSE public cloud update infrastructure on Azure. The relevant repositories are installed on your machine.

- If you want to switch back to the BYOS model, set `license-type` to `NONE`. This action removes all repositories from your VM and stops associated billing.

You can use the `az vm update` command to update the existing license type on your running VMs. For SLES VMs, run the command and set the `--license-type` parameter to one of the following license types: `SLES`, `SLES_SAP`, or `SLES_HPC`.

After you apply these changes, you might need to take some further steps to point the virtual machine's operating system to the Azure Subscription Management Tool (SMT) repositories. On the virtual machine, use the following commands to remove the previous BYOS license registration and register the new pay-as-you-go registration:

`# Fully remove the old BYOS license registration using the SUSEConnect licensing tool:
sudo SUSEConnect --clean

# Trigger the cloud registration service to query for new pay-as-you-go license information:
sudo registercloudguest --force-new

# Restart the cloud guest registration service:
sudo systemctl restart guestregister.service

# Confirm the new registration:
sudo SUSEConnect --status-text
`

## Azure Hybrid Benefit for reserved instance VMs

Azure reservations (Azure Reserved Virtual Machine Instances) help you save money by committing to one-year or three-year plans for multiple products. Azure Hybrid Benefit for PAYG VMs is available for reserved instances.

If you purchased compute costs at a discounted rate by using reserved instances, you can apply Azure Hybrid Benefit on the licensing costs for RHEL and SUSE. The steps to apply Azure Hybrid Benefit for a reserved instance are exactly the same as for a regular VM.

Note

If you already purchased reservations for RHEL or SUSE PAYG software in Azure Marketplace, wait for the reservation tenure to finish before you use Azure Hybrid Benefit for PAYG VMs.

## Compliance

- 
Red Hat compliance

- 
SUSE compliance

Customers who use Azure Hybrid Benefit for PAYG RHEL VMs agree to the standard legal terms and privacy statement associated with Azure Marketplace RHEL offers.

Customers who use Azure Hybrid Benefit for PAYG RHEL VMs have three options for providing software updates and patches to those VMs:

- Red Hat Update Infrastructure (default option)

- Red Hat Satellite Server

- Red Hat Subscription Manager

Customers can use RHUI as the main update source for Azure Hybrid Benefit for PAYG RHEL VMs without attaching subscriptions. Customers who choose the RHUI option are responsible for ensuring RHEL subscription compliance.

Customers using either Red Hat Satellite Server or Red Hat Subscription Manager should remove the RHUI configuration and attach a cloud-access-enabled RHEL subscription to Azure Hybrid Benefit for PAYG RHEL VMs.

For more information about Red Hat subscription compliance, software updates, and sources for Azure Hybrid Benefit for PAYG RHEL VMs, see the Red Hat article about using RHEL subscriptions with Azure Hybrid Benefit.

Customers who use the Azure Hybrid Benefit BYOS to PAYG capability for RHEL agree to the standard legal terms and privacy statement associated with Azure Marketplace RHEL offerings.

To use Azure Hybrid Benefit for PAYG SLES VMs, and to get information about moving from SLES PAYG to BYOS or moving from SLES BYOS to PAYG, see Azure Hybrid Benefit knowledge base article.

Customers who use Azure Hybrid Benefit for PAYG SLES VMs need to move the cloud update infrastructure to one of three options that provide software updates and patches to those VMs:

- SUSE Customer Center

- SUSE Multi-Linux Manager (available in the Azure Marketplace)

- SUSE Repository Mirroring Tool (part of SLES)

If you use the Azure Hybrid Benefit BYOS to PAYG capability for SLES and want more information about moving from SLES PAYG to BYOS, or moving from SLES BYOS to PAYG, see Azure Hybrid Benefit Support knowledge base article.

## Frequently asked questions

- Q: Can I use a license type of `RHEL_BYOS` with a SLES image or vice versa?

- A: No, you can't. Trying to enter a license type that incorrectly matches the distribution running on your VM will not update any billing metadata. But if you accidentally enter the wrong license type, updating your VM again to the correct license type still enables Azure Hybrid Benefit.

- Q: I've registered with Red Hat Cloud Access but still can't enable Azure Hybrid Benefit on my RHEL VMs. What should I do?

- A: It might take some time for your Red Hat Cloud Access subscription registration to propagate from Red Hat to Azure. If you still see the error after one business day, contact Microsoft support.

- Q: I've deployed a VM by using a RHEL BYOS "golden image." Can I convert the billing on this image from BYOS to PAYG?

- A: Yes, you can use Azure Hybrid Benefit for BYOS VMs to convert this subscription model.

- Q: I've uploaded my own RHEL or SLES image from on-premises (via Azure Migrate, Azure Site Recovery, or otherwise) to Azure. Can I convert the billing on these images from BYOS to PAYG?

- A: Yes, you can use Azure Hybrid Benefit for BYOS VMs to convert this subscription model.

- Q: I've uploaded my own RHEL or SLES image from on-premises (via Azure Migrate, Azure Site Recovery, or otherwise) to Azure. Do I need to do anything to benefit from Azure Hybrid Benefit?

- A: No, you don't. RHEL or SLES images that you upload are already considered BYOS, and you're charged only for Azure infrastructure costs. You're responsible for RHEL or SLES subscription costs, just as you are for your on-premises environments.

- Q: Can I use Azure Hybrid Benefit for PAYG VMs for Azure Marketplace RHEL and SLES SAP images?

- A: Yes. You can use the license type of RHEL_BYOS for RHEL VMs and SLES_BYOS for conversions of VMs deployed from Azure Marketplace RHEL and SLES SAP images.

- Q: Can I use Azure Hybrid Benefit for PAYG VMs on virtual machine scale sets for RHEL and SLES?

- A: Yes. Azure Hybrid Benefit on virtual machine scale sets for RHEL and SLES is available to all users. You can learn more about this benefit and how to use it.

- Q: Can I use Azure Hybrid Benefit for PAYG VMs on reserved instances for RHEL and SLES?

- A: Yes. Azure Hybrid Benefit for PAYG VMs on reserved instances for RHEL and SLES is available to all users.

- Q: Can I use Azure Hybrid Benefit for PAYG VMs on a VM deployed for SQL Server on RHEL images?

- A: No, you can't. There's no plan to support these VMs.

- Q: Can I use Azure Hybrid Benefit on my RHEL for Virtual Datacenters subscription?

- A: No. RHEL for Virtual Datacenters isn't supported on Azure at all, including for Azure Hybrid Benefit.

## AHBForRHEL Extension Changelog

The AHBForRHEL extension has a version number. As improvements and CVE fixes are introduced, the version number is increased.

### Identify which AHBForRHEL extension is installed on your VM

The AHBForRHEL extension uses the standard Semantic Versioning schema for each version. To identify the AHBForRHEL extension version being used, you can run the following command: `az vm get-instance-view`. Look for the AHBForRHEL extension and version number.

`az vm get-instance-view \
 --resource-group <RG> \
 --name <VM_NAME> \
 --query instanceView.extensions
`

### Update the AHBForRHEL extension installed on your VM

To change the AHBForRHEL extension installed on your VM, run the following command:

`az vm extension set \
 --resource-group <RG> \
 --vm-name <VM_NAME> \
 --name AHBForRHEL \
 --publisher Microsoft.Azure.AzureHybridBenefit \
 --version <NEW_VERSION> 
`

### Enable auto upgrades for the AHBForRHEL extension installed on your VM

To enable auto upgrades for the AHBForRHEL extension installed on your VM, run the following command:

`az vm extension set \
 --resource-group <RG> \
 --vm-name <VM_NAME> \
 --name AHBForRHEL \
 --publisher Microsoft.Azure.AzureHybridBenefit \
 --enable-auto-upgrade true
`

### AHBForRHEL extension versions available

2.3.2

Patch CVE-2026-33818, CVE-2026-39821, CVE-2026-46600, CVE-2026-56853, CVE-2026-56858, CVE-2026-56859, CVE-2026-56860, and CVE-2026-56862.

2.3.1

Patch CVE-2026-39824, CVE-2026-27145, CVE-2026-39822, CVE-2026-42504, CVE-2026-42505, and CVE-2026-42507.
Security improvements.

2.3.0

Patch CVE-2026-33811, CVE-2026-33814, CVE-2026-39820, CVE-2026-39823, CVE-2026-39825, CVE-2026-39826, CVE-2026-39836, CVE-2026-42499.
Security improvements.

2.2.0

Patch CVE-2022-29526, CVE-2026-25679, CVE-2026-27139, and CVE-2026-27142.
Security improvements.

2.1.0

Patch CVE-2025-467.
Security improvements.

## Related content

- Learn how to create and update VMs and add license types (RHEL_BYOS, SLES_BYOS) for Azure Hybrid Benefit by using the Azure CLI

- Learn about Azure Hybrid Benefit on virtual machine scale sets for RHEL and SLES and how to use it

 
 

 
 

 

 
 
 
 
 
 
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
 2026-10-15
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
