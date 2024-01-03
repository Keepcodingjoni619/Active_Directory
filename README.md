# Active_Directory
<p>Active Directory is a built in software that maintains Microsoft by centrally managing user accounts in a single place (Accounts, Passwords, Permissions). It helps with managing devices and control access to resources.</p>

<h3>Setup Resources in Azure</h3>
<ol>
  <li>Create the Domain Controller VM (Windows Server 2022) named “DC-1”</li>
  <li>Set Domain Controller’s NIC Private IP address to be static</li>
  <li>Create the Client VM (Windows 10) named “Client-1”</li>
  <li>Ensure that both VMs are in the same Vnet</li>
  
</ol>

![AD_01](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/013561bc-c3ae-41d5-a755-e3cf4099bc29)

![AD_02](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/f9b55c49-e85f-4b7f-b60c-340e046eb27d)

<h3>Ensure Connectivity between the client and Domain Controller</h3>
<ol>
 <li>Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t </li>
 <li>Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall</li>
 <li>Check back at Client-1 to see the ping succeed</li>
</ol>

![AD_03](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/180802a4-1ad9-4aff-9b71-90ab991c9fc5)

![AD_04](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/6bbdc6ef-2e67-41c6-ab64-3a1fae82b667)

<h3>Install Active Directory</h3>
<ol>
  <li>Login to DC-1 and install Active Directory Domain Services</li>
  <li>Promote as a DC: Setup a new forest as mydomain.com</li>
  <li>Restart and then log back into DC-1 as user: mydomain.com\labuser</li>
</ol>

![AD_05](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/aeedd7c1-779e-4e98-ab06-ce81b7d1ace6)

![AD_06](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/9cb6a437-9f34-4ae5-b789-4ca316595e0e)

<h3>Create an Admin and Normal User Account in AD</h3>
<ol>
  <li>In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”</li>
  <li>Create a new OU named “_ADMINS”</li>
  <li>Create a new employee named “Will Ferrell” (same password) with the username of “will_admin”</li>
  <li>Add will_admin to the “Domain Admins” Security Group
  <li>Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\will_admin”</li>
  <li>User will_admin will remain as your admin account </li>

</ol>

![AD_07](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/7539d0e7-ad1a-4512-829c-e076f34917fa)


![AD_08](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/1c29a7c6-5979-4f52-9e37-53d8ed0951df)

![AD_09](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/52a8ee26-842b-4c37-b75e-0fa7114b027c)

![AD_10](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/f9cc96e0-0d3d-46f5-ad3a-2fe454f32f0b)

<h3>Join Client-1 to your domain (mydomain.com)</h3>
<ol>
  <li>From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address</li>
  <li>From the Azure Portal, restart Client-1</li>
  <li>Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)</li>
  <li>Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain</li>
  <li>Create a new OU named “_CLIENTS” and drag Client-1</li>
</ol>

![AD_11](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/0636c717-8dcc-44eb-adef-4d9aa6327ec3)

![AD_12](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/2f64bb6c-477a-49ec-9e23-acba037784af)

<h3>Setup Remote Desktop for non-administrative users on Client-1</h3>
<ol>
  <li>Log into Client-1 as mydomain.com\will_admin and open system properties</li>
  <li>Allow “domain users” access to remote desktop</li>
</ol>

![AD_13](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/f62cad68-8b9a-4b84-af08-bf260fea9467)

<h3>Create a bunch of additional users and attempt to log into client-1 with one of the users</h3>
<ol>
  <li>Login to DC-1 as will_admin</li>
  <li>Open PowerShell_ise as an administrator</li>
  <li>When finished, open ADUC and observe the accounts in the appropriate OU</li>
  <li>attempt to log into Client-1 with one of the accounts</li>
</ol>

![AD_14](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/244053d4-6e16-4af3-92b5-b19bedb8be17)

![AD_15](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/c4c512c5-5064-4dc5-91c5-fd5a561e69e1)

![AD_16](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/a57ac9cf-524a-4099-a024-e6aa2a9dd847)

<p>I used powershell to populate 10,000 users from scripts I found through GitHub and made slight changes like the password</p>

![AD_17](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/e420fb40-2aa3-4037-8cf2-7d5e8ff093e7)

![AD_18](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/f401c24c-8d4f-4d62-ab3e-9ce67787cf23)

<h3>Using different user accounts </h3>
<p>The rest was to practice on learning Account Lockouts to Unlocks</p>
<p>Resetting Passwords</p>

![AD_19](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/ed8d0086-59cc-45ee-8bb6-24c2fb729592)

![AD_20_Lock](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/ae39eae6-6bb5-48bc-a942-8b0a38b3a089)

![AD_21_Unlock](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/b703cc79-1740-4cd6-a6a9-12d51499d59d)

![AD_22_Reset_PW](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/69da2fcc-478d-4619-9ee5-e6e7eee6319a)

![AD_23_dod](https://github.com/Keepcodingjoni619/Active_Directory/assets/82996237/627a6adc-bf01-4a37-9f4d-f35e0b8431bc)
