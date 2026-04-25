# 🔐 VLAN Segmentation & Trunking Lab (Multi-Switch Topology)

---

## 📌 Overview

This project demonstrates **VLAN configuration and trunking across multiple switches** using Cisco Packet Tracer.

The objective is to:

* Segment network into departments using VLANs
* Enable communication across switches using trunk ports
* Restrict communication between different VLANs

---

## 🏢 Network Scenario

A company network is divided into three departments:

* 🟦 **VLAN 10 → IT Department**
* 🟨 **VLAN 20 → HR Department**
* 🟩 **VLAN 30 → Sales Department**

The network uses **two switches connected via a trunk link** to allow VLAN traffic between them.

---

## 🧩 Topology Description

* 2 Cisco 2960 Switches
* 6 End Devices (PCs & Laptops)
* Trunk link between switches (Fa0/24 ↔ Fa0/24)
* Access ports assigned to different VLANs

---

## 🌐 IP Addressing Scheme

| Device               | VLAN    | IP Address   |
| -------------------- | ------- | ------------ |
| PC (IT - SW1)        | VLAN 10 | 192.168.10.2 |
| PC (HR - SW1)        | VLAN 20 | 192.168.20.2 |
| Laptop (Sales - SW1) | VLAN 30 | 192.168.30.6 |
| PC (IT - SW2)        | VLAN 10 | 192.168.10.3 |
| PC (Sales - SW2)     | VLAN 30 | 192.168.30.2 |
| Laptop (HR - SW2)    | VLAN 20 | 192.168.20.5 |

---

## ⚙️ Configuration

### 1️⃣ VLAN Creation (On Both Switches)

```bash id="9x6npa"
vlan 10
name IT

vlan 20
name HR

vlan 30
name SALES
```

---

### 2️⃣ Port Assignment

#### 🔹 Switch 1


interface fa0/1
switchport mode access
switchport access vlan 10

interface fa0/2
switchport mode access
switchport access vlan 20

interface fa0/3
switchport mode access
switchport access vlan 30
```

---

#### 🔹 Switch 2

interface fa0/1
switchport mode access
switchport access vlan 10

interface fa0/2
switchport mode access
switchport access vlan 30

interface fa0/3
switchport mode access
switchport access vlan 20
```

---

### 3️⃣ Trunk Configuration (Between Switches)


interface fa0/24
switchport mode trunk
switchport trunk allowed vlan 10,20,30
```

---

## 🧪 Testing & Results

### ✅ Successful Communication

* IT devices across switches (VLAN 10) → ✔ Working
* HR devices across switches (VLAN 20) → ✔ Working
* Sales devices across switches (VLAN 30) → ✔ Working

---

### ❌ Restricted Communication (Expected)

* VLAN 10 ✖ VLAN 20
* VLAN 10 ✖ VLAN 30
* VLAN 20 ✖ VLAN 30

👉 Inter-VLAN communication is not possible without a Layer 3 device.

---

## 🧠 Key Learnings

* VLANs provide logical segmentation at Layer 2
* Access ports belong to a single VLAN
* Trunk ports carry multiple VLANs between switches
* Same VLAN devices can communicate across switches
* Different VLANs are isolated by default

---


## 🛠️ Tools Used

* Cisco Packet Tracer
* Cisco CLI

---

---

## 📌 Conclusion

This lab demonstrates a real-world VLAN deployment across multiple switches, highlighting how network segmentation improves security and organization while maintaining scalability.

---
