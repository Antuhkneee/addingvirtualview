# addingvirtualview
Step by step process of running and installing virtual view KVM
KVM Virtualization Setup and Management
==============================================
Table of Contents
-----------------

    Introduction
    Updating and Upgrading Packages
    Installing KVM Hypervisor and Required Packages
    Verifying KVM Kernel Modules
    Creating a Virtual Machine
    Troubleshooting and Common Issues
    Managing Virtual Machines
    Network Configuration

Introduction
---------------
This README provides a step-by-step guide on setting up and managing KVM virtualization on a Linux system.
Updating and Upgrading Packages
---------------------------------
Before installing KVM, make sure your package index is up-to-date:
    Bash

    sudo apt update

Then, upgrade your packages:
Bash

    sudo apt full-upgrade

You can also use the -s flag to list the packages that will be upgraded before upgrading them:
Bash

    sudo apt full-upgrade -s

Installing KVM Hypervisor and Required Packages
-------------------------------------------------
Install the KVM hypervisor, libvirt, and other required packages:
Bash

    sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils

Additionally, you may need to install virtinst for the virt-install command:
Bash

    sudo apt install virtinst

Verifying KVM Kernel Modules
------------------------------
Verify that the KVM kernel modules are loaded:
Bash

    lsmod | grep kvm

Creating a Virtual Machine (You must already have an ISO file)
---------------------------
Create a virtual machine using the virt-install command:
Bash

    sudo virt-install --name myvm --ram 2048 --vcpus 2 --disk path=/var/lib/libvirt/images/    myvm.img,size=15 --cdrom /path/to/iso/image.iso

Note: The size=15 parameter specifies the maximum amount of space the virtual machine can use (in this case, 20GB).

Troubleshooting:
If you encounter a "kernel panic" error, the next VM you spin up be sure to pay attention to the GUI prompts and select "enter" on starting the install. 

Troubleshooting and Common Issues
--------------------------------------
Give libvirt-qemu permissions to the user's home directory: 

    sudo chmod o+x /home/username
Increase memory allocation: 

    --ram 2048
Activate the default network:

    sudo virsh net-start default
Restart the libvirt daemon: 

    sudo systemctl restart libvirtd

Managing Virtual Machines
---------------------------
Use the following commands to manage virtual machines:

    sudo virsh list to list all virtual machines
    sudo virsh start <vm_name> to start a virtual machine
    sudo virsh stop <vm_name> to stop a virtual machine
    sudo virsh destroy <vm_name> to delete a virtual machine
    sudo virsh destroy <vm_name> --remove-all-storage to delete a virtual machine and its storage

Network Configuration
----------------------

    Start the default network: sudo virsh net-start default
    List all networks: sudo virsh net-list
    Autostart the default network: sudo virsh net-autostart default
