# CCNA Packet Tracer Lab — Enterprise Campus Network

A full-integration CCNA lab simulating a real-world enterprise campus network for **TechCorp Ltd**, covering HQ and a remote branch office. Built in Cisco Packet Tracer.

---

**Devices:**
- 2x Cisco 2911 Routers (R1 – HQ Core, R2 – Branch)
- 2x Cisco 3560 Layer-3 Switches (DSW1, DSW2 – Distribution)
- 2x Cisco 2960 Layer-2 Switches (ASW1, ASW2 – Access)
- 1x Server (DNS + DHCP) in VLAN 40
- 4x End-user PCs

---

## 📚 Topics Covered

| # | Topic | Key Concepts |
|---|-------|--------------|
| 1 | VLANs, VTP & DTP | VLAN propagation, trunk negotiation, native VLAN security |
| 2 | Spanning Tree (STP) | Rapid PVST+, per-VLAN root bridge, PortFast, BPDU Guard |
| 3 | EtherChannel | LACP (802.3ad), logical port bundling |
| 4 | Inter-VLAN Routing | Layer-3 SVIs |
| 5 | OSPF | OSPFv2 Area 0, manually configured Router-IDs, passive interfaces |
| 6 | HSRP | Virtual IP, priority, preempt |
| 7 | DHCP & DNS | DHCP pools, internal DNS A records |
| 8 | ACLs | Extended + Standard ACLs, SSH restriction to IT VLAN only |
| 9 | CDP & LLDP | Neighbor discovery, disabling on access ports (security) |
| 10 | NTP | Server as Reference clock, all devices synchronized with authentication enabled|
| 11 | SYSLOG | Centralized logging to Server, ease of troubleshooting |
| 12 | SECURITY | Console and VTY local login (username: ademola, password: ccna) |
---

## 🌐 IP Addressing Summary

| VLAN | Name | Subnet | Size |
|------|------|--------|------|
| 10 | MANAGEMENT | 192.168.0.112/28 | 14 hosts (VLSM) |
| 20 | HR | 192.168.0.64/27 | 30 hosts (VLSM) |
| 30 | IT | 192.168.0.96/28 | 14 hosts (VLSM) |
| 40 | SERVERS | 192.168.0.128/28 | 14 hosts (VLSM) |
| — | WAN R1↔R2 | 10.0.0.0/30 | 2 hosts |
| — | Branch | 172.16.0.0/24 | 254 hosts |

---

## ✅ Verification Highlights

- `show ip ospf neighbor` → R1 & R2 in FULL state
- `show standby brief` → DSW1 Active, DSW2 Standby for VLAN 10 & 20
- `ping 192.168.0.100 source vlan 20` → **Fails** (ACL blocks HR → IT)
- `ping 192.168.0.132 source vlan 20` → **Succeeds** (server access allowed)
- `ipconfig` on PC-HR1 → DHCP address in 192.168.20.0/24
- `nslookup server1.techcorp.local` → Resolves to 192.168.0.132

---

## 🛠️ Requirements

- [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer) 8.0 or later
- Free Cisco NetAcad account to download Packet Tracer

---

*Built as part of my CCNA study journey. Feel free to fork, use, and learn from it!*
