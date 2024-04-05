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
- Allowing Local Netowrk Interactions
- Installing Active Directory
- Creating Administrator
- Adding Client to Domain
- Setting Up Remote Desktop users
- Adding Users

<h2>Setting Up Virtual Machines</h2>

<h3>Resource Group</h3>
<p>
The first VM (Virtual Machine) that we will create is the Domain Controller. This machine will run a server version of Windows 10. It will also be the brains of the operation and will house Active Directory. Later it will be important to add our Client Client computer to this Domain. Firstly we need to create a Resource Group.
</p>
<p>
<h4>Resource Group</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/352b3e37-42e3-4346-a7ec-7395b835606d" height="60%" width="60%"/>
</p>
<p>
I will be calling mine "Active_Directory" for simplicity's sake.
</p>
<p>
<h3>Domain Controller</h3>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/1f00face-1b29-4793-a969-733955f78c38" height="60%" width="60%"/>
</p>
<p>
Next you can create the Domain Controller, call it whatever you like, but to keep it simple I named mine 'DomainController' and added it to the resource group I created called 'Active Directory'. Once we set those we will then make the "Image" 'Windows Server 2019 Datacenter - x64 Gen2'. It is preferred to have at least 2vcpus for a virtual machine so it can run all of the processes efficiently.
</p>
<p>
<h4>User Information</h4>
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
<h3>Client Computer</h3>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/04cbf333-1118-46ec-9c35-62e1f0d8ca31" height="60%" width="60%"/>
</p>
<p>
Create the Client Computer, this will be the machine that we will add to the Domain, which will represent any computer within a company connecting to a single domain. Add it to the same Resource Group as DomainController, and I called mine 'Client'. This machine will run a regular version of Windows 10. Again ensure that this machine also has at least 2 vcpus.
</p>
<p>
<h4>User Information</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/1ff18143-d5b4-46c3-8bec-307d1913518c" height="60%" width="60%"/>
</p>
<p>
I made the username 'Client' matching the Virtual Machine Name, and the password is the same as DomainController: @dm1n1strat0r
</p>
<p>
<h4>Virtual Network</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/dd735c5c-8601-4307-bece-bfb25a5182ce" height="60%" width="60%"/>
</p>
<p>
Before we create this machine we need to make sure that the Virtual Network is connected to the DomainController, so be sure to navigate to the Network Tab and change the highlighted setting. It will be whatever you named your Domain Controller followed by "-vnet" for me it is "DomainController-vnet". Without this the Virtual Machines would be on two different networks, only able to interact on an external network instead of an internal one.
</p>
<br />

<h2>Allowing Local Network Interactions</h2>
<p>
Before we can allow the Netowrk Interactions we need to know what the Private IP Address of the DomainController is. Navigate to DomainController\Network settings\Private IP address. This is the IP that you will ping within the Client Computer.
</p>
<p>
<h4>Domain Controller Private IP</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/d892ea56-158c-4d81-9bf2-b13c6669125c" height="60%" width="60%"/>
</p>
<p>
After you have the private IP Address of the DomainController you should then find the Public IP of Client so you can connect using Remote Desktop Connection.
</p>
<p>
<h4>Client Public IP</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/7ef93632-5e2d-4bd7-ad57-cac0ce9fdc94" height="60%" width=60%"/>
</p>
<p>
Once you find that you can copy the IP into Remote Desktop Connection. This app is found on your personal Windows Computer, if you are using a Mac you will need to install Microsoft Remote Desktop.
</p>
<p>
<h4>Remote Desktop Connection</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/8efebe8f-8950-42f8-9ce2-55d940df630c" height="60%" width="60%"/>
</p>
<p>
Then click okay and sign in with a different user, and enter the user you created in Azure. The user I created is called Client, with the password: @dm1n1strat0r.
</p>
<p>
<h4>Login</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/145b55d6-ee78-4df0-a4b0-f55514cd1e1f" height="60%" width="60%"
</p>
<p>
Once you get inside the VM you can setup the OS, just turn off all settings and continue.
</p>
<p>
<h4>Pinging DomainController</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/41c5fab7-8f41-419f-8d96-37c1e500edc3" height="60%" width="60%"/>
</p>
<p>
Once you are in the computer you can press the keys windows+r and type cmd. When the window opens, type the command: ping -t 10.0.0.4 the last four numbers are the DomainControllers private IP address. It will correspond to whatever yours is, **IT MAY NOT BE 10.0.0.4** this is just what it is for me. It will fail. Leave it running and connect to the DomainController using the same method we used to connect to the Client computer. Find the public Ip Address, and plug it in to Remote Desktop Connection. For this VM I used the username: DC-1 and the Password: @dm1n1strat0r
</p>
<p>
<h4>Windows Defender Firewall with Advanced Security</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/ceabd62c-a6e0-4891-9f23-372e606adfa9" height="60%" width="60%"
</p>
<p>
Once you are within the DomainController you can use the search bar to find the app "Windows Defender Firewall with Advanced Security. This is what we will use to allow for local network interactions.
</p>
<p>
<h4>Allowing ICMPv4 Interactions</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/7857bebd-151c-4fca-bd91-eebf8c44317e" height="60%" width="60%"/>
</p>
<p>
When the window opens you should click on "Inbound Rules" in the top left, and then sort by Protocol in the bar along the top. Find all the rules having to do with ICMPv4 and enable them.
</p>
<p>
<h4>Checking Command Prompt on Client</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/a9e3af87-0b86-4e9e-97f3-9a97d0287d39" height="60%" width="60%"/>
</p>
<p>
Return back to the Client computer and watch as the ping begins to succeed, this means that you have successfully allowed for local network interactions between the two virtual machines.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
