#  University Network Topology Walkthrough

A step-by-step guide to implementing a university-wide network in **Cisco Packet Tracer**.

### Software

* **Cisco Packet Tracer:** [Download here](https://www.netacad.com/resources/lab-downloads)

---

## Network Overview

The network links the **Main Campus** and **Smaller Campus**, supporting internal services and external Internet access.

<img width="1898" height="820" alt="image" src="https://github.com/user-attachments/assets/4dffea17-15eb-417e-92f7-63624893b9b8" />


### 🏛️ Main Campus

| Layer            | Components           | Role                                                                                       |
| :--------------- | :------------------- | :----------------------------------------------------------------------------------------- |
| **Core**         | **Core Router (CR)** | Central routing hub, handles RIPv2, DHCP for Building A, and static route to the Internet. |
| **Distribution** | **DS-A, DS-B, DS-C** | Manage VLANs and aggregate traffic for each building.                                      |
| **Access**       | **AS-A, AS-B, AS-C** | Connect end-user PCs and labs.                                                             |

**Building Roles**

* **A – Admin & Business:** Management, HR, Finance, Business Faculty.
* **B – Academic:** Engineering, Computing, Art & Design.
* **C – IT & Labs:** IT Dept., Student Labs, Servers (e.g., Web, DNS).

**External Router (ER):** Connects to the Internet and Smaller Campus (via WAN or VPN).

---

### Smaller Campus

* **Smaller Campus Router (SCR):** Connects to Main Campus via WAN.
* **SDS + SAS Switches:** Manage VLANs for Staff and Student Labs.

---

## Configuration Summary

### 1. IP Addressing

Each department/faculty gets its own subnet.
Use /24 for LANs and /30 for router links.

**Example:**

* Bldg A: VLAN 10–40 (Mgmt, HR, Finance, Business)
* Bldg B: VLAN 50–60 (Engg, Design)
* Bldg C: VLAN 70–80 (IT, Labs)
* Smaller Campus: VLAN 90–100 (Staff, Students)

---

### 2. Switching

* **VLANs:** Unique IDs per department.
* **Trunks:** 802.1Q trunks between access/distribution/core.
* **Routing:** Router-on-a-Stick or L3 switch for inter-VLAN traffic.
* **Security:** Disable unused ports, use port security, and enable SSH.

---

### 3. Routing

* **RIPv2:** On CR and SCR, advertise internal subnets; set LANs as passive.
* **Static Routes:**

  * CR → default route to ER for Internet.
  * ER → optional static host route for external email server.

---

### 4. DHCP

* **Building A and B:** Every room must have a DCHP server PC which acts as DHCP server.

  * Assigns dynamic IPs for Management, HR, Finance, and Business VLANs.

---

### External Services

* **Email Server & Internet:** Accessible via Core → External Router → Cloud.

---
