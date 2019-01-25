# Starting with Cloud Computing Services: Microsoft AZURE



Manuel Parra (manuelparra@decsai.ugr.es) & José Manuel Benítez (j.m.benitez@decsai.ugr.es), January 2019
![DICITSlogo](http://sci2s.ugr.es/dicits/images/dicits.png)

Table of content:

* [Student registration](#student-registration)
* [Starting with Virtual Machines](#starting-with-virtual-machines)
+ [Create resource group](#create-resource-group)
+ [Create virtual machine](#create-virtual-machine)
+ [Connect to VM](#connect-to-vm)
+ [Marketplace of  VM images](#marketplace-of--vm-images)
+ [VM Running](#vm-running)
+ [Show details of a VM](#show-details-of-a-vm)
+ [Stop a VM](#stop-a-vm)
+ [Start a VM](#start-a-vm)
+ [Reboot a VM](#reboot-a-vm)
+ [Delete a VM](#delete-a-vm)
+ [VM Open Ports](#vm-open-ports)


## Student registration

First of all register at Microsoft Azure. It is a free Cloud Computing service and does not require a Credit Card. 
It is necessary to have an email address from the University of Granada (@correo.ugr.es or @ugr.es).

- https://azure.microsoft.com/es-es/free/students/

## Starting with Virtual Machines

We will use Open Azure Cloud Shell. Azure Cloud Shell is a free, interactive shell that you can use to run the steps in this article. Common Azure tools are preinstalled and configured in Cloud Shell for you to use with your account. 

In the upper-right corner of a code block click on Cloud Shell or open a new tab in your browser: https://shell.azure.com/bash

### Create resource group

Create a resource group with the az group create command.

An Azure resource group is a logical container into which Azure resources are deployed and managed. A resource group must be created before a virtual machine. In this example, a resource group named myResourceGroupVM is created in the eastus region.

```
az group create --name myResourceGroup --location eastus
```

The resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.


### Create virtual machine

Create a virtual machine with the az vm create command.

When you create a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials. The following example creates a VM named myVM that runs Ubuntu Server. A user account named azureuser is created on the VM, and SSH keys are generated if they do not exist in the default key location ``(~/.ssh)``:

```
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys

```

It may take a few minutes to create the VM. Once the VM has been created, the Azure CLI outputs information about the VM. Take note of the publicIpAddress, this address can be used to access the virtual machine.

After a few minutes: 

```
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "XXXXXXXXXXXX",
  "resourceGroup": "myResourceGroupVM"
}
```

### Connect to VM
You can now connect to the VM with SSH in the Azure Cloud Shell or from your local computer. Replace the example IP address with the publicIpAddress noted in the previous step.

```
ssh azureuser@XXXXXXXXXXX
```

Once logged in to the VM, you can install and configure applications. When you are finished, you close the SSH session as normal:

```
exit
```

### Marketplace of  VM images

The Azure marketplace includes many images that can be used to create VMs. In the previous steps, a virtual machine was created using an Ubuntu image. In this step, the Azure CLI is used to search the marketplace for a CentOS image, which is then used to deploy a second virtual machine.

To see a list of the most commonly used images, use the az vm image list command.

```
az vm image list --output table
```

### VM Running

List of VM running:

```
az vm list
```

### Show details of a VM

```
az vm show -g MyResourceGroup -n MyVm -d
```

### Stop a VM

Stop a running VM.

```
az vm stop -g MyResourceGroup -n MyVm
```

### Start a VM

Start a stopped VM

```
az vm start -g MyResourceGroup -n MyVm
```

### Reboot a VM

Reboot a VM:

```
az vm restart -g MyResourceGroup -n MyVm
```

### Delete a VM

```
az vm delete -g MyResourceGroup -n MyVm --yes
```


### VM Open Ports

For example: 

- Open Inbound LDAP Port

```
az vm open-port -g MyResourceGroup -n MyVm --port '389'
```

- Open Web HTTP Port and HTTPS Port
```
az vm open-port -g MyResourceGroup -n MyVm --port '80'
az vm open-port -g MyResourceGroup -n MyVm --port '443'
```

- Open SSH Port

```
az vm open-port -g MyResourceGroup -n MyVm --port '22'
```

Now go to the DashBoard and check if the rules are included in your dashboard:

- Dashboard > Virtual machines
- Click in your VM name.
- Select Networking.
- Add InBound Por RULE.



