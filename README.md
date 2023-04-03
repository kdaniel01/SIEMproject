# SIEMproject
Using Azure Sentinel to create a live cyber attack map

<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />


<h2>Description</h2>

<b>In this project,I deployed a honeypot and used Azure Log Analytics workspace and Azure Sentinel to visualize the failed RDP attempts into this honeypot.
</b>


<h2>Environments and Technologies Used</h2>

- <b>Azure Virtual Machines (Windows 10 Pro 21h2) <br /> 
- <b> Azure Log Analytics Workspace<br /> 
- <b> Azure Sentinel<br />
- <b>Powershell ISE<br />


<h2>Overview </h2>
- <b>Part 1- Creating Honeypot VM and RDP VM<br />
- <b>Part 2- <br />
- <b>Part 3-<br />
 
 
<h2>Part 1- Creating Honeypot VM and RDP VM:</h2>

<p align="center">
Created a Honeypot VM exposed to Internet. Another VM was created to RDP into this Honeypot.<br />
<img src="https://i.imgur.com/3vIUiH3.png" height="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/6orEoJz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/LGJeTS6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/Yymvr97.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
Secp-vm1 was created in its own resource group with virtual network.This VM will be used to create a few failed RDP attempt logs.<br />
<img src="https://i.imgur.com/LDjA1r8.png" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/aL2WexQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/nTEgjAa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/jMRB3I4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Created a Log Analytics workspace.<br />
<img src="https://i.imgur.com/cHN8BeH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/AWi9ZrZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/WStalxE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/vgnYutY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/as3Sb4e.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Created Azure Sentinel.<br />
<img src="https://i.imgur.com/VZ1HnAB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/RI8Ipou.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Made the Honeypot VM vulnerable by disabling Windows Defender Firewall.Now we can see ICMP pings are allowed.<br />
<img src="https://i.imgur.com/jMRB3I4.png"80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/dhE6hF8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/At1utmy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Performed a failed RDP attempt and verified it was logged in Event Viewer on the Honeypot VM which worked. <br />
<img src="https://i.imgur.com/5y0tdZ0.png"80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/bSlT44e.png"80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
A Powershell script which collects the IPs of failed RDP attempts which are sent to a 3rd party API (ipgeolocation.io) to be extracted. The latitude and longitude of these IPs which will be used in the map generation for Sentinel.We can also see my previous failed RDP attempt.<br />
<img src="https://i.imgur.com/2nkIjZD.png"80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/jZi88Uw.png"80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<h2>Part 2- Creating the custom log in the Log Analytics Workspace:</h2>


Created custom log in Log Analytics Workspace. The failed RDP attempts log collected by the powershell script was mapped.<br/>
<img src="https://i.imgur.com/onrCLyW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /><br /><br /><br /><br /><br /><br /><br />
<br /><br /><br />
Continue from here.....................................







 

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
