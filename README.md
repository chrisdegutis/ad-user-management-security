<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1><h1>Active Directory User Management and Security Policies</h1></h1>
<p>
This lab demonstrates common <b>Active Directory user management</b> and <b>identity security</b> tasks performed by system administrators in enterprise environments. Using the domain environment previously deployed in Microsoft Azure, the lab focuses on managing user accounts and enforcing authentication security policies within <b>Active Directory Domain Services (AD DS)</b>.
</p>
<p>
The exercises include configuring <b>account lockout policies through Group Policy</b>, triggering and resolving account lockouts, resetting user passwords, enabling and disabling domain accounts, and reviewing authentication events in <b>Windows Event Viewer</b>. These tasks simulate real-world identity management and security operations commonly handled by IT administrators and security teams.
</p>



## Lab Prerequisites

This lab builds on the Active Directory environment created in the following project:

**Active Directory Domain Deployment in Azure**

The environment includes:

- A Domain Controller (DC-1)
- A domain-joined client machine (Client-1)
- Organizational Units for users and client machines
- Multiple domain user accounts

If you have not completed that lab, follow the setup instructions here:

[https://github.com/chrisdegutis/ad-domain-deployment](https://github.com/chrisdegutis/ad-domain-deployment)
<hr>

<h2>Environments and Technologies Used</h2>

<ul>
<li>Microsoft Azure (Virtual Machines / Compute)</li>
<li>Remote Desktop Protocol (RDP)</li>
<li>Active Directory Domain Services (AD DS)</li>
<li>Group Policy Management</li>
<li>Windows Event Viewer</li>
<li>Authentication and Security Policies</li>
</ul>

<h2>Operating Systems Used</h2>

<ul>
<li>Windows Server 2025 Datacenter (Domain Controller)</li>
<li>Windows 10 Enterprise (Domain Client)</li>
</ul>

<h2>High-Level Deployment and Configuration Steps</h2>

<p>
This lab demonstrates common <b>Active Directory user management</b> and <b>identity security</b> operations performed by system administrators. Using the domain environment deployed in the previous lab, the following tasks are performed:
</p>

<ul>
<li>Ensuring the Domain Controller and client virtual machines are running in the Azure environment</li>

<li>Configuring <b>Account Lockout Policies</b> through <b>Group Policy</b> to enforce authentication security controls</li>

<li>Triggering multiple failed login attempts to simulate a user account lockout</li>

<li>Identifying and unlocking a locked user account within <b>Active Directory Users and Computers (ADUC)</b></li>

<li>Resetting user passwords and restoring account access</li>

<li>Disabling and re-enabling domain user accounts to simulate administrative account management tasks</li>

<li>Reviewing authentication activity in <b>Windows Event Viewer</b> to observe failed logins, successful authentications, and account lockout events</li>
</ul>
