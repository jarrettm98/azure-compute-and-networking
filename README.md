<h1> Exploring Azure and Networking Concepts</h1>

This is a tutorial on how to create a client virtual machine using Windows 10 as well as a server virtual machine using Ubuntu Server. It will be exploring how to set two virtual machines on the same network to send information to and from the server.

<h2>Environments and Technology Used</h2>

  - Microsoft Azure
  - Ubuntu Server
  - Wireshark
  - Windows Powershell

<h2>Operating Systems Used</h2>

  - Windows 10

<h2>List of Prerequisites</h2>

  - Azure Virtual Machines
  - Install Wireshark

<h2>Installation Steps</h2>

First, in Azure, create a Resource Group. (Recommended to keep virtual machines in one place) If you don't know how to create a Resource Group, click this link for a tutorial:

https://github.com/jarrettm98/azure-crash-course

Next, create a Virtual Machine(VM) with Azure. Assign the VM to the Resource Group previously created. Name the VM and keep track of the region it is located in. (This will be important when creating the other Virtual machine) Under "Image" use the Windows 10 Operating system. For the size, use any size. (Recommend 2 vcpus) Going down a bit insert a Admin user and password. (Important to remember while logging into the VM) Lastly check the box under licensing then "Review + create." Click create again.

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/cac8df60-b5c5-4fc9-813e-5b0d3c923402)

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/b51aa6a8-538a-4ede-845e-aa29016920cc)

Now, create the second VM. Assign it to the same Resource Group as the first one. Give it a name. Make sure the region is the same as the first VM. For the image of this VM, use the Ubuntu Server. Give it any size (Again recommend 2 vcpus) Then for "Authentication type", choose password, then input admin user and password. (Can be the same as the ones for the first VM) Now, click on "Next: Disks", then click on "Next: Network." For the Virtual Network it should be set to the same network as the first VM, if not, set it to that one. Now, click Review + create, then click create again.

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/189858c5-a6ee-40df-9f1b-fa4334ed4634)

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/a1460a64-e789-4938-91a5-f00c9a05e7c3)

Now the ip address to connect to the first VM. Search for and go to Virtual Machines, then click on the first VM. Copy the Public IP address.

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/e3b6cb97-788b-4677-a9e1-547eda7ea462)

Next open Remote Desktop Connection by searching for in the Windows Start Menu.
