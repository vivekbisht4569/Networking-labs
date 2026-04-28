# 🔐 Inter-VLAN Routing Lab (Legacy Method)

---

## 📌 Overview

This project demonstrates **Inter-VLAN Routing using the Legacy Method (multiple physical interfaces)** in Cisco Packet Tracer.

The goal was to enable communication between different VLANs by connecting each VLAN to a **dedicated router interface**.

---

## 🏢 Scenario

A company network is divided into multiple departments:

* 🟦 Engineering → VLAN 10
* 🟨 Accounts → VLAN 20
* 🟩 Sports → VLAN 30

Each department is placed in a separate VLAN, and a router is used to allow communication between them.

---

## 🧩 Topology Description

* 1 Router (Cisco 2811)
* 1 Switch (Cisco 2960)
* Multiple PCs/Laptops
* Separate physical connections between router and switch for each VLAN

---

## 🌐 IP Addressing

| VLAN | Department  | Network         | Gateway      |
| ---- | ----------- | --------------- | ------------ |
| 10   | Engineering | 192.168.10.0/24 | 192.168.10.1 |
| 20   | Accounts    | 192.168.20.0/24 | 192.168.20.1 |
| 30   | Support     | 192.168.30.0/24 | 192.168.30.1 |

---

## ⚙️ Configuration

### 1️⃣ VLAN Creation (Switch)

```bash
vlan 10
name Engineering

vlan 20
name Accounts

vlan 30
name Support
```

---

### 2️⃣ Port Assignment (Switch)

```bash
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

### 3️⃣ Router Connections (Important Concept)

Each VLAN is connected to the router using a **separate physical interface**.

---

### 4️⃣ Router Configuration

```bash
interface fa0/0
ip address 192.168.10.1 255.255.255.0
no shutdown

interface fa0/1
ip address 192.168.20.1 255.255.255.0
no shutdown

interface fa1/0
ip address 192.168.30.1 255.255.255.0
no shutdown
```

---

### 5️⃣ PC Configuration

Each device is configured with:

* IP Address
* Subnet Mask
* Default Gateway (router interface of its VLAN)

---

## 🧪 Testing & Results

### ✅ Successful Communication

* Devices from different VLANs can communicate

  * Example: VLAN 10 → VLAN 20 ✔
  * VLAN 20 → VLAN 30 ✔

---

## 🧠 Key Learnings

* Routers enable communication between VLANs (Layer 3)
* Each VLAN must have a gateway IP configured
* Legacy method uses **one interface per VLAN**
* Default gateway is critical for inter-network communication

---

## ⚠️ Limitations of Legacy Method

* Requires multiple router interfaces
* Not scalable for large networks
* Increases cabling complexity

---

## 🚀 Future Improvements

* Implement **Router-on-a-Stick (ROAS)**
* Reduce physical connections using trunking
* Add DHCP and routing protocols

---

## 🛠️ Tools Used

* Cisco Packet Tracer
* Cisco CLI

---

## 📸 Screenshots

*Add topology and ping results here*

---

## 🔗 GitHub Repository

(Add your repo link here)

---

## 📌 Conclusion

This lab demonstrates how inter-VLAN communication can be achieved using a router with multiple interfaces. It also highlights the limitations of this method and why modern networks prefer Router-on-a-Stick.

---
