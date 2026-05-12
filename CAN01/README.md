# 🏢 Cisco Packet Tracer — Campus Network Lab

> A comprehensive CCNA-level network simulation built in Cisco Packet Tracer, covering 22 core networking topics in a realistic three-tier campus architecture.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Device Inventory](#device-inventory)
- [IP Addressing Plan](#ip-addressing-plan)
- [Topics Covered](#topics-covered)
- [Build Order](#build-order)
- [Verification Commands](#verification-commands)
- [Skills Demonstrated](#skills-demonstrated)

---

## Overview

This lab simulates a multi-site enterprise campus network using a **three-tier architecture** (Core → Distribution → Access), a WAN/ISP edge, a dedicated server farm, and a remote branch site. Every feature is integrated into a cohesive, end-to-end design — nothing is isolated or artificially bolted on.

**Base Network:** `192.168.0.0/16` (VLSM-carved)  
**Simulator:** Cisco Packet Tracer  
**Difficulty:** CCNA / Entry-level Network Administrator  

---

## Device Inventory

| Role | Model | Hostname |
|------|-------|----------|
| Core Router / NAT Edge | Cisco 2911 | R1-EDGE |
| ISP Simulation | Cisco 2911 | R2-ISP |
| Remote Branch Router | Cisco 2911 | R3-BRANCH |
| Core Layer Switch (L3) | Cisco 3650 | SW-CORE |
| Distribution Switch A (L3) | Cisco 3650 | SW-DIST-A |
| Distribution Switch B (L3) | Cisco 3650 | SW-DIST-B |
| Access Switch 1 | Cisco 2960 | SW-ACC-1 |
| Access Switch 2 | Cisco 2960 | SW-ACC-2 |
| Access Switch 3 | Cisco 2960 | SW-ACC-3 |
| Server Farm Switch | Cisco 2960 | SW-SRV |
| DNS / DHCP / Syslog Server | Server-PT | SRV-DNS-DHCP |
| FTP / TFTP Server | Server-PT | SRV-FTP |
| NTP Server | Server-PT | SRV-NTP |
| End Hosts | PC-PT | PC-1 through PC-9 |

---

## IP Addressing Plan

### VLAN Subnets (VLSM)

| VLAN | Name | Subnet | Mask | Usable Range | Hosts |
|------|------|--------|------|--------------|-------|
| 10 | SALES | 192.168.0.0 | /26 | .1 – .62 | 60 |
| 20 | IT | 192.168.0.64 | /27 | .65 – .94 | 28 |
| 30 | GUEST | 192.168.0.96 | /27 | .97 – .126 | 28 |
| 40 | MGMT | 192.168.0.128 | /28 | .129 – .142 | 14 |
| 50 | SERVERS | 192.168.0.144 | /28 | .144 – .158 | 14 |
| 99 | NATIVE | 192.168.99.0 | /30 | — | — |

### Routed Point-to-Point Links

| Link | Subnet | R1-EDGE | Peer |
|------|--------|---------|------|
| R1-EDGE ↔ R2-ISP | 203.0.113.0/30 | .1 | .2 |
| R1-EDGE ↔ SW-CORE | 10.0.0.0/30 | .1 | .2 |
| R1-EDGE ↔ R3-BRANCH | 10.0.1.0/30 | .1 | .2 |
| SW-CORE ↔ SW-DST-1 | 10.0.2.0/30 | .1 | .2 |
| SW-CORE ↔ SW-DST-2 | 10.0.3.0/30 | .1 | .2 |
| R2-ISP Loopback | 8.8.8.8/32 | — | — |
| R3-BRANCH LAN | 172.16.1.0/24 | — | .1 |

---

## Topics Covered

| # | Topic | Implementation |
|---|-------|----------------|
| 1 | **Basic Device Security** | Enable secret, VTY passwords, banners, port shutdown |
| 2 | **LAN Switching** | 802.1Q trunks, access ports, native VLAN 99 |
| 3 | **IPv4 / VLSM Subnetting** | Right-sized subnets for each segment |
| 4 | **Static Routing** | Default route on R1-EDGE, branch static routes |
| 5 | **Dynamic Routing (OSPF)** | OSPF Area 0 across core/distribution layer |
| 6 | **VLANs** | VLANs 10, 20, 30, 40, 50, 99, 999 |
| 7 | **DTP** | Disabled on all links, trunks set manually |
| 8 | **VTP** | Server/Client/Transparent roles demonstrated |
| 9 | **STP** | PortFast, BPDUGuard, BPDUFilter, Root Guard, Loop Guard |
| 10 | **EtherChannel** | LACP Po1 between distribution switches |
| 11 | **FHRP (HSRP)** | Load-balanced HSRP active/standby per VLAN |
| 12 | **ACLs** | Extended, named, and standard ACLs applied |
| 13 | **CDP & LLDP** | Neighbor discovery, disabled on edge ports |
| 14 | **NTP** | Hierarchical time sync |
| 15 | **DNS** | A records for all servers, domain lookup enabled |
| 16 | **DHCP** | Server pools + relay agents on SVIs |
| 17 | **Syslog** | Centralized logging to SRV-DNS-DHCP |
| 18 | **SSH** | RSA keys, local auth, VTY lockdown |
| 19 | **FTP & TFTP** | Config backup, restore, file transfer |
| 20 | **NAT (PAT)** | Overload on R1-EDGE for all inside networks |
| 21 | **Port Security** | Sticky MAC, max MACs, violation modes |
| 22 | **DHCP Snooping** | Trusted uplinks, rogue server prevention |
| 23 | **Dynamic ARP Inspection** | ARP spoofing prevention on access VLANs |

---

## Build Order

| Step | Phase |
|------|-------|
| 1 | Physical topology and cabling |
| 2 | Basic device security on all devices |
| 3 | VTP domain and VLAN database |
| 4 | Trunk and access port config + DTP lockdown |
| 5 | STP tuning (root bridge, guards, PortFast) |
| 6 | EtherChannel (LACP Po1) |
| 7 | IP addressing — SVIs, routed links, loopbacks |
| 8 | FHRP — HSRP on distribution SVIs |
| 9 | OSPF + static routing + default route |
| 10 | NAT (PAT) on R1-EDGE |
| 11 | DHCP server pools and relay agents |
| 12 | DNS, NTP, Syslog server config |
| 13 | SSH verification and ACL lockdown |
| 14 | FTP/TFTP backup and restore |
| 15 | Port security, DHCP snooping, DAI |
| 16 | CDP/LLDP verification |
| 17 | End-to-end testing |

---

## Verification Commands

```cisco
! STP
show spanning-tree vlan 10

! EtherChannel
show etherchannel summary

! HSRP
show standby brief

! OSPF
show ip ospf neighbor
show ip route ospf

! NAT
show ip nat translations
show ip nat statistics

! DHCP
show ip dhcp binding
show ip dhcp pool

! DHCP Snooping
show ip dhcp snooping binding

! Dynamic ARP Inspection
show ip arp inspection statistics

! Port Security
show port-security interface Fa0/1

! VTP
show vtp status

! NTP
show ntp status
show ntp associations

! CDP / LLDP
show cdp neighbors detail
show lldp neighbors

! SSH
show ssh
show users

! ACL
show access-lists
show ip interface Fa0/0
```

---

## Skills Demonstrated

- **Network Design** — Three-tier campus architecture with redundancy at every layer
- **Subnetting / VLSM** — Efficient address allocation with right-sized masks
- **Layer 2 Security** — DHCP snooping, DAI, port security, STP hardening
- **Redundancy** — HSRP load balancing, EtherChannel, STP failover
- **Routing** — OSPF multi-area awareness, static routes, redistribution
- **Network Services** — DNS, DHCP, NTP, Syslog, FTP/TFTP in an integrated environment
- **Access Control** — Named/extended/standard ACLs, SSH-only VTY, MGMT VLAN isolation
- **NAT** — PAT overload for full inside network translation

---

> **Lab Status:** ✅ Completed  
> **Tools Used:** Cisco Packet Tracer  
> **Certification Target:** CCNA (200-301)
