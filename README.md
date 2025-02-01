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
<img src="https://github.com/user-attachments/assets/e5acfe58-529d-4fa9-8c37-68a3ee171266" height="75%" width="100%"/>
</p>
<p>
Reconnect but make sure to use your domain name in the username followed by your account name</p>
<br />









