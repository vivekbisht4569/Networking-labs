# 🔐 Router-on-a-Stick (ROAS) Lab

---

## 📌 Overview

This project demonstrates **Inter-VLAN Routing using Router-on-a-Stick (ROAS)** in Cisco Packet Tracer.

The objective of this lab was to:

* Create multiple VLANs
* Configure trunking between switches
* Enable communication between VLANs using a router
* Understand how subinterfaces and 802.1Q tagging work

---

## 🏢 Network Scenario

The network is divided into two departments:

* 🟦 VLAN 10 → IT Department
* 🟨 VLAN 20 → Accounts Department

Two switches are connected through a trunk link, and a router is used to route traffic between VLANs.

---

## 🧩 Topology Description

* 1 Router (Cisco 2811)
* 2 Cisco 2960 Switches
* Multiple PCs & Laptops
* Trunk link between switches
* Router connected to switch using a single trunk connection

---

## 🌐 IP Addressing Scheme

### 🟦 VLAN 10 – IT Department

| Device  | IP Address    |
| ------- | ------------- |
| PC1     | 192.168.10.5  |
| Laptop1 | 192.168.10.6  |
| Laptop2 | 192.168.10.10 |
| PC2     | 192.168.10.15 |

**Network:** `192.168.10.0/24`
**Gateway:** `192.168.10.1`

---

### 🟨 VLAN 20 – Accounts Department

| Device  | IP Address    |
| ------- | ------------- |
| Laptop3 | 192.168.20.5  |
| PC3     | 192.168.20.6  |
| PC4     | 192.168.20.60 |
| Laptop4 | 192.168.20.10 |

**Network:** `192.168.20.0/24`
**Gateway:** `192.168.20.1`

---

## ⚙️ Configuration

---

### 1️⃣ VLAN Creation (On Both Switches)

```bash id="8m0r7n"
vlan 10
name IT

vlan 20
name Accounts
```

---

### 2️⃣ Access Port Assignment

#### 🔹 VLAN 10

```bash id="6s3qqn"
interface range fa0/1 - 2
switchport mode access
switchport access vlan 10
```

#### 🔹 VLAN 20

```bash id="1jlwmz"
interface range fa0/3 - 4
switchport mode access
switchport access vlan 20
```

---

### 3️⃣ Trunk Configuration

#### Between Switches

```bash id="oqn4k8"
interface fa0/5
switchport mode trunk
```

#### Switch to Router

```bash id="1n3rxl"
interface fa0/6
switchport mode trunk
```

---

### 4️⃣ Router-on-a-Stick Configuration

```bash id="5sod5f"
interface fa0/0
no shutdown

interface fa0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0

interface fa0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
```

---

## 🧪 Testing & Results

### ✅ Successful Communication

* VLAN 10 devices successfully communicated with VLAN 20 devices
* Inter-VLAN routing worked correctly through the router

### ✅ VLAN Communication

* IT ↔ IT ✔
* Accounts ↔ Accounts ✔
* IT ↔ Accounts ✔

---

## 🧠 Key Learnings

* Router-on-a-Stick uses one physical router interface for multiple VLANs
* Trunk links carry traffic for multiple VLANs using 802.1Q tagging
* Subinterfaces act as gateways for VLANs
* Inter-VLAN communication requires Layer 3 routing

---

## ⚠️ Important Concepts

### 🔹 `encapsulation dot1Q`

Used to associate a subinterface with a VLAN.

Example:

```bash id="jj8mvw"
encapsulation dot1Q 10
```

---

### 🔹 Subinterfaces

Logical interfaces created under one physical router interface.

Example:

```bash id="0yjf5z"
fa0/0.10
fa0/0.20
```

---

## 🚀 Future Improvements

* Add DHCP configuration
* Implement ACLs between VLANs
* Configure VLAN security
* Perform packet analysis using Wireshark

---

## 🛠️ Tools Used

* Cisco Packet Tracer
* Cisco CLI

---





## 📌 Conclusion

This lab demonstrates how Router-on-a-Stick enables communication between VLANs using a single physical router interface and trunking. It provides a scalable and efficient alternative to legacy inter-VLAN routing methods.

---
