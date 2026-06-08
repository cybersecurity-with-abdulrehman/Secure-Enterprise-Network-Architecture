# 🌐 Secure Enterprise Network Architecture Blueprint

**Author:** Abdul Rehman Rashid | Network & Information Security Engineer

## 📌 Project Overview
This repository contains a production-ready, highly available network architecture designed for modern corporate infrastructures. The blueprint emphasizes absolute network redundancy, strict security segmentation (VLANs), and firewalled edge perimeters to ensure 100% operational uptime and zero-trust internal security.

---

## 🗺️ Logical Network Segmentation & IP Schema

The infrastructure is segmented into isolated broadcast domains (VLANs) via a Layer 3 Core Switch/Router setup to enforce strict traffic rules and prevent lateral movement of potential malware.

| Network Zone | VLAN ID | Subnet Pool | Security Access Level / Rules |
| :--- | :---: | :--- | :--- |
| **WAN 1 (Primary ISP)** | - | DHCP / Static | Active Main Gateway (Fiber Link) |
| **WAN 2 (Backup ISP)** | - | DHCP / Static | Failover Secondary Gateway (LTE/Radio Link) |
| **Management Zone** | VLAN 10 | 192.168.10.0/24 | Strictly restricted. Only authorized IT admin MACs allowed. |
| **Corporate Staff (HR/Fin)**| VLAN 20 | 192.168.20.0/24 | Can access internet; Zero access to Management or DMZ. |
| **Demilitarized Zone (DMZ)**| VLAN 30 | 10.0.30.0/24 | Hosts Public Web/Data Servers. Heavily Firewalled. |
| **Guest Network (Wi-Fi)** | VLAN 40 | 172.16.40.0/24 | Internet access only. Isolated from all internal corporate systems. |

---

## 🛠️ Key Architectural Implementations

### 1. Dual WAN Automatic Failover (MikroTik / Cisco Style)
* **Mechanism:** Implements Advanced IP Route Tracking (Check Gateway via Ping).
* **Operation:** Primary WAN 1 is assigned `Distance=1`. Secondary WAN 2 is assigned `Distance=2`. 
* **Failover Logic:** If the router detects 3 consecutive ping failures on WAN 1, it automatically invalidates the primary route. Traffic seamlessly switches to WAN 2 within **< 3 seconds**, ensuring zero downtime for enterprise operations.

### 2. Hardened Perimeter & Access Control Lists (ACLs)
* **Inbound Rules:** The Edge Firewall blocks all unsolicited incoming traffic by default (`Default Deny`). Only explicit ports (TCP 80/443 for DMZ web servers) are mapped via secure Destination NAT (DNAT).
* **Inter-VLAN Interruption:** Traffic between VLAN 20 (Staff) and VLAN 10 (Management) is completely dropped at the Layer 3 boundary. Staff cannot scan or access network switches, firewalls, or routers.

### 3. DMZ (Demilitarized Zone) Isolation
* Public-facing servers are sandboxed in VLAN 30. Even if a web application gets compromised by an attacker, the firewall prevents the DMZ servers from initiating any outbound connections into the internal corporate network pool.

---

## 💼 Business Value (Why this matters to Clients)
1. **Business Continuity:** Eliminates costly downtime caused by internet service provider (ISP) outages.
2. **Ransomware Containment:** If an employee opens a malicious email attachment on the Wi-Fi or Staff network, the breach is completely contained and cannot pivot to critical backend production servers.
3. **Compliance Ready:** Adheres to essential enterprise cybersecurity standards by ensuring complete isolation of corporate data environments.
