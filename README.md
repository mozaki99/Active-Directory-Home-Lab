<h1>Active Directory Home Lab</h1>

<h2>Description </h2>
This project is an attempt at creating a home lab running Active Directory, where there is a Domain Controller (VirtualBox machine) running Windows Server 2019. The domain controller has 2 network connections, one internal and one to the internet. I have added 1000 users to the network using a windows powershell script and the aim of the project is to get a second virtual machine running windows 10 to connect to the internet through the internal network of the domain controller.
I made a small visual diagram of the architecture here:
<img src="https://imgur.com/FK8tpN7.png" height="55%" width="55%"/>
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
I enjoyed this project despite running into quite a few problems when setting this up. One of the problems I ran into was the client computer not being able to connect to the domain. I searched this issue and found that I had installed a version of windows 10 which didn't work for this function. I then deleted the virtual machine and created a new one with a different Windows 10 ISO file, luckily this resolved the issue. I also noticed a few security considerations when setting up this network, for example I set the network to have all users using the same password (including admins!) for the powershell script to execute and this is not good for an actual Active Directory. I also learnt to review a downloaded file before executing it on a device, this is because the text file which I had installed to run the powershell command had 50+ repeated users at the end of the file which someone altered on the original file, this caused many repeated errors on the powershell command which required unique users and no repeats. Although this was harmless in the end, some other files may be corrupted and cause more issues, so it is best to be precautious.
<br/> One other security precaution I noticed is the IP lease duration allocated to the client computers, this duration should be considered if it is in a smaller network such as the computers in an internet cafe, where the clients lease should be reduced to a couple hours instead of days.
<img src="https://imgur.com/o2rQyCj.png" height="30%" width = "30%"

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
