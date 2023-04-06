# SIEMproject
Using Azure Sentinel to create a live cyber attack map

<img src="https://i.imgur.com/yqLiKUC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
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
- <b>Part 1- Creating Honeypot VM and RDP VM.<br />
- <b>Part 2- Creating the custom log in the Log Analytics Workspace.<br />
- <b>Part 3- Creating the failed rdp map in Sentinel.<br />
 
 
<h2>Part 1- Creating Honeypot VM and RDP VM:</h2>

<p align="center">
Created a Honeypot VM exposed to Internet. Another VM was also created to RDP into this Honeypot.<br />
<img src="https://i.imgur.com/3vIUiH3.png" height="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/6orEoJz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
An inbound rule was created to make the Honeypot VM open to all traffic from the internet.
<img src="https://i.imgur.com/LGJeTS6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/Yymvr97.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
Secp-vm1 was created in its own resource group with virtual network.This VM will be used to create a few failed RDP attempt logs.<br />
<img src="https://i.imgur.com/LDjA1r8.png" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/aL2WexQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
Tested Remoting into Honeypot VM which was susccessful.
<img src="https://i.imgur.com/nTEgjAa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/jMRB3I4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Created a Log Analytics workspace which was used to collect the failed rdp log data from the Honeypot.<br />
<img src="https://i.imgur.com/cHN8BeH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
SQL Server services was turned off as its not needed in defender plans. The data collection level was set to All events so that we can gather all logs.
<img src="https://i.imgur.com/AWi9ZrZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/WStalxE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/vgnYutY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/as3Sb4e.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Created Azure Sentinel and connected the Log Analytics Workspace to it. Sentinel is typically used to set up alerts and triggers from logs but failed rdp logo data is going to be visualized as map in this project.<br />
<img src="https://i.imgur.com/VZ1HnAB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/RI8Ipou.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Continued making the Honeypot VM more vulnerable by disabling Windows Defender Firewall. Now we can see ICMP pings are allowed.<br />
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
<br />
A Powershell script which collects the IPs of failed RDP attempts which are sent to a 3rd party API (ipgeolocation.io) to be extracted. The latitude and longitude of these IPs which will be used in the map generation for Sentinel.We can also see my previous failed RDP attempt.
<br />
<img src="https://i.imgur.com/2nkIjZD.png"80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/jZi88Uw.png"80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<h2>Part 2- Creating the custom log in the Log Analytics Workspace:</h2>
<p align="center">
Created a custom log in Log Analytics Workspace. The failed RDP attempts log collected by the powershell script was mapped into the L.A.W.<br/>
<img src="https://i.imgur.com/onrCLyW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/PUi2QX1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/br3xvEe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://i.imgur.com/s9JGrCE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
Checked if L.A.W is receiving logs by checking for updated Windows Security logs which it was. This was done by running ( SecurityEvent | where EventID == 4625 ) query which showed all recent failed rdp logs.<br />
<img src="https://i.imgur.com/a2BSobl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/DKiD3zH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
The 'FAILED_RDP_WITH_GEO1_CL' custom log data was then used to extract and create custom fields to organize data.This is done for efficient searching and accurate data visualization. This allowed us to create customs fields like latitude, longitude, username, country, state etc.
<img src="https://i.imgur.com/oJr7snR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/JeyFDx4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/Al6cWkM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/yXPey3s.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<h2>Part 3- Creating the failed rdp map in Sentinel: </h2>

<p align="center">
First performed some intentional failed RDP attempts to confirm that the logs were being parsed live. Then created the map in Sentinel.<br />
<img src="https://i.imgur.com/NZsy7YJ.png" height="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/dC6OSs6.png" height="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Visualized the logs as a map in Azure Sentinel to see where the attempts were originating from. A new workbook was created to show the map.<br/>
<img src="https://i.imgur.com/USL3nah.png" height="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/OtlYn2o.png" height="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/jiZnvKl.png" height="80%" alt="Disk Sanitization Steps"/>
<br />
 (FAILED_RDP_WITH_GEO1_CL | summarize event_count=count() by sourcehost_CF, latitude_CF, longitude_CF, country_CF, label_CF, destinationhost_CF) query was ran with the visualization option set to map. This generated the information needed to see the where these failed RDP logon attempts are originating from.
<img src="https://i.imgur.com/dRJIwwG.png" height="80%" alt="Disk Sanitization Steps"/>
<br />
There was an increase in attempts from Indonesia as shown on the map which corresponds with the log data generated on the Honeypot vm.<br />

<img src="https://i.imgur.com/A8G28NQ.png" height="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/jKLri07.png" height="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/5elwy4e.png" height="80%" alt="Disk Sanitization Steps"/>
<br />
<br /><br /><br /><br /><br /><br />
<br /><br /><br />








 

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
