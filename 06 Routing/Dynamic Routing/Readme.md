# Dynamic Routing Lab (RIP / OSPF / EIGRP)

## 📌 Project Overview

This lab demonstrates the implementation and verification of dynamic routing protocols in a simulated enterprise network environment.

Unlike static routing, where routes are manually configured by administrators, dynamic routing allows routers to automatically exchange routing information, discover networks, and update routing tables when network changes occur.

This lab focuses on understanding how routers communicate, learn routes, and maintain network connectivity using dynamic routing protocols.

---

## 🎯 Objectives

* Understand dynamic routing concepts
* Configure dynamic routing between multiple routers
* Learn automatic route advertisement
* Verify routing table updates
* Test end-to-end connectivity between different networks
* Compare dynamic routing behavior with static routing

---

## 🧠 Concepts Covered

### Dynamic Routing

Dynamic routing allows routers to automatically learn and maintain routes using routing protocols.

Advantages:

* Automatic route updates
* Better scalability
* Reduced manual configuration
* Network failure adaptation
* Efficient route selection

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

## Example Network Design

```
LAN A          LAN B          LAN C

PCs           PCs            PCs
 |             |              |
Switch        Switch         Switch
 |             |              |
Router1 ---- Router2 ---- Router3
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

# Dynamic Routing Configuration

## RIP Configuration Example

### Router 1

```bash
router rip
version 2

network 192.168.1.0
network 10.0.12.0

no auto-summary
```

---

### Router 2

```bash
router rip
version 2

network 10.0.12.0
network 10.0.23.0

no auto-summary
```

---

### Router 3

```bash
router rip
version 2

network 10.0.23.0
network 192.168.3.0

no auto-summary
```

---

# Verification Commands

## Check Routing Table

```bash
show ip route
```

Expected output:

```
R 192.168.3.0/24 via 10.0.12.2
```

`R` indicates the route was learned using RIP.

---

## Check Active Routing Protocol

```bash
show ip protocols
```

Displays:

* Routing protocol running
* Advertised networks
* Timers
* Neighbor information

---

## Test Connectivity

Ping from LAN A PC:

```bash
ping 192.168.3.x
```

Expected Result:

```
Reply received successfully
```

---

# Troubleshooting Commands

Check interfaces:

```bash
show ip interface brief
```

Check neighbors:

```bash
show cdp neighbors
```

Check routes:

```bash
show ip route
```

Debug routing updates:

```bash
debug ip rip
```

---

# Problems Encountered

## Issue 1: Routes Not Appearing

Cause:

* Wrong network advertised
* Interface shutdown

Solution:

* Verified interfaces
* Corrected network statements

---

## Issue 2: Ping Failed Between LANs

Cause:

Missing dynamic route entry.

Solution:

Checked:

```bash
show ip route
```

Reconfigured routing protocol.

---

# Key Learnings

✔ Dynamic routing configuration
✔ Router communication process
✔ Routing table analysis
✔ Network troubleshooting
✔ Route advertisement concepts
✔ Multi-router connectivity testing

---

# SOC Analyst Relevance

Understanding routing helps SOC analysts investigate:

* Suspicious network paths
* Unauthorized network communication
* Traffic flow issues
* Firewall/SIEM alerts
* Lateral movement investigation

Example:

An attacker moving between internal networks requires understanding:

```
Source Network
      |
Router
      |
Destination Network
```

Network knowledge helps identify abnormal communication.

---

# Tools Used

* Cisco Packet Tracer
* Cisco IOS CLI
* ICMP Testing
* Routing Table Analysis

---

# Status

Completed ✔

Lab Type: Networking Fundamentals
Focus Area: SOC Analyst / Network Security Foundation
