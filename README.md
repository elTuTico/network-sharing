<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Network Sharing On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the utilization of on-premises Active Directory within Azure Virtual Machines to gain a deep understanding of file sharing.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Sample Files
- Configure Sample Files permissions
- Attempt to utilize a User to access the Sample Files
- Create a new Security Group to accesss the Sample Files

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://github.com/elTuTico/network-sharing/assets/137955237/057287fc-cd58-4064-adcd-da76f13503d4" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Remote Desktop into the DC with the Domain Admin account made from the previous exercise; username: mydomain.com\alex_admin password: Password1. 
</p>
<br />

<p>
<img src="https://github.com/elTuTico/network-sharing/assets/137955237/16ede9a4-3b3f-4cc1-8ab0-e9ae8c25186f" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Utilizing one of the 1000 Users made through the script ran on Powershell ISE, Remote Desktop into Client; username: mydomain.com\baton.von password: Password1.
</p>
<br />

<p>
<img src="https://github.com/elTuTico/network-sharing/assets/137955237/abc04193-284b-436d-94ea-a9e055fd6993" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Within the DC open up the C:/ drive to create four folders named: “read-access”. “write-access”, “no-access”, and “accounting”. For each one of these the Properties of each folder will be altered to expand the Network Sharing possibilities of the DC.
</p>
<br />

<p>
<img src="https://github.com/elTuTico/network-sharing/assets/137955237/32043e57-07f4-4010-8711-fc5638ea2f50" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
“Read-access” folder will be shared by right clicking on the folder, properties, clicking “Share” and adding “Domain Users” with the "Read" permission granted.
</p>
<br />

<p>
<img src="https://github.com/elTuTico/network-sharing/assets/137955237/ad45b960-f630-499c-af7b-2dbb9d864de5" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
“Write-access” folder will be shared by right clicking on the folder, properties, clicking “Share” and adding “Domain Users” with the "Read/Write" permission granted.
</p>
<br />

<p>
<img src="https://github.com/elTuTico/network-sharing/assets/137955237/47e23b17-b50c-4d3d-88bc-5ca95694c82b" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
“No-access” folder will be shared by right clicking on the folder, properties, clicking “Share” and adding “Domain Admins” with the "Read/Write" permission granted. This will prevent All Users not within the _ADMIN Organizational Unit access to this folder. 
</p>
<br />

<p>
<img src="https://github.com/elTuTico/network-sharing/assets/137955237/b3da8b7c-72f0-44b2-b976-0369392bc730" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Utilizing the Client open up a File Explorer window and on the top search bar navigate to \\dc. From there all of the shared files/folders on the DC should be shown. 
</p>
<br />

<p>
<img src="https://github.com/elTuTico/network-sharing/assets/137955237/9e620381-7f70-4cc5-a0d0-ac101e54282f" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://github.com/elTuTico/network-sharing/assets/137955237/bc30831c-62d9-4b0b-8b8d-82a417a1d180" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://github.com/elTuTico/network-sharing/assets/137955237/b2c8ab9e-5c5c-4340-b9ac-5ea4a329e09e" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Navigate through the folders to see the access that was or wasn’t granted to the User that is being used to access the DC through the Client. 
</p>
<br />

<p>
<img src="https://github.com/elTuTico/network-sharing/assets/137955237/0542008f-39c3-4b19-ae8d-55900f285206" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://github.com/elTuTico/network-sharing/assets/137955237/7a5c195b-a8a9-4868-9e9a-86a80b5b6378" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Back on the DC, navigate to the “Active Directory Users and Computers” and create a new Organization Unit named “_SECURITY_GROUP”. Within that Unit create a new “Group” named “ACCOUNTANTS” with the "Group Type" being Security. 
</p>
<br />

<p>
<img src="https://github.com/elTuTico/network-sharing/assets/137955237/3edb0af4-fa17-478e-b883-c11e361b738b" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Within the DC's C:// drive create another folder named “accounting” that will be shared by right clicking on the folder, properties, clicking “Share” and adding “ACCOUNTANTS” with the "Read/Write" permission granted. This will prevent All Users not within the ACCOUNTANT Organizational Unit access to this folder. 
</p>
<br />

<p>
<img src="https://github.com/elTuTico/network-sharing/assets/137955237/9b016635-45b5-498a-ae37-6f36c379ecf6" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Utilizing the Client open up a File Explorer window and on the top search bar navigate to \\dc. From there the “accounting” folder should be visible, but not accessible.
</p>
<br />

<p>
<img src="https://github.com/elTuTico/network-sharing/assets/137955237/ccce7006-43e0-4ec8-b1f2-fe441b428b0d" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To grant the user that is utilizing the Client return to the “ACCOUNTANTS” “_SECURITY_GROUP” within the DC’s Active Directory Users and Computers. Open the Group up, navigate to Members, and search up the name of the End User logged into the Client. 
</p>
<br />

<p>
<img src="https://github.com/elTuTico/network-sharing/assets/137955237/3f40f09d-509d-4c17-bf73-d18f4a00126f" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Ensure to log out and back into the Client with the User to ensure that the new permissions are registered when trying to access folders on the C:// drive. That User should now be able to not only open the folder, but also create new documents within this folder that not even Domain Admins can access. 
</p>
<br />
