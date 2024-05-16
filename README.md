<h1>Failed RDP to IP Geolocation Information</h1>

### Project Overview

<h2>Description</h2>
<b>This repository houses a PowerShell script designed to parse failed RDP attack logs from Windows Event Viewer and enrich these logs with geographic information of the Threat actors by leveraging a third-party API. This script plays a crucial role in visualizing the origin of cyber-attacks on a global scale, utilizing Azure Sentinel for real-time analysis and mapping.</b>
<br />
<br />
In this demonstration, a live virtual machine acts as a honeypot to attract RDP Brute Force attacks from across the globe. The custom PowerShell script extracts failed login attempts, queries an IP Geolocation API for the attackers' location data, and visualizes this on a map within Azure Sentinel.
<br />
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
<b>Connect logs Workspace to VM:</b> 
<br />
<img src="https://i.imgur.com/15zZTvC.png" height="85%" width="85%" alt="Connect logs Workspace to VM"/>
</p>

- <b>IP Geolocation API (ipgeolocation.io):</b> Provides geographic information based on IP addresses of attackers.
- <b>IP Geolocation API (ipgeolocation.io):</b> Provides geographic information based on IP addresses of attackers.
- <b>IP Geolocation API (ipgeolocation.io):</b> Provides geographic information based on IP addresses of attackers.
- <b>IP Geolocation API (ipgeolocation.io):</b> Provides geographic information based on IP addresses of attackers.
- <b>IP Geolocation API (ipgeolocation.io):</b> Provides geographic information based on IP addresses of attackers.
- <b>IP Geolocation API (ipgeolocation.io):</b> Provides geographic information based on IP addresses of attackers.
- <b>IP Geolocation API (ipgeolocation.io):</b> Provides geographic information based on IP addresses of attackers.

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
