# configure-ad
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
Welcome Back! This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />



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
- Ensure Connection between Client and Domain Controller
- Install Active Directory and Admin Creation
- Create X-Amount of Client Users using PowerShell Script

<h2>Setup Resources in Azure</h2>
<p>
<img src="https://i.imgur.com/9OK8994.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
1. Create the Domain Controller VM (Windows Server 2022) named “DC-1"
   Take note of the Resource Group and Virtual Network (Vnet) that get created at this time
2. Set Domain Controller’s NIC Private IP address to be static
DC-1 > Networking > NIC > IP Configurations
</p>
<br />

<p>
<img src= "https://i.imgur.com/DWvn7I9.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
3. Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in the DC-1 step.
4. Ensure that both VMs are in the same Vnet [you can check the topology with Network Watcher]
Here is an illustration of what we are doing:
</p>
<br />
<p>
<img src="https://i.imgur.com/ThAaeTv.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/wgf8l75.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/></p>
</p>

</p>DC-1 has to have a static Private IP Address. Client one will connect to DC-1 to ensure connectivity we will try to ping DC-1 from Client-1. At first the ping will not work correctly. We have to enable ICMPv4 on the firewall on DC-1. Now we can ping DC-1 successfully from Client-1

<h2>Ensure Connection between Client and Domain Controller<h2>

 <img src="https://i.imgur.com/HvZBWzc.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
  <img src="https://i.imgur.com/1lrrGPw.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
  
 <h2>Install Active Directory<h2>

 1. Login to DC-1 and install Active Directory Domain Services
    
 
 - Server Manager > "Add Roles and Features" > Check "Active Directory Domain Services"
 ![vivaldi_od5BgUKG6G](https://user-images.githubusercontent.com/109401839/213214935-0fe230d0-60be-431a-bf31-53cfc50748b9.png)
 <img src="https://i.imgur.com/D0jC4Eg.jpg" height="60%" width="60%" alt="Disk Sanitization Steps"/>
    
 Promote the VM to DC, setup a new forest as "mydomain.com" afterwards restart then log back into DC-1 as user: "mydomain.com\labuser". If you performed the steps properly you should be able to run AD Users & Computers as shown below.  
