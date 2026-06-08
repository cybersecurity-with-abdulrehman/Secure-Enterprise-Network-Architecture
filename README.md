# 🌐 Secure Enterprise Network Architecture Blueprint

**Author:** Abdul Rehman Rashid | Network & Information Security Engineer

## 📌 What is this?
This repository showcases a production-ready corporate network infrastructure blueprint designed for high availability, zero-downtime redundancy, and strict security perimeter segmentation. The architecture is fully compatible with enterprise environments utilizing MikroTik, Cisco, and corporate firewall devices.

## 🛠️ Key Architectural Features
* **Dual WAN Failover (High Availability):** Implements a 2 WAN automatic failover mechanism ensuring 100% network uptime; if the primary ISP link drops, traffic instantly routes through the secondary backup link without interrupting business operations.
* **Network Segmentation (VLANs):** Strict isolation of sensitive business zones (Management, HR, Finance, and Production Servers) from standard employee networks and Guest Wi-Fi to limit lateral movement in case of a breach.
* **Hardened Edge Security (ACLs & DMZ):** Public-facing web servers are placed in a strictly monitored Demilitarized Zone (DMZ), protected by robust Access Control Lists (ACLs) allowing only essential protocols (HTTP/HTTPS).

## 💼 Business Value (Why clients need this)
An unsegmented, single-ISP network is a ticking time bomb for data loss and operational shutdown. This architecture ensures:
1. **Business Continuity:** No lost revenue due to internet service provider outages.
2. **Data Breach Containment:** Ransomware or malware in the employee network cannot easily hop over to production servers or financial endpoints.
3. **Compliance Ready:** Adheres to enterprise security frameworks by isolating corporate data environments.
