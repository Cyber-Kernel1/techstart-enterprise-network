# TechStart Enterprise Network

A hierarchical enterprise network for the fictional company **TechStart**, designed and simulated in **Cisco Packet Tracer**. It connects three departments (Sales, Development, HR) to a centralized server farm through a core router, using static routing and DHCP.

![Topology](topology.png)

📄 Full documentation (English): [TechStart_Report.pdf](TechStart_Report.pdf)

## Overview
- Each department has its own router, switch, and /24 subnet
- Branch routers connect to R-CORE over dedicated point-to-point links
- Centralized services (DNS, Web, FTP) sit in a separate server subnet
- Clients get their IP, gateway, and DNS automatically via DHCP

## Network Components
| Layer | Devices |
|-------|---------|
| Core | R-CORE |
| Branch routers | R-Sales, R-Dev, R-HR (Cisco 1941) |
| Access switches | S-Sales, S-Dev, S-HR (Cisco 2960-24TT) |
| Server farm | S-Server (2960-24TT), S-DNS, S-Web, S-FTP |
| End devices | 9 PCs (3 per department) |

## Subnet Plan (all /24 – 255.255.255.0)
| Network | Subnet | Gateway | Usable range | Broadcast |
|---------|--------|---------|--------------|-----------|
| Sales LAN | 10.4.1.0/24 | 10.4.1.1 | .1 – .254 | 10.4.1.255 |
| Dev LAN | 10.4.2.0/24 | 10.4.2.1 | .1 – .254 | 10.4.2.255 |
| HR LAN | 10.4.3.0/24 | 10.4.3.1 | .1 – .254 | 10.4.3.255 |
| Servers | 10.4.4.0/24 | 10.4.4.1 | .1 – .254 | 10.4.4.255 |
| Sales ↔ Core link | 10.4.10.0/24 | 10.4.10.1 | | 10.4.10.255 |
| Dev ↔ Core link | 10.4.20.0/24 | 10.4.20.1 | | 10.4.20.255 |
| HR ↔ Core link | 10.4.30.0/24 | 10.4.30.1 | | 10.4.30.255 |

## Device Addressing
| Device | Interface | IP Address | Gateway | DNS |
|--------|-----------|------------|---------|-----|
| S-DNS | Fa0 | 10.4.4.10 | 10.4.4.1 | 10.4.4.10 |
| S-Web | Fa0 | 10.4.4.20 | 10.4.4.1 | 10.4.4.10 |
| S-FTP | Fa0 | 10.4.4.30 | 10.4.4.1 | 10.4.4.10 |
| R-Sales | Gi0/1 (LAN) | 10.4.1.1 | N/A | N/A |
| R-Sales | Gi0/0 (to core) | 10.4.10.2 | N/A | N/A |
| R-Dev | Gi0/1 (LAN) | 10.4.2.1 | N/A | N/A |
| R-Dev | Gi0/0 (to core) | 10.4.20.2 | N/A | N/A |
| R-HR | Gi0/1 (LAN) | 10.4.3.1 | N/A | N/A |
| R-HR | Gi0/0 (to core) | 10.4.30.2 | N/A | N/A |
| R-CORE | Gi0/0 – Gi0/3 | 10.4.10.1 / 10.4.20.1 / 10.4.30.1 / 10.4.4.1 | N/A | N/A |

## DHCP
Each branch router serves its own LAN. Hosts receive addresses from `.11` to `.254`.

| Pool | Network | Default Gateway | DNS |
|------|---------|-----------------|-----|
| SALES-POOL | 10.4.1.0/24 | 10.4.1.1 | 10.4.4.10 |
| DEV-POOL | 10.4.2.0/24 | 10.4.2.1 | 10.4.4.10 |
| HR-POOL | 10.4.3.0/24 | 10.4.3.1 | 10.4.4.10 |

## Routing
**Static routing** on all routers. R-CORE has static routes to every department LAN through its branch router, and each branch router sends traffic for other networks toward R-CORE.

## DNS
The DNS server (10.4.4.10) resolves `www.techstart.com` to the Web server (10.4.4.20).

## Testing & Verification
- Ping between PCs in different departments
- Open `www.techstart.com` from a PC browser
- FTP access to 10.4.4.30
- Verify DHCP lease: `ipconfig /all`
- `show ip route`, `show ip interface brief`

## How to Run
1. Install Cisco Packet Tracer
2. Open `Med_0.pkt`
3. Test from any PC (Command Prompt / Web Browser)

## Skills Demonstrated
IP subnetting · Static routing · DHCP · DNS/HTTP/FTP services · Hierarchical network design · Packet Tracer simulation

## Author
**Ahmad Madi** – Cyber Security Engineering Student
[LinkedIn](https://linkedin.com/in/ahmad-madi0) | [GitHub](https://github.com/Cyber-Kernel1)
