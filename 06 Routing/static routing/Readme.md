# Static Routing Lab

## 📌 Project Overview

This lab demonstrates the implementation and verification of static routing in a multi-network environment.

Static routing is a routing method where network administrators manually configure routes on routers. Unlike dynamic routing protocols, static routes do not automatically update when network changes occur.

This lab focuses on understanding manual route configuration, routing tables, packet forwarding, and troubleshooting connectivity between different networks.

---

# 🎯 Objectives

* Understand static routing fundamentals
* Configure communication between multiple networks
* Manually create routing table entries
* Understand next-hop routing concepts
* Verify end-to-end connectivity
* Troubleshoot routing issues

---

# 🧠 Concepts Covered

## Static Routing

A static route tells a router how to reach a remote network manually.

General Syntax:

```bash
ip route [destination-network] [subnet-mask] [next-hop-ip]
```

Example:

```bash
ip route 192.168.3.0 255.255.255.0 10.0.12.2
```

Meaning:

Destination:

```
192.168.3.0/24
```

can be reached through:

```
10.0.12.2
```

---

# Static vs Dynamic Routing

| Static Routing               | Dynamic Routing              |
| ---------------------------- | ---------------------------- |
| Manually configured          | Automatically learns routes  |
| No routing protocol required | Uses protocols like RIP/OSPF |
| Low CPU usage                | More resource usage          |
| Best for small networks      | Better for large networks    |
| Does not adapt automatically | Automatically updates        |

---

# Network Topology

## Devices Used

| Device               | Quantity |
| -------------------- | -------- |
| Routers              | 3        |
| Switches             | 3        |
| PCs                  | 6        |
| Ethernet Connections | Multiple |

---

# Network Design

```
LAN A                 LAN B                 LAN C


PCs                   PCs                   PCs
 |                     |                     |
Switch                Switch                Switch
 |                     |                     |
Router1 -------- Router2 -------- Router3


192.168.1.0/24        Transit        192.168.3.0/24
```

---

# IP Addressing Table

| Device  | Interface | IP Address  | Network        |
| ------- | --------- | ----------- | -------------- |
| Router1 | G0/0      | 192.168.1.1 | 192.168.1.0/24 |
| Router1 | G0/1      | 10.0.12.1   | 10.0.12.0/30   |
| Router2 | G0/0      | 10.0.12.2   | 10.0.12.0/30   |
| Router2 | G0/1      | 10.0.23.1   | 10.0.23.0/30   |
| Router3 | G0/0      | 10.0.23.2   | 10.0.23.0/30   |
| Router3 | G0/1      | 192.168.3.1 | 192.168.3.0/24 |

---

# Configuration Steps

---

# 1. Router Interface Configuration

## Router 1

```bash
enable
configure terminal

interface g0/0
ip address 192.168.1.1 255.255.255.0
no shutdown


interface g0/1
ip address 10.0.12.1 255.255.255.252
no shutdown
```

---

## Router 2

```bash
enable
configure terminal


interface g0/0
ip address 10.0.12.2 255.255.255.252
no shutdown


interface g0/1
ip address 10.0.23.1 255.255.255.252
no shutdown
```

---

## Router 3

```bash
enable
configure terminal


interface g0/0
ip address 10.0.23.2 255.255.255.252
no shutdown


interface g0/1
ip address 192.168.3.1 255.255.255.0
no shutdown
```

---

# Static Route Configuration

## Router 1

Router1 does not know about LAN C.

Add route:

```bash
ip route 192.168.3.0 255.255.255.0 10.0.12.2
```

Explanation:

Destination Network:

```
192.168.3.0
```

Forward packets to:

```
Router2 → 10.0.12.2
```

---

## Router 2

Router2 needs routes for both LAN networks.

Route to LAN A:

```bash
ip route 192.168.1.0 255.255.255.0 10.0.12.1
```

Route to LAN C:

```bash
ip route 192.168.3.0 255.255.255.0 10.0.23.2
```

---

## Router 3

Router3 needs route back to LAN A.

```bash
ip route 192.168.1.0 255.255.255.0 10.0.23.1
```

---

# Verification

## Check Interface Status

```bash
show ip interface brief
```

Expected:

```
Interface        Status

Gig0/0           UP
Gig0/1           UP
```

---

## Check Routing Table

Command:

```bash
show ip route
```

Expected Output:

```
S 192.168.3.0/24 via 10.0.12.2
```

Meaning:

```
S = Static Route
```

Router learned this route manually.

---

# Connectivity Testing

From LAN A PC:

```bash
ping 192.168.3.x
```

Expected Result:

```
Reply from 192.168.3.x
```

Communication Successful ✔

---

# Packet Flow Explanation

Example:

PC-A sends traffic to PC-C

Step 1:

PC-A → Router1

Step 2:

Router1 checks routing table

Step 3:

Static route found:

```
192.168.3.0 via 10.0.12.2
```

Step 4:

Packet forwarded:

```
Router1 → Router2 → Router3 → PC-C
```

---

# Troubleshooting

## Problem 1:

Ping failed

Checks:

```bash
show ip route
```

```bash
show ip interface brief
```

Possible Causes:

* Missing static route
* Wrong next-hop IP
* Interface shutdown
* Incorrect gateway

---

## Problem 2:

One-way communication

Cause:

Return route missing.

Example:

Router1 knows Router3 network

but

Router3 does not know Router1 network.

Fix:

Add reverse static route.

---

# Important Commands Learned

| Command                 | Purpose              |
| ----------------------- | -------------------- |
| show ip route           | View routing table   |
| show running-config     | View configuration   |
| show ip interface brief | Check interfaces     |
| ping                    | Connectivity testing |
| traceroute              | Check packet path    |

---

# SOC Analyst Relevance

Routing knowledge helps SOC analysts understand:

* Internal network communication
* Traffic paths
* Firewall alerts
* Network segmentation
* Lateral movement detection

Example:

Suspicious connection:

```
Workstation
     |
Router
     |
Unknown Network
```

Understanding routes helps identify whether communication is expected or abnormal.

---

# Skills Gained

✔ Cisco router configuration
✔ Static route creation
✔ IP addressing
✔ Network troubleshooting
✔ Routing table investigation
✔ Packet flow understanding

---

# Tools Used

* Cisco Packet Tracer
* Cisco IOS CLI
* ICMP
* Routing Table Analysis

---

# Status

Completed ✔

Category: Networking Fundamentals
Focus: SOC Analyst / Network Security Foundation
