<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of Active Directory within Azure Virtual Machines.
<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2019
- Windows 10 (21H2)

<h2>Active Directory Setup Steps</h2>

- Setting Up Virtual Machines
- Allowing Connection Between Machines
- Installing Active Directory
- Creating Administrator
- Adding Client to Domain
- Setting Up Remote Desktop users
- Adding Users

<h2>Setting Up Virtual Machines</h2>

<h4>Resource Group</h4>
<p>
The first VM (Virtual Machine) that we will create is the Domain Controller. This machine will run a server version of Windows 10. It will also be the brains of the operation and will house Active Directory. Later it will be important to add our Client Client computer to this Domain. Firstly we need to create a Resource Group.
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/352b3e37-42e3-4346-a7ec-7395b835606d" height="60%" width="60%"/>
</p>
<p>
I will be calling mine "Active_Directory" for simplicity's sake.
</p>
<p>
<h4>Domain Controller</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/1f00face-1b29-4793-a969-733955f78c38" height="60%" width="60%"/>
</p>
<p>
Next you can create the Domain Controller, call it whatever you like, but to keep it simple I named mine 'DomainController' and added it to the resource group I created called 'Active Directory'. Once we set those we will then make the "Image" 'Windows Server 2019 Datacenter - x64 Gen2'. It is preferred to have at least 2vcpus for a virtual machine so it can run all of the processes efficiently.
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/8bcdb894-37b3-4804-8511-7d21494c0b65" height="60%" width="60%"/>
</p>
<p>
I set the username as 'DC-1' and the password as '@dm1n1strat0r' to make them easy to remember when we are loggin in with Remote Desktop Connection. Alternatively you could open a notepad and write down all the information. Then you can review and create the machine.
</p>
<p>
<h4>Configuring IP</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/300ecc2c-9bec-4bbb-ba8d-4a0b54913496" height="60%" width="60%"/>
</p>
<p>
Once the Virtual Machine is set up it is necessary to set the IP Configuration to static instead of dynamic, so that the IP will never change. This makes it easy for the Client Computer to connect to the Domain Controller with the same IP every single time. Your path to this setting is Home\DomainController\Network settings\domaincontroller631_z1\IP configurations\ipconfig1
</p>
<p>
<h4>Client Computer</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/04cbf333-1118-46ec-9c35-62e1f0d8ca31" height="60%" width="60%"/>
</p>
<p>
Create the Client Computer, this will be the machine that we will add to the Domain, which will represent any computer within a company connecting to a single domain. Add it to the same Resource Group as DomainController, and I called mine 'Client'. This machine will run a regular version of Windows 10. Again ensure that this machine also has at least 2 vcpus.
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/1ff18143-d5b4-46c3-8bec-307d1913518c" height="60%" width="60%"/>
</p>
<p>
I made the username 'Client' matching the Virtual Machine Name, and the password is the same as DomainController: @dm1n1strat0r
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/dd735c5c-8601-4307-bece-bfb25a5182ce" height="60%" width="60%"/>
</p>
<p>
Before we create this machine we need to make sure that the Virtual Network is connected to the DomainController, so be sure to navigate to the Network Tab and change the highlighted setting. It will be whatever you named your Domain Controller followed by "-vnet" for me it is "DomainController-vnet". Without this the Virtual Machines would be on two different networks, only able to interact on an external network instead of an internal one.
</p>
<br />


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
