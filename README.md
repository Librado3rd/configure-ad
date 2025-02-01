<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" height="40%" width="70%"alt="Microsoft Active Directory Logo"/>
</p>

<h1>Configuring Active Directory (On-Premises) Within Azure</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Resources
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (myadproject.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>
<p>
  Setup Resources in Azure
  <img src="https://github.com/user-attachments/assets/7616c794-f7e2-487a-b9bb-f34e8a90f2bd" height="75%" width="100%"/>
</p>
<p>
Create the resource group to house your network
</p>
<br />

<p>
  <img src="https://github.com/user-attachments/assets/59a250c0-5caf-4b44-860d-756336bf4d64" height="75%" width="100%"/>
</p>
<p>
Create the virtual network to house your virtual machines
</p>
<br />

<p>
  <img src="https://github.com/user-attachments/assets/98ff75ce-c545-4b00-8f33-26b2f0d45156" height="75%" width="100%"/>
</p>
<p>
Create the Domain Controller VM (Windows Server 2022) named “DC-1”
</p>
<br />

<p>
  <img src="https://github.com/user-attachments/assets/d681adb5-3441-44a9-b7f4-3911b61bd544" height="75%" width="100%"/>
</p>
<p>
Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in previous step:
</p>
<br />

<p>
  <img src="https://github.com/user-attachments/assets/a203463f-d871-428f-8feb-1e6905394ace" height="75%" width="100%"/>
</p>
<p>
Set Domain Controller’s NIC Private IP address to be static:
</p>
<br />

<p>
  <img src="https://github.com/user-attachments/assets/5e99eb89-b6a9-4e01-9099-fca45cf9fe9c" height="75%" width="100%"/>
</p>
<p>
Remote Control into your Domain Controller (VM-DC-1) and disable the 3 firewalls.
</p>
<br />

<p>
  <img src="https://github.com/user-attachments/assets/ae1c3f87-5383-466d-8ca6-e6e818a13023" height="75%" width="100%"/>
</p>
<p>
Change the DNS server of The Virtual machine (Client-1) so it points to the private Ip address of the Domain Controller (VM-DC-1)
</p>
<br />

<p>
  Ensure Connectivity between the client and Domain Controller
  <img src="https://github.com/user-attachments/assets/18c853df-6c43-4b10-8a41-1413da457752" height="75%" width="100%"/>
</p>
<p>
Log onto the Virtual machine (client-1) and use Powershell to ping to the Domain Controller (VM-DC-1) if the ping is successful you’ve connected to your virtual network.
</p>
<br />

<p>
Install Active Directory
<img src="https://github.com/user-attachments/assets/654ecb1b-985a-435b-a81b-e470e936394c" height="75%" width="100%"/>
</p>
<p>
Login to Virtual Machine (VM-DC-1) and install Active Directory Domain Services:
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/c5282673-ad75-4747-9a66-a2ca35c62f11" height="75%" width="100%"/>
</p>
<p>
Promote to a Domain Controller: When choosing the root domain name you can choose any website, i used mydomain.com. Once the process is finished the VM will restart.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/e5acfe58-529d-4fa9-8c37-68a3ee171266" height="75%" width="100%"/>
</p>
<p>
Reconnect but make sure to use your domain name in the username followed by your account name</p>
<br />

<p>
Create an Admin and Normal User Account in AD
<img src="https://github.com/user-attachments/assets/b84330b2-366e-485f-976a-66fd859cb4c6" height="75%" width="100%"/>
</p>
<p>
In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES” and another one called "_ADMINS":
<br />

<p>
<img src="https://github.com/user-attachments/assets/6464dc6d-d975-4dcf-896f-59b10cdfd4c0" height="75%" width="100%"/>
</p>
<p>
Create a new employee named “Jane Doe” with the username of “jane_admin”
<br />

<p>
<img src="https://github.com/user-attachments/assets/b34d72e6-93e8-4ffc-aec3-0bb2eec17ac7" height="75%" width="100%"/>
</p>
<p>
Add jane_admin to the “Domain Admins” Security Group
<br />

<p>
<img src="https://github.com/user-attachments/assets/59e5cb23-3d40-45dc-b761-b29516e31573" height="75%" width="100%"/>
</p>
<p>
Log out & close the Remote Desktop connection to DC-1 and log back in as “myadproject.com\jane_admin”. Use jane_admin as your admin account from now on: 
<br />

<p>
Join Client-1 to your domain (myadproject.com)
<img src="https://github.com/user-attachments/assets/fb0c897c-f12b-441e-b28c-f0b0f2442735" height="75%" width="100%"/>
<img src="https://github.com/user-attachments/assets/8a65f162-d97e-44db-9af6-8137152a1fdc" height="75%" width="100%"/>
</p>
<p>
Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart). Make sure to login to the right domain account.
<br />

<p>
<img src="https://github.com/user-attachments/assets/ce52cc5c-855e-4cec-be77-d50f528ff459" height="75%" width="100%"/>
</p>
<p>
Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain.
<br />

<p>
Setup Remote Desktop for non-administrative users on Client-1
<img src="https://github.com/user-attachments/assets/7497c3e5-7778-4b46-9ac6-0b92f4440218" height="75%" width="100%"/>
</p>
<p>
Create a new OU named “_CLIENTS” and drag Client-1 into there
<br />

<p>
<img src="https://github.com/user-attachments/assets/bac8f763-38e2-4300-ac8a-6a01de6a2d2a" height="75%" width="100%"/>
</p>
<p>
Log into Client-1 as [mydomain.com](http://mydomain.com/)\jane_admin and open system properties.

Click “Remote Desktop”.

Allow “domain users” access to remote desktop.

You can now log into Client-1 as a normal, non-administrative user now.

Normally you’d want to do this with Group Policy that allows you to change MANY systems at once
<br />

<p>
Create a bunch of additional users and attempt to log into client-1 with one of the users
<img src="https://github.com/user-attachments/assets/77487dc3-fa23-4c02-8f35-207166d52c6e" height="75%" width="100%"/>
</p>
<p>
Login to DC-1 as jane_admin

Open PowerShell_ise as an administrator.

Create a new File and paste the contents of this script (https://github.com/Xinloiazn/configure-ad/blob/main/adscript.ps1) into it
<br />

<p>
Run the script
<img src="https://github.com/user-attachments/assets/f32d0928-6f06-479f-aa01-d9bbd1bf87ed" height="75%" width="100%"/>
<img src="https://github.com/user-attachments/assets/8dbf6e9a-539d-409d-8f3a-06293e88a17f" height="75%" width="100%"/>
</p>
<p>
Run the script and observe the accounts being created. When finished, open ADUC and observe the accounts in the appropriate OU and attempt to log into Client-1 with one of the accounts (take note of the password in the script)
<br />

<p>
Login to one of the accounts
<img src="https://github.com/user-attachments/assets/1a24e709-9b2b-4649-be37-df5beaa5c7f5" height="75%" width="100%"/>
<img src="https://github.com/user-attachments/assets/4a465b3d-cb22-47fd-ab26-89a3229e5d63" height="75%" width="100%"/>
</p>
<p>
As you can see, we were able to login to one of the many account created.
<br />

<p>
Summary:
<img src="https://github.com/user-attachments/assets/280ed302-c836-4757-8a11-5da2afcd1b04" height="75%" width="100%"/>
</p>
<p>
I hope this tutorial helped you learn a little bit about network security protocols and observe traffic between virtual machines. This can be easily done on a PC or a Mac. Mac would just have an extra step to download the Remote Desktop App.
<br />
