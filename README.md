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

## Monitor for False Positives

Currently we only setup up the IDS section of Suricata. It is recommended that you check the **Alert** tab for a couple of days to analyze the traffic and attempt to identify false positives. You will have to Select the interface to view the logs. 

<img src="https://github.com/4LifeStrategy/Intrusion-Detection-and-Prevention-System/blob/64900f9c7643b41ab8047244df51dc462c0541f2/Suricata%20Alerts.png" width="500">

Once you detected a false positive, note down the **GID/SID** which would look like **1:2221010**. We will need these SIDs to add them to our list to allow the traffic or else it will be blocked causing the effect service not to function.

## Enable IPS

To enable the prevention system we will need to configure SID Rule lists.

1. Click **Services**
2. Click **Suricata**
3. Click **SID Mgmt** tab
4. Enable **Enable Automatic SID State Management**

**disabled** will completely ignore the rule and will not conduct any matching.
**enabled** will conduct matching and will create alerts.
**drop** will block the matched rule.

1. Right of **disablesid-sample.conf** click the **pencel icon** to edit
2. Clear the contents
3. Add all your fails flags alerts SIDs with a note to know what each SIDs are.

        #Synology Quick Connect
        1:2027757
4. Click **Save**
5. Right of **disablesid-sample.conf** click the **pencel icon** to edit
6. Clear the contents
7. Add all the specific categories list you desire and SIDs you want to block

        # Note: This file is used to specify what rules you wish to be set to have
        # an action of drop rather than alert.

        #specific categories
        emerging-3coresec
        emerging-ciarmy
        emerging-compromised
        emerging-current_events
        emerging-drop
        emerging-dshield
        emerging-dns
        emerging-botcc
        emerging-malware
        emerging-tor
        emerging-trojan
        emerging-scan
        feodotracker
        sslblacklist_tls_cert

        #flooded with SURICATA QUIC failed decrypt
        1:2231000

8. Click **Save**
9. Under **Interface SID Management List Assignments** assigned the proper list for each interface.
10. For **SID State Order** select **Disable, Enable**
11. For **Enable SID List** select **enablesid-sample.conf**
12. For **Disable SID List** select **disablesid-sample.conf**
13. For **Drop SID List** select **dropsid-sample.conf**<br /><img src="https://github.com/4LifeStrategy/Intrusion-Detection-and-Prevention-System/blob/e6bf96c2a29723dfd1853c700e06778f13c23105/Suricata%20SID%20Mgmt.png" width="500">
14. Under **Rebuild** select all the interfaces**
15. Click **Save**
