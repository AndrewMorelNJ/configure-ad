<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
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

- Setup Domain Controller
- Setup Client
- Ping
- 

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/dXLJ2AM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Setup Domain Controller in Azure by first creating a Resource Group. 
  
Name the group "Active-Directory-Lab".
</p>

<p>
<img src="https://i.imgur.com/sr0aZ2P.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Create a Virtual Network named "Active-Directory-VNet". 

Make sure it uses "Active-Direcory-Lab" as the Resource Group.
</p>

<p>
<img src="https://i.imgur.com/m8Yjue4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Create the Domain Controller VM (Windows Server 2022: Hotpatch) named “DC-1”.

Make sure your size has at least "2 vCPUs & 8 GiB memory".

(User: labuser / Password: Password1!)
</p>

<p>
<img src="https://i.imgur.com/Yl61TYd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Create the Client VM (Windows 10) named “Client-1”.

Make sure your size has at least "2 vCPUs & 8 GiB memory".

(User: labuser / Password: Password1!)
</p>

<p>
<img src="https://i.imgur.com/XYWa6pe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
In the Network Interface, check to see if the Public IP is "Client-1-ip".
</p>

<p>
<img src="https://i.imgur.com/Yto9TFI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
After VM is created, Go to "DC-1" Network settings & click on the primary highlighted above.
</p>

<p>
<img src="https://i.imgur.com/4sSmLp9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Click on "ipconfig1" & set Domain Controller’s NIC Private IP address to be static.
</p>

<p>
<img src="https://i.imgur.com/t28aPdg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Now use "DC-1"s Public IP address and open up Remote Desktop.
</p>

<p>
<img src="https://i.imgur.com/Qn3aP16.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Log into the VM, Right click on the Windows icon and click "Run".

Proceed to type "wf.msc" and click "OK".
</p>

<p>
<img src="https://i.imgur.com/2D0UKX0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Now disable the Windows Firewall (for testing connectivity).
  
Make sure all Firewall states are turned OFF.
</p>

<p>
<img src="https://i.imgur.com/RXEguFU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
After VM is created, set Client-1’s DNS settings to DC-1’s Private IP address & save.
</p>

<p>
<img src="https://i.imgur.com/rXqS1iR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
From the Azure Portal, restart Client-1.

<p>
<img src="https://i.imgur.com/I0f4xZk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Login to Client-1 with Remote Desktop.
</p>

<p>
<img src="https://i.imgur.com/767cvxB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Open PowerShell & Attempt to "Ping" DC-1’s private IP address.

Ensure the ping succeeded.
</p>

<p>
<img src="https://i.imgur.com/wW3m5eA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
From Client-1, open PowerShell and run "ipconfig /all".

The output for the DNS settings should show DC-1’s private IP Address.
</p>

<p>
<img src="https://i.imgur.com/d3uaW7z.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
From DC-1 install Active Directory Domain Services by clicking on "2. Add roles and features".
</p>

<p>
<img src="https://i.imgur.com/fPX21FH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Go to 'Active Directory Domain Services", add features, and install.
</p>

<p>
<img src="https://i.imgur.com/LyWBYnL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Next go to Server Manager to Promote as a DC (click on yellow !): 
</p>

<p>
<img src="https://i.imgur.com/08RakLB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p> 
Setup a new forest as mydomain.com (can be anything, just remember what it is).
  
You can use any password and user for the forest setup.
</p>

<p>
<img src="https://i.imgur.com/gg5O1ok.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p> 
Restart and then log back into DC-1 as user: mydomain.com\labuser
</p>

<p>
<img src="https://i.imgur.com/nitkN8D.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
In Active Directory Users and Computers (ADUC).
</p>

<p>
<img src="https://i.imgur.com/IZMthqN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Create an Organizational Unit (OU) called “_EMPLOYEES”.
</p>
 
<p>
<img src="https://i.imgur.com/xQ8T4R0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>  
Create a new OU named “_ADMINS”.
</p>

<p>
<img src="https://i.imgur.com/NDwZJuX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p> 
Create a new employee in Active Directory.
</p>

<p>
<img src="https://i.imgur.com/gV7aedg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p> 
Name the employee “Jane Doe” (same password) with the username of “jane_admin” / Password1!
</p>

<p>
<img src="https://i.imgur.com/hVcJkuc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p> 
Add jane_admin to the “Domain Admins” Security Group.

Log out / close the connection to DC-1 and log back in as “mydomain.com\jane_admin”.

Use User jane_admin as your admin account from now on.
</p>

<p>
<img src="https://i.imgur.com/kw1tM2d.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p> 
Login to Client-1 as the original local admin (labuser) and join it to the domain (computer will restart).
</p>

<p>
<img src="https://i.imgur.com/bK5YVDt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Login to the Domain Controller and verify Client-1 shows up in ADUC
  
Create a new OU named “_CLIENTS” and drag Client-1 into there.
</p>

<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>



