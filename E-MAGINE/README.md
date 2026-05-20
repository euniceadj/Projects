# E-MAGINE Healthcare Network Redesign

**Type:** Academic Group Project — Network Design & Security  
**Course:** CYB330L  
**Tools:** Cisco Packet Tracer · EIGRP · VLANs · ASA Firewall · TACACS+ · ACLs  
**Status:** Completed

---

## Overview

Designed and implemented a multi-site HIPAA-compliant network for a simulated healthcare organization across four locations: Main, Orlando, Chicago, and a dedicated Data Center. Responsibilities included security architecture, ACL design, compliance mapping, and the final technical presentation.

---

## Network Architecture

- **Four sites:** Main, Orlando, Chicago, and Data Center connected via serial WAN links running EIGRP
- **Data Center:** Spine-leaf topology connecting six servers; VLAN 30 restricted to ePHI access by Finance and Clinical VLANs only
- **DMZ:** Isolated zone separating public-facing services from internal network segments
- **Routing:** EIGRP dynamic routing across all routers with DUAL algorithm for automatic failover on WAN link failure
- **VLANs:** Departmental segmentation (VLANs 10–50 at Orlando); each subnet uses a non-overlapping IP addressing scheme
- **Redundancy:** Dual serial connections between main routers; spine-leaf provides redundant paths in the Data Center

---

## Security Controls

- **Firewalls:** ASA 5506-X at Main (perimeter) and Orlando (independent boundary); stateful inspection on ICMP and HTTP
- **ACLs:** Extended ACLs on all routers (R1, R2, R3, Orlando, DC, Chicago)
- **Authentication:** TACACS+ server in DC for centralized device authentication; SSH v2 on all routers; Telnet disabled
- **Endpoint:** Port security on all access switches with sticky MAC and violation shutdown
- **Remote access:** Dedicated VPN interface on Main ASA with isolated address pool and NAT

---

## Regulatory Compliance

- **HIPAA** (45 CFR §164.306 / §164.312) — access control, audit controls, integrity, and transmission security
- **NIST SP 800-41 Rev. 1** — firewall placement and zone policy
- **Virginia CDPA**, **Florida FIPA**, and **Illinois PIPA** — state-level data protection requirements for each site

---

## Testing & Validation

- EIGRP neighbor relationships verified on all routers including Chicago-R1, Main-R1, Main-R2, Main-R3, DataCenter-R1, and Orlando Router
- Chicago networks (10.24.x.x) confirmed in the routing tables of all routers
- Data Center VLANs 10, 20, and 30 servers verified reachable from their respective Leaf switch SVIs
- SSH access confirmed requiring credentials; unauthorized Telnet connections rejected
- Serial link corrections validated by successful EIGRP adjacency between Chicago-R1 and Main-R1
