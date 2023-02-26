<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in Active Directory
- Join Client-1 to your domain
- Setup Remote Desktop for non-administrative users on Client-1

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/0CQPTQl.png"/>
</p>
<p>
First go to virtual machines in Azure
</p>
<br />

<p>
<img src="https://i.imgur.com/T235zKA.png"/>
</p>
<p>
Select create virtual machine
</p>
<br />

<p>
<img src="https://i.imgur.com/scGLmbt.png"/>
</p>
<p>
Create the Domain Controller VM (Windows Server 2022)
</p>
<br />

<p>
<img src="https://i.imgur.com/nECngv6.png"/>
</p>
<p>
Create the Client VM (Windows 10), using the same Resource Group and Vnet that was created for the Domain Controller
</p>
<br />

<p>
<img src="https://i.imgur.com/ch5kxqe.png"/>
</p>
<p>
Go to the Domain Controller and select Networking
</p>
<br />

<p>
<img src="https://i.imgur.com/mpKiIJp.png"/>
</p>
<p>
Select the Network Interface
</p>
<br />

<p>
<img src="https://i.imgur.com/E7sRpiT.png"/>
</p>
<p>
Select ip configurations, and then ipconfig1
</p>
<br />

<p>
<img src="https://i.imgur.com/jpvqsYl.png"/>
</p>
<p>
Change the assignment from dynamic to static
</p>
<br />

<p>
<img src="https://i.imgur.com/Q2v3q82.png"/>
</p>
<p>
Login to Domain Controller with Remote Desktop
</p>
<br />

<p>
<img src="https://i.imgur.com/uRNXVEO.png"/>
</p>
<p>
Go to Windows Firewall
</p>
<br />

<p>
<img src="https://i.imgur.com/dn3wndk.png"/>
</p>
<p>
Go to inbound rules and enable ICMPv4
</p>
<br />

<p>
<img src="https://i.imgur.com/Ndwq0sD.png"/>
</p>
<p>
Open the Server Mager and add roles and features
</p>
<br />

<p>
<img src="https://i.imgur.com/9JVbEZX.png"/>
</p>
<p>
Install Active Directory Domain Services

</p>
<br />

<p>
<img src="https://i.imgur.com/FEenAp8.png"/>
</p>
<p>
Promote as a DC
</p>
<br />

<p>
<img src="https://i.imgur.com/mw48pQP.png"/>
</p>
<p>
Setup a new forest
</p>
<br />

<p>
<img src="https://i.imgur.com/9HvDrmM.png"/>
</p>
<p>
In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”

</p>
<br />

<p>
<img src="https://i.imgur.com/AG4bWNd.png"/>
</p>
<p>
Create a new OU named “_ADMINS”
</p>
<br />

<p>
<img src="https://i.imgur.com/t0LjrcH.png"/>
</p>
<p>
Create a new employee named “Jane Doe” with the username of “jane_admin”
</p>
<br />

<p>
<img src="https://i.imgur.com/lF8JfrL.png"/>
</p>
<p>
Add jane_admin to the “Domain Admins” Security Group
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Close the Remote Desktop connection and log back in as jane_admin
</p>
<br />

<p>
<img src="https://i.imgur.com/5XHjmwg.png"/>
</p>
<p>
From the Azure Portal, go to the Client VM, then Networking
</p>
<br />

<p>
<img src="https://i.imgur.com/5XHjmwg.png"/>
</p>
<p>
Then go to Network Interface
</p>
<br />

<p>
<img src="https://i.imgur.com/P4ImN5O.png"/>
</p>
<p>
Then DNS settings
</p>
<br />

<p>
<img src="https://i.imgur.com/dA8xl7u.png"/>
</p>
<p>
Change the DNS server to the private IP of the Domain Controller
</p>
<br />

<p>
<img src="https://i.imgur.com/oIX2aPt.png"/>
</p>
<p>
Login to Client-1 (Remote Desktop) as the original local admin (labuser) and go to System
</p>
<br />

<p>
<img src="https://i.imgur.com/mEKGgDX.png"/>
</p>
<p>
In System, click on Rename This PC
</p>
<br />

<p>
<img src="https://i.imgur.com/AG5sl3s.png"/>
</p>
<p>
The click on change
</p>
<br />

<p>
<img src="https://i.imgur.com/ZYenrt6.png"/>
</p>
<p>
Join Client to the domain controller
</p>
<br />

<p>
<img src="https://i.imgur.com/RvYkueJ.png"/>
</p>
<p>
Login to the Domain Controller, and create a new OU named “_CLIENTS” and drag Client-1 into there
</p>
<br />

<p>
<img src="https://i.imgur.com/ct3iQ8e.png"/>
</p>
<p>
Log into Client-1 and open system properties
</p>
<br />

<p>
<img src="https://i.imgur.com/Hxn1MO9.png"/>
</p>
<p>
Click “Remote Desktop” and then “Select users that can remotely access this pc”

</p>
<br />

<p>
<img src="https://i.imgur.com/35HpQBd.png"/>
</p>
<p>
Allow “domain users” access to remote desktop
</p>
<br />

