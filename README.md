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



<h2>Lab Prerequisites</h2>

This lab builds on the Active Directory environment created in the following project:

[Active Directory Domain Deployment in Azure](https://github.com/chrisdegutis/ad-domain-deployment)

The environment includes:

- A Domain Controller (DC-1)
- A domain-joined client machine (Client-1)
- Organizational Units for users and client machines
- Multiple domain user accounts



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
<b>This lab demonstrates common <b>Active Directory user management</b> and <b>identity security</b> operations performed by system administrators. Using the domain environment deployed in the previous lab, the following tasks are performed:</b>
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

<h2>Deployment and Configuration Steps</h2>

<h3>Step 1: Configure Account Lockout Policy</h3>
<p>
Log into <b>DC-1</b> using the administrative account <b>mydomain.com\jane_admin</b>.
</p>
<p>
Open <b>Group Policy Management</b> by selecting <b>Tools → Group Policy Management</b> from <b>Server Manager</b>.
</p>
<p>
In <b>Group Policy Management</b>, right-click <b>mydomain.com</b> and select <b>Create a GPO in this domain, and Link it here</b>. Name the policy <b>Account Lockout Policy</b>.
</p>
<p>
Right-click the newly created GPO and select <b>Edit</b>. Navigate to:
</p>
<p>
<b>Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Account Lockout Policy</b>
</p>
<p>
Set the <b>Account Lockout Threshold</b> to <b>5 invalid logon attempts</b>. This policy will automatically lock a user account after five failed authentication attempts.
</p>
<img width="800" height="1552" alt="image" src="https://github.com/user-attachments/assets/b0f5a02f-ef76-437d-a64b-e9b6271ff59d" />
<p>
Next, log into <b>Client-1</b> using <b>mydomain.com\jane_admin</b>. Open <b>PowerShell</b> and run the following command to update Group Policy immediately:
</p>
<p>
<pre><code>gpupdate /force</code></pre>
</p>
<p>
This ensures the newly configured account lockout policy is applied to the client machine before proceeding with the next steps.
</p>
<img width="800" height="1012" alt="image" src="https://github.com/user-attachments/assets/5367ad06-fe20-4310-9fe4-55602cdd7a4e" />
<hr>

<h3>Step 2: Trigger an Account Lockout</h3>
<p>
On <b>DC-1</b>, open <b>Active Directory Users and Computers (ADUC)</b> and within the <b>_EMPLOYEES OU</b> select a random user account that was created in the <a href="https://github.com/chrisdegutis/ad-domain-deployment">previous lab</a>.
</p>
<p>
<b>Double-click</b> (or right-click > properties) and in the <b>Account</b> tab, take note of the <b>user logon name</b>. In this lab, I will be using <b>John Baker (jbaker)</b> with the password <b>Password1</b>.
</p>
<p>
From your local machine, open <b>Remote Desktop Connection</b> and attempt to log into <b>Client-1</b> using the selected domain user account <b>(mydomain.com\jbaker)</b>.
</p>
<p>
Enter an incorrect password and attempt to log in 6-7 times. After exceeding the configured threshold of <b>5 failed login attempts</b>, the account will become locked due to the account lockout policy configured earlier.
</p>
