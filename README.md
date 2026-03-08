# CCNA-Enterprise-Lab

Multi-Floor Enterprise Network Design

CCNA Lab: High Availability & Layer 2 Redundancy

📌 Project Overview

This project simulates a three-story corporate office network. The primary goal was to design a resilient, loop-free architecture that ensures departmental segmentation and seamless failover for end-users.

🛠 Technologies & Protocols Used

- Switching: VLANs (Sales, HR, IT, Server, Guest), VTP (Server/Client), Hardcoded switchports.
- Redundancy: Rapid Per-VLAN Spanning Tree (Rapid-PVST), EtherChannel (LACP).
- Gateway High Availability: HSRP (Hot Standby Router Protocol).
-  Addressing: IPv4 VLSM.

🏗 Network Topology

Access Layer: 3x Cisco 2960 Switches (Floor 1, 2, and 3).

Distribution Layer: 2x Cisco 3650 Multilayer Switches.

Logical Segregation using VLSM:

- VLAN 10: HR (172.16.0.128/27)
- VLAN 20: SALES (172.16.0.0/25)
- VLAN 30: IT (172.16.0.176/28)
- VLAN 40: SERVER (172.16.0.192/29)
- VLAN 50: GUESTS (172.16.0.160/28)

🚀 Implementation Highlights

1. Load Balanced Redundancy (STP & EtherChannel)

To prevent network loops while maximizing bandwidth, I configured LACP EtherChannels between distribution switches.
I enabled Rapid-PVST and manually tuned its priority so that DSW1 is the Root Bridge for VLANs 10,20 and 30 and DSW2 is the Root for VLANs 40 and 50, ensuring all links are utilized.

2. First Hop Redundancy (HSRP)

I implemented HSRP to provide a virtual gateway.

- Active/Standby: If the primary distribution switch fails, the standby takes over in seconds without the end-user losing connectivity.
- Preemption: Configured to ensure the primary switch resumes its role once it recovers.

3. Security

- Enable Secret Password: Enabled to prevent unauthorized access to the privileged EXEC mode.
- Banner MOTD: Configured for legal compliance.

🏁 Verification Commands

The following commands were used to validate the stability of the environment:

- show ip interface brief - Verify interface status.
- show standby brief - Validate HSRP state (Active/Standby).
- show etherchannel summary - Confirm LACP bundling is operational.
- show spanning-tree vlan [ID] - Verify Root Bridge placement.
