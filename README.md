# Secure Bank Network Architecture

A robust, enterprise-grade network infrastructure designed and simulated using **Cisco Packet Tracer**. This project demonstrates the design and implementation of a secure multi-branch banking network, establishing reliable WAN communication between a Head Office (HO) and two remote branches (Branch 1 & Branch 2), while ensuring strict data separation and network resilience.

## ✨ Core Engineering Features

* **Layered Network Topology:** Structured using a Hub-and-Spoke (Star) enterprise design, ensuring all remote branches communicate securely through the Head Office core.
* **Segmented Local Area Networks (LANs):** Individual subnetting structures applied per site to eliminate broadcast storm risks and optimize traffic boundaries.
* **Static WAN Routing:** Fixed, deterministic path routing engineered across Serial WAN links for absolute control over cross-branch routing paths.
* **End-to-End Gateways:** Properly configured Default Gateways across all infrastructure nodes (Managers, Tellers, ATMs) to maintain persistent transactional routing.

---

## 🏗 Network Topology & Architecture

The architecture segregates the banking infrastructure into three primary logical zones, utilizing dedicated routing nodes to mimic real-world financial data separation:
## 📁 Network Topology & Architecture

The architecture segregates the banking infrastructure into three primary locations:

`
              +-------------+
              | Head Office |  (LAN: 192.168.10.0/24)
              |  HO-Router  |
              +------+------+
                     |
                     |
       +-------------+-------------+
       |                           |
       | WAN: 10.0.0.0/8           | WAN: 11.0.0.0/8
       v                           v
+--------------+            +--------------+
|   Branch 1   |            |   Branch 2   |
|  BR-Router   |            | BR2-Router0  |
+--------------+            +--------------+

 (LAN: 192.168.20.0/24)   (LAN: 192.168.30.0/24)

1.  **Head Office (HO):** The central hub managing high-level business systems (HO-Manager, HO-Server) and transactional endpoints (HO-Teller, HO-ATM).
2.  **Branch 1 (BR):** A standard remote branch environment supporting local administrative personnel and customer banking services.
3.  **Branch 2 (BR2):** An expanded micro-branch deployment mapped dynamically into the wider enterprise system routing tables.

---

## 📊 IP Addressing & Subnetting Schema

### 1. Router Interfaces Configuration

| Router | Interface | IP Address | Subnet Mask | Communication Type |
| :--- | :--- | :--- | :--- | :--- |
| **HO-Router** | Gig0/0 (LAN) | `192.168.10.1` | `255.255.255.0` | Ethernet (LAN Hub) |
| **HO-Router** | Se0/2/0 (WAN) | `10.0.0.1` | `255.0.0.0` | Serial (WAN Link to BR) |
| **BR-Router** | Gig0/0 (LAN) | `192.168.20.1` | `255.255.255.0` | Ethernet (LAN Branch 1) |
| **BR-Router** | Se0/3/0 (WAN) | `10.0.0.2` | `255.0.0.0` | Serial (WAN Link to HO) |
| **BR2-Router0**| Gig0/0 (LAN) | `192.168.30.1` | `255.255.255.0` | Ethernet (LAN Branch 2) |
| **BR2-Router0**| Se0/3/1 (WAN) | `11.0.0.2` | `255.0.0.0` | Serial (WAN Link to Central) |

### 2. End Devices Configuration Matrix

| Device Name | Assigned IP Address | Subnet Mask | Default Gateway | Connection Type |
| :--- | :--- | :--- | :--- | :--- |
| **HO-Manager** | `192.168.10.2` | `255.255.255.0` | `192.168.10.1` | LAN (Head Office) |
| **HO-Teller** | `192.168.10.3` | `255.255.255.0` | `192.168.10.1` | LAN (Head Office) |
| **HO-ATM** | `192.168.10.4` | `255.255.255.0` | `192.168.10.1` | LAN (Head Office) |
| **BR-Manager** | `192.168.20.2` | `255.255.255.0` | `192.168.20.1` | LAN (Branch 1) |
| **BR-Teller** | `192.168.20.3` | `255.255.255.0` | `192.168.20.1` | LAN (Branch 1) |
| **BR-ATM** | `192.168.20.4` | `255.255.255.0` | `192.168.20.1` | LAN (Branch 1) |
| **BR2-PC0** | `192.168.30.2` | `255.255.255.0` | `192.168.30.1` | LAN (Branch 2) |
| **BR2-PC1** | `192.168.30.3` | `255.255.255.0` | `192.168.30.1` | LAN (Branch 2) |

---

## 🛠️ Implemented Technologies & Protocols

* **Static Routing Pathways:** Manual insertion of static parameters chosen over dynamic protocols to maintain tight enterprise policy bounds and optimize processing overhead on edge hardware.
* **Cisco IOS CLI Configuration:** All devices configured sequentially via standard IOS Command Line interface, establishing interface metrics and bringing link protocols up natively.
* **ICMP Diagnostics:** Built-in validation using Layer 3 ICMP echo queries (`ping`) to verify convergence and check reachability matrices end-to-end.

## 🚀 How to Open and Review

1. Download and install **Cisco Packet Tracer** (v8.0 or later recommended).
2. Clone this repository locally or directly download the `Bank network project-IT (4).pkt` tracking file.
3. Open the file inside Packet Tracer to view live topology, inspect router CLI startup scripts, or trigger ICMP PDU simulation cycles.
