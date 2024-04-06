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
I set the username as 'DC-1' and the password as '@dm1n1strat0r' to make them easy to remember when we are logging in with Remote Desktop Connection. Alternatively you could open a notepad and write down all the information. Next click 'review+create'.
</p>
<p>
<h4>Configuring IP</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/300ecc2c-9bec-4bbb-ba8d-4a0b54913496" height="60%" width="60%"/>
</p>
<p>
Once the Virtual Machine is set up it is necessary to set the IP Configuration to static instead of dynamic, so that the IP will never change. This makes it easy for the Client Computer to connect to the Domain Controller with the same IP every single time. Your path to this setting is: "Home\DomainController\Network settings\domaincontroller631_z1\IP configurations\ipconfig1"
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
I made the username 'Client' and the password is the same as before.
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

<h2>Installing Active Directory</h2>
<p>
To install Active Directory you want to be in the DomainController machine and in the Server Manager App.
</p>
<p>
<h4>Add Roles and Features</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/8ebfd262-91b4-4866-99d0-4e6c1937b8fa" height="60%" width="60%"/>
</p>
<p>
On the home page of Server Manager there is a "Add Roles and Features" button, select it. Once inside click 'next until you can select the services you want to install, here you will select "Active Directory Domain Services". Then you will click on Add Features and install.
</p>
<p>
<h4>Promote Server to Domain Controller</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/aca174d1-e4f2-4884-a9d0-1b40ce28a9e6" height="60%" width="60%"/>
</p>
<p>
In the upper right hand corner of Server Manager there will be a little flag with a one next to it. Click on that and select 'Promote this server to a domain controller'.
</p>
<p>
<h4>Add New Forest</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/b4e1af31-6cbe-4a7a-8912-3e80c74b914d" height="60%" width="60%"/>
</p>
<p>
Next you will want to add a new forest, and call the root domain name whatever you want. For ease of use, I called mine 'example.com'.
</p>
<p>
<h4>Set Password</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/9b1f1202-79a9-47b8-9f23-f605bc92fb9c" height="60%" width="60%"/>
</p>
<p>
Next we will set the password, but it will not be that important as we will not use it again in this project. However, if you were to use this in an actual setting the password would be important. In this case i made it Password1
</p>
<p>
<h4>DNS Delegation</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/d414538a-d2a2-4d30-81f3-05f58dd07049" height="60%" width="60%"/>
</p>
<p>
When you come to this portion of the promotion you want to deselect this option and continue.
</p>
<p>
<h4>NetBIOS Population</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/020d568a-b11f-435e-802b-02724776e336" height="60%" width="60%"/>
</p>
<p>
When you get to this screen it may take a moment for the blank box to populate with the proper name, **DO NOT** enter any other information into the box and then click next.
</p>
<p>
<h4>AD DS Database</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/ce3b840c-4161-49d2-a6c1-e9983da4bf6e" height="60%' width="60%"/>
</p>
<p>
This page should auto populate as well, do not select any options and click next.
</p>
<p>
<h4>Install</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/25f1d7ac-2303-4afc-a91b-2e01d2431469" height="605" width="60%"/>
</p>
<p>
Now that all that is done you can click install. When it begins it may take a while to complete, but once done it will become a proper Domain Controller. The system may need to restart after this, you will just have to log back in afterwards. This time using the Domain we just created.
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/a6fafa1b-1245-43f4-9f81-4f2f9122fb97" heigt="60%" width="60%"/>
</p>
<br />

<h2>Create Domain Administrator</h2>
<p>
Now we can add a user who will be the admin on the Domain, to do that we need to use Active Directory Users and Computers.
</p>
<p>
<h4>Active Directory Users and Computers</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/19548dac-c5d1-45c2-889f-7b12ea847bb6" height="60%" width="60%"/>
</p>
<p>
<h4>Add Organizational Units</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/8c0eaa34-803a-47aa-b3b5-aff3dc9de443" height="60%" width="60%"/>
</p>
<p>
Once you make it into user and computers you will want to selet the file with the name of your domain on it. In my case that would be 'example' right click on it and select new and then organizational unit.
</p>
<p>
<h4>Employees and Users</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/224ab3f5-3bdb-4238-9177-f9ecec0b8ba8" height="60%" width="60%"/>
</p>
<p>
We are going to create two new organizational units, one called _EMPLOYEES and another called _ADMINS
</p>
<p>
<h4>_EMPLOYEES _ADMINS</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/bc0402d9-834e-48b7-b8c4-9d8e2fede314" height="60%" width="60%"
</p>
<p>
Next we need to add a new User that we can make the admin.
</p>
<p>
<h4>New User</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/b2c8408f-85ae-42a8-97e2-43098fc79068" height="60%" width="60%"/>
<p>
Left click inside the _EMPLOYEES Organizational Unit and then new, and user.
</p>
<p>
<h4>John Doe</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/0fe9ab92-9d0a-4606-9d10-cb267a3ec79d" height="60%" width="60%"/>
</p>
<p>
Add a user and call it whatever you'd like. I decided with John Doe. This will be the one we promote to administrator.
</p>
<p>
<h4>Password</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/91e2c06a-8f9e-40fc-b338-1368a534b561" height="60%" width="60%"/>
</p>
<p>
Set the password, I did Password1. No need to have the user change the password on the next login, because we will obviously be the ones using it.
</p>
<p>
<h4>User Properties</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/c1fb7b15-cdcc-47ae-a829-b2f6f3c73046" height="60%" width="60%"/>
</p>
<p>
Next right click on the user you created and select properties
</p>
<p>
<h4>Domain Admins</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/ed20334f-bcce-40ad-9133-9d73a1ddd148" height="60%" width="60%"
</p>
<p>
Select 'Member Of' 'Add' then type 'Domain Admins' and then ok
</p>
<p>
<h4>John Doe Login</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/d66ba841-7106-450d-afb9-1ee6ce998619" height="60%" width="60%"/>
</p>
<p>
Now that we have done that John Doe can now login to the Client Computer using the credentials we created: "example.com\john_admin" "Password1" if done correctly it should login with no problem. We have successfully added an Admin to the Domain
</p>
<br />

<h2>Adding Client to the Domain</h2>
<p>
Now we need to go through the process of putting our Client Computer onto the Domain so it can access Active Directory
</p>
<p>
<h4>Grab DomainController Private IP</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/269c03bb-38ff-462b-9d1c-b8795fcbab9f" height="60%" width="60%"/>
</p>
<p>
We are going to set the DNS of Client to the IP of the Domain Controller, to do that we need to have the Private IP Address and you can find it here.
</p>
<h4>Changing Client DNS</h4>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/ee44df05-db8b-41d0-b370-850e8a4e56ea" height="60%" width="60%"/>
</p>
<p>
Navigate in Azure to Client\Network settings\client512_z1\DNS servers then select custom and add the IP address of the Domain Controller
</p>
<p>
<h4>Client System</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/fd3f232a-ff05-4c25-bc40-3c0111a02b0b" height="60%" width="60%"/>
</p>
<p>
Inside of the Client virtual machine, right click on the windows icon and select 'System' from the menu.
</p>
<p>
<h4>Rename PC</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/df1f924d-c359-4056-9741-2e6f804b58bd" height="60%" width="60%"/>
</p>
<p>
Inside of "System" select 'Rename this PC (Advanced)' on the right hand column
</p>
<p>
<h4>Domain Change</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/2c020c25-aecd-4c7d-a462-b550066476f7" height="60%" width="60%"/>
</p>
<p>
Within the panel 'Computer Name' click 'Change' nect to "To rename this computer or change its domain or workgroup". Set the domain to the one we created in the beginning, for me it is example.com. Then login with the admin we created: "example.com\john_admin" "Password1"
</p>
<p>
<h4>Restart</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/01c86a05-e638-4c73-99ae-5aee0be72f2c" height="60%" width="60%"/>
</p>
<p>
You will need to restart the Virtual Mahcine for this to take effect, it may take some time.
</p>
<p>
<h4>Checking Domain Controller</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/74be5e64-d950-45c2-aa4e-92242ea6f9ae" height="60%" width="60%"/>
</p>
<p>
While the other VM resets, head on over to Domain Controller and navigate to "Active Directory Users and Computers" select "example.com" then "Computers" and ensure that "Client" is within the Organizational Unit. If it is, then you have successfully added Client to the Domain. Next time you login to client you will use john_admin.
</p>
<p>
<h4>Credentials</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/4291a3f3-209f-4530-895a-dd68ffa65db8" height="60%" width="60%"/>
</p>
<br />

<h2>Setting Up Remote Desktop Users</h2>
<p>
To set up remote desktop users you must be signed into Client as example.com\john_doe
</p>
<p>
<h4>Remote Desktop</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/07623781-719e-4429-be2e-2cb2249646fd" height="60%" width="60%"/>
</p>
<p>
To get to this page all you have to do is right click on the Windows icon and click on system. Within the system tab you will click on Remote Desktop on the right hand side of the console.
</p>
<p>
<h4>User Access</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/31be6311-33c2-4158-91bb-e29fbfb51d29" height="60%" width="60%"/>
</p>
<p>
Down at the bottom of this page click the link to 'Select users that can remotely access this PC'. Then you will add the Domain Users, and click ok.
</p>
<br />

<h2>Adding Users</h2>
<p>
Now we will add users to the Domain. This will be users that can log in to "Client" with any username and password. You can go in to the Server window and edit it within the Organization Units, but for this we will run a script. and for that you should be using DomainController and **NOT** Client.
</p>'
<p>
<h4>Windows PowerShell ISE</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/aeedd105-d689-4f1c-9231-b76a2153ef7a" height="60%" width="60%"/>
</p>
<p>
On DomainController you will want to search for "Windows PowerShell ISE" and run it as administrator.
</p>
<p>
<h4>PowerShell Script</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/b070d666-8f50-46f3-87d0-852d1abd6202" height="60%" width="60%"/>
</p>
<p>
When PowerShell opens you will then want to add a script, this will be the little icon underneath File, click there to open a new script.
</p>
<p>
<h4>Script</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/1044f62e-0041-4a09-8469-bc11b1ebd6f7" height="60%" width="60%"/>
</p>
<p>
Upon creating the new Script you will want to navigate to this url: "https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1" and copy this script and paste it in. I created 100 users, but it is set to creat 10,000 users. You can chose how many you want to create, it is only meant to simulate a business with multiple users. Note the password for each user is "Password1"
</p>
<p>
<h4>Picking a User</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/ea35eebc-5792-42a1-889c-59159594fe39" height="60%" width="60%"/>
</p>
<p>
When you run the script you will see a list of new users like this, I am going to pick this random one to sign in with on Client.
</p>
<p>
<h4>Signing in on Client</h4>
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/57bf5506-4bc3-4e76-b1f5-ee967f690c80" height="60%" width="60%"/>
</p>
<p>
As you can see I am logging in with this random user: Job Gir, and his username is: example.com\job.gir with a password of: Password1
</p>
<p>
<img src="https://github.com/CJones226/configure-ad/assets/158533476/42c64eb7-d4f3-470e-89ac-054e5b9d0527" height="60%" width="60%"/>
</p>
<p>
With that done you have just Installed Active Directory, added Admins and Users, have allowed for Network Communication, and added a computer to a Domain. Not to mention added a long list of users to the Domain that can all use different credentials to log in on the same machine. That is how you configure and run Active Directory with Microsoft Azure Virtual Machines.
</p>
<br />




















