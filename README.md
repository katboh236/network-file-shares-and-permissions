<p align="center">
<img src="https://i.imgur.com/AeiqMDZ.png" alt="Traffic Examination"/>
</p>

<h1>Network-File-Shares-and-Permissions</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. We will create folders in the DC-1 VM and share them on the network. Only designated people will be able to view certain files and certain files will have certain permissions. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Domain Controller/Client Machine)
- Remote Desktop
- Shared Network Files

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Active Directory running i Azure on a Virtual Machine (DC-1 - Domain Controller)
- Client Machine running in Azure on a Virtual Machine (Client-1) and joined to the domain

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Sample File Shares with Various Permissions
- Attempt to Access File Shares as a Normal User
- Create "ACCOUNTANTS" Security Group, Assign Permissions, and Test Access

<h2>Deployment and Configuration Steps</h2>
</p>
<p>
<img src="https://imgur.com/TMLtHLZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Connected into DC-1 as domain admin account (mydomain.com\jane_admin), connected into Client-1 as a normal user - buda.hes. On DC-1, on the C:\ drive, created 4 folders: "read-access", "write-access", "no-access", "accounting".
</p>
<br />
<p>
<img src="https://imgur.com/BzjhPv1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Set up following permissions for the "Domain Users" group: folder: "read-access" => group: "Domain users" => permission: "Read"; folder: "write-access" => group: "Domain Users" => permissions: "Read/Write"; folder: "no-access" => group: "Domain Admins" => permissions: "Read/Write".
</p>
<br />
<p>
<img src="https://imgur.com/C9ff8Zr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On Client-1, navigated to the shared folder (start, run, \\dc-1). Tried to access folders to see how permissions work.
</p>
<br />
<p>
<img src="https://imgur.com/5kqkRWW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://imgur.com/vApYZrU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On DC-1, in ACtive Directory, created Security Group called "ACCOUNTANTS". On the "accounting" folder created earlier, set following permissions: folder: "accounting" => group: "ACCOUNTANTS" => permissions: "Read/Write". 
</p>
<br />
<p>
<img src="https://imgur.com/OZn7Ics.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On Client-1, as <buda.hes> user tried to access the "ACCOUNTANTS" folder and it failed as log out of Client-1 is needed.
</p>
<br />
<p>
<img src="https://imgur.com/fbeHmWt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://imgur.com/ji62yUD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On DC-1, made "buda.hes> user a member of the "ACCOUNTANTS" Security Group, signed back to Client-1 as <buda.hes>, tried to access the "accounting" share in \\dc-1 and it worked. Success!
</p>
<br />
