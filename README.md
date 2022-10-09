<h1>Active Directory Home Lab</h1>

<h2>Description</h2>
This project is an attempt at creating a home lab running Active Directory, where there is a Domain Controller (VirtualBox machine) running Windows Server 2019. The domain controller has 2 network connections, one internal and one to the internet. I have added 1000 users to the network using a windows powershell script and the aim of the project is to get a second virtual machine running windows 10 to connect to the internet through the internal network of the domain controller. 
<br />


<h2>Software used</h2>

- <b>Oracle VirtualBox</b> 
- <b>Windows Powershell</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> 
- <b>Windows Server 2019</b> 

<h2>Process Walkthrough:</h2>

<p align="center">
After installing VirtualBox and installing Windows 2019 Server ISO on the first virtual machine, I enabled 2 network adapters for both the internet and internal network: <br/>
<img src="https://imgur.com/3P4mpBK.png" height="45%" width="45%"/>
<img src="https://imgur.com/T3300f9.png" height="45%" width="45%"
/>
<br />
<br />
For the internal network I configured the IPv4 and assigned DNS to be the Domain Controller so it refers back to itself : <br/>
<img src="https://imgur.com/sFMRVjY.png" height="30%" width="30%"
/>
<br />
<br />
Installing Active Directory Domain Services on the domain controller and setting it to mydomain.com and deploying it:  <br/>
<img src="https://imgur.com/Oaj1Emn.png" height="45%" width="45%"
<br />
<br />
Creating an Organisational Unit:  <br/>
<img src="https://imgur.com/CGNxOKw.png" height="50%" width="50%"
<br />
<br />
Adding new registry policy and changing the binary value to 1:
<img src=".png" height="60%" width="60%"
<br />
<br />
After this is done I used command prompt to view the IP address of the VM and pinged this on my main device : <br/>
<img src=".png" height="100%" width="100%"
<br />
<br />
Now the VM can be scanned on Nessus Essentials so I first did a basic scan:  <br/>
<img src=".png" height="100%" width="100%" 
<br />
<br />
There was only 1 medium detected vulnerability in the initial scan. As it was clear that there are more vulnerabilities it was time to do a credentialed scan - using the password of the VM host:  <br/>
<img src=".png" height="60%" width="60%" 
<br />
<br />
After enabling credentials, results of the second scan:  <br/>
<img src=".png" height="80%" width="80%" 
<br />
<br />
I then installed an older version of firefox to observe how this would reflect on the vulnerability of the VM host:  <br/>
<img src=".png" height="40%" width="40%" 
<br />
<br />
Credentialed Vulnerability Scan with old firefox installed:  <br/>
<img src=".png" height="60%" width="60%" 
<br />
<br />
Using the Nessus Software, the top 10 vulnerabilities found were displayed.
<img src=".png" height="50%" width="50%" 
<br />
<br />
I then followed the software's recommended remediation steps against these vulnerabilities:  <br/>
<img src=".png" height="60%" width="60%"
<br />
<br />
Instead of updating firefox I decided to just uninstall it and only update Windows, as I didn't want to strain my laptop with multiple updates: <br/>
<img src=".png" height="60%" width="60%"
<br />
<br />
After uninstalling firefox and updating windows the final scan: <br/>
<img src=".png" height="60%" width="60%"
<br />
<br />
Comparison graphs of each stage: <br/>
Initial <br/>
<img src=".png" height="30%" width="30%"
<br />
<br />
Credentialled <br/>
<img src=".png" height="30%" width="30%"
<br />
<br />
Depricated firefox <br/>
<img src=".png" height="30%" width="30%"
<br />
<br />
Post remediation <br/>
<img src=".png" height="30%" width="30%"
</p>
<h2>Final Thoughts</h2>
.
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
