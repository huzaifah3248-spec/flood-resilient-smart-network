# Flood-Resilient Smart City & Village Communication Network

A comprehensive Cisco Packet Tracer network simulation engineered to maintain mission-critical civic communication, emergency service coordination, and automated IoT disaster response during severe flood conditions[cite: 5].

---

## 📌 Project Overview

Urban and rural disaster management requires highly segmented, secure, and fault-tolerant network infrastructure[cite: 5]. This project implements:
* **Departmental Isolation:** Dedicated Virtual Local Area Networks (VLANs) with Layer 3 inter-VLAN routing[cite: 5].
* **Dynamic & Redundant Routing:** RIPv2 mesh topology connecting District Core, Village Gateway, and Backup Link paths[cite: 5].
* **Perimeter Security:** Cisco ASA Firewall with adaptive Access Control Lists (ACLs) and Dynamic Network Address Translation (NAT)[cite: 5].
* **Core Network Services:** Centralized multi-pool DHCP, DNS domain resolution, Emergency Web, FTP, and Mail servers[cite: 5].
* **Smart IoT Flood Mitigation:** Automated water-level sensing, siren triggers, emergency floodgates, warning lights, and camera monitoring[cite: 5].

---

## 🏗 Network Architecture & Topology

### 1. High-Level Topology Structure
* **District Core:** `SW-Core-L3` (Layer 3 Switch), `R1-District-Core`, `FW-District`[cite: 5].
* **Village & Redundant Path:** `R2-Village-Gateway`, `R3-Backup-Link`, `SW-Village`, `HG-Village` (Home Gateway)[cite: 5].
* **Server Farm:** Centralized servers providing DHCP, DNS, Emergency Web, Mail, FTP, and IoT registration[cite: 5].
* **Public & Edge Access:** Wireless Access Point (`AP-PublicWiFi`) and remote ISP simulation via `R4-ISP`[cite: 5].

---

## 🔢 Addressing & Subnetting Plan

| VLAN ID | Subnet Name | Network Address | Default Gateway | Function / Assignment |
| :--- | :--- | :--- | :--- | :--- |
| **VLAN 10** | RESCUE | `192.168.10.0/24` | `192.168.10.1` | Emergency Rescue Services[cite: 5] |
| **VLAN 20** | HOSPITAL | `192.168.20.0/24` | `192.168.20.1` | Healthcare & Medical Coordination[cite: 5] |
| **VLAN 30** | POLICE | `192.168.30.0/24` | `192.168.30.1` | Law Enforcement & Security[cite: 5] |
| **VLAN 40** | TRAFFIC | `192.168.40.0/24` | `192.168.40.1` | Evacuation & Route Control[cite: 5] |
| **VLAN 50** | GOVT | `192.168.50.0/24` | `192.168.50.1` | Administration & Civil Coordination[cite: 5] |
| **VLAN 60** | SERVER_ROOM | `192.168.60.0/24` | `192.168.60.1` | Core Data & Application Infrastructure[cite: 5] |
| **VLAN 70** | PUBLIC_WIFI | `192.168.70.0/24` | `192.168.70.1` | Public Emergency Wi-Fi Access[cite: 5] |
| **VLAN 80** | VILLAGE_BACKUP | `192.168.80.0/24` | `192.168.80.254` | Village Control & Disaster Fallback[cite: 5] |
| **VLAN 99** | MANAGEMENT | `192.168.99.0/24` | `192.168.99.1` | Network Switch/Router Management[cite: 5] |

### Router Point-to-Point Links
* **SW-Core-L3 ↔ R1-District-Core:** `10.0.1.0/30`[cite: 5]
* **R1-District-Core ↔ R2-Village-Gateway:** `10.0.0.0/30`[cite: 5]
* **R2-Village-Gateway ↔ R3-Backup-Link:** `10.0.0.4/30`[cite: 5]
* **R1-District-Core ↔ R3-Backup-Link:** `10.0.0.8/30`[cite: 5]
* **R3-Backup-Link ↔ FW-District:** `10.0.3.0/30`[cite: 5]
* **FW-District ↔ R4-ISP (Outside):** `8.8.8.0/24`[cite: 5]
* **R4-ISP ↔ Outer-World Hosts:** `203.0.113.0/24`[cite: 5]

---

## ⚙️ Core Configuration & Protocols

### Routing Engine
* **Inter-VLAN Routing:** Enabled via Switched Virtual Interfaces (SVIs) on `SW-Core-L3` with IP routing enabled[cite: 5].
* **Dynamic Routing:** RIP Version 2 configured without auto-summarization (`no auto-summary`) across `R1`, `R2`, and `R3`[cite: 5].
* **Backup Pathing:** Dual default routes and prioritized static routes directing traffic through alternative links when primary links saturate or fail[cite: 5].

### Firewall & NAT Security Policies (`FW-District`)
* **Dynamic PAT (NAT):** Maps all internal LAN subnets (`192.168.0.0/16`) and router links (`10.0.0.0/8`) to the outside interface `8.8.8.2`[cite: 5].
* **Access Control List Modes:**
  * `OUTSIDE-IN`: Permits standard diagnostic and application traffic (HTTP, HTTPS, SMTP, DNS, ICMP)[cite: 5].
  * `OUTSIDE-FLOOD`: Strict emergency mode blocking general ICMP probing while strictly allowing emergency alerts, DNS, FTP, and mail[cite: 5].
  * `OUTSIDE-SECURE`: Production rule set blocking unauthorized inbound network mapping while permitting only targeted service access and established return streams[cite: 5].

### Core Server Stack
* **DHCP Pools:** Distinct pools for `Rescue-Pool`, `Hospital-Pool`, `Police-Pool`, `Traffic-Pool`, `Govt-Pool`, and `PublicWiFi-Pool` allocating IP, subnet, gateway, and DNS parameters[cite: 5].
* **DNS A-Records:**
  * `emergency.gov.pk` ➔ `192.168.60.12`[cite: 5]
  * `floodalert.local` ➔ `192.168.60.12`[cite: 5]
  * `mail.flood.local` ➔ `192.168.60.13`[cite: 5]
  * `iot.flood.local` ➔ `192.168.60.14`[cite: 5]
  * `ftp.flood.local` ➔ `192.168.60.15`[cite: 5]

---

## 🌊 Smart IoT Flood Subsystem

The village segment is wired into a dedicated wireless Home Gateway (`HG-Village`) managing local environmental sensors and actuators[cite: 5]:
* **`IoT-FloodSensor`:** Real-time water-level detection[cite: 5].
* **`IoT-Siren` & `IoT-WarningLight`:** Localized auditory and visual hazard warnings[cite: 5].
* **`IoT-Gate`:** Automatic closure of vulnerable roads and water barriers[cite: 5].
* **`IoT-Camera`:** Surveillance feed for the emergency response center[cite: 5].

---

## 🚀 How to Run & Verify

1. Download and install **Cisco Packet Tracer (v8.0+)**.
2. Open `flood resilient.pkt` in Packet Tracer.
3. Switch between **Realtime** and **Simulation** mode to test data flows[cite: 5]:
   * **Ping Tests:** Validate inter-VLAN routing from Department PCs (`PC12`, `PC15`, `PC16`) to Server IPs[cite: 5].
   * **Web Browser Tests:** Open desktop browser on any host and navigate to `http://emergency.gov.pk` or `http://floodalert.local`[cite: 5].
   * **Security Verification:** Inbound traffic from external hosts (`PC-OuterCity3`) to unapproved internal addresses is blocked by the firewall as designed[cite: 5].

---

## 👥 Authors
* **Umar Ali** (S2025AI002)[cite: 5]
* **Huzaifa** (S2025AI036)[cite: 5]
* *Department of Artificial Intelligence, NASTP Institute of Information Technology (NIIT)*[cite: 5]
