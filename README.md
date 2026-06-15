[README.md](https://github.com/user-attachments/files/28955667/README.md)
# Company Enterprise Network - CCN Term Project

A scalable, multi-department enterprise network designed and simulated in Cisco Packet Tracer, built as a Computer Communication Networks (CCN) term project for the Faculty of Information Technology & Computer Science, University of Central Punjab.

## Project Objectives

- Design and implement a scalable, multi-department enterprise network architecture using Cisco Packet Tracer.
- Automate IP address allocation across end-user departments (IT, HR, Finance) using DHCP to eliminate manual configuration errors.
- Achieve dynamic routing across enterprise branches/zones using OSPF (Area 0) for fast convergence and optimal path selection.
- Deploy centralized network services: a DNS Server for custom domain resolution (`www.companyenterprise.com`), a Web Server (HTTP/HTTPS) for the internal corporate portal, and an FTP Server for secure file transfers.

## Network Overview

### Departments / VLANs
The network is logically segmented using dedicated VLANs per department (IT, HR, Finance) for improved security and traffic management. Trunk links (802.1Q) connect switches to routers, carrying traffic from all VLANs.

### Inter-VLAN Routing
Implemented using the **Router-on-a-Stick (ROAS)** method. Each department router has its physical `GigabitEthernet0/0` interface divided into logical sub-interfaces (e.g., `Gi0/0.10` for VLAN 10, `Gi0/0.20` for VLAN 20, `Gi0/0.30` for VLAN 30), each configured with `encapsulation dot1Q` and a gateway IP.

### Routing Protocol - OSPF (Single Area, Area 0)
- **Why OSPF:** Link-state protocol offering rapid convergence, VLSM support, and loop-free topology mapping via the SPF algorithm.
- **Implementation:** All core routers run under `router ospf 1`, advertising department subnets and the Server Zone (`192.168.50.0/24`) into a single backbone area (Area 0) for seamless any-to-any connectivity.

### Centralized Services (Server Zone)
| Service | Configuration |
|---|---|
| DHCP | Global pool automatically assigns IP, subnet mask, default gateway, and DNS server (`192.168.50.2`) to all dynamic hosts |
| DNS | A-Record mapping `www.companyenterprise.com` → `192.168.50.2` |
| HTTP/HTTPS | Enabled on the DNS/Web server, hosting the enterprise welcome portal |
| FTP | Authenticated file server (`admin`/`admin`) with full Read/Write/Delete/Rename/List permissions |

## Testing & Verification

- Ping connectivity between departments and the server zone
- Traceroute across OSPF-routed paths
- Application-layer access tests (DNS resolution + web portal)
- FTP login and file operations

All tests confirmed full connectivity and correct functioning of routing and services across the network.

## Repository Contents

| File | Description |
|---|---|
| `FINAL_CCN_LAB_PROJECT.pkt` | Cisco Packet Tracer project file (open with Packet Tracer) |
| `Company_Enterprise_Network__CCN_Project_.docx` | Full project report (topology diagram, IP addressing table, device configs, VLAN details, and screenshots) |

## How to Open

1. Install [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer).
2. Open `FINAL_CCN_LAB_PROJECT.pkt` to explore the live topology and configurations.
3. Refer to the `.docx` report for detailed documentation, IP addressing scheme, and verification screenshots.

## Conclusion

This project demonstrates the design, implementation, and verification of a scalable enterprise network. The integration of OSPF dynamic routing with Router-on-a-Stick Inter-VLAN routing achieved seamless connectivity between departmental segments and centralized services (DHCP, DNS, FTP), validating a stable and functional corporate network infrastructure.
