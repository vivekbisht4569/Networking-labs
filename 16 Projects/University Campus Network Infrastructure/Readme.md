# 🏫 University Campus Network Infrastructure

> A real-world enterprise networking project simulating a university campus network with VLAN segmentation, Router-on-a-Stick (ROAS), centralized DHCP services, Spanning Tree Protocol (STP), and inter-VLAN communication.

---

# 📌 Overview

This project simulates a secure and scalable university campus network designed using Cisco Packet Tracer. The network follows enterprise networking practices by logically separating departments into VLANs while enabling controlled communication between them through Router-on-a-Stick (ROAS).

Instead of assigning IP addresses manually, a centralized DHCP server automatically provides IP addresses to all client devices across multiple VLANs using DHCP Relay (`ip helper-address`).

The project also implements Spanning Tree Protocol (STP) to prevent Layer 2 switching loops and improve network reliability.

---

# 🎯 Objectives

- Design an enterprise-style campus network.
- Implement VLAN segmentation.
- Configure Router-on-a-Stick (ROAS) for Inter-VLAN Routing.
- Deploy a centralized DHCP server.
- Configure DHCP Relay using `ip helper-address`.
- Prevent Layer 2 loops using STP.
- Validate communication between all departments.

---

# 🏢 Network Architecture

The topology consists of:

- 1 Cisco 2811 Router
- 1 Cisco 3560 Core Switch
- 2 Cisco 2960 Access Switches
- 1 DHCP Server
- Multiple PCs distributed across departments

---

# 🖥 Department VLANs

| VLAN | Department | Network |
|------|------------|----------------|
| VLAN 10 | Administration | 192.168.10.0/24 |
| VLAN 20 | Faculty | 192.168.20.0/24 |
| VLAN 30 | Library | 192.168.30.0/24 |
| VLAN 40 | Computer Lab | 192.168.40.0/24 |

---

# ⚙ Technologies Implemented

- VLAN Segmentation
- IEEE 802.1Q Trunking
- Router-on-a-Stick (ROAS)
- Inter-VLAN Routing
- DHCP Server
- DHCP Relay (`ip helper-address`)
- Static IP Configuration
- Spanning Tree Protocol (STP)
- Cisco Switching Fundamentals

---

# 🔨 Configuration Methodology

## Phase 1 — Network Design

- Built the complete university topology.
- Connected all end devices.
- Added Core Switch, Access Switches, Router, and DHCP Server.

---

## Phase 2 — VLAN Configuration

Created four VLANs representing different university departments.

- VLAN 10 — Administration
- VLAN 20 — Faculty
- VLAN 30 — Library
- VLAN 40 — Computer Lab

Assigned every PC to its corresponding VLAN.

---

## Phase 3 — Trunk Configuration

Configured trunk links between:

- Router ↔ Core Switch
- Core Switch ↔ Access Switch 1
- Core Switch ↔ Access Switch 2

Allowed VLANs:

- VLAN 10
- VLAN 20
- VLAN 30
- VLAN 40

---

## Phase 4 — Router-on-a-Stick (ROAS)

Configured router subinterfaces for each VLAN.

Each VLAN received its own default gateway.

Example:

- VLAN 10 → 192.168.10.1
- VLAN 20 → 192.168.20.1
- VLAN 30 → 192.168.30.1
- VLAN 40 → 192.168.40.1

---

## Phase 5 — DHCP Deployment

Configured one centralized DHCP Server.

Created individual DHCP pools for:

- Administration
- Faculty
- Library
- Computer Lab

Each pool contained:

- Network Address
- Subnet Mask
- Default Gateway
- Start IP Address
- Maximum Users

---

## Phase 6 — DHCP Relay

Since the DHCP server resided in VLAN 40 while clients existed in multiple VLANs, DHCP Relay was configured using:

```bash
ip helper-address 192.168.40.10
```

on VLANs:

- VLAN 10
- VLAN 20
- VLAN 30

This allowed DHCP broadcast traffic to reach the centralized DHCP server.

---

## Phase 7 — STP Verification

Verified that:

- STP elected the correct Root Bridge.
- No switching loops existed.
- All redundant paths remained stable.

---

# 🔍 Troubleshooting & Challenges

During the project, several real-world networking issues were encountered and resolved.

---

## Issue 1 — PCs Failed to Obtain IP Addresses

### Symptoms

- DHCP Request Failed
- APIPA (169.254.x.x) addresses assigned
- PCs unable to communicate

### Root Cause

Initial troubleshooting revealed that DHCP itself was functioning correctly, but DHCP requests were not reaching the server.

### Resolution

- Verified DHCP pools.
- Verified server IP configuration.
- Verified DHCP service status.
- Confirmed DHCP Relay (`ip helper-address`) configuration.

---

## Issue 2 — PCs Could Not Ping Their Gateway

### Symptoms

- Static IP configured
- Unable to ping default gateway

### Root Cause

Incorrect Layer 2 forwarding path was suspected.

### Troubleshooting Steps

- Verified VLAN membership.
- Verified trunk links.
- Verified router subinterfaces.
- Verified VLAN tagging.

After corrections, gateway communication was successfully restored.

---

## Issue 3 — Trunk Configuration Error

One of the biggest troubleshooting lessons occurred during trunk configuration.

Initially, the DHCP Server port (Fa0/4) on the Core Switch was mistakenly configured as a trunk port.

### Why This Was Incorrect

A DHCP Server is an end device and should never operate as a trunk.

Only network devices such as:

- Routers
- Switches

should participate in trunk links.

### Correct Configuration

Router ↔ Core Switch → Trunk

Access Switch ↔ Core Switch → Trunk

DHCP Server ↔ Core Switch → Access Port (VLAN 40)

Once Fa0/4 was changed back to an **Access Port** in VLAN 40, DHCP communication functioned correctly.

This was the primary issue preventing successful DHCP operation.

---

## Issue 4 — End-to-End Testing

Performed complete connectivity verification.

Verified:

- DHCP address assignment
- Gateway reachability
- Inter-VLAN Routing
- Server communication
- Cross-department communication

All tests completed successfully.

---

# 📷 Project Screenshots

Include the following screenshots inside the repository.

- Network Topology
- VLAN Configuration
- Trunk Configuration
- Router-on-a-Stick Configuration
- DHCP Pool Configuration
- DHCP Lease Assignment
- Successful Ping Between VLANs
- STP Verification
- Router Configuration
- Final Working Topology

---

# 🧠 Key Networking Concepts Learned

- VLAN Segmentation
- Enterprise Network Design
- Router-on-a-Stick (ROAS)
- Inter-VLAN Routing
- IEEE 802.1Q Trunking
- DHCP Server Deployment
- DHCP Relay (`ip helper-address`)
- Static vs Dynamic IP Addressing
- Spanning Tree Protocol (STP)
- Layer 2 & Layer 3 Troubleshooting
- Systematic Network Troubleshooting Methodology

---

# ✅ Project Outcome

Successfully designed and deployed a fully functional enterprise-style university network capable of:

- Automatic IP address allocation using a centralized DHCP server.
- Communication between multiple VLANs through Router-on-a-Stick.
- Secure Layer 2 segmentation using VLANs.
- Loop-free switching with STP.
- Reliable inter-department communication.
- Real-world troubleshooting of trunking, DHCP relay, VLAN configuration, and routing issues.

This project strengthened practical knowledge of enterprise networking while reinforcing structured troubleshooting techniques used in production environments.

---

## 🛠 Technologies Used

- Cisco Packet Tracer
- Cisco 2811 Router
- Cisco Catalyst 3560 Switch
- Cisco Catalyst 2960 Switch
- IEEE 802.1Q Trunking
- Router-on-a-Stick (ROAS)
- DHCP
- STP
- VLANs
- IPv4 Networking

---

