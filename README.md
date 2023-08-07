<h1> Exploring Azure and Networking Concepts</h1>

This is a tutorial on how to create a client virtual machine using Windows 10 as well as a server virtual machine using Ubuntu Server. It will be exploring how to set two virtual machines on the same network to send information to and from the server.

<h2>Environments and Technology Used</h2>

  - Microsoft Azure
  - Ubuntu Server
  - Wireshark
  - Windows Powershell

<h2>Operating Systems Used</h2>

  - Windows 10
  - Ubuntu Server

<h2>Languages Used</h2>

  - PowerShell

<h2>List of Prerequisites</h2>

  - Azure Virtual Machine
  - Remote Desktop Connection

<h2>Installation Steps</h2>

First, in Azure, create a Resource Group. (Recommended to keep virtual machines in one place) If you don't know how to create a Resource Group, click this link for a tutorial:

https://github.com/jarrettm98/azure-crash-course

Next, create a Virtual Machine(VM) with Azure. Now, Assign the VM to the Resource Group previously created. Name the VM and keep track of the region it is located in. (This will be important when creating the other Virtual machine) Under "Image" use the Windows 10 Operating system. For the size, use any size. (Recommend 2 vcpus) Going down the page a bit, insert an Administrator user and password. (Important to remember while logging into the VM) Lastly check the box under licensing then click "Review + create." Click create again.

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/cac8df60-b5c5-4fc9-813e-5b0d3c923402)

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/b51aa6a8-538a-4ede-845e-aa29016920cc)

Now, create the second VM. Assign it to the same Resource Group as the first one. Give it a name. Make sure the region is the same as the first VM. For the image of this VM, use the Ubuntu Server. Give it any size (Again recommend 2 vcpus) Then for "Authentication type", choose "Password", then input admin user and password. (Can be the same as the ones for the first VM) Now, click on "Next: Disks", then click on "Next: Network." For the Virtual Network it should be set to the same network as the first VM, if not, set it to that one. Now, click Review + create, then click create again.

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/189858c5-a6ee-40df-9f1b-fa4334ed4634)

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/a1460a64-e789-4938-91a5-f00c9a05e7c3)

Now, get the IP address to connect to the first VM. Search for and go to "Virtual Machines", then click on the first VM. Copy the Public IP address.

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/e3b6cb97-788b-4677-a9e1-547eda7ea462)

Next, open Remote Desktop Connection by searching for it in the Windows Start Menu. Using the IP address, user, and password of the first VM, remote into the VM. 

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/44ca24a4-a20d-4883-af6b-2dc5d1c10b9f)

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/459f1d7a-8dd6-4702-ba16-0a66d9860660)

Once successfully connected to the VM, check all of the privacy settings so that they are all disabled and click "Accept"

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/25f2d7b8-6896-4b43-9762-46f3ef2f5e91)

Next, go to your browser and download and install Wireshark. Go with default settings, there is no need to make any tweaks or changes.

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/b3a7cb02-cc8c-452a-b5ef-e4ffbe90ddc9)

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/88732a7f-c8b5-4c32-a8f1-e634485f0d3a)

After Wireshark is installed, search for Wireshark in the start menu and launch it. When it is launched, click "Ethernet", then click the shark fin symbol in the top left.

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/b821b636-f259-4678-87bb-0c231f68eeb0)

There will be a lot of traffic going through.

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/47e46c4b-6c96-49e0-9c10-ee0ebbd007e9)

Now, in the filter bar, type "ICMP" to filter ICMP traffic, then click on the shark fin icon again. This will be the traffic that will go from the VM to the server and back. Nothing will be showing until it is pinged through PowerShell or Command prompt.

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/7048a5b3-a323-4808-a49c-b836dc6990b4)

First, to send traffic to the server, get the private IP address from the Ubuntu server. In this instance it is 10.0.0.5

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/753e43cb-718a-45b6-b6b3-5a4eb331a2fe)

Open Windows PowerShell or Command Prompt and type "ping 10.0.0.5" then press Enter. (Of course, input the private IP of your server)

There should be traffic being sent through ICMP.

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/832ac425-57c0-4850-9076-1fab52d57e1a)

Now, send continuous pings to the server by typing in "ping 10.0.0.5 -t" and go back to the Ubuntu server on Azure. Under the "Networking" tab, click "Add inbound port rule" 

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/eb793a55-48e7-4237-bb2e-8e2b1b8d2d2a)

In the new rule, set the protocol to "ICMP". Then, set the Access to "Deny." Lastly, set the "Priority" to 200. (Optional: Rename the rule to "ICMP") 

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/19589615-a9cf-49ca-ac03-5de93a78ea26)

Once, the rule has been created, Go back to the Virtual Machine and see that the request of traffic is timed out.

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/0b8af4a8-cf9b-4ef1-be40-832d13abb7f4)

Go back to the rule created and change the Access to "Allow". Now, see that the traffic is sending again to the server.

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/62d4af0b-17ad-44f8-ad22-4cc685cb8aaa)

In Wireshark, filter the traffic by "SSH." and click the shark fin icon. Now, in PowerShell, type ssh, then the username + @ + the Private IP address of the server. (In my case it goes as follows: ssh jmeier98@10.0.0.5)

Example below:

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/a43bb00d-dd21-4a48-a270-bb15a42ee6af)

Next, it will ask if the user wants to continue. Type "yes" and press Enter. Then it will prompt for a password. Type in the password created and press Enter. (Know that it will not show the user type out the password, just type it in, it should work if typed in correctly)

If done correctly, it should look like the image below:

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/23c91b67-12f6-41db-809e-fca477d67bce)

Now, check the ssh traffic in Wireshark.

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/21dfc448-afd5-47bc-9800-9c92461fe3f5)

Time to try some commands out. Type "id" in the PowerShell. Notice the traffic in Wireshark.

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/cb99d16d-2c02-4b71-8bfd-acd6ae736f73)

Now type in "pwd." There are plenty of commands that can be used, but just to show off the traffic with Wireshark, this is all that the tutorial will cover.

Now type "exit" in PowerShell to exit out of SSH.

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/9f89fce0-5995-4c2e-8420-eefa97472082)

In Wireshark, filter by "DHCP"

Now, in PowerShell, type "ipconfig /renew." Notice the traffic in Wireshark.

![image](https://github.com/jarrettm98/azure-compute-and-networking/assets/140662793/946e9302-2e1a-4c99-85b3-c06f794fa2a6)

Now, go back to Wireshark, filter by "DNS"

In PowerShell, type "nslookup www.google.com"

It should show all of the traffic to and from all of the public addresses for Google.

Thats all for this tutorial. Congrats! You now know the basics of Computing and Networking with Azure Virtual Machines.
