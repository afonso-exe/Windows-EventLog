<h1>Failed RDP to IP Geolocation Information</h1>

### Project Overview

<h2>Description</h2>
<br />
In this demonstration, a live virtual machine acts as a honeypot to attract RDP Brute Force attacks from across the globe. The custom PowerShell script extracts failed login attempts, queries an IP Geolocation API for the attackers' location data, and visualizes this on a map within Azure Sentinel.
<br />

<h2>Key Technologies</h2>

- <b>PowerShell:</b> Used for extracting failed RDP logon attempts and interacting with the IP Geolocation API.
- <b>Azure Sentinel:</b> Microsoft's SIEM system for real-time analytics and mapping of cyber-attacks.
- <b>Virtual Machine:</b> Set up as a honeypot to monitor and analyze RDP Brute Force attacks.

<h2>Utilities Used</h2>

- <b>IP Geolocation API (ipgeolocation.io):</b> Provides geographic information based on IP addresses of attackers.

<h2>Project Steps Overview</h2>

- <b>Creating the Virtual Machine, and in the network security group, setting an inbound rule to allow all in the firewall.
<p align="center">
<b>Virtual Machine:</b> 
<br />
<img src="https://i.imgur.com/whhlrlv.png" height="85%" width="85%" alt="Virtual Machine"/>
</p>
<p align="center">
<b>Rule to allow all:</b> 
<br />
<img src="https://i.imgur.com/ebM12Ja.png" height="85%" width="85%" alt="Rule to allow all"/>
</p>

- <b>Next we create a log analytics workspace to collect logs from our VM, to do that we first create the workspace, followed by allowing those logs to be collected in Microsoft Defender, and lastly we connect our Log analytics Workspace to our VM
<p align="center">
<b>Logs Workspace:</b>
<br />
<img src="https://i.imgur.com/5Axem0V.png" height="85%" width="85%" alt="Logs Workspace"/>
</p>
<p align="center">
<b>Activate Defender Plans:</b> 
<br />
<img src="https://i.imgur.com/m3VVZHT.png" height="85%" width="85%" alt="Activate Defender Plans"/>
</p>
<p align="center">
<b>Collect All events:</b> 
<br />
<img src="https://i.imgur.com/D9cHe3U.png" height="85%" width="85%" alt="Collect All events"/>
</p>
<p align="center">
<b>Connect logs Workspace to VM:</b> 
<br />
<img src="https://i.imgur.com/15zZTvC.png" height="85%" width="85%" alt="Connect logs Workspace to VM"/>
</p>

- <b>Next we can then proceed to create our Azure Sentinel, that will serve as our SIEM (Security Information And Event Management), and add it to our Logs workspace
<p align="center">
<b>Connect Azure Sentinel to Logs Workspace:</b> 
<br />
<img src="https://i.imgur.com/JQ9CpnT.png" height="85%" width="85%" alt="Connect logs Workspace to VM"/>
</p>

- <b>We are now ready to connect to our VM through Remote Desktop, using Its Public IP Address.
<p align="center">
<b>VM Overview:</b> 
<br />
<img src="https://i.imgur.com/ta73r8e.png" height="85%" width="85%" alt="Connect logs Workspace to VM"/>
</p>

- <b>After using remote desktop to enter the VM, we now have to turn off the firewall so people can discover it on the internet faster, to do that we search for "wf.msc" on the windows search bar. After that we transition to our personal computer and Start to continuously ping our VM, using "ping [VM's ip address] -t", and what we will notice is after we turn off the firewall the ping will pass through, making it easier for our machine to be discovered, which is what we want for this project.
<p align="center">
<b>Starting the ping and requests timing out:</b> 
<br />
<img src="https://i.imgur.com/6Z9PmxX.png" height="85%" width="85%" alt="Connect logs Workspace to VM"/>
</p>
<p align="center">
<b>Turning off the Firewalls:</b> 
<br />
<img src="https://i.imgur.com/CiWKnIu.jpeg" height="85%" width="85%" alt="Connect logs Workspace to VM"/>
</p>
<p align="center">
<b>Pings are finally successfull:</b> 
<br />
<img src="https://i.imgur.com/5XwxLtL.png" height="85%" width="85%" alt="Connect logs Workspace to VM"/>
</p>

- <b>For this Next part, we need to go to the windows event viewer. In Here we are able to see failed RDP logon attempts through EventID, and in those, we can see the IP of the attacker, timestamp, port he tried to use, etc..
- <b>Now, with our PowerShell Script, we can get the information on the attacker, along with his IP, which we use to get his geolocation, using a third party API. After we get all this information we send it to a file, that we will use to create our custom table in our log analytics workspace, that will then serve to create our map of the world in Sentinel.
<p align="center">
<b>Windows Event Viewer:</b> 
<br />
<img src="https://i.imgur.com/UdJnKbj.png" height="85%" width="85%" alt="Connect logs Workspace to VM"/>
</p>

- <b>Next, we create our custom table in our Logs Workspace, and in this table, we will feed it the information from the file that we get from our script.
<p align="center">
<b>Creating Custom Table:</b> 
<br />
<img src="https://i.imgur.com/YyILc8T.png" height="85%" width="85%" alt="Connect logs Workspace to VM"/>
</p>

- <b>After Some time the data becomes available, and we can query our custom table for information.
<p align="center">
<b>Data:</b> 
<br />
<img src="https://i.imgur.com/ejmlIwg.png" height="85%" width="85%" alt="Connect logs Workspace to VM"/>
</p>

- <b>All that is left to do is create our Workbook in Sentinel, add a map and fill it with our data, making it how we want it using a query.
<p align="center">
<b>Creating Workbook:</b> 
<br />
<img src="https://i.imgur.com/2lknpjC.png" height="85%" width="85%" alt="Connect logs Workspace to VM"/>
</p>
<p align="center">
<b>Creating our Query:</b> 
<br />
<img src="https://i.imgur.com/MQpB17m.png" height="85%" width="85%" alt="Connect logs Workspace to VM"/>
</p>


<h2>Insights into Attack Patterns</h2>

As the honeypot VM exposes vulnerabilities to the internet, it swiftly becomes a target for attackers worldwide. The collected data unveils patterns, frequency, and geographical distribution of cyber-attacks, highlighting the global nature of cyber threats.

<h2>Visualization of Attack Data</h2>

<p align="center">
<b>Initial Findings:</b> Snapshot of attack origins with geolocation data.
<br />
<img src="https://i.imgur.com/tMbJaIQ.png" height="85%" width="85%" alt="Initial attack data visualization"/>
</p>

<p align="center">
<b>First Map Analysis:</b> Comprehensive world map showing the first distribution of attacks.
<br />
<img src="https://i.imgur.com/qOOlEhf.png" height="85%" width="85%" alt="First Map Analysis"/>
</p>

<p align="center">
<b>24-Hour Analysis:</b> Comprehensive world map showing the distribution of attacks after 24 hours, enriched with custom geodata logs.
<br />
<img src="https://i.imgur.com/aV03yg2.png" height="85%" width="85%" alt="24-hour attack data analysis"/>
</p>

This project underscores the importance of robust cybersecurity measures and demonstrates the utility of honeypots in understanding and mitigating cyber threats.
