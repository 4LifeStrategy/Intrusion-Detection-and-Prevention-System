<div align="center" style="white-space: nowrap;">
  <img src="https://github.com/4LifeStrategy/4LifeStrategy/blob/88ffe3009f1399de4502d4d5641c8f7a0fd56852/4LifeStrategy%20Logo%20Center.png" alt="4LifeStrategy Logo" width="100" style="display:inline-block; vertical-align:middle; margin-right:10px;">
  <h1 style="margin:0; vertical-align:middle;">Intrusion Detection & Prevention System (Suricata)</h1>
</div>

## Description

**IDS/IPS** is intrusion detection & prevention system to detect malicious activities block the data traffic that passes through the pfSense firewall using Suricata.

## Project Scope

**Objective**: Implement IDS and IPS functionalities in a pfSense firewall using Suricata. Configured and managed enable, disable, and drop signature ID lists to monitor and block malicious network activity.

## Installation

We will need to login to our pfSense intense and make sure that you system is update to date. Then perform the following to install and Suricata.

1. Click **Systems**
2. Click **Package Manager**
3. Click **Available Packages**
4. Search **Suricata**
5. Click **Install**
6. Click **Confirm**

## Initial Setup

Once pfSense complete Suricata installation we can enable the package and perform initial configurations.

1. Click **Services**
2. Click **Suricata**
3. Click **Global Settings** tab
4. Enable **ETOpen is a free open source set of Suricata rules whose coverage is more limited than ETPro.**
5. Enable **Install Feodo Tracker Botnet C2 IP rules**<br /><img src="https://github.com/4LifeStrategy/Intrusion-Detection-and-Prevention-System/blob/651fbd34f934b7fa69a1584cfeddb097ab4c086a/Suricata%20Global%20Settings.png" width="500">
6. Enable **Install ABUSE.ch SSL Blacklist rules**
7. For **Update Interval** select **1 Day**
8. For **Update Start Time** set to **03:00**
9. Enable **Live Rule Swap on Update**<br /><img src="https://github.com/4LifeStrategy/Intrusion-Detection-and-Prevention-System/blob/f574fa2e3d9f3cb10df00f079e3503b17120e1b3/Suricata%20Global%20Setting_2.png" width="500">
10. Click **Save**
11. Click **Update** tab
12. Click **Update**
13. Click **Interfaces** tab
14. Click **Add**
15. Enable **Checking this box enables Suricata inspection on the interface.**
16. For **Description** put **LAN**
17. Click **Save**
18. Click on the **Pencel Icon** next to the **LAN Interface**
19. Click **LAN Categories** tab
20. Click **Select All**
21. Click **Save**
22. Click **Interfaces** tab
23. Click **Copy** Interface
24. For **Interface** select **OPT2 (igc3)** 
25. Click **Save**
26. Click **Copy** Interface
27. For **Interface** select **OPT1 (igc2)**
28. Click **Save**
29. Click the **Play Icon** on each interface to start Suricata

## Test & Monitor for Fails Positives

Currently we only setup up the IDS section of Suricata. It is recommended that you check the **Alert** tab for a couple of days to analyze the traffic and attempt to identify fails positives. You will have to Select the interface to view the logs. 

<img src="https://github.com/4LifeStrategy/Intrusion-Detection-and-Prevention-System/blob/f574fa2e3d9f3cb10df00f079e3503b17120e1b3/Suricata%20Global%20Setting_2.png" width="500">

Once you detected a fails positive, note down the **GID/SID** which would look like **1:2221010**. We will need these SIDs to add them to our list to allow the traffic or else it will be blocked causing the effect service not to function.

## Enable IPS

