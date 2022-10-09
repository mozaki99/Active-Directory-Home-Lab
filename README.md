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
Creating an Organisational Unit to add admin users:  <br/>
<img src="https://imgur.com/CGNxOKw.png" height="50%" width="50%"
<br />
<br />
Installing and deploying NAT on the domain controller: <br/>
<img src="https://imgur.com/49ARsKU.png" height="50%" width="50%"
<br />
<br />
After this is done, I selected public interface that was for the client: <br/>
<img src="https://imgur.com/qydiW3R.png" height="50%" width="50%"
<br />
<br />
Installing and deploying DHCP to allow the client computer to automatically be given an IP:  <br/>
<img src="https://imgur.com/5mhluDH.png" height="50%" width="50%" 
<br />
<br />
Setting the IP range for the DHCP so clients get assigned an IP within this range:  <br/>
<img src="https://imgur.com/zGcwHTE.png" height="50%" width="50%" 
<br />
<br />
Downloading a plain text file of 1000 random first and surnames:  <br/>
<img src="https://imgur.com/E1YShJX.png" height="70%" width="70%" 
<br />
<br />
Using a Powershell script to generate the users into the network, the script essentially takes content from the names text file and "re-orders" them in a username format and I have set all user passwords to be the same:  <br/>
<img src="https://imgur.com/OkfVn5K.png" height="80%" width="80%" 
<br />
<br />
Setting execution policy for Powershell to enable it to run the script:  <br/>
<img src="https://imgur.com/E8ujCrE.png" height="80%" width="80%" 
<br />
<br />
Executing the Powershell script, all users should now be part of the network:
<img src="https://imgur.com/kKqFSBx.png" height="80%" width="80%" 
<br />
<br />
The users now can be seen in the Organisational Unit:  <br/>
<img src="https://imgur.com/klbaa6y.png" height="50%" width="50%"
<br />
<br />
Setting up the client running windows 10 on a second VM, I've set the network to be internal - so it will use the Domain Controller in order to access the internet: <br/>
<img src="https://imgur.com/5dcYJKq.png" height="60%" width="60%"
<br />
<br />
Once the client VM has finished installation, we can see whether it can connect to the internet via the Domain Controller: <br/>
<img src="https://imgur.com/707vh3n.png" height="60%" width="60%"
<br />
<br />
Changing the client name and joining it to the domain, so that it can be used to log in on the main computer as a user: <br/>
<img src="https://imgur.com/Bhd6LGa.png" height="30%" width="30%"
<br />
<br />
Now the client computer is visible on the Active Directory as a computer, and it can log in to the domain as well as access the internet! : <br/>
<br/>
<img src="https://imgur.com/7i2PpeD.png" height="50%" width="50%"
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
