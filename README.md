# Smart Campus Multi-Site Enterprise Network Architecture
A high-availability, multi-campus enterprise network designed and simulated in Cisco Packet Tracer. This project features a 4-node redundant core mesh, dynamic multi-area routing, robust security filtering via Extended ACLs, and seamless enterprise service delivery.

## 📌 Project Overview
This architecture simulates a modern university enterprise network connecting a **Main Campus** with two regional sub-campuses (**Sub-Campus 1** and **Sub-Campus 2**). The infrastructure provides secure, role-based connectivity for three primary departments: Computer Science (CS), Electrical Engineering (EE), and Administration.

### 🏗️ Network Architecture Design
* **Core Backbone:** 4 Internal Core Routers arranged in a high-availability mesh topology to eliminate Single Points of Failure (SPOF).
* **Edge Boundaries:** 4 Dedicated Border Routers handling WAN traffic, sub-campus branch aggregation, and external internet transport.
* **Department Segmentation:** Hierarchical VLAN structures separating user traffic at Layer 2 to minimize broadcast storms and isolate network segments.

---

## 🛠️ Technical Specifications & Implementation

### 1. Routing Domain Architecture
* **Interior Gateway Protocol (IGP):** **OSPFv2 (Area 0)** deployed across **8 routing nodes** (4 Core Routers, 4 Border Routers) running Dijkstra's Shortest Path First algorithm for rapid convergence and path redundancy.
* **External Gateway Interface:** Connected to the public Internet Service Provider (ISP) via a static **Default Route (`0.0.0.0/0`)** to prevent internal topology leakage.

### 2. Layer 2 & Layer 3 Switching
* **Inter-VLAN Routing:** Managed via Switch Virtual Interfaces (SVIs) on Layer 3 Multilayer Switches.
* **Trunking Protocols:** IEEE 802.1Q encapsulation configured on all switch-to-switch and switch-to-core pathways.
* **VLAN Assignments per Site:**
    * **VLAN 10:** Computer Science Department (CS)
    * **VLAN 20:** Electrical Engineering Department (EE)
    * **VLAN 30:** Administration (Admin)

### 3. Enterprise Services (TCP/UDP Infrastructure)
* **Web Server (HTTP):** Hosted on **TCP Port 80** for internal learning management portals.
* **Mail Server (SMTP):** Configured on **TCP Port 25** for institutional email delivery.
* **File Server (FTP):** Operating on **TCP Ports 20/21** for secure file storage and transfers.
* **Dynamic Addressing & Resolution:** Centralized **DHCP (UDP 67/68)** scopes for automatic client scaling alongside **DNS (UDP 53)** for local domain translation.

---

## 🔒 Security & Traffic Engineering
To enforce strict institutional compliance, **Extended Access Control Lists (ACLs)** are applied inbound at the gateway level to restrict traffic based on source network, destination host, and specific application ports:

* **Admin Isolation Rules:** Sub-Campus 1 Admin department (`192.168.2.64/27`) is dynamically restricted from accessing the central Web Server (`192.168.1.100`) via HTTP over **TCP port 80**, while maintaining baseline ICMP (Ping) diagnostics.
* **IP Conflict Prevention:** Critical IP allocations (such as network printers on endpoints `.21`, `.51`, and `.85`) are actively withheld using `ip dhcp excluded-address` rules to isolate static peripherals from dynamic student scopes.

---

## 🧪 Redundancy & Validation Testing
The infrastructure supports strict failover verification:
1.  **Link-State Convergence Test:** Initiating a continuous transmission (`ping -t`) across the WAN and manually shutting down a primary interface (`shutdown`) prompts OSPF to instantly reroute packets through a backup mesh boundary within seconds.
2.  **Path Traversal Verification:** Using `traceroute` paths confirms the physical transition of data packages over alternate core routers during simulated structural line cuts.

---

## 📂 How to Run the Project
1. Download and install **Cisco Packet Tracer** (v8.0 or higher recommended).
2. Clone this repository to your local machine:
   ```bash
   git clone [https://github.com/mhamzashahidw/CN_University-Network.git](https://github.com/mhamzashahidw/CN_University-Network.git)
