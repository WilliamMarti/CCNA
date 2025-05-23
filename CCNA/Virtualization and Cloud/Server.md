Server Hardware 

- Cisco UCS (Unified Computing System)
- Dell EMC
- HPE
- IBM

Before Virtualization, 1-to-1 relationship between server and OS

![[Virtualization.PNG]]


**VMM** - Virtual Machine Monitor, another name for hypervisor

Type of hypervisor that runs  directly on top of the hardware is **Type 1**
- Vmware ESXi
- Microsoft Hyper-V

Also called bare-metal hypervisors
	aka native-hypervisors

**Type 2** - Hypervisors run as a program on an OS like a regular computer program
	Ex: Vmware Workstation, Oracle Virtualbox

OS running directly on the hardware is called the **Host OS**
OS running in a VM is called a **Guest OS**

Why use virtualization:

**Partitioning** - Run multiple system on 1 physical machine.  Divide Ssytem resource between virtual machines

**Isolation** - Fault and security isolation at the hardware level.  Preserve performance with advanced resource controls

**Encapsulation** - Save entire state of a virtual machine.  Can move/copy a virtual machine as easily as a file

**Hardware Independence** - Provision or migrate any virtual machine to any physical server

##### Connecting VMs to the network

 ![[VM-networking.PNG]]

