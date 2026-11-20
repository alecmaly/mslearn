# https://learn.microsoft.com/en-us/azure/virtual-machines/auto-shutdown-vm

Source: https://learn.microsoft.com/en-us/azure/virtual-machines/auto-shutdown-vm

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
 

 

 

 

 
 
# Auto-shutdown a virtual machine

 
 
 
 
 
 
 
 
 
 Feedback
 
 
 

 
 

 
 
 
 
 
 
 
 
 Summarize this article for me
 
 
 

 
 

 

 
 
 
## 
 In this article
 

 
 Learn how to automatically shut down virtual machines (VMs) in Azure. The auto-shutdown feature for Azure VMs can help reduce costs by shutting down the VMs during off hours when they aren't needed and automatically restarting them when they're needed again.

## Configure auto-shutdown for a virtual machine

- 
Portal

- 
Azure CLI

Sign in to the Azure portal.

- In the Azure portal, navigate to the virtual machine you want to configure auto-shutdown for.

- In the virtual machine's detail page, select "Auto-shutdown" under the Operations section.

- In the "Auto-shutdown" configuration screen, toggle the switch to "On."

- Set the time you want the virtual machine to shut down.

- If you want to receive notification before shutdown, select "Yes" in the "Send notification before shutdown" option and provide details in "Email Address" or "Webhook URL" as per your choice.

- Select "Save" to save the auto-shutdown configuration.

To configure auto-shutdown for a single virtual machine using the Azure CLI, you can use the following script:

`# Set the resource group name, VM name, and shutdown time
RESOURCE_GROUP_NAME="myResourceGroup"
VM_NAME="myVM" # Add your VM's name here
SHUTDOWN_TIME="18:00"

# Prompt the user to choose whether to auto-restart or leave the machines off
echo "Do you want to auto-restart the machine? (y/n)"
read RESTART_OPTION

# Set the auto-shutdown and auto-start properties based on the user's choice
if [ "$RESTART_OPTION" == "y" ]; then
 AUTO_SHUTDOWN="true"
 AUTO_START="true"
else
 AUTO_SHUTDOWN="true"
 AUTO_START="false"
fi

# Set the auto-shutdown and auto-start properties for the VM
az vm auto-shutdown -g $RESOURCE_GROUP_NAME -n $VM_NAME --time $SHUTDOWN_TIME

if [ "$AUTO_START" == "true" ]; then
 az vm restart -g $RESOURCE_GROUP_NAME -n $VM_NAME --no-wait
fi
`

To configure auto-shutdown for multiple virtual machines using the Azure CLI, you can use the following script:

`# Set the resource group name and shutdown time
RESOURCE_GROUP_NAME="myResourceGroup"
SHUTDOWN_TIME="18:00"

# Prompt the user to choose whether to auto-restart or leave the machines off
echo "Do you want to auto-restart the machines? (y/n)"
read RESTART_OPTION

# Set the auto-shutdown and auto-start properties based on the user's choice
if [ "$RESTART_OPTION" == "y" ]; then
 AUTO_SHUTDOWN="true"
 AUTO_START="true"
else
 AUTO_SHUTDOWN="true"
 AUTO_START="false"
fi

# Loop through all VMs in the resource group and set the auto-shutdown and auto-start properties
for VM_ID in $(az vm list -g $RESOURCE_GROUP_NAME --query "[].id" -o tsv); do
 az vm auto-shutdown --ids $VM_ID --time $SHUTDOWN_TIME
 az vm restart --ids $VM_ID --no-wait
done
`

The above scripts use the `az vm auto-shutdown` and `az vm restart` commands to set the `auto-shutdown` and `restart` properties of all the VMs in the specified resource group. The `--ids` option is used to specify the VMs by their IDs, and the `--time` and `--auto-start-`enabled options are used to set the auto-shutdown and autostart properties, respectively.

Both scripts also prompt to choose whether to auto restart the machines or leave them off until they're manually restarted. The choice is used to set the -`-auto-shutdown-enabled` property of the VMs.

Note

Remember to configure the time zone to match your requirements, as Coordinated Universal Time (UTC) is the default setting for the time zone.

## Clean up resources

If you no longer need the virtual machine, delete it with the following steps:

- Navigate to the virtual machine's Overview page on the left

- Select on "Delete" from the top middle option.

- Follow the prompts to delete the virtual machine.

For more information on how to delete a virtual machine, see delete a VM.

## Next steps

Learn about sizes and how to resize a VM:

- Types of virtual machine sizes.

- Change the size of a virtual machine.

 
 

 
 

 

 
 
 
 
 
 
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
 2026-01-13
 
 
 

 
 

 
 

 
 
 
 
 
 
 
 
 
### In this article

 
 
 
 
 
 
 
 Was this page helpful?
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Need help with this topic?
 

 
 Want to try using Ask Learn to clarify or guide you through this topic?
 

 
 
 
 
 
 
 
 
 
 
 
 
 Ask Learn
 
 
 
 
 
 Ask Learn
 
 

 
 
 
 
 Suggest a fix?
