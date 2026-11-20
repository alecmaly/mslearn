# https://learn.microsoft.com/en-us/azure/virtual-machines/extensions/overview

Source: https://learn.microsoft.com/en-us/azure/virtual-machines/extensions/overview

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
 

 

 

 

 
 
# Azure virtual machine extensions and features

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Extensions are small applications that provide post-deployment configuration and automation on Azure virtual machines (VMs). The Azure platform hosts many extensions covering VM configuration, monitoring, security, and utility applications. Publishers take an application, wrap it into an extension, and simplify the installation. All you need to do is provide mandatory parameters.

Note

Extensions are only supported on Endorsed Linux distributions on Azure.

Note

Try VM assist for faster diagnostics.
We recommend that you run VM assist for Windows or VM assist for Linux. These script-based diagnostic tools help you to identify common issues that affect the Azure VM Guest Agent and overall VM health.

If you're experiencing performance problems with virtual machines, before contacting support, run these tools.

## View available extensions

You can view available extensions for a VM in the Azure portal.

- In the portal, go to the Overview page for a VM.

- Under Settings, select Extensions + Applications.

The list of available extensions are displayed. To see the complete list of extensions, see Discovering VM Extensions for Linux and Discovering VM Extensions for Windows.

## Install and use extensions

Azure VM extensions can be managed by using the Azure CLI, PowerShell, Azure Resource Manager (ARM) templates, and the Azure portal.

- From the Extensions + Applications for the VM, on the Extensions tab, select + Add.

- Locate the Custom Script Extension option. Select the extension option, then select Next.

You can then pass in a command or script to run the extension.

For more information, see Linux Custom Script Extension and Windows Custom Script Extension.

### Check for prerequisites

Some individual VM extension applications might have their own environmental prerequisites, such as access to an endpoint. Each extension has an article that explains any prerequisites, including which operating systems are supported.

### Manage extension application lifecycle

You don't need to connect to a VM directly to install or delete an extension. The Azure extension lifecycle is managed outside of the VM and integrated into the Azure platform.

Automatic extension upgrade can be used to monitor for new minor versions and automatically upgrade extensions in a safe rolling manner.

## Troubleshoot extensions

If you're looking for general troubleshooting steps for Windows VM extensions, refer to Troubleshooting Azure Windows VM extension failures
.

Otherwise, specific troubleshooting information for each extension can be found in the Troubleshoot and support section in the overview for the extension. Here's a list of the troubleshooting information available:

Namespace
Troubleshooting

microsoft.azure.monitoring.dependencyagent.dependencyagentlinux
Azure Monitor Dependency for Linux

microsoft.azure.monitoring.dependencyagent.dependencyagentwindows
Azure Monitor Dependency for Windows

microsoft.azure.security.azurediskencryptionforlinux
Azure Disk Encryption for Linux

microsoft.azure.security.azurediskencryption
Azure Disk Encryption for Windows

microsoft.compute.customscriptextension
Custom Script for Windows

microsoft.ostcextensions.customscriptforlinux

microsoft.powershell.dsc
Desired State Configuration for Windows

microsoft.hpccompute.nvidiagpudriverlinux
NVIDIA GPU Driver Extension for Linux

microsoft.hpccompute.nvidiagpudriverwindows
NVIDIA GPU Driver Extension for Windows

microsoft.azure.security.iaasantimalware
Antimalware Extension for Windows

microsoft.enterprisecloud.monitoring.omsagentforlinux
Azure Monitor for Linux

microsoft.enterprisecloud.monitoring.microsoftmonitoringagent
Azure Monitor for Windows

stackify.linuxagent.extension.stackifylinuxagentextension
Stackify Retrace for Linux

vmaccessforlinux.microsoft.ostcextensions
VMAccess for Linux

microsoft.recoveryservices.vmsnapshot
Snapshot for Linux

microsoft.recoveryservices.vmsnapshot
Snapshot for Windows

## Next steps

- For more information about how the Linux Agent and extensions work, see Azure VM extensions and features for Linux.

- For more information about how the Windows Guest Agent and extensions work, see Azure VM extensions and features for Windows.

- To install the Linux Agent, see Azure Linux Virtual Machine Agent overview.

- To install the Windows Guest Agent, see Azure Windows Virtual Machine Agent overview.

- To automatically update the extensions to latest version, see Automatic Extension Upgrade for VMs and Scale Sets in Azure

 
 

 
 

 

 
 
 
 
 
 
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
 2025-11-10
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
