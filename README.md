<h1>Nessus Essentials Vulnerability Management Lab</h1>

<h2>Description</h2>
This is a walkthrough of how I created A Virtual Machine environment using VMWare running Windows 10. I did this project to gain experience with Nessus Essentials and learn how to scan for vulnerabilities and remediate them. This project will showcase two of the main steps in the Vulnerability Management Lifecycle. I will be using Nessus Essentials to scan local VMs hosted on VMWare Workstation in order run credentialed scans to discover vulnerabilities, remediate some of the vulnerabilities, then perform a rescan to verify remediation.
<br />

<h2>Utilities Used</h2>

- <b>Nessus Essentials</b> 
- <b>CMD</b>

<h2>Environments Used </h2>

- <b>VMWare</b>
- <b>Windows 10</b> (21H2)

<h2>Links</h2>

- <b>VMWare Workstation Pro:</b> https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html
- <b>Nessus Essentials:</b> https://www.tenable.com/products/nessus/nessus-essentials
- <b>Windows 10 ISO:</b> https://www.microsoft.com/en-us/software-download/windows10

<h2 align="center">Program walk-through</h2>

<p align="center">
<b>The first thing I am going to do is Download Nessus Essentials, my Vulnerability management software. It takes a long time to download so I can accomplish a few things while it is downloading, like downloading Windows 10 on a Virtual Machine and configuring it (which also takes a long time)</b> <br/>
</p>

![Downloading Nessus](https://user-images.githubusercontent.com/108043108/177885108-9e637032-e965-4ecb-8166-b6931dc2dcff.JPG)

<br />
<br />
<p align="center">
<b>For the Virtual Machine that I will be managing vulnerabilities on, I have to configure the network adapter to be bridged so it can be on the same network as my native. I do this because Nessus has to Secure Server Login (SSL) into the Virtual Machine and it's just easier if it's using my local network.</b> <br/>
</p>

![Configure_Network_Adapters](https://user-images.githubusercontent.com/108043108/177885541-29039f1c-6217-43b4-92ca-86a60d092d3b.JPG)

<br />
<br />
<p align="center">
<b>Nessus at this point is still downloading and my Virtual Machine successfully downloads Windows 10, so I open up CMD to figure out it's IP address which I will need to be able to run vulnerability scans on Nessus. I named the VM Admin. The screenshot shows that the IP address is 192.168.50.185</b> <br/>
</p>

![VM_IP](https://user-images.githubusercontent.com/108043108/177885744-426519f2-bd27-406c-a6eb-f71ef5a6bdcb.JPG)

<br />
<br />
<p align="center">
<b>I try to ping the VM from my native computer to see if I can communicate with the VM. The reason I am doing this is because of I can't ping the VM then Nessus won't be able to as well and can't run its scans. As we can see the pings are timing out, meaning my native PC can't establish a connection with it at the moment.</b> <br/>
</p>

![trying_to_ping_VM_Fails](https://user-images.githubusercontent.com/108043108/177886078-cec7b98b-60da-47a6-8e70-838a649a456f.JPG)

<br />
<br />
<p align="center">
<b>The reason my PC can't establish a connection is because the VM has a firewall active and it is blocking all connection attempts (which is a good thing, but not for the purposes of this lab) so I have to disable the firewalls. This is something I would NEVER do in a production environment as it could and would be catastrophic, but this is a just a junk VM so no worries.</b> <br/>
</p>

![windows_firewall_disable](https://user-images.githubusercontent.com/108043108/177886413-df1ba042-8e42-4ff6-a004-0057ac793cd1.JPG)

<br />
<br />
<p align="center">
<b>I have to turn off all three firewalls which are circled at the top in Red, Blue, and Green. Circled in Yellow is showing that the firewalls are currently On. I have to turn them Off to be able to communicate properly with the VM.</b> <br/>
</p>

![Turning_off_Firewalls](https://user-images.githubusercontent.com/108043108/177886437-e6b4addf-99e3-455f-b46f-c3941a433109.JPG)

<br />
<br />
<p align="center">
<b>Now that the VM's firewall is disabled, I try to Ping it again from my native PC and this time it is successful.</b> <br/>
</p>

![Ping_works](https://user-images.githubusercontent.com/108043108/177887412-f8078e7b-13a3-4480-b000-5ae84108cfab.JPG)

<br />
<br />
<p align="center">
<b>By this time Nessus Essentials successfully downloads. The first thing I want to do is create a new scan, then select Basic Network Scan.</b> <br/>
</p>

![Create_New_Scan](https://user-images.githubusercontent.com/108043108/177887661-793476e8-7e68-4c21-8983-8f955d7cff2e.JPG)

![basic_network_scan](https://user-images.githubusercontent.com/108043108/177887672-2d955508-edf1-4735-b78a-2836a81d2c9f.JPG)


<br />
<br />
<p align="center">
<b>The newly created scan asks me to name the scan and select a target to scan. I configure it to scan the VM's IP address which is 192.168.50.185</b> <br/>
</p>

![Scan_VM_IP](https://user-images.githubusercontent.com/108043108/177887914-87a2da10-be51-481c-a672-ec1104e3df7a.JPG)

<br />
<br />
<p align="center">
<b>I launch the newly created scan and it immediately goes to work scanning for any known vulnerabilities. When the grey checkmark appears, the scan is complete.</b> <br/>
</p>

![Launch_newly_created_scan](https://user-images.githubusercontent.com/108043108/177888041-95c53001-b8d2-4355-9311-3ee2637dff94.JPG)

![Scan_Running](https://user-images.githubusercontent.com/108043108/177888049-661dddfc-ebe0-42cf-ad87-14bc5af53fe5.gif)

![Scan_Completed](https://user-images.githubusercontent.com/108043108/177888068-25d4a86a-c150-4e77-a993-9df4178c5ba1.JPG)

<br />
<br />
<p align="center">
<b>Lets look at the results! It is showing 33 results, 32 of which are info and 1 low. If this was an actual production environment these most likely would be left alone. The Info results are probably because some things don't have proper credentials and are not essentially vulnerabilities</b> <br/>
</p>

![Results_Of_Scan](https://user-images.githubusercontent.com/108043108/177888196-3141c52f-df79-4c58-9fee-5daa68d78c5b.gif)

<br />
<br />
<p align="center">
<b>Looking at one of the INFO results you can see that the Target Credential Status By Authentication Procotol was triggered because we did not actually provide any credentials for this scan.</b> <br/>
</p>

![No_credentials_Given](https://user-images.githubusercontent.com/108043108/177888648-5679c8c1-e8ce-47e3-a424-067375964054.JPG)

<br />
<br />
<p align="center">
<b>Next thing I do is configure the VM to be able to accept authenticated scans and provide credentials to Nessus. I will then rescan the VM and compare the results. I go to services.MSC to start this process and enable Remote Registry. This will allow Nessus to connect to the VM's registry and properly scan for vulnerabilities such as insecure connections or deprecated cipher suites. I'm following these steps from Nessus and what they recommend to actually do credentialed scans. There might be a better way to do this.</b> <br/>
</p>

![Services_MSC](https://user-images.githubusercontent.com/108043108/177888931-9dbd1224-5155-4129-ba09-4f495976a0e2.JPG)

![Enabling_Remote_Registry](https://user-images.githubusercontent.com/108043108/177889042-0a885e18-bf64-4390-8f43-454bdaf79004.gif)

<br />
<br />
<p align="center">
<b>From there I go to User Account Controls and disable it. I have to do this because this VM is not on a domain so I kind of have to do hacker stuff to get it to work properly. I would never do this in an actual organization or production environment.</b> <br/>
</p>

![user_account_Settings](https://user-images.githubusercontent.com/108043108/177889466-907890fc-e67e-490b-8a17-b335263d0359.JPG)

![User_Account_settings_configuration](https://user-images.githubusercontent.com/108043108/177889473-ba988135-ce62-4717-bf04-1e426ec8c4b6.gif)

<br />
<br />
<p align="center">
<b>Then I'm going to open the registry and add a key that is suppose to allow Nessus to connect in by further disabling user account controls.</b> <br/>
</p>

![Registry_editor](https://user-images.githubusercontent.com/108043108/177889663-24088363-2291-4af0-8ea9-6f6486fc82ad.JPG)

<br />
<br />
<p align="center">
<b>Now I navigate the Registry to the file that Nessus instructs us to (highlighted Yellow in the search bar) and I have to add a DWORD value and name it LocalAccountTokenFilterPolicy and give it a value of 1. </b> <br/>
</p>

![Creating_a_new_DWORD](https://user-images.githubusercontent.com/108043108/177889894-f94747fa-fa05-401f-82d4-1c9ec9faa57f.JPG)

![DWORD_name](https://user-images.githubusercontent.com/108043108/177889904-aa294428-0864-4018-8cb5-b61da5e65478.JPG)

![Edit_DWORD](https://user-images.githubusercontent.com/108043108/177889915-70e9814c-5167-460c-be85-10abf056fd8f.JPG)

<br />
<br />
<p align="center">
<b>After doing that I have to restart the VM so the changes can take effect.</b> <br/>
</p>

![Restart_The_VM](https://user-images.githubusercontent.com/108043108/177889955-2511a00a-9b59-4b4d-a9be-c2abda9869a6.JPG)

<br />
<br />
<p align="center">
<b>With the registry configured, it is now time to go back into Nessus and configure the scan I created. I have to add the Credentials to the scan so it can work properly. The credentials I'm talking about is the username and password of the VM. This will allow Nessus to use those credentials in places where it is required in the VM registry.</b> <br/>
</p>

![Configure_Nessus](https://user-images.githubusercontent.com/108043108/177890138-e6420231-4ce8-4a2d-99fb-e1e992da6ebb.JPG)

![Adding_Credentials](https://user-images.githubusercontent.com/108043108/177890151-27496a20-72b8-4763-8c82-368a06a15d3f.gif)

<br />
<br />
<p align="center">
<b>After the scan is properly configured with the right credentials, I run it again.</b> <br/>
</p>

![Run_The_Scan_Again](https://user-images.githubusercontent.com/108043108/177890377-b412d84a-d8e2-40da-9995-dddbd3c4d388.JPG)

<br />
<br />
<p align="center">
<b>This new scan has given us a lot more vulnerabilities than the first one because it is able to scan deeper into the VM due to having credentials. The top picture is the new credentialed scan and the bottom picture is from the first non-credentialed scan. Most of the vulnerabilities found is probably because the version of Windows 10 this VM is running is not up to date.</b> <br/>
</p>

![new_scan_properly_credentialed](https://user-images.githubusercontent.com/108043108/177890582-7f4d0eec-3b5f-4a5f-b708-47b3ccfb5d83.JPG)

![Old_scan_not_credentialed](https://user-images.githubusercontent.com/108043108/177890589-e4e882ab-6733-4930-ad4c-1115a2c620b3.JPG)

<br />
<br />
<p align="center">
<b>I want to see how powerful this Nessus Scanner is so I'm going to download a very old version of Firefox which probably has many vulnerabilities and see if Nessus can discover them (I'm sure it will.)</b><br/>
</p>

![downloading_an_old_version_of_firefox](https://user-images.githubusercontent.com/108043108/177890787-5cd80be3-99a1-40a4-bddc-feb06ea9cda7.JPG)

<br />
<br />
<p align="center">
<b>After a deprecated version of Firefox is downloaded, I run another scan. We can see many new alerts and vulnerabilities just from Firefox! 68 Critical!</b> <br/>
</p>

![Old_Firefox_Scan](https://user-images.githubusercontent.com/108043108/177890872-ed890db9-a15d-4de9-b3b3-6723dd161f22.JPG)

<br />
<br />
<p align="center">
<b>A comparison between scans to show the progression of alerts and vulnerabilities.</b>  <br/>
</p>

![Vulnerability_Comparison](https://user-images.githubusercontent.com/108043108/177890918-c2fc7078-34b9-4120-a430-f096169ae177.jpg)

<br />
<br />
<p align="center">
<b>Showing what some of the alerts and vulnerabilites look like. We can see most of the Critical alerts are just from Firefox. A few ways we can remediate some of the vulnerabilities is by either Updated Firefox, which will probably remediate a lot of them, or we can simply delete Firefox.</b>  <br/>
</p>

![Showing_Vulnerabilities](https://user-images.githubusercontent.com/108043108/177891162-cf86e335-0539-4f9f-abb2-7150b482e689.gif)

<br />
<br />
<p align="center">
<b>To start the process of remediating vulnerabilities, I elect to just delete Firefox. That will instantly fix a lot of these issues.</b>  <br/>
</p>

![Fixing_Vulnerabilities_Uninstall_Firefox](https://user-images.githubusercontent.com/108043108/177891363-17bdc0ea-c872-434f-95a6-4bf6e4694ddf.JPG)

<br />
<br />
<p align="center">
<b>To remediate the Windows vulnerabilities, I choose to update Windows. This version is old so it takes a few restarts to get it up to date.</b>  <br/>
</p>

![Remediating_Vulnerabilities_Updating_WIndows_1](https://user-images.githubusercontent.com/108043108/177891464-75d2b603-cadf-4923-bc1f-61409b11169d.gif)

![Remediating_Vulnerabilities_Updating_Windows](https://user-images.githubusercontent.com/108043108/177891436-a7b26e21-8376-4650-aaee-aaf4bc2e451e.JPG)

<br />
<br />
<p align="center">
<b>After a few restarts, Windows is finally up to date. I run one more Nessus scan to find if the steps I took to remediate some of the alerts worked.</b>  <br/>
</p>

![VM_Up_To_date](https://user-images.githubusercontent.com/108043108/177891501-767d6764-8e4a-4bd0-85cc-6b70e48c62aa.JPG)

<br />
<br />
<p align="center">
<b>Here is a final comparison between the four scans I took while doing this lab. The last picture is the after remediation scan. There we can see a lot of the vulnerabilities that were being alerted are gone! Still a 1 critical but I'll remediate that another time!</b>  <br/>
</p>

![After_Vulnerability_Remediation](https://user-images.githubusercontent.com/108043108/177891719-3066c9bb-38dd-4b10-b8bb-6f9dd8a45a09.JPG)

<br />
<br />


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
